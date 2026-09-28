---
title: "🔍 **Tự Động Hóa Theo Dõi Bài Đăng LinkedIn Của Đối Thủ Với Airtop & Slack – Không Cần Code!**"
description: "Giải pháp tự động hóa 24/7 để theo dõi, phân tích và báo cáo bài đăng mới nhất của đối thủ trên LinkedIn, gửi kết quả tự động lên Slack. Tiết kiệm thời gian lên đến 10 giờ/tuần cho các sếp Marketing & Sales."
slug: "tu-dong-hoa-theo-doi-bai-dang-linkedin-doi-thu-voi-airtop"
tags: [n8n, automation, ai, linkedin, competitor-analysis, airtop, slack, google-sheets]
keywords: [tự động hóa linkedin, theo dõi đối thủ, airtop n8n, báo cáo đối thủ, tự động hóa marketing, n8n workflow ai]
---

# 🚀 **Tự Động Hóa Theo Dõi Bài Đăng LinkedIn Của Đối Thủ – Giúp Các Sếp Marketing & Sales Nắm Trọn Thông Tin Mới Nhất**

### **Nỗi Đau Của Các Sếp Hiện Nay**
Các sếp Marketing & Sales thường phải **tốn thời gian hàng giờ** mỗi tuần để:
- **Tìm kiếm thủ công** bài đăng mới nhất của đối thủ trên LinkedIn.
- **Đọc và phân tích** nội dung, chủ đề, và mức độ tương tác của từng bài.
- **Ghi chép vào file Excel** hoặc gửi báo cáo qua Slack/Email cho team.
- **Mất thời gian** để tổng hợp và đưa ra chiến lược phản ứng kịp thời.

**Kết quả?** Thông tin quan trọng bị bỏ lỡ, đối thủ có cơ hội dẫn đầu trong chiến lược nội dung và branding.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✅ **Tiết kiệm 10+ giờ/tuần** (không cần theo dõi thủ công).
✅ **Nhận báo cáo tự động** với:
   - **Số lượng bài đăng mới nhất** trong tuần (tối đa 5 bài).
   - **Chủ đề chính** được đối thủ nhấn mạnh.
   - **Mức độ tương tác** (like, comment, share) của mỗi bài.
✅ **Cập nhật liên tục** (không phụ thuộc vào thời gian làm việc).
✅ **Cá nhân hóa báo cáo** gửi trực tiếp lên Slack cho team.

