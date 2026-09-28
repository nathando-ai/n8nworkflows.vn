---
title: "🤖 **Tự Động Xử Lý Nhiều File Tệp Trong Telegram Với Gemini AI + Cơ Sở Dữ Liệu PostgreSQL**"
description: "Workflow tự động hóa hoàn toàn không cần code để nhận, phân tích, nhóm và lưu trữ các file đa dạng (PDF, Excel, hình ảnh, video, âm thanh, văn bản...) từ Telegram vào cơ sở dữ liệu PostgreSQL, đồng thời sử dụng Gemini AI để tổng hợp thông tin và trả lời tự động cho người dùng. Giúp doanh nghiệp tiết kiệm thời gian xử lý 1000+ file/ngày mà không cần nhân viên chuyên môn."
slug: "tự-dộng-xử-ly-file-telegram-gemini-postgres"
tags: [n8n, automation, no-code, telegram-bot, gemini-ai, postgresql, multimodal-ai, support-chatbot]
keywords: [n8n workflow telegram, tự động hóa xử lý file, gemini ai trong n8n, postgresql với n8n, chatbot hỗ trợ đa phương tiện, tự động hóa doanh nghiệp]
---

# 🚀 **Tự Động Xử Lý File Tệp Telegram Với Gemini AI + PostgreSQL: Giải Pháp "Không Cần Code" Cho Doanh Nghiệp**

## **💡 Giới Thiệu: Tại Sao Các Sếp Cần Workflow Này?**
Hiện nay, khi doanh nghiệp nhận được hàng trăm, ngàn file từ khách hàng qua Telegram (PDF, Excel, hình ảnh, video, âm thanh...), việc xử lý thủ công không chỉ tốn thời gian mà còn dễ xảy ra lỗi. Các sếp phải:
- **Tìm kiếm và lưu trữ** file một cách rải rác trên nhiều ứng dụng.
- **Phân tích nội dung** từng file để tổng hợp thông tin (ví dụ: hợp đồng, báo cáo, hình ảnh sản phẩm).
- **Trả lời khách hàng** với thông tin chính xác và cá nhân hóa, nhưng lại mất nhiều giờ mỗi ngày.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động nhận và phân loại** tất cả file từ Telegram (hình ảnh, video, âm thanh, văn bản, tài liệu).
✅ **Xử lý đa phương tiện** với **Gemini AI** (Google) để:
   - Trích xuất nội dung từ PDF, Excel, hình ảnh, video.
   - Phân tích âm thanh (gọi điện, tin nhắn âm thanh) thành văn bản.
   - Tổng hợp thông tin từ nhiều file cùng một lúc.
✅ **Lưu trữ hệ thống** vào **PostgreSQL** với cấu trúc logic để quản lý nhóm file (ví dụ: một hợp đồng có nhiều trang PDF).
✅ **Trả lời tự động** cho khách hàng với thông tin được tổng hợp, **không cần nhân viên hỗ trợ 24/7**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng. N8n chạy tốt nhất trên máy chủ có:
- **RAM ≥ 2GB** (đối với workflow có nhiều file đồng thời).
- **CPU 2 nhân trở lên** (để xử lý AI và PostgreSQL đồng thời).

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**).
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này).

