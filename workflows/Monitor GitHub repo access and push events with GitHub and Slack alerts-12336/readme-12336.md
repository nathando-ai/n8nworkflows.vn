---
title: "🚀 Giám sát quyền truy cập và sự kiện GitHub, cảnh báo bảo mật qua Slack tự động với n8n"
description: "Tự động quét các hoạt động rủi ro trên GitHub (Push, Member, Public events), đối chiếu whitelist và gửi cảnh báo tức thì qua Slack giúp bảo mật mã nguồn doanh nghiệp 24/7."
slug: "giam-sat-github-va-canh-bao-slack-tu-dong-voi-n8n"
tags: [n8n, automation, github, slack, security, secops]
keywords: [n8n workflow, gitHub security automation, giám sát github slack, bảo mật repository n8n, secops automation]
---

# 🚀 Giám sát quyền truy cập và sự kiện GitHub, cảnh báo bảo mật qua Slack tự động

Trong môi trường phát triển phần mềm hiện đại, việc kiểm soát ai có quyền đẩy code (push), thay đổi trạng thái repository (public/private) hoặc thêm thành viên mới là cực kỳ quan trọng đối với đội ngũ SecOps và quản lý. Việc kiểm tra thủ công bằng cơm rất dễ bỏ sót các hành vi trái phép hoặc thay đổi rủi ro.

Workflow n8n này sẽ giúp các sếp tự động hóa 100% việc giám sát các sự kiện nhạy cảm trên GitHub, đối chiếu danh sách nhân sự được phép (whitelist) và gửi cảnh báo ngay lập tức qua Slack khi phát hiện bất kỳ dấu hiệu bất thường nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảo mật thời gian thực:** Phát hiện ngay các hành vi đẩy code từ tài khoản lạ hoặc thay đổi quyền repo nguy hiểm.
- **Tự động đối chiếu Identity:** Sử dụng n8n Data Table để quản lý danh sách whitelist nhân sự và phân quyền (admin/developer) cực kỳ linh hoạt.
- **Cảnh báo tức thì:** Bắn message chi tiết kèm tên tài khoản, loại sự kiện và repo trực tiếp lên kênh Slack của team bảo mật.
- **Vận hành không gián đoạn:** Lịch trình tự động chạy ngầm liên tục mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **GitHub Account / Personal Access Token (PAT):** Để gọi API lấy thông tin sự kiện của repository.
- **Slack Bot Token:** Quyền gửi tin nhắn tự động vào các kênh Slack cảnh báo.
- **n8n Data Table:** Tạo sẵn bảng dữ liệu `it_whitelist` để lưu danh sách nhân sự.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này hoặc copy toàn bộ mã nguồn JSON dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành mượt mà, hãy chú ý cấu hình các node cốt lõi sau:

- **Schedule (Schedule Trigger):** Đặt lịch chạy định kỳ (ví dụ: mỗi 10 phút quét sự kiện một lần).
- **Github Events (HTTP) (HTTP Request Node):** 
  - Kết nối `githubApi` credentials (GitHub Personal Access Token).
  - Cấu hình gọi GitHub API để lấy các event gần nhất của tổ chức/repository.
- **Filter Member Events (Code Node):** Lọc các sự kiện quan trọng gồm `MemberEvent`, `PublicEvent` và `PushEvent`, bỏ qua các tín hiệu rác không cần thiết.
- **Check Whitelist (Data Table Node):** 
  - Chọn bảng dữ liệu `it_whitelist` (cần tạo sẵn với 2 cột: `github_username` và `role`).
  - *Mẹo:* Nhớ thêm username GitHub của chính các sếp với role là `admin` vào bảng này để tránh bị hệ thống tự cảnh báo nhầm (self-alerts). Thêm các developer khác với role tương ứng.
- **Switch Node:** Sử dụng biểu thức `{{ $item.json.type }}` ở chế độ *Rules* để phân luồng sự kiện tương ứng.
- **Các node IF (PublicEvent, PushEvent, MemberEvent):**
  - **PushEvent:** Kiểm tra nếu user không tồn tại trong whitelist (role trống hoặc thiếu) thì kích hoạt cảnh báo.
  - **Member & Public Events:** Kiểm tra nếu user thực hiện hành động nhưng role **không phải** là `admin` thì đánh dấu là trái phép.
- **Push Event Alert / Public Event Alert / Member Event Alert (Slack Nodes):**
  - Kết nối `slackApi` credentials.
  - Thiết lập gửi thông báo chi tiết bao gồm loại sự kiện, tên actor và thông tin repository khi luồng tín hiệu báo `True` (vi phạm bảo mật).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (Test step / Execute workflow) với dữ liệu mẫu để kiểm tra xem luồng lọc và bắn tin nhắn Slack hoạt động chuẩn xác chưa.
- Bật công tắc **Active** để workflow chính thức trực chiến 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin:** Kết hợp thêm node Telegram hoặc Microsoft Teams alongside Slack để đa kênh hóa cảnh báo bảo mật.
- **Ghi log vi phạm:** Lưu trữ toàn bộ các sự kiện vi phạm vào Google Sheets hoặc cơ sở dữ liệu nội bộ để phục vụ việc kiểm toán (audit log) hàng tháng.
- **Auto-remediation:** Thêm các bước tự động hóa phía sau (ví dụ: gọi API GitHub để tạm khóa quyền của user vi phạm nếu cần thiết).

### 📌 Kết luận
Workflow giám sát bảo mật GitHub kết hợp Slack này là một mảnh ghép SecOps không thể thiếu giúp các đội ngũ engineering chủ động phòng ngừa rủi ro rò rỉ mã nguồn hoặc lạm dụng quyền hạn. Hãy cài đặt ngay hôm nay để bảo vệ dự án của các sếp!