---
title: "🗑️ **Tự Động Xóa Tự Động Gmail: Xóa Spam, Promotions, Social & Trash Mỗi Ngày - Không Cần Code!**"
description: "Giải pháp tự động hóa hoàn toàn tự động xóa hàng loạt email không cần thiết (Spam, Promotions, Social, Trash) từ Gmail hàng ngày, giúp tiết kiệm không gian lưu trữ và thời gian thủ công. Hoạt động 24/7, không cần can thiệp của bạn."
slug: "tieu-dong-xoa-gmail-spam-promotions-social-trash"
tags: [n8n, tự động hóa gmail, xóa email tự động, quản lý email, lưu trữ gmail, no-code]
keywords: [tự động hóa gmail n8n, xóa spam gmail tự động, lưu trữ gmail hiệu quả, xóa email cũ gmail, tự động hóa email không cần code]
---

# 🚀 **Tự Động Xóa Gmail: Xóa Spam, Promotions, Social & Trash Mỗi Ngày - Không Cần Code!**

---

### **🔍 Nỗi Đau Của Các Sếp Với Gmail**
Hàng ngày, inbox của các sếp bị "ngập chìm" bởi hàng trăm email không cần thiết:
- **Spam**: Phishing, quảng cáo spam, email lừa đảo.
- **Promotions**: Marketing, ưu đãi, newsletter không mong muốn.
- **Social**: Thông báo từ Facebook, LinkedIn, Twitter...
- **Trash**: Email đã xóa nhưng vẫn chiếm không gian lưu trữ.

