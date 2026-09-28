---
title: "🤖 Tự Động Hóa Tóm Tắt & Trả Lời Câu Hỏi từ Tài Liệu PDF/TXT bằng GPT-4o + Thông Báo Slack (N8N)"
description: "Workflow này tự động trích xuất nội dung từ file PDF/TXT, tạo tóm tắt 150-200 từ và 5 câu hỏi trả lời thông minh bằng GPT-4o, đồng thời gửi kết quả về webhook và preview qua Slack. Giúp các sếp tiết kiệm thời gian phân tích tài liệu lên đến 80%."
slug: "tieu-dong-hoa-tom-tat-tai-lieu-pdf-txt-bang-gpt-4o"
tags: [n8n, automation, ai-summarization, document-extraction, slack-integration]
keywords: [n8n workflow pdf txt, tự động hóa tóm tắt tài liệu, gpt-4o n8n, trích xuất nội dung pdf, slack alert tự động]
---

# 🚀 **Tự Động Hóa Tóm Tắt & Trả Lời Câu Hỏi từ Tài Liệu PDF/TXT bằng GPT-4o + Thông Báo Slack**

### **Giải pháp cho các sếp:**
Bạn có bao giờ phải đọc hàng chục trang tài liệu PDF/TXT để tìm thông tin quan trọng, sau đó phải tóm tắt lại và trả lời các câu hỏi liên quan? Hoặc phải phân tích báo cáo dài dòng để chuẩn bị cho cuộc họp? **Workflow này sẽ tự động hóa toàn bộ quá trình đó chỉ trong vài giây!**

