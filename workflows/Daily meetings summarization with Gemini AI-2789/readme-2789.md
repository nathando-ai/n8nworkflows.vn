---
title: "🤖 Tự Động Hóa Tóm Tắt Cuộc Họp Hàng Ngày Với Gemini AI - Tiết Kiệm 5+ Giờ/Tuần Cho Các Sếp"
description: "Workflow tự động hóa tóm tắt tất cả cuộc họp hàng ngày từ Google Calendar và gửi kết quả qua Slack với Gemini AI - không cần code, hoạt động 24/7. Giúp các sếp nắm bắt được nội dung chính, hành động cần thực hiện và quyết định nhanh chóng mà không phải đọc lại hàng chục cuộc họp."
slug: "tomo-tat-cuoc-hop-hang-ngay-voi-gemini-ai"
tags: [n8n, automation, ai, google-calendar, slack, gemini-ai, no-code]
keywords: [tự động hóa cuộc họp, tóm tắt cuộc họp hàng ngày, gemini ai n8n, tự động hóa slack, tự động hóa google calendar, tiết kiệm thời gian quản lý cuộc họp]
---

# 🚀 **Tự Động Hóa Tóm Tắt Cuộc Họp Hàng Ngày Với Gemini AI - Không Cần Code**

### **Nỗi Đau Của Các Sếp Hàng Ngày**
Các sếp thường phải mất **từ 30 phút đến 1 giờ mỗi ngày** để:
- **Lọc và đọc lại** hàng chục cuộc họp trong Google Calendar.
- **Tóm tắt nội dung** và nhớ các hành động cần thực hiện.
- **Gửi báo cáo** cho đồng nghiệp hoặc bản thân sau khi làm việc.
- **Lo lắng bỏ sót** thông tin quan trọng khi quá tải công việc.

Kết quả? **Thời gian quý giá bị "chôn vùi" trong công việc thủ công**, còn quyết định quan trọng lại bị trì hoãn vì thiếu thông tin đầy đủ.

---
### **🎯 Giải Pháp: Workflow Tự Động Hóa Tóm Tắt Cuộc Họp Với Gemini AI**
Workflow này **tự động**:
✅ **Lấy tất cả cuộc họp** từ Google Calendar (không giới hạn ngày).
✅ **Gửi dữ liệu** vào **Gemini AI** (Google’s latest LLM) để tóm tắt **nhanh chóng và chính xác**.
✅ **Gửi kết quả** về Slack với **cấu trúc rõ ràng**:
   - **Nội dung chính** của cuộc họp.
   - **Hành động cần thực hiện** (to-do list).
   - **Thời gian và người tham gia**.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

**Kết quả?** Các sếp **tiết kiệm 5+ giờ/tuần**, **nắm bắt thông tin nhanh chóng** và **quản lý công việc hiệu quả hơn**.

