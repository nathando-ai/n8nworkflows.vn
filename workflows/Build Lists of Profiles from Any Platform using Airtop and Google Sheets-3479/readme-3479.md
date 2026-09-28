---
title: "🚀 Tự Động Xây Dựng Danh Sách Profile Từ Mọi Nền Tảng Với Airtop & Google Sheets"
description: "Workflow n8n giúp các sếp tự động tìm kiếm, trích xuất và lưu trữ danh sách profile (LinkedIn, Twitter, v.v.) vào Google Sheets chỉ với 1 cú click, không cần code."
slug: "tu-dong-xay-dung-danh-sach-profile-airtop-google-sheets"
tags: [n8n, automation, no-code, airtop, google-sheets, lead-generation]
keywords: [n8n workflow, tự động hóa lead, airtop ai, google sheets automation, scraping profile]
---

# 🚀 Tự Động Xây Dựng Danh Sách Profile Từ Mọi Nền Tảng Với Airtop & Google Sheets

Trong kỷ nguyên của Growth Hacking và Sales, việc xây dựng danh sách khách hàng tiềm năng (leads) là bước đầu tiên và quan trọng nhất. Tuy nhiên, việc thủ công tìm kiếm các profile trên LinkedIn, Twitter (X), hoặc các diễn đàn chuyên ngành cực kỳ tốn thời gian, dễ sai sót và không thể mở rộng quy mô (scale).

