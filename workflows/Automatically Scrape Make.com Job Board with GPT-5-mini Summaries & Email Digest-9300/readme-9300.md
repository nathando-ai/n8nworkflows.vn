---
title: "🚀 Tự Động Hàng Tuần: Scrape CV Make.com + Tóm Tắt AI GPT-5-mini + Email Digest Cho Các Sếp"
description: "Workflow tự động hóa 100% không code để scrape danh sách việc làm chuyên nghiệp từ Make.com, tóm tắt nội dung bằng GPT-5-mini, và gửi email tổng hợp hàng tuần cho các sếp. Tiết kiệm 10+ giờ/tháng so với cách làm thủ công."
slug: "tieu-dong-scrape-makecom-gpt5-email-digest"
tags: [n8n, automation, no-code, ai, email-marketing, job-scraping]
keywords: [tự động hóa scrape Make.com, GPT-5-mini n8n, email digest việc làm, tự động hóa việc làm chuyên nghiệp, n8n workflow AI]
---

# 🚀 **Tự Động Hàng Tuần: Scrape CV Make.com + Tóm Tắt AI GPT-5-mini + Email Digest Cho Các Sếp**

### **🔍 Nỗi Đau Của Các Sếp Hiện Nay**
Các sếp và nhà tuyển dụng thường phải **tốn thời gian hàng giờ** mỗi tuần để:
- Quét thủ công danh sách việc làm chuyên nghiệp trên Make.com.
- Đọc từng bài đăng chi tiết để lọc ra những cơ hội phù hợp.
- Ghi chép hoặc lưu trữ thông tin để theo dõi sau.

