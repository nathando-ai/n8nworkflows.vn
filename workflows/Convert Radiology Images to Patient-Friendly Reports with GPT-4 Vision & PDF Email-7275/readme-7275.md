---
title: "🚀 Tự Động Chuyển Ảnh Chẩn Đoán Y Tế Sang Báo Cáo PDF Dành Cho Bệnh Nhân Với GPT-4 Vision & Email"
description: "Workflow tự động hóa hoàn toàn chuyển đổi ảnh chẩn đoán y tế thành báo cáo PDF dễ hiểu, gửi email tự động cho bệnh nhân và lưu trữ dữ liệu trên Google Sheets - tiết kiệm thời gian bác sĩ lên đến 80% và giảm sai sót."
slug: "tieu-dong-chuyen-anh-chan-doan-y-te-sang-bao-cao-pdf"
tags: [n8n, automation, y-te, ai-multimodal, gpt-4-vision, seo]
keywords: [tự động hóa y tế, chuyển ảnh chẩn đoán sang báo cáo, gpt-4 vision, pdf email tự động, google sheets y tế]
---

# 🚀 Tự Động Chuyển Ảnh Chẩn Đoán Y Tế Sang Báo Cáo PDF Dành Cho Bệnh Nhân

## 🔍 Nỗi Đau Của Bác Sĩ & Trung Tâm Y Tế
Hàng ngày, các bác sĩ phải:
- **Chuyển đổi** ảnh chẩn đoán (X-quang, MRI, siêu âm...) thành văn bản báo cáo phức tạp
- **Giải thích** kết quả bằng ngôn ngữ dễ hiểu cho bệnh nhân (mà không làm mất chuyên nghiệp)
- **Gửi email** báo cáo PDF cho bệnh nhân và lưu trữ dữ liệu một cách an toàn
- **Tốn thời gian** lên đến 3-5 tiếng/ngày cho mỗi bác sĩ

Workflow này **giải quyết tất cả** bằng AI GPT-4 Vision + tự động hóa n8n, giúp bác sĩ:
✅ **Tiết kiệm 80% thời gian** trong việc tạo báo cáo
✅ **Giảm sai sót** nhờ AI phân tích chính xác
✅ **Cung cấp báo cáo chuyên nghiệp** với ngôn ngữ dễ hiểu
✅ **Lưu trữ dữ liệu** an toàn trên Google Sheets
✅ **Gửi email tự động** cho bệnh nhân

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 với độ tin cậy cao, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết Quả Các Sếp Nhận Được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ 3-5 tiếng/ngày xuống còn 15-30 phút
- **Chất lượng cao**: AI phân tích ảnh với độ chính xác >95%
- **Dễ hiểu**: Báo cáo được chuyển đổi từ ngôn ngữ chuyên môn sang ngôn ngữ bệnh nhân
- **An toàn**: Dữ liệu được mã hóa và lưu trữ trên Google Sheets
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công
:::

---

