---
title: "🤖 **Tự Động Hóa Quản Lý Nhiệm Vụ với AI Manager + Sub-Agent: Hỗ Trợ Tối Đa 24/7 Cho Doanh Nghiệp**"
description: "Workflow này tự động phân tích yêu cầu người dùng và giao nhiệm vụ cho các AI sub-agent chuyên biệt (viết email, phân tích dữ liệu) bằng GPT-4o-mini, tiết kiệm thời gian quản lý lên đến 80% cho các sếp và nhân viên. Đặc biệt phù hợp cho doanh nghiệp cần tự động hóa quy trình email, báo cáo và phân tích."
slug: "tieu-dong-hoa-quan-ly-nhiem-vu-ai-manager-sub-agent"
tags: [n8n, automation, no-code, ai-agent, langchain, openai, email-automation]
keywords: [n8n workflow ai agent, tự động hóa quản lý nhiệm vụ, AI sub-agent, GPT-4o-mini, phân tích dữ liệu tự động, viết email tự động]
---

# 🚀 **AI Manager + Sub-Agent: Hệ Thống Tự Động Hóa Quản Lý Nhiệm Vụ Siêu Cường**

## 🔍 **Nỗi Đau Của Các Sếp Và Giải Pháp Tự Động Hóa 100% Không Code**
Hàng ngày, các sếp và đội ngũ quản lý phải:
- **Phân loại và xử lý hàng trăm yêu cầu** từ nhân viên, khách hàng, hoặc hệ thống (email, chat, ticket).
- **Tốn thời gian** để viết email chuyên nghiệp, tổng hợp dữ liệu, hoặc phân tích báo cáo.
- **Mất tập trung** vào công việc chiến lược vì bị "dập tắt" bởi các nhiệm vụ lặp đi lặp lại.

