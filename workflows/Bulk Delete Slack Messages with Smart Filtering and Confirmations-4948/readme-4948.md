---
title: "🔥 **Xóa Nhiều Tin Nhắn Slack Tự Động Với Lọc Thông Minh & Xác Nhận (N8n) - Giúp Quản Lý Dữ Liệu Trơn Truyền**"
description: "Workflow này tự động xóa hàng loạt tin nhắn Slack theo tiêu chí lọc thông minh, yêu cầu xác nhận trước khi thực hiện và báo cáo chi tiết - tiết kiệm thời gian quản lý kênh Slack lên đến 80%. Phù hợp cho các team có lượng tin nhắn dư thừa hoặc cần duy trì vệ sinh kênh."
slug: "xoa-nhieu-tin-nhan-slack-tu-dong-voi-loc-thong-minh"
tags: [n8n, slack-automation, xoa-tin-nhan, no-code, itops, workflow-slack]
keywords: [xóa tin nhắn Slack tự động, tự động hóa Slack, n8n workflow Slack, lọc tin nhắn Slack, xác nhận trước khi xóa tin nhắn]
---

# 🚀 **Xóa Nhiều Tin Nhắn Slack Tự Động Với Lọc Thông Minh & Xác Nhận (N8n)**

### **Giải pháp hoàn hảo cho các sếp quản lý kênh Slack bị "đổ chồng" tin nhắn rác, tin nhắn cũ hoặc nội dung không cần thiết**

---

### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian quản lý**: Không cần xóa tin nhắn thủ công hàng ngày (giảm 80% công việc lặp lại).
- **Tránh xóa nhầm**: Yêu cầu xác nhận trước khi xóa bất kỳ tin nhắn nào.
- **Lọc thông minh**: Chỉ xóa tin nhắn phù hợp với tiêu chí (từ khóa, thời gian, tác giả...).
- **Báo cáo chi tiết**: Gửi thông báo tiến trình và kết quả xóa qua Slack.
- **Hoạt động 24/7**: Workflow chạy tự động khi kích hoạt, không cần can thiệp người dùng.
:::

---

