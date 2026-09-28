---
title: "🚀 Tự động lọc và chấm điểm job Upwork qua Gmail bằng AI OpenRouter gửi về Slack"
description: "Hướng dẫn xây dựng workflow n8n tự động bắt thông báo việc làm Upwork từ Gmail, phân tích bằng AI qua OpenRouter và bắn thông báo thông minh về Slack."
slug: "tu-dong-loc-cham-diem-upwork-job-gmail-slack-openrouter"
tags: [n8n, automation, upwork, ai, openrouter, slack, gmail]
keywords: [n8n workflow, tự động hóa upwork, lọc job upwork bằng ai, openrouter n8n, gmail to slack n8n]
---

# 🚀 Tự động lọc và chấm điểm job Upwork qua Gmail bằng AI OpenRouter gửi về Slack

Các sếp làm freelancer trên Upwork chắc chắn hiểu cảm giác mệt mỏi khi phải liên tục check email thông báo việc làm mới, đọc lướt qua hàng chục job mỗi ngày xem có phù hợp với kỹ năng hay không. Việc này cực kỳ tốn thời gian mà lại dễ bỏ lỡ các dự án ngon.

Giải pháp ở đây là gì? Hãy để tự động hóa lo! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ xịn sò được thiết kế bởi chuyên gia James Francis. Workflow này sẽ tự động tóm tắt email từ Upwork, dùng AI (qua OpenRouter) để chấm điểm mức độ phù hợp với hồ sơ của các sếp, và chỉ bắn thông báo về Slack khi gặp job thực sự chất lượng. 100% không cần code tay!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối**: Không cần phải đọc thủ công từng email thông báo job từ Upwork nữa.
- **Cá nhân hóa thông minh**: AI sẽ chấm điểm dựa trên kỹ năng thực tế của riêng các sếp (được cấu hình sẵn trong prompt).
- **Lọc nhiễu hiệu quả**: Chỉ nhận thông báo trên Slack với các job có điểm số phù hợp cao (ví dụ: từ 7/10 điểm trở lên).
- **Hoạt động 24/7**: Tự động quét email mỗi 10 phút, đảm bảo các sếp luôn là một trong những người ứng tuyển sớm nhất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Gmail** (Cần có đăng ký Upwork Freelancer Plus để nhận email job alerts).
- **Tài khoản OpenRouter** (Để sử dụng các mô hình LLM thông minh với chi phí tối ưu).
- **Workspace Slack** (Nơi nhận thông báo job được chọn lọc).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy file JSON của workflow hoặc tạo mới một workflow trống trong n8n Editor, sau đó dán toàn bộ cấu trúc 10 nodes vào. Danh sách các node bao gồm:
- `Get Filtered Messages` (Gmail Trigger)
- `Convert To Markdown` (Markdown)
- `Job Data Extractor` (Information Extractor)
- `OpenRouter Chat Model` (OpenRouter)
- `Opportunity Scorer` (Information Extractor)
- `OpenRouter Chat Model1` (OpenRouter)
- `Edit Fields` (Set)
- `Filter By Score` (Filter)
- `Send Slack Alert` (Slack)
- `Mark as Read` (Gmail)

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `Get Filtered Messages` (Gmail Trigger)**: 
  - Kết nối tài khoản Gmail của các sếp qua OAuth2.
  - *Lưu ý*: Mặc định workflow đang quét email mới mỗi 10 phút. Các sếp có thể điều chỉnh tần suất này tùy theo nhu cầu và giới hạn execution của n8n.
- **Nodes AI (`Job Data Extractor` & `Opportunity Scorer`)**:
  - Cấu hình credentials cho **OpenRouter Chat Model** và **OpenRouter Chat Model1**.
  - **CỰC KỲ QUAN TRỌNG**: Tại node `Opportunity Scorer`, hãy thay thế đoạn văn bản mẫu trong thẻ `<my_profile>` bằng chính hồ sơ freelancer, kỹ năng, kinh nghiệm của các sếp. Hồ sơ càng chi tiết, AI chấm điểm càng chuẩn xác!
- **Node `Filter By Score`**:
  - Mặc định workflow đang lọc các job có điểm match từ 7 trở lên (`Score >= 7`). Các sếp có thể thay đổi con số này tùy ý thích.
- **Node `Send Slack Alert`**:
  - Kết nối Slack Credentials và chọn đúng kênh (Channel) trong workspace của các sếp để nhận thông báo.
- **Node `Mark as Read`**:
  - Giúp tự động đánh dấu đã đọc email sau khi đã xử lý xong, giữ cho inbox luôn gọn gàng.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Node** hoặc **Test Workflow** để chạy thử với một vài email mẫu.
- Sau khi kiểm tra mọi thứ mượt mà, gạt công tắc sang **Active** để workflow chính thức tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo**: Ngoài Slack, các sếp có thể nhân bản node thông báo để bắn thêm tin nhắn về **Telegram Bot** cá nhân cho tiện check điện thoại mọi lúc mọi nơi.
- **Lưu trữ dữ liệu**: Thêm một node Google Sheets ở cuối luồng để lưu lại danh sách tất cả các job đã được AI chấm điểm, phục vụ cho việc thống kê xu hướng thị trường.
- **Tối ưu Prompt AI**: Thêm các tiêu chí loại trừ nghiêm ngặt vào prompt (ví dụ: loại bỏ các job có ngân sách quá thấp hoặc yêu cầu quá bất hợp lý).

### 📌 Kết luận
Với workflow n8n tích hợp AI OpenRouter này, việc săn việc trên Upwork của các sếp sẽ bước lên một tầm cao mới: nhanh hơn, chuẩn xác hơn và tốn ít công sức hơn. Hãy cài đặt ngay hôm nay để không bỏ lỡ bất kỳ cơ hội triệu đô nào nhé!