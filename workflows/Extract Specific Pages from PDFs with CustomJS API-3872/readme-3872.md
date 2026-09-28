---
title: "🚀 Trích xuất trang PDF tùy chỉnh tự động trong n8n với CustomJS API"
description: "Hướng dẫn cách tách, trích xuất các trang cụ thể từ file PDF một cách tự động, nhanh chóng sử dụng CustomJS API và n8n workflow."
slug: "trich-xuat-trang-pdf-tu-dong-voi-customjs-api"
tags: [n8n, automation, no-code, pdf-processing, customjs, api]
keywords: [n8n workflow, trích xuất pdf, tách trang pdf tự động, customjs api, n8n pdf toolkit]
---

# 🚀 Trích xuất trang PDF tùy chỉnh tự động trong n8n với CustomJS API

Các sếp có bao giờ gặp cảnh phải "vật lộn" với những file PDF dày cộp hàng trăm trang, chỉ để lấy ra vài trang nội dung quan trọng gửi cho khách hàng hoặc sếp lớn chưa? Việc copy/paste thủ công hay dùng các phần mềm cắt ghép rời rạc không chỉ tốn thời gian mà còn dễ sai sót, bực mình.

Đừng lo, bài toán này sẽ được giải quyết gọn gàng trong một nốt nhạc với workflow n8n sử dụng **CustomJS API**. Tự động hóa 100%, không cần viết code phức tạp, chỉ cần vài cú click là xong!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Bỏ qua thao tác thủ công mở file PDF, dò trang rồi cắt ghép.
- **Chính xác tuyệt đối:** Chỉ định chính xác trang cần lấy (ví dụ: trang 5, trang 10-15) mà không sợ nhầm lẫn.
- **Tích hợp linh hoạt:** Dễ dàng kết hợp kết quả trả về với email, Google Drive, Telegram hay Slack.
- **Hoạt động 24/7:** Xử lý tài liệu mọi lúc mọi nơi ngay trên hạ tầng n8n của các sếp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản và API Key từ **CustomJS API** (để sử dụng node `@custom-js/n8n-nodes-pdf-toolkit.ExtractPages`).
- File PDF nguồn cần xử lý (có thể lấy từ URL hoặc tải lên qua HTTP Request).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã nguồn JSON của workflow này và dán trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 3 nodes cốt lõi, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **When clicking ‘Test workflow’ (Node Trigger):** 
  - Dùng để chạy thử nghiệm thủ công. Sau khi hoàn thiện, các sếp có thể thay thế bằng *Webhook Trigger*, *Schedule* (định kỳ) hoặc *Google Drive Trigger* tùy theo nhu cầu thực tế.
- **HTTP Request (Node tải file PDF):** 
  - Cấu hình URL dẫn đến file PDF gốc mà các sếp muốn xử lý, hoặc nhận dữ liệu nhị phân (binary) từ bước trước chuyển sang.
- **Extract Pages From PDF1 (Node xử lý PDF):** 
  - Node này sử dụng custom community package `@custom-js/n8n-nodes-pdf-toolkit.ExtractPages`.
  - **Credentials:** Các sếp bắt buộc phải thiết lập `customJsApi` credentials bằng cách nhập API Key được cung cấp từ nền tảng CustomJS.
  - **Parameters:** Cấu hình số trang cần trích xuất (ví dụ: `1,3,5-8`) theo đúng cú pháp hướng dẫn của node.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** để kiểm tra xem file PDF mới được trích xuất có đúng ý các sếp chưa.
- Nếu mọi thứ mượt mà, hãy bật nút **Active** ở góc trên bên phải để workflow chính thức đi vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Lưu trữ:** Thêm node *Google Drive* hoặc *OneDrive* ngay sau bước trích xuất để tự động lưu file PDF mới vào thư mục chỉ định.
- **Thông báo kết quả:** Kết nối thêm node *Telegram* hoặc *Slack* để nhận thông báo kèm file PDF vừa cắt xong ngay trên điện thoại.
- **Xử lý hàng loạt:** Kết hợp vòng lặp (Loop/Split In Batches) nếu các sếp cần xử lý danh sách hàng chục file PDF cùng một lúc.

### 📌 Kết luận
Với workflow **Extract Specific Pages from PDFs with CustomJS API**, việc xử lý tài liệu PDF nặng nhọc giờ đây chỉ là chuyện nhỏ. Hãy cài đặt ngay để tối ưu hóa thời gian làm việc và nâng tầm hiệu suất tự động hóa cho doanh nghiệp của các sếp!