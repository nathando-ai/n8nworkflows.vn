---
title: "🚀 Tự Động Hóa Tạo Nội Dung Social Media Multi-Platform Với AI Sonnet 4.5 + Phê Chuẩn Người (GoToHuman) & Google Sheets"
description: "Workflow tự động hóa 100% không code tạo nội dung social media đa nền tảng, kết hợp AI Claude Sonnet 4.5 với phê duyệt con người qua GoToHuman, đồng bộ hóa với Google Sheets. Giúp các sếp tiết kiệm 80% thời gian soạn thảo, đảm bảo chất lượng nội dung cao và cá nhân hóa theo từng platform."
slug: "tieu-dong-hoa-tao-noi-dung-social-media-multi-platform"
tags: [n8n, automation, no-code, ai-powered, social-media, gotohuman, google-sheets, claude-sonnet-4-5]
keywords: [n8n workflow tự động hóa nội dung social, tạo bài viết AI Sonnet 4.5, phê duyệt nội dung GoToHuman, tự động hóa content marketing, Google Sheets + AI, nội dung đa nền tảng]
---

# 🚀 **Tự Động Hóa Tạo Nội Dung Social Media Multi-Platform Với AI Sonnet 4.5 + Phê Chuẩn Người (GoToHuman) & Google Sheets**

### **Giải pháp cho các sếp muốn:**
- **Tiết kiệm 80% thời gian** soạn thảo nội dung social media hàng ngày.
- **Đảm bảo chất lượng cao** với sự phê duyệt của con người trước khi xuất bản.
- **Tạo nội dung đa nền tảng** (Facebook, Instagram, LinkedIn, Twitter, TikTok...) từ một nguồn ý tưởng duy nhất.
- **Cá nhân hóa nội dung** theo từng platform mà không cần viết lại từ đầu.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ nhanh, ổn định cho AI)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: AI tự động tạo nội dung từ ý tưởng trong Google Sheets, chỉ cần phê duyệt 1 lần.
✅ **Chất lượng cao**: Kết hợp AI Sonnet 4.5 (mô hình ngôn ngữ tiên tiến của Anthropic) với phê duyệt con người qua GoToHuman.
✅ **Đa nền tảng**: Tạo nội dung cho **Facebook, Instagram, LinkedIn, Twitter, TikTok...** từ một template duy nhất.
✅ **Lưu trữ & theo dõi**: Tất cả ý tưởng và nội dung được đồng bộ hóa vào **Google Sheets**, dễ dàng theo dõi và cập nhật.
✅ **Hoạt động liên tục**: Workflow chạy tự động theo lịch trình (Schedule Trigger) hoặc khi có yêu cầu mới.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
📌 **Tài khoản & API Keys:**
- **Google Sheets**:
  - Tài khoản Google (để clone và chỉnh sửa template).
  - **Google Sheets OAuth 2.0 API Key** (cài đặt trong n8n Credentials).
