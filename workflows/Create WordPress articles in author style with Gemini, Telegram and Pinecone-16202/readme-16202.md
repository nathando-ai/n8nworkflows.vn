---
title: "🚀 Tự động hóa sáng tạo nội dung WordPress chuẩn văn phong tác giả với Google Gemini, Pinecone và Telegram"
description: "Xây dựng hệ thống content marketing tự động 100%: phân tích văn phong tác giả qua Pinecone & Gemini, duyệt ý tưởng qua Telegram và tự động đăng bài lên WordPress."
slug: "tu-dong-hoa-viet-bai-wordpress-gemini-pinecone-telegram"
tags: [n8n, automation, wordpress, google-gemini, telegram, pinecone, ai-agent]
keywords: [n8n workflow, viết bài wordpress tự động, ai agent writer, gemini pinecone, telegram approval]
---

# 🚀 Tự động hóa sáng tạo nội dung WordPress chuẩn văn phong tác giả với Google Gemini, Pinecone và Telegram

Viết blog đều đặn và giữ vững văn phong đặc trưng là một thử thách lớn đối với mọi nhà sáng tạo nội dung và doanh nghiệp. Việc thuê writer tốn kém chi phí, trong khi tự viết lại tốn hàng giờ đồng hồ nghiên cứu, lên ý tưởng và biên tập. 

Workflow n8n này sinh ra để giải quyết triệt để nỗi đau đó! Hệ thống sẽ tự động quét thông tin, học hỏi văn phong tác giả thông qua **Pinecone Vector Store** kết hợp sức mạnh của **Google Gemini**, đề xuất ý tưởng qua **Telegram** để các sếp duyệt 1 chạm, và cuối cùng tự động xuất bản bài viết hoàn chỉnh lên **WordPress**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Văn phong chuẩn xác 100%**: AI học trực tiếp từ các bài viết cũ của tác giả thông qua Vector Database Pinecone, không lo bài viết bị "vô hồn" hay mang mác AI lộ liễu.
- **Kiểm soát toàn diện qua Telegram**: Nhận ý tưởng bài viết trực tiếp trên Telegram, duyệt hoặc từ chối nhanh chóng chỉ bằng các nút bấm tương tác (Interactive Buttons).
- **Tự động hóa hoàn toàn quy trình**: Từ khâu lên ý tưởng, nghiên cứu dữ liệu (Perplexity/Reddit), viết bài cho đến đăng thẳng lên WordPress mà không cần thao tác thủ công.
- **Tiết kiệm 90% thời gian**: Giảm tải khối lượng công việc khổng lồ cho đội ngũ content marketing, giúp duy trì lịch đăng bài đều đặn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Google Gemini API Key** (Dành cho AI Agent, Chat Model và Embeddings).
- **Pinecone Account & Index** (Lưu trữ và truy xuất vector văn phong tác giả).
- **Telegram Bot Token** (Tạo qua @BotFather để gửi thông báo và nhận phản hồi duyệt bài).
- **Google Sheets** (Lưu trữ danh sách tác giả, trạng thái bài viết và nguồn dữ liệu).
- **WordPress Site** (Đã bật Application Passwords để n8n có quyền tạo bài viết).
- **Perplexity API hoặc OpenRouter** (Hỗ trợ nghiên cứu thông tin thời gian thực).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cấp hoặc copy toàn bộ JSON.
- Mở n8n Editor, chọn **Workflows** -> **Import from File** (hoặc dùng tổ hợp phím `Ctrl+V` / `Cmd+V` trực tiếp vào màn hình canvas).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các thông số quan trọng sau trong các node cốt lõi:
- **Google Sheets Nodes (`FetchAuthorList`, `Get All Articles from Sheet`, v.v.):** Kết nối tài khoản Google của các sếp, trỏ đúng đến file Google Sheets quản lý ý tưởng bài viết và danh sách tác giả.
- **Pinecone Vector Store (`Pinecone Vector Store`, `Pinecone Vector Store1`):** Nhập API Key của Pinecone, chọn đúng Index Name đã tạo để hệ thống lưu và tìm kiếm embedded document văn phong tác giả.
- **Google Gemini & Embeddings Nodes:** Cài đặt credentials cho Google Gemini. Đảm bảo các model như `Google Gemini Chat Model` được cấu hình đúng phiên bản (ví dụ: `gemini-1.5-pro` hoặc `gemini-1.5-flash`).
- **Telegram Nodes (`Send to Telegram - Send Article Idea with Buttons`, `Telegram Trigger`):** Điền Telegram Bot Token. Đảm bảo Bot đã được thêm vào nhóm chat hoặc kênh mà các sếp muốn nhận thông báo duyệt bài.
- **WordPress Node (`Create a post`, `Create a post1`):** Cấu hình URL trang WordPress của các sếp kèm theo tài khoản quản trị và Application Password (tránh dùng mật khẩu đăng nhập thông thường).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** trên một vài nhánh thủ công (`When clicking ‘Execute workflow’`) để kiểm tra kết nối với Google Sheets và Telegram.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để hệ thống tự động chạy theo lịch (`Schedule Trigger`) hoặc sự kiện tương tác (`Telegram Trigger`).

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Ngoài Telegram, các sếp có thể tích hợp thêm node Slack hoặc Discord để đội ngũ biên tập cùng theo dõi tiến độ duyệt bài.
- **Lưu log chi tiết:** Sử dụng thêm các node Google Sheets phụ để ghi lại lịch sử các bài viết đã xuất bản thành công kèm link trực tiếp.
- **Tinh chỉnh Prompt cho AI Agent:** Tùy biến system prompt trong node `AI Agent` để ép AI tuân thủ cấu trúc bài viết riêng của doanh nghiệp (ví dụ: có Call-To-Action, mục lục tự động, thẻ Heading chuẩn SEO).

### 📌 Kết luận
Với workflow tự động hóa này, việc sản xuất hàng loạt bài viết chất lượng cao, đậm chất cá nhân hóa trên WordPress không còn là gánh nặng. Hãy import workflow ngay hôm nay để tối ưu hóa hiệu suất đội ngũ content của các sếp!