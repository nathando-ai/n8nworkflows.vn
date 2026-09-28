---
title: "🚀 Tự Động Hoàn Thành Bài Giảng Webinar Sang Trang Tri Thông Tin Notion Với AI GPT-4o-mini & WayinVideo"
description: "Giải pháp tự động hóa 100% không code để chuyển đổi video webinar thành hệ thống tri thức Notion hoàn chỉnh, bao gồm tóm tắt, ý chính, hành động thực hiện, dẫn chứng nổi bật và nhãn tag. Tiết kiệm 10+ giờ công cho mỗi buổi webinar!"
slug: "tieu-dong-hoan-thanh-bai-giang-webinar-sang-notion-voi-gpt-4o-mini"
tags: [n8n, automation, no-code, ai-summarization, notion-automation, wayinvideo, gpt-4o-mini, knowledge-base]
keywords: [n8n workflow webinar, tự động hóa webinar sang notion, gpt-4o-mini extraxt knowledge, wayinvideo transcription, tự động hóa tri thức doanh nghiệp, notion knowledge base]
---

# 🚀 **Tự Động Hoàn Thành Bài Giảng Webinar Sang Trang Tri Thông Tin Notion Với AI GPT-4o-mini & WayinVideo**

### **Giải pháp cho:**
- **Các doanh nghiệp** cần hệ thống tri thức chuyên sâu từ webinar mà không phải xem lại video.
- **Giảng viên/đào tạo** muốn lưu trữ kiến thức từ buổi học dưới dạng trang tri thức dễ tìm kiếm.
- **Cố vấn/người chuyên môn** cần tổng hợp ý chính từ buổi chia sẻ để chia sẻ với khách hàng.
- **Nhóm marketing** muốn tối ưu hóa nội dung từ webinar thành tài liệu tham khảo.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7 mà không gặp lỗi, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ xử lý nhanh cho AI)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10+ giờ công** cho mỗi buổi webinar (không cần xem lại video hoặc ghi chú tay).
✅ **Hệ thống tri thức Notion hoàn chỉnh** với **3-8 trang chủ đề** (tùy theo nội dung), mỗi trang bao gồm:
   - Tóm tắt chi tiết
   - Ý chính và hành động thực hiện
   - Dẫn chứng nổi bật (quotes)
   - Thời gian xuất hiện trong video
   - Nhãn tag (tags) để phân loại
