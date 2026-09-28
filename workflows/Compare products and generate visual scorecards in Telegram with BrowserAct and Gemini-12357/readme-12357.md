---
title: "🚀 Tự Động So Sánh Sản Phẩm & Tạo Bảng Điểm Hình Ảnh Telegram Với AI Gemini & BrowserAct"
description: "Workflow này tự động so sánh 2 sản phẩm (ví dụ: iPhone 15 vs Galaxy S24) thông qua Telegram, thu thập dữ liệu từ BrowserAct, phân tích AI sâu và tạo ra bảng điểm hình ảnh 4K với AI Gemini. Giúp các sếp tiết kiệm 8+ giờ nghiên cứu hàng tháng."
slug: "tự-dộng-so-sánh-sản-phẩm-tao-bảng-điểm-telegram"
tags: [n8n, automation, ai-chatbot, market-research, browseract, google-gemini]
keywords: [n8n workflow so sánh sản phẩm, tự động hóa so sánh sản phẩm, ai gemini tạo hình ảnh, browseract scrap dữ liệu, telegram bot so sánh sản phẩm]
---

# 🚀 **Tự Động So Sánh Sản Phẩm & Tạo Bảng Điểm Hình Ảnh Telegram Với AI Gemini & BrowserAct**

## **🔍 Nỗi Đau Của Các Sếp**
Bạn có bao giờ phải mất **giờ đồng hồ** để so sánh hai sản phẩm (ví dụ: iPhone 15 vs Galaxy S24, MacBook Air vs Dell XPS) chỉ để đưa ra quyết định mua sắm hay báo cáo cho khách hàng? Thường thì quá trình này bao gồm:
✅ **Thu thập dữ liệu** từ nhiều nguồn (Amazon, G2, Trustpilot, trang web chính thức).
✅ **So sánh chi tiết** về cấu hình, giá cả, đánh giá người dùng, và trải nghiệm.
✅ **Tạo báo cáo hình ảnh** để dễ hiểu và thuyết phục khách hàng.
✅ **Cập nhật liên tục** khi có thông tin mới.

**Workflow này giải quyết tất cả bằng AI + tự động hóa 100% không cần code!**

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tốc độ và bảo mật.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 8+ giờ/tháng** so sánh sản phẩm thủ công.
- **Độ chính xác cao** nhờ AI phân tích từ nhiều nguồn dữ liệu.
- **Báo cáo hình ảnh 4K** tự động, dễ hiểu và thuyết phục khách hàng.
- **Hoạt động liên tục** 24/7, không cần can thiệp người dùng.
- **Cá nhân hóa** theo yêu cầu của từng khách hàng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot** (để nhận yêu cầu so sánh từ người dùng).
2. **API Key BrowserAct** (để scrap dữ liệu sản phẩm từ nhiều nguồn).
3. **Google Sheets** (để lưu trữ dữ liệu tạm thời).
4. **Google Gemini API** (để phân tích và tạo hình ảnh).
5. **Template "Product Comparison & Visualize Bo"** trên BrowserAct (để xác định nguồn dữ liệu phù hợp).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/12357](https://n8n.io/workflows/12357) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **24 node** và cần cấu hình chi tiết như sau:

#### **🔹 Node "User Sends Message to Bot" (TelegramTrigger)**
- **Cấu hình:**
  - Chọn **credentials** là `telegramApi` (đã cài đặt trước).
  - **Trigger Type:** `Message` (để bắt đầu workflow khi người dùng gửi tin nhắn).

#### **🔹 Node "Validate User Input" (Agent)**
- **Cấu hình:**
  - **Prompt:** AI sẽ phân tích yêu cầu so sánh (ví dụ: "iPhone 15 vs Galaxy S24").
  - **Output:** Xác định loại sản phẩm (Physical, Software, Service) để BrowserAct biết lấy dữ liệu từ nguồn nào.

#### **🔹 Node "Search for Each Product's Data" (BrowserAct)**
- **Cấu hình:**
  - **Credentials:** `browserActApi` (đã cài đặt).
  - **Template:** Chọn **"Product Comparison & Visualize Bo"** (đã tạo trước).
  - **Input:** Dữ liệu sản phẩm từ Telegram (ví dụ: "iPhone 15", "Galaxy S24").
  - **Output:** Dữ liệu chi tiết (cấu hình, giá, đánh giá, ...).

#### **🔹 Node "Google Gemini 1/2/3" (lmChatGoogleGemini)**
- **Cấu hình:**
  - **Credentials:** `googlePalmApi` (API Key của Google Gemini).
  - **Prompt:** AI sẽ phân tích dữ liệu theo **4 tiêu chí**:
    1. **Composition** (Cấu hình kỹ thuật).
    2. **Performance** (Hiệu suất).
    3. **Economics** (Giá cả).
    4. **Experience** (Trải nghiệm người dùng).
  - **Output:** Điểm số và phân tích chi tiết.

#### **🔹 Node "Generate Comparison Image" (googleGemini)**
- **Cấu hình:**
  - **Credentials:** `googlePalmApi`.
  - **Prompt:** AI tạo **mô tả hình ảnh chi tiết** (ví dụ: "Tạo một bảng điểm 4K so sánh iPhone 15 vs Galaxy S24, bao gồm điểm số, ưu nhược điểm, và logo 'Winner' cho sản phẩm chiến thắng").
  - **Output:** Hình ảnh 4K tự động được gửi về Telegram.

#### **🔹 Node "Send Photo Message to Bot" (Telegram)**
- **Cấu hình:**
  - **Credentials:** `telegramApi`.
  - **Operation:** `sendPhoto` (gửi hình ảnh so sánh về Telegram).

---

### **3. Kích Hoạt ⚡️**
1. **Test Run:** Gửi tin nhắn thử vào Telegram Bot (ví dụ: "Compare iPhone 15 vs Galaxy S24").
2. **Active Workflow:** Bật chế độ **Active** trong n8n Editor.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Email:**
   - Thay vì chỉ Telegram, có thể gửi kết quả so sánh đến **Slack** hoặc **Email** thông qua node `n8n-nodes-base.email`.

2. **Lưu Log Dữ Liệu:**
   - Sử dụng node `n8n-nodes-base.googleSheets` để lưu tất cả lịch sử so sánh vào một **Google Sheet** để theo dõi.

3. **Tự Động Cập Nhật Dữ Liệu:**
   - Sử dụng **n8n Scheduler** để chạy workflow định kỳ (ví dụ: hàng tuần) để cập nhật dữ liệu mới.

4. **Tạo Báo Cáo Định Kỳ:**
   - Kết hợp với **Google Docs** hoặc **PDF Generator** để tạo báo cáo chi tiết gửi cho khách hàng.

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc so sánh sản phẩm thủ công, đồng thời **tăng cường hiệu quả quyết định** nhờ AI phân tích và báo cáo hình ảnh chuyên nghiệp.

**🚀 Hãy áp dụng ngay và tiết kiệm 8+ giờ/tháng!**
Nếu có vấn đề, tham khảo:
- [Hướng dẫn BrowserAct](https://docs.browseract.com)
- [Cách cài đặt n8n trên VPS](https://docs.n8n.io/hosting/self-hosting/)

---
**💡 Mẹo cuối:** Nếu muốn tối ưu hơn, các sếp có thể **tùy chỉnh template BrowserAct** để lấy dữ liệu từ các nguồn khác (ví dụ: Lazada, Shopee) cho thị trường Việt Nam!