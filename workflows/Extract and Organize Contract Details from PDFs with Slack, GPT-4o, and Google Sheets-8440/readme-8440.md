---
title: "🚀 Tự động hóa quản lý hợp đồng từ Slack, GPT-4o đến Google Sheets với n8n"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động trích xuất thông tin hợp đồng PDF/Word từ Slack, sử dụng GPT-4o phân tích và lưu trữ vào Google Sheets."
slug: "tu-dong-hoa-quan-ly-hop-dong-slack-gpt-4o-google-sheets"
tags: [n8n, automation, ai, openai, google-sheets, slack]
keywords: [n8n workflow, tự động hóa hợp đồng, trích xuất pdf ai, gpt-4o google sheets, slack automation]
---

# 🚀 Tự động hóa quản lý hợp đồng từ Slack, GPT-4o đến Google Sheets

Việc quản lý hợp đồng thủ công từ trước đến nay luôn ngốn rất nhiều thời gian và dễ xảy ra sai sót. Các bộ phận pháp lý hay vận hành thường xuyên phải đau đầu khi phải đọc từng file hợp đồng, copy thủ công các thông tin như tên khách hàng, giá trị hợp đồng, thời hạn hiệu lực vào file Excel hoặc Google Sheets. 

Chưa kể, việc lưu trữ phân tán giữa các công cụ khiến việc tìm kiếm lại vô cùng khó khăn. Workflow này sẽ giải quyết triệt để nỗi đau đó bằng cách tự động hóa 100% quy trình: Nhận file từ Slack 👉 Đọc nội dung 👉 AI phân tích 👉 Lưu Google Sheets 👉 Báo cáo lại trên Slack. Các sếp không cần phải tốn một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn cảnh đọc hợp đồng thủ công và gõ phím mỏi tay.
- **Độ chính xác cao:** GPT-4o tự động trích xuất chính xác các trường dữ liệu quan trọng (Client, Giá trị, Ngày ký, Ngày hiệu lực...).
- **Đồng bộ thời gian thực:** Mọi hợp đồng mới đều được ghi nhận ngay lập tức vào Google Sheets và thông báo về Slack cho team nắm bắt.
- **Hoạt động 24/7:** Hệ thống âm thầm làm việc bất kể ngày đêm, không bỏ sót một tài liệu nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã chạy sẵn sàng (Cloud hoặc Self-hosted).
- **Tài khoản Slack:** Có quyền cấu hình Bot, nhận file và gửi tin nhắn trong kênh chỉ định.
- **Tài khoản OpenAI:** Có API Key và hạn mức sử dụng (để dùng model `gpt-4o`).
- **Google Sheets:** Đã chuẩn bị sẵn một file Google Sheets với các cột: `Client`, `Service Provider`, `Effective Date`, `Expiration Date`, `Signature Date`, và `Contract Value`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy toàn bộ mã JSON của workflow này, vào n8n Editor chọn **Import from Clipboard** hoặc kéo thả file JSON vào giao diện là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, hệ thống sẽ gồm 12 nodes. Các sếp cần chú ý cấu hình các node quan trọng sau:

- **Receive Contract File (`slackTrigger`):** Kết nối tài khoản Slack của các sếp và chọn kênh (Channel) mà team sẽ tải file hợp đồng lên.
- **Check File Format (`switch`):** Node này kiểm tra định dạng file tải lên. Hỗ trợ 2 định dạng chính là PDF và Word (.docx). Nếu file khác định dạng, hệ thống sẽ tự động chuyển sang nhánh báo lỗi.
- **Download PDF & Convert Word to PDF (`httpRequest`):** Các node này dùng thông tin từ Slack để tải file về hệ thống n8n chuẩn bị cho bước đọc chữ.
- **Extract Text from PDF & Extract Text from PDF1 (`extractFromFile`):** Trích xuất toàn bộ văn bản thô từ file tài liệu.
- **AI model (`lmChatOpenAi`) & Structure Output (`outputParserStructured`):** Cấu hình credentials của OpenAI, chọn model `gpt-4o` và thiết lập cấu trúc schema đầu ra (Client, Service Provider, Dates, Contract Value...).
- **Analyze Contract Content (`agent`):** Node AI Agent trung tâm, kết hợp AI model và bộ cấu trúc để đọc hiểu text và phân loại dữ liệu chính xác.
- **Save to Google Sheets (`googleSheets`):** Kết nối tài khoản Google OAuth2, chọn đúng file Sheet và Sheet Name đã chuẩn bị sẵn để map các trường dữ liệu AI trả về vào đúng cột.
- **Notify on Slack (`slack` & `Send Error Message`):** Cấu hình gửi thông báo thành công hoặc báo lỗi về đúng kênh Slack của team.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử bằng cách upload một file hợp đồng mẫu lên kênh Slack đã chọn.
- Kiểm tra kết quả trên Google Sheets và Slack xem dữ liệu đã đổ về chuẩn xác chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để workflow chính thức vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ báo qua Slack, các sếp có thể kết hợp thêm node Telegram hoặc Email để gửi bản tóm tắt hợp đồng cho Ban Giám đốc.
- **Lưu trữ file thông minh:** Kết hợp thêm node Google Drive hoặc OneDrive để tự động lưu bản cứng file hợp đồng vào thư mục tương ứng của từng khách hàng.
- **Báo cáo định kỳ:** Tạo thêm một nhánh trigger theo thời gian (Schedule) để tổng hợp số lượng hợp đồng đã ký trong tuần/tháng gửi vào nhóm chat chung.

### 📌 Kết luận
Tự động hóa quy trình quản lý hợp đồng với n8n, Slack và GPT-4o là bước tiến lớn giúp doanh nghiệp tối ưu hóa vận hành, giảm thiểu rủi ro pháp lý và tiết kiệm hàng đống thời gian quản trị. Hãy triển khai ngay hôm nay để đưa doanh nghiệp lên một tầm cao mới về tốc độ và sự chuyên nghiệp!