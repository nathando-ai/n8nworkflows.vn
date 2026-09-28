---
title: "🤖 **Tự Động Hóa So Sánh CV vs Mô Tả Vị Trí (JD) với AI Groq & GhostGenius – Giải Pháp ATS Cho Recruiter**"
description: "Workflow này tự động so sánh hồ sơ LinkedIn của ứng viên với mô tả công việc (JD) bằng AI Groq, phát hiện điểm mạnh/nguy cơ, và cung cấp báo cáo phân tích ATS chi tiết. Giúp recruiter tiết kiệm 80% thời gian đánh giá ứng viên."
slug: "tieu-dong-hoa-so-sanh-cv-va-jd-voi-groq-ai"
tags: [n8n, automation, ai-summarization, ats, ghostgenius, groq-ai, recruitment]
keywords: [tự động hóa tuyển dụng, so sánh cv và mô tả công việc, ats ai, ghostgenius api, groq ai, workflow n8n tuyển dụng]
---

# 🚀 **Tự Động Hóa So Sánh CV vs Mô Tả Vị Trí (JD) với AI – Giải Pháp ATS Cho Recruiter**

## 💡 **Nỗi Đau Của Recruiter Hiện Nay**
Hàng ngày, các sếp tuyển dụng phải:
- **Đọc hàng chục CV** để so sánh với mô tả công việc (JD) dài 1 trang.
- **Bị mất thời gian** vì không có công cụ tự động đánh giá điểm mạnh/nguy cơ của ứng viên.
- **Phải đánh giá chủ quan** về kinh nghiệm, kỹ năng, và sự phù hợp với yêu cầu.
- **Không biết** ứng viên có đáp ứng được yêu cầu **ngôn ngữ, địa điểm, hoặc kinh nghiệm cụ thể** trong JD.

