---
title: "🚀 Tự Động Hóa Phân Loại & Gửi Lỗi GitHub Sang Airtable, Notion & Slack Bằng GPT-4o (Miễn Code)"
description: "Workflow tự động phát hiện và phân loại lỗi GitHub bằng trí tuệ nhân tạo GPT-4o, sau đó tự động gửi kết quả phân loại đến Airtable, Notion và Slack với phân công đội ngũ phù hợp. Giúp các sếp tiết kiệm thời gian xử lý lỗi lên đến 90% và cải thiện hiệu suất phát triển phần mềm."
slug: "tieu-dong-hoa-phan-loai-loi-github-bang-gpt-4o"
tags: [n8n, automation, ai-agent, github, airtable, notion, slack, error-management, no-code]
keywords: [tự động hóa lỗi github, phân loại lỗi bằng ai, n8n workflow github, airtable tự động hóa, notion tự động hóa, slack alert lỗi phần mềm, gpt-4o tự động hóa]
---

# 🚀 **Tự Động Hóa Phân Loại Lỗi GitHub Bằng GPT-4o & Phân Công Cho Đội Ngũ**

## **🔍 Nỗi Đau Của Các Sếp Phát Triển Phần Mềm**
Hàng ngày, các sếp và đội ngũ kỹ thuật phải:
- **Tìm kiếm thủ công** lỗi trong các issue GitHub được nhãn "bug" hoặc "error".
- **Phân loại lỗi** theo loại (API, Backend, DevOps, Support) và mức độ nghiêm trọng.
- **Gửi thông báo** cho đội ngũ liên quan thông qua Slack/email.
- **Ghi chép lại** lỗi vào Airtable/Notion để theo dõi và phân tích sau này.

**Kết quả?** Thời gian và năng suất bị "chôn vùi" trong công việc thủ công, trong khi lỗi nghiêm trọng có thể bị bỏ qua.

---
## **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** phân loại và phân công lỗi.
- **Chính xác cao** với phân loại tự động bằng GPT-4o.
- **Phân công tự động** cho đội ngũ DevOps, Backend, API hoặc Support.
- **Ghi chép tự động** vào Airtable và Notion với thông tin chi tiết.
- **Thông báo Slack** kịp thời cho đội ngũ hành động nhanh chóng.
- **Hỗ trợ AI** đề xuất giải pháp và FAQ liên quan.
:::

