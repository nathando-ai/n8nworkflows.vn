---
title: "🚀 Tự động tạo System Prompt chuẩn chuyên gia cho LLM tích hợp Unli.dev với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động tạo system prompt tối ưu cho các mô hình ngôn ngữ lớn (LLM) thông qua API Unli.dev, giúp nâng cao hiệu suất AI."
slug: "tao-system-prompt-cho-llm-voi-unli-dev-n8n"
tags: [n8n, automation, ai, unli-dev, system-prompt, webhook]
keywords: [n8n workflow, tao system prompt, unli.dev api, ai automation, llm optimization, n8n webhook]
---

# 🚀 Tự động tạo System Prompt chuẩn chuyên gia cho LLM tích hợp Unli.dev với n8n

Viết một *System Prompt* chất lượng cao, chi tiết và hiệu quả cho các mô hình ngôn ngữ lớn (LLM) thường tốn rất nhiều thời gian và đòi hỏi kỹ năng Prompt Engineering chuyên sâu. Nếu các sếp đang phát triển các ứng dụng AI và cần một hệ thống tự động sinh system prompt chuẩn xác theo yêu cầu người dùng, workflow n8n này chính là giải pháp "tất cả trong một" vô cùng mạnh mẽ và không cần viết code phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Nhận yêu cầu qua Webhook và trả về System Prompt hoàn chỉnh ngay lập tức.
- **Tối ưu hóa LLM:** Tận dụng sức mạnh từ Unli.dev để sinh ra các prompt có cấu trúc chặt chẽ, giúp AI hoạt động chính xác hơn.
- **Tích hợp linh hoạt:** Dễ dàng kết nối với các ứng dụng bên ngoài như Postman, Frontend website, hay các bot chat nội bộ.
- **Tiết kiệm thời gian:** Không phải mất hàng giờ nghĩ cấu trúc prompt từ đầu cho từng Use Case khác nhau.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Unli.dev Account & API Key:** Tài khoản và thông tin xác thực (`httpHeaderAuth`) để gọi API từ Unli.dev.
- **Công cụ test:** Postman hoặc cURL (nếu muốn test API trực tiếp qua Webhook).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ JSON của workflow này và dán trực tiếp vào n8n Editor, hoặc import file JSON tải về từ kho lưu trữ.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 6 nodes chính hoạt động nhịp nhàng với nhau. Các sếp cần chú ý cấu hình các node sau:

- **Webhook (`Webhook`):** 
  - Đã được thiết lập sẵn path `systempromptgenerator` với phương thức `POST`. Các sếp sẽ dùng URL này (Production/Test URL) từ các ứng dụng bên ngoài hoặc Postman để gửi yêu cầu.
- **Set Prompt/Model (`Set Prompt/Model`) & Prepare API Body (`Prepare API Body`):**
  - Hai node này có nhiệm vụ nhận dữ liệu đầu vào từ Webhook, đóng gói tham số và cấu trúc lại payload gửi đi. Kiểm tra kỹ định dạng JSON đầu vào để đảm bảo truyền đúng biến (ví dụ: yêu cầu tạo prompt về lĩnh vực gì).
- **Unli.dev API (`Unli.Dev (Chat Completions)`):**
  - Node `httpRequest` gọi đến API Chat Completions của Unli.dev.
  - **Credentials:** Bắt buộc phải cấu hình `httpHeaderAuth` với API Key hợp lệ được cung cấp bởi Unli.dev.
- **Trích xuất kết quả (`Extract Answer`) & Phản hồi (`Respond to Webhook`):**
  - Node `Extract Answer` sẽ lọc lấy đoạn nội dung System Prompt từ kết quả trả về của LLM.
  - Node `Respond to Webhook` gửi trực tiếp kết quả hoàn chỉnh về cho client (Postman/Web app) vừa gọi request.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Node** hoặc **Test workflow** bằng cách gửi một request POST qua Postman vào Webhook URL.
- Sau khi kiểm tra dữ liệu trả về chính xác, gạt công tắc sang **Active** để đưa workflow vào vận hành chính thức 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ lịch sử:** Kết nối thêm một node Google Sheets hoặc Database (Supabase/PostgreSQL) ngay sau node *Extract Answer* để lưu lại tất cả các System Prompt đã được tạo ra, phục vụ cho việc tra cứu sau này.
- **Thông báo qua Telegram/Slack:** Thêm một node nhắn tin để thông báo cho đội ngũ dev biết mỗi khi có một System Prompt mới được generate thành công.
- **Tích hợp Frontend:** Xây dựng một giao diện web đơn giản (như Retool hoặc Form) gọi trực tiếp vào Webhook này để nhân viên kinh doanh hoặc content writer có thể tự tạo prompt mà không cần vào n8n.

### 📌 Kết luận
Với workflow **Generate AI System Prompts for LLMs with Unli.dev**, các sếp đã sở hữu ngay một "cỗ máy" tự động hóa việc sáng tạo prompt cực kỳ chuyên nghiệp và nhanh chóng. Hãy triển khai ngay vào hệ thống của mình để tối ưu hóa hiệu suất làm việc với AI nhé!