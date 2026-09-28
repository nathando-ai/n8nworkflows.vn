---
title: "🤖 Tự Động Đánh Giá Sơ Yêu Cầu (JD) Với CV Bằng GPT-4o, Google Drive & Sheets - N8n AI"
description: "Workflow tự động so sánh CV ứng viên với mô tả công việc (JD) bằng trí tuệ nhân tạo GPT-4o, tự động tính điểm phù hợp (0-100), phân tích điểm yếu và điểm mạnh, lưu kết quả vào Google Drive và Google Sheets. Giúp HR tiết kiệm 10+ giờ/tháng so sánh thủ công, giảm sai sót và đưa ra quyết định tuyển dụng chính xác hơn."
slug: "tieu-dong-danh-gia-jd-voi-cv-bang-gpt-4o"
tags: [n8n, automation, hr-automation, ai-resume-scoring, google-drive, google-sheets, gpt-4o, azure-openai]
keywords: [tự động hóa tuyển dụng n8n, đánh giá cv bằng ai, so sánh sơ yêu cầu với cv, gpt-4o tự động hóa, workflow n8n cho hr, tự động tính điểm phù hợp cv]
---

# 🚀 **Tự Động Đánh Giá CV Theo Sơ Yêu Cầu (JD) Bằng GPT-4o, Google Drive & Sheets**

## **🔍 Nỗi Đau Của HR: So Sánh CV Thủ Công Làm Mất Thời Gian & Sai Lầm**
Hàng ngày, các sếp HR phải:
- **So sánh từng CV** với hàng chục sơ yêu cầu công việc (JD) khác nhau.
- **Đọc lại và đánh giá** hàng trăm trang nội dung để tìm kiếm từ khóa, kỹ năng và kinh nghiệm phù hợp.
- **Ghi nhớ điểm mạnh/điểm yếu** của từng ứng viên để so sánh sau này.
- **Mất thời gian** để tổng hợp kết quả vào bảng Excel hoặc Google Sheets.

Kết quả? **Sai sót, mất thời gian, và quyết định tuyển dụng không chính xác**. Với **Workflow này**, các sếp sẽ tự động:
✅ **So sánh CV với JD** bằng trí tuệ nhân tạo GPT-4o (chính xác hơn con người).
✅ **Tính điểm phù hợp** từ 0-100 (90-100: Hire ngay, dưới 50: Loại bỏ).
✅ **Phân tích điểm yếu và điểm mạnh** của ứng viên.
✅ **Lưu kết quả** vào Google Drive (báo cáo chi tiết) và Google Sheets (dữ liệu theo dõi).
✅ **Tiết kiệm 10+ giờ/tháng** so sánh thủ công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: So sánh hàng trăm CV chỉ trong vài phút.
- **Đánh giá khách quan**: GPT-4o phân tích sâu hơn so với con người.
- **Dữ liệu theo dõi**: Lưu tất cả kết quả vào Google Sheets để phân tích sau này.
- **Báo cáo chi tiết**: Tạo file báo cáo tự động cho từng ứng viên.
- **Giảm sai sót**: Tránh bỏ sót kỹ năng hoặc kinh nghiệm quan trọng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive & Sheets**:
   - **Folder JD**: Lưu tất cả các file PDF mô tả công việc (JD).
   - **Folder Resume**: Lưu tất cả CV ứng viên (PDF).
   - **Google Sheet**: Bảng dữ liệu để lưu kết quả (ví dụ: `Candidate_Evaluation`).

