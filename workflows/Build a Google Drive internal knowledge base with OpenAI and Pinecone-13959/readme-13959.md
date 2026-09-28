---
title: "🧠 Tự Động Hóa Hệ Thống Tri Thức Nội Bộ (Internal Wiki) Sử Dụng AI RAG Với Google Drive + OpenAI + Pinecone"
description: "Workflow này chuyển đổi toàn bộ tài liệu Google Drive của doanh nghiệp thành một hệ thống tri thức AI tự động trả lời câu hỏi, tiết kiệm thời gian cho bộ phận hỗ trợ và quản lý thông tin. Hỗ trợ tìm kiếm semantic, trả lời chính xác với nguồn gốc và cập nhật tự động hàng tuần."
slug: "tự-dộng-hoa-knowledge-base-ai-rag-google-drive"
tags: [n8n, automation, no-code, ai-rag, google-drive, openai, pinecone, internal-wiki, self-hosted]
keywords: [n8n workflow knowledge base, tự động hóa tri thức nội bộ, AI RAG với Google Drive, Pinecone OpenAI, tự động hóa hỗ trợ khách hàng, hệ thống tri thức tự động]
---

# 🚀 **Tạo Hệ Thống Tri Thức Nội Bộ AI Tự Động Hỏi Đáp Với Google Drive + OpenAI + Pinecone**

## **💡 Giới Thiệu: Giải Pháp Cho Nỗi Đau "Trả Lời Lặp Lại Câu Hỏi"**
Các sếp đã bao giờ phải nghe bộ phận hỗ trợ khách hàng (hoặc chính mình) phải trả lời **ngàn lần** những câu hỏi như:
- *"Chính sách HR mới nhất là gì?"*
- *"Quá trình bán hàng của chúng ta như thế nào?"*
- *"Tài liệu tài chính năm nay có ở đâu?"*

**Kết quả?** Thời gian, năng suất và sự hài lòng của khách hàng bị ảnh hưởng. **Workflow này giải quyết vấn đề đó bằng cách:**
✅ **Chuyển đổi toàn bộ tài liệu Google Drive thành một hệ thống tri thức AI tự động trả lời**
✅ **Tìm kiếm thông tin chính xác bằng công nghệ RAG (Retrieval-Augmented Generation)**
✅ **Trả lời với nguồn gốc và độ tin cậy cao**
✅ **Cập nhật tự động hàng tuần khi có tài liệu mới/được sửa đổi**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian hỗ trợ khách hàng:** AI trả lời tự động thay vì nhân viên.
- **Chính xác 100%:** Trả lời dựa trên tài liệu chính thức, không sai lệch.
- **Cập nhật tự động:** Hệ thống kiểm tra và cập nhật tài liệu hàng tuần.
- **Tìm kiếm thông minh:** Dùng AI tìm kiếm semantic (hiểu ngữ cảnh) thay vì keyword.
- **Dễ dàng mở rộng:** Thêm tài liệu mới mà không cần can thiệp thủ công.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Google Drive** (để lưu trữ tài liệu)
✔ **Tài khoản Pinecone** (để lưu trữ embeddings)
✔ **API Key OpenAI** (để tạo embeddings và trả lời AI)
✔ **Tài khoản Gmail** (để gửi báo cáo hàng tuần)
✔ **Google Sheets** (để đăng ký và lưu log câu hỏi)

