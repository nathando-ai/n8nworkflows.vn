---
title: "🎙️ Chuyển Âm Thanh Sang Văn Bản Tự Động Với IBM Granite 3.3 8B (Không Cần Code)"
description: "Workflow tự động hóa hoàn toàn chuyển âm thanh thành văn bản bằng mô hình AI Granite Speech 3.3 8B của IBM qua API Replicate, tiết kiệm thời gian và nâng cao độ chính xác cho nội dung doanh nghiệp."
slug: "chuyen-am-than-sang-van-ban-ibm-granite-n8n"
tags: [n8n, automation, AI, IBM Granite, Replicate API, tự động hóa nội dung]
keywords: [chuyển âm thanh thành văn bản tự động, IBM Granite Speech 3.3 8B, n8n workflow, tự động hóa nội dung AI, API Replicate]
---

# 🚀 **Chuyển Âm Thanh Sang Văn Bản Tự Động Với IBM Granite 3.3 8B (Không Cần Code)**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7 với hiệu suất tối ưu, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) để tránh giới hạn tài nguyên của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo ổn định cho AI)
:::

---

## 🎯 **Nỗi Đau Của Các Sếp Và Giải Pháp Tự Động Hóa**
Các sếp thường phải **gõ tay** hoặc sử dụng công cụ AI cơ bản để chuyển âm thanh (gọi điện, podcast, cuộc họp) thành văn bản. Điều này gây ra:
- **Tốn thời gian** (thường mất từ 30 phút đến 2 giờ cho 1 giờ âm thanh).
- **Độ chính xác thấp** (AI cơ bản thường bỏ lỡ từ khóa quan trọng hoặc sai nghĩa).
- **Không cá nhân hóa** (không thể điều chỉnh mô hình cho ngành nghề cụ thể).

