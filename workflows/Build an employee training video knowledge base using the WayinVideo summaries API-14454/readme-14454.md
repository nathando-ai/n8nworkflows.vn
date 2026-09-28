---
title: "🎥 Tự Động Tạo Bảng Kiến Thức Học Tập Từ Video Bằng AI (Không Cần Code)"
description: "Workflow này tự động chuyển đổi video đào tạo YouTube thành bảng kiến thức cấu trúc, tiết kiệm thời gian cho các sếp 100% bằng AI + API WayinVideo. Kết quả: Bảng tổng hợp thông tin chi tiết, dễ tìm kiếm, và cập nhật tự động."
slug: "tay-dong-tao-bang-kien-thuc-tu-video-bang-ai"
tags: [n8n, automation, ai-summarization, google-sheets, wayinvideoa, no-code]
keywords: [tự động hóa video đào tạo, tạo bảng kiến thức từ video, ai tóm tắt video, wayinvideoa api, n8n workflow tự động]
---

# 🚀 **Tự Động Tạo Bảng Kiến Thức Học Tập Từ Video Bằng AI (Không Cần Code)**

## **Nỗi Đau Của Các Sếp**
Các sếp đã từng phải:
- **Tốn thời gian** sao chép nội dung video dài hàng giờ vào tài liệu Word/Google Docs.
- **Mất trật tự** khi không biết cách lưu trữ kiến thức từ nhiều video đào tạo.
- **Không cập nhật kịp** khi video mới được đăng tải.
- **Không tận dụng được AI** để tóm tắt và phân loại thông tin hiệu quả.

