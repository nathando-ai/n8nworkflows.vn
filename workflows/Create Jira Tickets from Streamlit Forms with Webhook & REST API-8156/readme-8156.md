---
title: "🚀 Tự Động Hóa Tạo Tickets Jira Từ Form Streamlit - Không Cần Code!"
description: "Giải pháp hoàn toàn tự động hóa việc chuyển đổi dữ liệu từ form Streamlit sang Jira thông qua Webhook và REST API, tiết kiệm thời gian và giảm thiểu lỗi nhân sự. Workflow này giúp các sếp quản lý dự án tự động hóa việc tạo ticket Jira từ ứng dụng Streamlit, đảm bảo tính chính xác và hoạt động liên tục 24/7."
slug: "tu-dong-hoa-tao-tickets-jira-tu-streamlit"
tags: [n8n, automation, project-management, jira, streamlit, no-code]
keywords: [n8n workflow jira, tự động hóa jira, streamlit và jira, tạo ticket jira tự động, webhook jira, api jira]
---

# 🚀 Tự Động Hóa Tạo Tickets Jira Từ Form Streamlit - Không Cần Code!

## 📌 **Nỗi Đau Của Các Sếp Quản Lý Dự Án**
Hàng ngày, các sếp và đội ngũ quản lý dự án phải mất thời gian thủ công để:
- Nhập thông tin ticket từ các form Streamlit vào Jira.
- Lo lắng về việc trùng lặp ticket hoặc thiếu thông tin quan trọng.
- Đảm bảo tính nhất quán và chính xác của dữ liệu giữa các hệ thống.

