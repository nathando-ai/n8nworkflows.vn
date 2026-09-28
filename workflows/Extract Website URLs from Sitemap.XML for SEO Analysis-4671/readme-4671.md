---
title: "🚀 Trích xuất danh sách URL từ Sitemap.XML tự động phục vụ phân tích SEO với n8n"
description: "Hướng dẫn tự động hóa quy trình crawl và trích xuất toàn bộ URL từ file Sitemap.XML của website, hỗ trợ file sitemap lớn và xuất file dữ liệu dễ dàng."
slug: "trich-xuat-url-tu-sitemap-xml-cho-seo-n8n"
tags: [n8n, automation, seo, marketing, sitemap-extractor, no-code]
keywords: [n8n workflow, trích xuất sitemap xml, crawl website url, phân tích seo tự động, n8n marketing automation]
---

# 🚀 Trích xuất danh sách URL từ Sitemap.XML tự động phục vụ phân tích SEO

Các sếp làm SEO hay Digital Marketing chắc chắn đều hiểu cảm giác "đau đầu" khi phải thủ công copy từng URL từ các sitemap khổng lồ (đặc biệt là các website thương mại điện tử lớn có hàng ngàn danh mục và sản phẩm). Việc này không chỉ tốn thời gian mà còn dễ sót dữ liệu.

Workflow n8n này do tác giả **Le Thua Phu** xây dựng sẽ giải quyết triệt để bài toán trên. Giúp các sếp tự động hóa 100% quy trình tải, phân tích và trích xuất toàn bộ URL từ Sitemap.XML (bao gồm cả sitemap index chứa nhiều sub-sitemap) chỉ với một cú click chuột!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các sitemap lớn mà không lo nghẽn mạng, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 99% thời gian:** Không cần copy/paste thủ công hàng ngàn URL từ sitemap lên Excel.
- **Xử lý linh hoạt Sitemap lớn:** Tự động nhận diện sitemap index, tách và xử lý từng sub-sitemap con một cách thông minh.
- **Dữ liệu sẵn sàng sử dụng:** Xuất file kết quả trực tiếp hoặc dễ dàng tích hợp chuyển thẳng vào Google Sheets để làm báo cáo SEO.
- **Vận hành đơn giản:** Chỉ cần nhập tên miền hoặc đường dẫn sitemap, phần còn lại để n8n lo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động (Phiên bản từ v1.0 trở lên).
- Tên miền website hoặc đường dẫn trực tiếp đến file `sitemap.xml`.
- (Tùy chọn) Tài khoản Google Drive / Google Sheets nếu các sếp muốn lưu trữ dữ liệu trực lên Cloud thay vì tải file về máy.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ n8n template hoặc copy trực tiếp mã JSON.
- Mở n8n Editor của các sếp, chọn **Add workflow** -> **Import from File / Clipboard** và dán đoạn mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà theo đúng ý muốn, các sếp chú ý cấu hình các node sau:
- **Set URL (Node `set`):** Điền tên miền website của các sếp vào đây (hoặc có thể bỏ qua node này và dán trực tiếp URL sitemap vào node Crawl sitemap).
- **Crawl sitemap & Crawl sitemap 2 (Nodes `httpRequest`):** 
  - Kiểm tra lại tham số URL gọi đến `{{ $json.Domain }}sitemap.xml`. Nếu muốn crawl một sitemap bất kỳ, hãy thay thế bằng link trực tiếp (ví dụ: `https://example.com/sitemap.xml`).
  - *Lưu ý lỗi Timeout:* Nếu sitemap của website phản hồi chậm, hãy tăng giá trị timeout trong phần options của các node HTTP Request này (mặc định đang là 10 giây).
- **Convert File hoặc Google Sheets:** Workflow mặc định sử dụng node **Convert to File** để tải file kết quả về máy. Nếu các sếp muốn lưu thẳng lên Google Drive/Sheets, hãy xóa node này và thay bằng node **Google Sheets**, sau đó map trường `loc` từ node **Split Out 2** vào cột tương ứng trong bảng tính.

#### 3. Kích hoạt ⚡️
- Nhấn nút **‘Test workflow’** tại node **When clicking ‘Test workflow’** để chạy thử nghiệm dữ liệu mẫu.
- Kiểm tra kết quả trả về ở các node XML và Split Out.
- Bật công tắc **Active** để sẵn sàng sử dụng bất cứ lúc nào.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Google Sheets tự động:** Thay vì tải file, kết nối thẳng với Google Sheets để tạo bảng theo dõi danh sách URL định kỳ hàng tuần.
- **Kết hợp Webhook/Telegram:** Thêm node Telegram để nhận thông báo ngay khi quá trình crawl sitemap hoàn tất kèm theo số lượng URL thu thập được.
- **Tối ưu tài nguyên:** Với các website lớn có hàng trăm nghìn URL, hãy đảm bảo VPS của các sếp có đủ RAM và CPU để tránh gặp lỗi tràn bộ nhớ (Out of Memory).

### 📌 Kết luận
Workflow "Extract Website URLs from Sitemap.XML for SEO Analysis" là một công cụ cực kỳ hữu ích giúp các anh em làm SEO tiết kiệm thời gian tối đa trong việc audit website hoặc thu thập cấu trúc site. Hãy import ngay vào n8n của các sếp và tối ưu hóa quy trình làm việc ngay hôm nay!