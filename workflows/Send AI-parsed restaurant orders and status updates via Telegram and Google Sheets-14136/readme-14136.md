---
title: "🤖 Tự Động Hóa Quản Lý Đơn Đặt Ăn Quán Hàng via Telegram + Google Sheets (AI Parse Order)"
description: "Workflow tự động hóa 100% không code giúp quán hàng quản lý đơn đặt hàng qua Telegram, phân tích đơn bằng AI Claude Haiku, cập nhật trạng thái tự động và gửi thông báo cho khách hàng. Giúp tiết kiệm 80% thời gian quản lý đơn hàng và giảm thiểu lỗi nhân sự."
slug: "tieu-dong-hoa-quan-ly-don-dat-anh-quan-hang-telegram-google-sheets"
tags: [n8n, automation, no-code, ai-chatbot, telegram-bot, google-sheets, ai-order-parsing, restaurant-management]
keywords: [n8n workflow tự động hóa đơn đặt ăn, chatbot quản lý quán hàng, AI phân tích đơn hàng, Telegram bot đặt hàng, Google Sheets tự động hóa, Claude Haiku tự động hóa]
---

# 🚀 **Tự Động Hóa Quản Lý Đơn Đặt Ăn Quán Hàng Với Telegram + Google Sheets (AI Parse Order)**

## **📌 Nỗi Đau Của Các Sếp Quán Hàng**
Hàng ngày, các sếp quán hàng phải:
- **Lặp đi lặp lại** xử lý hàng trăm đơn đặt hàng qua Telegram, Zalo, hoặc điện thoại.
- **Phân tích đơn hàng thủ công** từ tin nhắn không chuẩn (ví dụ: "2 pizza + 1 coke" → phải chuyển thành "2 Margherita Pizza + 1 Coca-Cola").
- **Quên cập nhật trạng thái** đơn hàng cho khách hàng, dẫn đến phản hồi tiêu cực.
- **Không theo dõi được lịch sử đơn** của khách hàng cũ, mất cơ hội tái mua.
- **Phải ngồi 24/7** để kiểm tra và phản hồi đơn hàng mới.

