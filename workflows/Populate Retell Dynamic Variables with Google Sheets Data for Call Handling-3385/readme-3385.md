---
title: "🤖 Tự Động Hóa Thông Tin Khách Hàng Từ Google Sheets Cho Retell AI (Không Cần Code)"
description: "Workflow này giúp các sếp tự động lấy thông tin khách hàng từ Google Sheets và truyền vào Retell AI để cá nhân hóa cuộc gọi, tiết kiệm thời gian và cải thiện trải nghiệm khách hàng. Đặc biệt phù hợp cho đội ngũ bán hàng, hỗ trợ khách hàng và dịch vụ chăm sóc."
slug: "tu-dong-hoa-thong-tin-khach-hang-retell-google-sheets"
tags: [n8n, automation, no-code, retell-ai, google-sheets, sales-automation]
keywords: [n8n workflow retell, tự động hóa cuộc gọi retell, google sheets api, động biến retell, tự động hóa bán hàng]
---

# 🚀 Tự Động Hóa Thông Tin Khách Hàng Từ Google Sheets Cho Retell AI

### **Giải pháp nào giúp các sếp:**
- **Tiết kiệm 100% thời gian** nhập liệu thủ công khi bắt đầu cuộc gọi.
- **Cá nhân hóa cuộc gọi** bằng thông tin khách hàng từ Google Sheets.
- **Hoạt động liên tục 24/7** mà không cần can thiệp người dùng.
- **Tích hợp hoàn hảo** với Retell AI để sử dụng động biến trong các prompt.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted) để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhập liệu thủ công trước mỗi cuộc gọi.
- **Cá nhân hóa cao**: Thông tin khách hàng (tên, số điện thoại, lịch sử giao dịch...) tự động được truyền vào Retell AI.
- **Tăng hiệu quả bán hàng**: Cuộc gọi trở nên chuyên nghiệp và cá nhân hóa ngay từ đầu.
- **Hoạt động tự động**: Khách hàng gọi vào bất kỳ thời điểm nào, thông tin cũng được lấy và truyền tự động.
- **Dễ dàng mở rộng**: Thêm thông tin mới vào Google Sheets, Retell AI sẽ tự động cập nhật.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Retell AI** và một **Agent** đã được tạo.
2. **Số điện thoại** đã mua và gắn với Agent.
3. **Google Sheets** chứa thông tin khách hàng với:
   - **Cột số điện thoại** bắt buộc (định dạng: `+841234567890`).
   - Các cột khác sẽ được sử dụng làm **động biến** cho Retell AI.
4. **API Key Google Sheets OAuth2** (cài đặt trong n8n).
5. **URL Webhook** của n8n (sau khi import workflow).
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Bước 1**: Tải file JSON từ [n8n.io/workflows/3385](https://n8n.io/workflows/3385).
- **Bước 2**: Mở **n8n Editor** và chọn **Import Workflow** → Chọn file JSON vừa tải.
- **Bước 3**: Chọn **Active** để kích hoạt workflow.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm **3 node chính**, các sếp cần chú ý cấu hình như sau:

##### **Node 1: Webhook (n8n-nodes-base.webhook)**
- **Path**: `retell-dynamic-variables` (không cần thay đổi).
- **HTTP Method**: `POST` (đã mặc định).
- **Lưu ý**:
  - Sau khi import, copy **URL Webhook** (ví dụ: `https://your-instance.app.n8n.cloud/webhook/retell-dynamic-variables`).
  - Đăng ký URL này vào Retell AI như hướng dẫn dưới đây.

##### **Node 2: Get user in DB by Phone Number (n8n-nodes-base.googleSheets)**
- **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cài đặt trước).
- **Sheet Name**: Tên của Google Sheets chứa thông tin khách hàng.
- **Range**: Chọn **tất cả dữ liệu** (ví dụ: `Sheet1!A:Z`).
- **Lưu ý**:
  - **Định dạng số điện thoại trong Google Sheets phải bắt đầu bằng `+`** (ví dụ: `+841234567890`).
  - **Không có khoảng trắng** trong số điện thoại.
  - **Cột số điện thoại** phải nằm ở **cột đầu tiên** (n8n sẽ lấy giá trị này để tìm kiếm).

