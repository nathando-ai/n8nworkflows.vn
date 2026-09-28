---
title: "📱 Gửi SMS Tự Động bằng MSG91 - Không Cần Code, Chỉ Với 2 Bước"
description: "Tự động hóa việc gửi SMS qua MSG91 chỉ trong 2 node, tiết kiệm thời gian và tăng hiệu quả giao tiếp với khách hàng. Phù hợp cho doanh nghiệp, marketer và người dùng cá nhân."
slug: "tu-dong-hoa-gui-sms-bang-msg91"
tags: [n8n, automation, SMS marketing, MSG91, no-code]
keywords: [n8n workflow SMS, tự động hóa gửi tin nhắn, MSG91 API, tự động hóa marketing, gửi SMS tự động]
---

# 🚀 Gửi SMS Tự Động bằng MSG91 - Không Cần Code

### **Tại sao các sếp lại phải gửi SMS thủ công?**
Gửi SMS một cách thủ công không chỉ tốn thời gian mà còn dễ gây lỗi, mất chính xác và không thể mở rộng. Đặc biệt với doanh nghiệp cần liên lạc với khách hàng hàng loạt (đăng ký dịch vụ, nhắc nhở, quảng cáo...), việc tự động hóa gửi SMS bằng **MSG91** sẽ giúp:
- **Tiết kiệm 100% thời gian** của nhân viên.
- **Chính xác 100%** với API hỗ trợ gửi hàng ngàn tin nhắn một lúc.
- **Hoạt động 24/7** mà không cần can thiệp của con người.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng. Với VPS TinoHost, các sếp có thể:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow SMS)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Gửi SMS hàng loạt** chỉ với một lần kích hoạt.
- **Không giới hạn số lượng** tin nhắn (tùy thuộc vào gói dịch vụ MSG91).
- **Dễ dàng mở rộng** cho các workflow khác (ví dụ: kết hợp với Slack, Telegram, hoặc email).
- **Hoạt động tự động** mà không cần can thiệp của con người.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow này, các sếp cần:
1. **Tài khoản MSG91** và **API Key**:
   - Đăng ký tại [MSG91 Developer Portal](https://developer.msg91.com/).
   - Nhận **API Key** từ trang cá nhân của MSG91.
2. **Tài khoản n8n** (cả phiên bản cloud lẫn self-hosted).
3. **N8n Node MSG91** (đã tích hợp sẵn trong n8n, không cần cài thêm).
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### **1. Import Workflow 📥**
Các sếp có thể import workflow này bằng cách:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/511) và import vào **n8n Editor**.
- **Copy JSON** từ link trên và dán vào **Create Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này chỉ có **2 node**, nhưng các sếp cần chú ý cấu hình chính xác:

##### **Node 1: Manual Trigger (Kích hoạt thủ công)**
- **Tên node**: "On clicking 'execute'"
- **Lưu ý**:
  - Node này **không cần cấu hình gì**, chỉ dùng để kích hoạt workflow khi cần.

##### **Node 2: Msg91 (Gửi SMS)**
- **Tên node**: "Msg91"
- **Credentials**:
  - Chọn **"msg91Api"** (nếu chưa có, tạo mới trong **Credentials** của n8n).
  - Điền **API Key** từ MSG91 vào trường tương ứng.
- **Cấu hình SMS**:
  - **Phone Number**: Điền số điện thoại nhận SMS (dạng quốc tế, ví dụ: `+841234567890`).
  - **Message**: Nội dung SMS (có thể sử dụng **variables** từ node trước nếu workflow phức tạp hơn).
  - **Sender ID**: ID người gửi (nếu có, tùy thuộc vào gói dịch vụ MSG91).

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Kích hoạt node **Manual Trigger** và kiểm tra SMS đã được gửi thành công.
2. **Bật Active**:
   - Sau khi kiểm tra, chuyển workflow sang **Active** để sử dụng thường xuyên.

---

### ✍️ Mẹo & gợi ý nâng cao
:::note[CÁCH NÂNG CAO WORKFLOW]
1. **Kết hợp với Webhook** để tự động gửi SMS khi có sự kiện (ví dụ: khi khách hàng đăng ký trên website).
2. **Lưu log SMS** bằng node **Google Sheets** hoặc **Notion** để theo dõi hiệu quả.
3. **Gửi SMS định kỳ** bằng **n8n Cron Trigger** (ví dụ: nhắc nhở khách hàng hàng tháng).
4. **Tích hợp với Slack/Telegram** để thông báo khi gửi SMS thất bại.
:::

---

### 📌 Kết luận
Workflow này giúp các sếp **gửi SMS tự động chỉ trong 2 bước**, tiết kiệm thời gian và tăng hiệu quả giao tiếp. **Không cần code**, không cần kiến thức kỹ thuật phức tạp – chỉ cần **n8n và MSG91**.

👉 **Hãy thử ngay** và tự động hóa SMS của doanh nghiệp bạn! Nếu có vấn đề, các sếp có thể tham khảo [hướng dẫn MSG91](https://developer.msg91.com/) hoặc liên hệ hỗ trợ n8n.

---