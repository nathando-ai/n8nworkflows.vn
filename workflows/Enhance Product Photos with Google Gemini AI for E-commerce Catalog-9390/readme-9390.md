---
title: "🚀 Tự động hóa chỉnh sửa ảnh sản phẩm Thương mại điện tử với Google Gemini AI và n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình tối ưu và chỉnh sửa ảnh sản phẩm cho danh mục e-commerce sử dụng Google Gemini AI và Google Drive."
slug: "tu-dong-hoa-chinh-sua-anh-san-pham-e-commerce-google-gemini-n8n"
tags: [n8n, automation, e-commerce, google-gemini, ai, google-drive]
keywords: [n8n workflow, chỉnh sửa ảnh tự động, google gemini ai, e-commerce catalog, tự động hóa n8n, google sheets tracking]
---

# 🚀 Tự động hóa chỉnh sửa ảnh sản phẩm Thương mại điện tử với Google Gemini AI

Các sếp làm trong ngành Thương mại điện tử (E-commerce) chắc chắn hiểu rõ nỗi đau: Việc chụp và chỉnh sửa hàng trăm, hàng ngàn bức ảnh sản phẩm để đồng bộ phong cách, xóa nền hoặc làm đẹp catalog tốn rất nhiều thời gian, chi phí nhân sự và cực kỳ nhàm chán khi làm thủ công.

Workflow n8n này sinh ra để giải quyết triệt để bài toán đó! Nó hoạt động như một "phòng studio AI tự động 24/7": Tự động phát hiện ảnh mới trong Google Drive, dùng sức mạnh thị giác của **Google Gemini AI** để chỉnh sửa theo prompt tùy chỉnh, lưu kết quả vào thư mục định sẵn và đồng thời ghi log tiến độ chi tiết lên Google Sheets mà không cần con người nhúng tay vào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Tự động hóa hoàn toàn quy trình xử lý ảnh hàng loạt (batch processing) mà không cần mở Photoshop từng cái.
- **Đồng bộ nhận diện catalog:** Đảm bảo toàn bộ ảnh sản phẩm có phong cách, ánh sáng và bối cảnh đồng nhất nhờ sức mạnh của Gemini AI.
- **Quản lý minh bạch:** Mọi trạng thái xử lý (Not Started, Done, Error) cùng thời gian bắt đầu/kết thúc đều được log tự động vào Google Sheets.
- **Hoạt động 24/7 không mệt mỏi:** Chỉ cần thả ảnh vào thư mục Google Drive, hệ thống sẽ tự động "gánh" phần còn lại.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Google:** Có quyền truy cập Google Drive và Google Sheets.
- **Google AI Studio Account:** Tài khoản để tạo **Google Gemini API Key** (dùng cho node AI xử lý ảnh).
- **Thư mục Google Drive:** Chuẩn bị sẵn 1 thư mục chứa ảnh gốc (Input) và 1 thư mục chứa ảnh sau khi xử lý (Output).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể lấy file JSON gốc từ [n8n Workflow #9390](https://n8n.io/workflows/9390), sau đó copy toàn bộ nội dung JSON và dán (Paste) trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các thành phần sau:

- **Node `Workflow Configuration` (Set):**
  - `google_sheet_id`: Điền ID của Google Sheet quản lý công việc (ID là đoạn ký tự nằm giữa URL của Google Sheet).
  - `dest_folder_id`: Điền ID thư mục Google Drive chứa ảnh sau khi xử lý (Output).
  - `text_prompt`: Câu lệnh (Prompt) hướng dẫn AI cách chỉnh sửa ảnh theo ý muốn (ví dụ: *"Enhance product lighting and place on a clean minimalist background"*).

- **Triggers `File Created` & `File Updated` (Google Drive Trigger):**
  - Chọn tài khoản Google OAuth2.
  - Trỏ trường **Folder** đến ID của thư mục Google Drive chứa ảnh gốc cần theo dõi.

- **Node `Edit Image` (Google Gemini / PaLM):**
  - Cấu hình credentials sử dụng **Google Gemini(PaLM) API Key** lấy từ Google AI Studio.
  - Node này sẽ thực hiện thao tác *Image Editing (Image + Text to Image)* dựa trên prompt đã cấu hình ở bước trên.

- **Các node Google Drive & Google Sheets còn lại:**
  - Đồng bộ sử dụng chung 1 tài khoản Google Credentials có quyền **Editor** đối với Google Sheet và thư mục Drive.
  - Đảm bảo Google Sheet có tên sheet là `"Photos"` với các cột tiêu đề ở hàng 1: `File name`, `Status`, `Start Time`, `End Time`, `Input File`, `Output File`.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử tải một bức ảnh mẫu lên thư mục Google Drive đầu vào để test run.
- Kiểm tra kết quả trên Google Drive đầu ra và theo dõi trạng thái `Done` trên Google Sheets.
- Nếu mọi thứ chạy trơn tru, hãy bật công tắc **Active** góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack vào nhánh `Update Entry to Done` để nhận tin nhắn thông báo mỗi khi có ảnh sản phẩm mới được AI xử lý xong.
- **Mở rộng use case:** Không chỉ dùng cho e-commerce, các sếp có thể áp dụng quy trình này để đồng bộ hóa ảnh chân dung nhân sự (team photos) lên website công ty, hoặc xử lý ảnh bìa bài viết blog hàng loạt.
- **Xử lý lỗi thông minh:** Tận dụng nhánh `Update Entry to Error` để ghi nhận các file lỗi định dạng, giúp dễ dàng kiểm tra và xử lý lại sau đó.

### 📌 Kết luận
Tự động hóa quy trình xử lý hình ảnh sản phẩm với Google Gemini AI và n8n là bước đi chiến lược giúp các sếp tối ưu hóa vận hành, tiết kiệm chi phí và tăng tốc độ đưa sản phẩm lên sàn thương mại điện tử. Hãy cài đặt ngay hôm nay để trải nghiệm sức mạnh của AI trong tự động hóa doanh nghiệp!