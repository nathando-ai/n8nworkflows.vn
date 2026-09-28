---
title: "📊 Tự Động Hóa Báo Cáo Tiến Độ Công Việc Tuần Kêephub Sang Slack - Giảm 100% Công Việc Lặp Lại"
description: "Workflow tự động hóa lấy dữ liệu tiến độ công việc từ Keephub trong tuần qua, tổng hợp và gửi báo cáo định kỳ sang Slack hàng tuần - tiết kiệm 5+ giờ công mỗi tháng cho các sếp quản lý dự án."
slug: "tu-dong-hoa-bao-cao-keehub-slack"
tags: [n8n, automation, project-management, keehub, slack, no-code]
keywords: [tự động hóa n8n, báo cáo tiến độ công việc, keehub slack integration, tự động hóa quản lý dự án, workflow hàng tuần]
---

# 🚀 **Tự Động Hóa Báo Cáo Tiến Độ Công Việc Tuần Kêephub Sang Slack - Không Cần Code**

Hàng tuần, các sếp quản lý dự án phải mất **30-60 phút** để tổng hợp tiến độ công việc từ Keephub, chỉnh sửa thành báo cáo, và gửi qua Slack cho đội nhóm. **Công việc lặp lại này không chỉ tốn thời gian mà còn dễ xảy ra lỗi do con người**. Với workflow này, các sếp sẽ **tự động hóa 100% quá trình**, nhận báo cáo chính xác, định kỳ hàng tuần vào **9h sáng thứ Hai**, và có thời gian tập trung vào việc **quản lý chiến lược** thay vì công việc thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5+ giờ công mỗi tháng**: Không còn phải tổng hợp báo cáo thủ công.
- **Dữ liệu chính xác 100%**: Tránh sai sót do con người trong quá trình nhập liệu.
- **Báo cáo cá nhân hóa**: Thêm logo, thông tin chi tiết theo yêu cầu của đội nhóm.
- **Hoạt động tự động**: Báo cáo được gửi hàng tuần vào **9h sáng thứ Hai**, không phụ thuộc vào thời gian làm việc của ai.
- **Dễ dàng mở rộng**: Chỉ cần thay đổi một vài tham số là có thể chuyển sang báo cáo **tháng** hoặc gửi sang **Telegram/Email**.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Keephub**:
   - **API Key Login** (để lấy danh sách công việc).
   - **API Key Bearer** (để lấy tiến độ công việc).
   - **Orgunit ID** (ID của đơn vị tổ chức cần theo dõi).
2. **Tài khoản Slack**:
   - **Bot Token** (để gửi tin nhắn vào channel).
   - **Channel ID** (địa chỉ của channel muốn nhận báo cáo).
3. **n8n Workflow Editor**:
   - Các sếp có thể **self-host** n8n trên VPS hoặc sử dụng phiên bản **n8n.cloud** (miễn phí cho 1000 execution/month).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow theo **2 cách**:
