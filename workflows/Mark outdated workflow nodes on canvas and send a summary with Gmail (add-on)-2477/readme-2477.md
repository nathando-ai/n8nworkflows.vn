---
title: "🚀 Tự động đánh dấu Node cũ trên Canvas n8n và gửi báo cáo qua Gmail"
description: "Hướng dẫn tự động hóa quét, gắn thẻ cảnh báo node lỗi thời trên canvas n8n và tổng hợp báo cáo chi tiết gửi thẳng vào Gmail của bạn."
slug: "tu-dong-danh-dau-node-cu-va-gui-gmail"
tags: [n8n, automation, no-code, workflow-optimization, gmail, n8n-api]
keywords: [n8n workflow, tự động hóa n8n, update n8n nodes, gmail automation, n8n api]
---

# 🚀 Tự động đánh dấu Node cũ trên Canvas n8n và gửi báo cáo qua Gmail

Các sếp đang vận hành hệ thống n8n với hàng chục, hàng trăm workflow chắc chắn sẽ gặp tình trạng "đau đầu" khi các node cũ (outdated nodes) bị bỏ quên, dẫn đến lỗi bất ngờ hoặc không tận dụng được các tính năng tối ưu mới nhất. Việc kiểm tra thủ công từng workflow là "nhiệm vụ bất khả thi". 

Giải pháp là đây! Workflow tự động hóa này sẽ giúp các sếp quét, tự động đánh dấu các node cũ trực tiếp trên giao diện Canvas (thêm icon nhận diện hoặc sắp xếp phiên bản mới ở gần đó) và gửi ngay một bản tổng hợp (summary) báo cáo chi tiết qua **Gmail**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần mất công check thủ công từng workflow xem có node nào cũ hay không.
- **Trực quan hóa Canvas:** Tự động gắn icon hoặc chuẩn bị sẵn node phiên bản mới ngay cạnh node cũ trên canvas để nâng cấp cực nhanh.
- **Báo cáo tức thì:** Nhận email tổng hợp danh sách các workflow và node cần cập nhật gửi thẳng vào Gmail cá nhân/doanh nghiệp.
- **Duy trì hiệu suất hệ thống:** Giúp hệ thống n8n luôn chạy trên các phiên bản node mới nhất, hạn chế tối đa lỗi xung đột.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Hệ thống n8n (Self-hosted hoặc Cloud có quyền truy cập API).
- **n8n API Credentials:** Để kết nối node n8n lấy và cập nhật thông tin workflow.
- **Gmail OAuth2 Credentials:** Để gửi email tổng hợp báo cáo.
- **Workflow tiền đề:** Workflow này hoạt động như một "Add-on" nhận dữ liệu từ [Workflow kiểm tra node cũ gốc](https://n8n.io/workflows/2301-check-if-workflows-contain-build-in-nodes-that-are-not-of-the-latest-version/).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ kho lưu trữ.
- Tại giao diện n8n Editor, chọn **Add workflow** -> **Import from File** và chọn file JSON vừa tải.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:
- **Node `Settings` & `Get Workflow` / `Update Workflow` (n8n node):** 
  - Cần cấu hình `n8nApi` credentials.
  - Cập nhật thông số `instanceBaseUrl` thành đường dẫn URL thực tế của instance n8n mà các sếp đang sử dụng (để tạo link direct dẫn thẳng tới workflow cần sửa trong email).
- **Node `Modify Workflow (if required)` (Code node):** 
  - Xử lý logic tự động thêm icon cảnh báo hoặc sắp xếp node mới lên canvas tùy chỉnh theo nhu cầu.
- **Node `Send Summary` (Gmail node):** 
  - Chọn tài khoản qua `gmailOAuth2`.
  - Thay đổi địa chỉ email người nhận (Recipient) thành email của sếp hoặc đội ngũ kỹ thuật.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test run) bằng cách cấp dữ liệu mẫu (mock data) từ workflow kiểm tra phiên bản node.
- Khi mọi thứ trả về kết quả màu xanh mượt mà, bật nút **Active** để hệ thống tự động hoạt động ngầm.

### ✍️ Nâng cấp & Gợi ý mở rộng
- **Tích hợp kênh chat:** Thay vì chỉ gửi Gmail, các sếp có thể nhân bản nhánh cuối để bắn thông báo trực tiếp vào **Telegram Bot** hoặc kênh **Slack** của đội ngũ dev.
- **Lưu log vào Google Sheets:** Lưu trữ lịch sử các lần quét phiên bản node để theo dõi tiến độ cập nhật của team theo tuần/tháng.
- **Lên lịch định kỳ (Cron):** Kết hợp với Schedule Trigger để chạy quét tự động mỗi tuần 1 lần vào sáng thứ Hai đầu tuần.

### 📌 Kết luận
Một hệ thống n8n khỏe mạnh bắt nguồn từ những chi tiết nhỏ nhất như các node luôn được cập nhật bản mới. Hãy "lên đồ" ngay workflow này để tiết kiệm hàng giờ kiểm tra thủ công cho đội ngũ kỹ thuật nhé các sếp!