**Giải pháp?** Một workflow tự động hóa hoàn toàn với **n8n** sẽ giúp bạn:
- **Tạo ticket Jira tự động** từ form Streamlit chỉ với một cú nhấp chuột.
- **Tránh trùng lặp** và đảm bảo tính hợp lệ của dữ liệu.
- **Tiết kiệm thời gian** lên đến **90%** trong việc quản lý ticket.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian** lên đến 90% trong việc tạo ticket Jira thủ công.
- **Tránh trùng lặp ticket** nhờ cơ chế kiểm tra duy nhất.
- **Tính chính xác cao** với dữ liệu được chuyển đổi và chuẩn hóa tự động.
- **Hoạt động liên tục 24/7** mà không cần can thiệp của con người.
- **Tương tác thân thiện** với người dùng thông qua phản hồi trực tiếp từ Streamlit.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Jira Cloud** (đăng ký tại [atlassian.com](https://www.atlassian.com/software/jira/overview)).
2. **API Token Jira** (tạo tại: **Cài đặt → API Tokens**).
3. **Ứng dụng Streamlit** đã được cấu hình với Webhook để gửi dữ liệu ticket.
4. **URL Webhook** của workflow n8n (sẽ được sử dụng trong ứng dụng Streamlit).
5. **Thông tin cấu hình Jira**:
   - Domain Jira (ví dụ: `your-company.atlassian.net`).
   - Email và API Token của Jira.
   - Thông tin các trường tùy chọn (nếu có): Story Points, Labels, Priority, Due Date.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1:** Tải workflow từ [n8n.io/workflows/8156](https://n8n.io/workflows/8156) hoặc sao chép JSON từ trang này.
- **Bước 2:** Mở **n8n Editor** và chọn **Import Workflow** (từ menu bên trái).
- **Bước 3:** Dán JSON vào và chọn **Import**.

:::note[LƯU Ý]
- **Không chạy node Jira HTTP thủ công!** Luôn kích hoạt workflow thông qua Webhook từ Streamlit.
- **Sử dụng URL Production** trong ứng dụng Streamlit (không dùng Test URL trong môi trường sản xuất).
:::

---

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này bao gồm **10 node** quan trọng, mỗi node đều cần cấu hình cẩn thận:

##### **A. Webhook Streamlit (n8n-nodes-base.webhook)**
- **Path:** Đặt tên duy nhất (ví dụ: `/create-jira-ticket`).
- **HTTP Method:** POST.
- **Response Mode:** Chọn **lastNode** để phản hồi từ node cuối cùng (node `Result`) được gửi trở lại Streamlit.

##### **B. Xử Lý Dữ Liệu Trước Khi Gửi Jira (n8n-nodes-base.code)**
- **Node `Process streamlit data`:**
  - Chuyển đổi dữ liệu từ Streamlit sang định dạng Jira:
    ```javascript
    // Ví dụ: Chuyển đổi projectKey thành project.key (in hoa)
    const fields = {
      project: { key: data.projectKey.toUpperCase() },
      issuetype: { name: data.type },
      summary: data.summary,
      description: data.description,
      priority: { name: data.priority },
      duedate: data.due_date ? new Date(data.due_date).toISOString().split('T')[0] : null,
      labels: data.labels || [],
      customfield_10016: data.story_points // Thay thế ID trường tùy thuộc vào Jira của bạn
    };
    return { fields };
    ```
- **Node `anti double`:**
  - Kiểm tra xem ticket đã tồn tại trong **Workflow Static Data** (n8n tự động lưu trữ dữ liệu này).
  - Nếu `ticket.id` hoặc `projectKey+type+summary+description` đã tồn tại, đánh dấu là **duplicate**.
  - Nếu `action` không phải `create_ticket` hoặc thiếu trường bắt buộc, đánh dấu là **invalid**.

##### **C. Gửi Request Jira (n8n-nodes-base.httpRequest)**
- **URL:** `https://<your-domain>.atlassian.net/rest/api/3/issue`
- **Method:** POST.
- **Auth:** Chọn **Jira Software Cloud API** và điền:
  - **Email:** Email Jira của bạn.
  - **API Token:** API Token từ Jira.
- **Headers:**
  - `Content-Type: application/json`
  - `Accept: application/json`
- **Body (Raw JSON):**
  ```json
  {
    "fields": {
      "project": { "key": "PROJ" },
      "issuetype": { "name": "Task" },
      "summary": "Tóm tắt ticket",
      "description": "Mô tả ticket (định dạng Markdown)",
      "priority": { "name": "High" },
      "duedate": "2024-12-31",
      "labels": ["bug", "critical"],
      "customfield_10016": 8
    }
  }
  ```
  - **Lưu ý:** Đảm bảo `fields` là **object JSON**, không phải chuỗi `"[object Object]"`!

##### **D. Trả Lại Kết Quả Cho Streamlit (n8n-nodes-base.code)**
- **Node `Result`:**
  - Trả về JSON cho Streamlit:
    ```json
    {
      "ok": true,
      "jiraKey": "TES-123",
      "url": "https://your-domain.atlassian.net/browse/TES-123"
    }
    ```
  - **Streamlit sẽ hiển thị:**
    - `TES-123` (key ticket mới).
    - Link mở ticket trên Jira.

---

#### **3. Kích Hoạt ⚡️**
- **Bước 1:** Chạy **Test Run** với dữ liệu mẫu từ Streamlit để kiểm tra:
  - Ticket có được tạo thành công không?
  - Có phản hồi từ Jira không?
- **Bước 2:** Bật **Active** workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CẢNH BÁO & TIẾP CẬN]
1. **Lưu Log Cho Debugging:**
   - Sử dụng **n8n-nodes-base.stickyNote** để ghi lại dữ liệu đầu vào và đầu ra trong quá trình debug.
   - Ví dụ: Ghi `raw data from streamlit` và `jira response` vào một sheet Google Sheets hoặc Slack.

2. **Gửi Báo Cáo Định Kỳ:**
   - Kết hợp với **n8n-nodes-base.email** hoặc **n8n-nodes-base.slack** để thông báo khi có ticket mới được tạo.

3. **Tích Hợp Slack/Telegram:**
   - Sử dụng **n8n-nodes-base.slack** hoặc **n8n-nodes-base.telegram** để thông báo ngay khi ticket được tạo thành công hoặc thất bại.

4. **Tùy Chỉnh Trường Tùy Chọn:**
   - Nếu Jira của bạn có trường tùy chỉnh (ví dụ: `customfield_10016` cho Story Points), hãy kiểm tra **ID trường** trong **Jira → Cài đặt → Trường tùy chỉnh**.
   - Thay đổi trong node `Process streamlit data` để phù hợp.

5. **Bảo Mật API Token:**
   - **Không bao giờ commit API Token vào GitHub!** Sử dụng **n8n Credentials** để lưu trữ an toàn.
   - Cách lưu: **Settings → Credentials → Add Credential** (chọn loại `Jira Software Cloud API`).
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp quản lý dự án muốn tự động hóa việc tạo ticket Jira từ Streamlit **không cần viết một dòng code nào**. Bằng cách kết hợp **Webhook, REST API, và logic kiểm tra duy nhất**, bạn sẽ:
✅ **Tiết kiệm thời gian** trong việc nhập liệu thủ công.
✅ **Tránh trùng lặp ticket** nhờ cơ chế kiểm tra.
✅ **Cung cấp trải nghiệm người dùng tốt** với phản hồi tức thời.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** để workflow hoạt động 24/7.
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Kích hoạt và thử nghiệm** với dữ liệu mẫu.

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%) để tự động hóa mọi lúc!

---
**Chia sẻ và đánh giá nếu bạn thấy hữu ích!** 🚀