---
## **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
- **Tài khoản GitHub** (đã cấp quyền OAuth2 cho n8n).
- **API Key OpenAI** (để sử dụng GPT-4o).
- **Tài khoản Airtable** (đã tạo bảng dữ liệu với các trường: `Error Code`, `Category`, `Severity`, `Suggested Action`, `Repo`, `Issue Link`).
- **Tài khoản Notion** (đã chọn database phù hợp để ghi chép lỗi).
- **Tài khoản Slack** (đã cấp quyền API và chọn channel thông báo).
- **VPS tự host n8n** (để workflow hoạt động 24/7).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/10335](https://n8n.io/workflows/10335) hoặc copy/paste JSON vào **n8n Editor**.
- **Nếu import từ file**:
  - Mở n8n Editor → Nhấn `Import` → Chọn file JSON → Nhấn `Import`.
- **Nếu copy/paste**:
  - Mở n8n Editor → Nhấn `Create new workflow` → Chọn `Import from JSON` → Dán JSON → Nhấn `Import`.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **22 node** và cần cấu hình chi tiết như sau:

#### **🔹 Node 1: GitHub Issue Trigger**
- **Cấu hình**:
  - Chọn **GitHub OAuth2** (đã cấu hình trước trong `Credentials`).
  - Chọn **repository** cần theo dõi.
  - **Lọc issue** theo nhãn: `bug` hoặc `error`.
  - **Output**: Dữ liệu được chuẩn bị thành JSON (title, body, repo, timestamp).

#### **🔹 Node 2-5: AI Classification (GPT-4o)**
- **Cấu hình**:
  - **LLM Model: GPT-4o**:
    - Chọn **OpenAI API** (đã cấu hình trong `Credentials`).
    - Đặt `model` thành `gpt-4o` (hoặc `gpt-4o-mini`).
    - **Prompt mẫu** (cần chỉnh sửa để phù hợp):
      ```json
      "Analyze the GitHub issue below and classify it into:
      - Category: API, Backend, DevOps, Support
      - Severity: Critical, High, Medium, Low
      - Root Cause: [AI tự phân tích]
      - Suggested Fix: [AI đề xuất giải pháp]
      - FAQ Match: [Nếu có, trích dẫn FAQ liên quan]
      Format response as structured JSON."
      ```
  - **Output Parser: Structured JSON Schema**:
    - Chọn **schema** phù hợp với output từ GPT-4o (ví dụ: `{"category": "...", "severity": "...", ...}`).

#### **🔹 Node 6-7: AI Memory Buffer & Parse Output**
- **Cấu hình**:
  - **AI Memory Buffer**: Giúp lưu trữ lịch sử phân loại (nếu cần).
  - **Parse AI Classification Output**:
    - Sử dụng **Code Node** để chuyển đổi output JSON thành dạng dễ sử dụng cho các node tiếp theo.

#### **🔹 Node 8: Check Valid AI Response**
- **Cấu hình**:
  - Nếu AI trả về kết quả không hợp lệ (trống hoặc lỗi), workflow sẽ **bỏ qua** và chuyển sang **Error Handler**.

#### **🔹 Node 9: Route by Assigned Team (Switch)**
- **Cấu hình**:
  - **Điều kiện phân công**:
    - `Category = "API"` → Chuyển đến **Airtable/Notion/Slack API Team**.
    - `Category = "Backend"` → Chuyển đến **Airtable/Notion/Slack Backend Team**.
    - `Category = "DevOps"` → Chuyển đến **Airtable/Notion/Slack DevOps Team**.
    - `Category = "Support"` → Chuyển đến **Airtable/Notion/Slack Support Team**.

#### **🔹 Node 10-19: Airtable & Notion Logging**
- **Cấu hình chung**:
  - **Airtable**:
    - Chọn **Airtable Token API** (đã cấu hình).
    - **Operation**: `create`.
    - **Fields cần điền**:
      - `Error Code`: `{{$node["AI: Classify API Error (GPT-4o)"].json()["error_code"]}}`
      - `Category`: `{{$node["AI: Classify API Error (GPT-4o)"].json()["category"]}}`
      - `Severity`: `{{$node["AI: Classify API Error (GPT-4o)"].json()["severity"]}}`
      - `Suggested Action`: `{{$node["AI: Classify API Error (GPT-4o)"].json()["suggested_action"]}}`
      - `Repo`: `{{$node["GitHub Issue Created/Updated"].json()["repository"]["full_name"]}}`
      - `Issue Link`: `{{$node["GitHub Issue Created/Updated"].json()["html_url"]}}`
  - **Notion**:
    - Chọn **Notion API** (đã cấu hình).
    - **Database**: Chọn database phù hợp (ví dụ: `Error Tracking`).
    - **Properties**:
      - `Status`: `{{$node["AI: Classify API Error (GPT-4o)"].json()["severity"]}}`
      - `Category`: `{{$node["AI: Classify API Error (GPT-4o)"].json()["category"]}}`
      - `Description`: `{{$node["GitHub Issue Created/Updated"].json()["body"]}}`
      - `Link`: `{{$node["GitHub Issue Created/Updated"].json()["html_url"]}}`

#### **🔹 Node 20-21: Slack Notify (Team-Specific)**
- **Cấu hình**:
  - **Slack API**: Chọn **Slack Webhook URL** (đã cấu hình).
  - **Message mẫu** (cần chỉnh sửa):
    ```json
    {
      "text": "🚨 **New Error Alert** 🚨",
      "attachments": [
        {
          "title": "{{$node["AI: Classify API Error (GPT-4o)"].json()["category"]}} Error",
          "title_link": "{{$node["GitHub Issue Created/Updated"].json()["html_url"]}}",
          "text": `Severity: **{{$node["AI: Classify API Error (GPT-4o)"].json()["severity"]}}**\nRoot Cause: **{{$node["AI: Classify API Error (GPT-4o)"].json()["root_cause"]}}**\nSuggested Fix: **{{$node["AI: Classify API Error (GPT-4o)"].json()["suggested_action"]}}**`,
          "color": "{{$node["AI: Classify API Error (GPT-4o)"].json()["severity"] === 'Critical' ? '#FF0000' : '#FFCC00'}}"
        }
      ]
    }
    ```

#### **🔹 Node 22: Error Handler**
- **Cấu hình**:
  - Nếu workflow gặp lỗi, **Slack Notify: Send Error Alert** sẽ gửi thông báo bao gồm:
    - **Node bị lỗi**.
    - **Lỗi cụ thể**.
    - **Thời gian xảy ra**.

---

### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Tạo một **issue mới** trên GitHub với nhãn `bug` hoặc `error`.
  - Chạy **Test Run** trong n8n Editor để kiểm tra workflow.
- **Bật Active**:
  - Sau khi kiểm tra thành công, **bật Active** để workflow hoạt động tự động.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH LÀM THÊM ĐỂ TĂNG CƠ HỘI]
- **Kết hợp với Jira**: Sử dụng **n8n Jira Node** để tự động tạo ticket từ lỗi GitHub.
- **Báo cáo định kỳ**: Sử dụng **n8n Email Node** để gửi báo cáo lỗi hàng tuần cho quản lý.
- **Tích hợp với PagerDuty**: Nếu lỗi **Critical**, workflow có thể gửi cảnh báo đến PagerDuty.
- **Lưu log chi tiết**: Sử dụng **n8n StickyNote Node** để lưu trữ log của mỗi lỗi.
- **Tự động đóng issue**: Sau khi xử lý xong, workflow có thể **close issue** trên GitHub.
- **Phân tích trend lỗi**: Sử dụng **n8n Google Sheets Node** để vẽ biểu đồ phân tích lỗi theo thời gian.
:::

---

## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp và đội ngũ kỹ thuật khỏi công việc thủ công phân loại lỗi. Với **GPT-4o**, lỗi được phân loại chính xác và **phân công tự động** cho đội ngũ phù hợp. **Airtable và Notion** giúp theo dõi lịch sử, trong khi **Slack** đảm bảo thông báo kịp thời.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (để workflow hoạt động 24/7).
2. **Cấu hình các API Key** (GitHub, OpenAI, Airtable, Notion, Slack).
3. **Import workflow** và **test run** với issue mẫu.
4. **Bật Active** và **theo dõi lỗi tự động**!

**🚀 Cải thiện hiệu suất phát triển phần mềm chỉ với một workflow!** 🚀