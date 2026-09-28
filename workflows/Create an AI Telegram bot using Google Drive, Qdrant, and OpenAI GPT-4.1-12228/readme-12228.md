---
title: "🤖 Tự Động Hóa Bot Telegram AI Cực Năng: Tích Hợp Google Drive + Qdrant + GPT-4.1 (Không Cần Code)"
description: "Workflow này tự động hóa việc tạo bot Telegram thông minh với cơ sở tri thức từ Google Drive, lưu trữ vector bằng Qdrant và sử dụng GPT-4.1 fine-tuned để trả lời câu hỏi chuyên sâu. Giúp các sếp tiết kiệm thời gian và nâng cao hiệu suất công việc 24/7."
slug: "tay-dong-hoa-bot-telegram-ai-google-drive-qdrant-gpt-4-1"
tags: [n8n, automation, ai-bot, google-drive, qdrant, openai, telegram-bot, no-code]
keywords: [tự động hóa bot telegram, n8n workflow ai, google drive automation, qdrant vector database, gpt-4.1 fine-tuned, chatbot doanh nghiệp]
---

# 🚀 **Tạo Bot Telegram AI Tự Động Hóa: Từ Google Drive → Qdrant → GPT-4.1 (Không Cần Code)**

Hiện nay, các sếp và doanh nghiệp thường phải mất nhiều thời gian để tổng hợp, xử lý và trả lời các câu hỏi liên quan đến tài liệu nội bộ. Thay vì phải tra cứu thủ công trên Google Drive hoặc nhớ các thông tin quan trọng, **workflow này tự động hóa toàn bộ quy trình** bằng cách:
- **Tự động tải và xử lý** tất cả tài liệu mới từ Google Drive.
- **Tạo cơ sở tri thức AI** bằng Qdrant (vector database) để lưu trữ và tìm kiếm thông tin nhanh chóng.
- **Tạo bot Telegram thông minh** trả lời câu hỏi dựa trên tri thức đã tích lũy, sử dụng **GPT-4.1 fine-tuned** (mô hình AI được huấn luyện riêng cho doanh nghiệp).
- **Lưu lịch sử hội thoại** riêng cho từng người dùng, đảm bảo tính cá nhân hóa và chính xác.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tra cứu thủ công trên Google Drive hoặc nhớ thông tin quan trọng.
- **Trả lời chính xác và nhanh chóng**: Bot sử dụng tri thức từ tài liệu doanh nghiệp để trả lời các câu hỏi chuyên sâu.
- **Hoạt động 24/7**: Workflow tự động xử lý và cập nhật tri thức liên tục.
- **Cá nhân hóa**: Lưu lịch sử hội thoại riêng cho từng người dùng, giúp bot hiểu rõ hơn về yêu cầu của từng cá nhân.
- **Tích hợp AI tiên tiến**: Sử dụng **GPT-4.1 fine-tuned** (mô hình AI được huấn luyện riêng) để đảm bảo chất lượng cao.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** (đã cấp quyền OAuth2 cho n8n).
2. **Tài khoản Qdrant** (để lưu trữ vector embeddings).
3. **Tài khoản OpenAI** (để sử dụng GPT-4.1 fine-tuned).
4. **Bot Telegram** (tạo trên @BotFather và cấp quyền cho n8n).
5. **Folder Google Drive**:
   - Một folder **Incoming** (để lưu tài liệu mới cần xử lý).
   - Một folder **Processed** (để lưu tài liệu đã xử lý).
