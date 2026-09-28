---
title: "🚀 Tự động hóa tạo Proposal Upwork cực đỉnh với GPT-4o-mini, Airtable và Slack"
description: "Hướng dẫn xây dựng workflow n8n tự động quét việc làm Upwork qua RSS, lọc kỹ năng thông minh, viết thư chào hàng bằng AI và gửi thông báo trực tiếp qua Slack."
slug: "tu-dong-hoa-tao-proposal-upwork-gpt-4o-mini-airtable-slack"
tags: [n8n, automation, upwork, ai, openai, airtable, slack]
keywords: [n8n workflow, tự động hóa upwork, viết proposal bằng ai, gpt-4o-mini, airtable slack automation]
---

# 🚀 Tự động hóa tạo Proposal Upwork cực đỉnh với GPT-4o-mini, Airtable và Slack

Các sếp làm Freelance trên Upwork chắc chắn hiểu cảm giác mệt mỏi khi phải liên tục F5 tìm job mới, lọc các job rác, và ngồi viết từng chiếc proposal (thư chào hàng) dài dòng nhưng chưa chắc khách đã đọc. Việc này ngốn vô số thời gian quý báu mà lẽ ra các sếp nên dành để làm chuyên môn hoặc nghỉ ngơi.

Đừng lo, bài toán đó sẽ được giải quyết triệt để với workflow n8n tự động hóa 100% này! Workflow sẽ thay các sếp "săn" job, kiểm tra độ phù hợp, để AI viết sẵn một bản proposal cực chuẩn, lưu lại vào cơ sở dữ liệu Airtable và bắn thẳng thông báo về Slack để các sếp chỉ việc "copy & paste" đi ứng tuyển.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần canh me Upwork hay vắt óc nghĩ câu mở đầu cho proposal nữa.
- **Cá nhân hóa thông minh:** GPT-4o-mini tự động đọc mô tả công việc và viết thư chào hàng 150–250 từ cực kỳ sát thực tế.
- **Lọc kỹ lưỡng:** Chỉ nhận job khớp với từ 2 kỹ năng trở lên và loại bỏ khách hàng đánh giá thấp.
- **Hoạt động 24/7:** Quét job mỗi phút qua RSS, tự động đồng bộ dữ liệu vào Airtable và thông báo ngay lập tức qua Slack.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Vollna** (vollna.com) để tạo RSS feed theo dõi job Upwork.
- **OpenAI API Key** (kết nối với model GPT-4o-mini).
- **Tài khoản Airtable** với một Base/Table chứa cấu trúc lưu trữ job và proposal.
- **Slack Workspace** và một Slack App được cấp quyền `chat:write` để nhận thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã nguồn JSON của workflow này và dán trực tiếp vào giao diện n8n Editor của mình, hoặc import file JSON đã tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các node quan trọng sau:
- **Node `RSS Feed - n8n & Automation` (rssFeedReadTrigger):** Dán URL RSS feed từ trang Vollna của các sếp vào đây để bắt đầu nhận dữ liệu job theo phút.
- **Các Node Code (`Filter: Skills Match`, `Filter: Client Rating`, `Build OpenAI Payload`):** 
  - Cập nhật danh sách kỹ năng của các sếp (`YOUR_SKILLS`) trong node lọc kỹ năng.
  - Điền thông tin profile/kinh nghiệm thực tế của các sếp (`MY PROFILE`) trong node Build OpenAI Payload để AI hiểu rõ bối cảnh và viết proposal chuẩn xác nhất.
- **Node `AI: Generate Proposal` (openAi):** Chọn credentials OpenAI API của các sếp và thiết lập model là `gpt-4o-mini`.
- **Node `Airtable: Check Duplicate` & `Airtable: Save Proposal` (airtable):** Kết nối Airtable API Token, sau đó trỏ đến đúng Base ID và Table ID đã chuẩn bị sẵn.
- **Node `Slack Notification` (slack):** Kết nối credentials Slack và chọn kênh (Channel) mà các sếp muốn nhận thông báo job mới.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (`Test workflow`) với một vài dữ liệu mẫu để kiểm tra luồng chạy từ đầu đến cuối.
- Kiểm tra lại kết quả trên Airtable và Slack.
- Bật công tắc **Active** để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram:** Nếu các sếp không dùng Slack, có thể thay thế node Slack bằng node Telegram để nhận thông báo proposal trực tiếp qua điện thoại cá nhân siêu tiện lợi.
- **Thêm bước tự động apply:** Nếu tự tin, các sếp có thể kết hợp thêm Puppeteer hoặc API tự động gửi proposal trực tiếp lên Upwork (cần lưu ý chính sách của nền tảng).
- **Báo cáo định kỳ:** Tạo thêm một nhánh chạy hàng tuần tổng hợp số lượng job đã nhận và proposal đã gửi qua Google Sheets.

### 📌 Kết luận
Một quy trình tự động hóa hoàn hảo giúp các sếp tối ưu hóa công việc tìm kiếm khách hàng trên Upwork. Hãy setup ngay hôm nay để biến AI thành "trợ lý cứng" đắc lực trong hành trình làm freelancer của mình nhé các sếp!