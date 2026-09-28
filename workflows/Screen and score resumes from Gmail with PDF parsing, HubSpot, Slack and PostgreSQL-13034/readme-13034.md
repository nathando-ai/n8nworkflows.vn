---
title: "🚀 Tự Động Hóa Xử Lý & Đánh Giá CV từ Gmail: AI + PDF + HubSpot + Slack + PostgreSQL (Miễn Code)"
description: "Workflow tự động hóa 100% không cần code để nhận, phân tích, đánh giá và quản lý ứng viên từ email Gmail, tự động đồng bộ vào HubSpot, Slack và PostgreSQL. Giúp tiết kiệm 10+ giờ/ngày cho bộ phận HR, giảm thiểu sai sót và tối ưu hóa quy trình tuyển dụng."
slug: "tự-dộng-hoa-xu-ly-danh-gia-cv-tu-gmail"
tags: [n8n, automation, hr, ai-summarization, hubspot, slack, postgresql, pdf-parsing, no-code]
keywords: [tự động hóa tuyển dụng, n8n workflow cv, phân tích cv bằng ai, hubspot automation, slack alert tuyển dụng, postgresql analytics]
---

# 🚀 **Tự Động Hóa Xử Lý CV từ Gmail: AI + PDF + HubSpot + Slack + PostgreSQL (Miễn Code)**

### **🔍 Nỗi Đau Của Các Sếp HR**
Bộ phận HR phải mất **giờ đồng hồ** mỗi ngày để:
- **Lọc và tải xuống** hàng trăm CV từ Gmail.
- **Phân tích thủ công** thông tin trong PDF, Excel hay Word.
- **Đánh giá và xếp hạng** ứng viên dựa trên kinh nghiệm, kỹ năng và phù hợp với vị trí.
- **Ghi chép vào CRM** (HubSpot, Salesforce...) và gửi phản hồi cá nhân hóa cho ứng viên bị loại.
- **Lưu trữ và theo dõi** quá trình tuyển dụng trong cơ sở dữ liệu.

**Kết quả?** Thời gian tuyển dụng kéo dài, chất lượng ứng viên bị bỏ lỡ, và HR phải làm việc **24/7** để không bỏ lỡ bất kỳ một CV nào.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✅ **Tiết kiệm 10+ giờ/ngày** cho việc xử lý CV thủ công.
✅ **Đánh giá chính xác** ứng viên với **AI + NLP**, giảm thiểu sai sót con người.
✅ **Tự động đồng bộ** thông tin ứng viên vào **HubSpot CRM** và **Slack** để theo dõi.
✅ **Lưu trữ CV** vào **Google Drive** (theo folder "Qualified" và "Rejected").
✅ **Nhận báo cáo analytics** từ **PostgreSQL** về hiệu suất tuyển dụng.
✅ **Gửi phản hồi cá nhân hóa** tự động cho ứng viên bị loại, cải thiện trải nghiệm ứng viên.

---
### **🔧 Yêu Cầu Cần Thiết**
Để workflow này hoạt động, các sếp cần chuẩn bị:
📌 **Tài Khoản & API Keys:**
- **Gmail OAuth 2.0** (để lấy email và gửi phản hồi).
- **HubSpot App Token** (để tạo contact trong CRM).
- **Google Drive OAuth 2.0** (để lưu trữ CV).
- **PostgreSQL** (để lưu log và analytics).
- **Slack Webhook** (để gửi cảnh báo về ứng viên phù hợp).
- **API Key cho `htmlcsstopdf`** (để chuyển đổi PDF thành text).

📌 **Cấu Trúc Cơ Sở Dữ Liệu:**
- **Google Drive:** Tạo 2 folder:
  - `Qualified` (để CV của ứng viên phù hợp).
  - `Rejected` (để CV của ứng viên không phù hợp).
