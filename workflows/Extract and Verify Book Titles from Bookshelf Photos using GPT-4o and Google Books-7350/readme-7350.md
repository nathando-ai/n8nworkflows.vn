---
title: "🚀 Trích xuất và Xác thực Tựa sách từ Ảnh Kệ sách tự động với GPT-4o và Google Books"
description: "Hướng dẫn xây dựng workflow n8n sử dụng AI đa phương thức (GPT-4o) để đọc ảnh chụp kệ sách, trích xuất danh sách đầu sách và tự động đối chiếu xác thực qua Google Books API."
slug: "trich-xuat-xac-thuc-tua-sach-tu-anh-ke-sach-gpt-4o-google-books"
tags: [n8n, automation, no-code, multimodal-ai, openAI, google-books]
keywords: [n8n workflow, tự động hóa, trích xuất sách từ ảnh, GPT-4o analyze image, Google Books API, n8n OCR AI]
---

# 🚀 Trích xuất và Xác thực Tựa sách từ Ảnh Kệ sách tự động với GPT-4o và Google Books

Các sếp có bao giờ đứng trước một kệ sách dày đặc, muốn lưu lại toàn bộ tựa sách nhưng việc gõ thủ công từng tên sách vào Excel hoặc ứng dụng quản lý sách khiến chúng ta nản lòng? Hoặc đơn giản là các sếp là người kinh doanh nhà sách, thư viện và muốn số hóa hàng nghìn tựa sách chỉ bằng một bức ảnh chụp nhanh? 

Việc nhập liệu thủ công không chỉ tốn hàng giờ đồng hồ mà tỷ lệ sai sót, gõ sai chính tả tên tác giả, tựa sách là rất cao. Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ thông minh, kết hợp giữa sức mạnh AI đa phương thức của **OpenAI GPT-4o** và cơ sở dữ liệu **Google Books** để tự động hóa toàn bộ quy trình này trong chớp mắt!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chỉ cần gửi một bức ảnh chụp kệ sách, hệ thống tự lo phần còn lại.
- **AI thông minh:** Sử dụng GPT-4o để "nhìn" và đọc các tựa sách trên gáy sách hoặc bìa sách với độ chính xác cao.
- **Xác thực dữ liệu chuẩn xác:** Đối chiếu trực tiếp từng tựa sách với Google Books API để đảm bảo tên sách, tác giả là có thật và chính xác tuyệt đối.
- **Tối ưu thời gian:** Xử lý hàng chục, hàng trăm đầu sách chỉ trong vòng vài giây, trả về danh sách gọn gàng, đã được lọc trùng lặp (dedupes).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **OpenAI API Key** (Có quyền truy cập GPT-4o để phân tích hình ảnh).
- **Endpoint hoặc Front-end giao diện** (Gửi request chứa link ảnh `imageURL` dạng chuỗi chuỗi qua Webhook).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow trống trong n8n, sau đó copy toàn bộ mã nguồn JSON của workflow (hoặc import file JSON từ nguồn cung cấp) vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 8 nodes được liên kết chặt chẽ với nhau theo luồng xử lý từ Front-end tới AI và trả về kết quả:

- **Webhook:** Nhận dữ liệu đầu vào từ Front-end (hoặc các ứng dụng bên thứ ba). Request cần truyền lên một chuỗi `imageURL` chứa đường dẫn hình ảnh kệ sách.
- **Input normalized (Set):** Chuẩn hóa dữ liệu đầu vào từ Webhook, trích xuất đường dẫn ảnh để chuẩn bị chuyển sang bước phân tích của AI.
- **Analyze image (OpenAI):** Node quan trọng nhất sử dụng mô hình GPT-4o để đọc hình ảnh. Các sếp cần cấu hình **Credentials** cho OpenAI, chọn Operation là `Analyze` và Resource là `Image`. Node này sẽ "quét" bức ảnh và trả về danh sách các tựa sách nhận diện được dưới dạng text thô hoặc cấu trúc JSON.
- **Item list split (Code):** Nhận kết quả danh sách thô từ AI và sử dụng đoạn mã JavaScript để tách chúng thành từng item riêng biệt (từng cuốn sách độc lập), chuẩn bị cho bước xác thực.
- **Title validation (HTTP Request):** Gửi từng tựa sách vừa tách đến **Google Books API** để kiểm tra, xác thực xem tựa sách và tác giả đó có tồn tại thực tế hay không, đồng thời lấy thêm thông tin chuẩn.
- **Data normalized (Set):** Chuẩn hóa lại các trường dữ liệu trả về từ Google Books sau khi xác thực (Tên sách, tác giả, năm xuất bản, v.v.).
- **Reaggregates list (Code):** Gom nhóm (aggregate) các cuốn sách đã được xác thực lại thành một danh sách hoàn chỉnh, đồng thời thực hiện loại bỏ các cuốn bị trùng lặp (dedupes).
- **Respond to Webhook:** Gửi toàn bộ danh sách sách đã được làm sạch và xác thực trả ngược lại về Front-end cho người dùng.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi một lệnh Test qua Webhook với một tấm ảnh kệ sách thực tế để kiểm tra log.
- Sau khi kiểm tra mọi thứ chạy mượt mà, các sếp gạt công tắc sang **Active** để đưa vào sử dụng chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ tự động:** Thêm một node Google Sheets hoặc Airtable vào sau bước *Reaggregates list* để tự động lưu toàn bộ danh sách sách quét được vào bảng tính quản lý.
- **Tích hợp Chatbot:** Kết nối webhook này với Telegram Bot hoặc Zalo OA, khách hàng/nhân viên chỉ cần gửi ảnh vào chat là bot tự động trả về danh sách sách đã xác thực.
- **Xử lý lỗi (Error Handling):** Thêm Error Trigger để ghi log hoặc thông báo về Slack/Telegram nếu bức ảnh quá mờ khiến OpenAI không đọc được.

### 📌 Kết luận
Workflow này là một minh chứng tuyệt vời cho thấy sức mạnh kết hợp giữa AI đa phương thức và các API bên thứ ba trong n8n. Hãy triển khai ngay để số hóa tủ sách của các sếp hoặc xây dựng những tính năng tuyệt vời cho ứng dụng của mình nhé! Chúc các sếp thao tác thành công!