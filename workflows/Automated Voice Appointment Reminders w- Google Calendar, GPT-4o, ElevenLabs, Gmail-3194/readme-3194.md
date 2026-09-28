---
title: "🚀 Tự Động Gửi Nhắc Lịch Hẹn Bằng Giọng Nói AI (GPT-4o + ElevenLabs)"
description: "Workflow n8n tự động quét Google Calendar, dùng GPT-4o viết nội dung, ElevenLabs chuyển thành giọng nói và gửi qua Gmail. Giải pháp hoàn hảo để giảm tỷ lệ khách hàng quên lịch hẹn."
slug: "tu-dong-gui-nhac-lich-hen-giong-noi-ai"
tags: [n8n, automation, ai, google-calendar, elevenlabs, gmail]
keywords: [n8n workflow, tự động hóa lịch hẹn, giọng nói AI, google calendar automation, giảm no-show]
---

# 🚀 Tự Động Gửi Nhắc Lịch Hẹn Bằng Giọng Nói AI (GPT-4o + ElevenLabs)

Bạn có bao giờ cảm thấy bực bội khi khách hàng liên tục quên lịch hẹn, gây lãng phí thời gian và doanh thu cho đội ngũ của bạn? Việc gọi điện nhắc nhở thủ công tốn kém nhân sự, trong khi gửi email văn bản thường bị bỏ qua hoặc không tạo được sự chú ý cần thiết.

Workflow này là giải pháp "chốt hạ" hoàn hảo: Nó tự động quét **Google Calendar** để tìm các cuộc hẹn sắp tới, sử dụng **GPT-4o** để soạn một thông điệp nhắc nhở thân thiện và chuyên nghiệp, sau đó dùng **ElevenLabs** để chuyển văn bản đó thành **giọng nói tự nhiên như con người**. Cuối cùng, file âm thanh được đính kèm và gửi qua **Gmail** đến khách hàng. Kết quả? Tỷ lệ khách hàng nhớ lịch hẹn tăng vọt, trải nghiệm dịch vụ trở nên đẳng cấp và cá nhân hóa hơn bao giờ hết.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Giảm thiểu No-show:** Giọng nói AI tạo sự chú ý cao hơn email văn bản thông thường, giúp khách hàng không bỏ lỡ lịch hẹn.
- **Tiết kiệm 100% thời gian nhân sự:** Không cần ai phải gọi điện hay soạn email nhắc nhở, hệ thống tự động chạy theo lịch trình.
- **Trải nghiệm khách hàng đẳng cấp:** Khách hàng nhận được lời nhắc bằng giọng nói tự nhiên, tạo cảm giác được chăm sóc đặc biệt.
- **Cá nhân hóa thông minh:** GPT-4o tự động điều chỉnh nội dung dựa trên chi tiết cuộc hẹn (tên khách, loại dịch vụ, thời gian).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị các tài khoản và credentials sau:
1. **Tài khoản n8n:** Đã cài đặt và chạy (Cloud hoặc Self-hosted).
2. **Google Account:**
   - Quyền truy cập **Google Calendar API** (để đọc lịch hẹn).
   - Quyền truy cập **Gmail API** (để gửi email kèm file đính kèm).
3. **OpenAI API Key:** Sử dụng model `gpt-4o-mini` (hoặc `gpt-4o`) để soạn nội dung.
4. **ElevenLabs API Key:** Để chuyển văn bản thành giọng nói (TTS).
5. **Dữ liệu lịch:** Đảm bảo Google Calendar của bạn đã có các sự kiện (appointments) với thông tin đầy đủ (tên khách, email khách, mô tả dịch vụ).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** và dán link: `https://n8n.io/workflows/3194` HOẶC copy JSON từ file workflow và dán vào n8n.
3. Sau khi import, các sếp sẽ thấy 9 nodes chính được kết nối sẵn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần click vào từng node và cấu hình credentials cũng như tham số:

*   **Node: `Schedule Trigger`**
    *   Đây là bộ đếm thời gian. Mặc định có thể là chạy mỗi giờ hoặc mỗi ngày. Các sếp nên chỉnh về thời điểm phù hợp (ví dụ: 8:00 sáng hàng ngày) để quét lịch và gửi nhắc nhở trước khi cuộc hẹn diễn ra.

*   **Node: `Get Appointments` (Google Calendar)**
    *   **Credentials:** Chọn hoặc tạo mới Google Calendar OAuth2.
    *   **Calendar ID:** Chọn đúng lịch chứa các cuộc hẹn của khách hàng.
    *   **Time Range:** Đảm bảo tham số thời gian được thiết lập để chỉ lấy các sự kiện trong tương lai gần (ví dụ: từ bây giờ đến 24-48 giờ tới) để tránh gửi nhắc nhở cho các cuộc hẹn đã qua hoặc quá xa.

