---
title: "🚀 Tự động trích xuất thông tin lịch trình PDF vào Google Sheets và gửi email thông báo với GPT-4.1-Mini"
description: "Hướng dẫn xây dựng workflow n8n tự động tải file PDF lịch trình, dùng OpenAI trích xuất dữ liệu thông minh, lưu trữ vào Google Sheets và gửi email xác nhận qua Gmail."
slug: "trich-xuat-pdf-vao-google-sheets-voi-gpt-va-gmail"
tags: [n8n, automation, no-code, openai, google-sheets, gmail]
keywords: [n8n workflow, trích xuất pdf tự động, ai extract pdf, google sheets automation, openai gpt-4.1-mini]
---

# 🚀 Tự động hóa trích xuất PDF lịch trình sang Google Sheets với AI và Gmail

Các sếp có bao giờ cảm thấy mệt mỏi khi phải mở từng file PDF lịch trình, hợp đồng, hóa đơn hay báo cáo để copy-paste dữ liệu thủ công vào Google Sheets? Công việc tẻ nhạt này không chỉ ngốn hàng giờ đồng hồ mà còn dễ dẫn đến sai sót nhầm lẫn dữ liệu.

Đừng lo, bài toán này sẽ được giải quyết triệt để 100% tự động bằng n8n workflow kết hợp sức mạnh siêu việt của OpenAI GPT và Gmail. Workflow này cho phép nhận các file PDF tải lên qua Form, xử lý hàng loạt bằng AI, tự động đồng bộ vào Google Sheets và gửi email xác nhận kết quả cho người dùng mà không cần đụng đến một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Xử lý hàng loạt file PDF cùng lúc, không cần nhập liệu thủ công.
- **Độ chính xác cực cao:** Tận dụng mô hình AI tiên tiến (`gpt-4.1-mini`) để bóc tách thông tin cấu trúc chính xác từ tài liệu không định dạng.
- **Đồng bộ thời gian thực:** Tự động ghi nhận dữ liệu vào Google Sheets kèm theo dấu thời gian (timestamp).
- **Trải nghiệm chuyên nghiệp:** Tự động gửi email thông báo kết quả cho người gửi ngay sau khi xử lý xong.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Cloud hoặc Self-hosted phiên bản v1.0.0 trở lên).
- **OpenAI API Key** (có sẵn số dư để gọi mô hình GPT).
- **Tài khoản Google Workspace** (để cấu hình Google Sheets và Gmail OAuth2).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow và paste trực tiếp vào trình soạn thảo n8n, hoặc import file JSON thông qua menu quản lý workflow.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Node `Form receives multiple PDF files` (`formTrigger`):** Node này tạo ra một giao diện web dạng form để người dùng upload nhiều file PDF cùng lúc. Các sếp có thể tùy chỉnh tiêu đề form, trường tải file cho phù hợp với nhu cầu.
- **Node `Split Files processes each PDF individually` (`splitOut`):** Giúp tách danh sách các file PDF được tải lên thành từng luồng riêng biệt để xử lý độc lập.
- **Node `Loop Over Items ensures each document` (`splitInBatches`):** Điều phối quá trình lặp qua từng file PDF một cách tuần tự và ổn định.
- **Node `OpenAI Chat Model` (`lmChatOpenAi`) & Node `Analyzes & extract PDF` (`informationExtractor`):** 
  - Chọn model là `gpt-4.1-mini`.
  - Cấu hình thông tin xác thực OpenAI API Key (`openAiApi`).
  - Viết prompt hướng dẫn AI cách nhận diện và trích xuất các trường dữ liệu cụ thể từ file PDF (ví dụ: Tên hành khách, ngày đi, địa điểm, chi phí...).
- **Node `Extracted information to Google Sheets` (`googleSheets`):** 
  - Chọn tài khoản Google Sheets OAuth2.
  - Chọn thao tác (Operation) là `appendOrUpdate` để thêm mới hoặc cập nhật dữ liệu.
  - Khớp nối (Map) các trường dữ liệu do AI trích xuất với các cột tương ứng trong Google Sheet của các sếp.
- **Node `Create Email` (`openAi`) & Node `email confirmation sent with results` (`gmail`):**
  - Cấu hình tài khoản Gmail OAuth2 để gửi email.
  - Tùy chỉnh nội dung email xác nhận kết quả trích xuất gửi đến người dùng.

#### 3. Kích hoạt ⚡️
- Bấm nút **Test Workflow** và upload thử một vài file PDF mẫu lên form để kiểm tra dữ liệu trả về trong Google Sheets và Gmail.
- Nếu mọi thứ chạy trơn tru, các sếp bật công tắc **Active** ở góc trên bên phải để đưa workflow vào vận hành thực tế 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng định dạng:** Không chỉ PDF, các sếp hoàn toàn có thể mở rộng workflow để xử lý file Word (`.docx`), Excel (`.xlsx`) hoặc hình ảnh hóa đơn (`.png`, `.jpg`).
- **Gửi thông báo qua Slack/Telegram:** Thêm node Slack hoặc Telegram vào sau bước trích xuất thành công để bắn tin nhắn thông báo tức thì vào nhóm chat nội bộ của công ty.
- **Lưu trữ file:** Thêm bước tự động lưu bản sao file PDF gốc lên Google Drive hoặc OneDrive để dễ dàng tra cứu về sau.

### 📌 Kết luận
Workflow trích xuất PDF tự động này chính là trợ thủ đắc lực giúp doanh nghiệp tối ưu hóa quy trình hành chính, loại bỏ khâu nhập liệu thủ công nhàm chán. Hãy áp dụng ngay hôm nay để nâng cấp hệ thống tự động hóa của các sếp lên một tầm cao mới!