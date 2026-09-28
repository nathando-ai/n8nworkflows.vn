---
title: "🚀 Tự Động Lấy Toàn Bộ Đơn Hàng Shopify Vượt Giới Hạn 250 Tránh Lỗi Phân Trang Bằng n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động đồng bộ toàn bộ đơn hàng từ Shopify qua GraphQL API, vượt qua giới hạn 250 đơn/lần gọi và lưu trữ gọn gàng vào Google Sheets."
slug: "tu-dong-lay-toan-bo-don-hang-shopify-vuot-gioi-han-250-n8n"
tags: [n8n, automation, shopify, google-sheets, graphql, e-commerce]
keywords: [n8n workflow, shopify orders automation, graphql pagination n8n, đồng bộ đơn hàng shopify, google sheets shopify sync]
---

# 🚀 Tự Động Lấy Toàn Bộ Đơn Hàng Shopify Vượt Giới Hạn 250 Tránh Lỗi Phân Trang Bằng n8n

Trong vận hành cửa hàng thương mại điện tử, việc thống kê và quản lý đơn hàng là công việc diễn ra hằng ngày. Tuy nhiên, khi sử dụng API của Shopify, các sếp thường gặp phải cơn ác mộng mang tên **"Giới hạn 250 đơn hàng mỗi lần gọi" (250-Limit)** và việc xử lý phân trang (pagination) phức tạp bằng tay hoặc các đoạn code rối rắm. 

Đừng lo! Workflow n8n được thiết kế bởi **Strategiflows** này sẽ giúp các sếp giải quyết triệt để bài toán trên. Với sự kết hợp thông minh giữa **Schedule Trigger**, **GraphQL API** và **Google Sheets**, hệ thống sẽ tự động quét, lặp (loop) qua toàn bộ các trang dữ liệu để lấy trọn vẹn 100% đơn hàng và lưu trữ gọn gàng mà không bỏ sót bất kỳ một đơn nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Vượt giới hạn 250 đơn:** Tự động gọi API lặp lại liên tục cho đến khi lấy sạch sẽ toàn bộ đơn hàng của cửa hàng Shopify.
- **Tự động hóa hoàn toàn:** Kích hoạt theo lịch trình (Schedule) định sẵn, không cần ai phải bấm nút thủ công mỗi ngày.
- **Xử lý dữ liệu thông minh:** Gom nhóm và phân loại sản phẩm theo Vendor trước khi đẩy dữ liệu vào Google Sheets.
- **Lưu trữ trực quan:** Dữ liệu đơn hàng được cập nhật minh bạch, sẵn sàng cho việc làm báo cáo doanh thu, tồn kho.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một tài khoản n8n (Cloud hoặc Self-hosted).
- **Shopify Store & Admin API / GraphQL Access Token** (Tạo Custom App trên Shopify Admin để lấy thông tin kết nối `httpHeaderAuth`).
- **Google Account** đã kết nối sẵn với n8n để ghi dữ liệu vào Google Sheets.
- Một file Google Sheets chuẩn bị sẵn các cột tương ứng với thông tin đơn hàng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy mã JSON của workflow từ nguồn gốc hoặc tải file về, sau đó chọn **Import from File** hoặc dán trực tiếp (`Ctrl + V`) vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 6 nodes chính hoạt động nhịp nhàng với nhau. Các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Schedule Trigger:** Thiết lập mốc thời gian chạy tự động (ví dụ: chạy mỗi sáng lúc 8:00 hoặc chạy mỗi giờ tùy nhu cầu cửa hàng).
- **searchPeriod (Set):** Cấu hình khoảng thời gian tìm kiếm đơn hàng (ví dụ: từ ngày hôm qua đến hôm nay, hoặc theo dõi theo chu kỳ cố định).
- **getOrderDoLoop (GraphQL):** 
  - Cấu hình thông tin xác thực (`httpHeaderAuth`) bằng Shopify Admin API Access Token của các sếp.
  - Kiểm tra lại câu truy vấn GraphQL để đảm bảo lấy đúng các trường thông tin đơn hàng mong muốn (Mã đơn, Khách hàng, Tổng tiền, Trạng thái...).
  - Thiết lập cơ chế lặp (loop) dựa trên biến con trỏ trang (`cursor` / `pageInfo`).
- **is hasNextPage = true (If):** Node điều kiện kiểm tra xem Shopify còn trang dữ liệu tiếp theo hay không (`hasNextPage == true`). Nếu còn, vòng lặp tiếp tục gọi API lấy dữ liệu trang kế tiếp.
- **groupItemListbyVendor (Code):** Node chạy mã JavaScript tùy chỉnh để xử lý, nhóm các item trong đơn hàng lại theo từng Nhà cung cấp (Vendor) nhằm phục vụ việc đối soát.
- **Google Sheets:** 
  - Chọn tài khoản kết nối Google Sheets OAuth2.
  - Chọn đúng file Google Sheet (`Document`) và Sheet Name đích.
  - Map các trường dữ liệu từ workflow vào đúng các cột trong bảng tính.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để chạy thử nghiệm (Test Run) với một khoảng thời gian ngắn nhằm kiểm tra dữ liệu trả về từ Shopify và chắc chắn rằng Google Sheets đã nhận đủ dòng.
- Sau khi test thành công, gạt công tắc sang chế độ **Active** để hệ thống tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack vào cuối chuỗi để bắn thông báo ngay về điện thoại mỗi khi đồng bộ thành công số lượng lớn đơn hàng trong ngày.
- **Xử lý lỗi (Error Handling):** Thêm node *Error Trigger* để nếu có sự cố mất kết nối mạng với Shopify API, hệ thống sẽ tự động gửi cảnh báo giúp các sếp xử lý kịp thời.
- **Lưu log chi tiết:** Lưu lại lịch sử các lần chạy (Run history) hoặc ghi log vào một Sheet phụ để dễ dàng kiểm tra khi có sai sót về dữ liệu tài chính.

### 📌 Kết luận
Việc quản lý đơn hàng thủ công trên Shopify vừa mất thời gian vừa dễ xảy ra sai sót khi lượng đơn hàng tăng mạnh. Với workflow n8n thông minh này, bài toán xử lý giới hạn phân trang GraphQL đã được giải quyết trọn gói. Hãy cài đặt ngay để tối ưu hóa quy trình vận hành cho cửa hàng của các sếp!