**Workflow này giải quyết tất cả!** Dùng AI Groq phân tích CV vs JD, tự động phát hiện điểm mạnh, điểm yếu, và đưa ra **báo cáo ATS chi tiết** chỉ trong vài giây.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: So sánh 100 CV chỉ trong vài phút thay vì nhiều giờ.
✅ **Đánh giá chính xác**: AI phát hiện **ngôn ngữ, địa điểm, kinh nghiệm** không phù hợp.
✅ **Báo cáo ATS chi tiết**: Danh sách **điểm mạnh, điểm yếu, và gợi ý cải thiện**.
✅ **Hoạt động liên tục**: Workflow chạy tự động khi nhận được CV/JD mới.
✅ **Cá nhân hóa**: AI đưa ra **lời khuyên cụ thể** cho từng ứng viên.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng, các sếp cần chuẩn bị:
✔ **Tài khoản GhostGenius** (để lấy dữ liệu CV/JD từ LinkedIn).
✔ **Tài khoản Groq AI** (để sử dụng mô hình AI `moonshotai/kimi-k2-instruct`).
✔ **n8n Self-hosted** (không dùng phiên bản Cloud để bảo mật API keys).
✔ **URL CV và JD** (cần gửi qua Webhook để workflow xử lý).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/8235](https://n8n.io/workflows/8235) (chọn "Export").
2. **Mở n8n Editor** → Nhấn **"Import"** → Chọn file JSON vừa tải.
3. **Chọn phiên bản n8n** phù hợp (cần hỗ trợ nodes `langchain` và `groq`).

#### **Cách 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [n8n.io/workflows/8235](https://n8n.io/workflows/8235) (chọn "Export").
2. **Mở n8n Editor** → Nhấn **"Import"** → Chọn **"Paste JSON"**.
3. **Chọn phiên bản n8n** phù hợp.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **15 node**, nhưng **các node quan trọng nhất** cần cấu hình kỹ:

#### **🔹 Node 1: Webhook (Nhận CV/JD)**
- **Tên node**: `Webhook (GET Form details)`
- **Cấu hình**:
  - **Method**: `POST`
  - **Path**: `linkedin`
  - **Credentials**: `httpBasicAuth` (nếu cần bảo mật).
  - **Lưu ý**: Workflow sẽ **chờ đợi** dữ liệu từ một **form ngoài** (ví dụ: Typeform, Google Form) hoặc **API custom** gửi URL CV/JD.

#### **🔹 Node 2 & 3: Lấy Dữ liệu CV & JD**
- **Tên node**:
  - `Get profile details` (lấy CV từ LinkedIn).
  - `Get job details` (lấy JD từ GhostGenius).
- **Cấu hình**:
  - **Credentials**:
    - `httpBasicAuth` (nếu GhostGenius yêu cầu).
    - `httpHeaderAuth` (để thêm headers như `Authorization: Bearer <API_KEY>`).
  - **URL mẫu**:
    - CV: `https://api.ghostgenius.com/profiles/{linkedin_url}`
    - JD: `https://api.ghostgenius.com/jobs/{job_description_url}`
  - **Lưu ý**:
    - **Không hardcode API key** vào node → **Đặt vào Credentials của n8n** (Settings → Credentials → Thêm mới).
    - **Kiểm tra CORS** nếu API yêu cầu.

#### **🔹 Node 4 & 5: Xây Dựng JSON CV & JD**
- **Tên node**:
  - `Build CV` (node `set`).
  - `Combine_CV` (node `aggregate`).
  - `Build JD` (node `set`).
  - `Combine_JD` (node `aggregate`).
- **Cấu hình**:
  - **Node `set`**: Chỉ định **mô tả JSON** cho CV/JD (ví dụ: `{ "name": "{{$json.name}}", "skills": "{{$json.skills}}", ... }`).
  - **Node `aggregate`**: Kết hợp dữ liệu từ nhiều nguồn (nếu có).

#### **🔹 Node 6: So Sánh ATS (Core Logic)**
- **Tên node**: `ATS compare` (node `set`).
- **Cấu hình**:
  - **Input**: Dữ liệu CV và JD đã kết hợp.
  - **Output**: JSON định dạng như:
    ```json
    {
      "matched_skills": ["Sales", "Negotiation"],
      "missing_skills": ["Dutch", "Mid-market"],
      "location_mismatch": true,
      "recommendation": "Candidate needs Dutch fluency"
    }
    ```
  - **Lưu ý**: **Không thay đổi logic** này quá nhiều, chỉ cần **cập nhật schema** nếu cần.

#### **🔹 Node 7: AI Recruiter Check (Groq)**
- **Tên node**: `Recruiter Check` (node `agent` + `lmChatGroq`).
- **Cấu hình**:
  - **Credentials**: `groqApi` (đặt API key Groq vào Credentials).
  - **Model**: `moonshotai/kimi-k2-instruct` (mô hình AI tốt cho phân tích văn bản).
  - **Prompt mẫu** (cần chỉnh sửa theo yêu cầu):
    ```
    Analyze the candidate's CV and job description. Return a structured JSON with:
    - Matched keywords (skills, experience)
    - Missing requirements (location, language, years of experience)
    - Recommendations for improvement
    ```
  - **Lưu ý**:
    - **Không hardcode API key** → Đặt vào Credentials.
    - **Kiểm tra token limit** của Groq (nếu CV/JD quá dài, cần tách nhỏ).

#### **🔹 Node 8: Trả Lời Webhook (Kết Quả)**
- **Tên node**: `Respond to Webhook`.
- **Cấu hình**:
  - **Response**: Trả về JSON hoặc HTML (tùy chỉnh trong **Code node**).
  - **Lưu ý**: Nếu muốn **gửi kết quả qua Slack/Email**, cần thêm node `n8n-nodes-base.httpRequest` để gọi API của dịch vụ đó.

#### **🔹 Node 9: Code Node (Chỉnh Sửa Kết Quả)**
- **Tên node**: `ThankYOU message` (node `code`).
- **Cấu hình**:
  - **Mã JavaScript** để **định dạng kết quả** thành HTML/JSON.
  - **Ví dụ**:
    ```javascript
    // Chuyển JSON thành HTML báo cáo
    const htmlReport = `
      <h2>ATS Analysis Report</h2>
      <h3>✅ Matched Skills</h3>
      <ul>${json.matched_skills.map(skill => `<li>${skill}</li>`).join('')}</ul>
      <h3>❌ Missing Requirements</h3>
      <ul>${json.missing_skills.map(skill => `<li>${skill}</li>`).join('')}</ul>
    `;
    return { html: htmlReport };
    ```
  - **Lưu ý**: **Không xóa node này** nếu muốn kết quả đẹp.

#### **🔹 Node 10: Xử Lý Lỗi (Error_node)**
- **Tên node**: `Error_node` (node `respondToWebhook`).
- **Cấu hình**:
  - **Trả về lỗi** nếu AI hoặc API gặp vấn đề.
  - **Ví dụ**:
    ```json
    {
      "error": "Failed to fetch CV data",
      "statusCode": 500
    }
    ```

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi **URL CV và JD** qua Webhook (ví dụ: `POST https://tên-n8n.com/webhook/linkedin`).
   - Kiểm tra **Output** của node `Respond to Webhook`.
2. **Bật Active workflow**:
   - Nhấn **"Active"** trên canvas.
   - **Kiểm tra Logs** để đảm bảo không lỗi.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Kết Nối Với Slack/Email**
- **Thêm node `n8n-nodes-base.httpRequest`** để gọi API của Slack/Email.
- **Ví dụ**:
  - Gửi báo cáo qua Slack:
    ```json
    {
      "url": "https://slack.com/api/chat.postMessage",
      "method": "POST",
      "body": {
        "channel": "#recruitment",
        "text": "📊 ATS Analysis Report: *{{$node["Respond to Webhook"].json.html}}*"
      }
    }
    ```

### **2. Lưu Log & Báo Cáo Định Kỳ**
- **Thêm node `n8n-nodes-base.airtable`** để lưu kết quả vào Airtable/Google Sheets.
- **Ví dụ**:
  - Lưu vào Google Sheets:
    ```json
    {
      "url": "https://sheets.googleapis.com/v4/spreadsheets/{{sheet_id}}/values/{{sheet_name}}",
      "method": "POST",
      "body": {
        "values": [
          ["CV URL", "{{$json.cv_url}}"],
          ["JD URL", "{{$json.jd_url}}"],
          ["ATS Score", "{{$json.score}}"]
        ]
      }
    }
    ```

### **3. Cập Nhật Prompt AI**
- **Chỉnh sửa prompt** trong node `lmChatGroq` để:
  - **Đánh giá kỹ năng mềm** (ví dụ: "leadership", "teamwork").
  - **So sánh với JD cụ thể** (ví dụ: "JD yêu cầu 3-5 năm kinh nghiệm, CV có 12 năm").
  - **Đưa ra gợi ý cụ thể** (ví dụ: "Cần thêm kinh nghiệm mid-market").

### **4. Tích Hợp Với Notion/Confluence**
- **Sử dụng node `n8n-nodes-base.httpRequest`** để tạo **báo cáo trong Notion**.
- **Ví dụ**:
  ```json
  {
    "url": "https://api.notion.com/v1/pages",
    "method": "POST",
    "headers": {
      "Authorization": "Bearer {{$credentials.notion_api_key}}",
      "Notion-Version": "2022-06-28"
    },
    "body": {
      "parent": {
        "database_id": "{{$credentials.notion_db_id}}"
      },
      "properties": {
        "Name": {
          "title": [
            {
              "text": {
                "content": "{{$json.candidate_name}}"
              }
            }
          ]
        },
        "ATS Score": {
          "number": {{$json.score}}
        }
      }
    }
  }
  ```

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp tuyển dụng bằng cách:
✔ **Tự động so sánh CV vs JD** chỉ trong vài giây.
✔ **Phát hiện điểm yếu** (ngôn ngữ, địa điểm, kinh nghiệm).
✔ **Đưa ra báo cáo ATS chi tiết** với gợi ý cải thiện.
✔ **Hoạt động 24/7** mà không cần can thiệp thủ công.

**Hành động ngay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình API keys** (GhostGenius, Groq).
3. **Test với CV/JD mẫu** và **bật Active**.
4. **Tích hợp với Slack/Email/Notion** để tự động hóa hoàn toàn!

**🚀 Cài đặt n8n Self-hosted ngay để bắt đầu tự động hóa tuyển dụng hiệu quả!**