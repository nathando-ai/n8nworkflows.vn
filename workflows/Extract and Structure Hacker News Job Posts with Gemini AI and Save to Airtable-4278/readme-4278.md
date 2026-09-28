---
title: "🚀 Tự động trích xuất và phân loại tuyển dụng Hacker News với Gemini AI & Airtable"
description: "Hướng dẫn xây dựng workflow n8n tự động quét bài đăng tuyển dụng trên Hacker News, sử dụng Gemini AI để cấu trúc hóa dữ liệu và lưu trữ trực tiếp vào Airtable."
slug: "tu-dong-trich-xuat-tuyen-dung-hacker-news-gemini-ai-airtable"
tags: [n8n, automation, no-code, gemini-ai, airtable, hacker-news]
keywords: [n8n workflow, trích xuất tuyển dụng, hacker news automation, gemini ai n8n, airtable integration, tự động hóa hr]
---

# 🚀 Tự động trích xuất và phân loại tuyển dụng Hacker News với Gemini AI & Airtable

Các sếp làm trong lĩnh vực Nhân sự (HR) hay Săn đầu người (Headhunter) có bao giờ thấy mệt mỏi khi phải thủ công lướt qua hàng trăm bình luận tuyển dụng "Who is hiring?" trên Hacker News mỗi tháng? Việc copy-paste thông tin công ty, vị trí, công nghệ, hình thức làm việc vào Excel không chỉ tốn hàng giờ đồng hồ mà còn dễ bỏ sót những cơ hội ngon ăn.

Giải pháp đây rồi! Workflow n8n này sẽ tự động hóa từ A-Z: quét dữ liệu từ Hacker News, dùng sức mạnh của **Google Gemini AI** để phân tách thông tin thành các trường dữ liệu gọn gàng, và đẩy thẳng vào **Airtable** để các sếp dễ dàng quản lý, lọc và tìm kiếm. Không cần viết code phức tạp, tự động 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần thủ công copy từng job post nữa, mọi thứ diễn ra tự động theo lịch hẹn.
- **Dữ liệu cấu trúc chuẩn xác:** Gemini AI đọc hiểu văn bản thô (raw text) và trả về dữ liệu chuẩn JSON (vị trí, công nghệ, mức lương, remote/onsite...).
- **Lưu trữ chuyên nghiệp:** Toàn bộ thông tin được đồng bộ trực tiếp vào bảng Airtable sẵn sàng cho team HR khai thác.
- **Vận hành tự động 24/7:** Chạy ngầm định kỳ nhờ `Schedule Trigger`, không lo bỏ lỡ bài đăng mới.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Gemini API Key:** Dùng để cấu hình cho model AI đọc và phân tích text.
- **Airtable Account:** Tạo sẵn một Base/Table với các trường (fields) phù hợp để lưu thông tin tuyển dụng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này (hoặc tải file JSON từ nguồn gốc) và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm các node chính sau cần cấu hình cẩn thận:

- **`Schedule Trigger`**: Thiết lập lịch chạy tự động (ví dụ: chạy định kỳ hàng tháng khi Hacker News đăng bài "Who is hiring?").
- **`HN API: Get Main Post` & `HI API: Get the individual job post` & `Search for Who is hiring posts`**: Các node `httpRequest` gọi API công khai của Hacker News để lấy dữ liệu bài viết gốc và các bình luận tuyển dụng. Kiểm tra lại đường dẫn API endpoint nếu cần.
- **`Clean text` & `Code`**: Các node xử lý dữ liệu thô, lọc bỏ các thẻ HTML hoặc ký tự rác trước khi ném vào AI.
- **`Google Gemini Chat Model` & `Trun into structured data` (Chain LLM)**: 
  - Kết nối Credentials cho **Google Gemini (Google Palm API)**.
  - Cấu hình Prompt trong node AI để hướng dẫn Gemini cách trích xuất dữ liệu (Công ty, Vị trí, Tech Stack, Link, Hình thức Remote...).
- **`Structured Output Parser`**: Đảm bảo cấu trúc đầu ra khớp với các trường dữ liệu mà các sếp muốn lưu.
- **`Limit for testing (optional)`**: Khi mới test workflow, hãy bật node Limit này (ví dụ: chỉ lấy 3-5 job posts) để tránh tốn quota API của Gemini và test lỗi nhanh hơn.
- **`Write results to airtable`**: 
  - Chọn Credentials loại `airtableTokenApi`.
  - Chọn đúng `Base` và `Table` đã chuẩn bị sẵn trên Airtable của các sếp, sau đó map các trường dữ liệu từ AI output vào các cột tương ứng trong Airtable.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** chạy thử với số lượng giới hạn ở node `Limit` để kiểm tra kết quả đổ về Airtable.
- Nếu mọi thứ mượt mà, gạt công tắc **Active** góc trên bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack ở cuối workflow để mỗi khi quét xong và lưu Airtable, bot sẽ gửi thông báo tóm tắt số lượng job mới về group chat cho team.
- **Lọc thông minh:** Thêm node `Filter` để chỉ lưu các job có chứa từ khóa công nghệ mà team quan tâm (ví dụ: `React`, `Python`, `Node.js`, `Remote`).
- **Gửi Email tự động:** Cấu hình tự động gửi email cho ứng viên tiềm năng hoặc chia sẻ danh sách job hàng tuần cho các thành viên trong team HR.

### 📌 Kết luận
Với workflow n8n kết hợp Gemini AI này, việc tổng hợp thị trường tuyển dụng công nghệ trên Hacker News trở nên dễ dàng hơn bao giờ hết. Chúc các sếp "lên đồ" thành công và tự động hóa thành công quy trình HR của mình!