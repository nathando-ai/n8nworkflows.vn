---
title: "🤖 Tự Động Hóa Gmail Với OpenAI + Học Máy Từ Telegram: Xóa Bỏ Công Việc Lặp Lại"
description: "Workflow tự động phân loại email Gmail bằng AI OpenAI, tự động gán nhãn và học từ phản hồi người dùng qua Telegram. Giúp tiết kiệm 8+ giờ/ngày cho các sếp và cải thiện hiệu suất làm việc."
slug: "tieu-dong-hoa-gmail-voi-openai-telegram"
tags: [n8n, automation, no-code, ai-summarization, gmail-automation, telegram-bot, openai]
keywords: [tự động hóa email gmail, phân loại email bằng ai, học máy tự động gmail, telegram review ai, workflow n8n gmail]
---

# 🚀 **Tự Động Hóa Phân Loại Email Gmail Với AI OpenAI + Học Máy Từ Telegram**

## **📌 Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải mất **8+ giờ** để:
- **Lọc và phân loại** hàng trăm email rác, newsletter, và tin nhắn quan trọng.
- **Tìm kiếm và đánh dấu** email cần ưu tiên (Important, Marketing, Newsletter...).
- **Học từ kinh nghiệm** để cải thiện hệ thống phân loại trong tương lai.

**Kết quả?** Thời gian quý giá bị "chôn vùi" trong công việc lặp lại, trong khi AI có thể làm tất cả những việc này **một cách thông minh và tự động**.

---
## **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 8+ giờ/ngày** bằng cách tự động phân loại email với độ chính xác cao.
- **Cải thiện hiệu suất** bằng cách AI học từ phản hồi người dùng qua Telegram.
- **Tự động gán nhãn** cho email mới dựa trên lịch sử và logic học máy.
- **Học từ kinh nghiệm** để AI ngày càng thông minh hơn trong tương lai.
- **Giảm thiểu rủi ro** bằng cách yêu cầu xác nhận cho email có độ tin cậy thấp.
:::

