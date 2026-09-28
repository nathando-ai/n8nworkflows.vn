---
title: "🚀 Tự động tạo video quảng cáo sản phẩm 8 giây từ Google Drive bằng Gemini & Veo"
description: "Hướng dẫn chi tiết workflow n8n tự động hóa quy trình biến hình ảnh sản phẩm thành video quảng cáo 8s chuyên nghiệp nhờ AI đa phương thức."
slug: "tao-video-quang-cao-san-pham-voi-gemini-va-veo-n8n"
tags: [n8n, automation, ai, google-drive, gemini, video-generation]
keywords: [n8n workflow, tạo video quảng cáo AI, google drive gemini veo, tự động hóa n8n]
---

# 🚀 Tự động tạo video quảng cáo sản phẩm 8 giây từ Google Drive bằng Gemini & Veo

Các sếp có đang đau đầu vì tốn quá nhiều thời gian và chi phí để sản xuất video quảng cáo ngắn cho sản phẩm? Việc thuê designer dựng hình, viết kịch bản rồi render video thủ công vừa tốn kém lại chậm chạp trong thời đại "content is king" này.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực đỉnh, tự động hóa 100% quy trình: **Lấy ảnh sản phẩm từ Google Drive ➡️ Phân tích bằng Gemini AI ➡️ Viết kịch bản & prompt ➡️ Tạo video chất lượng cao bằng Veo ➡️ Lưu kết quả ngược lại Google Drive**. Tất cả chỉ trong vài nốt nhạc và hoàn toàn tự động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Không cần can thiệp thủ công từ khâu đọc ảnh đến khi xuất video MP4.
- **Sức mạnh AI đa phương thức:** Kết hợp Google Gemini phân tích hình ảnh sắc bén và Veo tạo video đỉnh cao.
- **Tiết kiệm chi phí khủng:** Thay vì thuê agency sản xuất video hàng tuần, hệ thống tự lo phần visual và kịch bản.
- **Tài sản số đồng bộ:** Video thành phẩm tự động lưu trữ gọn gàng vào thư mục Google Drive định sẵn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n (Cloud hoặc Self-hosted).
- Tài khoản **Google Drive** (để lấy ảnh đầu vào và lưu video đầu ra).
- **Google Gemini API Key** (Google Palm API) cho các node AI.
- **API Key** cấu hình cho các HTTP Request gọi model tạo video (Veo).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow (hoặc tải file từ n8n.io/workflows/13920), sau đó dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 15 nodes được thiết kế mạch lạc, các sếp cần chú ý cấu hình các điểm cốt lõi sau:
- **Download ad image (Google Drive):** Chọn credentials Google Drive OAuth2 và trỏ tới file ảnh sản phẩm đầu vào của các sếp.
- **Creative Visualiser & Google Gemini Chat Model1:** Kết nối credentials `googlePalmApi` để cho phép Gemini phân tích hình ảnh (`analyze image`).
- **Product Video Prompt & Structured Output Parser:** Cấu hình node LangChain để Gemini tự động biên tập brief thành kịch bản video quảng cáo ngắn (ví dụ: kịch bản tiếng Việt 8 giây).
- **Generate Video (HTTP Request):** Cấu hình Header Auth API Key, tuỳ chỉnh các thông số quan trọng như `aspectRatio` (tỷ lệ khung hình), `resolution` (độ phân giải) và `durationSeconds` (thời lượng video).
- **Upload to Drive (Google Drive):** Chọn thư mục đích trên Google Drive để hệ thống tự động đẩy file MP4 thành phẩm lên sau khi node **Get Dowload Video** tải về hoàn tất.

#### 3. Kích hoạt ⚡️
- Nhấn **When clicking 'Test workflow'** (hoặc dùng `Manual Trigger`) để chạy thử nghiệm với một ảnh mẫu.
- Theo dõi quá trình xử lý qua các node **Wait** và **If** (kiểm tra trạng thái render video hoàn thành).
- Sau khi test thành công, bật nút **Active** để workflow sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack ở cuối luồng để nhận thông báo ngay khi video được render xong kèm link Google Drive.
- **Tự động hóa hàng loạt:** Thay thế nút Trigger thủ công bằng **Google Drive Trigger** (phát hiện có ảnh mới bỏ vào thư mục) để hệ thống tự động sinh video liên tục.
- **Lưu log vào Sheet:** Thêm node Google Sheets để ghi lại lịch sử tạo video, prompt đã dùng và link sản phẩm phục vụ việc quản lý content.

### 📌 Kết luận
Workflow này là một cỗ máy tự động hóa thực thụ giúp nâng tầm quy trình sản xuất nội dung video của các doanh nghiệp E-commerce và Content Creators. Hãy cài đặt ngay hôm nay để tối ưu hóa hiệu suất công việc của các sếp!