- **GoToHuman**:
  - Tài khoản [GoToHuman](https://www.gotohuman.com/) (dùng để phê duyệt nội dung).
  - **API Key** của GoToHuman (cài đặt trong n8n Credentials).
- **Anthropic API**:
  - **API Key** của [Anthropic](https://www.anthropic.com/) (để sử dụng mô hình **Claude Sonnet 4.5**).
- **n8n Instance**:
  - Cài đặt **n8n Self-hosted** (không dùng phiên bản cloud).
  - Cài đặt **n8n nodes** cần thiết:
    - `@gotohuman/n8n-nodes-gotohuman` (để kết nối với GoToHuman).
    - `@n8n/n8n-nodes-langchain` (để sử dụng AI Sonnet 4.5).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [link gốc](https://n8n.io/workflows/9402) hoặc sao chép JSON từ canvas.
2. **Mở n8n Editor** (trang chủ của n8n self-hosted).
3. Nhấn **"Import"** → Dán JSON → Chọn **"Import"** để tải workflow vào.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Nhấn **"Create new workflow"** → Chọn **"Import from JSON"**.
2. Dán toàn bộ JSON từ workflow vào ô **"Paste JSON"** → Nhấn **"Import"**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Step 1: Chuẩn bị Google Sheets**
1. **Clone template Google Sheets**:
   - Mở [Google Sheet mẫu](https://docs.google.com/spreadsheets/d/1WLdKRpPxwLzvD27uHZIlY5Lcc5i-79PmapcWyYzJevI/edit?usp=sharing).
   - **Sao chép** (File → Make a copy) để tránh sửa sai template gốc.
   - **Cập nhật các trường bắt buộc**:
     - **Date** (ngày tạo nội dung).
     - **Idea** (ý tưởng hoặc chủ đề cần tạo nội dung).
     - **Platform** (chọn nền tảng social media: Facebook, Instagram, LinkedIn, Twitter, TikTok...).

2. **Cấu hình Google Sheets trong n8n**:
   - Trong node **"Get ideas"** và **"Update row in sheet"**:
     - **Credentials**: Chọn `"googleSheetsOAuth2Api"` (đã cài đặt trước).
     - **Sheet Name**: Điền tên sheet đã clone (ví dụ: `"Social Media Content Plan"`).
     - **Range**: Điền `"Sheet1!A:D"` (hoặc điều chỉnh theo cấu trúc của bạn).

#### **🔹 Step 2: Cấu hình GoToHuman (Phê duyệt nội dung)**
1. **Tạo Review Template trên GoToHuman**:
   - Đăng nhập [GoToHuman](https://www.gotohuman.com/).
   - Nhấn **"Create New Review Template"**.
   - **Cấu hình template**:
     - **Title**: "Social Media Content Review".
     - **Fields**:
       - **Content** (điền nội dung AI tạo).
       - **Platform** (Facebook, Instagram, LinkedIn...).
       - **Feedback** (để người phê duyệt đánh giá).
     - **Save** template.

2. **Cấu hình node GoToHuman trong n8n**:
   - Trong node **"Send review request and wait for response"**:
     - **Credentials**: Chọn `"gotoHumanApi"` (đã cài đặt API Key).
     - **Review Template ID**: Sao chép từ GoToHuman (đường dẫn template).
     - **Fields**:
       - `content`: `{{$node["Social Media Content Creator"].json["content"]}}` (lấy từ node AI).
       - `platform`: `{{$node["Set Text"].json["platform"]}}` (lấy từ node Set Text).

#### **🔹 Step 3: Cấu hình AI Sonnet 4.5 (Anthropic)**
1. **Cài đặt Anthropic API Key**:
   - Trên [Anthropic Dashboard](https://www.anthropic.com/), tạo **API Key**.
   - Trong n8n:
     - **Credentials**: Chọn `"anthropicApi"` (đã cài đặt).
     - **Model**: Đảm bảo chọn `"claude-sonnet-4-5-20250929"` (đã cấu hình trong node `"Anthropic Chat Model"`).

2. **Cấu hình Prompt cho AI**:
   - Trong node **"Set new prompt"**:
     - **Text**: Cập nhật **prompt** để AI tạo nội dung phù hợp với platform:
       ```json
       "Tạo nội dung social media cho {{platform}} với chủ đề: {{idea}}. Nội dung phải:
       - Đúng với tone của {{platform}}.
       - Có từ 100-150 từ.
       - Được chia thành 3 phần: Hook, Body, Call-to-Action.
       - Tránh từ lặp lại và sử dụng ngôn ngữ thân thiện."
       ```
   - **Lưu ý**: Thay thế `{{platform}}` và `{{idea}}` bằng các biến từ Google Sheets.

#### **🔹 Step 4: Cấu hình Schedule Trigger (Nếu muốn chạy tự động)**
1. Trong node **"Schedule Trigger"**:
   - **Schedule**: Chọn **"Daily"** (hoặc **"Weekly"**).
   - **Time**: Đặt giờ chạy (ví dụ: **8h sáng** để nội dung được phê duyệt kịp thời).
   - **Active**: Bật **"Active"** để workflow chạy theo lịch.

#### **🔹 Step 5: Kết nối các node**
- **Flow logic**:
  1. **Manual Trigger** → Bắt đầu workflow (hoặc **Schedule Trigger**).
  2. **Get ideas** → Lấy ý tưởng từ Google Sheets.
  3. **Set Text** → Đặt biến `platform` và `idea`.
  4. **Social Media Content Creator (Agent)** → AI tạo nội dung.
  5. **Anthropic Chat Model** → Kiểm tra và hoàn thiện nội dung.
  6. **Send review request** → Gửi nội dung cho GoToHuman phê duyệt.
  7. **Switch** → Kiểm tra phản hồi:
     - **Nếu Approved**: Cập nhật nội dung vào Google Sheets.
     - **Nếu Rejected**: Gửi lại cho AI sửa (hoặc thông báo cho người quản lý).

---

### **3. Kích hoạt ⚡️**
1. **Test Run (Để thử nghiệm trước khi chạy thực tế)**:
   - Nhấn **"Run"** trên node **"Manual Trigger"**.
   - Kiểm tra:
     - AI có tạo nội dung không?
     - GoToHuman có nhận được yêu cầu phê duyệt không?
     - Google Sheets có cập nhật nội dung không?

2. **Bật Active Workflow**:
   - Sau khi test thành công, chuyển **"Active"** từ **OFF** sang **ON**.
   - Nếu dùng **Schedule Trigger**, workflow sẽ chạy tự động theo lịch.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **🔹 1. Tối ưu hóa Prompt cho AI**
- **Cập nhật prompt** để AI tạo nội dung phù hợp với từng platform:
  - **Facebook/Instagram**: Nội dung dài, cảm xúc, hình ảnh.
  - **LinkedIn**: Nội dung chuyên nghiệp, chia sẻ kiến thức.
  - **Twitter/X**: Gọn gàng, ngắn gọn, có hashtag.
  - **TikTok**: Nội dung ngắn, hấp dẫn, có âm thanh.

### **🔹 2. Kết nối với Slack/Telegram để thông báo**
- Thêm node **Slack** hoặc **Telegram Bot** để:
  - **Thông báo khi nội dung được phê duyệt**.
  - **Gửi link nội dung** cho team review.
- **Cách làm**:
  1. Thêm node **"Slack Webhook"** hoặc **"Telegram Bot"** vào workflow.
  2. Cấu hình **message template**:
     ```json
     "Nội dung mới được phê duyệt cho {{platform}}:\n\n{{$node["Social Media Content Creator"].json["content"]}}\n\n🔗 [Xem chi tiết trên Google Sheets]({{$node["Update row in sheet"].json["link"]}})"
     ```

### **🔹 3. Lưu log hoạt động vào Google Sheets**
- Thêm node **"Set"** trước node **"Update row in sheet"** để lưu:
  - Thời gian tạo.
  - Trạng thái (Approved/Rejected).
  - Người phê duyệt.
- **Cấu trúc cột mới trong Google Sheets**:
  | Date       | Idea          | Platform  | Content                     | Status   | Reviewer   | Time Created |
  |------------|---------------|-----------|-----------------------------|----------|------------|--------------|
  | 2024-05-20 | "Tips SEO 2024" | Facebook  | "Nội dung AI tạo..."        | Approved | Alice      | 08:30 AM    |

### **🔹 4. Tự động gửi báo cáo hàng tuần**
- Sử dụng **Schedule Trigger** để chạy **1 lần/tuần** và:
  - **Tính toán thống kê**: Số lượng nội dung được phê duyệt, tỷ lệ reject.
  - **Gửi báo cáo** qua email hoặc Slack.
- **Cách làm**:
  1. Thêm node **"Set"** để tính toán:
     ```json
     {
       "approved": "{{$json["status"] === "Approved" ? 1 : 0}}",
       "rejected": "{{$json["status"] === "Rejected" ? 1 : 0}}"
     }
     ```
  2. Thêm node **"Google Sheets"** để cập nhật báo cáo.
  3. Thêm node **"Email"** (nếu dùng Gmail) hoặc **"Slack"** để gửi báo cáo.

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tự động hóa 100% quá trình tạo nội dung social media**.
✔ **Đảm bảo chất lượng** với sự phê duyệt của con người.
✔ **Tiết kiệm thời gian** và tập trung vào chiến lược marketing hơn.

**Hành động ngay!**
1. **Clone Google Sheets** và cập nhật ý tưởng.
2. **Cấu hình GoToHuman** và Anthropic API.
3. **Import workflow** và **bật chạy**!
4. **Theo dõi kết quả** và tối ưu hóa prompt cho AI.

**🚀 Cài đặt n8n trên VPS ngay hôm nay** để workflow hoạt động **24/7** mà không bị gián đoạn:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)

---
**Chia sẻ & phản hồi:**
Nếu các sếp có **ý tưởng cải tiến** hoặc **vấn đề gặp phải**, hãy để lại comment dưới đây hoặc liên hệ