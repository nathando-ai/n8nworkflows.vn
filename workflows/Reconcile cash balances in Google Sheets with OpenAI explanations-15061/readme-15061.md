---
title: "🔍 Tự Động Hoà Giải Sổ Cổ Phần Tiền Tệ Trên Google Sheets Với Giải Thích AI (OpenAI) - Khắc Phục Sai Số 100% Không Code"
description: "Workflow này tự động so sánh số dư tài khoản giữa hệ thống nội bộ và tài khoản của bên giữ quỹ (custodian), phát hiện sai số và tự động tạo báo cáo chi tiết với giải thích bằng trí tuệ nhân tạo. Giúp các sếp tiết kiệm hàng giờ công kiểm tra thủ công mỗi tháng, giảm thiểu rủi ro sai sót và cải thiện độ chính xác trong quản lý tài chính."
slug: "tieu-dong-hoa-hoa-giai-so-co-phan-tien-te-google-sheets-ai"
tags: [n8n, automation, google-sheets, ai-summarization, cash-reconciliation, openai, no-code]
keywords: [tự động hóa n8n, hoà giải sổ cổ phần, giải thích sai số bằng AI, OpenAI với n8n, tự động hóa kiểm tra số dư tài khoản, workflow google sheets]
---

# 🚀 **Tự Động Hoà Giải Số Dư Tài Khoản Trên Google Sheets Với Giải Thích AI (OpenAI)**

### **Giải pháp cho nỗi đau "Sai số tài chính" của các sếp**
Hàng tháng, các sếp phải mất **tối thiểu 5-10 giờ** để so sánh số dư tài khoản giữa hệ thống nội bộ và tài khoản của bên giữ quỹ (custodian) bằng tay. Quá trình này không chỉ tốn thời gian mà còn dễ mắc sai sót do con người, đặc biệt khi số liệu lớn. **Workflow này tự động hóa toàn bộ quy trình**, phát hiện sai số và **tự động tạo báo cáo với giải thích bằng AI** (OpenAI), giúp các sếp:
✅ **Tiết kiệm 80% thời gian** so sánh thủ công.
✅ **Giảm thiểu rủi ro sai sót** do kiểm tra bằng mắt.
✅ **Hiểu rõ nguyên nhân sai số** nhờ giải thích tự động từ AI.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo bảo mật và tính liên tục.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hoà giải số dư** giữa hệ thống nội bộ và bên giữ quỹ **mỗi ngày/tuần/tháng** (tùy cấu hình).
- **Phát hiện sai số** và **categorize** thành 2 loại:
  - **Số dư khớp** → Được ghi log tự động.
  - **Số dư không khớp** → AI tự động **giải thích nguyên nhân** và chuẩn bị báo cáo.
- **Báo cáo tự động** được append vào Google Sheets với **cột giải thích AI** để dễ theo dõi.
- **Không cần code** – chỉ cần cấu hình các node và kết nối API.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Hai bảng Google Sheets** với cấu trúc tương tự:
   - **Bảng 1**: Số dư nội bộ (Internal Balances).
   - **Bảng 2**: Số dư của bên giữ quỹ (Custodian Balances).
   - **Cột chung bắt buộc**: `account_id` (để match giữa 2 bảng).
   - **Cột số dư**: Chỉ chứa **số liệu số** (không ký tự).
2. **API Key OpenAI** (để AI giải thích sai số).
3. **Credentials Google Sheets OAuth 2.0** (để n8n đọc/giữ dữ liệu).
4. **Thời gian chạy định kỳ** (ví dụ: hàng ngày lúc 8h sáng).