2. **API Key Azure OpenAI**:
   - **Mô hình**: `gpt-4o-mini` (rẻ và hiệu quả).
   - **Cách lấy API Key**: [Tạo tài khoản Azure OpenAI](https://azure.microsoft.com/en-us/products/cognitive-services/openai-service/) và tạo `API Key`.

3. **Credentials trong n8n**:
   - **Google Drive OAuth2**: Cấu hình trong `n8n Credentials`.
   - **Google Sheets OAuth2**: Cấu hình trong `n8n Credentials`.
   - **Azure OpenAI API**: Cấu hình trong `n8n Credentials`.

4. **File mẫu**:
   - **JD mẫu**: File PDF mô tả công việc (ví dụ: `Developer_JD.pdf`).
   - **CV mẫu**: File PDF của ứng viên (ví dụ: `Nguyen_Van_A_CV.pdf`).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/8531](https://n8n.io/workflows/8531) (chọn **Export JSON**).
2. Trong n8n Editor, nhấn **Import** và chọn file JSON tải xuống.
3. Chọn **Import** để thêm workflow vào canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở n8n Editor và tạo workflow mới.
2. Nhấn **Import** → **Paste JSON** và dán toàn bộ mã JSON từ [n8n.io/workflows/8531](https://n8n.io/workflows/8531).
3. Nhấn **Import** để hoàn tất.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **23 node**, nhưng các node quan trọng nhất cần cấu hình kỹ:

#### **🔹 Node "Manual Trigger" (Bắt đầu workflow)**
- **Chức năng**: Khởi động workflow thủ công.
- **Lưu ý**: Không cần chỉnh gì, chỉ nhấn **Execute workflow** khi cần chạy.

#### **🔹 Node "Search JD" & "Search Resume" (Tìm kiếm file trong Google Drive)**
- **Cấu hình**:
  - **Folder JD**: Đặt đường dẫn đến folder lưu JD (ví dụ: `/JD_store`).
  - **Folder Resume**: Đặt đường dẫn đến folder lưu CV (ví dụ: `/Resume_store`).
  - **File Type**: Chọn `PDF` để chỉ tìm file PDF.

#### **🔹 Node "Download File" (Tải xuống PDF)**
- **Credentials**: Chọn `googleDriveOAuth2Api` (đã cấu hình trước).
- **File ID**: Auto lấy từ node trước (không cần chỉnh).

#### **🔹 Node "Extract from File" (Trích xuất text từ PDF)**
- **Operation**: Chọn `pdf` (đã mặc định).
- **Lưu ý**: Nếu PDF có format đặc biệt, có thể cần chỉnh `Extract Text Options`.

#### **🔹 Node "AI Agent" (So sánh CV với JD bằng GPT-4o)**
- **Prompt mẫu** (cần chỉnh để phù hợp với JD cụ thể):
  ```json
  {
    "system": "Bạn là một chuyên gia tuyển dụng AI. So sánh CV ứng viên với mô tả công việc (JD) và trả về kết quả dưới dạng JSON với cấu trúc sau:
    {
      \"score\": <number>, // Điểm phù hợp (0-100)
      \"must_have_gaps\": [\"Kỹ năng 1\", \"Kỹ năng 2\"], // Điểm yếu cần bổ sung
      \"nice_to_have_bonuses\": [\"Kỹ năng 1\", \"Kỹ năng 2\"], // Điểm mạnh
      \"summary\": \"Tóm tắt phân tích\" // Giới thiệu ngắn về ứng viên
    }
    JD: {{JD_text}}
    CV: {{resume_text}}
    ",
    "tools": []
  }
  ```
- **Model**: Chọn `gpt-4o-mini` (đã mặc định).

#### **🔹 Node "Parse AI Response to JSON" (Chuyển text thành JSON)**
- **Code mẫu** (cần chỉnh để phù hợp với output của GPT-4o):
  ```javascript
  // Chuyển text của GPT-4o thành JSON
  const text = $input.all().text;
  const jsonString = text.replace(/```json\n|\n```/g, '');
  try {
    const json = JSON.parse(jsonString);
    return { json: json };
  } catch (e) {
    return { error: "Không thể parse JSON", text: text };
  }
  ```

#### **🔹 Node "Append or Update Row in Sheet" (Cập nhật Google Sheets)**
- **Sheet Name**: Chọn bảng Google Sheets lưu kết quả (ví dụ: `Candidate_Evaluation`).
- **Range**: Chọn ô bắt đầu (ví dụ: `A1`).
- **Headers**: Chọn các cột cần cập nhật (ví dụ: `Candidate Name`, `Score`, `Summary`).

#### **🔹 Node "Create file from text" (Tạo báo cáo kết quả)**
- **Folder**: Chọn `Resume_store` (để lưu báo cáo).
- **File Name**: `{{$node["Extract Resume Text Content"].json()["name"]}}_result-summary.txt`.
- **Content**: Nội dung từ node `AI Agent`.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** (kiểm tra trước khi chạy thực):
   - Chọn **Test Tab** và nhấn **Execute**.
   - Kiểm tra output của từng node (đặc biệt là `AI Agent` và `Parse JSON`).
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động khi nhấn **Execute workflow**.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH LÀM NÀY ĐỂ TĂNG HIỆU QUẢ]
1. **Tự động chạy hàng ngày**:
   - Thay thế `Manual Trigger` bằng **Schedule Trigger** (cài đặt chạy hàng ngày/lần tuần).
   - Cấu hình trong **Settings** → **Triggers**.

2. **Gửi báo cáo qua Email/Slack**:
   - Thêm node **Email** hoặc **Slack Webhook** sau node `Create file from text` để gửi báo cáo tự động.

3. **Lưu log vào Google Drive**:
   - Thêm node **Google Drive (Create File)** để lưu log của workflow (giúp debug dễ dàng).

4. **Tích hợp với LinkedIn/Job Boards**:
   - Sử dụng node **HTTP Request** để tự động tải CV từ LinkedIn hoặc các trang tuyển dụng.

5. **Tối ưu API Key Azure OpenAI**:
   - Nếu budget hạn chế, thay `gpt-4o-mini` bằng `gpt-3.5-turbo` (rẻ hơn).
   - Cấu hình **Rate Limit** trong `Azure OpenAI` để tránh bị chặn.

6. **Phân loại ứng viên tự động**:
   - Sử dụng node **Code** để phân loại ứng viên theo điểm (ví dụ: `score > 80` → `Hire`, `score < 50` → `Reject`).
   - Sau đó gửi kết quả vào **Google Sheets** với cột `Status`.

---
## 📌 **Kết Luận**
Workflow này **giải phóng HR khỏi công việc so sánh CV thủ công**, giúp:
✔ **Tiết kiệm thời gian** (so sánh hàng trăm CV chỉ trong vài phút).
✔ **Đánh giá chính xác** (GPT-4o phân tích sâu hơn con người).
✔ **Lưu trữ dữ liệu** (Google Sheets & Drive giúp theo dõi lâu dài).
✔ **Tự động hóa tuyển dụng** (giúp các sếp tập trung vào phần mềm hơn).

**Hành động ngay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình credentials** (Google Drive, Sheets, Azure OpenAI).
3. **Test Run** và **bật Active**.
4. **Tích hợp với Email/Slack** để nhận báo cáo tự động.

👉 **Bắt đầu tự động hóa tuyển dụng ngay hôm nay!** 🚀

---
**📌 Lưu ý cuối cùng**:
- Nếu gặp lỗi **API Key Azure OpenAI**, kiểm tra lại **Rate Limit** và **Subscription Plan**.
- Nếu **Google Drive/Sheets không kết nối**, kiểm tra lại **Credentials** trong n8n.
- **Mỗi JD khác nhau** sẽ cần **Prompt khác nhau** trong node `AI Agent`. Các sếp nên chỉnh lại prompt để phù hợp với mô tả công việc cụ thể.