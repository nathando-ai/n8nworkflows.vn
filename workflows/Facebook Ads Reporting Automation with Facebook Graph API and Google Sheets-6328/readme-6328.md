---
title: "📊 Tự động hóa báo cáo Facebook Ads vào Google Sheets với n8n và Facebook Graph API"
description: "Hướng dẫn cài đặt workflow n8n tự động lấy dữ liệu chiến dịch, thống kê và chuyển đổi từ Facebook Ads trực tiếp vào Google Sheets hoàn toàn tự động."
slug: "tu-dong-hoa-bao-cao-facebook-ads-google-sheets-n8n"
tags: [n8n, automation, facebook-ads, google-sheets, marketing-automation, graph-api]
keywords: [n8n workflow, facebook ads reporting, tự động hóa marketing, facebook graph api google sheets, n8n facebook ads]
---

# 📊 Tự động hóa báo cáo Facebook Ads vào Google Sheets với n8n

Các sếp chạy quảng cáo Facebook chắc chắn đã quá quen thuộc với cảnh mỗi sáng phải mở Ads Manager, xuất file Excel (CSV), copy-paste số liệu rồi lọc báo cáo cho sếp hoặc team. Việc này vừa mất thời gian, vừa dễ nhầm lẫn số liệu, lại chẳng thể cập nhật real-time. 

Giải pháp ư? Workflow n8n này sẽ thay các sếp làm trọn gói từ A-Z: Tự động kéo dữ liệu chiến dịch, thống kê chi phí, lượt chuyển đổi từ Facebook Graph API và đồng bộ thẳng tắp vào Google Sheets định kỳ mỗi ngày!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian thủ công:** Không còn cảnh loay hoay export/import file báo cáo mỗi ngày.
- **Số liệu luôn cập nhật:** Dữ liệu chi tiêu, reach, impression, conversion được đồng bộ tự động theo lịch trình thiết lập.
- **Quản trị minh bạch:** Toàn bộ lịch sử chiến dịch và số liệu thống kê được lưu trữ gọn gàng trên Google Sheets để team dễ dàng theo dõi.
- **Hoạt động 24/7 bền bỉ:** Chạy ngầm liên tục trên hệ thống tự động, không lo bỏ sót dữ liệu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Facebook Developer / Meta Business Suite:** Đã tạo App và lấy được Access Token để gọi Facebook Graph API.
- **Google Sheets:** Tài khoản Google có quyền tạo và chỉnh sửa file Sheets.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này (hoặc tải file JSON từ link nguồn) và import trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:
- **Set Schedule / Set Schedule1:** Cấu hình thời gian chạy định kỳ (ví dụ: mỗi sáng lúc 8:00 AM).
- **Add credentials to the Facebook Graph API:** Thêm thông tin xác thực Facebook Access Token của các sếp vào đây để kết nối với tài khoản quảng cáo.
- **Get Campaign from AD Account & Get Campaign statistics (HTTP Request):** Kiểm tra lại đường dẫn API endpoint và cấu hình truyền ID tài khoản quảng cáo (Ad Account ID) cho đúng chuẩn Facebook Graph API.
- **Get Campaign ID, Add your campaign to file, Update row in sheet4, Update Campaign statistics (Google Sheets):** 
  - Kết nối tài khoản Google Sheets của các sếp.
  - Trỏ đúng đến File Google Sheets và Sheet Name (Tên trang tính) mà các sếp muốn lưu trữ dữ liệu chiến dịch và thống kê.
- **Code1 & Checking Conversion (Code Nodes):** Kiểm tra lại các đoạn mã xử lý dữ liệu JSON trả về từ Facebook để đảm bảo map đúng các trường (fields) như spend, clicks, conversions, campaign_name...

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để chạy thử thủ công (Test run) với dữ liệu mẫu xem có lỗi phát sinh không.
- Sau khi test thành công, gạt công tắc **Active** ở góc trên cùng bên phải để bật chế độ tự động chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Bắn thông báo qua Telegram/Slack:** Thêm node Telegram hoặc Slack ở cuối workflow để mỗi khi cập nhật báo cáo xong, hệ thống sẽ gửi tóm tắt chi phí và kết quả quảng cáo thẳng vào nhóm chat của team.
- **Lưu lịch sử chạy (Log):** Kết hợp thêm một dòng ghi log thời gian chạy thành công vào một sheet riêng để dễ dàng debug nếu có sự cố.
- **Mở rộng báo cáo theo nhóm quảng cáo (Ad Set) hoặc Quảng cáo đơn lẻ (Ad):** Các sếp có thể nhân bản nhánh gọi API Facebook để lấy thêm thông tin chi tiết sâu hơn thay vì chỉ dừng lại ở cấp độ Chiến dịch (Campaign).

### 📌 Kết luận
Một workflow cực kỳ "must-have" cho các Digital Marketer, Agency hay các chủ doanh nghiệp tự chạy quảng cáo. Thiết lập một lần, thảnh thơi trọn đời. Chúc các sếp cài đặt thành công và tối ưu chi phí quảng cáo hiệu quả!