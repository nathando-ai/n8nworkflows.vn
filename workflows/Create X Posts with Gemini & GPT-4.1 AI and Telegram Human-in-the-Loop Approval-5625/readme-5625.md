---
title: "🚀 Tự động tạo bài đăng X (Twitter) với Gemini & GPT-4 cùng cơ chế Phê duyệt Telegram"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình sáng tạo nội dung mạng xã hội đa mô hình AI kết hợp quy trình kiểm duyệt (Human-in-the-Loop) qua Telegram."
slug: "tu-dong-tao-bai-dang-x-gemini-gpt4-telegram"
tags: [n8n, automation, no-code, ai, telegram, twitter, gemini, gpt-4]
keywords: [n8n workflow, tu dong hoa twitter, tao bai dang bang ai, gemini n8n, telegram human in the loop, openrouter n8n]
---

# 🚀 Tự động tạo bài đăng X (Twitter) với Gemini & GPT-4 cùng cơ chế Phê duyệt Telegram

Việc duy trì sự hiện diện thường xuyên và chất lượng trên mạng xã hội X (Twitter) đòi hỏi lượng lớn thời gian và sức lực. Tuy nhiên, việc để AI tự động đăng bài hoàn toàn đôi khi mang lại rủi ro về nội dung không chuẩn mực hoặc sai lệch thông tin. 

Giải pháp ở đây là gì? Workflow n8n này sẽ giúp các sếp kết hợp sức mạnh của các mô hình AI đa phương thức (Gemini qua OpenRouter) và AI lý luận đỉnh cao (GPT-4) để tự động sáng tạo nội dung, kết hợp tính năng **Human-in-the-Loop** qua Telegram để kiểm duyệt nội dung trước khi phát sóng thực tế. Toàn bộ quy trình hoàn toàn tự động, không cần code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa sáng tạo nội dung**: Tận dụng AI tối tân nhất (Gemini, GPT-4) qua OpenRouter để viết bài đăng X cực kỳ bén và bắt nhịp xu hướng.
- **Tích hợp tìm kiếm thông minh**: Sử dụng công cụ tìm kiếm tích hợp để nội dung luôn cập nhật thông tin mới nhất.
- **Kiểm soát tuyệt đối (Human-in-the-Loop)**: AI viết nháp, gửi trực tiếp qua Telegram để các sếp bấm nút duyệt, chỉnh sửa hoặc từ chối.
- **Tiết kiệm 90% thời gian**: Không còn phải vắt óc nghĩ ý tưởng hay lo lắng AI "nói cùn" đăng lung tung lên mạng xã hội.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản OpenRouter**: Cung cấp API Key để sử dụng các mô hình Gemini và GPT-4.
- **Tài khoản Telegram & Bot**: Tạo sẵn một Telegram Bot (thông qua BotFather) để nhận thông báo và tương tác duyệt bài.
- **Tài khoản X (Twitter Developer Account)**: Để cấp quyền cho n8n tự động đăng bài sau khi được duyệt.
- **Tavily API**: Dùng cho công cụ tìm kiếm thông tin bài viết (nếu sử dụng tính năng tra cứu dữ liệu).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ thư viện n8n chính thức (link gốc: `https://n8n.io/workflows/5625`), sau đó vào giao diện n8n chọn **Add workflow** -> **Import from File** hoặc copy và dán trực tiếp đoạn JSON vào workspace.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống mượt mà trơn tru, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Telegram_Trigger & Request Feedback**: Kết nối với tài khoản Telegram của các sếp bằng cách điền Bot Token. Node này chịu trách nhiệm nhận lệnh hoặc gửi bản nháp bài viết kèm các nút duyệt (Approve/Reject/Revision).
- **Text Classifier & Revision Agent**: Các agent AI chịu trách nhiệm phân loại phản hồi của các sếp (nếu sếp yêu cầu sửa bài) và tiến hành viết lại theo đúng ý đồ.
- **X Post Agent & Set Post**: Cấu hình các agent sinh nội dung chính dựa trên mô hình ngôn ngữ lớn.
- **2.0 Flash & GPT 4.1 (OpenRouter LM Chat)**: Nhập OpenRouter API Key của sếp vào đây để kích hoạt các model Gemini 2.0 Flash và GPT-4.
- **Tavily Search**: Điền API Key của Tavily để Agent có khả năng search web cập nhật tin tức nóng hổi.
- **X Post (Twitter Node)**: Kết nối tài khoản Twitter cá nhân/doanh nghiệp để workflow có quyền publish bài viết khi nhận được lệnh `Approved`.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để test thử nghiệm gửi yêu cầu qua Telegram.
- Kiểm tra xem Telegram Bot có gửi tin nhắn kèm nội dung nháp về máy hay không.
- Nếu mọi thứ hoạt động chuẩn chỉnh, bật công tắc **Active** góc trên cùng bên phải để chạy nền 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh phân phối**: Không chỉ đăng lên X, các sếp có thể nhân bản nhánh cuối để đẩy bài viết đã duyệt sang LinkedIn, Facebook Page hoặc nhóm Telegram cùng lúc.
- **Lưu trữ lịch sử**: Thêm node Google Sheets hoặc Airtable để lưu lại toàn bộ các bài viết đã được AI tạo và trạng thái duyệt để tiện xem lại báo cáo hiệu suất nội dung.
- **Tùy biến Persona cho AI**: Chỉnh sửa System Prompt trong các Agent AI để định hình giọng văn (Tone of Voice) phù hợp với thương hiệu cá nhân hoặc doanh nghiệp của các sếp.

### 📌 Kết luận
Ứng dụng AI vào sáng tạo nội dung mạng xã hội chưa bao giờ dễ dàng và an toàn đến thế nhờ sự kết hợp của LLM đỉnh cao và cơ chế kiểm duyệt trực tiếp qua Telegram. Hãy "lên đồ" ngay cho hệ thống n8n của các sếp để tối ưu hóa hiệu suất làm social media ngay hôm nay!