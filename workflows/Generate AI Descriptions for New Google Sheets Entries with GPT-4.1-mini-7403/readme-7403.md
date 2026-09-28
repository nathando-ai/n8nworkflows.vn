---
title: "🚀 Tự động tạo mô tả sản phẩm/nội dung bằng GPT-4o-mini và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động phát hiện dòng mới trên Google Sheets, sử dụng AI LangChain để viết mô tả chi tiết và cập nhật ngược lại file."
slug: "tu-dong-tao-mo-ta-ai-google-sheets-gpt-mini"
tags: [n8n, automation, openai, google-sheets, langchain, ai-content]
keywords: [n8n workflow, tự động hóa google sheets, ai viết mô tả, gpt-4o-mini n8n, langchain agent]
---

# 🚀 Tự động tạo mô tả sản phẩm & nội dung bằng AI trên Google Sheets

Các sếp có đang mệt mỏi khi phải ngồi hàng giờ nghĩ ý tưởng, viết mô tả cho hàng trăm sản phẩm, bài viết hay dự án mới đưa lên Google Sheets không? Việc làm thủ công này vừa tốn thời gian, dễ gây nhàm chán lại thiếu sự đồng nhất về văn phong.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n tự động hóa 100%. Ngay khi các sếp nhập một từ khóa (`topic`) mới vào Google Sheets, trợ lý AI thông minh sẽ tự động tiếp nhận, phân tích, viết một đoạn mô tả (description) chất lượng cao và tự động điền lại vào đúng dòng đó mà không cần động tay thêm một bước nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh copy-paste từ ChatGPT vào bảng tính thủ công.
- **Tự động hóa hoàn toàn:** Chạy ngầm liên tục, cứ có dòng mới là AI "nhảy" vào xử lý ngay lập tức.
- **Cấu trúc chuẩn chỉnh:** Sử dụng Structured Output Parser giúp kết quả trả về từ AI luôn đúng định dạng, dễ dàng đồng bộ hóa.
- **Nâng cao chất lượng nội dung:** Tận dụng sức mạnh của mô hình ngôn ngữ lớn (LLM) để tạo ra các đoạn mô tả cuốn hút, chuyên nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Google** (để kết nối Google Sheets).
- **OpenAI API Key** (có số dư để sử dụng model GPT).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải hoặc copy đoạn mã JSON của workflow này.
- Tại giao diện n8n của các sếp, chọn **Workflows** → **Import from JSON**.
- Dán nội dung JSON vào và bấm Import.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 6 nodes chính được thiết kế tối ưu hóa bằng LangChain. Các sếp cần chú ý cấu hình các điểm mấu chốt sau:

- **Row added - Google Sheet (Trigger Node):**
  - Cấu hình `Google Sheets Trigger OAuth2 credentials` bằng tài khoản Google của các sếp.
  - Chọn file Google Sheets quản lý dữ liệu và trỏ tới sheet có tên `data`.
  - Thiết lập chế độ quét dữ liệu (Poling) định kỳ (ví dụ: mỗi phút một lần).

- **OpenAI Chat Model (Node LM Chat OpenAI):**
  - Tạo hoặc chọn credentials cho **OpenAI API Key**.
  - Kiểm tra tham số model đảm bảo đang trỏ đến `gpt-4.1-mini` (hoặc model tương đương mới nhất).

- **Description Writer (Agent Node) & Structured Output Parser:**
  - Hai node này phối hợp với nhau để định hình câu lệnh (prompt) và cấu trúc dữ liệu đầu ra từ AI, đảm bảo kết quả trả về khớp hoàn hảo với cột `description` trong bảng tính.

- **Update row in sheet & Append row in sheet:**
  - Kết nối OAuth2 của Google Sheets để cho phép n8n ghi đè/cập nhật dữ liệu (Update) vào dòng tương ứng sau khi AI đã tạo xong nội dung.

#### 3. Kích hoạt ⚡️
- Thử nghiệm bằng cách nhập một dòng dữ liệu mẫu vào cột `topic` trên Google Sheets.
- Bấm **Execute Workflow** trên n8n để test thủ công lần đầu.
- Nếu mọi thứ chạy mượt mà, hãy gạt công tắc sang **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm một node Telegram hoặc Slack vào cuối workflow để nhận thông báo ngay khi AI viết xong một mô tả mới.
- **Mở rộng cột dữ liệu:** Các sếp có thể mở rộng bảng tính thêm các cột như `tone_of_voice` (vọng văn: chuyên nghiệp, hài hước, thân thiện) truyền vào AI Agent để cá nhân hóa nội dung tốt hơn.
- **Quản lý lịch sử:** Sử dụng thêm node ghi log vào một tab "actions" riêng biệt để theo dõi số lượng token AI đã tiêu thụ.

### 📌 Kết luận
Việc tự động hóa quy trình tạo nội dung với AI và Google Sheets không chỉ giúp tiết kiệm nguồn lực mà còn tối ưu hóa hiệu suất làm việc của cả đội ngũ. Hãy cài đặt ngay workflow này để tối ưu hóa công việc hàng ngày của các sếp nhé!