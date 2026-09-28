---
title: "🚀 Xây dựng AI Agent Nghiên Cứu Tin Tức & Phân Tích Cảm Xúc với Gemini và SearXNG trong n8n"
description: "Hướng dẫn chi tiết tự động hóa quy trình nghiên cứu thông tin thị trường và phân tích sắc thái tin tức bằng AI Agent sử dụng Google Gemini và SearXNG."
slug: "nghien-cuu-tin-tuc-va-phan-tich-cam-xuc-ai-agent-gemini-searxng"
tags: [n8n, automation, ai-agent, google-gemini, searxng, sentiment-analysis]
keywords: [n8n workflow, ai agent nghiên cứu tin tức, phân tích cảm xúc ai, google gemini n8n, searxng tool n8n]
---

# 🚀 Tự Động Hóa Nghiên Cứu Tin Tức & Phân Tích Cảm Xúc với AI Agent (Gemini & SearXNG)

Các sếp có bao giờ cảm thấy ngợp trước hàng núi thông tin, tin tức thị trường, đối thủ cạnh tranh mỗi ngày? Việc ngồi đọc, tổng hợp rồi đánh giá xem thông tin đó mang sắc thái tích cực, tiêu cực hay trung lập tốn rất nhiều thời gian thủ công. 

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một **AI Agent thông minh trong n8n** - giải pháp tự động hóa 100% không cần code, giúp gom nhặt tin tức thời gian thực từ internet và phân tích cảm xúc sắc bén chỉ trong vài giây!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động tìm kiếm:** Khai thác thông tin mới nhất trên web thông qua công cụ tìm kiếm riêng tư SearXNG.
- **Phân tích thông minh:** Sử dụng sức mạnh của Google Gemini để đóng vai trò các chuyên gia nghiên cứu và phân tích tâm lý thị trường.
- **Tương tác trực tiếp:** Trò chuyện trực tiếp qua giao diện Chat gọn gàng ngay trên n8n canvas.
- **Tiết kiệm 90% thời gian:** Thay vì mất hàng giờ đồng hồ lướt web và tổng hợp, AI sẽ làm thay toàn bộ quy trình.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị sẵn:
- Một instance n8n đang hoạt động (Cloud hoặc Self-hosted).
- **Google Gemini API Key** (`googlePalmApi`) để vận hành các mô hình ngôn ngữ.
- **SearXNG Instance** (tự host hoặc công khai) tích hợp API (`searXngApi`) để AI có quyền truy cập internet tìm kiếm dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ n8n (Link gốc: [n8n.io/workflows/5286](https://n8n.io/workflows/5286)) và tiến hành Import trực tiếp vào giao diện n8n của mình bằng cách chọn **Add workflow** -> **Import from File**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 6 nodes chính hoạt động mượt mà với nhau. Các sếp cần cấu hình các điểm sau:

- **Node `Gemini 2.5 Flash` (lmChatGoogleGemini):** 
  - Chọn hoặc thêm mới Credentials `Google Palm API` với API Key của các sếp.
  - Chọn model Gemini phù hợp (ví dụ: `gemini-1.5-flash` hoặc phiên bản mới hơn tùy nhu cầu).
- **Node `web_search` (toolSearXng):** 
  - Cấu hình Credentials `searXngApi` trỏ tới địa chỉ instance SearXNG của các sếp (hoặc server SearXNG tự host).
- **Node `Research Agent` & `Sentiment Analysis Agent` (agent):** 
  - Tinh chỉnh lại System Prompt (nhiệm vụ, vai trò) cho từng Agent. Research Agent sẽ chịu trách nhiệm đi cào/tìm kiếm thông tin, còn Sentiment Analysis Agent sẽ nhận dữ liệu đó để đánh giá xu hướng cảm xúc (tích cực, tiêu cực, trung lập).
- **Node `get_current_date` (dateTimeTool):** Giúp cung cấp mốc thời gian thực để AI biết đâu là tin tức mới nhất.
- **Node `When chat message received` (chatTrigger):** Điểm khởi đầu nhận câu lệnh/câu hỏi từ người dùng qua khung chat.

#### 3. Kích hoạt ⚡️
- Sử dụng giao diện Chat tích hợp sẵn trong n8n canvas để gửi thử một câu lệnh (Ví dụ: *"Nghiên cứu các tin tức mới nhất về cổ phiếu Tesla tuần này và phân tích cảm xúc thị trường"*).
- Kiểm tra kết quả trả về từ AI Agents xem đã chính xác chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để đưa workflow vào trạng thái sẵn sàng hoạt động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh liên lạc:** Thay vì dùng khung chat n8n, các sếp có thể thay thế node `chatTrigger` bằng **Telegram Trigger** hoặc **Slack Trigger** để nhận báo cáo tin tức tự động mỗi sáng ngay trên điện thoại.
- **Lưu trữ kết quả:** Nối thêm node **Google Sheets** hoặc **Notion** ở cuối luồng để lưu lại toàn bộ báo cáo nghiên cứu và phân tích cảm xúc làm tài liệu lưu trữ.
- **Lên lịch tự động:** Sử dụng node **Schedule Trigger** để hệ thống tự động chạy một chủ đề cố định vào khung giờ định sẵn mà không cần con người đặt câu hỏi.

### 📌 Kết luận
Với sự kết hợp hoàn hảo giữa Google Gemini và công cụ tìm kiếm mã nguồn mở SearXNG, workflow này là một trợ thủ đắc lực cho các nhà đầu tư, Marketer hay nhà sáng tạo nội dung muốn nắm bắt nhanh chóng mạch đập của thông tin. Hãy triển khai ngay hôm nay để tối ưu hóa năng suất làm việc của các sếp nhé!