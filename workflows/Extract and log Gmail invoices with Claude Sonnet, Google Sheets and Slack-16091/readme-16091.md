---
title: "🚀 Tự động hóa trích xuất hóa đơn Gmail với Claude Sonnet, Google Sheets & Slack"
description: "Giải pháp n8n workflow giúp tự động đọc email hóa đơn từ Gmail, trích xuất dữ liệu tài chính bằng Claude AI, lưu trữ vào Google Sheets và cảnh báo qua Slack."
slug: "tu-dong-hoa-trich-xuat-hoa-don-gmail-claude-sonnet-google-sheets-slack"
tags: [n8n, automation, ai, claude-sonnet, google-sheets, slack, gmail, invoice-processing]
keywords: [n8n workflow, trích xuất hóa đơn tự động, claude ai gmail sheets, xử lý hóa đơn tự động, n8n invoice automation]
---

# 🚀 Tự động hóa trích xuất hóa đơn Gmail với Claude Sonnet, Google Sheets & Slack

Các sếp có còn đang tốn hàng giờ mỗi tuần để thủ công mở từng email hóa đơn, copy số tiền, tên nhà cung cấp, ngày tháng rồi dập mật vào file Excel hay Google Sheets? Việc này không chỉ nhàm chán, mất thời gian mà còn cực kỳ dễ xảy ra sai sót hoặc bỏ quên các hóa đơn giá trị cao, hóa đơn đến hạn thanh toán.

Được thiết kế bởi chuyên gia tự động hóa **Akshay Chug**, workflow n8n này sẽ thay thế hoàn toàn quy trình thủ công đó. Hệ thống sẽ tự động quét hộp thư Gmail, sử dụng sức mạnh AI của **Claude Sonnet** để đọc hiểu nội dung hóa đơn (cả trong email lẫn file PDF đính kèm), tự động chống trùng lặp, lưu vào **Google Sheets** và bắn thông báo qua **Slack** cho các hóa đơn quan trọng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần upload file thủ công, không cần copy-paste số liệu từ email vào bảng tính.
- **Trích xuất thông minh với AI:** Claude Sonnet đọc hiểu chính xác 12 trường dữ liệu tài chính quan trọng (loại chứng từ, nhà cung cấp, số hóa đơn, ngày tháng, thuế, tổng tiền...).
- **Chống trùng lặp thông minh:** Hệ thống tự động kiểm tra xem hóa đơn đã tồn tại trong Google Sheets hay chưa trước khi ghi nhận.
- **Cảnh báo kịp thời:** Tự động gửi thông báo qua Slack đối với các hóa đơn giá trị cao hoặc hóa đơn đến hạn thanh toán.
- **Giữ hộp thư gọn gàng:** Tự động đánh dấu "Đã đọc" (Mark as Read) cho các email hóa đơn đã xử lý thành công.
:::

---

### Yêu cầu cần thiết
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và dịch vụ sau:
1. **n8n Instance** (Self-hosted hoặc n8n Cloud).
2. **Tài khoản Google (Gmail & Google Sheets):** Để quét email và lưu trữ dữ liệu.
3. **Anthropic API Key:** Để sử dụng model Claude Sonnet. Lấy key tại [console.anthropic.com](https://console.anthropic.com/).
4. **Tài khoản Slack (Tùy chọn):** Nếu muốn nhận thông báo thời gian thực về hóa đơn giá trị cao.

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow này hoặc tải file JSON từ nguồn cung cấp.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấn vào menu 3 chấm ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from JSON** và dán mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node sau để hệ thống chạy đúng ý muốn:

- **Check Gmail for Invoices (`gmailTrigger`):** Kết nối tài khoản Gmail của sếp. Mặc định workflow sẽ quét email mỗi 15 phút (có thể thay đổi tần suất này trong phần cài đặt trigger).
- **Configure Settings (`code`):** Mở node này để thiết lập các thông số quan trọng như:
  - `HIGH_VALUE_THRESHOLD`: Ngưỡng giá trị hóa đơn để kích hoạt cảnh báo Slack.
  - `SLACK_CHANNEL`: Kênh Slack nhận thông báo.
  - `LOG_SHEET_ID`: ID của file Google Sheets lưu trữ dữ liệu.
- **Claude Sonnet (`lmChatAnthropic`):** Click vào sub-node này nằm dưới node *Extract Invoice Data with Claude*, thêm credential mới bằng Anthropic API Key của sếp.
- **Check for Duplicate & Log Invoice to Sheets (`googleSheets`):** 
  - Tạo sẵn một Google Sheet có tên (hoặc cấu hình tên Sheet) với các cột dữ liệu: `Timestamp`, `From`, `Subject`, `Invoice Type`, `Vendor Name`, `Invoice Number`, `Invoice Date`, `Due Date`, `Currency`, `Subtotal`, `Tax`, `Total Amount`, `Payment Status`, `Line Items`, `Confidence`, `Email ID`.
  - Kết nối tài khoản Google của sếp cho cả hai node kiểm tra trùng lặp và ghi dữ liệu.
- **Notify - High Value or Overdue (`slack`):** Kết nối tài khoản Slack và chọn đúng kênh nhận tin. *(Lưu ý: Nếu không dùng Slack, các sếp có thể chuột phải vào node này và chọn Disable).*
- **Mark Email as Read (`gmail`):** Kết nối tài khoản Gmail để hệ thống tự động đánh dấu đã đọc các email đã xử lý.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng cách gửi một email hóa đơn mẫu vào hộp thư của sếp để kiểm tra dữ liệu trả về trong Google Sheets.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Ngoài Slack, các sếp có thể nhân bản node thông báo để gửi tin nhắn qua Telegram Bot hoặc Zalo OA để tiện theo dõi trên điện thoại.
- **Tự động chuyển tiếp cho kế toán:** Thêm một nhánh gửi email tự động (Gmail node) kèm thông tin hóa đơn trích xuất trực tiếp đến bộ phận kế toán hoặc phần mềm MISA/Fast.
- **Lưu trữ file PDF đính kèm:** Kết hợp thêm Google Drive node để tự động tải file PDF hóa đơn từ Gmail lên một thư mục riêng biệt trên Drive, giúp dễ dàng tra cứu chứng từ gốc khi quyết toán thuế.

---

### 📌 Kết luận
Với workflow tự động hóa này, các sếp sẽ tiết kiệm được hàng chục giờ làm việc thủ công mỗi tháng, loại bỏ hoàn toàn tình trạng thất lạc hóa đơn hay nhập liệu sai sót. Hãy cài đặt ngay hôm nay để tối ưu hóa quy trình tài chính cho doanh nghiệp của mình!