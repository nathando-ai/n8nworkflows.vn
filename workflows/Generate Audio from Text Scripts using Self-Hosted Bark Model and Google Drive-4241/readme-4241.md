---
title: "🎙️ Tự Động Hóa Chuyển Văn Bản Sang Âm Thanh Siêu Tốc Với Bark AI + Google Drive (N8N)"
description: "Workflow tự động hóa hoàn toàn không cần code chuyển đổi văn bản từ Google Drive thành âm thanh chất lượng cao bằng mô hình Bark AI tự host, tiết kiệm thời gian và nâng cao hiệu quả nội dung marketing. Kết quả: Âm thanh tự động, chính xác, và sẵn sàng chia sẻ trên mọi nền tảng."
slug: "tieu-dong-hoa-chuyen-van-ban-sang-am-than-bark-ai-google-drive"
tags: [n8n, automation, ai, marketing, google-drive, self-hosted]
keywords: [n8n workflow tự động hóa, chuyển văn bản sang âm thanh, Bark AI tự host, Google Drive API, tự động hóa nội dung marketing]
---

# 🚀 **Tự Động Hóa Chuyển Văn Bản Sang Âm Thanh Siêu Tốc Với Bark AI + Google Drive**

### **Giải pháp cho ai?**
Các sếp **marketing**, **content creator**, hoặc **nhà sản xuất nội dung** đang mệt mỏi vì phải **ghi âm thủ công** hoặc sử dụng các công cụ AI đòi hỏi code? Hay bạn muốn **tự động hóa quá trình tạo âm thanh** từ các **script marketing, podcast, hoặc video** mà không cần phải can thiệp vào từng bước?

