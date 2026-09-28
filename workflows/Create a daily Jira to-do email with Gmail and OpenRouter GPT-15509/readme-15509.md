---
title: "🚀 Tự Động Hóa Email To-Do Hàng Ngày Từ Jira Với Gmail & AI (OpenRouter) – Giảm 90% Công Việc Lặp Lại"
description: "Workflow tự động hóa gửi email danh sách công việc hàng ngày từ Jira, tổng hợp thông tin quan trọng và tạo kế hoạch hành động thông minh bằng AI OpenRouter. Giúp các sếp tiết kiệm 2+ giờ mỗi ngày và bắt đầu ngày làm việc hiệu quả hơn."
slug: "tieu-dong-hoa-email-to-do-tu-jira-voi-gmail-ai"
tags: [n8n, automation, jira, gmail, ai-summarization, openrouter, no-code]
keywords: [tự động hóa jira email, workflow n8n jira gmail, ai tổng hợp công việc hàng ngày, giảm công việc lặp lại, tự động hóa sản xuất phần mềm]
---

# 🚀 **Tự Động Hóa Email To-Do Hàng Ngày Từ Jira Với Gmail & AI (OpenRouter) – Giảm 90% Công Việc Lặp Lại**

### **Nỗi Đau Của Các Sếp**
Mỗi sáng, các sếp phải mất **2-3 giờ** để:
- **Lọc và tổng hợp** công việc từ Jira (issues, sprints, deadlines).
- **Tách biệt** những nhiệm vụ quan trọng từ những thông tin không cần thiết.
- **Tạo kế hoạch hành động** cho ngày làm việc, thường phải viết tay hoặc qua các tool như Notion/Google Docs.
- **Quên hoặc bỏ sót** những công việc cấp thiết khi bắt đầu ngày làm việc.

Kết quả? **Sự tập trung bị gián đoạn**, hiệu suất giảm, và nhiều công việc quan trọng bị bỏ quên.

---
### **🎯 Giải Pháp: Workflow Tự Động Hóa 100% Không Code**
Workflow này **tự động**:
1. **Lấy dữ liệu** từ Jira (issues được gán cho bạn).
2. **Tổng hợp thông tin** bằng AI OpenRouter (mô hình **GPT-120B miễn phí**).
3. **Tạo danh sách To-Do** được sắp xếp theo ưu tiên.
4. **Gửi email tự động** vào mỗi sáng (8h) với kế hoạch chi tiết.

