---
title: "🚀 Tự động làm giàu dữ liệu Influencer đa nền tảng với Influencers.club & Supabase trong n8n"
description: "Hướng dẫn xây dựng quy trình tự động hóa n8n giúp quét, trích xuất và làm giàu thông tin Creator (Instagram, TikTok, YouTube...) từ Influencers.club API và lưu trữ an toàn vào Supabase."
slug: "tu-dong-lam-giau-du-lieu-influencer-influencers-club-supabase-n8n"
tags: [n8n, automation, no-code, influencers-club, supabase, lead-generation]
keywords: [n8n workflow, tự động hóa influencer marketing, influencers.club api, supabase n8n, làm giàu dữ liệu creator]
---

# 🚀 Tự động làm giàu dữ liệu Influencer đa nền tảng với Influencers.club & Supabase

Các sếp làm trong ngành Influencer Marketing chắc chắn hiểu cảm giác "đau đầu" khi phải thu thập thủ công thông tin của hàng trăm, hàng nghìn nhà sáng tạo nội dung (Creator). Việc tìm kiếm handle, email, phân tích đối tượng (audience), nhân khẩu học và insights trên nhiều nền tảng (Instagram, TikTok, YouTube, Twitter...) tốn rất nhiều thời gian và dễ xảy ra sai sót.

Giải pháp là gì? Bài viết này sẽ hướng dẫn các sếp cách thiết lập một workflow n8n tự động hóa 100%: định kỳ quét các influencer chưa có dữ liệu, gọi API từ **Influencers.club** để làm giàu thông tin (enrichment) và cập nhật trực tiếp vào cơ sở dữ liệu **Supabase** một cách an toàn mà không lo bị ghi đè dữ liệu cũ.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hoàn toàn**: Chạy lịch trình hằng ngày (Daily Schedule) mà không cần can thiệp thủ công.
- **Dữ liệu đa nền tảng chuẩn xác**: Lấy toàn bộ thông tin chi tiết từ Influencers.club API (lượng audience, nội dung, chỉ số kiếm tiền, thông tin liên lạc...).
- **An toàn dữ liệu (Smart Update)**: Chỉ cập nhật các giá trị bị thiếu (Null values) hoặc sử dụng hàm SQL tùy chỉnh, tránh làm mất dữ liệu cũ khi chạy lại workflow.
- **Tối ưu hóa hiệu suất**: Xử lý theo từng lô (Batch processing) kết hợp thời gian nghỉ (Wait) để tránh vượt quá giới hạn API (Rate limit).
:::

### 📦 Các Nodes chính trong Workflow
Workflow bao gồm 8 nodes được tối ưu hóa cho tác vụ Lead Generation và Data Enrichment:
1. **Daily Refresh Schedule**: Kích hoạt workflow tự động chạy mỗi ngày một lần.
2. **List Influencers Without Enrichment (`supabase`)**: Lấy danh sách các influencer chưa được làm giàu dữ liệu từ cơ sở dữ liệu Supabase.
3. **Process in Batches (`splitInBatches`)**: Chia nhỏ danh sách creator thành từng lô để xử lý mượt mà.
4. **Influencers.club Enrichment API By Handle (`httpRequest`)**: Gửi yêu cầu truy vấn API để lấy dữ liệu mạng xã hội của creator theo handle.
5. **Wait 5 Second (`wait`)**: Tạm dừng 5 giây giữa các request để đảm bảo an toàn cho API.
6. **Normalize Creator Enrichment Payload (`code`)**: Sử dụng đoạn mã tùy chỉnh để chuẩn hóa dữ liệu trả về từ API.
7. **Update Null Values Only (`httpRequest` / SQL Function)**: Cập nhật dữ liệu vào Supabase thông qua hàm SQL giúp chỉ điền các trường còn thiếu (Khuyên dùng cho production).
8. **Update a row (`supabase`)**: Phương pháp thay thế để ghi đè hoặc cập nhật trực tiếp vào bảng (Lưu ý: Có thể ghi đè dữ liệu cũ nếu chạy lại).

---

### 🔧 Yêu cầu cần thiết
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Nợn (n8n) instance**: Đã cài đặt phiên bản n8n (Cloud hoặc Self-hosted).
- **Tài khoản Supabase**: Đã tạo sẵn bảng (Table) lưu trữ thông tin creator với các cột cần thiết và kết nối thông tin API Credentials (`supabaseApi`).
- **Tài khoản Influencers.club**: Đã đăng ký và lấy API Key/Header Authentication (`httpHeaderAuth`) để gọi dịch vụ enrichment.

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy đoạn JSON từ hệ thống n8n.
- Tại giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào dấu 3 chấm ở góc trên bên phải -> Chọn **Import from File** hoặc **Paste Workflow**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `List Influencers Without Enrichment` & `Update a row`**: 
  - Chọn đúng Credentials kết nối tới **Supabase** của các sếp.
  - Chỉ định đúng tên bảng (Table Name) chứa danh sách Influencer. Đảm bảo có bộ lọc kiểm tra các trường enrichment đang để trống (`NULL`).
- **Node `Influencers.club Enrichment API By Handle`**:
  - Cấu hình thông tin xác thực (`httpHeaderAuth`) bằng API Key lấy từ tài khoản Influencers.club của các sếp.
  - Kiểm tra endpoint URL của API theo tài liệu chính thức từ Influencers.club.
- **Node `Update Null Values Only` (Khuyên dùng)**:
  - Node này sử dụng hàm SQL tùy chỉnh trên Supabase để chỉ điền dữ liệu vào các ô còn trống, giúp workflow an toàn khi chạy lại nhiều lần mà không sợ mất dữ liệu đã có sẵn. (Tham khảo mã nguồn hàm SQL mẫu trên [GitHub của tác giả](https://github.com/GjPetrovski-IC/N8N-Public-Templates)).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử nghiệm (Test run) với một vài bản ghi mẫu để kiểm tra dữ liệu trả về qua từng node.
- Sau khi kiểm tra mọi thứ hoạt động trơn tru, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy theo lịch trình hằng ngày.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Thêm node Telegram hoặc Slack ở cuối workflow để gửi báo cáo tổng kết mỗi khi workflow chạy xong (ví dụ: *"Đã làm giàu thành công 50 creator mới hôm nay!"*).
- **Xử lý lỗi (Error Handling)**: Thêm node *Error Trigger* để nếu API Influencers.club gặp sự cố hoặc timeout, hệ thống sẽ tự động gửi cảnh báo cho đội ngũ kỹ thuật.
- **Lưu lịch sử chạy (Logging)**: Tạo thêm một bảng log trên Supabase để ghi nhận trạng thái thành công/thất bại của từng handle creator.

---

### 📌 Kết luận
Việc tự động hóa quy trình thu thập và làm giàu dữ liệu Influencer giúp đội ngũ marketing tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần, đồng thời đảm bảo cơ sở dữ liệu luôn mới mẻ và chính xác. Hãy áp dụng ngay workflow này vào hệ thống của các sếp để tối ưu hóa chiến dịch Influencer Marketing nhé!