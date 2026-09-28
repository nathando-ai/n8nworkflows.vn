---
title: "🚀 Tự Động Hóa Tìm Kiếm Lead Cục Bộ & Gửi Email Lạnh AI với Apify, Gmail & AI (N8n)"
description: "Workflow tự động hóa tìm kiếm lead địa phương từ các ngành nghề cụ thể, trích xuất email hợp lệ, và gửi email lạnh cá nhân hóa 100% không cần code. Giúp các sếp tiết kiệm 10+ giờ/ngày và tăng tỷ lệ chuyển đổi lead lên 30%."
slug: "tieu-dong-hoa-tim-kiem-lead-cuc-bo-va-email-lanh-ai"
tags: [n8n, automation, no-code, content-creation, multimodal-ai, gmail-automation, lead-generation]
keywords: [n8n workflow tìm kiếm lead, tự động hóa email lạnh, apify với n8n, ai chat gemini openai, tự động hóa gmail, tìm kiếm lead địa phương]
---

# 🚀 **Tự Động Hóa Tìm Kiếm Lead Cục Bộ & Gửi Email Lạnh AI: Giải Pháp "Không Code" Cho Doanh Nghiệp**

### **Nỗi Đau Của Các Sếp Hiện Nay**
Bạn đã bao giờ phải:
- **Tốn thời gian** tìm kiếm lead thủ công trên Google, Apify, hoặc các công cụ tìm kiếm địa phương?
- **Không biết email nào là hợp lệ** để liên hệ (tránh email @gmail.com, @yahoo.com, hoặc inbox không tồn tại)?
- **Gửi email lạnh một cách ngẫu nhiên**, dẫn đến tỷ lệ phản hồi thấp (<5%)?
- **Phải update dữ liệu lead** mỗi khi có thay đổi, mất công kiểm tra trùng lặp?

