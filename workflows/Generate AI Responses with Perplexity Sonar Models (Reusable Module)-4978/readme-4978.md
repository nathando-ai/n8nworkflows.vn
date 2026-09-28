---
title: "🚀 Tích hợp Perplexity Sonar API làm Sub-Workflow thông minh trong n8n"
description: "Hướng dẫn xây dựng và sử dụng module tái sử dụng (reusable module) gọi Perplexity Sonar Models để trả lời câu hỏi và tìm kiếm thông tin bằng AI với n8n."
slug: "tich-hop-perplexity-sonar-api-trong-n8n"
tags: [n8n, automation, no-code, ai, perplexity, api]
keywords: [n8n workflow, perplexity api, sonar model, tự động hóa ai, sub workflow n8n]
---

# 🚀 Tích hợp Perplexity Sonar API làm Sub-Workflow thông minh trong n8n

Các sếp có bao giờ cảm thấy việc lặp đi lặp lại cấu hình gọi LLM (Large Language Model) ở nhiều workflow khác nhau vừa tốn thời gian, vừa khó bảo trì chưa? Thay vì viết lại từng đoạn HTTP Request phức tạp, chúng ta hoàn toàn có thể đóng gói nó thành một **Sub-Workflow (Reusable Module)** cực kỳ gọn gàng.

Bài viết này sẽ hướng dẫn các sếp cách triển khai workflow **Generate AI Responses with Perplexity Sonar Models** do tác giả *Aleksey Panov* thiết kế. Workflow này hoạt động như một module con, nhận tham số đầu vào (`SystemPrompt` và `UserPrompt`) từ workflow chính, sau đó gọi trực tiếp Perplexity API để trả về kết quả AI thông minh, tích hợp sẵn khả năng tìm kiếm web thời gian thực.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các tác vụ AI mượt mà, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tái sử dụng tối đa:** Chỉ cần thiết kế một lần, gọi từ bất kỳ workflow cha nào trong hệ thống n8n của các sếp.
- **AI cập nhật thời gian thực:** Tận dụng sức mạnh của các mô hình `sonar` và `sonar-pro` từ Perplexity để lấy thông tin mới nhất từ internet.
- **Tùy biến linh hoạt:** Dễ dàng truyền `SystemPrompt` (định hình tính cách, vai trò AI) và `UserPrompt` (câu hỏi/nhiệm vụ) một cách linh hoạt.
- **Tiết kiệm thời gian lập trình:** Không cần code phức tạp, quản lý API Key tập trung tại một nơi duy nhất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Perplexity API Key:** Tài khoản và API Key hợp lệ từ [Perplexity AI](https://www.perplexity.ai/).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ chính thức của n8n (Workflow ID: `4978`), sau đó chọn **Import from File** hoặc copy/paste trực tiếp JSON vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 3 nodes chính, các sếp cần chú ý cấu hình các điểm sau:

- **Node `When Executed by Another Workflow` (Execute Workflow Trigger):**
  - Node này đóng vai trò nhận dữ liệu được truyền vào từ workflow cha. Đảm bảo các tham số truyền sang khớp với tên biến mà workflow này yêu cầu.

- **Node `Parameters` (Set Node):**
  - Nơi cấu hình các tham số mặc định và chọn model AI.
  - Các sếp có thể thay đổi giá trị của trường `"model"` tại đây để chuyển đổi giữa các mô hình hỗ trợ:
    - `sonar`: Phù hợp cho các tác vụ nhanh, tiết kiệm.
    - `sonar-pro`: Mô hình mạnh mẽ hơn cho các truy vấn phức tạp.
  - Tham khảo thêm tại [Perplexity Model Cards](https://docs.perplexity.ai/models/model-cards).

- **Node `Perplexity API Request` (HTTP Request Node):**
  - **Method:** `POST`
  - **URL:** `https://api.perplexity.ai/chat/completions`
  - **Authentication / Headers:** Thêm Header Auth với loại `Header Auth` hoặc `Bearer Token`, sử dụng **Perplexity API Key** của các sếp.
  - **Body Payload:** Node này sẽ tự động ánh xạ dữ liệu từ node `Parameters` và trigger để xây dựng mảng `messages` bao gồm `SystemPrompt` và `UserPrompt`.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Node** hoặc **Test workflow** với dữ liệu giả lập để kiểm tra phản hồi từ Perplexity API.
- Sau khi test thành công, bật công tắc **Active** để đưa sub-workflow vào trạng thái sẵn sàng phục vụ các workflow cha.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack / Telegram:** Tạo một workflow cha nhận câu hỏi từ chatwork/telegram của công ty, gọi sub-perplexity này, rồi trả kết quả tự động về cho người dùng.
- **Lưu lịch sử vào Google Sheets / Database:** Sau khi nhận câu trả lời từ Perplexity, các sếp có thể log lại câu hỏi và câu trả lời để phân tích chất lượng hoặc làm tài liệu nội dung.
- **Tạo hệ thống RAG thu nhỏ:** Dùng `SystemPrompt` để ép AI chỉ trả lời dựa trên tài liệu nội bộ được truyền vào từ bước trước đó.

### 📌 Kết luận
Việc đóng gói các API gọi AI thành Sub-Workflow trong n8n là một tư duy thiết kế cực kỳ chuyên nghiệp, giúp hệ thống automation của doanh nghiệp gọn gàng, dễ bảo trì và dễ mở rộng scale về sau. Hãy áp dụng ngay vào hệ thống của các sếp nhé!