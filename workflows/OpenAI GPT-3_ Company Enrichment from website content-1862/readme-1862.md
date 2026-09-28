---
title: "🚀 Tự Động Hóa Tăng Cường Thông Tin Doanh Nghiệp Từ Nội Dung Website Bằng AI (GPT-3) - Không Cần Code!"
description: "Workflow này tự động phân tích nội dung website của doanh nghiệp, sử dụng GPT-3 để trích xuất giá trị cốt lõi (value proposition) và cập nhật tự động vào Google Sheets. Giúp các sếp tiết kiệm 10+ giờ/tháng, đồng thời đảm bảo dữ liệu chính xác và cập nhật liên tục."
slug: "tieu-dong-hoa-tang-cuong-thong-tin-doanh-nghiep-bang-gpt-3"
tags: [n8n, automation, ai, marketing, sales, google-sheets, openai, no-code]
keywords: [tự động hóa marketing, gpt-3 n8n, trích xuất giá trị cốt lõi, google sheets automation, workflow n8n marketing]
---

# 🚀 **Tự Động Hóa Tăng Cường Thông Tin Doanh Nghiệp Từ Nội Dung Website Bằng AI (GPT-3)**

## **💡 Bạn đã từng phải làm gì?**
- **Phân tích hàng chục trang website** để tìm ra giá trị cốt lõi (value proposition) của doanh nghiệp?
- **Ghi chép thủ công** thông tin này vào Google Sheets hoặc Excel, mất nhiều thời gian và dễ sai sót?
- **Muốn cập nhật liên tục** nhưng không có thời gian để theo dõi mỗi thay đổi trên website?

Workflow này **giải quyết tất cả** bằng cách tự động:
✅ **Trích xuất nội dung** từ website (HTML)
✅ **Sử dụng GPT-3** để phân tích và tổng kết giá trị cốt lõi (value proposition) trong **25 từ hoặc ít hơn**
✅ **Cập nhật tự động** vào Google Sheets (hoặc bảng tính khác)
✅ **Hoạt động 24/7** mà không cần can thiệp của con người

