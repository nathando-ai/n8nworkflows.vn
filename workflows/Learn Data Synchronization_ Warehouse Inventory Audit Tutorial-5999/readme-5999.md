---
title: "🚀 Hướng dẫn đồng bộ dữ liệu kho hàng tự động trong n8n với Compare Datasets"
description: "Khám phá cách sử dụng node Compare Datasets mạnh mẽ trong n8n để tự động đối chiếu, phát hiện lệch dữ liệu và đồng bộ kho hàng giữa hệ thống nguồn và đích."
slug: "huong-dan-dong-bo-du-lieu-kho-hang-n8n-compare-datasets"
tags: [n8n, automation, data-synchronization, compare-datasets, inventory-management]
keywords: [n8n workflow, đồng bộ dữ liệu, compare datasets n8n, quản lý kho tự động, n8n tutorial]
keywords: [n8n workflow, đồng bộ dữ liệu, compare datasets n8n, quản lý kho tự động, n8n tutorial]
---

# 🚀 Hướng dẫn đồng bộ dữ liệu kho hàng tự động trong n8n với Compare Datasets

Các sếp có bao giờ đau đầu khi phải quản lý và đồng bộ dữ liệu thủ công giữa nhiều kho hàng hoặc hệ thống khác nhau chưa? Việc lệch số lượng tồn kho, sản phẩm thừa/thiếu giữa kho chính (Source of Truth) và kho phụ không chỉ gây mất thời gian kiểm tra mà còn ảnh hưởng trực tiếp đến doanh thu và uy tín doanh nghiệp.

Giải pháp là gì? Bài viết này sẽ hướng dẫn các sếp làm chủ một trong những node mạnh mẽ nhất của n8n: **Compare Datasets** (được thiết kế bởi chuyên gia Lucas Peyrin). Workflow mẫu này sẽ giúp các sếp hiểu rõ cách tự động hóa quy trình đối chiếu và đồng bộ dữ liệu kho hàng 100% không cần code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động đối chiếu thông minh:** So sánh dữ liệu giữa 2 kho hàng (hoặc 2 nguồn dữ liệu bất kỳ) bằng mã định danh độc nhất (`product_id`).
- **Phân loại tự động 4 trạng thái:** Tự động chia luồng dữ liệu thành: Giống nhau (All Good), Thiếu ở kho B (Add), Khác biệt số liệu (Update), và Thừa ở kho B (Remove).
- **Tiết kiệm 100% thời gian thủ công:** Không còn cảnh mở hai bảng Excel cạnh nhau để dò từng dòng sản phẩm.
- **Nền tảng mở rộng linh hoạt:** Dễ dàng thay thế các node giả lập (No-Op) bằng các thao tác thực tế như kết nối Google Sheets, Notion, Airtable hoặc Database.
:::

### 📦 Cấu trúc Workflow (10 Nodes)
Workflow này sử dụng các thành phần cốt lõi sau:
1. **Start Audit (`manualTrigger`):** Kích hoạt chạy thử nghiệm thủ công.
2. **Warehouse A & B (`set`):** Khởi tạo tập dữ liệu mẫu cho Kho chính (Source of Truth) và Kho phụ cần đồng bộ.
3. **Split Out Prducts (`splitOut`):** Tách mảng dữ liệu thành từng dòng riêng lẻ để xử lý.
4. **The Auditor (`compareDatasets`):** Node cốt lõi thực hiện so sánh hai tập dữ liệu dựa trên `product_id`.
5. **Các nhánh xử lý kết quả (`noOp`):** 
   - `✅ All Good (Do Nothing)`: Dữ liệu khớp nhau hoàn toàn.
   - `➕ Add to Warehouse B`: Sản phẩm có ở kho A nhưng thiếu ở kho B.
   - `🔄 Update in Warehouse B`: Sản phẩm có ở cả 2 kho nhưng lệch số lượng/thông tin.
   - `❌ Remove from Warehouse B`: Sản phẩm tồn tại ở kho B nhưng không có trong kho A.

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một tài khoản n8n (Cloud hoặc Self-hosted).
- Không cần API Key bên ngoài nào vì workflow này dùng dữ liệu mẫu (mock data) để hướng dẫn trực quan.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow này.
- Mở n8n Editor, tạo một workflow mới và chọn **Paste from Clipboard** để dán toàn bộ cấu trúc vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Khảo sát Node "The Auditor" (`compareDatasets`):** 
  - Xem cách node này cấu hình trường `product_id` làm khóa chính (barcode) để đối chiếu.
  - Thiết lập lấy phiên bản chuẩn từ Input A (`Warehouse A`) làm nguồn chân lý (Source of Truth).
- **Tùy biến nhánh xử lý:** Trong workflow mẫu, các node kết quả là `noOp` (No Operation - không làm gì cả). Khi áp dụng vào thực tế, các sếp hãy thay thế các node `noOp` này bằng các action thực tế (ví dụ: Google Sheets, Airtable, Database SQL, hoặc gửi thông báo qua Telegram/Slack).

#### 3. Kích hoạt ⚡️
- Nhấn nút **"Execute Workflow"** để chạy thử nghiệm.
- Click vào từng node kết quả (`noOp`) để quan sát cách n8n tự động phân loại các mặt hàng (như Webcam, Mouse, Monitor, Keyboard) vào đúng nhánh tương ứng.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối thông báo:** Thêm node Telegram hoặc Slack vào sau mỗi nhánh kết quả để nhận thông báo tức thì khi có sự chênh lệch tồn kho.
- **Tự động hóa định kỳ:** Thay thế node `manualTrigger` bằng `Schedule Trigger` để n8n tự động kiểm tra kho hàng mỗi ngày/mỗi tuần một lần.
- **Ứng dụng rộng rãi:** Ngoài kho hàng, logic này có thể áp dụng để đồng bộ danh sách khách hàng, phân quyền nhân sự, hoặc đối soát dữ liệu tài chính.

### 📌 Kết luận
Node **Compare Datasets** là một "vũ khí bí mật" giúp giải quyết bài toán đồng bộ dữ liệu cực kỳ tao nhã trong n8n. Hy vọng template này giúp các sếp nắm vững tư duy xử lý logic và tự tin áp dụng vào các dự án tự động hóa thực tế của doanh nghiệp!