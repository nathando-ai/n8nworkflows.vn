---
title: "🚀 Tự động thu thập và đồng bộ Leads từ Google Sheets sang Mailchimp với n8n"
description: "Hướng dẫn cài đặt workflow n8n tự động hóa việc đồng bộ danh sách khách hàng tiềm năng (leads) từ Google Sheets sang Mailchimp, giúp tối ưu hóa chiến dịch Email Marketing."
slug: "tu-dong-thu-thap-va-dong-bo-leads-google-sheets-mailchimp"
tags: [n8n, automation, no-code, sales, marketing, google-sheets, mailchimp]
keywords: [n8n workflow, đồng bộ leads, google sheets sang mailchimp, tự động hóa marketing, n8n viet nam]
---

# 🚀 Tự động đồng bộ Leads từ Google Sheets sang Mailchimp cực nhanh chóng

Các sếp làm Sales và Marketing chắc chắn đã quá ngán ngẩm cảnh phải copy-paste thủ công danh sách khách hàng tiềm năng từ file Google Sheets sang các công cụ Email Marketing như Mailchimp. Việc này vừa mất thời gian, dễ gây sai sót, lại làm lỡ mất "thời điểm vàng" để tiếp cận khách hàng.

Giải pháp là gì? Hãy để **n8n** tự động hóa toàn bộ quy trình này! Workflow này sẽ giúp các sếp tự động lấy dữ liệu leads mới từ Google Sheets và đẩy thẳng vào danh sách người đăng ký trên Mailchimp một cách trơn tru, không cần tốn một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian thủ công:** Không còn cảnh nhập liệu tay giữa Google Sheets và Mailchimp.
- **Loại bỏ sai sót:** Dữ liệu thông tin khách hàng (Email, Tên, Họ...) được đồng bộ chính xác tuyệt đối.
- **Tương tác kịp thời:** Leads vừa điền form/ghi nhận vào Sheet là ngay lập tức được đưa vào phễu Email Marketing của Mailchimp để chăm sóc.
- **Hoạt động tự động 24/7:** Chạy ngầm liên tục theo lịch trình cài đặt sẵn mà không cần sự can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
1. **Hệ thống n8n:** Đã cài đặt sẵn sàng (Self-hosted hoặc n8n Cloud).
2. **Google Sheets:** Một file Google Sheet chứa danh sách khách hàng tiềm năng (cần có các cột cơ bản như Email, First Name, Last Name...).
3. **Mailchimp Account:** Tài khoản Mailchimp đã tạo sẵn Audience (Danh sách người nhận) để hứng dữ liệu.
4. **Credentials:** 
   - Google API Credentials (OAuth2 hoặc Service Account) để n8n đọc được Google Sheets.
   - Mailchimp API Key để n8n kết nối và đẩy dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp tải file JSON của workflow này từ nguồn cung cấp.
- Trong giao diện n8n Editor, bấm vào menu **Add workflow** -> Chọn **Import from File** (hoặc copy toàn bộ JSON và dán trực tiếp vào màn hình làm việc của n8n).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 4 nodes cơ bản. Các sếp cần cấu hình chính xác các điểm sau để hệ thống chạy mượt mà:

- **Node `Interval` (Trigger định kỳ):** 
  - Node này quyết định tần suất workflow chạy (ví dụ: chạy mỗi 1 giờ, mỗi ngày...). Các sếp hãy cấu hình lại khoảng thời gian (Interval) cho phù hợp với nhu cầu thực tế của doanh nghiệp.
- **Node `On clicking 'execute'` (Manual Trigger):** 
  - Dùng để chạy thử nghiệm thủ công khi các sếp muốn test workflow ngay lập tức.
- **Node `Google Sheets`:** 
  - Chọn tài khoản Google Credentials đã kết nối.
  - Chỉ định đúng **Document ID** (Link hoặc ID của file Google Sheet) và **Sheet Name** (Tên tab chứa danh sách leads).
  - Cấu hình thao tác lấy dữ liệu (thường là "Get" hoặc "Get Many" rows).
- **Node `Mailchimp`:** 
  - Chọn Mailchimp API Credentials.
  - Chọn hành động là thêm/cập nhật thành viên vào danh sách (**Add/Update Member**).
  - Chọn đúng **Audience/List ID** trên Mailchimp của các sếp và map (ánh xạ) các trường dữ liệu từ Google Sheets sang Mailchimp (ví dụ: cột `Email` trong Sheet nối vào trường `Email Address` của Mailchimp, `First Name` nối vào `First Name`...).

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** trên node Manual Trigger hoặc dùng nút **Test step** ở từng node để kiểm tra xem dữ liệu từ Google Sheet có kéo về thành công và đẩy sang Mailchimp hay không.
- Sau khi test ngon lành, các sếp nhớ gạt công tắc sang chế độ **Active** ở góc trên bên phải màn hình để workflow chạy tự động theo lịch của node Interval nhé!

### ✍️ Mẹo & gợi ý nâng cao
Để workflow chuyên nghiệp và quản lý leads tốt hơn, các sếp có thể mở rộng thêm:
- **Thêm node Slack/Telegram:** Gửi một thông báo nhỏ vào nhóm chat nội bộ mỗi khi có một lead mới được đồng bộ thành công sang Mailchimp.
- **Đánh dấu trạng thái (Status):** Thêm một bước cập nhật ngược lại Google Sheets (thêm cột "Synced: Yes") để tránh việc workflow xử lý trùng lặp các dòng dữ liệu cũ trong những lần chạy sau.
- **Xử lý lỗi (Error Handling):** Thêm Error Trigger để nếu Mailchimp API lỗi (ví dụ email không hợp lệ), hệ thống sẽ báo cáo ngay cho đội ngũ kỹ thuật.

### 📌 Kết luận
Việc tự động hóa đồng bộ dữ liệu giữa Google Sheets và Mailchimp là bước đệm cực kỳ quan trọng để tối ưu hóa quy trình Sales & Marketing không tốn sức. Hãy cài đặt ngay workflow này để tối ưu hóa hiệu suất làm việc cho đội ngũ của các sếp ngay hôm nay! Chúc các sếp thao tác thành công!