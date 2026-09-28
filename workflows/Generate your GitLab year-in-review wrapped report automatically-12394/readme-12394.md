---
title: "🚀 Tự động tạo báo cáo GitLab Year-in-Review (GitLab Wrapped) cực đỉnh với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình tạo báo cáo tổng kết năm GitLab Wrapped cá nhân hóa, từ kiểm tra bảo mật PAT đến kích hoạt pipeline CI/CD."
slug: "tu-dong-tao-bao-cao-gitlab-wrapped-voi-n8n"
tags: [n8n, automation, gitlab, devops, ci-cd, no-code]
keywords: [n8n workflow, gitlab wrapped, tự động hóa gitlab, gitlab year in review, CI/CD pipeline automation]
---

# 🚀 Tự động tạo báo cáo GitLab Year-in-Review (GitLab Wrapped) cực đỉnh với n8n

Các sếp là lập trình viên hoặc DevOps Engineer chắc hẳn rất quen thuộc với những báo cáo tổng kết năm đầy cảm xúc (Year-in-Review) trên GitHub hay Spotify. Nhưng còn GitLab thì sao? Việc tổng hợp thủ công các đóng góp, commit, merge request trong cả một năm trời thực sự là một "nỗi đau" tốn rất nhiều thời gian và công sức.

Đừng lo, giải pháp đã ở đây! Với template n8n tuyệt vời này, các sếp có thể tự động hóa toàn bộ quy trình tạo báo cáo **GitLab Wrapped** cá nhân hóa chỉ thông qua một biểu mẫu (form) đơn giản. Workflow sẽ tự động xác thực bảo mật, fork dự án, cấu hình biến môi trường CI/CD và kích hoạt pipeline để trả về cho các sếp một trang báo cáo lung linh.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần thao tác thủ công phức tạp trên giao diện GitLab.
- **Bảo mật tuyệt đối:** Có sẵn lớp kiểm tra Personal Access Token (PAT) để tránh rò rỉ các dự án riêng tư.
- **Cá nhân hóa cao:** Tự động tạo báo cáo tổng kết chính xác theo tên người dùng và năm được chỉ định.
- **Trải nghiệm mượt mà:** Sử dụng Form Trigger để nhập thông tin và theo dõi tiến trình pipeline hoàn toàn tự động.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản GitLab cá nhân hoặc doanh nghiệp.
- **GitLab Personal Access Token (PAT)** với các quyền (scopes): `api`, `read_repository`, và `write_repository`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy toàn bộ mã JSON của workflow và paste trực tiếp vào n8n Editor của mình, hoặc import thông qua file JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 17 nodes được chia thành các phân đoạn logic rõ ràng. Các sếp cần chú ý cấu hình các điểm sau:

- **GitLab Wrapped Form (`formTrigger`):** Biểu mẫu đầu vào để thu thập thông tin từ người dùng bao gồm:
  - Tên người dùng GitLab (Username)
  - GitLab PAT Token
  - GitLab Instance URL (mặc định là `https://gitlab.com`)
  - Năm cần tạo báo cáo (Year)
- **Workflow Configuration (`set`):** Nơi thiết lập các biến cấu hình chung cho toàn bộ luồng chạy.
- **Security Validation (`Validate PAT Owner`, `Is PAT Owner invalid?`, `No Operation...`):** Node này đảm bảo token PAT không trùng khớp với username nhập vào, ngăn chặn rủi ro lộ dữ liệu từ các dự án private. Các sếp giữ nguyên logic này để đảm bảo an toàn.
- **Fork Setup (`Search Existing Fork`, `Try to fork`, `set ProjectId`, `Merge`):** Tự động tìm kiếm hoặc tạo bản fork của dự án gốc (`gitlab-wrapped`) trên tài khoản GitLab của người dùng.
- **CI/CD Configuration (`Set token env var`, `Set Username env var`, `Set Year env var`):** Tự động đẩy các biến môi trường cấu hình vào dự án fork.
- **Pipeline Execution (`Trigger Pipeline`, `Wait for CI/CD`, `Check Pipeline Status`, `Pipeline Complete?`):** Kích hoạt pipeline và tự động kiểm tra trạng thái định kỳ (poll mỗi 2 phút) cho đến khi hoàn thành.
- **Kết quả cuối cùng:** Sau khi hoàn tất, báo cáo sẽ sẵn sàng tại đường dẫn:
  `https://YOUR-USERNAME.gitlab.io/gitlab-wrapped` (Thay `YOUR-USERNAME` bằng username GitLab của các sếp).

#### 3. Kích hoạt ⚡️
- Test thử nghiệm (Test run) với dữ liệu mẫu thông qua form trigger.
- Kiểm tra log trên n8n để đảm bảo pipeline chạy thành công.
- Bật công tắc **Active** để chính thức đưa workflow vào vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack ở cuối workflow để bắn tin nhắn thông báo kèm link kết quả ngay khi pipeline chạy xong.
- **Lưu lịch sử:** Kết nối thêm Google Sheets hoặc Airtable để lưu lại danh sách những ai đã tạo báo cáo trong hệ thống.
- **Xử lý lỗi:** Bổ sung nhánh Error Trigger để gửi cảnh báo nếu pipeline GitLab gặp lỗi trong quá trình build.

### 📌 Kết luận
Việc tổng kết năm trong công việc lập trình chưa bao giờ thú vị và tự động hóa đến thế. Hãy "lên đồ" ngay template n8n này để khoe thành tích code của các sếp với đồng nghiệp nhé! Chúc các sếp thao tác thành công!