**Workflow này giải quyết tất cả bằng cách:**
✅ **Scrape tự động** tất cả bài đăng việc làm mới từ Make.com.
✅ **Tóm tắt bằng AI** (GPT-5-mini) để rút gọn nội dung thành 3-5 dòng chính.
✅ **Gửi email tổng hợp hàng tuần** (chỉ vào sáng thứ Hai) với danh sách việc làm mới nhất trong 7 ngày qua.
✅ **Tiết kiệm 10+ giờ/tháng** so với cách làm thủ công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Không cần quét thủ công hàng tuần.
- **Tính chính xác cao**: AI tóm tắt chính xác nội dung bài đăng.
- **Cá nhân hóa**: Email được gửi trực tiếp vào hộp thư cá nhân.
- **Hoạt động liên tục**: Chạy tự động hàng tuần, không cần can thiệp.
- **Dễ dàng mở rộng**: Thêm filter cho ngành nghề, mức lương, hoặc vị trí mong muốn.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Make.com** (để scrape danh sách việc làm).
2. **API Key OpenRouter** (để sử dụng GPT-5-mini):
   - Đăng ký tại [OpenRouter](https://openrouter.ai/) và lấy API key.
3. **Thông tin SMTP** (để gửi email):
   - Thông tin server SMTP (ví dụ: Gmail, Outlook) và mật khẩu ứng dụng (App Password).
4. **Địa chỉ email** để nhận email tổng hợp hàng tuần.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/9300](https://n8n.io/workflows/9300) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **14 node**, nhưng các node **quan trọng nhất** cần cấu hình kỹ là:

##### **A. Cấu Hình API OpenRouter (GPT-5-mini)**
- **Node**: `OpenRouter Chat Model` (sử dụng `gpt-5-mini`).
- **Hướng dẫn**:
  1. Vào **Credentials** trong n8n.
  2. Thêm **OpenRouter API** với API Key từ OpenRouter.
  3. Đảm bảo **model** được đặt là `openai/gpt-5-mini`.

##### **B. Cấu Hình Email SMTP**
- **Node**: `Send Weekly Job Digest`.
- **Hướng dẫn**:
  1. Vào **Credentials** và thêm **SMTP** với thông tin:
     - **Host**: `smtp.gmail.com` (hoặc server SMTP của bạn).
     - **Port**: `587` (hoặc `465` nếu SSL).
     - **Username**: Email của bạn.
     - **Password**: **App Password** (không phải mật khẩu thường).
     - **From Email**: Email bạn muốn hiển thị là người gửi.
     - **To Email**: Email nhận email tổng hợp.
  2. **Lưu ý**:
     - Nếu dùng Gmail, **bật 2FA** và tạo **App Password** tại [My Account > Security](https://myaccount.google.com/security).
     - Nếu SMTP không hoạt động, thử **N8n SMTP** (n8n-nodes-base.emailSend) với **SendGrid** hoặc **Mailgun**.

##### **C. Cấu Hình Filter Thời Gian (7 Ngày)**
- **Node**: `Filter New/Valid Jobs`.
- **Hướng dẫn**:
  - Mặc định, workflow chỉ scrape bài đăng trong **7 ngày qua**.
  - Nếu muốn thay đổi thời gian, chỉnh **condition** trong node `Filter` thành:
    ```json
    {{ $json.date > new Date(Date.now() - 7 * 24 * 60 * 60 * 1000) }}
    ```

##### **D. Cấu Hình Schedule (Chạy Hàng Tuần)**
- **Node**: `Run Weekly on Monday Morning`.
- **Hướng dẫn**:
  - Mặc định, workflow chạy **tự động vào sáng thứ Hai**.
  - Nếu muốn thay đổi thời gian, chỉnh **cron expression** trong node `Schedule Trigger` thành:
    ```json
    0 8 * * 2  # Chạy lúc 8h sáng thứ Hai
    ```

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy node `Fetch Main Job Board` để kiểm tra scrape có hoạt động không.
   - Kiểm tra node `OpenRouter Chat Model` để đảm bảo AI tóm tắt đúng.
   - Gửi email test bằng node `Send Weekly Job Digest`.
2. **Bật Active workflow**:
   - Đảm bảo tất cả node hoạt động ổn định trước khi bật **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**CÁC Ý TƯỞNG MỞ RỘNG**]
1. **Lọc theo ngành nghề/ngôn ngữ**:
   - Thêm node `Filter` sau khi scrape để chỉ lấy việc làm trong ngành **AI, Web3, hoặc tiếng Việt**.
   - Ví dụ: `{{ $json.keywords.includes("AI") }}`.

2. **Gửi báo cáo định kỳ khác**:
   - Thay đổi `Schedule Trigger` để gửi email **hàng tháng** hoặc **hàng ngày**.

3. **Lưu log vào Google Sheets/Notion**:
   - Thêm node `Google Sheets` hoặc `Notion` sau `Aggregate All Jobs` để lưu dữ liệu chi tiết.

4. **Kết hợp với Slack/Telegram**:
   - Thay node `emailSend` bằng `Slack Webhook` hoặc `Telegram Bot` để thông báo tức thời.

5. **Tối ưu AI Response**:
   - Chỉnh sửa **prompt** trong node `Extract Job Details with AI` để AI trả về định dạng cụ thể (ví dụ: `Tóm tắt bài đăng trong 3 câu, không có từ "tóm tắt"`).
   - Ví dụ prompt:
     ```json
     "Tóm tắt bài đăng việc làm này trong 3 câu ngắn gọn, nhấn mạnh yêu cầu kỹ thuật và kỹ năng cần thiết. Không bao gồm thông tin về mức lương hoặc địa điểm."
     ```

6. **Dùng n8n Cloud miễn phí (nếu không muốn self-host)**:
   - Nếu không muốn cài VPS, có thể dùng [n8n Cloud](https://n8n.io/cloud) (miễn phí cho 1 workflow).
   - **Nhược điểm**: Không tự động hóa hàng tuần (phải chạy thủ công).
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào việc **lựa chọn ứng viên** thay vì **quét thông tin**. Với **AI tóm tắt GPT-5-mini** và **email tự động hàng tuần**, bạn sẽ **không bỏ lỡ bất kỳ cơ hội việc làm nào** mà không cần can thiệp.

**🚀 Hành động ngay:**
1. **Import workflow** và cấu hình SMTP + OpenRouter API.
2. **Test run** để đảm bảo scrape và AI hoạt động.
3. **Bật Active** và **quên đi việc làm thủ công**!

---
:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Cần hỗ trợ thêm?**
- **Đăng ký tư vấn miễn phí** với Julian Kaiser (tác giả workflow) tại [liên kết này](https://juliankaiser.com/contact).
- **Hỏi đáp cộng đồng n8n** tại [Discord n8n](https://discord.gg/n8n).