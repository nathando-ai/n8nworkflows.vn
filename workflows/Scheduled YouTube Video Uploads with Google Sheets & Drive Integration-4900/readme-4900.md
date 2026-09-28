---
title: "🎥 **Tự Động Hóa Tải Video lên YouTube Từ Google Sheets & Drive – Không Cần Code!**"
description: "Workflow tự động hóa hoàn toàn tự động hóa việc lên video YouTube từ Google Sheets, đồng thời quản lý tệp và cập nhật trạng thái tự động. Giúp các sếp tiết kiệm thời gian lên đến 10 giờ/tuần và tránh sai sót khi làm thủ công."
slug: "tu-dong-hoa-tai-video-len-youtube-tu-google-sheets"
tags: [n8n, automation, youtube, google-sheets, google-drive, no-code, it-ops]
keywords: [tự động hóa youtube, upload video tự động, google sheets youtube, n8n workflow youtube, tự động hóa nội dung video]
---

# 🚀 **Tự Động Hóa Tải Video lên YouTube Từ Google Sheets & Drive – Không Cần Code!**

### **Giải pháp cho các sếp bị "chìm" trong công việc lên video YouTube**
Làm thủ công việc lên video YouTube là một công việc **mệt mỏi, tốn thời gian và dễ sai sót**. Các sếp phải:
- **Tạo danh sách video** trên Google Sheets (hoặc Excel).
- **Tải video từ Google Drive** lên YouTube một cách thủ công.
- **Cập nhật trạng thái** (đã tải, lỗi, chờ duyệt) bằng tay.
- **Quản lý tệp video** trong Drive (di chuyển, sắp xếp).