**Workflow này giải quyết tất cả đó!** Bằng cách sử dụng **AI Manager (Agent)** kết hợp với **2 Sub-Agent chuyên biệt** (viết email và phân tích dữ liệu), hệ thống sẽ:
✅ **Phân tích tự động** yêu cầu người dùng và **giao nhiệm vụ** cho AI phù hợp.
✅ **Viết email chuyên nghiệp** trong giây lát (follow-up, báo cáo, thông báo).
✅ **Tổng hợp và phân tích dữ liệu** từ các nguồn khác nhau (Excel, Airtable, Google Sheets).
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định và không bị gián đoạn, các sếp nên **self-host n8n trên VPS** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ xử lý nhanh cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm 80% thời gian quản lý nhiệm vụ lặp đi lặp lại (email, báo cáo, phân tích).
- **Chính xác và chuyên nghiệp**: Email và báo cáo được viết bởi AI với ngữ điệu phù hợp, tránh sai sót người dùng.
- **Tự động hóa phân loại nhiệm vụ**: AI Manager tự động xác định yêu cầu và giao cho sub-agent phù hợp.
- **Hoạt động liên tục**: Hệ thống hoạt động 24/7, không cần can thiệp của con người.
- **Dễ mở rộng**: Thêm sub-agent mới (ví dụ: sub-agent hỗ trợ Slack, Zoom) chỉ với vài bước cấu hình.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** với API Key:
   - Đăng ký tại [OpenAI](https://platform.openai.com/) và lấy **API Key** từ [tài khoản của bạn](https://platform.openai.com/api-keys).
   - **Model sử dụng**: `gpt-4o-mini` (rẻ và hiệu quả cho các tác vụ này).
2. **n8n Self-hosted** (không dùng phiên bản cloud để đảm bảo dữ liệu an toàn).
3. **Không cần kiến thức code**: Workflow này hoàn toàn **no-code**, chỉ cần copy/paste và cấu hình.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7158](https://n8n.io/workflows/7158) hoặc copy toàn bộ JSON dưới đây vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Editor** (trang chủ của workflow).
  2. Nhấp vào **Import** (icon "↑" ở góc trên bên phải).
  3. Chọn **Paste JSON** và dán toàn bộ nội dung JSON từ file tải xuống.
  4. Nhấp **Import**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **9 node** chính, nhưng các bước quan trọng nhất cần chú ý:

##### **A. Cấu Hình API Key OpenAI**
- **Node**: `OpenAI Chat Model`, `OpenAI Chat Model1`, `OpenAI Chat Model2`.
- **Hành động**:
  1. Vào **Credentials** của n8n (cài đặt > Credentials).
  2. Thêm **OpenAI API Key** với tên `openAiApi`.
  3. Điền **API Key** từ OpenAI vào trường `Api Key`.
  4. Chọn **Model**: `gpt-4o-mini` (đã được cấu hình sẵn trong workflow).

##### **B. Cấu Hình AI Manager (Node `ManagerAgent`)**
- **Node**: `ManagerAgent (Routing + Instruction Generator)` (type: `agent`).
- **Hành động**:
  1. Vào **System Message** của node này và **điền lại** nội dung sau:
     ```
     You are an AI Manager that delegates tasks to specialized agents.
     Your job is to analyze the user's message and decide whether it requires:
     - An EmailAgent for writing outreach, follow-up, or templated emails, or
     - A DataAgent for tasks involving data summaries, metrics, or analysis.
     Send the instructions to the sub agents.
     ```
  2. **Kết nối với Sub-Agent**:
     - Node này sẽ **gửi yêu cầu** đến `EmailAgent` và `DataAgent` thông qua các `ai_tool` input.

##### **C. Cấu Hình Sub-Agent (EmailAgent & DataAgent)**
###### **1. EmailAgent (Communication Specialist)**
- **Node**: `EmailAgent (Communication Specialist)` (type: `agentTool`).
- **Hành động**:
  1. Vào **Tool Description** và điền:
     ```
     Writes professional, friendly, or action-oriented emails based on instructions.
     ```
  2. Vào **System Message** và điền:
     ```
     You are an EmailAgent. Your job is to write emails that are clear, professional, and tailored to the user's needs.
     ```
  3. Vào **Input Text Field** và thay thế bằng:
     ```
     {{ $fromAI('Prompt__User_Message_', ``, 'string') }}
     ```
  4. **Kết nối với ManagerAgent**:
     - Đảm bảo node này được **gắn vào `ai_tool` input** của `ManagerAgent`.

###### **2. DataAgent (Insight Generator)**
- **Node**: `DataAgent (Insight Generator)` (type: `agentTool`).
- **Hành động**:
  1. Vào **Tool Description** và điền:
     ```
     Responds to instructions requiring metrics, summaries, or data analysis explanations.
     ```
  2. Vào **Input Text Field** và điền:
     ```
     {{json.query}}
     ```
  3. Vào **System Message** (nếu cần) và điền:
     ```
     You are a DataAgent. Your job is to analyze data, generate summaries, and provide insights based on the input.
     ```

##### **D. Cấu Hình Bộ Nhớ (Memory)**
- **Node**: `Simple Memory`, `Simple Memory1`, `Simple Memory2` (type: `memoryBufferWindow`).
- **Hành động**:
  - Các node này **lưu trữ lịch sử chat** để AI có thể nhớ các thông tin trước đó.
  - **Không cần chỉnh sửa gì** (n8n sẽ tự động quản lý).

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một yêu cầu mẫu vào **Webhook** (nếu có) hoặc sử dụng **n8n UI** để test.
   - Ví dụ:
     - **Yêu cầu 1**: *"Viết một email follow-up cho khách hàng ABC về đơn hàng #123."*
       → AI Manager sẽ **giao nhiệm vụ** cho `EmailAgent`.
     - **Yêu cầu 2**: *"Tổng hợp dữ liệu doanh thu quý 2 từ Google Sheets."*
       → AI Manager sẽ **giao nhiệm vụ** cho `DataAgent`.
2. **Bật Active**:
   - Sau khi test thành công, **bật workflow** để nó hoạt động liên tục.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Slack/Telegram**:
   - Thêm **node Slack/Telegram** để nhận thông báo khi AI hoàn thành nhiệm vụ.
   - Ví dụ: Sau khi `EmailAgent` viết xong email, nó sẽ gửi kết quả về Slack.

2. **Lưu Log & Báo Cáo**:
   - Thêm **node Google Sheets** hoặc **Airtable** để lưu lịch sử các nhiệm vụ đã xử lý.
   - Ví dụ: Lưu email đã viết, dữ liệu đã phân tích, và thời gian thực hiện.

3. **Cập Nhật Model AI**:
   - Nếu muốn nâng cấp hiệu suất, thay đổi model từ `gpt-4o-mini` sang `gpt-4` (tốn nhiều hơn nhưng chính xác hơn).

4. **Thêm Sub-Agent Mới**:
   - Ví dụ: Tạo **sub-agent hỗ trợ Zoom** để tự động tạo ghi chú cuộc họp.

5. **Tối Ưu Hóa Prompt**:
   - Nếu AI Manager không phân loại nhiệm vụ chính xác, cập nhật **System Message** của nó để rõ ràng hơn.

---

### 📌 **Kết Luận: Áp Dụng Ngay Để Tiết Kiệm Thời Gian!**
Workflow **AI Manager + Sub-Agent** này là **giải pháp hoàn hảo** cho các sếp và đội ngũ quản lý muốn:
✔ **Tự động hóa 80% công việc lặp đi lặp lại** (email, báo cáo, phân tích).
✔ **Giảm thiểu sai sót** nhờ AI viết và phân tích chính xác.
✔ **Hoạt động 24/7** mà không cần can thiệp của con người.

**Hành động ngay hôm nay**:
1. **Import workflow** vào n8n của bạn.
2. **Cấu hình API Key OpenAI** và các node quan trọng.
3. **Test với dữ liệu mẫu** và bật workflow.
4. **Mở rộng** bằng cách thêm sub-agent mới hoặc tích hợp với Slack/Google Sheets.

**Nếu gặp khó khăn**, liên hệ với tác giả **Robert Breen** qua:
📧 [robert@ynteractive.com](mailto:robert@ynteractive.com)
🔗 [LinkedIn](https://www.linkedin.com/in/robert-breen-29429625/)

---
**Chúc các sếp thành công với tự động hóa AI!** 🚀