✅ **Lưu trữ tự động** trên Google Sheets với liên kết trực tiếp đến Notion.
✅ **Hoạt động liên tục** 24/7, không phụ thuộc vào thời gian làm việc của nhân viên.
✅ **Cá nhân hóa** theo từng webinar (tên bài giảng, người dẫn, chủ đề, ngày tháng).
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản WayinVideo** (để transcribe video):
   - [Đăng ký miễn phí WayinVideo](https://wayin.video/) (có API key).
   - **Lưu ý:** API key phải có quyền `transcription`.
2. **Tài khoản OpenAI** (để sử dụng GPT-4o-mini):
   - [Đăng ký OpenAI](https://platform.openai.com/) và tạo **API key**.
3. **Tài khoản Notion** (để tạo trang tri thức):
   - [Đăng ký Notion](https://www.notion.so/) và tạo **database** để lưu trang chủ đề.
   - **Lưu ý:** Cần **ID của database** (thường là chuỗi số trong URL).
4. **Tài khoản Google Sheets** (để log lịch sử):
   - Tạo một **Google Sheet** mới với tab tên **"Knowledge Base Log"**.
   - Cấu trúc cột bắt buộc:
     | Webinar Title | Topic Title | Speaker | Topic Category | Webinar Date | Notion Page ID | Notion Page URL | Tags | Created On | Status |
     |---------------|-------------|---------|-----------------|--------------|-----------------|-------------------|--------|-----------|---------|
5. **VPS n8n** (để chạy workflow 24/7):
   - Khuyến nghị sử dụng **VPS Xeon 4GB** để tránh lag khi xử lý AI.

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/15358](https://n8n.io/workflows/15358) (ấn **Export**).
2. Trên **n8n Editor**, nhấn **Import** và chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở **n8n Editor** và tạo workflow mới.
2. Nhấn **Import** → **Paste JSON** và dán nội dung từ [n8n.io/workflows/15358](https://n8n.io/workflows/15358) (ấn **Export** → **Copy JSON**).
3. Chọn **Create new workflow** và nhấn **Import**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **Node 2 & 4: WayinVideo — Submit Transcription & Get Transcript Results**
- **Thay thế `YOUR_WAYINVIDEO_API_KEY`** bằng API key của bạn (tìm trong tài khoản WayinVideo).
- **Kiểm tra URL API**:
  - Submit: `https://api.wayin.video/v1/transcription`
  - Polling: `https://api.wayin.video/v1/transcription/{task_id}`

#### **Node 9: OpenAI — GPT-4o-mini Model**
- **Kết nối credential OpenAI**:
  1. Trên **n8n Editor**, nhấn **Credentials** → **Add new credential** → **OpenAI**.
  2. Nhập **API key** từ tài khoản OpenAI.
  3. Chọn credential này trong node **GPT-4o-mini**.

#### **Node 11: Notion — Create Topic Page**
- **Kết nối credential Notion OAuth**:
  1. Trên **n8n Editor**, nhấn **Credentials** → **Add new credential** → **Notion**.
  2. Nhập **Notion API key** (tạo từ [Notion API](https://www.notion.so/my-integrations)).
  3. **Thiết lập Parent Database ID**:
     - Mở database Notion bạn muốn lưu trang chủ đề.
     - Copy **ID** từ URL (ví dụ: `https://www.notion.so/workspace/abc123...` → `abc123...`).
     - Điền vào trường **Parent Database ID** trong node Notion.

#### **Node 12: Google Sheets — Log Created Pages**
- **Kết nối credential Google Sheets OAuth2**:
  1. Trên **n8n Editor**, nhấn **Credentials** → **Add new credential** → **Google Sheets**.
  2. Nhập **Client ID** và **Client Secret** từ [Google Cloud Console](https://console.cloud.google.com/).
  3. **Thay thế `YOUR_GOOGLE_SHEET_LOG_ID`** bằng **ID của Google Sheet** (tìm trong URL của tab "Knowledge Base Log").
  4. **Kiểm tra cấu trúc cột** trong Google Sheet (phải khớp với mô tả ở trên).

#### **Node 7 & 10: Code — Format Transcript & Parse Topics**
- **Không cần chỉnh sửa** nếu đã import workflow chính xác.
- **Lưu ý:** Nếu video webinar quá dài (>30 phút), có thể tăng thời gian chờ trong **Node 3 (Wait — 90 Seconds)** lên **120-180 giây**.

---

### **3. Kích hoạt ⚡️**
1. **Test run với dữ liệu mẫu**:
   - Nhập URL của một video webinar ngắn (ví dụ: dưới 10 phút) vào **Form Trigger**.
   - Chạy workflow và kiểm tra:
     - Transcript có được tạo không?
     - AI có extraxt được 3-8 chủ đề không?
     - Notion có tạo trang chủ đề không?
     - Google Sheets có log dữ liệu không?
2. **Bật Active workflow**:
   - Sau khi test thành công, nhấn **Active** trên workflow.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tối ưu hóa cho webinar dài**
- **Tăng thời gian chờ** trong **Node 3 (Wait — 90 Seconds)** lên **180 giây** nếu video >30 phút.
- **Sử dụng WayinVideo Pro** (nếu có) để tăng tốc độ transcribe.

### **2. Kết hợp với Slack/Telegram để thông báo**
- Thêm **Node Slack/Telegram** sau **Node 12 (Google Sheets)** để gửi thông báo khi trang Notion được tạo thành công.
- **Cách làm**:
  1. Thêm node **Slack** (hoặc **Telegram**) vào cuối workflow.
  2. Cấu hình message mẫu:
     ```
     📌 **New Knowledge Page Created!**
     - **Webinar:** [{{ $json["webinar_title"] }}]
     - **Topic:** [{{ $json["topic_title"] }}]
     - **Notion URL:** [{{ $json["notion_url"] }}]
     ```

### **3. Lưu log lỗi và báo cáo định kỳ**
- Thêm **Node StickyNote** (hoặc **Google Sheets**) để log lỗi nếu workflow bị crash.
- **Cách làm**:
  1. Thêm node **StickyNote** sau **Node 5 (IF — Transcription Complete?)**.
  2. Cấu hình để ghi lỗi nếu transcribe thất bại.

### **4. Tự động chia sẻ trang Notion cho nhóm**
- Sử dụng **Node Notion — Share Page** để tự động chia sẻ trang chủ đề cho thành viên nhóm.
- **Cách làm**:
  1. Thêm node **Notion — Share Page** sau **Node 11**.
  2. Chọn **Permission Level** là **Read** và nhập **Email** của thành viên.

### **5. Tích hợp với CRM (HubSpot, Salesforce)**
- Sử dụng **Node HTTP Request** để gửi thông tin trang Notion vào CRM khi webinar liên quan đến khách hàng.
- **Cách làm**:
  1. Thêm node **HTTP Request** sau **Node 12**.
  2. Gửi payload JSON đến API của CRM (ví dụ: HubSpot).

---

## 📌 **Kết luận**
Workflow này **giải phóng bạn khỏi công việc thủ công** khi phải xem lại video webinar và ghi chú. Với **AI GPT-4o-mini**, nó tự động extraxt **3-8 chủ đề chính**, xây dựng **trang tri thức Notion hoàn chỉnh**, và **log dữ liệu** để quản lý dễ dàng.

👉 **Hành động ngay:**
1. **Chuẩn bị tài khoản** (WayinVideo, OpenAI, Notion, Google Sheets).
2. **Import workflow** và **cấu hình credential**.
3. **Test với video mẫu** và **bật Active**.
4. **Kết hợp với Slack/CRM** để tối ưu hóa hơn.

**Không cần code, không cần chuyên môn AI — chỉ cần copy/paste và chạy!** 🚀

---
**Cần hỗ trợ?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) và liên hệ **isaWOW** trên [n8n Community](https://community.n8n.io/) để tối ưu workflow!