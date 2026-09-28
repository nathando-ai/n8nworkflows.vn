---
title: "🚀 Tự động tạo Metadata, Timestamps và Tags cho video YouTube bằng AI với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hoàn toàn quy trình tạo mô tả, mốc thời gian (timestamps) và thẻ (tags) cho video YouTube mới bằng Apify và Mistral AI."
slug: "tu-dong-hoa-tao-metadata-youtube-ai-n8n"
tags: [n8n, automation, no-code, youtube, ai, mistral-ai, apify, marketing]
keywords: [n8n workflow, tự động hóa youtube, tạo metadata youtube ai, mistral ai n8n, apify youtube scraper]
---

# 🚀 Tự động hóa tạo Metadata, Timestamps và Tags cho video YouTube với AI

Các sếp làm nội dung trên YouTube chắc hẳn đều hiểu cảm giác "ngán ngẩm" khi phải ngồi hàng giờ liền viết mô tả chuẩn SEO, sắp xếp mốc thời gian (timestamps) hay chọn thẻ (tags) phù hợp cho mỗi video mới xuất bản. Việc này không chỉ tốn thời gian mà đôi khi còn làm giảm cảm0 hứng sáng tạo.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n cực kỳ thông minh do tác giả Nasser xây dựng. Workflow này sẽ tự động phát hiện video mới, cào dữ liệu qua Apify, sử dụng trí tuệ nhân tạo (Mistral AI) để tạo ra bộ metadata hoàn chỉnh, sau đó tự động cập nhật ngược lại kênh YouTube của các sếp một cách mượt mà!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần tự viết description, tìm tags hay định dạng timestamps thủ công nữa.
- **Tối ưu SEO chuyên nghiệp:** AI (Mistral Large) sẽ phân tích nội dung để tạo ra metadata hấp dẫn, giữ chân người xem lâu hơn.
- **Tự động hóa 100%:** Ngay khi video mới được đăng tải hoặc qua trigger RSS/Channel, hệ thống sẽ tự động quét và cập nhật ngầm.
- **Đồng bộ trực tiếp:** Tự động đẩy kết quả hoàn thiện (Mô tả, Timestamps, Tags) thẳng vào video trên YouTube Studio.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API sau:
1. **n8n Instance:** (Self-hosted hoặc n8n Cloud).
2. **Tài khoản Apify:** Dùng để cào dữ liệu video YouTube mới nhất (Cần chuẩn bị API Token).
3. **Tài khoản Mistral AI Cloud:** Sử dụng mô hình `mistral-large-latest` để sinh nội dung thông minh.
4. **Google Cloud Console / YouTube API:** Cấu hình OAuth2 để n8n có quyền cập nhật video trên kênh YouTube của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, vào giao diện n8n Editor, chọn **Import from Clipboard** và dán vào là xong!

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 15 nodes được chia thành 5 giai đoạn chính, các sếp cần chú ý cấu hình các điểm sau:

- **Trigger New Video Posted (`rssFeedReadTrigger`):** Cần điền ID kênh YouTube của các sếp. Cách lấy: Vào trang kênh YouTube, lấy đoạn mã phía sau chữ `channel/` trong URL và gắn vào sau `?channel_id=`.
- **Apify Nodes (`Scrape Video`, `Check IF Finished`, `Wait`, `Get DataSet`):** Cần kết nối tài khoản Apify bằng Apify API Token để hệ thống có quyền cào dữ liệu video.
- **Mistral Cloud Chat Model (`lmChatMistralCloud`) & Structured Output Parser (`outputParserStructured`):** Kết nối API Key của Mistral Cloud. Node này đảm bảo AI trả về kết quả theo đúng cấu trúc JSON mong muốn (Timestamps, Description, Tags).
- **Generate Description (`chainLlm`):** Kiểm tra lại Prompt mặc định (nếu muốn tinh chỉnh giọng văn AI theo ý thích).
- **Update YTB Video (`youTube`):** Cần kết nối thông qua Google Cloud OAuth2 Credentials để cho phép n8n thực hiện thao tác `update` resource `video`.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một video mẫu để kiểm tra dữ liệu trả về từ Apify và Mistral AI có chính xác không.
- Sau khi kiểm tra mọi thứ chạy xanh mướt, hãy gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để nhận thông báo ngay khi AI đã tối ưu hóa và cập nhật xong video mới.
- **Lưu log vào Google Sheets:** Thêm node Google Sheets để ghi lại lịch sử các video đã được AI tạo metadata nhằm dễ dàng kiểm soát nội dung.
- **Đa dạng hóa ngôn ngữ:** Sửa prompt trong LLM để yêu cầu AI tạo mô tả bằng tiếng Anh, tiếng Việt hoặc song ngữ tùy thuộc vào đối tượng khán giả của kênh.

### 📌 Kết luận
Tự động hóa quy trình quản lý kênh YouTube chưa bao giờ dễ dàng đến thế với sức mạnh kết hợp giữa n8n, Apify và Mistral AI. Hãy cài đặt ngay workflow này để giải phóng sức lao động và tập trung toàn tâm toàn ý vào việc sáng tạo nội dung chất lượng cao!