---
title: "🚀 Tự Động Hoàn Chỉnh Hóa Hóa Đơn Quà Bằng Gemini AI + Google Drive & Sheets (Không Cần Code)"
description: "Workflow này tự động quét, đọc và phân loại hóa đơn từ ảnh/PDF trên Google Drive bằng Gemini AI, ghi dữ liệu vào Google Sheets và di chuyển hóa đơn đã xử lý sang thư mục riêng. Giúp các sếp tiết kiệm 100% thời gian thủ công, tránh sai sót và quản lý chi phí hiệu quả 24/7."
slug: "tieu-dong-hoan-chinh-hoa-don-gemini-google-drive-sheets"
tags: [n8n, automation, ai-summarization, google-drive, google-sheets, gemini-ai, invoice-processing]
keywords: [tự động hóa hóa đơn, gemini ai đọc hóa đơn, google drive tự động hóa, google sheets tự động hóa, workflow n8n hóa đơn, quản lý chi phí tự động]
---

# 🚀 **Tự Động Hoàn Chỉnh Hóa Đơn Quà Bằng AI + Google Drive & Sheets (Không Cần Code)**

### **Nỗi Đau Của Các Sếp Và Giải Pháp Tự Động Hóa**
Các sếp đã từng phải:
- **Quét hàng chục hóa đơn thủ công** mỗi tháng, tốn thời gian và dễ mắc sai sót.
- **Đọc hóa đơn bằng mắt** để ghi số liệu vào bảng Excel, dẫn đến lỗi nhập liệu.
- **Quên di chuyển hóa đơn đã xử lý** sang thư mục riêng, gây rối loạn quản lý.
- **Không biết cách phân loại chi phí** một cách chính xác và nhanh chóng.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Quét hóa đơn từ ảnh/PDF** trên Google Drive.
✅ **Đọc và trích xuất dữ liệu** (ngày, tên cửa hàng, tổng tiền, thuế, phương thức thanh toán, loại chi phí) bằng **Gemini AI** (mô hình OCR tiên tiến của Google).
✅ **Ghi dữ liệu vào Google Sheets** với định dạng chuẩn.
✅ **Di chuyển hóa đơn đã xử lý** sang thư mục riêng để tránh lặp lại.
✅ **Hoạt động liên tục 24/7** mà không cần can thiệp của con người.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 5-10 giờ/tháng** cho việc nhập liệu thủ công.
- **Giảm sai sót** do con người (không còn phải đọc hóa đơn bằng mắt).
- **Dữ liệu chính xác và sẵn sàng** cho báo cáo tài chính.
- **Quản lý chi phí hiệu quả** với phân loại tự động.
- **Hoạt động tự động** ngay cả khi các sếp nghỉ ngơi.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để sử dụng Google Drive, Google Sheets và Gemini API).
2. **API Key của Gemini**:
   - Đăng ký tại [Google AI Studio](https://aistudio.google/) và lấy **API Key**.
   - Thêm vào **Variables** của n8n với tên `GEMINI_API_KEY`.
3. **OAuth2 Credentials cho Google Drive & Sheets**:
   - Cài đặt trong **n8n Credentials** (Google Drive và Google Sheets).
4. **Hai thư mục trên Google Drive**:
   - **Thư mục "New Receipts"** (để drop hóa đơn mới).
   - **Thư mục "Processed"** (để lưu hóa đơn đã xử lý).
5. **Bảng Google Sheets** với các cột sau:
   - `date`, `store_name`, `total_amount`, `tax_amount`, `payment_method`, `category`, `source_file`, `original_file_id`.
6. **ID của thư mục và bảng**:
   - Lấy từ liên kết Google Drive/Sheets (ví dụ: `https://drive.google.com/drive/folders/1AbCdEfGhIjKlMnOp` → `1AbCdEfGhIjKlMnOp`).
---

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/15758](https://n8n.io/workflows/15758) và import vào **n8n Editor**.
- **Copy/paste JSON** từ link trên vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **12 node**, các sếp cần chú ý cấu hình các node sau:

##### **🔹 Node "Watch Drive Folder" (googleDriveTrigger)**
- **Cấu hình**:
  - Chọn **Credentials**: OAuth2 của Google Drive.
  - **Folder ID**: ID của thư mục "New Receipts".
  - **Polling Interval**: 60 giây (để kiểm tra thư mục mỗi phút).

##### **🔹 Node "Filter Image or PDF" (if)**
- **Điều kiện**: Chỉ cho phép **images (JPEG, PNG) và PDFs** qua.
- **Lưu ý**: Các file khác (Word, Excel) sẽ bị bỏ qua.

##### **🔹 Node "Download File" (googleDrive)**
- **Credentials**: OAuth2 của Google Drive.
- **File ID**: Auto lấy từ node trước.

##### **🔹 Node "Convert to Base64" (code)**
- **Mã JavaScript**:
  ```javascript
  return { file: { data: $input.all().file.data, mimeType: $input.all().file.mimeType } };
  ```
- **Lưu ý**: Chuyển file thành định dạng Base64 để Gemini AI xử lý.

##### **🔹 Node "Gemini OCR" (httpRequest)**
- **URL**: `https://generativelanguage.googleapis.com/v1beta/models/gemini-pro-vision:generateContent`
- **Headers**:
  - `Content-Type: application/json`
  - `Authorization: Bearer ${$env{"GEMINI_API_KEY"}}`
- **Body (JSON)**:
  ```json
  {
    "contents": [
      {
        "parts": [
          {
            "inlineData": {
              "dataBase64": "{{$json('data').data}}",
              "mimeType": "{{$json('mimeType')}}"
            }
          }
        ]
      }
    ],
    "safetySettings": [
      {
        "category": "HARM_CATEGORY_HARASSMENT",
        "threshold": "BLOCK_MEDIUM_AND_ABOVE"
      }
    ]
  }
  ```
- **Lưu ý**:
  - Thay `{{$json('data').data}}` và `{{$json('mimeType')}}` bằng dữ liệu từ node trước.
  - **Prompt mặc định** của Gemini sẽ tự động trích xuất:
    - Ngày, tên cửa hàng, tổng tiền, thuế, phương thức thanh toán, loại chi phí.

##### **🔹 Node "Parse JSON Response" (code)**
- **Mã JavaScript** (để trích xuất dữ liệu từ Gemini):
  ```javascript
  const response = $input.all().json;
  const text = response.candidates[0].content.parts[0].text;

  // Sử dụng regex để trích xuất dữ liệu (cần điều chỉnh theo kết quả Gemini)
  const dateMatch = text.match(/Ngày\s*(\d{2}\/\d{2}\/\d{4})/);
  const storeMatch = text.match(/Cửa hàng\s*([^\n]+)/i);
  const totalMatch = text.match(/Tổng tiền\s*([\d,]+)/);
  const taxMatch = text.match(/Thuế\s*([\d,]+)/);
  const paymentMatch = text.match(/Thanh toán\s*([^\n]+)/i);
  const categoryMatch = text.match(/Loại chi phí\s*([^\n]+)/i);

  return {
    date: dateMatch ? dateMatch[1] : null,
    store_name: storeMatch ? storeMatch[1] : null,
    total_amount: totalMatch ? parseFloat(totalMatch[1].replace(/,/g, '')) : null,
    tax_amount: taxMatch ? parseFloat(taxMatch[1].replace(/,/g, '')) : null,
    payment_method: paymentMatch ? paymentMatch[1] : null,
    category: categoryMatch ? categoryMatch[1] : null,
    source_file: $input.all().file.name,
    original_file_id: $input.all().file.id
  };
  ```
- **Lưu ý**:
  - **Regex trên chỉ là ví dụ**, các sếp cần **cập nhật** dựa trên kết quả trả về từ Gemini.
  - Nếu Gemini trả về định dạng khác, hãy **kiểm tra và điều chỉnh mã**.

##### **🔹 Node "Append to Sheet" (googleSheets)**
- **Credentials**: OAuth2 của Google Sheets.
- **Spreadsheet ID**: ID của bảng Google Sheets.
- **Sheet Name**: Tên sheet (ví dụ: "Receipts").
- **Columns**:
  - `date`, `store_name`, `total_amount`, `tax_amount`, `payment_method`, `category`, `source_file`, `original_file_id`.

##### **🔹 Node "Move to Processed" (googleDrive)**
- **Credentials**: OAuth2 của Google Drive.
- **Folder ID**: ID của thư mục "Processed".
- **File ID**: Auto lấy từ node trước.

##### **🔹 Node "Check Remaining Files" (httpRequest)**
- **URL**: `https://www.googleapis.com/drive/v3/files?q=mimeType+contains+'image%2Fjpeg'%20or%20mimeType+contains+'application%2Fpdf'%20and%20parents+in+%28${folderId}%29&fields=fileList%28id%29`
- **Headers**:
  - `Authorization: Bearer ${$input.all().credentials.accessToken}`
- **Lưu ý**: Thay `folderId` bằng ID của thư mục "New Receipts".

##### **🔹 Node "Has More Files?" (if)**
- **Điều kiện**: Nếu còn file trong thư mục, tiếp tục xử lý.

##### **🔹 Node "Wait 30s" (wait)**
- **Thời gian chờ**: 30 giây giữa các lần xử lý (để tránh overloading API).

##### **🔹 Node "Get Next File" (code)**
- **Mã JavaScript** (để lấy file tiếp theo):
  ```javascript
  const files = $input.all().json.fileList;
  if (files.length > 0) {
    return { fileId: files[0].id };
  } else {
    return { error: "No more files" };
  }
  ```
- **Lưu ý**: Node này sẽ **lặp lại** cho đến khi hết file.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với một file mẫu (ảnh/PDF) trên Google Drive.
2. **Kiểm tra Google Sheets** để xác nhận dữ liệu đã được ghi chính xác.
3. **Bật Active** workflow.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**TẠO TRẢI NGHIỆM TỐT HƠN**]
1. **Kết nối với Slack/Telegram**:
   - Thêm node **Slack/Telegram** để thông báo khi hoàn thành xử lý hóa đơn.
   - Ví dụ: `"Hóa đơn {{$json('store_name')}} đã được xử lý thành công!"`.

