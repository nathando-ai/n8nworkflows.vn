---
title: "🚀 Tự Động Hóa Đăng Video Trên 9 Mạng Xã Hội Từ Google Sheets Với Blotato – Giảm 90% Thời Gian Chỉnh Sửa"
description: "Workflow này giúp các sếp tự động hóa việc đăng video lên 9 nền tảng xã hội (Instagram, TikTok, Facebook, LinkedIn, Pinterest, Threads, X/Twitter, YouTube, Bluesky) từ Google Sheets, tiết kiệm thời gian và đảm bảo nội dung được phân phối đồng bộ. Sau khi đăng, hệ thống tự động cập nhật trạng thái và ghi log lỗi để quản lý dễ dàng."
slug: "tu-dong-hoa-dang-video-tren-9-mang-xa-hoi-tu-google-sheets"
tags: [n8n, automation, social-media, google-sheets, blotato, no-code]
keywords: [tự động hóa đăng video, n8n workflow, đăng video lên nhiều mạng xã hội, google sheets tự động, blotato api, tự động hóa marketing digital]
---

# 🚀 **Tự Động Hóa Đăng Video Trên 9 Mạng Xã Hội Từ Google Sheets – Không Cần Code**

Hiện nay, các sếp và marketer phải mất **giờ đồng hồ** để đăng video lên từng nền tảng xã hội một cách thủ công. Điều này không chỉ tốn thời gian mà còn dễ gây **lỗi nhầm lẫn** (quên đăng, nội dung không đồng bộ, hoặc cập nhật sai trạng thái). Workflow này sẽ **giải quyết tất cả những vấn đề đó** bằng cách tự động hóa toàn bộ quy trình từ **Google Sheets** đến **9 nền tảng xã hội** (Instagram, TikTok, Facebook, LinkedIn, Pinterest, Threads, X/Twitter, YouTube, Bluesky) chỉ trong **vài giây**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Đăng video lên 9 nền tảng chỉ trong **vài giây** thay vì mất **giờ đồng hồ**.
- **Đồng bộ nội dung**: Video và caption được đăng **ngay lập tức** trên tất cả nền tảng.
- **Quản lý dễ dàng**: Trạng thái đăng thành công hoặc lỗi được **tự động cập nhật** trên Google Sheets.
- **Hoạt động liên tục**: Workflow chạy theo **lịch trình tự động** (daily/hourly) mà không cần can thiệp.
- **Không lo quên đăng**: Hệ thống **ghi log lỗi** để các sếp biết những video nào chưa thành công.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để lưu trữ danh sách video và trạng thái).
2. **API Keys hoặc OAuth** cho các nền tảng xã hội (Instagram, TikTok, Facebook, LinkedIn, Pinterest, Threads, X/Twitter, YouTube, Bluesky).
   - **Lưu ý**: Các nền tảng như Instagram và TikTok yêu cầu **API Business** hoặc **OAuth 2.0**.
