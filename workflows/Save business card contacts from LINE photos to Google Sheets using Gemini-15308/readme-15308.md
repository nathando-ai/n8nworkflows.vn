---
title: "🚀 Tự Động Hóa Lưu Thông Tin Thẻ Doanh Nghiệp Từ Ảnh LINE Sang Google Sheets Với Gemini AI"
description: "Workflow tự động hóa hoàn toàn không cần code để trích xuất thông tin từ ảnh thẻ doanh nghiệp trên LINE, xử lý và lưu vào Google Sheets, đồng thời gửi thông báo đến Slack và phản hồi tự động cho người dùng. Giúp tiết kiệm thời gian lên tới 90% trong quản lý liên lạc mới."
slug: "tieu-dong-hoa-luu-thong-tin-the-doanh-nghiep-line-sang-google-sheets-gemini"
tags: [n8n, automation, no-code, ai-summarization, google-sheets, line-bot, gemini-ai]
keywords: [n8n workflow tự động hóa, trích xuất thông tin từ ảnh, LINE bot tự động, Google Sheets API, Gemini AI, lưu thông tin thẻ doanh nghiệp]
---

# 🚀 **Tự Động Hóa Lưu Thông Tin Thẻ Doanh Nghiệp Từ Ảnh LINE Sang Google Sheets Với Gemini AI**

### **Giải pháp cho doanh nghiệp không muốn mất thời gian ghi chép thủ công thông tin thẻ doanh nghiệp**
Hàng ngày, các sếp phải mất **30-60 phút** để ghi chép thông tin từ thẻ doanh nghiệp (tên, số điện thoại, email, vị trí công ty...) vào Google Sheets hoặc CRM. Với **workflow này**, bạn chỉ cần **chụp ảnh thẻ doanh nghiệp trên LINE**, hệ thống sẽ tự động:
✅ **Trích xuất thông tin** từ ảnh bằng **Gemini AI** (Google’s latest LLM)
✅ **Kiểm tra trùng lặp** trong Google Sheets
✅ **Lưu dữ liệu** vào bảng tính tự động
✅ **Gửi thông báo** đến Slack và phản hồi tự động trên LINE

