---
title: "🚀 Tự động trích xuất hóa đơn PDF sang JSON bằng Gemini AI và n8n"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động hóa quy trình đọc file hóa đơn PDF, sử dụng sức mạnh AI của Google Gemini để trích xuất dữ liệu và chuyển đổi thành định dạng JSON chuẩn xác."
slug: "trich-xuat-hoa-don-pdf-sang-json-voi-gemini-ai-trong-n8n"
tags: [n8n, automation, no-code, gemini-ai, pdf-extraction, ai-summarization]
keywords: [n8n workflow, trích xuất hóa đơn pdf, gemini ai n8n, chuyển đổi pdf sang json, tự động hóa kế toán]
---

# 🚀 Tự động trích xuất hóa đơn PDF sang JSON bằng Gemini AI và n8n

Các sếp có đang đau đầu với việc phải nhập liệu thủ công từng hóa đơn, chứng từ PDF vào hệ thống? Việc đọc hàng chục, hàng trăm hóa đơn mỗi ngày không chỉ tốn thời gian, dễ xảy ra sai sót mà còn làm gián đoạn các quy trình kinh doanh quan trọng. 

Đừng lo! Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n tự động hóa 100% không cần code: nhận file PDF hóa đơn qua biểu mẫu, bóc tách văn bản, tận dụng trí tuệ nhân tạo **Google Gemini AI** để phân tích dữ liệu thông minh và xuất ra định dạng JSON sẵn sàng tích hợp vào bất kỳ hệ thống nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh gõ tay từng con số, tên công ty, mã số thuế hay tổng tiền trên hóa đơn.
- **Độ chính xác cực cao:** Nhờ sức mạnh đa phương thức (multimodal) của Google Gemini, AI hiểu được cấu trúc hóa đơn phức tạp nhất.
- **Định dạng chuẩn hóa:** Dữ liệu đầu ra là chuỗi JSON sạch sẽ, dễ dàng lưu vào Database, Google Sheets hoặc đẩy qua các API khác.
- **Vận hành tự động 24/7:** Biểu mẫu tiếp nhận file hoạt động liên tục, xử lý ngay lập tức khi có file gửi lên.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng n8n (Cloud hoặc Self-hosted).
- **Google Gemini API Key:** Tài khoản Google AI Studio để kết nối với node Gemini.
- **File PDF hóa đơn mẫu:** Dùng để test quá trình trích xuất.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng mã nguồn JSON của workflow do chuyên gia Mauricio Perera thiết kế (Link gốc: [n8n Workflow #8460](https://n8n.io/workflows/8460)) bằng cách copy và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 6 nodes chính được chia thành các bước xử lý logic rõ ràng:

- **On form submission (`formTrigger`):** 
  - Node này tạo một giao diện Web Form đơn giản để người dùng tải file PDF hóa đơn lên. Các sếp có thể cấu hình lại tiêu đề form hoặc thêm các trường thông tin nếu cần.
- **Extract from File (`extractFromFile`):** 
  - Cấu hình sẵn thao tác `operation: pdf`. Node này sẽ đọc nội dung văn bản thô từ file PDF mà người dùng vừa upload qua Form.
- **Message a model (`googleGemini`):** 
  - **Credentials:** Cần cấu hình kết nối `googlePalmApi` bằng API Key lấy từ Google AI Studio.
  - **Prompt:** Các sếp cần cấu hình câu lệnh (prompt) hướng dẫn Gemini đọc văn bản hóa đơn và trả về kết quả theo cấu trúc XML/JSON mong muốn (Ví dụ: tách lấy Tên nhà cung cấp, Mã số thuế, Ngày hóa đơn, Tổng tiền, Chi tiết các mặt hàng...).
- **Limpio data (`set`) & Limpio XML (`set`):** 
  - Hai node này thực hiện việc làm sạch dữ liệu đầu ra từ AI, chuẩn hóa các chuỗi văn bản để đảm bảo cấu trúc XML/JSON không bị lỗi cú pháp.
- **XML to JSON (`xml`):** 
  - Chuyển đổi cấu trúc dữ liệu từ XML sang JSON object hoàn chỉnh, giúp các bước tiếp theo dễ dàng sử dụng dữ liệu dạng key-value.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và tải lên một file hóa đơn PDF mẫu thông qua URL của Form để test thử.
- Kiểm tra kết quả trả về ở node cuối cùng (`XML to JSON`) để đảm bảo dữ liệu JSON đã chính xác.
- Bật công tắc **Active** để đưa workflow vào trạng thái chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình kế toán và xử lý hóa đơn, các sếp có thể mở rộng workflow này bằng cách:
1. **Lưu tự động vào Google Sheets / Airtable:** Thêm node Google Sheets ngay sau bước `XML to JSON` để lưu trữ lịch sử hóa đơn vào bảng tính.
2. **Gửi thông báo qua Telegram / Slack:** Bắn thông báo ngay cho bộ phận kế toán kèm theo thông tin tổng tiền và tên nhà cung cấp mỗi khi có hóa đơn mới được xử lý thành công.
3. **Lưu trữ file PDF:** Đẩy file PDF gốc lên Google Drive hoặc OneDrive và lưu kèm đường dẫn vào database quản lý.

### 📌 Kết luận
Việc tự động hóa trích xuất hóa đơn PDF chưa bao giờ dễ dàng và thông minh đến thế nhờ sự kết hợp giữa n8n và Google Gemini AI. Hãy áp dụng ngay workflow này để giải phóng sức lao động cho đội ngũ kế toán và tối ưu hóa vận hành doanh nghiệp ngay hôm nay các sếp nhé!