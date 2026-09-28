---
title: "🚀 Tự động tạo Tuyên bố Khả năng tiếp cận Website (Accessibility Statement) chuẩn EU với AI và WAVE"
description: "Hướng dẫn xây dựng workflow n8n tự động quét website, phân tích lỗi tiếp cận bằng WAVE API, sử dụng Google Gemini AI để soạn thảo Tuyên bố khả năng tiếp cận (Accessibility Statement) tuân thủ Đạo luật Khả năng tiếp cận Châu Âu (EAA) và gửi kết quả qua Gmail."
slug: "tu-dong-tao-accessibility-statement-voi-ai-va-wave"
tags: [n8n, automation, ai, google-gemini, wave-api, eaa-compliance, seo]
keywords: [n8n workflow, accessibility statement, european accessibility act, wave api, google gemini, tự động hóa n8n]
---

# 🚀 Tự động tạo Tuyên bố Khả năng tiếp cận Website chuẩn EU với AI và WAVE

Các doanh nghiệp hoạt động tại châu Âu đang phải đối mặt với áp lực lớn từ **Đạo luật Khả năng tiếp cận Châu Âu (European Accessibility Act - EAA)**. Việc thiếu một Tuyên bố Khả năng tiếp cận (*Erklärung zur Barrierefreiheit*) hợp pháp trên website có thể dẫn đến rủi ro pháp lý lớn. Tuy nhiên, việc tự tay kiểm tra mã nguồn, phân tích lỗi và soạn thảo một văn bản pháp lý chuẩn chỉnh tốn rất nhiều thời gian và chi phí.

Workflow n8n này sẽ giải quyết triệt để nỗi đau đó bằng cách tự động hóa 100%: quét website, lấy báo cáo lỗi từ WAVE API, giao cho AI Agent phân tích và tự động xuất ra file `.html` hoàn chỉnh, sau đó gửi thẳng vào email của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tuân thủ pháp lý EAA:** Tự động tạo tài liệu pháp lý bắt buộc cho website doanh nghiệp một cách nhanh chóng.
- **Tiết kiệm 90% thời gian:** Thay vì mất hàng giờ kiểm tra code và viết lách, AI sẽ xử lý toàn bộ từ A-Z chỉ trong vài phút.
- **Độ chính xác cao:** Kết hợp dữ liệu thực tế từ công cụ kiểm tra uy tín (WAVE) và khả năng lập luận sắc bén của Google Gemini Pro.
- **Nhận file sẵn sàng sử dụng:** File HTML được định dạng chuyên nghiệp và gửi trực tiếp qua email để team kỹ thuật đưa lên web ngay lập tức.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **WAVE API Key:** Tài khoản và API key từ WebAIM WAVE để quét lỗi website.
- **Google AI Studio API Key:** Dùng cho mô hình Google Gemini Pro.
- **Gmail Account:** Tài khoản Google để cấu hình node gửi email tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tạo một workflow mới trên n8n, sao chép toàn bộ mã JSON của workflow này và dán trực tiếp vào n8n Editor, hoặc import file JSON tải từ nguồn cấp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các node sau:

- **`CHANGE THESE: dependencies` (Node Set):** Đây là bảng điều khiển trung tâm của sếp. Hãy bấm vào node này và điền đầy đủ các thông tin quan trọng bao gồm:
  - URL website cần quét.
  - WAVE API Key.
  - Thông tin chi tiết về công ty (tên công ty, địa chỉ, liên hệ).
  - Ngôn ngữ đầu ra mong muốn cho bản Tuyên bố.

- **`gemini 2.5 pro` (Node lmChatGoogleGemini):** 
  - Cần kết nối Credentials với `Google Palm/Gemini API`.
  - Đảm bảo tài khoản API có đủ hạn mức để gọi model tạo văn bản dài.

- **`Send accessibility statement by email` (Node Gmail):**
  - Kết nối Credentials sử dụng `Gmail OAuth2`.
  - Cấu hình địa chỉ email nhận file HTML báo cáo hoàn chỉnh.

#### 3. Kích hoạt ⚡️
- Bấm **`When clicking ‘Execute workflow’`** để test chạy thử toàn bộ quy trình với dữ liệu mẫu.
- Kiểm tra email xem file `.html` đã được gửi về thành công chưa.
- Sau khi kiểm tra mọi thứ hoàn tất, bật nút **Active** ở góc trên bên phải để hoàn tất.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng lưu trữ:** Thay vì chỉ gửi qua email, các sếp có thể kết nối thêm node Google Drive hoặc Notion để tự động lưu trữ tất cả các bản tuyên bố theo từng phiên bản cập nhật website.
- **Tích hợp kênh chat nội bộ:** Thêm node Slack hoặc Telegram để thông báo ngay cho team quản trị website khi có báo cáo mới được tạo xong.
- **Tự động định kỳ:** Thay thế node `Manual Trigger` bằng `Schedule Trigger` để hệ thống tự động quét và cập nhật báo cáo hàng quý hoặc hàng năm.

### 📌 Kết luận
Việc tuân thủ các quy định pháp lý trực tuyến chưa bao giờ dễ dàng đến thế. Với workflow n8n tự động hóa này, các sếp vừa tiết kiệm được chi phí thuê dịch vụ pháp lý bên ngoài, vừa chủ động nắm bắt thời hạn tuân thủ EAA một cách nhanh chóng và chuyên nghiệp. Lên đồ và trải nghiệm ngay thôi các sếp!