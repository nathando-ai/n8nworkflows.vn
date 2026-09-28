---
title: "🌅 Tự Động Hóa Todoist + AI OpenRouter: Lên Kế Hoạch Ngày Hàng Ngày Và Nhận Tóm Tắt Trên Slack Mỗi Sáng"
description: "Workflow tự động hóa lấy danh sách Todoist, phân tích và ưu tiên nhiệm vụ hàng ngày bằng AI OpenRouter, sau đó gửi tóm tắt chi tiết lên Slack mỗi sáng. Giúp các sếp tiết kiệm 3+ giờ/ngày và bắt đầu ngày với kế hoạch rõ ràng, tối ưu hóa năng suất."
slug: "tieu-dong-hoa-todoist-ai-openrouter-slack"
tags: [n8n, automation, no-code, ai, todoist, slack, openrouter, langchain, self-hosted]
keywords: [tự động hóa todoist, ai phân tích nhiệm vụ, openrouter n8n, gửi tóm tắt slack hàng ngày, tự động hóa năng suất, workflow n8n ai]
---

# 🚀 **Tự Động Hóa Todoist + AI OpenRouter: Lên Kế Hoạch Ngày Hàng Ngày Và Nhận Tóm Tắt Trên Slack Mỗi Sáng**

## **📌 Nỗi Đau Của Các Sếp Hiện Nay**
Mỗi sáng, các sếp phải mất **30-60 phút** để:
✅ Lọc và phân loại hàng trăm nhiệm vụ trong Todoist.
✅ Phân biệt nhiệm vụ **ưu tiên cao** (deadline, tác động lớn) từ những nhiệm vụ nhỏ.
✅ Đặt lịch và ưu tiên dựa trên **công việc quan trọng nhất (MIT)** mà không bị phân tâm.
✅ Ghi nhớ và theo dõi tiến độ trong ngày.

**Kết quả?** → **Stress, năng suất thấp, và cảm giác "bị chìm" trong công việc.**

---
### **🎯 Giải Pháp: Workflow Tự Động Hóa AI + Todoist + Slack**
Workflow này **tự động hóa toàn bộ quy trình** bằng cách:
✔ **Lấy danh sách Todoist** (hoặc Google Tasks, Notion) vào **8h sáng**.
✔ **Phân tích và ưu tiên nhiệm vụ** bằng **AI OpenRouter** (giống GPT-4 nhưng rẻ hơn).
✔ **Gửi tóm tắt chi tiết** lên **Slack** với:
   - Danh sách nhiệm vụ ưu tiên cao.
   - Thời gian ước tính hoàn thành.
   - Gợi ý thời gian bắt đầu.
   - Cảnh báo nhiệm vụ **quan trọng nhưng dễ bị quên**.

**Kết quả?** → **Bắt đầu ngày với kế hoạch rõ ràng, tiết kiệm 3+ giờ/ngày, và năng suất tăng gấp đôi!**

---

## **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 3-5 giờ/ngày** cho việc lên kế hoạch.
- **Ưu tiên nhiệm vụ chính xác** bằng AI, không còn "làm gì trước".
- **Nhận báo cáo hàng ngày** trên Slack, không phải nhớ thủ công.
- **Hoạt động 24/7** mà không cần can thiệp.
- **Cá nhân hóa** theo nhu cầu công việc riêng (ví dụ: ưu tiên nhiệm vụ liên quan đến khách hàng).
:::

---

## **🔧 Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Trước khi import workflow, các sếp cần chuẩn bị:
✅ **Tài khoản Todoist** (hoặc Google Tasks/Notion nếu thay thế).
✅ **API Key OpenRouter** (để sử dụng AI phân tích).
✅ **Credentials Slack** (để gửi tóm tắt).
✅ **n8n Self-hosted** (không hỗ trợ trên n8n.cloud vì sử dụng node LangChain).

