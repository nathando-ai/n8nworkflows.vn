---
title: "🚀 Tự Động Hóa Xử Lý Batch Requests OpenAI Với Queue FIFO Supabase - Giảm Chi Phí AI 50%"
description: "Workflow này tự động hóa việc xử lý hàng loạt yêu cầu OpenAI Batch API với chi phí thấp hơn 50% so với API tiêu chuẩn, đồng thời sử dụng Supabase làm hàng đợi FIFO (First-In-First-Out) để theo dõi và quản lý batch jobs một cách hiệu quả. Phù hợp cho các startup, doanh nghiệp AI hoặc nhà phát triển cần xử lý lượng lớn dữ liệu text."
slug: "tieu-dong-hoa-openai-batch-supabase"
tags: [n8n, automation, openai, ai-summarization, supabase, postgres, no-code, api-automation]
keywords: [n8n workflow openai batch, tự động hóa xử lý batch openai, supabase postgres fifo queue, giảm chi phí ai, xử lý hàng loạt prompt openai]
---

# 🚀 **Tự Động Hóa Xử Lý Batch Requests OpenAI Với Queue FIFO Supabase**

## **Giới Thiệu**
Bạn đã bao giờ phải xử lý **hàng trăm hoặc ngàn yêu cầu OpenAI** một lúc mà không muốn bị "bị chặn" do giới hạn API hoặc chi phí skyrocket? Hoặc bạn đang muốn **tối ưu hóa chi phí** khi sử dụng các mô hình LLM như GPT-4, GPT-5 Mini với lượng dữ liệu lớn?

Workflow này là **giải pháp hoàn hảo** cho các sếp và nhà phát triển muốn:
✅ **Giảm chi phí OpenAI** lên đến **50%** so với API tiêu chuẩn (thông qua Batch API).
✅ **Xử lý hàng loạt yêu cầu** một cách **liên tục và tự động**, không cần code.
✅ **Theo dõi và quản lý batch jobs** một cách **an toàn và hiệu quả** bằng Supabase + Postgres.
✅ **Đảm bảo thứ tự FIFO** (First-In-First-Out) để tránh tình trạng "đua nhau" trong xử lý.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này **chạy 24/7** mà không gặp vấn đề về ổn định, các sếp nên **self-host n8n** trên VPS chuyên dụng.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ xử lý nhanh cho Batch API)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Giảm chi phí OpenAI** lên đến **50%** so với API tiêu chuẩn (thông qua Batch API).
- **Xử lý hàng loạt yêu cầu** một cách **liên tục và tự động**, không cần code.
- **Theo dõi và quản lý batch jobs** một cách **an toàn và hiệu quả** bằng Supabase + Postgres.
- **Đảm bảo thứ tự FIFO** (First-In-First-Out) để tránh tình trạng "đua nhau" trong xử lý.
- **Tích hợp hoàn toàn với n8n**, không cần viết một dòng code nào.
- **Lưu trữ kết quả** một cách **cá nhân hóa** và dễ truy cập.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** với **API Key** và **tài khoản tiền điện tử** (để thanh toán cho Batch API).
2. **Supabase Project** (miễn phí hoặc paid) với:
   - **Table `openai_batches`** (cấu trúc sẽ được hướng dẫn sau).
   - **Credentials Supabase** (URL, API Key, Service Role Key).
3. **PostgreSQL Database** (nếu không dùng Supabase Database, nhưng Supabase đã bao gồm nó).
4. **n8n Self-hosted** (trên VPS) để chạy workflow 24/7.
5. **Dữ liệu đầu vào**:
   - Mảng `inputs` (một danh sách các text cần xử lý).
   - `systemPrompt` (câu lệnh hệ thống cho OpenAI).

---

