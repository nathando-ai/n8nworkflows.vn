---
title: "🚀 FloWatch: Tự động Phân tích & Chẩn đoán Lỗi n8n bằng AI (OpenAI) & Gửi Email"
description: "Workflow n8n tự động bắt lỗi thực thi (Error Trigger), sử dụng AI Agent (GPT-4o) để phân tích nguyên nhân gốc rễ, đưa ra giải pháp khắc phục và gửi báo cáo chi tiết qua Gmail – Giúp vận hành tự động hóa ổn định, zero-touch."
slug: "flowatch-tu-dong-phan-tich-chuan-doan-loi-n8n-bang-ai"
tags: [n8n, automation, ai-agent, error-handling, openai, gmail, devops]
keywords: [n8n workflow, tự động hóa xử lý lỗi, ai chẩn đoán lỗi, openai gpt-4o, error trigger n8n, gửi email báo cáo lỗi]
---

# 🚀 FloWatch: "Cánh tay phải" AI giám sát & chẩn đoán lỗi n8n 24/7

Bạn đang vận hành hàng chục workflow n8n quan trọng? Mỗi lần workflow fail là bạn phải mở Execution log, đọc đống JSON lỗi, search Google, hỏi ChatGPT rồi mới biết sửa sao? **Quá tốn thời gian và mệt mỏi!**

**FloWatch** giải quyết triệt để bài toán này: **Tự động bắt lỗi ➡️ AI đọc hiểu ngữ cảnh ➡️ Chẩn đoán nguyên nhân ➡️ Đề xuất fix ➡️ Gửi thẳng vào Inbox Gmail.** Bạn chỉ việc mở mail, đọc báo cáo, copy fix -> done. Không cần code, không cần canh màn hình.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow giám sát lỗi chạy ổn định 24/7 (đặc biệt là Error Trigger cần instance luôn online), các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **🛡️ Zero-touch Monitoring:** Tự động phát hiện lỗi ngay lập tức khi workflow bất kỳ fail, không cần setup webhook cho từng workflow.
- **🧠 Chẩn đoán cấp chuyên gia:** GPT-4o phân tích stack trace, node config, input data để tìm *root cause* (nguyên nhân gốc rễ) thay vì chỉ đọc message lỗi bề mặt.
- **💡 Đề xuất giải pháp hành động:** Không chỉ báo lỗi, AI Agent đưa ra bước sửa cụ thể (ví dụ: "Sai mapping field ở node HTTP Request", "Token Google Sheets hết hạn", "Webhook URL sai format").
- **📧 Báo cáo chuyên nghiệp về Email:** Nhận mail định dạng đẹp, có tiêu đề workflow, thời gian, link trực tiếp đến Execution failed trên n8n để debug ngay.
- **⚙️ Linh hoạt kiểm soát:** Bật/tắt giám sát cho Manual Execution (chạy test thủ công) chỉ bằng một cái switch trên node `If`.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi import, các sếp chuẩn bị sẵn 3 credential sau trong n8n:
1.  **n8n API Credential** (`n8nApi`): Dùng để node `Get Failed Exec` gọi API nội bộ lấy chi tiết execution lỗi.
    *   *Cách lấy:* Settings > API > Create API Key (cần n8n version hỗ trợ API).
2.  **OpenAI API Credential** (`openAiApi`): Dùng cho node `OpenAI Chat Model` (model `gpt-4o` khuyến nghị) và `Error Solver Agent`.
3.  **Gmail OAuth2 Credential** (`gmailOAuth2`): Dùng cho node `Send Gmail` để gửi báo cáo.
    *   *Lưu ý:* Cần bật Gmail API trên Google Cloud Console, cấu hình OAuth Consent Screen, thêm scope `https://www.googleapis.com/auth/gmail.send`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON workflow về máy.
- Trên n8n Editor: Click **Workflows** > **Import** > Chọn file JSON > **Import**.
- Hoặc copy toàn bộ JSON > Paste vào Editor mới (Ctrl+V).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Mở workflow lên, các sếp **bắt buộc** cấu hình các node sau:

