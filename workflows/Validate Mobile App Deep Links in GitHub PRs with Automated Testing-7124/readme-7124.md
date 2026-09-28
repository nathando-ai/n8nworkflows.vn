---
title: "🚀 Kiểm tra tự động Deep Links trong PR GitHub với n8n"
description: "Tự động hóa kiểm tra Deep Links trong Pull Requests GitHub bằng n8n - Giảm thời gian kiểm tra thủ công, tăng chất lượng mã nguồn và tiết kiệm thời gian cho các nhà phát triển."
slug: "kiem-tra-tu-dong-deep-links-trong-pr-github-voi-n8n"
tags: [n8n, automation, no-code, devops, github]
keywords: [n8n workflow, tự động hóa, kiểm tra deep links, github pr, devops]
---

# 🚀 Kiểm tra tự động Deep Links trong PR GitHub với n8n

[Các sếp] có biết rằng mỗi lần kiểm tra thủ công các Deep Links trong Pull Requests GitHub đều tốn thời gian và dễ gây lỗi? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình kiểm tra này chỉ trong vài phút, giúp tăng chất lượng mã nguồn và tiết kiệm thời gian quý giá cho đội ngũ phát triển.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm thời gian kiểm tra thủ công từ vài giờ xuống còn vài phút.
- **Chính xác cao**: Kiểm tra toàn bộ Deep Links trong PR một cách tự động và chính xác.
- **Tăng chất lượng mã nguồn**: Phát hiện lỗi Deep Links sớm, giảm khả năng xảy ra lỗi trong sản phẩm cuối cùng.
- **Tích hợp dễ dàng**: Kết nối liền mạch với quy trình làm việc hiện tại của các sếp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản GitHub với quyền truy cập vào repository cần kiểm tra.
- API Key của GitHub (để tạo comment tự động).
- Script kiểm tra Deep Links (có thể sử dụng các công cụ như Fastlane hoặc DeepLinkChecker).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của các sếp, hãy làm theo các bước sau:

1. Truy cập vào n8n Editor của các sếp.
2. Nhấp vào nút "Import from URL" ở góc trên bên phải.
3. Dán link sau vào ô nhập liệu: `https://n8n.io/workflows/7124`
4. Nhấp vào nút "Import" để hoàn tất quá trình import.

Hoặc các sếp cũng có thể tải file JSON của workflow từ [đây](https://n8n.io/workflows/7124) và import thủ công vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần chú ý cấu hình các node sau:

- **GitHub PR Webhook**:
  - Đảm bảo rằng các sếp đã cấu hình webhook trong repository GitHub của mình để gửi yêu cầu đến endpoint `/validate-pr` với phương thức POST.
  - Các sếp có thể cấu hình webhook trong GitHub bằng cách truy cập vào `Settings > Webhooks > Add webhook`.

- **CONFIG - Variables**:
  - Cấu hình các biến môi trường cần thiết cho workflow, bao gồm:
    - `GITHUB_REPO_OWNER`: Tên chủ sở hữu của repository GitHub.
    - `GITHUB_REPO_NAME`: Tên của repository GitHub.
    - `VALIDATION_SCRIPT_PATH`: Đường dẫn đến script kiểm tra Deep Links.

- **Run Validation Script**:
  - Đảm bảo rằng các sếp đã cài đặt và cấu hình đúng script kiểm tra Deep Links trên máy chủ n8n.
  - Các sếp có thể sử dụng các công cụ như Fastlane hoặc DeepLinkChecker để kiểm tra Deep Links.

- **Format Markdown**:
  - Node này được sử dụng để định dạng kết quả kiểm tra thành định dạng Markdown để hiển thị trong comment GitHub.
  - Các sếp không cần thay đổi gì trong node này.

- **GitHub**:
  - Cấu hình credentials cho node GitHub để có thể tạo comment tự động trong PR.
  - Các sếp cần cung cấp API Key của GitHub để node này có thể hoạt động.

#### 3. Kích hoạt ⚡️
Sau khi các sếp đã cấu hình xong các node, hãy làm theo các bước sau để kích hoạt workflow:

1. Nhấp vào nút "Activate" ở góc trên bên phải của n8n Editor.
2. Kiểm tra lại các cấu hình và đảm bảo rằng tất cả các node đều hoạt động đúng.
3. Nhấp vào nút "Save" để lưu workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Các sếp có thể cấu hình workflow để gửi thông báo kết quả kiểm tra qua Slack hoặc Telegram.
- **Lưu log kiểm tra**: Các sếp có thể lưu log kiểm tra để theo dõi lịch sử kiểm tra và phát hiện lỗi.
- **Gửi báo cáo định kỳ**: Các sếp có thể cấu hình workflow để gửi báo cáo kiểm tra định kỳ qua email.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quá trình kiểm tra Deep Links trong Pull Requests GitHub, giảm thời gian kiểm tra thủ công và tăng chất lượng mã nguồn. Các sếp chỉ cần cấu hình một lần và workflow sẽ tự động hoạt động mỗi khi có PR mới. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của đội ngũ phát triển!