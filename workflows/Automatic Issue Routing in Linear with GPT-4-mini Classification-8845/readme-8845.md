---
title: "🚀 Tự Động Phân Loại & Giao Nhận Issue Tự Động trên Linear với GPT-4-mini (Không Cần Code)"
description: "Workflow tự động hóa phân loại và giao nhận issue từ Linear sang các team phù hợp (Engineering, Product, Design) bằng trí tuệ nhân tạo GPT-4-mini, tiết kiệm 80% thời gian triaging thủ công. Hoạt động 24/7 mà không cần can thiệp người dùng."
slug: "tu-dong-phan-loai-giao-nhan-issue-linear-gpt-4-mini"
tags: [n8n, automation, no-code, linear, ai, gpt-4-mini, content-creation, agentic-ai]
keywords: [tự động hóa linear, phân loại issue với ai, giao nhận tự động, gpt-4-mini n8n, workflow linear ai, triaging issue không code]
---

# 🚀 **Tự Động Phân Loại & Giao Nhận Issue trên Linear với GPT-4-mini (Không Cần Code)**

### **Giải pháp cho các sếp đang mệt mỏi với việc triaging issue thủ công**
Hàng ngày, các team Engineering, Product và Design phải mất **từ 30-60 phút** để phân loại và giao nhận issue từ Linear. Các issue mới được tạo hoặc cập nhật liên tục, nhưng việc **phân loại thủ công** không chỉ tốn thời gian mà còn dễ gây **lỗi phân loại** (ví dụ: issue về UI giao cho team Engineering). **Workflow này tự động hóa toàn bộ quy trình** bằng trí tuệ nhân tạo (GPT-4-mini), giúp:
- **Phân loại issue chính xác** (Engineering, Product, Design, hoặc Default) chỉ trong **vài giây**.
- **Giao nhận tự động** sang team phù hợp trên Linear, **không cần can thiệp người dùng**.
- **Tiết kiệm 80% thời gian** cho các sếp và team, đồng thời **giảm thiểu lỗi phân loại** do con người gây ra.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng thay vì dùng phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian triaging**: Không cần phải đọc từng issue một, AI tự phân loại và giao nhận.
✅ **Chính xác cao**: GPT-4-mini hiểu ngữ cảnh của issue, giảm thiểu lỗi phân loại so với cách thủ công.
✅ **Hoạt động liên tục**: Workflow chạy **24/7** mà không cần người dùng kích hoạt.
✅ **Cá nhân hóa giao nhận**: Issue được tự động gán cho team phù hợp (Engineering, Product, Design).
✅ **Dễ dàng mở rộng**: Thêm team hoặc quy tắc phân loại mới chỉ bằng cách **cập nhật prompt** của AI.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Linear** (để kết nối API):
   - **Linear API Key** (tạo tại [Linear API Settings](https://linear.app/settings/api)).
   - **Team ID** của các team (Engineering, Product, Design) để giao nhận issue.
   - **Workspace ID** của Linear.

2. **Tài khoản OpenAI** (để sử dụng GPT-4-mini):
   - **API Key** từ [OpenAI Platform](https://platform.openai.com/account/api-keys).
   - **Tài khoản có đủ credit** (GPT-4-mini tính theo token, ~0.15$/1M tokens).

3. **N8n Editor** (cài đặt phiên bản **self-hosted** để ổn định):
   - [Cài đặt n8n trên VPS](https://docs.n8n.io/hosting/installation/installation-on-a-vps/) (khuyến nghị dùng **Docker**).
   - **N8n Node Manager** (để cài đặt các node bổ sung như `@n8n/n8n-nodes-langchain`).

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/8845](https://n8n.io/workflows/8845) (click "Export").
- **Import vào n8n Editor**:
  - Mở **n8n Editor** → Nhấn **"Import"** → Chọn file JSON vừa tải.
  - **Hoặc** copy toàn bộ JSON và dán vào **"Import from JSON"** trong Editor.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **13 node**, nhưng các sếp cần **cấu hình kỹ 3 phần quan trọng**:

##### **A. Cấu hình Linear API**
- **Node "🔔 Linear Trigger"** và **4 node giao nhận** (`Assign to Engineering`, `Assign to Product`, `Assign to Design`, `Assign to Default`) **cần credentials `linearApi`**.
  - **Cách thiết lập**:
    1. Trong **n8n Editor**, nhấn **"Credentials"** (góc trên bên phải).
    2. Tạo **mới một credential** với tên `linearApi`.
    3. Điền:
      - **API Key**: API Key từ Linear (tạo tại [Linear API Settings](https://linear.app/settings/api)).
      - **Workspace ID**: ID của workspace Linear (thường là một chuỗi hexa, tìm trong URL của Linear).
    4. **Lưu** và chọn `linearApi` cho các node cần thiết.

##### **B. Cấu hình OpenAI API**
- **Node "🧠 OpenAI Chat Model"** và **"🤖 AI Agent (Bug Classifier)"** cần credentials `openAiApi`.
  - **Cách thiết lập**:
    1. Tạo credential mới với tên `openAiApi`.
    2. Điền:
      - **API Key**: API Key từ OpenAI.
      - **Model**: Để mặc định là `gpt-4-mini` (không cần thay đổi).
    3. **Lưu** và chọn `openAiApi` cho hai node trên.

##### **C. Cấu hình Team ID cho Routing**
- Các node **`Engineering Router`**, **`Product Router`**, **`Design Router`**, và **`Default Router`** cần **ID của team** trên Linear.
  - **Cách lấy Team ID**:
    1. Mở Linear → Chọn team (ví dụ: Engineering).
    2. URL của team sẽ có dạng: `https://linear.app/org/[ORG_ID]/team/[TEAM_ID]`.
    3. **TEAM_ID** là chuỗi hexa sau `/team/`.
  - **Cập nhật trong workflow**:
    - Mở node **`Engineering Router`** → Nhấn **"Edit"** → Trong **Switch Condition**, thay thế `[TEAM_ID_ENGINEERING]` bằng Team ID thực tế.
    - Lặp lại cho **Product**, **Design**, và **Default**.

##### **D. Kiểm tra Filter New Issues Only**
- Node **"📋 Filter New Issues Only"** **lọc bỏ issue không có tiêu đề** (tránh xử lý issue trống).
  - **Không cần chỉnh sửa** nếu các sếp đã cấu hình Linear API đúng.

---
#### **3. Kích hoạt ⚡️**
1. **Test Run** với một issue mẫu:
   - Tạo một issue mới trên Linear (ví dụ: "Bug: Button không hoạt động khi click").
   - Chạy **Manual Test** trong n8n Editor để kiểm tra workflow.
   - Kiểm tra:
     - AI có phân loại issue chính xác không?
     - Issue có được giao nhận cho team đúng không?

2. **Bật Active**:
   - Sau khi test thành công, nhấn **"Active"** trên workflow.

---
### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm team mới**:
   - Nếu có team khác (ví dụ: Marketing), **thêm node `Switch` và `Linear` mới** tương tự như Engineering/Product/Design.
   - Cập nhật **prompt** của AI Agent để phân loại team mới.

2. **Lưu log hoạt động**:
   - Thêm node **`n8n-nodes-base.googleSheets`** sau node **`Assign to [Team]`** để ghi lại lịch sử giao nhận.
   - **Cấu hình**:
     - Tạo một sheet Google Sheets với các cột: `Issue ID`, `Team`, `Title`, `Created At`.
     - Thêm node **`Set`** trước khi ghi vào Sheets để định dạng dữ liệu.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **`n8n-nodes-base.email`** hoặc **`n8n-nodes-base.slack`** để thông báo khi có issue mới được giao nhận.
   - Ví dụ: Gửi email cho **Product Manager** khi có issue mới về Product.

4. **Optimize prompt cho AI**:
   - Nếu AI phân loại sai, **cập nhật prompt** trong node **`AI Agent (Bug Classifier)`**:
     ```json
     "prompt": "You are a bug classifier. Classify the following issue into one of these categories: Engineering, Product, Design, or Default. Only return the category name. Issue: {{ $json.title }} Description: {{ $json.description }}"
     ```
   - **Thêm ví dụ** để AI hiểu rõ hơn:
     ```json
     "examples": [
       { "input": "Button not working", "output": "Engineering" },
       { "input": "UI design for login page", "output": "Design" }
     ]
     ```

5. **Sử dụng Webhook cho hệ thống khác**:
   - Thêm node **`n8n-nodes-base.webhook`** trước **Linear Trigger** để nhận issue từ **Jira, Trello, hoặc Slack**.
   - **Cấu hình**:
     - Tạo một Webhook URL trong n8n.
     - Cấu hình hệ thống khác (ví dụ: Jira) để gửi issue đến URL này thay vì Linear.

---
### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp và team khỏi việc **triaging issue thủ công**, đồng thời **tăng cường chính xác** nhờ trí tuệ nhân tạo. **Chỉ cần 3 bước đơn giản**:
1. **Import workflow** từ n8n.io.
2. **Cấu hình Linear API + OpenAI API** (5 phút).
3. **Test và bật Active**.

**Hành động ngay!** Tự động hóa quy trình này và **tiết kiệm 80% thời gian** cho team của bạn. Nếu có vấn đề, **hãy comment bên dưới** hoặc liên hệ với [Avkash Kakdiya](https://itechnotion.com/) (tác giả workflow) để hỗ trợ!

---
**💡 Bạn muốn tự động hóa gì tiếp theo?**
- **Tự động tạo PR từ issue** (GitHub + n8n)?
- **Phân loại email tự động** (Gmail + GPT-4)?
- **Tự động tạo báo cáo Salesforce**?
**Hãy chia sẻ ý tưởng của bạn!** 🚀