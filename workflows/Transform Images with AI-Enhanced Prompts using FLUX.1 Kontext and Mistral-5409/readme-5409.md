---
title: "🚀 Tự động sinh ảnh AI với FLUX.1 Kontext & Mistral: Workflow n8n hoàn chỉnh"
description: "Giải pháp tự động 100% không code để lấy dữ liệu từ Airtable, tạo prompt AI, sinh ảnh với Fal AI và lưu trữ kết quả, giúp doanh nghiệp tiết kiệm thời gian và nâng cao chất lượng nội dung."
slug: "tuyendung-sinh-anh-ai-flux-mistral"
tags: [n8n, automation, no-code, ai, image-generation]
keywords: [n8n workflow, tự động hóa, AI image generation, flux, mistral, fal ai]
---

# 🚀 Tự động sinh ảnh AI với FLUX.1 Kontext & Mistral

Bạn đang phải làm thủ công lấy dữ liệu, tạo prompt, gọi API sinh ảnh và lưu trữ kết quả? Điều này không chỉ tốn thời gian mà còn dễ xảy ra lỗi. Workflow n8n dưới đây sẽ giúp bạn tự động hoá toàn bộ quy trình: từ lấy dữ liệu Airtable, tạo prompt bằng LLM, sinh ảnh qua Fal AI (FLUX.1 Kontext), kiểm tra trạng thái, và lưu kết quả trở lại Airtable – hoàn toàn không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài phút thủ công thành vài giây tự động.  
- **Độ chính xác cao**: Prompt được tạo tự động, giảm sai sót do con người.  
- **Tự động hoá liên tục**: Chạy 24/7, không cần can thiệp.  
- **Dễ dàng mở rộng**: Thêm Slack, Telegram, hoặc gửi báo cáo định kỳ chỉ vài dòng cấu hình.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
| Dịch vụ | Tên Credential | Mô tả |
|---------|----------------|-------|
| Airtable | `airtableTokenApi` | API token của Airtable (để đọc/ghi dữ liệu). |
| Mistral Cloud | `mistralCloudApi` | API key của Mistral Cloud (để gọi LLM). |
| Fal AI (FLUX KONTEXT MAX) | `falAiApiToken` | Token API của Fal AI (được nhập trong node HTTP Request). |
| (Tùy chọn) Email/Slack | `slackToken` | Nếu muốn gửi thông báo. |
:::

> **Lưu ý**: Đảm bảo các bảng Airtable đã có cột `Base Image URL`, `Description`, `Situation`, `Prompt`, `Generated Image URL` và `Status`.

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/5409).  
2. Trong n8n, vào **Workflows** → **Import** → **Upload file** → chọn file JSON.  
3. Hoặc copy toàn bộ nội dung JSON và dán vào **Editor** → **Paste JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên Node | Cấu hình cần chỉnh | Ghi chú |
|------|----------|--------------------|---------|
| 1 | `When clicking ‘Execute workflow’` | Không cần chỉnh | Trigger thủ công. |
| 2 | `Airtable` (search) | `Base ID`, `Table name`, `Search column` | Đặt `Base ID` và `Table name` của bảng chứa dữ liệu. |
| 3 | `Generate Prompt` (chainLlm) | `Prompt template` | Sử dụng dữ liệu từ Airtable (`{{ $json["Description"] }}` + `{{ $json["Situation"] }}`). |
| 4 | `Generate Image` (httpRequest) | `URL`, `Headers`, `Body` | `URL`: `https://api.fal.ai/v1/models/fal-ai/flux-pro/kontext/max/inference` <br> `Headers`: `Authorization: Bearer {{ $credentials.falAiApiToken }}` <br> `Body`: JSON chứa `prompt` và `image_url`. |
| 5 | `Check IF Generated` (httpRequest) | `URL`, `Method` | Kiểm tra trạng thái của job. |
| 6 | `Wait` | `Seconds` | Thời gian chờ giữa các lần kiểm tra (ví dụ: 30s). |
| 7 | `Mistral Cloud Chat Model` (lmChatMistralCloud) | `Model`: `mistral-large-latest` | Dùng để xử lý prompt hoặc phân tích kết quả (tuỳ chọn). |
| 8 | `Edit Fields` (set) | `Fields to set` | Cập nhật `Prompt`, `Generated Image URL`, `Status`. |
| 9 | `Log Image Posts` (airtable update) | `Base ID`, `Table name`, `Record ID` | Ghi lại kết quả vào Airtable. |

> **Tip**: Đặt `Base ID` và `Table name` trong các node Airtable bằng cách click **Edit** → **Credentials** → **Add New** → chọn credential đã tạo.

#### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow thủ công, kiểm tra log từng node.  
2. Kiểm tra Airtable xem dữ liệu đã được cập nhật.  
3. Khi mọi thứ ổn, bật **Active** cho workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack**: Thêm node `Slack` sau `Log Image Posts` để gửi thông báo khi ảnh được sinh thành công.  
- **Lưu log**: Sử dụng node `Google Sheets` hoặc `MySQL` để lưu lịch sử sinh ảnh.  
- **Báo cáo định kỳ**: Kết hợp với node `Cron` để tự động chạy workflow hàng ngày.  
- **Tùy chỉnh prompt**: Thêm biến `Style` từ Airtable để đa dạng hoá phong cách ảnh.  

### 📌 Kết luận
Workflow này giúp các sếp chuyển từ quy trình thủ công sang tự động hoá hoàn toàn, giảm thiểu sai sót và tăng năng suất. Hãy thử ngay, tùy chỉnh theo nhu cầu và chia sẻ kết quả! 🚀

---

**Video hướng dẫn**  
[![Watch on YouTube](https://img.youtube.com/vi/0SVj70-dA0Q/maxresdefault.jpg)](https://www.youtube.com/watch?v=0SVj70-dA0Q)