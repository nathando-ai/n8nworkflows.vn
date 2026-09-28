---
title: "🚀 Tự động khám phá và làm giàu dữ liệu khách hàng của đối thủ với PredictLeads và Google Sheets"
description: "Khám phá danh sách khách hàng của đối thủ cạnh tranh tự động 100% bằng PredictLeads API, trích xuất thông tin chi tiết và lưu trực tiếp vào Google Sheets."
slug: "tu-dong-kham-pha-khach-hang-doi-thu-predictleads-google-sheets"
tags: [n8n, automation, market-research, predictleads, google-sheets]
keywords: [n8n workflow, nghiên cứu đối thủ cạnh tranh, predictleads api, tự động hóa n8n, thu thập lead]
---

# 🚀 Tự động khám phá và làm giàu dữ liệu khách hàng của đối thủ với PredictLeads và Google Sheets

Việc nghiên cứu thị trường và tìm hiểu xem **khách hàng của đối thủ là ai** luôn là một bài toán tiêu tốn rất nhiều thời gian của các đội ngũ Sales và Marketing. Nếu làm thủ công, bạn sẽ phải mò mẫm từng website, mạng xã hội hay báo cáo của đối thủ để đoán xem họ đang hợp tác với ai. 

Workflow n8n này do chuyên gia **Yaron Been** xây dựng sẽ giải quyết triệt để nỗi đau đó. Hệ thống sẽ tự động đọc danh sách tên miền (domain) của đối thủ từ Google Sheets, khai thác dữ liệu quan hệ khách hàng thông qua PredictLeads API, làm giàu thông tin công ty (quy mô, ngành nghề, địa điểm) và tự động xuất toàn bộ vào Google Sheets để bạn tha hồ phân tích.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Thấu hiểu thị trường:** Nắm bắt chính xác danh sách khách hàng, đối tác đang sử dụng sản phẩm/dịch vụ của đối thủ cạnh tranh.
- **Tiết kiệm 90% thời gian:** Tự động hóa hoàn toàn quy trình cào dữ liệu, gọi API và tổng hợp thay vì làm tay.
- **Làm giàu dữ liệu (Data Enrichment):** Tự động bổ sung thông tin chi tiết của từng khách hàng (ngành nghề, số lượng nhân viên, vị trí địa lý).
- **Dữ liệu sẵn sàng sử dụng:** Toàn bộ kết quả được đẩy thẳng vào Google Sheets, giúp đội ngũ Sales dễ dàng tiếp cận làm lead.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Google Sheets** và cấu hình Google Sheets OAuth2 API credentials.
- **Tài khoản PredictLeads** và **API Key** để truy cập dịch vụ Connections và Company API ([Truy cập PredictLeads tại đây](https://predictleads.com)).
- **File Google Sheets nguồn**: Chứa danh sách các domain của đối thủ cạnh tranh.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn.
- Mở n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dán trực tiếp vào màn hình canvas).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 9 nodes hoạt động tuần tự. Các sếp cần cấu hình kỹ các điểm sau:

- **📋 Read Competitors (Google Sheets):** 
  - Chọn Credentials tài khoản Google Sheets của bạn.
  - Điền đúng **Document ID** và **Sheet Name** chứa danh sách domain đối thủ.
- **🔍 Fetch Connections & 🔍 Enrich Client Company (HTTP Request):** 
  - Cấu hình Header chứa **API Key** được cung cấp từ tài khoản PredictLeads của bạn để xác thực các request gọi API.
- **⚙️ Extract Client Domains & ⚙️ Format Output Row (Code):** 
  - Các node Code đã được viết sẵn logic JavaScript để bóc tách domain khách hàng và định dạng lại cấu trúc dữ liệu, các sếp không cần chỉnh sửa gì thêm trừ khi muốn thay đổi cấu trúc trường dữ liệu xuất ra.
- **📊 Write to Google Sheets (Google Sheets):** 
  - Chọn Credentials Google Sheets.
  - Trỏ tới file Google Sheets dùng để lưu kết quả xuất ra (bao gồm các cột: Competitor source, Client domain, Client company name, Industry, Employee count, Location).

#### 3. Kích hoạt ⚡️
- Nhấn **▶️ Manual Trigger** để chạy thử nghiệm (Test run) với một vài dòng dữ liệu mẫu trong Google Sheets.
- Kiểm tra kết quả trả về trong Google Sheets đích.
- Sau khi mọi thứ chạy mượt mà, hãy gạt công tắc **Active** ở góc trên bên phải để kích hoạt workflow chính thức.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình nghiên cứu thị trường, các sếp có thể mở rộng workflow này bằng cách:
- **Tích hợp thông báo:** Thêm node Slack hoặc Telegram để gửi tin nhắn tóm tắt mỗi khi workflow chạy xong và tìm được các khách hàng mới của đối thủ.
- **Tự động hóa định kỳ:** Thay thế `Manual Trigger` bằng `Schedule Trigger` (chạy mỗi tuần/tháng một lần) để tự động cập nhật biến động khách hàng của đối thủ theo thời gian.
- **Kết nối CRM:** Đẩy thẳng dữ liệu khách hàng vừa làm giàu vào HubSpot, Pipedrive hoặc Salesforce để đội ngũ Sales tiến hành outreach ngay lập tức.

### 📌 Kết luận
Workflow "Discover and enrich competitor clients with PredictLeads and Google Sheets" là một thứ vũ khí hạng nặng cho các Marketer và Growth Hacker muốn thấu hiểu đối thủ cạnh tranh. Hãy cài đặt ngay hôm nay để tự động hóa toàn bộ quy trình thu thập và làm giàu dữ liệu khách hàng!