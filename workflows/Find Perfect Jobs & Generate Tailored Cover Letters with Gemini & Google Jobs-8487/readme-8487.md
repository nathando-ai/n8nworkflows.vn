---
title: "🚀 Tự động tìm việc và viết Thư xin việc (Cover Letter) chuẩn chỉnh với Gemini & Google Jobs trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa hoàn toàn quy trình phân tích CV, tìm kiếm việc làm qua Google Jobs và viết Cover Letter cá nhân hóa bằng AI Gemini."
slug: "tu-dong-tim-viec-va-viet-cover-letter-voi-gemini-google-jobs"
tags: [n8n, automation, ai, google-gemini, job-search, productivity]
keywords: [n8n workflow, tu dong tim viec, viet cover letter bang ai, google jobs api, gemini pro n8n]
---

# 🚀 Tự động tìm việc và viết Thư xin việc (Cover Letter) chuẩn chỉnh với Gemini & Google Jobs

Việc tìm kiếm công việc mơ ước và viết hàng chục bức thư xin việc (Cover Letter) tùy chỉnh cho từng vị trí là một cơn ác mộng tốn rất nhiều thời gian và công sức. Bạn phải đọc mô tả công việc, nghiên cứu công ty và sửa đổi CV liên tục.

Workflow n8n này sẽ giải quyết triệt để nỗi đau đó bằng cách tự động hóa 100%: Tiếp nhận CV của bạn qua Form, dùng AI (Gemini) kết hợp công cụ tìm kiếm việc làm (SerpAPI - Google Jobs) để chọn ra công việc hoàn hảo nhất, viết sẵn một Cover Letter cực kỳ chuyên nghiệp và gửi thẳng kết quả vào Gmail của bạn. Không cần code, chỉ cần thiết lập một lần và sử dụng mãi mãi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn phải thủ công tìm việc và soạn từng bức thư xin việc riêng lẻ.
- **Cá nhân hóa sâu sắc:** Cover Letter được AI viết dựa trên đúng nội dung CV PDF của bạn và yêu cầu tuyển dụng thực tế.
- **Tự động hoàn toàn:** Nhận kết quả qua email ngay sau khi submit form mà không cần can thiệp thủ công.
- **Hoạt động liên tục 24/7:** Hệ thống sẵn sàng phục vụ bất cứ lúc nào bạn muốn ứng tuyển vị trí mới.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google AI Studio (Gemini) API Key:** Dành cho model Gemini 2.5 Pro xử lý logic ngôn ngữ và viết thư.
- **SerpAPI Key:** Để quét kết quả tìm kiếm việc làm từ Google Jobs.
- **Tài khoản Gmail:** Kết nối qua OAuth2 để workflow gửi email tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ nguồn gốc (tác giả Khairul Muhtadin) hoặc copy/paste trực tiếp JSON vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 9 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:
- **Node `On form submission` (formTrigger):** Node này tạo sẵn một giao diện form web để người dùng upload CV (định dạng PDF) và điền các tiêu chí (địa điểm, mức lương, loại công việc, email nhận kết quả). Các sếp có thể lấy link form này chia sẻ trực tiếp hoặc nhúng vào website cá nhân.
- **Node `Extract CV from PDF` (extractFromFile):** Nhận file PDF từ form và trích xuất toàn bộ văn bản để lưu vào biến `cvData`.
- **Node `Job Hunter Agent` (@n8n/n8n-nodes-langchain.agent):** Node cốt lõi tích hợp AI Agent. Sếp cần kết nối đúng 2 công cụ đi kèm là **SerpAPI** và **Gemini 2.5 Pro**. Prompt hệ thống được cấu hình sẵn để ép AI chỉ trả về **1 kết quả công việc phù hợp nhất** kèm theo Cover Letter dưới dạng JSON cấu trúc.
- **Node `Gemini 2.5 Pro` (lmChatGoogleGemini):** Thêm Credentials `Google Palm / Gemini` bằng API key lấy từ [Google AI Studio](https://aistudio.google.com/).
- **Node `SerpAPI` (toolSerpApi):** Thêm Credentials `SerpAPI` lấy từ trang quản trị SerpAPI để hệ thống quét dữ liệu Google Jobs.
- **Node `Send a message` (gmail):** Cấu hình tài khoản `gmailOAuth2` để gửi email tự động chứa tiêu đề *"Your Job MATCH!"*, thông tin việc làm và Cover Letter đến đúng email người dùng đã điền ở form.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng cách submit một CV mẫu qua Form để kiểm tra dòng dữ liệu từ đầu đến cuối.
- Kiểm tra hộp thư Gmail xem đã nhận được email định dạng HTML đẹp mắt chưa.
- Bật công tắc **Active workflow** ở góc trên bên phải để đưa hệ thống vào trạng thái tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy chỉnh Prompt:** Các sếp có thể chỉnh sửa System Prompt trong node `Job Hunter Agent` để thay đổi giọng văn, độ dài hoặc phong cách của Cover Letter cho phù hợp với cá tính bản thân.
- **Mở rộng nguồn việc làm:** Ngoài SerpAPI (Google Jobs), có thể tích hợp thêm các tool gọi API từ LinkedIn, Indeed hoặc TopCV nếu có key kết nối.
- **Lưu trữ lịch sử:** Thêm một node Google Sheets hoặc Airtable ngay sau bước xử lý agent để lưu lại danh sách các công việc hệ thống đã tìm giúp bạn theo dõi tiến độ ứng tuyển.
- **Nâng cấp LLM:** Có thể thay thế Gemini bằng các model mạnh mẽ khác như GPT-4o hoặc Claude 3.5 Sonnet nếu muốn khả năng lý luận và viết văn bản sắc sảo hơn.

### 📌 Kết luận
Với workflow n8n thông minh này, việc tìm kiếm việc làm và chuẩn bị hồ sơ ứng tuyển không còn là gánh nặng. Hãy cài đặt ngay để tối ưu hóa hành trình sự nghiệp của bạn bằng sức mạnh của AI và tự động hóa!