| Node | Tên hiển thị | Hành động cấu hình bắt buộc |
| :--- | :--- | :--- |
| **🔐 Credentials** | (Toàn bộ workflow) | Click vào từng node có biểu tượng khóa 🔒 (OpenAI Chat Model, Get Failed Exec, Send Gmail) > Chọn **Credential** tương ứng đã tạo ở mục "Yêu cầu cần thiết". |
| **📧 SET EMAIL** | `SET EMAIL` | **QUAN TRỌNG:** Điền email nhận báo cáo vào field `toEmail` (hoặc `recipient`). Có thể thêm nhiều email cách nhau bằng dấu phẩy. |
| **🤖 OpenAI Chat Model** | `OpenAI Chat Model` | Kiểm tra **Model**: Khuyến nghị `gpt-4o` (hoặc `gpt-4-turbo`). Temperature để thấp (`0.1 - 0.3`) để output nhất quán, logic. |
| **🧠 Error Solver Agent** | `Error Solver Agent` | Node Agent này đã được cấu hình sẵn System Prompt chuyên biệt. **KHÔNG NÊN SỬA PROMPT** trừ khi các sếp rành về Prompt Engineering. Chỉ cần đảm bảo nó kết nối đúng `OpenAI Chat Model` và `Structured Output Parser`. |
| **📝 Structured Output Parser** | `Structured Output Parser` | Đảm bảo schema JSON output khớp với những gì node `Generate Email` và `Set Diagnosis Fields` mong đợi (thường gồm: `rootCause`, `suggestedFix`, `severity`, `affectedNode`). |
| **🔀 Remove Manual Exec** | `Remove Manual Exec` | Node `If` này lọc bỏ lỗi do chạy thủ công (Manual Execution).<br>• **True (Giữ lại):** Chạy tự động (Webhook, Cron, Trigger).<br>• **False (Bỏ qua):** Chạy test bằng nút "Execute Workflow".<br>👉 Mặc định để **True** để không spam mail khi test. |
| **📥 Get Failed Exec** | `Get Failed Exec` | Operation: `Get`, Resource: `Execution`. Node này dùng `executionId` từ `Error Trigger` để pull full log. Không cần đổi param. |
| **🛠️ Extract Error Details** | `Extract Error Details` | Node `Code` (JavaScript) trích xuất: `error.message`, `node.name`, `node.type`, `inputData`, `stack trace`. **Không cần sửa code** trừ khi n8n đổi cấu trúc response API. |
| **✍️ Generate Email** | `Generate Email` | Node `Code` render HTML email đẹp từ output của Agent. Kiểm tra biến `toEmail` có lấy đúng từ `SET EMAIL` không. |
| **📤 Send Gmail** | `Send Gmail` | - **From:** Email gửi (thường là tài khoản OAuth2).<br>- **To:** Expression `{{ $json.toEmail }}`.<br>- **Subject:** `🚨 [FloWatch] Lỗi Workflow: {{ $json.workflowName }}`.<br>- **Body:** HTML từ node `Generate Email`. |

#### 3. Kích hoạt ⚡️
1.  Click **Save** lưu workflow.
2.  Chạy **Test Workflow** (Execute Workflow) -> Lúc này node `Remove Manual Exec` sẽ chặn (False) -> Không gửi mail. **Đây là hành vi đúng.**
3.  Để test thật: Tạo một workflow khác -> Thêm node `Error Trigger` (hoặc để fail tự nhiên) -> Chạy **Production** (Active) -> Để nó fail.
4.  Kiểm tra Inbox email nhận báo cáo.
5.  Bật toggle **Active** (góc trên phải) cho workflow **FloWatch**.

### ✍️ Mẹo & gợi ý nâng cao
- **🔔 Gửi song song qua Slack/Telegram:** Thêm node `Slack` hoặc `Telegram` sau `Set Diagnosis Fields` để post vào channel #devops-alerts. Team phản ứng nhanh hơn mail.
- **📊 Lưu log lịch sử vào Google Sheets / Baserow / Airtable:** Thêm node `Google Sheets` (Append) để lưu: `Timestamp`, `Workflow Name`, `Error Type`, `Root Cause`, `Fix Suggestion`, `Status (Open/Fixed)`. Dùng để báo cáo MTTR (Mean Time To Resolve).
- **🔁 Tự động Retry (Healing):** Nếu lỗi dạng "Rate Limit" hoặc "Timeout", có thể thêm node `If` check `rootCause` chứa từ khóa -> Gọi node `n8n` (Resource: Execution, Action: Retry) để tự chạy lại. *Cẩn thận vòng lặp vô tận!*
- **🏷️ Phân loại độ ưu tiên:** Dùng output `severity` từ Agent (Critical/High/Medium/Low) để routing: Critical -> Gọi API PagerDuty/Opsgenie + SMS; Low -> Chỉ log Sheet.

### 📌 Kết luận
**FloWatch** biến n8n từ một công cụ "chạy automation" thành một hệ thống **"tự vận hành, tự chữa bệnh"**. Thay vì các sếp làm "cứu hỏa" lúc 2h sáng, hãy để AI Agent làm việc nặng nhọc: đọc log, hiểu code, tìm bug, viết ticket sửa. Các sếp chỉ việc ra quyết định phê duyệt fix.

👉 **Import ngay hôm nay, cấu hình 3 credential, bật Active -> Ngủ ngon không lo workflow fail lặng lẽ!** 😴🚀