**Workflow này giải quyết tất cả!** Với sự kết hợp giữa **Apify** (tìm kiếm lead), **AI Gemini/OpenAI** (trích xuất email), và **Gmail Automation**, bạn sẽ:
✅ **Tìm kiếm lead địa phương** theo ngành nghề, địa điểm, và số lượng mong muốn (với Apify).
✅ **Trích xuất email hợp lệ** từ website của doanh nghiệp (không phải email @gmail.com).
✅ **Gửi email lạnh cá nhân hóa** với subject/body tự động tạo bằng AI.
✅ **Lưu log và update trạng thái** trên Google Sheets để theo dõi hiệu quả.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của n8n.cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/ngày**: Không cần tìm kiếm lead thủ công.
- **Tỷ lệ lead hợp lệ cao**: Trích xuất email từ website chính thức (không phải email cá nhân).
- **Email lạnh cá nhân hóa**: Subject/body tự động tạo dựa trên ngành nghề và email style.
- **Hoạt động 24/7**: Workflow tự động chạy sau khi cấu hình, không cần can thiệp.
- **Theo dõi hiệu quả**: Dữ liệu lead và trạng thái gửi được lưu trên Google Sheets.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Apify** (để tìm kiếm lead địa phương).
2. **API Key của Google Sheets** (để lưu lead và log).
3. **Tài khoản Gmail** (để gửi email lạnh).
4. **API Key của OpenAI** (để sử dụng GPT-4.1-mini) **hoặc** **API Key của Google Gemini** (lựa chọn tùy ý).
5. **Google Sheet** để lưu trữ lead (cấu trúc gồm cột: Company, Category, Website, Phone, Address, Email, Status).
6. **Mô hình email style** (ví dụ: "Chào [Tên], tôi là [Tên], và tôi thấy [Doanh nghiệp] có [Giá trị]...").

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/8986](https://n8n.io/workflows/8986) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n Editor.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **4 bước chính**, các sếp cần chú ý đến các node sau:

##### **🔹 STEP 1: Intake & Search (Tìm Kiếm Lead)**
- **Node "On form submission" (formTrigger)**:
  - Cấu hình **form** để nhập:
    - **Business Type** (ngành nghề, ví dụ: "Cafe", "Lâu đài du lịch").
    - **Location** (địa điểm, ví dụ: "Hà Nội", "Đà Nẵng").
    - **Lead Number** (số lượng lead muốn tìm).
    - **Email Style** (mô hình email, ví dụ: "Chào [Tên], tôi là [Tên]...").
- **Node "HTTP Request" (httpRequest)**:
  - **URL**: `https://api.apify.com/v2/actors/your-apify-actor/run` (thay bằng actor Apify của bạn).
  - **Headers**:
    - `Authorization`: `Bearer YOUR_APIFY_API_TOKEN`
    - `Content-Type`: `application/json`
  - **Body**:
    ```json
    {
      "input": {
        "businessType": "{{$node["On form submission"].json()["businessType"]}}",
        "location": "{{$node["On form submission"].json()["location"]}}",
        "limit": "{{$node["On form submission"].json()["leadNumber"]}}"
      }
    }
    ```
  - **Lưu ý**: Đăng ký **actor Apify** miễn phí tại [Apify](https://apify.com) và lấy token API từ [Dashboard Apify](https://apify.com/dashboard/tokens).

##### **🔹 STEP 2: Website & Email Extraction (Trích Xuất Email)**
- **Node "Filter"**:
  - Lọc dữ liệu để chỉ giữ các lead có **website** (tránh lead không có trang web).
- **Node "Information Extractor"**:
  - **Prompt AI** (sử dụng **Google Gemini** hoặc **OpenAI**):
    ```
    Trích xuất email chính thức từ trang web: {{$node["HTTP Request"].json()["website"]}}.
    Đảm bảo email là inbox cá nhân (không phải @gmail.com, @yahoo.com, hoặc email chung như info@).
    Nếu không tìm thấy email, trả về null.
    ```
  - **Lưu ý**: Cấu hình **credentials** là `googlePalmApi` (Gemini) hoặc `openAiApi` (OpenAI).

##### **🔹 STEP 3: Validate & Persist (Xác Minh & Lưu Dữ Liệu)**
- **Node "If"**:
  - Kiểm tra email có chứa `@` (đảm bảo email hợp lệ).
- **Node "Append row in sheet"**:
  - **Google Sheet Name**: Thay bằng tên sheet của bạn.
  - **Range**: `Sheet1!A1` (đảm bảo có cột: Company, Category, Website, Phone, Address, Email).
  - **Lưu ý**: Đặt `matchingColumns` = `Email` để tránh trùng lặp.

##### **🔹 STEP 4: Outreach & Logging (Gửi Email & Log)**
- **Node "Loop Over Items" (splitInBatches)**:
  - **Batch Size**: 1 (để gửi email một lúc một lead).
  - **Delay**: 5000ms (5 giây giữa mỗi email để tránh bị flag spam).
- **Node "Information Extractor1"**:
  - **Prompt AI** để tạo subject/body email:
    ```
    Tạo email lạnh cá nhân hóa cho lead: {{$node["Append row in sheet"].json()["Company"]}}.
    Sử dụng email style: "{{$node["On form submission"].json()["emailStyle"]}}".
    Subject: "Chào [Tên Doanh Nghiệp], tôi là [Tên] và tôi thấy [Giá trị]..."
    Body: "Thân mến [Tên Doanh Nghiệp], tôi là [Tên], và tôi đang tìm kiếm [Giá trị] cho khách hàng của bạn..."
    ```
- **Node "Send a message" (gmail)**:
  - **To**: `{{$node["Information Extractor1"].json()["email"]}}`
  - **Subject**: `{{$node["Information Extractor1"].json()["subject"]}}`
  - **Body**: `{{$node["Information Extractor1"].json()["body"]}}`
  - **Lưu ý**: Nếu body có markup HTML, chuyển sang **HTML Mode**.
- **Node "Append or update row in sheet"**:
  - **Cột Status**: Đặt thành `"✅ Sent"` và thêm **Send Time**.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhập dữ liệu mẫu vào **formTrigger** và chạy workflow.
   - Kiểm tra **Google Sheets** và **Gmail** để xác nhận email đã gửi thành công.
2. **Bật Active**:
   - Chuyển trạng thái workflow từ **Inactive** sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** để thông báo khi email được gửi thành công.
2. **Lưu Log Chi Tiết**:
   - Thêm cột **Response** vào Google Sheets để ghi lại phản hồi từ lead.
3. **Tự Động Xóa Lead Trùng Lặp**:
   - Sử dụng **Google Apps Script** để tự động xóa lead trùng lặp hàng tuần.
4. **Tối Ưu Hóa AI**:
   - Thử nghiệm **prompt khác** để cải thiện tỷ lệ trích xuất email (ví dụ: yêu cầu AI loại bỏ email @gmail.com).
5. **Gửi Email Theo Thời Gian**:
   - Sử dụng **node `dateTime`** để gửi email vào giờ làm việc (ví dụ: 9h-17h).

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa **tìm kiếm lead địa phương** và **gửi email lạnh cá nhân hóa** mà **không cần viết một dòng code**. Với sự hỗ trợ của **Apify, AI Gemini/OpenAI, và Gmail**, bạn sẽ:
✔ **Tiết kiệm thời gian** để tập trung vào chiến lược bán hàng.
✔ **Tăng tỷ lệ phản hồi** nhờ email cá nhân hóa.
✔ **Theo dõi hiệu quả** một cách dễ dàng trên Google Sheets.

**Hãy import workflow ngay hôm nay và bắt đầu tự động hóa lead của mình!** 🚀

---
**💡 Lưu ý cuối cùng**:
- Nếu gặp lỗi **API rate limit**, hãy tăng **delay** trong node `splitInBatches`.
- Để tránh bị **Gmail flag spam**, hãy gửi email từ một tài khoản mới hoặc sử dụng **Gmail API** thay vì OAuth2.