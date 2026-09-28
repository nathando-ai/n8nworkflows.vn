---
title: "🚀 Tự động tìm kiếm và xác thực hồ sơ LinkedIn chuẩn xác với Airtop"
description: "Hướng dẫn xây dựng workflow n8n tự động tìm kiếm thông qua Google và xác thực tài khoản LinkedIn chính chủ bằng AI Browser Automation của Airtop."
slug: "tu-dong-tim-kiem-va-xac-thuc-ho-so-linkedin-voi-airtop"
tags: [n8n, automation, airtop, linkedin, sales-automation, lead-generation]
keywords: [n8n workflow, tìm kiếm linkedin tự động, xác thực profile linkedin, airtop api, automation sales]
---

# 🚀 Tự động tìm kiếm và xác thực hồ sơ LinkedIn chuẩn xác với Airtop

Việc tìm kiếm và xác thực chính xác profile LinkedIn của khách hàng tiềm năng hoặc ứng viên là bước sống còn trong các chiến dịch Sales Prospecting hay Recruitment. Tuy nhiên, việc tra cứu thủ công từng người trên Google rồi bấm vào check profile mất rất nhiều thời gian và dễ xảy ra nhầm lẫn do trùng tên.

Workflow n8n này sẽ giải quyết triệt để nỗi đau đó bằng cách tự động hóa 100% quy trình: Nhận thông tin nhân sự 👉 Tìm kiếm trên Google 👉 Điều hướng và kiểm tra chéo lịch sử kinh nghiệm bằng AI Browser của Airtop 👉 Trả về link LinkedIn chính xác nhất. Không cần code, hoạt động hoàn toàn tự động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Thay vì phải tra cứu thủ công từng người, hệ thống tự động hóa hoàn toàn quy trình tìm kiếm và lọc kết quả.
- **Độ chính xác cao:** Không chỉ dừng lại ở việc lấy link Google Search, workflow còn dùng Airtop để truy cập trực tiếp vào profile, đối chiếu kinh nghiệm và thông tin để xác thực "chính chủ".
- **Linh hoạt đầu vào:** Có thể kích hoạt thông qua Form nhập liệu trực tiếp hoặc gọi tự động từ một workflow khác (như danh sách từ CRM/Google Sheets).
- **Hoạt động liên tục 24/7:** Sẵn sàng sàng lọc hàng trăm leads mỗi ngày mà không lo bị chặn hayCAPTCHA nhờ công nghệ browser automation thông minh của Airtop.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã sẵn sàng để import workflow.
- **Airtop API Key:** Lấy tại [Airtop Portal API Keys](https://portal.airtop.ai/api-keys).
- **Airtop Profile (Khuyên dùng):** Một Profile trình duyệt trên Airtop đã đăng nhập sẵn tài khoản LinkedIn ([Airtop Browser Profiles](https://portal.airtop.ai/browser-profiles)) để có thể xem chi tiết profile mà không bị LinkedIn chặn đăng nhập.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã nguồn JSON.
- Trong giao diện n8n Editor, bấm vào **Add workflow** -> Dọn dẹp canvas hoặc chọn dấu `...` ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các thành phần sau để workflow chạy mượt mà:

- **Node `Search Profile URL` (Airtop):** 
  - Kết nối `airtopApi` credentials bằng API Key của các sếp.
  - Kiểm tra lại Prompt trích xuất, hệ thống đang dùng lệnh AI để phân tích kết quả Google Search và trả về URL LinkedIn hoặc chữ `NA` nếu không tìm thấy.
- **Node `Verify Profile URL` (Airtop):** 
  - Sử dụng chung `airtopApi` credentials.
  - Node này sẽ điều hướng trực tiếp vào trang LinkedIn tìm được, đối chiếu lịch sử làm việc với thông tin đầu vào (`Person_info`) để chắc chắn đây đúng là người cần tìm.
- **Node `Unify Parameters` (Set) & `Is valid Linkedin link?` (Filter):** 
  - Kiểm tra logic lọc dữ liệu để đảm bảo chỉ những link hợp lệ (khác `NA`) mới được chuyển tiếp tới các bước tiếp theo trong hệ thống của các sếp.
- **Triggers (`On form submission` hoặc `When Executed by Another Workflow`):** 
  - Chọn cách kích hoạt phù hợp: Dùng Form nếu muốn nhập tay từng người, hoặc cấu hình chạy ngầm khi nhận data từ các workflow khác.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử nhập một thông tin mẫu (ví dụ: *"Elon Musk Tesla CEO"*) để test xem Airtop tìm kiếm và trả về kết quả ra sao.
- Sau khi test thành công, gạt công tắc sang **Active** để đưa workflow vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Email Lookup:** Đưa workflow này vào quy trình làm giàu dữ liệu (Data Enrichment), kết hợp với các công cụ tìm email ở bước trước đó.
- **Tích hợp CRM:** Nối tiếp node Filter bằng node HubSpot, Pipedrive hoặc Google Sheets để tự động cập nhật link LinkedIn đã xác thực vào hồ sơ khách hàng.
- **Tự động hóa Outreach:** Sau khi có profile LinkedIn đã xác thực, có thể đẩy tiếp dữ liệu sang các công cụ tự động gửi kết bạn/nhắn tin để tối ưu hóa phễu Sales.

### 📌 Kết luận
Tự động hóa việc tìm kiếm và xác thực LinkedIn với Airtop giúp đội ngũ Sales và tuyển dụng tiết kiệm hàng đống thời gian, loại bỏ các profile giả mạo hoặc nhầm lẫn tên tuổi. Hãy import workflow này ngay hôm nay để nâng cấp hệ thống prospecting của doanh nghiệp lên một tầm cao mới!