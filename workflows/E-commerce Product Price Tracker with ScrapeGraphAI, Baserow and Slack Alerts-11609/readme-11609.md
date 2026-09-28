---
title: "🚀 Tự động theo dõi giá sản phẩm E-commerce với ScrapeGraphAI, Baserow và Slack Alerts"
description: "Hướng dẫn xây dựng workflow n8n tự động cào giá sản phẩm thương mại điện tử bằng AI, lưu trữ dữ liệu vào Baserow và gửi cảnh báo tức thì qua Slack khi có biến động giá."
slug: "theo-doi-gia-san-pham-e-commerce-scrapegraphai-baserow-slack"
tags: [n8n, automation, scrapegraphai, baserow, slack, e-commerce]
keywords: [n8n workflow, theo dõi giá sản phẩm, scrapegraphai, baserow, slack alerts, tự động hóa e-commerce]
keywords: [n8n workflow, tự động hóa, theo dõi giá sản phẩm, scrapegraphai, baserow, slack alerts]
---

# 🚀 Tự động theo dõi giá sản phẩm E-commerce với ScrapeGraphAI, Baserow và Slack Alerts

Các sếp kinh doanh ngành hàng E-commerce có bao giờ đau đầu vì việc kiểm tra giá đối thủ hoặc nguồn hàng thủ công mỗi ngày? Việc này không chỉ tốn hàng giờ đồng hồ mà còn dễ bỏ lỡ các đợt giảm giá chớp nhoáng (flash sale) hay thay đổi nguồn cung đột ngột. 

Giải pháp hoàn hảo cho các sếp đây! Bài viết này sẽ hướng dẫn chi tiết cách vận hành một workflow n8n tự động hóa 100% quy trình: cào dữ liệu thông minh bằng AI, lưu trữ lịch sử giá và chủ động gửi cảnh báo khi giá chạm ngưỡng mong muốn. Không cần code phức tạp, các sếp chỉ cần "lên đồ" theo hướng dẫn dưới đây.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chạy định kỳ hàng tuần nhờ **Weekly Schedule**, không cần thao tác tay.
- **Bất chấp thay đổi giao diện:** Sử dụng **ScrapeGraphAI** thông minh trích xuất dữ liệu chuẩn xác mà không lo website đối thủ đổi CSS selectors.
- **Lưu trữ dữ liệu lịch sử:** Tự động đẩy toàn bộ bản ghi giá vào **Baserow** giúp phân tích xu hướng thị trường dễ dàng.
- **Cảnh báo thời gian thực:** Lập tức nhận thông báo qua **Slack** (hoặc kênh tùy chỉnh) ngay khi sản phẩm rớt giá dưới ngưỡng cài đặt.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị sẵn các tài nguyên sau:
- Tài khoản n8n đang hoạt động (Self-hosted hoặc Cloud).
- API Key từ **ScrapeGraphAI**.
- Tài khoản và cơ sở dữ liệu trên **Baserow** kèm API Token.
- Workspace và Bot Token của **Slack** để nhận cảnh báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow (hoặc tải file JSON từ nguồn gốc) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 12 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:
- **Define Product Sources**: Mở Code node này và điền danh sách các URL sản phẩm E-commerce mà các sếp muốn theo dõi giá.
- **Scrape Product Page**: Điền thông tin Credentials của ScrapeGraphAI để AI có thể bắt đầu đọc hiểu trang web.
- **Store Price Record**: Kết nối tài khoản Baserow, chọn đúng Base, Table ID và map các trường dữ liệu tương ứng (Product Name, Price, Currency, Availability, URL, Timestamp).
- **Is Price Below Threshold?**: Điều chỉnh mức giá giới hạn (`PRICE_ALERT_THRESHOLD`) trong điều kiện IF để hệ thống lọc ra các deal hời.
- **Send a message**: Cấu hình kênh Slack nhận thông báo để team kịp thời nắm bắt cơ hội.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử với dữ liệu mẫu và kiểm tra xem dữ liệu có đổ về Baserow/Slack thành công không.
- Sau khi test ngon lành, gạt công tắc sang **Active** để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Ngoài Slack, các sếp có thể nối thêm node Telegram hoặc Email để gửi tin nhắn đến nhiều phòng ban cùng lúc.
- **Tạo Dashboard phân tích:** Kết nối Baserow với các công cụ BI hoặc Metabase để vẽ biểu đồ biến động giá theo mùa cực kỳ chuyên nghiệp.
- **Xử lý lỗi thông minh:** Tận dụng node **Error Handler** để đẩy log lỗi về một channel riêng trên Slack giúp dễ dàng giám sát hệ thống.

### 📌 Kết luận
Với workflow n8n kết hợp AI này, việc nghiên cứu thị trường và theo dõi giá đối thủ sẽ trở nên nhẹ nhàng hơn bao giờ hết. Chúc các sếp cài đặt thành công và tối ưu hóa hiệu quả kinh doanh! Áp dụng ngay thôi nào!