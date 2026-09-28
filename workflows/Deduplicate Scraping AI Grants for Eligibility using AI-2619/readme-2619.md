---
title: "🚀 Tự động săn và lọc học bổng, tài trợ AI mỗi ngày bằng n8n & OpenAI"
description: "Hướng dẫn xây dựng hệ thống tự động quét, loại bỏ trùng lặp, phân tích điều kiện bằng AI và gửi email thông báo học bổng/tài trợ AI qua n8n."
slug: "tu-dong-san-va-loc-hoc-bong-tai-tro-ai-bang-n8n"
tags: [n8n, automation, ai, openai, airtable, gmail]
keywords: [n8n workflow, tự động hóa tài trợ, săn học bổng AI, openai information extractor, airtable n8n]
---

# 🚀 Tự động săn và lọc học bổng, tài trợ AI mỗi ngày bằng n8n & OpenAI

Chào các sếp! Việc tìm kiếm các khoản tài trợ (grants) hay học bổng trong lĩnh vực AI thủ công ngốn rất nhiều thời gian của đội ngũ: từ việc cào dữ liệu, kiểm tra xem đã xem qua chưa, cho đến việc đọc hiểu hàng tá tiêu chí phức tạp để xem doanh nghiệp có đủ điều kiện hay không. 

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực đỉnh do chuyên gia **Jimleuk** thiết kế, giúp tự động hóa 100% quy trình từ quét dữ liệu, dùng AI phân tích, lưu trữ vào Airtable và gửi email bản tin (newsletter) cho đội ngũ hoặc khách hàng vào mỗi sáng!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ treo, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hoàn toàn**: Chạy ngầm mỗi ngày vào buổi sáng, mang thông tin tài trợ mới tinh đặt thẳng vào hòm thư đội ngũ trước giờ làm việc.
- **Loại bỏ trùng lặp thông minh**: Sử dụng node `Remove Duplicates` theo dõi xuyên suốt các lần chạy (executions), đảm bảo không bao giờ gửi 1 khoản tài trợ 2 lần.
- **AI thông minh phân tích điều kiện**: Tự động trích xuất tóm tắt và đánh giá các yếu tố đủ điều kiện (eligibility factors) dựa trên ngữ cảnh công ty các sếp cung cấp.
- **Quản lý tập trung**: Lưu trữ toàn bộ dữ liệu sạch lên Airtable và tự động soạn thảo email dạng HTML đẹp mắt gửi qua Gmail.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **OpenAI API Key** (Dùng cho các node LLM phân tích dữ liệu).
- **Airtable Account** (Tạo database lưu trữ grants và danh sách subscribers).
- **Gmail Account** (Hoặc dịch vụ email tùy ý hỗ trợ SMTP/OAuth2 để gửi bản tin).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc import file JSON tải về từ trang chủ n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần chú ý cấu hình các node quan trọng sau:

- **Schedule Trigger (`Everyday @ 9am` & `Everyday @ 8.30am`)**: 
  - Điều chỉnh mốc thời gian kích hoạt tự động vào buổi sáng phù hợp với múi giờ làm việc của đội ngũ.
- **AI Grants since Yesterday & Get Grant Details (`httpRequest`)**: 
  - Cấu hình endpoint API nguồn cấp dữ liệu tài trợ (mặc định lấy từ các nguồn như grants.gov theo danh mục "AI"). Các sếp có thể thay đổi endpoint này sang nguồn lead hoặc dữ liệu khác tùy nhu cầu.
- **Only New Grants (`removeDuplicates`)**: 
  - Node này cực hay, chọn cơ chế `Remove Items Seen in Previous Executions` dựa trên ID của khoản tài trợ để lọc sạch các tin cũ đã xử lý ở các ngày trước.
- **Summarize Synopsis & Eligibility Factors (`informationExtractor`) & OpenAI Chat Model**: 
  - Kết nối credentials `OpenAI API`. 
  - **Mẹo quan trọng**: Cần bổ sung thông tin chi tiết về công ty của các sếp vào **System Prompt** của các node AI này để AI có cơ sở đối chiếu chính xác liệu công ty có đủ điều kiện nhận tài trợ hay không.
- **Save to Tracker & Get New Eligible Grants Today & Get Subscribers (`airtable`)**: 
  - Kết nối tài khoản Airtable bằng `Airtable Token API`. 
  - Các sếp nên copy mẫu Airtable tại đây để đồng bộ cấu trúc: [Airtable Template Mẫu](https://airtable.com/appiNoPRvhJxz9crl/shrRdP6zstgsxjDKL).
- **Generate Email (`html`)**: 
  - Tùy chỉnh template HTML bản tin theo ý thích để hiển thị danh sách các khoản tài trợ mới một cách bắt mắt, chuyên nghiệp nhất.
- **Send Subscriber Email (`gmail`)**: 
  - Kết nối credentials `Gmail OAuth2` để hệ thống tự động quét danh sách người nhận từ Airtable và gửi email hàng loạt.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử thủ công một lần với dữ liệu mẫu để kiểm tra kết nối các API (OpenAI, Airtable, Gmail).
- Nếu mọi thứ xanh mướt, hãy bật công tắc **Active** ở góc trên bên phải để workflow tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm ChatOps**: Nối thêm node **Telegram** hoặc **Slack** sau bước lọc AI thành công để bắn tin nhắn nhanh vào nhóm chat nội bộ, giúp team nắm bắt cơ hội ngay lập tức.
- **Mở rộng nguồn dữ liệu**: Không chỉ giới hạn ở tài trợ AI, các sếp có thể biến template này thành hệ thống tự động quét báo chí, đối thủ cạnh tranh, hoặc các nguồn tìm kiếm khách hàng tiềm năng (Leads Generation) khác.
- **Lưu log lỗi**: Thêm nhánh Error Trigger để gửi cảnh báo về Telegram cá nhân nếu có lỗi phát sinh trong quá trình gọi OpenAI API hoặc Airtable.

### 📌 Kết luận
Workflow tự động hóa kết hợp giữa n8n, OpenAI và Airtable này là giải pháp hoàn hảo giúp doanh nghiệp tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần trong việc săn học bổng, tài trợ hoặc tìm kiếm thông tin thị trường. Triển khai ngay trên VPS của các sếp để tối ưu hóa hiệu suất làm việc ngay hôm nay!