---
title: "🚀 Tự Động Hóa Cảnh Báo Công Việc Upwork Với MongoDB & Slack - Không Cần Code"
description: "Workflow tự động theo dõi và cảnh báo công việc mới trên Upwork, lưu trữ dữ liệu vào MongoDB, và gửi thông báo ngay lập tức qua Slack - tiết kiệm thời gian lên tới 80% cho các sếp freelancer."
slug: "tự-dộng-hoa-cảnh-báo-upwork-mongodb-slack"
tags: [n8n, automation, freelance, no-code, mongodb, slack, upwork]
keywords: [tự động hóa upwork, cảnh báo công việc mới, mongodb n8n, slack notification, tự động hóa freelancer]
---

# 🚀 **Tự Động Hóa Cảnh Báo Công Việc Upwork Với MongoDB & Slack**

### **Giải pháp hoàn hảo cho các sếp freelancer**
Làm thế nào để không bỏ lỡ bất kỳ cơ hội nào trên Upwork? Thay vì phải **quét hàng chục trang** mỗi ngày, hoặc **đăng ký nhận email** từ nhiều nguồn khác nhau, **Workflow này tự động hóa toàn bộ quá trình** cho bạn:
- **Theo dõi liên tục** các công việc mới trên Upwork theo URL bạn chọn.
- **Lưu trữ dữ liệu** vào MongoDB để theo dõi lịch sử và tránh trùng lặp.
- **Gửi cảnh báo ngay lập tức** qua Slack, giúp bạn **không bỏ lỡ bất kỳ cơ hội nào**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không phải quét thủ công hàng ngày, tự động cập nhật mỗi khi có công việc mới.
✅ **Không bỏ lỡ cơ hội**: Cảnh báo ngay lập tức qua Slack, giúp bạn phản hồi nhanh hơn đối thủ.
✅ **Lưu trữ dữ liệu**: Tất cả lịch sử công việc được lưu vào MongoDB, dễ dàng theo dõi và phân tích.
✅ **Hoạt động 24/7**: Workflow chạy tự động theo lịch trình, không phụ thuộc vào giờ làm việc của bạn.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
- **Tài khoản Upwork** (để lấy API token từ Apify).
- **Tài khoản MongoDB Atlas** (hoặc MongoDB self-hosted) để lưu trữ dữ liệu.
- **Tài khoản Slack** và **Slack API Token** để gửi thông báo.
- **Apify Token** (để truy cập API Upwork).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/2834](https://n8n.io/workflows/2834) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** và chọn **"Import"** → Dán JSON hoặc tải file JSON lên.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **a. Thiết lập Credentials**
- **MongoDB**:
  - Tạo **credentials mới** trong n8n với loại `MongoDB`.
  - Điền thông tin kết nối (URI, tên database, tên collection).
- **Slack**:
  - Tạo **credentials mới** với loại `Slack`.
  - Chọn **Slack API Token** và chọn **workspace** (Slack team) muốn gửi thông báo.
- **HTTP Query Auth (Apify Token)**:
  - Tạo **credentials mới** với loại `HTTP Query Auth`.
  - Đặt **key = `token`** và **value = Apify Token** (mua từ [Apify](https://apify.com/)).

##### **b. Cấu hình Node "Assign parameters"**
- Mở node **"Assign parameters"** và chỉnh sửa **URLs** của các công việc Upwork bạn muốn theo dõi.
- Ví dụ:
  ```json
  {
    "urls": [
      "https://www.upwork.com/o/jobs/browse/?search=web+development",
      "https://www.upwork.com/o/jobs/browse/?search=python+developer"
    ]
  }
  ```

##### **c. Cấu hình Node "If Working Hours"**
- Mở node **"If Working Hours"** và chỉnh sửa **thời gian hoạt động** (ví dụ: từ 8h sáng đến 6h chiều).
- Nếu bạn muốn workflow chạy **tất cả thời gian**, bỏ qua node này hoặc đặt điều kiện luôn `true`.

##### **d. Kiểm tra Node "Find Existing Entries"**
- Node này **tránh trùng lặp** bằng cách kiểm tra MongoDB trước khi thêm mới.
- Đảm bảo **collection** trong MongoDB có **trường `jobId`** để so sánh.

##### **e. Node "Send message in #general"**
- Đảm bảo **channel Slack** (`#general`) tồn tại và bạn có quyền gửi tin nhắn.
- Thay đổi **message template** nếu muốn thay đổi nội dung cảnh báo.

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Chọn **Schedule Trigger** và nhấn **"Execute"** để kiểm tra workflow với dữ liệu mẫu.
  - Kiểm tra **Slack** và **MongoDB** để xác nhận dữ liệu được lưu và gửi đúng.
- **Bật Active**:
  - Sau khi test thành công, bật **Active** cho workflow.
  - Đặt **Schedule Trigger** theo lịch trình mong muốn (ví dụ: **mỗi 1 giờ**).

---

### ✍️ **Mẹo & gợi ý nâng cao**
- **Tăng cường cảnh báo**:
  - Thêm **node Slack** thứ 2 để gửi tin nhắn riêng cho bạn hoặc team.
  - Sử dụng **node Email** (n8n-nodes-base.email) để gửi cảnh báo qua email.
- **Lưu log chi tiết**:
  - Thêm **node StickyNote** để ghi lại lịch sử chạy workflow.
- **Tự động phản hồi**:
  - Kết hợp với **node Webhook** để tự động gửi ứng tuyển khi có công việc mới.
- **Phân tích dữ liệu**:
  - Sử dụng **node MongoDB Query** để lấy ra các công việc phù hợp nhất và gửi báo cáo định kỳ.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp freelancer, giúp bạn **không bỏ lỡ bất kỳ cơ hội nào** trên Upwork mà không cần viết một dòng code nào. **Hãy tự động hóa ngay hôm nay** và tập trung vào việc **nắm bắt công việc chất lượng**!

👉 **Bắt đầu ngay**: [Tải workflow từ n8n.io](https://n8n.io/workflows/2834) và import vào n8n của bạn!