**Kết quả?** Inbox lộn xộn, không gian lưu trữ bị "cạn kiệt", và phải mất **giờ đồng hồ** mỗi tuần để xóa thủ công. **Đã đến lúc dừng việc làm thủ công này!**

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần xóa email thủ công hàng ngày.
✅ **Giảm không gian lưu trữ**: Xóa hàng loạt email không cần thiết tự động.
✅ **Inbox sạch sẽ**: Chỉ giữ lại email quan trọng.
✅ **Hoạt động 24/7**: Workflow chạy tự động mỗi ngày (hoặc thời gian bạn chọn).
✅ **An toàn & linh hoạt**: Có thể điều chỉnh để **chỉ xóa email cũ hơn 30 ngày** hoặc **di chuyển vào Thùng Rác** thay vì xóa vĩnh viễn.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
- **Tài khoản Gmail chính**: Workflow cần quyền truy cập vào tài khoản Gmail để xóa email.
- **API Key Gmail OAuth 2.0**:
  - Cài đặt **OAuth 2.0** cho Gmail trong n8n:
    1. Tạo **Credentials mới** trong n8n (n8n-nodes-base.gmail).
    2. Đăng nhập vào [Google Cloud Console](https://console.cloud.google.com/) và tạo **API Key OAuth 2.0**.
    3. Cấu hình **Redirect URI** là `http://localhost:5678/connect/gmail/oauth/callback`.
    4. Sau khi đăng nhập, copy **Client ID** và **Client Secret** vào n8n.
- **n8n Self-hosted** (khuyến nghị):
  - Để workflow chạy ổn định 24/7, các sếp nên **cài n8n trên VPS riêng** (Self-hosted).
  - 👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
  - 👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**

:::

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7952](https://n8n.io/workflows/7952).
- **Cách 1**: Nhấn **Import** trong n8n Editor và chọn file JSON.
- **Cách 2**: Copy toàn bộ nội dung JSON và **dán vào Editor** của n8n (trong tab "Import").

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **6 node chính**, nhưng có **3 node quan trọng cần cấu hình kỹ**:

##### **🔹 Node 1: Thiết Lập OAuth 2.0 cho Gmail**
- Mở **Credentials** trong n8n (n8n-nodes-base.gmail).
- Chọn **gmailOAuth2** và **cấu hình lại**:
  - **Client ID** và **Client Secret** từ Google Cloud Console.
  - **Redirect URI**: `http://localhost:5678/connect/gmail/oauth/callback`.
  - **Scopes**: Chọn `https://www.googleapis.com/auth/gmail.readonly` (để đọc email) và `https://www.googleapis.com/auth/gmail.modify` (để xóa email).

##### **🔹 Node 2: Thiết Lập Thời Gian Chạy (Schedule Trigger)**
- Mở node **"Trigger every day at midnight"**.
- **Điều chỉnh thời gian chạy**:
  - Mặc định là **mỗi ngày lúc 00:00** (giờ Việt Nam).
  - Có thể thay đổi thành **tối ngày thứ 7**, **mỗi tuần**, hoặc **thời gian tùy chỉnh**.
  - Ví dụ: **"Mỗi ngày lúc 22:00"** để xóa email vào buổi tối.

##### **🔹 Node 3: Điều Chỉnh Lọc Email (Tùy Chọn)**
- Mở từng node **Fetch Spam Emails**, **Fetch Promotions Emails**, **Fetch Social Emails**, **Fetch Trash Emails**.
- **Thêm điều kiện lọc** (nếu cần):
  - Ví dụ: **"Chỉ xóa email cũ hơn 30 ngày"**:
    - Trong **Gmail Query**, thêm `older_than:30d`.
    - Ví dụ: `label:spam older_than:30d` (xóa spam cũ hơn 30 ngày).
  - **Lưu ý**: Nếu không thêm điều kiện, **tất cả email trong folder đó sẽ bị xóa**.

##### **🔹 Node 4: Thay Đổi Thao Tác Xóa (Tùy Chọn)**
- Mở node **"Delete Mails"**.
- **Có 2 lựa chọn**:
  - **Xóa vĩnh viễn** (mặc định): Email sẽ không thể khôi phục.
  - **Di chuyển vào Thùng Rác** (an toàn hơn):
    - Thay đổi **operation** từ `delete` thành `moveToTrash`.

#### **3. Kích Hoạt ⚡️**
- **Test Run** với dữ liệu mẫu:
  - Chạy **Manual Run** để kiểm tra workflow có hoạt động không.
  - Kiểm tra **log** trong n8n để đảm bảo email được xóa đúng.
- **Bật Active**:
  - Sau khi kiểm tra thành công, **bật Active** để workflow chạy tự động hàng ngày.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
- **Gửi báo cáo định kỳ**:
  - Thêm node **Slack/Telegram** để thông báo khi xóa thành công.
  - Ví dụ: `"Xóa thành công 500 email Spam vào ngày [ngày]"`.
- **Lưu log vào Google Sheets**:
  - Thêm node **Google Sheets** để ghi lại lịch sử xóa email.
  - Dễ dàng theo dõi số lượng email được xóa mỗi ngày.
- **Kết hợp với AI (LLM)**:
  - Sử dụng node **LLM** để phân tích email trước khi xóa (nếu cần).
  - Ví dụ: Xóa email có từ khóa "quảng cáo" hoặc "scam".
- **Xóa email theo chủ đề**:
  - Thêm điều kiện lọc để **chỉ xóa email từ các domain nhất định** (ví dụ: `@gmail.com`, `@yahoo.com`).
:::

---
### **📌 Kết Luận**
Workflow **Scheduled Gmail Cleanup** là **giải pháp hoàn hảo** để các sếp **tự động hóa việc xóa email không cần thiết**, tiết kiệm **thời gian và không gian lưu trữ** mà không cần viết một dòng code nào.

**Hành động ngay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình OAuth 2.0** và **thời gian chạy**.
3. **Test Run** và **bật Active**.
4. **Xem inbox của mình trở nên sạch sẽ mỗi ngày!**

👉 **Bắt đầu tự động hóa Gmail của bạn ngay hôm nay!** 🚀

---
### **🔗 Tài Liệu Tham Khảo**
- [Cách cài đặt OAuth 2.0 cho Gmail trong n8n](https://docs.n8n.io/integrations/builtins/nodes/n8n-nodes-base.gmail#authentication)
- [Cách cấu hình Schedule Trigger](https://docs.n8n.io/integrations/builtins/nodes/n8n-nodes-base.scheduleTrigger)
- [Tự động hóa Gmail với n8n (Hướng dẫn chi tiết)](https://n8n.io/learn/)