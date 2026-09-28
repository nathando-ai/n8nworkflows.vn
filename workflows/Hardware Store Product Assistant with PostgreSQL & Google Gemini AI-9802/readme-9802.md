---
title: "🚀 Xây dựng Trợ lý AI Quản lý Kho & Tư vấn Sản phẩm Cửa hàng với n8n, PostgreSQL và Google Gemini"
description: "Hướng dẫn tích hợp AI Agent với cơ sở dữ liệu PostgreSQL thông qua MCP Client Tool và Google Gemini để tự động tra cứu sản phẩm, tư vấn vật liệu và tạo báo giá cho cửa hàng phần cứng/vật liệu."
slug: "tro-ly-ai-cua-hang-phan-cung-postgres-gemini"
tags: [n8n, automation, ai-agent, postgresql, google-gemini, chatbot]
keywords: [n8n workflow, ai agent postgresql, google gemini n8n, mcp client tool, chatbot cửa hàng vật liệu, tự động hóa n8n]
---

# 🚀 Xây dựng Trợ lý AI Quản lý Kho & Tư vấn Sản phẩm Cửa hàng với n8n, PostgreSQL và Google Gemini

Các sếp kinh doanh cửa hàng vật liệu xây dựng, dụng cụ cơ khí hay thiết bị phần cứng thường xuyên đối mặt với việc nhân viên tốn hàng giờ để tra cứu mã sản phẩm, kiểm tra tồn kho, danh mục hay làm báo giá thủ công cho khách. Điều này không chỉ làm chậm tốc độ phản hồi mà còn dễ dẫn đến sai sót.

Giải pháp ở đây là gì? Workflow n8n tích hợp **AI Agent**, **Google Gemini** và **PostgreSQL** này sẽ biến dữ liệu kho hàng của các sếp thành một trợ lý ảo thông minh. Khách hàng hoặc nhân viên chỉ cần chat trực tiếp để tra cứu sản phẩm theo ID, tên, danh mục, mô tả... theo thời gian thực mà không cần chạm tay vào hệ thống quản lý cơ sở dữ liệu phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và phản hồi các truy vấn cơ sở dữ liệu mượt mà, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tra cứu thông tin tức thì:** Tìm kiếm sản phẩm linh hoạt qua ID, tên, danh mục, phân mục hoặc ghi chú bằng ngôn ngữ tự nhiên.
- **Tư vấn chuyên sâu:** AI hiểu rõ ngữ cảnh để tư vấn vật liệu phù hợp cho các dự án xây dựng, sửa chữa của khách hàng.
- **Tạo báo giá tự động:** Trợ lý AI tự tổng hợp thông tin sản phẩm từ cơ sở dữ liệu để xuất ra bảng báo giá chi tiết trong tích tắc.
- **Hoạt động liên tục 24/7:** Chatbot tích hợp trực tiếp, sẵn sàng giải đáp thắc mắc khách hàng mọi lúc mọi nơi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (hỗ trợ các node LangChain và MCP).
- **Cơ sở dữ liệu PostgreSQL:** Đã có sẵn bảng dữ liệu sản phẩm phần cứng/vật liệu.
- **Google Gemini API Key:** Tài khoản Google AI Studio để lấy API Key cho mô hình Gemini.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ nguồn cung cấp, sau đó vào giao diện n8n, chọn **Add workflow** -> Click vào dấu ba chấm (...) ở góc trên bên phải -> Chọn **Import from File / Clipboard** và dán đoạn mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 12 nodes kết hợp giữa LangChain AI Agent và cơ sở dữ liệu. Các sếp cần cấu hình các điểm sau:

- **Các node `Query Product by ID`, `Query Product by Name`, `Query Product by Description`, `Query Product by Category`, `Query Product by Subcategory`, `Query Product by Note` (PostgreSQL Tools):**
  - Kết nối và chọn đúng **PostgreSQL Credentials** của hệ thống kho hàng các sếp.
  - Đảm bảo câu lệnh SQL truy vấn bên trong các tool này khớp với cấu trúc bảng (table schema) sản phẩm thực tế của doanh nghiệp.
- **Node `Language Model (Google Gemini)`:**
  - Thiết lập **Google Palm/Gemini API Credentials** bằng API Key cá nhân từ Google AI Studio.
  - Chọn model Gemini phù hợp (ví dụ: `gemini-1.5-pro` hoặc `gemini-1.5-flash`).
- **Node `AI Agent`, `Chat Memory`, `Chat Trigger` & `DB Tools Client` (MCP Client Tool):**
  - Giữ nguyên cấu trúc liên kết MCP (Model Context Protocol) để AI Agent có quyền gọi các công cụ truy vấn cơ sở dữ liệu PostgreSQL một cách linh hoạt.

#### 3. Kích hoạt ⚡️
- Click vào nút **Chat Window** (hoặc dùng Chat Trigger) để thử hỏi trợ lý vài câu lệnh mẫu như: *"Tìm cho tôi các sản phẩm búa trong danh mục dụng cụ cầm tay"* hoặc *"Lấy thông tin sản phẩm có ID 105"*.
- Kiểm tra xem AI đã gọi đúng tool PostgreSQL để trả về kết quả chính xác chưa.
- Sau khi test ngon lành, gạt công tắc sang **Active** để đưa trợ lý vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh chat đa nền tảng:** Thay vì chỉ dùng Chat Trigger nội bộ của n8n, các sếp có thể thay thế bằng Telegram Trigger hoặc Slack Trigger để nhân viên hoặc khách hàng chat trực tiếp qua app nhắn tin.
- **Lưu lịch sử hội thoại:** Kết hợp thêm node lưu trữ lịch sử chat vào Google Sheets hoặc chính PostgreSQL để phân tích nhu cầu tìm kiếm của khách hàng.
- **Gửi báo cáo định kỳ:** Tạo một nhánh workflow định kỳ tổng hợp các sản phẩm được tra cứu nhiều nhất và gửi thông báo qua email hoặc nhóm Slack cho bộ phận kinh doanh.

### 📌 Kết luận
Với sự kết hợp mạnh mẽ giữa n8n, Google Gemini AI và PostgreSQL MCP Tool, việc tự động hóa dịch vụ khách hàng và tra cứu kho hàng chưa bao giờ dễ dàng đến thế. Hãy triển khai ngay hôm nay để tối ưu hóa vận hành cho cửa hàng của các sếp!