Không cần **code**, không cần **hiểu sâu về AI** – chỉ cần **cài đặt và chạy**!

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 10+ giờ/tháng** so với cách làm thủ công.
- **Giá trị cốt lõi chính xác** do AI phân tích, không bị chủ quan như con người.
- **Cập nhật tự động** khi website thay đổi (không cần kiểm tra thủ công).
- **Dữ liệu tập trung** trên Google Sheets, dễ dàng chia sẻ với team marketing/sales.
- **Cá nhân hóa** thông tin cho từng khách hàng hoặc đối tác.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** (để sử dụng GPT-3):
   - API Key từ [OpenAI](https://platform.openai.com/account/api-keys) (miễn phí 5 triệu token/tháng).
   - **Lưu ý**: Nếu dùng tài khoản miễn phí, cần **kiểm tra ngân sách** để tránh bị cắt API.
2. **Tài khoản Google Sheets**:
   - File Google Sheets đã tạo sẵn với **bảng dữ liệu** để lưu kết quả (cấu trúc sau sẽ hướng dẫn).
   - **OAuth 2.0 Credentials** từ [Google Cloud Console](https://console.cloud.google.com/) (để kết nối với Google Sheets).
3. **Website cần phân tích**:
   - URL của website (hoặc danh sách URL) cần trích xuất nội dung.
   - **Lưu ý**: Workflow hiện tại hỗ trợ **1 website/lần**, nhưng có thể mở rộng cho nhiều website bằng cách **tự động hóa trigger** (xem phần Mẹo & Gợi ý Nâng Cao).
4. **n8n Self-hosted** (không dùng phiên bản miễn phí trên cloud):
   - **👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - **👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (ổn định cho workflow AI).

---

## **🚀 Cách Import & Lưu ý khi "Lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/1862](https://n8n.io/workflows/1862) (chọn **Export as JSON**).
2. **Mở n8n Editor** (trên VPS hoặc phiên bản self-hosted).
3. **Nhấp vào "Import"** → Chọn file JSON vừa tải → **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/1862](https://n8n.io/workflows/1862) (chọn **Export as JSON**).
2. **Mở n8n Editor** → **Nhấp vào "Import"** → **Chọn "Paste JSON"** → Dán và **Import**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này có **11 node**, nhưng **3 node quan trọng nhất** cần cấu hình cẩn thận:

#### **🔹 Node 1: Manual Trigger (Bắt đầu workflow)**
- **Không cần chỉnh gì**, chỉ cần nhấp vào **"Execute Workflow"** khi muốn chạy.

#### **🔹 Node 2: HTTP Request (Trích xuất nội dung website)**
- **Tham số cần điền**:
  - **Method**: `GET`
  - **URL**: `= $input["websiteUrl"]` (đây là **input từ node Manual Trigger**).
    - **Lưu ý**: Nếu muốn **nhập URL trực tiếp**, thay bằng:
      ```json
      "https://example.com"
      ```
  - **Headers**:
    - `Accept`: `text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8`
    - `User-Agent`: `Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36`

#### **🔹 Node 3: HTML Extract (Lọc nội dung chính)**
- **Tham số cần chỉnh**:
  - **Selector**: `body` (lấy toàn bộ nội dung HTML của trang).
  - **Limit**: `10000` (để tránh nội dung quá dài).
  - **Output**: Chọn `content` (nội dung HTML sau khi lọc).

#### **🔹 Node 4: OpenAI (Phân tích bằng GPT-3)**
- **Tham số cần điền**:
  - **Credentials**: Chọn `openAiApi` (đã cấu hình trước khi import).
  - **Prompt** (đã sẵn trong workflow, nhưng có thể tùy chỉnh):
    ```json
    "=This is the content of the website {{ $node["Split In Batches"].json["Domain"] }}:\"{{ $json["contentShort"] }}\"\n\nIn a JSON format:\n\n- Give me the value proposition of the company. In less than 25 words. In English. Casual Tone. Format is: \"[Company Name] helps [target audience] [achieve desired result]\"\n\n- What are the 3 main services/products? List them in bullet points.\n\n- What is the unique selling point (USP) of the company? In 1-2 sentences."
    ```
  - **Model**: `text-davinci-003` (hoặc `gpt-3.5-turbo` nếu muốn tiết kiệm chi phí).
  - **Temperature**: `0.7` (để kết quả không quá ngẫu nhiên).

#### **🔹 Node 5: Google Sheets (Cập nhật kết quả)**
- **Tham số cần chỉnh**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.
  - **Spreadsheet ID**: ID của file Google Sheets (tìm trong URL của file: `https://docs.google.com/spreadsheets/d/[SPREADSHEET_ID]/edit`).
  - **Sheet Name**: Tên sheet cần cập nhật (ví dụ: `DoanhNghiep`).
  - **Range**: `A1` (để cập nhật từ ô A1).
  - **Operation**: `update` (để ghi đè hoặc thêm mới).
  - **Values**: Chọn `JSON` từ node **Parse JSON** (node thứ 9).

#### **🔹 Node 6: Code (Clean Content & Parse JSON)**
- **Node "Clean Content"**:
  - **Mã JavaScript** (đã sẵn trong workflow, nhưng có thể chỉnh):
    ```javascript
    return {
      contentShort: $input.all()[0].json.content.replace(/<[^>]*>/g, '').trim().substring(0, 2000)
    };
    ```
  - **Nghĩa**: Lọc bỏ thẻ HTML và giữ lại **2000 ký tự đầu tiên** của nội dung.
- **Node "Parse JSON"**:
  - **Mã JavaScript** (để chuyển kết quả OpenAI thành JSON):
    ```javascript
    const response = $input.all()[0].json;
    const jsonResponse = JSON.parse(response.choices[0].text);
    return {
      json: jsonResponse
    };
    ```

---

### **3. Kích hoạt ⚡️**
1. **Test Run** (để kiểm tra workflow hoạt động):
   - Nhập **URL website** vào node **HTTP Request**.
   - Chạy workflow và kiểm tra kết quả trên **Google Sheets**.
2. **Bật Active**:
   - Nhấp vào **toggle "Active"** ở góc trên bên phải → **Workflow sẽ chạy tự động** khi nhấn **"Execute Workflow"**.

---

## **✍️ Mẹo & Gợi ý Nâng Cao**

### **🔹 Mở rộng cho nhiều website**
- **Sử dụng node "Split In Batches"** để chia danh sách URL thành nhiều batch.
- **Kết hợp với Webhook** (thay vì Manual Trigger) để tự động chạy khi có thay đổi trên website (ví dụ: sử dụng **n8n-nodes-base.webhook**).

### **🔹 Lưu log hoạt động**
- **Thêm node "Set"** sau node **OpenAI** để lưu kết quả vào biến:
  ```json
  {
    "json": {
      "website": $input["websiteUrl"],
      "valueProposition": $input["json"]["valueProposition"],
      "services": $input["json"]["services"],
      "timestamp": new Date().toISOString()
    }
  }
  ```
- **Kết nối với Slack/Telegram** để thông báo khi workflow hoàn thành.

### **🔹 Tự động hóa định kỳ**
- **Sử dụng node "Schedule"** (n8n Pro) để chạy workflow hàng ngày/tuần.
- **Ví dụ**: Chạy vào **8h sáng hàng ngày** để cập nhật thông tin mới nhất.

### **🔹 Tùy chỉnh prompt cho mục đích cụ thể**
- Nếu muốn **trích xuất thông tin khác** (ví dụ: danh sách khách hàng, giá sản phẩm), chỉnh sửa **prompt** trong node OpenAI:
  ```json
  "=Analyze the website content of {{ $node["Split In Batches"].json["Domain"] }} and extract:\n\n1. List of 5 main customers/clients (if any).\n2. Pricing range for their services/products.\n3. Any recent news or updates (last 6 months).\n\nFormat the response in JSON."
  ```

---

## **📌 Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc **phân tích website thủ công**, đồng thời **cập nhật dữ liệu chính xác** vào Google Sheets. **Không cần code**, **không cần chuyên gia AI** – chỉ cần **cài đặt và chạy**!

**🚀 Hành động ngay:**
1. **Đăng ký VPS** để self-host n8n (để workflow hoạt động 24/7).
2. **Import workflow** và **cấu hình** theo hướng dẫn.
3. **Nhấn "Execute Workflow"** và **nhận kết quả tự động**!

**💬 Cần hỗ trợ?** Để lại comment bên dưới hoặc liên hệ với cộng đồng n8n trên [Discord](https://discord.gg/n8n). Chúc các sếp thành công! 🎉