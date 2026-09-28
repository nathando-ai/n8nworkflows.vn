---
title: "💰 Tự Động Hóa Ghi Chép Giao Dịch & Tạo Báo Cáo Ngân Sách với Gemini AI, Telegram & Firefly III (Không Cần Code)"
description: "Workflow tự động hóa ghi nhận giao dịch từ ảnh/PDF gửi qua Telegram, phân tích thông tin bằng Gemini AI, và tự động đăng ký vào Firefly III. Kết hợp với tính năng báo cáo ngân sách tháng hiện tại chỉ bằng cách gửi từ khóa 'Report'."
slug: "tu-dong-hoa-ghi-chép-giao-dịch-voi-gemini-telegram-firefly"
tags: [n8n, automation, no-code, ai-chatbot, firefly-iii, gemini-ai, telegram-bot]
keywords: [tự động hóa ghi chép giao dịch, gemini ai n8n, firefly iii automation, telegram bot ghi chép, báo cáo ngân sách tự động]
---

# 🚀 **Tự Động Hóa Ghi Chép Giao Dịch & Tạo Báo Cáo Ngân Sách với Gemini AI, Telegram & Firefly III**

### **Giải Pháu Nỗi Đau Của Các Sếp:**
Hàng ngày, các sếp phải mất **30-60 phút** để:
- **Ghi chép thủ công** giao dịch từ hóa đơn, ảnh screenshot, hoặc file PDF.
- **Nhập liệu vào Firefly III** một cách chậm chạp và dễ mắc lỗi.
- **Tính toán ngân sách tháng** bằng Excel, mất thời gian và dễ sai sót.
- **Không có báo cáo tự động** để theo dõi chi tiêu thực tế so với kế hoạch.

