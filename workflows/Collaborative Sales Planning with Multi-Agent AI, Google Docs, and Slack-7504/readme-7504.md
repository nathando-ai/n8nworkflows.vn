---
title: "🚀 **Tự Động Hóa Kế Hoạch Bán Hàng Nhóm Lực Lượng AI + Google Docs + Slack (Multi-Agent Collaboration)**"
description: "Workflow tự động hóa hoàn toàn không cần code giúp các sếp **tạo kế hoạch bán hàng chi tiết** từ nhiều góc nhìn (Marketing, Operations, Finance) bằng AI, xuất ra PDF và chia sẻ ngay Slack. Giảm thời gian lên đến 80% so với làm thủ công!"
slug: "tieu-dong-hoa-ke-hoach-ban-hang-multi-agent"
tags: [n8n, automation, no-code, ai-multi-agent, google-docs, slack-integration, sales-planning]
keywords: [n8n workflow tự động hóa, kế hoạch bán hàng AI, multi-agent collaboration, Google Docs PDF, Slack tự động, tự động hóa doanh nghiệp nhỏ]
---

# **🚀 Tự Động Hóa Kế Hoạch Bán Hàng Nhóm Lực Lượng AI: Từ Nhóm Nhận Diện → PDF Chia Sẻ Slack**

## **🔥 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hàng tuần, các sếp phải:
- **Tập hợp ý kiến** từ Marketing, Operations và Finance để xây dựng kế hoạch bán hàng.
- **Làm việc song song** giữa các bộ phận, dẫn đến trùng lặp, thiếu đồng bộ và mất thời gian.
- **Chuyển đổi từ văn bản thô** sang tài liệu chuyên nghiệp (PDF) để chia sẻ với ban lãnh đạo.
- **Quên hoặc bỏ sót** một số chi tiết quan trọng (như ngân sách, rủi ro vận hành, hoặc chiến dịch marketing).

**Kết quả?** Kế hoạch bán hàng **chậm, không đồng bộ, và dễ sai sót** – ảnh hưởng trực tiếp đến doanh thu.

---
## **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✅ **Tiết kiệm 80% thời gian** so với làm thủ công (từ 5-7 tiếng/tháng xuống còn 1-2 tiếng).
✅ **Kế hoạch bán hàng đồng bộ** giữa Marketing, Operations và Finance, **không trùng lặp**.
✅ **Tài liệu chuyên nghiệp** (PDF) được tự động tạo và chia sẻ ngay Slack, **không cần chỉnh sửa thủ công**.
✅ **AI tự động giải quyết xung đột** (ví dụ: ngân sách Marketing vs. ngân sách Operations).
✅ **Dễ dàng cập nhật** cho các kế hoạch bán hàng định kỳ (hàng tuần, tháng).

---
## **🔧 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
📌 **Tài khoản và API Keys:**
- **OpenAI API Key** (hoặc LLM khác như Mistral, Anthropic) để sử dụng AI.
- **Google Drive API Key** (để tạo và xuất PDF từ Google Docs).
- **Slack OAuth Token** (để chia sẻ file PDF).

