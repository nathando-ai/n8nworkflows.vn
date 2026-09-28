---
title: "🚀 Tạo công thức nấu ăn tự động với Ollama AI Chef Agent trong n8n"
description: "Xây dựng trợ lý ảo đầu bếp thông minh sử dụng Ollama AI và n8n Agent để sáng tạo công thức nấu ăn từ các nguyên liệu có sẵn một cách nhanh chóng."
slug: "tao-cong-thuc-nau-an-tu-dong-voi-ollama-ai-chef-agent"
tags: [n8n, automation, no-code, AI, Ollama, Chatbot, Chef Agent]
keywords: [n8n workflow, tự động hóa, Ollama AI, AI Agent, tạo công thức nấu ăn, chatbot nấu ăn]
keywords: [n8n workflow, tự động hóa, Ollama AI, AI Agent, tạo công thức nấu ăn, chatbot nấu ăn]
---

# 🚀 Tạo công thức nấu ăn tự động với Ollama AI Chef Agent

Các sếp có bao giờ rơi vào cảnh mở tủ lạnh ra thấy một đống nguyên liệu lộn xộn: chút thịt bò thừa, nửa củ hành tây, vài quả cà chua và không biết phải nấu món gì chưa? Việc tra cứu công thức thủ công vừa mất thời gian lại chẳng sáng tạo. 

Đừng lo, bài toán này sẽ được giải quyết triệt để với **Generate Recipes from Ingredients with Ollama AI Chef Agent** do nhóm Clown Mutiny phát triển. Workflow n8n này sẽ biến n8n thành một đầu bếp AI thực thụ, sẵn sàng tư vấn thực đơn và công thức nấu ăn độc đáo dựa trên chính xác những gì các sếp đang có trong tủ lạnh!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tận dụng tối đa nguyên liệu:** Gợi ý món ăn ngon từ những gì còn lại trong tủ lạnh, chống lãng phí thực phẩm.
- **Tương tác linh hoạt:** Hỗ trợ cả giao diện Chat trực tiếp lẫn qua Webhook để tích hợp vào ứng dụng riêng.
- **Tư duy thông minh:** Tích hợp AI Agent và công cụ suy nghĩ (`Think`), giúp đầu bếp AI lên thực đơn chi tiết, chuẩn xác từ bước chuẩn bị đến cách chế biến.
- **Bảo mật và tự chủ:** Chạy mô hình ngôn ngữ lớn (LLM) cục bộ thông qua **Ollama**, không lo lộ dữ liệu hay tốn phí API bên thứ ba.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Hệ thống n8n:** Đã cài đặt n8n (phiên bản hỗ trợ Langchain nodes).
- **Ollama:** Đã cài đặt và chạy Ollama trên máy tính hoặc VPS cá nhân (kèm theo mô hình chat như Llama 3, Mistral, v.v.).
- **Credentials:** Thông tin kết nối Ollama API trong n8n (`ollamaApi`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tải file JSON của workflow (hoặc copy toàn bộ JSON từ nguồn cấp) và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 7 nodes chính kết hợp giữa AI Agent và Webhook. Các sếp cần chú ý cấu hình các điểm sau:
- **Ollama Chat Model (`lmChatOllama`):** 
  - Chọn đúng Credentials kết nối tới Ollama của các sếp.
  - Điền tên model đang chạy trên Ollama (ví dụ: `llama3` hoặc `mistral`).
- **Chef AI Agent (`agent`):** 
  - Kiểm tra lại cấu hình System Prompt của Agent để đảm bảo AI đóng vai một "Đầu bếp trưởng vui tính và tài ba", chuyên gia biến nguyên liệu thừa thành món ăn triệu đô.
- **Webhook (`webhook`):** 
  - Đường dẫn mặc định được thiết lập là `/lets-cook`. Các sếp có thể thay đổi path này nếu muốn tích hợp với các ứng dụng khác như Telegram, Zalo hoặc Web app cá nhân.
- **Simple Memory (`memoryBufferWindow`):** 
  - Giúp AI nhớ được ngữ cảnh trò chuyện trước đó (ví dụ: người dùng dị ứng món gì, thích ăn cay hay nhạt).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử gửi tin nhắn qua giao diện `When chat message received` hoặc test request qua Webhook để kiểm tra phản hồi từ Chef AI.
- Sau khi test ngon lành, bật **Active** để đưa đầu bếp ảo vào hoạt động chính thức!

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống xịn sò hơn nữa, các sếp có thể mở rộng workflow với các ý tưởng sau:
- **Tích hợp Telegram/Messenger Bot:** Thay vì dùng chat mặc định của n8n, hãy nối Webhook với Telegram Bot để các sếp nhắn tin hỏi công thức trực tiếp từ điện thoại khi đứng trong bếp.
- **Lưu lịch sử món ăn:** Thêm node Google Sheets để lưu lại các công thức mà AI đã gợi ý mỗi khi các sếp nấu thành công.
- **Tạo danh sách mua sắm tự động:** Kết hợp thêm công cụ tìm kiếm hoặc AI phụ để liệt kê những gia vị thiếu cần mua thêm cho món ăn hoàn hảo hơn.

### 📌 Kết luận
Workflow **Generate Recipes from Ingredients with Ollama AI Chef Agent** là một ứng dụng tuyệt vời, vui nhộn nhưng cực kỳ hữu ích của AI trong đời sống hàng ngày. Hãy cài đặt ngay lên hệ thống n8n của các sếp để có một trợ lý nấu ăn cực chất ngay hôm nay!