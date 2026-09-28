---
title: "🎵 **Tự Động Hóa Gợi Ý Nhạc Indie Đài Loan Cá Nhân Hóa Theo Mùa Trời, Cung Mệnh & AI** – Spotify + OpenAI"
description: "Workflow này tự động gợi ý bài nhạc indie Đài Loan phù hợp với tâm trạng, cung mệnh, thời tiết hiện tại và ngày sinh của bạn – chỉ cần kích hoạt 1 lần! Kết quả bao gồm link Spotify, lý do chọn bài và thông tin chi tiết về âm nhạc."
slug: "tieu-dong-hoa-gi-nhac-indie-tai-loan-canh-nhac-ai-spotify"
tags: [n8n, automation, no-code, ai, spotify, astrology, weather-api]
keywords: [n8n workflow, tự động hóa nhạc indie Đài Loan, AI gợi ý âm nhạc, Spotify API, cung mệnh và âm nhạc, thời tiết và tâm trạng]
---

# 🎵 **Tự Động Hóa Gợi Ý Nhạc Indie Đài Loan Cá Nhân Hóa Theo Mùa Trời, Cung Mệnh & AI**

## **🔥 Nỗi Đau Của Các Sếp (Và Giải Pháp Của n8n)**
Bạn có bao giờ mệt mỏi khi phải **tìm kiếm thủ công** bài nhạc indie Đài Loan phù hợp với tâm trạng, thời tiết lạnh giá hay nắng nóng của ngày hôm nay? Hay muốn **tận dụng thông tin cung mệnh** để chọn những ca khúc mang năng lượng phù hợp với ngày sinh? Thì với **workflow này**, các sếp sẽ:
✅ **Tiết kiệm 30 phút/tuần** tìm kiếm và lựa chọn nhạc.
✅ **Nhận gợi ý âm nhạc cá nhân hóa** dựa trên **thời tiết, cung mệnh và tâm trạng**.
✅ **Nghe nhạc từ Spotify** với link trực tiếp, không cần copy-paste.
✅ **Hiểu lý do** tại sao bài nhạc được chọn (ví dụ: "Bài này phù hợp với cung Song Tử vì âm hưởng mạnh mẽ").

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
- **Tự động hóa 100%**: Chỉ cần kích hoạt 1 lần, workflow sẽ tự lấy dữ liệu thời tiết, tính cung mệnh và gợi ý nhạc.
- **Cá nhân hóa cao**: Kết hợp **thời tiết hiện tại**, **cung mệnh**, **tâm trạng** và **ngày sinh** để chọn nhạc phù hợp.
- **Link Spotify sẵn sàng**: Không cần tìm kiếm thêm, workflow sẽ trả về **URL Spotify** của bài nhạc được gợi ý.
- **Giải thích lý do**: Biết tại sao bài nhạc đó phù hợp với bạn (ví dụ: "Bài này có nhịp điệu nhanh phù hợp với cung Thân Tử").
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI CHẠY**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Spotify** (để lấy API Key OAuth2):
   - Tạo **Spotify Developer Account** tại [developer.spotify.com](https://developer.spotify.com/) và đăng ký ứng dụng.
   - **Lưu ý**: Cần cấp quyền `user-read-recently-played`, `user-read-playback-state`, `user-modify-playback-state`.
2. **API Key OpenAI**:
   - Tạo tài khoản tại [openai.com](https://openai.com/) và lấy **API Key** từ Dashboard.
3. **Thông tin cá nhân** (điền vào node `infomation`):
   - **Thành phố** (ví dụ: Đài Bắc, Đài Trung).
   - **Ngày sinh** (để tính cung mệnh).
   - **Tâm trạng** (ví dụ: Happy, Sad, Relaxed).
   - **Ngôn ngữ đầu ra** (Tiếng Việt hoặc Tiếng Anh).
:::

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import:
- **Tải file JSON** từ [n8n.io/workflows/4210](https://n8n.io/workflows/4210) và import vào **n8n Editor**.
- **Copy JSON** từ trang trên và **dán vào n8n Editor** (Menu → Import → Paste JSON).

:::note[**Lưu ý quan trọng**]
- **Không xóa node `infomation`** (nó chứa thông tin đầu vào).
- **Không thay đổi tên node** (nếu muốn sử dụng template này).
:::

#### **2. Cấu Hình Cần Thay Đổi 📌**
Các sếp **phải chỉnh** các node sau để workflow hoạt động:

| **Node**               | **Cần Thay Đổi Gì?**                                                                 | **Hướng Dẫn**                                                                 |
|------------------------|------------------------------------------------------------------------------------|-------------------------------------------------------------------------------|
| **Manual Trigger**     | Không cần chỉnh, chỉ kích hoạt bằng nút **"Test workflow"**.                     | Bấm nút này để chạy workflow.                                                 |
| **OpenAI (get song recommendation)** | Chỉnh **API Key** ở `credentials` → `openAiApi`. | Dán API Key OpenAI vào đây.                                                   |
| **Spotify**            | Chỉnh **API Key OAuth2** ở `credentials` → `spotifyOAuth2Api`. | Sử dụng API Key từ Spotify Developer Account.                                |
| **infomation (set)**   | **Điền thông tin cá nhân** (city, birthday, mood, language).                     | Ví dụ: `{"city": "Taipei", "birthday": "1996/11/21", "mood": "Happy"}`       |
| **Final Output (set)** | Không cần chỉnh, chỉ dùng để hiển thị kết quả.                                   | Workflow tự động compile kết quả.                                            |

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Kích hoạt **Manual Trigger** và kiểm tra kết quả.
   - Kiểm tra **Final Output** để đảm bảo:
     - Thời tiết hiện tại của thành phố được lấy.
     - Cung mệnh và vận may hàng ngày được tính.
     - Spotify URL của bài nhạc được gợi ý.
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** để workflow chạy tự động.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**3 Ý Tưởng Thực Tiễn**]
1. **Kết Nối Với Slack/Telegram**:
   - Thêm **node Slack/Telegram Webhook** vào cuối workflow để nhận kết quả tự động qua chat.
2. **Lưu Log Lịch Sử**:
   - Sử dụng **node Database (Postgres/SQL)** để lưu lịch sử gợi ý nhạc của bạn.
3. **Tự Động Chạy Hàng Ngày**:
   - Sử dụng **node Cron** (n8n Enterprise) để chạy workflow vào mỗi sáng 7h.
:::

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp khỏi việc tìm kiếm nhạc thủ công, đồng thời **tăng trải nghiệm nghe nhạc** bằng cách kết hợp **AI, thời tiết và astrology**. **Chỉ cần 5 phút để setup**, sau đó **nghe nhạc phù hợp với tâm trạng** mỗi ngày!

👉 **Bắt đầu ngay** bằng cách import workflow và điền thông tin cá nhân. Nếu có vấn đề, **hãy để lại comment** dưới đây!

---
:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng** (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**#n8n #TựĐộngHóa #NhạcIndie #AI #Spotify #CungMệnh**