📌 **Dịch vụ cần kết nối:**
- **n8n Self-hosted** (để chạy workflow 24/7).
- **Google Workspace** (để tạo và xuất tài liệu).
- **Slack Workspace** (để chia sẻ kết quả).

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7504](https://n8n.io/workflows/7504).
- **Mở n8n Editor** → Nhấn **"Import"** → Chọn file JSON vừa tải.
- **Hoặc copy/paste** JSON từ file vào Editor và nhấn **"Create Workflow"**.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
#### **🔹 Node "Edit Fields" (Nhập Thông Tin Khởi Đầu)**
- **Cấu hình form** với các trường bắt buộc:
  - `company` (Tên công ty)
  - `products` (Sản phẩm/dịch vụ)
  - `audience` (Đối tượng mục tiêu)
  - `start_date` & `end_date` (Khoảng thời gian kế hoạch)
  - `channels` (Các kênh marketing: email, social, search...)
  - `constraints` (Ràng buộc: ngân sách, hàng tồn kho, quy định pháp lý)
  - `metrics` (Chỉ tiêu đo lường: doanh thu, ROI, CAC)

#### **🔹 Node "CEO Agent" (Orchestrator - AI Quản Lý)**
- **Cấu hình system prompt** để AI:
  - **Đọc brief** từ các trường nhập trên.
  - **Gọi 3 bộ phận (Marketing, Operations, Finance) một lần duy nhất**.
  - **Gộp kết quả** và giải quyết xung đột (ví dụ: ngân sách Marketing vs. ngân sách Operations).
  - **Xuất ra 2 định dạng**:
    - **Markdown** (dễ đọc cho con người).
    - **JSON** (dễ tự động hóa cho hệ thống).

**Mẫu system prompt cho CEO Agent:**
```plaintext
Bạn là CEO của công ty [{{ $json.company }}]. Hãy phân tích brief sau và yêu cầu 3 bộ phận (Marketing, Operations, Finance) trả lời từng nhiệm vụ riêng biệt.

**Yêu cầu:**
1. Gọi Marketing Agent để đề xuất chiến dịch marketing (các kênh, nội dung, KPI).
2. Gọi Operations Agent để lên kế hoạch vận hành (hàng tồn kho, nhân sự, rủi ro).
3. Gọi Finance Agent để phân bổ ngân sách và đặt mục tiêu tài chính.

**Format trả về:**
- `plan_md`: Kế hoạch bán hàng dưới dạng Markdown (các phần: Tóm tắt, Thời gian biểu, Marketing, Vận hành, Giá cả, Rủi ro, Hành động tiếp theo).
- `plan_json`: Dữ liệu máy tính hóa (JSON) để tự động hóa (chiến dịch, ngân sách, ngày tháng, hành động).
```

#### **🔹 Node "Marketing Agent", "Operations Agent", "Finance Agent"**
Mỗi bộ phận cần **system prompt riêng** để trả về JSON chuẩn:
- **Marketing Agent:**
  ```json
  {
    "campaigns": [{"name": "", "channel": "", "message": "", "kpi": ""}],
    "content_calendar": [{"date": "YYYY-MM-DD", "channel": "", "asset": "", "cta": ""}],
    "notes": ""
  }
  ```
- **Operations Agent:**
  ```json
  {
    "inventory_note": "",
    "staffing_plan": [{"team": "", "need": "", "when": ""}],
    "fulfillment_steps": [{"step": "", "owner": "", "due": ""}],
    "operational_risks": [{"risk": "", "mitigation": ""}]
  }
  ```
- **Finance Agent:**
  ```json
  {
    "discounts": [{"product": "", "type": "%|fixed", "value": 0, "notes": ""}],
    "budget_split": {"marketing": 0, "ops": 0, "contingency": 0},
    "targets": {"revenue": 0, "roi": 0, "gross_margin_pct": 0},
    "notes": ""
  }
  ```

#### **🔹 Node "Create document file" (Tạo Google Docs)**
- **Chọn Google Drive OAuth2 API** và cấu hình:
  - **File Name:** `{{ $json.plan_json.company }} — Sales Season Plan ({{ $json.plan_json.window.start }} → {{ $json.plan_json.window.end }})`
  - **Content:** Dữ liệu Markdown từ `plan_md` (được chuyển từ Markdown → HTML).

#### **🔹 Node "Convert to PDF" (Xuất PDF)**
- **Chọn Google Drive** và thực hiện **download file** để chuyển từ Google Docs sang PDF.

#### **🔹 Node "Upload a file" (Chia Sẻ Slack)**
- **Cấu hình Slack OAuth2 API** và gửi tin nhắn kèm file PDF:
  ```plaintext
  📄 Kế Hoạch Bán Hàng Đã Sẵn Sàng
  Công Ty: {{ $json.plan_json.company }}
  Khoảng Thời Gian: {{ $json.plan_json.window.start }} → {{ $json.plan_json.window.end }}
  File PDF đã được đính kèm. Vui lòng xem xét và để lại bình luận.
  ```

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Bước Xác Nhận (Approval Step):**
   - Sử dụng **Slack "Send & Wait"** trước khi xuất PDF để ban lãnh đạo có thể **đánh giá và chỉnh sửa** trước khi hoàn tất.

2. **Kết Nối với CRM/PM Tool:**
   - **Tự động đẩy hành động tiếp theo** (`next_actions`) vào Jira, Asana, hoặc Trello.

3. **Tự Động Hóa Định Kỳ:**
   - Thay **Manual Trigger** bằng **Cron Trigger** để chạy tự động hàng tuần/tháng.

4. **Dữ Liệu Địa Phương (RAG - Retrieval-Augmented Generation):**
   - Kết nối với **Google Sheets, Notion, hoặc cơ sở dữ liệu** để AI **trích xuất thông tin thực tế** (ví dụ: lịch sử doanh số, sản phẩm hiện có).

5. **Chia Sẻ Trên Google Drive thay Slack:**
   - Thay vì Slack, **tự động lưu PDF vào Google Drive** với tên file tự động.

6. **Hỗ Trợ Nhiều Ngôn Ngữ:**
   - Thêm **Agent Dịch Ngữ** để chuyển kế hoạch sang tiếng Anh, Trung Quốc, hoặc tiếng Nhật.

7. **Giới Hạn Chi Phí (Cost Guardrails):**
   - **Limit số token** để tránh chi phí OpenAI quá cao.
   - **Kiểm tra ngân sách** trước khi AI đề xuất chiến dịch.

---
## **📌 Kết Luận**
Workflow này **giải quyết hoàn toàn tự động hóa** quá trình xây dựng kế hoạch bán hàng từ nhiều góc nhìn, **giảm thời gian và tăng độ chính xác**. Các sếp không cần viết code, chỉ cần **cấu hình các system prompt** và kết nối API là có thể **tạo kế hoạch chuyên nghiệp** chỉ trong vài phút.

**👉 Hãy thử ngay và tiết kiệm thời gian cho đội ngũ của mình!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**📌 Lưu ý cuối cùng:**
- Nếu gặp lỗi, **kiểm tra lại API Key** và **cấu hình Google Drive/Slack**.
- **Test run** với dữ liệu mẫu trước khi bật **Active Workflow**.
- **Cập nhật system prompt** nếu AI trả về kết quả không phù hợp.