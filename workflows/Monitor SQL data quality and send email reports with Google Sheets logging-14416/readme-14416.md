---
title: "🚀 Tự động giám sát chất lượng dữ liệu SQL và gửi báo cáo qua Email với n8n"
description: "Hướng dẫn thiết lập workflow n8n tự động kiểm tra lỗi dữ liệu PostgreSQL (Null, trùng lặp, outlier, row count), đánh giá trạng thái và gửi báo cáo HTML qua Gmail kèm lưu log Google Sheets."
slug: "tu-dong-giam-sat-chat-luong-du-lieu-sql-n8n"
tags: [n8n, automation, postgresql, data-quality, google-sheets, gmail]
keywords: [n8n workflow, giám sát chất lượng dữ liệu, kiểm tra dữ liệu postgresql, tự động gửi báo cáo email, data quality monitor n8n]
---

# 🚀 Tự động giám sát chất lượng dữ liệu SQL và gửi báo cáo qua Email với n8n

Các sếp có bao giờ đau đầu khi dữ liệu trong database bị lỗi (null quá nhiều, trùng lặp bản ghi, biến động số lượng dòng bất thường hay dữ liệu ngoại lai - outlier) mà chỉ phát hiện ra khi hệ thống báo lỗi hoặc khách hàng phàn nàn? Việc kiểm tra thủ công mỗi ngày là bất khả thi và tốn rất nhiều thời gian.

Giải pháp ở đây là gì? Workflow n8n tự động hóa 100% này sẽ thay các sếp "gác cửa" cơ sở dữ liệu định kỳ, tự động chạy 4 bài kiểm tra quan trọng, đánh giá sức khỏe dữ liệu (`PASS` / `WARN` / `FAIL`), gửi báo cáo HTML chi tiết qua Gmail và lưu vết toàn bộ lịch sử vào Google Sheets để tiện kiểm toán.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phát hiện lỗi sớm:** Tự động quét lỗi dữ liệu (Null, Duplicate, Row Count, Outlier) theo lịch trình (mặc định 8h sáng hàng ngày).
- **Báo cáo chuyên nghiệp:** Nhận báo cáo định dạng HTML trực quan, đầy đủ chỉ số trực tiếp qua Gmail.
- **Lưu trữ minh bạch:** Tự động ghi log chi tiết lịch sử kiểm tra vào Google Sheets để dễ dàng theo dõi xu hướng chất lượng dữ liệu.
- **Hoạt động tự động 24/7:** Không cần con người can thiệp, tiết kiệm hàng giờ kiểm tra thủ công mỗi tuần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **PostgreSQL Database:** Tài khoản kết nối cơ sở dữ liệu cần giám sát.
- **Google Account:** Tài khoản Google để kết nối Google Sheets (`googleSheetsOAuth2Api`).
- **Gmail Account:** Tài khoản Gmail hoặc dịch vụ SMTP để gửi email báo cáo (`gmailOAuth2`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào n8n Editor của mình, hoặc import file JSON tải từ nguồn chính thức.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 10 nodes chính, các sếp cần cấu hình kỹ các điểm sau:

- **Node `Schedule Trigger`**: Mặc định chạy định kỳ mỗi ngày lúc 8:00 sáng. Các sếp có thể điều chỉnh lại lịch chạy cho phù hợp với nhu cầu.
- **Node `Config` (Set)**: Điền chính xác tên bảng dữ liệu (`table name`), tên các cột cần kiểm tra (`columns`), các mức ngưỡng (`thresholds`) và danh sách email nhận báo cáo (`Email Distribution list`). *Lưu ý: Tên cột phải khớp chính xác 100% với schema trong database.*
- **4 Nodes kiểm tra cơ sở dữ liệu (`Null Check`, `Duplicate Check`, `Row Count`, `Outlier Check`)**: 
  - Kiểu node: `Postgres`.
  - Kết nối tài khoản `postgres` credential của các sếp.
  - *Mẹo:* Nếu dùng MySQL hoặc DB khác, các sếp chỉ cần đổi loại node tương ứng.
- **Node `Evaluate & Format` (Code)**: Node này sẽ nhận kết quả song song từ 4 câu lệnh SQL, chạy logic so sánh ngưỡng để gán nhãn `PASS`, `WARN`, `FAIL` và dựng sẵn template báo cáo HTML.
- **Node `Log to Google Sheets`**: 
  - Kết nối tài khoản Google Sheets.
  - Chuẩn bị sẵn một Google Sheet với các cột tiêu đề: `Timestamp`, `Table`, `Null_Pct`, `Dup_Pct`, `Row_Count`, `Outlier_Pct`, `Status`.
- **Node `Send a message` (Gmail)**: Kết nối tài khoản Gmail cá nhân hoặc doanh nghiệp để gửi email báo cáo dựa trên nội dung HTML được tạo từ code node trước đó.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** để chạy thử nghiệm xem dữ liệu có đổ về Google Sheets và email có được gửi đi thành công hay không.
- Nếu mọi thứ mượt mà, gạt công tắc **Active** để workflow chính thức tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Có thể kết nối thêm node Slack hoặc Telegram để bắn tin nhắn cảnh báo ngay lập tức vào group team kỹ thuật khi trạng thái trả về `FAIL`.
- **Lưu trữ dài hạn:** Kết hợp thêm các biểu đồ (Charts) trực tiếp trên Google Sheets dựa trên log dữ liệu để theo dõi xu hướng cải thiện chất lượng dữ liệu theo tuần/tháng.
- **Tùy chỉnh ngưỡng:** Tăng hoặc giảm ngưỡng threshold trong node `Config` để kiểm soát độ khắt khe của việc kiểm tra dữ liệu.

### 📌 Kết luận
Việc kiểm soát chất lượng dữ liệu chưa bao giờ dễ dàng đến thế với sự trợ giúp của n8n. Hãy thiết lập ngay workflow này để bảo vệ nguồn dữ liệu cốt lõi của doanh nghiệp các sếp nhé!