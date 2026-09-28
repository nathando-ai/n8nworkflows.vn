---
title: "🚀 Tự động phát hiện deal đóng băng trong Zoho CRM bằng Gemini AI và Gmail"
description: "Hướng dẫn xây dựng hệ thống n8n tự động quét deal đóng băng hàng tuần trên Zoho CRM, phân tích rủi ro bằng Gemini AI, gửi cảnh báo qua Gmail và tạo task ưu tiên."
slug: "tu-dong-phat-hien-deal-dong-bang-zoho-crm-gemini-ai"
tags: [n8n, automation, zoho-crm, gemini-ai, gmail, sales-automation]
keywords: [n8n workflow, zoho crm automation, gemini ai crm, tu dong hoa ban hang, canh bao deal dong bang]
keywords: [n8n workflow, zoho crm automation, gemini ai crm, tự động hóa bán hàng, cảnh báo deal đóng băng]
---

# 🚀 Tự động phát hiện deal đóng băng trong Zoho CRM bằng Gemini AI và Gmail

Các sếp có đang gặp tình trạng nhân viên sales "bỏ quên" các cơ hội (deals) tiềm năng trong CRM, khiến doanh số tụt giảm mà không rõ nguyên nhân? Việc kiểm tra thủ công hàng trăm deal mỗi tuần vừa tốn thời gian, vừa dễ bỏ sót các dấu hiệu rủi ro.

Giải pháp đây rồi! Workflow n8n này sẽ tự động hóa toàn bộ quy trình: định kỳ quét dữ liệu trên Zoho CRM, tính toán thời gian không tương tác (inactivity), sử dụng sức mạnh của **Gemini AI** để chấm điểm sức khỏe deal, đồng thời tự động gửi email cảnh báo qua **Gmail** và tạo task khẩn cấp ngay trong CRM cho các deal có nguy cơ cao. 100% tự động, không tốn một giọt mồ hôi thủ công!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Chạy lịch trình hàng tuần (Weekly Scan) mà không cần can thiệp thủ công.
- **AI thông minh:** Gemini AI phân tích sâu dữ liệu deal, đưa ra điểm rủi ro (Risk Score) và đề xuất hành động cụ thể.
- **Phản ứng tức thì:** Tự động gửi email cảnh báo đến sales phụ trách và tạo task độ ưu tiên cao trong Zoho CRM ngay lập tức nếu phát hiện deal có vấn đề.
- **Tối ưu chuyển đổi:** Giúpội ngũ sales cứu vãn kịp thời các deal sắp "chết", tăng tỷ lệ chốt đơn.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Zoho CRM Account:** Tài khoản quản trị để kết nối API (OAuth2).
- **Google Gemini API Key:** Sử dụng cho các node AI phân tích deal.
- **Gmail Account:** Tài khoản Gmail đã cấu hình OAuth2 để gửi email cảnh báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc sử dụng tính năng copy/paste JSON workflow.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 12 nodes được thiết kế tỉ mỉ. Các sếp cần cấu hình chính xác các điểm sau:

- **Weekly Deal Health Scan Trigger (`scheduleTrigger`):** Cài đặt thời gian chạy định kỳ (ví dụ: mỗi thứ Hai hàng tuần).
- **Fetch Active Deals From Zoho & Create At-Risk Task (`httpRequest`):** Kết nối tài khoản Zoho thông qua **Zoho OAuth2 API**. Đảm bảo endpoint API lấy danh sách deals và tạo task trỏ đúng vào region của tài khoản Zoho (US, EU, IN,...).
- **Calculate Deal Metrics (`code`):** Kiểm tra đoạn code JavaScript tính toán thời gian không tương tác (inactivity age) và tuổi của giai đoạn (stage age) xem đã khớp với quy tắc kinh doanh của công ty chưa.
- **Google Gemini Chat Model & AI Deal Health Scoring (`lmChatGoogleGemini` & `chainLlm`):** Thêm Google Gemini API credentials. Tinh chỉnh Prompt trong node AI để model đánh giá đúng trọng tâm sản phẩm/dịch vụ của doanh nghiệp.
- **Send At-Risk Alert Email (`gmail`):** Kết nối tài khoản Gmail qua OAuth2. Thay thế địa chỉ email nhận bằng trường email của chủ sở hữu deal (deal owner) lấy trực tiếp từ dữ liệu Zoho CRM.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một vài record mẫu để kiểm tra luồng dữ liệu từ Zoho -> AI -> Gmail/Task.
- Sau khi chắc chắn mọi thứ hoạt động trơn tru, hãy bật trạng thái **Active** cho workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ gửi qua Gmail, các sếp có thể nối thêm node **Telegram** hoặc **Slack** để bắn thông báo thẳng vào nhóm chat sales để anh em phản ứng nhanh hơn.
- **Lưu log báo cáo:** Lưu kết quả quét deal hàng tuần vào **Google Sheets** để làm báo cáo hiệu suất (Dashboard) cho quản lý theo dõi theo tháng.
- **Tùy chỉnh ngưỡng rủi ro:** Điều chỉnh logic ở node **Is Deal At-Risk?** để phù hợp với khẩu vị rủi ro của từng loại sản phẩm.

### 📌 Kết luận
Hệ thống giám sát deal tự động này là "vũ khí bí mật" giúp các Sales Manager quản lý sát sao đội ngũ mà không tốn công kiểm tra thủ công từng deal. Hãy triển khai ngay hôm nay để không bỏ lỡ bất kỳ cơ hội doanh thu nào!