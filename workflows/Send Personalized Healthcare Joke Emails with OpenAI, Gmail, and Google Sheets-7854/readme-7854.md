---
title: "🚀 Tự động hóa Email Chăm sóc sức khỏe với OpenAI, Gmail và Google Sheets"
description: "Hướng dẫn chi tiết cách tự động gửi email châm biếm sức khỏe cá nhân hóa hàng ngày cho danh sách liên hệ của bạn bằng n8n, OpenAI, Gmail và Google Sheets"
slug: "tu-dong-hoa-email-cham-soc-suc-khoe"
tags: [n8n, automation, no-code, openai, gmail, google-sheets]
keywords: [n8n workflow, tự động hóa email sức khỏe, openai email, gmail automation, google sheets tracking]
---

# 🚀 Tự động hóa Email Chăm sóc sức khỏe với OpenAI, Gmail và Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các chuyên gia chăm sóc sức khỏe khi phải gửi hàng trăm email cá nhân hóa hàng ngày. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động gửi hàng trăm email cá nhân hóa hàng ngày mà không cần can thiệp
- Tăng tương tác: Sử dụng châm biếm sức khỏe để tạo kết nối thân thiện
- Theo dõi hiệu quả: Theo dõi trạng thái email trong Google Sheets
- Tránh spam: Giới hạn 10 email mỗi lần chạy và thêm độ trễ ngẫu nhiên
- Hoạt động liên tục: Chạy tự động hàng ngày vào lúc 13h00
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail để gửi email
- Google Sheets chứa danh sách liên hệ với các cột: First Name, Email, Emailed
- API Key từ OpenAI để tạo nội dung email
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link: https://n8n.io/workflows/7854
3. Hoặc tải file JSON về và chọn "Import from File"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Daily Trigger (1 PM)**: Node này kích hoạt workflow hàng ngày vào lúc 13h00. Các sếp có thể thay đổi thời gian này trong node này.

2. **Healthcare_Contact_List**: Node Google Sheets đầu tiên để lấy danh sách liên hệ. Các sếp cần:
   - Chọn credentials Google Sheets của mình
   - Nhập Spreadsheet ID và Sheet Name chứa danh sách liên hệ
   - Đảm bảo có các cột: First Name, Email, Emailed

3. **AI Email Generator**: Node Agent của LangChain để tạo nội dung email. Các sếp có thể:
   - Chỉnh sửa system message để thay đổi phong cách email
   - Cập nhật template email trong node này

4. **OpenAI Chat Model**: Node để chọn model OpenAI. Mặc định là gpt-4o-mini. Các sếp có thể thay đổi model này nếu cần.

5. **Send Email**: Node Gmail để gửi email. Các sếp cần:
   - Chọn credentials Gmail của mình
   - Cấu hình template email trong node này

6. **Update Email Status**: Node Google Sheets cuối cùng để cập nhật trạng thái email. Các sếp cần:
   - Đảm bảo cấu hình giống với node đầu tiên (Healthcare_Contact_List)
   - Đảm bảo có cột Emailed để lưu thời gian gửi email

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu bằng cách nhấn vào nút "Execute Workflow" với 1-2 liên hệ thử nghiệm
2. Kiểm tra email thử nghiệm và Google Sheets để đảm bảo dữ liệu được cập nhật đúng
3. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack/Telegram để nhận thông báo khi workflow chạy thành công
- Lưu log hoạt động vào Google Sheets hoặc cơ sở dữ liệu
- Gửi báo cáo hàng tuần về hiệu quả của chiến dịch email
- Thêm chức năng theo dõi mở email và nhấp chuột bằng Google Analytics

### 📌 Kết luận
Workflow này giúp các chuyên gia chăm sóc sức khỏe tự động hóa hàng trăm email cá nhân hóa hàng ngày mà không cần can thiệp. Với khả năng theo dõi hiệu quả và tránh spam, đây là giải pháp hoàn hảo cho các doanh nghiệp chăm sóc sức khỏe muốn duy trì mối quan hệ với khách hàng một cách chuyên nghiệp và thân thiện. Hãy áp dụng ngay để tiết kiệm thời gian và tăng tương tác với khách hàng!