- **Tải file JSON** từ [n8n.io/workflows/13533](https://n8n.io/workflows/13533) và import vào **n8n Editor**.
- **Copy JSON** từ trang trên và **paste** vào **Import Workflow** trong n8n.

:::note[Lưu ý]
Nếu sử dụng phiên bản **n8n.cloud**, các sếp cần cài đặt **n8n-nodes-keephub** trước bằng cách:
1. Vào **Settings** → **Manage installed nodes**.
2. Tìm và cài đặt **Keephub** node.
:::

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **10 node**, các sếp cần chú ý cấu hình **các node sau**:

##### **A. Cấu hình Keephub**
1. **Node "Get Tasks by Orgunit"**:
   - **Credentials**: Chọn `keephubLoginApi` (đã thêm trước đó).
   - **Orgunit ID**: Thay thế `orgunitId` bằng **ID của đơn vị tổ chức** trong Keephub (có thể tìm trong URL của đơn vị đó).
   - **Example**: Nếu URL của đơn vị là `https://app.keehub.com/orgunits/12345`, thì `orgunitId = 12345`.

2. **Node "Get Progress"**:
   - **Credentials**: Chọn `keephubBearerApi`.
   - **Không cần thay đổi** các tham số khác, workflow sẽ tự động lấy tiến độ từ các task đã được lấy ở node trước.

##### **B. Cấu hình Slack**
1. **Node "Send a message"**:
   - **Credentials**: Thêm **Slack Bot Token** (tạo từ [Slack API](https://api.slack.com/apps)).
   - **Channel**: Chọn **channel** muốn nhận báo cáo (ví dụ: `#daily-update`).
   - **Message Format**: Workflow đã định dạng sẵn, các sếp có thể chỉnh sửa **template** trong node **"Format for Message"** (node Code) nếu muốn thay đổi nội dung.

##### **C. Cấu hình lịch trình**
- **Node "Every Monday 9am"**: Đã cấu hình sẵn để chạy **tự động hàng tuần vào 9h sáng thứ Hai**.
- **Node "Last Week Start" & "Last Week End"**: Đã tính toán sẵn để lấy dữ liệu từ **thứ Hai đến Chủ Nhật tuần trước**.

##### **D. Node Code (Format for Message)**
- Workflow sử dụng **JavaScript** để định dạng tin nhắn Slack.
- Các sếp có thể **chỉnh sửa** nội dung báo cáo bằng cách mở node **"Format for Message"** và thay đổi **template** trong phần `JSON`:
  ```json
  {
    "blocks": [
      {
        "type": "header",
        "text": { "type": "plain_text", "text": "📊 BÁO CÁO TIẾN ĐỘ CÔNG VIỆC TUẦN ${weekStart} - ${weekEnd}", "emoji": true }
      },
      {
        "type": "section",
        "text": { "type": "mrkdwn", "text": "*Tổng số công việc:* ${totalTasks}" }
      },
      {
        "type": "divider"
      },
      {
        "type": "section",
        "text": { "type": "mrkdwn", "text": "📌 DANH SÁCH CÔNG VIỆC:" }
      },
      // Thêm danh sách task vào đây (workflow tự động sinh)
    ]
  }
  ```

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chọn **node "Or Manually Run"** và nhấn **Execute Workflow** để kiểm tra.
   - Kiểm tra **Slack** xem báo cáo có được gửi đúng không.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật Active** cho node **"Every Monday 9am"**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Logo & Thông Tin Công Ty**:
   - Trong node **"Format for Message"**, các sếp có thể thêm **logo** và **thông tin công ty** vào header:
     ```json
     {
       "type": "image",
       "image_url": "https://example.com/logo.png",
       "alt_text": "Logo Công Ty"
     }
     ```

2. **Gửi Báo Cáo Sang Email**:
   - Thay thế node **Slack** bằng **node Email** (n8n-nodes-base.email) để gửi báo cáo qua email định kỳ.

3. **Lưu Log Lịch Sử**:
   - Thêm **node Database** (n8n-nodes-base.database) để lưu lịch sử báo cáo vào **Google Sheets** hoặc **Airtable**.

4. **Báo Cáo Tháng**:
   - Thay đổi **node "Every Monday 9am"** thành **"Every First Day of Month 9am"** và điều chỉnh **dateTime** để lấy dữ liệu **30 ngày trước**.

5. **Kết hợp với Trello/Notion**:
   - Sử dụng **node Trello** hoặc **Notion** để cập nhật tiến độ công việc từ Keephub vào các công cụ quản lý khác.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp quản lý dự án, giúp họ **tập trung vào việc chiến lược** thay vì công việc thủ công. **Chỉ cần 10 phút setup**, các sếp sẽ nhận được **báo cáo tự động hàng tuần**, chính xác và chuyên nghiệp.

**Hành động ngay hôm nay**:
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test run** để đảm bảo báo cáo được gửi đúng.
3. **Bật tự động** và **quên đi công việc lặp lại này**!

👉 [Tải workflow JSON](https://n8n.io/workflows/13533) và bắt đầu tự động hóa ngay!