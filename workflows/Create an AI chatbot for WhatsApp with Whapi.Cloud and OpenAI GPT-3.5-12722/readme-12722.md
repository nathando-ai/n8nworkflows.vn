---
title: "🤖 Tạo Chatbot AI Trả Lời Trên WhatsApp Với Whapi.Cloud & OpenAI GPT-3.5 (Không Cần Code!)"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp xây dựng chatbot AI trả lời tin nhắn WhatsApp thông minh, hỗ trợ từ câu hỏi tự nhiên đến các lệnh số (1-9) như gửi hình ảnh, tài liệu, sản phẩm... chỉ với 1 dòng lệnh. Tiết kiệm thời gian hỗ trợ khách hàng lên đến 80%!"
slug: tao-chatbot-ai-whatsapp-whapi-cloud-openai
tags: [n8n, automation, no-code, chatbot-ai, whatsapp-business, openai, whapi-cloud]
keywords: [chatbot whatsapp tự động hóa, n8n workflow whatsapp, tự động trả lời tin nhắn whatsapp, chatbot ai trả lời tự nhiên, whapi cloud api, openai gpt-3.5 trên whatsapp]
---

# 🚀 **Chatbot AI Trả Lời WhatsApp: Từ Tin Nhắn Tự Nhiên Đến Lệnh Số (1-9) – Không Cần Code!**

Hãy tưởng tượng một chatbot AI có thể:
- **Trả lời tự nhiên** mọi câu hỏi khách hàng gửi với `/AI [câu hỏi]` (ví dụ: `/AI "Bao nhiêu thời gian giao hàng?"`).
- **Thực hiện lệnh số** chỉ bằng 1 số (1-9) như gửi hình ảnh, tài liệu, sản phẩm, hoặc tạo nhóm chat.
- **Hoạt động 24/7** mà không cần can thiệp của bạn.

