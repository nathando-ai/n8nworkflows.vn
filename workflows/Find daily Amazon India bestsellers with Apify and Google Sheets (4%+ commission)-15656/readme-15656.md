---
title: "🚀 Tự động săn sản phẩm bán chạy Amazon Ấn Độ với Apify và Google Sheets"
description: "Khám phá cách tự động hóa việc tìm kiếm các sản phẩm bán chạy nhất trên Amazon Ấn Độ (mức hoa hồng 4%+) bằng n8n, Apify và Google Sheets để làm Affiliate Marketing cực nhàn."
slug: "tu-dong-san-san-pham-ban-chay-amazon-india-apify-google-sheets"
tags: [n8n, automation, no-code, affiliate-marketing, apify, google-sheets, e-commerce]
keywords: [n8n workflow, tự động hóa affiliate amazon, apify amazon scraper, google sheets automation, săn hàng bán chạy amazon india]
keywords: [n8n workflow, tự động hóa affiliate amazon, apify amazon scraper, google sheets automation, săn hàng bán chạy amazon india]
---

# 🚀 Tự động săn sản phẩm bán chạy Amazon Ấn Độ với Apify và Google Sheets

Việc làm Affiliate Marketing cho các nền tảng thương mại điện tử lớn như Amazon đòi hỏi các sếp phải liên tục cập nhật xu hướng và tìm ra các sản phẩm có tỷ lệ hoa hồng cao (từ 4% trở lên) cùng lượng mua khủng để làm nội dung. Nếu ngồi cào dữ liệu thủ công mỗi ngày, các sếp sẽ mất hàng giờ đồng hồ lướt web, lọc danh mục và copy-paste vào bảng tính.

Giải pháp ở đây là gì? Workflow n8n này sẽ tự động hóa 100% quy trình: tự động quét danh mục theo mùa, gọi API của Apify để cào dữ liệu sản phẩm bán chạy trên Amazon Ấn Độ, lọc ra những "món hời" tiềm năng nhất và lưu thẳng vào Google Sheets để các sếp tha hồ lên chiến dịch content!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hoàn toàn**: Mỗi sáng, hệ thống tự động chạy ngầm mà không cần can thiệp thủ công.
- **Tiết kiệm hàng chục giờ**: Loại bỏ hoàn toàn thao tác cào data tay, giúp tập trung vào tối ưu nội dung và chiến dịch.
- **Dữ liệu luôn tươi mới**: Cập nhật sát sao các sản phẩm "Best Sellers" theo xu hướng mùa vụ.
- **Tối ưu hóa lợi nhuận**: Dễ dàng nhắm đến các sản phẩm có biên độ hoa hồng hấp dẫn (4%+).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động (Self-hosted hoặc n8n Cloud).
- Tài khoản **Apify** (có API Token để gọi Actor cào dữ liệu Amazon).
- Tài khoản **Google Sheets** đã chuẩn bị sẵn một file Google Sheet để lưu trữ danh sách sản phẩm.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc import file JSON tải từ nguồn chính thức.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 6 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Every Day at 8:02 AM (`scheduleTrigger`)**: Node này đặt lịch chạy tự động mỗi ngày vào lúc 8:02 sáng. Các sếp có thể đổi lại múi giờ hoặc khung giờ cho phù hợp với chiến dịch.
- **Select Seasonal Category (`code`)**: Node JavaScript này dùng để chọn danh mục sản phẩm theo mùa vụ. Các sếp có thể tùy chỉnh danh mục sản phẩm Amazon muốn quét bên trong đoạn mã code.
- **Post to Apify Actor API (`httpRequest`)**: Gửi yêu cầu đến Apify Actor. Cần cấu hình **Apify API Token** trong phần Credentials để xác thực.
- **Retrieve Apify Dataset (`@apify/n8n-nodes-apify.apify`)**: Node này lấy kết quả dataset từ Apify trả về. Đảm bảo cấu hình đúng Apify Credential ở đây.
- **Calculate and Select Top Products (`code`)**: Đoạn code xử lý logic, tính toán và lọc ra các sản phẩm top đầu đáp ứng tiêu chí hoa hồng và lượt bán.
- **Append Products to Sheets (`googleSheets`)**: Node kết nối Google Drive/Sheets. Các sếp cần kết nối tài khoản Google, chọn đúng **Spreadsheet ID** và **Sheet Name** để dữ liệu đổ về đúng chỗ.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** để chạy thử nghiệm với dữ liệu mẫu xem các node có hoạt động mượt mà không.
- Sau khi kiểm tra dữ liệu đã đổ về Google Sheets chuẩn chỉnh, hãy bật nút **Active** ở góc trên bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack**: Thêm node Telegram hoặc Slack vào cuối workflow để nhận thông báo ngay lập tức về điện thoại mỗi khi có danh sách sản phẩm mới được tìm thấy.
- **Tự động tạo nội dung AI**: Kết hợp thêm OpenAI/Claude node sau bước lọc sản phẩm để tự động viết bài review hoặc tiêu đề bài đăng affiliate dựa trên tên sản phẩm vừa quét được.
- **Mở rộng thị trường**: Sửa lại cấu hình Apify Actor để quét thêm các quốc gia khác như Amazon Mỹ (US), Nhật Bản (JP) nếu muốn mở rộng Global Affiliate.

### 📌 Kết luận
Tự động hóa quy trình nghiên cứu thị trường và tìm kiếm sản phẩm affiliate là chìa khóa giúp các sếp đi trước đối thủ một bước. Hãy "lên đồ" ngay workflow này trên n8n để tối ưu hóa công việc kinh doanh của mình nhé!