## 🚀 **Cách Import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Workflow này đã được **tạo sẵn trên n8n.io** với ID **13238**. Các sếp có thể:
- **Tải JSON** từ [đây](https://n8n.io/workflows/13238) và import vào n8n Editor.
- **Copy JSON** và dán vào **Import Workflow** trong n8n.

:::note[Lưu ý]
Nếu các sếp **self-host n8n**, hãy **không sử dụng phiên bản demo** của n8n.io, mà phải **tải workflow từ GitHub** hoặc **copy JSON** từ trang n8n.io.
:::

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **📌 Phase 1: Submit Batch (Gửi yêu cầu lên OpenAI)**
1. **Node "Start (mock data)"**:
   - Thay thế **mock data** bằng **dữ liệu thực tế**:
     ```json
     {
       "systemPrompt": "You are a helpful assistant. Summarize the following text in 3 bullet points.",
       "inputs": [
         "Text 1 to summarize...",
         "Text 2 to summarize...",
         "Text 3 to summarize..."
       ]
     }
     ```
   - **Lưu ý**: Nếu `inputs` quá dài, OpenAI Batch API sẽ **tách thành nhiều batch** tự động.

2. **Node "Convert to batch requests in .jsonl" (Code Node)**:
   - **Không cần chỉnh sửa** nếu muốn sử dụng cấu trúc mặc định.
   - Nếu muốn **thay đổi mô hình OpenAI**, hãy chỉnh sửa trong **Code Node**:
     ```javascript
     // Thay đổi từ `gpt-5-mini` sang `gpt-4` hoặc `gpt-3.5-turbo`
     const model = "gpt-5-mini"; // <-- Thay đổi ở đây
     ```

3. **Node "Call Files API" & "Call Batch API"**:
   - **Đảm bảo đã thêm credentials `openAiApi`** (API Key OpenAI).
   - **Kiểm tra lại** để tránh lỗi `401 Unauthorized`.

4. **Node "Create a row in batch table" (Supabase)**:
   - **Không cần chỉnh sửa** nếu đã tạo table `openai_batches` theo hướng dẫn sau.

---

#### **📌 Phase 2: Poll & Retrieve (Lấy kết quả từ OpenAI)**
1. **Node "Cron Job (5 mins)"**:
   - **Không cần chỉnh sửa** nếu muốn **kiểm tra status mỗi 5 phút**.
   - Nếu muốn **kiểm tra thường xuyên hơn**, hãy thay đổi `*/5 * * * *` thành `*/1 * * * *` (mỗi phút).

2. **Node "Get the earliest uncompleted batch" (Postgres)**:
   - **Đảm bảo query lấy batch chưa hoàn thành**:
     ```sql
     SELECT * FROM openai_batches WHERE batch_status != 'completed' ORDER BY created_at ASC LIMIT 1;
     ```
   - **Nếu muốn strict FIFO**, hãy **không bỏ `LIMIT 1`**.

3. **Node "Update status" & "Update status and result" (Supabase)**:
   - **Không cần chỉnh sửa** nếu đã cấu hình table `openai_batches` đúng.
   - **Lưu ý**: Nếu kết quả quá lớn, OpenAI sẽ **tải về dưới dạng file**, nên cần **decode base64** (đã được xử lý tự động trong workflow).

---

### **3. Kích hoạt ⚡️**
1. **Test Run với dữ liệu mẫu**:
   - Chạy **manual trigger** để kiểm tra **Phase 1** (Submit Batch).
   - Chờ **5 phút** để **Cron Job** chạy và lấy kết quả.
   - Kiểm tra **table `openai_batches`** trong Supabase để xem **status** và **result**.

2. **Bật Active workflow**:
   - Sau khi **test thành công**, hãy **bật Active** để workflow chạy tự động.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Tối ưu hóa chi phí OpenAI**
- **Sử dụng mô hình rẻ hơn** như `gpt-5-mini` thay vì `gpt-4`.
- **Tách batch lớn** thành nhiều batch nhỏ (nếu OpenAI cho phép).

### **2. Lưu trữ kết quả một cách hiệu quả**
- **Thêm node `httpRequest`** để **gửi kết quả về Slack/Telegram** khi hoàn thành.
- **Tạo một dashboard** trong Supabase để **theo dõi tất cả batch jobs**.

### **3. Xử lý lỗi tự động**
- **Thêm node `if`** để **kiểm tra lỗi OpenAI** và **gửi thông báo Slack** nếu batch thất bại.
- **Sử dụng `noOp`** để **log lỗi** vào một file hoặc table khác.

### **4. Kết hợp với các công cụ khác**
- **N8n + Zapier**: Nếu muốn **gửi kết quả vào Google Sheets/Notion**.
- **N8n + Airtable**: **Lưu trữ kết quả** một cách dễ dàng.

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Giảm chi phí OpenAI** lên đến **50%**.
✔ **Xử lý hàng loạt yêu cầu** một cách **tự động và an toàn**.
✔ **Theo dõi và quản lý batch jobs** một cách **cá nhân hóa**.

**Hãy thử ngay và tiết kiệm hàng nghìn USD cho doanh nghiệp!** 🚀

---
**🔗 [Tải workflow từ n8n.io](https://n8n.io/workflows/13238)**
**📌 [Hướng dẫn tạo table `openai_batches` trong Supabase](#setup-supabase-table)**