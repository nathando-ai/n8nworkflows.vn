---
title: "🚀 Tự động Gợi ý Deal Mua Sắm Cá Nhân Hóa qua Email với Bright Data & GPT-4o-mini"
description: "Xây dựng hệ thống tự động cào dữ liệu ưu đãi từ website, phân tích bằng AI và gửi email đề xuất deal theo yêu cầu của khách hàng thông qua Form."
slug: "tu-dong-goi-y-deal-mua-sam-qua-email-bright-data-gpt-4o-mini"
tags: [n8n, automation, no-code, sales, ai, bright-data, openai]
keywords: [n8n workflow, tự động hóa bán hàng, gợi ý deal ai, bright data n8n, gpt-4o-mini, form trigger]
---

# 🚀 Tự động Gợi ý Deal Mua Sắm Cá Nhân Hóa qua Email với Bright Data & GPT-4o-mini

Các sếp trong ngành sales, marketing hay thương mại điện tử chắc chắn hiểu rõ: việc thủ công tìm kiếm các chương trình giảm giá, lọc sản phẩm theo nhu cầu riêng của từng khách hàng và gửi email tư vấn tốn cực kỳ nhiều thời gian. Khách hàng thì ngày càng thiếu kiên nhẫn, nếu phản hồi chậm là họ bay màu ngay.

Giải pháp ở đây là gì? Hãy để workflow n8n này "gánh" hết! Hệ thống sẽ tự động hóa từ A-Z: nhận yêu cầu qua Form, cào dữ liệu deal hot từ website (ví dụ: MediaMarkt) bằng **Bright Data**, dùng AI **GPT-4o-mini** để chọn lọc deal chuẩn xác nhất theo sở thích khách hàng, đóng gói thành HTML đẹp mắt và gửi thẳng vào hộp thư của họ. Tất cả diễn ra chỉ trong vài giây mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Cá nhân hóa 100%:** Khách hàng điền form cần tìm món gì, AI sẽ đãi cát tìm vàng, chọn đúng các deal phù hợp nhất.
- **Tiết kiệm 95% thời gian:** Không còn cảnh lướt web thủ công tìm deal rồi copy paste gửi email nữa.
- **Tăng tỷ lệ chuyển đổi:** Email gửi đi nhanh chóng, trình bày chuyên nghiệp với HTML bắt mắt, kích thích khách hàng chốt đơn ngay lập tức.
- **Hoạt động tự động 24/7:** Khách submit form lúc nửa đêm, hệ thống vẫn phục vụ nhiệt tình không cần nhân sự túc trực.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản sau:
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Bright Data Account:** Tài khoản và API Key/Credentials để cào dữ liệu website (`Bright Data API`).
- **OpenAI Account:** API Key để sử dụng model GPT-4o-mini (`OpenAI API`).
- **SMTP Server:** Thông tin kết nối SMTP (Gmail, SendGrid, Amazon SES...) để gửi email tự động cho khách hàng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ kho lưu trữ n8n.
- Trong giao diện n8n Editor, bấm vào menu **Add workflow** -> **Import from File** và chọn file JSON vừa tải. Hoặc đơn giản là copy toàn bộ mã JSON và dán thẳng vào màn hình làm việc của n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Node `When User Completes Form` (Form Trigger):** 
  - Cấu hình các trường (fields) trên form để thu thập thông tin từ khách hàng (Ví dụ: Email nhận kết quả, Danh mục sản phẩm muốn tìm deal, Khoảng giá...).
- **Node `Get MediaMarkt Offers Website` (Bright Data):** 
  - Kết nối tài khoản `Bright Data` của các sếp.
  - Cấu hình URL trang web thương mại điện tử cần cào dữ liệu ưu đãi (mặc định trong template là MediaMarkt, các sếp có thể đổi sang trang web khác tùy nhu cầu).
- **Node `Extract Body and Title from Website` (HTML):** 
  - Giữ nguyên cấu hình trích xuất nội dung HTML từ kết quả trả về của Bright Data.
- **Node `Generate List of Deals by Category` (OpenAI / GPT-4o-mini):** 
  - Chọn credentials `OpenAI API`.
  - Thiết lập Prompt cho AI để nó lọc ra danh sách deal chuẩn xác dựa trên dữ liệu website và yêu cầu của người dùng từ form.
- **Node `Extract items from results` (Split Out):** 
  - Đảm bảo node này tách các deal thành từng item riêng lẻ để xử lý tiếp.
- **Node `Create HTML for Email` (Document Generator):** 
  - Tùy chỉnh mẫu HTML theo brand (thương hiệu) của các sếp để email trông chuyên nghiệp và bắt mắt nhất.
- **Node `Notify End User by Email` (Send Email):** 
  - Nhập thông tin kết nối `SMTP` của các sếp.
  - Cấu hình địa chỉ nhận (`To`) lấy từ đầu ra của Form (`{{ $('When User Completes Form').item.json.email }}`).
- **Node `Show Form Results Page` (Form):** 
  - Cấu hình trang hiển thị lời cảm ơn khi khách hàng hoàn thành việc submit form.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử bằng cách điền form mẫu để kiểm tra xem email gửi về có đúng nội dung không.
- Nếu mọi thứ chạy ngon lành, hãy gạt công tắc sang chế độ **Active** để chính thức đưa vào vận hành thực tế!

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack:** Thêm một node Telegram hoặc Slack ở đầu workflow để nhân viên sales nhận được thông báo ngay khi có khách hàng mới điền form tìm deal.
- **Lưu trữ vào Google Sheets:** Thêm node Google Sheets để lưu lại thông tin khách hàng và nhu cầu của họ, phục vụ cho việcRemarketing sau này.
- **Đa ngôn ngữ hóa:** Tinh chỉnh prompt của AI để có thể tự động dịch hoặc viết lại mô tả sản phẩm bằng tiếng Việt thật mượt mà, cuốn hút.

### 📌 Kết luận
Workflow này là một cỗ máy tự động hóa cực kỳ mạnh mẽ giúp các sếp tối ưu hóa quy trình chăm sóc khách hàng và đẩy mạnh doanh số mà không tốn sức. Hãy cài đặt ngay hôm nay để trải nghiệm sức mạnh của AI và No-code trong kinh doanh!