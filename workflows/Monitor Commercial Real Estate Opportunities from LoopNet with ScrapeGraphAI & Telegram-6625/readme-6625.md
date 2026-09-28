---
title: "🚀 Tự động săn bất động sản thương mại từ LoopNet với ScrapeGraphAI & Telegram"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu LoopNet bằng ScrapeGraphAI, phân tích cơ hội đầu tư bất động sản và gửi cảnh báo qua Telegram, lưu log vào Google Sheets."
slug: "tu-dong-san-bat-dong-san-thuong-mai-loopnet-n8n"
tags: [n8n, automation, ai-summarization, market-research, telegram, google-sheets]
keywords: [n8n workflow, loopnet scraper, scrapegraphai, telegram alert, bất động sản thương mại, tự động hóa n8n]
---

# 🚀 Tự động săn bất động sản thương mại từ LoopNet với ScrapeGraphAI & Telegram

Các nhà đầu tư và môi giới bất động sản thương mại (CRE) luôn đối mặt với một thách thức lớn: thị trường thay đổi từng giờ, việc dò tìm các mặt bằng tiềm năng trên LoopNet hay các nền tảng lớn tốn hàng giờ đồng hồ mỗi ngày. Nếu bỏ lỡ một tin đăng "ngon", các sếp sẽ mất cơ hội vàng vào tay đối thủ.

Giải pháp là gì? Hãy để **n8n** thay các sếp làm việc đó 24/7! Workflow này tự động quét dữ liệu, phân tích thông minh bằng AI, lọc ra các cơ hội đầu tư tốt nhất và bắn thông báo trực tiếp về điện thoại qua Telegram, đồng thời lưu trữ toàn bộ lịch sử vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Quét thị trường bất động sản hàng ngày mà không cần thao tác thủ công.
- **Cảnh báo tức thì:** Nhận tin nhắn Telegram ngay khi có cơ hội đầu tư tiềm năng (giá tốt, diện tích chuẩn).
- **Tránh spam:** Chỉ gửi thông báo khi thực sự tìm thấy cơ hội, không làm phiền các sếp bằng tin nhắn rác.
- **Lưu trữ dữ liệu khoa học:** Tự động ghi nhận lịch sử thị trường vào Google Sheets để phục vụ phân tích xu hướng dài hạn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn (Self-hosted hoặc Cloud).
- **ScrapeGraphAI API Key:** Dùng để cào dữ liệu thông minh từ web.
- **Telegram Bot:** Tạo qua `@BotFather` để lấy Token và Chat ID.
- **Google Sheets:** Tài khoản Google Cloud / Service Account để ghi log dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ n8n.io (ID: 6625) hoặc copy trực tiếp đoạn mã JSON và dán vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 6 nodes chính hoạt động nhịp nhàng. Các sếp cần cấu hình các điểm sau:

- **Daily CRE Scanner (`scheduleTrigger`):** 
  - Mặc định chạy mỗi 24 giờ. Các sếp có thể điều chỉnh lại lịch chạy (ví dụ: 8h sáng hàng ngày) cho phù hợp múi giờ và chiến dịch.
- **CRE Data Collector (`httpRequest`):** 
  - Cấu hình API endpoint và Header chứa ScrapeGraphAI API Key để hệ thống tự động cào dữ liệu từ LoopNet hoặc các trang đích chỉ định.
- **CRE Analyzer & Dashboard (`code`):** 
  - Node này dùng mã JavaScript để xử lý, tính toán các chỉ số trung bình (giá thuê/sqft, số lượng tài sản, điểm số cơ hội). Không cần chỉnh sửa code trừ khi các sếp muốn custom logic lọc riêng.
- **Check for Opportunities (`if`):** 
  - Kiểm tra biến `opportunities_found > 0`. Nếu đúng, chuyển sang bước gửi tin nhắn; nếu không, tiếp tục quy trình lưu log mà không làm phiền các sếp.
- **Send Opportunity Alert (`telegram`):** 
  - Kết nối với **Telegram Bot Credentials** của các sếp. Điền chính xác `Chat ID` nhóm hoặc cá nhân để nhận báo cáo tóm tắt kèm các cơ hội top đầu.
- **Log to Google Sheets (`googleSheets`):** 
  - Kết nối Google Account, trỏ tới Spreadsheet ID và chọn Sheet name là `CRE_Analysis` để lưu vết dữ liệu hàng ngày.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thủ công một lần, kiểm tra xem dữ liệu có đổ về Telegram và Google Sheets chuẩn chỉnh chưa.
- Nếu mọi thứ xanh mướt, hãy gạt công tắc sang **Active** để hệ thống tự chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp AI LLM (OpenAI/Claude):** Có thể bổ sung thêm một node AI Agent sau bước cào dữ liệu để viết lời nhận xét chi tiết hơn về tiềm năng sinh lời của từng bất động sản.
- **Đa kênh thông báo:** Ngoài Telegram, các sếp có thể gắn thêm node **Slack** hoặc **Discord** để team môi giới cùng nắm thông tin.
- **Báo cáo tuần:** Tạo thêm một nhánh chạy vào Chủ Nhật hàng tuần để tổng hợp số liệu từ Google Sheets và gửi biểu đồ tóm tắt xu hướng thị trường.

### 📌 Kết luận
Với workflow n8n này, việc nghiên cứu thị trường bất động sản thương mại không còn là nỗi ám ảnh tốn thời gian. Hãy thiết lập ngay hôm nay để luôn là người đầu tiên nắm bắt những cơ hội vàng trên thị trường!