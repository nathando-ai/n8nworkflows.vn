---
title: "🎥 Tự Động Kiểm Tra Trạng Thái Tạo Video KIE.ai & Gửi Kết Quả qua Telegram (N8n)"
description: "Workflow tự động hóa 100% không code để theo dõi tiến trình tạo video từ KIE.ai, tải xuống và chia sẻ kết quả qua Telegram với chất lượng 1080p. Giúp các sếp tiết kiệm thời gian và tối ưu hóa quy trình content creation."
slug: "tieu-dong-kiem-tra-trang-thai-tao-video-kie-ai-telegram"
tags: [n8n, automation, content-creation, multimodal-ai, telegram-bot, s3-storage, redis-cache]
keywords: [tự động hóa tạo video, kiểm tra trạng thái KIE.ai, chia sẻ video Telegram, n8n workflow, tự động hóa không code]
---

# 🚀 **Tự Động Kiểm Tra Trạng Thái Tạo Video KIE.ai & Gửi Kết Quả qua Telegram**

### **Giải pháp cho các sếp bị "đợi video" suốt ngày**
Hãy tưởng tượng một tình huống: Bạn gửi yêu cầu tạo video từ KIE.ai (một trong những công cụ AI tiên tiến nhất hiện nay) để sử dụng trong marketing, nhưng phải chờ **tối thiểu 15 phút** để biết kết quả. Trong thời gian đó, bạn phải liên tục refresh trang web hoặc gọi API để kiểm tra trạng thái. **Thời gian quý giá của bạn bị lãng phí!**

Workflow này **tự động hóa toàn bộ quy trình**:
✅ **Theo dõi trạng thái tạo video** (Veo 3.1, Sora 2, Seedance) mỗi **60 giây** cho đến khi hoàn thành.
✅ **Tải xuống video chất lượng 1080p** và lưu trữ an toàn trên **S3**.
✅ **Gửi kết quả qua Telegram** với **button publish** để chia sẻ nhanh chóng.
✅ **Xử lý lỗi và thời gian chờ** (thay vì bỏ qua, workflow sẽ thông báo nếu quá thời gian chờ).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải refresh hoặc gọi API thủ công.
- **Chất lượng 1080p**: Video luôn được tải xuống với độ phân giải cao nhất.
- **Tự động hóa hoàn chỉnh**: Từ kiểm tra trạng thái đến chia sẻ kết quả.
- **Dữ liệu an toàn**: Video được lưu trên **S3** và metadata được quản lý bằng **Redis**.
- **Tích hợp Telegram**: Kết quả được gửi ngay khi hoàn thành (hoặc báo lỗi nếu quá thời gian chờ).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **API Key KIE.ai** (để gọi API kiểm tra trạng thái).
2. **Credentials S3** (để lưu trữ video và metadata).
3. **Credentials Redis** (để lưu trữ session và trạng thái).
4. **Telegram Bot Token** (để gửi video preview).
5. **Webhook URL** (để "Retry Poll" gọi lại nếu video chưa hoàn thành).

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/12684](https://n8n.io/workflows/12684) hoặc copy/paste JSON vào **n8n Editor**.
- **Chọn "Import"** và chọn file JSON đã tải.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **27 node**, nhưng các bước **quan trọng nhất** cần điều chỉnh:

##### **A. Cấu hình Webhook Trigger**
- Node: **"Poll Trigger"** (Webhook)
  - **Path**: `video-poll` (không cần thay đổi).
  - **HTTP Method**: `POST` (để nhận yêu cầu từ workflow chính).

##### **B. Thiết lập KIE.ai API**
- Node: **"Check KIE Status"** (HTTP Request)
  - **Credentials**: Chọn `httpHeaderAuth` (đã cấu hình API Key KIE.ai).
  - **URL**: Đảm bảo trỏ đến API chính xác của KIE.ai (ví dụ: `https://api.kie.ai/v1/tasks/{taskId}`).

##### **C. Cấu hình Redis**
- Node: **"Get Session"** và **"Update Session"** (Redis)
  - **Credentials**: Chọn `redis` (đã cấu hình Redis).
  - **Key Parameters**:
    - `operation`: `get` (lấy session) và `set` (cập nhật session).

##### **D. Thiết lập S3**
- Node: **"Download Video"**, **"Upload a file"**, **"Upload Metadata"** (S3)
  - **Credentials**: Chọn `s3` (đã cấu hình bucket S3).
  - **Folder**: Đặt tên folder lưu trữ (ví dụ: `kie-ai-videos`).

##### **E. Telegram Bot**
- Node: **"Send Video Preview (Veo)"**, **"Send Video Preview (Other)"**, **"Send Merge Options"**, **"Send Timeout"**
  - **Credentials**: Chọn `telegramApi` (đã cấu hình bot token).
  - **Chat ID**: Điền ID chat của Telegram (có thể lấy từ `@username_to_id_bot`).
  - **Caption**: Tùy chỉnh thông điệp (ví dụ: `Video đã hoàn thành! Click để publish`).

##### **F. Webhook URL cho "Retry Poll"**
- Node: **"Retry Poll"** (HTTP Request)
  - **URL**: Đặt lại thành **webhook URL của n8n instance** (ví dụ: `https://tên-vps-của-bạn.com/webhook/video-poll`).

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Gửi một **yêu cầu mẫu** (JSON) đến webhook `video-poll` để kiểm tra.
  - Dữ liệu mẫu:
    ```json
    {
      "taskId": "abc123",
      "model": "Veo 3.1",
      "chatId": "123456789"
    }
    ```
- **Bật Active**: Sau khi test thành công, bật workflow.

---
### ✍️ **Mẹo & gợi ý nâng cao**
1. **Lưu log tự động**:
   - Thêm node **"stickyNote"** để ghi lại trạng thái của mỗi task (ví dụ: `Task {taskId} hoàn thành tại {thời gian}`).

2. **Gửi báo cáo định kỳ**:
   - Sử dụng node **HTTP Request** kết hợp với **Telegram Bot** để gửi **báo cáo hàng ngày** về số lượng video hoàn thành.

3. **Tích hợp Slack**:
   - Thay vì Telegram, có thể gửi kết quả qua **Slack** bằng node `n8n-nodes-base.slack`.

4. **Xử lý video extend**:
   - Nếu workflow yêu cầu **merge video** (ví dụ: extend clip), node **"Is Extend?"** sẽ tự động xử lý.

5. **Optimize thời gian chờ**:
   - Thay đổi **thời gian wait** (node **"Wait 1 Minute"**) từ 60s sang 30s nếu KIE.ai phản hồi nhanh.

---
### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc phải theo dõi thủ công trạng thái tạo video. **Tự động hóa từ đầu đến cuối** với:
✔ **Kiểm tra trạng thái** mỗi phút.
✔ **Tải xuống video 1080p** và lưu trên S3.
✔ **Gửi kết quả qua Telegram** với button publish.
✔ **Xử lý lỗi và thời gian chờ** một cách chuyên nghiệp.

**Hành động ngay!**
- **Import workflow** và bắt đầu tự động hóa ngay.
- **Tối ưu hóa** bằng cách thêm log hoặc tích hợp Slack.
- **Chia sẻ kết quả** với đồng nghiệp để tăng hiệu suất team!

---
**💡 Lưu ý cuối cùng**:
Nếu gặp vấn đề với **API KIE.ai** hoặc **Redis**, hãy kiểm tra lại **credentials** và **URL API**. Nếu cần hỗ trợ, có thể tham khảo [n8n Community](https://community.n8n.io/) hoặc liên hệ tác giả JoeVenner.