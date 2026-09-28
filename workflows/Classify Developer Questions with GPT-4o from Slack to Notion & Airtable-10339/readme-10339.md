---
title: "🤖 Tự Động Hóa Phân Loại Câu Hỏi Phát Triển Sử Dụng GPT-4o: Từ Slack → Notion & Airtable"
description: "Workflow tự động phân loại, lưu trữ câu hỏi phát triển từ Slack vào Notion (FAQ) và Airtable (chờ xử lý), tiết kiệm 80% thời gian hỗ trợ kỹ thuật. Sử dụng GPT-4o để tự động hóa triết lý tri thức nội bộ."
slug: "tieu-dong-hoa-phan-loai-cau-hoi-phat-trien-gpt-4o"
tags: [n8n, automation, ai-agent, slack, notion, airtable, gpt-4o, no-code, internal-wiki]
keywords: [n8n workflow tự động hóa, phân loại câu hỏi phát triển, GPT-4o tự động hóa, Slack → Notion, lưu trữ FAQ tự động, Airtable cho câu hỏi chưa trả lời]
---

# 🚀 **Tự Động Hóa Phân Loại Câu Hỏi Phát Triển: Từ Slack → Notion & Airtable**

### **Nỗi Đau Của Các Sếp & Giải Pháp N8n**
Hàng ngày, các sếp và đội ngũ kỹ thuật phải mất **từ 30-60 phút** để:
- **Lọc và phân loại** hàng chục câu hỏi phát triển trên Slack.
- **Tìm kiếm và sao chép** câu trả lời từ FAQ cũ (nếu có).
- **Lưu trữ** câu hỏi mới vào Notion để xây dựng tri thức nội bộ.
- **Đánh giá** chất lượng câu trả lời và **đánh dấu** những câu hỏi chưa được trả lời để hỗ trợ sau.

