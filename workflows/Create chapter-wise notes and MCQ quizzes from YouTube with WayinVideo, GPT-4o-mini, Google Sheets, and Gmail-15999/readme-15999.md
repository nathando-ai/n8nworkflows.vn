---
title: "🎓 **Tự Động Hóa Chuyển Bài Giảng YouTube Thành Chương Trình Học + Trắc Nghiệm MCQ Với AI (0 Code!)**"
description: "Giải pháp tự động hóa hoàn toàn chuyển video bài giảng YouTube thành tài liệu học tập có cấu trúc, trắc nghiệm tự động và báo cáo theo dõi - chỉ cần nhập URL. Sử dụng WayinVideo, GPT-4o-mini, Google Sheets và Gmail."
slug: "tieu-dong-hoa-chuyen-bai-giang-youtube-thanh-chuong-trinh-hoc-va-trac-nghiem"
tags: [n8n, automation, ai-summarization, content-creation, no-code, wayinvideo, gpt-4o-mini, google-sheets, gmail]
keywords: [tự động hóa bài giảng youtube, tạo tài liệu học tập từ video, trắc nghiệm mcq tự động, n8n workflow ai, gpt-4o-mini tự động hóa, google sheets tự động hóa]
---

# 🚀 **Tự Động Hóa Bài Giảng YouTube Sang Chương Trình Học + Trắc Nghiệm MCQ (Không Cần Code!)**

## **🔥 Nỗi Đau Của Học Sinh & Giảng Viên**
Học sinh phải mất **giờ đồng hồ** để ghi chép lại nội dung bài giảng từ YouTube, phân chia thành chương trình học, và tự tạo trắc nghiệm để kiểm tra kiến thức. Giảng viên lại phải **lặp đi lặp lại** công việc này cho từng video, dẫn đến:
❌ **Tốn thời gian** (thay vì học/tạo nội dung)
❌ **Chất lượng ghi chép không đồng nhất**
❌ **Không có trắc nghiệm tự động** để đánh giá hiểu biết
❌ **Không theo dõi được tiến độ học tập**