**Workflow này giải quyết tất cả vấn đề trên bằng:**
✅ **AI tự động phân tích đơn hàng** từ tin nhắn tự nhiên (không cần khách hàng nhập theo mẫu).
✅ **Cập nhật trạng thái đơn tự động** khi nhân viên thay đổi trên Google Sheets.
✅ **Gửi thông báo tự động** cho khách hàng khi đơn hàng được chuẩn bị, sẵn sàng, hoàn tất hoặc bị hủy.
✅ **Hiển thị lịch sử đơn** cho khách hàng với chỉ một lệnh `/myorders`.
✅ **Không cần code** – chỉ cần cài đặt và chạy!

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** quản lý đơn hàng (không cần nhập liệu thủ công).
- **Giảm thiểu lỗi** trong phân tích đơn hàng (AI Claude Haiku chính xác hơn con người).
- **Tăng trải nghiệm khách hàng** với thông báo tự động và lịch sử đơn dễ dàng truy cập.
- **Hoạt động 24/7** – không cần nhân viên ngồi canh đơn hàng.
- **Dễ dàng mở rộng** cho nhiều quán hàng khác nhau.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - Tạo bot mới trên [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Bot này sẽ được đặt tên là `@new_nirav_restaurant_bot` (hoặc tùy chỉnh).
   - **Lưu ý**: Bot phải được thêm vào nhóm hoặc chat cá nhân với khách hàng.

2. **Google Sheets**:
   - Tạo một bảng Google Sheets mới với tên **"Restaurant Orders"** (hoặc tùy chỉnh).
   - **Cấu trúc cột bắt buộc** (các sếp copy từ mẫu dưới đây):
     | Queue Number | Chat ID | Name | Order | Status | Order Time | Order Date | Last Status Sent |
     |--------------|---------|------|-------|--------|------------|-------------|-------------------|
     | (Auto)       | (Number)| (Text)| (Text)| (Text)   | (Date)     | (Date)        | (Text)            |
   - **Cột "Last Status Sent"** (cột H) **phải tồn tại** để lưu trạng thái cuối cùng đã gửi cho khách hàng.

3. **API Key Claude Haiku (Anthropic)**:
   - Đăng ký tài khoản trên [Anthropic](https://www.anthropic.com/) và lấy **API Key**.
   - Model sử dụng: `claude-haiku-4-5-20251001`.

4. **VPS cho n8n (Self-hosted)**:
   - Để workflow chạy 24/7 ổn định, các sếp nên cài n8n trên VPS riêng.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

5. **Credentials cho n8n**:
   - Tạo các **credentials** trong n8n Editor cho:
     - **Telegram Bot Token** (dùng cho bot và trigger).
     - **Google Sheets API** (dùng cho đọc/giữ sheet).
     - **Anthropic API Key** (dùng cho Claude Haiku).
---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/14136) hoặc copy toàn bộ JSON từ đây.
- Trong n8n Editor, nhấn **Import Workflow** và dán JSON vào.
- **Không cần chỉnh sửa cấu trúc** của workflow, chỉ cần điền thông tin credentials sau.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **2 phần chính**:
- **Phần 1: Customer Bot** (quản lý đơn hàng từ khách hàng).
- **Phần 2: Staff Status Notifier** (cập nhật trạng thái đơn tự động).

##### **A. Cấu Hình Phần 1: Customer Bot**
1. **Node "Customer Bot Listener" (Telegram Trigger)**:
   - Chọn **credentials** Telegram Bot Token.
   - **Chat ID** sẽ tự động lấy từ tin nhắn của khách hàng.

2. **Node "AI Parse Order" (Agent - Claude Haiku)**:
   - Chọn **credentials** Anthropic API Key.
   - **Prompt** đã được tối ưu hóa để phân tích đơn hàng tự nhiên (ví dụ: "2 pizza + 1 coke" → `{ "items": "2 Margherita Pizza + 1 Coke", "valid": true }`).
   - **Lưu ý**: Nếu AI trả về `valid: false`, workflow sẽ tự động gửi tin nhắn lỗi cho khách hàng.

3. **Node "Save Order" (Google Sheets)**:
   - Chọn **credentials** Google Sheets API.
   - **Sheet Name**: Nhập tên chính xác của bảng Google Sheets (`Restaurant Orders`).
   - **Operation**: Đặt là `append` (thêm mới).
   - **Columns to Write**:
     - `Queue Number` (auto-generate, ví dụ: `ORD-001`).
     - `Chat ID`, `Name`, `Order`, `Status=Pending`, `Order Time`, `Order Date`.
     - **Cột `Last Status Sent`** sẽ để trống ban đầu.

4. **Node "Find Order to Cancel" / "Find Order Status" (Google Sheets)**:
   - Chọn cùng **credentials** Google Sheets API.
   - **Sheet Name**: `Restaurant Orders`.
   - **Query**: Sử dụng `WHERE` để tìm đơn hàng theo `Queue Number` hoặc `Chat ID`.

5. **Node "Can Cancel?" (If)**:
   - **Logic**: Chỉ cho phép hủy đơn khi `Status = Pending`.
   - Nếu không thỏa mãn, workflow sẽ gửi tin nhắn "Không thể hủy đơn này" cho khách hàng.

6. **Node "Send Confirmation" / "Send Cancel Reply" / "Send Status" (Telegram)**:
   - Chọn **credentials** Telegram Bot Token.
   - **Chat ID**: Lấy từ `jsonPath: $.json.chat.id` (tự động lấy từ tin nhắn khách hàng).
   - **Text**: Sử dụng **code nodes** (`Build Order Response`, `Build Status Reply`) để xây dựng tin nhắn động.

7. **Node "Send Menu" / "Send My Orders" (Telegram)**:
   - **Menu**: Sử dụng tin nhắn định sẵn (ví dụ: danh sách món ăn).
   - **My Orders**: Lấy dữ liệu từ Google Sheets theo `Chat ID` và hiển thị 5 đơn gần nhất.

##### **B. Cấu Hình Phần 2: Staff Status Notifier**
1. **Node "Every 1 Minute" (Schedule Trigger)**:
   - Đặt **cron expression**: `* * * * *` (chạy mỗi phút).
   - **Lưu ý**: Không thể dùng trigger từ Google Sheets vì nó không phát hiện được thay đổi cụ thể.

2. **Node "Read All Rows" (Google Sheets)**:
   - Chọn **credentials** Google Sheets API.
   - **Sheet Name**: `Restaurant Orders`.
   - **Operation**: `list`.

3. **Node "Detect Changed Row" (Code)**:
   - **Logic**:
     - Bỏ qua hàng nếu không có `Queue Number` hoặc `Chat ID`.
     - Bỏ qua nếu `Status = Pending` (không cần thông báo).
     - Bỏ qua nếu `Status = Last Status Sent` (đã gửi thông báo trước).
     - Chỉ giữ lại hàng nếu `Status` đã thay đổi.

4. **Node "Prep Sheet Update" / "Save Last Status Sent" (HTTP Request)**:
   - **Cập nhật cột `Last Status Sent`** để tránh gửi thông báo trùng lặp.
   - **API Endpoint**: `https://sheets.googleapis.com/v4/spreadsheets/{sheetId}/values/{range}?valueInputOption=RAW`.
   - **Credentials**: Google Sheets API.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Gửi tin nhắn mẫu cho bot Telegram (ví dụ: `/start`, `/help`, `2 pizza + 1 coke`).
   - Kiểm tra Google Sheets có cập nhật đơn hàng không.
   - Thay đổi trạng thái đơn trên Google Sheets và kiểm tra thông báo tự động được gửi không.

2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
1. **Kết hợp với Slack/Email**:
   - Thêm node **Slack** hoặc **Email** để thông báo cho nhân viên khi có đơn mới.
   - Ví dụ: Khi đơn hàng mới được thêm vào Google Sheets, gửi tin nhắn Slack cho team.

2. **Lưu Log Tất Cả Các Thao Tác**:
   - Thêm node **HTTP Request** để ghi log vào một bảng Google Sheets khác với nội dung:
     - Thời gian, Chat ID, Action (Place Order / Cancel / Status Check), Status Before/After.

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **Schedule Trigger** để gửi báo cáo tổng hợp đơn hàng hàng ngày cho quản lý.
   - Ví dụ: "Đơn hàng trong ngày: 50 đơn, Doanh thu: 2.500.000 VND".

4. **Tùy Chỉnh Menu Động**:
   - Thay vì gửi menu cố định, kết nối với **Google Sheets Menu** để cập nhật danh sách món ăn tự động.

5. **Phân Loại Khách Hàng**:
   - Thêm cột `Customer Tier` (VIP, Thường, Mới) và gửi tin nhắn cá nhân hóa cho VIP.

6. **Hỗ Trợ Nhiều Ngôn Ngữ**:
   - Sử dụng **LLM** để dịch tin nhắn của khách hàng sang tiếng Việt nếu cần.
   - Ví dụ: Nếu khách hàng gửi đơn bằng tiếng Anh, AI sẽ tự động chuyển thành tiếng Việt trước khi phân tích.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để các sếp quán hàng tự động hóa toàn bộ quy trình quản lý đơn đặt hàng, từ nhận đơn đến cập nhật trạng thái và gửi thông báo cho khách hàng. **Không cần code**, chỉ cần cài đặt và chạy – tiết kiệm thời gian, giảm lỗi và tăng trải nghiệm khách hàng!

**Hành động ngay hôm nay:**
1. **Chuẩn bị tài khoản** Telegram Bot, Google Sheets và API Key Claude Haiku.
2. **Import workflow** và cấu hình credentials.
3. **Test và bật Active** để bắt đầu tự động hóa đơn hàng!

👉 **Bạn có thể tùy chỉnh workflow này cho nhiều quán hàng khác nhau** bằng cách thay đổi tên bot và sheet. Hãy chia sẻ kết quả sau khi áp dụng nhé! 🚀

---
**📌 Lưu ý cuối cùng**:
- Nếu gặp vấn đề, tham khảo [hướng dẫn gốc](https://n8n.io/workflows/14136) hoặc liên hệ cộng đồng n8n trên [Discord](https://n8n.io/community).
- Để workflow chạy ổn định, **không nên dùng phiên bản n8n miễn phí** (n8n.cloud) vì có giới hạn node và không hỗ trợ schedule trigger liên tục. **Self-hosted là lựa chọn tối ưu!**