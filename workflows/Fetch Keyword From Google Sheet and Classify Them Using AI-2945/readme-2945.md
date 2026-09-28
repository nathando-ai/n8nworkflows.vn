---
title: "🚀 Tự động phân loại từ khóa SEO bằng AI và Google Sheets với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy danh sách từ khóa từ Google Sheets, sử dụng AI Agent (OpenAI) để phân loại và cập nhật kết quả ngược lại Google Sheets một cách thông minh."
slug: "tu-dong-phan-loai-tu-khoa-seo-ai-google-sheets-n8n"
tags: [n8n, automation, no-code, seo, ai, google-sheets]
keywords: [n8n workflow, phân loại từ khóa seo, ai agent, openai gpt-4o-mini, google sheets automation]
---

# 🚀 Tự động phân loại từ khóa SEO bằng AI và Google Sheets với n8n

Việc nghiên cứu và phân loại hàng ngàn từ khóa (keywords) thủ công cho các chiến dịch SEO là một "cực hình" tốn rất nhiều thời gian và dễ xảy ra sai sót. Làm sao để phân nhóm từ khóa theo chủ đề, ý định tìm kiếm (Search Intent) hay độ khó một cách nhanh chóng mà không cần tốn hàng giờ đồng hồ xử lý Excel?

Giải pháp chính là đây! Workflow n8n này sẽ giúp các sếp tự động hóa toàn bộ quy trình: lấy danh sách từ khóa từ Google Sheets, giao cho trợ lý AI (OpenAI) phân tích và tự động ghi kết quả phân loại chuẩn chỉnh quay lại Google Sheets. Hoàn toàn tự động 100% và không cần viết code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn phải lọc, gắn nhãn từng từ khóa bằng tay trên bảng tính.
- **Phân loại thông minh & chính xác:** Sử dụng sức mạnh của OpenAI GPT-4o-mini để hiểu sâu ngữ nghĩa và ý định tìm kiếm của từng từ khóa.
- **Xử lý mượt mà số lượng lớn:** Chia nhỏ batch và có độ trễ (delay) thông minh giúp tránh tuyệt đối lỗi quá tải API (Rate Limiting).
- **Đồng bộ hóa tức thì:** Kết quả phân loại được cập nhật thẳng vào Google Sheets theo thời gian thực.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Bản Cloud hoặc Self-hosted đều được.
- **Tài khoản Google Sheets & Google Drive:** Chứa file danh sách từ khóa cần phân loại.
- **OpenAI API Key:** Để kết nối với mô hình ngôn ngữ AI phân tích dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ trang chính thức của n8n (hoặc sử dụng mã JSON mẫu) và chọn **Import from File** hoặc **Paste Workflow** trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần cấu hình các node quan trọng sau:

- **Node `Fetch Keywords from Sheet` (Google Sheets):** 
  - Chọn **Credentials** kết nối tài khoản Google của sếp.
  - Chỉ định đúng **Document [ID]** và **Sheet Name** chứa danh sách từ khóa thô cần phân tích.
- **OpenAI Chat Model & AI Agent:**
  - Kết nối **OpenAI API Credentials**.
  - Thiết lập model là `gpt-4o-mini` (hoặc model tùy chọn khác) để tiết kiệm chi phí mà vẫn đảm bảo độ thông minh.
  - Viết câu lệnh (Prompt) trong AI Agent hướng dẫn rõ ràng cách phân loại từ khóa (Ví dụ: phân loại theo nhóm chủ đề, Search Intent: Informational, Transactional...).
- **Node `Structured Output Parser`:**
  - Đảm bảo định dạng đầu ra của AI trả về đúng cấu trúc JSON mà các sếp mong muốn để dễ dàng map dữ liệu vào bảng tính.
- **Node `Process Keywords in Batches` & `Prevent API Rate Limiting`:**
  - Điều chỉnh số lượng từ khóa mỗi batch (ví dụ: 10-20 từ khóa/lần) và thời gian chờ (Wait) phù hợp để không bị OpenAI khóa giới hạn request (Rate Limit).
- **Node `Update Sheet with Analysis Results` (Google Sheets):**
  - Cấu hình operation là `update`.
  - Map các trường dữ liệu kết quả từ AI Agent vào đúng các cột tương ứng trên Google Sheets của sếp.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** để chạy thử với vài dòng dữ liệu đầu tiên, kiểm tra kết quả trả về trong Google Sheets.
- Sau khi mọi thứ chạy mượt mà, gạt công tắc sang **Active** để hoàn tất quá trình tự động hóa.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp thông báo Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay cho sếp khi AI đã phân loại xong toàn bộ danh sách từ khóa.
- **Tự động hóa theo lịch:** Thay thế node `When clicking ‘Test workflow’` bằng `Schedule Trigger` để workflow tự động quét và phân loại từ khóa mới vào mỗi đầu tuần hoặc đầu tháng.
- **Mở rộng trường dữ liệu:** Yêu cầu AI Agent trả về thêm độ khó ước tính, gợi ý tiêu đề bài viết (Content Title) dựa trên từ khóa vừa phân loại.

### 📌 Kết luận
Workflow "Fetch Keyword From Google Sheet and Classify Them Using AI" là một trợ thủ đắc lực cho bất kỳ marketer hay SEOer nào muốn tối ưu hóa hiệu suất làm việc bằng AI. Hãy cài đặt ngay hôm nay để giải phóng bản thân khỏi những tác vụ lặp đi lặp lại!