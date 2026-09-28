---
title: "🚀 Xây dựng AI Agent tùy chỉnh với LangChain & Gemini (Self-Hosted)"
description: "Tự động hoá chatbot AI cá nhân hoá bằng LangChain và Google Gemini, không cần viết code, chạy 24/7."
slug: "xay-dung-ai-agent-langchain-gemini"
tags: [n8n, automation, no-code, AI, LangChain, Gemini]
keywords: [n8n workflow, tự động hóa, AI agent, LangChain, Google Gemini]
---

# 🚀 Xây dựng AI Agent tùy chỉnh với LangChain & Gemini (Self-Hosted)

Doanh nghiệp ngày càng phụ thuộc vào các trợ lý ảo để hỗ trợ khách hàng, nhân viên nội bộ hoặc tự động hoá quy trình.  
Tuy nhiên, **việc triển khai một AI Agent chất lượng** thường đòi hỏi:

* Viết code phức tạp, phải duy trì server riêng.  
* Quản lý lịch sử hội thoại, prompt engineering và lựa chọn mô hình AI.  
* Đảm bảo tính ổn định 24/7 mà không tốn quá nhiều chi phí.

**Workflow này** giải quyết tất cả những vấn đề trên bằng cách kết hợp **LangChain** và **Google Gemini** trong môi trường **n8n** – không cần một dòng code nào, chỉ cần cấu hình và bật chạy.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Chatbot trả lời ngay lập tức mà không cần nhân viên can thiệp.  
- **Độ chính xác cao**: Sử dụng mô hình Gemini mạnh mẽ, kết hợp prompt tùy chỉnh.  
- **Cá nhân hoá hội thoại**: Lưu lịch sử và nhớ ngữ cảnh nhờ Memory Buffer Window.  
- **Hoạt động liên tục 24/7**: Chạy trên VPS, không phụ thuộc vào máy cá nhân.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Google Cloud** với **Google Gemini (Palm) API key**.  
- **n8n** đã được cài đặt (Self‑hosted hoặc Cloud).  
- **Credentials** trong n8n: `googlePalmApi` (được tạo từ API key).  
- Truy cập **Editor** của n8n để import workflow.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow (hoặc sao chép nội dung JSON).  
2. Vào **n8n → Workflows → Import** → Dán JSON → **Import**.  
3. Đặt tên cho workflow (mặc định: *Build Custom AI Agent with LangChain & Gemini*).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Loại | Hướng dẫn cấu hình |
|------|------|--------------------|
| **When chat message received** | `chatTrigger` | - Đặt **Title** cho giao diện chat (ví dụ: “AI Agent của công ty”). <br> - Kiểm tra **Webhook URL** được tạo tự động; dùng để truy cập chat UI. |
| **Google Gemini Chat Model** | `lmChatGoogleGemini` | - Chọn **Credentials** → `googlePalmApi`. <br> - Kiểm tra **Model** (mặc định: `gemini-pro`). |
| **Store conversation history** | `memoryBufferWindow` | - Thiết lập **Buffer Size** (số tin nhắn lưu trong lịch sử, ví dụ: `5`). <br> - Đảm bảo **Output** được kết nối tới node **Construct & Execute LLM Prompt**. |
| **Construct & Execute LLM Prompt** | `code` (LangChain) | - Mở tab **Code** và chỉnh **Template** theo hướng dẫn dưới **Prompt Engineering**: <br>```js\nconst prompt = `You are a helpful AI assistant. {chat_history}\nUser: {input}\nAssistant:`;\nreturn { prompt };\n``` <br> - **KHÔNG** xóa `{chat_history}` và `{input}` – chúng là placeholder quan trọng cho LangChain. <br> - Nếu muốn thay đổi tính cách AI, chỉnh nội dung trước `{chat_history}` (ví dụ: “Bạn là một chuyên gia tài chính”). |
| **(Optional) Sticky Note** | `stickyNote` | Dùng để ghi chú nội bộ, không ảnh hưởng tới luồng. |

#### 3. Kích hoạt ⚡️
1. **Test**: Nhấn nút **Chat** trên node *When chat message received* → nhập câu hỏi mẫu.  
2. Kiểm tra phản hồi từ Gemini và lịch sử hội thoại được lưu.  
3. Khi mọi thứ ổn, bật **Active** ở góc trên bên phải của workflow.  

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack / Telegram**: Thêm node **Slack** hoặc **Telegram** để nhận tin nhắn từ kênh chat nội bộ.  
- **Lưu log vào Google Sheets**: Dùng node **Google Sheets** để ghi lại mỗi lượt hội thoại (timestamp, user, prompt, response).  
- **Báo cáo định kỳ**: Kết hợp **Cron** + **Email** để gửi bản tóm tắt hội thoại hàng ngày/tuần.  
- **Retrieval Augmented Generation (RAG)**: Thêm node **Google Drive** hoặc **Notion** làm nguồn dữ liệu, rồi truyền vào prompt để AI trả lời dựa trên tài liệu nội bộ.  

### 📌 Kết luận
Với chỉ 4 node đơn giản, các sếp đã có ngay một **AI Agent tùy chỉnh**, có khả năng nhớ ngữ cảnh, trả lời chính xác và luôn sẵn sàng 24/7. Hãy **import, cấu hình credentials, test và bật chạy** ngay hôm nay để nâng cao trải nghiệm khách hàng và tối ưu hoá quy trình nội bộ! 🚀