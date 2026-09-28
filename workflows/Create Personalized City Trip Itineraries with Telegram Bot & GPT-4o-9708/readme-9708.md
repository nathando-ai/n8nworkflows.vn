---
title: "🌟 Tự Động Hoá Lập Kế Hoạch Du Lịch Cá Nhân Hóa Cho Thành Phố Bằng Telegram Bot & GPT-4o (N8n)"
description: "Workflow này tự động tạo kế hoạch du lịch cá nhân hóa cho khách hàng qua Telegram Bot, kết hợp với GPT-4o để phân tích nhu cầu và gửi kết quả chi tiết về từng ngày. Giúp doanh nghiệp tiết kiệm thời gian lên đến 90% so với cách làm thủ công."
slug: "tieu-dong-hoa-ke-hoach-du-lich-canh-nhan-hoa-telegram-gpt-4o"
tags: [n8n, automation, no-code, telegram-bot, ai-ml, du-lich]
keywords: [n8n workflow du lịch, tự động hóa kế hoạch du lịch, telegram bot gpt-4o, tạo kế hoạch du lịch cá nhân hóa, n8n ai/ml api]
---

# 🚀 **Tự Động Hoá Lập Kế Hoạch Du Lịch Cá Nhân Hóa Cho Thành Phố Với Telegram Bot & GPT-4o**

Hiện nay, việc tạo kế hoạch du lịch cá nhân hóa cho khách hàng thường tốn thời gian và dễ mắc sai sót khi làm thủ công. Các sếp phải dành hàng giờ để nghiên cứu điểm tham quan, thời gian di chuyển, và lựa chọn các địa điểm phù hợp với sở thích của khách hàng. **Workflow này giải quyết vấn đề này bằng cách tự động hóa toàn bộ quy trình, chỉ cần khách hàng gửi yêu cầu qua Telegram!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 và xử lý nhiều yêu cầu đồng thời, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) với tài nguyên tối thiểu 2GB RAM.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 90%** so với cách làm thủ công.
- **Cá nhân hóa hoàn toàn** kế hoạch du lịch dựa trên sở thích của khách hàng (du lịch gia đình, du lịch cực hạn, du lịch văn hóa...).
- **Hoạt động liên tục 24/7** mà không cần can thiệp của con người.
- **Trải nghiệm tương tác tự nhiên** với Telegram Bot, giúp khách hàng cảm thấy được chăm sóc cá nhân.
- **Dễ dàng mở rộng** cho nhiều thành phố và loại hình du lịch khác nhau.
:::

---

### 🔧 **Yêu cầu cần thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - Tạo bot trên [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Cài đặt bot vào nhóm hoặc chat cá nhân để khách hàng tương tác.
2. **API Key cho AI/ML API**:
   - Đăng ký tài khoản tại [AI/ML API](https://aimlapi.com/) và lấy **API Key**.
3. **Thiết lập n8n Self-hosted**:
   - Cài đặt n8n trên VPS hoặc máy chủ riêng (hướng dẫn chi tiết [tại đây](https://docs.n8n.io/hosting/installation/)).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải workflow từ [n8n.io/workflows/9708](https://n8n.io/workflows/9708) hoặc tải file JSON đã cung cấp.
- **Bước 2**: Mở **n8n Editor** và chọn **Import Workflow** (từ menu bên trái).
- **Bước 3**: Chọn file JSON và nhấn **Import**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **15 node** với các chức năng chính sau. Các sếp cần chú ý cấu hình các node sau:

##### **A. Cấu hình Telegram Bot**
1. **Node "Start: Receive Message on Telegram"**:
   - Điền **API Token** từ BotFather vào trường `credentials.telegramApi`.
   - Chọn **Chat ID** của bot (có thể lấy từ [@userinfobot](https://t.me/userinfobot)).
   - Chọn **Trigger Type**: `message` (để bot lắng nghe tin nhắn).

2. **Node "Show Typing Indicator"**:
   - Sử dụng cùng **credentials.telegramApi** như node trên.
   - Không cần cấu hình thêm, node này sẽ tự động hiển thị trạng thái "đang gõ" khi bot xử lý yêu cầu.

3. **Node "Send message to Telegram"**:
   - Sử dụng cùng **credentials.telegramApi**.
   - Node này sẽ gửi kết quả cuối cùng về cho khách hàng.

##### **B. Cấu hình AI/ML API (GPT-4o)**
1. **Node "Generate personalized answer"**:
   - Điền **API Key** vào `credentials.aimlApi` (từ tài khoản AI/ML API).
   - Node này sẽ gọi API GPT-4o để tạo kế hoạch du lịch dựa trên:
     - **Thành phố** (do khách hàng nhập).
     - **Số ngày** (mặc định là 3 ngày).
     - **Loại du lịch** (cozy, extreme, family, luxury...).

##### **C. Cấu hình Prompt cho từng loại du lịch**
Workflow đã định sẵn **10 loại prompt** cho các loại du lịch khác nhau. Các sếp không cần chỉnh sửa nội dung prompt (nếu muốn tối ưu hóa, có thể cập nhật tại các node `set` như `cozy_prompt`, `luxury_prompt`, v.v.).

##### **D. Node "Route by Input Type" (Switch)**
- Node này phân loại yêu cầu của khách hàng dựa trên **prefix** (ví dụ: `/cozy`, `/luxury`).
- Nếu khách hàng không nhập prefix, bot sẽ sử dụng **prompt mặc định** (tự động hóa).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi tin nhắn mẫu đến bot (ví dụ: `/luxury Paris, 4-day plan`).
   - Kiểm tra kết quả trả về có hợp lý không.
2. **Bật Active**:
   - Nhấn **Active** ở thanh menu trên cùng của n8n Editor.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm nhiều thành phố và loại du lịch**:
   - Các sếp có thể **tạo thêm prompt** cho các thành phố mới (ví dụ: `hanoi_prompt`, `ho_chi_minh_prompt`) và kết nối với node `Route by Input Type`.

2. **Lưu lịch sử yêu cầu**:
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu tất cả yêu cầu và kết quả du lịch. Điều này giúp theo dõi và phân tích hiệu suất của bot.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng node **Email** hoặc **Slack** để báo cáo số lượng yêu cầu và thành phố phổ biến nhất cho đội ngũ marketing.

4. **Cập nhật nội dung động**:
   - Nếu muốn cập nhật thông tin mới về điểm tham quan, các sếp có thể **tạo một node Set** mới để lưu trữ danh sách địa điểm và kết hợp với AI để tạo kế hoạch.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các doanh nghiệp du lịch muốn tự động hóa việc tư vấn và tạo kế hoạch du lịch cá nhân hóa. Với chỉ **vài bước thiết lập**, các sếp có thể tiết kiệm thời gian và nâng cao trải nghiệm khách hàng.

**Hãy áp dụng ngay và bắt đầu tự động hóa du lịch của mình!** 🌍✨

---
**Ghi chú cuối cùng**:
- Nếu gặp vấn đề với API Key hoặc Telegram Bot, hãy kiểm tra lại **credentials** trong các node.
- Để tối ưu hóa hiệu suất, các sếp nên **cập nhật phiên bản n8n mới nhất** và **tăng tài nguyên VPS** nếu xử lý nhiều yêu cầu đồng thời.