---
:::info[CHUẨN BỊ CÁC CREDENTIALS]
- **Google Drive OAuth2:** Cấu hình trong `n8n Credentials` với quyền đọc/tải xuống.
- **Google Sheets OAuth2:** Cấu hình với quyền ghi vào sheet.
- **Gmail OAuth2:** Cấu hình với quyền gửi email.
- **Pinecone API:** API Key từ [Pinecone.io](https://www.pinecone.io/).
- **OpenAI API:** API Key từ [OpenAI](https://platform.openai.com/).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/13959](https://n8n.io/workflows/13959) và import vào n8n Editor.
- **Copy/paste JSON** từ file vào `Import Workflow` trong n8n.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **3 phần chính**, các sếp cần chú ý:

#### **📂 Phần 1: Ingest Tài Liệu (SW1 - Manual Trigger)**
- **Node `List Knowledge Base Docs`:** Chọn **Google Drive OAuth2** và **folder Knowledge Base**.
- **Node `Download Doc as Text`:** Đảm bảo **Google Drive OAuth2** có quyền đọc.
- **Node `Store Embeddings in Pinecone`:** Điền **Pinecone API Key** và **index name** (phải tạo trước với `dimensions=1536, metric=cosine`).
- **Node `Log to Document Registry`:** Chọn **Google Sheets OAuth2** và **sheet name** để lưu log.

#### **🤖 Phần 2: Trả Lời Câu Hỏi (SW2 - Webhook)**
- **Node `Question Webhook`:** Cấu hình **path: `/knowledge-brain`** và **HTTP Method: POST**.
- **Node `Extract Question & User`:** Sử dụng **JavaScript** để trích xuất `question` từ payload.
- **Node `Search Knowledge Base`:** Điền **Pinecone API Key** và **index name**.
- **Node `Answer Generator`:** Chọn **OpenAI API** và **model** (ví dụ: `gpt-4o`).
- **Node `Send Answer Response`:** Đảm bảo **webhook URL** trả về kết quả cho người dùng.

#### **📅 Phần 3: Cập Nhật Hàng Tuần (SW3 - Schedule Trigger)**
- **Node `Weekly Sunday 11AM Trigger`:** Cấu hình **schedule** là `0 11 * * 0` (Chủ nhật 11h sáng).
- **Node `Detect New or Updated Docs`:** Sử dụng **JavaScript** để so sánh với **Document Registry**.
- **Node `Re-ingest into Pinecone`:** Đảm bảo **Pinecone API Key** và **index name** đúng.
- **Node `Send Weekly KB Digest`:** Chọn **Gmail OAuth2** và **template email** (có thể chỉnh sửa trong `Build KB Digest Email`).

---
### **3. Kích Hoạt ⚡️**
1. **Test Run:** Chạy **Manual Ingestion Trigger** với 1-2 tài liệu mẫu để kiểm tra.
2. **Bật Active:** Mở **Active** cho cả 3 phần workflow.
3. **Test Webhook:** Gửi **POST request** đến `https://[your-n8n-url]/knowledge-brain` với payload:
   ```json
   {
     "question": "Chính sách HR mới nhất là gì?"
   }
   ```

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram:** Thay vì webhook, các sếp có thể dùng **Slack Webhook** để người dùng gửi câu hỏi qua Slack.
2. **Lưu Log Chi Tiết:** Thêm **Google Sheets** để lưu log tất cả câu hỏi và trả lời.
3. **Báo Cáo Hàng Tháng:** Sử dụng **Google Sheets + Gmail** để gửi báo cáo tổng hợp về hoạt động của hệ thống.
4. **Cập Nhật Tự Động:** Nếu tài liệu trong Google Drive thay đổi, hệ thống sẽ tự động cập nhật embeddings vào Pinecone.

---
## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp và nhân viên khỏi việc trả lời lặp lại câu hỏi, đồng thời **tăng cường tính chính xác và hiệu quả** của hệ thống tri thức nội bộ. **Hãy áp dụng ngay để:**
✔ **Tiết kiệm 50% thời gian hỗ trợ khách hàng**
✔ **Cập nhật tri thức tự động hàng tuần**
✔ **Trả lời chính xác với nguồn gốc rõ ràng**

**Bắt đầu ngay với n8n và biến Google Drive thành một AI Knowledge Base thông minh!** 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/13959)**
**📌 [Hướng dẫn cài đặt n8n Self-hosted](https://docs.n8n.io/)**