---
title: "🤖 **Tự Động Hóa Chatbot RAG Tối Ưu với Supabase + TogetherAI + OpenRouter (Không Cần Code!)**"
description: "Xây dựng một chatbot RAG thông minh tự động hóa từ nội dung Google Docs, tích hợp AI vector search và mô hình ngôn ngữ lớn miễn phí để trả lời câu hỏi chính xác 100% dựa trên dữ liệu nội bộ. Giúp các sếp tiết kiệm thời gian tra cứu và cải thiện trải nghiệm khách hàng/nhân viên."
slug: "chatbot-rag-supabase-togetherai-openrouter"
tags: [n8n, automation, ai-rag, supabase, togetherai, openrouter, no-code, chatbot, vector-search]
keywords: [n8n workflow rag, tự động hóa chatbot doanh nghiệp, supabase embedding, togetherai api, openrouter qwen, chatbot dựa trên dữ liệu nội bộ]
---

# 🚀 **Chatbot RAG Tối Ưu: Trả Lời Câu Hỏi Bằng Dữ Liệu Nội Bộ (Không Cần Code!)**

## **Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp và nhân viên phải mất **giờ đồng hồ** để tra cứu thông tin trong:
- **Google Docs** chứa các tài liệu nội bộ (chính sách, thủ tục, báo cáo).
- **Email** hoặc **Slack** để tìm câu trả lời cho câu hỏi liên quan đến quy trình.
- **Câu hỏi lặp đi lặp lại** về nội dung đã có sẵn nhưng phải tra cứu thủ công.

**Kết quả?** Thời gian bị lãng phí, thông tin không nhất quán, và trải nghiệm khách hàng/nhân viên bị giảm xuống.

---
### **🎯 Giải Pháp: Chatbot RAG Tự Động Hóa**
Workflow này **tự động hóa toàn bộ quy trình** để tạo ra một **chatbot thông minh** có thể:
✅ **Học** từ nội dung Google Docs của bạn.
✅ **Tìm kiếm** thông tin chính xác bằng **vector search** (Supabase).
✅ **Trả lời** câu hỏi **chỉ dựa trên dữ liệu nội bộ** (không bị sai lệch).
✅ **Hoạt động 24/7** trên **Telegram** (hoặc Slack, Discord nếu mở rộng).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)** để tránh giới hạn miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## **🎯 Kết Quả Các Sếp Nhận Được**
### **📌 Lợi Ích Cốt Lõi**
| **Lợi Ích**               | **Giải Thích**                                                                 |
|---------------------------|-------------------------------------------------------------------------------|
| **Tiết kiệm thời gian**    | Không phải tra cứu thủ công trong Google Docs, email hay Slack.              |
| **Trả lời chính xác**     | Chatbot **chỉ trả lời dựa trên dữ liệu nội bộ**, không bị sai lệch.           |
| **Hoạt động liên tục**   | Cài đặt 1 lần, hoạt động **24/7** trên Telegram (hoặc Slack/Discord).         |
| **Cải thiện trải nghiệm**  | Khách hàng/nhân viên **nhận câu trả lời tức thì**, không phải chờ đợi.       |
| **Miễn phí (hoặc rẻ)**    | Sử dụng mô hình **Qwen-3-8B (free)** từ OpenRouter và API TogetherAI miễn phí. |

---