3. **Danh sách video** trong Google Sheets với các cột:
   - `Video URL` (đường dẫn video)
   - `Caption` (mô tả video)
   - `Status` (đặt mặc định là `pending` để workflow biết cần đăng)
   - `Platforms` (danh sách nền tảng muốn đăng, ví dụ: `Instagram,TikTok,Facebook`)

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải workflow từ [đây](https://n8n.io/workflows/12836) (hoặc sử dụng file JSON đã cung cấp).
2. Mở **n8n Editor** → Nhấn **Import Workflow** → Chọn file JSON.
3. Hoặc copy toàn bộ JSON và dán vào **Import Workflow** → **Paste JSON**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này có **13 node**, nhưng các sếp chỉ cần chú ý đến các phần sau:

##### **A. Cấu hình Google Sheets**
- **Node: "Read Pending Posts (Google Sheets)"**
  - Chọn **Spreadsheet ID** và **Sheet Name** trong Google Sheets.
  - **Query**: `SELECT * WHERE Status = 'pending'` (chỉ lấy video có trạng thái `pending`).
  - **Output Format**: Chọn `JSON` để n8n dễ xử lý.

- **Node: "Update Sheet – Mark as Published"**
  - Chọn cùng **Spreadsheet ID** và **Sheet Name**.
  - **Operation**: `update` (cập nhật trạng thái thành `published` khi đăng thành công).

- **Node: "Update Sheet – Log Error"**
  - Chọn cùng **Spreadsheet ID** và **Sheet Name**.
  - **Operation**: `update` (ghi lỗi vào cột `Error` nếu đăng thất bại).

##### **B. Cấu hình Blotato (API cho 9 nền tảng xã hội)**
Các sếp cần **cài đặt node Blotato** trước (nếu chưa có):
1. Mở **n8n Editor** → **Add Node** → Tìm `@blotato/n8n-nodes-blotato` → Cài đặt.
2. **Tạo credentials** cho mỗi nền tảng:
   - Mở **Credentials** trong n8n → **Add Credential** → Chọn `@blotato/n8n-nodes-blotato`.
   - Điền **API Key** hoặc **OAuth Token** của từng nền tảng (cách lấy token xem [đây](https://blotato.com/docs/)).
   - **Lưu ý**:
     - **Instagram**: Cần **API Business** và **Page Access Token**.
     - **TikTok**: Cần **Developer API Key**.
     - **Facebook**: Cần **Page Access Token**.
     - **LinkedIn**: Cần **OAuth 2.0 Token**.
     - **Pinterest**: Cần **API Key**.
     - **Threads**: Cần **API Key**.
     - **X/Twitter**: Cần **API Key**.
     - **YouTube**: Cần **OAuth 2.0 Token**.
     - **Bluesky**: Cần **API Key**.

##### **C. Cấu hình Lịch trình (Schedule Trigger)**
- Mở **node "Schedule Content Publishing"** → Chọn **Time Zone** và **Frequency** (ví dụ: **daily at 9 AM**).
- **Lưu ý**: Nếu muốn chạy **ngay lập tức**, chọn **Manual Trigger** (nhấn nút **Run Workflow**).

##### **D. Kích hoạt Workflow**
1. **Test Run** với 1 video mẫu:
   - Chọn **Run Workflow** → Chọn **Test Execution**.
   - Kiểm tra **Google Sheets** để xem trạng thái được cập nhật như thế nào.
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tối ưu hóa Google Sheets**:
   - Thêm cột `Error` để ghi lỗi chi tiết (ví dụ: `Lỗi: TikTok API rejected`).
   - Sử dụng **color coding** trong Google Sheets để phân biệt trạng thái (`pending`, `published`, `error`).

2. **Kết hợp với Slack/Telegram**:
   - Thêm **node Slack/Telegram** để **báo cáo thành công/lỗi** ngay khi workflow chạy.
   - Ví dụ: Khi đăng thành công, gửi tin nhắn: *"Video [Tên Video] đã đăng thành công trên 3 nền tảng!"*.

3. **Lưu log chi tiết**:
   - Thêm **node Log** (n8n-nodes-base.log) để ghi **tất cả hoạt động** vào file JSON.
   - Có thể kết nối với **Google Drive** để lưu log dài hạn.

4. **Chỉ đăng trên một số nền tảng**:
   - Nếu không muốn đăng trên tất cả 9 nền tảng, **tắt node** của nền tảng không cần thiết (ví dụ: chỉ đăng trên Instagram và TikTok).

5. **Sử dụng AI tự động tạo caption**:
   - Thêm **node LLM** (n8n-nodes-base.llm) để tự động **tạo caption** từ video (nếu chưa có).
   - Ví dụ: Gửi **URL video** vào LLM và yêu cầu: *"Tạo caption hấp dẫn cho video này, tối đa 200 ký tự"*.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp từ việc đăng video thủ công, đồng thời **đảm bảo nội dung được phân phối đồng bộ** trên tất cả nền tảng xã hội. **Không cần code**, chỉ cần **cấu hình đơn giản** là có thể tự động hóa toàn bộ quy trình.

**Hành động ngay hôm nay**:
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Import workflow** và **cấu hình Google Sheets + API Keys**.
3. **Bật Active** và **nhận kết quả ngay lập tức**!

👉 **Bắt đầu tự động hóa ngay [tại đây](https://n8n.io/workflows/12836)**! 🚀