---
title: "🎬 Tự Động Sáng Tạo & Đăng Video AI Hài Hước lên TikTok với Sora 2 - Không Cần Code!"
description: "Workflow tự động hóa 100% sử dụng n8n để tạo video AI hài hước bằng Sora 2, tự động tối ưu tiêu đề với GPT-5 và đăng trực tiếp lên TikTok. Giúp các sếp tiết kiệm thời gian, tăng engagement và tự động hóa content marketing 24/7."
slug: "tieu-tao-video-ai-sora-2-den-tiktok"
tags: [n8n, automation, content-creation, ai-multimodal, tiktok-automation]
keywords: [tự động hóa video tiktok, sora 2 n8n, tạo video ai tự động, content marketing tự động, n8n self-hosted]
---

# 🚀 **Tự Động Sáng Tạo Video AI Hài Hước với Sora 2 và Đăng Trực Tiếp lên TikTok**

### **Giải pháp cho các sếp muốn:**
- **Tạo video AI hài hước** chỉ với một form đơn giản, không cần kỹ năng thiết kế hoặc quay video.
- **Tối ưu tiêu đề video** bằng trí tuệ nhân tạo (GPT-5) để tăng tỷ lệ xem và tương tác.
- **Đăng video tự động lên TikTok** mà không cần can thiệp thủ công.
- **Tiết kiệm thời gian** lên đến 80% so với cách làm thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định 24/7, các sếp nên **self-host n8n** trên VPS để đảm bảo tính riêng tư và hiệu suất tối ưu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Chỉ cần nhập nội dung vào form, workflow sẽ tự động xử lý từ tạo video đến đăng tải.
- **Nội dung cá nhân hóa**: Tiêu đề video được tối ưu bằng GPT-5 để phù hợp với xu hướng TikTok.
- **Hoạt động liên tục**: Workflow chạy tự động theo lịch trình (mỗi 5 phút) hoặc khi có form submission.
- **Tăng engagement**: Video AI hài hước thu hút người dùng, giúp tăng lượt xem và tương tác.
- **Không cần kỹ năng code**: Sử dụng n8n với các node chuyên dụng, không cần viết một dòng mã.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản và API Key**:
   - [Tài khoản Sora 2 (Fal.ai)](https://fal.ai/) → Lấy **API Key** để truy cập API.
   - [Tài khoản Postiz](https://postiz.com/?ref=n3witalia) (7 ngày miễn phí) → Lấy **API Key** và **ChannelId** TikTok.
2. **N8n Self-hosted**:
   - Cài đặt n8n trên VPS (không dùng phiên bản cloud để sử dụng node **Postiz**).
3. **Các node bổ sung**:
   - `@n8n/n8n-nodes-langchain` (để sử dụng OpenAI GPT-5).
   - Node **Form Trigger** để nhận input từ người dùng.

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/10212) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON hoặc dán JSON vào ô.
  2. Chọn **Self-hosted** (nếu dùng phiên bản cloud, node **Postiz** sẽ không hoạt động).

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **A. Cấu hình API Key và Header Auth**
- **Node "Get status"**, **"Create Video"**, **"Get Url Video"**, **"Upload Video to Postiz"**:
  - **Credentials**: Chọn `httpHeaderAuth`.
  - **Header Name**: `Authorization`
  - **Header Value**: `Key YOUR_API_KEY_SORA_2` (thay `YOUR_API_KEY_SORA_2` bằng API Key từ Fal.ai).

#### **B. Cấu hình TikTok ChannelId**
- **Node "TikTok" (Postiz)**:
  - **Credentials**: Chọn `postizApi` (điền API Key từ Postiz).
  - **ChannelId**: Thay `XXX` bằng **ChannelId TikTok** của bạn (lấy từ **Calendar tab** trên Postiz sau khi kết nối TikTok).

#### **C. Cấu hình OpenAI GPT-5 (Generate title)**
- **Node "Generate title"**:
  - **Credentials**: Chọn `openAi` (điền API Key OpenAI).
  - **Prompt**: Sử dụng template mặc định để GPT-5 tự động tạo tiêu đề hấp dẫn cho video.

#### **D. Cấu hình Form Trigger**
- **Node "On form submission"**:
  - Thiết kế form với các trường input như:
    - **Tên video** (ví dụ: "AI tạo video hài hước về [chủ đề]")
    - **Mô tả** (nội dung video)
    - **Thẻ hashtag** (nếu muốn tự động thêm)
  - Kết nối form với node đầu tiên trong workflow để bắt đầu quá trình tự động.

#### **E. Thiết lập Schedule Trigger (lựa chọn)**
- Nếu muốn workflow chạy tự động theo lịch:
  - Thêm node **Schedule Trigger** (n8n-nodes-base.schedule).
  - Cấu hình chạy **mỗi 5 phút** (như hướng dẫn trong canvas gốc).

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** với dữ liệu mẫu (ví dụ: nhập "AI tạo video về con chó" vào form).
   - Kiểm tra từng node để đảm bảo không có lỗi.
2. **Active Workflow**:
   - Sau khi test thành công, chuyển trạng thái workflow sang **Active**.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Tối ưu video cho TikTok**:
   - Thêm node **Resize Video** (n8n-nodes-base.video) để đảm bảo video phù hợp với định dạng TikTok (9:16).
2. **Lưu log hoạt động**:
   - Thêm node **Google Sheets** (n8n-nodes-base.googleSheets) để ghi lại lịch sử video đã tạo và đăng.
3. **Gửi báo cáo định kỳ**:
   - Sử dụng node **Email** (n8n-nodes-base.email) để gửi báo cáo thống kê performance video hàng tuần.
4. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack/Telegram** (n8n-nodes-base.slack) để thông báo khi video được đăng thành công.
5. **Tăng tính cá nhân hóa**:
   - Sử dụng node **OpenAI Chat** để tự động tạo **câu chuyện kèm video** dựa trên input từ form.

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quá trình tạo và đăng video AI lên TikTok **không cần code**. Bằng cách kết hợp **Sora 2, GPT-5 và API TikTok**, các sếp có thể:
✅ **Tiết kiệm thời gian** lên đến 80%.
✅ **Tăng engagement** với nội dung hài hước và tối ưu.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

**Hãy import workflow này ngay hôm nay và bắt đầu tự động hóa content marketing của mình!** 🚀

---
**Ghi chú cuối:**
- Workflow này **chỉ hoạt động trên phiên bản self-hosted** của n8n.
- Để tối ưu hiệu suất, các sếp nên cài đặt n8n trên **VPS với tài nguyên cao** (như VPS Xeon 4GB+).
- Nếu gặp vấn đề, liên hệ tác giả Davide qua [LinkedIn](https://linkedin.com/in/davideboizza) hoặc email **info@n3w.it**.