---
title: "🚀 Tự động hóa xuất dữ liệu Mirakl Offers ra file CSV và gửi email qua Gmail với n8n"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động lấy danh sách sản phẩm/ưu đãi từ Mirakl API, chuyển đổi thành file CSV và gửi báo cáo qua Gmail định kỳ."
slug: "tu-dong-hoa-xuat-mirakl-offers-csv-gui-email-gmail"
tags: [n8n, automation, no-code, mirakl, api, gmail, file-management]
keywords: [n8n workflow, mirakl offers, export csv, tự động hóa gmail, schedule trigger, http request]
---

# 🚀 Tự động hóa xuất dữ liệu Mirakl Offers ra file CSV và gửi email qua Gmail

Các sếp quản lý sàn thương mại điện tử sử dụng nền tảng **Mirakl** chắc chắn hiểu rõ nỗi khổ khi phải thủ công đăng nhập, tải danh sách ưu đãi (`offers`) hàng ngày để phân tích hoặc báo cáo. Việc làm thủ công này không chỉ tốn thời gian, dễ sai sót mà còn làm gián đoạn dòng chảy thông tin kinh doanh.

Giải pháp là đây! Workflow n8n này sẽ tự động hóa **100%** quy trình: Lên lịch chạy định kỳ, gọi API lấy dữ liệu từ Mirakl, xử lý và đóng gói thành file CSV, sau đó tự động gửi thẳng vào hộp thư của các sếp (hoặc đối tác, bộ phận vận hành) thông qua Gmail mà không cần động tay vào một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Loại bỏ hoàn toàn thao tác trích xuất dữ liệu thủ công mỗi ngày/tuần.
- **Chính xác & Kịp thời:** Dữ liệu được đồng bộ trực tiếp từ Mirakl API và gửi đi theo lịch trình chính xác đến từng phút.
- **Báo cáo chuyên nghiệp:** File CSV được định dạng chuẩn, đính kèm trực tiếp vào email Gmail cá nhân hóa.
- **Hoạt động 24/7 bền bỉ:** Tự động chạy ngầm trên hệ thống n8n của các sếp mà không lo quên lịch.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
1. **Hệ thống n8n** (Cloud hoặc Self-hosted).
2. **Mirakl API Credentials**: API URL và API Key từ tài khoản người bán/quản trị Mirakl của các sếp.
3. **Tài khoản Gmail**: Đã cấu hình OAuth2 Credentials trên n8n để gửi email tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy đoạn mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc import file JSON tải từ kho lưu trữ n8n chính thức.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 5 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Daily Export Trigger (`scheduleTrigger`)**: 
  - Node này quyết định tần suất chạy (hàng ngày, hàng tuần...). Các sếp hãy cấu hình lại mốc thời gian (ví dụ: chạy lúc 8:00 sáng mỗi ngày) cho phù hợp với nhu cầu vận hành.
- **Set Configuration Parameters (`set`)**: 
  - Nơi các sếp khai báo các biến cấu hình quan trọng như: Đường dẫn Mirakl API (`API URL`), khóa bảo mật (`API Key`), và địa chỉ email nhận báo cáo.
- **Fetch Mirakl Offers (`httpRequest`)**: 
  - Node này dùng phương thức HTTP Request để gọi dữ liệu từ Mirakl API dựa vào các biến đã thiết lập ở node *Set Configuration Parameters*. Đảm bảo Header chứa đúng API Key của Mirakl.
- **Convert to Spreadsheet Format (`code`)**: 
  - Sử dụng đoạn mã tùy chỉnh để bóc tách dữ liệu JSON thô nhận được từ Mirakl và chuyển đổi thành định dạng bảng (spreadsheet/CSV) sẵn sàng để đính kèm email.
- **Send Email via Gmail (`gmail`)**: 
  - Chọn tài khoản **Gmail OAuth2** đã kết nối với n8n.
  - Điền địa chỉ email người nhận, tiêu đề thư và nội dung. Đảm bảo cấu hình file đính kèm (`attachments`) trỏ đúng vào dữ liệu CSV được xuất ra từ bước trước.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thủ công một lần xem dữ liệu có được fetch và email có được gửi đi thành công hay không.
- Sau khi test xanh mướt, hãy gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa hơn nữa quy trình này, các sếp có thể mở rộng workflow bằng cách:
- **Tích hợp Slack / Telegram:** Gửi thông báo dạng text nhanh vào nhóm chat (ví dụ: *"Đã xuất thành công 1,250 offers từ Mirakl lúc 8:00"*).
- **Lưu trữ lịch sử:** Thêm một node Google Drive hoặc S3 để lưu lại bản sao của file CSV mỗi ngày nhằm phục vụ việc kiểm toán (audit) về sau.
- **Xử lý lỗi (Error Handling):** Thêm nhánh Error Trigger để nếu API Mirakl lỗi, hệ thống sẽ tự động bắn tin nhắn cảnh báo về Telegram cho đội kỹ thuật.

### 📌 Kết luận
Việc tự động hóa trích xuất dữ liệu sàn thương mại điện tử chưa bao giờ dễ dàng đến thế với n8n. Chỉ với vài phút thiết lập ban đầu, các sếp đã giải phóng bản thân khỏi những tác vụ lặp đi lặp lại nhàm chán. Hãy triển khai ngay hôm nay và tối ưu hóa vận hành kinh doanh của mình nhé!