---
## **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
✅ **Tài khoản Gmail** (cần cấp quyền OAuth 2.0 cho n8n).
✅ **API Key OpenAI** (đăng ký tại [OpenAI](https://platform.openai.com/account/api-keys)).
✅ **Bot Telegram** (tạo bot tại [@BotFather](https://t.me/BotFather) và lấy API Token).
✅ **Danh sách nhãn Gmail** bắt đầu bằng `AI/` (ví dụ: `AI/Important`, `AI/Newsletter`, `AI/Marketing`).
✅ **VPS n8n** (để workflow chạy 24/7, không cần restart).
:::

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/15805](https://n8n.io/workflows/15805) và import vào n8n Editor.
- **Copy/Paste JSON** từ file vào n8n Editor (đảm bảo không có lỗi syntax).

:::note[LƯU Ý]
- **Không xóa node nào** trong workflow, chỉ chỉnh sửa các tham số cần thiết.
- **Không thay đổi cấu trúc nhãn Gmail** (nếu muốn sử dụng khác, phải cập nhật ở node `Gmail Trigger`).
:::

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node `Gmail Trigger` (Gmail: Gmail Trigger)**
- **Query:** `-label:AI` (đảm bảo email đã được xử lý không bị reprocess).
- **Credentials:** Chọn `gmailOAuth2` (cần cấu hình OAuth 2.0 trong n8n).

#### **🔹 Node `Gmail Backfill` (Gmail: Gmail Backfill)**
- **Query:** Tìm email trong **14 ngày gần nhất** chưa có nhãn `AI`.
- **Credentials:** Chọn `gmailOAuth2`.

#### **🔹 Node `Get all labels` (Gmail: Get all labels)**
- **Credentials:** Chọn `gmailOAuth2`.
- **Lưu ý:** Workflow **tự động phát hiện** nhãn bắt đầu bằng `AI/`, nhưng nếu muốn thay đổi, phải cập nhật ở node `filter for AI labels`.

#### **🔹 Node `OpenAI Chat Model` (lmChatOpenAi)**
- **Model:** Chọn `gpt-5.4-mini` (hoặc `gpt-5-mini` nếu muốn).
- **Credentials:** Chọn `openAiApi` (điền API Key OpenAI).
- **System Prompt:** Cần **cập nhật** để phù hợp với nhãn Gmail của các sếp (xem phần **Hướng Dẫn Cập Nhật System Prompt** dưới đây).

#### **🔹 Node `Telegram: Train` (Telegram: Telegram)**
- **Credentials:** Chọn `telegramApi` (điền API Token Telegram).
- **Operation:** `sendAndWait` (để nhận phản hồi từ người dùng).

#### **🔹 Node `set confidence threshold` (Code)**
- **Giá trị mặc định:** `0.9` (có thể điều chỉnh từ `0.7` đến `0.95`).
  - **0.95:** Chỉ tự động khi AI rất chắc chắn.
  - **0.80:** Tự động nhiều hơn, nhưng có rủi ro nhỏ.
  - **0.70:** Tự động nhiều, nhưng cần kiểm tra thường xuyên.

#### **🔹 Node `Add fixed labels` (Gmail: Add Labels)**
- **Labels:** `AI` (nhãn cha để tránh reprocess).
- **Credentials:** Chọn `gmailOAuth2`.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với 1-2 email mẫu để kiểm tra logic.
2. **Bật Active** workflow.
3. **Chạy Backfill** để xử lý email cũ (nếu cần).

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **🔹 Cập Nhật System Prompt Cho AI**
System prompt là **cốt lõi** quyết định độ chính xác của AI. Các sếp nên:
```javascript
// Ví dụ cấu trúc system prompt (cần thay đổi theo nhãn của mình)
"Bạn là một trợ lý AI phân loại email. Dưới đây là danh sách các nhãn có sẵn:
- AI/Important: Email cần ưu tiên ngay lập tức.
- AI/Newsletter: Email marketing, không cần trả lời.
- AI/Marketing: Email quảng cáo, có thể lưu lại.
- AI/Archive: Email không quan trọng, có thể xóa sau.

Hãy phân loại email dựa trên:
1. Nội dung email.
2. Sender (người gửi).
3. Lịch sử tương tác trước đó (nếu có).

Nếu độ tin cậy < {confidenceThreshold}, hãy yêu cầu xác nhận từ người dùng."
```
**Lưu ý:** Đặt system prompt trong node `AI Check Email` (type: `agent`).

### **🔹 Thay Thế Telegram Bằng Slack/Email**
Nếu không muốn dùng Telegram, có thể:
- **Sử dụng Slack Webhook** (thay thế node `Telegram: Train` bằng `Slack`).
- **Gửi email tự động** (thay thế bằng `Email` node).

### **🔹 Lưu Log Cho Dễ Dàng Theo Dõi**
- Thêm node **`StickyNote`** để ghi lại lịch sử phân loại.
- Sử dụng **`DataTable`** để lưu trữ quy tắc học máy.

### **🔹 Tự Động Gửi Báo Cáo Hàng Tuần**
- Sử dụng **`Execute Workflow Trigger`** để chạy workflow định kỳ.
- Gửi báo cáo qua **Telegram/Email** về số email đã tự động phân loại.

---
## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp bằng cách:
✅ **Tự động phân loại email** với độ chính xác cao.
✅ **Học từ phản hồi người dùng** để AI ngày càng thông minh.
✅ **Giảm thiểu công việc lặp lại** bằng cách tự động gán nhãn.

**Hành động ngay:**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Import workflow** và cấu hình các node quan trọng.
3. **Test với email mẫu** trước khi chạy toàn bộ.

👉 **[Đăng ký VPS n8n chỉ 50k/tháng tại TinoHost](https://tino.vn/vps-n8n?affid=388)** (mã giảm giá: **VPSN8N**).

---
**🚀 Hãy tự động hóa ngay hôm nay và dành thời gian cho những việc quan trọng hơn!**