---
### **🎯 Kết quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải đọc lại cuộc họp thủ công.
- **Tóm tắt chính xác**: Gemini AI hiểu ngữ cảnh và tóm tắt **như một người tham gia cuộc họp**.
- **Cấu trúc rõ ràng**: Kết quả được chia thành **nội dung, hành động, và người liên quan**.
- **Hoạt động liên tục**: Workflow chạy tự động **mỗi ngày** (hoặc theo lịch bạn thiết lập).
- **Tích hợp Slack**: Nhận báo cáo ngay trên kênh công việc, không phải mở nhiều tab.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Calendar** (đã cấp quyền cho n8n).
2. **Tài khoản Slack** (đã tạo **API Token** và chọn kênh cần gửi báo cáo).
3. **API Key Google Gemini** (đăng ký tại [Google AI Studio](https://aistudio.google.com/)).
4. **n8n Self-hosted** (không dùng phiên bản cloud để đảm bảo dữ liệu an toàn).
:::

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/2789](https://n8n.io/workflows/2789) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ trang trên và **paste** vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **5 node chính**, các sếp cần cấu hình kỹ lưỡng:

##### **🔹 Node 1: Schedule Trigger (Động cơ kích hoạt hàng ngày)**
- **Cấu hình**:
  - Chọn **Daily** (hàng ngày).
  - Thời gian chạy: **Sáng sớm (ví dụ 7h sáng)** để có thời gian xử lý trước khi bắt đầu công việc.
  - **Lưu ý**: Nếu muốn chạy vào giờ khác, chỉnh **timezone** phù hợp (ví dụ: `Asia/Ho_Chi_Minh` cho Việt Nam).

##### **🔹 Node 2: Google Calendar - Get Events (Lấy tất cả cuộc họp)**
- **Cấu hình**:
  - **Credentials**: Chọn `googleCalendarOAuth2Api` (đã cấu hình trước khi import).
  - **Operation**: Đảm bảo chọn `getAll` (lấy tất cả cuộc họp trong ngày).
  - **Lưu ý**:
    - Nếu muốn **lọc cuộc họp trong một khoảng thời gian cụ thể**, thêm **filter** như:
      ```json
      {
        "startTime": "2024-01-01T00:00:00Z",
        "endTime": "2024-01-01T23:59:59Z"
      }
      ```
    - **Không bỏ qua** bước **authorize** trong n8n để kết nối với Google Calendar.

##### **🔹 Node 3: Google Gemini Chat Model (Gọi API Gemini AI)**
- **Cấu hình**:
  - **Credentials**: Chọn `googlePalmApi` (đã điền `API Key` từ Google AI Studio).
  - **Prompt mẫu** (cần chỉnh sửa để phù hợp):
    ```json
    "Tóm tắt cuộc họp {meetingName} diễn ra vào {startTime} với nội dung chính:
    - Thời gian: {startTime} đến {endTime}
    - Người tham gia: {attendees}
    - Nội dung:
    {description}
    Hãy tóm tắt ngắn gọn (max 300 từ) và liệt kê các hành động cần thực hiện (to-do list)."
    ```
  - **Lưu ý**:
    - **Không bỏ trống** `description` trong cuộc họp (nếu cuộc họp không có mô tả, Gemini sẽ không tóm tắt được).
    - **Test prompt** trước khi chạy toàn bộ workflow để đảm bảo kết quả chính xác.

##### **🔹 Node 4: Calendar AI Agent (Agent xử lý AI)**
- **Cấu hình**:
  - **Memory**: Đặt thành `None` (do workflow chỉ chạy **1 lần duy nhất** cho mỗi cuộc họp).
  - **Lưu ý**: Nếu muốn lưu lịch sử, có thể cấu hình **memory** sau này.

##### **🔹 Node 5: Send Response Back to Slack Channel (Gửi kết quả về Slack)**
- **Cấu hình**:
  - **Credentials**: Chọn `slackApi` (đã cấu hình trước).
  - **Channel**: Chọn kênh Slack cần gửi báo cáo (ví dụ: `#meeting-summary`).
  - **Message Format**: Sử dụng **template** để định dạng kết quả:
    ```json
    {
      "text": "📅 **Tóm tắt cuộc họp {meetingName}**",
      "attachments": [
        {
          "title": "📝 Nội dung chính",
          "text": "{summary}",
          "color": "#36a64f"
        },
        {
          "title": "📋 Hành động cần thực hiện",
          "text": "{actions}",
          "color": "#f6c23e"
        }
      ]
    }
    ```
  - **Lưu ý**:
    - **Kiểm tra lại kênh Slack** để đảm bảo không gửi vào kênh nhạy cảm.
    - **Test run** trước khi bật workflow để xem kết quả trên Slack.

#### **3. Kích Hoạt ⚡️**
- **Bước 1**: **Test Run** với **1 cuộc họp mẫu** để kiểm tra:
  - Dữ liệu từ Google Calendar có lấy được không?
  - Gemini AI có tóm tắt chính xác không?
  - Slack có nhận được báo cáo không?
- **Bước 2**: Nếu test thành công, **bật Active** workflow.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC TỐC ĐỘNG MỞ RỘNG]
1. **Gửi báo cáo qua Email** (thay vì Slack):
   - Thêm **node `n8n-nodes-base.email`** sau node Slack.
   - Cấu hình gửi cho **các sếp cụ thể** hoặc nhóm.

2. **Lưu log vào Google Sheets/Notion**:
   - Thêm **node `n8n-nodes-base.googleSheets`** hoặc `n8n-nodes-base.notion` để lưu lịch sử tóm tắt.
   - **Ưu điểm**: Dễ dàng **tra cứu lại** cuộc họp cũ.

3. **Kết hợp với Microsoft Teams**:
   - Sử dụng **node `n8n-nodes-base.microsoftTeams`** để gửi báo cáo vào Teams thay vì Slack.

4. **Tùy chỉnh prompt cho từng loại cuộc họp**:
   - Ví dụ:
     - Cuộc họp **kinh doanh**: Yêu cầu Gemini **tóm tắt số liệu và KPI**.
     - Cuộc họp **phát triển**: Yêu cầu **liệt kê các task kỹ thuật** cần thực hiện.

5. **Chạy workflow vào giờ khác**:
   - Nếu các sếp muốn **tóm tắt buổi tối**, chỉnh **Schedule Trigger** vào **18h-19h**.

6. **Dùng AI để phân loại cuộc họp**:
   - Thêm **node `n8n-nodes-base.if`** để:
     - **Cuộc họp quan trọng** → Gửi qua Slack + Email.
     - **Cuộc họp thường xuyên** → Gửi qua kênh riêng.
:::

---
### **📌 Kết Luận**
Workflow **Tự Động Hóa Tóm Tắt Cuộc Họp Hàng Ngày Với Gemini AI** là **giải pháp hoàn hảo** cho các sếp:
✔ **Không cần code**.
✔ **Hoạt động 24/7** mà không tốn thời gian.
✔ **Tóm tắt chính xác** nhờ Gemini AI.
✔ **Tiết kiệm thời gian** để tập trung vào công việc chiến lược.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n Self-hosted** (để đảm bảo dữ liệu an toàn).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test run** và **bật workflow** để bắt đầu tiết kiệm thời gian!

---
:::note[💡 CHÚ Ý CUỐI CÙNG]
- **Nếu gặp lỗi API Google Gemini**, kiểm tra lại **API Key** và **quota** (Google AI có giới hạn sử dụng).
- **Nếu muốn nâng cấp**, có thể thử **Gemini Pro** thay vì Flash để tóm tắt chi tiết hơn.
- **N8n Self-hosted** giúp **an toàn dữ liệu** hơn phiên bản cloud.
:::

---
**🚀 CÓ THỂ THỬ N8N TRÊN VPS MIỄN PHÍ?**
:::info[🔥 ĐĂNG KÝ VPS CHO N8N]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow AI)
:::

---
**BẠN CÓ THẮC MẮC GÌ?**
Hãy để lại **comment** bên dưới hoặc liên hệ **Johnny Rafael** (tác giả workflow) qua [n8n Community](https://community.n8n.io/) để được hỗ trợ! 🚀