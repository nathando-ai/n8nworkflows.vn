---
title: "🚀 Tự Động Xóa Email Spam trong Gmail Hàng Tuần"
description: "Workflow n8n tự động xóa toàn bộ email spam trong Gmail vào lúc nửa đêm Chủ Nhật, giúp hòm thư luôn sạch sẽ mà không cần thao tác thủ công."
slug: "tu-dong-xoa-email-spam-gmail"
tags: [n8n, automation, no-code, gmail, schedule]
keywords: [n8n workflow, tự động hóa, Gmail, xóa spam, lịch trình]
---

# 🚀 Tự Động Xóa Email Spam trong Gmail Hàng Tuần

Bạn có bao giờ mở Gmail lên và thấy hàng trăm, thậm chí hàng nghìn email rác trong mục **Spam**?  
Việc xoá chúng một cách thủ công không chỉ tốn thời gian mà còn khiến bạn dễ bỏ lỡ những email quan trọng nếu vô tình xóa nhầm.  
**Workflow “Automatically Delete Spam Emails in Gmail on Schedule”** sẽ giải quyết vấn đề này 100% tự động, chạy vào lúc nửa đêm Chủ Nhật mỗi tuần, xóa sạch mọi email Spam mà không cần bạn can thiệp một dòng lệnh nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn phải mở Gmail và xóa spam thủ công.  
- **Inbox luôn sạch sẽ**: Giảm tối đa rác trong mục Spam, tránh nhầm lẫn.  
- **Tiết kiệm dung lượng**: Xóa email rác giúp giảm dung lượng lưu trữ trên Gmail.  
- **Hoạt động liên tục**: Tự động chạy mỗi tuần mà không cần giám sát.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Gmail** mà bạn muốn tự động dọn dẹp.  
- **OAuth2 credentials cho Gmail** trong n8n (cần quyền `https://mail.google.com/`).  
- **n8n** đã được cài đặt và có quyền truy cập internet để gọi API Gmail.  
- **Node Schedule** để thiết lập thời gian chạy (đã có trong workflow).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập link gốc: <https://n8n.io/workflows/4285> và tải file JSON của workflow.  
2. Trong n8n Editor, nhấn **Import** → **Upload JSON** → chọn file vừa tải.  
3. Hoặc copy toàn bộ nội dung JSON → **Import** → **Paste JSON** → **Import**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Hướng dẫn cấu hình chi tiết |
|------|-----------------------------|
| **Trigger at Sunday midnight** (Schedule Trigger) | - **Mode**: *Every Week* <br> - **Day of Week**: *Sunday* <br> - **Time**: *00:00* (đặt múi giờ phù hợp với tài khoản của bạn). |
| **Get all SPAM emails** (Gmail – Get All) | - **Credentials**: Chọn `gmailOAuth2` đã tạo. <br> - **Operation**: *Get All* <br> - **Label**: *SPAM* (đảm bảo nhập đúng tên label “SPAM”). <br> - **Return All**: *Yes* (để lấy toàn bộ email). |
| **Delete SPAM emails** (Gmail – Delete) | - **Credentials**: Cùng `gmailOAuth2`. <br> - **Operation**: *Delete* <br> - **Message ID**: Dùng **Expression** để lấy ID từ node “Get all SPAM emails”. <br>   ```<br>   {{ $json["id"] }}<br>   ``` <br>   (Nếu node trả về mảng, sử dụng `{{ $json["messages"] }}` và bật **Batch**). |
| **Sticky Note** (chỉ ghi chú) | Không cần cấu hình, chỉ để mô tả trên canvas. |

> **Lưu ý:** Đảm bảo OAuth2 đã được cấp quyền **Full Access to Gmail**; nếu chưa, hãy tạo lại credentials và bật scope `https://mail.google.com/`.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** lần đầu với dữ liệu mẫu để kiểm tra: workflow sẽ lấy danh sách spam và xóa chúng.  
2. Kiểm tra Gmail → mục **Spam** để xác nhận email đã bị xóa.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải) để workflow tự động chạy vào mỗi Chủ Nhật.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node Slack hoặc Telegram ngay sau node “Delete SPAM emails” để gửi báo cáo số lượng email đã xóa.  
- **Lưu log vào Google Sheet**: Dùng node Google Sheets để ghi lại `Message ID`, `Subject`, và thời gian xóa, giúp bạn theo dõi lịch sử.  
- **Xử lý lỗi**: Bọc các node Gmail trong **Error Workflow** để gửi email cảnh báo nếu có lỗi API (quota, token hết hạn).  
- **Tùy chỉnh tần suất**: Thay đổi node Schedule để chạy hàng ngày hoặc hàng tháng tùy nhu cầu.

### 📌 Kết luận
Với chỉ **3 node** đơn giản, workflow này giúp các sếp **giải phóng inbox**, **tiết kiệm thời gian** và **đảm bảo Gmail luôn sạch sẽ** mà không cần viết một dòng code nào. Hãy import ngay, cấu hình Gmail OAuth2, bật Active và để n8n làm việc cho bạn! 🚀