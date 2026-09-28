---
title: "🚀 Tự động trích xuất thông tin kênh YouTube và lưu vào Google Docs với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy toàn bộ metadata kênh YouTube qua RapidAPI từ form nhập liệu và lưu trữ gọn gàng vào Google Docs."
slug: "trich-xuat-youtube-metadata-google-docs-n8n"
tags: [n8n, automation, youtube, google-docs, rapidapi, no-code]
keywords: [n8n workflow, tự động hóa youtube, trích xuất metadata youtube, rapidapi youtube, n8n google docs]
---

# 🚀 Tự động trích xuất thông tin kênh YouTube và lưu vào Google Docs

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thủ công đi tìm kiếm, copy và paste từng thông tin của các đối thủ hoặc KOLs trên YouTube (như số lượngSubscriber, tổng số view, mô tả, từ khóa...) vào file báo cáo không? Việc này vừa tốn thời gian, lại dễ thiếu sót khi cần làm nghiên cứu thị trường (Market Research).

Đừng lo, bài viết này sẽ hướng dẫn các sếp cách "lên đồ" một workflow n8n tự động hóa 100%: Chỉ cần nhập link kênh YouTube vào một form web, hệ thống sẽ tự động quét thông tin qua RapidAPI, xử lý gọn gàng và lưu thẳng vào Google Docs một cách chuyên nghiệp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần copy-paste thủ công, xử lý hàng loạt thông tin kênh chỉ trong vài giây.
- **Dữ liệu chuẩn xác, trực quan:** Dữ liệu trả về được code lại tự động kèm emoji và định dạng Markdown cực kỳ dễ đọc.
- **Lưu trữ tập trung:** Tự động đồng bộ toàn bộ báo cáo phân tích vào Google Docs để dễ dàng chia sẻ với team.
- **Hoạt động 24/7:** Sẵn sàng nhận yêu cầu bất cứ lúc nào thông qua giao diện Web Form thân thiện.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị sẵn:
- Một instance n8n (Cloud hoặc Self-hosted).
- Tài khoản **RapidAPI** và đăng ký một gói API chuyên cung cấp YouTube Channel Metadata.
- Tài khoản **Google Cloud / Google Workspace** để cấu hình Google Docs Credentials (OAuth2 hoặc Service Account).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy và paste trực tiếp vào n8n Editor của mình. Workflow bao gồm 4 nodes chính hoạt động nhịp nhàng với nhau:
1. **On form submission** (`formTrigger`)
2. **YouTube Channel Metadata** (`httpRequest`)
3. **Reformat** (`code`)
4. **Add Data in Google Docs** (`googleDocs`)

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không lỗi, các sếp cần chú ý cấu hình kỹ các node sau:

- **Node: On form submission (`formTrigger`)**
  - Đây là điểm khởi đầu, tạo một trang web form nhỏ để nhập URL kênh YouTube. Các sếp có thể tuỳ chỉnh tiêu đề form cho phù hợp.

- **Node: YouTube Channel Metadata (`httpRequest`)**
  - Node này dùng để gọi API từ RapidAPI. Các sếp cần điền đúng **Endpoint URL** của dịch vụ RapidAPI chọn mua, đồng thời gắn **API Key** và **API Host** vào phần Header của HTTP Request. Biến truyền vào body/query sẽ là URL kênh YouTube lấy từ form trước đó.

- **Node: Reformat (`code`)**
  - Node này chạy một đoạn mã Javascript ngắn để bóc tách các trường dữ liệu thô (Raw JSON) trả về từ API thành một chuỗi văn bản sạch sẽ (`docContent`), có kèm emoji và định dạng tiêu đề đẹp mắt. Không cần sửa code trừ khi các sếp muốn đổi cách hiển thị.

- **Node: Add Data in Google Docs (`googleDocs`)**
  - **Credentials:** Kết nối tài khoản Google của các sếp.
  - **Operation:** Chọn `Update` (hoặc Append tùy theo cấu trúc tài liệu).
  - **Document ID:** Dán ID của Google Docs mà các sếp muốn lưu dữ liệu vào (lấy phần chuỗi dài trên URL của file Google Docs).
  - **Text:** Map biến `{{ $json.docContent }}` từ node Reformat vào đây.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** để thử nghiệm nhập một link YouTube bất kỳ vào form và kiểm tra kết quả trên Google Docs.
- Nếu mọi thứ hiển thị ngon lành, hãy bật nút **Active** ở góc trên bên phải để workflow chính thức chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống xịn sò hơn nữa, các sếp có thể mở rộng workflow này bằng cách:
- **Tích hợp Telegram/Slack Bot:** Gửi thông báo ngay về nhóm chat khi có một kênh YouTube mới được phân tích xong.
- **Lưu vào Google Sheets thay vì Docs:** Nếu muốn làm bảng so sánh nhiều kênh, hãy đổi node Google Docs thành Google Sheets để tạo bảng dữ liệu dạng cột.
- **AI Phân tích sâu:** Thêm một node OpenAI/Claude sau bước Reformat để AI tự động viết tóm tắt điểm mạnh, điểm yếu của kênh YouTube đó dựa trên metadata thu được.

### 📌 Kết luận
Workflow "Extract YouTube Channel Metadata to Google Docs" là một "vũ khí" cực kỳ lợi hại cho anh em làm Content Creator, Marketer hay Nghiên cứu thị trường. Chỉ với vài bước cài đặt cơ bản trên n8n, các sếp đã tiết kiệm được hàng tá thời gian để tập trung vào những chiến lược quan trọng hơn. Chúc các sếp cài đặt thành công!