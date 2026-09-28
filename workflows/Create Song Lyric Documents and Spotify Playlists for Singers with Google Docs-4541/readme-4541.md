---
title: "🎤 Tự Động Hoàn Thành Tài Liệu Lyric & Playlist Spotify Cho Ca Sĩ - Không Cần Code!"
description: "Workflow tự động hóa lấy lyrics từ Spotify, tạo tài liệu Google Docs chi tiết và playlist Spotify cho các buổi biểu diễn, tiết kiệm thời gian lên tới 80% cho các ca sĩ và nhóm nhạc."
slug: "tieu-dong-hoan-thanh-ta-lieu-lyric-va-playlist-spotify"
tags: [n8n, automation, no-code, spotify, google-docs, ai-chatbot, google-sheets]
keywords: [n8n workflow spotify, tự động hóa lyric, playlist spotify tự động, google docs tự động, ai chatbot n8n]
---

# 🎤 **Tự Động Hoàn Thành Tài Liệu Lyric & Playlist Spotify Cho Ca Sĩ**

### **Giải Pháp Tiết Kiệm Thời Gian Cho Các Buổi Biểu Diễn**
Các sếp ca sĩ hay nhóm nhạc đã từng phải mất **giờ đồng hồ** để:
- Tìm kiếm lyrics từng bài hát trên Spotify.
- Chép tay hoặc sao chép lyrics vào tài liệu Google Docs.
- Tạo playlist Spotify cho buổi biểu diễn.
- Đảm bảo tên nghệ sĩ và tên bài hát chính xác.

