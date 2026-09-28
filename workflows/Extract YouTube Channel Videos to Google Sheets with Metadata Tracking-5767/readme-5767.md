---
title: "🚀 Tự động trích xuất Video kênh YouTube vào Google Sheets bằng n8n"
description: "Hướng dẫn chi tiết cách sử dụng n8n workflow để tự động crawl danh sách video, tiêu đề, mô tả và metadata từ bất kỳ kênh YouTube nào vào Google Sheets."
slug: "tu-dong-trich-xuat-video-youtube-vao-google-sheets"
tags: [n8n, automation, youtube, google-sheets, market-research, no-code]
keywords: [n8n workflow, crawl video youtube, google sheets automation, youtube api n8n, tự động hóa marketing]
---

# 🚀 Tự động trích xuất Video kênh YouTube vào Google Sheets

Các sếp có đang tốn hàng giờ để thủ công copy link, tiêu đề và mô tả video của đối thủ để làm nghiên cứu thị trường (Market Research)? Việc thu thập dữ liệu thủ công từ YouTube vừa tốn thời gian, dễ sai sót, lại khó cập nhật liên tục khi đối thủ ra video mới.

Đừng lo! Workflow n8n siêu việt này từ **Agent Circle** sẽ giúp các sếp tự động hóa 100% quy trình: đọc danh sách kênh từ Google Sheets, gọi YouTube API lấy toàn bộ thông tin video (URL, tiêu đề, mô tả, thumbnail, ngày xuất bản...), sau đó ghi ngược lại vào Google Sheets một cách ngăn nắp và tự động cập nhật trạng thái (`Ready`, `Finished`, `Error`). Hoàn toàn không cần viết code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần copy/paste thủ công từng video của đối thủ hay kênh yêu thích.
- **Dữ liệu cấu trúc sạch sẽ:** Tự động phân loại URL, tiêu đề, mô tả, thumbnail, ngày xuất bản vào đúng các tab Google Sheets.
- **Quản lý thông minh qua trạng thái:** Tự động chuyển trạng thái `Ready` thành `Finished` khi thành công hoặc `Error` nếu gặp lỗi để dễ dàng kiểm tra.
- **Linh hoạt giới hạn số lượng:** Dễ dàng tùy chỉnh số lượng video muốn lấy mỗi kênh (mặc định 10 video, có thể tăng tùy ý qua Google Sheets).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt và hoạt động bình thường.
- **Google Cloud Console Credentials:** 
  - OAuth2 API hoặc API Key có bật quyền truy cập **Google Sheets API** và **YouTube Data API v3**.
- **Google Sheets Template:** Copy bản mẫu Google Sheet chính thức tại [YouTube - Get Channel Videos Sheet Template](https://docs.google.com/spreadsheets/d/1GIdiUUx1PtEZXOzSUP3aJkrDaVcJdxCGRmCOT94BytA/edit?gid=426418282#gid=426418282).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này.
- Mở giao diện n8n, chọn **Import from File** hoặc copy toàn bộ mã JSON và dán trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 15 nodes được thiết kế tối ưu, các sếp cần chú ý cấu hình kỹ các phần sau:
- **Kết nối Google Sheets Credentials:** Áp dụng cho các node đọc/ghi dữ liệu:
  - Node `Google Sheets - Get Channel URLs`: Kết nối đúng vào tab **Channel URLs**.
  - Node `Google Sheets - Update Data`: Kết nối vào tab **Videos**.
  - Node `Google Sheets - Update Data - Success` & `Google Sheets - Update Data - Error`: Kết nối về tab **Channel URLs** để cập nhật trạng thái (`Finished` / `Error`).
- **Kết nối YouTube API Credentials (`youTubeOAuth2Api`):**
  - Cần cấu hình OAuth2 cho các node: `HTTP Request - Get Channel ID` và `HTTP Request - Get Channel Videos`.
- **Logic xử lý đầu vào (Switch Node):**
  - Node `Switch - Detect Channel ID or Channel URL` sẽ tự động nhận diện nếu các sếp nhập Channel ID nguyên bản hay Full/Custom Channel URL để tự động gọi API lấy đúng Channel ID tương ứng.

#### 3. Kích hoạt ⚡️
- Điền một vài URL kênh YouTube hoặc Channel ID vào cột tương ứng trong Google Sheet (Tab `Channel URLs`), đặt trạng thái là **Ready**. 
- Nếu muốn thay đổi số lượng video muốn lấy cho mỗi kênh, hãy điền số lượng mong muốn vào **Cột C** (mặc định là 10).
- Nhấp **Test workflow** để chạy thử nghiệm xem dữ liệu đổ về Google Sheets có chính xác không.
- Sau khi test thành công, bật nút **Active** để workflow sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa toàn diện:** Thay vì chạy thủ công bằng nút `Test workflow`, các sếp có thể thay thế node `When clicking ‘Test workflow’` bằng **Google Sheets Trigger** hoặc **Schedule Trigger** để hệ thống tự động quét các kênh mới cứ sau mỗi vài giờ hoặc hàng ngày.
- **Mở rộng Metadata:** Các sếp có thể tùy chỉnh thêm các tham số trong `HTTP Request - Get Channel Videos` để lấy thêm số lượng view, thời lượng video (duration), hoặc thống kê lượt tương tác nếu YouTube API hỗ trợ.
- **Gửi thông báo:** Kết hợp thêm node Slack hoặc Telegram ở cuối workflow để gửi báo cáo tóm tắt (Ví dụ: *"Đã crawl xong 50 video từ 5 kênh YouTube đối thủ!"*) về điện thoại cho các sếp.

### 📌 Kết luận
Với workflow n8n trích xuất video YouTube này, việc nghiên cứu đối thủ hay tổng hợp kho tàng nội dung video chưa bao giờ dễ dàng đến thế. Hãy "lên đồ" ngay để tối ưu hóa hiệu suất làm việc cho đội ngũ marketing của các sếp!