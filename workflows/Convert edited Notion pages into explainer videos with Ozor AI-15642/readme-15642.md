---
title: "🎬 Tự Động Chuyển Đổi Trang Notion Đã Sửa Sang Video Giải Thích Với Ozor AI – Không Cần Code!"
description: "Workflow tự động hóa chuyển đổi các trang Notion (SOP) đã chỉnh sửa thành video đào tạo chuyên nghiệp bằng Ozor AI, tự động cập nhật vào trang gốc. Giúp doanh nghiệp tiết kiệm thời gian, duy trì nội dung đồng bộ và nâng cao trải nghiệm học tập cho nhân viên."
slug: "tieu-dong-chuyen-doi-notion-sang-video-ozor-ai"
tags: [n8n, automation, content-creation, multimodal-ai, notion, ozor-ai]
keywords: [n8n workflow tự động hóa, chuyển đổi Notion sang video, Ozor AI, tự động hóa đào tạo nội bộ, video LMS tự động]
---

# 🚀 **Tự Động Chuyển Đổi Trang Notion Đã Sửa Sang Video Giải Thích Với Ozor AI**

### **Giải pháp hoàn hảo cho các sếp muốn:**
- **Tiết kiệm 100 giờ/năm** không phải thủ công cập nhật video đào tạo khi SOP thay đổi.
- **Duy trì nội dung đồng bộ** giữa tài liệu Notion và video LMS.
- **Nâng cao hiệu quả đào tạo** với video chuyên nghiệp, tự động sinh ra từ nội dung hiện có.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7 ổn định, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ export video nhanh)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công khi SOP thay đổi.
✅ **Video chuyên nghiệp**: Ozor AI tự động phân tích nội dung và thiết kế video với phong cách phù hợp.
✅ **Duy trì đồng bộ**: Video luôn cập nhật cùng với trang Notion gốc.
✅ **Tiết kiệm chi phí**: Không cần thuê nhà sản xuất video cho mỗi lần cập nhật.
✅ **Tăng cường trải nghiệm học tập**: Video động hình ảnh hơn so với tài liệu văn bản.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Notion**:
   - **Trình độ**: Admin hoặc có quyền đọc/viết vào database "Document Hub".
   - **Thông tin cần cung cấp**:
     - API Key Notion (tạo tại [Notion Developer](https://www.notion.so/my-integrations)).
     - Database chứa các trang SOP (Standard Operating Procedures) cần tự động hóa.

2. **Tài khoản Ozor AI**:
   - **Trình độ**: Tài khoản Pro (đảm bảo giới hạn API đủ cho video export).
   - **Thông tin cần cung cấp**:
     - API Key Ozor (tạo tại [Ozor Dashboard](https://ozor.ai/)).
     - **Lưu ý**: Các sếp cần **cấu hình credential** trong n8n với tên:
       - `notionApi` (cho Notion).
       - `ozorApi` (cho Ozor).

3. **Hạ tầng kỹ thuật**:
   - **VPS** (n8n self-hosted) với tối thiểu **2GB RAM** (để xử lý video export).
   - **Thời gian chạy**: ~5–10 phút/lần (do thời gian export video là bước chậm nhất).
   - **Lưu trữ**: Không cần thêm, Ozor tự lưu video vào Google Cloud Storage.

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/15642](https://n8n.io/workflows/15642) và import vào n8n Editor.
- **Copy/paste JSON** từ file vào tab "Import" của n8n.

:::note[Lưu ý quan trọng]
- **Không sử dụng phiên bản n8n Community** (n8n.io) vì giới hạn API và thời gian chạy.
- **Không xóa node nào** trong workflow, chỉ chỉnh sửa các tham số sau:
:::

---

### **2. Các bước chỉnh sửa BẮT BUỘC**
#### **🔹 Node 1: Every 15 Minutes**
- **Giữ nguyên** thời gian trigger là **15 phút** (đảm bảo không trùng với thời gian export video).
- **Lưu ý**: Nếu video export thường mất >5 phút, các sếp nên **giảm thời gian trigger** (ví dụ: 30 phút) để tránh xung đột.

#### **🔹 Node 2: Notion — Recently Edited SOPs**
- **Không cần chỉnh sửa** vì node này tự động lấy trang SOP mới nhất.
- **Yêu cầu**: Database Notion phải có các trường sau:
  - `name` (tên trang).
  - `last_edited_time` (thời gian chỉnh sửa).
  - `category` (danh mục SOP, ví dụ: "HR", "Tech").

#### **🔹 Node 3 & 4: Get Many Child Blocks + Code (JavaScript)**
- **Node 3** tự động lấy tất cả block (text, image) từ trang Notion.
- **Node 4 (Code)** cần **không chỉnh sửa** vì nó tự động xây dựng prompt cho Ozor AI:
  ```javascript
  // Nội dung mã tự động chạy, các sếp chỉ cần đảm bảo:
  - Block URL (`{{ $json.url }}`) đúng với trang Notion.
  - Thư viện JavaScript trong n8n đã được cài đặt (n8n tự động cung cấp).
  ```
- **Lưu ý**: Nếu trang Notion có **nhiều block >50**, các sếp cần chỉnh `Limit` từ 50 thành số lớn hơn.

#### **🔹 Node 5: Ozor — Analyze Notion Page**
- **Không cần chỉnh sửa** vì node này tự động phân tích nội dung và tạo **video plan**.
- **Yêu cầu**: API Key Ozor đã được cấu hình trong `ozorApi`.

#### **🔹 Node 6 & 7: Ozor — Generate From Plan + Export a Video**
- **Node 6** bắt đầu tạo video từ plan.
- **Node 7** export video MP4 (thời gian chờ ~5 phút).
- **Lưu ý**:
  - Nếu video export thất bại, kiểm tra:
    - **API Key Ozor** có hiệu lực không.
    - **Thời gian chạy** của n8n có đủ (n8n self-hosted).
    - **Lưu trữ Ozor** có đủ dung lượng không (hiển thị trong dashboard Ozor).

#### **🔹 Node 8: Append a Block (Notion)**
- **Chỉnh sửa**:
  - **Target Block ID**: Đảm bảo trỏ đến **trang Notion gốc** của SOP.
    ```json
    {{ $('Get many child blocks').all()[0].json.parent.page_id }}
    ```
  - **Block Type**: Giữ nguyên là **Image**.
  - **Image URL**: Đảm bảo lấy từ `{{ $json.downloadUrl }}` (link video từ Ozor).

---

### **3. Kích hoạt ⚡️ Workflow**
1. **Test run** với một trang SOP mẫu:
   - Chọn **Execute workflow** trên canvas.
   - Kiểm tra:
     - Video có xuất hiện trong Notion không?
     - Có lỗi nào trong log không?
2. **Bật Active** nếu test thành công.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tối ưu hóa thời gian chạy**
- **Chỉ chạy vào giờ không bận**: Ví dụ: 22h–6h sáng (giảm tải server).
- **Sử dụng node `set`** để lưu trạng thái export (tránh chạy trùng).

### **2. Cập nhật video định kỳ**
- **Thêm node `scheduleTrigger`** để chạy workflow vào đầu tuần (ví dụ: Chủ Nhật 8h sáng) để **cập nhật tất cả video**.

### **3. Gửi thông báo khi video sẵn sàng**
- **Kết hợp với Slack/Email**:
  ```json
  {
    "operation": "sendMessage",
    "resource": "slack",
    "message": "🎥 Video mới đã cập nhật cho SOP: {{ $json.name }}",
    "channel": "#training-updates"
  }
  ```

### **4. Lưu log cho theo dõi**
- **Thêm node `set`** để lưu:
  - ID trang Notion.
  - Link video.
  - Thời gian export.
  - Trạng thái (thành công/thất bại).

### **5. Xử lý lỗi tự động**
- **Thêm node `if`** để:
  - Nếu export thất bại, gửi **email cảnh báo** cho team.
  - Nếu Notion không lấy được trang, **log lỗi** và tiếp tục.

---

## 📌 **Kết luận**
Workflow này **giải phóng hoàn toàn thời gian** của các sếp khỏi việc thủ công cập nhật video đào tạo khi SOP thay đổi. Với **Ozor AI + n8n**, nội dung Notion được tự động chuyển thành video chuyên nghiệp, đồng bộ và luôn mới nhất.

### **Hành động ngay hôm nay:**
1. **Import workflow** và cấu hình credential.
2. **Test với 1–2 trang SOP** để đảm bảo hoạt động.
3. **Bật tự động hóa** và **quên đi việc cập nhật video thủ công!**

👉 **Bắt đầu tự động hóa ngay** với [n8n self-hosted](https://n8n.io/) và [Ozor AI](https://ozor.ai/)!

---
**Cần hỗ trợ?** Đăng ký tư vấn miễn phí tại [TinoHost](https://tino.vn/vps-n8n?affid=388) hoặc liên hệ [Ozor AI](https://ozor.ai/support).