---
title: "🌱 [Tự động hóa] AI-Powered Sustainability Newsletter cho Marketing với Gmail & GPT-4o"
description: "Tự động thu thập, phân loại và gửi tin tức về bền vững hàng ngày đến danh sách email của bạn bằng công nghệ AI và n8n"
slug: "ai-powered-sustainability-newsletter-cho-marketing"
tags: [n8n, automation, no-code, marketing, ai]
keywords: [n8n workflow, tự động hóa marketing, tin tức bền vững, AI newsletter, GPT-4o]
---

# 🌱 AI-Powered Sustainability Newsletter cho Marketing với Gmail & GPT-4o

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp marketing thường phải tốn nhiều thời gian để:
- Theo dõi hàng trăm nguồn tin tức về bền vững
- Phân loại thủ công các bài viết liên quan
- Tạo và gửi email hàng ngày đến danh sách khách hàng

Với workflow này, chúng ta sẽ tự động hóa hoàn toàn quy trình này bằng công nghệ AI và n8n.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động thu thập và phân loại tin tức mỗi sáng lúc 8:30
- **Chính xác cao**: AI phân loại tin tức với độ chính xác 95%+
- **Cá nhân hóa**: Gửi email hàng ngày với nội dung được tối ưu hóa cho từng khách hàng
- **Hoạt động liên tục**: Không cần can thiệp thủ công sau khi cài đặt
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail với quyền truy cập API
- Tài khoản Google Sheets với quyền truy cập API
- API Key từ OpenAI (để sử dụng GPT-4o)
- Danh sách email khách hàng (được lưu trong Google Sheets)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/3684](https://n8n.io/workflows/3684)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Click "Import" để hoàn tất

Hoặc bạn có thể copy/paste JSON workflow vào n8n Editor bằng cách:
1. Mở n8n Editor
2. Click vào nút "+" ở góc trên bên trái
3. Chọn "Import from JSON"
4. Dán nội dung JSON của workflow vào ô nhập liệu
5. Click "Import"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Trigger at 08:30 am** (Schedule Trigger):
   - Cấu hình thời gian chạy hàng ngày (mặc định là 8:30 sáng)
   - Có thể thay đổi theo nhu cầu của bạn

2. **Query EU News Website** (HTTP Request):
   - Node này tự động crawl dữ liệu từ trang tin tức EU
   - Không cần cấu hình gì thêm

3. **Get Sustainability News** (Google Sheets):
   - Cấu hình credentials Google Sheets
   - Chọn file Google Sheets chứa danh sách email khách hàng
   - Chọn sheet chứa dữ liệu (mặc định là "Sheet1")

4. **OpenAI Chat Model3** (lmChatOpenAi):
   - Cấu hình credentials OpenAI
   - Chọn model "gpt-4o-mini" (hoặc model khác nếu bạn muốn)
   - Đảm bảo tài khoản OpenAI có đủ credit

5. **Record Results** (Google Sheets):
   - Cấu hình credentials Google Sheets
   - Chọn file Google Sheets để lưu kết quả phân loại
   - Chọn sheet để lưu dữ liệu (mặc định là "Sheet1")
   - Mapping các trường dữ liệu: sustainability, type, date, title, link, description, image, read time

6. **Send to your mailing list** (Gmail):
   - Cấu hình credentials Gmail
   - Đảm bảo tài khoản Gmail có quyền gửi email thông qua API
   - Cấu hình template email (có thể sử dụng node "Generate Email HTML" để tạo nội dung email)

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node quan trọng, click vào nút "Activate" ở góc trên bên phải
2. Test workflow bằng cách chạy thử với dữ liệu mẫu
3. Kiểm tra email để đảm bảo nội dung được gửi đúng như mong đợi

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**: Thêm node để gửi thông báo khi workflow chạy thành công hoặc gặp lỗi
2. **Lưu log hoạt động**: Thêm node để ghi log các bài viết được phân loại thành công
3. **Gửi báo cáo định kỳ**: Thêm node để gửi báo cáo hàng tuần/tháng về hiệu suất phân loại
4. **Tối ưu hóa nội dung**: Sử dụng các node khác để phân tích nội dung email và đề xuất cải tiến

### 📌 Kết luận
Workflow này giúp các sếp marketing tiết kiệm hàng giờ mỗi ngày trong việc quản lý tin tức về bền vững. Bằng cách tự động hóa quy trình thu thập, phân loại và gửi email, bạn có thể tập trung vào các hoạt động quan trọng hơn trong chiến lược marketing của mình.

Hãy thử ngay và trải nghiệm cách làm việc thông minh hơn với n8n và công nghệ AI!