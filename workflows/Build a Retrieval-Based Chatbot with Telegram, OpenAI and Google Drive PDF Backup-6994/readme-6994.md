---
title: "🤖 **Tự Động Hóa Chatbot Telegram Trực Tuyến Từ PDF + AI RAG + Lưu Trữ Google Drive (Miễn Phí 100%)**"
description: "Workflow n8n tự động hóa chatbot Telegram sử dụng AI RAG (Retrieval-Augmented Generation) để trả lời câu hỏi từ PDF, đồng thời tự động sao lưu tài liệu lên Google Drive. Giúp các sếp tiết kiệm thời gian tra cứu, tăng tính chính xác và bảo mật dữ liệu."
slug: "chatbot-telegram-ai-rag-google-drive"
tags: [n8n, automation, ai-rag, telegram-bot, google-drive, openai, no-code]
keywords: [n8n workflow telegram, tự động hóa chatbot pdf, ai rag pdf, lưu trữ google drive tự động, chatbot telegram miễn phí]
---

# **🚀 Chatbot Telegram AI-Powered Từ PDF + Lưu Trữ Google Drive (Không Cần Code)**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải mất **giờ đồng hồ** để tra cứu thông tin trong các tài liệu PDF, email, hoặc tài liệu nội bộ. Thậm chí, khi có nhiều người truy cập cùng một tài liệu, việc cập nhật hoặc sao lưu lại trở nên **phức tạp và dễ bị lỗi**.

**Workflow này giải quyết:**
✅ **Tự động trả lời câu hỏi từ PDF** bằng AI RAG (Retrieval-Augmented Generation) – trả lời chính xác, không sai lệch như Google Search.
✅ **Lưu trữ tự động lên Google Drive** – không lo mất dữ liệu, có thể truy cập từ mọi nơi.
✅ **Hoạt động 24/7** – không cần can thiệp thủ công, tiết kiệm thời gian cho các sếp.
✅ **Không cần code** – chỉ cần cấu hình các API và upload tài liệu là xong.

---

### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm 50% thời gian tra cứu** – AI trả lời ngay lập tức từ PDF, không cần đọc từng trang.
- **Chính xác 100%** – Không sai lệch như Google Search, trả lời dựa trên nội dung chính xác của tài liệu.
- **Lưu trữ an toàn** – Tất cả PDF được tự động sao lưu lên Google Drive, không lo mất dữ liệu.
- **Hoạt động liên tục** – Chatbot Telegram hoạt động 24/7, không cần can thiệp thủ công.
- **Dễ dàng mở rộng** – Có thể kết nối với Slack, Email, hoặc các hệ thống khác.
:::

---

### **🔧 Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi Bắt Đầu**]
Các sếp cần chuẩn bị:
✔ **Tài khoản Telegram Bot** (tạo từ [@BotFather](https://t.me/botfather))
✔ **API Key OpenAI** (đăng ký tại [OpenAI](https://platform.openai.com/))
✔ **Tài khoản Google Drive** (để lưu trữ PDF)
✔ **n8n Self-Hosted** (khuyến nghị dùng VPS để workflow hoạt động 24/7)
✔ **Các PDF cần tra cứu** (ví dụ: tài liệu nội bộ, sách, báo cáo)
:::

---

## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow Từ File JSON**
:::note[**Bước 1: Tải Workflow**]
- Tải file JSON từ [n8n.io/workflows/6994](https://n8n.io/workflows/6994) (hoặc copy JSON từ trang này).
- Trong n8n Editor, nhấn **Import** → Dán JSON hoặc tải file `.json`.
:::

### **2. Cấu Hình Cần Thiết (Bắt Buộc)**
:::warning[**Các Node Quan Trọng Cần Chỉnh**]
| **Node** | **Cần Chỉnh Gì?** | **Lưu Ý** |
|----------|-------------------|------------|
| **Telegram Trigger** | Điền `token` từ BotFather | Chọn `webhook` hoặc `polling` |
| **OpenAI Embeddings** | Điền `openAiApi` (API Key) | Chọn model `text-embedding-ada-002` |
| **OpenAI Chat Model** | Điền `openAiApi` (API Key) | Chọn model `gpt-4o-mini` (rẻ và hiệu quả) |
| **Google Drive** | Điền `googleDriveOAuth2Api` | Chọn folder lưu trữ PDF |
| **Default Data Loader** | Không cần chỉnh (auto đọc PDF) | Chỉ cần upload file |
| **Vector Store (Embeddings)** | Không cần chỉnh (auto lưu) | Đảm bảo cùng model với Embeddings |
| **Telegram Document Query Agent** | Không cần chỉnh (auto trả lời) | AI sẽ tự tìm kiếm từ PDF |
:::

### **3. Kích Hoạt Workflow**
1. **Test Run** – Nhấn **Run Workflow** với dữ liệu mẫu (ví dụ: upload PDF mẫu).
2. **Bật Active** – Đảm bảo tất cả node hoạt động bình thường.
3. **Kiểm Tra Telegram Bot** – Gửi tin nhắn text để test AI trả lời.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::tip[**Cách Tối Ưu Hiệu Quả**]
- **Kết nối với Slack/Email** → Sử dụng node `webhook` để nhận tin nhắn từ Slack/Email và chuyển sang Telegram.
- **Lưu Log Câu Hỏi** → Sử dụng node `database` (PostgreSQL, MongoDB) để ghi lại lịch sử câu hỏi.
- **Tự động Upload PDF từ Google Drive** → Sử dụng node `googleDriveWatch` để phát hiện file mới và tự động embed.
- **Tăng Cường AI với Prompt Engineering** → Chỉnh sửa node `agent` để trả lời chính xác hơn.
- **Duyệt PDF từ Telegram** → Mở rộng node `formTrigger` để người dùng có thể upload PDF trực tiếp qua Telegram.
:::

---

## **📌 Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa tra cứu PDF, tiết kiệm thời gian và bảo mật dữ liệu. **Không cần code, chỉ cần cấu hình** và workflow sẽ hoạt động 24/7.

**🚀 Hãy áp dụng ngay và thử nghiệm với PDF của mình!**
Nếu có vấn đề, các sếp có thể liên hệ tác giả [Trung Tran](mailto:lets@automatewith.me) để hỗ trợ.

---
:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**📌 Sample PDF để test:** [Tải PDF mẫu](https://ptgmedia.pearsoncmg.com/images/9780138203283/samplepages/9780138203283_Sample.pdf)