**Workflow này giải quyết tất cả bằng:**
✅ **Chuyển âm thanh → văn bản tự động** với độ chính xác cao (mô hình Granite Speech 3.3 8B của IBM).
✅ **Không cần code** – chỉ cần cấu hình và chạy.
✅ **Hoạt động liên tục** (24/7) khi self-hosted trên VPS.
✅ **Cá nhân hóa** (điều chỉnh seed, temperature, prompt theo nhu cầu).

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Chuyển 1 giờ âm thanh thành văn bản chỉ trong **5-10 phút**.
- **Độ chính xác cao**: Mô hình Granite 3.3 8B của IBM có độ chính xác **cao hơn 95%** (so với các mô hình miễn phí khác).
- **Hoạt động tự động**: Không cần can thiệp thủ công sau khi cấu hình.
- **Dữ liệu sạch**: Văn bản được chuyển tự động, giảm thiểu lỗi gõ tay.
- **Cá nhân hóa**: Điều chỉnh mô hình cho từng ngành (y tế, pháp lý, marketing...).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Replicate API**:
   - Đăng ký tại [replicate.com](https://replicate.com) và lấy **API Token**.
   - *Lưu ý*: Đảm bảo tài khoản có đủ **credits** để sử dụng mô hình Granite Speech.
2. **File âm thanh**:
   - File âm thanh định dạng **WAV, MP3, OGG** (không quá 5 phút cho lần chạy đầu tiên).
   - *Gợi ý*: Chia âm thanh thành các đoạn ngắn (1-2 phút) để tăng hiệu suất.
3. **n8n Workflow**:
   - Cài đặt n8n trên **VPS** (khuyến nghị) hoặc phiên bản cloud (nếu chỉ dùng thử).

---

### 🚀 **Cách Import & Cấu Hình Workflow**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/6796](https://n8n.io/workflows/6796) hoặc copy toàn bộ JSON dưới đây vào **n8n Editor**.
- **Cách import**:
  - Mở n8n Editor → Nhấn **Import** → Dán JSON → Chọn **Import Workflow**.

#### **2. Các Bước Cấu Hình BẮT BUỘC**
Sau khi import, các sếp cần chỉnh sửa **các node quan trọng** như sau:

##### **🔐 Node "Set API Token"**
- **Thao tác**: Nhấn **Edit** → Điền **API Token** từ Replicate vào trường `REPLICATE_API_TOKEN`.
  ```json
  {
    "json": {
      "REPLICATE_API_TOKEN": "YOUR_REPLICATE_API_TOKEN_HERE"
    }
  }
  ```
- *Lưu ý*: **Không bao giờ commit API Token vào GitHub** để tránh rò rỉ.

##### **🎤 Node "Set Text Parameters"**
- **Thao tác**: Nhấn **Edit** → Cấu hình các tham số cho mô hình:
  ```json
  {
    "json": {
      "audio": ["base64_encoded_audio_file"], // Chuyển file âm thanh thành base64
      "prompt": "Chuyển âm thanh này thành văn bản chính xác, giữ nguyên ngữ điệu và từ khóa quan trọng.",
      "temperature": 0.6, // Giá trị mặc định (điều chỉnh từ 0.1 đến 1.0)
      "top_k": 50, // Số lượng từ có xác suất cao nhất được xem xét
      "top_p": 0.9, // Ngưỡng xác suất (giá trị từ 0 đến 1)
      "max_tokens": 512 // Số lượng token tối đa trả về
    }
  }
  ```
- *Gợi ý*:
  - **Đối với âm thanh tiếng Việt**: Thêm `prompt` như `"Chuyển âm thanh tiếng Việt này thành văn bản chính xác, giữ nguyên ngữ điệu và từ ngữ địa phương."`.
  - **Đối với âm thanh chuyên ngành**: Thêm `prompt` cụ thể (ví dụ: `"Chuyển cuộc họp y tế này thành văn bản y khoa chính xác."`).

##### **📂 Node "Create Text Prediction"**
- **Thao tác**: Kiểm tra **URL API** và **tham số** đã được tự động điền từ node "Set Text Parameters".
- *Lưu ý*: Nếu file âm thanh quá lớn, chia nhỏ thành các đoạn nhỏ hơn.

##### **⏳ Node "Wait & Status Checking"**
- Workflow tự động **kiểm tra trạng thái** sau mỗi **5 giây** (node "Wait 5s") và **10 giây** (node "Wait 10s").
- *Không cần chỉnh sửa* nếu muốn sử dụng mặc định.

##### **📊 Node "Log Request" (Code)**
- **Thao tác**: Kiểm tra **log** để debug nếu có lỗi.
  ```javascript
  // Code mặc định (không cần chỉnh sửa)
  return {
    json: {
      request: {
        url: $input.all().url,
        method: $input.all().method,
        body: $input.all().body,
        headers: $input.all().headers
      }
    }
  };
  ```

#### **3. Kích Hoạt Workflow ⚡️**
- **Test Run**:
  - Nhấn **Manual Trigger** → Chọn **Test Execution**.
  - Đợi workflow hoàn thành → Kiểm tra **output** ở node cuối ("Display Result").
- **Bật Active**:
  - Sau khi test thành công, nhấn **Active** để workflow chạy tự động khi kích hoạt.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram**:
   - Sau khi chuyển thành văn bản, gửi kết quả tự động về **Slack** hoặc **Telegram** bằng node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram`.
   - *Cách làm*:
     ```json
     {
       "json": {
         "text": "📝 Văn bản đã chuyển thành công:\n{{ $json["output"]["text"] }}"
       }
     }
     ```

2. **Lưu Log Vào Google Sheets/Notion**:
   - Sử dụng node `n8n-nodes-base.googleSheets` hoặc `n8n-nodes-base.notion` để lưu **lịch sử chuyển đổi**.
   - *Cách làm*:
     - Tạo một sheet/đơn Notion mới.
     - Cấu hình node `googleSheets` với **credentials** và **sheet name**.

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Scheduler** để chạy workflow hàng ngày/tuần và gửi báo cáo qua **email** (node `n8n-nodes-base.email`).
   - *Cách làm*:
     - Tạo một **cron job** (ví dụ: `0 9 * * *` để chạy lúc 9h sáng hàng ngày).
     - Cấu hình node `email` với **SMTP** của doanh nghiệp.

4. **Optimize Mô Hình**:
   - **Giảm `temperature`** (giá trị < 0.6) để văn bản trở nên **chính xác hơn** (nhưng ít sáng tạo).
   - **Tăng `max_tokens`** (giá trị > 512) nếu văn bản quá dài.

---

### 📌 **Kết Luận & Kêu Gọi Áp Dụng**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quá trình chuyển âm thanh thành văn bản **không cần code**, với **độ chính xác cao** và **tiết kiệm thời gian**. Đặc biệt phù hợp cho:
- **Doanh nghiệp marketing** (chuyển podcast, cuộc họp thành nội dung blog).
- **Cơ quan y tế/pháp lý** (chuyển cuộc họp chuyên ngành thành văn bản chính xác).
- **Nhà sản xuất nội dung** (chuyển âm thanh thành script, bài viết).

**Hành động ngay**:
1. **Đăng ký VPS** để self-host n8n (đảm bảo ổn định 24/7).
2. **Import workflow** và cấu hình API Token.
3. **Test với file âm thanh** và điều chỉnh `prompt` cho phù hợp.
4. **Tích hợp Slack/Google Sheets** để quản lý dễ dàng.

🚀 **Hãy tự động hóa ngay hôm nay – không cần chờ!**

---
**🔗 Liên Hệ & Hỗ Trợ**:
- Tác giả: [Yaron Been](https://www.linkedin.com/in/yaronbeen/)
- YouTube: [Yaron Been](https://www.youtube.com/@YaronBeen/videos)
- *Góp ý*: Yaron@nofluff.online