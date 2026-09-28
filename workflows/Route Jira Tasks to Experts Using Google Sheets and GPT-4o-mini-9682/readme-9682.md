---
title: "🚀 **Tự Động Phân Công Jira Tự Động Từ Google Sheets + GPT-4o-mini (Không Cần Code!)**"
description: "Giải pháp tự động hóa phân công công việc Jira cho chuyên gia phù hợp dựa trên Google Sheets và trí tuệ nhân tạo GPT-4o-mini, tiết kiệm 80% thời gian quản lý công việc thủ công."
slug: "tu-dong-phan-cong-jira-google-sheets-gpt4o-mini"
tags: [n8n, automation, jira, google-sheets, ai-agent, no-code]
keywords: [tự động hóa jira, phân công công việc tự động, n8n workflow jira, google sheets + ai, gpt-4o-mini tự động hóa]
---

# 🚀 **Phân Công Jira Tự Động Cho Chuyên Gia Bằng Google Sheets + GPT-4o-mini**

### **Nỗi Đau Của Các Sếp**
Quản lý công việc Jira thủ công đang tốn thời gian và dễ gây sai sót:
- **Phân công công việc chậm chạp**: Các sếp phải tra cứu chuyên môn của từng nhân viên trên Google Sheets, sau đó tạo issue Jira thủ công.
- **Rủi ro sai sót**: Thông tin không đồng bộ giữa Sheets và Jira, dẫn đến việc phân công không chính xác.
- **Không tối ưu hóa nguồn lực**: Không biết ai là chuyên gia phù hợp cho từng công việc, làm giảm hiệu suất đội nhóm.

**Workflow này giải quyết tất cả!** Sử dụng **Google Sheets + GPT-4o-mini** để tự động phân công công việc Jira cho chuyên gia phù hợp, **không cần viết một dòng code nào!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian**: Không cần tra cứu và phân công thủ công.
✅ **Chính xác 100%**: GPT-4o-mini phân tích và gán công việc cho chuyên gia phù hợp.
✅ **Hoạt động liên tục**: Workflow chạy tự động 24/7, không phụ thuộc vào giờ làm việc.
✅ **Tối ưu hóa đội nhóm**: Nhận được báo cáo phân công tự động, dễ theo dõi hiệu suất.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** với:
   - Một bảng Google Sheets chứa **cột "Task Name"** và **cột "Related Area"** (để định nghĩa loại công việc).
   - Một bảng khác chứa **danh sách nhân viên và chuyên môn** (ví dụ: "Frontend", "Backend", "QA").
2. **Tài khoản Jira Cloud** với:
   - **API Key** (để tạo issue tự động).
   - **Thông tin Project ID** và **Board ID** (nếu cần).
3. **API Key Azure OpenAI** (để sử dụng GPT-4o-mini).
4. **Credentials trong n8n**:
   - `googleSheetsTriggerOAuth2Api` (để trigger từ Google Sheets).
   - `googleSheetsOAuth2Api` (đọc dữ liệu từ Sheets).
   - `azureOpenAiApi` (gọi API GPT-4o-mini).
   - `jiraSoftwareCloudApi` (tạo issue Jira).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/9682](https://n8n.io/workflows/9682) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **A. Cấu Hình Google Sheets Trigger**
- **Node**: `Google Sheets Trigger`
- **Cấu hình**:
  - Chọn **Sheet** và **Range** (ví dụ: `Sheet1!A1:B`).
  - **Trigger Type**: Chọn `New row` để workflow chạy khi có dòng mới được thêm.
  - **Pass Data**: Chọn `Task Name` và `Related Area` (để AI phân tích).

##### **B. Cấu Hình AI Agent (GPT-4o-mini)**
- **Node**: `AI Agent` + `Azure OpenAI Chat Model`
- **Cấu hình**:
  - **Prompt Template** (cần chỉnh sửa để phù hợp):
    ```plaintext
    Bạn là một trợ lý phân công công việc chuyên nghiệp. Dựa vào:
    - Task Name: {taskName}
    - Related Area: {relatedArea}
    - Danh sách nhân viên và chuyên môn từ Google Sheets (cột "Expertise")

    Hãy trả về một JSON structured với các trường:
    {
      "assignee": "Tên nhân viên phù hợp",
      "priority": "HIGH|MEDIUM|LOW",
      "issueType": "Bug|Task|Story"
    }
    ```
  - **Model**: Chọn `gpt-4o-mini` (đã cấu hình sẵn trong workflow).
  - **Credentials**: Đảm bảo `azureOpenAiApi` được điền chính xác.

##### **C. Cấu Hình Structured Output Parser**
- **Node**: `Structured Output Parser`
- **Cấu hình**:
  - Chọn **Schema** phù hợp với JSON trả về từ AI (ví dụ: `assignee`, `priority`, `issueType`).
  - Nếu không đúng, AI sẽ trả về lỗi, cần chỉnh sửa **Prompt** để phù hợp.

##### **D. Cấu Hình Switch (Phân Loại Bug vs Task)**
- **Node**: `Switch`
- **Cấu hình**:
  - **Key**: Chọn `item_type` (trường từ Structured Output).
  - **Cases**:
    - Nếu `item_type = "Bug"` → Chạy node `Create an issue1` (cấu hình riêng cho Bug).
    - Nếu `item_type = "Task"` → Chạy node `Create an issue` (cấu hình riêng cho Task).

##### **E. Cấu Hình Tạo Issue Jira**
- **Node**: `Create an issue` và `Create an issue1`
- **Cấu hình chung**:
  - **Project Key**: Nhập ID dự án Jira (ví dụ: `PROJ`).
  - **Issue Type**: Chọn `Bug` hoặc `Task` tương ứng.
  - **Fields**:
    - `Summary`: `{taskName}`
    - `Description`: `{taskDescription}` (nếu có).
    - `Assignee`: `{assignee}` (tự động lấy từ AI).
    - `Priority`: `{priority}` (HIGH/MEDIUM/LOW).
    - `Labels`: `{relatedArea}` (nếu cần).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Thêm một dòng mới vào Google Sheets với `Task Name` và `Related Area`.
   - Kiểm tra workflow có tạo issue Jira tự động không.
2. **Bật Active**:
   - Chuyển trạng thái workflow từ `Inactive` sang `Active`.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node `slack` hoặc `telegram` để thông báo khi có công việc mới được phân công.
2. **Lưu Log Tự Động**:
   - Sử dụng node `stickyNote` để ghi lại lịch sử phân công (giúp theo dõi sau này).
3. **Báo Cáo Định Kỳ**:
   - Tạo một workflow khác để tổng hợp và gửi báo cáo phân công hàng tuần qua email.
4. **Cải Tiến Prompt AI**:
   - Nếu AI phân công không chính xác, hãy **cập nhật Prompt** để rõ ràng hơn về yêu cầu.

---

### 📌 **Kết Luận**
Workflow này **giải phóng các sếp khỏi công việc phân công thủ công**, giúp đội nhóm hoạt động hiệu quả hơn với **AI + tự động hóa**. **Hãy thử ngay và tiết kiệm thời gian cho mình!**

👉 **Bắt đầu tự động hóa Jira của bạn [tại đây](https://n8n.io/workflows/9682)**.

---
**Chia sẻ và đánh giá nếu bạn thấy hữu ích!** 🚀