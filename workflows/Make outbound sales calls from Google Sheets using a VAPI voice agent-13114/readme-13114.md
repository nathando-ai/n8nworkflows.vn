---
title: "🚀 Tự động gọi điện chăm sóc khách hàng từ Google Sheets bằng trợ lý giọng nói VAPI"
description: "Hướng dẫn xây dựng workflow n8n tự động gọi điện cho lead mới từ Google Sheets bằng VAPI, kiểm tra múi giờ làm việc và cập nhật kết quả cuộc gọi."
slug: "tu-dong-goi-dien-sales-google-sheets-vapi-n8n"
tags: [n8n, automation, vapi, ai-voice, lead-nurturing, google-sheets]
keywords: [n8n workflow, vapi ai voice, tu dong goi dien sales, outbound sales automation, google sheets n8n]
---

# 🚀 Tự động gọi điện Sales từ Google Sheets với VAPI Voice Agent

Việc gọi điện chăm sóc khách hàng (Outbound Sales) thủ công tốn rất nhiều thời gian, nhân lực và đôi khi gặp rủi ro gọi nhầm giờ nghỉ ngơi của khách. 

Workflow n8n này sẽ giúp các sếp giải quyết triệt để bài toán trên bằng cách tự động hóa 100%: Lắng nghe khách hàng mới từ Google Sheets, làm sạch số điện thoại, kiểm tra múi giờ địa phương (chỉ gọi giờ hành chính từ 8h sáng - 5h chiều), thực hiện cuộc gọi qua **VAPI** và tự động ghi nhận kết quả (trạng thái, tóm tắt cuộc gọi, cảm xúc khách hàng,...) ngược lại vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình gọi Sales**: Không cần bấm số thủ công, lead vừa vào bảng là hệ thống tự tiếp cận.
- **Thông minh theo múi giờ**: Tự động nhận diện mã vùng điện thoại và chỉ gọi trong khung giờ vàng (8h - 17h), tránh làm phiền khách hàng.
- **Lọc số trùng lặp**: Tránh gọi lại nhiều lần cho cùng một số điện thoại nhờ node Filter thông minh.
- **Báo cáo chi tiết thời gian thực**: Cập nhật trạng thái "Đã gọi", bản ghi âm, tóm tắt cuộc gọi và cảm xúc (sentiment) trực tiếp vào Google Sheets sau khi kết thúc cuộc gọi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Self-hosted hoặc Cloud).
- Tài khoản [VAPI](https://vapi.ai/?aff=n8ntemplate) (Miễn phí $10 credit đầu tiên, tương đương ~70 phút gọi).
- Tài khoản Google Sheets kết nối với n8n (Google OAuth2).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các node sau:

- **Node `New lead` (Google Sheets Trigger)**: 
  - Kết nối tài khoản Google Sheets của các sếp.
  - Trỏ tới file Google Sheet chuẩn bị sẵn. Cấu trúc các cột tối thiểu cần có: `Phone Number`, `Name`, `Status` (đặt giá trị mặc định cho lead mới là "Not called").

- **Node `Cleanse phone numbers` & `Get lead's timezone` (Code)**: 
  - Các node này xử lý định dạng số điện thoại (loại bỏ khoảng trắng, dấu gạch ngang, dấu cộng, ngoặc đơn) và xác định múi giờ dựa trên mã quốc gia.

- **Node `Make phone call` (HTTP Request)**: 
  - Cần thêm **Bearer Auth credential** lấy từ API Key của VAPI.
  - Trong phần Body JSON của node, hãy thay đổi các tham số sau cho đúng với tài khoản VAPI của các sếp:
    - `phoneNumberId`: ID số điện thoại Vapi của các sếp.
    - `number`: Trỏ biến tới `{{ $json['Phone Number'] }}`.
    - `assistantId`: ID trợ lý giọng nói (AI Assistant) đã tạo trên VAPI.

- **Node `Update Google Sheets with call information` (Google Sheets)**: 
  - Chọn thao tác `update` để ghi đè kết quả cuộc gọi (Call Summary, Sentiment, Transcript, Status...) vào đúng dòng của khách hàng tương ứng.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test workflow) với 1 dòng dữ liệu mẫu trong Google Sheets để kiểm tra tiến trình gọi và cập nhật dữ liệu.
- Bật công tắc **Active** để workflow tự động hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa nguồn Lead**: Thay thế Google Sheets Trigger bằng Webhook từ Landing Page, Typeform, hoặc CRM (Hubspot, Salesforce).
- **Cảnh báo qua Slack/Telegram**: Thêm node gửi tin nhắn thông báo về kênh nhóm ngay khi cuộc gọi kết thúc với các khách hàng có cảm xúc tích cực (Positive).
- **Mở rộng khung giờ**: Tùy chỉnh lại điều kiện trong node `Is it between 8am-5pm for them?` nếu sản phẩm/dịch vụ của các sếp đặc thù cho phép gọi muộn hơn.

### 📌 Kết luận
Workflow gọi Sales tự động bằng VAPI kết hợp n8n là vũ khí cực kỳ mạnh mẽ giúp tối ưu hóa đội ngũ Telesales, tiết kiệm chi phí và tăng tỷ lệ chuyển đổi lead nóng cực nhanh. Hãy thiết lập ngay hôm nay để gia tăng lợi thế cạnh tranh cho doanh nghiệp của các sếp!