**Workflow này giải quyết tất cả!** Chỉ với một video URL và tên chủ đề, hệ thống sẽ tự động:
✅ **Tóm tắt video** bằng AI (WayinVideo API).
✅ **Lọc ra những điểm nổi bật** (highlights).
✅ **Lưu vào Google Sheets** dưới dạng bảng kiến thức sẵn sàng chia sẻ.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần sao chép thủ công, AI làm tất cả trong vài phút.
- **Kiến thức hệ thống hóa**: Tất cả video đào tạo được lưu vào một bảng Google Sheets dễ tìm kiếm.
- **Cập nhật tự động**: Khi có video mới, chỉ cần submit URL là xong.
- **Dễ chia sẻ**: Bảng kiến thức có thể chia sẻ với toàn bộ đội ngũ hoặc khách hàng.
- **Tối ưu hóa học tập**: AI tóm tắt và phân loại thông tin chính xác, giúp nhân viên học nhanh hơn.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **API Key của WayinVideo** (đăng ký tại [WayinVideo](https://wayinvideoa.com/)).
2. **Tài khoản Google** (để kết nối với Google Sheets).
3. **Google Sheet đã chuẩn bị** với các cột sau:
   - **Topic/Department** (Chủ đề/Phòng ban)
   - **Video URL** (Link video)
   - **Video Title** (Tiêu đề video)
   - **Key Summary** (Tóm tắt chính)
   - **Highlights** (Điểm nổi bật)
   - **Tags** (Nhãn phân loại)
4. **Mã giảm giá VPS** (nếu tự host n8n):
   - 🎁 **VPSN8N** (giảm 39% tại [TinoHost](https://tino.vn/vps-n8n?affid=388))
   - Xeon 4GB chỉ **50k/tháng** ([BNIX](https://my.bnix.one/aff.php?aff=172))
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ file JSON**
1. Tải workflow từ [n8n.io](https://n8n.io/workflows/14454) (đăng nhập tài khoản).
2. Nhấn **Export** (icon ba chấm) → Chọn **Export as JSON**.
3. Trên n8n Editor của bạn, nhấn **Import** (icon mũi tên vào) → Dán JSON vào và nhấn **Import**.

#### **Cách 2: Copy/Paste JSON**
1. Mở n8n Editor → Nhấn **Import** → Chọn **Paste JSON**.
2. Copy toàn bộ JSON từ [n8n.io/workflows/14454](https://n8n.io/workflows/14454) → Dán vào và nhấn **Import**.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **6 node chính**, nhưng **3 node quan trọng nhất** cần cấu hình kỹ:

#### **🔹 Node 1: Form Trigger (Bắt đầu workflow)**
- **Tên node**: "Form — Video URL + Topic1"
- **Cấu hình**:
  - Thêm **2 trường nhập**:
    - **Video URL** (loại: `text`, bắt buộc).
    - **Topic/Department** (loại: `text`, bắt buộc).
  - **Chia sẻ form** với đội ngũ qua link (sau khi hoàn thành).

#### **🔹 Node 2 & 4: WayinVideo API Requests (Tóm tắt video)**
- **Tên node**:
  - "WayinVideo — Submit Summary Request" (**Node 2**).
  - "WayinVideo — Fetch Summary Result" (**Node 4**).
- **Cấu hình**:
  - **Headers**:
    - `Authorization`: `Bearer YOUR_WAYINVIDEO_API_KEY` (thay `YOUR_WAYINVIDEO_API_KEY` bằng API Key của bạn).
    - `Content-Type`: `application/json`.
  - **Body (Node 2)**:
    ```json
    {
      "url": "{{ $input.current.url }}"
    }
    ```
  - **URL API**:
    - **Node 2**: `https://api.wayinvideoa.com/summarize`
    - **Node 4**: `https://api.wayinvideoa.com/status` (để kiểm tra trạng thái tóm tắt).

#### **🔹 Node 5: If Condition (Kiểm tra highlights đã sẵn sàng)**
- **Tên node**: "Check — Highlights Ready?"
- **Cấu hình**:
  - **Condition**: `{{ $json.status }} === "completed"` (kiểm tra trạng thái hoàn tất).
  - **Nếu đúng**: Tiến đến **Node 6** (lưu vào Google Sheets).
  - **Nếu sai**: Quay lại **Node 3** (đợi 30s) và **Node 4** (kiểm tra lại).

#### **🔹 Node 6: Google Sheets (Lưu kết quả)**
- **Tên node**: "Save — Append Row to Google Sheet"
- **Cấu hình**:
  - **Credentials**: Chọn tài khoản Google đã kết nối.
  - **Google Sheets URL**: Thay bằng link của sheet của bạn (ví dụ: `https://docs.google.com/spreadsheets/d/ID_SHEET/edit`).
  - **Sheet Name**: Tên sheet (ví dụ: `Training_Knowledge_Base`).
  - **Row Data**:
    ```json
    {
      "Topic/Department": "{{ $input.current.topic }}",
      "Video URL": "{{ $input.current.url }}",
      "Video Title": "{{ $json.title }}",
      "Key Summary": "{{ $json.summary }}",
      "Highlights": "{{ $json.highlights }}",
      "Tags": "{{ $input.current.topic }}",
      "Date Added": "{{ $now }}"
    }
    ```
  - **Operation**: `Append` (thêm hàng mới).

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với một video mẫu:
   - Nhập URL video và chủ đề vào form → Kiểm tra workflow có chạy không.
   - Xem kết quả trong Google Sheets.
2. **Bật Active**:
   - Nhấn **Active** trên workflow → Workflow sẽ hoạt động 24/7.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CẬP NHẬT & TỐI ƯU]
- **Thêm thông báo Slack/Email**:
  - Sau **Node 6**, thêm **Slack Node** hoặc **Email Node** để thông báo khi có video mới được lưu.
  - Ví dụ Slack:
    ```json
    {
      "text": "📌 New training video added:\n🎥 {{ $input.current.url }}\n📝 Topic: {{ $input.current.topic }}"
    }
    ```
- **Thêm ngày cập nhật tự động**:
  - Trong **Node 6**, thêm cột `Date Added` bằng `{{ $now }}` để biết thời gian lưu.
- **Giới hạn số lần retry**:
  - Thêm **Node Counter** trước **Node 5** để tránh vòng lặp vô hạn (ví dụ: chỉ retry 5 lần).
- **Tùy chỉnh thời gian đợi**:
  - Trong **Node 3 (Wait)**, tăng thời gian đợi từ 30s lên 1-2 phút nếu video dài.
:::

---

## ⚠️ **Lưu Ý Quan Trọng**
:::warning[TRÁNH VÒNG LẬP VÔ HẠN]
- **Rủi ro**: Nếu WayinVideo không trả về highlights, workflow sẽ retry vô hạn.
- **Giải pháp**:
  - Thêm **Node Counter** để giới hạn số lần retry (ví dụ: 5 lần).
  - Thêm **Node If** kiểm tra số lần retry đã vượt quá giới hạn → Dừng workflow và gửi email thông báo lỗi.
:::

---

## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa việc tạo bảng kiến thức từ video đào tạo **không cần viết code**. Bằng cách kết hợp **API WayinVideo** và **n8n**, bạn đã có một hệ thống:
✔ **Tiết kiệm thời gian** (AI làm tất cả).
✔ **Kiến thức hệ thống hóa** (Google Sheets).
✔ **Cập nhật tự động** (chỉ cần submit URL).
✔ **Dễ chia sẻ** (chia sẻ link Google Sheets).

**Hành động ngay!**
1. **Đăng ký API Key WayinVideo** ([Đăng ký miễn phí](https://wayinvideoa.com/)).
2. **Chuẩn bị Google Sheet** với các cột cần thiết.
3. **Import workflow** và cấu hình theo hướng dẫn.
4. **Chia sẻ form** với đội ngũ để bắt đầu tự động hóa!

**Nếu có vấn đề**, hãy để lại comment bên dưới hoặc liên hệ với tác giả [isaWOW](https://n8n.io/workflows/14454) trên n8n.io. 🚀