Workflow **Build Lists of Profiles from Any Platform using Airtop and Google Sheets** do Cesar @ Airtop AI phát triển chính là giải pháp "chìa khóa trao tay". Nó sử dụng sức mạnh của AI (Airtop) để "đọc" và trích xuất dữ liệu từ các trang web động, sau đó tự động hóa toàn bộ quy trình lưu trữ vào Google Sheets. Các sếp chỉ cần nhập yêu cầu (ví dụ: "CEO tại Việt Nam trên LinkedIn"), workflow sẽ lo phần còn lại.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi cần chạy hàng loạt danh sách, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Thay vì mất hàng giờ lướt web, các sếp chỉ mất vài giây để nhập prompt và chờ kết quả.
- **Chính xác cao nhờ AI:** Airtop sử dụng AI để hiểu ngữ cảnh trang web, giúp trích xuất đúng tên, handle và URL mà không bị lỗi do thay đổi cấu trúc HTML.
- **Dữ liệu sạch & Sẵn sàng dùng:** Workflow tự động loại bỏ trùng lặp (Dedupe) và định dạng dữ liệu chuẩn trước khi đưa vào Google Sheets.
- **Linh hoạt tuyệt đối:** Có thể áp dụng cho bất kỳ nền tảng nào (LinkedIn, GitHub, Product Hunt, Reddit...) chỉ bằng cách thay đổi prompt.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Bản Cloud hoặc Self-hosted.
2. **Tài khoản Airtop AI:** Đăng ký tại [airtop.ai](https://airtop.ai) và lấy **API Key**.
3. **Tài khoản Google:** Đã tạo sẵn một Google Sheet để lưu dữ liệu.
4. **Credentials trong n8n:**
   - `airtopApi`: Kết nối với Airtop.
   - `googleSheetsOAuth2Api`: Kết nối với Google Sheets (OAuth2).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** hoặc **Import from File** (nếu các sếp đã tải file JSON về).
3. Dán link gốc: `https://n8n.io/workflows/3479` hoặc dán trực tiếp JSON code vào.
4. Workflow sẽ hiện ra với 7 nodes chính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Các sếp cần kiểm tra kỹ các node sau:

**A. Node `Parameters` (Set Node)**
- Đây là nơi các sếp nhập "lệnh" cho AI.
- **Trường `who`**: Ai mà các sếp muốn tìm? (Ví dụ: `Marketing Managers`, `Founders`, `Python Developers`).
- **Trường `where`**: Ở đâu? (Ví dụ: `LinkedIn`, `Twitter`, `GitHub`, `Product Hunt`).
- *Mẹo:* Càng cụ thể, kết quả càng chính xác.

**B. Node `Get urls` (Airtop Node)**
- **Credentials**: Chọn credential `airtopApi` đã tạo.
- **Prompt**: Mặc định workflow đã có prompt tìm kiếm 10 kết quả không quảng cáo. Các sếp có thể chỉnh sửa prompt này nếu muốn thay đổi số lượng kết quả đầu vào (ví dụ: tăng lên 20 hoặc 50).
- *Lưu ý:* Node này sẽ truy cập trang web tìm kiếm và trả về danh sách các URL chứa danh sách profile.

**C. Node `Get people` (Airtop Node)**
- **Credentials**: Dùng chung `airtopApi`.
- **Prompt**: Đây là node "trái tim" của workflow. Nó truy cập từng URL từ node trước và trích xuất dữ liệu.
- Mặc định trích xuất: `name`, `handle or ID`, `URL`.
- *Tùy biến:* Nếu các sếp cần thêm trường dữ liệu (ví dụ: `Job Title`, `Company`), hãy sửa prompt trong node này. Ví dụ: *"Extract up to 20 items. For each person extract: name, job title, company, handle, URL."*

**D. Node `Dedupe results` (Code Node)**
- Node này chạy script JavaScript để loại bỏ các profile trùng lặp dựa trên URL hoặc Handle.
- **Không cần chỉnh sửa** trừ khi các sếp muốn thay đổi logic dedupe (ví dụ: dedupe theo tên thay vì URL).

**E. Node `Add to spreadsheet` (Google Sheets Node)**
- **Credentials**: Chọn `googleSheetsOAuth2Api`.
- **Document ID**: Dán ID của Google Sheet mà các sếp muốn lưu dữ liệu.
- **Sheet Name**: Tên tab trong Sheet (ví dụ: `Sheet1` hoặc `Leads`).
- **Mapping**: Kiểm tra xem các trường dữ liệu từ Airtop (name, handle, url) có được map đúng vào các cột trong Sheet không.

#### 3. Kích hoạt ⚡️
1. **Test Run**: Nhấn nút **Test workflow**.
   - Quan sát node `Parameters` để đảm bảo `who` và `where` đã đúng.
   - Quan sát node `Get urls` xem Airtop có trả về danh sách URL không.
   - Quan sát node `Get people` xem dữ liệu trích xuất có đầy đủ không.
   - Kiểm tra Google Sheets xem dữ liệu đã được append vào chưa.
2. **Bật Active**: Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải.
3. **Tự động hóa**: Nếu muốn chạy định kỳ, các sếp có thể thêm node `Schedule Trigger` thay thế cho `Manual Trigger` và đặt lịch chạy hàng ngày/tuần.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Email/Slack:** Sau node `Add to spreadsheet`, các sếp có thể thêm node `Send Email` hoặc `Slack` để thông báo ngay khi có danh sách mới.
- **Lọc dữ liệu sâu hơn:** Thêm một node `IF` hoặc `Code` sau `Dedupe results` để lọc ra chỉ những profile có chứa từ khóa nhất định trong tên hoặc công ty.
- **Đa nền tảng:** Chạy workflow này song song với nhiều cặp `who`/`where` khác nhau để xây dựng cơ sở dữ liệu đa kênh.
- **Lưu log lỗi:** Thêm node `Error Trigger` để ghi log các lần chạy thất bại vào một Sheet riêng, giúp các sếp dễ dàng debug khi Airtop gặp lỗi tạm thời.

### 📌 Kết luận
Workflow **Build Lists of Profiles** là công cụ "vũ khí" mạnh mẽ cho bất kỳ ai làm Sales, Marketing hoặc Research. Với sự kết hợp giữa AI trích xuất dữ liệu (Airtop) và tự động hóa quy trình (n8n + Google Sheets), các sếp có thể xây dựng danh sách khách hàng tiềm năng chất lượng cao trong thời gian kỷ lục. Hãy import ngay và bắt đầu tự động hóa quy trình tìm kiếm leads của mình!