---
title: "🚀 Giám sát giá khách sạn đối thủ và trả lời Q&A qua WhatsApp với OpenAI GPT-4.1"
description: "Tự động hóa việc theo dõi giá phòng khách sạn đối thủ qua Amadeus API, phân tích biến động bằng AI Agent và nhận cảnh báo, trò chuyện chiến lược qua WhatsApp."
slug: "giam-sat-gia-khach-san-doi-thu-whatsapp-openai"
tags: [n8n, automation, no-code, openai, whatsapp, market-research, ai-agent]
keywords: [n8n workflow, giám sát giá khách sạn, amadeus api, openai gpt-4, whatsapp automation, revenue manager]
---

# 🚀 Giám sát giá khách sạn đối thủ và trả lời Q&A qua WhatsApp với OpenAI GPT-4.1

Các sếp làm trong ngành khách sạn (Revenue Manager, General Manager) chắc chắn hiểu cảm giác mệt mỏi khi mỗi ngày phải thủ công mở hàng loạt trang web để check giá phòng của đối thủ, lập bảng Excel so sánh, rồi cố đoán xem vì sao họ tăng/giảm giá. Việc này vừa tốn thời gian, vừa dễ bỏ lỡ các cơ hội điều chỉnh giá "vàng".

Đừng lo, workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình "rate shop", phân tích nguyên nhân biến động giá nhờ AI kết hợp sự kiện địa phương, và gửi báo cáo trực tiếp qua WhatsApp. Thậm chí các sếp còn có thể chat trực tiếp với AI để hỏi về lịch sử giá bất cứ lúc nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Thay thế hàng giờ cào dữ liệu thủ công mỗi ngày bằng hệ thống chạy tự động theo lịch (Intraday Monitoring).
- **Thông minh đa chiều (Contextual Intelligence):** Không chỉ báo giá thay đổi, hệ thống còn tự quét các sự kiện/hội nghị tại địa phương để giải thích *lý do* vì sao đối thủ tăng giá.
- **Chiến lược hành động từ AI:** AI Agent đóng vai trò như một Revenue Manager thực thụ, đưa ra các đề xuất chiến lược giá cụ thể thay vì chỉ đưa ra con số thô.
- **Tương tác trực tiếp:** Nhận cảnh báo qua WhatsApp và có thể hỏi đáp (Q&A) với AI dựa trên dữ liệu lịch sử giá đã lưu trữ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Amadeus API (hoặc OTA API tương tự):** Để lấy giá phòng khách sạn đối thủ thời gian thực.
- **OpenAI API Key:** Sử dụng model `gpt-4.1-mini` cho các Agent phân tích và trả lời Q&A.
- **WhatsApp Business API (WhatsApp Trigger / WhatsApp Node):** Để gửi cảnh báo và nhận câu hỏi tương tác.
- **n8n Data Tables / Database:** Lưu trữ snapshots giá, lịch sử giá và tóm tắt cảnh báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn hoặc copy toàn bộ JSON, sau đó paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 2 nhánh chính (Nhánh trên: Giám sát tự động & Cảnh báo; Nhánh dưới: Tương tác Q&A qua WhatsApp). Các sếp cần chú ý cấu hình các node quan trọng sau:
- **Node `Config` (Set):** Điền thông tin khách sạn của các sếp và danh sách ID/tên khách sạn đối thủ cần theo dõi. Thiết lập ngưỡng cảnh báo (ví dụ: chỉ cảnh báo nếu giá đối thủ biến động > 10%).
- **Node `Amadeus OAuth` & `Amadeus Hotel Offers` (HTTP Request):** Cấu hình thông tin xác thực API của Amadeus để lấy dữ liệu 30 ngày tới.
- **Node `OpenAI Chat Model` & `OpenAI Chat Model2` (lmChatOpenAi):** Chọn kết nối OpenAI Credentials và xác thực model `gpt-4.1-mini`.
- **Node `WhatsApp Trigger` & `Q&A` / `Send WhatsApp Alert` (WhatsApp):** Kết nối tài khoản WhatsApp Business API để gửi tin nhắn cảnh báo và nhận tin nhắn hỏi đáp từ người dùng.
- **Các node `DataTable` (`Get Our Hotel Rates`, `Upsert Latest Rates`, `Get Hotel_Rates_History`...):** Đảm bảo các bảng dữ liệu trong n8n đã được tạo sẵn để lưu trữ lịch sử giá và ngữ cảnh phân tích.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (`Test workflow`) nhánh trên (`Daily Market Check`) bằng cách trigger thủ công để kiểm tra xem dữ liệu có trả về và tin nhắn WhatsApp có gửi đi hay không.
- Nhắn tin thử qua WhatsApp vào `WhatsApp Trigger` để kiểm tra nhánh Q&A.
- Sau khi mọi thứ chạy mượt mà, gạt công tắc sang **Active** để hệ thống tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Kết hợp thêm node Slack hoặc Telegram bên cạnh WhatsApp để đội ngũ Sales & Marketing cùng theo dõi biến động giá.
- **Tối ưu hóa Data Table:** Thiết lập lịch trình tự động xóa hoặc nén dữ liệu cũ sau 6-12 tháng để tối ưu dung lượng lưu trữ.
- **Tùy chỉnh Prompt AI:** Tinh chỉnh system prompt trong AI Agent để AI đưa ra chiến lược giá phù hợp hơn với mô hình kinh doanh cụ thể của khách sạn (resort, boutique hotel hay hotel 5 sao).

### 📌 Kết luận
Với workflow n8n này, việc giám sát thị trường và đối thủ cạnh tranh không còn là cơn ác mộng tốn thời gian. Hãy triển khai ngay hôm nay để đưa ra các quyết định về giá nhanh chóng, chính xác và tối ưu doanh thu cho khách sạn của các sếp!