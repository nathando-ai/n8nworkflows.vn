---
title: "🚀 Xây dựng chatbot RAG chi phí thấp với GPT‑4.1 và Lookio"
description: "Giải pháp tự động trả lời câu hỏi dựa trên tài liệu, tối ưu chi phí bằng mô hình nhỏ và Lookio RAG."
slug: "xay-dung-chatbot-rag-gpt-4-1-lookio"
tags: [n8n, automation, no-code, chatbot, ai, rag]
keywords: [n8n workflow, tự động hóa, chatbot, RAG, GPT-4.1, Lookio]
---

# 🚀 Xây dựng chatbot RAG chi phí thấp với GPT‑4.1 và Lookio

Bạn đang phải trả tiền lớn cho các mô hình AI “đại” để trả lời câu hỏi từ tài liệu?  
Workflow này giúp bạn **định tuyến** các câu hỏi đơn giản sang mô hình nhỏ (gpt‑4.1‑nano / gpt‑4.1‑mini) và chỉ dùng mô hình “đại” (gpt‑4.1) khi cần truy xuất kiến thức thực sự qua Lookio.  
Kết quả: **giảm chi phí, tăng tốc độ** và vẫn giữ độ chính xác cao cho các câu hỏi phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm chi phí**: chỉ dùng mô hình lớn khi thực sự cần.  
- **Tốc độ phản hồi nhanh**: mô hình nhỏ xử lý ngay lập tức.  
- **Dữ liệu luôn cập nhật**: Lookio tự động lấy thông tin từ tài liệu mới nhất.  
- **Dễ dàng mở rộng**: thêm Slack/Telegram, lưu log, gửi báo cáo định kỳ.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
| Dịch vụ | Mô tả | API Key / Credentials |
|---------|-------|------------------------|
| **OpenAI** | Mô hình GPT‑4.1 (nano, mini, full) | `openAiApi` (đã cấu hình trong n8n) |
| **Lookio** | Truy xuất dữ liệu RAG | `API Key` và `Workspace ID` (đặt trong node `RAG via Lookio`) |
| **Chat Platform** | Ví dụ: Discord, Telegram, Slack | `chatTrigger` và `chat` node cần credentials tương ứng |
| **N8N** | Self‑hosted hoặc Cloud | Đảm bảo phiên bản >= 0.200 |
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON từ link gốc: <https://n8n.io/workflows/12521>  
2. Trong n8n Editor, chọn **Import** → **Upload JSON** → chọn file vừa tải.  
3. Hoặc copy toàn bộ JSON và dán vào ô **Paste JSON**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên Node | Cấu hình cần chỉnh | Ghi chú |
|------|----------|---------------------|---------|
| **chatTrigger** | `When chat message received` | Credentials (điền token của nền tảng chat) | Bắt đầu workflow khi có tin nhắn |
| **lmChatOpenAi** | `Very small model` | `model = gpt-4.1-nano` | Đảm bảo credential `openAiApi` đã được cấu hình |
| **lmChatOpenAi** | `Mini model` | `model = gpt-4.1-mini` | |
| **lmChatOpenAi** | `Large model` | `model = gpt-4.1` | |
| **textClassifier** | `Intent router` | Định nghĩa các intent (e.g., “simple”, “knowledge”) | Sử dụng để chuyển hướng |
| **httpRequest** | `RAG via Lookio` | `URL = https://api.lookio.app/v1/assistants/{assistantId}/query`<br>`Headers: Authorization: Bearer {API_KEY}`<br>`Body: { "query": "{{ $json.query }}" }` | Thay `{assistantId}` và `{API_KEY}` bằng giá trị thực |
| **memoryManager** | `Find past messages` & `Store messages` | Không cần chỉnh thêm | Lưu trữ lịch sử hội thoại |
| **memoryBufferWindow** | `Simple Memory` | Không cần chỉnh thêm | Giữ ngắn hạn các tin nhắn |
| **chainLlm** | `Prepare retrieval query`, `Write the final response`, `Simple response` | Đặt `LLM` tương ứng (mini hoặc large) | |
| **chat** | `Respond to Chat` | Credentials (điền token của nền tảng chat) | Gửi phản hồi cho người dùng |

> **Tip**: Kiểm tra **Credentials** trong n8n → **Credentials** → **OpenAI** và **Lookio** trước khi chạy.

### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn nút **Execute Workflow** với dữ liệu mẫu (ví dụ: “What is the company policy on remote work?”).  
2. Kiểm tra log: xem node nào được thực thi, dữ liệu trả về từ Lookio.  
3. Khi mọi thứ ổn, bật **Active** (đánh dấu workflow là “Active”) để nó chạy tự động khi có tin nhắn.

## ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack**: Thêm node `Slack` để gửi báo cáo hàng ngày về số lượng câu hỏi và chi phí sử dụng mô hình.  
- **Telegram Bot**: Thay `chatTrigger` và `chat` bằng node `Telegram` để mở rộng kênh.  
- **Lưu log**: Dùng node `Write Binary File` hoặc `Google Sheets` để ghi lại lịch sử hội thoại.  
- **Scheduled Reports**: Thêm node `Cron` + `HTTP Request` để gửi email báo cáo chi phí hàng tuần.  
- **Fine‑tune Prompt**: Tùy chỉnh prompt trong các node `chainLlm` để phù hợp với ngữ cảnh doanh nghiệp.

## 📌 Kết luận
Workflow “Build a cost‑efficient Lookio RAG chatbot with GPT‑4.1 models for knowledge Q&A” của Guillaume Duvernay đã được tối ưu để **giảm chi phí** và **tăng tốc độ** trả lời.  
Hãy thử ngay, cài đặt trên VPS riêng, và trải nghiệm chatbot thông minh, không cần code, chỉ với vài bước cấu hình.  

> **Cùng nhau nâng tầm tự động hóa** – áp dụng ngay hôm nay!