---
title: "🚀 Tự động hóa quét Leads Google Maps và trích xuất Email với SerpApi & Airtable"
description: "Hướng dẫn xây dựng hệ thống tự động tìm kiếm doanh nghiệp trên Google Maps, cào dữ liệu website và làm sạch email chuyên sâu bằng n8n."
slug: "tu-dong-hoa-quet-leads-google-maps-serpapi-airtable"
tags: [n8n, automation, lead-generation, serpapi, airtable, web-scraping]
keywords: [n8n workflow, serpapi google maps, airtable lead gen, cào email tự động, automation lead generation]
---

# 🚀 Tự động hóa quét Leads Google Maps và trích xuất Email với SerpApi & Airtable

Chào các sếp! Việc tìm kiếm khách hàng tiềm năng (Lead Generation) thủ công trên Google Maps tốn rất nhiều thời gian: vừa phải copy tên doanh nghiệp, địa chỉ, số điện thoại, lại vừa phải mò mẫm vào từng website để tìm địa chỉ email liên hệ. 

Chưa kể, dữ liệu thu về thường xuyên bị trùng lặp, thiếu thông tin hoặc dính nhiều email rác không hoạt động.

Giải pháp ở đây là gì? Workflow n8n siêu việt này sẽ thay các sếp làm 100% các công việc nặng nhọc đó: Tự động truy vấn từ khóa từ Airtable, quét Google Maps thông qua **SerpApi**, cào sâu vào website để bóc tách email, lọc bỏ email rác và đồng bộ toàn bộ dữ liệu sạch sẽ quay lại Airtable chỉ trong một nốt nhạc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Quét hàng trăm doanh nghiệp trên Google Maps và website của họ mà không cần click chuột thủ công.
- **Lọc email thông minh:** Hệ thống code nodes tự động cào, loại bỏ email trùng lặp và xác thực email hợp lệ.
- **Đồng bộ hóa liền mạch:** Lưu trữ toàn bộ kết quả (tên, SĐT, địa chỉ, website, email) trực tiếp vào cơ sở dữ liệu Airtable.
- **Xử lý hàng loạt mượt mà:** Sử dụng các node `Split In Batches` giúp chia nhỏ tác vụ, tránh bị quá tải API hoặc lỗi timeout.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** (Self-hosted hoặc n8n Cloud).
- **Tài khoản SerpApi:** Để gọi API tìm kiếm dữ liệu trên Google Maps (`serpApi` credentials).
- **Tài khoản Airtable:** Nơi lưu trữ từ khóa tìm kiếm đầu vào và nhận danh sách leads sạch (`airtableTokenApi` credentials).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này, dán thẳng vào giao diện n8n Editor của mình hoặc import trực tiếp file JSON từ nguồn gốc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động trơn tru, các sếp cần chú ý cấu hình các node cốt lõi sau:

- **Retrieve Searches from Airtable (Node Airtable):** 
  - Kết nối với tài khoản Airtable của các sếp.
  - Cấu hình chọn đúng **Base** và **Table** chứa danh sách từ khóa tìm kiếm (Search Queries) đầu vào.
- **Perform Google Maps Search (Node SerpApi):** 
  - Thêm thông tin xác thực `SerpApi` API Key.
  - Đảm bảo tham số truy vấn (`google_maps`) nhận đúng dữ liệu truyền từ bước Airtable qua các biến (variables).
- **Trích xuất và Xử lý Email (`Extract Emails`, `Remove Invalid Emails`, `Check for Email Presence`):**
  - Các code nodes này đã được viết sẵn logic JavaScript để bóc tách định dạng email và lọc bỏ các email không hợp lệ (như đuôi `.png`, `.jpg`,...). Các sếp có thể giữ nguyên hoặc tùy chỉnh theo ý muốn.
- **Airtable Record Sync (Node Airtable):**
  - Cấu hình operation ở chế độ **Upsert**.
  - Map chính xác các trường dữ liệu đầu ra từ n8n (Tên doanh nghiệp, Website, Email đã lọc, Số điện thoại...) khớp với các cột tương ứng trong bảng Airtable đích để tránh tạo ra bản ghi trùng lặp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử nghiệm thủ công với 1-2 từ khóa mẫu để kiểm tra dòng dữ liệu qua các bước `Wait 4 Seconds`, `Fetch Main Domain`, `Combine Email and Map Data`.
- Sau khi test thành công và dữ liệu đổ về Airtable chuẩn chỉnh, hãy bật nút **Active** để hệ thống sẵn sàng vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm một node Telegram hoặc Slack vào cuối quy trình để nhận thông báo tức thì mỗi khi quét xong một mảng leads mới.
- **Mở rộng nguồn dữ liệu:** Thay vì chỉ lấy từ khóa từ Airtable, các sếp có thể kết nối thêm Webhook từ Google Forms hoặc Typeform để khách hàng nhập ngành nghề cần quét trực tiếp.
- **Lưu log lỗi:** Sử dụng nhánh `Error Trigger` để bắt lỗi khi website của doanh nghiệp bị sập (down) hoặc API phản hồi chậm, giúp việc kiểm tra vận hành dễ dàng hơn.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ mạnh mẽ giúp các đội ngũ Sales và Marketing tối ưu hóa quy trình thu thập dữ liệu khách hàng. Hãy thiết lập ngay hôm nay để tiết kiệm hàng chục giờ làm việc thủ công và bắt đầu chiến dịch tiếp cận khách hàng chất lượng cao!