---
title: "🚀 Tự động quét và trích xuất email doanh nghiệp với Serper.dev và ScrapingBee qua Google Sheets"
description: "Hướng dẫn xây dựng hệ thống tự động hóa tìm kiếm khách hàng tiềm năng (Lead Generation), tìm kiếm website công ty qua Serper.dev, quét trang liên hệ bằng ScrapingBee và lưu kết quả trực tiếp vào Google Sheets."
slug: "tu-dong-trich-xuat-email-doanh-nghiep-serper-scrapingbee-n8n"
tags: [n8n, automation, no-code, lead-generation, scrapingbee, serper-dev, google-sheets]
keywords: [n8n workflow, trích xuất email tự động, lead generation n8n, serper.dev api, scrapingbee n8n, google sheets automation]
---

# 🚀 Tự động quét và trích xuất email doanh nghiệp với Serper.dev và ScrapingBee qua Google Sheets

Việc tìm kiếm khách hàng tiềm năng (Lead Generation) thủ công như lên Google tra cứu từng doanh nghiệp, lọc website, mò mẫm vào trang Liên hệ (`/contact`, `/about`) để copy email thường ngốn hàng giờ đồng hồ nhưng hiệu quả lại thấp. 

Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình trên: kích hoạt ngay khi cập nhật Google Sheets, tìm kiếm thông tin doanh nghiệp qua **Serper.dev**, kiểm tra URL sống/chết, quét nội dung trang web bằng **ScrapingBee**, trích xuất email tự động và cập nhật ngược lại Google Sheets một cách mượt mà!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Divider] [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chỉ cần đổi trạng thái `activate` trên Google Sheet, hệ thống tự động làm việc từ A-Z.
- **Dữ liệu chính xác, sạch sẽ:** Kết hợp Serper.dev tìm đúng doanh nghiệp theo địa phương và ScrapingBee xử lý việc vượt qua các lớp chống bot của website.
- **Quản lý trạng thái thông minh:** Tự động ghi nhận các trạng thái `Missing information`, `Running`, hay `Finished` trực tiếp trên bảng tính.
- **Tiết kiệm 90% thời gian:** Gom toàn bộ email liên hệ của hàng loạt công ty vào chung một file Google Sheets chỉ trong vài phút.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn (Self-hosted hoặc Cloud).
- **Google Sheets:** Tài khoản Google và quyền kết nối API (Google Cloud OAuth2). Sử dụng sẵn [Sheet Template mẫu tại đây](https://docs.google.com/spreadsheets/d/1222TvBxE2UBb1MK2xDMoQSd5WHQ7mA5Ew-W6vBgfCJs/edit?usp=sharing).
- **Serper.dev API Key:** Đăng ký tài khoản miễn phí tại [Serper.dev](https://serper.dev/).
- **ScrapingBee API Key:** Đăng ký tài khoản miễn phí tại [ScrapingBee](https://www.scrapingbee.com/).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này hoặc copy toàn bộ mã nguồn JSON.
- Trong giao diện n8n Editor, nhấn vào dấu **`+` (Add workflow)** -> Chọn **Import from File** hoặc dán trực tiếp vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thành phần sau trong workflow (tổng cộng 20 nodes):

- **Google Sheets Trigger:** Kết nối tài khoản Google Sheets của các sếp qua OAuth2, trỏ tới file Google Sheet quản lý lead.
- **Set Information (Node `Set Information`):** Điền các tham số cấu hình tìm kiếm mặc định như:
  - `country`: Quốc gia tìm kiếm (Ví dụ: United States, Argentina...).
  - `country_code`: Mã quốc gia (Ví dụ: `US`, `AR`).
  - `language`: Ngôn ngữ (`en`, `es`,...).
  - `result_count`: Số lượng kết quả trả về cho mỗi truy vấn.
- **Search Companies (Serper.dev) (Node `Search Companies (Serper.dev)`):** Thêm Header Authentication chứa API Key lấy từ Serper.dev để thực hiện gọi API tìm kiếm doanh nghiệp.
- **Scraping Bee (Node `Scraping Bee`):** Cấu hình URL và chèn ScrapingBee API Key để tiến hành cào dữ liệu từ các trang liên hệ (`/contact`, `/about`) của công ty.
- **Các node Google Sheets (`Update Running Status`, `Update Missing Information Status`, `Add research Results`, `Update Finished Status`, `Add Emails`):** Đảm bảo map đúng tên các cột trong file Google Sheets template (`business type`, `city`, `state`, `activate`,...).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test workflow**) với 1 dòng dữ liệu mẫu trên Google Sheets để kiểm tra luồng chạy của các nhánh `If`, vòng lặp `Loop Over Items` (Split In Batches).
- Sau khi test thành công, bật nút **Active** ở góc trên bên phải để workflow tự động hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng nguồn dữ liệu:** Có thể cấu hình để đọc các tham số `country`, `country_code` động trực tiếp từ từng dòng trong Google Sheet thay vì dùng cố định ở node *Set Information*.
- **Blacklist từ khóa:** Tinh chỉnh code node lọc kết quả trong workflow để loại bỏ các trang web không mong muốn (như Wikipedia, trang báo chí, mạng xã hội...).
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack ở cuối luồng để nhận thông báo ngay lập tức mỗi khi có một batch doanh nghiệp được quét và tìm thấy email thành công.

### 📌 Kết luận
Workflow tích hợp giữa **Serper.dev** và **ScrapingBee** này là vũ khí cực kỳ mạnh mẽ cho đội ngũ Sales và Marketing muốn xây dựng phễu khách hàng tự động với chi phí tối ưu. Hãy triển khai ngay hôm nay để tối ưu hóa năng suất làm việc của các sếp!