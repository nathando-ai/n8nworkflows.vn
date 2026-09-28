---
title: "🚀 Tự động hóa bản tin tài chính thông minh với Google Gemini AI và gửi qua Outlook"
description: "Xây dựng hệ thống tự động thu thập tin tức tài chính, phân tích bằng Google Gemini AI và gửi báo cáo tóm tắt chuyên nghiệp qua Microsoft Outlook mỗi ngày."
slug: "tu-dong-hoa-tin-tuc-tai-chinh-google-gemini-outlook"
tags: [n8n, automation, no-code, ai, google-gemini, microsoft-outlook, finance]
keywords: [n8n workflow, tin tức tài chính, google gemini ai, microsoft outlook, tự động hóa bản tin, ai agent n8n]
---

# 🚀 Tự động hóa bản tin tài chính thông minh với Google Gemini AI và gửi qua Outlook

Các sếp làm trong lĩnh vực tài chính, đầu tư hay quản trị doanh nghiệp chắc chắn luôn phải đối mặt với áp lực cập nhật thông tin thị trường liên tục. Việc đọc hàng chục trang báo, lọc tin rác và tổng hợp lại thành một bản tin (digest) tốn rất nhiều thời gian mỗi ngày.

Giải pháp là đây! Workflow n8n này sẽ tự động hóa toàn bộ quy trình: từ việc lấy tin tức tài chính trực tuyến, sử dụng sức mạnh của **Google Gemini AI** để phân tích, chắt lọc các điểm tin đắt giá, cho đến việc tự động gửi bản phân tích hoàn chỉnh vào hòm thư **Microsoft Outlook** của các sếp. Hoàn toàn tự động, không tốn một phút làm thủ công!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Thay vì mất hàng giờ lướt web đọc tin tài chính, các sếp có ngay bản tóm tắt gọn gàng trong email mỗi sáng.
- **AI thông minh phân tích sâu:** Google Gemini giúp lọc bỏ nhiễu, giữ lại các thông tin kinh tế cốt lõi ảnh hưởng trực tiếp đến danh mục hoặc thị trường.
- **Tự động hóa 100%:** Kết hợp giữa `Schedule Trigger` và Microsoft Outlook, bản tin được gửi đi đúng giờ mà không cần sự can thiệp thủ công.
- **Chuyên nghiệp và nhất quán:** Định dạng email rõ ràng, súc tích, dễ dàng nắm bắt thông tin chỉ trong vài phút.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản **Google Gemini API Key** (để cấu hình cho các node AI Agent và Chat Model).
- Tài khoản **Microsoft Outlook** để kết nối và gửi email tự động.
- Nguồn cấp dữ liệu tin tức tài chính (API hoặc trang web qua node `Get financial news online`).
:::

###  Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow từ nguồn (hoặc tải file JSON) và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình các node quan trọng sau:

- **Schedule Trigger / When clicking ‘Test workflow’:** Chọn lịch chạy định kỳ (ví dụ: 8h sáng mỗi ngày) ở node `Schedule Trigger`, hoặc dùng `When clicking ‘Test workflow’` để test thủ công.
- **Get financial news online (`httpRequest`):** Cấu hình URL endpoint hoặc API nguồn cung cấp tin tức tài chính mà các sếp muốn khai thác.
- **Google Gemini Chat Model & Google Gemini Chat Model1 (`lmChatGoogleGemini`):** Điền `Gemini API Key` của các sếp để cung cấp quyền truy cập mô hình ngôn ngữ AI.
- **AI Agent & AI Agent1 (`agent`):** Kiểm tra lại các Prompt hệ thống (System Prompt) bên trong các Agent này để tinh chỉnh cách AI lọc tin, tóm tắt và định dạng nội dung theo đúng ý muốn của các sếp.
- **Send the summary by e-mail (`microsoftOutlook`):** Kết nối tài khoản Microsoft Outlook của các sếp, chọn người nhận (To), tiêu đề email và đưa nội dung đã được tổng hợp từ các node phía trước vào phần thân email (Body).
- **Loop Over Items (`splitInBatches`) & Aggregate / Code:** Đảm bảo các node xử lý vòng lặp và gộp dữ liệu chạy chính xác nếu số lượng tin tức lớn, tránh việc tràn giới hạn token của AI.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** để chạy thử nghiệm và kiểm tra xem email có được gửi về Outlook thành công hay không.
- Nếu mọi thứ đã ổn áp, hãy gạt công tắc sang **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin:** Ngoài Microsoft Outlook, các sếp có thể gắn thêm node `Telegram` hoặc `Slack` để nhận bản tin ngay trên điện thoại di động.
- **Lưu trữ lịch sử:** Thêm một node `Google Sheets` hoặc cơ sở dữ liệu (Notion, PostgreSQL) để lưu lại các bản tin đã gửi phục vụ việc tra cứu về sau.
- **Tùy biến ngôn ngữ:** Yêu cầu Google Gemini dịch và phân tích tin tức sang tiếng Việt hoàn toàn với văn phong chuyên nghiệp, phù hợp với văn hóa doanh nghiệp Việt Nam.

### 📌 Kết luận
Với workflow tự động hóa bản tin tài chính này, việc cập nhật tin tức thị trường trở nên dễ dàng và tinh gọn hơn bao giờ hết. Hãy "lên đồ" ngay cho hệ thống n8n của các sếp để tối ưu hóa năng suất làm việc từ hôm nay!