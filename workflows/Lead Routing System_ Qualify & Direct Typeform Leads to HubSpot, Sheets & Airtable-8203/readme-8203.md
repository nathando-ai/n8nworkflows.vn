---
title: "🚀 Xây dựng hệ thống phân loại và điều hướng Lead tự động từ Typeform đến HubSpot, Google Sheets và Airtable"
description: "Tự động hóa 100% quy trình tiếp nhận lead từ Typeform, lọc ngân sách, đồng bộ vào HubSpot CRM, Google Sheets, Airtable và gửi email chăm sóc khách hàng tức thì."
slug: "he-thong-phan-loai-va-dieu-huong-lead-tu-dong-n8n"
tags: [n8n, automation, no-code, lead-generation, hubspot, crm]
keywords: [n8n workflow, tự động hóa lead, phân loại lead tự động, typeform hubspot n8n, crm automation]
---

# 🚀 Xây dựng hệ thống phân loại và điều hướng Lead tự động từ Typeform đến HubSpot, Google Sheets và Airtable

Các sếp có bao giờ cảm thấy quá tải khi mỗi ngày phải thủ công copy dữ liệu từ các form đăng ký, lọc xem khách hàng nào có ngân sách lớn, rồi lại phân phối họ vào CRM, Google Sheets hay Airtable? Việc này không chỉ tốn hàng giờ đồng hồ mà còn dễ dẫn đến tình trạng phản hồi chậm trễ, khiến những khách hàng tiềm năng cao (high-ticket leads) nguội lạnh.

Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ do **Avkash Kakdiya** (Founder của iTechNotion) thiết kế. Hệ thống này sẽ tự động hóa toàn bộ quy trình: tiếp nhận lead, đánh giá ngân sách, đồng bộ CRM, phân loại nguồn dữ liệu và gửi email chăm sóc tự động ngay lập tức!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Lọc Lead thông minh:** Tự động nhận diện các khách hàng có ngân sách lớn (> $5,000) để ưu tiên xử lý đặc biệt.
- **Đồng bộ đa nền tảng:** Đẩy dữ liệu chuẩn chỉnh vào HubSpot CRM, Google Sheets hoặc Airtable tùy theo nguồn lead mà không cần đụng tay.
- **Chăm sóc khách hàng tức thì:** Tự động gửi email cảm ơn và thông báo thời gian phản hồi qua Gmail ngay sau khi khách submit form.
- **Hoạt động 24/7:** Loại bỏ hoàn toàn thao tác thủ công, giúp đội ngũ sales tập trung vào việc chốt deal thay vì nhập liệu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và kết nối sau:
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Typeform** (để tạo form thu thập lead).
- Tài khoản **HubSpot CRM** (kèm quyền API/App Token).
- Tài khoản **Google Sheets** (để lưu trữ lead từ Facebook/quảng cáo).
- Tài khoản **Airtable** (để quản lý dữ liệu từ SurveyMonkey/nguồn khác).
- Tài khoản **Gmail** (hoặc Google Workspace để gửi email tự động).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ n8n (Link gốc: [n8n.io/workflows/8203](https://n8n.io/workflows/8203)), sau đó vào n8n Editor chọn **Import from File** hoặc dán trực tiếp đoạn JSON vào workspace.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 9 nodes chính được chia thành các luồng logic rõ ràng. Các sếp cần cấu hình kỹ các điểm sau:

- **📋 Typeform Submission Trigger**: Kết nối tài khoản Typeform của các sếp và chọn đúng Form ID cần lắng nghe dữ liệu.
- **💰 Check High-Budget Lead**: Kiểm tra điều kiện logic (If node). Mặc định workflow sẽ lọc các lead có trường ngân sách (budget) lớn hơn $5,000. Hãy chỉnh lại mức ngân sách cho phù hợp với mô hình kinh doanh của doanh nghiệp.
- **👤 HubSpot — Create/Update Contact** & **📝 HubSpot — Add Priority Task**: 
  - Chọn `HubSpot App Token` credentials.
  - Node đầu tiên sẽ tạo mới hoặc cập nhật thông tin liên hệ. Node thứ hai (`engagement` resource) sẽ tự động tạo một Task ưu tiên trong HubSpot để đội ngũ sales gọi điện ngay cho khách hàng VIP.
- **📘 Check if Facebook Lead** & **📊 Check if SurveyMonkey Lead**: Các node If này phân loại nguồn lead đổ về từ đâu để đẩy vào bảng dữ liệu tương ứng.
- **📄 Log Facebook Lead to Google Sheet**: Kết nối Google Sheets OAuth2, chọn đúng Spreadsheet và Worksheet (Sheet con) để ghi log lead phục vụ marketing.
- **📦 Store SurveyMonkey Lead in Airtable**: Kết nối tài khoản Airtable, chọn Base và Table phù hợp để lưu trữ dữ liệu dạng bảng có cấu trúc.
- **📧 Send Gmail Auto-Response**: Kết nối Gmail OAuth2. Soạn sẵn nội dung email tự động xác nhận đã nhận thông tin và cam kết phản hồi trong vòng 24 giờ.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thực hiện một bài test submit form trên Typeform để kiểm tra luồng dữ liệu chạy qua các nhánh If, Hubspot, Google Sheets/Airtable và Gmail.
- Nếu mọi thứ chạy xanh mướt (success), hãy gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống xịn xò hơn nữa, các sếp có thể mở rộng workflow này với các ý tưởng sau:
1. **Tích hợp Telegram/Slack:** Thêm một node Telegram hoặc Slack Bot để bắn thông báo ngay lập tức vào nhóm "Sales Hot Leads" mỗi khi có khách hàng VIP submit form.
2. **AI Scoring:** Kết hợp với OpenAI Node để phân tích ngữ nghĩa câu trả lời trong form, từ đó chấm điểm mức độ quan tâm (Lead Scoring) chuẩn xác hơn trước khi đẩy vào CRM.
3. **Báo cáo định kỳ:** Tạo thêm một nhánh chạy theo lịch (Cron/Schedule Trigger) tổng hợp số liệu lead trong tuần gửi về email cho quản lý vào mỗi sáng thứ Hai.

### 📌 Kết luận
Hệ thống điều hướng và phân loại lead tự động này là mảnh ghép hoàn hảo giúp tối ưu hóa phễu bán hàng, không bỏ sót bất kỳ khách hàng tiềm năng nào và tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần. Chúc các sếp cài đặt thành công và "bão đơn"!