---
title: "📄 Tự Động Hóa Quét & Phân Tích Hóa Đơn: Giảm 90% Thời Gian Kiểm Tra Tài Chính Cho Các Sếp"
description: "Workflow này tự động quét, trích xuất và phân tích hóa đơn từ Google Drive, sau đó ghi dữ liệu vào Google Sheets với độ chính xác cao. Giúp các sếp tiết kiệm hàng giờ công sức hàng tuần và giảm thiểu lỗi thủ công."
slug: "tieu-dong-hoa-quet-phan-tich-hoa-don"
tags: [n8n, automation, no-code, ai, google-drive, google-sheets, mistral-ai, openai]
keywords: [tự động hóa hóa đơn, quét hóa đơn, phân tích hóa đơn, n8n workflow, ai cho tài chính, google drive automation]
---

# 🚀 **Tự Động Hóa Quét & Phân Tích Hóa Đơn: Giải Pháp AI Cho Tài Chính Hiệu Quả**

### **Nỗi Đau Của Các Sếp**
Hàng tuần, các sếp phải mất **3-5 giờ** để:
- **Quét và nhập liệu** hóa đơn từ giấy sang Excel.
- **Kiểm tra thủ công** số liệu, ngày hạn, và chi tiết chi tiêu.
- **Ghi chép vào sổ sách** hoặc hệ thống tài chính.
- **Phát hiện lỗi** như số hóa đơn trùng, ngày sai, hoặc chi tiết không rõ ràng.

