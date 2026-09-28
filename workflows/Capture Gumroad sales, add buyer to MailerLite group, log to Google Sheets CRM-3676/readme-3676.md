---
title: "🚀 Tự Động Hóa Bán Hàng Gumroad → Nhóm MailerLite + CRM Google Sheets (Không Cần Code)"
description: "Workflow tự động chụp tất cả đơn hàng từ Gumroad, thêm khách hàng vào nhóm MailerLite để gửi email tự động, đồng thời ghi log vào Google Sheets CRM. Giúp doanh nghiệp tiết kiệm 100% thời gian quản lý khách hàng mới."
slug: "tu-dong-hoa-gumroad-mailerlite-google-sheets"
tags: [n8n, automation, ecommerce, mailerlite, google-sheets, gumroad]
keywords: [tự động hóa gumroad, mailerlite api, google sheets automation, bán hàng tự động, workflow n8n bán hàng]
---

# 🚀 **Tự Động Hóa Bán Hàng Gumroad → Nhóm MailerLite + CRM Google Sheets**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Bạn đã bao giờ phải **thủ công** ghi chép thông tin khách hàng mới từ Gumroad vào MailerLite và Google Sheets? Hoặc phải **quay lại kiểm tra** mỗi khi có đơn hàng mới để thêm vào nhóm email? Với workflow này, **tất cả đều tự động hóa** chỉ trong vài phút sau khi cài đặt!

- **Không cần code**: Sử dụng n8n để kết nối Gumroad, MailerLite và Google Sheets một cách dễ dàng.
- **Tiết kiệm thời gian**: Khách hàng mới tự động được thêm vào nhóm MailerLite và ghi log vào CRM.
- **Tăng cường tương tác**: Sử dụng tính năng **nhóm MailerLite** để gửi email tự động (dòng chuyển đổi) cho khách hàng mới.
- **Dữ liệu thống kê**: Ghi chép tất cả đơn hàng vào Google Sheets để theo dõi doanh số và phân tích.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
✅ **Tự động chụp đơn hàng Gumroad** → Không phải thủ công ghi chép.
✅ **Thêm khách hàng vào nhóm MailerLite** → Gửi email tự động (dòng chuyển đổi).
✅ **Ghi log vào Google Sheets CRM** → Theo dõi doanh số và phân tích.
✅ **Hoạt động liên tục 24/7** → Không cần can thiệp thủ công.

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Gumroad** (đã có sản phẩm bán).
2. **Tài khoản MailerLite** (đã tạo nhóm email).
3. **Tài khoản Google Sheets** (đã cấu hình API OAuth2).
4. **API Keys & Credentials**:
   - **Gumroad API Key** (tạo từ **Settings > Advanced > Applications**).
   - **MailerLite API Key** (tạo từ **Integrations > API**).
   - **Google Sheets OAuth2 Credentials** (cài đặt từ [n8n docs](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.googlesheets/)).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/3676) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Editor** → Nhấn **"Import"** → Chọn file JSON.
  2. Hoặc **copy toàn bộ JSON** vào ô **"Import Workflow"** và nhấn **"Import"**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **4 node chính**, các sếp cần cấu hình như sau:

##### **🔹 Node 1: Gumroad Sale Trigger (Gumroad Trigger)**
- **Tên node**: `Gumroad Sale Trigger`
- **Cấu hình**:
  - Chọn **credentials**: `gumroadApi` (đã tạo từ API Key Gumroad).
  - **Resource**: `sale` (đã mặc định).
  - **Test run**: Nhấn **"Test"** để xác nhận kết nối.

##### **🔹 Node 2: Assign to Group (MailerLite - Thêm vào nhóm)**
- **Tên node**: `Assign to group` (là một **HTTP Request**).
- **Cấu hình**:
  - **Credentials**: `mailerLiteApi` (API Key MailerLite).
  - **URL**: `https://api.mailerlite.com/api/v2/groups/{groupId}/subscribers/{subscriberId}`
    - **Lấy `groupId`** từ **MailerLite** (tạo nhóm trước, sau đó gọi API `GET /api/v2/groups` để lấy ID).
    - **Lấy `subscriberId`** từ **Node 3** (add subscriber).
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_MAILERLITE_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON)**:
    ```json
    {
      "subscriber": {
        "email": "{{ $node["add subscriber to MailerLite"].json()["email"] }}"
      }
    }
    ```

##### **🔹 Node 3: Add Subscriber to MailerLite (Thêm khách hàng mới)**
- **Tên node**: `add subscriber to MailerLite`
- **Cấu hình**:
  - **Credentials**: `mailerLiteApi`.
  - **Email**: `{{ $node["Gumroad Sale Trigger"].json()["email"] }}` (lấy từ đơn hàng Gumroad).
  - **Name**: `{{ $node["Gumroad Sale Trigger"].json()["name"] }}` (tên khách hàng).
  - **Test run**: Nhấn **"Test"** để thêm khách hàng mẫu.

##### **🔹 Node 4: Append Row in CRM (Google Sheets - Ghi log)**
- **Tên node**: `append row in CRM`
- **Cấu hình**:
  - **Credentials**: `googleSheetsOAuth2Api`.
  - **Sheet Name**: Tên bảng Google Sheets bạn muốn ghi log.
  - **Headers**:
    ```json
    {
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON)**:
    ```json
    {
      "values": [
        [
          "{{ $node["Gumroad Sale Trigger"].json()["email"] }}",  // Email
          "{{ $node["Gumroad Sale Trigger"].json()["name"] }}",  // Tên
          "{{ $node["Gumroad Sale Trigger"].json()["product"] }}", // Sản phẩm
          "{{ $node["Gumroad Sale Trigger"].json()["price"] }}",  // Giá
          "{{ $node["Gumroad Sale Trigger"].json()["date"] }}"   // Ngày mua
        ]
      ]
    }
    ```
  - **Test run**: Nhấn **"Test"** để ghi log mẫu.

#### **3. Kích Hoạt ⚡️**
- **Test run** với một đơn hàng mẫu để kiểm tra workflow.
- **Bật Active** workflow để nó hoạt động liên tục.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối Slack/Telegram** để thông báo khi có đơn hàng mới:
   - Sử dụng **node Slack Webhook** hoặc **Telegram Bot** để gửi tin nhắn tự động.
2. **Lưu log chi tiết** vào Google Sheets:
   - Thêm cột **status** (hoàn tất/thất bại) và **timestamp** để theo dõi.
3. **Gửi email tự động từ MailerLite**:
   - Tạo **dòng chuyển đổi (automation)** trong MailerLite khi khách hàng vào nhóm mới.
4. **Tích hợp với Stripe/PayPal** (nếu bán nhiều kênh):
   - Sử dụng **node Stripe Trigger** hoặc **PayPal Webhook** để chụp đơn hàng từ nhiều nguồn.

---

### 📌 **Kết Luận**
Workflow này **giúp các sếp tự động hóa toàn bộ quy trình bán hàng từ Gumroad đến CRM**, tiết kiệm **100% thời gian thủ công** và tăng **tỷ lệ chuyển đổi** nhờ email tự động. **Hãy áp dụng ngay** và bắt đầu bán hàng hiệu quả hơn!

👉 **Bạn cần hỗ trợ thêm?** Hãy tham gia **Discord của 1node.ai** để được tư vấn chi tiết: [Join 1node.ai Discord](https://discord.gg/1nodeai).

---
**Chúc các sếp thành công với tự động hóa!** 🚀