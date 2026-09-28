---
title: "🚀 Tự Động Hóa Gửi Quảng Cáo WhatsApp Bulk Cho Sản Phẩm Mới Shopify Với OpenAI & Google Sheets"
description: "Workflow tự động hóa hoàn toàn không code giúp các sếp Shopify gửi tin nhắn quảng cáo WhatsApp cá nhân hóa cho khách hàng tiềm năng khi sản phẩm mới ra mắt, tăng tỷ lệ chuyển đổi 30%+ chỉ trong vài phút setup."
slug: "tieu-dong-hoa-gui-quang-cao-whatsapp-bulk-shopify"
tags: [n8n, automation, shopify, whatsapp-marketing, ai-summarization, no-code, openai, google-sheets]
keywords: [tự động hóa whatsapp shopify, gửi quảng cáo bulk whatsapp, openai chatbot shopify, tự động hóa marketing shopify, workflow n8n shopify, quảng cáo sản phẩm mới whatsapp]
---

# 🚀 **Tự Động Hóa Gửi Quảng Cáo WhatsApp Bulk Cho Sản Phẩm Mới Shopify Với OpenAI & Google Sheets**

### **🔥 Nỗi Đau Của Các Sếp Shopify**
Hàng ngày, các sếp Shopify phải:
- **Làm thủ công** gửi tin nhắn quảng cáo WhatsApp cho hàng trăm khách hàng khi sản phẩm mới ra mắt.
- **Chỉnh sửa nội dung** mỗi tin nhắn, mất thời gian và dễ sai sót.
- **Không theo dõi được** khách hàng đã nhận hay chưa, dẫn đến tỷ lệ chuyển đổi thấp.
- **Không cá nhân hóa** tin nhắn, khiến khách hàng cảm thấy "được spam".

