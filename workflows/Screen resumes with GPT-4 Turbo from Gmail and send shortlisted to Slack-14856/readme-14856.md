---
title: "🤖 **Tự Động Hóa Xét Duyệt Hồ Sơ CV Bằng GPT-4 Turbo Từ Gmail & Gửi Kết Quả Sang Slack - Không Cần Code!**"
description: "Workflow tự động hóa hoàn toàn bằng n8n giúp các sếp HR lấy CV từ Gmail, phân tích nội dung bằng AI (GPT-4 Turbo), đánh giá điểm số phù hợp với yêu cầu công việc, và tự động gửi danh sách ứng viên lọt chọn sang Slack. Giảm thời gian xét duyệt CV từ 30 phút/lần xuống còn 5 phút!"
slug: "tieu-duyet-cv-bang-gpt-4-turbo-va-gui-kq-sang-slack"
tags: [n8n, automation, hr, ai-summarization, gpt-4-turbo, slack-integration, gmail-api]
keywords: [tự động hóa xét duyệt CV, n8n workflow HR, AI phân tích hồ sơ, GPT-4 Turbo tự động hóa, gửi kết quả Slack, giảm thời gian tuyển dụng]
---

# 🚀 **Tự Động Hóa Xét Duyệt Hồ Sơ CV Bằng AI (GPT-4 Turbo) Từ Gmail & Gửi Kết Quả Sang Slack**

### **Giải pháp cho nỗi đau của các sếp HR:**
Hàng ngày, các sếp phải mất **30-60 phút** để xem xét từng hồ sơ CV từ email, sao chép thông tin vào bảng tính, và đánh giá phù hợp với yêu cầu công việc. Với **số lượng ứng viên lớn**, quá trình này trở nên **mệt mỏi, dễ sai sót**, và không thể hoạt động liên tục 24/7.

**Workflow này giải quyết toàn bộ vấn đề bằng cách:**
✅ **Lấy tự động** tất cả CV từ Gmail (dạng PDF/Word) trong một email duy nhất.
✅ **Phân tích AI** bằng GPT-4 Turbo để trích xuất **tên, kỹ năng, kinh nghiệm, điểm số phù hợp** với yêu cầu công việc.
✅ **Đánh giá tự động** và **lọc ứng viên** dựa trên ngưỡng điểm số (các sếp có thể điều chỉnh).
✅ **Gửi kết quả** sang Slack với **danh sách ứng viên lọt chọn** (kèm điểm số, kỹ năng nổi bật) và **ghi chú từ AI**.
✅ **Hoạt động liên tục** mà không cần can thiệp thủ công.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 80% thời gian** so với cách làm thủ công (từ 30 phút/lần xuống còn 5 phút).
- **Chính xác 100%** nhờ AI trích xuất thông tin từ CV một cách logic.
- **Cá nhân hóa đánh giá** với điểm số phù hợp với yêu cầu công việc cụ thể.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Gửi báo cáo tự động** sang Slack để dễ dàng theo dõi và chia sẻ với team.
- **Giảm sai sót** khi đánh giá thủ công (ví dụ: bỏ qua ứng viên có kỹ năng phù hợp).
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (đã cấp quyền OAuth 2.0 cho n8n):
   - Các sếp cần **cho phép n8n truy cập vào email** để lấy CV từ drafts.
   - **Lưu ý:** Chỉ lấy email **có chứa CV** (không lấy toàn bộ thư mục Inbox).
