---
title: "🚀 Tự động hóa Chatbot WhatsApp với Google Drive RAG, GPT-4.1-mini và Cohere Reranking"
description: "Hướng dẫn chi tiết cách tự động hóa chatbot WhatsApp sử dụng Google Drive RAG, GPT-4.1-mini và Cohere Reranking để cung cấp câu trả lời chính xác và nhanh chóng cho khách hàng."
slug: "tu-dong-hoa-chatbot-whatsapp-voi-google-drive-rag-gpt-4-1-mini-va-cohere-reranking"
tags: [n8n, automation, no-code, whatsapp, chatbot, ai, google-drive, supabase, cohere, openai]
keywords: [n8n workflow, tự động hóa, chatbot whatsapp, google drive rag, gpt-4.1-mini, cohere reranking, supabase]
---

# 🚀 Tự động hóa Chatbot WhatsApp với Google Drive RAG, GPT-4.1-mini và Cohere Reranking

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian và công sức cho đội ngũ hỗ trợ khách hàng.
- Cung cấp câu trả lời chính xác và nhanh chóng cho khách hàng.
- Tăng cường trải nghiệm khách hàng thông qua chatbot tự động hóa.
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n đang chạy với URL công khai.
- Tài khoản WhatsApp Business đã kết nối với ứng dụng.
- Các credentials đã được cấu hình trong n8n:
  - WhatsApp Trigger (App ID, Secret, Verify Token).
  - WhatsApp Send (Phone Number ID + Access Token) cho node `Send message`.
  - OpenAI (cho Chat + Transcription) được sử dụng bởi `OpenAI Chat Model` và `Translate a recording`.
  - Supabase (URL + Key) được sử dụng bởi `Kknowledge_base` (vector store).
  - Cohere (tùy chọn nhưng được kết nối) cho reranking.
- Bảng Supabase `documents` đã được điền với các FAQ, chính sách và dịch vụ của phòng khám.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **WhatsApp Trigger**: Đăng ký sự kiện `messages`; đặt Verify Token; sử dụng URL webhook **Production** trong Meta.
- **Switch node**: Các quy tắc kiểm tra chính xác `text` hoặc `audio` trên `messages[0].type`.
- **Đường dẫn Audio**:
  - `HTTP Request` GET dữ liệu media từ Graph API sử dụng `messages[0].audio.id` + `access_token` query.
  - `HTTP Request1` tải file sử dụng URL trả về và header `Authorization: Bearer <PAGE_ACCESS_TOKEN>`.
  - `Translate a recording` sử dụng credential **OpenAI** (Whisper/translate) để xuất ra văn bản.
- **Edit Fields1**: Xác nhận các biểu thức:
  ```
  Phone   = {{$('WhatsApp Trigger').item.json.messages[0].from}}
  text    = {{$json.text}}{{$json.messages[0].text.body}}
  ```
  Đoạn mã này nối kết cả transcription (`$json.text`) hoặc văn bản gõ tay.
- **Agent**:
  - `OpenAI Chat Model`: model `gpt-4.1-mini`, nhiệt độ `0.3`.
  - `AI Agent` system message bao gồm tone và các quy tắc bảo vệ cho **HolistiCare (DHA, Lahore)**.
  - **Kết nối** Memory (`Simple Memory` với `sessionKey = {{$json.Phone}}`) và Tool (`Kknowledge_base`) với Agent.
- **Supabase KB** (`Kknowledge_base`): mode `retrieve-as-tool`, table `documents`, `topK=10`, `useReranker=true`. Đảm bảo embeddings trong bảng của bạn phù hợp với model bạn đã index.
- **Reranker Cohere** (tùy chọn): được kết nối với KB cho kết quả tốt hơn; cần key hợp lệ.
- **Send message**: Đặt `phoneNumberId` và credential cho tài khoản WhatsApp Business; người nhận là `{{$('WhatsApp Trigger').item.json.messages[0].from}}`.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Tone**: điều chỉnh trong thông điệp hệ thống của Agent (giữ nguyên độ dài và các quy tắc bảo vệ).
- **Giới hạn từ**: thay đổi quy tắc bảo vệ trong thông điệp hệ thống và kiểm tra lại.
- **Cửa sổ bộ nhớ**: cấu hình độ dài buffer của `Simple Memory` cho nhiều hoặc ít ngữ cảnh hơn.
- **Đất nền mạnh hơn**: giảm `topK` hoặc thu hẹp nội dung KB; xem xét thêm các thẻ miền trong tài liệu Supabase của bạn.
- **Dịch ngôn ngữ**: dựa vào đường dẫn dịch của OpenAI cho audio; cho văn bản, thêm bước phát hiện ngôn ngữ trước nếu cần.

### 📌 Kết luận
Workflow này chuyển đổi các tin nhắn WhatsApp đến (văn bản hoặc audio) thành các câu trả lời ngắn gọn và thân thiện của phòng khám bằng cách sử dụng Agent AI với bộ nhớ và cơ sở kiến thức được hỗ trợ bởi Supabase. Nó tuân theo các quy tắc bảo vệ (≤100 từ, không báo giá trừ khi trong KB, không bán hàng cứng). Hãy áp dụng ngay để nâng cao trải nghiệm khách hàng và tiết kiệm thời gian cho đội ngũ hỗ trợ!