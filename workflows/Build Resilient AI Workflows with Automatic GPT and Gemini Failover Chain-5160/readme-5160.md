---
title: "🚀 Xây dựng Workflow AI chịu lỗi với Chuỗi dự phòng GPT & Gemini"
description: "Tự động chuyển đổi giữa GPT‑4o và Google Gemini khi một mô hình gặp lỗi, giúp AI luôn phản hồi nhanh, chính xác và không gián đoạn."
slug: "xay-dung-workflow-ai-resilient-failover"
tags: [n8n, automation, no-code, AI, GPT, Gemini]
keywords: [n8n workflow, tự động hóa, AI, GPT, Gemini, failover, chain]
---

# 🚀 Xây dựng Workflow AI chịu lỗi với Chuỗi dự phòng GPT & Gemini

Khi các dự án AI phụ thuộc vào một mô hình duy nhất (ví dụ: GPT‑4o), **rủi ro gián đoạn** luôn hiện hữu: nếu API của OpenAI gặp sự cố, thời gian phản hồi tăng, thậm chí không có phản hồi nào.  
Đối với các doanh nghiệp, việc phải dừng lại để chờ khắc phục hoặc chuyển đổi thủ công gây mất thời gian, giảm uy tín và làm giảm năng suất.

**Workflow này** giải quyết vấn đề bằng cách **tự động chuyển đổi** giữa OpenAI GPT‑4o và Google Gemini (hoặc bất kỳ mô hình nào bạn muốn) dựa trên số lần thất bại liên tiếp. Nhờ chuỗi dự phòng (fallback chain), AI luôn có **một mô hình thay thế sẵn sàng**, giúp quy trình chạy 100 % không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Không gián đoạn**: Khi mô hình A (GPT‑4o) lỗi, workflow tự động chuyển sang mô hình B (Gemini) ngay lập tức.  
- **Tiết kiệm thời gian**: Loại bỏ việc phải kiểm tra, khởi động lại hay thay đổi cấu hình thủ công.  
- **Chi phí tối ưu**: Chỉ sử dụng mô hình dự phòng khi thực sự cần, tránh lãng phí token.  
- **Độ tin cậy cao**: Đếm số lần thất bại, tự động tăng độ bền cho các tác vụ quan trọng (gửi email, tạo nội dung, trả lời khách hàng...).  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản OpenAI** với API Key (để sử dụng GPT‑4o).  
- **Tài khoản Google Cloud** bật Gemini API và có API Key.  
- **n8n** (phiên bản mới nhất) được cài đặt trên môi trường ổn định (VPS hoặc Docker).  
- **Kết nối internet** ổn định để gọi API bên ngoài.  
- (Tùy chọn) **Webhook URL** nếu muốn kích hoạt workflow từ bên ngoài.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. **Tải file JSON** của workflow (từ link gốc https://n8n.io/workflows/5160).  
2. Vào n8n → **Workflows** → **Import** → Chọn file JSON → **Import**.  
   *Hoặc* sao chép toàn bộ nội dung JSON, vào **Editor** → **Import from Clipboard** → Dán và **Import**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là hướng dẫn chi tiết từng node cần cấu hình:

| Node | Loại | Cấu hình cần làm |
|------|------|------------------|
| **Manual Trigger** | manualTrigger | Không cần cấu hình. Dùng để khởi chạy workflow thủ công hoặc kết nối webhook. |
| **Agent Variables** | set | - Thêm **Variable**: `fail_count` → **Number** → Giá trị khởi tạo **0**.<br>- (Tùy chọn) Thêm các biến khác như `userPrompt` nếu muốn truyền prompt từ bên ngoài. |
| **Fallback Models** | code | Đoạn JavaScript mẫu (đã có trên canvas) sẽ đọc `fail_count` và trả về tên mô hình cần dùng. <br>**Kiểm tra**: Đảm bảo `items[0].json.fail_count` được truyền đúng từ node **Agent Variables**. |
| **First Model** | lmChatOpenAi | - **Model**: `gpt-4o` (đã được preset).<br>- **Credentials**: Chọn **OpenAI API** → Điền **API Key**.<br>- **Temperature**, **Max Tokens** tùy nhu cầu. |
| **Falback Model** | lmChatGoogleGemini | - **Model**: để trống (sẽ dùng model mặc định của Gemini).<br>- **Credentials**: Chọn **Google Gemini API** → Điền **API Key**.<br>- Các tham số tùy chỉnh (temperature, top‑p…) nếu cần. |
| **AI Agent** | agent | - **Prompt**: Nhập **Prompt** mà bạn muốn AI thực hiện (có thể lấy từ **Agent Variables** hoặc nhập trực tiếp).<br>- **Input** `ai_languageModel`: Kết nối **output** của node **Fallback Models**.<br>- **Output**: Kết nối tới node tiếp theo (ví dụ: Slack, Email) hoặc để **Return** để xem kết quả trong UI. |
| **Sticky Note** (nếu có) | stickyNote | Chỉ dùng để ghi chú, không ảnh hưởng tới luồng. |

> **Lưu ý quan trọng**:  
> - **Thứ tự kết nối** các mô hình (First Model → Falback Model) quyết định thứ tự thử. Đảm bảo **First Model** được nối vào **Fallback Models** trước, sau đó mới nối **Falback Model**.  
> - **fail_count** sẽ tự động tăng mỗi khi node **AI Agent** trả về lỗi (status != 200). Nếu muốn giới hạn số lần thử, thêm một node **If** kiểm tra `fail_count < 3` trước khi quay lại **Fallback Models**.

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn nút **Execute Workflow** → Kiểm tra log của các node, đặc biệt là **Fallback Models** và **AI Agent**.  
2. Nếu mọi thứ hoạt động (prompt trả về kết quả), **bật** workflow bằng cách chuyển **Active** sang **ON**.  
3. Đối với môi trường production, **đặt** trigger (Webhook, Cron) để workflow tự động chạy theo lịch hoặc khi nhận yêu cầu.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo lỗi qua Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** sau **AI Agent** để gửi tin nhắn khi `fail_count` > 0.  
- **Lưu log vào Supabase hoặc Google Sheets**: Dùng node **Postgres** hoặc **Google Sheets** để ghi lại mỗi lần gọi, mô hình được dùng, thời gian phản hồi.  
- **Thêm mô hình thứ ba** (Anthropic Claude, Cohere…) bằng cách kéo thêm node **lmChat...** và nối vào **Fallback Models** theo thứ tự mong muốn.  
- **Dynamic Prompt**: Sử dụng node **Set** để lấy prompt từ webhook payload, giúp workflow phục vụ nhiều trường hợp (tạo nội dung blog, trả lời support, v.v.).  
- **Giới hạn token**: Trong node **First Model** và **Falback Model**, thiết lập **Max Tokens** để tránh chi phí vượt mức.

### 📌 Kết luận
Với workflow **“Build Resilient AI Workflows with Automatic GPT and Gemini Failover Chain”**, các sếp có thể yên tâm triển khai các tác vụ AI quan trọng mà không lo bị gián đoạn khi một mô hình gặp lỗi. Chỉ cần cấu hình API key, thiết lập chuỗi dự phòng, và bật workflow – mọi thứ sẽ tự động chạy 24/7, giúp tiết kiệm thời gian, giảm chi phí và nâng cao độ tin cậy cho toàn bộ quy trình kinh doanh.  

**Áp dụng ngay** để biến AI thành một công cụ “không bao giờ ngủ” cho doanh nghiệp của bạn! 🚀