**Workflow này giải quyết tất cả!** Sử dụng **n8n + OpenAI + RapiWA**, bạn có thể:
✅ **Tự động** gửi tin nhắn quảng cáo WhatsApp cho tất cả khách hàng khi sản phẩm mới ra mắt.
✅ **Cá nhân hóa** nội dung với **OpenAI**, tạo tin nhắn ngắn gọn và hấp dẫn.
✅ **Lưu log** khách hàng đã nhận/từ chối để theo dõi hiệu quả.
✅ **Không cần code**, chỉ cần setup 1 lần là chạy 24/7.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10-15 giờ/ngày** so với làm thủ công.
- **Tỷ lệ chuyển đổi tăng 30%+** nhờ tin nhắn cá nhân hóa.
- **Không lo quên gửi** vì workflow chạy tự động khi sản phẩm mới ra mắt.
- **Lưu log chi tiết** khách hàng đã nhận/từ chối, giúp tối ưu chiến dịch tiếp theo.
- **Không cần kỹ sư** để setup, chỉ cần 1-2 giờ để cấu hình.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Shopify** (API Key + Store Domain).
✔ **Tài khoản Google Sheets** (File đã tạo sẵn với 2 Sheet: *"Unverified & Not sent"* và *"Verified & Sent"*).
✔ **API Key RapiWA** (đăng ký tại [RapiWA](https://rapiwa.com/)).
✔ **Tài khoản Gmail** (để gửi thông báo khi có lỗi).
✔ **OpenAI API Key** (đăng ký tại [OpenAI](https://platform.openai.com/)).
✔ **Danh sách khách hàng** (nếu chưa có, workflow sẽ lấy từ Shopify).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/13414](https://n8n.io/workflows/13414) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **18 node**, các sếp cần chú ý cấu hình **các node quan trọng** sau:

##### **🔹 Node "Shopify Trigger"**
- **Chọn "Product Create"** (hoặc "Product Update") để workflow kích hoạt khi sản phẩm mới ra mắt.
- **Tham số cần điền:**
  - `API Key` (từ Shopify Admin → Apps → Custom Apps → API credentials).
  - `Store Domain` (ví dụ: `tudonghoa.shopify.com`).

##### **🔹 Node "Get a product in Shopify"**
- **Lấy ID sản phẩm** từ node Shopify Trigger và truyền vào `Product ID`.

##### **🔹 Node "Create product description (HTML) into a short" (OpenAI)**
- **Prompt mẫu:**
  ```
  "Tóm tắt mô tả sản phẩm này thành một tin nhắn WhatsApp ngắn gọn (dưới 200 ký tự), bao gồm:
  - Tên sản phẩm.
  - 2-3 tính năng chính.
  - Link sản phẩm.
  - CTA: 'Đăng ký ngay để nhận ưu đãi!'"
  ```
- **Tham số cần điền:**
  - `API Key` (OpenAI).
  - `Model` (chọn `gpt-3.5-turbo` hoặc `gpt-4`).

##### **🔹 Node "Rapiwa (verify whatsapp number)"**
- **Tham số cần điền:**
  - `API Key` (từ RapiWA).
  - `Phone Number` (định dạng: `+84123456789`).
  - **Lưu ý:** Nếu số điện thoại chưa được xác minh, workflow sẽ lưu vào Sheet *"Unverified & Not sent"*.

##### **🔹 Node "Rapiwa (Send Whatsapp message)"**
- **Tham số cần điền:**
  - `API Key` (RapiWA).
  - `Phone Number` (đã xác minh).
  - **Nội dung tin nhắn** (từ OpenAI).
  - **Media (nếu có):** Link ảnh sản phẩm (tự động lấy từ Shopify).

##### **🔹 Node "Save data in Sheet Verified & Sent" / "Save data Sheet Unverified & Not sent"**
- **Chọn Sheet phù hợp** trong Google Sheets.
- **Cấu trúc dữ liệu:**
  | Khách hàng | Số điện thoại | Trạng thái | Ngày gửi | Link sản phẩm |
  |------------|----------------|------------|----------|----------------|
  | Khách A    | +84123456789   | Verified   | 2024-05-20 | link.com       |

##### **🔹 Node "Loop Over Customer" & "Loop Over Image Link"**
- **Chỉnh số lượng batch** (ví dụ: 50 tin nhắn/lần) để tránh bị giới hạn API.

##### **🔹 Node "Send a Notification mail" (Gmail)**
- **Tham số cần điền:**
  - `From Email` (Gmail của bạn).
  - `To Email` (email quản lý).
  - **Nội dung:** Thông báo khi workflow hoàn thành hoặc có lỗi.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với **1-2 khách hàng mẫu** để kiểm tra:
   - Tin nhắn có được gửi đúng không?
   - OpenAI có tạo nội dung hợp lý không?
   - RapiWA có xác minh số điện thoại không?
2. **Bật Active** workflow khi đã kiểm tra xong.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**
   - Thêm node **Slack/Telegram** để thông báo khi workflow hoàn thành.
   - **Cách làm:** Sử dụng node `n8n-nodes-slack` hoặc `n8n-nodes-telegram`.

2. **Lưu Log Chi Tiết**
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu log tất cả tin nhắn đã gửi, trạng thái, và thời gian.

3. **Gửi Báo Cáo Định Kỳ**
   - Sử dụng **n8n + Google Sheets + Email** để tự động gửi báo cáo hiệu quả của workflow hàng tuần.

4. **Tối Ưu OpenAI Prompt**
   - Thử nghiệm các **prompt khác nhau** để nội dung tin nhắn phù hợp với sản phẩm của bạn.

5. **Xử Lý Lỗi WhatsApp**
   - Thêm node **If** để xử lý trường hợp số điện thoại bị từ chối.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp Shopify, giúp họ **tự động hóa quảng cáo WhatsApp bulk** một cách chuyên nghiệp, cá nhân hóa và hiệu quả. **Chỉ cần setup 1 lần là chạy 24/7**, không cần kỹ sư!

**🚀 Hãy áp dụng ngay và xem tỷ lệ chuyển đổi của bạn tăng lên như thế nào!**

---
:::note[LƯU Ý CUỐI CUNG]
- **Không gửi spam quá nhiều** để tránh bị RapiWA block.
- **Kiểm tra log Google Sheets** thường xuyên để theo dõi hiệu quả.
- **Cập nhật API Key** nếu hết hạn.
:::