2. **Lưu log vào Google Drive**:
   - Sử dụng node **Google Drive (create file)** để lưu log xử lý (ngày giờ, file ID, kết quả).

3. **Gửi báo cáo định kỳ**:
   - Tạo một workflow riêng để **tổng hợp dữ liệu từ Google Sheets** và gửi báo cáo qua email (sử dụng node **Send Email**).

4. **Tùy chỉnh prompt Gemini**:
   - Nếu Gemini không trích xuất được dữ liệu chính xác, **cập nhật prompt** trong node "Gemini OCR" để phù hợp với mẫu hóa đơn của các sếp.
   - Ví dụ:
     ```json
     {
       "contents": [
         {
           "parts": [
             {
               "text": "Trích xuất dữ liệu hóa đơn theo định dạng sau:\n- Ngày: [ngày]\n- Tên cửa hàng: [tên]\n- Tổng tiền: [số tiền]\n- Thuế: [số tiền]\n- Phương thức thanh toán: [cash/chuyển khoản]\n- Loại chi phí: [điện nước, ăn uống, xăng dầu]"
             }
           ]
         }
       ]
     }
     ```

5. **Sử dụng n8n Cloud (nếu không muốn self-host)**:
   - Nếu các sếp không muốn cài đặt VPS, có thể dùng **n8n Cloud** (miễn phí cho workflow đơn giản).
   - Tuy nhiên, **self-hosted** vẫn tốt hơn vì:
     - **Đảm bảo bảo mật** (không chia sẻ API key với n8n).
     - **Không giới hạn** về số lượng workflow.
     - **Tiết kiệm chi phí dài hạn**.
:::

---
### 📌 **Kết Luận**
Workflow này **giải phóng các sếp khỏi công việc thủ công mệt mỏi**, giúp quản lý hóa đơn một cách **chính xác, tự động và hiệu quả**. Với **Gemini AI**, dữ liệu được trích xuất nhanh chóng và chính xác hơn so với cách đọc bằng mắt.

**Hành động ngay hôm nay!**
1. **Chuẩn bị tài khoản và cấu hình** theo hướng dẫn trên.
2. **Import workflow** và **test với file mẫu**.
3. **Bật Active** và **nhận kết quả tự động hóa ngay từ hôm nay!**

---
:::success[**💡 LƯU Ý CUỐI CÙNG**]
- **Nếu gặp lỗi**, kiểm tra:
  - **API Key Gemini** có đúng không?
  - **Credentials OAuth2** của Google Drive/Sheets có được cấu hình chính xác?
  - **Folder ID và Sheet ID** có đúng không?
- **Nếu muốn nâng cao**, kết hợp với **Zapier, Make (Integromat)** để mở rộng tính năng.
:::