6. **Collection Qdrant**: Tạo một collection để lưu trữ embeddings.
7. **Chat ID Telegram**: ID của chat hoặc người dùng được phép sử dụng bot (tìm bằng cách gửi tin nhắn cho @userinfobot).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### 1. **Import Workflow 📥**
- **Bước 1**: Tải workflow từ [link gốc](https://n8n.io/workflows/12228) hoặc copy JSON từ trang này.
- **Bước 2**: Mở **n8n Editor** và chọn **Import Workflow** (hoặc paste JSON vào).
- **Bước 3**: Chọn **Create New Workflow** và dán JSON vào.

### 2. **Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **2 flow chính**:
- **Flow 1: Xử lý tài liệu từ Google Drive** (tự động tải, chia nhỏ, tạo embeddings và lưu vào Qdrant).
- **Flow 2: Bot Telegram trả lời câu hỏi** (lọc người dùng, tìm kiếm tri thức và trả lời bằng AI).

#### **Cấu hình chi tiết các node quan trọng**:
| **Node**                     | **Yêu cầu cấu hình**                                                                 | **Lưu ý**                                                                                     |
|------------------------------|--------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------|
| **New File Trigger**         | Chọn **Google Drive OAuth2** (credentials: `googleDriveOAuth2Api`).                   | Chọn folder **Incoming** để theo dõi.                                                          |
| **Download File**            | Chọn **Google Drive OAuth2** (credentials: `googleDriveOAuth2Api`).                   | Chọn **Operation: Download**.                                                                  |
| **Move to Processed Folder** | Chọn **Google Drive OAuth2** (credentials: `googleDriveOAuth2Api`).                   | Chọn folder **Processed** để di chuyển file sau khi xử lý.                                    |
| **Load Document Data**       | Không cần cấu hình thêm.                                                            | Node này tự động tải dữ liệu từ file đã tải xuống.                                           |
| **Split Text into Chunks**  | Chọn **RecursiveCharacterTextSplitter** (mặc định).                                 | Chia văn bản thành các chunk nhỏ để dễ xử lý.                                                |
| **Insert into Qdrant**        | Chọn **Qdrant API** (credentials: `qdrantApi`).                                       | Điền **Collection Name** (tên collection đã tạo trên Qdrant).                                |
| **Telegram Message Trigger** | Chọn **Telegram API** (credentials: `telegramApi`).                                   | Chọn **Chat ID** của bot Telegram.                                                            |
| **Filter Authorized User**   | Điền **Chat ID** của người dùng được phép sử dụng bot (tìm bằng @userinfobot).     | Chỉ cho phép người dùng đã được cấp quyền truy cập.                                          |
| **OpenAI Embeddings**        | Chọn **OpenAI API** (credentials: `openAiApi`).                                        | Chọn mô hình embeddings (mặc định là `text-embedding-ada-002`).                               |
| **AI Agent1**                | Chọn **System Prompt** (mô tả nhiệm vụ của bot).                                      | Thay đổi prompt để tùy chỉnh tính cách và chuyên môn của bot.                                |
| **OpenAI Chat Model1**       | Chọn **OpenAI API** (credentials: `openAiApi`).                                        | Chọn mô hình **`ft:gpt-4.1-2025-04-14:aimagine:adept3:CrV9Ir4p`** (fine-tuned).                |
| **Qdrant Knowledge Base**    | Chọn **Qdrant API** (credentials: `qdrantApi`).                                       | Chọn **Collection Name** (giống với node **Insert into Qdrant**).                            |
| **Send Response to Telegram**| Chọn **Telegram API** (credentials: `telegramApi`).                                   | Chọn **Chat ID** của bot để gửi trả lời.                                                     |

#### **Cách thêm credentials**:
1. **Google Drive OAuth2**:
   - Tạo credentials mới trong **n8n Credentials** (nút **Credentials** trên thanh công cụ).
   - Chọn **Google Drive OAuth2** và đăng nhập tài khoản Google.
2. **Qdrant API**:
   - Tạo credentials mới với **API Key** từ Qdrant.
3. **OpenAI API**:
   - Tạo credentials mới với **API Key** từ OpenAI.
4. **Telegram API**:
   - Tạo bot trên [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Thêm credentials trong n8n với **Telegram API Token**.

---
### 3. **Kích hoạt ⚡️**
- **Bước 1**: Test run với dữ liệu mẫu:
  - Tải một file vào folder **Incoming** trên Google Drive.
  - Gửi tin nhắn cho bot Telegram để kiểm tra phản hồi.
- **Bước 2**: Bật **Active** workflow.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Tích hợp Slack/Email**:
   - Sử dụng node **Slack** hoặc **Email** để gửi thông báo khi có file mới được xử lý.
2. **Lưu log hoạt động**:
   - Thêm node **Google Sheets** hoặc **Database** để lưu lịch sử hoạt động của bot.
3. **Báo cáo định kỳ**:
   - Sử dụng node **Google Calendar** hoặc **Email** để gửi báo cáo tổng hợp về tri thức đã tích lũy.
4. **Tùy chỉnh mô hình AI**:
   - Thay đổi **system prompt** trong node **AI Agent** để bot phù hợp với ngành nghề cụ thể (VD: y tế, pháp lý, kỹ thuật).
5. **Cập nhật tri thức tự động**:
   - Sử dụng **webhook** từ các hệ thống khác (VD: CRM, ERP) để cập nhật tri thức liên tục.
:::

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa việc quản lý tri thức và tạo bot Telegram thông minh **không cần viết code**. Với sự kết hợp giữa **Google Drive, Qdrant và GPT-4.1 fine-tuned**, bot không chỉ trả lời nhanh chóng mà còn **hiểu sâu về nội bộ doanh nghiệp**, giúp tiết kiệm thời gian và nâng cao hiệu suất công việc.

**Hành động ngay!**
- **Cài đặt n8n trên VPS** để workflow hoạt động 24/7.
- **Tùy chỉnh credentials** và bắt đầu sử dụng bot ngay hôm nay!
- **Mở rộng** với các tính năng như tích hợp Slack, báo cáo tự động hoặc tùy chỉnh mô hình AI.

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%) để tự động hóa mọi lúc, mọi nơi!