##### **Node 3: Respond to Webhook (n8n-nodes-base.respondToWebhook)**
- **Response Format**: Đã cấu hình sẵn để trả về dữ liệu từ Google Sheets.
- **Lưu ý**:
  - Retell AI sẽ **trả về tất cả dữ liệu dưới dạng chuỗi** (string).
  - Các **động biến** trong Retell AI sẽ được thay thế bằng dữ liệu từ Google Sheets.

#### 3. Kích hoạt ⚡️
- **Bước 1**: Đăng ký **Webhook URL** vào Retell AI:
  1. Mở **Retell Dashboard** → Chọn **Phone Numbers**.
  2. Chọn số điện thoại cần cấu hình → **Enable Inbound Webhook**.
  3. Dán **URL Webhook** từ n8n vào ô **Webhook URL**.
  4. Lưu thay đổi.
- **Bước 2**: **Test Run** với dữ liệu mẫu:
  - Gọi vào số điện thoại đã cấu hình.
  - Kiểm tra **n8n Editor** để xem liệu dữ liệu đã được lấy từ Google Sheets và trả về Retell AI chưa.
- **Bước 3**: Bật **Active** workflow.

---

### ✍️ Mẹo & gợi ý nâng cao
:::tip[CÁCH LÀM NÀY ĐỂ TĂNG HIỆU QUẢ]
1. **Tích hợp với Slack/Telegram**:
   - Thêm **node Slack/Telegram** để thông báo khi có cuộc gọi mới và dữ liệu khách hàng.
   - Ví dụ: `{{$json["name"]}} đã gọi vào số {{$json["phone"]}} với thông tin: {{$json["note"]}}`.

2. **Lưu log cuộc gọi**:
   - Thêm **node Google Sheets** để ghi lại lịch sử cuộc gọi (thời gian, số điện thoại, thông tin động biến).
   - Cấu hình cột mới trong Google Sheets để lưu log.

3. **Tự động gửi báo cáo hàng ngày**:
   - Sử dụng **node n8n-nodes-base.schedule** để chạy workflow định kỳ (ví dụ: 8h sáng) và gửi báo cáo tổng hợp về hoạt động của Retell AI qua email.

4. **Cập nhật động biến động态**:
   - Nếu thông tin khách hàng thay đổi (ví dụ: trạng thái giao dịch), cập nhật ngay vào Google Sheets. Retell AI sẽ tự động lấy dữ liệu mới khi khách hàng gọi lại.

5. **Sử dụng nhiều Google Sheets**:
   - Nếu có nhiều nhóm khách hàng (ví dụ: khách VIP, khách mới), chia dữ liệu vào các Google Sheets khác nhau và cấu hình **điều kiện** trong workflow để lấy dữ liệu từ Sheet phù hợp.
:::

---

### 📌 Kết luận
Workflow này giúp các sếp **tự động hóa hoàn toàn quá trình cá nhân hóa cuộc gọi** bằng cách lấy thông tin từ Google Sheets và truyền vào Retell AI. Không cần viết một dòng code nào, chỉ cần **cấu hình và kích hoạt**, hệ thống sẽ hoạt động 24/7, tiết kiệm thời gian và nâng cao chất lượng dịch vụ.

**Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với số điện thoại mẫu** để đảm bảo hoạt động.
3. **Tích hợp với Retell AI** và bắt đầu cá nhân hóa cuộc gọi!

Nếu có bất kỳ thắc mắc nào, các sếp có thể tham khảo [hướng dẫn chính thức của Retell AI](https://docs.retellai.com/build/dynamic-variables) hoặc liên hệ với **Agent Studio** để hỗ trợ kỹ thuật.

🚀 **Chúc các sếp thành công với tự động hóa Retell AI!** 🚀