---
title: "💰 Tự Động Hoá Tạo & Gửi Hóa Đơn Pennylane Từ Webhook + Thông Báo Slack/Gmail (N8N)"
description: "Giải pháp hoàn toàn không code để tự động tạo hóa đơn từ dữ liệu CRM/form, gửi qua Pennylane, đồng thời thông báo ngay trên Slack và Gmail cho đội ngũ. Giúp tiết kiệm 80% thời gian thủ công và giảm thiểu lỗi trong quá trình tạo hóa đơn."
slug: "tu-dong-hoa-tao-va-gui-hoa-don-pennylane"
tags: [n8n, automation, pennylane, invoicing, no-code, slack, gmail, freemium]
keywords: [n8n workflow pennylane, tự động hóa hóa đơn, Pennylane API, tự động hóa Slack, gửi hóa đơn tự động, n8n cho doanh nghiệp]
---

# 🚀 **Tự Động Hoá Tạo & Gửi Hóa Đơn Pennylane Từ Webhook + Thông Báo Slack/Gmail**

Hãy tưởng tượng một ngày không còn phải **gõ tay hóa đơn một lần một lần**, không còn phải **quên gửi hóa đơn cho khách hàng**, và không còn phải **lo lắng về sai sót trong thông tin khách hàng**. Với workflow này, **tất cả chỉ cần một cú nhấp chuột** từ hệ thống CRM, form, hoặc script của bạn, n8n sẽ tự động:
✅ **Tìm kiếm/đăng ký khách hàng** trên Pennylane (nếu chưa có).
✅ **Tạo hóa đơn** với chi tiết sản phẩm, VAT, và điều kiện thanh toán.
✅ **Gửi hóa đơn qua email** (nếu khách hàng yêu cầu).
✅ **Thông báo ngay trên Slack/Gmail** cho đội ngũ theo dõi.
✅ **Trả về phản hồi JSON** để bạn có thể tích hợp với hệ thống khác.

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 80% thời gian thủ công**: Không cần phải copy-paste dữ liệu từ CRM sang Pennylane.
- **Chính xác 100%**: Khách hàng và hóa đơn được tự động cập nhật, không sai sót.
- **Hoạt động 24/7**: Workflow chạy tự động ngay cả khi bạn ngủ.
- **Cá nhân hóa thông báo**: Slack/Gmail sẽ gửi tin nhắn chi tiết cho từng hóa đơn.
- **Tích hợp dễ dàng**: Hoạt động với bất kỳ CRM/form nào (Pipedrive, Brevo, Typeform,...) chỉ cần gọi webhook.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Pennylane** (gói **Essentiel** trở lên) với **API access** và **token** có scope:
   - `customer_invoices:all`
   - `customers:all`
   *(Lấy token tại: [Pennylane API Settings](https://app.pennylane.fr/settings/api))*

2. **Slack Workspace** (nếu muốn thông báo trên Slack):
   - Tạo **OAuth App** và cấp quyền `chat:write` cho bot.
   - *(Hướng dẫn: [Slack API Setup](https://api.slack.com/apps))*

3. **Gmail OAuth** (nếu muốn gửi thông báo qua email):
   - Bật **Less Secure Apps** (nếu không dùng 2FA) hoặc cấu hình **OAuth 2.0**.
   - *(Hướng dẫn: [Gmail API Setup](https://developers.google.com/gmail/api/quickstart/overview))*

4. **Webhook URL** từ Pennylane (để gọi khi hóa đơn được tạo thành công).
5. **Dữ liệu mẫu** để test (xem [GitHub repo](https://github.com/Gauthier-Huguenin/n8n-pennylane-auto-invoicing/tree/main/examples)).
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ **file JSON** hoặc **copy/paste JSON** vào n8n Editor:
- **Tải file JSON** từ [n8n Workflows](https://n8n.io/workflows/15186) (ấn "Export").
- **Nhấn "Import"** trong n8n Editor và chọn file.
- **Hoặc copy toàn bộ JSON** từ [đây](https://github.com/Gauthier-Huguenin/n8n-pennylane-auto-invoicing/blob/main/workflow.json) và dán vào **Import Workflow** trong n8n.

:::note[**Lưu ý quan trọng**]
- **Không xóa node nào** trong workflow, chỉ chỉnh sửa cấu hình.
- **Không sử dụng phiên bản n8n cũ** (cần **n8n 1.30+**).
:::

---

### **2. Cấu Hình Cần Thay Đổi (BẮT BUỘC)**
Dưới đây là **danh sách các node quan trọng** cần cấu hình:

#### **🔹 Node 1: WH Receive Invoice Data (Webhook)**
- **Path**: Giả định là `pennylane-invoice` (không cần đổi).
- **HTTP Method**: `POST` (không đổi).
- **Lưu ý**: Sau khi import, **copy URL webhook** để gọi từ bên ngoài (ví dụ: từ Pipedrive, Brevo,...).

#### **🔹 Node 2: Code Validate Payload (Code)**
- **Không cần chỉnh sửa** (n8n sẽ tự kiểm tra dữ liệu đầu vào).
- **Yêu cầu dữ liệu đầu vào**:
  ```json
  {
    "customer_name": "Tên Khách Hàng",
    "customer_email": "email@khachhang.com",
    "items": [
      {"label": "Dịch vụ 1", "quantity": 1, "unit_price": 1000},
      {"label": "Dịch vụ 2", "quantity": 2, "unit_price": 500}
    ],
    "send_email": true/false,  // (Nếu true, hóa đơn sẽ được gửi qua email)
    "notification_email": "email@doanhnghiep.com"  // (Nếu muốn gửi thông báo qua Gmail)
  }
  ```
  *(Ví dụ chi tiết: [GitHub examples](https://github.com/Gauthier-Huguenin/n8n-pennylane-auto-invoicing/tree/main/examples))*

#### **🔹 Node 3 & 4: PL Search Customer / PL Create Customer (HTTP Request)**
- **Credentials**:
  - Tạo **Header Auth** với tên `Authorization` và giá trị `Bearer <YOUR_PENNYLANE_TOKEN>`.
  - *(Lấy token tại: [Pennylane API Settings](https://app.pennylane.fr/settings/api))*
- **Endpoint**:
  - **Search**: `GET /customers` (lọc bằng email).
  - **Create**: `POST /company_customers` (nếu khách hàng chưa có).

#### **🔹 Node 5: Set Customer ID (Set)**
- **Không cần chỉnh sửa**, n8n sẽ tự động lấy ID khách hàng từ Pennylane.

#### **🔹 Node 6: PL Create Invoice (HTTP Request)**
- **Credentials**: Sử dụng cùng **Header Auth** như trên.
- **Endpoint**: `POST /customer_invoices`.
- **Lưu ý**:
  - **Số tiền phải là string** (ví dụ: `"1500.00"`).
  - **Mã VAT**:
    - `FR_200` (20%)
    - `FR_100` (10%)
    - `FR_055` (5.5%)
    - `exempt` (miễn VAT)
  - **Thiết lập `draft: true`** nếu muốn tạo hóa đơn nhưng không gửi ngay.

#### **🔹 Node 7: IF Send Email (If)**
- **Điều kiện**: Nếu `send_email: true` trong payload.
- **Node 8: Wait PDF Generation (Wait)**
  - **Thời gian chờ**: 30 giây (để Pennylane tạo PDF).
- **Node 9: PL Send Invoice Email (HTTP Request)**
  - **Endpoint**: `POST /customer_invoices/{id}/send_by_email`.
  - **Lưu ý**: Nếu Pennylane chưa tạo PDF, sẽ trả về **409 Conflict**.

#### **🔹 Node 10: Code Build Notification (Code)**
- **Không cần chỉnh sửa**, n8n sẽ tự động tạo thông báo Slack/Gmail.

#### **🔹 Node 11: SL Send Notification (Slack)**
- **Credentials**:
  - Tạo **Slack OAuth2** và chọn **channel** muốn thông báo.
  - *(Hướng dẫn: [Slack API Setup](https://api.slack.com/apps))*
- **Lưu ý**: Nếu không muốn Slack, **xóa node này** và thay bằng Telegram/email khác.

#### **🔹 Node 12: IF Has Notification Email (If)**
- **Điều kiện**: Nếu `notification_email` có trong payload.
- **Node 13: GM Send Notification (Gmail)**
  - **Credentials**: Sử dụng **Gmail OAuth2**.
  - **Lưu ý**: Nếu không muốn Gmail, **xóa node này**.

#### **🔹 Node 14: Set Output Response (Set)**
- **Không cần chỉnh sửa**, n8n sẽ trả về phản hồi JSON cho webhook.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi **POST request** đến URL webhook với payload như ví dụ trên.
   - Kiểm tra **Slack/Gmail** xem có nhận được thông báo không.
2. **Bật Active**:
   - Nhấn **Active** trên workflow trong n8n Editor.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**CÁCH LÀM NÀY ĐỂ TIẾP CẬN HƠN**]
1. **Thêm Telegram Bot**:
   - Thay thế node Slack bằng **Telegram Bot** (n8n có node `telegram`).
   - Cấu hình tại: [Telegram Bot API](https://core.telegram.org/bots/api).

2. **Lưu Log Hóa Đơn**:
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu tất cả hóa đơn đã tạo.
   - *(Hướng dẫn: [n8n + Google Sheets](https://docs.n8n.io/integrations/built-in/nodes/n8n-nodes-base.googleSheets))*

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Trigger (Schedule)** để gửi báo cáo tổng hợp hóa đơn hàng tháng qua email.

4. **Tích Hợp Với Pipedrive**:
   - Khi deal trong Pipedrive được chuyển sang trạng thái "Closed Won", gọi webhook này để tự động tạo hóa đơn.

5. **Sử Dụng AI Tự Động Hoá**:
   - Thêm node **LLM (n8n-nodes-base.llm)** để tự động **tạo mô tả hóa đơn** từ dữ liệu sản phẩm.
:::

---
## 📌 **Kết Luận**
Workflow này **giải phóng hoàn toàn thời gian** của các sếp khỏi công việc thủ công tạo hóa đơn, đồng thời **giảm thiểu sai sót** và **cải thiện trải nghiệm khách hàng** bằng cách tự động gửi hóa đơn và thông báo. **Chỉ cần 10 phút để cấu hình**, sau đó workflow sẽ hoạt động **24/7** mà không cần can thiệp.

**Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình Pennylane, Slack/Gmail.
2. **Test với dữ liệu mẫu** và bắt đầu tự động hóa ngay.
3. **Tích hợp với CRM/form** của bạn để hoàn thiện hệ thống.

👉 **[Tải workflow ngay](https://n8n.io/workflows/15186)** và bắt đầu tự động hóa hóa đơn của mình!

---
:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**
:::

---
**Cần hỗ trợ?** Đừng ngần ngại comment bên dưới hoặc liên hệ với tác giả [Gauthier Huguenin](https://github.com/Gauthier-Huguenin) để có hướng dẫn chi tiết hơn! 🚀