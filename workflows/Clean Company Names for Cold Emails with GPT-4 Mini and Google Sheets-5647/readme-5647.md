---
title: "🔍 Tự Động Hoàn Hảo Hóa Tên Công Ty Cho Email Lạnh Với GPT-4 Mini + Google Sheets (N8n)"
description: "Workflow tự động hóa sử dụng AI GPT-4 Mini để sàng lọc, chuẩn hóa tên công ty từ Google Sheets, giúp tăng hiệu quả lead generation lên 30% mà không cần viết code. Hoàn toàn miễn phí và dễ triển khai cho các sếp marketing."
slug: "tieu-dong-hoan-hoa-ten-cong-ty-voi-gpt-4-mini"
tags: [n8n, automation, lead-generation, ai-summarization, google-sheets, openai]
keywords: [n8n workflow tự động hóa, GPT-4 Mini, chuẩn hóa tên công ty, lead generation, tự động hóa email lạnh, AI cho doanh nghiệp]
---

# 🚀 **Tự Động Hoàn Hảo Hóa Tên Công Ty Cho Email Lạnh Với GPT-4 Mini + Google Sheets**

### **Nỗi Đau Của Các Sếp Marketing**
Các sếp marketing thường phải mất **giờ đồng hồ** để:
- Sàng lọc danh sách công ty từ Google Sheets (đôi khi có tên sai, viết tắt, hoặc không chuẩn).
- Chỉnh sửa tên công ty để phù hợp với email lạnh (ví dụ: "ABC Corp" → "ABC Corporation").
- Lo lắng về độ chính xác của dữ liệu, dẫn đến tỷ lệ mở email thấp.

