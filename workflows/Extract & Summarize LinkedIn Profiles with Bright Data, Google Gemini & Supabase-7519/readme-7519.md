---
title: "🚀 Tự động trích xuất và tóm tắt hồ sơ LinkedIn với Bright Data, Google Gemini và Supabase"
description: "Xây dựng hệ thống tự động hóa thông minh giúp cào dữ liệu profile LinkedIn, phân tích và tóm tắt chuyên sâu bằng AI Gemini, sau đó lưu trữ gọn gàng vào cơ sở dữ liệu Supabase."
slug: "tu-dong-trich-xuat-va-tom-tat-ho-so-linkedin-bright-data-gemini-supabase"
tags: [n8n, automation, ai-summarization, bright-data, google-gemini, supabase]
keywords: [n8n workflow, cào linkedin tự động, bright data n8n, google gemini ai extraction, supabase automation]
---

# 🚀 Tự động trích xuất và tóm tắt hồ sơ LinkedIn bằng AI & n8n

Việc thu thập thông tin ứng viên, đối tác hay khách hàng tiềm năng từ LinkedIn theo cách thủ công (copy-paste từng profile, đọc lướt qua kinh nghiệm, kỹ năng rồi lưu vào Excel) cực kỳ tốn thời gian và nhàm chán. Đặc biệt với các đội ngũ tuyển dụng (HR) hoặc sales B2B, việc này làm giảm năng suất đáng kể.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code. Hệ thống sẽ tiếp nhận link LinkedIn, sử dụng **Bright Data** để cào dữ liệu, giao cho **Google Gemini AI** phân tích bóc tách thông tin chi tiết (kỹ năng, kinh nghiệm, vai trò nổi bật...) và cuối cùng lưu trữ toàn bộ có hệ thống vào **Supabase**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Chỉ cần gửi yêu cầu qua Webhook, hệ thống tự động cào và xử lý dữ liệu profile LinkedIn mà không cần can thiệp thủ công.
- **Phân tích thông minh bằng AI:** Tận dụng sức mạnh của Google Gemini để tóm tắt profile, trích xuất kỹ năng, kinh nghiệm và nhận diện vai trò tiềm năng một cách chính xác.
- **Lưu trữ dữ liệu chuẩn hóa:** Quản lý thông tin hồ sơ tập trung, an toàn trên cơ sở dữ liệu Supabase, hỗ trợ kiểm tra xem bản ghi đã tồn tại hay chưa để tránh trùng lặp.
- **Phản hồi tức thì:** Tích hợp các node `Respond to Webhook` trả về kết quả nhanh chóng cho ứng dụng gọi API.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Bright Data:** Lấy API Key/Credentials để sử dụng dịch vụ cào dữ liệu LinkedIn (`Access and extract data from a specific URL`).
- **Google Gemini API Key:** Cần thiết cho các node LangChain Chat Model của Gemini (`Google Gemini Chat Model for Summarization`, `Skill Extraction`, v.v.).
- **Supabase Project:** Tạo sẵn một bảng (table) trên Supabase để lưu trữ thông tin profile (`Create a row`, `Get a row`, `Update Row`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ n8n hoặc copy trực tiếp mã nguồn JSON, sau đó paste vào giao diện n8n Editor của các sếp qua tính năng **Import from JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Khi các sếp mở workflow lên, hãy chú ý cấu hình các thành phần sau:
- **Webhook Node (`Webhook`):** Điểm đầu vào nhận URL profile LinkedIn cần xử lý. Hãy cấu hình đường dẫn (Path) và phương thức (POST/GET) phù hợp với hệ thống của sếp.
- **Bright Data Node (`Access and extract data from a specific URL`):** Thiết lập thông tin kết nối/Credentials tài khoản Bright Data để hệ thống có quyền cào dữ liệu từ LinkedIn.
- **Google Gemini Chat Models:** Các node như `Google Gemini Chat Model for Skill Extraction`, `Summarization`, `Basic Profile Info`,... đều yêu cầu Google Gemini API Credentials. Các sếp nhớ tạo API key từ Google AI Studio và điền vào.
- **Supabase Nodes (`Create a row`, `Get a row`, `Update Row`):** Kết nối với dự án Supabase của các sếp, chọn đúng bảng (Table) lưu trữ dữ liệu ứng viên/profile đã chuẩn bị trước đó.
- **Các node điều kiện (`If record exist`, `If force create?`, `If status code <> 200`):** Kiểm tra kỹ logic nhánh (Branching) để đảm bảo hệ thống xử lý đúng trường hợp profile đã tồn tại trong cơ sở dữ liệu hay cần tạo mới.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một request mẫu chứa URL LinkedIn qua Webhook để test thử luồng chạy.
- Sau khi kiểm tra dữ liệu trả về và ghi nhận thành công trên Supabase, gạt công tắc sang **Active** để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack ở cuối luồng để gửi thông báo ngay lập tức cho team tuyển dụng/sales khi một profile LinkedIn mới được phân tích xong.
- **Báo cáo định kỳ:** Kết hợp thêm Google Sheets hoặc Email node để tổng hợp danh sách các profile đã phân tích gửi về inbox vào cuối tuần.
- **Xử lý hàng loạt (Batching):** Nếu các sếp muốn cào danh sách lớn, hãy kết hợp thêm node Split In Batches để tránh vượt quá giới hạn Rate Limit của Bright Data và Gemini API.

### 📌 Kết luận
Workflow "Extract & Summarize LinkedIn Profiles with Bright Data, Google Gemini & Supabase" là một cỗ máy tự động hóa mạnh mẽ giúp tiết kiệm hàng tá giờ làm việc thủ công. Hãy áp dụng ngay vào quy trình của các sếp để tối ưu hóa năng suất và nâng tầm chuyên nghiệp!