Kết quả? **Thời gian bị lãng phí, rủi ro sai sót cao, và không thể tự động hóa quy trình**. **Workflow này giải quyết tất cả những vấn đề trên bằng AI và tự động hóa 100% không cần code!**

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (Đảm bảo tốc độ xử lý nhanh cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 5-7 giờ/tuần** cho bộ phận tài chính.
✅ **Độ chính xác 99%** (không còn sai sót do nhập liệu thủ công).
✅ **Dữ liệu tự động phân loại** (ngày, số hóa đơn, tổng tiền, chi tiết).
✅ **Ghi dữ liệu vào Google Sheets** một cách tự động, sẵn sàng cho báo cáo.
✅ **Hoạt động liên tục** (không cần can thiệp người dùng).
✅ **Kết hợp AI Mistral & OpenAI** để hiểu và phân tích văn bản hóa đơn phức tạp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** (để lưu hóa đơn và kích hoạt trigger).
2. **API Key Mistral AI** ([Đăng ký tại đây](https://mistral.ai/)) để trích xuất văn bản.
3. **API Key OpenAI** ([Đăng ký tại đây](https://platform.openai.com/)) để phân tích dữ liệu.
4. **Google Sheets** (để lưu kết quả phân tích).
5. **Google Drive OAuth 2.0** (để n8n có quyền truy cập vào folder hóa đơn).

:::note[LƯU Ý]
- **Không cần code** – workflow đã sẵn sàng, chỉ cần cấu hình API keys.
- **Hóa đơn phải là file PDF hoặc image** (n8n sẽ tự động trích xuất văn bản).
- **Folder Google Drive** phải được chia sẻ với n8n (quyền đọc).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow:

**Cách 1: Từ file JSON**
1. Tải workflow từ [đây](https://n8n.io/workflows/7990) (nút **Export**).
2. Trên n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

**Cách 2: Copy/Paste JSON**
1. Tải workflow từ [đây](https://n8n.io/workflows/7990) và chọn **Export**.
2. Mở n8n Editor → Nhấn **Import** → Chọn **Paste JSON**.
3. Dán toàn bộ nội dung JSON và nhấn **Import**.

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow có **7 node chính**, các sếp cần **cấu hình cẩn thận** các node sau:

##### **🔹 Node 1: Google Drive Trigger**
- **Chức năng**: Kích hoạt khi có file mới được upload vào folder Google Drive.
- **Cấu hình**:
  - Chọn **credentials**: `googleDriveOAuth2Api`.
  - **Folder**: Chọn folder chứa hóa đơn (ví dụ: `Hóa Đơn Nhập`).
  - **File Type**: Chỉ chọn `PDF` hoặc `Image` (JPG/PNG).

##### **🔹 Node 2: HTTP Request (Trích xuất văn bản)**
- **Chức năng**: Gửi file lên Mistral AI để trích xuất văn bản.
- **Cấu hình**:
  - **Method**: `POST`.
  - **URL**: `https://api.mistral.ai/v1/chat/completions` (hoặc URL API Mistral của các sếp).
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_MISTRAL_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body**:
    ```json
    {
      "model": "mistral-tiny",
      "messages": [
        {
          "role": "user",
          "content": "Extract all text from this receipt: {{$node["Google Drive Trigger"].json["file"]}}"
        }
      ]
    }
    ```

##### **🔹 Node 3: Extract Text (Mistral AI)**
- **Chức năng**: Trích xuất văn bản từ hóa đơn.
- **Cấu hình**:
  - **Credentials**: `mistralCloudApi`.
  - **Prompt**: Sẵn sàng, không cần chỉnh sửa (n8n đã tối ưu).

##### **🔹 Node 4: AI Agent (LangChain)**
- **Chức năng**: Phân tích văn bản trích xuất (ngày, số hóa đơn, tổng tiền, chi tiết).
- **Cấu hình**:
  - **Model**: Sẵn sàng, không cần chỉnh sửa.
  - **Tool Use**: Chọn `Structured Output Parser` (node tiếp theo).

##### **🔹 Node 5: OpenAI Chat Model (gpt-4.1-mini)**
- **Chức năng**: Xác nhận và hoàn thiện dữ liệu phân tích.
- **Cấu hình**:
  - **Credentials**: `openAiApi`.
  - **Model**: `gpt-4.1-mini` (đã được thiết lập).
  - **Prompt**: Sẵn sàng, không cần chỉnh sửa (n8n tự động điều chỉnh).

##### **🔹 Node 6: Structured Output Parser**
- **Chức năng**: Chuyển dữ liệu phân tích thành **bảng dữ liệu có cấu trúc** (JSON).
- **Cấu hình**:
  - **Schema**: Sẵn sàng, không cần chỉnh sửa.
  - **Output**: Dữ liệu sẽ được chuyển sang node tiếp theo.

##### **🔹 Node 7: Append Row in Sheet (Google Sheets)**
- **Chức năng**: Ghi dữ liệu vào Google Sheets.
- **Cấu hình**:
  - **Credentials**: `googleSheetsOAuth2Api`.
  - **Sheet Name**: Chọn tên sheet (ví dụ: `Hóa Đơn Nhập`).
  - **Range**: `A1` (n8n sẽ tự động append dữ liệu).
  - **Headers**: Bắt buộc phải có (n8n sẽ tự động tạo từ structured data).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với **1 file mẫu**:
   - Upload 1 hóa đơn vào Google Drive.
   - Chạy workflow **manual** (nút **Run Workflow**).
   - Kiểm tra kết quả trong Google Sheets.

2. **Bật Active**:
   - Sau khi test thành công, **bật Active** workflow.
   - Từ nay, **mỗi khi có file mới trong Google Drive**, workflow sẽ tự động chạy.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để nhận **thông báo khi có hóa đơn mới**.
   - Ví dụ: *"Hóa đơn #1234 đã được phân tích thành công!"*

2. **Lưu Log & Báo Cáo**:
   - Thêm node **Google Drive** để lưu **log phân tích** (để theo dõi lỗi).
   - Tạo **báo cáo hàng tháng** tự động bằng **Google Sheets + Apps Script**.

3. **Phân loại Hóa Đơn**:
   - Sử dụng **AI Agent** để phân loại hóa đơn theo **ngành nghề** (ví dụ: điện, nước, internet).
   - Ghi vào **cột mới** trong Google Sheets để dễ dàng báo cáo.

4. **Kết hợp với ERP**:
   - Nếu sử dụng **SAP, QuickBooks, hoặc ERP khác**, các sếp có thể **export dữ liệu từ Google Sheets** vào hệ thống tài chính.

---

### 📌 **Kết Luận: Tự Động Hóa Hóa Đơn Bây Giờ!**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc **nhập liệu và kiểm tra thủ công**, đồng thời **tăng độ chính xác** và **giảm rủi ro sai sót**.

**Bắt đầu ngay hôm nay!**
1. **Import workflow** theo hướng dẫn.
2. **Cấu hình API keys** và Google Drive.
3. **Test với 1 hóa đơn mẫu**.
4. **Bật Active** và **quên đi việc nhập liệu thủ công!**

👉 **[Xem video hướng dẫn chi tiết](https://www.youtube.com/playlist?list=PLWYu7XaUG3XOJwOOGiX89SQ_w67vw3dq7)** (do Aemal Sayer hướng dẫn).

---
**Các sếp có thắc mắc?** Để lại comment bên dưới hoặc liên hệ qua [email](mailto:support@n8n.io) để được hỗ trợ! 🚀