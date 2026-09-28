---
title: "🚀 Tự động giám sát tin tức tiêu cực của danh sách công ty với Google Sheets, SerpAPI, Groq và Gmail"
description: "Hướng dẫn xây dựng workflow n8n tự động quét tin tức, sử dụng AI từ Groq để phân tích cảm xúc tiêu cực và gửi cảnh báo qua Gmail cho các công ty trong danh sách theo dõi."
slug: "tu-dong-giam-sat-tin-tuc-tieu-cuc-cong-ty"
tags: [n8n, automation, ai-summarization, market-research, groq, gmail, google-sheets]
keywords: [n8n workflow, giám sát tin tức tiêu cực, serpapi, groq ai, tự động hóa marketing, cảnh báo email]
---

# 🚀 Tự động giám sát tin tức tiêu cực của danh sách công ty với Google Sheets, SerpAPI, Groq và Gmail

Việc theo dõi thông tin truyền thông, đặc biệt là các tin tức tiêu cực, khủng hoảng truyền thông của đối thủ cạnh tranh hoặc các công ty trong danh sách theo dõi (Watchlist) thủ công là một công việc cực kỳ tốn thời gian và dễ bỏ sót. Nếu không phát hiện kịp thời, doanh nghiệp có thể bỏ lỡ những cơ hội hoặc rủi ro pháp lý/thị trường quan trọng.

Workflow n8n này ra đời như một giải pháp tự động hóa 100% không cần code giúp các sếp giải quyết triệt để bài toán trên. Hệ thống sẽ tự động đọc danh sách công ty từ Google Sheets, quét tin tức mới nhất qua SerpAPI, lọc bỏ các bản ghi trùng lặp, sử dụng AI siêu tốc từ Groq để phân tích độ tiêu cực, lưu trữ kết quả và tự động gửi cảnh báo qua Gmail khi phát hiện rủi ro.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn 24/7:** Không cần nhân sự ngồi đọc báo hay search Google thủ công hàng ngày.
- **Phát hiện rủi ro chớp nhoáng:** AI từ Groq (Groq Chat Model) đánh giá chính xác mức độ tiêu cực (Negative sentiment) và mức độ nghiêm trọng (Severity) của từng bài báo.
- **Chống trùng lặp thông minh:** Hệ thống tự động sinh ID duy nhất cho mỗi bài viết và đối chiếu với Google Sheets để không bao giờ xử lý lại bài cũ.
- **Cảnh báo tức thì:** Gửi email HTML trực quan qua Gmail ngay khi phát hiện tin tức rủi ro cao.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và dịch vụ sau:
- **n8n Instance:** Đã cài đặt sẵn (Cloud hoặc Self-hosted).
- **Google Sheets:** File Google Sheets chứa danh sách công ty cần theo dõi và file lưu trữ lịch sử tin tức.
- **SerpAPI:** Tài khoản và API Key để lấy dữ liệu tìm kiếm tin tức.
- **Groq API Key:** Để sử dụng mô hình ngôn ngữ AI phân tích nội dung.
- **Gmail Account:** Kết nối OAuth2 để gửi email cảnh báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào n8n Editor, hoặc import file JSON thông qua giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần cấu hình kỹ các node trọng điểm sau:
- **Start Workflow (Manual Trigger):** Có thể thay thế bằng Schedule Trigger để workflow tự động chạy định kỳ mỗi ngày/mỗi tuần tùy ý.
- **Read Watchlist & Lookup Existing Articles & Append Processed News (Google Sheets):** Kết nối tài khoản `googleSheetsOAuth2Api`, trỏ tới đúng file Google Sheets quản lý danh sách công ty và bảng lưu lịch sử tin tức.
- **Fetch News (HTTP Request):** Cấu hình gọi API tới SerpAPI với dynamic query (ví dụ: `{{ $('Read Watchlist').item.json.Companies }} news`).
- **Process Articles & Filter Article List (Code):** Các node viết bằng JavaScript giúp làm sạch dữ liệu, loại bỏ các kết quả không liên quan và tạo Unique ID dựa trên URL/Tiêu đề.
- **Groq Chat Model & Structured Output Parser:** Kết nối tài khoản `groqApi`, chọn model (ví dụ: `openai/gpt-oss-120b` hoặc model tương đương trên Groq) và đảm bảo cấu hình Output Parser trả về định dạng JSON nghiêm ngặt (`is_negative`, `reason`, `severity`).
- **Filter Negative News (If):** Thiết lập điều kiện lọc (`is_negative === true` hoặc mức độ nghiêm trọng vượt ngưỡng).
- **Send Alert (Gmail):** Kết nối tài khoản `gmailOAuth2`, thiết lập người nhận và định dạng nội dung HTML để email hiển thị chuyên nghiệp nhất.
- **Throttle API Calls (Wait):** Đảm bảo không gửi quá nhiều request dồn dập, tránh việc bị giới hạn API từ phía SerpAPI hoặc Groq.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm (Test run) với một vài dòng dữ liệu mẫu trong Google Sheets xem hệ thống có fetch tin, phân tích AI và gửi email thành công hay không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow tự động hoạt động.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Ngoài Gmail, các sếp có thể gắn thêm node Telegram Bot hoặc Slack để nhận thông báo ngay lập tức trên điện thoại.
- **Mở rộng bộ lọc:** Tùy chỉnh prompt trong AI Analysis để lọc cụ thể các từ khóa nhạy cảm liên quan đến pháp lý, tài chính hoặc bê bối lãnh đạo.
- **Lưu log định kỳ:** Tạo thêm một nhánh tổng hợp báo cáo tuần gửi vào Slack tổng kết số lượng tin tiêu cực đã quét được.

### 📌 Kết luận
Workflow này là một "vũ khí" cực mạnh cho các đội ngũ PR, Marketing, và Quản trị rủi ro doanh nghiệp. Hãy triển khai ngay hôm nay để bảo vệ hình ảnh thương hiệu trước mọi biến động thông tin trên Internet!