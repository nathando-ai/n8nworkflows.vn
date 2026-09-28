---
title: "🚀 Tự động trích xuất thông tin LinkedIn chuyên sâu với Airtop và AI"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa trích xuất dữ liệu hồ sơ LinkedIn có cấu trúc bằng Airtop API và AI, giúp tiết kiệm thời gian nghiên cứu và làm giàu dữ liệu lead."
slug: "trich-xuat-du-lieu-linkedin-tu-dong-airtop-ai"
tags: [n8n, automation, airtop, ai, linkedin, web-scraping, sales]
keywords: [n8n workflow, trích xuất dữ liệu linkedin, airtop api, tự động hóa sales, ai parsing linkedin]
---

# 🚀 Tự động trích xuất thông tin LinkedIn chuyên sâu với Airtop và AI

Việc thủ công copy thông tin từ hàng loạt hồ sơ LinkedIn để làm giàu dữ liệu khách hàng (lead enrichment) hay nghiên cứu ứng viên tuyển dụng cực kỳ tốn thời gian và dễ xảy ra sai sót. 

Giải pháp? Workflow n8n tích hợp **Airtop API** và AI sẽ thay bạn mở trình duyệt tự động, đọc hiểu hồ sơ và trả về dữ liệu có cấu trúc 100% tự động mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh copy-paste thủ công từng trường thông tin (Họ tên, chức vụ, công ty, phần giới thiệu...).
- **Dữ liệu chuẩn cấu trúc:** Nhận về định dạng JSON sạch sẽ, sẵn sàng đẩy thẳng vào CRM (HubSpot, Salesforce, Airtable, Google Sheets).
- **Vượt qua rào cản đăng nhập:** Tận dụng hệ thống trình duyệt thông minh của Airtop đã kết nối sẵn với tài khoản LinkedIn của các sếp.
- **Hoạt động linh hoạt:** Có thể kích hoạt qua Form nộp trực tuyến hoặc gọi từ một workflow khác (Sub-workflow).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- **Airtop API Key:** Tạo miễn phí tại [Airtop Portal](https://portal.airtop.ai/api-keys).
- **Airtop Profile:** Một Profile trình duyệt trên Airtop đã được đăng nhập sẵn tài khoản LinkedIn cá nhân của các sếp (xem tại [Airtop Browser Profiles](https://portal.airtop.ai/browser-profiles)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ n8n.io (ID: 4203) hoặc copy trực tiếp đoạn JSON template và dán vào màn hình chỉnh sửa workflow trong n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 5 nodes chính, các sếp cần chú ý cấu hình các điểm sau:
- **Node `On form submission` & `When Executed by Another Workflow`**: Đây là 2 điểm khởi đầu (Triggers). Các sếp chọn 1 trong 2 cách kích hoạt phù hợp với nhu cầu (nhập qua form web hoặc gọi từ workflow khác truyền URL sang).
- **Node `Parameters` & `Edit Fields` (Set)**: Nơi khai báo các biến đầu vào quan trọng:
  - `airtop_profile`: Tên profile trình duyệt Airtop đã kết nối LinkedIn.
  - `linkedin_url`: Đường dẫn URL của profile LinkedIn cần trích xuất.
- **Node `Airtop`**: 
  - Kết nối tài khoản bằng **Airtop API Key**.
  - Cấu hình tham số trích xuất (`Prompt`) theo ý muốn. Mặc định AI sẽ lấy: Họ tên, Headline, Vị trí địa lý, Công ty hiện tại, Chức vụ hiện tại, và phần Giới thiệu (About). Các sếp có thể tùy chỉnh prompt để lấy thêm Kinh nghiệm, Học vấn, Kỹ năng... nếu muốn.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step / Test workflow** với một URL LinkedIn mẫu để kiểm tra kết quả trả về từ AI.
- Sau khi dữ liệu hiển thị chính xác, gạt công tắc sang **Active** để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Đẩy dữ liệu vào CRM:** Kết nối thêm node Google Sheets, Airtable hoặc HubSpot ở bước cuối để tự động lưu trữ thông tin profile vừa trích xuất.
- **Xử lý hàng loạt (Bulk Processing):** Kết hợp workflow này với một Web scraping tool tìm kiếm LinkedIn để xử lý danh sách hàng trăm profile tự động mỗi ngày.
- **Mở rộng nền tảng:** Dễ dàng thay đổi prompt và URL để áp dụng trích xuất dữ liệu từ GitHub, Twitter/X, hoặc các trang web thương mại điện tử khác.

### 📌 Kết luận
Tự động hóa trích xuất LinkedIn với Airtop và AI là "vũ khí" cực mạnh cho đội ngũ Sales, Recruiter và Marketing để khai thác data nhanh chóng. Hãy cài đặt ngay hôm nay để tối ưu hóa hiệu suất công việc của các sếp!