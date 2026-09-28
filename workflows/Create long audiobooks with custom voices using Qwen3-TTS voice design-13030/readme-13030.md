---
title: "🎧 **Tự Động Hóa Sáng Tạo Audiobook Dài Hạng Năng Lực với Giọng Nói Đặc Trưng bằng Qwen3-TTS (n8n)**"
description: "Workflow này tự động chuyển đổi văn bản từ Google Sheets thành audiobook dài, với giọng nói cá nhân hóa và chất lượng chuyên nghiệp, tiết kiệm thời gian lên đến 90% so với phương pháp thủ công. Kết quả là audiobook hoàn chỉnh được lưu trên Google Drive với tên file tự động theo thời gian."
slug: "tu-dong-hoa-tao-tao-audiobook-dai-voi-qwen3-tts"
tags: [n8n, automation, content-creation, ai-multimodal, google-sheets, google-drive, qwen3-tts, fal-run, replicate]
keywords: [tự động hóa audiobook, qwen3 tts n8n, tạo audiobook từ google sheets, voice design ai, ffmpeg audio merge, n8n workflow tự động]
---

# 🚀 **Tự Động Hóa Sáng Tạo Audiobook Dài Hạng Năng Lực với Giọng Nói Đặc Trưng**

### **Nỗi Đau Của Các Sếp**
Các sếp đang phải **tốn thời gian vô cùng** để chuyển đổi văn bản thành audiobook bằng cách thu âm từng phần thủ công, hoặc phải thuê giọng nói chuyên nghiệp với chi phí cao. Kết quả thường không đồng nhất về chất lượng giọng nói, và việc chỉnh sửa lại sau khi phát hiện lỗi là một quá trình **mệt mỏi và tốn khác**.

