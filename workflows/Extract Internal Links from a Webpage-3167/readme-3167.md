---
title: "🚀 Tự động trích xuất liên kết nội bộ từ website với n8n Workflow"
description: "Hướng dẫn chi tiết cách sử dụng n8n workflow để cào và lọc toàn bộ internal links (liên kết nội bộ) từ một trang web bất kỳ một cách tự động và chính xác."
slug: "trich-xuat-lien-ket-noi-bo-tu-website-n8n"
tags: [n8n, automation, web-scraping, seo, marketing, engineering]
keywords: [n8n workflow, trích xuất internal links, cào link website, tự động hóa seo, n8n html node]
---

# 🚀 Tự động trích xuất liên kết nội bộ từ website với n8n Workflow

Các sếp làm SEO, content marketing hay lập trình viên chắc đã từng đau đầu khi cần crawl (cào) toàn bộ các liên kết nội bộ (internal links) từ một bài viết hoặc trang web để phục vụ cho việc tối ưu cấu trúc website, audit link hoặc phân tích nội dung. Nếu làm thủ công bằng tay hoặc dùng các công cụ trả phí phức tạp thì vừa tốn thời gian, vừa bất tiện.

Giải pháp ở đây là gì? Workflow n8n **"Extract Internal Links from a Webpage"** do tác giả *Audun* thiết kế sẽ giúp các sếp tự động hóa 100% quy trình này: chỉ cần nhập URL, hệ thống sẽ tự động tải trang, bóc tách toàn bộ thẻ `<a>`, lọc bỏ các liên kết ngoại vi (external links) và trả về danh sách các liên kết nội bộ sạch sẽ, chuẩn xác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chỉ mất vài giây để lấy danh sách hàng trăm liên kết trên một trang web mà không cần thao tác thủ công.
- **Lọc thông minh:** Tự động nhận diện và phân loại liên kết tuyệt đối/tương đối, chỉ giữ lại các liên kết nội bộ (internal links) đúng yêu cầu SEO.
- **Linh hoạt tích hợp:** Dễ dàng kết nối tiếp với Google Sheets, Airtable hoặc gửi báo cáo qua Telegram/Slack.
- **Tiết kiệm chi phí:** Không cần mua các, phần mềm crawl dữ liệu đắt đỏ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động (Cloud hoặc Self-hosted).
- URL của trang web cần trích xuất liên kết.
- Không cần tài khoản API phức tạp vì workflow sử dụng HTTP Request và HTML Node cơ bản.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON từ trang nguồn n8n, sau đó vào giao diện n8n của mình, chọn **Add workflow** -> **Import from File** (hoặc copy toàn bộ JSON và dán trực tiếp vào n8n Editor).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 9 nodes được sắp xếp logic từ khâu nhận diện URL, cào dữ liệu đến xử lý logic. Các sếp cần chú ý các node sau:

- **When clicking ‘Test workflow’ (`manualTrigger`):** Điểm khởi đầu để chạy thử thủ công. Các sếp có thể đổi sang *Webhook* hoặc *Schedule* nếu muốn tự động hóa định kỳ.
- **Set Base URL (`set`):** Nơi các sếp khai báo URL gốc của trang web cần phân tích và domain chính để dùng làm mốc so sánh liên kết nội bộ.
- **Fetch base URL (`httpRequest`):** Node thực hiện gọi API dạng GET để tải mã nguồn HTML của trang web mục tiêu.
- **Extract links (`html`):** Node bóc tách dữ liệu sử dụng CSS Selector để quét toàn bộ các thẻ `<a>` và lấy thuộc tính `href`.
- **Split Out (`splitOut`):** Tách mảng các link thô thành các items riêng biệt để dễ dàng xử lý ở các bước sau.
- **Find relative links (`if`) & Append base URL (`set`):** Xử lý thông minh các đường dẫn dạng tương đối (relative path như `/about-us`) và tự động gắn thêm domain gốc vào để biến chúng thành đường dẫn tuyệt đối đầy đủ.
- **Filter external links (`filter`):** Bộ lọc cốt lõi giúp loại bỏ các link trỏ ra ngoài tên miền chính (external links), chỉ giữ lại các internal links thuần túy.
- **Merge (`merge`):** Đồng bộ hóa lại dữ liệu sau khi đã xử lý xong các luồng rẽ nhánh.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** để chạy thử với URL mẫu và kiểm tra kết quả trả về ở node cuối cùng.
- Nếu dữ liệu trả về chính xác các internal links, các sếp chỉ cần gạt công tắc sang **Active** để đưa workflow vào trạng thái hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
Để workflow này trở thành một "trợ lý SEO" đắc lực thực thụ, các sếp có thể mở rộng thêm:
- **Đẩy dữ liệu vào Google Sheets / Airtable:** Thêm một node Google Sheets ở cuối để tự động lưu danh sách link vào bảng tính phục vụ việc audit website.
- **Kết hợp Slack / Telegram:** Gửi thông báo kèm file hoặc danh sách link trực tiếp về nhóm chat khi quá trình trích xuất hoàn tất.
- **Kiểm tra trạng thái HTTP (Link Checker):** Gắn thêm một node HTTP Request kiểm tra xem các internal link đó có bị lỗi 404 hay không.

### 📌 Kết luận
Workflow **Extract Internal Links from a Webpage** là một công cụ cực kỳ hữu ích, gọn nhẹ và dễ tùy biến cho bất kỳ ai làm trong lĩnh vực tối ưu hóa website hoặc phát triển web. Hãy cài đặt ngay lên hệ thống n8n của các sếp để tối ưu hóa thời gian làm việc ngay hôm nay!