- **PostgreSQL:** Tạo bảng `candidate_applications` với các cột:
  ```sql
  CREATE TABLE candidate_applications (
      id SERIAL PRIMARY KEY,
      email VARCHAR(255),
      qualification_score INT,
      skill_match_percentage INT,
      tier VARCHAR(50),
      status VARCHAR(50),
      created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
  );
  ```

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13034](https://n8n.io/workflows/13034) hoặc copy/paste JSON vào **n8n Editor**.
- **Nhấn "Import"** và chọn **Self-hosted** (nếu tự cài đặt trên VPS).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này được chia thành **4 Phase** chính. Dưới đây là hướng dẫn chi tiết cho từng phần quan trọng:

##### **📧 PHASE 1: Nhận & Kiểm Tra CV (Gmail Trigger + PDF Validation)**
- **Node `Gmail Trigger`:**
  - Chọn **credentials** là `gmailOAuth2`.
  - **Tham số cần thiết:**
    - `Label`: `resume_submissions` (để chỉ định folder email nhận CV).
    - `Subject contains`: `CV` hoặc `Application` (tùy chỉnh theo tiêu đề email).
- **Node `IF: Valid PDF Attachment?`:**
  - Kiểm tra xem email có **đính kèm file PDF** không.
  - Nếu **không có PDF**, workflow sẽ **bỏ qua** và không thực hiện bước tiếp theo.

##### **🧠 PHASE 2: Phân Tích CV Bằng AI (PDF → Text → Scoring)**
- **Node `PDF to Text: Extract Content`:**
  - Sử dụng **API `htmlcsstopdf`** để chuyển đổi PDF thành **JSON**.
  - **Tham số cần thiết:**
    - `operation`: `parsePdfToJson`.
    - `resource`: `pdfManipulation`.
    - **Credentials**: `htmlcsstopdfApi` (cần đăng ký API từ [htmlcsstopdf.com](https://htmlcsstopdf.com/)).
- **Node `Code: AI Resume Parser`:**
  - **Mã JavaScript** trong node này sẽ:
    - **Trích xuất** thông tin như **tên, email, số điện thoại, kinh nghiệm, kỹ năng, giáo dục**.
    - **Áp dụng NLP** để đánh giá phù hợp với vị trí tuyển dụng.
    - **Đánh giá điểm** (từ 0-100) và **xếp hạng** (A+, A, B, C, D).
  - **Lưu ý:** Các sếp có thể **tùy chỉnh mã** để phù hợp với tiêu chí tuyển dụng của công ty.

##### **🎯 PHASE 3: Xếp Hạng & Đồng Bộ Hóa (HubSpot + Slack + Google Drive)**
- **Node `IF: Qualified Candidate?`:**
  - **Điều kiện:** Nếu `qualification_score >= 70`, workflow sẽ **chuyển sang đường dẫn "Qualified"**.
  - Nếu `< 70`, sẽ **chuyển sang đường dẫn "Rejected"**.
- **Đường dẫn "Qualified":**
  - **HubSpot: Create Contact:**
    - **Credentials**: `hubspotAppToken`.
    - **Tham số cần thiết:**
      - `properties`: Điền thông tin từ CV (tên, email, số điện thoại, kinh nghiệm, kỹ năng).
  - **Slack: Qualified Alert:**
    - **Webhook URL**: Đăng ký từ Slack (Settings > Apps > Custom Integrations > Incoming Webhooks).
    - **Thông báo mẫu:**
      ```json
      {
        "text": "🚀 New Qualified Candidate: <@UXXXXXX> - Score: {{ $node["Code: AI Resume Parser"].json()["qualification_score"] }}",
        "attachments": [
          {
            "title": "{{ $node["Code: AI Resume Parser"].json()["name"] }}",
            "title_link": "https://drive.google.com/file/d/{{ $node["Google Drive: Archive Qualified"].json()["id"] }}",
            "text": "Skills: {{ $node["Code: AI Resume Parser"].json()["skills"] }}"
          }
        ]
      }
      ```
  - **Google Drive: Archive Qualified:**
    - **Folder ID**: Điền ID của folder `Qualified` (lấy từ liên kết Google Drive).
    - **File Name**: `{{ $node["Code: AI Resume Parser"].json()["name"] }}_CV.pdf`.
- **Đường dẫn "Rejected":**
  - **Gmail: Send Rejection:**
    - **Credentials**: `gmailOAuth2`.
    - **Thông báo mẫu:**
      ```html
      <p>Chúng tôi đã xem xét CV của bạn và rất tiếc phải thông báo rằng bạn không phù hợp với vị trí này.</p>
      <p><strong>Điểm của bạn:</strong> {{ $node["Code: AI Resume Parser"].json()["qualification_score"] }}/100</p>
      <p><strong>Lý do:</strong> {{ $node["Code: AI Resume Parser"].json()["rejection_reason"] }}</p>
      <p>Chúng tôi mong bạn sẽ tiếp tục nỗ lực và chúc bạn may mắn trong tương lai!</p>
      ```
  - **Slack: Rejection Log:**
    - Gửi thông báo về Slack với nội dung:
      ```json
      {
        "text": "❌ Rejected Candidate: <@UXXXXXX> - Score: {{ $node["Code: AI Resume Parser"].json()["qualification_score"] }}",
        "attachments": [
          {
            "title": "{{ $node["Code: AI Resume Parser"].json()["name"] }}",
            "text": "Reason: {{ $node["Code: AI Resume Parser"].json()["rejection_reason"] }}"
          }
        ]
      }
      ```
  - **Google Drive: Archive Rejected:**
    - **Folder ID**: Điền ID của folder `Rejected`.
    - **File Name**: `{{ $node["Code: AI Resume Parser"].json()["name"] }}_CV_rejected.pdf`.

##### **📊 PHASE 4: Analytics & Feedback Loop (PostgreSQL)**
- **Node `Code: Analytics Calculator`:**
  - **Mã JavaScript** sẽ tính toán các **metrics** như:
    - `Funnel Conversion Rate` (tỷ lệ ứng viên phù hợp vs tổng CV nhận được).
    - `Average Qualification Score`.
    - `Time to Hire`.
  - **Lưu ý:** Các sếp có thể **tùy chỉnh** để phù hợp với báo cáo nội bộ.
- **Node `PostgreSQL: Store Analytics`:**
  - **Query SQL mẫu:**
    ```sql
    INSERT INTO hiring_funnel_metrics (
        date,
        total_applications,
        qualified_applications,
        average_score,
        conversion_rate,
        time_to_hire_days
    ) VALUES (
        CURRENT_DATE,
        {{ $node["Merge: Qualified Path"].json()["total_applications"] }},
        {{ $node["Merge: Qualified Path"].json()["qualified_applications"] }},
        {{ $node["Code: Analytics Calculator"].json()["average_score"] }},
        {{ $node["Code: Analytics Calculator"].json()["conversion_rate"] }},
        {{ $node["Code: Analytics Calculator"].json()["time_to_hire"] }}
    );
    ```

#### **3. Kích Hoạt ⚡️**
- **Test Run:**
  - Gửi một email mẫu với **CV PDF** vào folder `resume_submissions` trên Gmail.
  - Kiểm tra **Slack** và **HubSpot** để xác nhận workflow hoạt động.
- **Bật Active:**
  - Nhấn **"Active"** trên n8n Editor.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối với Zoom/Teams:**
   - Sử dụng **node `zoom`** để tự động tạo cuộc gọi phỏng vấn với ứng viên phù hợp.
2. **Gửi Báo Cáo Hàng Tuần:**
   - Sử dụng **node `email`** để gửi báo cáo analytics cho CEO/HR Manager.
3. **Tích Hợp với AI Chatbot (Replicate/Perplexity):**
   - Sử dụng **node `code`** để gọi API AI để **tóm tắt CV** và **gợi ý phỏng vấn**.
4. **Lưu Log Chi Tiết:**
   - Sử dụng **node `postgres`** để lưu **tất cả log** của workflow để phân tích sau này.
5. **Tự Động Xóa Email Sau Xử Lý:**
   - Sử dụng **node `gmail`** với **operation: `delete`** để xóa email sau khi xử lý.

---
### **📌 Kết Luận**
Workflow này **giải phóng HR khỏi công việc lặp lại**, giúp **tuyển dụng nhanh chóng và chính xác hơn** nhờ **AI + Automation**. Các sếp không cần **viết code**, chỉ cần **cấu hình và chạy** là có thể tự động hóa **tất cả quy trình tuyển dụng** từ nhận CV đến đánh giá và đồng bộ hóa.

**🚀 Hãy áp dụng ngay và tiết kiệm thời gian cho bộ phận HR của mình!**

---
**🔗 Link Workflow gốc:** [n8n.io/workflows/13034](https://n8n.io/workflows/13034)
**📌 Cần hỗ trợ?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để chạy workflow 24/7!