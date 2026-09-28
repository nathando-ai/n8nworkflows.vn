---
title: "🚀 Tự Động Thông Báo Thông Tin Thầu IT BOAMP Trên Slack - Không Cần Code!"
description: "Workflow tự động hóa lấy thông tin thầu IT mới từ API BOAMP và gửi ngay lên Slack, giúp các sếp tiết kiệm thời gian theo dõi thị trường và không bỏ lỡ cơ hội nào. Hoạt động 24/7, không cần can thiệp thủ công."
slug: "tieu-dong-thong-bao-thau-boamp-tren-slack"
tags: [n8n, automation, market-research, api-integration, slack-notification, boamp]
keywords: [tự động hóa n8n, thông báo thầu BOAMP, API BOAMP Slack, tự động hóa thị trường IT, workflow n8n không code]
---

# 🚀 **Tự Động Thông Báo Thầu IT BOAMP Trên Slack - Không Cần Code!**

### **Nỗi Đau Của Các Sếp Trong Thị Trường Thầu IT**
Hàng ngày, các sếp và chuyên gia thị trường IT phải dành nhiều giờ để:
- **Quét thủ công** trên trang BOAMP để tìm thông tin thầu mới.
- **So sánh và đánh giá** các cơ hội thầu theo yêu cầu của công ty.
- **Bỏ lỡ cơ hội** vì không theo dõi kịp thời hoặc bị quá tải thông tin.

