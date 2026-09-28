---
title: "🚀 Tạo Chatbot AI cho Website với Langflow Backend & Branding Tùy Chỉnh"
description: "Tự động hoá chatbot AI trên website bằng n8n + Langflow, không cần code, tích hợp branding riêng, hoạt động 24/7."
slug: "tao-chatbot-ai-website-langflow"
tags: [n8n, automation, no-code, AI, chatbot]
keywords: [n8n workflow, tự động hóa, chatbot AI, Langflow, no-code AI]
---

# 🚀 Tạo Chatbot AI cho Website với Langflow Backend & Branding Tùy Chỉnh

Bạn đang phải đối mặt với **chi phí nhân lực cao**, **độ trễ trả lời** và **không đồng nhất** khi hỗ trợ khách hàng qua chat truyền thống?  
Việc **cài đặt và duy trì một chatbot AI** thường đòi hỏi lập trình phức tạp, khiến nhiều doanh nghiệp bỏ lỡ cơ hội nâng cao trải nghiệm người dùng.

**Workflow n8n** này sẽ giải quyết toàn bộ vấn đề trên:  
- **Kết nối website** của bạn với **Langflow** – nền tảng low‑code AI mạnh mẽ.  
- **Tự động nhận tin nhắn**, gửi tới Langflow để xử lý, trả về câu trả lời ngay lập tức.  
- **Branding tùy chỉnh** hoàn toàn qua đoạn mã JavaScript, không cần viết một dòng code server.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: trả lời tự động 24/7, không cần nhân viên trực chat.  
- **Độ chính xác cao**: nhờ mô hình AI của Langflow, câu trả lời luôn chuẩn và liên quan.  
- **Branding nhất quán**: giao diện chat được tùy chỉnh màu sắc, logo, lời chào riêng.  
- **Mở rộng dễ dàng**: chỉ cần thay đổi Flow ID hoặc thêm node mới trong n8n.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
1. **Tài khoản Langflow** (để lấy `LANGFLOW_URL` và `FLOW_ID`).  
2. **API Key** cho Langflow – sẽ được lưu dưới credential `httpHeaderAuth` trong n8n.  
3. **Webhook URL** của n8n (được tạo khi node **When chat message received** được kích hoạt).  
4. **Truy cập vào website** để chèn đoạn mã CDN của n8n Chat (xem phần “Enable n8n CDN on your website”).  
5. **n8n** đã được cài đặt và chạy (đề xuất trên VPS riêng).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở **n8n Editor**.  
2. Click **Import** → **Upload JSON** và chọn file JSON của workflow (hoặc copy/paste nội dung JSON).  
3. Nhấn **Import** → workflow sẽ xuất hiện trên canvas với 3 node:  
   - `When chat message received` (chatTrigger)  
   - `Edit Fields` (set)  
   - `Langflow` (httpRequest)

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Hành động cần cấu hình | Chi tiết |
|------|------------------------|----------|
| **When chat message received** | **Webhook URL** | Sau khi lưu workflow, n8n sẽ tạo URL webhook (ví dụ: `https://your-n8n.com/webhook/123`). Sao chép URL này để dùng trong đoạn mã CDN (xem phần “Enable n8n CDN on your website”). |
| **Edit Fields** (set) | **Mapping dữ liệu** | Đặt các trường: <br>• `chatInput` → `{{$json["message"]}}` <br>• `sessionId` → `{{$json["sessionId"]}}` (hoặc tạo UUID nếu chưa có). |
| **Langflow** (httpRequest) | **Endpoint & Header** | - **URL**: `{{ $env.LANGFLOW_URL }}/api/v1/flows/{{ $env.FLOW_ID }}/run` <br> - **Method**: `POST` <br> - **Headers**: `Authorization: Bearer {{ $credentials.httpHeaderAuth.apiKey }}` <br> - **Body (JSON)**: <br>```json { "input": "{{$json["chatInput"]}}", "session_id": "{{$json["sessionId"]}}" }``` |
| **Credentials** | **httpHeaderAuth** | Tạo credential mới → **HTTP Header Auth** → nhập **API Key** của Langflow. |

> **Lưu ý:** Đảm bảo các biến môi trường `LANGFLOW_URL` và `FLOW_ID` được khai báo trong **Settings → Environment Variables** của n8n, hoặc thay thế trực tiếp trong node nếu không dùng env.

#### 3. Kích hoạt ⚡️
1. **Test run**: Gửi một tin nhắn thử nghiệm từ website (sử dụng đoạn mã CDN). Kiểm tra log node `Langflow` để xác nhận phản hồi từ AI.  
2. Khi mọi thứ hoạt động ổn, bật **Active** cho workflow (nút chuyển đổi ở góc trên‑phải).  

### ✍️ Mẹo & gợi ý nâng cao
- **Ghi log chi tiết**: Thêm node `Function` sau `Langflow` để lưu câu trả lời và thời gian phản hồi vào Google Sheets hoặc Database.  
- **Thông báo Slack/Telegram**: Khi có lỗi hoặc phản hồi đặc biệt (ví dụ: “khách hàng yêu cầu hỗ trợ người thật”), dùng node **Slack** hoặc **Telegram** để cảnh báo đội ngũ.  
- **Báo cáo định kỳ**: Dùng node **Cron** + **Google Analytics** để tổng hợp số lượng tin nhắn, thời gian phản hồi, mức độ hài lòng.  
- **Thêm đa ngôn ngữ**: Cập nhật `defaultLanguage` và `i18n` trong đoạn mã `createChat` để hỗ trợ tiếng Việt, tiếng Anh, …  

### 📌 Kết luận
Với chỉ **3 node** trong n8n, các sếp đã có thể triển khai **chatbot AI** mạnh mẽ, **đầy thương hiệu** cho website mà không cần viết code server. Hãy **import workflow**, **điền các credential**, **chèn CDN** và **bật hoạt động** ngay hôm nay – để khách hàng của bạn luôn nhận được phản hồi nhanh chóng, chính xác và đồng nhất.  

Chúc các sếp thành công! 🚀