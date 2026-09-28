---
title: "🚀 Tự động trích xuất email từ mã nguồn HTML website bằng n8n"
description: "Hướng dẫn xây dựng API cào và trích xuất địa chỉ email từ website tự động 100% bằng n8n, giúp đội ngũ Sales và Marketing tối ưu quy trình tìm kiếm khách hàng tiềm năng."
slug: "trich-xuat-email-tu-website-html-bang-n8n"
tags: [n8n, automation, no-code, email-scraping, sales-automation, marketing]
keywords: [n8n workflow, cào email website, trích xuất email tự động, extract emails html, sales automation n8n]
---

# 🚀 Tự động trích xuất email từ website cực nhanh với n8n

Các sếp trong ngành Sales và Marketing chắc chắn đã từng tốn hàng giờ đồng hồ lướt từng trang web thủ công chỉ để tìm một địa chỉ email liên hệ của đối tác hoặc khách hàng tiềm năng. Việc này vừa nhàm chán, vừa tốn thời gian mà năng suất lại không cao.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow **"Extract emails from website HTMLs"** do chuyên gia **Imperol** thiết kế. Workflow này giúp các sếp tự động hóa 100% quy trình gọi API, tải mã nguồn HTML của trang web, bóc tách và lọc ra toàn bộ địa chỉ email sạch sẽ mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Biến n8n thành một Email Scraping API cá nhân chỉ trong tích tắc.
- **Tiết kiệm 90% thời gian**: Không còn phải thủ công "soi" trang Liên hệ (Contact Us) của từng website.
- **Loại bỏ trùng lặp**: Tự động lọc và trả về danh sách email độc nhất, không bị lặp lại.
- **Linh hoạt tích hợp**: Dễ dàng gọi API từ bất kỳ hệ thống CRM, Google Sheets hoặc trình duyệt nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động (Cloud hoặc Self-hosted).
- Không cần tài khoản dịch vụ trả phí bên thứ ba nào vì workflow sử dụng HTTP Request trực tiếp tới HTML website.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy toàn bộ mã JSON của workflow này và dán trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 7 nodes chính phối hợp nhịp nhàng với nhau:
- **Webhook**: Đóng vai trò là điểm tiếp nhận yêu cầu (API Endpoint). URL sẽ có dạng: `http://<domain-n8n>/webhook/ea568868-5770-4b2a-8893-700b344c995e`.
- **Get the website data (HTTP Request)**: Nhận query parameter từ Webhook (tham số `Website`) để tải mã nguồn HTML của trang web mục tiêu.
  👉 *Lưu ý quan trọng:* Khi truyền tham số URL trên trình duyệt, các sếp nhớ dùng tiền tố `http://` hoặc `https://` (ví dụ: `?Website=https://mailsafi.com`) để tránh lỗi phát sinh.
- **Extract the emails found (Set)**: Sử dụng biểu thức chính quy (Regex) để quét và bóc tách các định dạng email xuất hiện trong đoạn HTML vừa tải về.
- **Split Out & Remove Duplicates**: Tách các kết quả tìm được thành từng dòng riêng biệt và tự động lọc bỏ các email bị trùng lặp.
- **If contains email & Respond to Webhook**: Kiểm tra xem trang web có chứa email hay không. Nếu có, trả về danh sách email; nếu không, trả về thông báo workflow thực thi thành công.

#### 3. Kích hoạt ⚡️
- Thử nghiệm gọi Webhook trên trình duyệt với cú pháp: 
  `http://<n8n-host>/webhook/ea568868-5770-4b2a-8893-700b344c995e?Website=https://mailsafi.com`
- Kiểm tra kết quả trả về trên màn hình thực thi của n8n.
- Bật công tắc **Active** để đưa workflow vào trạng thái sẵn sàng hoạt động chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Google Sheets / Airtable**: Mở rộng workflow bằng cách tự động lưu danh sách email trích xuất được vào file quản lý khách hàng.
- **Tích hợp Telegram/Slack**: Gửi thông báo trực tiếp về nhóm chat mỗi khi quét xong một danh sách website lớn.
- **Xử lý hàng loạt (Batch Processing)**: Kết hợp node n8n để đọc danh sách hàng trăm website từ Google Sheets và gọi API này tự động theo dạng vòng lặp (Loop).

### 📌 Kết luận
Workflow "Extract emails from website HTMLs" là một công cụ cực kỳ mạnh mẽ và tiết kiệm chi phí giúp các sếp tự động hóa khâu thu thập dữ liệu khách hàng. Hãy "lên đồ" ngay hôm nay để tối ưu hóa hiệu suất làm việc cho đội ngũ Sales và Marketing của mình nhé!