---
### **🔧 Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
🔹 **Tài khoản Airtop** (miễn phí):
   - [Tạo API Key](https://portal.airtop.ai/api-keys)
   - [Tạo Profile LinkedIn](https://portal.airtop.ai/browser-profiles) (đăng nhập vào LinkedIn để Airtop tự động hóa tương tác).
🔹 **Google Sheet** chứa danh sách URL LinkedIn của đối thủ:
   - [Mẫu Google Sheet](https://docs.google.com/spreadsheets/d/1TknyHS8ie0KONgF4-KFGR76I74egHLt7-M9sIxjQXGY/edit) (các sếp sao chép và cập nhật URL).
🔹 **Slack Bot** với quyền gửi tin nhắn vào channel:
   - [Hướng dẫn tạo Slack Bot](https://api.slack.com/apps).
🔹 **n8n Self-hosted** (để workflow chạy 24/7):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---
### **🚀 Cách Import & Cấu Hình Workflow**

#### **1. Import Workflow từ File JSON**
Các sếp có thể:
- **Tải workflow** từ [n8n.io](https://n8n.io/workflows/5167) và import vào n8n Editor.
- **Copy JSON** từ link trên và dán vào n8n Editor (đường dẫn: `https://n8n.io/workflows/5167/raw`).

#### **2. Các Bước Cấu Hình BẮT BUỘC**
Sau khi import, các sếp cần chỉnh sửa **4 node chính**:

##### **📌 Node 1: Schedule Trigger (Đặt Lịch Trình)**
- **Thiết lập thời gian chạy tự động** (ví dụ: **mỗi thứ 2 hàng tuần lúc 8h sáng**).
- **Lưu ý:** Chọn **timezone** phù hợp với giờ làm việc của team.

##### **📌 Node 2: Get Competitors (Lấy Danh Sách Đối Thủ từ Google Sheets)**
- **Chọn credentials:** `googleSheetsOAuth2Api` (đã cấu hình trước khi import).
- **Sheet Name:** Đặt tên là **"Competitor Profiles"** (hoặc tên sheet trong file mẫu).
- **Range:** Chọn **A2:A** (giả sử cột A chứa URL LinkedIn).
- **Lưu ý:** Đảm bảo **Google Sheet** đã được chia sẻ với tài khoản OAuth2 của n8n.

##### **📌 Node 3: Analyze Posts (Phân Tích Bài Đăng với Airtop)**
- **Chọn credentials:** `airtopApi` (API Key đã tạo trên Airtop).
- **Profile Name:** Nhập tên **Profile LinkedIn** đã tạo trên Airtop (đăng nhập vào LinkedIn).
- **Prompt:** Đã được cấu hình sẵn, **không cần chỉnh sửa** (nếu muốn thay đổi, các sếp có thể tự viết prompt mới):
   ```plaintext
   This is a list of posts.
   Perform the following steps:
   1. Extract the text of up to 5 posts that were published no more than 1 week ago.
   2. Summarize the selected posts and highlight:
      - Number of posts published in the last week
      - Main topics covered in the posts
      - Level of user engagement with the posts
   ```
- **Lưu ý:**
  - Airtop sẽ tự động **login LinkedIn** và **trích xuất bài đăng mới nhất**.
  - Nếu gặp lỗi, kiểm tra **Profile LinkedIn** có được cấu hình đúng không.

##### **📌 Node 4: Send Summary (Gửi Báo Cáo lên Slack)**
- **Chọn credentials:** `slackApi` (Bot Token đã tạo trên Slack).
- **Channel:** Chọn **channel** muốn nhận báo cáo (ví dụ: `#competitor-monitoring`).
- **Message Format:** Cấu hình sẵn, **không cần chỉnh sửa** (nếu muốn thay đổi, các sếp có thể tự viết template mới).
- **Lưu ý:**
  - Đảm bảo **Slack Bot** có quyền gửi tin nhắn vào channel.
  - Báo cáo sẽ có **format rich text** với tiêu đề, nội dung tóm tắt, và số liệu chi tiết.

#### **3. Kích Hoạt Workflow**
- **Test Run:** Chạy **manual test** với 1-2 URL đối thủ để kiểm tra kết quả.
- **Active Workflow:** Bật **Active** để workflow chạy tự động theo lịch trình.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Log Lịch Sử:**
   - Sử dụng **Sticky Note** (node `stickyNote`) để lưu **log** của mỗi lần chạy (ví dụ: ngày giờ, URL bài đăng, kết quả phân tích).
   - **Cách làm:** Thêm node `stickyNote` sau `Analyze Posts` và cấu hình để lưu dữ liệu.

2. **Gửi Báo Cáo qua Email:**
   - Thay vì Slack, các sếp có thể **kết nối với Gmail** (node `n8n-nodes-base.email`) để gửi báo cáo tự động qua Email.

3. **Tăng Số Lượng Bài Đăng:**
   - Nếu muốn phân tích **nhiều hơn 5 bài**, chỉnh sửa **prompt** trong node `Analyze Posts`:
     ```plaintext
     Extract up to 10 posts...
     ```

4. **Kết Nối với CRM:**
   - Sau khi phân tích, **ghi dữ liệu vào CRM** (ví dụ: HubSpot, Salesforce) bằng node `n8n-nodes-base.http` để theo dõi đối thủ lâu dài.

5. **Báo Cáo Định Kỳ:**
   - Sử dụng **node `scheduleTrigger`** để chạy workflow **hàng ngày/tháng** và gửi báo cáo tổng hợp.

---
### **📌 Kết Luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn** quá trình theo dõi đối thủ trên LinkedIn, tiết kiệm thời gian và cung cấp **dữ liệu chính xác, cập nhật liên tục**. **Không cần code**, chỉ cần cấu hình vài bước đơn giản.

**🚀 Hành động ngay:**
1. **Đăng ký VPS** để n8n chạy 24/7: [TinoHost](https://tino.vn/vps-n8n?affid=388) (mã giảm **VPSN8N**).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và **nhận báo cáo tự động** mỗi tuần!

**Cần hỗ trợ?** Đăng ký [hỗ trợ kỹ thuật n8n](https://n8n.io/community) hoặc liên hệ Airtop qua [đây](https://portal.airtop.ai/support). 💡