---
:::note[Lưu ý quan trọng]
- **Không được** sử dụng cùng một bảng Google Sheets cho cả 2 loại số dư (nội bộ và bên giữ quỹ).
- **Cột `account_id` phải duy nhất** trong mỗi bảng để workflow match chính xác.
- **Số dư phải là số nguyên hoặc số thập phân** (không có ký tự như "$", ",").
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [link gốc](https://n8n.io/workflows/15061).
2. Trên **n8n Dashboard**, chọn **"Import"** → Chọn file JSON.
3. Hoặc copy toàn bộ JSON và paste vào **"Create Workflow"** → **"Import from JSON"**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **12 node**, các sếp cần chú ý cấu hình sau:

##### **A. Cấu hình Google Sheets**
- **Node "Fetch Internal Balances"** và **"Fetch Custodian Balances"**:
  - Chọn **credentials**: `googleSheetsOAuth2Api`.
  - Điền **URL của 2 bảng Google Sheets** tương ứng.
  - Chọn **Sheet Name** (trong trường hợp bảng có nhiều sheet).
  - **Chọn cột `account_id`** (để match giữa 2 bảng).
  - **Chọn cột số dư** (ví dụ: `internal_balance` và `custodian_balance`).

##### **B. Cấu hình Schedule Trigger**
- **Node "Run Reconciliation on Schedule"**:
  - Chọn **thời gian chạy định kỳ** (ví dụ: `0 8 * * *` = hàng ngày lúc 8h sáng).
  - **Không cần cấu hình thêm** nếu muốn chạy theo lịch đã thiết lập.

##### **C. Cấu hình AI (OpenAI)**
- **Node "Generate AI Mismatch Explanation"**:
  - Chọn **credentials OpenAI** (đã cấu hình trước trong n8n).
  - **Prompt mẫu** (có thể tùy chỉnh):
    ```
    "Analyze the following financial discrepancy between internal and custodian balances for account {account_id}:
    - Internal Balance: {internal_balance}
    - Custodian Balance: {custodian_balance}
    Provide a concise explanation (max 3 sentences) for the difference."
    ```
  - **Model**: Chọn `gpt-3.5-turbo` (hoặc `gpt-4` nếu có budget).

##### **D. Cấu hình Logging & Output**
- **Node "Log Matched Records"** và **"Append The Data In The Sheet"**:
  - Chọn **credentials Google Sheets** (cùng credentials OAuth 2.0).
  - **Chọn sheet logging** (để ghi kết quả).
  - **Cấu trúc cột**:
    - `account_id`, `internal_balance`, `custodian_balance`, `difference`, `status` (matched/mismatched), `ai_explanation` (nếu có sai số).

##### **E. Cấu hình Logic Sai Số**
- **Node "Check for Balance Mismatch" (IF)**:
  - **Điều kiện**: `$.json[0].difference !== 0` (nếu khác 0 → sai số).
  - **Nếu sai số** → Chuyển sang node AI giải thích.
  - **Nếu khớp** → Ghi log tự động.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy workflow với **mode "Test"** để kiểm tra logic.
   - Kiểm tra **Google Sheets logging** xem có ghi dữ liệu không.
2. **Bật Active**:
   - Sau khi test thành công, **bật "Active"** để workflow chạy tự động theo lịch.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Gửi báo cáo sai số qua Slack/Email**:
   - Thêm **node Slack** hoặc **node Email** sau node **"Prepare Exception Record"** để thông báo khi phát hiện sai số.
   - Ví dụ:
     ```json
     {
       "operation": "sendMessage",
       "text": `🚨 Sai số phát hiện cho account ${account_id}!\n- Số dư nội bộ: ${internal_balance}\n- Số dư bên giữ quỹ: ${custodian_balance}\n- Giải thích AI: ${ai_explanation}`,
       "channel": "#finance-alerts"
     }
     ```

2. **Lưu log sai số vào cơ sở dữ liệu**:
   - Thay vì chỉ ghi vào Google Sheets, các sếp có thể **append vào cơ sở dữ liệu** (MySQL, PostgreSQL) bằng node **`database`** để dễ dàng phân tích sau này.

3. **Tự động gửi báo cáo định kỳ**:
   - Sử dụng **node `email`** hoặc **node `google-drive`** để tự động tạo và gửi báo cáo Excel/PDF cho team tài chính mỗi cuối tháng.

4. **Tùy chỉnh prompt AI**:
   - Nếu AI giải thích không chính xác, các sếp có thể **tùy chỉnh prompt** để phù hợp với ngữ cảnh tài chính của công ty:
     ```
     "Treat this as a financial discrepancy. Provide a professional and concise explanation for the difference, including possible causes like transaction delays, currency conversion errors, or accounting misclassifications."
     ```

---

### 📌 **Kết luận**
Workflow này **giải phóng các sếp khỏi công việc thủ công mệt mỏi** trong hoà giải số dư tài khoản, đồng thời **cải thiện độ chính xác** nhờ trí tuệ nhân tạo. **Chỉ cần cấu hình 1 lần**, workflow sẽ hoạt động tự động hàng ngày, giúp các sếp **tập trung vào việc phân tích và quyết định** thay vì kiểm tra số liệu.

**Bắt tay vào tự động hóa ngay hôm nay!**
👉 [Tải workflow JSON](https://n8n.io/workflows/15061) và **cài đặt trên VPS** để bắt đầu. 🚀

---
**Cần hỗ trợ?** Đăng ký **hỗ trợ chuyên nghiệp** từ [WeblineIndia](https://weblineindia.com/) để tối ưu hóa workflow cho doanh nghiệp của các sếp!