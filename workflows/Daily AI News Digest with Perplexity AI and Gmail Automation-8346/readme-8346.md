---
title: "🚀 Tự Động Hóa Báo Cáo Tin AI Hàng Ngày Với Perplexity AI & Gmail (Không Cần Code)"
description: "Workflow tự động hóa gửi báo cáo tin tức AI mới nhất hàng ngày qua email, tổng hợp từ Perplexity AI với định dạng chuyên nghiệp, tiết kiệm thời gian cho các sếp và chuyên gia tech. Đảm bảo nhận được tin tức cập nhật 24/7 mà không cần can thiệp thủ công."
slug: "tieu-dong-hoa-bao-cao-tin-ai-hang-ngay-perplexity-gmail"
tags: [n8n, automation, ai-summarization, gmail-automation, perplexity-ai, no-code-workflow]
keywords: [n8n workflow tự động hóa tin tức AI, gửi báo cáo email hàng ngày với Perplexity, tự động hóa tin tức tech, n8n + Gmail + AI, tổng hợp tin tức AI tự động]
---

# 🚀 **Tự Động Hóa Báo Cáo Tin AI Hàng Ngày Với Perplexity AI & Gmail**

### **Nỗi Đau Của Các Sếp & Chuyên Gia Tech**
Trong thế giới phát triển nhanh chóng của AI, các sếp và chuyên gia tech thường phải **tốn thời gian quét qua hàng trăm bài báo, blog và nguồn tin** để cập nhật những tin tức mới nhất. Điều này không chỉ **tốn công sức** mà còn **không đảm bảo tính toàn diện** của thông tin. Hơn nữa, việc **gửi báo cáo tổng hợp** cho đồng nghiệp hay khách hàng cũng là một công việc tẻ nhạt, dễ bị bỏ quên.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động tổng hợp tin tức AI mới nhất** từ Perplexity AI trong vòng 24 giờ.
✅ **Định dạng chuyên nghiệp** với HTML, giống như một email newsletter thực sự.
✅ **Gửi tự động hàng ngày** vào email của các sếp, không cần can thiệp thủ công.
✅ **Tiết kiệm thời gian** lên đến **5-10 giờ/tuần** cho các sếp và đội ngũ tech.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần quét tin tức thủ công hàng ngày.
- **Tin tức toàn diện**: Lấy từ các nguồn uy tín được Perplexity AI lọc sàng.
- **Định dạng chuyên nghiệp**: Email với HTML đẹp mắt, dễ đọc.
- **Hoạt động tự động**: Gửi hàng ngày vào giờ cố định (10:00 AM).
- **Tính cá nhân hóa**: Có thể thay đổi email nhận và nội dung tùy ý.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (để kết nối với Gmail API):
   - **OAuth 2.0 Credentials** (cài đặt trong [Google Cloud Console](https://console.cloud.google.com/)).
   - Email nhận tin tức (ví dụ: `xyz@gmail.com`).
2. **API Key Perplexity AI**:
   - Đăng ký tại [Perplexity API](https://www.perplexity.ai/api) và lấy `perplexityApi` credentials.
3. **n8n Self-hosted** (để chạy workflow 24/7).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/8346](https://n8n.io/workflows/8346) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ trang trên và dán vào **Create Workflow** → **Import JSON** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **4 node chính**, các sếp cần cấu hình kỹ lưỡng như sau:

##### **🔹 Node 1: Schedule Trigger (Khởi Động Lịch Hẹn)**
- **Cấu hình**:
  - **Schedule**: Chọn **"Daily"** và đặt thời gian là **10:00 AM** (hoặc thời gian phù hợp).
  - **Time Zone**: Chọn múi giờ của mình (ví dụ: `Asia/Ho_Chi_Minh`).
- **Lưu ý**:
  - Nếu workflow chưa chạy, **bật Active** và **test run** để kiểm tra.

##### **🔹 Node 2: Message a Model (Gửi Yêu Cầu Cho Perplexity AI)**
- **Cấu hình**:
  - **Credentials**: Chọn `perplexityApi` (đã tạo trước).
  - **Model**: Đặt là `sonar-pro` (mô hình AI mạnh mẽ của Perplexity).
  - **Prompt (System Instructions)**:
    ```
    Retrieve the latest AI and tech news from trusted sources over the last 24 hours.
    Output must be in HTML format with inline CSS, styled like an email newsletter.
    Include headline, summary, and full URL for each item.
    ```
  - **Input Data**: Nếu muốn thêm điều kiện đặc biệt, có thể chỉnh sửa ở **Expression** (ví dụ: `{{ $json.query }}`).
- **Lưu ý**:
  - Nếu Perplexity API trả về lỗi, kiểm tra **API Key** và **quota** (Perplexity có giới hạn free tier).

##### **🔹 Node 3: HTML Node (Chuyển Đổi Sang HTML)**
- **Cấu hình**:
  - **Input**: Chọn `{{ $json.message }}` (nội dung từ Perplexity AI).
  - **Output**: Workflow sẽ tự động chuyển đổi thành HTML sạch.
- **Lưu ý**:
  - Nếu HTML không hiển thị đúng, kiểm tra **cấu trúc JSON** từ Perplexity.

##### **🔹 Node 4: Send a Message (Gửi Email Với Gmail)**
- **Cấu hình**:
  - **Credentials**: Chọn `gmailOAuth2` (đã cấu hình trước).
  - **Recipients**: Nhập email nhận (ví dụ: `xyz@gmail.com`).
  - **Subject**: `Latest Tech and AI news update 🚀`.
  - **Message Body**: Chọn `{{ $json.html }}` (nội dung HTML từ node trước).
- **Lưu ý**:
  - Nếu email không gửi được, kiểm tra:
    - **OAuth 2.0 Credentials** có đúng không?
    - **Quota Gmail API** (nếu dùng free tier, có giới hạn 100 email/ngày).
    - **SPF/DKIM** (nếu email bị đánh dấu spam).

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Chọn **Run Workflow** và kiểm tra email nhận có nhận được không.
- **Bật Active**:
  - Sau khi test thành công, **bật Active** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Thêm Slack/Telegram Notification**:
   - Sử dụng **Slack Node** hoặc **Telegram Bot Node** để thông báo khi workflow chạy thành công.
2. **Lưu Log Lịch Sử**:
   - Thêm **Database Node** (ví dụ: Airtable, Google Sheets) để lưu lịch sử tin tức đã gửi.
3. **Tùy Chỉnh Nội Dung**:
   - Sử dụng **Expression** trong **Perplexity Node** để lọc tin tức theo chủ đề (ví dụ: AI, blockchain, robotics).
4. **Gửi Báo Cáo Định Kỳ**:
   - Thay đổi **Schedule Trigger** để gửi báo cáo **tối hôm trước** thay vì sáng.
5. **Kết Hợp Với Notion/Confluence**:
   - Sử dụng **Notion API** để tự động cập nhật tin tức vào trang wiki công ty.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp và chuyên gia tech muốn **tự động hóa việc cập nhật tin tức AI hàng ngày** mà không cần can thiệp thủ công. Với **Perplexity AI** làm nguồn tin uy tín và **Gmail Automation** để gửi email chuyên nghiệp, các sếp sẽ **tiết kiệm thời gian, tăng hiệu suất và luôn cập nhật tin tức mới nhất**.

**Hãy áp dụng ngay và bắt đầu tự động hóa công việc của mình!** 🚀

---
**🔗 [Tải workflow nguyên bản tại n8n.io](https://n8n.io/workflows/8346)**
**💬 Có thắc mắc? Hỏi ngay trong community n8n [đây](https://community.n8n.io/)**.