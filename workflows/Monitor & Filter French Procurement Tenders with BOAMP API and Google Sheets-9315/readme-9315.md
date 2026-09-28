---
title: "🚀 Tự động giám sát và lọc gói thầu Pháp qua BOAMP API với n8n"
description: "Hướng dẫn xây dựng hệ thống tự động cào dữ liệu thầu từ BOAMP (Pháp), lọc theo danh mục, quét nội dung PDF và phân loại từ khóa lưu vào Google Sheets."
slug: "tu-dong-giam-sat-loc-goi-thau-boamp-api-google-sheets"
tags: [n8n, automation, no-code, google-sheets, api-integration, ai-agents]
keywords: [n8n workflow, BOAMP API, lọc gói thầu, tự động hóa đấu thầu, google sheets automation]
keywords: [n8n workflow, BOAMP API, lọc gói thầu, tự động hóa đấu thầu, google sheets automation]
---

# 🚀 Tự động giám sát và lọc gói thầu Pháp qua BOAMP API với n8n

Việc theo dõi thủ công các cổng thông tin mua sắm công (như BOAMP của Pháp) để tìm kiếm các gói thầu phù hợp là một ác mộng tốn thời gian. Các doanh nghiệp thường xuyên bỏ lỡ cơ hội kinh doanh chỉ vì không kịp cập nhật thông tin, hoặc mất hàng giờ đồng hồ mỗi ngày để đọc qua hàng trăm tài liệu PDF dài dằng dặc.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code, giúp các sếp kết nối trực tiếp với BOAMP API, tự động tải tài liệu, phân tích từ khóa bằng bộ lọc thông minh và lưu trữ gọn gàng vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn 24/7:** Không cần thao tác thủ công, hệ thống tự động quét và thu thập dữ liệu thầu mới nhất.
- **Lọc thông minh theo ngành nghề & từ khóa:** Chỉ giữ lại các gói thầu thực sự tiềm năng (Travaux, Services, Fournitures) dựa trên bộ từ khóa tùy chỉnh.
- **Trích xuất nội dung PDF tự động:** Tự động tải file PDF của gói thầu và quét sâu vào bên trong để tìm kiếm từ khóa khớp.
- **Quản lý tập trung trên Google Sheets:** Dữ liệu được phân loại rõ ràng thành các tab (Cấu hình, Tất cả, Mục tiêu cần theo dõi).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản Google Workspace để kết nối Google Sheets (sử dụng Google Sheets OAuth2 API).
- Bản sao Google Sheets Template cấu hình sẵn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n hoặc copy toàn bộ mã nguồn JSON, sau đó dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần thực hiện cấu hình các thành phần sau để hệ thống chạy mượt mà:

- **Phase 0 (Google Sheets Template):** 
  - Truy cập [Google Sheets Template](https://docs.google.com/spreadsheets/d/1wapLLWjwzo7SfG_YEsUlFaPRs1MmjxPRhRc6BlwBUAY/edit?gid=966659321#gid=966659321) và chọn **File → Make a copy** về Drive cá nhân.
  - Cấu hình các tab: `Config` (chọn loại thị trường, thời gian quét theo ngày, danh sách từ khóa), tab lưu dữ liệu (`All` và `Target`).
- **Các node Google Sheets (`Get config`, `Get All`, `Append row in sheet`, v.v.):** 
  - Chọn lại Credentials (`googleSheetsOAuth2Api`) của các sếp.
  - Cập nhật lại `Spreadsheet ID` và trỏ đúng tên các Sheet/Tab tương ứng.
- **Schedule Trigger / Schedule Trigger1:** 
  - Cấu hình thời gian chạy tự động (Mặc định: Ngày đầu tiên của mỗi tháng lúc 8:00 AM, hoặc chỉnh lại theo nhu cầu hàng ngày).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Test step / Execute workflow**) với một vài bản ghi mẫu để kiểm tra kết quả trả về trong Google Sheets.
- Bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo tức thì:** Nối thêm node Telegram hoặc Slack sau bước *Save Matching Tenders to Target Sheet* để nhận thông báo ngay khi có gói thầu phù hợp.
- **Sử dụng AI Agent:** Thay thế hoặc bổ sung node lọc từ khóa thông thường bằng OpenAI/Anthropic Node để phân tích sâu hơn độ phù hợp của gói thầu đối với năng lực công ty.
- **Ghi log lỗi:** Thêm nhánh Error Trigger để gửi cảnh báo về email hoặc chat nếu API BOAMP gặp sự cố gián đoạn.

### 📌 Kết luận
Với workflow n8n này, đội ngũ của các sếp sẽ tiết kiệm hàng chục giờ đồng hồ mỗi tuần, không bỏ lỡ bất kỳ cơ hội thầu công nào tại thị trường Pháp. Hãy triển khai ngay hôm nay để tối ưu hóa quy trình kinh doanh của mình!