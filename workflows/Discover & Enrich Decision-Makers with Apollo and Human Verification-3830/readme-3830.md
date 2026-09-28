---
title: "🚀 Tự Động Khám Phá & Làm Giàu Dữ Liệu Người Ra Quyết Định Với Apollo, AI và Slack trong n8n"
description: "Xây dựng hệ thống tự động tìm kiếm công ty, lọc người ra quyết định (CEO, CTO, VP...) từ Apollo.io, xác thực bằng AI và duyệt qua Slack hoàn toàn tự động."
slug: "tu-dong-kham-pha-nguoi-ra-quyet-dinh-apollo-ai-n8n"
tags: [n8n, automation, apollo, ai, openai, google-sheets, slack, sales-automation]
keywords: [n8n workflow, apollo enrichment, tim kiem lead b2b, tu dong hoa sales, openAI n8n, slack approval]
---

# 🚀 Tự Động Khám Phá & Làm Giàu Dữ Liệu Người Ra Quyết Định Với Apollo, AI và Slack

Các đội ngũ Sales và Growth B2B thường tốn hàng giờ đồng hồ mỗi tuần để lên danh sách công ty, tìm kiếm website chính xác, săn tìm thông tin người ra quyết định (CEO, COO, CTO, Director) trên Apollo.io và cập nhật thủ công vào Google Sheets. Việc này vừa chậm chạp, dễ sai sót lại vừa lãng phí nhân lực.

Bài viết này sẽ hướng dẫn các sếp triển khai một **n8n workflow 25 nodes cực kỳ mạnh mẽ**, tự động hóa toàn bộ quy trình: từ việc nhận dữ liệu tên công ty đầu vào, tìm website, kiểm duyệt qua Slack (Human-in-the-Loop), khai thác thông tin từ Apollo, sử dụng OpenAI để phân loại phòng ban/tóm tắt doanh nghiệp, cho đến việc lưu trữ vào Google Sheets và báo cáo hàng tuần qua Slack!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% phễu Lead Gen B2B**: Từ tên công ty thô biến thành danh sách người ra quyết định (có email, LinkedIn, số điện thoại) đã được xác thực.
- **Tích hợp Human-in-the-Loop thông minh**: Dùng Slack để duyệt website doanh nghiệp trước khi gọi API, đảm bảo độ chính xác tuyệt đối.
- **Sức mạnh AI (OpenAI)**: Tự động tóm tắt mô hình kinh doanh cốt lõi và phân loại phòng ban của nhân sự dựa trên chức vụ.
- **Báo cáo định kỳ tự động**: Gửi thống kê số lượng lead chất lượng cao được tạo ra trong tuần thẳng vào kênh Slack của đội ngũ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance** (Cloud hoặc Self-hosted bản mới nhất).
- **Apollo.io Account & API Key**: Dùng cho Organization/People Search & Enrichment.
- **OpenAI API Key**: Dùng cho các node xử lý LLM (Summarize Core Business, Determine Department).
- **Google Sheets Template**: Chuẩn bị sẵn file Google Sheets (Tham khảo [Template Google Sheets mẫu](https://docs.google.com/spreadsheets/d/1KqKFZ7Uxrt1MivBjLklGdPRMgNBhEc0slpthoSjt2wI/edit?gid=0#gid=0) và cài đặt Apps Script theo hướng dẫn trong sheet).
- **Slack Workspace**: Cần kết nối để nhận thông báo duyệt website (`Approve Company Website`) và gửi báo cáo hàng tuần (`Send Weekly Report`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow (hoặc lấy từ nguồn gốc ID 3830), sau đó trong giao diện n8n Editor, chọn **Add workflow** -> Nhấn vào biểu tượng menu (dấu ba chấm) -> **Import from File** và chọn file JSON tương ứng.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow vận hành trơn tru, các sếp cần cấu hình chính xác các node sau:
- **Google Sheets Trigger**: Chọn đúng file Google Sheets quản lý lead của các sếp và trỏ tới tab `Companies`. Workflow sẽ kích hoạt ngay khi một dòng mới được thêm hoặc cập nhật.
- **Approve Company Website (Slack)**: Cấu hình tính năng `Send and Wait`. Node này sẽ gửi thông tin website công ty lên Slack để nhân sự kiểm tra, chỉnh sửa (nếu cần) và bấm nút phê duyệt trước khi bước sang các bước tìm kiếm tiếp theo.
- **Apollo Organization Search & Enrichment / Find Decision Makers / Enrich Decision Makers (HTTP Request)**: Nhập Apollo API Key vào phần Credentials của các node này để hệ thống gọi API truy xuất dữ liệu doanh nghiệp và nhân sự hàng loạt (batching 1,000 domain/lần).
- **Summarize Core Business & Determine Contact's Department (OpenAI)**: Kết nối OpenAI Credentials và kiểm tra lại Model (khuyên dùng `gpt-4o-mini` hoặc `gpt-4o`) để đảm bảo việc phân tích nội dung công ty và phòng ban nhân sự diễn ra mượt mà, chính xác.
- **Add Contacts / Enrich Contacts / Add Company Website (Google Sheets)**: Map chính xác các cột dữ liệu tương ứng giữa output của n8n và các cột trong Google Sheet của các sếp (sử dụng tính năng `appendOrUpdate`).
- **Send Weekly Report (Slack)** & **Weekly Report Trigger (Schedule Trigger)**: Cấu hình lịch chạy định kỳ (ví dụ: Thứ Hai hàng tuần) và chọn kênh Slack nhận báo cáo tổng kết lead.

#### 3. Kích hoạt ⚡️
- Thử nghiệm chạy dòng dữ liệu mẫu (Test step/Test execution) trên một vài dòng công ty ở Google Sheet để kiểm tra toàn bộ luồng.
- Sau khi test thành công, gạt công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Đẩy Lead sang CRM**: Thay vì chỉ dừng lại ở Google Sheets, các sếp có thể gắn thêm node **HubSpot**, **Salesforce** hoặc **Pipedrive** ngay sau bước lọc lead đã xác thực để đồng bộ thẳng vào hệ thống CRM của công ty.
- **Tích hợp Email Outreach**: Kết nối kết quả lead đã được enrich vào các công cụ như Instantly, Lemlist hoặc ném thẳng vào node **Gmail** để chạy chuỗi email cold outreach tự động.
- **Mở rộng kênh thông báo**: Ngoài Slack, có thể cấu hình gửi thêm cảnh báo hoặc báo cáo tóm tắt qua **Telegram Bot** để tiện theo dõi trên điện thoại di động.

### 📌 Kết luận
Workflow "Discover & Enrich Decision-Makers with Apollo and Human Verification" là một mảnh ghép hoàn hảo cho bất kỳ đội ngũ Sales B2B nào muốn tối ưu hóa quy trình tìm kiếm khách hàng tiềm năng. Kết hợp giữa dữ liệu mạnh mẽ của Apollo, trí tuệ nhân tạo của OpenAI và sự kiểm soát của con người qua Slack, các sếp sẽ tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần. Triển khai ngay thôi nào!