**Workflow này tự động hóa toàn bộ quá trình chỉ với một cú nhấp chuột!** Từ việc lấy dữ liệu từ Google Sheets, sử dụng AI để xác minh thông tin, lấy lyrics, tạo tài liệu chi tiết và playlist Spotify, tất cả đều được hoàn thành **một cách chính xác và tự động**.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tìm kiếm lyrics từng bài, tiết kiệm **giờ đồng hồ** cho mỗi buổi biểu diễn.
- **Chính xác 100%**: AI xác minh tên nghệ sĩ và tên bài hát, tránh sai sót.
- **Tài liệu sẵn sàng**: Tất cả lyrics được lưu trong Google Docs với định dạng chuyên nghiệp.
- **Playlist Spotify tự động**: Tất cả bài hát được thêm vào playlist chỉ với một cú nhấp chuột.
- **Hoạt động liên tục**: Workflow chạy 24/7, không phụ thuộc vào thời gian làm việc của các sếp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google**:
   - **Google Sheets**: File `Setlist_Manager` với cột `Artist` và `SongTitle`.
   - **Google Docs**: Để lưu trữ lyrics.
   - **OAuth 2.0 Credentials** cho Google Sheets và Google Docs (cài đặt trong [Google Cloud Console](https://console.cloud.google.com/)).
2. **Tài khoản Spotify**:
   - **Spotify Developer Account** (đăng ký tại [Spotify for Developers](https://developer.spotify.com/)).
   - **OAuth 2.0 Credentials** cho Spotify.
3. **Tài khoản OpenAI**:
   - **API Key** của OpenAI (đăng ký tại [OpenAI](https://platform.openai.com/)).
4. **n8n Workflow**:
   - Workflow này yêu cầu **n8n Community Edition** hoặc **n8n Enterprise**.
   - Các sếp có thể **self-host** trên VPS hoặc sử dụng **n8n Cloud** (miễn phí cho 1000 execution/tháng).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n Editor](https://n8n.io/editor/) và chọn **Import Workflow**.
2. Chọn file JSON từ [link gốc](https://n8n.io/workflows/4541) hoặc copy toàn bộ JSON từ đây và dán vào ô **Paste JSON**.
3. Nhấn **Import** để hoàn tất.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp cần cấu hình các node quan trọng như sau:

##### **A. Cấu Hình Credentials**
1. **Google Sheets & Google Docs**:
   - Đi đến **Credentials** trong n8n và thêm:
     - **googleSheetsOAuth2Api** (cấu hình OAuth 2.0 từ Google Cloud Console).
     - **googleDocsOAuth2Api** (cùng cách như trên).
2. **Spotify**:
   - Thêm **spotifyOAuth2Api** và cấu hình OAuth 2.0 từ Spotify Developer Dashboard.
3. **OpenAI**:
   - Thêm **openAiApi** và điền **API Key** từ tài khoản OpenAI.

##### **B. Cấu Hình Node "Get Data" (Google Sheets)**
- **Sheet Name**: Đặt là `Setlist_Manager`.
- **Range**: Chọn toàn bộ dữ liệu (ví dụ: `Sheet1!A:B`).
- **Credentials**: Chọn `googleSheetsOAuth2Api`.

##### **C. Cấu Hình Node "OpenAI Chat Model"**
- **Model**: Chọn `gpt-4o-mini` (hoặc model khác nếu muốn).
- **Prompt**: Workflow sẽ tự động sử dụng prompt mặc định để xác minh tên nghệ sĩ và bài hát.
- **Credentials**: Chọn `openAiApi`.

##### **D. Cấu Hình Node "Get Lyrics" (HTTP Request)**
- **URL**: Sử dụng API của Genius (hoặc API khác lấy lyrics) hoặc API của Spotify.
- **Headers**: Thêm `Authorization: Bearer <Spotify API Key>` (nếu sử dụng Spotify API).
- **Method**: POST hoặc GET tùy thuộc vào API.

##### **E. Cấu Hình Node "Populate Doc" (Google Docs)**
- **File ID**: Lấy từ URL của Google Doc mới tạo (ví dụ: `https://docs.google.com/document/d/[FILE_ID]/edit`).
- **Credentials**: Chọn `googleDocsOAuth2Api`.

##### **F. Cấu Hình Node "Search for Song" & "Add Song to Playlist" (Spotify)**
- **Playlist ID**: Đặt tên playlist là `Setlist - [ngày hôm nay]` (ví dụ: `Setlist - 2024-05-20`).
- **Credentials**: Chọn `spotifyOAuth2Api`.

##### **G. Cấu Hình Node "Create Playlist" (Spotify)**
- **Playlist Name**: Tự động lấy từ ngày hôm nay.
- **Description**: Có thể thêm mô tả như `Playlist cho buổi biểu diễn ngày [ngày]`.
- **Credentials**: Chọn `spotifyOAuth2Api`.

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Execute Workflow** và chọn **Test Execution**.
   - Điền dữ liệu mẫu vào Google Sheets (ví dụ: `Artist: Taylor Swift`, `SongTitle: Blank Space`).
   - Kiểm tra kết quả:
     - Lyrics được thêm vào Google Docs.
     - Bài hát được thêm vào playlist Spotify.
2. **Bật Active**:
   - Sau khi test thành công, chuyển trạng thái workflow từ **Inactive** sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự Động Tạo Playlist Hàng Ngày**:
   - Sử dụng **n8n Scheduler** để chạy workflow hàng ngày (ví dụ: lúc 8h sáng) để cập nhật playlist cho buổi biểu diễn sắp tới.

2. **Gửi Báo Cáo Định Kỳ**:
   - Kết hợp với **Slack** hoặc **Email** để thông báo khi workflow hoàn thành (ví dụ: `🎵 Playlist và tài liệu lyrics đã sẵn sàng!`).

3. **Lưu Log Hoạt Động**:
   - Sử dụng **Sticky Note** hoặc **Google Sheets** để lưu lịch sử hoạt động của workflow (ví dụ: ngày tạo, số bài hát, tên nghệ sĩ).

4. **Cải Thiện Prompt AI**:
   - Nếu AI không xác minh chính xác tên nghệ sĩ hoặc bài hát, các sếp có thể chỉnh sửa **prompt** trong node `OpenAI Chat Model` để rõ ràng hơn:
     ```plaintext
     "Xác minh tên nghệ sĩ và bài hát dựa trên dữ liệu từ Google Sheets. Nếu có sai sót, hãy trả về thông báo lỗi."
     ```

5. **Kết Hợp Với YouTube**:
   - Sử dụng **YouTube API** để tìm video ca nhạc và thêm vào tài liệu Google Docs.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các ca sĩ và nhóm nhạc muốn **tiết kiệm thời gian, tránh sai sót và chuẩn bị sẵn sàng cho buổi biểu diễn**. Với chỉ **một lần cấu hình**, các sếp sẽ không bao giờ phải lo lắng về việc tìm kiếm lyrics hoặc tạo playlist lại.

**Hãy áp dụng ngay và tập trung vào nghệ thuật!** 🎶

---
**🔗 [Tải Workflow Nguyên Bản](https://n8n.io/workflows/4541)**
**📌 [Cài Đặt n8n Self-Hosted](https://docs.n8n.io/)**
**🎁 [Mã Giảm Giá VPS](https://tino.vn/vps-n8n?affid=388)**