*Lưu ý:* Nếu dùng n8n.cloud (miễn phí), workflow có thể bị giới hạn về số lượng file đồng thời và thời gian xử lý.
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10-20 giờ/ngày** cho đội ngũ hỗ trợ khách hàng.
- **Chính xác 100%** trong việc trích xuất và tổng hợp thông tin từ file.
- **Cá nhân hóa phản hồi** cho từng khách hàng dựa trên nội dung file.
- **Hoạt động liên tục** 24/7, không cần nhân viên trực ca.
- **Quản lý file hiệu quả** với cơ sở dữ liệu PostgreSQL, dễ dàng tra cứu và phân tích sau này.
- **Giảm chi phí** so với việc thuê thêm nhân viên xử lý file.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
#### **1. Tài Khoản & API Keys**
| **Dịch Vụ**          | **Thông Tin Cần Thiết**                                                                 | **Lưu Ý**                                                                 |
|----------------------|----------------------------------------------------------------------------------------|----------------------------------------------------------------------------|
| **Telegram Bot**     | - Token API từ [@BotFather](https://t.me/BotFather)                                      | Cần cấp quyền `getMessages`, `sendMessages`, `sendDocument`.              |
| **Google Gemini API**| - API Key từ [Google Cloud Console](https://console.cloud.google.com/)                 | Chọn dịch vụ **Generative AI API** và **Vertex AI**.                     |
| **PostgreSQL**       | - Thông tin kết nối (Host, Port, Database Name, Username, Password)                   | Cần tạo 3 bảng: `media_group`, `media_queue`, `chat_histories` (xem hướng dẫn dưới đây). |
| **N8n Self-Hosted**  | - Máy chủ VPS (gợi ý cấu hình trên)                                                    | N8n phiên bản **v1.0+** (cập nhật node `@n8n/n8n-nodes-langchain`).         |

#### **2. Cấu Trúc Cơ Sở Dữ Liệu PostgreSQL**
Workflow yêu cầu **3 bảng** được tạo trước:
```sql
-- Bảng 1: media_group (lưu thông tin nhóm file)
CREATE TABLE media_group (
    id SERIAL PRIMARY KEY,
    media_group_id VARCHAR(255) UNIQUE,
    chat_id VARCHAR(255),
    description TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Bảng 2: media_queue (để trigger xử lý nhóm file)
CREATE TABLE media_queue (
    id SERIAL PRIMARY KEY,
    media_group_id VARCHAR(255) UNIQUE,
    chat_id VARCHAR(255),
    captions TEXT,
    processed BOOLEAN DEFAULT FALSE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Bảng 3: chat_histories (lưu lịch sử chat với AI)
CREATE TABLE chat_histories (
    id SERIAL PRIMARY KEY,
    chat_id VARCHAR(255),
    message TEXT,
    response TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/7455](https://n8n.io/workflows/7455) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/7455) và paste vào **Create Workflow** → **Import JSON**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này **phức tạp** với **87 node**, nhưng chỉ cần chú ý đến các phần sau:

##### **A. Cấu Hình Credentials (Tài Khoản)**
| **Node**                     | **Credentials Cần Chỉnh**       | **Hướng Dẫn**                                                                 |
|------------------------------|----------------------------------|--------------------------------------------------------------------------------|
| **Telegram Trigger**         | `telegramApi`                    | Điền **Token Bot** từ `@BotFather`.                                         |
| **PostgreSQL Nodes**         | `postgres`                       | Điền thông tin kết nối PostgreSQL (Host, Port, Database, Username, Password). |
| **Google Gemini Nodes**       | `googlePalmApi`                  | Điền **API Key** từ Google Cloud Console.                                    |
| **Agent (LangChain)**        | `postgres` (memory)              | Chọn **Postgres Chat Memory** để lưu lịch sử chat.                          |

##### **B. Cấu Hình Cấu Trúc Dữ Liệu**
Workflow sử dụng **PostgreSQL Trigger** để theo dõi bảng `media_queue`. Các sếp cần:
1. **Kiểm tra bảng `media_queue`** đã được tạo như hướng dẫn trên.
2. **Cập nhật query trong node `Media_queue Trigger`** (nếu cần):
   ```json
   {
     "operation": "select",
     "query": "SELECT * FROM media_queue WHERE processed = FALSE LIMIT 1"
   }
   ```

##### **C. Cấu Hình AI Agent (Purple Section)**
- **Không có prompt cố định**: Workflow tự động truyền dữ liệu theo định dạng nhất quán vào AI.
- **Định dạng đầu vào AI**:
  ```json
  {
    "captions": "Nội dung từ Telegram (nếu có)",
    "files": [
      {
        "name": "file1.pdf",
        "type": "pdf",
        "description": "Nội dung trích xuất từ PDF"
      },
      {
        "name": "image.jpg",
        "type": "image",
        "description": "Mô tả từ Gemini AI"
      }
    ]
  }
  ```
- **Nếu muốn thay đổi AI model**: Thay thế node `lmChatGoogleGemini` bằng model khác (ví dụ: OpenAI).

##### **D. Cấu Hình Telegram Bot**
- **Cấp quyền cho Bot**:
  - Mở chat với Bot → Gửi `/setcommands` với danh sách lệnh:
    ```
    /start - Bắt đầu chat
    /help - Hỗ trợ
    ```
- **Test Bot**: Gửi tin nhắn đến Bot để kiểm tra:
  ```
  /start
  ```
  Bot sẽ trả lời và bắt đầu xử lý file.

#### **3. Kích Hoạt ⚡️**
1. **Test Run với dữ liệu mẫu**:
   - Gửi một file PDF, Excel hoặc hình ảnh đến Bot Telegram.
   - Kiểm tra **n8n Dashboard** để xem workflow có chạy đúng không.
2. **Bật Active workflow**:
   - Đảm bảo tất cả **credentials** đã được cấu hình.
   - Chuyển trạng thái workflow từ **Inactive** → **Active**.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
#### **1. Kết Nối Với Slack/Telegram Của Doanh Nghiệp**
- Thay vì chỉ trả lời qua Telegram, các sếp có thể:
  - **Gửi báo cáo định kỳ** về Slack với tổng hợp file mới nhất.
  - **Lưu log** vào PostgreSQL để phân tích sau này.
  *Cách thực hiện:* Thêm node **Slack** hoặc **Telegram** vào cuối workflow để gửi thông báo.

#### **2. Tự Động Xóa File Sau Xử Lý**
- Sau khi AI xử lý xong, các sếp có thể **xóa file tạm** trên Telegram để tiết kiệm dung lượng.
  *Cách thực hiện:* Thêm node **Telegram → Delete Message** sau khi hoàn tất xử lý.

#### **3. Thêm Hệ Thống Nhận Dạng File Tự Động**
- Nếu muốn **chỉ xử lý file nhất định** (ví dụ: chỉ PDF, Excel), thêm node **Filter** trước khi gửi vào AI.
  *Cách thực hiện:* Sử dụng node **Set** để kiểm tra `file.type` và chỉ cho phép file cần thiết.

#### **4. Tích Hợp Với Google Drive/Dropbox**
- Thay vì chỉ lưu vào PostgreSQL, các sếp có thể **tải file lên Google Drive** sau khi xử lý.
  *Cách thực hiện:* Thêm node **Google Drive** vào cuối workflow.

#### **5. Tạo Báo Cáo Hàng Ngày**
- Sử dụng **n8n Scheduler** để chạy workflow vào mỗi sáng và gửi báo cáo tổng hợp về Slack/Email.
  *Cách thực hiện:*
  1. Tạo một **Manual Trigger** mới.
  2. Thêm node **Schedule** để chạy hàng ngày.
  3. Thêm node **Aggregate** để tổng hợp dữ liệu từ PostgreSQL.
  4. Gửi báo cáo qua **Slack** hoặc **Email**.

---
### 📌 **Kết Luận: Áp Dụng Ngay Để Tiết Kiệm Thời Gian & Tăng Doanh Thu**
Workflow này là **giải pháp hoàn hảo** cho các doanh nghiệp cần:
✔ **Tự động hóa xử lý file** từ Telegram một cách **không cần code**.
✔ **Tích hợp AI Gemini** để phân tích nội dung file một cách chính xác.
✔ **Quản lý file hiệu quả** với cơ sở dữ liệu PostgreSQL.
✔ **Tiết kiệm chi phí** so với việc thuê thêm nhân viên.

**Hành động ngay:**
1. **Cài đặt n8n trên VPS** (gợi ý cấu hình trên).
2. **Import workflow** và cấu hình credentials.
3. **Test với 1-2 file mẫu** để đảm bảo hoạt động.
4. **Bật Active** và bắt đầu tự động hóa!

---
**💬 Cần hỗ trợ thêm?**
- **Hỏi đáp trên [Community n8n](https://community.n8n.io/)**.
- **Mua VPS chuyên dụng** từ [TinoHost](https://tino.vn) hoặc [BNIX](https://my.bnix.one) với mã giảm giá đã cung cấp.
- **Tư vấn cá nhân hóa** workflow cho doanh nghiệp: Liên hệ qua [email](mailto:support@n8n.io).

---
**🚀 Chúc các sếp thành công với workflow tự động hóa này!** 🚀