---
title: "🚀 Tự động trò chuyện với LLM nội bộ bằng n8n & Ollama"
description: "Kết nối n8n với Ollama để tạo giao diện chat AI nội bộ, gửi prompt và nhận phản hồi ngay trong workflow – không cần viết code."
slug: "tu-dong-tro-chuyen-llm-ollama-n8n"
tags: [n8n, automation, no-code, AI, LLM, Ollama]
keywords: [n8n workflow, tự động hóa, LLM, Ollama, chat AI]
---

# 🚀 Tự động trò chuyện với LLM nội bộ bằng n8n & Ollama

Doanh nghiệp ngày càng muốn khai thác sức mạnh của các Large Language Model (LLM) **được triển khai nội bộ** để bảo mật dữ liệu và giảm chi phí cloud. Tuy nhiên, việc **tương tác thủ công** qua terminal hoặc API test tool khiến quy trình chậm, dễ sai và không thân thiện với người dùng cuối.

Workflow này giải quyết vấn đề bằng cách **kết nối n8n với Ollama** – công cụ quản lý LLM nội bộ – để tạo một giao diện chat trực quan. Khi người dùng gửi tin nhắn, n8n sẽ truyền prompt tới Ollama, nhận phản hồi AI và trả lại ngay trong cùng một luồng, **không cần viết một dòng code nào**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).

👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn phải mở terminal, copy‑paste prompt.
- **Độ chính xác cao**: Dữ liệu luôn được truyền qua API nội bộ, không bị gián đoạn.
- **Cá nhân hoá**: Dễ dàng tích hợp với các hệ thống nội bộ (CRM, ERP, ticketing).
- **Hoạt động liên tục 24/7**: Workflow tự động nhận và trả lời mọi tin nhắn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Ollama** đã được cài đặt và chạy (mặc định `http://localhost:11434`).  
- **Credential “ollamaApi”** trong n8n, chứa URL Ollama và (nếu cần) token truy cập.  
- **n8n** đang chạy (đề nghị triển khai trên VPS hoặc Docker).  
- **Kết nối mạng**: Nếu n8n chạy trong Docker, phải khởi động với `--net=host` để truy cập Ollama.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow (hoặc sao chép nội dung JSON).  
2. Vào **n8n → Workflows → Import** → Dán JSON → **Import**.  
3. Đặt tên cho workflow (mặc định: *Chat with local LLMs using n8n and Ollama*).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Hướng dẫn cấu hình |
|------|-------------------|
| **When chat message received** (`chatTrigger`) | - Chọn **Chat Trigger** phù hợp (WebSocket, Slack, Telegram, v.v.) tùy môi trường. <br> - Đặt **Trigger Name** và **Channel/Room** nếu cần. |
| **Ollama Chat Model** (`lmChatOllama`) | - **Credentials**: chọn `ollamaApi`. <br> - **Ollama URL**: mặc định `http://localhost:11434`; thay đổi nếu Ollama chạy ở địa chỉ khác. <br> - **Model**: nhập tên model đã tải trên Ollama (ví dụ: `llama2`, `mistral`). |
| **Chat LLM Chain** (`chainLlm`) | - Để **Input** là `{{$json["message"]}}` (hoặc trường chứa tin nhắn từ node trigger). <br> - **Output** sẽ được trả về cho node tiếp theo (hoặc trực tiếp cho chat interface). <br> - Kiểm tra **Prompt Template** nếu muốn tùy chỉnh ngữ cảnh. |

> **Lưu ý:** Sau khi cấu hình, nhấn **Execute Node** từng bước để kiểm tra kết nối tới Ollama và nhận phản hồi mẫu.

#### 3. Kích hoạt ⚡️
1. Nhấn **Save** → **Activate** workflow.  
2. Gửi một tin nhắn thử nghiệm từ giao diện chat đã cấu hình.  
3. Kiểm tra log trong n8n để xác nhận rằng prompt đã tới Ollama và phản hồi được trả về.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` làm trigger thay cho `chatTrigger` để nhân viên có thể chat trực tiếp từ kênh họ đã quen.  
- **Lưu log**: Dùng node `Write Binary File` hoặc `MongoDB` để ghi lại toàn bộ hội thoại, hỗ trợ audit và training model nội bộ.  
- **Báo cáo định kỳ**: Kết hợp `Cron` + `Google Sheets` để tổng hợp số lượng tin nhắn, thời gian phản hồi và gửi báo cáo qua email hàng tuần.  
- **Chain multiple LLMs**: Thêm node `chainLlm` thứ hai để so sánh kết quả của hai model khác nhau và chọn đáp án tốt nhất bằng một hàm custom.

### 📌 Kết luận
Với chỉ **3 node** và một vài cấu hình đơn giản, các sếp đã có thể biến n8n thành một **trung tâm chat AI nội bộ** mạnh mẽ, bảo mật và hoàn toàn không cần viết code. Hãy triển khai ngay hôm nay, tích hợp vào quy trình hỗ trợ khách hàng hoặc nội bộ để nâng cao năng suất và trải nghiệm người dùng! 🚀