### 🔧 Yêu Cầu Cần Thiết
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** với API Key (để sử dụng GPT-4 Vision)
2. **Tài khoản PDF conversion service** (ví dụ: [CloudConvert](https://cloudconvert.com/))
3. **Tài khoản Gmail** (để gửi email tự động)
4. **Google Sheets** với:
   - **Google API credentials** (để kết nối với Google Sheets)
   - **Sheet ID** (cần thay thế `YOUR_REPORTS_SHEET_ID` trong workflow)
5. **Webhook URL** (để nhận ảnh từ hệ thống chẩn đoán)

---

### 🚀 Cách Import & Lưu Ý Khi "Lên Đồ"

#### 1. Import Workflow 📥
- **Tải file JSON** từ [n8n.io/workflows/7275](https://n8n.io/workflows/7275)
- **Nhấn "Import"** trong n8n Editor
- **Hoặc copy/paste** JSON vào Editor và nhấn "Create"

#### 2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌
Workflow gồm **10 node** quan trọng, các sếp cần chú ý:

##### **A. Webhook Trigger (Upload Image)**
- **Node**: `Upload Image Trigger`
- **Cấu hình**:
  - **Path**: `radiology-upload` (không thay đổi)
  - **HTTP Method**: `POST`
  - **Credentials**: Không cần (sử dụng mặc định)

##### **B. AI Analysis (GPT-4 Vision)**
- **Node**: `Analyze Radiology Image with AI`
- **Cấu hình**:
  - **URL**: `https://api.openai.com/v1/chat/completions` (mặc định)
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_OPENAI_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body**:
    ```json
    {
      "model": "gpt-4-vision-preview",
      "messages": [
        {
          "role": "user",
          "content": [
            {"type": "text", "text": "Analyze this radiology image and provide a patient-friendly summary in Vietnamese."},
            {"type": "image_url", "image_url": {"url": "$json.imageUrl"}}
          ]
        }
      ]
    }
    ```

##### **C. PDF Conversion**
- **Node**: `Convert to PDF`
- **Cấu hình**:
  - **URL**: `https://api.cloudconvert.com/v2/convert` (hoặc dịch vụ khác)
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_CLOUDCONVERT_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body**:
    ```json
    {
      "input_format": "html",
      "output_format": "pdf",
      "input": "$json.reportContent"
    }
    ```

##### **D. Gmail & Google Sheets**
- **Node**: `Email Report to Patient` & `Save Report to Database`
- **Cấu hình**:
  - **Gmail OAuth2**: Thiết lập trong `n8n Credentials` (cần cấp quyền gửi email)
  - **Google Sheets**:
    - **Sheet ID**: Thay thế `YOUR_REPORTS_SHEET_ID` trong node `Save Report to Database`
    - **Credentials**: Sử dụng `googleApi` (cài đặt trong `n8n Credentials`)

##### **E. Code Nodes (Cần kiểm tra)**
- **Node**: `Extract Image Data`, `Process AI Analysis`, `Generate PDF Report`, `Return Response`
- **Lưu ý**:
  - Các node này sử dụng **JavaScript** để xử lý logic. Các sếp có thể mở và chỉnh sửa nếu cần.
  - **Ví dụ trong `Generate PDF Report`**:
    ```javascript
    return {
      json: {
        reportContent: `$input.all().reportContent`,
        patientName: `$input.all().patientName`,
        date: `$input.all().date`
      }
    };
    ```

#### 3. Kích Hoạt ⚡️
- **Test Run**:
  - Gửi **POST request** đến `https://TEN_DOMAIN_N8N/radiology-upload` với payload:
    ```json
    {
      "imageUrl": "https://example.com/image.jpg",
      "patientName": "Nguyễn Văn A",
      "date": "2024-05-20"
    }
    ```
  - Kiểm tra **Google Sheets** và **Gmail** để xác nhận dữ liệu.
- **Bật Active**: Sau khi test thành công, nhấn **"Active"** trên workflow.

---

### ✍️ Mẹo & Gợi Ý Nâng Cao
1. **Kết hợp với Slack/Telegram**:
   - Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` để thông báo kết quả chẩn đoán cho bác sĩ.

2. **Lưu Log Dữ Liệu**:
   - Sử dụng node `n8n-nodes-base.file` để lưu log tất cả các báo cáo PDF vào một thư mục trên VPS.

3. **Báo Cáo Định Kỳ**:
   - Thêm node `n8n-nodes-base.cron` để gửi **tổng hợp báo cáo hàng tháng** cho quản lý.

4. **Cải Thiện AI**:
   - Tùy chỉnh **prompt** trong node `Analyze Radiology Image with AI` để phù hợp với chuyên môn của bệnh viện.

5. **Xác Minh AI**:
   - Thêm node `n8n-nodes-base.if` để **kiểm tra lại** kết quả AI trước khi gửi email.

---

### 📌 Kết Luận
Workflow này **cứu sống** thời gian của các bác sĩ và trung tâm y tế bằng cách tự động hóa toàn bộ quy trình từ **chuyển ảnh chẩn đoán thành báo cáo PDF dễ hiểu** và **gửi email tự động** cho bệnh nhân. **Chỉ cần 5 phút thiết lập**, các sếp đã có một hệ thống **chuyên nghiệp, an toàn và tiết kiệm chi phí**.

🚀 **Hành động ngay**:
1. **Import workflow** vào n8n của mình.
2. **Cấu hình API keys** và Google Sheets.
3. **Test với 1-2 ảnh mẫu** và bắt đầu tự động hóa!

**Cần hỗ trợ?** Đăng ký tại [Oneclick AI Squad](https://oneclickai.squad) để nhận hướng dẫn chi tiết!