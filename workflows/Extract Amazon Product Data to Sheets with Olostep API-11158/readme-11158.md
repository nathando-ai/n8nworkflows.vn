---
title: "🚀 Tự Động Cào Dữ Liệu Sản Phẩm Amazon Vào Bảng Dữ Liệu Với Olostep API"
description: "Hướng dẫn xây dựng workflow n8n tự động cào hàng loạt sản phẩm trên Amazon (tên, link) từ từ khóa tìm kiếm qua Olostep API và lưu thẳng vào Google Sheets / Data Table."
slug: "tu-dong-cao-du-lieu-san-pham-amazon-olostep-api"
tags: [n8n, automation, no-code, web-scraping, amazon-scraper, olostep]
keywords: [n8n workflow, cào dữ liệu amazon, olostep api, tự động hóa n8n, web scraping no code, google sheets automation]
---

# 🚀 Tự Động Cào Dữ Liệu Sản Phẩm Amazon Vào Bảng Dữ Liệu Với Olostep API

Các sếp có đang mất hàng giờ liền để lướt Amazon, copy từng tên sản phẩm và đường dẫn (URL) thủ công để làm nghiên cứu thị trường (Market Research)? Việc này không chỉ tốn thời gian, dễ sai sót mà còn cực kỳ nhàm chán.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n siêu việt, kết hợp sức mạnh của **Olostep API**. Chỉ cần nhập một từ khóa tìm kiếm bất kỳ, hệ thống sẽ tự động lướt qua nhiều trang Amazon, trích xuất dữ liệu sạch sẽ và lưu trữ gọn gàng vào bảng dữ liệu mà không cần đụng đến code hay trình duyệt phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các tác vụ cào dữ liệu nặng mà không lo sập nguồn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Thay vì copy/paste thủ công từng trang, hệ thống tự động cào từ trang 1 đến trang 10 chỉ với 1 cú click.
- **Dữ liệu sạch & chuẩn hóa**: Tự động lọc bỏ các link điều hướng rác của Amazon, chỉ giữ lại tiêu đề và đường dẫn sản phẩm hợp lệ.
- **Tích hợp linh hoạt**: Lưu trữ trực tiếp vào Google Sheets hoặc Data Table để phục vụ phân tích dữ liệu ngay lập tức.
- **Kiểm soát tốc độ**: Tích hợp cơ chế chờ thông minh (`Wait`), tránh việc bị giới hạn tốc độ (Rate Limit) từ phía API.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Olostep API** và API Key để thực hiện việc trích xuất dữ liệu web.
- **Google Sheets** hoặc cấu hình **Data Table** sẵn có trong n8n để lưu kết quả.
:::

---

## 🏗️ Tổng quan về Workflow (11 Nodes)
Workflow sử dụng các node chính sau đây để vận hành quy trình:
1. **On form submission** (`formTrigger`): Giao diện nhập từ khóa tìm kiếm (Ví dụ: *"wireless bluetooth headphones"*).
2. **Edit Fields / Set** (`set`): Chuẩn bị cấu trúc dữ liệu và tạo danh sách phân trang (Pagination từ 1 đến 10).
3. **Loop Over Items** (`splitInBatches`): Lần lượt duyệt qua từng trang tìm kiếm.
4. **scrape amazon products** (`httpRequest`): Gửi yêu cầu qua Olostep API để trích xuất dữ liệu thông minh bằng LLM.
5. **Parse & Split** (`splitOut`, `parsedInfo`): Giải mã JSON và tách dữ liệu thành từng sản phẩm riêng lẻ.
6. **URL Normalization** (`Edit Fields1`): Chuẩn hóa đường dẫn tương đối thành URL Amazon hoàn chỉnh.
7. **If** (`if`): Kiểm tra và lọc bỏ các URL không hợp lệ.
8. **Wait** (`wait`): Tạm dừng một nhịp giữa các request để tuân thủ giới hạn tốc độ API.
9. **Insert row** (`dataTable` / Google Sheets): Lưu thông tin sản phẩm (Title, URL) vào bảng.

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ kho lưu trữ n8n.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** và chọn file JSON vừa tải.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `On form submission`**: Thiết lập form hiển thị để người dùng nhập từ khóa tìm kiếm sản phẩm trên Amazon.
- **Node `scrape amazon products`**: 
  - Cần cấu hình **Credentials** cho Olostep API (nhập API Key của các sếp).
  - Kiểm tra phần JSON schema trong `llm_extract` để đảm bảo hệ thống trả về đúng 2 trường: `title` và `url`.
  - *Cảnh báo từ tác giả:* Nếu gặp lỗi `504 Gateway Timeout` do `llm_extract` quá tải, các sếp có thể đơn giản hóa schema trong request và dùng một node LLM riêng của n8n để bóc tách thông tin sau đó.
- **Node `Insert row`**: Kết nối tài khoản Google Sheets của các sếp hoặc trỏ trực tiếp vào n8n Data Table, map đúng 2 trường dữ liệu `title` và `url` vào các cột tương ứng.

#### 3. Khởi chạy & Kiểm tra ⚡️
- Nhấn **Test step** hoặc mở form preview để chạy thử với một từ khóa bất kỳ (Ví dụ: *"mechanical keyboard"*).
- Theo dõi quá trình chạy qua từng trang (Pagination 1-10) xem dữ liệu đã được đổ vào bảng chính xác chưa.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để đưa workflow vào vận hành chính thức!

---

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa workflow này cho các chiến dịch nghiên cứu thị trường lớn, các sếp có thể mở rộng thêm:
- **Tích hợp Telegram / Slack Bot**: Gửi thông báo ngay về máy khi workflow cào xong toàn bộ danh sách sản phẩm.
- **Mở rộng trường dữ liệu**: Tinh chỉnh Olostep API để lấy thêm giá bán (Price), đánh giá sao (Rating), hoặc số lượng đã bán nếu cần thiết.
- **Lưu lịch sử chạy**: Thêm một bước ghi log thời gian và số lượng sản phẩm cào được vào Google Sheets để dễ dàng theo dõi hiệu suất.

### 📌 Kết luận
Với sự kết hợp giữa n8n và Olostep API, việc cào dữ liệu sản phẩm Amazon chưa bao giờ trở nên mượt mà và tự động đến thế. Hãy triển khai ngay hôm nay để tiết kiệm hàng tá thời gian cho công việc nghiên cứu thị trường của doanh nghiệp các sếp nhé!