Không cần viết một dòng code nào! **100% tự động hóa**, hoạt động **24/7** mà không tốn chi phí thêm.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Hỗ trợ 24/7)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần ghi chép thủ công, giảm **90% công việc lặp lại**.
- **Chính xác 100%**: Gemini AI trích xuất thông tin từ ảnh với độ chính xác cao, giảm sai sót.
- **Tự động kiểm tra trùng lặp**: Tránh lưu trùng dữ liệu trong Google Sheets.
- **Cá nhân hóa thông báo**: Gửi thông tin mới đến Slack và phản hồi tự động trên LINE.
- **Hoạt động liên tục**: Workflow chạy **24/7** mà không cần can thiệp của con người.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản LINE Developer** (để tạo **Channel Access Token**)
✔ **Google Sheets** (để lưu dữ liệu, cần chia sẻ quyền cho n8n)
✔ **Slack Webhook URL** (để gửi thông báo)
✔ **API Key Gemini** (tự động cấp khi đăng ký [Google AI Studio](https://aistudio.google.com/))
✔ **Webhook URL của LINE** (để n8n nhận được tin nhắn từ LINE)

---
:::note[Lưu ý quan trọng]
- **Không cần cài đặt LINE Bot** trên máy tính, chỉ cần **chia sẻ ảnh thẻ doanh nghiệp** qua LINE Messenger.
- **Google Sheets** phải có **bảng tính đã định dạng** (cột: Tên, Số điện thoại, Email, Vị trí công ty...).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
**Bước 1:** Tải file JSON từ [n8n.io/workflows/15308](https://n8n.io/workflows/15308) hoặc copy toàn bộ JSON dưới đây vào **n8n Editor**.

**Bước 2:** Mở **n8n Workflow Editor** và chọn **Import Workflow** → Chọn file JSON hoặc **Paste JSON**.

---
#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

##### **A. Cấu hình biến môi trường (Set Configuration Parameters)**
Mở node **"Set Configuration Parameters"** và điền các giá trị sau vào **Environment Variables**:
| Biến môi trường | Giá trị | Mô tả |
|------------------|---------|-------|
| `LINE_CHANNEL_ACCESS_TOKEN` | `YOUR_LINE_CHANNEL_ACCESS_TOKEN` | Lấy từ [LINE Developer Console](https://developers.line.biz/) |
| `GOOGLE_SHEET_ID` | `YOUR_GOOGLE_SHEET_ID` | Lấy từ URL Google Sheets (ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz` từ `https://docs.google.com/spreadsheets/d/1AbCdEfGhIjKlMnOpQrStUvWxYz/edit`) |
| `GOOGLE_SHEET_RANGE` | `Sheet1!A1:D1000` | Địa chỉ phạm vi lưu dữ liệu (đổi `Sheet1` thành tên sheet của bạn) |
| `SLACK_WEBHOOK_URL` | `YOUR_SLACK_WEBHOOK_URL` | Lấy từ **Custom Integrations** trong Slack |
| `GEMINI_API_KEY` | `YOUR_GEMINI_API_KEY` | Lấy từ [Google AI Studio](https://aistudio.google.com/) |

##### **B. Cấu hình Webhook LINE**
Mở node **"When LINE Event Received"** và chỉnh:
- **Path**: `business-card-webhook` (không đổi)
- **HTTP Method**: `POST` (không đổi)

**Bước 3:** Trong **LINE Developer Console**, thêm **Webhook URL** của n8n vào **Channel Settings** của LINE Bot.

##### **C. Cấu hình Gemini AI**
Mở node **"Setup Gemini for Card Data"** và **"Extract Card Info with Gemini"**:
- Đảm bảo **`GEMINI_API_KEY`** đã được điền vào **Environment Variables**.
- **Prompt** đã được cấu hình sẵn, **không cần chỉnh sửa** (n8n sẽ tự động sử dụng).

##### **D. Cấu hình Google Sheets**
Mở node **"Read Contacts from Sheets"** và **"Append Contact to Sheets"**:
- **Credentials**: Chọn **Google Sheets** đã tạo trước đó.
- **Sheet Name**: Đổi thành tên sheet của bạn (ví dụ: `Thẻ Doanh Nghiệp`).
- **Range**: Đổi thành `Sheet1!A1:D1000` (hoặc phạm vi phù hợp).

##### **E. Cấu hình Slack & LINE Response**
- **Slack Webhook URL**: Đã cấu hình trong **Environment Variables**.
- **LINE Response Messages**: Đã sẵn sàng, **không cần chỉnh sửa** (n8n sẽ tự động phản hồi).

---
#### **3. Kích hoạt ⚡️**
**Bước 1:** **Test Run** với một ảnh mẫu thẻ doanh nghiệp để kiểm tra:
- Gemini có trích xuất thông tin chính xác không?
- Dữ liệu có được lưu vào Google Sheets không?
- Slack có nhận được thông báo không?

**Bước 2:** Nếu test thành công, **bật Active workflow**.

---
### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động gửi báo cáo hàng tuần**:
   - Sử dụng **n8n Schedule Node** để gửi báo cáo tổng hợp về **Slack/Email** định kỳ.

2. **Kết hợp với CRM (HubSpot, Salesforce)**:
   - Thay vì lưu vào Google Sheets, **đổi node Google Sheets thành HubSpot API** để tự động đồng bộ vào CRM.

3. **Lưu log hoạt động**:
   - Thêm **n8n Database Node** để lưu lịch sử trích xuất và phản hồi.

4. **Cải thiện Gemini Prompt**:
   - Nếu Gemini trích xuất sai, **chỉnh sửa Prompt** trong node `Extract Card Info with Gemini` để phù hợp với kiểu thẻ của bạn.

5. **Tích hợp với Telegram**:
   - Thay vì Slack, **đổi node `httpRequest` thành Telegram Bot API** để gửi thông báo.

---
### 📌 **Kết luận**
**Workflow này không chỉ tiết kiệm thời gian mà còn giảm thiểu sai sót trong quản lý thông tin liên lạc.** Bằng cách **chỉ cần chụp ảnh thẻ doanh nghiệp trên LINE**, hệ thống sẽ tự động:
✔ **Trích xuất** thông tin bằng AI Gemini
✔ **Kiểm tra trùng lặp**
✔ **Lưu vào Google Sheets**
✔ **Gửi thông báo** đến Slack và phản hồi tự động

**Hãy áp dụng ngay để tự động hóa công việc quản lý liên lạc của mình!** 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/15308) | [Cài đặt n8n Self-hosted](https://docs.n8n.io/)**