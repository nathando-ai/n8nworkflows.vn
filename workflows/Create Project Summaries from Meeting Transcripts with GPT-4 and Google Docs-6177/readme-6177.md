---
title: "🤖 Tự Động Tóm Tắt Cuộc Họp từ Transcript sang Google Docs với GPT-4 (Không Cần Code)"
description: "Workflow tự động hóa lấy nội dung cuộc họp từ Google Docs, sử dụng GPT-4 tóm tắt và lưu kết quả vào tài liệu mới với cấu trúc chuyên nghiệp - tiết kiệm thời gian cho các sếp lên báo cáo hàng tuần."
slug: "tu-dong-tom-tat-cuoc-hop-voi-gpt-4-google-docs"
tags: [n8n, automation, ai-summarization, google-docs, gpt-4, no-code]
keywords: [tự động hóa cuộc họp, tóm tắt cuộc họp với AI, gpt-4 google docs, workflow n8n, tự động hóa báo cáo dự án]
---

# 🚀 **Tự Động Tóm Tắt Cuộc Họp từ Transcript sang Google Docs với GPT-4**

### **Nỗi Đau Của Các Sếp**
Các sếp thường phải mất **30-60 phút/tuần** để:
- Đọc lại transcript cuộc họp dài 10-20 trang.
- Tóm tắt nội dung chính để gửi cho CEO hoặc khách hàng.
- Chỉnh sửa lại cấu trúc để phù hợp với yêu cầu báo cáo.

**Workflow này giải quyết tất cả bằng một cú nhấp chuột!** Nó tự động:
✅ **Lấy transcript** từ Google Docs.
✅ **Tóm tắt bằng GPT-4** với cấu trúc chuyên nghiệp.
✅ **Lưu kết quả** vào tài liệu mới với tiêu đề và phân đoạn logic.
✅ **Hoạt động 24/7** khi tự động hóa trên VPS.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 50% thời gian** so với cách làm thủ công.
- **Độ chính xác cao** nhờ GPT-4 tóm tắt logic và ngữ cảnh.
- **Cấu trúc chuyên nghiệp** với tiêu đề tự động (e.g., "Điểm chính", "Hành động cần thực hiện").
- **Hoạt động liên tục** khi chạy trên VPS (không phụ thuộc vào máy tính cá nhân).
- **Dễ dàng mở rộng** cho nhiều dự án khác nhau.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** với quyền truy cập vào:
   - **Google Docs** (để lấy transcript và lưu kết quả).
   - **Google Drive API** (để tạo tài liệu mới).
