---
title: "🚀 Tự động tạo GitHub Bug Report từ Google Form bằng n8n & AI"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình tiếp nhận báo lỗi từ Google Form, sử dụng AI phân tích và tạo Issue trên GitHub, đồng thời thông báo qua Discord."
slug: "tu-dong-tao-github-bug-report-tu-google-form-n8n-ai"
tags: [n8n, automation, no-code, github, google-sheets, ai, lang-chain]
keywords: [n8n workflow, tự động hóa github, google form to github, ai bug report, n8n openai lang-chain]
---

# 🚀 Biến Google Form thành GitHub Bug Report chuyên nghiệp với n8n & AI

Trong các dự án phần mềm, việc khách hàng hoặc đội ngũ tester báo cáo lỗi (bug) qua Google Form rất phổ biến. Tuy nhiên, việc phải copy-paste thủ công từng nội dung lên GitHub Issues vừa tốn thời gian, vừa dễ bỏ sót thông tin, lại thiếu đi sự chuẩn hóa.

Giải pháp là đây! Workflow n8n này sẽ tự động hóa toàn bộ quy trình: Lắng nghe phản hồi từ Google Form, đồng bộ vào Google Sheets, sử dụng **AI Agent (OpenAI)** để phân tích, định dạng lại nội dung, sau đó tự động tạo Issue trên **GitHub** và gửi thông báo kèm đường dẫn về **Discord**. Tất cả diễn ra trong vòng vài giây mà không cần một dòng code thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian thủ công**: Không còn phải copy/paste nội dung từ form sang GitHub.
- **Báo cáo chuẩn hóa nhờ AI**: AI Agent tự động phân loại, tóm tắt và trình bày lỗi một cách khoa học, dễ đọc cho lập trình viên.
- **Đồng bộ dữ liệu minh bạch**: Mọi bug được lưu trữ gọn gàng trong Google Sheets kèm đường dẫn trực tiếp tới GitHub Issue.
- **Thông báo tức thì**: Đội ngũ kỹ thuật nhận được thông báo ngay lập tức trên Discord để xử lý kịp thời.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Account**: Đã tạo sẵn một Google Form liên kết với Google Sheets để hứng dữ liệu submit.
- **OpenAI API Key**: Dành cho AI Agent xử lý và cấu trúc hóa nội dung báo lỗi.
- **GitHub Personal Access Token (PAT)**: Có quyền tạo Issues trên Repository mục tiêu.
- **Discord Webhook URL**: Để gửi thông báo về kênh chat của team.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ n8n template (ID: 2938) và import trực tiếp vào giao diện n8n Editor của mình, hoặc tạo mới và thêm các node tương ứng.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 11 nodes phối hợp nhịp nhàng. Các sếp cần tập trung cấu hình kỹ các điểm cốt lõi sau:

- **Google Form Trigger / Add new Form submissions to Google Sheets**: 
  - Kết nối tài khoản Google của các sếp.
  - Chọn đúng file Google Sheets và Sheet Name được liên kết với form báo lỗi.
- **OpenAI Chat Model & Window Buffer Memory & Structured Output Parser**:
  - Nhập OpenAI API Key hợp lệ.
  - Cấu hình Model (khuyên dùng `gpt-4o-mini` hoặc `gpt-4o` để phân tích văn bản tốt nhất).
  - Đảm bảo `Structured Output Parser` được thiết lập đúng schema để ép AI trả về dữ liệu chuẩn JSON cho GitHub Issue (Tiêu đề, Mô tả, Nhãn/Labels...).
- **format message /output parsing (Agent)**:
  - Kiểm tra lại Prompt của Agent để đảm bảo AI hiểu đúng cách trích xuất thông tin từ form người dùng gửi.
- **If / Filter out already posted issues (NoOp)**:
  - Thiết lập điều kiện lọc để tránh việc một form submit bị xử lý trùng lặp.
- **Add issue to GitHub**:
  - Kết nối tài khoản GitHub (chọn OAuth2 hoặc GitHub API Token).
  - Chọn đúng `Owner` (Repository Owner) và `Repository` để tạo Issue mới.
  - Map các trường dữ liệu đã được AI xử lý vào phần Title và Body của Issue.
- **Add Github link to the sheet**:
  - Node Google Sheets này sẽ cập nhật ngược lại link của GitHub Issue vừa tạo vào dòng tương ứng trong Google Sheets.
- **Send notification to discord w link**:
  - Dùng node HTTP Request trỏ tới Discord Webhook URL để bắn thông báo đẹp mắt kèm link chi tiết issue.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử submit một form mẫu để kiểm tra toàn bộ luồng chạy.
- Nếu dữ liệu đổ về Google Sheets, GitHub tạo Issue thành công và Discord báo tin nhắn ting ting, các sếp hãy bật **Active** để workflow chính thức chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Ngoài Discord, các sếp có thể thay thế hoặc bổ sung node gửi tin nhắn qua Telegram, Slack hoặc Microsoft Teams tùy thuộc vào công cụ làm việc của team.
- **Gắn nhãn thông minh (Auto Labeling)**: Tận dụng AI để tự động đọc nội dung lỗi và gán nhãn (`bug`, `ui`, `backend`, `urgent`...) lên GitHub Issue dựa trên mức độ nghiêm trọng.
- **Lưu trữ Log lỗi**: Thêm nhánh xử lý lỗi (Error Trigger) để nếu API OpenAI hoặc GitHub gặp sự cố, hệ thống sẽ tự động gửi cảnh báo về một kênh riêng để dev kiểm tra.

### 📌 Kết luận
Việc tự động hóa quy trình báo lỗi phần mềm không chỉ giúp giảm tải công việc hành chính mà còn tăng tốc độ phản hồi của đội ngũ kỹ thuật. Hãy áp dụng ngay workflow này để tối ưu hóa năng suất cho team của các sếp nhé!