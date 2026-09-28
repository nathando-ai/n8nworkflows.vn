---
title: "🎬 Tự Động Tạo Thư Viện Clip Huấn Luyện Mới Nhập Công Ty Với WayinVideo, Google Drive & Gmail (Không Cần Code)"
description: "Giải pháp tự động hóa hoàn toàn cho HR tự động tách clip từ video onboarding, lưu trữ trên Google Drive và gửi email cá nhân hóa cho nhân viên mới - tiết kiệm 10+ giờ công mỗi tháng."
slug: "tay-dong-tao-thu-vien-clip-huan-luyen-moi-nhap"
tags: [n8n, automation, hr, wayinvide, google-drive, gmail, ai-summarization, no-code]
keywords: [tự động hóa hr, cách tách clip video, wayinvide api, lưu trữ clip google drive, email cá nhân hóa nhân viên mới, workflow n8n hr]
---

# 🚀 **Tự Động Tạo Thư Viện Clip Huấn Luyện Mới Nhập Công Ty Với WayinVideo, Google Drive & Gmail**

### **Giải pháp cho HR tự động hóa quá trình tách clip từ video onboarding**
Hiện nay, các đội HR phải mất **từ 5-10 giờ** mỗi tháng để:
- Chỉnh sửa video onboarding dài 1-2 giờ thành các clip ngắn (30-60 giây)
- Tải lên Google Drive và quản lý trong Google Sheets
- Gửi email cá nhân hóa cho từng nhân viên mới với link clip