### **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Slack Business+ hoặc Enterprise Grid** (các plan cơ bản không hỗ trợ API xóa tin nhắn).
2. **API Token Slack**:
   - Tạo từ [Slack API Tokens](https://api.slack.com/apps) với quyền:
     - `chat:delete` (xóa tin nhắn)
     - `chat:read` (đọc tin nhắn)
     - `groups:history` (lấy lịch sử kênh)
   - Lưu token này trong **Credentials** của n8n (node **Slack**).
3. **Kênh Slack cụ thể** để xóa tin nhắn (điền vào node **Get Channel Messages**).
4. **Mã lệnh kích hoạt**: Ví dụ: `!cleanslack <từ khóa> <thời gian>` (cấu hình trong node **Parse Command**).
5. **VPS n8n** (self-hosted) để workflow chạy liên tục:
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/4948](https://n8n.io/workflows/4948) (ấn nút **Export**).
- **Cách 1**: Trên trang **n8n Editor**, chọn **Import** → Chọn file JSON vừa tải.
- **Cách 2**: Copy toàn bộ JSON từ file → Dán vào **Import Workflow** (nút **Import** ở góc trên bên phải).

#### **2. Các lưu ý BẮT BUỘC phải chỉnh 📌**
Workflow này **phức tạp** vì có nhiều node xử lý logic. Dưới đây là các bước **cần thiết** để cấu hình:

##### **A. Cấu hình node Slack (API Token & Kênh)**
- Mở node **Get Channel Messages** và **Delete Message**:
  - **Credentials**: Chọn hoặc tạo mới **Slack API Token** (đã lưu trước ở bước chuẩn bị).
  - **Channel ID**: Nhập ID kênh Slack muốn xóa tin nhắn (tìm bằng cách mở kênh → URL chứa `C1234567890`).
  - **Limit**: Đặt giá trị cao (ví dụ: `1000`) để lấy nhiều tin nhắn.

##### **B. Cấu hình lệnh kích hoạt (Parse Command)**
- Mở node **Parse Command**:
  - Thay đổi mã JavaScript để phù hợp với lệnh của các sếp. Ví dụ:
    ```javascript
    // Lệnh: !cleanslack <từ khóa> <thời gian> (ví dụ: !cleanslack "temp" "1d")
    const command = $input.all().command.trim().toLowerCase();
    const searchTerm = $input.all().searchTerm || "";
    const timeRange = $input.all().timeRange || "1d"; // Mặc định 1 ngày
    return {
      command,
      searchTerm,
      timeRange
    };
    ```
  - **Lưu ý**: Cần chỉnh node **Check if Valid Command** để kiểm tra lệnh hợp lệ.

##### **C. Cấu hình lọc tin nhắn (Filter Messages by Search Term)**
- Mở node **Filter Messages by Search Term**:
  - Thay đổi mã JavaScript để lọc tin nhắn theo tiêu chí:
    ```javascript
    // Ví dụ: Lọc tin nhắn chứa "temp" và thời gian < 1 ngày
    const messages = $input.all();
    return messages.filter(msg =>
      msg.text.toLowerCase().includes($input.all().searchTerm.toLowerCase()) &&
      new Date(msg.ts) > new Date(Date.now() - parseTimeRange($input.all().timeRange))
    );
    ```
  - **Hàm `parseTimeRange`**: Cần thêm để chuyển đổi `1d`, `7d` thành milliseconds:
    ```javascript
    function parseTimeRange(range) {
      const units = { d: 86400000, h: 3600000, m: 60000 };
      const [value, unit] = range.match(/(\d+)([dhm])/);
      return value * units[unit];
    }
    ```

##### **D. Xác nhận trước khi xóa (Delete or Cancel?)**
- Node **Delete or Cancel?** sử dụng **Slack Interactive Message** để yêu cầu xác nhận:
  - Cấu hình **payload** trong node **Send Confirmation Message** để tạo modal xác nhận:
    ```json
    {
      "type": "modal",
      "title": {
        "type": "plain_text",
        "text": "Xác nhận xóa tin nhắn"
      },
      "blocks": [
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "Bạn có chắc chắn muốn xóa *<count>* tin nhắn chứa *<searchTerm>*?"
          }
        },
        {
          "type": "actions",
          "elements": [
            {
              "type": "button",
              "text": {
                "type": "plain_text",
                "text": "Xóa"
              },
              "value": "confirm",
              "style": "danger"
            },
            {
              "type": "button",
              "text": {
                "type": "plain_text",
                "text": "Hủy"
              },
              "value": "cancel"
            }
          ]
        }
      ]
    }
    ```
  - **Lưu ý**: Node **Store Pending Deletion** lưu thông tin tin nhắn cần xóa trước khi xác nhận.

##### **E. Xóa tin nhắn với thời gian chờ (Wait Between Deletes)**
- Node **Wait Between Deletes**:
  - Đặt thời gian chờ giữa các lần xóa (ví dụ: `5000` ms = 5 giây) để tránh bị Slack chặn API.
  - Cấu hình trong node **Set**:
    ```json
    {
      "waitTime": 5000
    }
    ```

##### **F. Xóa tin nhắn cũ & thông báo lỗi**
- Các node **Delete Workflow Messages**, **Error Report**, **Delete Error Final** tự động xóa tin nhắn thông báo sau khi hoàn thành.
- **Lưu ý**: Node **Clean Up Workflow Messages** cần cấu hình để xóa tin nhắn tạm thời trong quá trình chạy.

---

#### **3. Kích hoạt ⚡️**
1. **Test run** với dữ liệu mẫu:
   - Gửi lệnh `!cleanslack test 1d` vào kênh Slack (nếu cấu hình webhook).
   - Kiểm tra node **Respond to Webhook** để đảm bảo lệnh được parse đúng.
2. **Bật Active workflow**:
   - Chuyển trạng thái từ **Inactive** sang **Active** trên trang **Workflows** của n8n.

---

### **✍️ Mẹo & gợi ý nâng cao**
:::info[CẤP NHẬT & MỞ RỘNG]
1. **Kết hợp với Google Sheets**:
   - Lưu danh sách tin nhắn đã xóa vào Google Sheets để theo dõi lịch sử.
   - Sử dụng node **Google Sheets** + **Code** để ghi dữ liệu.

2. **Gửi báo cáo định kỳ**:
   - Tạo một workflow riêng để gửi báo cáo tổng hợp hàng tuần qua email (n8n + **Email Node**).

3. **Lọc tin nhắn theo tác giả**:
   - Thêm tiêu chí lọc tin nhắn của một user cụ thể (ví dụ: `user_id: U12345678`).

4. **Tích hợp với Notion**:
   - Ghi tin nhắn xóa vào Notion Database để quản lý triệt để.

5. **Cảnh báo trước khi xóa**:
   - Gửi tin nhắn cảnh báo qua Slack/Email trước 24h nếu có nhiều tin nhắn cần xóa.
   - Sử dụng node **Set** + **Wait** + **Slack Notification**.

6. **Log tất cả hoạt động**:
   - Ghi log vào file hoặc cơ sở dữ liệu (ví dụ: **n8n-nodes-base.database**).
   - Dùng node **Code** để ghi vào file JSON:
     ```javascript
     const fs = require('fs');
     const logData = $input.all();
     fs.appendFileSync('./logs/deletion_logs.json', JSON.stringify(logData) + '\n');
     ```
:::

---

### **📌 Kết luận**
Workflow này là **giải pháp hoàn hảo** để các sếp quản lý kênh Slack một cách **tự động hóa, an toàn và hiệu quả**. Bằng cách kết hợp **lọc thông minh, xác nhận trước khi xóa và báo cáo chi tiết**, nó giúp tiết kiệm thời gian và tránh sai sót khi quản lý tin nhắn.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (đăng ký link trên).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test với dữ liệu mẫu** trước khi áp dụng cho kênh chính.

👉 **Bạn có thể tùy chỉnh thêm tiêu chí lọc hoặc tích hợp với các dịch vụ khác** như Trello, Notion để phù hợp với nhu cầu của team. Hãy chia sẻ kết quả sau khi áp dụng nhé! 🚀

---
**Chú ý**: N8n là công cụ mạnh mẽ nhưng cần **cấu hình cẩn thận** để tránh xóa tin nhắn quan trọng. Luôn **backup kênh Slack** trước khi chạy workflow đầu tiên.