**Thủ công?** Tốn thời gian, dễ quên, và không thể xử lý hàng trăm tin nhắn cùng lúc.
**Với n8n?** Bạn chỉ cần **cài đặt 1 lần**, chatbot sẽ tự động hóa **tất cả** – từ nhận tin nhắn đến trả lời AI, gửi file, quản lý nhóm chat.

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
✅ **Tiết kiệm 80% thời gian hỗ trợ khách hàng** – Chatbot tự động trả lời 24/7.
✅ **Trải nghiệm cá nhân hóa** – Khách hàng nhận câu trả lời tự nhiên từ AI (OpenAI GPT-3.5) hoặc lệnh số nhanh chóng.
✅ **Quản lý tin nhắn chuyên nghiệp** – Gửi hình ảnh, tài liệu, sản phẩm, hoặc tạo nhóm chat chỉ bằng 1 số.
✅ **Hoạt động liên tục** – Không cần ngủ, không cần nghỉ, và không sai sót như con người.
✅ **Dễ dàng mở rộng** – Thêm lệnh mới hoặc tích hợp với Slack/Telegram chỉ bằng vài click.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi Bắt Đầu**]
Để workflow này hoạt động, các sếp cần:
1. **Tài khoản Whapi.Cloud** (đăng ký tại [whapi.cloud](https://panel.whapi.cloud/)) và **Channel Token** (tìm ở **Dashboard → Channels**).
2. **API Key OpenAI** (nếu sử dụng tính năng AI trả lời tự nhiên).
3. **Các thông tin tùy chọn** (nếu cần):
   - `OPENAI_API_KEY` (để chatbot AI hoạt động).
   - `PRODUCT_ID` (để gửi sản phẩm).
   - `GROUP_ID` (để gửi tin nhắn đến nhóm chat).
   - **URL công khai** cho hình ảnh, tài liệu, video (nếu sử dụng lệnh số 2, 3, 4).
4. **N8n Self-hosted** (để workflow hoạt động 24/7). 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/12722](https://n8n.io/workflows/12722) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Workflow Editor**.
  2. Nhấn **Import** và chọn file JSON.
  3. Hoặc nhấn **Create new workflow** → **Import from JSON** và dán code.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **28 node** và cần cấu hình **cẩn thận** để hoạt động. Dưới đây là hướng dẫn chi tiết cho từng phần quan trọng:

#### **🔹 Node 1️⃣: Receive WhatsApp Message (Webhook)**
- **Không cần chỉnh sửa** nếu đã cấu hình Webhook ở Whapi.Cloud.
- **Lưu ý**:
  - **Không sử dụng URL Test** khi workflow live! Sử dụng **Production URL** từ node Webhook.
  - Ở **Whapi.Cloud**, đi đến **Channel Settings → Webhooks** và thêm:
    - **Event**: `messages`
    - **Method**: `POST`
    - **URL**: Dán **Production URL** từ node Webhook.
    - **Mode**: `Body`

#### **🔹 Node 4️⃣: What Type of Command? (Switch)**
- **Cấu trúc logic**:
  - Nếu tin nhắn bắt đầu bằng `/AI ` → Gửi đến OpenAI.
  - Nếu tin nhắn là số (1-9) → Xử lý lệnh tương ứng.
  - Còn lại → Hiển thị menu trợ giúp.

#### **🔹 Node 5️⃣: Which Number Command? (1-9) (Switch)**
- **Mỗi lệnh số (1-9) có logic riêng**:
  - **1**: Gửi tin nhắn văn bản.
  - **2**: Gửi hình ảnh.
  - **3**: Gửi tài liệu (PDF).
  - **4**: Gửi video.
  - **5**: Gửi thẻ liên lạc (vCard).
  - **6**: Gửi sản phẩm.
  - **7**: Tạo nhóm chat.
  - **8**: Gửi tin nhắn đến nhóm chat.
  - **9**: Danh sách nhóm chat.

- **Cách chỉnh sửa**:
  - Mở node **Prepare: Simple Text** (lệnh 1) và thay đổi `body` (nội dung tin nhắn).
  - Mở node **Prepare: Image** (lệnh 2) và thay đổi:
    - `mediaPath`: URL hình ảnh công khai (ví dụ: `https://example.com/image.jpg`).
    - `caption`: Dòng mô tả.
  - Mở node **Prepare: Product** (lệnh 6) và thay đổi `ProductID` (tìm ở [Whapi Cloud API](https://whapi.readme.io/reference/getproducts)).

#### **🔹 Node 19️⃣: Message a model (OpenAI)**
- **Cấu hình OpenAI**:
  1. Tạo **credentials OpenAI** ở n8n:
     - Đi đến **Credentials → Add new credential → OpenAI**.
     - Nhập `OPENAI_API_KEY` (tìm ở [OpenAI Dashboard](https://platform.openai.com/account/api-keys)).
  2. Trong node **Message a model**:
     - Chọn **Credential** là OpenAI vừa tạo.
     - Đảm bảo `model` là `gpt-3.5-turbo` (mặc định).

#### **🔹 Node 28️⃣: ✔✔ Mark message as read (HTTP Request)**
- **Không cần chỉnh sửa** – node này đánh dấu tin nhắn đã đọc trên Whapi.Cloud.

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test run** với dữ liệu mẫu:
   - Gửi tin nhắn `/AI "Chào bot, bạn là ai?"` để kiểm tra AI trả lời.
   - Gửi số **1** để kiểm tra lệnh gửi tin nhắn văn bản.
2. **Bật Active workflow**:
   - Nhấn **Active** ở góc trên bên phải.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**Cách Tối Ưu Hiệu Quả**]
1. **Tích hợp với Slack/Telegram**:
   - Sử dụng node **Slack** hoặc **Telegram** để gửi thông báo khi có tin nhắn mới.
   - Ví dụ: Khi khách hàng gửi `/AI`, gửi tin nhắn cảnh báo cho team ở Slack.

2. **Lưu log hoạt động**:
   - Thêm node **Google Sheets** hoặc **Airtable** để ghi lại tất cả tin nhắn và phản hồi của chatbot.
   - Dễ dàng theo dõi và phân tích hiệu suất.

3. **Tự động gửi báo cáo hàng ngày**:
   - Sử dụng node **Set** + **HTTP Request** để gửi email tổng hợp (ví dụ: số tin nhắn, lệnh phổ biến nhất) mỗi sáng.

4. **Cập nhật nội dung động**:
   - Sử dụng **Environment Variables** để quản lý `PRODUCT_ID`, `GROUP_ID`, hoặc `OPENAI_API_KEY` một cách dễ dàng.

5. **Hỗ trợ nhiều ngôn ngữ**:
   - Thêm node **Translate** (n8n có node hỗ trợ Google Translate) để chatbot trả lời bằng nhiều ngôn ngữ.
:::

---
## 📌 **Kết Luận: Chatbot AI WhatsApp – Giải Pháp Tự Động Hóa Chuyên Nghiệp**
Workflow này **giải phóng bạn khỏi việc trả lời tin nhắn WhatsApp thủ công**, đồng thời **cung cấp trải nghiệm khách hàng chuyên nghiệp** với AI trả lời tự nhiên và lệnh số nhanh chóng.

**Bắt đầu ngay!**
1. **Import workflow** từ [n8n.io/workflows/12722](https://n8n.io/workflows/12722).
2. **Cấu hình Webhook** ở Whapi.Cloud.
3. **Test với tin nhắn mẫu** và **bật Active**.
4. **Mở rộng** với các tính năng nâng cao như tích hợp Slack hoặc lưu log.

**🚀 Hãy tự động hóa ngay hôm nay – khách hàng của bạn sẽ cảm ơn bạn!** 😊

---
### **🔗 Tài Liệu Tham Khảo**
- [Whapi.Cloud Dashboard](https://panel.whapi.cloud/)
- [OpenAI API Documentation](https://platform.openai.com/docs/api-reference)
- [n8n Workflow Original](https://n8n.io/workflows/12722)