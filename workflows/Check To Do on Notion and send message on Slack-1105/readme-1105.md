---
title: "🚀 Tự Động Kiểm Tra Todo Notion & Gửi Thông Báo Slack Mỗi Ngày - Không Cần Code!"
description: "Workflow tự động hóa kiểm tra danh sách Todo trên Notion và gửi thông báo Slack cho bạn mỗi khi có nhiệm vụ mới được gán cho mình. Giúp bạn không bỏ lỡ công việc quan trọng và tối ưu thời gian làm việc."
slug: "tu-dong-hoa-kiem-tra-todo-notion-slack"
tags: [n8n, automation, notion, slack, no-code, productivity]
keywords: [n8n workflow tự động hóa, kiểm tra todo notion, gửi thông báo slack tự động, tự động hóa công việc hàng ngày, n8n cron job]
---

# 🚀 **Tự Động Kiểm Tra Todo Notion & Gửi Thông Báo Slack Mỗi Ngày**

### **Bạn đã bao giờ cảm thấy "bị chôn vùi" dưới núi công việc trên Notion mà không biết cách theo dõi hiệu quả?**
Workflow này sẽ **giải quyết vấn đề đó** bằng cách:
✅ **Kiểm tra tự động** danh sách Todo của bạn trên Notion mỗi ngày (hoặc theo lịch trình bạn thiết lập).
✅ **Gửi thông báo Slack** khi có nhiệm vụ mới được gán cho bạn, giúp bạn **không bỏ lỡ bất kỳ công việc quan trọng nào**.
✅ **Tiết kiệm thời gian** lên đến **30 phút/ngày** so với cách làm thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh phụ thuộc vào phiên bản miễn phí có giới hạn.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao, không lag)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Không bỏ lỡ công việc**: Nhận thông báo Slack ngay khi có Todo mới được gán cho mình.
- **Tối ưu thời gian**: Không cần phải mở Notion thủ công hàng ngày để kiểm tra.
- **Hoạt động liên tục**: Workflow chạy tự động theo lịch trình (cron), kể cả khi bạn **ngủ hoặc đi làm**.
- **Dễ dàng mở rộng**: Có thể kết hợp với **Google Calendar, Trello, hoặc Microsoft Teams** sau này.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Notion** (đã tạo **Database Todo** và chia sẻ cho bot n8n).
2. **API Key Notion**:
   - Tạo tại [Notion API](https://www.notion.so/my-integrations) và lưu vào **Credentials** trong n8n (tên: `notionApi`).
3. **Tài khoản Slack**:
   - Tạo **App Slack** tại [Slack API](https://api.slack.com/apps) và cấp quyền:
     - `chat:write` (để gửi DM).
     - `channels:history` (nếu cần).
   - Lưu **Token OAuth** vào **Credentials** trong n8n (tên: `slackApi`).
4. **Tên người dùng Slack** (để lọc Todo gán cho mình, ví dụ: `@harshil` hoặc `#harshil`).

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/1105](https://n8n.io/workflows/1105) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và **paste** vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **6 node**, nhưng **3 node quan trọng nhất** cần cấu hình kỹ:

##### **A. Node "Get To Dos" (Notion)**
- **Tham số cần thiết**:
  - **Database ID**: Tìm trong URL của Database Todo trên Notion (ví dụ: `https://www.notion.so/workspace/abc123...` → `abc123` là Database ID).
  - **Filter (lọc Todo gán cho mình)**:
    ```json
    {
      "property": "Assigned to",
      "relation": "contains",
      "value": "harshil"  // Thay bằng tên Slack của bạn (không dấu @)
    }
    ```
    - Nếu Todo dùng **tên người khác** (ví dụ: `Harshil` vs `harshil`), **đảm bảo trùng khớp chính xác**.

##### **B. Node "If task assigned to Harshil?" (If)**
- **Điều kiện**: Kiểm tra nếu `Assigned to` **không trống** (nó sẽ tự động lọc Todo gán cho bạn).
- **Lưu ý**: Nếu không có Todo nào, workflow sẽ **bỏ qua** node Slack sau.

##### **C. Node "Create a Direct Message" & "Send a Direct Message" (Slack)**
- **Tham số cần thiết**:
  - **User ID**: Tìm bằng cách gửi `/api/test` vào Slack và copy `id` từ kết quả (hoặc dùng `@harshil` nếu đã cấu hình trước).
  - **Message Format**:
    ```json
    {
      "blocks": [
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "*Todo mới được gán cho bạn!*\n<https://www.notion.so/{{$node["Get To Dos"].json["url"]}}|Xem chi tiết>"
          }
        },
        {
          "type": "divider"
        },
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "*Chi tiết:*\n- **Tiêu đề**: {{$node["Get To Dos"].json["properties"]["Name"]["title"][0]["plain_text"]}}\n- **Mô tả**: {{$node["Get To Dos"].json["properties"]["Description"]["rich_text"][0]["plain_text"]}}"
          }
        }
      ]
    }
    ```
    - **Lưu ý**: Nếu Todo không có mô tả, hãy thay bằng `{{$node["Get To Dos"].json["properties"]["Description"]["rich_text"][0]["plain_text"] || "Không có mô tả"}}`.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chạy **manual test** với một Todo mẫu để kiểm tra kết quả Slack.
   - **Kiểm tra**:
     - Thông báo có xuất hiện không?
     - Link Notion có hoạt động không?
     - Nội dung có chính xác không?

2. **Bật Active**:
   - Sau khi test thành công, **bật Active** và chọn **Cron** (ví dụ: `0 8 * * *` để chạy lúc 8h sáng hàng ngày).

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Google Calendar**:
   - Sử dụng node **Google Calendar** để **lọc Todo gán cho ngày hôm nay** và gửi thông báo vào buổi sáng.

2. **Lưu log vào Notion**:
   - Thêm node **Notion (Update Block)** để ghi lại **lịch sử thông báo** đã được gửi.

3. **Gửi báo cáo tuần/Tháng**:
   - Sử dụng **Cron khác** (ví dụ: `0 0 * * 0` để chạy Chủ Nhật) và gửi **tóm tắt công việc đã hoàn thành** qua Slack.

4. **Dùng với Trello/Zapier**:
   - Nếu Todo trên **Trello**, thay node Notion bằng **Trello API** và cấu hình tương tự.

---

### 📌 **Kết luận**
Workflow này **giải phóng bạn khỏi việc phải kiểm tra Todo thủ công hàng ngày**, giúp bạn **tập trung vào công việc quan trọng** mà không lo bỏ lỡ nhiệm vụ. **Chỉ cần import, cấu hình và bật Active** – n8n sẽ làm tất cả!

👉 **Hãy thử ngay và chia sẻ kết quả với chúng tôi!** 🚀
#n8n #Automation #Productivity #Slack #Notion