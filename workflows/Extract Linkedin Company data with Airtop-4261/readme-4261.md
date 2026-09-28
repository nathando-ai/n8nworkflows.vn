---
title: "🚀 Tự động trích xuất dữ liệu công ty trên LinkedIn bằng Airtop và n8n"
description: "Hướng dẫn tự động hóa quy trình cào dữ liệu công ty từ LinkedIn sử dụng Airtop AI Browser Automation và n8n, giúp sales và nhà đầu tư tiết kiệm thời gian nghiên cứu."
slug: "tu-dong-trich-xuat-du-lieu-cong-ty-linkedin-airtop-n8n"
tags: [n8n, automation, airtop, linkedin, ai-agents, web-scraping]
keywords: [n8n workflow, trích xuất dữ liệu linkedin, airtop api, tự động hóa sales, lead generation]
---

# 🚀 Tự động trích xuất dữ liệu công ty trên LinkedIn bằng Airtop

Các sếp làm trong ngành sales, tuyển dụng hoặc đầu tư (VC) chắc chắn đều hiểu cảm giác "nản" cỡ nào khi phải thủ công lướt từng trang LinkedIn của công ty mục tiêu, copy-paste thông tin về quy mô, thông tin giới thiệu, vòng gọi vốn hay mức độ ứng dụng AI để nghiên cứu. Quy trình này vừa tốn thời gian, vừa nhàm chán.

Giải pháp ở đây là gì? Tự động hóa 100% với n8n kết hợp cùng **Airtop** – công cụ cung cấp API tự động hóa trình duyệt thông minh bằng AI. Workflow này sẽ giúp các sếp gom toàn bộ dữ liệu cấu trúc từ một URL công ty trên LinkedIn chỉ trong vòng vài nốt nhạc mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh copy-paste thủ công thông tin từ LinkedIn vào file Excel.
- **Dữ liệu chuẩn hóa (Structured JSON):** Trả về đầy đủ các trường thông tin từ định danh, quy mô, phân loại doanh nghiệp đến thông tin gọi vốn.
- **Hoạt động linh hoạt:** Có thể kích hoạt trực tiếp qua Form n8n hoặc gọi tự động từ một workflow khác (CRM, hệ thống lead generation).
- **Vượt qua bảo mật dễ dàng:** Tận dụng công nghệ AI Browser của Airtop giúp thao tác trên trình duyệt mượt mà như người thật.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản [Airtop Portal](https://portal.airtop.ai/).
- **Airtop API Key** để kết nối với n8n.
- **Airtop Browser Profile** đã được đăng nhập sẵn tài khoản LinkedIn của các sếp tại [Airtop Browser Profiles](https://portal.airtop.ai/browser-profiles).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã nguồn JSON của workflow (hoặc import file JSON tương ứng từ kho lưu trữ n8n với ID `4261`) vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 5 nodes chính phối hợp nhịp nhàng với nhau. Các sếp cần chú ý các điểm sau:

- **On form submission (`formTrigger`) & When Executed by Another Workflow (`executeWorkflowTrigger`):** 
  - Đây là 2 điểm khởi đầu (Triggers) của workflow. Các sếp có thể dùng Form nhập liệu có sẵn để test nhanh, hoặc gọi workflow này từ hệ thống CRM/Google Sheets thông qua webhook/execute workflow.
  - Tham số đầu vào bắt buộc cần truyền vào là **Company's LinkedIn URL** và **Airtop Profile ID**.
- **Unify Params (`set`):**
  - Node này dùng để chuẩn hóa các tham số đầu vào từ form hoặc workflow gọi sang định dạng chuẩn trước khi đẩy vào Airtop.
- **Extract Company's information (`airtop`):**
  - **Credentials:** Các sếp cần tạo một Airtop API Credential mới và điền **Airtop API Key** vào đây.
  - **Key Parameters:** 
    - Chọn Operation: `query`, Resource: `extraction`.
    - **Prompt:** Node này đã được cấu hình sẵn một Prompt mẫu cực kỳ chi tiết bằng tiếng Anh để hướng dẫn Airtop trích xuất các thông tin: Định danh công ty (Tên, Tagline, Địa điểm, Website), Quy mô nhân sự, Phân loại doanh nghiệp (Mức độ AI, trình độ kỹ thuật) và Hồ sơ gọi vốn. Các sếp có thể tinh chỉnh prompt này nếu muốn lấy thêm các trường dữ liệu khác.
- **Map output (`set`):**
  - Node này nhận kết quả dạng thô từ Airtop và ánh xạ (map) lại thành một cấu trúc dữ liệu JSON gọn gàng, sẵn sàng để đẩy tiếp vào Google Sheets, Notion, hoặc CRM của công ty.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và điền URL một trang công ty LinkedIn bất kỳ vào Form để test thử.
- Sau khi kiểm tra thấy kết quả trả về đúng ý muốn, các sếp gạt công tắc **Active** ở góc trên bên phải để đưa workflow vào trạng thái vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Google Sheets / Airtable:** Nối thêm node Google Sheets ở cuối workflow để tự động lưu mọi thông tin công ty vừa cào được vào một bảng quản lý danh sách khách hàng tiềm năng.
- **Gửi thông báo qua Slack/Telegram:** Thêm node thông báo để team Sales nhận được ngay thông tin chi tiết về công ty vừa phân tích ngay khi form được submit.
- **Kết hợp People Data:** Mở rộng workflow bằng cách kết hợp cào thêm dữ liệu nhân sự cấp cao (Founder, C-level) của công ty đó để phục vụ chiến dịch Cold Email cá nhân hóa sâu.

### 📌 Kết luận
Với sự kết hợp giữa n8n và Airtop AI, việc nghiên cứu đối thủ hay sàng lọc khách hàng tiềm năng trên LinkedIn nay đã trở nên tự động hoàn toàn. Hãy "lên đồ" ngay cho hệ thống của các sếp để tối ưu hóa hiệu suất làm việc ngay hôm nay!