2. **API Key OpenAI** (để sử dụng GPT-4 Turbo):
   - Đăng ký tài khoản tại [OpenAI](https://platform.openai.com/) và lấy **API Key**.
   - **Khuyến nghị:** Sử dụng **GPT-4 Turbo** (mô hình mới nhất, hiệu quả cao nhất).
3. **Tài khoản Slack** (để gửi kết quả):
   - Tạo **Bot Slack** và lấy **API Token** từ [Slack API](https://api.slack.com/apps).
   - Chọn **Channel Slack** để nhận thông báo (ví dụ: `#hiring`).
4. **Yêu cầu công việc cụ thể** (để AI đánh giá):
   - Các sếp cần **định nghĩa rõ ràng** các kỹ năng, kinh nghiệm, và tiêu chí đánh giá (ví dụ: "Cần kỹ năng Python, 2+ năm kinh nghiệm Fullstack").
   - **Mô hình này sẽ tự động** trích xuất và so sánh với yêu cầu của các sếp.

---
## 🚀 **Cách Import & Lưu ý khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/14856](https://n8n.io/workflows/14856) (chọn **Export as JSON**).
2. **Mở n8n Editor** (trên máy chủ self-hosted hoặc n8n.cloud).
3. **Nhấn "Import"** và chọn file JSON vừa tải.
4. **Xác nhận import** và workflow sẽ hiện lên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/14856](https://n8n.io/workflows/14856).
2. **Mở n8n Editor** và nhấn **"Import"** → **"Paste JSON"**.
3. **Xác nhận** và workflow sẽ được tạo.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **13 node** quan trọng, các sếp cần **cấu hình kỹ lưỡng** các phần sau:

#### **🔹 Node 1: "Start Workflow Manually" (manualTrigger)**
- **Chức năng:** Khởi động workflow thủ công (không tự động chạy).
- **Lưu ý:**
  - Các sếp **không cần thiết lập trigger tự động** (ví dụ: Webhook) vì workflow này chỉ chạy khi **nhấn nút "Run"** trên n8n Editor.
  - **Mẹo:** Đặt **lịch chạy định kỳ** (nếu muốn) bằng cách kết nối với **n8n-nodes-base.schedule**.

#### **🔹 Node 2: "Fetch Gmail" (gmail)**
- **Chức năng:** Lấy tất cả email draft từ Gmail có chứa CV.
- **Cấu hình:**
  - **Credentials:** Chọn **"gmailOAuth2"** (đã cấu hình trước).
  - **Operation:** Đặt **"getAll"** (lấy tất cả email draft).
  - **Lọc email:** Các sếp cần **sửa code trong node "Format Attachments"** (node 3) để chỉ lấy email có **tên file CV** (ví dụ: `*.pdf`, `*.docx`).
    ```javascript
    // Sửa trong node "Format Attachments" (type: function)
    const emailsWithAttachments = data.map(email => {
      const hasPdf = email.attachments.some(att => att.filename.endsWith('.pdf'));
      const hasDocx = email.attachments.some(att => att.filename.endsWith('.docx'));
      return { ...email, hasResume: hasPdf || hasDocx };
    });
    return emailsWithAttachments.filter(email => email.hasResume);
    ```

#### **🔹 Node 3: "Format Attachments" (function)**
- **Chức năng:** Lọc và chuẩn bị danh sách CV từ email.
- **Lưu ý:**
  - **Sửa code** như trên để chỉ lấy email có **CV** (PDF/Word).
  - **Output:** Danh sách email có thuộc tính `hasResume: true`.

#### **🔹 Node 4: "Check Attachments Exist" (if)**
- **Chức năng:** Kiểm tra xem email có CV không.
- **Cấu hình:**
  - **Condition:** `$.hasResume === true` (đã được xử lý trong node 3).

#### **🔹 Node 5: "Process Each Attachment" (splitInBatches)**
- **Chức năng:** Chia từng CV thành một batch riêng.
- **Cấu hình:**
  - **Batch Size:** Đặt **1** (xử lý từng CV một).
  - **Output:** Mỗi CV sẽ được xử lý riêng trong các node tiếp theo.

#### **🔹 Node 6: "Validate PDF File" (if)**
- **Chức năng:** Kiểm tra xem file CV có phải PDF không.
- **Lưu ý:**
  - **Sửa condition** nếu muốn hỗ trợ **Word/Excel**:
    ```javascript
    // Sửa trong node "Validate PDF File" (type: if)
    const isPdf = data.filename.endsWith('.pdf');
    const isDocx = data.filename.endsWith('.docx');
    return { isValid: isPdf || isDocx };
    ```
  - **Output:** Chỉ cho phép file **PDF/Word** tiếp tục.

#### **🔹 Node 7: "Extract Resume Text" (extractFromFile)**
- **Chức năng:** Trích xuất văn bản từ CV (PDF/Word).
- **Cấu hình:**
  - **Operation:** Đặt **"pdf"** (nếu là PDF) hoặc **"docx"** (nếu là Word).
  - **Lưu ý:** Nếu CV là **Word**, cần cài **node `extractFromFile` hỗ trợ DOCX** (có thể cài thêm từ [n8n Marketplace](https://marketplace.n8n.io/)).

#### **🔹 Node 8: "AI Resume Analyzer" (agent)**
- **Chức năng:** Gửi văn bản CV vào GPT-4 Turbo để phân tích.
- **Cấu hình:**
  - **Credentials:** Chọn **"openAiApi"** (đã cấu hình API Key).
  - **Model:** Đặt **"gpt-4-turbo"** (mô hình mới nhất).
  - **Prompt:** **Sửa theo yêu cầu công việc cụ thể** của các sếp.
    **Ví dụ prompt:**
    ```
    Bạn là một chuyên gia tuyển dụng AI. Hãy phân tích hồ sơ CV dưới đây và trả lời theo định dạng JSON:
    {
      "name": "Tên ứng viên",
      "skills": ["Danh sách kỹ năng", "nó có phù hợp không"],
      "experience": {
        "years": "Số năm kinh nghiệm",
        "relevant": "Có phù hợp với công việc không (true/false)"
      },
      "contact": {
        "email": "Email",
        "phone": "Số điện thoại"
      },
      "matchScore": "Điểm số từ 0-100 (căn cứ vào yêu cầu công việc)"
    }

    Yêu cầu công việc:
    - Kỹ năng cần: Python, JavaScript, Docker, AWS
    - Kinh nghiệm: 2+ năm Fullstack
    - Tiêu chí đánh giá:
      1. Nếu có 3+ kỹ năng trên → điểm số >= 80
      2. Nếu có 2 kỹ năng + 3+ năm kinh nghiệm → điểm số >= 70
      3. Nếu không phù hợp → điểm số < 50

    CV:
    {{{$json.text}}}
    ```
  - **Lưu ý:** **Prompt này là chìa khóa** quyết định độ chính xác của AI. Các sếp nên **điều chỉnh** theo yêu cầu cụ thể của công ty.

#### **🔹 Node 9: "Parse AI Response" (code)**
- **Chức năng:** Chuyển kết quả JSON từ AI thành định dạng dễ đọc.
- **Lưu ý:**
  - **Sửa code** để đảm bảo kết quả từ AI được **parse chính xác**:
    ```javascript
    // Sửa trong node "Parse AI Response" (type: code)
    const aiResponse = JSON.parse(data.json);
    return {
      ...aiResponse,
      formattedSkills: aiResponse.skills.join(", "),
      isShortlisted: aiResponse.matchScore >= 70 // Điều chỉnh ngưỡng điểm
    };
    ```

#### **🔹 Node 10: "Evaluate Candidate Score" (if)**
- **Chức năng:** Lọc ứng viên dựa trên điểm số.
- **Cấu hình:**
  - **Condition:** `$.matchScore >= 70` (điều chỉnh ngưỡng điểm theo yêu cầu).
  - **Lưu ý:** Nếu điểm số **< 70**, ứng viên sẽ được **ghi nhãn "Rejected"** (node 13).

#### **🔹 Node 11: "Send Shortlisted to Slack" (slack)**
- **Chức năng:** Gửi thông báo ứng viên lọt chọn sang Slack.
- **Cấu hình:**
  - **Credentials:** Chọn **"slackApi"** (đã cấu hình).
  - **Channel:** Chọn **Channel Slack** (ví dụ: `#hiring`).
  - **Message Format:** **Sửa template** để hiển thị thông tin chi tiết:
    ```json
    {
      "text": "🔍 **Ứng viên lọt chọn**: {{ $json.name }}",
      "attachments": [
        {
          "title": "Thông tin chi tiết",
          "text": `
          - **Điểm số**: {{ $json.matchScore }}/100
          - **Kỹ năng**: {{ $json.formattedSkills }}
          - **Kinh nghiệm**: {{ $json.experience.years }} năm
          - **Email**: {{ $json.contact.email }}
          - **Số điện thoại**: {{ $json.contact.phone }}
          - **Ghi chú từ AI**: {{ $json.aiNotes || "Không có ghi chú" }}
          `,
          "color": "#2eb67d" // Màu xanh (lọt chọn)
        }
      ]
    }
    ```
  - **Lưu ý:** Sử dụng **`{{ $json.key }}`** để hiển thị dữ liệu từ AI.

#### **🔹 Node 12: "Mark as Rejected" (set)**
- **Chức năng:** Ghi nhãn ứng viên bị loại.
- **Cấu hình:**
  - **Property:** `status`
  - **Value:** `"Rejected"` (hoặc tùy chỉnh theo yêu cầu).

---
### **3. Kích hoạt ⚡️**
1. **Test Run** với **1-2 CV mẫu**:
   - Gửi email draft có **CV PDF/Word** vào Gmail.
   - **Nhấn "Run"** trên workflow.
   - Kiểm tra **Slack** để xem kết quả.
2. **Bật Active**:
   - Sau khi test thành công, **bật "Active"** để workflow chạy tự động khi nhấn nút.

---
## ✍️ **Mẹo & Gợi ý Nâng Cao**
:::info[**CÁC TỐI ƯU HÓAN CẢNH BÁO**]
1. **Kết hợp với Google Sheets để lưu dữ liệu:**
   - Thêm **node `googleSheets`** sau node **"Send Shortlisted