🔹 **Lưu ý:** Workflow này **không hoạt động trên n8n.cloud** vì sử dụng node `@n8n/n8n-nodes-langchain` (chỉ có trên self-hosted).
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Từ file JSON**
1. **Tải workflow** từ [đây](https://n8n.io/workflows/9564) (nút "Export").
2. **Mở n8n Editor** (trang chủ của n8n self-hosted).
3. Nhấn **"Import"** → Chọn file JSON vừa tải.
4. **Chọn workspace** (nếu có nhiều workspace).

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ file export.
2. Trong n8n Editor, nhấn **"Import"** → **"Paste JSON"**.
3. **Chọn workspace** và nhấn **"Import"**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow có **7 node chính**, các sếp cần **cấu hình kỹ lưỡng** các node sau:

#### **🔹 Node 1: Morning Schedule Trigger (8h sáng)**
- **Điều chỉnh thời gian** trong node này để phù hợp với giờ làm việc của các sếp.
  - Mở node → Tab **"Settings"** → Thay đổi `"cron"` từ `"0 8 * * *"` (8h sáng) thành `"0 9 * * *"` (nếu muốn chạy lúc 9h).
  - **Cú pháp cron:**
    - `0 8 * * *` → 8h sáng hàng ngày.
    - `0 9 * * 1-5` → 9h sáng từ thứ 2 đến thứ 6.

#### **🔹 Node 2: Get Todo List (Lấy danh sách Todoist)**
- **Thiết lập credentials Todoist:**
  1. Trong n8n Editor, nhấn **"Credentials"** (góc trên bên phải).
  2. Tạo mới **Todoist OAuth2** (nếu chưa có).
  3. **Cấu hình OAuth2:**
     - **Client ID & Secret:** Lấy từ [Todoist Developer](https://todoist.com/app/settings/developer).
     - **Callback URL:** `http://localhost:5678/oauth2/callback/todoistOAuth2Api` (hoặc URL của VPS nếu self-hosted).
  4. **Kết nối** và **cho phép quyền** khi Todoist yêu cầu.

#### **🔹 Node 3: AI Task Analyzer (Phân tích nhiệm vụ bằng AI)**
- **Thiết lập credentials OpenRouter:**
  1. Tạo **OpenRouter API Key** tại [OpenRouter](https://openrouter.ai/).
  2. Trong n8n, thêm **credentials mới** (nếu chưa có) với tên `openRouterApi`.
  3. **Điền API Key** vào trường `apiKey`.
  4. **Cấu hình Prompt (gợi ý):**
     - Mở node → Tab **"Settings"** → **"Advanced"** → **"Prompt"**.
     - **Sửa prompt mặc định** (nếu muốn AI ưu tiên khác):
       ```json
       "You are an AI assistant that helps prioritize tasks. For each task, analyze:
       - Deadline (if any)
       - Effort required (low/medium/high)
       - Impact on business goals
       - Dependencies on other tasks
       Return a structured JSON with:
       - 'priority': 'high/medium/low'
       - 'estimated_time': '15min/1h/2h+'
       - 'notes': 'Additional context'
       "
       ```

#### **🔹 Node 4: Task Priority Parser (Xử lý kết quả AI)**
- **Node này tự động chuyển đổi** output của AI thành định dạng JSON.
- **Không cần chỉnh sửa** trừ khi AI trả về kết quả không chuẩn.

#### **🔹 Node 5: Format AI Summary (Định dạng tin nhắn)**
- **Không cần chỉnh sửa** (node này tự động tạo ra format Slack).
- **Nếu muốn thay đổi nội dung**, mở node → Tab **"Settings"** → **"Advanced"** → **"Template"**.

#### **🔹 Node 6: Send to Slack (Gửi tóm tắt lên Slack)**
- **Thiết lập credentials Slack:**
  1. Trong n8n, thêm **Slack OAuth2** (nếu chưa có).
  2. **Cấu hình:**
     - **Client ID & Secret:** Lấy từ [Slack API](https://api.slack.com/apps).
     - **Scopes:** `chat:write`, `users:read`.
     - **Callback URL:** `http://localhost:5678/oauth2/callback/slackOAuth2Api`.
  3. **Chọn channel/DM** trong node:
     - Mở node → Tab **"Settings"** → **"Advanced"** → **"Channel ID"** (hoặc `@username` nếu gửi DM).
     - **Lấy Channel ID:**
       - Mở Slack → Nhấn `Ctrl + Shift + P` → Gõ `Copy link` → Chọn channel → Copy ID từ URL.

#### **🔹 Node 7: OpenRouter Chat Model (Model AI)**
- **Không cần chỉnh sửa** trừ khi muốn thay đổi **model AI**:
  - Mở node → Tab **"Settings"** → **"Advanced"** → **"Model"** (ví dụ: `openrouter/mistral-7b`).
  - **Lưu ý:** Các model miễn phí có giới hạn request.

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run (kiểm tra trước khi chạy thực tế):**
   - Nhấn **"Run Workflow"** (nút play).
   - **Kiểm tra Slack** để xem kết quả.
   - **Sửa lỗi** nếu có (ví dụ: Todoist không lấy được task, AI trả về kết quả sai).

2. **Bật Active:**
   - Sau khi test thành công, nhấn **"Active"** (đỏ → xanh).

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::tip[**CÁCH LÀM NÀY ĐỂ TỐT HƠN**]
- **Thay thế Todoist bằng Google Tasks/Notion:**
  - Thay node `Get Todo List` bằng `Google Tasks` hoặc `Notion API`.
  - **Cách thay đổi:**
    1. Xóa node `Get Todo List`.
    2. Thêm node `Google Tasks` (nếu dùng Google).
    3. Cấu hình credentials Google.

- **Gửi báo cáo định kỳ (ngày/tuần):**
  - Sửa node `Morning Schedule Trigger` thành:
    - **Hàng tuần:** `"0 9 * * 0"` (9h sáng Chủ Nhật).
    - **Hàng tháng:** `"0 9 1 * *"` (ngày 1 hàng tháng).

- **Lưu log vào StickyNote (dành cho debug):**
  - Thêm node `StickyNote` sau node `Format AI Summary` để lưu kết quả.
  - **Cách thêm:**
    1. Nhấn **"Add Node"** → Tìm `StickyNote`.
    2. Kết nối với node `Format AI Summary`.
    3. **Lưu ý:** Node này chỉ có trên self-hosted.

- **Kết hợp với Microsoft Teams/Discord:**
  - Thay node `Slack` bằng `Microsoft Teams` hoặc `Webhook` (Discord).
  - **Cách thay đổi:**
    1. Xóa node `Slack`.
    2. Thêm node `Microsoft Teams` (nếu dùng Teams).
    3. Cấu hình credentials Teams.

- **Tự động xóa nhiệm vụ đã hoàn thành:**
  - Thêm node `Todoist` mới sau `Send to Slack` với **operation = "complete"** (đánh dấu hoàn thành).
  - **Cách thêm:**
    1. Nhấn **"Add Node"** → `Todoist`.
    2. Chọn **operation = "complete"**.
    3. **Lọc task đã hoàn thành** bằng `filter` trong node.
:::

---

## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào công việc **quan trọng nhất**, thay vì mất giờ lên kế hoạch hàng ngày. Với **AI OpenRouter** phân tích nhiệm vụ và **Slack** báo cáo tóm tắt, các sếp sẽ:
✅ **Bắt đầu ngày với kế hoạch rõ ràng**.
✅ **Ưu tiên nhiệm vụ chính xác** (không còn "làm gì trước").
✅ **Tiết kiệm 3-5 giờ/ngày** cho việc quản lý công việc.

**🚀 Hành động ngay!**
1. **Cài đặt n8n self-hosted** (nếu chưa có) trên [VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (mã giảm **VPSN8N**).
2. **Import workflow** và **cấu hình credentials**.
3. **Bật Active** và **nhận tóm tắt hàng ngày** trên Slack!

**💡 Mẹo cuối:** Nếu gặp vấn đề, **hãy test run trước** và **kiểm tra log** trong n8n Editor (tab **"Logs"**).

---
**🔥 Cảm ơn các sếp đã sử dụng workflow này!** 🔥
**📢 Chia sẻ kinh nghiệm** khi sử dụng trong comment dưới đây!