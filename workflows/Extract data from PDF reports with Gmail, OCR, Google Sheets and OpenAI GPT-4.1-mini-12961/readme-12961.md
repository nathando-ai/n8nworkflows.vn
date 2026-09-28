---
title: "📄 Tự Động Hóa Trích Xuất Dữ Liệu PDF Báo Cáo Với Gmail, OCR & GPT-4.1-mini"
description: "Workflow n8n tự động nhận email chứa PDF, trích xuất dữ liệu bằng AI, phân loại hóa đơn/báo cáo và lưu vào Google Sheets, gửi thông báo Slack."
slug: "tu-dong-trich-xuat-du-lieu-pdf-bao-cao-gmail-ai"
tags: [n8n, automation, no-code, ai, pdf-extraction, google-sheets]
keywords: [n8n workflow, tự động hóa pdf, trích xuất dữ liệu ai, gmail trigger, google sheets automation]
---

# 📄 Tự Động Hóa Trích Xuất Dữ Liệu PDF Báo Cáo Với Gmail, OCR & GPT-4.1-mini

Trong môi trường kinh doanh hiện đại, các sếp thường phải đối mặt với hàng đống email chứa file PDF: hóa đơn, báo cáo tài chính, hợp đồng... Việc mở từng file, đọc nội dung, sao chép dữ liệu vào Excel hoặc Google Sheets không chỉ tốn thời gian mà còn dễ dẫn đến sai sót do con người.

Workflow này là giải pháp "chốt hạ" cho bài toán đó. Nó hoạt động như một nhân viên ảo 24/7: tự động quét email mới, nhận diện file PDF, sử dụng sức mạnh của AI (OpenAI GPT-4.1-mini) để trích xuất chính xác các trường dữ liệu quan trọng, phân loại loại tài liệu, lưu trữ có hệ thống vào Google Sheets và gửi thông báo ngay lập tức qua Slack. Toàn bộ quy trình diễn ra hoàn toàn tự động, không cần viết một dòng code phức tạp nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm hàng giờ mỗi tuần:** Loại bỏ hoàn toàn thao tác nhập liệu thủ công từ PDF.
- **Độ chính xác cao:** AI GPT-4.1-mini trích xuất dữ liệu có cấu trúc, giảm thiểu lỗi con người.
- **Phân loại thông minh:** Tự động tách biệt hóa đơn (Invoice) và báo cáo (Report) để xử lý riêng biệt.
- **Đồng bộ hóa dữ liệu:** Dữ liệu được lưu ngay vào Google Sheets và team được thông báo qua Slack trong vài giây.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Gmail:** Đã kết nối với n8n (OAuth2).
2. **Tài khoản Google Sheets:** Đã kết nối với n8n. Cần tạo sẵn một Sheet với các cột phù hợp (ví dụ: Date, Vendor, Amount, Type, Summary...).
3. **Tài khoản OpenAI:** Có API Key để sử dụng model `gpt-4.1-mini`.
4. **Tài khoản Slack:** Đã kết nối với n8n (OAuth2) và có Channel để nhận thông báo.
5. **File JSON Workflow:** Tải từ link gốc hoặc copy từ kho workflow n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** và dán link: `https://n8n.io/workflows/12961` HOẶC
3. Copy toàn bộ JSON của workflow và dán vào ô **Import from Clipboard**.
4. Sau khi import, các sếp sẽ thấy 16 nodes được kết nối sẵn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Các sếp cần click vào từng node sau để cấu hình:

**1. Node: `New PDF Email Trigger` (Gmail Trigger)**
- Chọn **Credential** Gmail của bạn.
- Trong phần **Filter**, hãy cấu hình để chỉ trigger khi email có attachment (file đính kèm).
- *Mẹo:* Có thể thêm filter theo Subject hoặc From để chỉ xử lý email từ các đối tác cụ thể.

**2. Node: `Workflow Configuration` (Set)**
- Node này chứa các biến cấu hình chung. Các sếp có thể chỉnh sửa các giá trị mặc định nếu cần (ví dụ: tên Sheet, tên Channel Slack).

