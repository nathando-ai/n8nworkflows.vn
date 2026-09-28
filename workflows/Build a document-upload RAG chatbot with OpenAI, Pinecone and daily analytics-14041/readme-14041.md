---
title: "🤖 Tự động hóa Chatbot RAG Tích hợp OpenAI & Pinecone: Tạo Wiki Nội bộ Hiểu Biết + Báo cáo Hàng ngày"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp xây dựng chatbot RAG (Retrieval-Augmented Generation) từ tài liệu PDF/CSV/JSON, tích hợp OpenAI (gpt-4o-mini) và Pinecone để trả lời câu hỏi chính xác từ nội bộ, đồng thời tự động phân tích và gửi báo cáo hàng ngày về hiệu suất sử dụng. Giảm thời gian tìm kiếm thông tin từ 30 phút xuống 0 giây!"
slug: "tự-dộng-hoa-chatbot-rag-openai-pinecone"
tags: [n8n, automation, ai-rag, openai, pinecone, internal-wiki, analytics]
keywords: [n8n workflow rag, tự động hóa chatbot nội bộ, pinecone openai, báo cáo hàng ngày chatbot, vector database, gpt-4o-mini]
---

# 🚀 **Chatbot RAG Tự động hóa: Từ Tài liệu → Trả lời Tự động + Báo cáo Hàng ngày**

## **Nỗi đau của các sếp khi quản lý kiến thức nội bộ**
Hiện nay, nhiều doanh nghiệp vẫn phụ thuộc vào việc tìm kiếm thủ công thông tin trong tài liệu PDF, CSV hay JSON để trả lời câu hỏi của nhân viên. Quá trình này thường mất **30 phút đến 1 giờ** mỗi lần, dễ gây sai sót và không thể theo dõi được hiệu suất sử dụng của tài liệu.

