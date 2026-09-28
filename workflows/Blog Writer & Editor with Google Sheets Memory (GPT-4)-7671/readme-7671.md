---
title: "🤖 **Tự Động Hóa Viết & Chỉnh Sửa Bài Blog với GPT-4 + Google Sheets (N8N) – Không Cần Code!**"
description: "Workflow tự động hóa viết bài blog từ đầu đến cuối với trí tuệ nhân tạo GPT-4, lưu trữ lịch sử chỉnh sửa trong Google Sheets, và quản lý phiên làm việc thông minh. Giúp các sếp tiết kiệm 80% thời gian soạn thảo, đồng thời đảm bảo tính nhất quán và cá nhân hóa nội dung."
slug: "tieu-dong-hoa-viet-chinh-sua-blog-gpt-4-google-sheets"
tags: [n8n, automation, content-creation, ai-writing, google-sheets, openai, no-code]
keywords: [n8n workflow viết blog, tự động hóa viết bài blog, GPT-4 viết blog, lưu trữ lịch sử chỉnh sửa, Google Sheets + AI, tự động hóa nội dung marketing]
---

# 🚀 **Tự Động Hóa Viết & Chỉnh Sửa Bài Blog với GPT-4 + Google Sheets (N8N)**

### **Giải pháp hoàn hảo cho các sếp cần viết blog nhanh chóng, chính xác và không tốn thời gian**
Viết bài blog là một trong những công việc tốn thời gian nhất trong marketing nội dung. Thường thì các sếp phải:
- **Tìm kiếm ý tưởng** từ đầu đến cuối.
- **Chỉnh sửa lại và lại** để nội dung phù hợp với SEO và mục tiêu.
- **Lưu trữ lịch sử chỉnh sửa** để theo dõi tiến trình.
- **Lo lắng về tính nhất quán** của nội dung.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Viết bài blog tự động** từ một chủ đề đơn giản chỉ với GPT-4.
✅ **Chỉnh sửa lại nội dung** dựa trên yêu cầu cụ thể.
✅ **Lưu trữ lịch sử** tất cả phiên làm việc vào Google Sheets (hoặc Airtable/Notion).
✅ **Ngăn chặn lặp lại** bằng cách đếm số lần chỉnh sửa cho mỗi phiên.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này chạy ổn định và không bị gián đoạn, các sếp nên **self-host n8n trên VPS** để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian soạn thảo** – Chỉ cần cung cấp chủ đề, GPT-4 sẽ viết bài hoàn chỉnh.
- **Nội dung chuyên nghiệp & SEO-friendly** – AI đảm bảo cấu trúc bài viết logic và phù hợp với từ khóa.
- **Lưu trữ lịch sử chỉnh sửa** – Theo dõi tất cả phiên làm việc trong Google Sheets (hoặc Airtable).
- **Ngăn chặn lặp lại** – Workflow tự động dừng nếu đã chỉnh sửa quá nhiều lần cho một phiên.
- **Hoạt động tự động** – Không cần can thiệp thủ công, chạy 24/7 mà vẫn đảm bảo chất lượng.
- **Dễ dàng mở rộng** – Kết nối với Slack/Telegram để thông báo kết quả, hoặc xuất bài viết ra WordPress.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** (để sử dụng GPT-4):
   - [Tạo API Key OpenAI](https://platform.openai.com/api-keys)
   - **Nạp tiền** vào tài khoản (GPT-4 có chi phí cao hơn so với GPT-3.5).
   - **Cấu hình credentials** trong n8n với tên `openAiApi`.

2. **Google Sheets (hoặc Airtable/Notion)**:
   - **Tạo một bảng mới** theo mẫu [đây](https://docs.google.com/spreadsheets/d/1NwnABaQIReMmG2sRGrC-lv-5kpmsKJkUlRm-KmvPsCE/edit?gid=0#gid=0).
   - **Cột bắt buộc**:
     - `session` (ID phiên làm việc).
     - `Rows` (số lần chỉnh sửa).
     - `output` (nội dung bài viết).
   - **Cấu hình OAuth2** trong n8n với tên `googleSheetsOAuth2Api`.

3. **n8n Self-hosted** (không dùng phiên bản cloud để đảm bảo bảo mật và hiệu suất).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** của workflow từ [đây](https://n8n.io/workflows/7671).
- **Mở n8n Editor** → Nhấn `Import` → Chọn file JSON vừa tải.
- **Hoặc copy/paste JSON** từ file vào `Import Workflow` trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **13 node** quan trọng, các sếp cần cấu hình kỹ lưỡng như sau:

##### **A. Cấu hình OpenAI (GPT-4)**
- **Node**: `OpenAI Chat Model2` (type: `lmChatOpenAi`)
  - **Model**: Chọn `gpt-4` (hoặc `gpt-4-1106-preview` nếu muốn tiết kiệm chi phí).
  - **API Key**: Điền vào `openAiApi` (đã cấu hình trước ở bước yêu cầu).

##### **B. Cấu hình Google Sheets**
- **Node**: `Get History` & `n8n History` (type: `googleSheets`)
  - **Spreadsheet**: Chọn bảng Google Sheets đã tạo.
  - **Worksheet**: Chọn sheet chính (ví dụ: `Sheet1`).
  - **Operation**: Đặt `append` để thêm dữ liệu mới vào cuối bảng.

##### **C. Cấu hình Logic & Agent**
- **Node**: `Choose to Write or Edit Blog` (type: `code`)
  - **Mã JavaScript**:
    ```javascript
    // Xác định phiên làm việc và số lần chỉnh sửa
    const sessionId = $input.all()[0].json.sessionId || Math.random().toString(36).substring(2, 15);
    const rows = $input.all()[0].json.rows || 0;

    // Tạo prompt cho AI
    const systemPrompt = `Bạn là một nhà viết blog chuyên nghiệp. Hãy viết một bài blog về chủ đề: ${$input.all()[0].json.topic}. Bài viết phải có cấu trúc rõ ràng, phù hợp với SEO và có độ dài khoảng 1000-1500 từ.`;
    const userPrompt = `Nếu phiên này đã có ${rows} lần chỉnh sửa, hãy tối ưu nội dung thay vì viết lại từ đầu. Nếu chưa, hãy viết bài mới.`;

    return {
      sessionId: sessionId,
      system_prompt: systemPrompt,
      user_prompt: userPrompt,
    };
    ```

- **Node**: `Blog Writer & Editor` (type: `agent`)
  - **Tool**: Chọn `google` (sub-workflow đếm số lần chỉnh sửa).
  - **Output Parser**: Chọn `Structured Output Parser` để AI trả về định dạng JSON.

##### **D. Cấu hình Sub-Workflow (Đếm số lần chỉnh sửa)**
- **Node**: `google` (type: `toolWorkflow`)
  - **Workflow con**: Tạo một workflow nhỏ để lấy dữ liệu từ Google Sheets và đếm số dòng có `sessionId` tương ứng.
  - **Cấu hình**:
    - **Node 1**: `Get History` (lấy dữ liệu từ Google Sheets).
    - **Node 2**: `Filter` (lọc theo `session`).
    - **Node 3**: `Summarize` (đếm số dòng).

##### **E. Cấu hình Node "Check if Ran 4+ times"**
- **Node**: `Check if Ran 4+ times` (type: `if`)
  - **Condition**: `$json.rows > 3` (ngăn chặn chỉnh sửa quá nhiều lần).
  - **Action**:
    - Nếu `true` → **Dừng workflow** hoặc gửi thông báo (ví dụ: Slack).
    - Nếu `false` → **Tiếp tục viết/chỉnh sửa**.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một **chủ đề blog** vào node `Ask about blog topic` (type: `chatTrigger`).
   - Kiểm tra kết quả trong Google Sheets.
2. **Bật Active** workflow sau khi kiểm tra thành công.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết nối với Slack/Telegram**:
   - Thêm node `Slack` hoặc `Telegram Bot` để thông báo kết quả bài viết mới.
   - Ví dụ: Khi workflow hoàn thành, gửi tin nhắn như:
     > *"Bài blog về [Chủ đề] đã hoàn thành! Link: [Đường dẫn]."*

2. **Xuất bài viết ra WordPress**:
   - Sử dụng node `WordPress` để tự động xuất bài viết vào trang blog.
   - Cấu hình `WordPress API Key` và `Site URL`.

3. **Lưu log hoạt động**:
   - Thêm node `Set` hoặc `Sticky Note` để ghi lại thời gian và người thực hiện.
   - Ví dụ:
     ```json
     {
       "timestamp": $datetime.now(),
       "user": "admin",
       "status": "completed"
     }
     ```

4. **Tối ưu chi phí OpenAI**:
   - Thay `gpt-4` bằng `gpt-3.5-turbo` (rẻ hơn) nếu không cần tính năng mới nhất.
   - Sử dụng **temperature** thấp (0.3-0.5) để AI trả về kết quả ổn định hơn.

5. **Tự động gửi báo cáo định kỳ**:
   - Tạo một workflow mới để lấy dữ liệu từ Google Sheets và gửi báo cáo qua email (ví dụ: hàng tuần).

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần viết blog nhanh chóng, chuyên nghiệp và không tốn thời gian. Bằng cách kết hợp **GPT-4, Google Sheets và n8n**, các sếp có thể:
✔ **Tiết kiệm thời gian** soạn thảo.
✔ **Đảm bảo tính nhất quán** của nội dung.
✔ **Theo dõi lịch sử chỉnh sửa** một cách dễ dàng.
✔ **Hoạt động tự động** 24/7.

**Hãy import workflow này ngay hôm nay và bắt đầu tự động hóa quá trình viết blog của mình!** 🚀

---
**Cần hỗ trợ thêm?**
- Liên hệ với tác giả: [Robert Breen](https://www.linkedin.com/in/robert-breen-29429625/) hoặc email: [robert@ynteractive.com](mailto:robert@ynteractive.com).
- **Tự host n8n** với VPS ưu đãi: [TinoHost](https://tino.vn/vps-n8n?affid=388) hoặc [BNIX](https://my.bnix.one/aff.php?aff=172).