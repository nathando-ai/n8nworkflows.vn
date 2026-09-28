---
title: "🚀 Tự động hóa xử lý và trích xuất dữ liệu bảo hiểm y tế với VLM Run, Google Drive và Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động phát hiện hồ sơ bảo hiểm y tế mới trên Google Drive, trích xuất dữ liệu thông minh bằng VLM Run và lưu trữ trực tiếp vào Google Sheets."
slug: "tu-dong-hoa-xu-ly-ho-so-bao-hiem-y-te-n8n-vlm-run"
tags: [n8n, automation, no-code, ai-summarization, multimodal-ai, google-drive, google-sheets]
keywords: [n8n workflow, xử lý bảo hiểm y tế, vlm run, trích xuất dữ liệu tài liệu, tự động hóa google sheets, ai multimodal]
---

# 🚀 Tự động hóa xử lý hồ sơ bảo hiểm y tế với VLM Run và Google Workspace

Việc xử lý các thủ tục, đơn yêu cầu bồi thường bảo hiểm y tế hay giấy tờ y tế thủ công thường tốn rất nhiều thời gian, dễ xảy ra sai sót khi nhập liệu và làm chậm tiến độ hoàn tiền cho bệnh nhân. Các doanh nghiệp bảo hiểm và cơ sở y tế thường đối mặt với núi tài liệu cần xử lý mỗi ngày.

Giải pháp hoàn hảo là đây! Workflow n8n này sẽ tự động hóa toàn bộ quy trình: ngay khi có tài liệu hồ sơ y tế được tải lên Google Drive, hệ thống sẽ tự động tải xuống, sử dụng AI đa phương thức (Multimodal AI) từ **VLM Run** để trích xuất cấu trúc dữ liệu chính xác và tự động lưu thẳng vào **Google Sheets** để các sếp dễ dàng theo dõi, báo cáo. Không cần code, hoạt động 100% tự động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình tiếp nhận:** Không cần nhân sự phải kiểm tra và nhập liệu thủ công từng hồ sơ.
- **Trích xuất thông minh và chính xác:** Biến các biểu mẫu y tế phức tạp (PDF, hình ảnh) thành dữ liệu JSON cấu trúc rõ ràng nhờ VLM Run.
- **Lưu trữ khoa học:** Mọi thông tin như Tên bệnh nhân, Mã bảo hiểm, Mã dịch vụ, Số tiền thanh toán... tự động cập nhật vào Google Sheets theo thời gian thực.
- **Tăng tốc xử lý:** Rút ngắn thời gian xét duyệt, nâng cao trải nghiệm khách hàng và tối ưu hóa tuân thủ quy định của cơ quan thanh toán.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Server:** Đã cài đặt và đang hoạt động (Self-hosted hoặc n8n Cloud).
- **VLM Run API Key:** Tài khoản và API access từ dịch vụ VLM Run.
- **Google tài khoản (Google Drive & Google Sheets):** Cấp quyền OAuth2 để n8n có thể truy cập đọc/ghi file và dữ liệu bảng tính.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n Editor, sau đó copy toàn bộ mã nguồn JSON của workflow hoặc import file cấu hình tương ứng vào hệ thống n8n của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Google Drive Trigger:** 
  - Chọn tài khoản Google Drive OAuth2 Credentials.
  - Chỉ định thư mục cụ thể trên Google Drive (`Watch Folder`) nơi nhân viên hoặc đối tác sẽ tải lên các form yêu cầu bồi thường y tế. Node này sẽ tự động bắt sự kiện khi có file mới xuất hiện và truyền metadata (ID file, tên, định dạng) sang bước tiếp theo.
- **Download file:** 
  - Sử dụng Google Drive Credentials.
  - Node này nhận File ID từ Trigger phía trên để tải toàn bộ nội dung file (dạng nhị phân PDF hoặc ảnh) xuống, đảm bảo VLM Run có dữ liệu sạch để xử lý.
- **VLM Run:** 
  - Cấu hình `vlmRunApi` Credentials với API Key hợp lệ.
  - Sử dụng danh mục (Category/Model) chuẩn cho bài toán y tế: `healthcare.claims-processing`. Node này sẽ bóc tách các thông tin chi tiết như: Tên bệnh nhân, ngày sinh, số bảo hiểm, mã chẩn đoán (ICD), mã CPT/HCPCS, số tiền yêu cầu thanh toán, thông tin nhà cung cấp dịch vụ y tế và phản hồi từ bên chi trả.
- **Append row in sheet:** 
  - Cấu hình Google Sheets OAuth2 Credentials.
  - Chọn file Google Sheet và Sheet Name phù hợp để lưu trữ dữ liệu. Các cột cần chuẩn bị sẵn trên Sheet bao gồm: *Patient, DOB, Insurance ID, CPT/HCPCS Code, Diagnosis Code, Billed Amount, Modifiers, Provider, Date of Service, Payer Response*. Map các trường dữ liệu JSON trả về từ VLM Run vào tương ứng các cột này.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử upload một file hồ sơ y tế mẫu lên thư mục Google Drive đã chọn để kiểm tra kết quả test run.
- Sau khi thấy dữ liệu được bóc tách và đẩy thành công vào Google Sheet, hãy gạt công tắc sang **Active** để workflow chính thức tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo qua Slack/Telegram:** Thêm node gửi tin nhắn ngay sau bước Append Row để thông báo cho đội ngũ xét duyệt mỗi khi có một hồ sơ mới được xử lý thành công.
- **Xử lý ngoại lệ (Error Handling):** Thêm Error Trigger để bắt các trường hợp file lỗi, định dạng không hỗ trợ hoặc lỗi API, sau đó gửi cảnh báo vào kênh chat nội bộ.
- **Phân loại hồ sơ:** Mở rộng workflow bằng cách thêm các nhánh điều kiện (If/Switch) dựa trên kết quả trả về của VLM Run để phân loại hồ sơ cần duyệt tự động hay cần chuyên viên xem xét thủ công.

### 📌 Kết luận
Workflow xử lý hồ sơ y tế tự động với VLM Run và Google Workspace là trợ thủ đắc lực giúp số hóa quy trình vận hành, tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần. Hãy thiết lập ngay hôm nay để tối ưu hóa năng suất cho tổ chức của các sếp!