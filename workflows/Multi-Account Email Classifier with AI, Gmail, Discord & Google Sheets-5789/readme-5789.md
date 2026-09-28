---
title: "🚀 Tự động hóa phân loại email đa tài khoản với AI, Gmail, Discord và Google Sheets"
description: "Hướng dẫn cài đặt workflow n8n giúp quản lý và phân loại email thông minh từ nhiều tài khoản Gmail cùng lúc bằng OpenAI, đồng thời thông báo qua Discord và đồng bộ Google Sheets."
slug: "tu-dong-hoa-phan-loai-email-nhieu-tai-khoan-ai-gmail-discord"
tags: [n8n, automation, no-code, gmail, openai, discord, google-sheets]
keywords: [n8n workflow, phan loai email tu dong, ai agent gmail discord, tich hop openai google sheets, quan ly email da tai khoan]
---

# 🚀 Tự động hóa phân loại email đa tài khoản với AI, Gmail, Discord và Google Sheets

Các sếp có đang cảm thấy quá tải khi phải quản lý hộp thư đến từ nhiều tài khoản Gmail khác nhau? Việc kiểm tra thủ công từng email, lọc bỏ thư rác (spam) và chọn lọc email quan trọng để phản hồi không chỉ ngốn rất nhiều thời gian mà còn dễ bỏ lỡ các cơ hội kinh doanh quan trọng.

Giải pháp ở đây là gì? Hãy để hệ thống tự động hóa lo! Bài viết này sẽ hướng dẫn các sếp triển khai một siêu workflow n8n được thiết kế bởi tác giả **Jay Emp0**, giúp gom toàn bộ email từ **nhiều tài khoản Gmail**, sử dụng **AI Agent (OpenAI)** để phân tích thông minh, lọc spam bằng **Google Sheets** và bắn thông báo trực tiếp về **Discord**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Quản lý đa tài khoản tập trung:** Theo dõi email từ nhiều địa chỉ Gmail khác nhau (account1, account2, account3, account4) trên cùng một hệ thống.
- **AI thông minh phân loại:** Sử dụng mô hình `gpt-4o-mini` để đọc hiểu ngữ cảnh, trích xuất thông tin và chỉ lọc ra các email quan trọng thực sự.
- **Tự động hóa chống Spam:** Tự động đối chiếu và cập nhật danh sách spam thông qua Google Sheets.
- **Cảnh báo tức thì:** Gửi thông báo chi tiết qua Discord để đội ngũ có thể nắm bắt và phản hồi nhanh chóng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Google** (Cần kết nối tối đa 4 tài khoản Gmail và Google Sheets qua OAuth2).
- **Tài khoản OpenAI** (Lấy API Key và cấu hình model `gpt-4o-mini`).
- **Tài khoản Discord** (Tạo Bot và cấu hình quyền truy cập kênh để gửi/nhận tin nhắn).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sao chép đoạn mã JSON của workflow từ nguồn gốc (`https://n8n.io/workflows/5789`), sau đó vào giao diện n8n Editor, chọn **Add workflow** -> **Import from File/Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 22 nodes hoạt động nhịp nhàng, các sếp cần lưu ý cấu hình kỹ các điểm sau:
- **Các node Gmail Trigger (`Gmail Trigger`, `Gmail Trigger1`, `Gmail Trigger2`, `Gmail Trigger3`):** Kết nối đúng các tài khoản Gmail tương ứng (`account1@gmail.com`, `account2@gmail.com`, v.v.) để hệ thống lắng nghe email mới đến.
- **Node OpenAI Chat Model (`OpenAI Chat Model1`, `OpenAI Chat Model3`):** Điền `OpenAI API Key` và đảm bảo model đang chọn là `gpt-4o-mini`.
- **Node Google Sheets Tools (`Get spam list`, `update spam list`, `Get spam list1`):** Trỏ tới file Google Sheets chứa danh sách bộ lọc/spam của doanh nghiệp, cấu hình đúng tên Sheet (Sheet Name) và các cột dữ liệu.
- **Các node Discord (`Send a message`, `Discord - reply1`, `Get a message in Discord`):** Cấu hình `Discord OAuth2 API` và chọn đúng Channel ID nơi bot sẽ gửi thông báo email quan trọng và nhận lệnh phản hồi.
- **Node Webhook (`Webhook`):** Cấu hình đường dẫn endpoint (`email-feedback`) để nhận phản hồi dữ liệu từ bên ngoài khi cần thiết.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi thử email vào các tài khoản Gmail đã cấu hình để test luồng dữ liệu.
- Kiểm tra kết quả trên Google Sheets và Discord xem thông báo đã bắn về chính xác chưa.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ dùng Discord, các sếp có thể nhân bản node thông báo để bắn thêm tin nhắn về Telegram, Slack hoặc Zalo OA để đồng đội dễ nắm bắt.
- **Lưu lịch sử chi tiết:** Tích hợp thêm một bước ghi log toàn bộ email (cả spam và email quan trọng) vào Google Sheets để phục vụ việc thống kê, phân tích sau này.
- **Tùy biến Prompt cho AI Agent:** Tinh chỉnh prompt trong các node `AI Agent1` và `AI Agent2` để AI hiểu sâu hơn về lĩnh vực kinh doanh của doanh nghiệp, từ đó phân loại email chuẩn xác theo đúng ý đồ riêng.

### 📌 Kết luận
Workflow tự động hóa phân loại email đa tài khoản này là một vũ khí cực mạnh giúp tiết kiệm hàng giờ đồng hồ mỗi ngày cho các sếp và đội ngũ CSKH/Sales. Hãy cài đặt ngay hôm nay để tối ưu hóa quy trình vận hành và không bỏ lỡ bất kỳ khách hàng tiềm năng nào!