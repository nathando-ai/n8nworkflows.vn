---
title: "🚀 Trích xuất thông tin sản phẩm từ ảnh chụp màn hình website tự động với Dumpling AI và GPT-4o"
description: "Hướng dẫn xây dựng workflow n8n tự động chụp ảnh màn hình website, trích xuất dữ liệu bằng Dumpling AI, phân tích thông tin sản phẩm qua GPT-4o và lưu trữ vào Google Sheets."
slug: "trich-xuat-thong-tin-san-pham-tu-screenshot-dumpling-ai-gpt-4o"
tags: [n8n, automation, no-code, ai, gpt-4o, google-sheets, web-scraping]
keywords: [n8n workflow, trích xuất thông tin sản phẩm, dumpling ai, gpt-4o, chụp ảnh màn hình website, tự động hóa google sheets]
---

# 🚀 Trích xuất thông tin sản phẩm từ ảnh chụp màn hình website tự động với GPT-4o & Dumpling AI

Các sếp làm trong ngành E-commerce, Marketing hay Competitor Analysis chắc chắn đã ngán ngẩm cảnh phải mở từng trang web sản phẩm thủ công, copy tên, giá, đánh giá rồi paste vào file Excel. Vừa tốn thời gian, dễ sai sót lại chẳng thể scale lớn được. 

Giải pháp là đây! Workflow n8n này sẽ tự động hóa toàn bộ quy trình: nhận URL từ Google Sheets 👉 chụp ảnh toàn trang web (Full-page Screenshot) 👉 trích xuất toàn bộ text/dữ liệu hình ảnh 👉 dùng sức mạnh AI của **GPT-4o** để phân tích cấu trúc sản phẩm 👉 lưu trữ gọn gàng vào Google Sheets và Google Drive. 100% tự động, không cần viết code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chỉ cần thả URL vào Google Sheets, mọi việc còn lại n8n lo.
- **Lưu trữ đa tầng:** Lưu hình ảnh chụp màn hình gốc lên Google Drive để tra cứu khi cần.
- **AI thông minh (GPT-4o):** Bóc tách chính xác các trường dữ liệu phức tạp như tên sản phẩm, giá, đánh giá (rating), số lượng đã bán, ưu đãi...
- **Báo cáo chuẩn chỉnh:** Tự động tách từng sản phẩm thành các dòng riêng biệt và ghi vào bảng tính để phân tích, làm giá hay nghiên cứu thị trường.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n Instance:** Đã chạy sẵn (Cloud hoặc Self-hosted).
- **Google Sheets & Google Drive Account:** Để theo dõi URL, lưu ảnh và ghi nhận kết quả.
- **Dumpling AI Account & API Key:** Dùng để chụp ảnh màn hình và trích xuất text từ ảnh.
- **OpenAI API Key:** Sở hữu sức mạnh của GPT-4o để phân tích dữ liệu sản phẩm.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp tải file JSON của workflow này, vào giao diện n8n chọn **Add workflow** -> **Import from File** (hoặc copy/paste trực tiếp JSON vào n8n Editor).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 9 nodes chính hoạt động mượt mà theo chuỗi logic, các sếp cần cấu hình kỹ các điểm sau:

- **Trigger on New URL in Sheet (`googleSheetsTrigger`):** 
  - Kết nối tài khoản Google Sheets của các sếp qua OAuth2.
  - Chọn file Spreadsheet và Sheet cụ thể chứa danh sách các URL sản phẩm cần quét.
- **Take Full-Page Screenshot using Dumpling AI (`httpRequest`):**
  - Cấu hình thông tin xác thực (Credentials) dạng Header Auth cho Dumpling AI.
  - Truyền tham số URL nhận được từ Trigger vào body/query của request.
- **Extract All Visible Data from Screenshot (`httpRequest`) & Download Screenshot File (`httpRequest`):**
  - Node gọi API Dumpling AI để lấy toàn bộ text/UI elements và tải file ảnh về dưới dạng binary data.
- **Save Screenshot to Drive Folder (`googleDrive`):**
  - Kết nối Google Drive OAuth2.
  - Chọn thư mục đích trên Drive để lưu trữ ảnh chụp màn hình làm tài liệu tham khảo lâu dài.
- **Log Screenshot URL to Spreadsheet (`googleSheets`):**
  - Cập nhật (Append or Update) đường dẫn hình ảnh vừa lưu trên Drive trở lại Google Sheets.
- **Extract Product Info from Screenshot Text with GPT-4o (`openAi`):**
  - Sử dụng model `gpt-4o`.
  - Cấu hình System Prompt/User Prompt để hướng dẫn AI bóc tách các thông tin cụ thể: Tên sản phẩm, giá cả, đánh giá, lượt mua, chương trình khuyến mãi... từ dữ liệu text thô mà Dumpling AI cung cấp.
- **Split Each Product into Individual Record (`splitOut`):**
  - Tách mảng dữ liệu JSON sản phẩm trả về từ GPT-4o thành các bản ghi độc lập.
- **Save Products info to Google Sheet (`googleSheets`):**
  - Thêm các dòng dữ liệu sản phẩm đã được cấu trúc gọn gàng vào một Sheet hoặc bảng tính riêng biệt để tiện phân tích.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Test step / Execute workflow**) với một URL mẫu để kiểm tra kết quả trả về ở Google Sheets và Google Drive.
- Sau khi thấy mọi thứ chạy mượt mà, gạt nút **Active** để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node **Telegram** hoặc **Slack** ở cuối luồng để gửi thông báo tóm tắt mỗi khi quét xong một danh sách sản phẩm.
- **Xử lý lỗi (Error Handling):** Thêm Error Trigger để bắt lỗi trong trường hợp URL bị hỏng hoặc Dumpling AI/OpenAI quá tải, tránh làm gián đoạn toàn bộ workflow.
- **Lịch trình chạy định kỳ:** Ngoài trigger theo Sheet, có thể kết hợp thêm Schedule Trigger để tự động quét lại các sản phẩm đối thủ theo tuần/tháng.

### 📌 Kết luận
Với sự kết hợp đỉnh cao giữa **Dumpling AI** (chụp và đọc chữ từ ảnh) và **GPT-4o** (hiểu ngữ nghĩa và cấu trúc dữ liệu), workflow này giải quyết triệt để bài toán thu thập dữ liệu web phức tạp mà không cần viết một dòng code nào. Chúc các sếp cài đặt thành công và tối ưu hóa năng suất công việc!