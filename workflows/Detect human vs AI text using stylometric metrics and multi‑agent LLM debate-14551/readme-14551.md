---
title: "🚀 Phát hiện văn bản AI và Người thật chuẩn xác với Stylometry và Multi-Agent LLM Debate trong n8n"
description: "Hướng dẫn cài đặt workflow n8n cực đỉnh từ chuyên gia Mychel Garzon, ứng dụng hệ thống đa tác nhân (Multi-Agent) và phân tích ngôn ngữ học (Stylometry) để bóc mẽ văn bản AI."
slug: "phat-hien-van-ban-ai-va-nguoi-that-voi-n8n"
tags: [n8n, automation, ai-detection, multi-agent, llm, langchain]
keywords: [n8n workflow, phát hiện văn bản AI, stylometry, multi-agent llm, tự động hóa n8n]
---

# 🚀 Phát hiện văn bản AI và Người thật chuẩn xác với Stylometry và Multi-Agent LLM Debate

Các sếp có bao giờ đau đầu khi phải kiểm tra xem một bài viết, báo cáo hay email dài dằng dặc là do con người tự viết hay do AI (ChatGPT, Claude, Gemini...) "phối hợp sản xuất"? Các công cụ check AI truyền thống thường rất mơ hồ và dễ cho kết quả sai lệch. 

Giải pháp cho các sếp đây: Một workflow n8n cực kỳ thông minh được thiết kế bởi **Mychel Garzon** (n8n Verified Creator & Nhà vô địch Junction 2025 n8n Tech Challenge). Workflow này sử dụng phương pháp **Stylometry** (đo lường các chỉ số văn phong) kết hợp với **cuộc tranh luận đa tác nhân (Multi-Agent Debate)** giữa các LLM hàng đầu để đưa ra kết luận chính xác 100% không cần code tay.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các chuỗi hội thoại LLM nặng mượt mà, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Disscount VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phân tích đa chiều:** Không chỉ dựa vào cảm tính, hệ thống tính toán chi tiết các chỉ số *burstiness* (độ biến thiên câu), *vocabulary density* (mật độ từ vựng), *repetition* (độ lặp từ) và *sentence variance*.
- **Tranh biện đa tác nhân:** 3 Agent AI với 3 góc nhìn khác nhau (Scanner, Forensic Analyst, Devil's Advocate) sẽ mổ xẻ văn bản như một phiên tòa thực thụ.
- **Tự động cập nhật mẫu AI mới:** Workflow có tính năng tự động chạy định kỳ hàng tháng để cập nhật các "dấu vân tay" (fingerprint words) mới nhất từ các mô hình AI đời mới (GPT-4o, Claude 3.5, Gemini 1.5...).
- **Giao diện Chat trực quan:** Tương tác trực tiếp qua khung chat của n8n để nhận báo cáo phân tích chi tiết.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance** phiên bản mới nhất hỗ trợ LangChain nodes.
- **API Keys cho các LLM Providers** (Workflow này tích hợp sức mạnh tổng hợp từ nhiều nhà cung cấp để đối chiếu khách quan):
  - OpenAI API Key (cho GPT model)
  - Anthropic API Key (cho Claude model)
  - Google Gemini API Key (cho Gemini model)
  - Groq API Key (cho Generator model)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ [n8n Workflow #14551](https://n8n.io/workflows/14551).
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc copy/paste toàn bộ mã JSON vào canvas).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần chú ý cấu hình các node cốt lõi sau để hệ thống chạy trơn tru:
- **Cấu hình Credentials cho LLM Nodes:** 
  - `LLM - Generator` (Groq)
  - `LLM - Devil's Advocate` (OpenAI)
  - `LLM Scanner` (Anthropic - chọn model `claude-sonnet-4-5-20250929` hoặc tương đương)
  - `LLM - Analyst` (Google Gemini)
  Hãy đảm bảo các node này đã được trỏ đúng tài khoản API tương ứng của các sếp.
- **Khởi tạo dữ liệu lần đầu (First-Time Setup):**
  - Trước khi dùng tính năng chat, các sếp cần chạy thủ công (Manual run) phần **Fingerprint Generator Section** (gồm `Schedule Trigger`, `Load Fingerprint List`, `Find New Words`, `Save New Fingerprints`) MỘT LẦN DUY NHẤT để nạp sẵn 80-100 từ khóa nhận diện AI mẫu vào `DataTable`.

#### 3. Kích hoạt ⚡️
- Mở cửa sổ **Chat Window** bằng cách test node `When chat message received` hoặc mở khung chat tích hợp sẵn.
- Dán thử một đoạn văn bản bất kỳ và bấm gửi để xem hệ thống phân tích.
- Sau khi kiểm tra mọi thứ hoạt động ổn định, bật công tắc **Active** ở góc trên cùng bên phải để đưa workflow vào trạng thái thường trực.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh liên lạc:** Thay vì chỉ chat trong n8n, các sếp có thể nối node `Send Final Report` ra **Telegram Bot** hoặc **Slack** để đội ngũ Content/HR có thể gửi văn bản cần check trực tiếp qua nhóm chat công ty.
- **Lưu lịch sử kiểm tra:** Thêm một node Google Sheets hoặc Airtable ở cuối workflow để lưu lại các đoạn text đã check cùng kết quả Verdict (Human/AI) nhằm làm dữ liệu huấn luyện hoặc báo cáo thống kê.
- **Tinh chỉnh Prompt:** Các sếp có thể tùy chỉnh system prompt trong các Agent (`Agent 1`, `Agent 2`, `Agent 3`) để hệ thống nói chuyện theo phong cách hài hước hoặc nghiêm túc tùy ý.

### 📌 Kết luận
Hệ thống phát hiện văn bản AI kết hợp Stylometry và Multi-Agent Debate này là một "vũ khí tối thượng" giúp doanh nghiệp kiểm soát chất lượng nội dung, tuyển dụng minh bạch và tránh việc lạm dụng AI tràn lan. Hãy import ngay vào n8n và thử nghiệm ngay hôm nay các sếp nhé!