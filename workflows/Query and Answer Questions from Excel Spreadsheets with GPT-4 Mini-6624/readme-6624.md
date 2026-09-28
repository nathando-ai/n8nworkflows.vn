---
title: "🚀 Trả lời Câu hỏi từ Excel với GPT‑4 Mini – Tự động hóa 100%"
description: "Giải pháp tự động trả lời câu hỏi dựa trên dữ liệu Excel bằng GPT‑4 Mini, giúp doanh nghiệp tiết kiệm thời gian và nâng cao độ chính xác."
slug: "tra-ly-cau-hoi-tu-excel-gpt-4-mini"
tags: [n8n, automation, no-code, ai, excel]
keywords: [n8n workflow, tự động hóa, GPT‑4 Mini, Excel, chatbot]
---

# 🚀 Trả lời Câu hỏi từ Excel với GPT‑4 Mini – Tự động hóa 100%

Bạn đang phải trả lời hàng trăm câu hỏi liên quan tới dữ liệu trong bảng tính Excel? Việc tra cứu thủ công không chỉ mất thời gian mà còn dễ sai sót. Workflow này kết hợp **LangChain**, **GPT‑4 Mini** và **Microsoft Excel** để tự động trả lời mọi câu hỏi ngay lập tức, không cần viết code.

:::info[Hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài phút thành ngay lập tức.  
- **Độ chính xác cao**: GPT‑4 Mini hiểu ngữ cảnh và trả lời dựa trên dữ liệu thực tế.  
- **Không cần code**: Chỉ cần cấu hình một vài node.  
- **Hoạt động liên tục**: Khi có câu hỏi mới, workflow tự động xử lý.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **OpenAI API Key** – để gọi GPT‑4 Mini.  
- **Microsoft Excel credentials** (OneDrive/SharePoint) – để truy cập bảng tính.  
- **n8n instance** – có thể Self‑hosted hoặc n8n Cloud.  
:::

### 🚀 Cách import & Lưu ý khi “lên đồ”

#### 1. Import Workflow 📥
- Tải file JSON từ link gốc: <https://n8n.io/workflows/6624>  
- Trong n8n Editor, chọn **Import** → **Upload JSON** hoặc copy‑paste nội dung JSON vào ô “Import JSON”.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cấu hình cần chỉnh |
|------|-------|---------------------|
| **Start Chat Conversation** (`chatTrigger`) | Nhận câu hỏi từ người dùng (ví dụ qua webhook, Slack, hoặc UI). | - Chọn “Webhook URL” (nếu dùng webhook).<br>- Định nghĩa “Message” field (điền tên trường chứa câu hỏi). |
| **Smart AI Agent** (`agent`) | Xử lý logic, gọi GPT‑4 Mini và truy vấn Excel. | - **Memory**: Chọn “Remember Chat History” node.<br>- **Tools**: Thêm “Get Excel Data” node.<br>- **Prompt**: Tùy chỉnh prompt mẫu: “Bạn là trợ lý chuyên nghiệp. Dựa vào dữ liệu trong bảng Excel, trả lời câu hỏi: {{question}}”. |
| **Remember Chat History** (`memoryBufferWindow`) | Lưu lại lịch sử hội thoại để GPT hiểu ngữ cảnh. | - **Window Size**: 10 (hoặc tùy ý). |
| **Get Excel Data** (`microsoftExcelTool`) | Truy vấn dữ liệu từ bảng tính. | - **File ID**: ID của file Excel.<br>- **Sheet Name**: Tên sheet chứa dữ liệu.<br>- **Query**: Ví dụ `SELECT * FROM Sheet1 WHERE Column1 = '{{question}}'`. |
| **OpenAI Chat Model** (`lmChatOpenAi`) | Gọi GPT‑4 Mini. | - **API Key**: Đưa vào credentials.<br>- **Model**: `gpt-4-mini`.<br>- **Temperature**: 0.7 (hoặc tùy ý). |

> **Lưu ý**: Đảm bảo các credentials đã được tạo trong **Credentials** tab của n8n trước khi chạy workflow.

#### 3. Kích hoạt ⚡️
- **Test run**: Nhấn “Execute Workflow” với dữ liệu mẫu (ví dụ: “Số lượng bán hàng tháng 3?”). Kiểm tra output trong node “OpenAI Chat Model”.  
- **Bật Active**: Khi mọi thứ ổn, chuyển workflow sang trạng thái **Active** để tự động phản hồi khi có câu hỏi mới.

### ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram integration**: Thêm node “Slack” hoặc “Telegram” để nhận câu hỏi và gửi trả lời ngay.  
- **Lưu log**: Dùng node “Write Binary File” để ghi lại lịch sử hội thoại vào Google Drive hoặc OneDrive.  
- **Báo cáo định kỳ**: Thêm node “Cron” để chạy “Get Excel Data” hàng ngày và gửi báo cáo qua email.  
- **Tùy chỉnh prompt**: Thêm các “system messages” trong LangChain để GPT hiểu vai trò và ngữ cảnh cụ thể (ví dụ: “Bạn là chuyên gia bán hàng”).  

### 📌 Kết luận
Workflow “Query and Answer Questions from Excel Spreadsheets with GPT‑4 Mini” giúp các sếp chuyển từ việc tra cứu thủ công sang tự động, nhanh chóng và chính xác. Hãy thử ngay, điều chỉnh prompt và credentials phù hợp với dữ liệu của mình, và trải nghiệm sự tiện lợi của AI trong công việc hàng ngày!