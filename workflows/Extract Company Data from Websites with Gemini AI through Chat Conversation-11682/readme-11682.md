---
title: "🚀 Trích xuất thông tin doanh nghiệp tự động từ Website bằng Gemini AI và Chatbot n8n"
description: "Hướng dẫn xây dựng workflow n8n tích hợp Gemini AI và Chatbot thông minh giúp tự động cào dữ liệu, phân tích website công ty và trích xuất thông tin theo yêu cầu qua hội thoại."
slug: "trich-xuat-thong-tin-doanh-nghiep-gemini-ai-n8n"
tags: [n8n, automation, no-code, gemini-ai, ai-agent, market-research]
keywords: [n8n workflow, trích xuất thông tin công ty, gemini ai n8n, ai agent cào dữ liệu website, chatbot n8n]
---

# 🚀 Trích xuất thông tin doanh nghiệp tự động từ Website bằng Gemini AI và Chatbot n8n

Các sếp có bao giờ cảm thấy mệt mỏi khi phải tốn hàng giờ đồng hồ truy cập vào từng website của đối thủ hoặc khách hàng tiềm năng để thu thập thông tin như: mô hình kinh doanh, dịch vụ, thông tin liên hệ hay quy mô công ty để làm báo cáo thị trường? Việc làm thủ công này không chỉ tốn thời gian, dễ sai sót mà còn phụ thuộc hoàn toàn vào tốc độ của nhân sự.

Giải pháp ở đây là gì? Hãy để AI làm thay các sếp! Workflow n8n này sẽ biến một cửa sổ Chat quen thuộc thành một trợ lý nghiên cứu thị trường thông minh. Các sếp chỉ cần gửi một đường link website công ty bất kỳ, trợ lý **Gemini AI** sẽ tự động "đột nhập" vào trang web đó, phân tích nội dung và trả về toàn bộ thông tin doanh nghiệp một cách chuẩn xác, nhanh chóng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình nghiên cứu:** Không còn phải copy-paste thủ công từ website vào file Excel.
- **Tương tác dạng hội thoại linh hoạt:** Dễ dàng đổi URL, yêu cầu bổ sung thông tin hoặc hỏi tiếp ngay trong khung chat (`When chat message received`, `Request User Input`).
- **Tùy biến linh hoạt:** Dễ dàng thay đổi các trường dữ liệu cần trích xuất và ngôn ngữ hiển thị thông qua node `Config`.
- **Ứng dụng AI Agent mạnh mẽ:** Kết hợp giữa khả năng phân tích ngôn ngữ tự nhiên và công cụ truy cập web (`HttpRequestTool`).
:::

### 📦 Các thành phần chính trong Workflow (14 Nodes)
- **Chat Triggers & Responses:** `When chat message received`, `Request User Input`, `Request Next URL`, `Respond to Chat`
- **AI Agents & LLM Models:** `AI Agent (Extract URL)`, `AI Agent (Access URL)`, `Google Gemini Chat Model`, `Google Gemini Chat Model1`
- **Tools & Utilities:** `HttpRequestTool`, `Config`, `Check URL`
- **Data Processing (Code):** `ExtractedChatInput`, `ParsedCsv`, `ChatResponse`

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Google AI Studio API Key:** Đăng ký miễn phí tại [Google AI Studio](https://aistudio.google.com/api-keys) để lấy API key kết nối với các node Gemini.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy đoạn mã JSON của workflow này hoặc tải file JSON từ nguồn cung cấp.
- Mở giao diện n8n Editor, chọn **Add workflow** -> Nhấn dấu `...` ở góc trên bên phải -> Chọn **Import from File / Clipboard** và dán dữ liệu vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Cấu hình Credentials Gemini:** 
  - Tìm đến các node `Google Gemini Chat Model` và `Google Gemini Chat Model1`.
  - Thêm mới Credentials loại `Google Palm Api` (hoặc Gemini API) và dán API Key đã lấy từ Google AI Studio vào.
- **Tùy chỉnh Node `Config`:**
  - Node này cực kỳ quan trọng giúp các sếp định nghĩa các trường dữ liệu muốn trích xuất (`targetCompanyFields`) và ngôn ngữ trả về kết quả (`language` - ví dụ: Tiếng Việt, Tiếng Anh, Tiếng Nhật...).
- **Kiểm tra các AI Agent:**
  - Đảm bảo các node `AI Agent (Extract URL)` và `AI Agent (Access URL)` đã được liên kết chính xác với các model Gemini và các công cụ hỗ trợ (`HttpRequestTool`).

#### 3. Kích hoạt ⚡️
- Nhấn nút **Chat** test trực tiếp ngay trong giao diện n8n (hoặc mở Chat UI tích hợp).
- Gửi thử một URL website bất kỳ (ví dụ: `https://example.com/`).
- Kiểm tra kết quả trả về từ AI Agent. Nếu mọi thứ hoạt động trơn tru, hãy bật công tắc **Active** phía trên góc phải để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ tự động:** Kết nối thêm node **Google Sheets** hoặc **Airtable** ở cuối luồng chat để tự động lưu lại thông tin các công ty đã trích xuất thành một cơ sở dữ liệu gọn gàng.
- **Tích hợp kênh liên lạc:** Thay vì dùng chat nội bộ của n8n, các sếp có thể đổi trigger thành **Telegram Trigger** hoặc **Slack** để nhân viên sales có thể gửi link vào nhóm chat và nhận báo cáo ngay lập tức.
- **Gửi email báo cáo:** Thêm node **Gmail** hoặc **SendGrid** để gửi toàn bộ thông tin phân tích vào email cá nhân khi cần lưu trữ lâu dài.

### 📌 Kết luận
Workflow trích xuất thông tin doanh nghiệp bằng Gemini AI và Chatbot chính là trợ thủ đắc lực giúp các đội ngũ Sales, Marketing và Nghiên cứu thị trường tiết kiệm hàng chục giờ làm việc mỗi tuần. Hãy "lên đồ" ngay hôm nay để tối ưu hóa năng suất doanh nghiệp cùng n8n nhé các sếp!