---
title: "🤖 **Tự Động Hóa Email Tóm Tắt Tin Tức AI Hàng Ngày - Không Cần Code!**"
description: "Workflow tự động hóa gửi email tổng hợp tin tức AI hàng ngày từ Google News, xử lý bằng AI OpenRouter, và gửi qua Gmail - tiết kiệm thời gian cho các sếp lên đến 30 phút/ngày. Đảm bảo tin tức được tóm tắt, lọc và cá nhân hóa 100% tự động."
slug: "tieu-dong-hoa-email-tom-tat-tin-tuc-ai-hang-ngay"
tags: [n8n, automation, ai-summarization, google-news, openrouter, gmail, no-code]
keywords: [n8n workflow tự động hóa email, tổng hợp tin tức AI hàng ngày, OpenRouter AI, tự động hóa Google News, gửi email tự động bằng n8n]
---

# 🚀 **Tự Động Hóa Email Tóm Tắt Tin Tức AI Hàng Ngày - Không Cần Code!**

### **Giải Phóng Thời Gian Cho Các Sếp!**
Hàng ngày, các sếp phải mất **30-60 phút** để đọc và tổng hợp tin tức AI từ nhiều nguồn khác nhau, từ đó gửi cho đồng nghiệp hoặc bản thân để cập nhật. **Workflow này tự động hóa toàn bộ quá trình** bằng cách:
- **Lấy dữ liệu** từ Google News với 3 từ khóa chính: *AI, Generative AI + LLM, AI Agents + Automation*.
- **Xử lý bằng AI** (OpenRouter) để lọc, tóm tắt và đánh giá tin tức quan trọng nhất.
- **Gửi email tự động** với thiết kế HTML đẹp mắt, bao gồm:
  - Danh sách 8 tin tức hàng đầu.
  - Tóm tắt 2-3 câu cho mỗi tin.
  - Phân tích *"Why It Matters"* (Tại sao tin tức này quan trọng).
  - Thiết kế gradient header và nút đọc nhanh.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
✅ **Tiết kiệm thời gian**: Không cần đọc hàng trăm tin tức mỗi ngày.
✅ **Tin tức được lọc và tóm tắt**: Chỉ nhận những tin quan trọng nhất.
✅ **Cá nhân hóa hoàn toàn**: Thiết kế email chuyên nghiệp, dễ đọc.
✅ **Hoạt động 24/7**: Khởi động lúc 9h sáng (UTC) và tự động gửi hàng ngày.
✅ **Miễn phí**: Sử dụng mô hình AI **nvidia/nemotron-3-super-120b** (không cần thẻ tín dụng).
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi Bắt Đầu**]
Các sếp cần chuẩn bị:
1. **Tài khoản OpenRouter**:
   - Đăng ký miễn phí tại [openrouter.ai](https://openrouter.ai/).
   - Tạo **API Key** và lưu trữ an toàn.
   - Trong n8n, thêm **Credentials mới** → Chọn *OpenRouter API* → Dán API Key.
2. **Tài khoản Gmail**:
   - Đăng nhập vào n8n và tạo **OAuth2 Credential** cho Gmail.
   - Chọn quyền *Send Email* (không cần quyền đọc thư).
3. **Email nhận**:
   - Điền địa chỉ email của mình (hoặc đồng nghiệp) vào node *Send Email via Gmail*.
:::

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15997](https://n8n.io/workflows/15997) hoặc copy toàn bộ JSON từ trang này.
- Trong **n8n Editor**, nhấp vào **Import Workflow** → Dán JSON → Nhấn *Import*.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **Node 1: Schedule Trigger (9 AM)**
- **Cài đặt**:
  - Chọn *Trigger Interval* → *Days*.
  - Thời gian mặc định là **9:00 AM (UTC)**. Nếu muốn điều chỉnh giờ Việt Nam (7h sáng), chỉnh *Time Zone* thành *Asia/Ho_Chi_Minh*.

##### **Node 2-4: RSS Feed Read (3 Node)**
- **Tên node**:
  - *Artificial Intelligence* (từ khóa: "artificial intelligence").
  - *Gen AI + LLM* (từ khóa: "generative AI + LLM").
  - *AI Agent* (từ khóa: "AI agents + automation tools").
- **Cài đặt**:
  - Để tất cả các tùy chọn mặc định.
  - **Không cần thay đổi URL RSS** (n8n tự động lấy từ Google News).

##### **Node 5: Merge All RSS Feeds**
- **Kết nối**: Gắn tất cả 3 node RSS vào *Merge* (input 0, 1, 2).
- **Lưu ý**: Không cần chỉnh sửa gì cả.

##### **Node 6: Prepare Articles (Code)**
- **Nội dung code**:
  ```javascript
  // Code mặc định đã xử lý tự động:
  // - Lọc trùng lặp.
  // - Lấy tiêu đề, liên kết, ngày, nguồn và tóm tắt.
  // - Giới hạn 15 tin tức duy nhất.
  // - Loại bỏ HTML tags.
  ```
- **Không cần chỉnh sửa** nếu muốn sử dụng logic mặc định.

##### **Node 7: OpenRouter Chat Model**
- **Cài đặt quan trọng**:
  - Chọn *Model*: `nvidia/nemotron-3-super-120b:free`.
  - Chọn *Credential* đã tạo từ OpenRouter.
  - **Kết nối với AI Chain**:
    - Kéo node này **vào purple connector** (connector màu tím) ở dưới node *AI Chain - Select & Summarize* (Node 8).
    - **Không kết nối với green connector** (connector chính).

##### **Node 8: AI Chain - Select & Summarize**
- **Prompt mặc định**:
  ```plaintext
  You are an AI assistant that curates and summarizes the most important news articles.
  For each article, provide:
  1. A 2-3 sentence summary.
  2. A "Why It Matters" insight (1 sentence).
  Select the top 8 articles from the list below.
  ```
- **Không cần chỉnh sửa** nếu muốn sử dụng logic mặc định.

##### **Node 9: Build HTML Email (Code)**
- **Nội dung code**:
  ```javascript
  // Code tự động tạo email HTML với:
  // - Header gradient.
  // - Danh sách tin tức số hóa.
  // - Box "Why It Matters".
  // - Nút đọc nhanh.
  ```
- **Chỉnh sửa nếu cần**:
  - Thay đổi màu gradient trong `background: linear-gradient(...)`.
  - Thêm logo công ty vào `<img>` ở header.

##### **Node 10: Send Email via Gmail**
- **Cài đặt**:
  - Chọn *Credential* Gmail OAuth2 đã tạo.
  - Điền **email nhận** (ví dụ: `sếp@example.com`).
  - **Subject mặc định**: *"Daily AI News Digest - [Ngày tháng]"*.
  - **Body**: Chọn *emailHtml* từ node trước.

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn *Execute Workflow* để kiểm tra email mẫu.
   - Kiểm tra **Gmail** để xem email đã gửi thành công chưa.
2. **Bật Active**:
   - Nhấn *Active* trên node *Schedule Trigger*.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**Tối Ưu Hóa Workflow**]
