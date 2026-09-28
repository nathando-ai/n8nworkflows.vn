---
title: "🚀 Tự động quét Lead doanh nghiệp địa phương, chấm điểm AI và gửi Cold Email với n8n"
description: "Xây dựng hệ thống tìm kiếm khách hàng tiềm năng tự động từ Google Maps, làm giàu dữ liệu bằng Decodo & OpenAI, sau đó gửi email cá nhân hóa qua Gmail."
slug: "tu-dong-quet-lead-doanh-nghiep-dia-phuong-decodo-openai-gmail"
tags: [n8n, automation, lead-generation, openai, gmail, google-sheets]
keywords: [n8n workflow, lead generation automation, decodo google maps scraper, openai lead scoring, cold email n8n]
---

# 🚀 Tự động quét Lead doanh nghiệp địa phương, chấm điểm AI và gửi Cold Email

Các sếp có đang tốn hàng giờ mỗi ngày để lên Google Maps tìm kiếm khách hàng tiềm năng, copy thủ công thông tin vào Google Sheets, rồi lại lò mò vào từng website để viết email chào hàng (cold email) không? Công việc thủ công nhàm chán này không chỉ ngốn thời gian mà còn làm giảm năng suất đội ngũ Sales.

Workflow n8n này chính là giải pháp tự động hóa toàn diện từ A-Z giúp các sếp giải quyết triệt để bài toán tìm kiếm và tiếp cận khách hàng địa phương. Hệ thống sẽ tự động quét Google Maps, làm giàu dữ liệu bằng AI (OpenAI), lọc lead chất lượng cao và tự động gửi email cá nhân hóa qua Gmail một cách trơn tru!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted) do workflow này sử dụng Decodo community node.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% phễu Sales:** Từ khâu tìm kiếm trên Google Maps, lọc lead, chấm điểm tiềm năng đến gửi email chăm sóc.
- **Cá nhân hóa thông minh:** Sử dụng OpenAI để phân tích website doanh nghiệp, tìm ra điểm đau (pain points) và soạn nội dung cold email cực kỳ chuẩn chỉnh, tỉ lệ phản hồi cao.
- **Tiết kiệm thời gian & chi phí:** Thay vì thuê nhân sự cào data thủ công, hệ thống chạy tự động mỗi ngày theo lịch trình định sẵn.
- **Quản lý tập trung:** Toàn bộ dữ liệu lead, trạng thái (Mới, Đã làm giàu, Đã liên hệ) được lưu trữ và cập nhật đồng bộ trên Google Sheets.
:::

### 📦 Tổng quan 3 giai đoạn hoạt động của Workflow
1. **📍 Stage 1 (Discovery):** Tự động kích hoạt lúc 10h sáng hàng ngày, cào dữ liệu doanh nghiệp từ Google Maps thông qua **Decodo**, sau đó lưu vào Google Sheets với trạng thái `New`.
2. **📍 Stage 2 (Enrichment):** Quét các lead mới có website, sử dụng **Decodo** cào nội dung trang web và để **OpenAI** chấm điểm, tóm tắt, phân loại doanh nghiệp. Cập nhật trạng thái thành `Enriched`.
3. **📍 Stage 3 (Outreach):** Lọc các lead đạt điểm số (score threshold), cào sâu hơn vào website nếu cần, nhờ AI viết nội dung cold email cá nhân hóa rồi gửi tự động qua **Gmail**, sau đó đổi trạng thái thành `Contacted`.

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy mượt mà, các sếp cần chuẩn bị trước các tài nguyên sau:
- **Tài khoản n8n Self-hosted** (vì template này sử dụng Decodo community node).
- **Tài khoản & API Key Decodo** (dùng để cào Google Maps và Website).
- **Tài khoản & API Key OpenAI** (dùng để chấm điểm lead và viết cold email).
- **Tài khoản Google Sheets & Google Gmail** (cấp quyền OAuth2 trong n8n).
- **1 Google Sheet mẫu** có sẵn các cột thông tin lead (tên doanh nghiệp, địa chỉ, số điện thoại, website, email, điểm số, trạng thái...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn JSON.
- Trong giao diện n8n, chọn **Add workflow** -> Nhấp vào biểu tượng ba chấm ở góc trên bên phải -> Chọn **Import from File / Paste JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node sau trước khi kích hoạt:
- **Search Config (Node Set):** Điền chính xác các tham số tìm kiếm như Ngành nghề (niche), Thành phố (city), tọa độ (geo), giới hạn số lượng lead (max leads), điểm chuẩn (score threshold) và thông tin người gửi.
- **Decodo Nodes (Decodo: Scrape Google Maps, Decodo: Scrape Business Website, Decodo: Deep Scrape Website):** Kết nối tài khoản Decodo của các sếp.
- **Google Sheets Nodes (Save Lead, Update Lead, Get Enriched Leads, v.v.):** Kết nối tài khoản Google Sheets OAuth2, sau đó trỏ đến File Google Sheet và Sheet Name đã chuẩn bị sẵn.
- **OpenAI Nodes (AI: Score & Enrich Lead, AI: Write Cold Email):** Thêm OpenAI API Credentials và kiểm tra lại System/User Prompt nếu muốn điều chỉnh văn phong email.
- **Gmail Node (Gmail: Send Cold Email):** Cấu hình tài khoản Gmail gửi đi (OAuth2).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (Test workflow) với 1-2 dữ liệu mẫu để kiểm tra từ bước cào data đến gửi email (có thể tạm thời ngắt node gửi mail thật trong lúc test).
- Sau khi kiểm tra mọi thứ hoạt động trơn tru, bật công tắc **Active** ở góc trên bên phải để hệ thống tự động chạy theo lịch hẹn (Schedule: Daily 10AM).

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo qua Slack/Telegram:** Thêm node Slack hoặc Telegram sau bước *Gmail: Send Cold Email* để bắn thông báo về điện thoại cho đội ngũ Sales mỗi khi có một lead mới được tiếp cận thành công.
- **Thêm bước kiểm tra Email (Email Verification):** Trước node gửi Gmail, có thể tích hợp thêm các dịch vụ check sống email (như NeverBounce, Hunter) để giảm tỷ lệ bounce email.
- **Chiến dịch nuôi dưỡng (Nurturing):** Mở rộng workflow bằng cách thêm nhánh hẹn giờ (Wait node) sau 3 ngày nếu lead chưa phản hồi để gửi email follow-up tự động thứ hai.

### 📌 Kết luận
Workflow "Generate and enrich local business leads with Decodo, OpenAI and Gmail" là một vũ khí hạng nặng giúp tối ưu hóa toàn bộ quy trình Sales Outreach cho các agency và đội ngũ B2B. Hãy thiết lập ngay hôm nay để tự động hóa dòng khách hàng tiềm năng về cho doanh nghiệp của các sếp!