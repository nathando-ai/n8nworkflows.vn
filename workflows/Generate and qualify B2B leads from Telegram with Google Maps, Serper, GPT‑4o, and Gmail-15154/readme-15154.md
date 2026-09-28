---
title: "🚀 Tự động hóa tìm kiếm và chấm điểm Lead B2B qua Telegram tích hợp Google Maps, AI & Gmail"
description: "Xây dựng hệ thống tìm kiếm khách hàng tiềm năng B2B tự động 100% từ Telegram, quét dữ liệu Google Maps, đánh giá bằng OpenAI GPT-4o và chăm sóc qua Gmail."
slug: "tu-dong-hoa-tim-kiem-lead-b2b-telegram-google-maps-openai-gmail"
tags: [n8n, automation, lead-generation, telegram, openai, google-sheets]
keywords: [n8n workflow, b2b lead generation, tự động tìm kiếm khách hàng, google maps api, openai gpt-4o, gmail automation]
---

# 🚀 Tự động hóa tìm kiếm và chấm điểm Lead B2B qua Telegram tích hợp Google Maps, AI & Gmail

Các sếp có đang đau đầu vì việc tìm kiếm khách hàng tiềm năng (B2B Leads) thủ công tốn quá nhiều thời gian? Việc phải ngồi lướt Google Maps, tìm thông tin liên hệ, đánh giá tiềm năng rồi soạn email chào hàng tốn hàng giờ đồng hồ mỗi ngày mà hiệu suất lại không cao?

Hôm nay, em xin giới thiệu một siêu phẩm workflow n8n giúp các sếp tự động hóa toàn bộ quy trình này từ A-Z. Chỉ với một tin nhắn ngắn gọn qua Telegram, hệ thống sẽ tự động quét Google Maps, làm giàu dữ liệu bằng tìm kiếm bên ngoài, chấm điểm lead bằng AI (OpenAI), lưu vào Google Sheets, tự động gửi email chào hàng, chờ đợi và gửi chuỗi email chăm sóc (follow-up) cực kỳ chuyên nghiệp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Thay vì tìm kiếm thủ công, hệ thống tự động hóa toàn bộ từ quét dữ liệu, lọc trùng đến gửi email.
- **Chất lượng lead được kiểm duyệt kỹ càng:** AI (GPT-4o) chấm điểm và xác thực thông tin liên hệ, đảm bảo chỉ tiếp cận những khách hàng thực sự tiềm năng.
- **Nuôi dưỡng khách hàng tự động:** Tự động gửi email giới thiệu ban đầu, chờ 3 ngày và tự động gửi email chăm sóc (follow-up) tiếp theo.
- **Báo cáo tức thì:** Nhận thông báo báo cáo chi tiết trực tiếp qua Telegram ngay khi quy trình hoàn tất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Telegram Bot Token:** Để nhận lệnh tìm kiếm và gửi báo cáo.
- **OpenAI API Key:** Sử dụng cho các node AI Research Agent, Generate Email Content và Follow-up.
- **Google Maps API Key & Serper (hoặc API tìm kiếm tương đương):** Phục vụ việc truy vấn dữ liệu địa điểm và tìm kiếm thông tin liên hệ.
- **Google Sheets:** Tài khoản Google để lưu trữ danh sách lead tự động.
- **Gmail Account (OAuth2):** Tài khoản Gmail để tự động gửi email chăm sóc khách hàng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này, vào giao diện n8n Editor, chọn **Add workflow** -> **Import from JSON** và dán vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các thành phần trọng yếu sau:
- **Telegram Message Trigger & Send Telegram Report:** Kết nối với credentials Telegram Bot của các sếp và cấu hình Chat ID nhận tin nhắn.
- **Post to Maps API & Các API HTTP Request (Email/LinkedIn Search):** Điền chính xác API Keys của Google Maps và dịch vụ tìm kiếm mở rộng để hệ thống có thể bóc tách dữ liệu địa điểm và mạng xã hội.
- **AI Research Agent, Generate Email Content, Generate Follow-up Email:** Chọn credentials OpenAI API, kiểm tra lại model (khuyên dùng `gpt-4o`) và tuỳ chỉnh prompt nếu muốn phong cách viết email phù hợp với ngành hàng của các sếp.
- **Append Lead to Sheets:** Kết nối tài khoản Google Sheets OAuth2, chọn đúng file Google Sheets và sheet mà các sếp muốn lưu trữ thông tin lead.
- **Send Initial Email & Send Follow-up Email:** Kết nối credentials Gmail OAuth2 để cho phép n8n gửi email tự động thay mặt các sếp.
- **Deduplicate All Fields:** Node này giúp lọc trùng các lead đã từng xuất hiện trong các lần chạy trước (`removeItemsSeenInPreviousExecutions`), giúp tiết kiệm tài nguyên và không spam khách hàng.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test workflow**) bằng cách gửi một tin nhắn yêu cầu qua Telegram (ví dụ: *"Digital marketing agencies in New York"*).
- Kiểm tra dữ liệu trả về ở Google Sheets và xem email nháp/gửi đi (nếu bật chế độ live).
- Bật công tắc **Active** để workflow chính thức hoạt động tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Kết hợp thêm node Slack hoặc Discord bên cạnh Telegram để đội ngũ sales nhận được thông báo lead nóng ngay lập tức.
- **Tối ưu Prompt AI:** Tinh chỉnh prompt trong các node OpenAI để email chào hàng có độ cá nhân hóa cao hơn dựa trên website hoặc lĩnh vực hoạt động của doanh nghiệp được tìm thấy trên Google Maps.
- **Quản lý trạng thái Lead:** Thêm các cột trạng thái (Đã gửi email, Đã phản hồi, Từ chối...) trong Google Sheets để dễ dàng theo dõi phễu bán hàng.

### 📌 Kết luận
Workflow này là một cỗ máy tự động hóa hoàn hảo giúp đội ngũ B2B tối ưu hóa quy trình tìm kiếm và tiếp cận khách hàng bằng sức mạnh của AI và tự động hóa. Hãy triển khai ngay hôm nay để gia tăng tỷ lệ chuyển đổi và bứt phá doanh số cho doanh nghiệp của các sếp nhé!