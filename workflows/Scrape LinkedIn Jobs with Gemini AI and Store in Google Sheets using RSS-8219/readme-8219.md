---
title: "🚀 Tự Động Hóa Tìm Việc: Scrape LinkedIn Jobs & AI Summarize vào Google Sheets"
description: "Workflow n8n tự động quét tin tuyển dụng từ LinkedIn RSS, dùng Gemini AI để tóm tắt và lưu trữ có cấu trúc vào Google Sheets. Giải pháp hoàn hảo cho các sếp muốn theo dõi thị trường việc làm hoặc tìm nhân sự chất lượng cao mà không cần code."
slug: "scrape-linkedin-jobs-gemini-ai-google-sheets"
tags: [n8n, automation, no-code, linkedin, gemini-ai, google-sheets, web-scraping]
keywords: [n8n workflow, tự động hóa tìm việc, scrape linkedin, gemini ai, google sheets automation]
---

# 🚀 Tự Động Hóa Tìm Việc: Scrape LinkedIn Jobs & AI Summarize vào Google Sheets

Trong kỷ nguyên dữ liệu, việc tìm kiếm nhân sự phù hợp hoặc theo dõi xu hướng tuyển dụng trên LinkedIn thường là một quá trình tốn kém thời gian. Các sếp phải mất hàng giờ mỗi ngày để lướt qua hàng trăm tin tuyển dụng, đọc mô tả công việc dài dòng, và sao chép thủ công vào bảng tính. Không chỉ mệt mỏi, phương pháp này còn dễ bỏ sót những cơ hội vàng hoặc dẫn đến dữ liệu không nhất quán.

Workflow này ra đời như một "trợ lý ảo" 24/7. Nó tự động đọc nguồn tin RSS từ LinkedIn, truy cập từng trang tin tuyển dụng để lấy dữ liệu chi tiết, sử dụng sức mạnh của **Google Gemini AI** để phân tích và tóm tắt thông tin quan trọng, sau đó lưu trữ một cách có cấu trúc vào **Google Sheets**. Toàn bộ quy trình diễn ra hoàn toàn tự động, không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 (đặc biệt nếu các sếp muốn nó chạy theo lịch trình định kỳ), việc cài đặt n8n trên VPS riêng (Self-hosted) là lựa chọn tối ưu về chi phí và hiệu năng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian thủ công:** Không cần click chuột hay copy-paste, hệ thống tự động cập nhật dữ liệu mới nhất.
- **Dữ liệu sạch & Có cấu trúc:** Thay vì các đoạn văn bản dài dòng, Gemini AI sẽ trích xuất các trường dữ liệu cụ thể (Vị trí, Địa điểm, Yêu cầu, Mức lương...) giúp dễ dàng lọc và phân tích.
- **Tóm tắt thông minh:** AI sẽ tóm tắt mô tả công việc (Job Description) thành những điểm chính, giúp các sếp nắm bắt bản chất công việc trong vài giây.
- **Lưu trữ tập trung:** Tất cả dữ liệu được lưu vào Google Sheets, dễ dàng chia sẻ với team tuyển dụng hoặc tích hợp thêm các công cụ khác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Bản miễn phí hoặc bản trả phí (khuyến nghị Self-hosted).
2. **Tài khoản Google:**
   - Dùng để tạo **Google Sheet** lưu trữ dữ liệu.
   - Cấp quyền OAuth2 cho n8n để truy cập Sheet.
