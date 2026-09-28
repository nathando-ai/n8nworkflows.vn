---
title: "🚀 Tự Động Hóa RSS Tech Sang Email Tóm Tắt AI - GPT-5 Mini + Gmail (Miễn Phí 24/7)"
description: "Workflow tự động hóa thu thập, tóm tắt và gửi email tổng hợp tin tức công nghệ hàng ngày từ 27 nguồn RSS hàng đầu, được lọc và tổng hợp bởi GPT-5 Mini. Tiết kiệm 3+ giờ/ngày cho các sếp theo dõi tin tức tech."
slug: "tieu-dong-hoa-rss-tech-sang-email-gpt-5-mini"
tags: [n8n, automation, no-code, ai-summarization, gmail-integration, rss-feed]
keywords: [n8n workflow rss, tự động hóa tin tức tech, gpt-5 mini email digest, tổng hợp tin tức hàng ngày, n8n self-hosted]
---

# 🚀 **Tự Động Hóa RSS Tech Sang Email Tóm Tắt AI: Từ 27 Nguồn Tin Tức → Email Hàng Ngày Với GPT-5 Mini**

### **Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải mất **30-60 phút** để:
- Theo dõi **Hacker News, TechCrunch, The Verge** và các nguồn tin công nghệ khác.
- Lọc ra những bài viết **quan trọng, mới nhất và đa dạng**.
- Tóm tắt nội dung dài để **đọc nhanh** trong email.
- **Quên bỏ** một số bài viết quan trọng vì quá nhiều thông tin.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Thu thập** từ 27 nguồn RSS hàng đầu (Tech, AI, Startup, Science, Blogger).
✅ **Lọc và tóm tắt** 30 bài viết **đa dạng và quan trọng nhất** bằng **GPT-5 Mini**.
✅ **Gửi email tổng hợp** hàng ngày vào **8h sáng** với **định dạng đẹp mắt** (HTML + gradient header).
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (Đảm bảo tốc độ nhanh cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 3+ giờ/ngày** so với việc theo dõi thủ công.
- **Nhận email tổng hợp** với **30 bài viết lọc kỹ** (không spam, không trùng lặp).
- **Tóm tắt AI** bằng GPT-5 Mini → **đọc nhanh** trong 5 phút thay vì 1 giờ.
- **Định dạng email đẹp mắt** (gradient header, card bài viết, số thứ tự).
- **Hoạt động tự động** từ **8h sáng** hàng ngày, **không cần nhớ**.
- **Không lo bị lỗi** vì có **error handling** cho RSS broken.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** (để sử dụng **GPT-5 Mini**):
   - [Đăng ký tài khoản OpenAI](https://platform.openai.com/signup) (miễn phí với giới hạn credit).
   - **API Key** (tìm ở [trang tài khoản OpenAI](https://platform.openai.com/account/api-keys)).
2. **Tài khoản Gmail** (để gửi email tổng hợp):
   - **OAuth 2.0 Credentials** (cấu hình trong n8n).
   - **Email nhận** (điền vào node **"Send Digest Email"**).
3. **n8n Self-hosted** (không dùng phiên bản cloud để tránh giới hạn).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/14952](https://n8n.io/workflows/14952) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/14952) và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **8 node**, các sếp cần chú ý cấu hình sau:

##### **🔹 Node 1: Daily Morning Trigger**
- **Thời gian kích hoạt:** Đặt lại thành **8h sáng** (hoặc thời gian phù hợp).
- **Lưu ý:** Nếu dùng phiên bản cloud, có thể bị giới hạn thời gian chạy. **Self-hosted là lựa chọn tốt nhất**.

##### **🔹 Node 2 & 3: Define RSS Sources + Fetch RSS Feeds**
- **Không cần chỉnh sửa** (đã cấu hình sẵn 27 nguồn RSS).
- **Error handling:** Nếu một nguồn RSS bị lỗi, workflow vẫn tiếp tục với các nguồn khác.

##### **🔹 Node 4: Clean and Prepare for AI (Code Node)**
- **Chức năng:**
  - Loại bỏ **trùng lặp** (bằng URL).
  - **Xóa HTML tags** khỏi description.
  - **Giới hạn 150 bài viết mới nhất**.
- **Không cần chỉnh sửa** (đã tối ưu sẵn).

##### **🔹 Node 5: AI Article Curator (Agent Node)**
- **Sử dụng GPT-5 Mini** để lọc **30 bài viết tốt nhất**.
- **Prompt mặc định:**
  > *"Tôi là một nhà báo công nghệ. Hãy lọc ra 30 bài viết **đa dạng và quan trọng nhất** từ danh sách dưới đây. Yêu cầu:
  > - Loại bỏ bài viết trùng lặp.
  > - Ưu tiên bài viết từ **TechCrunch, Hacker News, The Verge**.
  > - Tránh bài viết quá cũ (trước 1 tuần).
  > - Giữ bài viết có **tóm tắt ngắn gọn** và **đánh giá cao**."*

- **Lưu ý:**
  - Nếu **GPT-5 Mini không hoạt động**, có thể thay bằng **GPT-4** (tùy chọn trong `lmChatOpenAi` node).
  - **Không cần chỉnh sửa prompt** nếu muốn kết quả mặc định.

##### **🔹 Node 6: OpenAI GPT-5 Mini (lmChatOpenAi)**
- **Cấu hình:**
  - **Credentials:** Chọn **"openAiApi"** (đã cấu hình sẵn API Key).
  - **Model:** Đặt là **"gpt-5-mini"** (nếu có, nếu không thì **gpt-4**).
  - **Temperature:** Giữ mặc định (**0.7**).

##### **🔹 Node 7: Build Digest Email (Code Node)**
- **Chức năng:**
  - **Tạo email HTML đẹp** với:
    - **Header gradient màu tím**.
    - **Card bài viết** (tên, tóm tắt, ngày, nguồn).
    - **Số thứ tự** cho dễ đọc.
- **Không cần chỉnh sửa** (đã thiết kế sẵn).

##### **🔹 Node 8: Send Digest Email (Gmail Node)**
- **Cấu hình:**
  - **Credentials:** Chọn **"gmailOAuth2"** (cấu hình OAuth 2.0 trong n8n).
  - **Email To:** Điền **email của bạn** (đã là placeholder).
  - **Subject:** Giữ mặc định (**"📰 Tech Digest - [Ngày]"**).
  - **HTML Body:** Chọn **`json`** từ node trước.

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run:**
   - Chạy **manual test** để kiểm tra:
     - RSS được fetch đúng không?
     - AI lọc được 30 bài viết không?
     - Email được gửi đúng định dạng không?
2. **Bật Active:**
   - Đặt **switch Active** thành **ON**.
   - **Xem email vào 8h sáng** để kiểm tra kết quả.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Nguồn RSS Cụ Thể:**
   - Mở node **"Define RSS Sources"** (Code Node) và thêm URL mới vào mảng `rssSources`.
   - Ví dụ:
     ```javascript
     const rssSources = [
       { name: "Dev.to", url: "https://dev.to/feed" },
       // ... (các nguồn hiện có)
     ];
     ```

2. **Tùy Chỉnh Prompt AI:**
   - Mở node **"AI Article Curator"** và chỉnh sửa **prompt** để:
     - **Ưu tiên chủ đề** (ví dụ: AI, Cloud, Startup).
     - **Loại bỏ** những bài viết không phù hợp (quảng cáo, opinion).
   - Ví dụ:
     > *"Hãy loại bỏ tất cả bài viết về **quảng cáo, crypto, hoặc opinion**."*

3. **Lưu Log & Theo Dõi:**
   - Thêm **Sticky Note Node** để ghi lại:
     - Số lượng bài viết được fetch.
     - Số bài viết bị loại bỏ (trùng lặp, lỗi).
     - Thời gian chạy của workflow.

4. **Gửi Email Đến Nhóm:**
   - Thay vì gửi riêng, **copy email** từ node **"Send Digest Email"** và gửi đến **Slack/Telegram** bằng **n8n-nodes-base.slack** hoặc **n8n-nodes-base.telegram**.

5. **Tự Động Lưu Bài Viết Vào Google Sheets:**
   - Thêm **Google Sheets Node** sau node **"AI Article Curator"** để lưu:
     - Tiêu đề bài viết.
     - Link.
     - Tóm tắt AI.
   - **Cấu hình:**
     - **Sheet Name:** `"Tech Digest"`.
     - **Credentials:** `"googleSheetsOAuth2"`.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **các quyết định chiến lược** thay vì mất giờ theo dõi tin tức. Với **GPT-5 Mini**, email tổng hợp không chỉ **nhanh chóng** mà còn **đa dạng và chất lượng cao**.

**Hành động ngay:**
1. **Cài n8n Self-hosted** (nếu chưa có).
2. **Import workflow** và cấu hình **OpenAI + Gmail**.
3. **Bật Active** và **nhận email tổng hợp hàng ngày** từ 8h sáng!

---
**💡 Mẹo cuối:** Nếu muốn **cải thiện hiệu suất**, các sếp có thể:
- **Tăng RAM** cho VPS (4GB+).
- **Sử dụng cache** cho RSS (tránh fetch lại liên tục).
- **Thêm node Slack** để báo động khi workflow lỗi.

**Chúc các sếp thành công!** 🚀