Workflow này **giải quyết tất cả** bằng cách:
✅ **Tự động lấy văn bản** từ Google Drive (dạng `.txt`).
✅ **Chuyển đổi sang âm thanh** bằng mô hình **Bark AI** (tự host) với chất lượng siêu thực.
✅ **Tự động upload** kết quả vào Google Drive, sẵn sàng chia sẻ trên **YouTube, podcast, hoặc email marketing**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và tối ưu hiệu suất, các sếp nên **self-host n8n** trên **VPS** với cấu hình tối thiểu:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**).
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ cho workflow này chạy mượt).
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần ghi âm thủ công, chỉ cần **upload script** là xong.
- **Chất lượng âm thanh cao**: Sử dụng mô hình **Bark AI** (tự host) cho giọng nói **tự nhiên, đa dạng**.
- **Tự động hóa hoàn toàn**: Workflow chạy **24/7**, không cần can thiệp.
- **Dễ dàng chia sẻ**: Âm thanh tự động được **upload lên Google Drive**, sẵn sàng dùng cho **video, podcast, hoặc email**.
- **Cá nhân hóa**: Thay đổi **script** là có **âm thanh mới**, không cần tái tạo.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Google Drive** (đã cấp quyền **Google Drive API**).
✔ **Folder chứa script** (định dạng `.txt`, chỉ chứa văn bản thuần túy).
✔ **Folder lưu âm thanh** (để lưu kết quả sau khi chuyển đổi).
✔ **Mô hình Bark AI tự host**:
   - Python script **`generate_voice.py`** phải được **deploy tại `/scripts/`** trên server n8n.
   - **Mô hình Bark** phải được **cài đặt và sẵn sàng** (hướng dẫn cài đặt [tại đây](https://github.com/suno-ai/bark)).
✔ **Credentials Google Drive OAuth 2.0** (cấu hình trong n8n).

---
:::note[LƯU Ý QUAN TRỌNG]
- **Script phải là `.txt`** và **chỉ chứa văn bản thuần túy** (không có định dạng HTML, code, hoặc ký tự đặc biệt).
- **Mô hình Bark** phải được **tự host** trên server n8n (không dùng API cloud).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
- **Tải file JSON** từ [n8n.io/workflows/4241](https://n8n.io/workflows/4241) và **import vào n8n Editor**.
- **Copy toàn bộ JSON** từ link trên và **paste vào n8n Editor** (tab `Import`).

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp **phải cấu hình** các node quan trọng sau:

##### **A. Cấu hình Credentials Google Drive**
- **Node "Get Scripts"** và **"Upload Audio"** cần **credentials `googleDriveOAuth2Api`**.
- **Cách cấu hình**:
  1. Vào **Settings > Credentials** trong n8n.
  2. Tạo **mới một credential** với loại **Google Drive OAuth 2.0**.
  3. **Cấp quyền** cho folder script và folder lưu âm thanh.
  4. **Ghi lại `id_repo_script`** (folder chứa script) và `id_repo_audio` (folder lưu âm thanh).

##### **B. Cấu hình Python Script Bark**
- **Node "Generate WAV"** sử dụng **command `python3 /scripts/generate_voice.py`**.
- **Yêu cầu**:
  - File `generate_voice.py` phải **được deploy tại `/scripts/`** trên server n8n.
  - Script phải **đọc input từ stdin** và **ghi output ra file `.wav`**.
  - **Ví dụ script cơ bản**:
    ```python
    import sys
    import bark
    from bark import SAMPLE_RATE, generate_audio, preload_models

    preload_models()
    text = sys.stdin.read()
    audio_array = generate_audio(text)
    bark.save_audio(audio_array, "output.wav")
    ```
  - **Lưu ý**: Nếu mô hình Bark **không tự động tải**, các sếp phải **cài đặt trước** bằng lệnh:
    ```bash
    pip install bark
    ```

##### **C. Cấu hình Inputs**
- **Node "Test Values"** cần **điền 2 tham số**:
  - `id_repo_script`: **ID folder Google Drive chứa script** (dạng `folder_id`).
  - `id_repo_audio`: **ID folder Google Drive lưu âm thanh**.

##### **D. Cấu hình Batch Processing**
- **Node "Loop Scripts"** (splitInBatches) sẽ **chia script thành batch** để xử lý đồng thời.
- **Khuyến nghị**:
  - **Batch size = 1** (nếu script dài hoặc mô hình Bark cần nhiều RAM).
  - **Delay giữa batch** (nếu server quá tải).

#### **3. Kích hoạt ⚡️**
1. **Test run** với **1 file script mẫu**:
   - Chọn **node "Start: Manual Test"** và **click "Execute"**.
   - Kiểm tra **file `.wav`** được tạo ra và **upload lên Google Drive**.
2. **Bật Active workflow**:
   - Chuyển **node "Start: External Trigger"** sang **Active**.
   - **Cấu hình Webhook** (nếu muốn kích hoạt từ bên ngoài).

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động tạo playlist âm thanh**:
   - Sau khi **upload audio**, các sếp có thể **kết hợp với YouTube API** để tự động tạo playlist từ danh sách âm thanh.

2. **Gửi âm thanh qua Slack/Telegram**:
   - **Thêm node Slack/Telegram** sau "Upload Audio" để **báo cáo kết quả** hoặc **chia sẻ âm thanh ngay khi hoàn thành**.

3. **Lưu log hoạt động**:
   - **Thêm node `stickyNote`** để **ghi lại lịch sử** (file nào đã xử lý, thời gian, lỗi nếu có).

4. **Tối ưu mô hình Bark**:
   - Nếu **âm thanh chất lượng không tốt**, các sếp có thể:
     - **Tăng RAM** cho server.
     - **Sử dụng mô hình Bark mới nhất** (check [GitHub](https://github.com/suno-ai/bark)).
     - **Optimize script Python** để giảm thời gian xử lý.

5. **Tự động xóa script cũ**:
   - **Thêm node Google Drive** để **xóa file `.txt`** sau khi đã chuyển đổi thành âm thanh.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc **ghi âm thủ công** và **tự động hóa hoàn toàn** quá trình tạo âm thanh từ văn bản. Với **Bark AI tự host** và **Google Drive**, các sếp có thể:
✔ **Tạo âm thanh siêu thực** chỉ bằng **1 click**.
✔ **Chia sẻ nhanh** trên **YouTube, podcast, hoặc email**.
✔ **Tiết kiệm chi phí** so với việc thuê giọng nói chuyên nghiệp.

**Hành động ngay!**
1. **Import workflow** và **cấu hình** theo hướng dẫn.
2. **Upload script đầu tiên** và **chờ kết quả âm thanh**.
3. **Tích hợp với Slack/Telegram** để **báo cáo tự động**.

**🚀 Cùng tự động hóa nội dung của mình ngay hôm nay!** 🎤