---
title: "🚀 Tự động hóa thực đơn dinh dưỡng cá nhân hóa theo huyết áp với Gemini, Google Search và QuickChart"
description: "Xây dựng trợ lý dinh dưỡng AI tự động phân tích huyết áp hàng tuần từ Google Sheets, tìm kiếm công thức nấu ăn, vẽ biểu đồ xu hướng và gửi email báo cáo chi tiết."
slug: "tu-dong-hoa-thuc-don-dinh-duong-theo-huyet-ap-n8n"
tags: [n8n, automation, ai-chatbot, google-gemini, google-sheets, quickchart]
keywords: [n8n workflow, tu dong hoa thuc don, gemini ai, quan ly huyet ap, google sheets, quickchart]
keywords: [n8n workflow, tự động hóa, google sheets, gemini ai, quản lý huyết áp]
---

# 🚀 Trợ lý Dinh dưỡng AI: Tự động lên thực đơn và phân tích huyết áp hàng tuần

Các sếp có đang gặp khó khăn trong việc theo dõi chỉ số huyết áp cá nhân, loay hoay không biết hôm nay ăn gì để tốt cho sức khỏe tim mạch, hay mệt mỏi với việc tổng hợp dữ liệu thủ công mỗi tuần? Việc duy trì chế độ ăn uống khoa học dựa trên số liệu thực tế chưa bao giờ là dễ dàng nếu làm bằng tay.

Giải pháp đây rồi! Workflow n8n này sẽ đóng vai trò như một **chuyên gia dinh dưỡng AI cá nhân**. Hệ thống tự động lấy dữ liệu huyết áp từ Google Sheets, nhờ AI Gemini phân tích xu hướng, tìm kiếm công thức nấu ăn chuẩn xác, tạo biểu đồ trực quan và gửi email báo cáo tận gốc cho các sếp vào mỗi thứ Hai hàng tuần. 100% tự động, không tốn một phút thao tác thủ công!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Không cần nhớ lịch kiểm tra huyết áp hay tự tay tính toán chỉ số trung bình mỗi tuần.
- **Cá nhân hóa thông minh:** AI Gemini tự động đề ra chiến lược dinh dưỡng (ví dụ: thực đơn ít muối, giàu kali...) dựa sát vào tình trạng huyết áp thực tế.
- **Báo cáo trực quan:** Tự động tạo biểu đồ xu hướng huyết áp sinh động qua QuickChart và gửi thẳng vào hộp thư Gmail cá nhân.
- **Hoạt động 24/7:** Chạy ngầm định kỳ mỗi sáng thứ Hai (7:00 AM), sẵn sàng phục vụ các sếp ngay khi thức dậy.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Sheets & Gmail** (kết nối qua OAuth2).
- **Google Gemini API Key** (cho các node AI xử lý phân tích và tạo thực đơn).
- **Google Custom Search API** (để tìm kiếm các công thức nấu ăn thực tế trên mạng).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc sử dụng tính năng Copy/Paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp nhớ cấu hình kỹ các node sau:
- **Workflow Configuration (Node Set):** Điền các thông số cấu hình chung, ID bảng tính và các API keys cần thiết vào đây.
- **Get Blood Pressure Data (Node Google Sheets):** Kết nối tài khoản Google Sheets của các sếp. Đảm bảo bảng tính có sẵn các cột: `date` (ngày), `systolic` (huyết áp tâm thu), `diastolic` (huyết áp tâm trương).
- **Message a model & Message a model2 (Node Google Gemini):** Chọn credentials Google Palm/Gemini API và thiết lập model (`gemini-1.5-flash`) để AI thực hiện nhiệm vụ phân tích từ khóa và viết thực đơn.
- **Google Custom Search (Node HTTP Request):** Cấu hình API tìm kiếm để lấy dữ liệu công thức nấu ăn phù hợp dựa trên từ khóa do Gemini đề xuất.
- **Send Email Report (Node Gmail):** Kết nối tài khoản Gmail và điền địa chỉ email nhận báo cáo của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test run thủ công dữ liệu mẫu xem email có về hay không.
- Nếu mọi thứ mượt mà, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy theo lịch hẹn.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm thông báo:** Nối thêm node Telegram hoặc Slack vào cuối workflow để nhận thông báo nhanh tóm tắt thực đơn ngay trên điện thoại.
- **Lưu lịch sử:** Ghi log các thực đơn AI đã tạo vào một tab khác trên Google Sheets để dễ dàng tra cứu lại sau này.
- **Mở rộng nhắc nhở uống nước:** Thêm một nhánh nhỏ nhắc nhở uống đủ nước dựa trên thời tiết hoặc chỉ số sức khỏe.

### 📌 Kết luận
Ứng dụng AI vào chăm sóc sức khỏe cá nhân chưa bao giờ dễ dàng đến thế với n8n. Hãy "lên đồ" ngay workflow này để làm chủ huyết áp và có những bữa ăn lành mạnh mỗi tuần, các sếp nhé!