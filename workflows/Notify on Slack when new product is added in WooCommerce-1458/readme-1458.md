---
title: "🚀 Tự Động Thông Báo Mới Sản Phẩm WooCommerce Trên Slack - Không Cần Code!"
description: "Giải pháp tự động hóa hoàn toàn miễn phí để các sếp nhận thông báo tức thời khi có sản phẩm mới được thêm vào WooCommerce, giúp theo dõi và phản hồi nhanh chóng mà không mất thời gian kiểm tra thủ công."
slug: "tieu-dong-thong-bao-woocommerce-slack"
tags: [n8n, automation, woocommerce, slack, ecommerce]
keywords: [tự động hóa woocommerce, thông báo sản phẩm mới slack, n8n workflow, tự động hóa bán hàng online, tự động hóa marketing]
---

# 🚀 **Tự Động Thông Báo Mới Sản Phẩm WooCommerce Trên Slack - Không Cần Code!**

### **Nỗi Đau Của Các Sếp Trong Bán Hàng Online**
Các sếp bán hàng online thường phải **kiểm tra thủ công** danh sách sản phẩm mới hàng ngày trên WooCommerce để cập nhật, quảng bá hoặc kiểm tra chất lượng. Điều này không chỉ **tốn thời gian** mà còn **rất dễ bỏ sót** sản phẩm quan trọng, ảnh hưởng đến doanh thu và trải nghiệm khách hàng.

**Giải pháp?** Một **workflow tự động hóa hoàn toàn** trên n8n sẽ **gửi thông báo tức thời** đến Slack mỗi khi có sản phẩm mới được thêm vào WooCommerce, giúp các sếp **nhận thông tin ngay lập tức** mà không cần phải mở cửa hàng hoặc kiểm tra thường xuyên.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải kiểm tra thủ công hàng ngày.
- **Tức thời & chính xác**: Nhận thông báo ngay khi sản phẩm mới được thêm.
- **Tích hợp hoàn hảo**: Slack giúp các sếp theo dõi từ mọi nơi, kể cả trên điện thoại.
- **Hoạt động 24/7**: Workflow chạy tự động, không cần can thiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản WooCommerce** với quyền API (để n8n có thể truy cập dữ liệu sản phẩm).
2. **Slack Workspace** và **API Token** của Slack (để gửi thông báo).
3. **n8n Self-hosted** (để workflow chạy 24/7).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste** JSON vào n8n Editor:
- **Tải workflow từ link gốc**: [Tải Workflow](https://n8n.io/workflows/1458)
- **Cách import**:
  - Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON hoặc **paste** JSON từ link trên.
  - Hoặc **copy** toàn bộ JSON từ link và **paste** vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này chỉ có **2 node**, nhưng **cấu hình sai credentials sẽ làm workflow không hoạt động**. Các sếp cần chú ý:

##### **Node 1: Product Created (wooCommerceTrigger)**
- **Loại node**: `wooCommerceTrigger` (nghĩa là nó sẽ **nghe** sự kiện mới sản phẩm được thêm).
- **Credentials cần thiết**:
  - **wooCommerceApi**: Các sếp phải **cấu hình API Key** của WooCommerce trong **Credentials** của n8n.
    - **Cách lấy API Key**:
      1. Vào **WooCommerce Dashboard** → **Settings** → **Advanced** → **REST API**.
      2. Nhấn **Add New Key** → Chọn **Read/Write** (để workflow có thể nghe sự kiện mới).
      3. Copy **Consumer Key** và **Consumer Secret** → Dán vào **Credentials** của n8n.

##### **Node 2: Send to Slack (slack)**
- **Loại node**: `slack` (gửi thông báo đến Slack).
- **Credentials cần thiết**:
  - **slackApi**: Các sếp phải **cấu hình OAuth Token** của Slack.
    - **Cách lấy OAuth Token**:
      1. Vào [Slack API](https://api.slack.com/apps) → Tạo một **new app**.
      2. Chọn **OAuth & Permissions** → Thêm **scopes** như `chat:write` (để gửi tin nhắn).
      3. Sau khi tạo app, **install** vào workspace Slack của mình.
      4. Copy **OAuth Token** → Dán vào **Credentials** của n8n.

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Các sếp nên **thêm một sản phẩm mẫu** vào WooCommerce và kiểm tra xem thông báo có xuất hiện trên Slack không.
- **Bật Active**: Sau khi kiểm tra thành công, **bật workflow** để nó hoạt động liên tục.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::note[CÁCH LÀM NỔI BẬT HƠN]
- **Thêm thông tin chi tiết sản phẩm** vào Slack:
  - Sử dụng **node `Set`** để thêm trường dữ liệu như **tên sản phẩm, giá, mô tả** vào payload trước khi gửi Slack.
  - Ví dụ: `{{ $json["name"] }} - Giá: {{ $json["price"] }}`
- **Gửi thông báo đến kênh riêng**:
  - Trong **node Slack**, chọn **channel** cụ thể (ví dụ: `#woo-notifications`) thay vì DM.
- **Lưu log hoạt động**:
  - Sử dụng **node `Google Sheets`** để ghi lại tất cả thông báo đã gửi, giúp theo dõi dễ dàng.
- **Tích hợp với Telegram**:
  - Thay vì Slack, các sếp có thể sử dụng **node `telegram`** để gửi thông báo qua Telegram.
:::

---

### 📌 **Kết Luận**
**Tự động hóa thông báo sản phẩm mới từ WooCommerce đến Slack** là một trong những **workflow đơn giản nhưng cực kỳ hữu ích** để các sếp **tiết kiệm thời gian** và **tránh bỏ sót** sản phẩm mới. Với chỉ **2 node**, workflow này đã giải quyết được **nỗi lo thủ công** trong quản lý sản phẩm online.

**Hãy áp dụng ngay và bắt đầu tự động hóa bán hàng của mình!** 🚀

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::