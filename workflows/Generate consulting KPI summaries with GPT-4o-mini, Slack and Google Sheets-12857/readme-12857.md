---
title: "🚀 Tự động hóa tóm tắt KPI tư vấn với GPT-4o-mini, Slack và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động tổng hợp KPI, phân tích thông minh bằng AI, lưu trữ Google Sheets và cảnh báo qua Slack/Email."
slug: "tu-dong-hoa-tom-tat-kpi-tu-van-gpt-4o-mini"
tags: [n8n, automation, ai-summarization, google-sheets, slack, openai]
keywords: [n8n workflow, tự động hóa KPI, GPT-4o-mini, Google Sheets, Slack automation]
---

# 🚀 Tự động hóa tóm tắt KPI tư vấn với GPT-4o-mini, Slack và Google Sheets

Các sếp làm trong ngành tư vấn hoặc quản lý dự án chắc chắn đều ngán ngẩm cảnh mỗi ngày phải "đào bới" dữ liệu từ hàng loạt dashboard, copy-paste số liệu thủ công rồi ngồi viết báo cáo KPI dài dằng dặc gửi sếp lớn hoặc khách hàng. Việc này vừa tốn thời gian, dễ sai sót, lại làm lỡ mất các cơ hội xử lý khủng hoảng khi chỉ số KPI rớt thảm hại.

Để giải quyết triệt để nỗi đau này, workflow n8n được thiết kế bởi chuyên gia Hyrum Hurst sẽ giúp các sếp tự động hóa 100% quy trình: từ việc kéo dữ liệu KPI, phân tích thông minh bằng AI, lưu lịch sử, đến việc tự động bắn tin báo cáo lên Slack và gửi email chỉ trong một nốt nhạc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Kéo dữ liệu định kỳ mỗi ngày mà không cần chạm tay vào nút "Run".
- **AI thông minh phân tích:** Sử dụng GPT-4o-mini để lọc ra các insight đắt giá từ đống số liệu thô.
- **Cảnh báo tức thì:** Tự động phát hiện KPI nguy hiểm và bắn alert khẩn cấp qua Slack/Gmail.
- **Lưu trữ chuẩn chỉnh:** Tự động ghi log toàn bộ số liệu vào Google Sheets và lên lịch họp follow-up khi cần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản **OpenAI API Key** (cho model GPT-4o-mini).
- Tài khoản **Google Sheets** và file Google Sheet mẫu để lưu log KPI.
- Tài khoản **Google Calendar** (để tự động lên lịch họp).
- Workspace **Slack** và Bot Token để gửi tin nhắn cảnh báo/báo cáo.
- Tài khoản **Gmail** để gửi email báo cáo chi tiết.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow (hoặc tải file JSON từ nguồn gốc) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node quan trọng sau:
- **Daily KPI Report Trigger (`scheduleTrigger`):** Cài đặt khung thời gian chạy báo cáo định kỳ mỗi ngày (ví dụ: 8:00 sáng).
- **Fetch Client Dashboard 1 & 2 KPIs (`httpRequest`):** Điền Endpoint API chính xác của các hệ thống dashboard khách hàng để kéo dữ liệu thô.
- **Log KPIs to Google Sheets (`googleSheets`):** Kết nối tài khoản Google, chọn đúng File Sheet và Sheet Name để lưu dữ liệu.
- **OpenAI GPT-4o-mini (`lmChatOpenAi`):** Cung cấp OpenAI API Key và cấu hình model `gpt-4o-mini` cho Agent.
- **Generate KPI Summary and Insights (`agent`):** Tùy chỉnh System Prompt để AI viết báo cáo đúng văn phong mong muốn.
- **Check Critical KPI Thresholds (`switch`):** Thiết lập điều kiện ngưỡng KPI (ví dụ: nếu KPI < 50% thì chuyển nhánh cảnh báo khẩn cấp).
- **Post Summary to Slack / Send Critical Alert to Slack (`slack`):** Chọn Channel Slack nhận báo cáo chung và channel nhận cảnh báo khẩn cấp.
- **Email Full Report / Email Critical Alert (`gmail`):** Cấu hình tài khoản gửi email cho khách hàng hoặc ban quản trị.
- **Schedule Follow-up Meeting (`googleCalendar`):** Kết nối lịch để hệ thống tự động tạo lịch họp khi có chỉ số bất thường.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với dữ liệu test để kiểm tra xem các node có chạy xanh (thành công) hết không.
- Bật công tắc **Active** ở góc trên bên phải để n8n tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram:** Thay vì chỉ dùng Slack, các sếp có thể nhân bản nhánh cảnh báo sang Telegram Bot để nhận thông báo ngay trên điện thoại cá nhân.
- **Lưu trữ lịch sử AI:** Thêm một node Google Sheets ở nhánh AI để lưu lại toàn bộ các nhận định, insight mà GPT-4o-mini đã tạo ra, phục vụ cho việc đối chiếu xu hướng dài hạn.
- **Tùy biến Prompt AI:** Thêm các quy tắc cụ thể vào LangChain Agent để AI đánh giá theo tone giọng nghiêm túc, hài hước hoặc chuyên gia tài chính tùy thuộc vào đối tượng nhận báo cáo.

### 📌 Kết luận
Workflow tự động hóa tóm tắt KPI với GPT-4o-mini này là trợ thủ đắc lực giúp các agency tư vấn và quản lý dự án tiết kiệm hàng chục giờ mỗi tuần. Hãy thiết lập ngay hôm nay để tối ưu hóa hiệu suất vận hành doanh nghiệp của các sếp!