Workflow này **giải quyết tất cả** bằng cách:
✅ **Tự động hóa hoàn toàn** quá trình từ văn bản → giọng nói → audiobook hoàn chỉnh.
✅ **Cá nhân hóa giọng nói** theo mô tả chi tiết (tuổi, giới tính, cảm xúc, giọng địa phương...).
✅ **Kết hợp AI Qwen3-TTS** (Replicate) với công cụ **FFmpeg** (Fal.run) để tạo ra audiobook dài **không giới hạn thời lượng**.
✅ **Lưu trữ tự động** trên Google Drive với tên file theo thời gian, sẵn sàng chia sẻ.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tốc độ và tính bảo mật cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 90%** so với phương pháp thủ công.
- **Chất lượng giọng nói chuyên nghiệp**, cá nhân hóa theo yêu cầu (tuổi, giọng, cảm xúc).
- **Không giới hạn độ dài audiobook** (thuật toán FFmpeg hỗ trợ merge nhiều đoạn).
- **Tự động lưu trên Google Drive** với tên file theo thời gian (vd: `Audiobook_2024-05-20_14-30.mp3`).
- **Hoạt động liên tục 24/7** trên VPS, không phụ thuộc vào máy tính cá nhân.
- **Dễ dàng mở rộng** cho nhiều dự án audiobook khác nhau.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** với **bảng dữ liệu mẫu** (được clone từ [đây](https://docs.google.com/spreadsheets/d/1f4rB-i3cVDzKLi6nv8EMvjjyg9n4rgkOVx28_EI1NBI/edit?usp=sharing)).
   - **Cột bắt buộc**:
     - `Text`: Nội dung văn bản cần chuyển thành giọng nói.
     - `Speaker`: Tên người phát âm (giống mô tả giọng nói).
     - `Voice Description`: Mô tả chi tiết giọng nói (vd: *"Nam, 40 tuổi, giọng miền Bắc, giọng điệu nghiêm túc"*).
     - `Style Instruction`: Hướng dẫn giọng nói (vd: *"Chậm rãi, giọng kể chuyện"*).
     - `Temp URL`: URL tạm thời để lưu trữ audio đoạn (sẽ được tự động cập nhật).
     - `To Merge`: Dùng để đánh dấu các đoạn cần merge thành audiobook cuối cùng.

2. **API Keys**:
   - **Replicate API Key** (để sử dụng Qwen3-TTS).
     👉 [Đăng ký tại Replicate](https://replicate.com/) (miễn phí cho lượng sử dụng nhỏ).
   - **Fal.run API Key** (để sử dụng FFmpeg merge audio).
     👉 [Đăng ký tại Fal.run](https://fal.run/) (miễn phí cho lượng sử dụng nhỏ).
   - **Google Drive OAuth 2.0** (để lưu audiobook cuối cùng).
     👉 [Cấu hình tại Google Cloud Console](https://developers.google.com/drive/api/v3/quickstart/python).

3. **Google Drive Folder ID**:
   - Thiết lập **thư mục đích mục tiêu** trong Google Drive để lưu audiobook cuối cùng.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [đây](https://n8n.io/workflows/13030) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [link trên](#) và dán vào **n8n Editor** → **Import Workflow**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **14 node**, nhưng các node **quan trọng nhất** cần cấu hình kỹ như sau:

##### **A. Cấu Hình Google Sheets**
- **Node: "Get scripts"** và **"Update Temp URL"**
  - **Credentials**: Chọn `googleSheetsOAuth2Api` đã cấu hình trước.
  - **Sheet Name**: Đặt tên trùng với **bảng dữ liệu mẫu** (vd: `Audiobook Scripts`).
  - **Range**: Chọn toàn bộ dữ liệu (vd: `Sheet1!A:F`).
  - **Lưu ý**:
    - Đảm bảo **cột `Temp URL`** trống ban đầu để workflow tự động cập nhật.
    - **Cột `To Merge`** sẽ được tự động đánh dấu khi đoạn audio đã hoàn thành.

##### **B. Cấu Hình API Qwen3-TTS (Replicate)**
- **Node: "Voice Design"**
  - **Credentials**: Chọn `httpBearerAuth` và điền **Replicate API Key**.
  - **Payload**:
    ```json
    {
      "input": {
        "text": "{{$json.text}}",
        "voice_descriptions": "{{$json.Voice Description}}",
        "style_instructions": "{{$json.Style Instruction}}"
      }
    }
    ```
  - **Headers**:
    - `Content-Type`: `application/json`
    - `Authorization`: `Bearer YOUR_REPLICATE_API_KEY`

##### **C. Cấu Hình Merge Audio (FFmpeg - Fal.run)**
- **Node: "Merge Audios"**
  - **Credentials**: Chọn `httpHeaderAuth` và điền **Fal.run API Key**.
  - **Payload**:
    ```json
    {
      "inputs": [
        "{{$json.Temp URL}}"
      ],
      "output_format": "mp3"
    }
    ```
  - **Lưu ý**:
    - **Giới hạn merge 5 đoạn/lần** (do API Fal.run). Để tạo audiobook dài, cần **sử dụng vòng lặp (Loop) + Code node** để merge từng nhóm 5 đoạn trước, rồi merge lại.
    - **Node "Set AudioUrls Json"** sẽ tự động xử lý logic này bằng JavaScript.

##### **D. Cấu Hình Upload Google Drive**
- **Node: "Upload Audiobook"**
  - **Credentials**: Chọn `googleDriveOAuth2Api`.
  - **File**: Chọn `Get File` (node sau merge).
  - **Folder ID**: Điền **Folder ID** của thư mục mục tiêu trong Google Drive.
  - **File Name**: Sử dụng biểu thức:
    ```
    "Audiobook_{{$datetime.now('YYYY-MM-DD_HH-mm').toString()}}.mp3"
    ```
    (Đảm bảo tên file **không trùng** với file cũ).

##### **E. Cấu Hình Status Polling**
- **Node: "Get status"** và **"Completed?"**
  - **Credentials**: Chọn `httpHeaderAuth` (Fal.run API Key).
  - **URL**: Điền URL API của Fal.run để kiểm tra trạng thái merge.
  - **Lưu ý**:
    - Workflow sẽ **chờ 30 giây** sau mỗi lần gọi API (node `Wait 30 sec.`).
    - **Node "Completed?"** sẽ kiểm tra nếu `status === "completed"` thì tiến hành download file.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Điền **dữ liệu mẫu** vào Google Sheets (vd: 1-2 dòng với nội dung ngắn).
   - Chạy **Test Execution** trong n8n để kiểm tra các node hoạt động như mong đợi.
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** workflow và kích hoạt bằng **Manual Trigger**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tối ưu hóa giọng nói**:
   - Thử nghiệm các **mô tả giọng nói khác nhau** (vd: *"Giọng trẻ em, giọng miền Nam, giọng kể chuyện cổ tích"*).
   - Sử dụng **Style Instruction** để điều chỉnh tốc độ, âm lượng (vd: `"Giọng nói chậm rãi, âm lượng trung bình"`).

2. **Merge audiobook dài**:
   - Nếu audiobook quá dài (trên 5 đoạn), **sử dụng vòng lặp (Loop) + Code node** để merge từng nhóm 5 đoạn trước, rồi merge lại.
   - Ví dụ: Merge 10 đoạn → Merge 2 nhóm 5 đoạn → Merge 2 file mp3 thành 1.

3. **Lưu log hoạt động**:
   - Thêm **node `stickyNote`** để ghi lại lỗi hoặc trạng thái của workflow.
   - Ví dụ: `"Lỗi tại đoạn {{$node.previous.output.data.text}}: {{$node.error}}"` (sử dụng node `Code`).

4. **Gửi báo cáo định kỳ**:
   - Thêm **node Email** (n8n-nodes-base.email) để gửi email thông báo khi audiobook hoàn thành.
   - Ví dụ: Gửi email cho team với **link download** từ Google Drive.

5. **Kết hợp với Slack/Telegram**:
   - Thêm **node Slack/Telegram** để thông báo tiến trình thực thời.
   - Ví dụ: `"🎧 Audiobook đang được tạo: {{$node.previous.output.data.text}}"` (sử dụng node `Code` để format).

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào nội dung hơn, đồng thời **cải thiện chất lượng audiobook** với giọng nói cá nhân hóa và tự động hóa hoàn toàn. **Không cần code**, chỉ cần **cấu hình API và Google Sheets**, các sếp đã có thể tạo ra audiobook dài **một cách chuyên nghiệp và hiệu quả**.

👉 **Bắt đầu ngay bằng cách**:
1. Clone **Google Sheets mẫu** và điền dữ liệu.
2. Cấu hình **API Keys** (Replicate, Fal.run, Google Drive).
3. Import workflow và **bật Active**.
4. **Kích hoạt Manual Trigger** và chờ kết quả!

**Nếu có vấn đề**, các sếp có thể tham khảo:
- [Hướng dẫn chi tiết từ tác giả Davide](https://n8n.io/workflows/13030).
- [YouTube Channel của Davide](https://youtube.com/@n3witalia) (có nhiều template tự động hóa khác).

**Hãy thử ngay và chia sẻ kết quả với team của mình!** 🚀