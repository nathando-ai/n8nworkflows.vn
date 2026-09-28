---
title: "🚀 Tự động quét và phát hiện các Workflow n8n bị ảnh hưởng bởi lỗi Migration 0.214.3"
description: "Hướng dẫn sử dụng workflow n8n tự động quét toàn bộ hệ thống để tìm ra các workflow và node bị lỗi kết nối do sự cố nâng cấp phiên bản 0.214.3."
slug: "tu-dong-quet-workflow-n8n-bi-anh-huong-migration-0-214-3"
tags: [n8n, automation, it-ops, migration, webhook, code-node]
keywords: [n8n migration 0.214.3, n8n workflow affected, tu dong hoa n8n, n8n api, it ops automation]
---

# 🚀 Tự động quét và phát hiện các Workflow n8n bị ảnh hưởng bởi lỗi Migration 0.214.3

Khi các sếp nâng cấp n8n lên phiên bản `0.214.3`, một lỗi không mong muốn đã xảy ra khiến một số workflow bị cấu hình lại sai đường đi kết nối (re-wired). Sự cố này chủ yếu ảnh hưởng đến các node có từ 2 đầu ra (output) trở lên như `If`, `Switch`, và `Compare Datasets`. Việc đi kiểm tra thủ công từng workflow trên hệ thống lớn thực sự là một cơn ác mộng.

Giải pháp là đây! Workflow tự động này sẽ thay các sếp quét toàn bộ hệ thống, lọc ra các workflow tiềm ẩn rủi ro và xuất ra một báo cáo HTML trực quan chỉ trong vài giây.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các hệ thống n8n lớn mượt mà, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Không cần click thủ công hàng trăm workflow để kiểm tra từng node kết nối.
- **Báo cáo trực quan:** Trả về một trang HTML rõ ràng, liệt kê chính xác tên workflow và các node bị ảnh hưởng.
- **Truy cập nhanh chóng:** Có sẵn đường dẫn trực tiếp để mở từng workflow cần kiểm tra trong tab mới.
- **Chủ động phòng ngừa:** Giúp hệ thống tự động hóa của doanh nghiệp không bị gián đoạn hay sai sót logic ngầm.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Quyền **Instance Owner** trên hệ thống n8n của các sếp.
- **n8n API Key** (có thể tạo tại mục *Settings > n8n API* trên giao diện n8n).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy mã JSON của workflow này, dán trực tiếp vào n8n Editor của mình hoặc import thông qua file JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống quét chính xác, các sếp cần cấu hình các node cốt lõi sau:

- **Node "Get all workflows" (`n8n`):** 
  - Cần cấu hình kết nối sử dụng thông tin `n8n API` (chọn credential loại `n8nApi`). Lấy API Key từ *Settings > n8n API* trên instance n8n của các sếp dán vào đây.
- **Node "Parse potentially affected workflows" (`code`):** 
  - Nếu hệ thống có cài đặt các **Community Nodes** (node cộng đồng) có từ 2 đầu ra trở lên, các sếp nhớ bổ sung tên các node đó vào biến hằng số `MULTI_OUTPUT_NODES` trong đoạn code của node này.
- **Node "Webhook" (`webhook`) & "Serve HTML Report" (`respondToWebhook`):** 
  - Đường dẫn webhook mặc định sẽ là `/webhooks/affected-workflows`. Các sếp có thể giữ nguyên để tiện truy cập.

#### 3. Kích hoạt ⚡️
- Sau khi cấu hình xong API Key, hãy bật trạng thái **Active** cho workflow này.
- Mở trình duyệt web và truy cập vào đường dẫn: `{YOUR_INSTANCE_URL}/webhooks/affected-workflows` (thay `{YOUR_INSTANCE_URL}` bằng domain n8n của các sếp).
- Báo cáo HTML sẽ hiển thị danh sách các workflow và các node cần kiểm tra. Click trực tiếp vào dòng tương ứng để mở workflow đó lên và fix lại kết nối nếu cần.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thay vì phải truy cập thủ công vào link webhook, các sếp có thể nối thêm node Telegram hoặc Slack ở cuối để hệ thống tự động đẩy báo cáo cảnh báo thẳng vào nhóm chat IT.
- **Lưu trữ lịch sử:** Kết nối thêm Google Sheets hoặc Notion để lưu lại danh sách các lần quét, giúp theo dõi tiến độ xử lý của đội ngũ kỹ thuật.

### 📌 Kết luận
Một sự cố nhỏ ở bản cập nhật cũ có thể âm thầm làm hỏng logic tự động hóa của doanh nghiệp. Hãy áp dụng ngay workflow này để quét sạch rủi ro, đảm bảo hệ thống n8n của các sếp luôn chạy mượt mà và chính xác 100%!