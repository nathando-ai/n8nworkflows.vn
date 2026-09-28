---
title: "💰 Tự động cập nhật tỷ giá tiền tệ trong hóa đơn bằng Google Sheet và API ExchangeRate"
description: "Hướng dẫn tự động hóa cập nhật tỷ giá tiền tệ trong hóa đơn hàng ngày bằng n8n, Google Sheets và API ExchangeRate. Tiết kiệm thời gian và đảm bảo dữ liệu luôn được cập nhật chính xác."
slug: "tu-dong-cap-nhat-ty-gia-tien-te-hoa-don-google-sheet"
tags: [n8n, automation, no-code, google-sheets, exchange-rate]
keywords: [n8n workflow, tự động hóa hóa đơn, tỷ giá tiền tệ, google sheets, exchange rate api]
---

# 💰 Tự động cập nhật tỷ giá tiền tệ trong hóa đơn bằng Google Sheet và API ExchangeRate

[Các sếp đang gặp khó khăn khi phải cập nhật tỷ giá tiền tệ trong hóa đơn hàng ngày một cách thủ công. Việc này tốn thời gian, dễ xảy ra lỗi và không đảm bảo tính chính xác. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này chỉ trong vài bước đơn giản.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động cập nhật tỷ giá tiền tệ hàng ngày mà không cần can thiệp thủ công.
- **Đảm bảo tính chính xác**: Dữ liệu tỷ giá luôn được cập nhật từ nguồn đáng tin cậy.
- **Hoạt động liên tục**: Workflow chạy tự động vào lúc 8:00 sáng hàng ngày.
- **Lưu trữ dữ liệu**: Ghi lại lịch sử tỷ giá để theo dõi và phân tích.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets.
- API Key từ [ExchangeRate-API](https://www.exchangerate-api.com/).
- File Google Sheet mẫu đã được sao chép từ [Template Sheet](https://docs.google.com/spreadsheets/d/1SjzMb2q-6-byx9qmHbkrLseBWj9jEGduinH_5xi-c7g/edit?usp=sharing).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào [n8n.io/workflows/3556](https://n8n.io/workflows/3556).
2. Nhấn vào nút "Import" để tải workflow về máy.
3. Mở n8n Editor và chọn "Import from File" để tải workflow vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Trigger - 08:00 am**:
   - Node này sẽ kích hoạt workflow hàng ngày lúc 8:00 sáng.
   - Không cần cấu hình gì thêm.

2. **USD Query**:
   - Node này gọi API ExchangeRate để lấy tỷ giá tiền tệ từ USD sang các loại tiền khác.
   - Thay thế `<YOUR_API_KEY>` trong URL bằng API Key của bạn.
   - Ví dụ: `https://v6.exchangerate-api.com/v6/YOUR_API_KEY/latest/USD`.

3. **Update Rate Sheet**:
   - Node này cập nhật tỷ giá tiền tệ mới nhất vào sheet "Invoice Template" trong Google Sheet.
   - Cấu hình credentials Google Sheets và chọn file Google Sheet đã sao chép từ template.
   - Chọn sheet "Invoice Template" và cấu hình các trường dữ liệu cần cập nhật.

4. **Archive Rates**:
   - Node này ghi lại lịch sử tỷ giá tiền tệ vào sheet "Record" trong Google Sheet.
   - Cấu hình tương tự như node "Update Rate Sheet", nhưng chọn sheet "Record".

5. **Format Output to JSON**:
   - Node này định dạng dữ liệu đầu ra thành JSON.
   - Không cần cấu hình gì thêm.

6. **Filter Fields**:
   - Node này lọc các trường dữ liệu cần thiết.
   - Không cần cấu hình gì thêm.

7. **Final Outputs**:
   - Node này hợp nhất các dữ liệu đầu ra cuối cùng.
   - Không cần cấu hình gì thêm.

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, nhấn vào nút "Activate" để kích hoạt workflow.
2. Test workflow bằng cách nhấn vào nút "Execute Workflow" để kiểm tra xem workflow có hoạt động đúng không.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node gửi thông báo qua Slack hoặc Telegram khi workflow hoàn thành.
- **Lưu log**: Thêm node ghi log để theo dõi lịch sử chạy workflow.
- **Gửi báo cáo định kỳ**: Thêm node gửi báo cáo định kỳ qua email với các tỷ giá tiền tệ mới nhất.
- **Tự động hóa thêm**: Kết hợp với các workflow khác để tự động hóa các quy trình liên quan đến hóa đơn.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc cập nhật tỷ giá tiền tệ trong hóa đơn hàng ngày một cách dễ dàng và chính xác. Với việc chạy tự động vào lúc 8:00 sáng hàng ngày, các sếp không cần phải lo lắng về việc cập nhật dữ liệu thủ công nữa. Hãy áp dụng ngay workflow này để tiết kiệm thời gian và tăng hiệu quả làm việc!