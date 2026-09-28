---
title: "🚀 Tự động hóa Phân loại Bệnh nhân & Đặt lịch Khám Y tế với GPT-4 và JotForm"
description: "Xây dựng hệ thống phân loại bệnh nhân thông minh bằng AI, tự động xử lý biểu mẫu JotForm, phân tầng cấp cứu và đặt lịch khám tự động 24/7."
slug: "tu-dong-hoa-phan-loai-benh-nhan-y-te-gpt-4-jotform"
tags: [n8n, automation, ai, openai, jotform, healthcare]
keywords: [n8n workflow, y tế tự động hóa, medical triage ai, gpt-4 medical, jotform n8n]
---

# 🚀 Tự động hóa Phân loại Bệnh nhân & Đặt lịch Khám Y tế với GPT-4 và JotForm

Các phòng khám, bệnh viện và cơ sở y tế thường đối mặt với áp lực lớn trong việc tiếp nhận thông tin bệnh nhân qua biểu mẫu trực tuyến. Việc phân loại mức độ khẩn cấp (Triage) thủ công không chỉ tốn thời gian, dễ sai sót mà còn có thể gây nguy hiểm chậm trễ cho các ca cấp cứu.

Workflow n8n này do chuyên gia **Jitesh Dugar** phát triển sẽ giải quyết triệt để bài toán trên. Hệ thống tự động tiếp nhận thông tin từ JotForm, sử dụng sức mạnh phân tích ngữ nghĩa của **GPT-4** để đánh giá mức độ triệu chứng, tự động định tuyến ca bệnh (Cấp cứu, Khẩn cấp, hoặc Định kỳ) và kích hoạt các hành động thông báo phù hợp tới bác sĩ, bộ phận tiếp đón cũng như gửi hướng dẫn cho bệnh nhân ngay lập tức.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tối ưu thời gian phản hồi:** Các ca cấp cứu được phát hiện và cảnh báo tức thì qua Slack và Email dưới 15 phút.
- **Phân loại chính xác bằng AI:** GPT-4 phân tích triệu chứng chuyên sâu, chuẩn hóa dữ liệu đầu vào thành JSON cấu trúc rõ ràng.
- **Tự động hóa toàn trình:** Tự động điều phối lịch khám theo 3 luồng (Cấp cứu, Khẩn cấp 24-48h, Định kỳ 1-2 tuần) và lưu trữ dữ liệu tập trung lên Google Sheets.
- **Hoạt động 24/7:** Không bỏ sót bất kỳ thông tin đăng ký nào của bệnh nhân, đảm bảo tính tuân thủ và chăm sóc liên tục.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- **Tài khoản JotForm** (có tích hợp Trigger trên n8n).
- **OpenAI API Key** (Sử dụng model `gpt-4o`).
- **Tài khoản Gmail** (hoặc cấu hình SMTP) để gửi email xác nhận cho bệnh nhân và thông báo nhân viên.
- **Slack Webhook / Bot Token** (để bắn tin nhắn cảnh báo ca cấp cứu).
- **Google Sheets** (để lưu trữ cơ sở dữ liệu bệnh nhân).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy đoạn JSON của workflow hoặc tải file JSON gốc.
- Mở n8n Editor, chọn **Add workflow** -> **Import from File** / **Import from Clipboard** và dán dữ liệu vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **JotForm Trigger1**: Kết nối tài khoản JotForm của các sếp và chọn đúng Form thu thập thông tin bệnh nhân (`Patient Intake Collection`).
- **Extract Patient Data & Calculate Patient Info**: Kiểm tra lại cấu trúc dữ liệu JSON trả về từ form để đảm bảo các trường họ tên, triệu chứng, số điện thoại khớp với code xử lý.
- **AI Medical Triage & Analysis & OpenAI Chat Model**: Cấu hình credentials OpenAI và kiểm tra prompt trong AI Agent để đảm bảo tiêu chí phân loại bệnh án chuẩn xác.
- **Structured Output Parser**: Đảm bảo schema đầu ra của AI khớp với định dạng kiểm tra điều kiện ở các node tiếp theo.
- **Is Emergency? & Is Urgent?**: Kiểm tra logic rẽ nhánh (IF nodes) dựa trên kết quả phân loại của AI (Emergency, Urgent, Routine).
- **Alert Emergency Team (Slack)**: Cấu hình kênh Slack nhận cảnh báo khẩn cấp cho đội ngũ y bác sĩ trực ban.
- **Gmail Nodes** (Cấp cứu, Khẩn cấp, Định kỳ): Kết nối tài khoản Gmail OAuth2, chỉnh sửa nội dung template email gửi cho bác sĩ trực, nhân viên lễ tân (Front Desk/Scheduler) và email xác nhận cho bệnh nhân.
- **Log to Patient Database**: Chọn đúng file Google Sheets và Sheet Name để ghi nhận toàn bộ hành trình dữ liệu bệnh nhân phục vụ lưu trữ và phân tích.

#### 3. Kích hoạt ⚡️
- Thực hiện test run thủ công bằng cách submit một bản ghi mẫu trên JotForm để kiểm tra từng luồng chạy (Cấp cứu / Khẩn cấp / Định kỳ).
- Sau khi test thành công, bật công tắc **Active** góc trên bên phải để workflow chính thức vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Zalo ZNS / SMS:** Thay vì chỉ gửi email, các sếp có thể tích hợp thêm nhà mạng gửi tin nhắn SMS hoặc Zalo ZNS nhắc lịch khám tự động cho bệnh nhân.
- **Bổ sung Webhook CRM:** Đồng bộ dữ liệu bệnh nhân sang các hệ thống CRM y tế như HubSpot hoặc Zoho CRM để quản lý quan hệ khách hàng toàn diện hơn.
- **Báo cáo định kỳ:** Thêm một Scheduled Trigger chạy hàng ngày để tổng kết số lượng bệnh nhân theo phân loại và gửi báo cáo qua Email cho quản lý phòng khám.

### 📌 Kết luận
Workflow Medical Triage & Automation với GPT-4 và JotForm là một giải pháp chuyển đổi số y tế cực kỳ mạnh mẽ, giúp tiết kiệm hàng chục giờ làm việc thủ công và nâng cao mức độ an toàn cho bệnh nhân. Hãy áp dụng ngay vào phòng khám hoặc hệ thống y tế của các sếp để tối ưu hóa vận hành!