---
title: "🚀 Tự động trích xuất thông tin sản phẩm từ ảnh chụp màn hình website với Dumpling AI và Google Sheets"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động chụp màn hình website, dùng AI phân tích và lưu thông tin sản phẩm vào Google Sheets không cần code."
slug: "trich-xuat-thong-tin-san-pham-tu-anh-chup-man-hinh-website-voi-dumpling-ai"
tags: [n8n, automation, no-code, ai, google-sheets, dumpling-ai, web-scraping]
keywords: [n8n workflow, trích xuất thông tin sản phẩm, dumbling ai, google sheets automation, tự động hóa no-code]
---

# 🚀 Tự động trích xuất thông tin sản phẩm từ ảnh chụp màn hình website với Dumpling AI và Google Sheets

Các sếp có bao giờ cảm thấy mệt mỏi khi phải ngồi hàng giờ để copy-paste thủ công tên sản phẩm, giá cả, giảm giá và đánh giá từ các trang web đối thủ hoặc danh mục hàng hóa của mình vào Google Sheets chưa? Công việc lặp đi lặp lại này không chỉ tốn thời gian mà còn dễ dẫn đến sai sót dữ liệu.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ thông minh, tự động hóa 100% quy trình: chỉ cần dán URL vào Google Sheets, hệ thống sẽ tự động chụp màn hình trang web, dùng AI phân tích hình ảnh và trả về dữ liệu có cấu trúc gọn gàng ngay lập tức!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần copy-paste thủ công từng sản phẩm, tự động hóa hoàn toàn từ URL đến bảng tính.
- **Dữ liệu chính xác tuyệt đối:** Sử dụng sức mạnh của AI (Dumpling AI) để đọc hiểu hình ảnh trang web và bóc tách đúng các trường dữ liệu (Tên, giá, khuyến mãi, rating...).
- **Cập nhật catalog nhanh chóng:** Giúp đội ngũ kinh doanh, marketing nắm bắt thông tin giá cả và sản phẩm của thị trường một cách liên tục, theo thời gian thực.
- **Hoạt động tự động 24/7:** Chạy ngầm liên tục trên n8n mà không cần sự can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu "lên đồ", các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Google Sheets** có sẵn một file chứa cột URL sản phẩm.
- **Tài khoản/API Key từ Dumpling AI** để thực hiện chụp màn hình và trích xuất dữ liệu từ hình ảnh.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow này và dán trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 7 nodes chính phối hợp nhịp nhàng với nhau. Các sếp cần chú ý cấu hình các node sau:

- **Watch for New Screenshot URLs in Google Sheets (`googleSheetsTrigger`):** 
  - Kết nối tài khoản Google thông qua OAuth2.
  - Chọn đúng file Spreadsheet và Sheet chứa danh sách URL sản phẩm của các sếp. Node này sẽ làm nhiệm vụ "lắng nghe" khi có dòng mới được thêm vào.
- **Create Screenshot File via Dumpling AI & Extract Text from Screenshot with Dumpling AI (`httpRequest`):**
  - Cần cấu hình `Credentials` bằng `httpHeaderAuth` với API Key được cấp từ Dumpling AI.
  - Đảm bảo endpoint API trỏ đúng đến dịch vụ chụp màn hình và phân tích ảnh của Dumpling AI.
- **Download Screenshot Image File from Dumpling AI (`httpRequest`):**
  - Node này tải file ảnh screenshot về dạng binary để chuẩn bị cho bước chuyển đổi tiếp theo.
- **Convert Image File to Base64 (`extractFromFile`):**
  - Sử dụng thông số `operation: "binaryToPropery"` để chuyển đổi định dạng ảnh từ binary sang chuỗi Base64 chuẩn bị gửi cho AI phân tích.
- **Format Extracted Data for Google Sheets (`set`):**
  - Node này giúp tinh chỉnh, gán nhãn và ánh xạ các trường dữ liệu mà AI vừa trích xuất (tên, giá, giảm giá, đánh giá...) khớp với các cột trên Google Sheets.
- **Save extracted data to Google Sheets (`googleSheets`):**
  - Cấu hình `operation` thành `appendOrUpdate`.
  - Chọn lại file Google Sheets ban đầu để node này ghi đè hoặc thêm mới dữ liệu vào đúng dòng chứa URL sản phẩm tương ứng.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử thêm một URL sản phẩm mới vào Google Sheets để kiểm tra xem dữ liệu có được trả về bảng tính chính xác hay không.
- Sau khi test thành công, hãy gạt công tắc sang **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình làm việc, các sếp có thể mở rộng workflow này bằng cách:
1. **Thêm thông báo Telegram/Slack:** Gửi tin nhắn thông báo về Slack hoặc Telegram mỗi khi có một sản phẩm mới được cào và lưu thành công.
2. **Xử lý lỗi (Error Handling):** Thêm Error Trigger để bắt lỗi nếu URL bị lỗi 404 hoặc trang web chặn bot, giúp hệ thống không bị dừng đột ngột.
3. **Lên lịch báo cáo định kỳ:** Kết hợp thêm Schedule Trigger để quét lại toàn bộ danh sách sản phẩm cũ nhằm cập nhật biến động giá theo tuần/tháng.

### 📌 Kết luận
Với sự kết hợp mượt mà giữa Google Sheets, Dumpling AI và n8n, việc thu thập dữ liệu sản phẩm từ website chưa bao giờ dễ dàng đến thế. Hãy triển khai ngay hôm nay để giải phóng sức lao động cho đội ngũ của các sếp!