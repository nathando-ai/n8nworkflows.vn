---
title: "🚀 Tự động trích xuất và cấu trúc dữ liệu hóa đơn với DocSumo, n8n và Excel"
description: "Hướng dẫn chi tiết cách xây dựng hệ thống tự động hóa xử lý hóa đơn, trích xuất dữ liệu thông minh qua DocSumo API và xuất file Excel chuyên nghiệp với n8n."
slug: "tu-dong-trich-xuat-du-lieu-hoa-don-docsumo-excel"
tags: [n8n, automation, docsumo, invoice-processing, ai-summarization, excel]
keywords: [n8n workflow, trích xuất hóa đơn, DocSumo API, tự động hóa kế toán, xử lý hóa đơn AI, n8n excel]
---

# 🚀 Tự động trích xuất và cấu trúc dữ liệu hóa đơn với DocSumo và Excel

Việc nhập liệu hóa đơn thủ công hàng ngày luôn là "cơn ác mộng" đối với các bộ phận kế toán và vận hành. Nhân viên thường mất hàng giờ để đọc từng file PDF, bóc tách các trường dữ liệu như tên nhà cung cấp, mã số thuế, tổng tiền, chi tiết từng mặt hàng và gõ lại vào file Excel. Quy trình này vừa tốn thời gian, dễ xảy ra sai sót, lại vừa nhàm chán.

Giải pháp? Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình trên! Chỉ cần tải file hóa đơn lên qua form giao diện gọn gàng, hệ thống sẽ tự động gọi API của DocSumo để phân tích thông minh, xử lý dữ liệu qua JavaScript và xuất ra file Excel chuẩn chỉnh ngay lập tức.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn cảnh gõ Excel thủ công, giải phóng nhân sự cho các công việc chiến lược hơn.
- **Độ chính xác cao:** Ứng dụng công nghệ AI/OCR từ DocSumo giúp nhận diện bóc tách dữ liệu hóa đơn cực kỳ chính xác.
- **Giao diện thân thiện:** Tích hợp form nộp tài liệu trực quan, dễ dàng sử dụng cho bất kỳ ai trong công ty.
- **Tự động hóa liền mạch:** Nhận file, xử lý và trả về file Excel tải về ngay tức thì mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản DocSumo:** Cần đăng ký tài khoản tại DocSumo để lấy API Key phục vụ việc trích xuất tài liệu/hóa đơn.
- **Credentials:** Chuẩn bị sẵn API Key của DocSumo để cấu hình trong các node HTTP Request.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này hoặc sao chép toàn bộ mã JSON.
- Trong giao diện n8n Editor, nhấn vào mục **Workflows** > **Add workflow** > **Import from File / Paste JSON**.
- Dán mã JSON vào và lưu lại.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 6 nodes chính hoạt động nhịp nhàng. Các sếp cần chú ý cấu hình kỹ các điểm sau:

- **On form submission (`formTrigger`):** 
  - Node này tạo ra một giao diện Web Form để người dùng tải file hóa đơn lên. Các sếp có thể tùy chỉnh tiêu đề form hoặc thêm các trường thông tin nếu muốn.
- **HTTP Request, HTTP Request1, HTTP Request2 (`httpRequest`):**
  - Đây là chuỗi các request kết nối tới DocSumo API (gồm các bước: tải file lên, kích hoạt tiến trình trích xuất, và lấy kết quả trả về).
  - Các sếp **bắt buộc** phải điền DocSumo API Key vào phần Header Authentication của các node này để hệ thống có quyền gọi API.
- **Code (`code`):**
  - Node này dùng ngôn ngữ JavaScript để chuẩn hóa và định dạng lại cấu trúc dữ liệu thô nhận được từ DocSumo (gom nhóm header hóa đơn hoặc danh sách các mặt hàng line-item). 
  - *Lưu ý từ tác giả:* Các sếp có thể tùy chỉnh lại đoạn code này để thêm/bớt các cột dữ liệu xuất ra Excel cho phù hợp với nhu cầu thực tế của doanh nghiệp.
- **Convert to File (`convertToFile`):**
  - Cấu hình sẵn với thao tác (`operation: "xls"`), node này sẽ gom dữ liệu đã được xử lý sạch sẽ từ node Code và chuyển đổi thành một tệp Excel hoàn chỉnh sẵn sàng để tải xuống hoặc gửi đi.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử tải lên một hóa đơn mẫu qua form để test xem dữ liệu trả về đã đúng ý chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để đưa workflow vào trạng thái vận hành tự động thực tế.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống xịn sò hơn nữa, các sếp có thể mở rộng workflow này bằng cách:
1. **Gửi thông báo qua Telegram/Slack:** Thêm node gửi tin nhắn tự động kèm thông tin tổng tiền hóa đơn ngay sau khi xử lý xong.
2. **Lưu trữ tự động lên Google Drive / OneDrive:** Thay vì chỉ cho tải về qua form, tự động lưu file Excel kết quả vào thư mục kế toán trên Cloud.
3. **Gửi email xác nhận:** Tích hợp node Gmail hoặc SMTP để tự động gửi báo cáo tổng hợp hóa đơn về email của kế toán trưởng.

### 📌 Kết luận
Với workflow tự động hóa xử lý hóa đơn kết hợp giữa n8n và DocSumo này, các sếp đã có thể số hóa hoàn toàn quy trình kế toán thủ công chỉ trong vài nốt nhạc. Bắt tay vào cài đặt ngay để tối ưu hóa hiệu suất doanh nghiệp nào!