**Workflow này giải quyết:**
✅ **Tự động hóa trả lời câu hỏi** từ tài liệu nội bộ (PDF, CSV, JSON) bằng AI RAG (Retrieval-Augmented Generation).
✅ **Tích hợp OpenAI (gpt-4o-mini) + Pinecone** để lưu trữ và tra cứu thông tin nhanh chóng.
✅ **Báo cáo hàng ngày tự động** về hiệu suất chatbot, tỉ lệ thành công, tài liệu được tham khảo nhiều nhất.
✅ **Không cần code** – chỉ cần cấu hình trên n8n.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Trả lời câu hỏi từ tài liệu chỉ trong **0 giây** thay vì 30 phút.
- **Chính xác 100%**: Chatbot chỉ trả lời dựa trên thông tin từ tài liệu đã tải lên (không tưởng tượng).
- **Báo cáo tự động hàng ngày**: Nhận email tổng hợp về hiệu suất chatbot, tỉ lệ thành công, và tài liệu được tham khảo nhiều nhất.
- **Tích hợp hoàn chỉnh**: Hỗ trợ PDF, CSV, JSON và nhiều định dạng khác.
- **Mở rộng dễ dàng**: Có thể kết nối với Slack/Teams để thông báo kết quả.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI**:
   - API Key từ [OpenAI](https://platform.openai.com/account/api-keys) (đăng ký miễn phí).
   - Model: `gpt-4o-mini` (được cấu hình sẵn trong workflow).

2. **Tài khoản Pinecone**:
   - API Key và Environment từ [Pinecone](https://www.pinecone.io/).
   - **Index Name**: Tên index Pinecone để lưu trữ embeddings (ví dụ: `internal-wiki-index`).
   - **Namespace**: Namespace trong Pinecone (ví dụ: `default`).

3. **Tài khoản Gmail**:
   - Địa chỉ email và mật khẩu (hoặc App Password nếu sử dụng 2FA).
   - Địa chỉ email nhận báo cáo hàng ngày.

4. **n8n Self-hosted**:
   - Workflow này **không chạy được trên n8n Cloud** do yêu cầu tính toán cao (OpenAI + Pinecone).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

5. **Các node bổ sung (nếu cần mở rộng)**:
   - Slack/Telegram Bot (để thông báo kết quả).
   - Google Sheets (để lưu log chi tiết).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/14041](https://n8n.io/workflows/14041) (chọn **Export as JSON**).
2. Trên n8n Editor, nhấn **Import** và chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ JSON từ [n8n.io/workflows/14041](https://n8n.io/workflows/14041).
2. Trên n8n Editor, nhấn **Import** → **Paste JSON** và dán vào.
3. Chọn **Create new workflow** và nhấn **Import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình Workflow Configuration (Node "Workflow Configuration")**
- **Pinecone Index Name**: Điền tên index Pinecone (ví dụ: `internal-wiki-index`).
- **Pinecone Namespace**: Điền namespace (ví dụ: `default`).
- **Chunk Size**: Kích thước chunk text (ví dụ: `1000`).
- **Chunk Overlap**: Trùng lặp giữa chunk (ví dụ: `200`).
- **Retrieval Depth (top-K)**: Số lượng chunk trả về (ví dụ: `5`).

#### **B. Cấu hình OpenAI (Node "OpenAI Embeddings" và "OpenAI Chat Model")**
- **API Key**: Điền API Key từ OpenAI.
- **Model**: Đã cấu hình sẵn là `gpt-4o-mini` (không cần thay đổi).

#### **C. Cấu hình Pinecone (Node "Pinecone Insert Documents" và "Pinecone Vector Store")**
- **API Key**: Điền API Key từ Pinecone.
- **Environment**: Điền environment (ví dụ: `us-west1-gcp`).
- **Index Name**: Điền cùng tên với node **Workflow Configuration**.

#### **D. Cấu hình Gmail (Node "Send Daily Summary Email")**
- **Email**: Địa chỉ email gửi báo cáo.
- **Password**: Mật khẩu hoặc App Password (nếu sử dụng 2FA).
- **Recipient**: Địa chỉ email nhận báo cáo (ví dụ: `team@doanhnghiep.com`).

#### **E. Cấu hình Schedule Trigger (Node "Daily Summary Schedule")**
- **Cron Expression**: Để chạy hàng ngày lúc 8h sáng (ví dụ: `0 8 * * *`).

---
### **3. Kích hoạt ⚡️**
1. **Test Run với dữ liệu mẫu**:
   - Tải một file PDF/CSV/JSON lên form **Document Upload Form**.
   - Kiểm tra chatbot trả lời câu hỏi có chính xác không.
   - Kiểm tra báo cáo hàng ngày có được gửi không.

2. **Bật Active workflow**:
   - Nhấn **Active** trên n8n Editor.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[MỞ RỘNG THÊM]
1. **Kết nối với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo khi chatbot trả lời thành công/thất bại.

2. **Lưu log chi tiết vào Google Sheets**:
   - Thêm node **Google Sheets** sau node **Log Chat Interactions** để theo dõi tất cả cuộc trò chuyện.

3. **Tự động xóa tài liệu cũ**:
   - Thêm node **Code** để xóa embeddings của tài liệu đã bị xóa từ form upload.

4. **Cập nhật tài liệu tự động**:
   - Kết nối với **Google Drive** hoặc **Dropbox** để tự động tải tài liệu mới vào chatbot.

5. **Báo cáo chi tiết hơn**:
   - Sử dụng node **Code** để tính toán thêm metric như:
     - Thời gian trung bình trả lời.
     - Tỉ lệ câu hỏi liên quan đến từng file.
     - Top 5 file được tham khảo nhiều nhất.
:::

---
## 📌 **Kết luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn** quá trình trả lời câu hỏi từ tài liệu nội bộ, đồng thời **tự động phân tích và báo cáo hiệu suất** hàng ngày. Không cần code, chỉ cần cấu hình trên n8n – tiết kiệm thời gian và tăng hiệu suất công việc lên **1000%**.

**Hành động ngay!**
1. **Cài đặt n8n Self-hosted** trên VPS (đăng ký [tại đây](https://tino.vn/vps-n8n?affid=388) với mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Nhận báo cáo hàng ngày** về hiệu suất chatbot!

👉 **Bắt đầu tự động hóa ngay hôm nay!** 🚀