Với **n8n + GPT-4o**, bạn có thể:
✅ **Trích xuất văn bản** từ file PDF/TXT một cách chính xác.
✅ **Tạo tóm tắt 150-200 từ** và **5 câu hỏi trả lời thông minh** bằng trí tuệ nhân tạo.
✅ **Kiểm tra và log lỗi** nếu AI trả về kết quả không hợp lệ.
✅ **Gửi kết quả về hệ thống** thông qua webhook và **preview qua Slack** để các thành viên team nhanh chóng review.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 80%** khi phân tích tài liệu thủ công.
- **Chính xác cao** với tóm tắt và câu hỏi trả lời được AI tối ưu hóa.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Dễ dàng mở rộng** với các tính năng như lưu log, báo cáo định kỳ, hoặc tích hợp với nhiều hệ thống khác.
- **Cá nhân hóa** kết quả với khả năng điều chỉnh prompt cho từng loại tài liệu.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n Self-hosted** (để chạy 24/7 ổn định).
2. **API Key Azure OpenAI** (để sử dụng GPT-4o).
3. **Credentials Google Sheets** (để log lỗi nếu AI trả về kết quả không hợp lệ).
4. **Credentials Slack API** (để gửi preview kết quả).
5. **Webhook URL** (để nhận kết quả cuối cùng từ workflow).
:::

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Bước 1:** Tải file JSON của workflow từ [n8n.io/workflows/11736](https://n8n.io/workflows/11736).
- **Bước 2:** Mở **n8n Editor** và chọn **Import Workflow** → Chọn file JSON vừa tải.
- **Bước 3:** Chọn **Import** để workflow xuất hiện trên canvas.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **15 node** với các chức năng chính sau. Dưới đây là hướng dẫn chi tiết để cấu hình:

##### **📥 Nhận và kiểm tra file tải lên**
- **Node: "Receive Document Upload via Webhook"**
  - **Cấu hình:**
    - **Path:** `65df1798-c390-404d-827c-be1bf6fbe411` (không thay đổi).
    - **HTTP Method:** POST (không thay đổi).
    - **Credentials:** Không cần thiết (sử dụng mặc định).

- **Node: "Check If Uploaded File Is PDF" & "Check If Uploaded File Is TXT"**
  - **Cấu hình:**
    - Chọn **File** từ node trước đó (`Receive Document Upload via Webhook`).
    - **Condition:** Kiểm tra `file.name.endsWith('.pdf')` (cho PDF) hoặc `file.name.endsWith('.txt')` (cho TXT).

##### **📄 Trích xuất văn bản từ file**
- **Node: "Extract Text from PDF File"**
  - **Cấu hình:**
    - **Operation:** `pdf` (không thay đổi).
    - **Input:** Chọn kết quả từ node `Check If Uploaded File Is PDF`.

- **Node: "Extract Text from TXT File"**
  - **Cấu hình:**
    - **Operation:** `text` (không thay đổi).
    - **Input:** Chọn kết quả từ node `Check If Uploaded File Is TXT`.

##### **🤖 Tạo tóm tắt và câu hỏi trả lời bằng AI**
- **Node: "Provide LLM Engine for Document Analysis"**
  - **Cấu hình:**
    - **Credentials:** Chọn `azureOpenAiApi` (đã cấu hình trước khi import).
    - **Model:** `gpt-4o` (không thay đổi).
    - **Prompt:** Nếu muốn điều chỉnh, chỉnh sửa trong node `Generate Summary & Q&A Using AI` (xem bên dưới).

- **Node: "Generate Summary & Q&A Using AI"**
  - **Cấu hình:**
    - **Agent:** Chọn `agent` (đã cấu hình sẵn trong workflow).
    - **Input:** Chọn kết quả từ node trích xuất văn bản (`Extract Text from PDF File` hoặc `Extract Text from TXT File`).
    - **Prompt mẫu (nếu cần chỉnh sửa):**
      ```json
      {
        "instruction": "Tóm tắt nội dung tài liệu này thành 150-200 từ. Sau đó, tạo 5 câu hỏi thường gặp về nội dung này và trả lời chi tiết cho mỗi câu hỏi. Đảm bảo câu trả lời ngắn gọn và chính xác.",
        "outputSchema": {
          "summary": "string",
          "qas": [
            {
              "question": "string",
              "answer": "string"
            }
          ]
        }
      }
      ```

- **Node: "Parse AI Summary and Q&A into Structured JSON"**
  - **Cấu hình:**
    - **Input:** Chọn kết quả từ node `Generate Summary & Q&A Using AI`.
    - **Output Parser:** Chọn `outputParserStructured` (đã cấu hình sẵn).

##### **⚠️ Kiểm tra và log lỗi**
- **Node: "Validate AI Output Before Processing"**
  - **Cấu hình:**
    - **Condition:** Kiểm tra `$.output !== null && $.output !== undefined`.

- **Node: "Log Invalid AI Output to Google Sheet"**
  - **Cấu hình:**
    - **Credentials:** Chọn `googleSheetsOAuth2Api`.
    - **Sheet Name:** Điền tên sheet (ví dụ: `AI_Error_Logs`).
    - **Range:** `A1` (để ghi dữ liệu từ hàng đầu tiên).
    - **Input:** Chọn kết quả từ node `Validate AI Output Before Processing` (nếu lỗi).

##### **📤 Chuẩn bị và gửi kết quả cuối cùng**
- **Node: "Unwrap AI Output Object"**
  - **Cấu hình:**
    - **Code:** Sử dụng mã sau để đảm bảo kết quả là một object đơn giản:
      ```javascript
      return {
        summary: $input.all()[0].json.output.summary,
        qas: $input.all()[0].json.output.qas
      };
      ```

- **Node: "Prepare Final Response Payload"**
  - **Cấu hình:**
    - **Code:** Đảm bảo kết quả là JSON sạch:
      ```javascript
      return {
        json: {
          summary: $input.all()[0].json.summary,
          qas: $input.all()[0].json.qas
        }
      };
      ```

- **Node: "Send Final Summary & Q&A Response to Webhook"**
  - **Cấu hình:**
    - **Webhook URL:** Điền URL của webhook bạn muốn nhận kết quả.
    - **Input:** Chọn kết quả từ node `Prepare Final Response Payload`.

- **Node: "Send Summary Preview to Slack"**
  - **Cấu hình:**
    - **Credentials:** Chọn `slackApi`.
    - **Channel:** Điền tên channel Slack (ví dụ: `#document-summaries`).
    - **Message:** Sử dụng template:
      ```
      *Tóm tắt tài liệu mới:*
      {{ $input.all()[0].json.summary.substring(0, 300) }}...
      ```

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Tích hợp với Google Drive/OneDrive:**
   - Sử dụng node `googleDrive` hoặc `onedrive` để tự động tải tài liệu từ cloud vào workflow.

2. **Gửi báo cáo định kỳ:**
   - Sử dụng node `set` + `schedule` để gửi tổng hợp tóm tắt hàng tuần qua email hoặc Slack.

3. **Cải thiện prompt cho từng loại tài liệu:**
   - Tạo các prompt riêng biệt cho PDF báo cáo, tài liệu pháp lý, hoặc bài giảng để tăng độ chính xác.

4. **Lưu log chi tiết vào Google Sheets:**
   - Thêm cột `timestamp`, `file_name`, và `user_id` vào sheet log để theo dõi lịch sử.

5. **Tích hợp với Microsoft Teams:**
   - Thay thế node Slack bằng node `microsoftTeams` để gửi preview kết quả.
:::

---
### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần tự động hóa việc phân tích tài liệu PDF/TXT một cách nhanh chóng và chính xác. Bằng cách kết hợp **trích xuất văn bản, AI tóm tắt, và thông báo Slack**, bạn sẽ tiết kiệm thời gian và giảm thiểu sai sót trong quá trình làm việc.

**Hãy thử ngay!**
1. **Cài đặt n8n Self-hosted** trên VPS (để chạy 24/7).
2. **Cấu hình các credentials** (Azure OpenAI, Google Sheets, Slack).
3. **Import workflow** và **bật Active**.
4. **Upload file PDF/TXT** qua webhook và xem kết quả!

👉 **Nếu cần hỗ trợ thêm, hãy liên hệ với cộng đồng n8n hoặc đăng ký VPS ổn định từ [TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm giá **VPSN8N**!** 🚀