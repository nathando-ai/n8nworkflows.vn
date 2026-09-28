---
title: "🚀 Tự động hóa CRM: Đồng bộ HighLevel với Google Sheets và báo cáo hàng ngày qua Gmail với GPT-4o"
description: "Hướng dẫn chi tiết cách tự động đồng bộ cơ hội từ HighLevel CRM vào Google Sheets và gửi báo cáo hàng ngày qua Gmail sử dụng trí tuệ nhân tạo GPT-4o. Tiết kiệm thời gian và nâng cao hiệu suất làm việc."
slug: "tu-dong-hoa-crm-highlevel-google-sheets-gmail-gpt4o"
tags: [n8n, automation, no-code, crm, google-sheets, gmail, ai, gpt-4o]
keywords: [n8n workflow, tự động hóa crm, đồng bộ dữ liệu, báo cáo tự động, gpt-4o, google sheets, gmail]
---

# 🚀 Tự động hóa CRM: Đồng bộ HighLevel với Google Sheets và báo cáo hàng ngày qua Gmail với GPT-4o

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có biết không? Với lượng công việc ngày càng tăng, việc phải đồng bộ dữ liệu giữa các hệ thống CRM và Google Sheets thủ công không chỉ tốn thời gian mà còn dễ gây lỗi. Hãy tưởng tượng bạn phải nhập tay hàng trăm bản ghi cơ hội từ HighLevel CRM vào Google Sheets mỗi ngày - một công việc nhàm chán và dễ gây sai sót. Đó chính là lý do mà workflow này được tạo ra - để tự động hóa hoàn toàn quy trình này với trí tuệ nhân tạo GPT-4o.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động đồng bộ dữ liệu hàng ngày mà không cần can thiệp thủ công.
- Dữ liệu chính xác: Giảm thiểu lỗi nhập liệu nhờ quy trình tự động hóa.
- Cá nhân hóa: Báo cáo hàng ngày được tạo tự động với thông tin chi tiết và dễ đọc.
- Hoạt động liên tục: Workflow chạy tự động 24/7 mà không cần giám sát.
- Nâng cao hiệu suất: Giúp đội ngũ bán hàng tập trung vào những việc quan trọng hơn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản HighLevel CRM với quyền truy cập API.
- Tài khoản Google với quyền truy cập Google Sheets và Gmail.
- Azure OpenAI với quyền truy cập GPT-4o.
- Biết cách tạo và cấu hình credentials trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của bạn, các sếp làm theo các bước sau:

1. Truy cập trang [n8n.io/workflows/10838](https://n8n.io/workflows/10838)
2. Nhấp vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Nhấp vào "Import" để hoàn tất quá trình

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Configure GPT-4o Model**:
   - Cần tạo credential "azureOpenAiApi" trong n8n
   - Điền thông tin API key và endpoint từ Azure OpenAI
   - Đảm bảo model được đặt là "gpt-4o"

2. **Fetch Opportunities from HighLevel CRM**:
   - Tạo credential "highLevelOAuth2Api" trong n8n
   - Điền thông tin client ID và client secret từ HighLevel
   - Có thể điều chỉnh số lượng bản ghi lấy về bằng tham số "limit"

3. **Log Invalid Opportunities to Google Sheets**:
   - Tạo credential "googleSheetsOAuth2Api" trong n8n
   - Điền thông tin client ID và client secret từ Google
   - Chỉnh sửa tên sheet và phạm vi dữ liệu cần ghi

4. **Update Opportunity Records in Google Sheets**:
   - Sử dụng cùng credential với node trước
   - Chỉnh sửa tên sheet và phạm vi dữ liệu cần cập nhật
   - Đảm bảo trường "id" được sử dụng làm khóa chính

5. **Send Daily Opportunity Summary via Gmail**:
   - Tạo credential "gmailOAuth2" trong n8n
   - Điền thông tin client ID và client secret từ Google
   - Chỉnh sửa địa chỉ email nhận báo cáo

#### 3. Kích hoạt ⚡️
Sau khi cấu hình xong các node quan trọng, các sếp cần thực hiện các bước sau:

1. Nhấp vào nút "Execute workflow" để kiểm tra dữ liệu đầu ra
2. Kiểm tra các node xử lý dữ liệu để đảm bảo dữ liệu được chuyển đổi đúng cách
3. Kiểm tra email nhận được để đảm bảo báo cáo được tạo đúng định dạng
4. Sau khi kiểm tra thành công, nhấp vào nút "Active workflow" để kích hoạt tự động hóa

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack để thông báo khi có cơ hội mới được thêm vào
- Tạo báo cáo định kỳ hàng tuần/tháng bằng cách thay đổi tần suất chạy workflow
- Kết hợp với các công cụ phân tích dữ liệu khác để tạo báo cáo chi tiết hơn
- Thêm node để lưu log các hoạt động của workflow để theo dõi hiệu suất

### 📌 Kết luận
Workflow này không chỉ giúp các sếp tiết kiệm thời gian mà còn nâng cao chất lượng dữ liệu và hiệu suất làm việc. Với sự kết hợp của trí tuệ nhân tạo GPT-4o và các công cụ tự động hóa mạnh mẽ, các sếp có thể tập trung vào những việc quan trọng hơn trong công việc hàng ngày. Hãy thử áp dụng ngay để trải nghiệm sự khác biệt!