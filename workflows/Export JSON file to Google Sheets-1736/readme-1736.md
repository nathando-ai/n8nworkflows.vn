---
title: "🚀 Tự động hóa xuất dữ liệu từ File JSON lên Google Sheets trong n8n"
description: "Hướng dẫn chi tiết cách sử dụng n8n workflow để đọc file JSON cục bộ, chuyển đổi dữ liệu nhị phân và tự động append vào Google Sheets một cách nhanh chóng."
slug: "export-json-file-to-google-sheets"
tags: [n8n, automation, no-code, google-sheets, json-parser, file-management]
keywords: [n8n workflow, export json to google sheets, doc file json len google sheets, tu dong hoa n8n, read binary file n8n]
---

# 🚀 Tự động hóa xuất dữ liệu từ File JSON lên Google Sheets trong n8n

Các sếp có bao giờ gặp cảnh phải xử lý hàng đống file JSON chứa dữ liệu khách hàng, đơn hàng hay log hệ thống, sau đó lọ mọ copy-paste thủ công lên Google Sheets chưa? Công việc nhàm chán này không chỉ ngốn hàng giờ đồng hồ mà còn rất dễ xảy ra sai sót. 

Giải pháp hoàn hảo cho các sếp đây: Workflow n8n tự động hóa 100% quy trình đọc file JSON cục bộ, xử lý cấu trúc dữ liệu nhị phân và đẩy thẳng lên Google Sheets chỉ trong một nốt nhạc! Không cần biết code phức tạp, các sếp chỉ cần import và cấu hình nhẹ là chạy mượt mà.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Tạm biệt thao tác thủ công, chuyển đổi file JSON sang bảng tính tự động.
- **Độ chính xác tuyệt đối:** Dữ liệu được map chuẩn xác từng trường (field) từ JSON sang cột tương ứng trên Google Sheets.
- **Xử lý linh hoạt:** Dễ dàng áp dụng cho các file JSON từ nhiều nguồn khác nhau xuất ra (API, hệ thống cũ, web scraper...).
- **Vận hành tự động 24/7:** Có thể kết hợp thêm các trigger thời gian hoặc webhook để chạy định kỳ mỗi khi có file mới.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Hệ thống n8n:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Google:** Cần có Google Account để kết nối Google Sheets thông qua OAuth2.
- **File JSON mẫu:** Chuẩn bị sẵn một file JSON có cấu trúc rõ ràng lưu trên thư mục của server/máy tính chạy n8n để workflow có thể đọc.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy đoạn mã JSON của workflow hoặc tải file JSON gốc từ tác giả Lorena (`https://n8n.io/workflows/1736`), sau đó dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 3 nodes cơ bản hoạt động tuần tự. Các sếp cần chú ý cấu hình từng node như sau:

- **Node `read json file` (Read Binary File):**
  - Node này chịu trách nhiệm đọc file JSON từ đường dẫn trên server.
  - Các sếp cần điền chính xác đường dẫn tuyệt đối tới file JSON (ví dụ: `/data/input.json`) vào mục **File Path**.

- **Node `move binary data 2` (Move Binary Data):**
  - Node này giúp chuyển đổi định dạng dữ liệu nhị phân từ file vừa đọc thành dữ liệu JSON mà các node phía sau có thể hiểu và bóc tách được.
  - Thông thường các sếp có thể giữ nguyên cấu hình mặc định của node này.

- **Node `Google Sheets1` (Google Sheets):**
  - **Credentials:** Chọn kết nối Google Sheets OAuth2 API của các sếp.
  - **Operation:** Đặt là `Append` (Thêm hàng mới).
  - **Document & Sheet:** Chọn đúng file Google Sheets và tên Sheet (Tab) mà các sếp muốn đẩy dữ liệu vào.
  - **Mapping:** Map các trường dữ liệu từ file JSON vào đúng các cột tương ứng trên Google Sheets.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** từng node để kiểm tra xem file JSON đã được đọc và đẩy lên Google Sheets thành công chưa.
- Sau khi test ngon lành, các sếp bật công tắc **Active** góc trên bên phải để workflow sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình này hơn nữa, các sếp có thể mở rộng workflow với các ý tưởng sau:
- **Nhận thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để gửi thông báo "Đã đẩy thành công X bản ghi từ file JSON lên Google Sheets!" cho team.
- **Tự động xóa file cũ:** Kết hợp thêm node thực thi lệnh hệ thống (Execute Command) để xóa hoặc di chuyển file JSON vào thư mục `archive` sau khi đã xử lý xong, tránh việc đọc nhầm file cũ ở lần chạy sau.
- **Đặt lịch chạy tự động (Cron/Schedule Trigger):** Thay vì chạy thủ công, hãy gắn thêm node *Schedule Trigger* để tự động quét thư mục và đồng bộ file JSON vào Google Sheets mỗi ngày/mỗi giờ.

### 📌 Kết luận
Việc quản lý và đồng bộ dữ liệu từ file JSON lên Google Sheets chưa bao giờ dễ dàng đến thế với workflow n8n này. Hãy cài đặt ngay hôm nay để tối ưu hóa thời gian vận hành cho doanh nghiệp của các sếp! Chúc các sếp thao tác thành công!