Kết quả? **Thời gian bị "chìm" trong công việc này lên đến 10 giờ/tuần**, trong khi có thể sử dụng thời gian đó để **tạo nội dung chất lượng cao hơn** hoặc **quản lý kênh hiệu quả hơn**.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Lấy dữ liệu video từ Google Sheets** (tiêu đề, mô tả, thumbnail, link video).
✅ **Tải video từ Google Drive** lên YouTube **một cách tự động**.
✅ **Cập nhật trạng thái** trên Google Sheets khi video đã tải thành công.
✅ **Di chuyển video đã tải** vào folder riêng để quản lý dễ dàng.
✅ **Chạy định kỳ** (mỗi ngày hoặc theo lịch trình cá nhân hóa).

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 10 giờ/tuần** (giá trị ~10 triệu đồng/năm nếu tính theo mức lương trung bình).
- **Tránh sai sót** khi làm thủ công (ví dụ: quên cập nhật trạng thái, tải video sai file).
- **Quản lý video hiệu quả hơn** với hệ thống folder tự động và trạng thái cập nhật.
- **Tự động hóa hoàn toàn** – không cần can thiệp thủ công sau khi setup.
- **Cá nhân hóa** – có thể chạy theo lịch trình riêng (ví dụ: 9h, 12h, 15h hàng ngày).
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để sử dụng Google Sheets, Google Drive và YouTube).
2. **API Key của YouTube** (cần tạo trên [YouTube Data API Console](https://developers.google.com/youtube/v3/getting-started)).
3. **Tài khoản Google Drive** với quyền truy cập vào folder chứa video cần tải lên YouTube.
4. **Google Sheet** có cấu trúc như sau (các cột bắt buộc):
   - **Title** (Tiêu đề video)
   - **Description** (Mô tả)
   - **Thumbnail Link** (Link thumbnail từ Google Drive)
   - **Video Link** (Link video từ Google Drive)
   - **Status** (Trạng thái: "Chờ tải", "Đã tải", "Lỗi")
5. **Folder trong Google Drive** để lưu trữ video đã tải thành công (để quản lý dễ dàng).
:::

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Workflow này được cung cấp dưới dạng **JSON**, các sếp có thể import theo hai cách:
- **Cách 1: Import từ file JSON**
  1. Tải file JSON từ [đây](https://n8n.io/workflows/4900) (hoặc copy JSON từ link trên).
  2. Mở **n8n Editor** (trên máy chủ self-hosted hoặc n8n.cloud).
  3. Nhấp vào **Import** → Chọn file JSON → Nhấp **Import**.
- **Cách 2: Copy/Paste JSON**
  1. Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/4900).
  2. Trong **n8n Editor**, nhấp vào **Import** → Chọn **Paste JSON** → Dán và nhấp **Import**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **8 node chính**, các sếp cần **cấu hình kỹ lưỡng** các node sau:

##### **A. Node "M-F 9am,12pm,3pm" (ScheduleTrigger)**
- **Chọn ngày và giờ chạy**: Mặc định là **Thứ 2 đến Thứ 6, 9h, 12h, 15h**. Các sếp có thể điều chỉnh theo lịch trình riêng.
- **Lưu ý**: Nếu muốn chạy **ngày nào đó**, hãy chọn **Every day** và cấu hình ngày tháng cụ thể.

##### **B. Node "Google Sheets" (Get Data)**
- **Chọn Google Sheet**: Chọn **Google Sheet** chứa danh sách video.
- **Chọn Sheet Name**: Chọn **tab** (lớp) trong Google Sheet (ví dụ: "Video List").
- **Chọn Range**: Chọn **A1:Z1000** (hoặc điều chỉnh theo số lượng video).
- **Credentials**: Chọn **Google OAuth** đã cấu hình trước đó trong n8n.

##### **C. Node "Get Folder Name" (Google Drive)**
- **Chọn Folder**: Chọn **folder trong Google Drive** chứa video cần tải lên YouTube.
- **Lưu ý**: Folder này sẽ được sử dụng để lấy **ID của video** và **di chuyển video sau khi tải lên YouTube**.

##### **D. Node "Download Video Data" (Google Drive)**
- **Chọn File ID**: Sử dụng **ID của video** từ Google Sheet (cột "Video Link").
- **Lưu ý**: Node này sẽ **tải video từ Google Drive** để chuẩn bị upload lên YouTube.

##### **E. Node "Upload to YouTube" (YouTube)**
- **API Key**: Điền **API Key của YouTube** (tạo trước trên [YouTube Data API Console](https://developers.google.com/youtube/v3/getting-started)).
- **Credentials**: Chọn **YouTube OAuth** đã cấu hình.
- **Video Title**: Sử dụng **cột "Title"** từ Google Sheet.
- **Description**: Sử dụng **cột "Description"** từ Google Sheet.
- **Thumbnail Link**: Sử dụng **cột "Thumbnail Link"** từ Google Sheet.
- **Video File**: Chọn **file video** từ node "Download Video Data".

##### **F. Node "Update Status" (Google Sheets)**
- **Chọn Google Sheet**: Cùng sheet như trước.
- **Update Range**: Chọn **cột "Status"** để cập nhật trạng thái.
- **New Value**: Đặt thành **"Đã tải"** (hoặc tùy chỉnh theo ý muốn).

##### **G. Node "Move Video File to Folder" (Google Drive)**
- **Chọn Folder**: Chọn **folder mới** để lưu video đã tải thành công (ví dụ: "Uploaded Videos").
- **File ID**: Sử dụng **ID của video** từ node "Download Video Data".

---
#### **3. Kích hoạt ⚡️**
1. **Test Run** (kiểm tra trước khi chạy thực tế):
   - Nhấp vào **Run Workflow** và chọn **1 dòng dữ liệu** từ Google Sheet.
   - Kiểm tra:
     - Video có tải lên YouTube không?
     - Trạng thái trên Google Sheet có cập nhật không?
     - Video có di chuyển vào folder mới không?
2. **Bật Active**:
   - Sau khi test thành công, nhấp vào **Active** để workflow chạy tự động theo lịch trình.

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi thông báo Slack/Telegram khi video tải thành công**
   - Sử dụng **node Slack/Telegram** để gửi thông báo khi workflow hoàn thành.
   - Ví dụ: *"Video [Tiêu đề] đã tải lên YouTube thành công!"*

2. **Lưu log hoạt động**
   - Sử dụng **node StickyNote** để ghi lại lịch sử hoạt động (ví dụ: thời gian tải, trạng thái lỗi).

3. **Tự động tạo mô tả từ AI**
   - Kết hợp với **node LLM (AI)** để tự động tạo mô tả video từ tiêu đề hoặc nội dung video.

4. **Chỉ tải video mới**
   - Thêm **node Filter** để chỉ lấy video có trạng thái **"Chờ tải"** trong Google Sheet.

5. **Tự động chia sẻ video sau khi tải**
   - Sử dụng **node YouTube** để tự động chia sẻ video lên kênh chính hoặc kênh phụ.
:::

---
### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc **mệt mỏi, tẻ nhạt** là lên video YouTube thủ công. Với **tự động hóa hoàn toàn**, các sếp có thể:
✔ **Tiết kiệm thời gian** lên đến 10 giờ/tuần.
✔ **Tránh sai sót** khi làm thủ công.
✔ **Quản lý video hiệu quả** với hệ thống tự động.
✔ **Tập trung vào nội dung chất lượng** thay vì công việc lặp lại.

**Hãy setup ngay hôm nay!** Nếu có bất kỳ câu hỏi, các sếp có thể tham khảo [tài liệu chính thức của n8n](https://docs.n8n.io/) hoặc liên hệ cộng đồng n8n trên [Discord](https://n8n.io/community).

---
:::success[🚀 **Bắt đầu tự động hóa ngay!**]
1. **Cài đặt n8n Self-hosted** (để chạy 24/7) trên [VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (mã giảm giá: **VPSN8N**).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và để nó làm việc cho các sếp!
:::

---
**Chúc các sếp thành công với việc tự động hóa YouTube!** 🎬💻