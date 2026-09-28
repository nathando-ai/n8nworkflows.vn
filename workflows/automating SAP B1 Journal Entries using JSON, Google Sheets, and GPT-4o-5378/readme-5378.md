---
title: "🚀 Tự Động Hóa Nhập Sổ Cái SAP B1 Bằng JSON, Google Sheets & GPT-4o – Giải Pháp Không Code Cho Kế Toán"
description: "Giải quyết thủ công nhập sổ cái SAP B1 bằng cách tự động hóa quá trình từ JSON, Google Sheets đến API SAP, với AI GPT-4o tự động hóa tổng kết và kiểm tra dữ liệu. Tiết kiệm 80% thời gian kiểm tra và giảm sai sót cho bộ phận kế toán."
slug: "tu-dong-hoa-sap-b1-nhap-so-cai-json-gpt-4o"
tags: [n8n, automation, SAP B1, Google Sheets, AI, GPT-4o, kế toán tự động hóa]
keywords: [tự động hóa SAP B1, nhập sổ cái SAP không code, GPT-4o tổng kết báo cáo, Google Sheets + n8n, giảm thời gian kế toán]
---

# 🚀 **Tự Động Hóa Nhập Sổ Cái SAP B1 Bằng JSON, Google Sheets & GPT-4o**

### **Giải pháp không code cho kế toán: Từ dữ liệu thô đến sổ cái chính xác chỉ trong vài giây**
Bạn đã bao giờ phải **nhập hàng trăm dòng sổ cái SAP B1 thủ công** mỗi ngày? Hay phải **kiểm tra lại dữ liệu** để tránh sai sót gây ảnh hưởng đến báo cáo tài chính? Với workflow này, các sếp sẽ **tự động hóa toàn bộ quy trình** từ **JSON, Google Sheets đến API SAP**, với sự hỗ trợ của **GPT-4o** để tổng kết và kiểm tra dữ liệu một cách chính xác và nhanh chóng.

