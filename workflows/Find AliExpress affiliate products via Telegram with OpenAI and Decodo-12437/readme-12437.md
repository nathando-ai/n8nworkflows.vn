---
title: "🚀 Tự động tìm kiếm sản phẩm AliExpress Affiliate qua Telegram bằng OpenAI & Decodo"
description: "Xây dựng Bot Telegram thông minh tích hợp AI để tự động tìm kiếm sản phẩm trên AliExpress, tạo link affiliate và gửi trực tiếp vào nhóm một cách mượt mà."
slug: "tu-dong-tim-kiem-san-pham-aliexpress-affiliate-telegram-openai"
tags: [n8n, automation, no-code, telegram, openai, aliexpress, affiliate]
keywords: [n8n workflow, telegram bot affiliate, aliexpress affiliate automation, openai n8n, decodo scraping]
---

# 🚀 Tự động tìm kiếm sản phẩm AliExpress Affiliate qua Telegram bằng OpenAI & Decodo

Việc tìm kiếm thủ công các sản phẩm hot trên AliExpress để làm nội dung hay chia sẻ link tiếp thị liên kết (affiliate) vào các nhóm Telegram thường tốn rất nhiều thời gian, từ việc lọc từ khóa, cào dữ liệu đến tạo link tracking. 

Giải pháp? Workflow n8n tự động hóa toàn diện này sẽ biến con bot Telegram của các sếp thành một "cỗ máy" săn sale thực thụ. Chỉ cần người dùng gửi yêu cầu tìm kiếm vào nhóm, AI sẽ kiểm duyệt nội dung, tối ưu từ khóa, cào dữ liệu qua **Decodo**, tạo link Affiliate chính hãng và gửi trả lại một chiếc card sản phẩm cực kỳ chuyên nghiệp kèm hình ảnh và nút bấm tương tác!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [👉 Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Bot hoạt động 24/7 trong nhóm Telegram, tự phản hồi ngay khi khách hàng/thành viên hỏi tìm sản phẩm.
- **Kiểm duyệt thông minh:** Sử dụng OpenAI để loại bỏ các nội dung spam, link rác hoặc yêu cầu không phù hợp trước khi xử lý.
- **Tạo Link Affiliate tự động:** Chuyển đổi URL sản phẩm thô thành link tracking kiếm hoa hồng thông qua AliExpress Affiliate API.
- **Trải nghiệm mượt mà:** Gửi hình ảnh, thông tin chi tiết và hỗ trợ các nút bấm (inline buttons) để người dùng yêu cầu thêm tùy chọn sản phẩm.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- **Telegram Bot Token:** Tạo qua `@BotFather` và thêm bot vào nhóm Telegram (cấp quyền Admin).
- **OpenAI API Key:** Dùng cho các node `Message a model`, `Creating a professional search term` và `Wording for message`.
- **Decodo API Credentials:** Dùng cho các node data scraping (`Data scraping1`, `data scraping`).
- **AliExpress Affiliate API Credentials:** Dùng cho các node tạo link affiliate (`Creating an affiliate link`, `Creating an affiliate link3`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này hoặc copy trực tiếp mã nguồn.
- Mở n8n Editor của các sếp, chọn **Import from File** hoặc dán (Paste) trực tiếp vào không gian làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công, các sếp cần cấu hình lại các thông số sau:
- **Telegram Trigger & Telegram Nodes:** Kết nối với `Telegram API` credential của các sếp. Đảm bảo bot đã được add vào group và có quyền đọc/ghi tin nhắn.
- **OpenAI Nodes (`Message a model`, `Creating a professional search term`, `Wording for message`):** Chọn `OpenAI API` credential và kiểm tra model (khuyến nghị dùng `gpt-4o-mini` hoặc `gpt-4o` tùy nhu cầu tối ưu chi phí).
- **Decodo Nodes (`Data scraping1`, `data scraping`):** Cấu hình `Decodo API` credentials để bot có thể cào dữ liệu sản phẩm từ AliExpress một cách chính xác.
- **AliExpress Affiliate Nodes (`Creating an affiliate link`, `Creating an affiliate link3`):** Điền thông tin `AliExpress Affiliate API` credentials (App Key & Secret) để hệ thống sinh link hoa hồng chuẩn xác.
- **Các node If & Code JavaScript:** Kiểm tra kỹ logic nhóm chat ID (`Checking if we are in a certain group`) để đảm bảo bot chỉ hoạt động trong các group được phép.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử gửi một tin nhắn yêu cầu tìm kiếm sản phẩm mẫu vào nhóm Telegram để kiểm tra luồng dữ liệu.
- Sau khi test thành công, bật nút **Active** ở góc trên bên phải để bot chính thức "lên sóng".

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Kết hợp thêm node Slack hoặc Discord để đội ngũ quản trị nhận cảnh báo khi có từ khóa vi phạm hoặc lỗi API xảy ra.
- **Lưu lịch sử tìm kiếm:** Tích hợp thêm Google Sheets hoặc Airtable node để lưu lại các từ khóa mà khách hàng hay tìm kiếm, từ đó phân tích xu hướng thị trường.
- **Tùy chỉnh ngôn ngữ:** Tinh chỉnh system prompt trong các node OpenAI để bot trả lời bằng giọng điệu hài hước, thân thiện hoặc chuyên nghiệp theo phong cách thương hiệu của các sếp.

### 📌 Kết luận
Workflow này là một "vũ khí" cực mạnh cho các làm nội dung, MMO hay xây dựng cộng đồng săn sale Telegram. Triển khai ngay để tối ưu hóa nguồn thu nhập thụ động từ Affiliate mà không cần tốn công chăm sóc thủ công từng tin nhắn!