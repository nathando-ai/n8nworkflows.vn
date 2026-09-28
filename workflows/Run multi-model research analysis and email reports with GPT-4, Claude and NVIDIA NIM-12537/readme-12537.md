---
title: "🚀 Tự động phân tích nghiên cứu đa mô hình và gửi báo cáo qua email với GPT‑4, Claude và NVIDIA NIM"
description: "Workflow tự động thu thập dữ liệu, phân tích bằng nhiều mô hình LLM, và gửi báo cáo chi tiết qua email, giảm thời gian xử lý và tăng độ chính xác."
slug: "tu-ong-phan-tich-nhiem-viec-anh-voi-gpt4-claude-nvidia-nim"
tags: [n8n, automation, no-code, ai, llm, email]
keywords: [n8n workflow, tự động hóa, LLM, GPT‑4, Claude, NVIDIA NIM, báo cáo email]
---

# 🚀 Tự động phân tích nghiên cứu đa mô hình và gửi báo cáo qua email với GPT‑4, Claude và NVIDIA NIM

Bạn đang phải xử lý hàng nghìn tài liệu nghiên cứu, trích xuất dữ liệu, phân tích nội dung và gửi báo cáo cho khách hàng? Việc làm thủ công không chỉ tốn thời gian mà còn dễ gây sai sót. Workflow này giúp bạn **tự động hoá toàn bộ quy trình**: từ nhận dữ liệu, phân tích bằng nhiều mô hình LLM, lưu trữ, gửi thông báo Slack, tới gửi báo cáo chi tiết qua email – **không cần viết một dòng code**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ làm thủ công xuống chỉ vài phút.
- **Độ chính xác cao**: Sử dụng GPT‑4, Claude và NVIDIA NIM để phân tích đa chiều.
- **Tự động hóa liên tục**: Workflow chạy 24/7, không cần can thiệp.
- **Cá nhân hóa báo cáo**: Gửi email tùy chỉnh theo yêu cầu khách hàng.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
| Dịch vụ / API | Mô tả | Key / Credential cần thiết |
|----------------|-------|-----------------------------|
| **Slack** | Gửi thông báo khi workflow bắt đầu/hoàn thành | Slack OAuth Token |
| **PostgreSQL** | Lưu trữ dữ liệu phân tích | Host, Port, Database, User, Password |
| **Email (SMTP)** | Gửi báo cáo qua email | SMTP Host, Port, Username, Password, From Address |
| **OpenAI (GPT‑4)** | Truy cập mô hình GPT‑4 | OpenAI API Key |
| **Anthropic (Claude)** | Truy cập mô hình Claude | Anthropic API Key |
| **NVIDIA NIM** | Truy cập mô hình NVIDIA NIM | NVIDIA NIM API Key |
| **HTTP Request** | Gọi các API bên ngoài (nếu cần) | API Key / Token tùy dịch vụ |
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/12537) hoặc sao chép nội dung JSON.
2. Mở **n8n Editor** → **Import** → **Import from file** hoặc **Import from clipboard**.
3. Chọn file JSON hoặc dán nội dung, rồi nhấn **Import**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Mô tả | Cài đặt cần chỉnh |
|------|-------|--------------------|
| **Webhook** | Kích hoạt workflow khi nhận request | URL, HTTP Method, Authentication (nếu cần) |
| **Set** | Định nghĩa các biến dữ liệu đầu vào | `inputData`, `modelChoice`, `emailRecipient`, v.v. |
| **Code** | Xử lý logic tùy chỉnh (ví dụ: chuẩn bị prompt) | Đảm bảo `nodeData` đúng định dạng |
| **Wait** | Thời gian chờ giữa các bước (để tránh rate‑limit) | `waitTime` (ms) |
| **Merge** | Kết hợp dữ liệu từ nhiều nguồn | `mode` (e.g., `mergeAll`) |
| **Switch** | Chọn mô hình phân tích (GPT‑4 / Claude / NVIDIA) | `conditions` dựa trên `modelChoice` |
| **Postgres** | Lưu trữ kết quả | `Connection`, `Table`, `Query` |
| **EmailSend** | Gửi báo cáo | `SMTP Credentials`, `To`, `Subject`, `Body` (HTML/Markdown) |
| **Slack** | Gửi thông báo | `Slack Credentials`, `Channel`, `Message` |
| **StickyNote** | Ghi chú nội bộ | Không cần cấu hình |
| **HttpRequest** | Gọi API bên ngoài (ví dụ: lấy dữ liệu tài liệu) | `URL`, `Method`, `Headers`, `Body` |

> **Lưu ý**: Mỗi node **đối với credentials** cần được cấu hình trong phần **Credentials** của n8n. Nếu chưa có, tạo mới bằng cách nhấn **New** và điền thông tin API Key / OAuth Token.

### 3. Kích hoạt ⚡️

1. **Test run**: Chạy workflow với dữ liệu mẫu (bấm **Execute Workflow**). Kiểm tra log, xác nhận dữ liệu lưu trữ và email được gửi.
2. **Bật Active**: Khi mọi thứ ổn định, chuyển workflow sang trạng thái **Active** để tự động chạy khi webhook nhận request.

## ✍️ Mẹo & gợi ý nâng cao

- **Slack + Telegram**: Thêm node Slack hoặc Telegram để nhận cảnh báo ngay khi workflow bắt đầu hoặc gặp lỗi.
- **Log lưu trữ**: Sử dụng node **Postgres** hoặc **Google Sheets** để ghi lại lịch sử chạy, thời gian, kết quả.
- **Báo cáo định kỳ**: Thêm node **Cron** để gửi báo cáo hàng ngày/tuần cho khách hàng.
- **Tùy chỉnh prompt**: Sử dụng node **Code** để động tạo prompt dựa trên dữ liệu đầu vào, giúp mô hình trả về kết quả chính xác hơn.

## 📌 Kết luận

Workflow này là **đối tác đáng tin cậy** cho các sếp muốn tự động hoá quy trình phân tích nghiên cứu, giảm tải công việc thủ công và nâng cao chất lượng báo cáo. Hãy thử ngay, điều chỉnh các tham số phù hợp với doanh nghiệp của bạn, và trải nghiệm sự tự do của **no‑code AI automation**!

---