**3. Node: `Extract Text from PDF` (Extract from File)**
- Node này tự động nhận file PDF từ bước trước.
- Đảm bảo rằng input data từ Gmail Trigger đã được map đúng vào trường `file` hoặc `binary` của node này.

**4. Node: `Parse Key Fields with AI` (Agent) & `OpenAI Chat Model`**
- **Credential:** Chọn API Key OpenAI.
- **Model:** Chọn `gpt-4.1-mini` (hoặc model tương đương).
- **Prompt:** Node này đã có prompt mẫu để trích xuất dữ liệu. Các sếp nên kiểm tra prompt để đảm bảo nó yêu cầu đúng các trường dữ liệu mà mình cần (ví dụ: Ngày, Nhà cung cấp, Tổng tiền, Số hóa đơn...).
- **Structured Output Parser:** Đảm bảo schema JSON output khớp với các cột trong Google Sheets của bạn.

**5. Node: `Classify Document Type` (Switch)**
- Node này phân loại tài liệu dựa trên dữ liệu đã trích xuất.
- Kiểm tra các điều kiện (Conditions) để đảm bảo logic phân loại "Invoice" và "Report" phù hợp với nghiệp vụ của công ty.

**6. Node: `Store Invoice Data` & `Store All Extracted Data` (Google Sheets)**
- **Credential:** Chọn tài khoản Google của bạn.
- **Document ID:** Chọn Sheet đã tạo sẵn.
- **Sheet Name:** Chọn tên Tab trong Sheet.
- **Operation:** Chọn `Append` (Thêm dòng mới).
- **Mapping:** Map các trường dữ liệu từ bước AI (ví dụ: `vendor`, `amount`) vào các cột tương ứng trong Sheet.

**7. Node: `Notify Contract Team` & `Send Summary Notification` (Slack)**
- **Credential:** Chọn workspace Slack.
- **Channel:** Chọn channel cần nhận thông báo.
- **Message:** Kiểm tra nội dung thông báo. Node này thường dùng template để hiển thị dữ liệu trích xuất được một cách dễ đọc.

**8. Node: `Error Handler and Logger` (Code)**
- Node này xử lý lỗi nếu quá trình trích xuất thất bại. Các sếp có thể tùy chỉnh logic log hoặc gửi thông báo lỗi nếu cần.

#### 3. Kích hoạt ⚡️
1. **Test Run:** Gửi một email mẫu chứa file PDF (hóa đơn hoặc báo cáo) đến tài khoản Gmail đã kết nối.
2. Chạy workflow bằng nút **Execute Workflow**.
3. Kiểm tra kết quả:
   - Dữ liệu có xuất hiện trong Google Sheets không?
   - Có nhận được thông báo trong Slack không?
   - Dữ liệu trích xuất có chính xác không?
4. Nếu mọi thứ ổn, bật **Active** workflow để nó chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy chỉnh Schema Output:** Nếu các sếp cần trích xuất thêm trường dữ liệu (ví dụ: Mã VAT, Ghi chú), hãy sửa prompt trong node `Parse Key Fields with AI` và cập nhật `Structured Output Parser` cùng cột trong Google Sheets.
- **Gửi Email Xác nhận:** Thêm một node Gmail Send Email để gửi email xác nhận cho người gửi rằng file đã được xử lý thành công.
- **Lưu trữ File PDF:** Thêm node Google Drive Upload để lưu lại file PDF gốc vào thư mục tương ứng, giúp truy xuất lại khi cần.
- **Báo cáo Định kỳ:** Kết hợp thêm node Schedule Trigger để tổng hợp dữ liệu từ Google Sheets và gửi báo cáo tuần/tháng qua Email hoặc Slack.

### 📌 Kết luận
Workflow này là một ví dụ điển hình cho sức mạnh của AI trong tự động hóa văn phòng. Thay vì mất thời gian đọc từng trang PDF, các sếp chỉ cần tập trung vào việc ra quyết định dựa trên dữ liệu đã được dọn dẹp và cấu trúc sẵn. Hãy thử áp dụng ngay để trải nghiệm sự khác biệt mà tự động hóa mang lại!