*   **Node: `create message` (Chain LLM)**
    *   **Model:** Node `OpenAI Chat Model` đã được cấu hình sẵn model `gpt-4o-mini`. Các sếp cần đảm bảo đã gắn **OpenAI API Key** vào credentials của node này.
    *   **Prompt:** Kiểm tra prompt trong node `create message`. Prompt này hướng dẫn GPT viết một lời nhắc nhở ngắn gọn, thân thiện, bao gồm tên khách hàng, thời gian và địa điểm/dịch vụ. Các sếp có thể tùy chỉnh giọng văn (formal/informal) tại đây.
    *   **Structured Output Parser:** Node này đảm bảo output của GPT là một object JSON có cấu trúc (ví dụ: `{ "text": "Nội dung nhắc nhở" }`), giúp các bước sau xử lý dễ dàng.

*   **Node: `Generate Voice Reminder` (HTTP Request)**
    *   Đây là node gọi API của **ElevenLabs**.
    *   **Headers:** Các sếp cần điền **ElevenLabs API Key** vào phần Header (thường là `xi-api-key`).
    *   **Body:** Kiểm tra phần Body JSON. Nó sẽ lấy `text` từ bước GPT và gửi lên ElevenLabs.
    *   **Voice ID:** Các sếp có thể thay đổi `voice_id` trong body để chọn giọng đọc khác (nữ/male, tiếng Việt/Anh). *Lưu ý: ElevenLabs hỗ trợ tiếng Việt rất tốt, hãy chọn một voice phù hợp với ngôn ngữ của prompt GPT.*

*   **Node: `Change filename` (Code Node)**
    *   Node này xử lý dữ liệu trả về từ ElevenLabs (thường là base64 hoặc binary) và đặt tên file âm thanh (ví dụ: `reminder_[ten_khach].mp3`). Các sếp không cần chỉnh gì nhiều trừ khi muốn đổi định dạng tên file.

*   **Node: `Send Voice Reminder` (Gmail)**
    *   **Credentials:** Chọn hoặc tạo mới **Gmail OAuth2**.
    *   **To:** Điền email của khách hàng (lấy từ dữ liệu Google Calendar).
    *   **Subject:** Tiêu đề email (ví dụ: "Nhắc nhở lịch hẹn của bạn").
    *   **Attachments:** Đảm bảo node này được cấu hình để đính kèm file âm thanh từ node `Change filename`.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   *   Click vào node `When clicking 'Test workflow'` (Manual Trigger) để chạy thử.
   *   Kiểm tra xem GPT có tạo ra nội dung đúng không.
   *   Kiểm tra xem ElevenLabs có trả về file âm thanh không.
   *   Kiểm tra xem Gmail có gửi email thành công không (các sếp nên dùng email của chính mình làm test case đầu tiên).
2. **Bật Active:**
   *   Sau khi test thành công, click nút **Active** ở góc trên bên phải để workflow bắt đầu chạy tự động theo lịch trình `Schedule Trigger`.

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy chỉnh giọng đọc:** Thay vì dùng giọng mặc định, các sếp có thể clone giọng nói của chính mình hoặc giọng nói thương hiệu trên ElevenLabs để tạo sự nhận diện thương hiệu mạnh mẽ.
- **Gửi đa kênh:** Thay vì chỉ gửi Gmail, các sếp có thể thêm node **Telegram** hoặc **WhatsApp** (qua Twilio) để gửi file âm thanh trực tiếp vào chat, tăng tỷ lệ mở tin nhắn.
- **Lọc sự kiện:** Trong node `Get Appointments`, các sếp có thể thêm điều kiện lọc để chỉ gửi nhắc nhở cho các loại dịch vụ cao cấp hoặc khách hàng VIP.
- **Theo dõi phản hồi:** Thêm một webhook hoặc nút "Xác nhận" trong email để khách hàng click xác nhận đã nhận lịch hẹn, giúp đo lường hiệu quả chiến dịch.

### 📌 Kết luận
Việc tự động hóa nhắc lịch hẹn bằng giọng nói AI không chỉ là một tính năng "xịn xò" mà còn là công cụ tăng trưởng doanh thu thực sự. Bằng cách kết hợp sức mạnh của GPT-4o và ElevenLabs, các sếp có thể biến những cuộc hẹn bị bỏ quên thành những cơ hội kinh doanh đã được bảo vệ. Hãy import workflow này, cấu hình credentials và để AI làm việc thay cho bạn ngay hôm nay!