2. **API Key OpenAI** (để sử dụng GPT-4).
3. **File transcript** đã được lưu trong Google Docs (ví dụ: `Cuộc họp dự án ABC - 2024-05-20`).
4. **VPS** (để chạy workflow 24/7 - **không thể chạy trên máy tính cá nhân**).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/6177](https://n8n.io/workflows/6177) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **9 node**, nhưng các sếp cần chú ý đặc biệt đến **3 node quan trọng**:

##### **A. Node `Get meeting transcript` (Google Docs)**
- **Chức năng:** Lấy nội dung từ file transcript đã chọn.
- **Cách cấu hình:**
  1. Vào **Google Docs OAuth2Api** (credentials) và **cập nhật lại token** (nếu đã hết hạn).
  2. Trong node `Get meeting transcript`:
     - Chọn **File ID** của transcript (để tìm: mở file Google Docs → URL sẽ có dạng `https://docs.google.com/document/d/[FILE_ID]/edit`).
     - Chọn **Sheet Name** (nếu transcript là file Excel) hoặc **Document Name** (nếu là file Docs).
     - **Operation:** Đặt là `get`.

##### **B. Node `OpenAI Chat Model` (GPT-4)**
- **Chức năng:** Tóm tắt transcript bằng GPT-4.
- **Cách cấu hình:**
  1. Vào **OpenAI API** (credentials) và điền **API Key** (tạo tại [OpenAI](https://platform.openai.com/)).
  2. Trong node `OpenAI Chat Model`:
     - **Model:** Đặt là `gpt-4.1-mini` (rẻ hơn GPT-4 nhưng vẫn hiệu quả).
     - **Prompt:** Sẵn sàng trong workflow, nhưng các sếp có thể **tùy chỉnh** để phù hợp với yêu cầu:
       ```plaintext
       Tóm tắt nội dung cuộc họp dưới dạng:
       1. Điểm chính (3-5 điểm)
       2. Hành động cần thực hiện (AI, Dev, PM)
       3. Thời gian hoàn thành
       4. Người chịu trách nhiệm
       ```
     - **Temperature:** Đặt là `0.7` (để kết quả logic hơn).

##### **C. Node `CreateGoogleDoc` (Tạo tài liệu mới)**
- **Chức năng:** Lưu kết quả tóm tắt vào Google Docs mới.
- **Cách cấu hình:**
  1. Đảm bảo **Google Drive OAuth2Api** đã được cấu hình (cùng credentials với node `Get meeting transcript`).
  2. Trong node `CreateGoogleDoc`:
     - **Title:** Đặt tên tự động như `Tóm tắt Cuộc họp - [Tên dự án]` (sử dụng node `set_fields` để động).
     - **Content:** Chọn kết quả từ node `Project Summary` (sẽ được truyền tự động).

#### **3. Kích Hoạt ⚡️**
1. **Test Run:**
   - Nhấn **Execute Workflow** để thử với một file transcript mẫu.
   - Kiểm tra kết quả trong Google Docs mới tạo.
2. **Bật Active:**
   - Sau khi kiểm tra thành công, **bật Active** để workflow hoạt động tự động khi có trigger.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH LÀM NÂNG CAO]
1. **Tự động hóa định kỳ:**
   - Sử dụng **n8n Trigger Node** (n8n-nodes-base.schedule) để chạy workflow hàng tuần (ví dụ: Chủ Nhật 8h sáng).
   - Cấu hình trong **Schedule Node**:
     - **Cron:** `0 8 * * 0` (Chủ Nhật, 8h sáng).
     - **Time Zone:** Đặt theo giờ Việt Nam (`Asia/Ho_Chi_Minh`).

2. **Gửi kết quả qua Email/Slack:**
   - Thêm **node `n8n-nodes-base.email`** hoặc **`n8n-nodes-base.slack`** sau node `CreateGoogleDoc` để thông báo kết quả.
   - Ví dụ:
     ```plaintext
     "Kết quả tóm tắt đã hoàn thành! Link: [LINK_TO_DOCS]"
     ```

3. **Lưu log hoạt động:**
   - Thêm **node `stickyNote`** để ghi lại thời gian chạy và file được xử lý.
   - Cách cấu hình:
     - **Message:** `Workflow chạy thành công - File: [{{ $json["fileName"] }}] - Thời gian: {{ $json["timestamp"] }}`

4. **Tùy chỉnh prompt cho từng dự án:**
   - Sử dụng **node `set_fields`** để truyền **tên dự án** vào prompt GPT-4.
   - Ví dụ:
     ```javascript
     // Trong node `set_fields`:
     {
       "projectName": "{{ $node["Get meeting transcript"].json["fileName"] }}"
     }
     ```
   - Sau đó, trong **prompt GPT-4**, thêm:
     ```plaintext
     "Tóm tắt cuộc họp về dự án: {{ $json["projectName"] }}"
     ```

5. **Dùng cho nhiều file cùng lúc:**
   - Thay vì lấy 1 file, các sếp có thể **lấy danh sách file** từ Google Drive và xử lý song song.
   - Cách làm:
     - Thêm **node `googleDriveListFiles`** trước `Get meeting transcript`.
     - Sử dụng **node `set`** để truyền danh sách file vào vòng lặp.
     - Thêm **node `loop`** để xử lý từng file một.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc tóm tắt cuộc họp thủ công, đồng thời **tăng chất lượng báo cáo** nhờ GPT-4. Khi chạy trên **VPS**, nó hoạt động **24/7** mà không cần can thiệp.

**Hành động ngay:**
1. **Đăng ký VPS** để tự động hóa hoàn toàn (không phụ thuộc máy tính cá nhân).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **Import workflow** và **cấu hình theo hướng dẫn** trên.
3. **Bật Active** và **quên đi công việc tóm tắt cuộc họp**!

**Chia sẻ kết quả** của các sếp sau khi sử dụng nhé! 🚀