**Workflow này tự động hóa toàn bộ quá trình chỉ trong 5 phút thiết lập!**
- **Tách tự động** clip từ video onboarding theo chủ đề (ví dụ: "culture and team values")
- **Tải lên Google Drive** với tên file cấu trúc (TênNV_Department_Clip1_Score95.mp4)
- **Gửi email cá nhân hóa** cho nhân viên mới với link clip và hướng dẫn
- **Lưu trữ toàn bộ metadata** trong Google Sheets để quản lý dễ dàng

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ công/tháng** cho đội HR (không cần chỉnh sửa video thủ công)
- **Cá nhân hóa hoàn toàn** mỗi clip theo nhân viên, bộ phận và chủ đề
- **Chất lượng cao** với clip HD 720p, phụ đề động và thời gian tải nhanh
- **Quản lý trung tâm** tất cả clip trong Google Sheets với 15 trường metadata
- **Hoạt động 24/7** không cần can thiệp của con người
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản WayinVideo** (đăng ký tại [wayinvide.com](https://wayinvide.com/))
   - API Key (được cung cấp sau khi đăng ký)
2. **Tài khoản Google** (để kết nối Google Drive & Google Sheets)
   - OAuth2 credentials cho Google Drive và Google Sheets
3. **Tài khoản Gmail** (để gửi email cá nhân hóa)
   - OAuth2 credentials cho Gmail
4. **Google Sheet** với tab tên **"Onboarding Clip Library"** và các cột sau:
   ```
   Employee Name | Employee Email | Department | Start Date | Company | Topic
   Clip Title | Description | Timestamp | Score | Tags | Drive Link
   Drive File ID | Onboarding Recording URL | Date Added
   ```
5. **Folder Google Drive** để lưu trữ clip (để lấy `YOUR_GDRIVE_FOLDER_ID`)
6. **Form Google** (hoặc link trực tiếp) để HR nhập thông tin nhân viên mới:
   - URL video onboarding
   - Tên nhân viên
   - Email nhân viên
   - Bộ phận
   - Ngày bắt đầu làm việc
   - Chủ đề huấn luyện (4-6 từ, ví dụ: "company culture and team values")
   - Tên công ty

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow theo **2 cách**:
- **Tải file JSON** từ [n8n.io/workflows/15567](https://n8n.io/workflows/15567) và import vào n8n Editor.
- **Copy/paste JSON** từ link trên vào n8n Editor (chọn **Import Workflow** → **Paste JSON**).

:::note[Lưu ý]
- **Không sử dụng phiên bản n8n Community** (n8n.io) để chạy workflow này 24/7. **Cài đặt n8n trên VPS** để đảm bảo hoạt động liên tục.
  👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
  👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Dưới đây là **các node quan trọng** cần cấu hình:

##### **🔹 Node 2 & 4: WayinVideo — Submit Find Moments & Get Clips Result**
- **Thay thế `YOUR_WAYINVIDEO_API_KEY`** bằng API Key từ tài khoản WayinVideo.
- **Cấu hình HTTP Request**:
  - Method: `POST` (Submit) và `GET` (Poll)
  - URL:
    - Submit: `https://api.wayinvide.com/v1/find-moments`
    - Poll: `https://api.wayinvide.com/v1/find-moments/{jobId}`
  - Headers:
    ```json
    {
      "Authorization": "Bearer YOUR_WAYINVIDEO_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - Body (Submit):
    ```json
    {
      "url": "{{ $json.url }}",
      "query": "{{ $json.topic }}",
      "limit": 5,
      "resolution": "720p",
      "captions": true,
      "export": true,
      "noReframe": true
    }
    ```

##### **🔹 Node 9: Google Drive — Upload Clip**
- **Kết nối OAuth2** của Google Drive.
- **Thay thế `YOUR_GDRIVE_FOLDER_ID`** bằng ID folder bạn muốn lưu clip.
- **Cấu hình filename**:
  ```
  {{ $json.employeeName }}_{{ $json.department }}_Clip_{{ $json.clipIndex }}_Score_{{ $json.score }}.mp4
  ```
  Ví dụ: `NguyenVanA_DepartmentX_Clip1_Score95.mp4`

##### **🔹 Node 10: Google Sheets — Save to Library**
- **Kết nối OAuth2** của Google Sheets.
- **Thay thế `YOUR_GOOGLE_SHEET_ID`** bằng ID sheet (tìm trong URL tab `Onboarding Clip Library`).
- **Cấu hình operation**: `append` (thêm dữ liệu mới vào cuối sheet).

##### **🔹 Node 11: Gmail — Send Welcome Email**
- **Kết nối OAuth2** của Gmail.
- **Cấu hình email HTML**:
  ```html
  <h2>Welcome to {{ $json.company }}!</h2>
  <p>Your onboarding recording is ready. Here are your training clips:</p>
  <p><a href="{{ $json.driveLink }}">View your clips in Google Drive</a></p>
  <p>Check the <a href="{{ $json.sheetLink }}">Onboarding Clip Library</a> for all training materials.</p>
  ```

##### **🔹 Node 7: Code — Split Each Clip**
- **Mã JavaScript** đã được cung cấp trong workflow. Các sếp **không cần chỉnh sửa** trừ khi muốn thêm logic mới.
- **Output** sẽ là mảng các clip với metadata như:
  ```json
  {
    "title": "Clip 1: Company Culture Introduction",
    "exportLink": "https://export.wayinvide.com/...",
    "score": 95,
    "tags": ["culture", "team"],
    "description": "CEO explains company values",
    "timestamps": [{"start": 120, "end": 180}]
  }
  ```

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhập URL video onboarding và chủ đề (ví dụ: "company culture and team values").
   - Kiểm tra các clip được tách ra có đúng không.
2. **Bật Active workflow**:
   - Chuyển trạng thái từ **Inactive** sang **Active** trong n8n Editor.
   - **Lưu workflow** và **đặt lên đồ** (Deploy).

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo khi clip được tạo thành công.
   - Ví dụ: `New clip created for {{ $json.employeeName }}! Score: {{ $json.score }}`

2. **Lưu log hoạt động**:
   - Thêm node **Sticky Note** (Node 6 trong workflow) để ghi lại thời gian và trạng thái của mỗi clip.
   - Cấu hình để lưu vào Google Sheets hoặc một file CSV.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n Trigger** (ví dụ: Trigger hàng tuần) để gửi email báo cáo tổng hợp số clip được tạo, bộ phận có nhiều clip nhất, và trung bình điểm số.

4. **Tối ưu chủ đề tìm kiếm**:
   - **Không dùng từ quá chung** như "culture" hoặc "HR". Thay vào đó, dùng cụ thể:
     - ✅ "company culture and team values explanation"
     - ✅ "HR policy and leave management overview"
     - ❌ "culture" (quá rộng)

5. **Tự động xóa clip cũ**:
   - Thêm logic trong **Code Node** để xóa clip từ Google Drive sau 30 ngày nếu không được truy cập.

---

### 📌 **Kết luận**
Workflow này **giải phóng HR khỏi công việc thủ công** và tự động hóa toàn bộ quy trình tách clip, lưu trữ và gửi email cá nhân hóa. **Chỉ cần 5 phút thiết lập**, các sếp sẽ tiết kiệm **10+ giờ công/tháng** và nâng cao trải nghiệm onboarding cho nhân viên mới.

**Bắt đầu ngay!**
1. Import workflow và cấu hình các API key.
2. Kết nối Google Drive, Sheets và Gmail.
3. **Bật Active** và bắt đầu tự động hóa!

---
**💡 Cần hỗ trợ thêm?**
- **Diễn đàn n8n**: [community.n8n.io](https://community.n8n.io/)
- **TinoHost (VPS n8n)**: [tino.vn/vps-n8n](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N**)