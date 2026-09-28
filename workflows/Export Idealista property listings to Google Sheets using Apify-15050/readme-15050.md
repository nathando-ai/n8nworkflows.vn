---
title: "🚀 Tự động trích xuất danh sách bất động sản Idealista vào Google Sheets với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu nhà đất từ Idealista sử dụng Apify và đồng bộ trực tiếp vào Google Sheets không cần code."
slug: "export-idealista-property-listings-to-google-sheets-n8n"
tags: [n8n, automation, real-estate, google-sheets, apify, web-scraping]
keywords: [n8n workflow, idealista scraper, export idealista to google sheets, tự động hóa bất động sản, apify n8n]
---

# 🚀 Tự động trích xuất danh sách bất động sản Idealista vào Google Sheets

Các sếp làm trong lĩnh vực bất động sản hoặc nghiên cứu thị trường chắc chắn đã từng "nản lòng" khi phải copy-paste thủ công hàng trăm, hàng nghìn tin đăng từ Idealista vào file Excel để phân tích giá cả, vị trí hay diện tích. Việc này không chỉ tốn hàng giờ đồng hồ mà dữ liệu còn dễ bị sai sót, lỗi thời.

Đừng lo! Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ gọn nhẹ nhưng mạnh mẽ, giúp tự động cào toàn bộ dữ liệu bất động sản từ Idealista và lưu trữ thẳng vào Google Sheets một cách mượt mà.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn phải thủ công thu thập dữ liệu tin đăng nhà đất.
- **Dữ liệu chuẩn hóa:** Tự động lọc và định dạng các trường dữ liệu (giá, diện tích, vị trí, liên hệ...) vào các cột Google Sheets ngăn nắp.
- **Sẵn sàng phân tích:** Dữ liệu nằm ngay trên Google Sheets giúp các sếp dễ dàng vẽ biểu đồ, chạy báo cáo hoặc chia sẻ cho team sales.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Tài khoản Apify:** Cần có tài khoản và API Token để kết nối với node Idealista Scraper.
- **Tài khoản Google:** Để tạo Google Sheets credentials và lưu trữ dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ JSON của workflow từ nguồn cung cấp và paste trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 4 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Run Manually (`manualTrigger`):** Node kích hoạt thủ công, dùng để test workflow ngay lập tức.
- **Fetch Idealista Listings (`n8n-nodes-idealista-scraper.idealistaScraper`):** 
  - Cần kết nối tài khoản Apify của các sếp.
  - Cấu hình thông số tìm kiếm (Operation: `sale`), URL danh sách bất động sản cần cào, bộ lọc giá hoặc khu vực theo nhu cầu thực tế.
- **Prepare Property Data (`code`):** 
  - Node này dùng ngôn ngữ JavaScript để làm sạch dữ liệu thô từ scraper.
  - Các sếp cần kiểm tra lại logic trong đoạn code để đảm bảo tên các cột trả về khớp hoàn toàn với cấu trúc bảng Google Sheets phía sau.
- **Append Properties in Sheets (`googleSheets`):** 
  - Kết nối tài khoản Google Sheets của các sếp.
  - Chọn đúng file Spreadsheet và Worksheet (Tab) đích để lưu trữ danh sách bất động sản.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để test chạy thử với dữ liệu mẫu từ Idealista.
- Kiểm tra lại Google Sheets xem dữ liệu đã đổ về các cột chính xác chưa.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để chính thức vận hành hệ thống tự động hóa.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống xịn xò hơn nữa, các sếp có thể mở rộng workflow với các ý tưởng sau:
- **Gửi thông báo:** Thêm node Telegram hoặc Slack để bắn thông báo ngay về máy mỗi khi cào xong một mẻ dữ liệu bất động sản mới.
- **Chạy định kỳ:** Thay thế node `Run Manually` bằng `Schedule Trigger` để n8n tự động cào dữ liệu mỗi ngày/mỗi tuần mà không cần động tay.
- **Lọc trùng lặp:** Thêm một bước kiểm tra ID bất động sản trong Google Sheets trước khi ghi mới để tránh bị trùng lặp tin đăng.

### 📌 Kết luận
Chỉ với 4 nodes cơ bản trong n8n, các sếp đã sở hữu ngay một "con bot" nghiên cứu thị trường bất động sản tự động 100%. Áp dụng ngay để tối ưu hóa công việc kinh doanh và phân tích dữ liệu của mình nào!