**Workflow này giải quyết tất cả!** Nó tự động lấy thông tin thầu IT mới từ **API BOAMP** và gửi ngay lên **Slack**, giúp các sếp:
✅ **Tiết kiệm 10+ giờ/tuần** không phải theo dõi thủ công.
✅ **Không bỏ lỡ bất kỳ cơ hội nào** nhờ thông báo tức thời.
✅ **Tập trung vào phân tích** thay vì công việc lặp lại.
✅ **Hoạt động 24/7** mà không cần can thiệp.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và độ tin cậy cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
| **Lợi Ích**               | **Chi Tiết** |
|---------------------------|-------------|
| **Tự động hóa theo dõi thầu** | Workflow chạy tự động mỗi ngày (hoặc theo lịch) để lấy thông tin mới từ BOAMP. |
| **Thông báo tức thời trên Slack** | Mỗi thông tin thầu mới được gửi ngay lên kênh Slack với định dạng rõ ràng. |
| **Tiết kiệm thời gian** | Không cần phải truy cập BOAMP hàng ngày, giảm thiểu công việc lặp lại. |
| **Tính chính xác cao** | Dữ liệu lấy từ API chính thức BOAMP, không bị sai sót như khi copy thủ công. |
| **Hoạt động liên tục** | Chạy 24/7, không phụ thuộc vào giờ làm việc của nhân viên. |

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản BOAMP API**:
   - Đăng ký và lấy **API Key** từ [BOAMP Developer Portal](https://developer.boamp.com/).
   - Xác nhận quyền truy cập vào **API BOAMP** để lấy thông tin thầu IT.

2. **Tài khoản Slack**:
   - Một **Slack Workspace** và **Bot Token** để gửi thông báo.
   - **Channel Slack** để nhận thông tin thầu (ví dụ: `#thau-it`).
   - **Permissions** cho bot để gửi tin nhắn vào channel.

3. **N8n Self-hosted**:
   - Một máy chủ VPS hoặc máy chủ nội bộ để chạy workflow 24/7.
   - **N8n Core** đã cài đặt và hoạt động (cập nhật phiên bản mới nhất).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13764](https://n8n.io/workflows/13764).
- **Mở n8n Editor** và chọn **Import Workflow** → Chọn file JSON đã tải.
- **Hoặc copy/paste JSON** từ file vào n8n Editor (đảm bảo không có lỗi cú pháp).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này sử dụng các **node chính** sau. Các sếp cần cấu hình kỹ lưỡng:

##### **A. Node `Schedule Trigger` (n8n-nodes-base.scheduleTrigger)**
- **Chọn lịch chạy**:
  - **Daily** (mỗi ngày) hoặc **Custom** (ví dụ: 8h sáng để bắt đầu ngày mới).
  - **Timezone**: Đặt theo giờ của công ty (ví dụ: `Asia/Ho_Chi_Minh`).

##### **B. Node `HTTP Request` (n8n-nodes-base.httpRequest)**
- **Endpoint API BOAMP**:
  - **Method**: `GET`
  - **URL**: `https://api.boamp.com/v1/tenders` (hoặc endpoint cụ thể cho thầu IT).
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_BOAMP_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Query Parameters** (nếu cần):
    ```json
    {
      "status": "open",
      "sector": "IT",
      "country": "VN"
    }
    ```
  - **Lưu ý**:
    - Thay thế `YOUR_BOAMP_API_KEY` bằng API Key thực tế từ BOAMP.
    - Nếu API yêu cầu **pagination**, cấu hình `page` và `limit` trong query.

##### **C. Node `Code` (n8n-nodes-base.code)**
- **Lọc và xử lý dữ liệu**:
  - Workflow sử dụng **JavaScript** để lọc thông tin thầu mới (so sánh với lần chạy trước).
  - **Cấu hình**:
    ```javascript
    // Ví dụ: Lọc thầu mới (cập nhật logic theo yêu cầu)
    const previousTenders = $input.all().filter(item => item.status === "previous");
    const newTenders = $input.all().filter(item => item.status === "new");

    return {
      json: {
        newTenders: newTenders
      }
    };
    ```
  - **Lưu ý**:
    - Sửa đổi logic để phù hợp với cách BOAMP trả về dữ liệu (ví dụ: trường `id`, `title`, `deadline`).

##### **D. Node `Slack` (n8n-nodes-base.slack)**
- **Cấu hình bot Slack**:
  - **Token**: Điền **Bot Token** từ Slack (tìm trong **Apps & Bot** → **Basic Information**).
  - **Channel**: Chọn **Channel ID** của kênh muốn gửi thông báo (ví dụ: `#thau-it`).
  - **Message Format**:
    ```json
    {
      "text": "🚨 Thầu IT mới trên BOAMP: {{ $node["HTTP Request"].json["title"] }}",
      "attachments": [
        {
          "title": "{{ $node["HTTP Request"].json["title"] }}",
          "title_link": "{{ $node["HTTP Request"].json["link"] }}",
          "text": `📅 Hạn chót: {{ $node["HTTP Request"].json["deadline"] }}\n💰 Ngân sách: {{ $node["HTTP Request"].json["budget"] }}`,
          "color": "#36a64f"
        }
      ]
    }
    ```
  - **Lưu ý**:
    - Thay thế `{{ $node["HTTP Request"].json["..."] }}` bằng các trường thực tế từ API BOAMP.
    - Sử dụng **emoji** và **format đẹp** để thông báo dễ đọc.

##### **E. Node `Sticky Note` (n8n-nodes-base.stickyNote)**
- **Ghi chú cho debug**:
  - Dùng để lưu **dữ liệu mẫu** hoặc **lỗi** khi test.
  - **Lưu ý**: Xóa node này sau khi debug xong để workflow nhẹ hơn.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chạy **Manual Trigger** để kiểm tra workflow với dữ liệu mẫu.
   - Kiểm tra **Slack** để xem thông báo có đúng định dạng không.
   - **Sửa lỗi** nếu có (ví dụ: API Key sai, format Slack không đúng).

2. **Bật Active**:
   - Sau khi test thành công, **bật Active** cho workflow.
   - **Monitor** qua **n8n Dashboard** để đảm bảo không có lỗi.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự động lưu log**:
   - Thêm node **`Google Sheets`** hoặc **`Database`** để lưu lịch sử thầu đã nhận.
   - **Cách làm**:
     - Sử dụng node `HTTP Request` để gửi dữ liệu vào Google Sheets.
     - Cấu hình **Sheet Name** và **Range** trong node `Google Sheets`.

2. **Gửi báo cáo định kỳ**:
   - Tạo một **workflow phụ** để tổng hợp và gửi **báo cáo tuần/month** về thầu IT.
   - **Dùng node `Schedule Trigger`** để chạy hàng tuần và gửi qua **Email** hoặc **Slack**.

3. **Kết hợp với LLM (AI Chatbot)**:
   - Sử dụng **node `LLM`** (n8n-nodes-base.llm) để **tóm tắt** thông tin thầu và gửi qua Slack.
   - **Prompt ví dụ**:
     ```
     Tóm tắt thông tin thầu này trong 3 dòng và đánh giá mức độ phù hợp với công ty.
     ```

4. **Bộ lọc thông tin thầu**:
   - Thêm **node `Code`** để lọc thầu theo **ngân sách**, **ngành nghề**, hoặc **địa điểm**.
   - **Ví dụ**:
     ```javascript
     const filteredTenders = $input.all().filter(item =>
       item.budget > 100000000 && item.sector === "IT"
     );
     return { json: { filteredTenders } };
     ```

5. **Thông báo qua Email**:
   - Thêm node **`Email`** (n8n-nodes-base.email) để gửi thông báo cho team.
   - **Cấu hình**:
     - **SMTP Server** (ví dụ: Gmail, SendGrid).
     - **Subject**: `🚨 Thầu IT mới: {{ title }}`.
     - **Body**: Nội dung HTML với link và thông tin chi tiết.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp lại, giúp họ **tập trung vào chiến lược** thay vì theo dõi thị trường thủ công. Với **n8n**, bạn không cần biết code để tự động hóa quy trình này - chỉ cần **import, cấu hình và bật chạy**!

**Hành động ngay hôm nay**:
1. **Đăng ký VPS** để self-host n8n (nếu chưa có).
2. **Import workflow** và cấu hình API/Slack.
3. **Bật Active** và bắt đầu nhận thông báo thầu IT mỗi ngày!

**Cần hỗ trợ?** Để lại comment bên dưới hoặc liên hệ với cộng đồng n8n trên [Discord](https://n8n.io/discord). 🚀

---
**#TựĐộngHóa #N8nVietnam #ThầuIT #BOAMP #SlackAutomation**