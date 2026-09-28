---
title: "🚀 Tự Động Hoà Instagram Carousel AI: Từ Nghiên Cứu → Tạo Hình → Đăng Bài Chỉ Với 1 Clic!"
description: "Workflow này tự động hóa toàn bộ quy trình tạo và đăng bài carousel Instagram chuyên nghiệp bằng AI, tiết kiệm thời gian cho các sếp 100% không cần code. Từ nghiên cứu sâu, viết nội dung, tạo hình ảnh AI đến đăng bài - tất cả chỉ cần duyệt qua Slack!"
slug: "tieu-dong-hoa-instagram-carousel-ai"
tags: [n8n, automation, content-creation, ai-integration, instagram-marketing]
keywords: [n8n workflow instagram, tự động hóa content instagram, ai tạo hình ảnh, carousel instagram tự động, n8n + openai + kie.ai]
---

# 🚀 **Tự Động Hoà Instagram Carousel AI: Từ Nghiên Cứu → Tạo Hình → Đăng Bài Chỉ Với 1 Clic!**

### **🔥 Nỗi Đau Của Các Sếp Content Creator**
Các sếp đang mất **giờ đồng hồ** mỗi tuần để:
✅ Nghiên cứu chủ đề, tổng hợp thông tin từ nhiều nguồn
✅ Viết nội dung, cấu trúc bài viết thành nhiều slide carousel
✅ Tạo hình ảnh chuyên nghiệp (hoặc phải mua từ freelancer)
✅ Đăng bài lên Instagram và quản lý phản hồi

**Workflow này giải quyết tất cả!** Dùng AI + n8n để **tự động hóa toàn bộ quy trình**, chỉ cần duyệt qua Slack là xong.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với làm thủ công
- **Nội dung chuyên nghiệp** do AI nghiên cứu và viết
- **Hình ảnh AI** (Nano Banana Pro) phù hợp với từng slide
- **Đăng bài tự động** sau khi duyệt qua Slack
- **Hoạt động liên tục** 24/7, không phụ thuộc vào giờ làm việc
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản API**:
- **OpenAI** (API Key cho GPT-4o-mini & GPT-5-mini)
- **Slack** (Token API + Channel ID để duyệt nội dung)
- **Facebook Graph API** (Page Access Token cho đăng bài Instagram)
- **Kie.ai** (API Key cho tạo hình ảnh AI)

✔ **Thông tin cấu hình**:
- **ID Instagram Page** (để đăng bài)
- **Channel Slack** (để duyệt nội dung trước khi đăng)

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/11694](https://n8n.io/workflows/11694) (chọn **Export as JSON**)
2. Trên n8n Editor, nhấn **Import** → Chọn file JSON vừa tải
3. Chọn **Create new workflow** và nhấn **Import**

#### **Cách 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/11694](https://n8n.io/workflows/11694)
2. Trên n8n Editor, nhấn **Import** → Chọn **Paste JSON**
3. Chọn **Create new workflow** và nhấn **Import**

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
#### **🔹 Node `Schedule Trigger`**
- **Cấu hình**: Thiết lập lịch chạy (ví dụ: **mỗi ngày 9h sáng**)
- **Lưu ý**: Nếu không muốn chạy tự động, có thể bỏ qua và kích hoạt thủ công.

#### **🔹 Node `Research Agent` & `Drafting Agent` (OpenAI)**
- **Model**: Đã cấu hình sẵn **GPT-4o-mini** và **GPT-5-mini**
- **Prompt**: Các sếp có thể chỉnh sửa trong **`lmChatOpenAi`** nếu muốn thay đổi logic AI.

#### **🔹 Node `Slack Approval (Draft)` & `Slack Approval (Final)`**
- **Cấu hình**:
  - **Channel ID**: Điền ID của Slack Channel muốn duyệt (ví dụ: `#content-approval`)
  - **Message Template**: Có thể chỉnh sửa để phù hợp với nội dung (ví dụ: `Xin duyệt nội dung carousel về [topic]`)
- **Lưu ý**: Các sếp cần **cấu hình Slack API** trước khi chạy.

#### **🔹 Node `Image Generation (Kie.ai)`**
- **API Key**: Điền **API Key** của Kie.ai (nếu không có, đăng ký tại [kie.ai](https://kie.ai))
- **Prompt Template**: Workflow tự động tạo **prompt AI** từ nội dung slide, nhưng các sếp có thể chỉnh sửa trong **`JSON Parse (Prompts)`**.

#### **🔹 Node `IG Create Container` & `IG Publish` (Facebook Graph API)**
- **Page Access Token**: Điền **Page Access Token** của Instagram Page (cần có quyền **Page Publisher**)
- **Lưu ý**: Nếu token hết hạn, cần **refresh lại** trên [Facebook Developer](https://developers.facebook.com/)

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhập **topic** vào node `Schedule Trigger` (hoặc kích hoạt thủ công)
   - Kiểm tra **Slack** để duyệt nội dung
   - Sau khi duyệt, hệ thống sẽ tự động tạo hình và đăng bài

2. **Bật Active workflow**:
   - Nhấn **Active** trên n8n Editor
   - Đảm bảo **tất cả credentials** đã đúng

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Tích Hợp Telegram thay vì Slack**
- Thay thế node `slack` bằng **Telegram Bot** để duyệt nội dung qua Telegram
- **Cách làm**:
  ```json
  {
    "name": "Telegram Approval",
    "type": "httpRequest",
    "method": "post",
    "url": "https://api.telegram.org/bot[BOT_TOKEN]/sendMessage",
    "body": {
      "chat_id": "[CHAT_ID]",
      "text": "{{ $node["Slack Approval (Draft)"].json["message"] }}"
    }
  }
  ```

### **2. Lưu Log Tất Cả Các Bài Đăng**
- Thêm node **`n8n-nodes-base.googleSheets`** sau `IG Publish` để lưu:
  - **Topic**
  - **Ngày đăng**
  - **Link bài**
  - **Trạng thái (Đã duyệt/Đã đăng)**

### **3. Gửi Báo Cáo Định Kỳ**
- Sử dụng **`n8n-nodes-base.email`** hoặc **Slack Alert** để báo cáo:
  - **Số bài đăng thành công**
  - **Thời gian chạy**
  - **Topic phổ biến**

### **4. Tối Ưu Hóa Prompt AI**
- Chỉnh sửa **`Research Agent`** và **`Drafting Agent`** để:
  - **Nghiên cứu sâu hơn** (ví dụ: thêm yêu cầu "nêu ra 3 điểm quan trọng")
  - **Viết nội dung ngắn gọn hơn** (hoặc dài hơn tùy chủ đề)

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy** thay vì làm thủ công. **Chỉ cần duyệt qua Slack là xong** – AI sẽ tự động:
✅ Nghiên cứu và viết nội dung
✅ Tạo hình ảnh chuyên nghiệp
✅ Đăng bài lên Instagram

**🚀 Hãy thử ngay và tiết kiệm 80% thời gian content creation!**

---
**🔗 [Xem workflow gốc](https://n8n.io/workflows/11694) | 📌 [Cài đặt n8n Self-hosted](https://n8n.io/docs/)**