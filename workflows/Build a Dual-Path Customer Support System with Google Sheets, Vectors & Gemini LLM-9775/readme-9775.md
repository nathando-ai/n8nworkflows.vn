---
title: "🤖 Hệ Thống Hỗ Trợ Khách Hàng Song Đường Lối: Tự Động Hóa Trả Lời FAQ + LLM Gemini (Google Sheets + Vector DB)"
description: "Workflow tự động hóa hỗ trợ khách hàng thông minh với 2 đường lối: Trả lời nhanh từ FAQ (Google Sheets) hoặc sử dụng LLM Gemini để giải đáp câu hỏi phức tạp. Giảm thời gian phản hồi 90% và nâng cao trải nghiệm khách hàng."
slug: "he-thong-ho-tro-khach-hang-song-duong-li-gemini"
tags: [n8n, automation, no-code, google-sheets, gemini-llm, vector-database, chatbot]
keywords: [n8n workflow hỗ trợ khách hàng, tự động hóa FAQ, Gemini API n8n, vector store tự động hóa, chatbot doanh nghiệp]
---

# 🚀 **Hệ Thống Hỗ Trợ Khách Hàng Song Đường Lối: Tích Hợp FAQ + LLM Gemini**

## **🔥 Giải pháp cho doanh nghiệp đang mắc phải:**
- **Thời gian phản hồi chậm:** Đội ngũ hỗ trợ phải tra cứu FAQ thủ công, mất trung bình **3-5 phút/câu hỏi**.
- **Trải nghiệm khách hàng không đồng nhất:** Một số câu hỏi phức tạp không được trả lời chính xác, dẫn đến **tỷ lệ phản hồi thấp** và **sự thất vọng**.
- **Không tối ưu hóa nguồn lực:** Nhân viên phải xử lý **lặp đi lặp lại** những câu hỏi cơ bản, trong khi bỏ qua những vấn đề cần tư vấn chuyên sâu.

**Workflow này giải quyết tất cả đó bằng cách:**
✅ **Tự động hóa 100%:** Không cần code, chỉ cần **Google Sheets** và **API Gemini** (Google).
✅ **Song đường lối thông minh:** Trả lời **FAQ từ cơ sở dữ liệu** (nếu câu hỏi đơn giản) hoặc **sử dụng LLM Gemini** (nếu câu hỏi phức tạp).
✅ **Tăng tốc độ phản hồi:** Giảm thời gian xử lý từ **5 phút → dưới 1 giây**.
✅ **Cải thiện chất lượng:** Trả lời **cá nhân hóa** và **chính xác cao** nhờ vector database.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7** và **mở rộng khả năng**, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Giảm **90% công việc thủ công** của đội hỗ trợ.
- **Trả lời chính xác:** Sử dụng **vector database** để tìm câu trả lời gần nhất trong cơ sở dữ liệu FAQ.
- **Cá nhân hóa:** LLM Gemini **hiểu ngữ cảnh** và trả lời **một cách tự nhiên**, giống như một chuyên viên hỗ trợ.
- **Hoạt động liên tục:** Workflow **chạy 24/7** trên n8n self-hosted, không phụ thuộc vào thời gian làm việc.
- **Dễ mở rộng:** Thêm **Slack/Telegram** hoặc **email** để khách hàng tương tác dễ dàng.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google Sheets** (để lưu trữ FAQ và cơ sở dữ liệu tri thức).
✔ **API Key HuggingFace** (để tạo **embeddings** từ câu hỏi).
✔ **API Key Google Gemini (Palm API)** (để sử dụng LLM trả lời).
✔ **Tài khoản n8n** (cài đặt **self-hosted** hoặc dùng **n8n.cloud** miễn phí cho testing).

---
:::note[CHUẨN BỊ CƠ SỞ DỮ LIỆU FAQ]
Workflow cần **1 sheet Google Sheets** với **cấu trúc sau** (cột `Question` và `Answer`):
| Question               | Answer                          |
|------------------------|---------------------------------|
| "Mã giảm giá có hiệu lực bao lâu?" | "Mã giảm giá áp dụng trong 7 ngày từ ngày mua." |
| "Làm sao để hủy đơn hàng?" | "Bạn có thể hủy đơn trong vòng 24h từ khi đặt hàng..." |
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/9775](https://n8n.io/workflows/9775).
- **Nhấn "Import"** trong **n8n Editor** (trang chủ).
- **Hoặc copy/paste** JSON vào **Create Workflow** → **Import from JSON**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow có **2 đường lối chính**, các sếp cần cấu hình kỹ:

##### **A. Cấu hình Google Sheets (FAQ Database)**
1. **Node "Knowledge Database"**:
   - **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước).
   - **Sheet Name**: Điền tên **sheet** chứa FAQ (ví dụ: `FAQ_Database`).
   - **Range**: Điền `Sheet1!A2:B` (giả sử dữ liệu bắt đầu từ hàng 2).

