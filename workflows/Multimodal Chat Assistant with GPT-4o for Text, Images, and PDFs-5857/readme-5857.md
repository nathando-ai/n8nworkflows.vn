---
title: "🚀 Trợ lý Chat Đa Mô Hình GPT-4o: Tự động hoá phản hồi văn bản, hình ảnh và PDF"
description: "Workflow n8n giúp xây dựng chatbot thông minh, phân tích hình ảnh và PDF, trả lời câu hỏi 100% tự động, không cần code."
slug: "trợ-lý-chat-gpt4o-multimodal"
tags: [n8n, automation, no-code, ai, chatbot, multimodal]
keywords: [n8n workflow, tự động hóa, chatgpt, GPT-4o, chatbot AI]
---

# 🚀 Trợ lý Chat Đa Mô Hình GPT-4o: Tự động hoá phản hồi văn bản, hình ảnh và PDF

Bạn đang phải trả lời hàng trăm câu hỏi khách hàng mỗi ngày? Bạn muốn một chatbot có thể đọc và hiểu hình ảnh, PDF, đồng thời trả lời bằng văn bản một cách tự nhiên?  
Workflow này sẽ giúp bạn **tự động hoá hoàn toàn** quy trình này, không cần viết code, chỉ cần cấu hình một vài node trong n8n.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: 90% câu hỏi được trả lời tự động, giảm tải công việc cho nhân viên.  
- **Chính xác & nhất quán**: GPT-4o luôn trả lời dựa trên dữ liệu đã lưu trong bộ nhớ.  
- **Cá nhân hóa**: Mỗi cuộc trò chuyện được lưu trữ, giúp chatbot nhớ lịch sử và thích ứng.  
- **Hoạt động liên tục**: Không giới hạn thời gian, luôn sẵn sàng 24/7.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản OpenAI** với API Key.  
- **API Key** của OpenAI được cấu hình trong n8n dưới tên credential `openAiApi`.  
- Không cần dịch vụ bên ngoài nào khác; workflow chỉ dùng các node có sẵn trong n8n.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON từ link gốc:  
   <https://n8n.io/workflows/5857>  
2. Mở n8n, vào **Workflows → Import** → **Upload JSON**.  
3. Hoặc copy toàn bộ nội dung JSON và dán vào **Editor → Import JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên trong workflow | Cấu hình cần chỉnh | Ghi chú |
|------|--------------------|---------------------|---------|
| **OpenAI** | `OpenAI` | *Credentials*: `openAiApi` <br>*Operation*: `analyze` <br>*Resource*: `image` | Dùng để phân tích hình ảnh được gửi vào chat. |
| **OpenAI Chat Model** | `OpenAI Chat Model` | *Credentials*: `openAiApi` <br>*Model*: `gpt-4o` | Đặt model chính cho trả lời văn bản. |
| **OpenAI Chat Model1** | `OpenAI Chat Model1` | *Credentials*: `openAiApi` <br>*Model*: `gpt-4o` | Dùng cho phần xử lý sau khi tải file. |
| **Basic LLM Chain** | `Basic LLM Chain` | *Không cần chỉnh* | Xử lý logic chuỗi LLM. |
| **AI Agent** | `AI Agent` | *Không cần chỉnh* | Định nghĩa hành vi của agent. |
| **If** | `If` | *Điều kiện*: `{{ $json["fileType"] === "image" || $json["fileType"] === "pdf" }}` | Kiểm tra loại file. |
| **chatTrigger** | `chat` | *Webhook URL*: lấy từ n8n → **Webhooks** | Định nghĩa điểm bắt đầu khi có tin nhắn. |
| **memoryBufferWindow** | `Simple Memory`, `Simple Memory1`, `Simple Memory2` | *Window size*: 10 (hoặc tùy chỉnh) | Lưu trữ lịch sử hội thoại. |
| **memoryManager** | `chatmem`, `chatmem1` | *Không cần chỉnh* | Quản lý bộ nhớ giữa các node. |

> **Tip**: Đảm bảo tất cả các node `lmChatOpenAi` đều dùng cùng một credential `openAiApi` và model `gpt-4o`. Nếu thay đổi model, hãy cập nhật ở tất cả các node.

#### 3. Kích hoạt ⚡️
1. **Test run**: Gửi một tin nhắn thử (với hoặc không có file) tới webhook URL. Kiểm tra log để xác nhận mọi node chạy đúng.  
2. **Bật Active**: Trong giao diện n8n, chuyển trạng thái workflow từ **Inactive** sang **Active**.  
3. **Theo dõi**: Kiểm tra tab **Execution** để xem lịch sử chạy. Nếu có lỗi, sửa node tương ứng.

### ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram integration**: Thêm node Slack hoặc Telegram để gửi phản hồi ngay trong kênh.  
- **Lưu log**: Dùng node `Write Binary File` hoặc `Google Sheets` để ghi lại lịch sử hội thoại.  
- **Báo cáo định kỳ**: Thêm node `Cron` + `Email` để gửi báo cáo hàng ngày về số lượng câu hỏi, thời gian phản hồi.  
- **Tùy chỉnh prompt**: Sửa prompt trong node `Basic LLM Chain` để phù hợp với lĩnh vực (ví dụ: hỗ trợ kỹ thuật, bán hàng, giáo dục).  

### 📌 Kết luận
Workflow “Trợ lý Chat Đa Mô Hình GPT-4o” là giải pháp hoàn hảo cho doanh nghiệp muốn **tự động hoá** quy trình hỗ trợ khách hàng, phân tích tài liệu và trả lời câu hỏi một cách nhanh chóng, chính xác.  
Hãy **đăng ký VPS**, **cấu hình OpenAI** và **đưa workflow lên n8n** ngay hôm nay để trải nghiệm chatbot thông minh 100% không cần code!