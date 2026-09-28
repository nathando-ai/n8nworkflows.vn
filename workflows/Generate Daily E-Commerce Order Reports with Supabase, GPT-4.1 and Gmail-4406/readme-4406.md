---
title: "🚀 Tự động tạo và gửi báo cáo đơn hàng thương mại điện tử hàng ngày với Supabase, GPT-4 và Gmail"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa hoàn toàn việc trích xuất dữ liệu đơn hàng từ Supabase, phân tích bằng GPT-4 và gửi báo cáo qua Gmail mỗi ngày."
slug: "tu-dong-tao-bao-cao-don-hang-thuong-mai-dien-tu-supabase-gpt-4-gmail"
tags: [n8n, automation, no-code, supabase, openai, gmail, ai-agent, ecommerce]
keywords: [n8n workflow, tự động hóa đơn hàng, báo cáo thương mại điện tử, supabase n8n, openai gpt-4, gmail automation]
---

# 🚀 Tự động tạo và gửi báo cáo đơn hàng thương mại điện tử hàng ngày với Supabase, GPT-4 và Gmail

Các sếp có đang mệt mỏi mỗi sáng phải vào hệ thống cơ sở dữ liệu, tổng hợp dữ liệu đơn hàng, sản phẩm, khách hàng rồi viết báo cáo gửi cho sếp lớn hoặc đội ngũ quản lý? Việc làm thủ công này không chỉ ngốn hàng giờ đồng hồ mỗi tuần mà còn dễ xảy ra sai sót khi tính toán các chỉ số kinh doanh.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n tự động hóa 100%. Workflow này sẽ âm thầm làm việc thay các sếp: đúng 8 giờ sáng mỗi ngày, AI Agent sẽ tự động truy vấn dữ liệu từ Supabase (Đơn hàng, Khách hàng, Sản phẩm, Chi tiết đơn hàng), sử dụng sức mạnh phân tích của GPT-4 để tổng hợp tình hình kinh doanh, sau đó tự động soạn thảo và gửi báo cáo trực tiếp qua Gmail. Không cần một dòng code nào cả!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Loại bỏ hoàn toàn 100% công sức làm báo cáo thủ công mỗi ngày.
- **Báo cáo thông minh:** GPT-4 không chỉ liệt kê số liệu mà còn phân tích xu hướng, điểm nổi bật trong ngày kinh doanh.
- **Chính xác và kịp thời:** Báo cáo được gửi đúng 8:00 sáng hàng ngày vào hòm thư Gmail của quản lý.
- **Hoạt động bền bỉ 24/7:** Chạy tự động trên n8n mà không cần sự can thiệp thủ công.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để vận hành trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và thông tin sau:
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Supabase Account:** Tài khoản và thông tin kết nối cơ sở dữ liệu chứa các bảng Orders, Order Items, Clients, Products.
- **OpenAI API Key:** Tài khoản OpenAI có quyền sử dụng mô hình GPT-4.
- **Gmail Account:** Tài khoản Google/Gmail để cấp quyền gửi email tự động qua OAuth2.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp tiến hành copy mã JSON của workflow (hoặc tải file JSON từ nguồn) và dán trực tiếp vào n8n Editor của mình thông qua tính năng Import từ Clipboard.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, workflow bao gồm 9 nodes chính sẽ hiển thị. Các sếp cần cấu hình lần lượt các điểm sau:

- **Node `Daily 8am` (Schedule Trigger):** 
  - Mặc định lịch chạy đã được thiết lập là 8:00 sáng hàng ngày. Các sếp có thể thay đổi múi giờ hoặc khung giờ tùy theo nhu cầu kinh doanh của doanh nghiệp.
- **Các nodes Supabase (`Get Orders`, `Get Order Items`, `Get Clients`, `Get Products`):**
  - Cần kết nối credential `supabaseApi` (điền Supabase URL và Service Role/Anon Key).
  - Chọn đúng tên các bảng tương ứng trong database Supabase của các sếp (`orders`, `order_items`, `clients`, `products`).
- **Node `OpenAI Chat Model`:**
  - Kết nối credential `openAiApi` với API Key của OpenAI.
  - Chọn model là `gpt-4.1` (hoặc các phiên bản GPT-4 tương đương) để đảm bảo chất lượng phân tích ngôn ngữ tự nhiên tốt nhất.
- **Node `Set Sender Email`:**
  - Cấu hình lại địa chỉ email người nhận hoặc các thông tin tùy biến hiển thị trên email báo cáo.
- **Node `Send Gmail Summary` (Gmail Tool):**
  - Kết nối tài khoản Gmail cá nhân hoặc email doanh nghiệp thông qua OAuth2 để cấp quyền gửi thư.
- **Node `AI Agent`:**
  - Kiểm tra lại phần Prompt hệ thống (System Prompt) trong AI Agent để đảm bảo AI hiểu rõ cách thức tổng hợp số liệu, định dạng báo cáo (tiếng Việt/tiếng Anh, có các mục doanh thu, sản phẩm bán chạy, v.v.) phù hợp với văn hóa công ty.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** để chạy thử nghiệm xem AI Agent có kết nối được với Supabase và soạn thảo bản nháp Gmail thành công không.
- Sau khi test thành công, gạt công tắc sang **Active** để bật chế độ tự động chạy hàng ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Ngoài việc gửi qua Gmail, các sếp có thể gắn thêm node Telegram hoặc Slack để bắn thông báo tóm tắt doanh thu ngay vào nhóm chat nội dung của công ty.
- **Lưu lịch sử báo cáo:** Thêm một node Supabase Insert vào cuối chuỗi để lưu lại nội dung báo cáo mà AI đã tạo vào bảng `daily_reports` trong database nhằm phục vụ việc tra cứu lại sau này.
- **Tùy chỉnh KPI:** Cập nhật System Prompt trong AI Agent để AI tự động so sánh doanh thu hôm nay với mục tiêu KPI đã đặt ra.

### 📌 Kết luận
Việc tự động hóa quy trình báo cáo kinh doanh chưa bao giờ dễ dàng đến thế với sự kết hợp giữa n8n, Supabase và AI. Hãy cài đặt ngay workflow này để tối ưu hóa vận hành và giúp đội ngũ quản lý nắm bắt số liệu nhanh chóng mỗi ngày!