**Workflow này tự động hóa toàn bộ quy trình trên bằng AI (GPT-4o) + n8n**, giúp:
✅ **Tiết kiệm 80% thời gian** cho đội ngũ kỹ thuật.
✅ **Tự động phân loại** câu hỏi thành "đã trả lời" (được lưu vào Notion) hoặc "chưa trả lời" (được chuyển sang Airtable).
✅ **Xây dựng tri thức nội bộ** một cách tự động từ các cuộc thảo luận Slack.
✅ **Giảm thiểu sự lặp lại** bằng cách tái sử dụng câu trả lời từ FAQ.

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình hỗ trợ kỹ thuật** từ Slack đến Notion/Airtable.
- **Giảm tải cho đội ngũ kỹ thuật** bằng cách tự động phân loại và lưu trữ câu hỏi.
- **Xây dựng FAQ tự động** từ các cuộc thảo luận Slack, giúp mới viên nhanh chóng tìm kiếm thông tin.
- **Theo dõi câu hỏi chưa trả lời** trong Airtable để hỗ trợ kịp thời.
- **Lưu log lỗi** trong Google Sheets để theo dõi và sửa chữa workflow.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Slack** với quyền truy cập vào channel phát triển (ví dụ: `#dev-questions`).
2. **API Key Azure OpenAI** (để sử dụng GPT-4o).
3. **Tài khoản Notion** với quyền chỉnh sửa database FAQ.
4. **Tài khoản Airtable** với quyền tạo bản ghi mới.
5. **Google Sheets** để lưu log lỗi (nếu cần).
6. **Credentials trong n8n**:
   - `slackApi` (Slack Token).
   - `azureOpenAiApi` (API Key Azure OpenAI).
   - `notionApi` (Notion Integration Token).
   - `airtableTokenApi` (Airtable API Key).
   - `googleSheetsOAuth2Api` (Google Sheets OAuth 2.0).
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/10339](https://n8n.io/workflows/10339) hoặc copy toàn bộ JSON từ trang này.
- **Mở n8n Editor** và chọn **Import Workflow** → Dán JSON hoặc tải file `.json`.
- **Kích hoạt workflow** bằng cách bấm **Active** ở góc trên bên phải.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **10 node** quan trọng, các sếp cần cấu hình kỹ lưỡng:

#### **A. Node "Slack Channel Trigger – Developer Q&A"**
- **Chọn channel Slack** cần theo dõi (ví dụ: `#dev-questions`).
- **Lưu ý**:
  - Chỉ **câu hỏi từ người dùng** mới được xử lý (loại bỏ tin nhắn hệ thống).
  - Nếu channel không hoạt động, kiểm tra **permissions** của Slack App.

#### **B. Node "Configure GPT-4o Model"**
- **Điền `azureOpenAiApi`** (credentials đã thiết lập trước).
- **Chọn model**: `gpt-4o` (đã cấu hình sẵn).
- **Lưu ý**:
  - Nếu API Key Azure OpenAI hết hạn, workflow sẽ **bị lỗi** và log vào Google Sheets.

#### **C. Node "Classify Developer Question (AI)"**
- **AI Agent này** sẽ so sánh câu hỏi với **FAQ nội bộ** và trả về kết quả JSON.
- **Cấu hình**:
  - **Prompt**: N8n tự động sử dụng template mặc định (không cần chỉnh sửa).
  - **Output**: Kết quả sẽ là JSON với các trường:
    ```json
    {
      "status": "answered" | "unanswered",
      "answer_quality": "high" | "medium" | "low",
      "canonical_answer": "Câu trả lời tiêu chuẩn"
    }
    ```

#### **D. Node "Save Answered Question to Notion FAQ"**
- **Chọn database Notion** cần lưu (ví dụ: `FAQ Database`).
- **Cấu hình trường**:
  - `Status`: `answered`
  - `Answer Quality`: `high`/`medium`/`low`
  - `Canonical Answer`: Câu trả lời từ AI.
- **Lưu ý**:
  - Nếu Notion API lỗi, workflow sẽ **log vào Google Sheets**.

#### **E. Node "Log Unanswered Question to Airtable"**
- **Chọn bảng Airtable** (ví dụ: `Unanswered Questions`).
- **Cấu hình trường**:
  - `Question Text`: Nội dung câu hỏi từ Slack.
  - `User ID`: ID người gửi.
  - `AI Classification`: Kết quả phân loại từ AI.
- **Lưu ý**:
  - Airtable sẽ tự động tạo **một bản ghi mới** cho mỗi câu hỏi chưa trả lời.

#### **F. Node "Log Workflow Errors to Google Sheets"**
- **Chọn sheet Google Sheets** (ví dụ: `n8n-error-log`).
- **Cấu hình cột**:
  - `Error ID`: ID lỗi tự động.
  - `Error Description`: Nội dung lỗi.
  - `Timestamp`: Thời gian xảy ra.
- **Lưu ý**:
  - **Bắt buộc** phải có sheet này để theo dõi lỗi.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** với một câu hỏi mẫu từ Slack:
   - Gửi tin nhắn vào channel đã cấu hình.
   - Kiểm tra **Notion** (nếu câu hỏi đã trả lời) và **Airtable** (nếu chưa).
2. **Bật Active workflow** sau khi kiểm tra thành công.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH LÀM NÀY ĐỂ TIẾT KIỆM THÊM THỜI GIAN]
- **Kết hợp với Slack Bot**: Tạo một bot Slack để **gửi thông báo** khi câu hỏi được trả lời hoặc chuyển sang Airtable.
- **Tự động cập nhật FAQ**: Sau khi có đủ câu hỏi, **dùng Python + n8n** để **tập huấn mô hình AI** để cải thiện chất lượng phân loại.
- **Gửi báo cáo định kỳ**: Sử dụng **n8n + Google Sheets** để **tạo báo cáo hàng tuần** về số lượng câu hỏi đã trả lời vs. chưa trả lời.
- **Lưu log AI**: Sử dụng **Sticky Note** để lưu **prompt và output** của AI để theo dõi và cải thiện.
- **Kết hợp với Jira**: Nếu có câu hỏi liên quan đến bug, **tự động tạo ticket Jira** từ Airtable.
:::

---
## 📌 **Kết Luận**
Workflow này **giải phóng đội ngũ kỹ thuật** khỏi việc lặp lại công việc thủ công, đồng thời **xây dựng tri thức nội bộ** một cách tự động. Với **GPT-4o + n8n**, các sếp có thể:
✔ **Tiết kiệm 80% thời gian** cho đội ngũ hỗ trợ.
✔ **Tự động phân loại** câu hỏi thành "đã trả lời" và "chưa trả lời".
✔ **Xây dựng FAQ tự động** từ các cuộc thảo luận Slack.
✔ **Theo dõi và cải thiện** chất lượng hỗ trợ kỹ thuật.

**🚀 Hãy áp dụng ngay workflow này và tự động hóa quy trình hỗ trợ kỹ thuật của doanh nghiệp!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::