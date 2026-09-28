---
title: "🚀 Tự động quét Lead Google Maps và Viết Email Sale cá nhân hóa bằng AI với n8n"
description: "Hướng dẫn chi tiết workflow n8n tự động cào dữ liệu doanh nghiệp từ Google Maps qua Apify, phân tích website và sử dụng OpenAI để tạo email sale siêu cá nhân hóa."
slug: "tu-dong-quet-lead-google-maps-va-viet-email-sale-ai"
tags: [n8n, automation, apify, openai, google-sheets, lead-generation]
keywords: [n8n workflow, quét lead google maps, viết email sale ai, apify google maps scraper, openai email automation]
---

# 🚀 Tự động quét Lead Google Maps & Viết Email Sale cá nhân hóa bằng AI

Việc tìm kiếm khách hàng tiềm năng (Lead Generation) và viết từng email chăm sóc thủ công cho mỗi doanh nghiệp địa phương tốn rất nhiều thời gian và công sức. Các sếp có đang phải mất hàng giờ lướt Google Maps, copy thông tin rồi vắt óc nghĩ cách viết email sao cho không bị coi là spam?

Workflow n8n này sẽ tự động hóa 100% quy trình đó: Từ việc quét danh sách doanh nghiệp trên Google Maps, ghé thăm website của họ để hiểu họ kinh doanh gì, cho đến việc dùng **OpenAI** viết ra một bức email sale cực kỳ cá nhân hóa và lưu toàn bộ vào **Google Sheets**. Các sếp chỉ việc kiểm tra lại và bấm gửi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian**: Tự động hóa hoàn toàn từ khâu tìm kiếm lead, cào dữ liệu website đến soạn thảo email.
- **Email cá nhân hóa cao**: OpenAI sẽ đọc nội dung website của từng quán cà phê, tiệm spa, phòng gym... để đưa ra điểm nổi bật, giúp email có tỷ lệ phản hồi (reply rate) cao hơn hẳn.
- **Quản lý gọn gàng**: Mọi thông tin từ tên, số điện thoại, địa chỉ, website cho đến bản nháp email đều được đồng bộ thẳng vào Google Sheets.
- **Vận hành linh hoạt**: Dễ dàng tùy chỉnh từ khóa tìm kiếm (ngành nghề, khu vực) và thông tin dịch vụ của các sếp chỉ với vài cú click.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản sau:
- **n8n Instance** (v1.0 trở lên).
- **Apify Account**: Tài khoản Apify để sử dụng Actor quét Google Maps (`compass/google-maps-scraper`).
- **OpenAI API Key**: Để AI phân tích website và viết email.
- **Google Cloud Platform / Google Sheets**: Tài khoản kết nối Google Sheets để lưu trữ dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, sau đó dán trực tiếp vào giao diện n8n Editor (hoặc Import file JSON thông qua menu).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình các node quan trọng sau:

- **Node `Workflow Configuration` (Set)**: Mở node này và cấu hình các thông số chiến dịch:
  - `searchQuery`: Từ khóa và khu vực cần tìm (Ví dụ: *"Gyms in London"* hoặc *"Cafes in Shibuya"*).
  - `serviceName`: Tên sản phẩm/dịch vụ các sếp đang cung cấp.
  - `serviceStrength`: Điểm độc đáo (USP) dịch vụ của các sếp giúp giải quyết vấn đề cho khách hàng.
- **Node `Get user runs list` (Apify)**: Chọn credentials tài khoản Apify và cấu hình Actor `compass/google-maps-scraper`.
- **Node `Generate Personalized Email` (OpenAI)**: Kết nối OpenAI Credentials (`openAiApi`). Các sếp có thể tùy chỉnh System Prompt bên trong để đổi ngôn ngữ (tiếng Việt, tiếng Anh, tiếng Nhật...) hoặc giọng điệu email (thân thiện, chuyên nghiệp, hài hước...).
- **Node `Check Website URL Exists` (If)**: Đảm bảo workflow bỏ qua các doanh nghiệp không có website để tránh lỗi khi cào dữ liệu.
- **Node `Save to Google Sheets` (Google Sheets)**: Tạo sẵn một Google Sheet với các tiêu đề cột sau ở dòng đầu tiên:
  - `店舗名` (Store Name)
  - `住所` (Address)
  - `Webサイト` (Website)
  - `電話番号` (Phone Number)
  - `サイトから取得した情報` (Info from Website)
  - `生成されたメール件名` (Generated Subject)
  - `生成されたメール本文` (Generated Body)
  Sau đó chọn file Google Sheet này trong node.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thử với một vài dữ liệu mẫu từ nút `Manual Trigger`.
- Kiểm tra kết quả trả về trong Google Sheets. Nếu mọi thứ OK, hãy bật công tắc **Active** để workflow sẵn sàng hoạt động tự động theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Thêm một node Telegram hoặc Slack ở cuối workflow để bot bắn tin nhắn báo cáo ngay về máy mỗi khi có một lead mới được cào và viết email xong.
- **Kiểm duyệt trước khi gửi**: Thay vì chỉ lưu Google Sheets, các sếp có thể kết hợp thêm node gửi bản nháp vào Gmail Drafts để dễ dàng duyệt lại trước khi bấm gửi chính thức.
- **Giới hạn số lượng (Rate Limit)**: Điều chỉnh thông số `maxPlaces` trong node Configuration để kiểm soát số lượng lead cào mỗi lần chạy, tránh tốn quá nhiều credits của Apify và OpenAI.

### 📌 Kết luận
Tự động hóa phễu tìm kiếm khách hàng với AI và Google Maps chưa bao giờ dễ dàng đến thế. Hãy cài đặt ngay workflow này để tối ưu hóa đội ngũ sales và bứt phá doanh thu ngay hôm nay các sếp nhé!