2. **Node "Get Respective Answers"**:
   - **Credentials**: Cùng `googleSheetsOAuth2Api`.
   - **Sheet Name**: Giống như trên.
   - **Range**: `Sheet1!A2:B` (để lấy cả câu hỏi và trả lời).

##### **B. Cấu hình HuggingFace API (Embeddings)**
1. **Node "Embeddings HuggingFace Inference"**:
   - **Credentials**: Chọn `huggingFaceApi` (đã cấu hình trước).
   - **Model**: Chọn `sentence-transformers/all-MiniLM-L6-v2` (mô hình miễn phí tốt cho embeddings).

2. **Node "Embeddings HuggingFace Inference2"**:
   - **Credentials**: Cùng `huggingFaceApi`.
   - **Model**: Giống như trên.

##### **C. Cấu hình Google Gemini (LLM)**
1. **Node "Chat Model"**:
   - **Credentials**: Chọn `googlePalmApi` (đã cấu hình trước).
   - **Model**: Chọn `gemini-pro` (mô hình mạnh nhất hiện tại).
   - **Prompt**: Sử dụng mặc định hoặc tùy chỉnh:
     ```
     You are a customer support assistant. Answer the user's question based on the provided context. If the question is not related to FAQ, provide a detailed and helpful response.
     ```

##### **D. Cấu hình Node "Determine Question Type" (If/Else)**
- **Threshold score**: **Tùy chỉnh** để điều chỉnh độ chính xác:
  - **Nếu score > 0.7**: Trả lời từ FAQ (đường lối 1).
  - **Nếu score ≤ 0.7**: Gửi đến Gemini (đường lối 2).
  - *Lưu ý*: Threshold này phụ thuộc vào **dữ liệu FAQ** của bạn. Thử nghiệm và điều chỉnh!

##### **E. Cấu hình Node "Forward Chat Message" (Merge)**
- **Kết hợp** dữ liệu từ:
  - Câu hỏi của khách hàng (`$json.chatInput`).
  - Trả lời từ FAQ hoặc Gemini (`$json.answer`).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Execute Workflow"** và nhập một **câu hỏi mẫu** (ví dụ: *"Làm sao để đổi trả sản phẩm?"*).
   - Kiểm tra:
     - Nếu câu hỏi trong FAQ → Trả lời tự động.
     - Nếu không → Gemini trả lời chi tiết.

2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật "Active"** để workflow chạy tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết nối với Slack/Telegram**:
   - Thêm **node `n8n-nodes-base.slack`** hoặc **`n8n-nodes-base.telegram`** để khách hàng tương tác dễ dàng.
   - *Cách làm*: Sau node `Forward Chat Message`, thêm node **Slack/Telegram** để gửi tin nhắn.

2. **Lưu log hoạt động**:
   - Thêm **node `n8n-nodes-base.set`** để lưu **lịch sử câu hỏi** vào Google Sheets.
   - *Ưu điểm*: Theo dõi **tần suất câu hỏi** và **cải thiện FAQ**.

3. **Báo cáo tự động hàng tuần**:
   - Sử dụng **node `n8n-nodes-base.email`** để gửi **tóm tắt thống kê** (số câu hỏi, câu hỏi phổ biến) cho team.

4. **Cập nhật FAQ tự động**:
   - Thêm **node `n8n-nodes-base.googleSheets`** để **cập nhật FAQ** khi có thay đổi từ bên ngoài (ví dụ: từ một form feedback).

---

### 📌 **Kết luận**
Workflow này **không chỉ tự động hóa hỗ trợ khách hàng**, mà còn **tối ưu hóa trải nghiệm** bằng cách kết hợp **FAQ + LLM Gemini**. Các sếp có thể:
✅ **Giảm thời gian phản hồi** từ phút sang giây.
✅ **Tăng chất lượng hỗ trợ** nhờ trí tuệ nhân tạo.
✅ **Tiết kiệm chi phí** bằng cách giảm công việc thủ công.

**Bắt đầu ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với dữ liệu thật** và điều chỉnh threshold.
3. **Kết nối với kênh khách hàng** (Slack/Email/Telegram).

**🚀 [Tải workflow ngay](https://n8n.io/workflows/9775) và tự động hóa hỗ trợ khách hàng của bạn!**