---
title: "🚀 Tự động hóa báo cáo Meta Ads hàng ngày vào Google Sheets và gửi Email"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy dữ liệu quảng cáo Meta Ads, lưu trữ vào Google Sheets và gửi báo cáo HTML qua Gmail mỗi ngày."
slug: "tu-dong-hoa-bao-cao-meta-ads-google-sheets-gmail"
tags: [n8n, automation, no-code, meta-ads, google-sheets, gmail, marketing]
keywords: [n8n workflow, tự động hóa meta ads, báo cáo quảng cáo facebook, google sheets, gmail automation]
---

# 🚀 Tự động hóa báo cáo Meta Ads hàng ngày vào Google Sheets và gửi Email

Việc tổng hợp dữ liệu quảng cáo Facebook (Meta Ads) thủ công mỗi ngày để làm báo cáo cho sếp hoặc khách hàng ngốn rất nhiều thời gian và dễ xảy ra sai sót. Các chỉ số như chi phí (spend), lượt chuyển đổi (conversions), hay CPC, CPM cứ phải copy-paste liên tục từ Ads Manager sang Excel. 

Giải pháp ư? Hãy để n8n lo việc đó! Workflow này sẽ tự động hóa 100% quy trình: lấy dữ liệu ngày hôm qua từ Meta Ads, cập nhật thẳng vào Google Sheets và soạn một bản báo cáo HTML cực kỳ chuyên nghiệp gửi qua Gmail vào 9 giờ sáng mỗi ngày. Các sếp chỉ việc uống cà phê và check mail thôi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian thủ công:** Không còn cảnh sáng sớm phải lọ mọ vào Ads Manager xuất file Excel.
- **Dữ liệu luôn minh bạch, cập nhật:** Tự động hóa lịch trình chạy đều đặn mỗi ngày lúc 9h sáng.
- **Báo cáo chuyên nghiệp:** Email dạng HTML trực quan, dễ nhìn giúp nắm bắt hiệu suất chiến dịch ngay lập tức.
- **Lưu trữ dài hạn:** Mọi số liệu được đồng bộ hóa gọn gàng vào Google Sheets để tiện phân tích xu hướng (trend).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Meta Business / Facebook Ads API** (Access Token có quyền đọc dữ liệu Insights).
- Tài khoản **Google Account** (để kết nối Google Sheets).
- Tài khoản **Gmail** (để gửi email báo cáo).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ n8n (hoặc sử dụng link gốc ID `5125`), sau đó copy toàn bộ mã JSON và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 7 nodes chính, các sếp cần cấu hình lần lượt theo thứ tự luồng xử lý:

1. **Trigger - Daily at 9AM (`scheduleTrigger`):**
   - Mặc định lịch chạy là 9:00 sáng mỗi ngày. Các sếp có thể thay đổi múi giờ (timezone) cho trùng với giờ Việt Nam (Asia/Ho_Chi_Minh).
2. **Set Yesterday's Date (`set`):**
   - Node này tự động tính toán mốc thời gian của ngày hôm qua để query dữ liệu chính xác từ Meta Ads. Không cần chỉnh sửa gì nhiều trừ khi muốn đổi khoảng thời gian (ví dụ: 7 ngày gần nhất).
3. **Fetch Ads Data (`httpRequest`):**
   - Cấu hình API endpoint tới Meta Marketing API. Các sếp cần điền **Access Token** của Meta Ads và **Ad Account ID** vào phần Header/Query Parameters để n8n có quyền lấy dữ liệu.
4. **Transform Ads Data (`code`):**
   - Đoạn mã Javascript (Node.js) giúp lọc và làm sạch dữ liệu thô từ Meta API, chuyển đổi các định dạng số liệu cho dễ đọc.
5. **Update Google Sheet (`googleSheets`):**
   - Kết nối tài khoản Google Sheets thông qua **OAuth2 API**. 
   - Chọn file Google Sheet và Sheet Name cụ thể để dòng dữ liệu mới tự động `append` (thêm vào cuối bảng) mỗi ngày.
6. **Generate Email HTML (`code`):**
   - Đoạn mã tạo template HTML cho email. Các sếp có thể tùy chỉnh lại màu sắc, logo hoặc bố cục hiển thị các chỉ số chi phí, ROAS, CPA tùy theo sở thích.
7. **Send Email Report (`gmail`):**
   - Kết nối tài khoản Gmail (`gmailOAuth2`) và điền danh sách email nhận báo cáo (của sếp, team marketing hoặc khách hàng).

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** lần đầu để kiểm tra xem dữ liệu từ Meta Ads có đổ về Google Sheets và gửi email thành công không.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram/Slack:** Ngoài gửi email, các sếp có thể gắn thêm node Telegram Bot để bắn thông báo nhanh vào group chat của team ngay sau khi cập nhật sheet xong.
- **Cảnh báo ngân sách (Budget Alert):** Thêm điều kiện `If` trong code, nếu chi phí vượt mức cho phép hoặc CPA quá cao, tự động gửi cảnh báo khẩn cấp.
- **Lưu log chạy:** Ghi lại trạng thái thành công/thất bại vào một sheet riêng để dễ dàng debug nếu API Meta có sự cố gián đoạn.

### 📌 Kết luận
Tự động hóa báo cáo Meta Ads chưa bao giờ dễ dàng đến thế với n8n. Chỉ với một lần thiết lập duy nhất, các sếp đã giải phóng bản thân khỏi những con số lặp đi lặp lại mỗi ngày. Triển khai ngay thôi nào!