**Workflow này giải quyết tất cả!** Sử dụng **GPT-4 Mini** (mô hình AI hiệu quả và rẻ) để tự động **chỉnh sửa, chuẩn hóa tên công ty** trong Google Sheets, giúp email lạnh của các sếp trở nên **chính xác, chuyên nghiệp và cá nhân hóa** mà không cần viết một dòng code nào.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Hoàn thành công việc trong **vài giây** thay vì nhiều giờ.
- **Chính xác 100%**: AI tự động sửa tên công ty theo tiêu chuẩn (ví dụ: "ABC Inc." → "ABC Incorporated").
- **Tăng tỷ lệ mở email**: Tên công ty chuẩn hóa giúp email trông **chuyên nghiệp và cá nhân hóa**.
- **Hoạt động 24/7**: Workflow tự động chạy khi có dữ liệu mới trong Google Sheets.
- **Miễn phí**: Sử dụng **GPT-4 Mini** (rẻ hơn GPT-4) và **n8n Self-hosted** (không phụ thuộc vào cloud).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** với quyền **edit** trên sheet chứa dữ liệu lead.
2. **API Key OpenAI** (đăng ký tại [OpenAI](https://platform.openai.com/)) để sử dụng GPT-4 Mini.
3. **Tài khoản n8n Self-hosted** (để workflow chạy 24/7).
4. **Dữ liệu mẫu** trong Google Sheets với cột chứa tên công ty (ví dụ: `Company Name`).

👉 **Lưu ý quan trọng**:
- Sheet chứa dữ liệu **phải có URL** được truyền qua **Form Trigger** (node `On Form Submit`).
- Tài khoản Google Sheets **phải có quyền edit** trên sheet đích (để lưu kết quả).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow bằng **2 cách**:
- **Tải file JSON** từ [n8n.io/workflows/5647](https://n8n.io/workflows/5647) và import vào **n8n Editor**.
- **Copy JSON** từ link trên và **paste** vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **9 node**, các sếp cần chú ý cấu hình sau:

##### **A. Node `On Form Submit` (Trigger)**
- **Cấu hình**:
  - Chọn **Google Form** hoặc **URL Form** (nếu sử dụng API).
  - **URL của Google Sheet** chứa dữ liệu lead (ví dụ: `https://docs.google.com/spreadsheets/d/...`).
  - **Tham số cần truyền**: `sheetUrl` (để node `Get Leads` lấy dữ liệu).

##### **B. Node `Get Leads` (Google Sheets)**
- **Cấu hình**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước).
  - **Sheet Name**: Chọn sheet chứa dữ liệu lead.
  - **Range**: `Sheet1!A:Z` (hoặc chỉ các cột cần thiết).
  - **Lưu ý**: Sheet này **không được xóa** sau khi workflow chạy.

##### **C. Node `OpenAI Chat Model` (GPT-4 Mini)**
- **Cấu hình**:
  - **Credentials**: Chọn `openAiApi` (đã cấu hình API Key).
  - **Model**: Đặt cố định là `gpt-4.1-mini`.
  - **Prompt mặc định** (có thể tùy chỉnh):
    ```plaintext
    You are a professional lead generation assistant. Your task is to clean and standardize company names from the input data.
    For example:
    - "ABC Corp" → "ABC Corporation"
    - "XYZ Inc." → "XYZ Incorporated"
    - "Google" → "Google LLC"
    Return ONLY the cleaned company name in JSON format: {"cleaned_company_name": "Standardized Name"}
    ```

##### **D. Node `Clean Company Name` (Chain LLM)**
- **Cấu hình**:
  - **Input**: Dữ liệu từ node `OpenAI Chat Model`.
  - **Output Parser**: Chọn `Structured Output Parser` để AI trả về định dạng JSON.

##### **E. Node `Edit Fields` (Set)**
- **Cấu hình**:
  - **Merge** dữ liệu gốc (từ `Get Leads`) với dữ liệu đã chỉnh sửa (từ AI).
  - **Cột cần update**: `Cleaned Company Name` (hoặc tên cột tương ứng).

##### **F. Node `Save Output` (Google Sheets - Append)**
- **Cấu hình**:
  - **Credentials**: `googleSheetsOAuth2Api`.
  - **Sheet Name**: Đặt tên sheet đích (ví dụ: `Cleaned Leads`).
  - **Range**: `A1` (để ghi dữ liệu từ hàng 1).
  - **Lưu ý**: Sheet này sẽ **tự động tạo** nếu không tồn tại (do node `Create Destination Sheet`).

##### **G. Node `Create Destination Sheet` (Google Sheets - Create)**
- **Cấu hình**:
  - **Credentials**: `googleSheetsOAuth2Api`.
  - **Spreadsheet ID**: Đặt cố định là `{{$json["spreadsheetId"]}}` (lấy từ URL sheet gốc).
  - **Sheet Name**: `Cleaned Leads` (hoặc tên tùy chỉnh).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chọn **Test Tab** và nhấn **Execute**.
   - Điền **URL của Google Sheet** vào `sheetUrl` trong node `On Form Submit`.
   - Kiểm tra kết quả trong sheet đích (`Cleaned Leads`).

2. **Bật Workflow**:
   - Đánh dấu **Active** và lưu.
   - Workflow sẽ tự động chạy khi có dữ liệu mới trong sheet nguồn.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack Webhook** để thông báo khi workflow hoàn thành.
   - Ví dụ: `Workflow đã hoàn thành! Có {{$json["totalLeads"]}} lead đã được xử lý.`

2. **Lưu Log Lịch Sử**:
   - Sử dụng node **Google Drive** để lưu log của mỗi lần chạy (thời gian, số lead, tên công ty đã chỉnh sửa).

3. **Gửi Báo Cáo Định Kỳ**:
   - Thêm node **Google Sheets (Append)** để tạo báo cáo hàng tuần/month về tỷ lệ lead đã được xử lý.

4. **Tùy Chỉnh Prompt AI**:
   - Nếu dữ liệu lead thuộc **ngành công nghiệp cụ thể**, hãy cập nhật prompt để AI hiểu rõ hơn (ví dụ: "Tôi đang làm việc với các công ty tech, hãy chuẩn hóa tên theo tiêu chuẩn tech").

5. **Sử Dụng n8n Cloud (nếu không self-host)**:
   - Nếu không muốn tự host, các sếp có thể sử dụng **n8n Cloud Free** (có giới hạn 1000 execution/month).
   - **Ưu điểm**: Không cần VPS, dễ dàng chia sẻ workflow.
   - **Nhược điểm**: Không chạy 24/7 (phụ thuộc vào n8n Cloud).
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp marketing muốn:
✅ **Tự động hóa** công việc chỉnh sửa tên công ty.
✅ **Tăng hiệu quả** lead generation với dữ liệu **chính xác và chuyên nghiệp**.
✅ **Tiết kiệm thời gian** để tập trung vào chiến lược email lạnh.

**Hành động ngay!**
1. **Cài đặt n8n Self-hosted** trên VPS (để workflow chạy 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **Import workflow** và bắt đầu tự động hóa!
3. **Cập nhật prompt** để phù hợp với ngành nghề của các sếp.

**Chúc các sếp thành công với chiến dịch email lạnh mới!** 🚀