## **🔧 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
### **📌 Tài Khoản & API Keys**
| **Dịch Vụ**               | **Thông Tin Cần Thiết**                                                                 | **Lưu Ý**                                                                 |
|---------------------------|---------------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| **Google Docs**           | - **Service Account** (để đọc file Google Docs).                                      | Cần tạo **Service Account** và cấp quyền cho file Google Docs.           |
| **Supabase**              | - **URL Supabase** và **API Key** (để lưu trữ embedding và vector search).           | Tạo bảng `embed` với schema: `id (UUID), text (text), embedding (vector)`. |
| **TogetherAI**            | - **API Key** (để tạo embedding và chat với mô hình AI).                            | [Đăng ký miễn phí](https://together.ai/) và lấy API Key.                   |
| **OpenRouter**            | - **API Key** (để sử dụng mô hình Qwen-3-8B).                                        | [Đăng ký miễn phí](https://openrouter.ai/) và lấy API Key.                 |
| **Telegram**              | - **Token Bot** (để nhận tin nhắn từ Telegram).                                      | Tạo bot trên [@BotFather](https://t.me/BotFather) và lấy token.           |

### **📄 File Google Docs**
- **Yêu cầu**: File Google Docs chứa **nội dung cần chatbot trả lời** (ví dụ: FAQ, thủ tục, báo cáo).
- **Ví dụ**: File có tên `"Internal_Wiki_Company"` với nội dung như:
  ```
  ### Chính sách Mua Hàng
  1. Quy trình duyệt đơn:
     - Bước 1: Nhận đơn từ bộ phận Marketing.
     - Bước 2: Ký duyệt bởi Giám đốc Kinh Doanh.
     - Bước 3: Xác nhận thanh toán từ bộ phận Tài Chính.
  ```

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/5680](https://n8n.io/workflows/5680).
2. **Nhấn "Import"** trong n8n Editor.
3. **Chọn file JSON** và nhấn **"Import"**.

#### **Cách 2: Copy/Paste JSON**
1. **Mở n8n Editor** và chọn **"Import"** → **"From JSON"**.
2. **Dán JSON** từ [n8n.io/workflows/5680](https://n8n.io/workflows/5680) và nhấn **"Import"**.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này **phân thành 2 phần chính**:
- **Phần 1: Chuẩn bị dữ liệu (chỉ chạy 1 lần)** → Tạo embedding và lưu vào Supabase.
- **Phần 2: Chatbot hoạt động** → Trả lời câu hỏi từ Telegram.

#### **🔹 Phần 1: Chuẩn Bị Dữ Liệu (Chỉ Chạy 1 Lần)**
**Node quan trọng**: `Content for the Training` → `Splitting into Chunks` → `Embedding Uploaded Document` → `Save the embedding in DB`

| **Node**                     | **Cần Chỉnh Sửa Gì?**                                                                 | **Hướng Dẫn**                                                                 |
|------------------------------|---------------------------------------------------------------------------------------|-------------------------------------------------------------------------------|
| **Google Docs**              | - **URL File**: Điền link Google Docs của bạn.                                       | Ví dụ: `https://docs.google.com/document/d/FILE_ID/edit`                     |
| **Code (Splitting into Chunks)** | - **Kích thước chunk**: Mặc định là **1000 ký tự**, có thể điều chỉnh.          | Nếu text quá dài, giảm kích thước (ví dụ: 500 ký tự).                       |
| **TogetherAI (Embedding)**   | - **API Key**: Điền API Key từ TogetherAI.                                           | Tham số mặc định: `model: text-embedding-ada-002` (hoặc mô hình khác).       |
| **Supabase (Save Embedding)** | - **Table Name**: Đảm bảo bảng `embed` đã tạo sẵn.                                | Schema cần có: `id (UUID), text (text), embedding (vector)`.                 |

#### **🔹 Phần 2: Chatbot Hoạt Động**
**Node quan trọng**: `Telegram Trigger` → `When chat message received` → `OpenRouter Chat Model`

| **Node**                     | **Cần Chỉnh Sửa Gì?**                                                                 | **Hướng Dẫn**                                                                 |
|------------------------------|---------------------------------------------------------------------------------------|-------------------------------------------------------------------------------|
| **Telegram Trigger**         | - **Token Bot**: Điền token từ BotFather.                                             | Ví dụ: `123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11`                          |
| **Chat Trigger**             | - **Prompt**: Cần chỉnh sửa để phù hợp với nội dung của bạn.                        | Mặc định: `"Answer the question based on the provided context only."`        |
| **OpenRouter (Qwen-3-8B)**   | - **API Key**: Điền API Key từ OpenRouter.                                           | Mô hình mặc định: `qwen/qwen3-8b:free` (miễn phí).                           |
| **Supabase (Search Embeddings)** | - **RPC Function**: Đảm bảo đã tạo hàm `matchembeddings1` trong Supabase.       | Hàm này sẽ tìm kiếm **top 5 embedding** gần nhất với query của người dùng.   |

---

### **3. Kích Hoạt ⚡️**
#### **Bước 1: Chạy Phần Chuẩn Bị (Chỉ 1 Lần)**
1. **Tắt** node `Telegram Trigger` (nếu muốn).
2. **Chạy workflow** từ node `Content for the Training` đến `Save the embedding in DB`.
3. **Kiểm tra Supabase**: Bảng `embed` sẽ có dữ liệu embedding đã tạo.

#### **Bước 2: Bật Chatbot**
1. **Mở lại** node `Telegram Trigger`.
2. **Gửi tin nhắn** cho bot Telegram (ví dụ: `@YourBotName`).
3. **Test câu hỏi**:
   - **Câu hỏi tốt**: *"Quy trình duyệt đơn mua hàng như thế nào?"*
   - **Câu trả lời**: Chatbot sẽ trả lời **chỉ dựa trên nội dung Google Docs** của bạn.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **1. Mở Rộng Sang Slack/Discord**
- Thay thế `telegramTrigger` bằng `slackTrigger` hoặc `discordTrigger`.
- Cần tạo **webhook** từ Slack/Discord và cấu hình trong node.

### **2. Lưu Log Hoạt Động**
- Thêm node `stickyNote` để **ghi lại lịch sử câu hỏi-trả lời**.
- Có thể kết nối với **Google Sheets** để lưu dữ liệu dài hạn.

### **3. Cập Nhật Dữ Liệu Tự Động**
- Sử dụng **n8n Scheduler** để **tự động cập nhật embedding** khi Google Docs thay đổi.
- Ví dụ: Chạy workflow hàng ngày để **cập nhật nội dung mới**.

### **4. Tối Ưu Hóa Prompt**
- Chỉnh sửa **prompt** trong `chainLlm` để:
  - **Trả lời ngắn gọn** (ví dụ: `"Trả lời trong 2 câu."`).
  - **Tránh trả lời ngoài phạm vi** (ví dụ: `"Chỉ sử dụng thông tin từ context."`).

### **5. Sử Dụng Mô Hình AI Miễn Phí Khác**
- Thay `qwen/qwen3-8b:free` bằng mô hình khác từ OpenRouter (ví dụ: `mistral/mistral-7b-instruct`).
- **Lưu ý**: Một số mô hình miễn phí có **giới hạn request**.

---

## **📌 Kết Luận: Áp Dụng Ngay Để Tiết Kiệm Thời Gian!**
Chatbot RAG này **giải phóng bạn khỏi việc tra cứu thủ công**, giúp:
✔ **Tiết kiệm hàng giờ** mỗi tuần.
✔ **Cải thiện trải nghiệm** cho khách hàng/nhân viên.
✔ **Duy trì tính nhất quán** trong thông tin.

**Bước đầu tiên**: [Tải workflow](https://n8n.io/workflows/5680) và **cài đặt ngay** trên VPS của bạn!

---
### **🚀 Bắt Đầu Hôm Nay!**
👉 [Tải workflow](https://n8n.io/workflows/5680)
👉 [Đăng ký VPS miễn phí](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N**)

**Câu hỏi?** Để lại comment bên dưới hoặc liên hệ tôi qua Telegram! 🚀