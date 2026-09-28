---
title: "🎥 **Tự Động Hóa Chuyển Tiếng YouTube + Tránh Trùng Lặp Dữ Liệu với Transcript.io & Supabase (Miễn Phí 25 Video/Tháng)**"
description: "Workflow tự động hóa lấy video mới từ kênh YouTube, chuyển tiếng thành văn bản, tránh trùng lặp và lưu dữ liệu vào Supabase - hoàn toàn không cần code. Giúp các sếp tiết kiệm thời gian theo dõi nội dung và tối ưu hóa công việc quản lý video."
slug: "tieu-dong-hoa-chuyen-tieng-youtube-tranh-trung-lap-dulieu"
tags: [n8n, automation, youtube, transcript, supabase, no-code, youtube-transcript]
keywords: [n8n workflow youtube, tự động hóa chuyển tiếng youtube, tránh trùng lặp video, transcript.io api, supabase tự động hóa, lấy video mới youtube]
---

# 🚀 **Tự Động Hóa Chuyển Tiếng YouTube + Tránh Trùng Lặp Dữ Liệu (Miễn Phí 25 Video/Tháng)**

## **💡 Bạn đang gặp vấn đề gì?**
- **Tốn thời gian** theo dõi và chuyển tiếng hàng loạt video từ YouTube?
- **Bị trùng lặp** dữ liệu khi lưu nhiều lần cùng một video?
- **Không biết cách tự động hóa** quá trình này mà không cần code?
- **Muốn tích hợp dữ liệu** vào cơ sở dữ liệu để phân tích sau?

Workflow này **giải quyết tất cả** bằng cách:
✅ **Lấy video mới** từ kênh YouTube theo lịch trình (tùy chỉnh)
✅ **Tránh trùng lặp** bằng cơ chế kiểm tra URL trong Supabase
✅ **Chuyển tiếng tự động** với API miễn phí (25 video/tháng)
✅ **Lưu dữ liệu** vào Supabase để quản lý và phân tích
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần** so với cách làm thủ công.
- **Chính xác 100%** với cơ chế tránh trùng lặp tự động.
- **Dữ liệu sạch** với transcript được xử lý và lưu vào Supabase.
- **Hoạt động liên tục** theo lịch trình tự động (ví dụ: hàng ngày, hàng tuần).
- **Miễn phí** cho 25 video/tháng (dùng API Transcript.io).
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Supabase** (để lưu dữ liệu và tránh trùng lặp):
   - Tạo **database** và **table** `content_queue_1` (cần cấu hình trong workflow).
   - Lấy **Supabase API Key** (tìm trong `Project Settings > API`).
2. **API Key của Transcript.io** (miễn phí 25 video/tháng):
   - Đăng ký tại [youtube-transcript.io](https://www.youtube-transcript.io/) và lấy **API Key**.
3. **Danh sách Channel ID YouTube** (tìm bằng [TunePocket](https://www.tunepocket.com/youtube-channel-id-finder)).
4. **n8n Self-hosted** (để workflow chạy 24/7):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/9749) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import Workflow** → Dán JSON và nhấn **Import**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **4 bước chính**, các sếp cần cấu hình kỹ lưỡng:

#### **📌 Bước 1: Cấu hình Supabase**
- **Node `Check if URL Is In Database`**:
  - Điền **Supabase API Key** vào `credentials.supabaseApi`.
  - Chọn **Database URL** và **Project Name** (tìm trong `Supabase Dashboard`).
  - **Table Name**: Đặt là `content_queue_1` (phải tạo trước trong Supabase).
- **Node `Add to Content Queue Table`**:
  - Cấu hình giống như trên, đảm bảo **table** và **credentials** khớp.

#### **📌 Bước 2: Thêm Channel ID và API Key**
- **Node `Channels To Track`**:
  - Điền danh sách **Channel ID** của các kênh YouTube muốn theo dõi (tìm bằng [TunePocket](https://www.tunepocket.com/youtube-channel-id-finder)).
  - Ví dụ: `UCx9oQl6ykyNWZiDdDy4xgQg` (kênh n8n.io).
- **Node `Get Transcript from API`**:
  - Chọn **HTTP Query Auth** và **HTTP Header Auth**.
  - Điền **API Key** từ Transcript.io vào `httpQueryAuth` và `httpHeaderAuth`.

#### **📌 Bước 3: Thiết lập lịch trình và giới hạn tuổi video**
- **Node `Max Content Age Days`**:
  - Đặt số ngày muốn lấy video mới (ví dụ: `7` để lấy video trong 7 ngày gần nhất).
- **Node `Schedule Trigger`**:
  - Chọn **lịch trình** (ví dụ: `0 0 * * *` để chạy hàng ngày lúc 00:00).

#### **📌 Bước 4: Lọc bỏ YouTube Shorts (tùy chọn)**
- **Node `Filter Out YouTube Shorts`**:
  - **Mặc định**: Không lấy Shorts.
  - **Nếu muốn lấy Shorts**: Xóa điều kiện thứ 2 trong node này.

#### **📌 Các node quan trọng khác**
- **Node `Find Channel's Videos`**:
  - Sử dụng **RSS Feed** để lấy video từ YouTube (n8n tự động tạo URL RSS từ Channel ID).
- **Node `Get Transcript from API`**:
  - Đảm bảo **URL video** được truyền đúng vào `url` của request.
- **Node `Transcript Failed`**:
  - Nếu API thất bại, workflow sẽ **dừng và báo lỗi** (có thể sửa thành `continue` nếu muốn).

---

### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Nhấn **Run Workflow** và kiểm tra **log** để đảm bảo mọi thứ hoạt động.
- **Bật Active**:
  - Sau khi kiểm tra thành công, nhấn **Active** để workflow chạy tự động theo lịch trình.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi báo cáo định kỳ**:
   - Sử dụng **node Slack/Email** để gửi báo cáo video mới được chuyển tiếng hàng ngày.
   - Ví dụ: `"Hôm nay có 5 video mới được chuyển tiếng: [Danh sách]"`.
2. **Lưu log chi tiết**:
   - Thêm **node Log** để ghi lại trạng thái của mỗi video (thành công/thất bại).
3. **Tích hợp với Google Sheets**:
   - Sử dụng **node Google Sheets** để lưu transcript vào bảng tính thay vì Supabase.
4. **Lọc video theo từ khóa**:
   - Thêm **node Code** sau `Get Transcript from API` để lọc video chứa từ khóa nhất định.
5. **Tự động chia sẻ trên Telegram**:
   - Sử dụng **node Telegram Bot** để gửi thông báo video mới cho nhóm.
:::

---

## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công chuyển tiếng YouTube, đồng thời **tránh trùng lặp dữ liệu** và **tích hợp tự động** vào cơ sở dữ liệu. **Chỉ cần 10 phút cấu hình**, workflow sẽ hoạt động 24/7 theo lịch trình!

👉 **Bắt đầu ngay**:
1. Cài đặt **n8n Self-hosted** trên VPS.
2. Import workflow và cấu hình theo hướng dẫn.
3. **Bật Active** và để nó làm việc!

**Cần hỗ trợ?** Đăng ký **Skool Community** của tác giả [@automedia](https://n8n.io/workflows/9749) để học thêm kỹ thuật nâng cao! 🚀