**Kết quả:**
✅ **Tiết kiệm 2-3 giờ/ngày** cho công việc lặp lại.
✅ **Công việc được ưu tiên** tự động, không bỏ sót.
✅ **Kế hoạch cá nhân hóa** dựa trên lối sống làm việc của bạn.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
| **Lợi Ích**               | **Chi Tiết**                                                                 |
|---------------------------|-----------------------------------------------------------------------------|
| **Tiết kiệm thời gian**    | Không cần lọc công việc từ Jira thủ công, AI tự động tổng hợp.             |
| **Công việc ưu tiên tự động** | AI phân loại nhiệm vụ theo mức độ quan trọng và deadline.               |
| **Kế hoạch cá nhân hóa**  | Email To-Do được tạo theo lối sống làm việc riêng của bạn.                |
| **Không bỏ sót công việc** | Workflow chạy tự động hàng ngày, không phụ thuộc vào người dùng.         |
| **Tích hợp AI miễn phí**   | Sử dụng mô hình **GPT-120B của OpenRouter** (không cần trả phí).           |

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| **Dịch Vụ**       | **Thao Tác Cần Thực Hiện**                                                                 | **Link Hướng Dẫn**                                                                 |
|-------------------|-------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| **Jira Cloud**    | Tạo **API Token** để truy cập dữ liệu issues.                                             | [Tạo API Token Jira](https://support.atlassian.com/atlassian-account/docs/manage-api-tokens/) |
| **Gmail**         | Tạo **OAuth 2.0 Credential** cho n8n gửi email.                                          | [Cài đặt OAuth Gmail](https://developers.google.com/gmail/api/quickstart/python)       |
| **OpenRouter**    | Tạo **API Key** để sử dụng mô hình AI.                                                   | [Tạo API Key OpenRouter](https://openrouter.ai/workspaces/default/keys/)             |

### **2. Thông Tin Cấu Hình Jira**
- **URL Jira Cloud** (ví dụ: `https://your-company.atlassian.net`).
- **Email & API Token** của Jira (để lấy dữ liệu issues).

### **3. Thông Tin Email Gmail**
- **Email chính** để nhận email To-Do hàng ngày.
- **OAuth 2.0 Credential** đã cấu hình trong n8n.

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io](https://n8n.io/workflows/15509) (ấn "Export" trên canvas).
2. **Mở n8n Editor** (trang chủ của workflow).
3. **Nhấn "Import"** và chọn file JSON vừa tải.
4. **Chọn "Create new workflow"** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Mở n8n Editor** và tạo workflow mới.
2. **Nhấn "Import"** → Chọn **Paste JSON**.
3. **Dán JSON** từ file workflow (hoặc copy từ [n8n.io](https://n8n.io/workflows/15509)).
4. **Nhấn "Import"**.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **8 node** chính, các sếp cần cấu hình kỹ lưỡng các node sau:

#### **🔹 Node 1: Schedule Trigger (Động cơ kích hoạt hàng ngày)**
- **Cấu hình:**
  - **Schedule:** `0 8 * * *` (chạy lúc 8h00 sáng hàng ngày).
  - **Time Zone:** Chọn **múi giờ của bạn** (ví dụ: `Asia/Ho_Chi_Minh`).
- **Lưu ý:** Nếu muốn chạy ở giờ khác, chỉnh sửa biểu thức cron theo [format này](https://crontab.guru/).

#### **🔹 Node 2: HTTP Request (Lấy dữ liệu từ Jira)**
- **Credentials:** Chọn `jiraSoftwareCloudApi` (đã cấu hình trước).
- **Tham số cần điền:**
  - **Method:** `GET`
  - **URL:** `https://api.atlassian.com/ex/jira/{your-jira-url}/rest/api/3/myissues?maxResults=100`
    *(Thay `{your-jira-url}` bằng URL Jira của bạn, ví dụ: `your-company.atlassian.net`)*
  - **Headers:**
    ```
    Authorization: Bearer {your-jira-api-token}
    ```
- **Lưu ý:**
  - Đảm bảo **API Token Jira** có quyền đọc `My Issues`.
  - Nếu Jira URL có dấu gạch nối (`-`), phải encode URL (ví dụ: `your-company.atlassian.net` → `your-company.atlassian.net`).

#### **🔹 Node 3 & 4: AI Agent + OpenRouter Chat Model (Tổng hợp thông tin)**
- **Credentials:** Chọn `openRouterApi` (đã cấu hình trước).
- **Tham số cần chỉnh:**
  - **Model:** `openai/gpt-oss-120b:free` (mô hình miễn phí).
  - **Prompt (cần chỉnh sửa):**
    ```
    Bạn là một trợ lý ảo chuyên nghiệp giúp tôi tổng hợp công việc hàng ngày từ Jira.
    Dữ liệu đầu vào là danh sách issues từ Jira, bao gồm:
    - Tiêu đề (Summary)
    - Mô tả (Description)
    - Trạng thái (Status)
    - Deadline (Due Date)
    - Người gán (Assignee)

    Yêu cầu:
    1. Lọc bỏ những issue đã hoàn thành (status = "Done") hoặc không liên quan.
    2. Phân loại công việc thành:
       - **Cấp thiết (Urgent):** Deadline trong 24h hoặc status = "Blocked".
       - **Quan trọng (Important):** Deadline trong 3 ngày hoặc status = "In Progress".
       - **Thường xuyên (Routine):** Công việc hàng ngày không deadline.
    3. Tạo danh sách To-Do với:
       - Thứ tự ưu tiên (1-3).
       - Thời gian ước tính hoàn thành (Estimated Time).
       - Ghi chú nếu cần (Notes).
    4. Trả về kết quả dưới dạng JSON:
    {
      "urgent_tasks": [...],
      "important_tasks": [...],
      "routine_tasks": [...],
      "summary": "Tóm tắt công việc ngày hôm nay."
    }
    ```
- **Lưu ý:**
  - **Chỉnh sửa prompt** để phù hợp với cách bạn muốn AI xử lý công việc.
  - Nếu muốn sử dụng mô hình khác, thay đổi `model` trong `keyParameters`.

#### **🔹 Node 5: Edit Fields (Chỉnh sửa dữ liệu trước khi gửi email)**
- **Cấu hình:**
  - **JSON Path:** `$` (sử dụng toàn bộ dữ liệu từ AI).
  - **Transform:** Chỉnh sửa nếu cần (ví dụ: thêm thông tin cá nhân vào email).
- **Lưu ý:** Node này giúp **tái cấu trúc dữ liệu** trước khi gửi email.

#### **🔹 Node 6: Send a Message (Gmail)**
- **Credentials:** Chọn `gmailOAuth2` (đã cấu hình trước).
- **Tham số cần điền:**
  - **To:** Email của bạn (ví dụ: `sếp@example.com`).
  - **Subject:** `📌 To-Do List Hôm Nay - ${currentDate}` (để tự động thêm ngày).
  - **HTML Body:** Sử dụng **template HTML** để email đẹp mắt:
    ```html
    <h1>📌 To-Do List Hôm Nay - {{ $node["Edit Fields"].json["summary"] }}</h1>
    <p><strong>Cấp Thiết (Urgent):</strong></p>
    <ul>
      {% for task in $node["Edit Fields"].json["urgent_tasks"] %}
        <li>
          <strong>{{ task.title }}</strong> -
          <span style="color: red;">🚨 Deadline: {{ task.dueDate }}</span><br>
          <small>Thời gian: {{ task.estimatedTime }} | Ghi chú: {{ task.notes }}</small>
        </li>
      {% endfor %}
    </ul>
    <p><strong>Quan Trọng (Important):</strong></p>
    <ul>
      {% for task in $node["Edit Fields"].json["important_tasks"] %}
        <li>
          <strong>{{ task.title }}</strong> -
          <span style="color: orange;">📅 Deadline: {{ task.dueDate }}</span><br>
          <small>Thời gian: {{ task.estimatedTime }} | Ghi chú: {{ task.notes }}</small>
        </li>
      {% endfor %}
    </ul>
    ```
- **Lưu ý:**
  - **Template HTML** hỗ trợ **loop** (`{% for %}`) và **variable** (`{{ }}`).
  - Nếu email không hiển thị đúng, kiểm tra **syntax HTML** và **dữ liệu JSON** từ AI.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** và kiểm tra:
     - Dữ liệu Jira được lấy đúng không?
     - AI tổng hợp thông tin có logic không?
     - Email được gửi đúng không?
2. **Bật Active Workflow**:
   - Sau khi kiểm tra thành công, **bật toggle Active** trên canvas.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Tích Hợp Slack/Telegram**
- **Thêm node Slack/Telegram** sau node `Edit Fields` để **báo động công việc cấp thiết** ngay khi có.
- **Cấu hình:**
  - **Slack:** Sử dụng node `n8n-nodes-slack`.
  - **Telegram:** Sử dụng node `n8n-nodes-telegram`.
- **Ví dụ:**
  ```plaintext
  "urgent_tasks": [
    {
      "title": "Fix critical bug",
      "dueDate": "2024-05-20",
      "message": "⚠️ Bug nghiêm trọng cần fix ngay! Deadline: 20/5."
    }
  ]
  ```
  → AI sẽ tự động gửi tin nhắn Slack/Telegram khi có công việc cấp thiết.

### **2. Lưu Log & Báo Cáo Định Kỳ**
- **Thêm node `n8n-nodes-base.stickyNote`** để lưu **lịch sử công việc** hàng ngày.
- **Cấu hình:**
  - **Sticky Note:** Tạo một **sticky note** mới mỗi ngày với nội dung:
    ```
    Ngày: {{ $node["Schedule Trigger"].json["date"] }}
    Công việc hoàn thành: {{ completedTasks }}
    Công việc còn lại: {{ remainingTasks }}
    ```
- **Kết hợp với Google Sheets/Notion** để **báo cáo tuần/Tháng**.

### **3. Cập Nhật Prompt AI**
- **Nếu AI không phân loại công việc chính xác**, chỉnh sửa **prompt** trong node `OpenRouter Chat Model`:
  ```plaintext
  "Yêu cầu AI phân loại công việc theo tiêu chí mới:
  - Nếu công việc liên quan đến sprint X, ưu tiên cao hơn.
  - Nếu công việc có từ khóa 'urgent' trong mô tả, luôn xếp vào cấp thiết."
  ```
- **Test lại** với dữ liệu mẫu trước khi áp dụng.

### **4. Sử Dụng Mô Hình AI Khác**
- **Thay đổi mô hình** trong `keyParameters`:
  ```json
  "model": "mistralai/mixtral-8x7b:free"
  ```
  *(Lưu ý: Một số mô hình miễn phí có giới hạn request/ngày.)