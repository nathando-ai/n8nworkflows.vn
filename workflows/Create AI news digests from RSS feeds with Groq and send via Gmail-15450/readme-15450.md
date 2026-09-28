---
title: "🤖 Tự Động Tạo Tóm Tắt Tin Tức AI Từ RSS Feeds Với Groq & Gửi Email (N8n)"
description: "Workflow tự động hóa lấy tin tức mới nhất từ The Verge và TechCrunch về AI/Tech, tóm tắt bằng AI (Groq), và gửi newsletter định kỳ qua Gmail - tiết kiệm 5+ giờ công mỗi tuần cho các sếp và chuyên gia kỹ thuật."
slug: "tieu-dong-tao-tom-tat-tin-tuc-ai-rss-groq-gmail"
tags: [n8n, automation, ai-summarization, groq, gmail, rss-feed, no-code]
keywords: [n8n workflow tự động hóa, tóm tắt tin tức AI, Groq API, RSS feeds, gửi newsletter tự động, tự động hóa email]
---

# 🚀 **Tự Động Tạo Newsletter AI Từ RSS Feeds Với Groq & Gmail**

Hết sức mệt mỏi phải tra cứu hàng chục nguồn tin tức AI/Tech mỗi ngày? Hay phải mất thời gian tóm tắt và gửi cho đồng nghiệp? **Workflow này sẽ tự động hóa toàn bộ quá trình** - lấy tin tức mới nhất từ The Verge và TechCrunch, tóm tắt bằng AI Groq, và gửi newsletter định kỳ qua Gmail - **không cần viết một dòng code nào!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 mà không gián đoạn, các sếp nên **self-host n8n trên VPS** để đảm bảo tính ổn định và bảo mật cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5+ giờ/tuần**: Không phải tra cứu và tóm tắt tin tức thủ công.
- **Tin tức mới nhất**: Lấy từ 2 nguồn tin chính (The Verge & TechCrunch) về AI/Tech.
- **Tóm tắt chuyên nghiệp**: AI Groq (Llama 3.3 70B) tự động tóm tắt và sắp xếp tin tức.
- **Gửi tự động**: Newsletter định kỳ qua Gmail (hoặc thay thế bằng Slack/Telegram).
- **Cá nhân hóa**: Thêm/loại bỏ nguồn tin hoặc điều chỉnh nội dung dễ dàng.
- **Hoạt động liên tục**: Chỉ cần kích hoạt 1 lần, workflow sẽ tự động chạy hàng ngày.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Groq API**:
   - [Đăng ký tài khoản Groq](https://console.groq.com/) và lấy **API Key**.
   - Mô hình AI được sử dụng: `llama-3.3-70b-versatile` (miễn phí trong giới hạn).
2. **Tài khoản Gmail**:
   - Tài khoản Gmail để nhận và gửi newsletter (cần **OAuth2**).
   - Địa chỉ email nhận (cần thiết định trong node Gmail).
3. **RSS Feeds** (đã cấu hình sẵn):
   - The Verge (AI/Tech): `https://feeds.theverge.com/rss/ai`
   - TechCrunch (AI): `https://feeds.feedburner.com/TechCrunch/AI`
   *(Các sếp có thể thay đổi nguồn tin theo nhu cầu.)*
4. **N8n Workspace**:
   - N8n phiên bản **2.5000+** (để hỗ trợ nodes Groq và Agent).
   - Nodes cần thiết: `n8n-nodes-base`, `@n8n/n8n-nodes-langchain`.

---

### 🚀 **Cách Import & Lưu ý khi "Lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/15450) hoặc copy toàn bộ JSON từ canvas.
- **Cách import**:
  - Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON hoặc dán JSON vào ô `Paste JSON`.
  - Nhấn **Import Workflow**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **22 node**, nhưng các sếp chỉ cần chú ý đến các phần sau:

##### **A. Cấu hình Groq API**
- **Node "Groq Chat Model2" và "Groq Chat Model3"**:
  - Đi đến **Credentials** → Thêm **Groq API Key** (đã lấy từ bước chuẩn bị).
  - **Model**: Đã mặc định là `llama-3.3-70b-versatile` (không cần thay đổi).

##### **B. Cấu hình Gmail**
- **Node "Send a message"**:
  - Nhấn **Add Credential** → Chọn **Gmail OAuth2**.
  - Đăng nhập tài khoản Gmail và cấp quyền.
  - **Tham số cần chỉnh**:
    - `sendTo`: Địa chỉ email nhận (ví dụ: `tinnhan@doanhnghiep.com`).
    - `subject`: Tiêu đề email (mặc định: `🤖 AI News Digest - [Ngày]`).
    - `html`: Nội dung HTML (sẽ tự động được tạo bởi AI).

##### **C. Cấu hình RSS Feeds**
- **Node "The verge1" và "TechCrunch1"**:
  - **URL Feed**: Đã mặc định, nhưng các sếp có thể thay đổi nếu muốn lấy từ nguồn khác.
  - **Example**: `https://feeds.theverge.com/rss/ai` → `https://feeds.feedburner.com/TechCrunch/AI`.

##### **D. Tham số quan trọng khác**
- **Node "Limit1"**:
  - **Limit**: Đặt số lượng bài viết tối đa (mặc định: **6 bài**).
- **Node "memory1"**:
  - Đây là **bộ nhớ tạm thời** của workflow để lưu trữ kết quả tóm tắt.
  - **Không cần chỉnh**, nhưng các sếp có thể xóa dữ liệu cũ bằng cách **reset workflow**.
- **Node "AI Agent2"**:
  - AI này sẽ **lập trình lại** toàn bộ tin tức thành một newsletter hoàn chỉnh.
  - **Prompt mặc định** đã được tối ưu, nhưng các sếp có thể chỉnh sửa trong **node "Code in JavaScript1"** nếu muốn.

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Nhấn **Execute Workflow** để chạy thử với dữ liệu mẫu.
  - Kiểm tra **Gmail** để xem kết quả.
- **Bật Active**:
  - Sau khi kiểm tra thành công, chuyển **Status** từ `Inactive` sang `Active`.
- **Cài đặt lịch chạy (Optional)**:
  - Thay thế **Manual Trigger** bằng **Schedule Trigger** (ví dụ: **8h sáng hàng ngày**).
  - Cách cài đặt:
    1. Thêm node **Schedule Trigger** vào đầu workflow.
    2. Chỉnh **cron expression** (ví dụ: `0 8 * * *` để chạy lúc 8h sáng).

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm nguồn tin khác**:
   - Thêm node **RSS Feed Read** mới và kết nối vào **Merge All RSS Items1**.
   - Ví dụ: `https://feeds.feedburner.com/Techmeme` (tin tức công nghệ).

2. **Gửi newsletter qua Slack/Telegram**:
   - Thay thế node **Gmail** bằng **Slack Webhook** hoặc **Telegram Bot**.
   - Cách làm:
     - Tạo **webhook Slack** hoặc **bot Telegram**.
     - Thêm node **Slack** hoặc **Telegram Bot** và cấu hình.

3. **Lưu log hoạt động**:
   - Thêm node **Google Sheets** hoặc **Notion** để ghi lại lịch sử newsletter.
   - Cách làm:
     - Thêm node **Google Sheets** vào cuối workflow.
     - Cấu hình để ghi dữ liệu như `Ngày`, `Số bài viết`, `Link tin tức`.

4. **Tùy chỉnh nội dung AI**:
   - Mở node **Code in JavaScript1** để chỉnh sửa **prompt** cho AI.
   - Ví dụ: Yêu cầu AI thêm **đánh giá ngắn** hoặc **điểm nổi bật** cho mỗi bài.

5. **Chia sẻ newsletter cho nhiều người**:
   - Thay thế `sendTo` trong node Gmail bằng **danh sách email** (ví dụ: `tinnhan@doanhnghiep.com, team@doanhnghiep.com`).

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp và chuyên gia kỹ thuật để tập trung vào công việc chiến lược hơn. Bằng cách tự động hóa việc lấy tin tức, tóm tắt và gửi newsletter, các sếp sẽ **luôn cập nhật với xu hướng AI/Tech mới nhất mà không mất thời gian**.

**Hành động ngay!**
1. Import workflow vào **n8n Editor**.
2. Cấu hình **Groq API** và **Gmail**.
3. Chạy thử và **bật lịch chạy hàng ngày**.
4. **Chia sẻ kết quả** với đồng nghiệp và bắt đầu tiết kiệm thời gian!

👉 **Bắt đầu tự động hóa ngay hôm nay!** Nếu có vấn đề, hãy để lại bình luận dưới đây. Chúc các sếp thành công! 🚀