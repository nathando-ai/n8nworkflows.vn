---
title: "🚀 Tự động Giám sát Bất động sản Realtor, Xuất file CSV/XLSX và Gửi Email với MrScraper & Gmail"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu nhà đất từ Realtor, chuyển đổi định dạng CSV/XLSX và gửi báo cáo qua Gmail một cách nhanh chóng."
slug: "tu-dong-giam-sat-bat-dong-san-realtor-mrscraper-gmail"
tags: [n8n, automation, no-code, scraping, real-estate, mrscraper, gmail]
keywords: [n8n workflow, tự động hóa realtor, cào dữ liệu bất động sản, mrscraper, n8n gmail, xuat file csv xlsx]
---

# 🚀 Tự động Giám sát Bất động sản Realtor, Xuất file CSV/XLSX và Gửi Email

Việc theo dõi thị trường bất động sản thủ công trên Realtor.com để tìm kiếm cơ hội đầu tư hoặc phân tích giá cả tốn rất nhiều thời gian và công sức. Các nhà môi giới và nhà đầu tư thường xuyên phải copy-paste dữ liệu, làm sạch và gửi báo cáo cho đội ngũ. 

Workflow n8n này sinh ra để giải quyết triệt để nỗi đau đó! Bằng cách kết hợp **MrScraper** để cào dữ liệu tự động, các node xử lý dữ liệu của **n8n**, và **Gmail** để gửi báo cáo, các sếp sẽ có ngay một hệ thống tự động hóa 100% không cần code, giúp tiết kiệm hàng chục giờ làm việc mỗi tuần.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Lịch trình chạy tự động (Schedule Trigger) hoặc kích hoạt thủ công (Manual Trigger) giúp lấy dữ liệu mới nhất từ Realtor mà không cần đụng tay.
- **Dữ liệu chuẩn hóa:** Tự động tổng hợp và chuyển đổi dữ liệu thành các định dạng quen thuộc như CSV hoặc XLSX (Excel) sẵn sàng để phân tích.
- **Báo cáo tức thì:** Gửi trực tiếp file dữ liệu qua Gmail đến cá nhân hoặc đội ngũ ngay sau khi quá trình cào hoàn tất.
- **Hoạt động không nghỉ:** Hệ thống tự động phân chia lô xử lý (Split in Batches) giúp xử lý lượng dữ liệu lớn mà không lo bị quá tải hay lỗi API.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị sẵn các tài khoản và thông tin sau:
- **Tài khoản n8n:** Đã cài đặt sẵn (Self-hosted hoặc Cloud).
- **Tài khoản MrScraper:** Để thiết lập scraper cào dữ liệu từ Realtor (cần có API Key/Credentials).
- **Tài khoản Google (Gmail & Google Drive):** Để cấu hình gửi email báo cáo và lưu trữ file tạm nếu cần.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dán trực tiếp bằng phím tắt `Ctrl+V` / `Cmd+V`).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Khi import xong, các sếp cần cấu hình các node cốt lõi sau để workflow chạy mượt mà:
- **Schedule Trigger / Manual Trigger:** Thiết lập lịch chạy tự động theo ngày/tuần tùy nhu cầu theo dõi thị trường của các sếp, hoặc dùng Trigger thủ công để test.
- **MrScraper Node (`n8n-nodes-mrscraper.mrscraper`):** Kết nối tài khoản MrScraper của sếp, cấu hình đường dẫn URL Realtor cần cào dữ liệu và các trường thông tin cần lấy.
- **Split in Batches:** Kiểm tra lại số lượng bản ghi chia lô cho phù hợp nếu lượng dữ liệu từ Realtor trả về quá lớn.
- **Convert to File (`n8n-nodes-base.convertToFile`):** Cấu hình định dạng file đầu ra mong muốn (CSV hoặc XLSX) để phù hợp với nhu cầu đọc dữ liệu của đội ngũ.
- **Gmail Node (`n8n-nodes-base.gmail`):** Kết nối tài khoản Gmail cá nhân hoặc doanh nghiệp, thiết lập người nhận (To), tiêu đề và nội dung email kèm file đính kèm vừa được chuyển đổi.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm (Test run) với dữ liệu mẫu xem hệ thống có cào và gửi mail thành công hay không.
- Sau khi kiểm tra mọi thứ hoạt động trơn tru, gạt công tắc sang **Active** để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình kinh doanh bất động sản, các sếp có thể mở rộng workflow này bằng các cách sau:
- **Tích hợp Chatbot:** Thêm node Telegram hoặc Slack để bắn thông báo nhanh (ví dụ: *"Đã cào xong 50 căn nhà mới trên Realtor, đã gửi file qua Gmail"*).
- **Lưu trữ đám mây:** Kết hợp thêm node **Google Drive** để lưu trữ tự động các file CSV/XLSX vào một thư mục riêng biệt phục vụ việc lưu trữ lịch sử dữ liệu.
- **Lọc thông minh:** Thêm node **Code** hoặc **If** để lọc ra các bất động sản có mức giá hoặc diện tích phù hợp với tiêu chí đầu tư trước khi xuất file gửi báo cáo.

### 📌 Kết luận
Với workflow **Monitor Realtor listings and export CSV-XLSX with MrScraper and Gmail**, các sếp đã sở hữu ngay một trợ lý ảo đắc lực trong việc nghiên cứu thị trường bất động sản. Hãy thiết lập ngay hôm nay để tối ưu hóa thời gian và không bỏ lỡ bất kỳ cơ hội đầu tư nào!