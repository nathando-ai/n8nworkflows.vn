---
title: "🚀 Tự động hóa chiến dịch email cá nhân hóa với HubSpot, Groq AI và Gmail trên n8n"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động quét liên hệ mới từ HubSpot, sử dụng Groq AI (Llama 3.3) để phân tích và tạo chiến dịch quảng cáo cá nhân hóa, sau đó gửi email tự động qua Gmail."
slug: "tao-email-campaign-hubspot-groq-ai-gmail-n8n"
tags: [n8n, automation, no-code, hubspot, groq-ai, gmail, ai-agent]
keywords: [n8n workflow, tự động hóa email, hubspot crm, groq ai, lamma 3.3, email marketing tự động]
---

# 🚀 Tự động hóa chiến dịch email cá nhân hóa với HubSpot, Groq AI và Gmail trên n8n

Việc thủ công tìm kiếm thông tin khách hàng mới từ CRM, nghiên cứu doanh nghiệp của họ và viết những nội dung email chào hàng (cold email) cá nhân hóa tốn rất nhiều thời gian của các đội ngũ sales và marketing. Nếu làm thủ công, bạn chỉ tiếp cận được vài chục khách hàng mỗi ngày, dễ dẫn đến sự mệt mỏi và bỏ sót cơ hội.

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách tự động hóa 100% quy trình: Quét liên hệ mới từ HubSpot -> Phân tích doanh nghiệp bằng Groq AI siêu tốc -> Viết chiến dịch quảng cáo tùy chỉnh -> Tự động gửi email qua Gmail mà không cần can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Siêu cá nhân hóa:** AI phân tích tên công ty và website của từng khách hàng từ HubSpot để tạo chiến dịch quảng cáo độc nhất, đúng "nỗi đau" của họ.
- **Tiết kiệm 90% thời gian:** Thay vì mất hàng giờ nghiên cứu và soạn email, hệ thống xử lý hàng loạt hoàn toàn tự động.
- **Hoạt động 24/7:** Chạy theo lịch trình (Schedule Trigger) định kỳ, đảm bảo không bỏ sót bất kỳ khách hàng tiềm năng mới nào trong 24 giờ qua.
- **Tăng tỷ lệ chuyển đổi (Conversion Rate):** Email gửi đi mang tính chuyên môn cao, đúng trọng tâm giúp khách hàng phản hồi nhiều hơn.
:::

### 📦 Các thành phần chính trong Workflow (7 Nodes)
1. **Schedule Trigger:** Kích hoạt workflow tự động theo lịch trình.
2. **Search contacts (Hubspot):** Lọc và lấy danh sách các liên hệ mới được tạo trong 24 giờ qua từ HubSpot CRM.
3. **Loop Over Contacts (Split In Batches):** Duyệt qua từng liên hệ một cách tuần tự để tránh quá tải hoặc lỗi API.
4. **AI Agent & Groq Chat Model (`llama-3.3-70b-versatile`):** Đóng vai chuyên gia marketing, phân tích thông tin doanh nghiệp và lên chiến lược quảng cáo.
5. **Format AI's output (Code):** Xử lý và định dạng lại nội dung do AI trả về thành một cấu trúc email rõ ràng, chuyên nghiệp.
6. **Send a message (Gmail):** Tự động gửi email chiến dịch đã cá nhân hóa đến khách hàng.

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản HubSpot** (Đã có sẵn danh sách contacts với tên công ty và website).
- **Groq API Key** (Lấy miễn phí tại [Groq Console](https://console.groq.com/)).
- **Tài khoản Gmail** (Hoặc Google Workspace đã kết nối OAuth2 với n8n).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow hoặc tải file JSON từ nguồn cung cấp.
- Mở n8n Editor, chọn **Add workflow** -> Nhấn vào dấu `...` ở góc trên bên phải -> **Import from File** hoặc dán trực tiếp JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các credentials và tham số cho các node sau:
- **Search contacts (Hubspot):** Kết nối tài khoản HubSpot của bạn bằng OAuth2 hoặc Private App Token. Cấu hình điều kiện tìm kiếm các contact được tạo trong khoảng thời gian phù hợp (ví dụ: trong vòng 24 giờ qua).
- **Groq Chat Model:** Thêm Groq API Key vào credentials. Đảm bảo model được chọn là `llama-3.3-70b-versatile` để có tốc độ phản hồi cực nhanh và chất lượng phân tích văn bản tốt nhất.
- **AI Agent:** Kiểm tra lại System Prompt bên trong agent để đảm bảo AI hiểu đúng văn phong, ngôn ngữ (tiếng Việt hoặc tiếng Anh) và định dạng đầu ra mà bạn mong muốn cho chiến dịch email.
- **Send a message (Gmail):** Kết nối tài khoản Gmail của bạn. Map trường email người nhận từ kết quả của HubSpot và nội dung email từ node **Format AI's output**.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Test Workflow**) với một vài dữ liệu mẫu để kiểm tra luồng chạy từ HubSpot sang AI rồi đến Gmail.
- Sau khi kiểm tra email gửi thành công và đúng định dạng, bật nút **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thêm node **Slack** hoặc **Telegram** sau bước gửi email để thông báo cho đội ngũ Sales biết ngay khi AI vừa gửi email cho một khách hàng lớn.
- **Lưu lịch sử vào Google Sheets:** Thêm một node Google Sheets trước hoặc sau khi gửi email để ghi lại log (Tên khách hàng, Email, Nội dung AI đã tạo, Thời gian gửi) nhằm dễ dàng quản lý và theo dõi.
- **Tùy chỉnh Prompt theo ngành nghề:** Tách workflow thành nhiều nhánh hoặc tạo các prompt riêng biệt dựa theo ngành nghề của khách hàng trên HubSpot để mức độ cá nhân hóa đạt đỉnh cao nhất.

### 📌 Kết luận
Workflow tự động hóa kết hợp HubSpot, Groq AI và Gmail chính là "vũ khí bí mật" giúp các startup, agency tối ưu hóa quy trình outbound sales mà không cần tốn chi phí thuê nhân sự thủ công quá lớn. Hãy import ngay vào n8n của các sếp và bắt đầu "lên đồ" tự động hóa ngay hôm nay!