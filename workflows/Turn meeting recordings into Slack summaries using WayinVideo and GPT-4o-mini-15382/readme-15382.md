---
title: "🚀 Tự động hóa ghi chú cuộc họp: WayinVideo + GPT-4o-mini + Slack + Google Sheets"
description: "Giải pháp tự động hóa hoàn toàn không cần code để chuyển đổi bản ghi cuộc họp thành tóm tắt Slack và lưu trữ trong Google Sheets"
slug: "tu-dong-hoa-ghi-chu-cuoc-hop-wayinvideo-gpt4o-slack-sheets"
tags: [n8n, automation, no-code, ai, google-sheets, slack, wayinvideo]
keywords: [n8n workflow, tự động hóa cuộc họp, tóm tắt cuộc họp, wayinvideo, gpt-4o-mini, slack, google sheets]
---

# 🚀 Tự động hóa ghi chú cuộc họp: WayinVideo + GPT-4o-mini + Slack + Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có biết rằng mỗi tuần phải dành bao nhiêu giờ để ghi chú cuộc họp? Với workflow này, các sếp có thể tự động hóa hoàn toàn quy trình này, tiết kiệm hàng giờ quý giá mỗi tuần.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 2-3 giờ mỗi tuần cho việc ghi chú thủ công
- Tự động hóa hoàn toàn quy trình ghi chú cuộc họp
- Tạo tóm tắt chất lượng cao bằng AI (GPT-4o-mini)
- Lưu trữ toàn bộ thông tin cuộc họp trong Google Sheets
- Chia sẻ thông tin quan trọng với toàn bộ team qua Slack
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WayinVideo (API Key)
- Tài khoản OpenAI (API Key)
- Tài khoản Slack (OAuth2 Credential)
- Tài khoản Google (OAuth2 Credential)
- Google Sheet với tên tab "Meeting Log" và các cột: Meeting Title, Team, Date, Duration (min), Attendees, Summary, Action Items, Decisions, Next Steps, Recording URL, Slack Channel, Slack Message TS, Logged On
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/15382)
2. Click vào nút "Copy JSON"
3. Trong n8n Editor, click vào "Import from Clipboard"
4. Dán JSON đã copy và click "Import"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node 2. WayinVideo — Submit Transcription**:
   - Thay thế `YOUR_WAYINVIDEO_API_KEY` bằng API Key của bạn
   - Đảm bảo URL của cuộc họp được nhập đúng định dạng

2. **Node 4. WayinVideo — Get Transcript Results**:
   - Thay thế `YOUR_WAYINVIDEO_API_KEY` bằng API Key của bạn

3. **Node 9. OpenAI — GPT-4o-mini Model**:
   - Kết nối OpenAI credential của bạn
   - Đảm bảo model được chọn là `gpt-4o-mini`

4. **Node 11. Slack — Post Action Items**:
   - Kết nối Slack OAuth2 credential của bạn
   - Thay thế `YOUR_SLACK_CHANNEL_ID` bằng ID kênh Slack của bạn

5. **Node 12. Google Sheets — Log Meeting Summary**:
   - Kết nối Google Sheets OAuth2 credential của bạn
   - Thay thế `YOUR_GOOGLE_SHEET_ID` bằng ID của Google Sheet của bạn
   - Đảm bảo tên tab là "Meeting Log" và có các cột như đã chỉ định

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu bằng cách submit một URL cuộc họp mẫu
2. Kiểm tra kết quả trên Slack và Google Sheets
3. Bật Active workflow để sử dụng thực tế

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp với các nền tảng khác**: Kết nối với Microsoft Teams hoặc Zoom để tự động lấy URL cuộc họp
2. **Tùy chỉnh prompt AI**: Chỉnh sửa prompt trong node 8 để phù hợp với nhu cầu cụ thể của team
3. **Thông báo lỗi**: Thêm node gửi email hoặc Slack thông báo khi có lỗi xảy ra trong quy trình
4. **Lịch sử tìm kiếm**: Tạo một Google Sheet riêng để lưu trữ lịch sử tìm kiếm và kết quả

### 📌 Kết luận
Workflow này mang lại giải pháp toàn diện cho việc tự động hóa ghi chú cuộc họp, giúp các sếp tiết kiệm thời gian quý giá và tập trung vào những việc quan trọng hơn. Với sự kết hợp của WayinVideo, GPT-4o-mini, Slack và Google Sheets, các sếp có thể dễ dàng quản lý và chia sẻ thông tin cuộc họp một cách hiệu quả. Hãy áp dụng ngay để trải nghiệm sự khác biệt!