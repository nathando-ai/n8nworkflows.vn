---
title: "🚀 Tự động lấy dữ liệu thời tiết hàng ngày và lưu trữ vào Airtable với n8n"
description: "Hướng dẫn thiết lập workflow n8n tự động gọi API thời tiết mỗi ngày và lưu trữ thông tin chi tiết vào Airtable để xây dựng cơ sở dữ liệu lịch sử thời tiết."
slug: "tu-dong-lay-du-lieu-thoi-tiet-hang-ngay-va-luu-vao-airtable"
tags: [n8n, automation, no-code, weather-api, airtable, schedule-trigger]
keywords: [n8n workflow, tự động hóa thời tiết, lưu weather data vào airtable, openweathermap n8n, schedule trigger n8n]
---

# 🚀 Tự động lấy dữ liệu thời tiết hàng ngày và lưu trữ vào Airtable

Các sếp có đang tốn thời gian theo dõi, cập nhật thông tin thời tiết thủ công mỗi ngày cho các ứng dụng, báo cáo nội bộ hay dự án cá nhân không? Việc quên cập nhật hoặc thiếu dữ liệu lịch sử (historical data) thường xuyên gây gián đoạn công việc. 

Giải pháp ở đây chính là workflow n8n **"Get Daily Weather and Save It in Airtable"** – một trợ thủ tự động hóa 100% giúp các sếp lấy thông tin thời tiết chính xác qua API và lưu trữ ngăn nắp vào Airtable mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chạy ngầm mỗi ngày theo lịch trình cố định (Schedule Trigger) mà không cần can thiệp thủ công.
- **Lưu trữ khoa học:** Dữ liệu nhiệt độ, độ ẩm, sức gió... được đồng bộ trực tiếp vào bảng Airtable, tạo kho lưu trữ lịch sử thời tiết chuẩn chỉnh.
- **Tiết kiệm thời gian:** Loại bỏ hoàn toàn các thao tác copy-paste số liệu thời tiết thủ công mỗi sáng.
- **Hoạt động bền bỉ:** Hệ thống tự động ghi nhận và sẵn sàng phục vụ cho các phân tích sâu hơn về sau.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
- **Hệ thống n8n:** Đã cài đặt và sẵn sàng sử dụng (Self-hosted hoặc Cloud).
- **Tài khoản Weather API:** Tài khoản từ các nhà cung cấp dịch vụ thời tiết (ví dụ: OpenWeatherMap) để lấy API Key.
- **Tài khoản Airtable:** Tạo sẵn một Base và một Table với các trường tương ứng (Temperature, Humidity, Wind Speed, Date...) và chuẩn bị **Airtable Personal Access Token**.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc sao chép mã nguồn JSON.
- Mở giao diện n8n Editor, nhấn vào biểu tượng **Menu (dấu ba chấm)** ở góc trên bên phải > Chọn **Import from File** hoặc **Import from Clipboard** và dán đoạn mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 3 node chính, các sếp cần cấu hình chuẩn xác các điểm sau:

- **Schedule Trigger (Node kích hoạt lịch trình):**
  - Cấu hình tần suất chạy (ví dụ: Chạy lúc 8:00 sáng mỗi ngày).
- **Get Weather Data (Node HTTP Request):**
  - Điền Endpoint API của nhà cung cấp thời tiết (OpenWeatherMap API hoặc dịch vụ tương đương).
  - Cung cấp thông tin xác thực (`credentials`) như API Key hoặc Header phù hợp mà dịch vụ thời tiết yêu cầu.
- **Store Weather Data (Node Airtable):**
  - Chọn **Credentials**: Kết nối tài khoản Airtable của các sếp bằng **Airtable Token API**.
  - Chọn **Operation**: Đặt là `create` (Tạo mới bản ghi).
  - Chọn đúng **Base** và **Table** đã chuẩn bị sẵn, sau đó map (ánh xạ) các trường dữ liệu trả về từ node thời tiết vào đúng các cột trong Airtable (Nhiệt độ, Độ ẩm, Thời gian...).

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để test thủ công lần đầu, kiểm tra xem dữ liệu có đẩy thành công vào Airtable hay không.
- Nếu mọi thứ xanh mướt, hãy gạt công tắc sang chế độ **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
Để workflow trở nên "lợi hại" hơn, các sếp có thể mở rộng thêm:
- **Bắn thông báo Telegram/Slack:** Thêm một node Telegram hoặc Slack ngay sau Airtable để gửi bản tin thời tiết tóm tắt vào nhóm chat công ty mỗi sáng.
- **Cảnh báo thời tiết cực đoan:** Thêm node `If` để kiểm tra điều kiện (ví dụ: Nhiệt độ > 35°C hoặc có mưa lớn) thì kích hoạt cảnh báo khẩn cấp.
- **Ghi log lỗi:** Kết nối đường nhánh lỗi (Error Trigger) để nếu API thời tiết sập hoặc Airtable quá hạn mức, hệ thống sẽ gửi email báo động cho các sếp.

### 📌 Kết luận
Chỉ với vài bước cấu hình đơn giản trên n8n, các sếp đã có ngay một hệ thống tự động thu thập và lưu trữ dữ liệu thời tiết cực kỳ chuyên nghiệp. Bắt tay vào cài đặt ngay để tối ưu hóa quy trình làm việc của mình nhé!