Không cần viết một dòng code, chỉ cần **cấu hình và chạy**, workflow sẽ:
✅ **Nhập sổ cái SAP B1 từ JSON hoặc Google Sheets** một cách tự động.
✅ **Sử dụng GPT-4o để tổng kết và kiểm tra logic** của các dòng nhập.
✅ **Ghi log thành công/thất bại lên Google Sheets** để theo dõi.
✅ **Giảm thời gian nhập sổ cái từ 80%**, đồng thời **minim hóa sai sót** do con người gây ra.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian nhập sổ cái**: Không cần nhập thủ công hàng trăm dòng.
- **Chính xác 100%**: GPT-4o tự động kiểm tra logic và tổng kết dữ liệu.
- **Hoạt động 24/7**: Workflow chạy tự động khi có dữ liệu mới từ JSON hoặc Google Sheets.
- **Ghi log toàn bộ quá trình**: Theo dõi thành công/thất bại trên Google Sheets.
- **Cá nhân hóa cho từng doanh nghiệp**: Dễ dàng điều chỉnh cấu trúc sổ cái theo yêu cầu.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản SAP B1** với quyền truy cập API (để lấy token và cấu hình `SAP Login`).
2. **Google Sheets** với:
   - Một **bảng dữ liệu mẫu** (cấu trúc sẽ được hướng dẫn sau).
   - **API Key Google Sheets** (tạo tại [Google Cloud Console](https://console.cloud.google.com/)).
3. **API Key OpenAI** (để sử dụng GPT-4o trong `LLM Transform`).
4. **URL Webhook** (để nhận dữ liệu từ bên ngoài hoặc tự động kích hoạt workflow).
5. **VPS n8n** (để chạy workflow 24/7):
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Workflow được cung cấp dưới dạng **JSON**. Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/5378](https://n8n.io/workflows/5378) và import vào **n8n Editor**.
- **Copy/paste JSON** từ file vào **n8n Editor** (tab `Import/Export`).

:::note[LƯU Ý]
- **Không chỉnh sửa JSON trực tiếp** nếu không hiểu cấu trúc, tránh làm workflow bị lỗi.
- **Kích hoạt chế độ "Debug"** để theo dõi lỗi nếu workflow không chạy.
:::

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow có **2 đường dẫn chính**:
1. **Nhập từ JSON** (quy trình tự động).
2. **Nhập từ Google Sheets** (quy trình thủ công hoặc tự động).

##### **A. Cấu hình SAP Login (HTTP Request)**
- **Node**: `SAP Login`
- **Hướng dẫn**:
  - Điền **URL API SAP B1** (ví dụ: `https://tên_máy_chủ_machine:50000/B1SERV/`).
  - Thêm **header** với `Authorization: Bearer <token_SAP>` (lấy từ SAP).
  - **Method**: `POST`.
  - **Body**:
    ```json
    {
      "UserName": "tên_dang_nhap",
      "Password": "mật_khẩu",
      "CompanyDB": "tên_công_ty"
    }
    ```
  - **Lưu ý**: Nếu SAP yêu cầu **OTP**, cần thêm node `Set` trước `SAP Login` để truyền OTP.

##### **B. Cấu hình Google Sheets**
- **Node**: `Load Sheet Data`, `Log Success/Error`
- **Hướng dẫn**:
  - **API Key**: Điền `API Key Google Sheets` (tạo tại [Google Cloud Console](https://console.cloud.google.com/)).
  - **Spreadsheet ID**: Lấy từ liên kết Google Sheets (ví dụ: `1AbCdeFgHiJkLmNoPqRsTuVwXyZ`).
  - **Sheet Name**: Điền tên tab (ví dụ: `Dữ liệu_Sổ_Cái`).
  - **Range**: Điền `A1:Z1000` (hoặc điều chỉnh theo số dòng dữ liệu).
  - **Lưu ý**: Đảm bảo **bảng Google Sheets có cấu trúc chuẩn** (cột: `DocEntry`, `CardName`, `DocDate`, `LineTotal`, `Description`, ...).

##### **C. Cấu hình GPT-4o (LLM Transform)**
- **Node**: `LLM Transform (Manual)`, `LLM Transform (Sheet)`
- **Hướng dẫn**:
  - **API Key OpenAI**: Điền `sk-...` từ tài khoản OpenAI.
  - **Model**: Chọn `gpt-4o`.
  - **Prompt**:
    ```plaintext
    Bạn là một chuyên gia kế toán SAP. Hãy kiểm tra và tổng kết dòng sổ cái sau:
    {{{$json}}}
    Cần trả về JSON với cấu trúc:
    {
      "IsValid": true/false,
      "Reason": "Lý do nếu không hợp lệ",
      "ProcessedData": {
        "DocEntry": "ABC123",
        "CardName": "Người nhận",
        "DocDate": "2024-05-20",
        "LineTotal": 1000000,
        "Description": "Mô tả chi tiết",
        "VAT": 100000,
        "AccountCode": "123456"
      }
    }
    ```
  - **Lưu ý**: **Không thay đổi prompt** nếu không hiểu rõ logic, tránh sai kết quả.

##### **D. Cấu hình Webhook (Trigger)**
- **Node**: `Webhook Trigger`
- **Hướng dẫn**:
  - **URL Webhook**: Điền URL của **n8n** (ví dụ: `https://tên_máy_chủ.n8n.workflows/your-workflow-url`).
  - **Method**: `POST`.
  - **Payload Example**:
    ```json
    {
      "source": "json",
      "data": {
        "DocEntry": "ABC123",
        "CardName": "Người nhận",
        "DocDate": "2024-05-20",
        "Lines": [
          {"LineTotal": 1000000, "Description": "Mua hàng"},
          {"LineTotal": 500000, "Description": "Phí vận chuyển"}
        ]
      }
    }
    ```
  - **Lưu ý**: Nếu không có Webhook, có thể **kích hoạt từ Google Sheets** bằng node `Set` + `Google Sheets`.

##### **E. Cấu hình Log (Google Sheets)**
- **Node**: `Log Success (JSON)`, `Log Success (Sheet)`, `Log Error (JSON)`, `Log Error (Sheet)`
- **Hướng dẫn**:
  - **Sheet Name**: Điền `Log_Sổ_Cái` (tạo tab mới trong Google Sheets).
  - **Range**: `A1:F1000` (cột: `Time`, `Status`, `DocEntry`, `Error`, `ProcessedData`).
  - **Lưu ý**: Workflow sẽ tự động ghi **thành công/thất bại** vào bảng này.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Sử dụng **Webhook** để gửi JSON mẫu (ví dụ từ Postman).
   - Kiểm tra **Google Sheets Log** để xác nhận dữ liệu đã được xử lý.
2. **Bật Active**:
   - Đi đến tab `Settings` của workflow và bật `Active`.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Slack/Telegram**:
   - Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` để **báo cáo kết quả** khi workflow hoàn thành.
   - **Ví dụ**:
     ```json
     {
       "text": `Sổ cái ${docEntry} đã nhập thành công vào SAP!`,
       "attachments": [
         {
           "title": "Chi tiết",
           "text": `Người nhận: ${cardName}\nTổng: ${lineTotal}`
         }
       ]
     }
     ```

2. **Lưu log vào Database (MySQL/PostgreSQL)**:
   - Thay thế node `Google Sheets` bằng `n8n-nodes-base.database` để lưu log vào cơ sở dữ liệu.

3. **Tự động nhập từ Excel/CSV**:
   - Sử dụng node `n8n-nodes-base.fileSystem` để đọc file Excel/CSV và chuyển thành JSON.

4. **Tự động gửi báo cáo định kỳ**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow hàng ngày và gửi báo cáo qua email (node `n8n-nodes-base.email`).

5. **Tối ưu hóa GPT-4o**:
   - **Tăng độ dài prompt** để GPT-4o hiểu rõ hơn về quy trình sổ cái của doanh nghiệp.
   - **Sử dụng System Prompt** để định nghĩa rõ ràng các trường hợp đặc biệt (ví dụ: VAT 0%, nhập hàng trả trước...).

6. **Xây dựng Dashboard theo dõi**:
   - Kết hợp với **Google Data Studio** hoặc **Power BI** để tạo **bảng điều khiển thực thời** cho bộ phận kế toán.
:::

---

### 📌 **Kết luận**
Workflow này **giải phóng bộ phận kế toán** khỏi công việc nhập sổ cái mòn mỏi, đồng thời **giảm sai sót** nhờ AI GPT-4o kiểm tra logic. Với **cấu hình đơn giản** và **không cần code**, các sếp có thể **tự động hóa 100% quy trình sổ cái SAP B1** chỉ trong vài giờ.

**Hành động ngay hôm nay**:
1. **Chuẩn bị tài khoản SAP, Google Sheets và OpenAI**.
2. **Import workflow** và **cấu hình theo hướng dẫn**.
3. **Test Run** và **bật Active** để bắt đầu tự động hóa!

👉 **Nếu gặp khó khăn**, để lại comment bên dưới hoặc liên hệ với cộng đồng n8n tại [n8n Community](https://community.n8n.io/). Chúc các sếp thành công! 🚀