**Giải pháp?** Một **workflow tự động hóa hoàn toàn** chỉ cần **nhập URL YouTube**, hệ thống sẽ:
✅ **Trích xuất toàn bộ nội dung** từ video (kèm timestamp, người nói)
✅ **Phân tích và tạo tài liệu học tập theo chương** (mỗi chương là một chủ đề lớn)
✅ **Tự động sinh 5 câu hỏi trắc nghiệm MCQ** cho mỗi chương (câu trả lời + giải thích)
✅ **Gửi kết quả qua email** (định dạng HTML đẹp mắt)
✅ **Lưu lịch sử học tập** vào Google Sheets (để theo dõi tiến độ)

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 80% thời gian** so với ghi chép thủ công.
- **Tài liệu học tập có cấu trúc** (mỗi chương rõ ràng, dễ theo dõi).
- **Trắc nghiệm tự động** giúp học sinh ôn tập hiệu quả.
- **Hoạt động 24/7** (không cần can thiệp người dùng).
- **Báo cáo tự động** (Google Sheets theo dõi lịch sử học tập).
- **Cá nhân hóa** (học sinh nhận email với nội dung phù hợp).
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI SỬ DỤNG**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản WayinVideo API** (để trích xuất transcript từ YouTube):
   - Đăng ký tại [wayin.ai](https://wayin.ai/wayinvideo/api-dashboard) và mua **API units**.
   - Lấy **API Key** từ Dashboard.
2. **Tài khoản OpenAI** (để sử dụng GPT-4o-mini):
   - Đăng ký tại [OpenAI](https://platform.openai.com/) và lấy **API Key**.
3. **Tài khoản Google (Gmail + Google Sheets)**:
   - **Gmail OAuth2** (để gửi email tự động).
   - **Google Sheets OAuth2** (để lưu lịch sử học tập).
4. **Google Sheet mẫu** (cần tạo trước):
   - Tạo một bảng mới với **cột sau**:
     | Date | YouTube URL | Subject | Lecture Title | Chapters Generated | Quiz Questions | Summary | Notes | Quiz | Status |
   - Đặt tên tab là **"Study Log"**.
5. **VPS n8n (khuyến nghị)**:
   - Để workflow chạy **24/7** mà không bị gián đoạn.
   - 👉 [Đăng ký VPS TinoHost (Mã giảm giá: **VPSN8N** - 39% off)](https://tino.vn/vps-n8n?affid=388)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---
## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow từ File JSON**
:::step-by-step
1. **Tải workflow** từ [n8n.io/workflows/15999](https://n8n.io/workflows/15999) (chọn **Export as JSON**).
2. **Mở n8n Editor** (trên máy hoặc VPS).
3. **Nhấn "Import"** và chọn file JSON vừa tải.
4. **Xác nhận import** (n8n sẽ tạo workflow với 14 node).
:::

### **2. Các Bước Cấu Hình BẮT BUỘC**
Dưới đây là **các node quan trọng** cần chỉnh sửa:

#### **🔹 Node 2: HTTP — WayinVideo Submit Transcription**
- **Thay thế `YOUR_WAYINVIDEO_API_KEY`** bằng API Key của bạn (lấy từ WayinVideo Dashboard).
- **Kiểm tra header**:
  ```json
  {
    "Authorization": "Bearer YOUR_WAYINVIDEO_API_KEY",
    "x-wayinvideo-api-version": "v2"
  }
  ```

#### **🔹 Node 5: HTTP — Poll Transcription Status**
- **Cũng thay thế `YOUR_WAYINVIDEO_API_KEY`** như trên.
- **URL endpoint**:
  ```
  https://api.wayin.ai/wayinvideo/v2/tasks/{taskId}/results
  ```

#### **🔹 Node 10: AI Agent — Generate Notes and Quiz (GPT-4o-mini)**
- **Kết nối OpenAI API Key**:
  - Vào **Credentials** → Thêm **OpenAI** → Điền API Key.
  - Chọn **Model**: `gpt-4o-mini`.
- **Prompt mẫu** (n8n đã cấu hình sẵn, không cần chỉnh sửa):
  ```json
  {
    "role": "user",
    "content": "Analyze the transcript and generate structured chapter-wise notes and 5 MCQ questions per chapter."
  }
  ```

#### **🔹 Node 12: Google Sheets — Log Study Session**
- **Kết nối Google Sheets OAuth2**:
  - Vào **Credentials** → Thêm **Google Sheets** → Đăng nhập Google.
  - **Thay thế `YOUR_GOOGLE_SHEET_ID`** bằng ID của sheet Study Log (lấy từ URL sheet).
- **Cấu hình cột**:
  - Đảm bảo sheet có **các cột tương ứng** với bảng mẫu trên.

#### **🔹 Node 13: Gmail — Send Notes and Quiz**
- **Kết nối Gmail OAuth2**:
  - Vào **Credentials** → Thêm **Gmail** → Đăng nhập tài khoản Gmail.
  - **Chọn email mặc định** để gửi.

---
### **3. Kích Hoạt Workflow**
:::step-by-step
1. **Test Run với dữ liệu mẫu**:
   - Nhập **URL YouTube** vào form (ví dụ: [Bài giảng Toán cơ bản](https://www.youtube.com/watch?v=example)).
   - Chọn **Subject** (ví dụ: "Toán học").
   - Nhập **số chương** (ví dụ: 5).
   - Điền **email** để nhận kết quả.
   - Nhấn **"Execute"** để test.
2. **Kiểm tra kết quả**:
   - **Google Sheets**: Kiểm tra tab **Study Log** có dữ liệu mới không.
   - **Gmail**: Mở email để xem tài liệu học tập + trắc nghiệm.
3. **Bật Active**:
   - Sau khi test thành công, **bật switch Active** để workflow chạy tự động.
:::

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Tự Động Hóa Cho Nhiều Video**
- **Sử dụng Slack/Telegram Webhook** để nhận URL từ nhóm học tập:
  ```json
  {
    "type": "httpRequest",
    "method": "POST",
    "url": "https://your-n8n-url/webhook/your-webhook-id",
    "headers": {
      "Content-Type": "application/json"
    }
  }
  ```
- **Kết hợp với Zapier/Make** để tự động nhận dữ liệu từ các nguồn khác.

### **2. Lưu Log Lịch Sử Học Tập**
- **Thêm node `StickyNote`** để lưu **lịch sử hoạt động** (ví dụ: thời gian xử lý, trạng thái).
- **Tạo báo cáo tuần/month** bằng **Google Data Studio** hoặc **Power BI**.

### **3. Cải Tiến Trắc Nghiệm**
- **Thêm node `Code`** sau **GPT-4o-mini** để:
  - **Sắp xếp câu hỏi theo độ khó** (dễ → khó).
  - **Thêm hình ảnh minh họa** (nếu video có).
  - **Tạo file PDF** thay vì email (sử dụng **n8n-nodes-base.pdf**).

### **4. Chia Sẻ Kết Quả Cho Nhóm Học Tập**
- **Gửi kết quả qua Slack/Telegram** thay vì email:
  ```json
  {
    "type": "httpRequest",
    "method": "POST",
    "url": "https://api.telegram.org/bot YOUR_BOT_TOKEN/sendMessage",
    "body": {
      "chat_id": "YOUR_CHAT_ID",
      "text": "📚 Tài liệu học tập đã sẵn sàng: {{ $node["13"].json["htmlBody"] }}"
    }
  }
  ```

---
## 📌 **Kết Luận: Áp Dụng Ngay Hôm Nay!**

Workflow này **giải phóng thời gian** cho học sinh và giảng viên, đồng thời **cải thiện chất lượng học tập** bằng cách:
✔ **Tự động hóa 100%** (không cần code).
✔ **Tài liệu học tập có cấu trúc** (mỗi chương rõ ràng).
✔ **Trắc nghiệm tự động** để kiểm tra kiến thức.
✔ **Theo dõi lịch sử học tập** (Google Sheets).
✔ **Hoạt động 24/7** (không phụ thuộc vào thời gian làm việc).

**Bước đầu tiên?** **Import workflow và cấu hình API Key** ngay bây giờ! Sau đó, chỉ cần **nhập URL YouTube**, hệ thống sẽ tự làm tất cả.

---
### **🔗 Tài Liệu Tham Khảo**
- [WayinVideo API Dashboard](https://wayin.ai/wayinvideo/api-dashboard)
- [OpenAI API Docs](https://platform.openai.com/docs)
- [n8n Google Sheets Node](https://docs.n8n.io/integrations/builtins/nodes/googleSheets/)
- [n8n Gmail Node](https://docs.n8n.io/integrations/builtins/nodes/gmail/)

---
**🚀 CÓ THẮC MẮC?** Hãy để lại **comment** bên dưới hoặc liên hệ với tác giả [isaWOW](https://n8n.io/workflows/15999) để hỗ trợ!