1. **Thêm Slack/Telegram Notifications**:
   - Kết nối node *Send Email* với *Slack Webhook* hoặc *Telegram Bot* để thông báo khi email được gửi.
2. **Lưu Log Lịch Sử**:
   - Thêm node *Set* hoặc *Google Sheets* để ghi lại lịch sử tin tức đã gửi.
3. **Cập Nhật Từ Khóa**:
   - Thay đổi từ khóa trong node RSS để theo dõi chủ đề mới (ví dụ: "AI in Healthcare").
4. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng node *Schedule Trigger* khác để gửi báo cáo tuần/monthly tổng hợp.
5. **Tích Hợp với Notion/Google Drive**:
   - Thay vì email, lưu tin tức vào Notion hoặc Google Drive với node *Notion* hoặc *Google Drive*.
:::

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào công việc chiến lược hơn. **Không cần kỹ thuật**, chỉ cần:
1. Chuẩn bị **OpenRouter API** và **Gmail OAuth2**.
2. Import và cấu hình theo hướng dẫn.
3. **Bật Active** và nhận email hàng ngày!

**Hành động ngay hôm nay**:
- [Tải workflow từ n8n.io](https://n8n.io/workflows/15997).
- [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) để chạy 24/7 (mã giảm giá: **VPSN8N**).
- **Chia sẻ với đồng nghiệp** để cùng tự động hóa công việc!

---
:::note[**Lưu Ý Cuối Cùng**]
- **Mô hình AI miễn phí** của OpenRouter có giới hạn request. Nếu workflow bị lỗi, kiểm tra lại API Key.
- **Gmail OAuth2** chỉ cho phép gửi email từ tài khoản đã đăng ký. Không sử dụng cho mục đích spam.
- **Thời gian UTC**: Nếu muốn chạy lúc 7h sáng Việt Nam, chỉnh *Time Zone* trong *Schedule Trigger*.
:::

---
**Cảm ơn các sếp đã đọc đến cuối!** 🚀
Nếu có vấn đề, hãy để lại comment bên dưới hoặc liên hệ qua [n8n Community](https://community.n8n.io/).