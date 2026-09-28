---
title: "🚀 Tự động hóa Phân tích Mạng xã hội & Tạo Email Cá nhân hóa với n8n"
description: "Giải pháp tự động hóa 100% không cần code giúp phân tích LinkedIn/Twitter và tạo email cá nhân hóa cho lead, tiết kiệm thời gian và tăng hiệu quả chăm sóc khách hàng."
slug: "tu-dong-hoa-phan-tich-mang-xa-hoi-tao-email-ca-nhan-hoa"
tags: [n8n, automation, no-code, marketing, ai]
keywords: [n8n workflow, tự động hóa, phân tích mạng xã hội, email cá nhân hóa, lead generation]
---

# 🚀 Tự động hóa Phân tích Mạng xã hội & Tạo Email Cá nhân hóa với n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường phải đối mặt với những thách thức lớn khi cố gắng chăm sóc khách hàng tiềm năng (lead) một cách hiệu quả. Việc phân tích hồ sơ mạng xã hội của lead, so sánh với ngành nghề kinh doanh của công ty và viết email cá nhân hóa cho từng người đều là những công việc tốn thời gian và dễ mắc sai sót. Bạn có bao giờ cảm thấy mệt mỏi khi phải làm những công việc lặp đi lặp lại này không? Với workflow này, các sếp có thể tự động hóa hoàn toàn quy trình này chỉ trong vài bước đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa quy trình phân tích và viết email, giảm thời gian xử lý từ vài giờ xuống còn vài phút.
- **Chính xác cao**: Dữ liệu được lấy từ các nguồn đáng tin cậy (LinkedIn, Twitter) và được xử lý bởi AI, đảm bảo độ chính xác cao.
- **Cá nhân hóa hoàn hảo**: Mỗi email được tạo ra đều phù hợp với ngành nghề, sở thích và phong cách của từng lead.
- **Hoạt động liên tục**: Workflow có thể chạy tự động 24/7, không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Google Sheets**: Tạo bảng tính với các cột: LinkedIn URL, tên, Twitter handle, email và cột "done" để theo dõi tiến độ.
- **Tài khoản RapidAPI**:
  - Đăng ký và đăng ký gói Twitter API (500 tweets/tháng miễn phí).
  - Đăng ký và đăng ký gói LinkedIn API (100 profile/tháng miễn phí).
- **OpenAI API Key**: Đăng ký tài khoản OpenAI và tạo API key để sử dụng mô hình ChatGPT.
- **Email SMTP**: Cấu hình tài khoản email (Gmail, Outlook,...) hoặc dịch vụ SMTP để gửi email tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/2823](https://n8n.io/workflows/2823).
3. Hoặc tải file JSON về và import thủ công qua nút "Import from File".

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Set your company's variables** (Node "set"):
   - Điền thông tin công ty của bạn: tên, ngành nghề, email gửi đi.

2. **Get linkedin Posts** (Node "httpRequest"):
   - Cấu hình credentials "httpHeaderAuth" với API key từ RapidAPI.
   - Điền URL API LinkedIn và các tham số cần thiết.

3. **Get twitter ID** (Node "httpRequest"):
   - Cấu hình credentials "httpHeaderAuth" với API key từ RapidAPI.
   - Điền URL API Twitter và các tham số cần thiết.

4. **Get tweets** (Node "httpRequest"):
   - Cấu hình credentials "httpHeaderAuth" với API key từ RapidAPI.
   - Điền URL API Twitter và các tham số cần thiết.

5. **OpenAI Chat Model** (Node "lmChatOpenAi"):
   - Cấu hình credentials "openAiApi" với API key từ OpenAI.
   - Chọn mô hình "gpt-4o" (hoặc mô hình khác phù hợp).

6. **Send Cover letter and CC me** (Node "emailSend"):
   - Cấu hình credentials "smtp" với thông tin tài khoản email của bạn.
   - Điền địa chỉ email nhận (lead) và email CC (bản sao cho bạn).

7. **Google Sheets Trigger** (Node "googleSheetsTrigger"):
   - Cấu hình credentials "googleSheetsTriggerOAuth2Api".
   - Chọn bảng tính và cột cần theo dõi.

8. **Google Sheets** (Node "googleSheets"):
   - Cấu hình credentials "googleSheetsOAuth2Api".
   - Chọn bảng tính và cột cần cập nhật.

#### 3. Kích hoạt ⚡️
1. **Test run dữ liệu mẫu**:
   - Thêm một vài dòng dữ liệu mẫu vào Google Sheets.
   - Chạy workflow với dữ liệu mẫu để kiểm tra kết quả.

2. **Bật Active workflow**:
   - Sau khi kiểm tra thành công, nhấn nút "Activate" để workflow chạy tự động khi có dữ liệu mới.

### ✍️ Mẹo & gợi ý nâng cao
- **Tối ưu hóa prompt**: Chỉnh sửa prompt trong node "Generate Subject and cover letter based on match" để phù hợp với phong cách và ngôn ngữ của công ty.
- **Kết hợp với Slack/Telegram**: Thêm node để gửi thông báo khi workflow hoàn thành hoặc gặp lỗi.
- **Lưu log hoạt động**: Thêm node để lưu log các email đã gửi vào Google Sheets hoặc cơ sở dữ liệu.
- **Tự động hóa báo cáo**: Tạo báo cáo định kỳ về hiệu quả của chiến dịch email.

### 📌 Kết luận
Workflow "Social Media Analysis and Automated Email Generation" là giải pháp hoàn hảo cho các sếp muốn tiết kiệm thời gian và tăng hiệu quả chăm sóc khách hàng. Với sự kết hợp của phân tích dữ liệu từ mạng xã hội và sức mạnh của AI, các sếp có thể tạo ra những email cá nhân hóa hoàn hảo mà không cần phải tốn nhiều thời gian và công sức. Hãy áp dụng ngay workflow này để nâng cao hiệu quả kinh doanh của công ty bạn!