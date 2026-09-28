---
title: "🚀 Tự động tạo và đăng câu hỏi trắc nghiệm (MCQ Poll) lên Telegram bằng Gemini AI và Google Sheets"
description: "Hướng dẫn xây dựng hệ thống tự động hóa 100% với n8n: AI tự động sinh câu hỏi trắc nghiệm độc nhất không trùng lặp, lưu vào Google Sheets và đăng poll lên Telegram."
slug: "tu-dong-tao-va-dang-mcq-poll-telegram-gemini-ai-google-sheets"
tags: [n8n, automation, telegram-bot, google-sheets, google-gemini, ai-agent, content-creation]
keywords: [n8n workflow, tạo trắc nghiệm tự động, telegram poll bot, google gemini ai, google sheets automation]
---

# 🚀 Tự động tạo và đăng câu hỏi trắc nghiệm (MCQ Poll) lên Telegram bằng Gemini AI và Google Sheets

Các thầy cô, trung tâm luyện thi hay quản trị viên cộng đồng học tập thường xuyên phải đối mặt với việc "vắt óc" nghĩ câu hỏi trắc nghiệm hàng ngày, sau đó thủ công copy-paste lên kênh Telegram. Việc này cực kỳ tốn thời gian, dễ bị trùng lặp nội dung và ngắt quãng nếu bận rộn.

Workflow n8n này chính là "cứu cánh" tự động hóa toàn bộ quy trình: Sử dụng sức mạnh của **Google Gemini AI** để tự động sinh câu hỏi độc nhất (dựa trên lịch sử trong Google Sheets để chống trùng lặp), sau đó tự động xuất bản dạng **Telegram Poll** chuyên nghiệp mà các sếp không cần chạm tay vào máy tính!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Không cần tự soạn câu hỏi hay tạo poll thủ công trên Telegram mỗi ngày.
- **Nội dung độc nhất, không trùng lặp:** AI tự động đọc dữ liệu cũ trong Google Sheets để làm bộ nhớ (Memory) tránh lặp lại câu hỏi.
- **Tự động hóa 2 chiều linh hoạt:** Vừa có nhánh tự động sinh câu hỏi định kỳ, vừa có nhánh tự động quét và đẩy lên Telegram khi có dữ liệu mới.
- **Tương tác cao:** Đăng dạng Quiz Poll native của Telegram, giúp học viên dễ dàng tương tác và học tập ngay trên chat.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Sheets:** Một file Google Sheet chứa các cột: Question, Option A, Option B, Option C, Option D, Correct Answer, Explanation, Approval Status, Posted on Telegram.
- **Google Gemini API Key:** Tài khoản hoặc API key để kết nối với Google Gemini Chat Model.
- **Telegram Bot:** Token của Telegram Bot và Chat ID của kênh hoặc group Telegram cần đăng poll.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor, hoặc import file JSON thông qua menu *Add workflow -> Import from file*.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Google Gemini Chat Model & AI Agent:** Kết nối credentials của Google Gemini. Trong node `AI Agent`, hãy tùy chỉnh lại `systemMessage` để định hình chủ đề câu hỏi (ví dụ: Luyện thi lập trình, Tiếng Anh, Kiến thức chung...) và ngôn ngữ mong muốn (Anh, Việt...).
- **Google Sheets Nodes (`Read Quiz Data`, `Google Sheets Trigger`, `Update Quiz Status1`, v.v.):** Kết nối tài khoản Google của các sếp và trỏ đúng đường dẫn tới file Google Sheet quản lý câu hỏi trắc nghiệm.
- **Send Telegram Poll (HTTP Request):** Thay thế đoạn `<TELEGRAM_BOT_TOKEN>` bằng Token thực tế của bot và `<TELEGRAM_CHAT_ID>` bằng ID kênh/nhóm Telegram của các sếp.
- **Check New Quiz Added (If):** Kiểm tra logic điều kiện xem câu hỏi đã được duyệt và trạng thái `Posted on Telegram` đã là `✅` hay chưa trước khi gửi.

#### 3. Kích hoạt ⚡️
- Bấm **Test workflow** hoặc chạy thử từng node để kiểm tra kết nối Google Sheets và Telegram.
- Sau khi test thành công, bật nút **Active** ở góc trên bên phải màn hình để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kiểm duyệt qua Slack/Telegram:** Thêm bước gửi thông báo về một kênh riêng để admin bấm nút Duyệt (Approve) trước khi bot tự động đẩy lên kênh chính thức.
- **Lưu Log chi tiết:** Kết nối thêm node Google Sheets hoặc cơ sở dữ liệu để ghi lại số lượng học viên tương tác với từng poll nếu Telegram Bot hỗ trợ callback data.
- **Đa dạng hóa AI:** Dễ dàng thay thế Google Gemini bằng OpenAI GPT-4o nếu muốn đổi phong cách sinh câu hỏi.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ lợi hại cho các nhà sáng tạo nội dung giáo dục, quản trị viên cộng đồng muốn tối ưu hóa thời gian và gia tăng tương tác tự động. Hãy cài đặt ngay hôm nay để hệ thống tự động làm việc thay cho các sếp!