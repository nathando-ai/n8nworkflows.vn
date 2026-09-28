---
title: "🚀 Tạo chatbot AI thương hiệu cho website với Flowise Multi-Agent Chatflows"
description: "Giải pháp tự động hóa 100% không cần code, giúp doanh nghiệp triển khai chatbot AI nhanh chóng, tùy chỉnh và tích hợp dễ dàng với website."
slug: "tao-chatbot-ai-flowise"
tags: [n8n, automation, no-code, ai, flowise]
keywords: [n8n workflow, tự động hóa, chatbot AI, Flowise, multi-agent chatflows]
---

# 🚀 Tạo chatbot AI thương hiệu cho website với Flowise Multi-Agent Chatflows

Bạn đang phải trả giá cao cho đội ngũ chăm sóc khách hàng, hoặc gặp khó khăn khi muốn cung cấp hỗ trợ 24/7 mà không muốn viết mã?  
Workflow này sẽ giúp bạn **tự động hóa hoàn toàn** quy trình tạo chatbot AI, tích hợp ngay vào website của mình, không cần viết bất kỳ dòng code nào. Bạn chỉ cần cấu hình một vài thông số, và voilà – một chatbot chuyên nghiệp, có thể trả lời khách hàng, thu thập dữ liệu và hỗ trợ bán hàng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần viết code, triển khai trong vài phút.  
- **Chính xác & nhất quán**: Mọi câu trả lời đều dựa trên mô hình LLM đã được cấu hình.  
- **Tùy chỉnh thương hiệu**: Thêm logo, màu sắc, lời chào cá nhân hóa ngay trong widget.  
- **Hoạt động liên tục**: Chatbot luôn sẵn sàng 24/7, giảm tải cho đội ngũ nhân viên.  
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **N8n**: Cài đặt phiên bản mới nhất (Self-hosted hoặc Cloud).  
- **Flowise**: Đăng ký hoặc tự host Flowise, có **API Key** và **URL**.  
- **Credentials**:  
  - `httpHeaderAuth` trong n8n (Authorization: Bearer <FLOWSIE_API_KEY>).  
- **Website**: Có thể thêm widget chat qua CDN (đoạn mã dưới đây).  
- **Webhook URL**: URL của workflow n8n (được tạo khi lưu workflow).  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ trang n8n (https://n8n.io/workflows/4651).  
2. Trong n8n, chọn **Import** → **Upload JSON** → chọn file vừa tải.  
3. Kiểm tra lại các node đã được import đúng.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên node | Thông số cần cấu hình | Hướng dẫn |
|------|----------|-----------------------|-----------|
| **chatTrigger** | *When chat message received* | `Webhook URL` | Dùng URL của workflow (được copy từ n8n → Settings → Webhook URL). |
| **set** | *Edit Fields* | `Flow ID`, `Flowise URL` | Đặt `Flow ID` (ID của chatflow trong Flowise) và `Flowise URL` (địa chỉ API). |
| **httpRequest** | *Flowise* | `URL`, `Headers` | `URL`: `${Flowise URL}/api/v1/flow/${Flow ID}/chat` <br> `Headers`: `Authorization: Bearer <FLOWSIE_API_KEY>` (đã được cấu hình trong credentials). |

#### Cấu hình chi tiết
1. **chatTrigger**  
   - Mở node, vào tab **Webhook** → **Webhook URL** → dán URL đã lấy từ n8n.  
   - Đặt **Method** là `POST`.  
2. **set**  
   - Thêm hai trường:  
     - `flowId`: ID của Flowise flow (được lấy từ Flowise UI).  
     - `flowiseUrl`: URL cơ bản của Flowise (ví dụ `https://your-flowise.com`).  
3. **httpRequest**  
   - **URL**: `{{ $json["flowiseUrl"] }}/api/v1/flow/{{ $json["flowId"] }}/chat`  
   - **Method**: `POST`  
   - **Headers**: `Authorization: Bearer {{ $credentials.httpHeaderAuth.apiKey }}`  
   - **Body**: `{{ $json["body"] }}` (được truyền từ node trước).  

### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn “Execute Node” trên `chatTrigger` với payload mẫu (định dạng JSON tương tự như widget gửi).  
2. Kiểm tra phản hồi từ Flowise trong n8n → Logs.  
3. Khi mọi thứ hoạt động, bật **Active** cho workflow.

## ✍️ Mẹo & gợi ý nâng cao
- **Slack Notification**: Thêm node Slack để gửi tin nhắn khi có câu hỏi mới.  
- **Google Sheets Log**: Ghi lại mọi tin nhắn và trả lời vào bảng tính để phân tích.  
- **Email Summary**: Gửi báo cáo hàng ngày về số lượng câu hỏi, thời gian phản hồi.  
- **Custom Welcome Message**: Sử dụng `initialMessages` trong `createChat` để thay đổi lời chào.  

## 📌 Kết luận
Workflow này giúp các sếp **đưa chatbot AI vào website** chỉ trong vài phút, tiết kiệm chi phí và thời gian, đồng thời nâng cao trải nghiệm khách hàng.  
Hãy tải file JSON, cấu hình các thông số cần thiết, và triển khai ngay hôm nay! 🚀