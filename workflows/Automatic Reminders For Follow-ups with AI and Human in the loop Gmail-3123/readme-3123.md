---
title: "🤖 **Tự Động Hóa Gợi Ý & Đặt Lịch Hẹn Follow-up AI + Con Người (Gmail) - Không Cần Code!**"
description: "Workflow tự động hóa AI + Human-in-the-loop giúp các sếp nhắc nhở và đặt lịch hẹn lại với khách hàng tiềm năng từ lịch sử cuộc họp qua Gmail & Google Calendar, tiết kiệm thời gian lên đến 80% so với làm thủ công."
slug: "tieu-dong-hoa-gop-y-dat-lich-hen-follow-up-ai-gmail"
tags: [n8n, automation, ai-agent, gmail, google-calendar, human-in-the-loop, sales-automation]
keywords: [n8n workflow tự động hóa, tự động hóa follow-up sales, AI đặt lịch hẹn, tự động hóa Gmail Calendar, human-in-the-loop n8n]
---

# 🚀 **Tự Động Hóa Gợi Ý & Đặt Lịch Hẹn Follow-up AI + Con Người (Gmail)**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Bạn đã bao giờ phải:
- **Quên nhắc nhở khách hàng tiềm năng** sau cuộc họp?
- **Tốn thời gian tìm kiếm lịch sử cuộc họp** để quyết định thời điểm tiếp theo?
- **Lo lắng không biết khách hàng có sẵn sàng tiếp tục**?
- **Mất khách hàng** vì không có hệ thống nhắc nhở tự động?