3. **API Key Google Gemini:**
   - Đăng ký tại [Google AI Studio](https://aistudio.google.com/) để lấy API Key.
   - Workflow sử dụng model Gemini để xử lý ngôn ngữ tự nhiên.
4. **URL RSS Feed của LinkedIn:**
   - Các sếp cần có địa chỉ RSS feed của danh sách việc làm mong muốn (ví dụ: RSS của một từ khóa tìm kiếm cụ thể trên LinkedIn).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from File** hoặc **Import from URL**.
3. Dán file JSON của workflow hoặc link gốc: [https://n8n.io/workflows/8219](https://n8n.io/workflows/8219).
4. Workflow sẽ hiện ra với các node đã được kết nối sẵn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần cấu hình lại các node sau để phù hợp với nhu cầu thực tế:

**A. Node `Read RSS Feed.`**
- **URL:** Thay thế URL mặc định bằng **RSS Feed URL** của danh sách việc làm LinkedIn mà các sếp quan tâm.
  - *Mẹo:* Trên LinkedIn, sau khi tìm kiếm việc làm, các sếp có thể tìm link RSS trong phần "Share" hoặc sử dụng các công cụ chuyển đổi tìm kiếm LinkedIn sang RSS.
- **Limit:** Điều chỉnh số lượng tin tức tối đa muốn đọc mỗi lần chạy (mặc định có thể là 10-20).

**B. Node `Scrape Job HTML.` (HTTP Request)**
- Node này sẽ truy cập từng link job từ RSS.
- **Headers:** Đảm bảo các header User-Agent được cấu hình đúng để tránh bị LinkedIn chặn (thường workflow đã cấu hình sẵn, nhưng cần kiểm tra nếu gặp lỗi 403).

**C. Node `Pre-clean Before AI` (Code)**
- Node này xử lý dữ liệu thô từ HTML.
- Các sếp có thể chỉnh sửa logic ở đây nếu cấu trúc HTML của LinkedIn thay đổi, nhưng thường thì code mặc định đã xử lý tốt việc loại bỏ tag HTML và khoảng trắng thừa.

**D. Node `AI Agent` & `Google Gemini Chat Model`**
- **Credentials:** Chọn hoặc tạo mới credential **Google Gemini**.
- **API Key:** Điền API Key của các sếp vào credential.
- **System Prompt (trong AI Agent):**
  - Đây là "linh hồn" của workflow. Các sếp có thể chỉnh sửa prompt để yêu cầu Gemini trích xuất các trường dữ liệu cụ thể.
  - Ví dụ: "Hãy trích xuất: Job Title, Company Name, Location, Salary Range, Key Responsibilities (tóm tắt 3-5 gạch đầu dòng), Required Skills."
  - Đảm bảo output format khớp với `Structured Output Parser`.

**E. Node `Structured Output Parser`**
- Kiểm tra schema JSON để đảm bảo các trường dữ liệu mà Gemini trả về khớp với cột trong Google Sheet.
- Nếu các sếp muốn thêm cột mới (ví dụ: "Level of Experience"), cần thêm trường này vào schema ở đây và cập nhật prompt của AI Agent.

**F. Node `Update Google Sheet.`**
- **Credentials:** Chọn credential **Google Sheets** (OAuth2).
- **Document ID:** ID của Google Sheet mà các sếp muốn lưu dữ liệu.
- **Sheet Name:** Tên tab trong Sheet (ví dụ: "Jobs").
- **Operation:** Mặc định là `appendOrUpdate`.
  - *Lưu ý:* Workflow thường dùng một trường duy nhất (như Link Job hoặc Job ID) để xác định dòng dữ liệu. Nếu job đã tồn tại, nó sẽ cập nhật; nếu chưa, nó sẽ thêm mới. Hãy đảm bảo cột "Link" hoặc "ID" trong Sheet được dùng làm khóa chính.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Nhấn nút **Execute Workflow** (hoặc chọn một node cụ thể để test từng bước).
   - Kiểm tra output của node `AI Agent` xem dữ liệu đã được tóm tắt đúng ý chưa.
   - Kiểm tra node `Update Google Sheet` xem dữ liệu đã được ghi vào Sheet chưa.
2. **Bật Active:**
   - Nếu chạy theo lịch trình (ví dụ: mỗi 1 giờ), các sếp cần thêm node **Schedule Trigger** thay thế hoặc bổ sung vào đầu workflow.
   - Bật công tắc **Active** ở góc trên bên phải để workflow bắt đầu chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack:** Sau khi có dữ liệu mới, các sếp có thể thêm node `Telegram` hoặc `Slack` để gửi thông báo ngay lập tức khi phát hiện ra một vị trí việc làm "hot" phù hợp với tiêu chí.
- **Lọc theo từ khóa:** Trong node `Pre-clean Before AI` hoặc trước khi gọi AI, các sếp có thể thêm logic để lọc bỏ các job không liên quan (ví dụ: chỉ giữ job có từ "Python" hoặc "Manager" trong tiêu đề).
- **Lưu trữ lịch sử:** Thay vì chỉ cập nhật, các sếp có thể tạo một Sheet riêng để lưu log lịch sử các job đã xem, giúp phân tích xu hướng tuyển dụng theo thời gian.
- **Tự động gửi email:** Nếu tìm được job phù hợp với hồ sơ ứng viên cụ thể, workflow có thể tự động gửi email giới thiệu job đó cho ứng viên.

### 📌 Kết luận
Với workflow **Scrape LinkedIn Jobs with Gemini AI and Store in Google Sheets**, các sếp đã sở hữu một cỗ máy tìm kiếm việc làm thông minh, tự động và chính xác. Thay vì lãng phí thời gian lướt mạng xã hội, hãy để AI làm việc nặng nhọc, còn các sếp tập trung vào việc ra quyết định và đàm phán.

Hãy import workflow, cấu hình API Key và bắt đầu thu thập dữ liệu việc làm chất lượng cao ngay hôm nay! 🚀