**Workflow này tự động hóa toàn bộ quy trình chỉ bằng một cú nhấp chuột!** Khi gửi **ảnh hóa đơn, PDF, hoặc từ khóa "Report"** qua Telegram, hệ thống sẽ:
✅ **Phân tích tự động** thông tin từ ảnh/PDF bằng **Gemini AI**.
✅ **Ghi chép giao dịch** vào Firefly III một cách chính xác.
✅ **Tạo báo cáo ngân sách tháng** chỉ bằng cách gửi từ khóa "Report".
✅ **Gửi xác nhận** qua Telegram cho từng giao dịch được xử lý.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ xử lý nhanh cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 50% thời gian** so với ghi chép thủ công.
- **Chính xác 100%** nhờ AI phân tích tự động từ ảnh/PDF.
- **Báo cáo ngân sách tự động** mỗi khi cần (chỉ gửi "Report").
- **Hoạt động liên tục** 24/7, không phụ thuộc vào thời gian làm việc.
- **Kết nối đa nền tảng**: Telegram (gửi dữ liệu), Firefly III (lưu trữ), Gemini AI (phân tích).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Telegram** (để gửi ảnh/PDF và nhận kết quả).
✔ **API Key Telegram Bot** (tạo tại [@BotFather](https://t.me/BotFather)).
✔ **Tài khoản Firefly III** (để lưu trữ giao dịch).
✔ **OAuth2 Credential cho Firefly III** (cài đặt theo [hướng dẫn](https://docs.firefly-iii.org/how-to/firefly-iii/features/api/#create-an-oauth2-client)).
✔ **API Key Google Gemini** (đăng ký tại [Google AI Studio](https://makersuite.google.com/)).
✔ **Domain Firefly III** (ví dụ: `https://firefly.tinohost.vn`).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/11339](https://n8n.io/workflows/11339) và import vào **n8n Editor**.
- **Copy JSON** từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **17 node** quan trọng, các sếp cần cấu hình kỹ lưỡng:

##### **A. Cấu Hình Telegram (Gửi & Nhận Dữ liệu)**
- **Node "Transaction Image or PDF Received"** (TelegramTrigger):
  - Chọn **credentials** là `telegramApi` (đã tạo từ BotFather).
  - Chọn **chat ID** là nhóm/channel Telegram muốn nhận dữ liệu.
- **Node "Get file from server" & "Get image from server"** (Telegram):
  - Chọn cùng **credentials** `telegramApi`.
  - Đảm bảo **file permission** cho bot đọc file từ Telegram.

##### **B. Cấu Hình Gemini AI (Phân Tích Ảnh/PDF)**
- **Node "Analyze the image or pdf"** (googleGemini):
  - Chọn **credentials** `googlePalmApi` (API Key Gemini).
  - Chọn **model** phù hợp (ví dụ: `gemini-pro`).
  - **Customize Prompt** (nếu cần):
    ```json
    {
      "role": "user",
      "content": "Analyze this transaction document and extract: Date, Amount, Payee, Category, Description. Return in JSON format."
    }
    ```
- **Node "Analyzer Scraper"** (lmChatGoogleGemini):
  - Cấu hình tương tự như node trên, nhưng dùng để **tái xác nhận** dữ liệu.

##### **C. Cấu Hình Firefly III (Lưu Giao Dịch)**
- **Node "Post to Firefly"** (httpRequest):
  - Chọn **credentials** `oAuth2Api` (đã tạo từ Firefly).
  - Điền **URL Firefly** (ví dụ: `https://firefly.tinohost.vn/api/v1/transactions`).
  - **Headers** cần thiết:
    ```json
    {
      "Authorization": "Bearer {{ $json["access_token"] }}",
      "Content-Type": "application/json"
    }
    ```
  - **Body** (dữ liệu gửi lên Firefly):
    ```json
    {
      "date": "{{ $node["Analyze the image or pdf"].json()["date"] }}",
      "amount": "{{ $node["Analyze the image or pdf"].json()["amount"] }}",
      "payee": "{{ $node["Analyze the image or pdf"].json()["payee"] }}",
      "category": "{{ $node["Parse details & add category"].json()["category"] }}",
      "description": "{{ $node["Analyze the image or pdf"].json()["description"] }}"
    }
    ```
- **Node "Get Remaining Budget"** (httpRequest):
  - Gửi yêu cầu API để lấy **ngân sách còn lại** của tháng.
  - URL ví dụ: `https://firefly.tinohost.vn/api/v1/budgets`.

##### **D. Cấu Hình Báo Cáo Ngân Sách (Tính Toán & Gửi CSV)**
- **Node "Parse JSON"** (code):
  - Chuyển đổi dữ liệu từ Gemini thành **dạng JSON chuẩn** cho Firefly.
  - Mẫu code (cần chỉnh sửa theo cấu trúc dữ liệu cụ thể):
    ```javascript
    return {
      json: {
        transactions: $input.all().map(item => ({
          date: item.json.date,
          amount: item.json.amount,
          payee: item.json.payee,
          category: item.json.category
        }))
      }
    };
    ```
- **Node "Make CSV"** (convertToFile):
  - Chuyển dữ liệu thành **file CSV** để gửi qua Telegram.
  - **Headers CSV**:
    ```
    Date,Amount,Payee,Category
    ```
- **Node "Send CSV"** (telegram):
  - Gửi file CSV về Telegram với **operation = "sendDocument"**.
  - **Caption** có thể là: `Báo cáo ngân sách tháng {{ $date.now("MMMM YYYY") }}`.

##### **E. Cấu Hình Tự Động Hóa (Switch & Loop)**
- **Node "Switch"** (switch):
  - Chuyển hướng logic nếu gửi **từ khóa "Report"** (tạo báo cáo) hoặc **ảnh/PDF** (ghi chép giao dịch).
- **Node "Loop for Multiple Items"** (splitInBatches):
  - Chia **nhiều giao dịch** thành batch để xử lý hiệu quả.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run** với **dữ liệu mẫu**:
  - Gửi **ảnh hóa đơn** hoặc **PDF** qua Telegram.
  - Kiểm tra **Firefly III** có ghi chép giao dịch không.
  - Gửi **từ khóa "Report"** để kiểm tra báo cáo ngân sách.
- **Bật Active** workflow sau khi kiểm tra thành công.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối với Slack/Email**:
   - Thêm **node Slack** hoặc **node Email** để gửi **báo cáo định kỳ** (ví dụ: cuối tháng).
   - Mẫu code cho Slack:
     ```javascript
     return {
      json: {
        text: `📊 Báo cáo ngân sách tháng ${$date.now("MMMM YYYY")}:\n- Tổng chi tiêu: ${{ $input.all().reduce((sum, item) => sum + item.json.amount, 0) }}`
      }
    };
     ```

2. **Lưu Log Dữ Liệu**:
   - Thêm **node Database (PostgreSQL/MySQL)** để lưu **lịch sử giao dịch** dài hạn.
   - Sử dụng **node Set** để lưu trữ dữ liệu vào cơ sở dữ liệu.

3. **Tự Động Xóa File Tạm**:
   - Sau khi xử lý xong, **xóa file ảnh/PDF** từ Telegram để tiết kiệm dung lượng.

4. **Cập Nhật Thông Tin Ngân Sách**:
   - Kết nối với **Google Sheets** để **cập nhật ngân sách thực tế** tự động.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc **ghi chép giao dịch và báo cáo ngân sách** bằng cách tự động hóa toàn bộ quy trình với **Gemini AI, Telegram, và Firefly III**.

**Hành động ngay:**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Test với dữ liệu mẫu** và bật **Active workflow**.
4. **Gửi ảnh hóa đơn/PDF hoặc từ khóa "Report"** qua Telegram để trải nghiệm!

**🚀 Hãy tự động hóa ngay hôm nay và tiết kiệm thời gian cho công việc quan trọng hơn!**