Workflow này **giải quyết tất cả** bằng cách:
✅ **Tự động lấy lịch sử cuộc họp** từ Google Calendar.
✅ **Kiểm tra tương tác qua email** để xác định khách hàng có cần nhắc nhở.
✅ **Sử dụng AI gợi ý thời gian hợp lý** cho cuộc họp tiếp theo.
✅ **Yêu cầu xác nhận từ con người** trước khi đặt lịch (Human-in-the-loop).
✅ **Đặt lịch tự động** nếu được chấp thuận.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm 80% thời gian** so với làm thủ công (không cần tìm kiếm, nhắc nhở, hoặc đặt lịch).
- **Tăng tỷ lệ chuyển đổi** với khách hàng tiềm năng nhờ nhắc nhở kịp thời.
- **Giảm rủi ro mất khách** do quên hoặc không có kế hoạch follow-up.
- **Tự động hóa hoàn toàn** sau khi cấu hình, hoạt động 24/7.
- **Chất lượng cao hơn** nhờ AI phân tích lịch sử cuộc họp để gợi ý thời gian phù hợp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi Bắt Đầu**]
Để workflow này hoạt động, các sếp cần:
1. **Tài khoản Google** (đã kết nối với **Google Calendar** và **Gmail**).
2. **API Key OpenAI** (để sử dụng AI gợi ý thời gian).
3. **Lịch Google Calendar** (cần phải là lịch cá nhân hoặc có quyền quản lý).
4. **Tài khoản email chính** (để gửi nhắc nhở và xác nhận).
5. **n8n Self-hosted** (không dùng phiên bản miễn phí để đảm bảo hoạt động liên tục).
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [đây](https://n8n.io/workflows/3123) (hoặc copy JSON từ trang này).
2. **Mở n8n Editor** trên VPS của mình.
3. **Nhấn "Import"** → Dán JSON vào và chọn **"Import"**.
4. **Chờ workflow tải xong** (có thể mất vài phút).

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [trang workflow](https://n8n.io/workflows/3123).
2. **Tạo workflow mới** trong n8n Editor.
3. **Nhấn "Import"** → Dán JSON và chọn **"Import"**.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này **không hoạt động ngay** sau khi import. Các sếp cần cấu hình **các node quan trọng** sau:

#### **🔹 Node 1: Schedule Trigger (Đặt lịch chạy hàng ngày)**
- **Cấu hình:**
  - **Time:** `09:00 AM` (hoặc thời gian phù hợp với giờ làm việc của bạn).
  - **Time Zone:** Chọn **Asia/Ho Chi Minh** (hoặc khu vực của bạn).
  - **Enable:** Bật để workflow chạy tự động hàng ngày.

#### **🔹 Node 2: Get Past Events (Lấy lịch sử cuộc họp)**
- **Cấu hình:**
  - **Google Calendar Credentials:** Chọn tài khoản Google đã kết nối.
  - **Calendar ID:** Nhập ID của lịch cần lấy (thường là `primary` hoặc ID cụ thể của lịch).
  - **Time Range:** Đặt từ **2-3 ngày trước** (để lấy lịch sử cuộc họp đã kết thúc).

#### **🔹 Node 3: Get Emails Since (Kiểm tra email sau cuộc họp)**
- **Cấu hình:**
  - **Gmail Credentials:** Chọn tài khoản Gmail đã kết nối.
  - **Query:** `after:{{$node["Schedule Trigger"].json()["date"]}}` (để lấy email từ ngày cuộc họp kết thúc).
  - **Label:** Chọn **Inbox** hoặc nhãn phù hợp.

#### **🔹 Node 4: Availability (Kiểm tra sẵn sàng của bạn)**
- **Cấu hình:**
  - **Google Calendar Credentials:** Chọn cùng tài khoản như Node 2.
  - **Calendar ID:** Nhập ID lịch của bạn.
  - **Time Range:** Đặt từ **ngày hôm nay đến 7 ngày sau** (để AI gợi ý thời gian hợp lý).

#### **🔹 Node 5: Model (AI Gợi Ý Thời Gian)**
- **Cấu hình:**
  - **OpenAI API Key:** Nhập API Key từ tài khoản OpenAI.
  - **Model:** Chọn `gpt-4o-mini` (hoặc model khác nếu muốn).
  - **Prompt:** Workflow đã cấu hình sẵn, **không cần chỉnh sửa** (nếu muốn tối ưu, có thể thêm thông tin về khách hàng vào prompt).

#### **🔹 Node 6: Meeting Availability Agent (AI Tìm Thời Gian Hợp Lý)**
- **Cấu hình:**
  - **AI Agent:** Chọn **Meeting Availability Agent** (đã cấu hình sẵn).
  - **Input:** Lấy dữ liệu từ Node **Availability**.
  - **Output:** AI sẽ trả về **danh sách thời gian sẵn sàng** của bạn.

#### **🔹 Node 7: Generate Message (Tạo Nội Dung Email Nhắc Nhở)**
- **Cấu hình:**
  - **Template:** Workflow đã cấu hình sẵn, **không cần chỉnh sửa** (nếu muốn cá nhân hóa, có thể thêm biến `{{$json["customer_name"]}}` vào).
  - **AI Input:** Lấy dữ liệu từ Node **Meeting Availability Agent**.

#### **🔹 Node 8: Send for Human Approval (Yêu Cầu Xác Nhận Từ Con Người)**
- **Cấu hình:**
  - **Gmail Credentials:** Chọn tài khoản Gmail đã kết nối.
  - **To:** Nhập email của bạn (hoặc nhóm quản lý).
  - **Subject:** `Xác nhận đặt lịch follow-up với [Tên Khách Hàng]`.
  - **Body:** Nội dung email đã cấu hình sẵn, **không cần chỉnh sửa** (nếu muốn thêm thông tin, có thể mở rộng ở Node **Generate Message**).

#### **🔹 Node 9: Meeting Booking Agent (Đặt Lịch Nếu Được Chấp Thuận)**
- **Cấu hình:**
  - **AI Agent:** Chọn **Meeting Booking Agent**.
  - **Input:** Lấy dữ liệu từ **Gmail (Send-and-wait-for-approval)**.
  - **Output:** Nếu người dùng **chấp thuận**, AI sẽ đặt lịch trên Google Calendar.

#### **🔹 Node 10: Mark as Seen (Tránh Lặp Lại)**
- **Cấu hình:**
  - **Operation:** Chọn `removeItemsSeenInPreviousExecutions` (để workflow không xử lý lại cuộc họp đã được nhắc nhở).

---

### **3. Kích Hoạt ⚡️**
1. **Test Run (Kiểm Tra Trước Khi Bật)**
   - Nhấn **"Execute Workflow"** để chạy thử với **dữ liệu mẫu**.
   - Kiểm tra:
     - AI có gợi ý thời gian hợp lý không?
     - Email nhắc nhở có được gửi đúng không?
     - Nếu bạn **chấp thuận**, AI có đặt lịch không?

2. **Bật Workflow**
   - Sau khi kiểm tra thành công, **bật "Active"** để workflow chạy tự động hàng ngày.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[**Cách Tối Ưu Workflow**]
1. **Thêm Logs (Lưu Lịch Sử)**
   - Sử dụng **Sticky Note** để ghi lại lịch sử cuộc họp và phản hồi của khách hàng.
   - **Cách làm:** Thêm node **Sticky Note** sau Node **Send for Human Approval** để lưu thông tin.

2. **Kết Nối Với Slack/Telegram**
   - Thay vì chỉ gửi email, có thể **gửi thông báo trên Slack/Telegram** bằng node **Webhook** hoặc **Slack**.
   - **Cách làm:** Thêm node **Webhook** sau Node **Generate Message** và kết nối với Slack/Telegram.

3. **Tự Động Gửi Báo Cáo Hàng Tuần**
   - Sử dụng **Schedule Trigger** khác để gửi **báo cáo tổng hợp** về số lượng cuộc họp đã nhắc nhở và tỷ lệ chuyển đổi.
   - **Cách làm:** Tạo workflow mới với **Google Sheets** hoặc **Email** để tổng hợp dữ liệu.

4. **Cá Nhân Hóa Nội Dung Email**
   - Thay vì sử dụng template mặc định, **tạo prompt AI động** để nội dung email phù hợp với từng khách hàng.
   - **Cách làm:** Sử dụng **Set Node** trước Node **Generate Message** để truyền thêm thông tin về khách hàng (ví dụ: tên, ngành nghề, cuộc họp trước đó).

5. **Sử Dụng AI Khác (Ngoài OpenAI)**
   - Nếu không muốn dùng OpenAI, có thể **thay thế bằng Mistral AI, BARD, hoặc các model khác** bằng cách cấu hình lại **Node `lmChatOpenAi`**.
   - **Cách làm:** Cập nhật **API Key** và **model** trong Node **Model** và **Model1**.

---

## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào việc **quan hệ khách hàng** thay vì làm thủ công. Với **AI gợi ý thời gian** và **Human-in-the-loop**, bạn **không bao giờ quên nhắc nhở** khách hàng tiềm năng và **tránh mất khách** do không có kế hoạch follow-up.

**👉 Hãy áp dụng ngay và tự động hóa sales của mình!**

---
### **🔗 Tài Liệu Tham Khảo**
- [Hướng dẫn Google Calendar Node](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.googlecalendar)
- [Hướng dẫn Gmail Node](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.gmail)
- [AI Agents trong n8n](https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/)
- [Human-in-the-loop trong n8n](https://docs.n8n.io/advanced-ai/examples/human-fallback/)

---
### **💬 Có Thắc Mắc?**
- **Giới thiệu n8n** trên [Discord](https://discord.com/invite/XPKeKXeB7d).
- **Đăng câu hỏi** trên [Forum n8n](https://community.n8n.io/).
- **Mua VPS Self-hosted** để workflow chạy 24/7:
  - 👉 [TinoHost (Mã giảm giá: **VPSN8N**)](https://tino.vn/vps-n8n?affid=388)
  - 👉 [BNIX (Xeon 4GB chỉ 50k/tháng)](https://my.bnix.one/aff.php?aff=172)