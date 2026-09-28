---
title: "🚀 Tự động tìm kiếm trang LinkedIn doanh nghiệp cực nhanh với Airtop trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa tìm kiếm và xác thực trang LinkedIn chính thức của công ty bằng Airtop API, giúp tối ưu hóa quy trình Sales và Data Enrichment."
slug: "tu-dong-tim-kiem-trang-linkedin-doanh-nghiep-voi-airtop"
tags: [n8n, automation, airtop, sales, lead-generation, linkedin]
keywords: [n8n workflow, tìm linkedin công ty, airtop api, sales automation, tự động hóa n8n]
---

# 🚀 Tự động tìm kiếm trang LinkedIn doanh nghiệp cực nhanh với Airtop

Trong các chiến dịch Sales Outreach hoặc Data Enrichment (làm giàu dữ liệu khách hàng), việc tìm kiếm chính xác trang LinkedIn (Company Page) của hàng loạt doanh nghiệp là một việc làm tốn rất nhiều thời gian nếu làm thủ công. Các sếp thường phải tự tra Google, mò vào từng website hoặc tìm kiếm trên LinkedIn, rất dễ nản và sai sót.

Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ thông minh, tự động hóa 100% quy trình này bằng **Airtop AI Browser Automation API** kết hợp trí tuệ nhân tạo để lùng sục, trích xuất và xác thực link LinkedIn của bất kỳ công ty nào chỉ trong tích tắc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa đa tầng thông minh:** Tự động quét trực tiếp từ website công ty 👉 nếu không thấy sẽ chuyển sang tìm trên LinkedIn 👉 nếu vẫn chưa có sẽ quét tiếp qua Google Search.
- **Tiết kiệm 90% thời gian:** Giải phóng đội ngũ Sales khỏi các tác vụ tìm kiếm thủ công nhàm chán.
- **Độ chính xác cao:** Tích hợp AI của Airtop kết hợp bước xác thực (Verify) giúp lọc ra đúng trang LinkedIn chính chủ của doanh nghiệp.
- **Linh hoạt kích hoạt:** Hỗ trợ nhận dữ liệu đầu vào qua Form trực tuyến hoặc gọi tự động từ các workflow khác (`Execute Workflow`).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Tài khoản Airtop:** 
  - [Airtop API Key](https://portal.airtop.ai/api-keys) (Miễn phí tạo).
  - [Airtop Profile](https://portal.airtop.ai/browser-profiles) đã đăng nhập sẵn tài khoản LinkedIn (Yêu cầu đăng nhập 1 lần duy nhất để trình duyệt ảo thao tác).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này từ kho lưu trữ n8n (Link gốc: [n8n.io/workflows/4254](https://n8n.io/workflows/4254)), sau đó paste trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 11 nodes được bố trí mạch lạc. Các sếp cần chú ý cấu hình các điểm mấu chốt sau:

- **Node `On form submission` & `When Executed by Another Workflow`**: Đây là 2 điểm khởi đầu (Triggers). Các sếp chọn cách vận hành phù hợp: điền form trực tiếp hoặc nhận domain từ một bảng Google Sheets/CRM chạy ngầm.
- **Node `Unify parameters` & `Map data`**: Dùng để chuẩn hóa các tham số đầu vào (ví dụ: `Company domain`) truyền đi xuyên suốt workflow.
- **Node `Webpage search`, `Linkedin search`, `Google search` (Loại: Airtop)**: 
  - Cần kết nối tài khoản thông qua **Airtop API Credentials** của các sếp.
  - Các node này sử dụng AI Prompt tự nhiên để chỉ thị cho trình duyệt ảo Airtop trích xuất chính xác đường dẫn LinkedIn từ footer website, kết quả tìm kiếm trên LinkedIn hoặc Google.
- **Node `Company LinkedIn exists?`, `LinkedIn link found?`, `LinkedIn link found?1` (Loại: Filter & IF)**: Các điều kiện rẽ nhánh kiểm tra xem đã tìm thấy URL hay chưa. Nếu tìm thấy ở bước quét website, workflow sẽ bỏ qua các bước quét sau để tối ưu tốc độ.
- **Node `Verify LinkedIn link`**: Chạy một sub-workflow con để kiểm tra lại tính hợp lệ của URL LinkedIn thu được.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng một vài domain công ty mẫu (ví dụ: `google.com`, `microsoft.com`) để kiểm tra dữ liệu trả về ở các node Airtop.
- Sau khi test thành công, gạt công tắc sang **Active** để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Google Sheets / Airtable:** Lưu danh sách domain công ty vào một file Sheets, cho n8n chạy vòng lặp (Loop) và tự động ghi đè cột "LinkedIn URL" cực kỳ mượt mà.
- **Tích hợp kênh thông báo:** Bắn tin nhắn qua Telegram hoặc Slack mỗi khi quét xong một lô danh sách doanh nghiệp hoặc báo cáo lỗi nếu không tìm thấy trang.
- **Kết hợp People Enrichment:** Sau khi có trang LinkedIn công ty, nối tiếp workflow tìm kiếm danh sách Key Person (CEO, Founder, HR Manager) để phục vụ chiến dịch Cold Email.

### 📌 Kết luận
Việc tìm kiếm thông tin doanh nghiệp giờ đây đã được tự động hóa hoàn toàn nhờ sức mạnh của AI Browser Automation từ Airtop trên n8n. Hãy áp dụng ngay workflow này để tối ưu hóa đội ngũ Sales và tăng tốc độ tiếp cận khách hàng tiềm năng lên gấp nhiều lần các sếp nhé!