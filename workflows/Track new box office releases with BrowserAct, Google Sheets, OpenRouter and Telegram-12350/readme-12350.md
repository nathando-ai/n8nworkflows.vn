---
title: "🎬 Tự động theo dõi phim mới ra rạp với n8n: BrowserAct + Google Sheets + OpenRouter + Telegram"
description: "Hướng dẫn tự động hóa 100% không cần code để theo dõi phim mới ra rạp, lọc trùng dữ liệu và gửi thông báo Telegram hàng tuần"
slug: "tu-dong-theo-doi-phim-moi-ra-rap-n8n"
tags: [n8n, automation, no-code, phim, box-office, telegram]
keywords: [n8n workflow, tự động hóa phim, box office, google sheets, openrouter]
---

# 🎬 Tự động theo dõi phim mới ra rạp với n8n: BrowserAct + Google Sheets + OpenRouter + Telegram

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp trong ngành điện ảnh khi phải theo dõi thủ công dữ liệu box office hàng tuần. Giới thiệu workflow như giải pháp tự động hóa hoàn chỉnh.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 2-3 giờ mỗi tuần cho việc theo dõi thủ công
- Dữ liệu box office được cập nhật tự động hàng tuần
- Lọc tự động phim đã có trong cơ sở dữ liệu
- Thông báo Telegram được định dạng chuyên nghiệp
- Lưu trữ dữ liệu lịch sử đầy đủ trong Google Sheets
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản BrowserAct với template **Box Office Trifecta**
- API Key từ OpenRouter (Google Gemini)
- Quyền truy cập Google Sheets với bảng có tên "Movie history" và các cột: `Name`, `Budget`, `Opening_Weekend`, `Gross_Worldwide`, `Cast`, `Link`, `Summary`
- Thông tin đăng nhập Telegram (Bot Token và Channel ID)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/12350)
2. Click vào nút "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Extract From IMDB Box Office"**:
   - Cấu hình credentials BrowserAct
   - Đảm bảo đã lưu template **Box Office Trifecta** trong tài khoản BrowserAct

2. **Node "OpenRouter"**:
   - Cấu hình credentials OpenRouter
   - Đảm bảo đã chọn model "google/gemini-3-pro-preview"

3. **Node "Retrieve Stored Data"**:
   - Cấu hình credentials Google Sheets
   - Điền tên bảng là "Movie history"

4. **Node "Store Extracted Data"**:
   - Cấu hình credentials Google Sheets
   - Đảm bảo đã chọn operation "append"

5. **Node "Send Post to Telegram Channel"**:
   - Cấu hình credentials Telegram
   - Điền Channel ID của kênh Telegram muốn gửi thông báo

#### 3. Kích hoạt ⚡️
1. Click vào nút "Test Workflow" để kiểm tra dữ liệu mẫu
2. Sau khi xác nhận hoạt động bình thường, click vào nút "Activate" để kích hoạt workflow
3. Workflow sẽ chạy tự động hàng tuần theo lịch trình đã cài đặt

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh thông báo**: Chỉnh sửa prompt trong node "Create posts for Telegram" để thay đổi định dạng thông báo
2. **Thêm kênh thông báo**: Kết nối thêm node để gửi thông báo đến Slack hoặc Discord
3. **Lịch sử truy vấn**: Lưu log các lần chạy workflow để theo dõi hiệu suất
4. **Báo cáo định kỳ**: Tạo báo cáo tổng hợp từ dữ liệu trong Google Sheets và gửi qua email

### 📌 Kết luận
Workflow này giúp các sếp trong ngành điện ảnh tiết kiệm thời gian quý giá, tự động hóa quy trình theo dõi box office hàng tuần và nhận thông báo chuyên nghiệp qua Telegram. Hãy áp dụng ngay để nâng cao hiệu quả làm việc!