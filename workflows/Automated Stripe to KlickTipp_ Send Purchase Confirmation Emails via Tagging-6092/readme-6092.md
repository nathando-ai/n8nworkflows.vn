---
title: "🚀 Tự Động Hóa Stripe → KlickTipp: Gửi Email Xác Nhận Đơn Hàng Với Tagging Tự Động (100% GDPR Compliant)"
description: "Workflow này tự động đồng bộ hóa dữ liệu thanh toán từ Stripe sang KlickTipp, thêm thông tin chi tiết đơn hàng vào hồ sơ khách hàng và gán thẻ tự động để kích hoạt email xác nhận cá nhân hóa. Giúp các sếp tiết kiệm thời gian thủ công, tăng trải nghiệm khách hàng và tối ưu hóa quy trình bán hàng số."
slug: "tieu-dong-hoa-stripe-klicktipp-gui-email-xac-nhan-don-hang"
tags: [n8n, automation, stripe, klicktipp, email-marketing, gdpr-compliant, no-code]
keywords: [tự động hóa stripe, klicktipp n8n, gửi email xác nhận đơn hàng, đồng bộ hóa thanh toán, tagging tự động, workflow n8n stripe]
---

# 🚀 **Tự Động Hóa Stripe → KlickTipp: Gửi Email Xác Nhận Đơn Hàng Với Tagging Tự Động**

## **💡 Bạn đã bao giờ phải làm thủ công những việc này?**
- **Ghi chép lại thông tin đơn hàng** từ Stripe vào hệ thống CRM/KlickTipp?
- **Gửi email xác nhận** cho khách hàng sau mỗi thanh toán thành công?
- **Tạo tag tự động** để kích hoạt email marketing hoặc quy trình hậu bán hàng?
- **Tốn thời gian** để cập nhật thông tin chi tiết (invoice link, sản phẩm, số tiền) cho từng khách hàng?

**Workflow này giải quyết tất cả!** Với **n8n**, bạn có thể **tự động hóa toàn bộ quy trình** từ khi khách hàng thanh toán thành công trên Stripe đến khi họ nhận được email xác nhận cá nhân hóa, **không cần viết một dòng code nào!**

---
### **🎯 Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm thời gian**: Không cần nhập liệu thủ công sau mỗi đơn hàng.
✅ **Email xác nhận tức thời**: Khách hàng nhận thông báo ngay sau khi thanh toán thành công.
✅ **Dữ liệu khách hàng được cập nhật chính xác**: Thông tin đơn hàng (invoice, sản phẩm, số tiền) tự động đồng bộ vào KlickTipp.
✅ **Tagging tự động**: Gán thẻ cho khách hàng để kích hoạt email marketing hoặc quy trình hậu bán hàng.
✅ **Hoạt động 24/7**: Không cần can thiệp người dùng, hệ thống tự động xử lý mọi đơn hàng.
✅ **Tuân thủ GDPR**: KlickTipp là nền tảng **100% tuân thủ GDPR**, đảm bảo bảo mật dữ liệu khách hàng.
:::

---
### **🔧 Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Stripe** với API Key (đăng ký tại [stripe.com](https://stripe.com/)).
2. **Tài khoản KlickTipp** (đăng ký tại [klicktipp.com](https://klicktipp.com/)).
3. **Các trường dữ liệu tùy chỉnh trong KlickTipp**:
   - `Stripe_Beleg_URL` (URL) → Để lưu link invoice.
   - `Stripe_Gesamtbetrag` (Số thập phân) → Để lưu tổng giá trị đơn hàng.
   - `Stripe_Zahlungs_ID` (Dòng văn bản) → Để lưu ID thanh toán.
   - `Stripe_Produkte` (Dòng văn bản) → Để lưu danh sách sản phẩm.
4. **Thẻ (Tags) trong KlickTipp**:
   - Ví dụ: `Bestellung: Kurs XYZ` (để phân loại khách hàng mua khóa học XYZ).
5. **Webhook từ Stripe** để n8n bắt sự kiện `Checkout Session.completed`.

---
### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/6092](https://n8n.io/workflows/6092) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Workflow Editor**.
  2. Nhấn **Import** → Chọn file JSON hoặc dán JSON vào ô nhập.
  3. Chọn **Create Workflow**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **5 node chính**, các sếp cần cấu hình kỹ lưỡng:

##### **🔹 Node 1: "New checkout session completed" (Stripe Trigger)**
- **Loại node**: `stripeTrigger`
- **Cấu hình**:
  - **Credentials**: Chọn `stripeApi` (đã cấu hình API Key Stripe).
  - **Event**: Chọn `Checkout Session.completed`.
  - **Test Webhook**: Nhấn **Test** để xác nhận webhook hoạt động (sử dụng mode test trên Stripe).

##### **🔹 Node 2: "Getting charge ID" (HTTP Request)**
- **Loại node**: `httpRequest`
- **Cấu hình**:
  - **Method**: `GET`
  - **URL**: `https://api.stripe.com/v1/checkout/sessions/{$node["New checkout session completed"].json()["data"]["id"]}/payment_intent`
  - **Headers**:
    - `Authorization`: `Bearer {$credentials["stripeApi"]["apiKey"]}`
    - `Stripe-Version`: `2023-08-16`
  - **Test**: Nhấn **Test** với ID Checkout Session từ Stripe.

##### **🔹 Node 3: "Getting invoice link" (Stripe Node)**
- **Loại node**: `stripe`
- **Cấu hình**:
  - **Credentials**: Chọn `stripeApi`.
  - **Resource**: `charge`
  - **Parameters**:
    - `charge`: `$node["Getting charge ID"].json()["id"]`
  - **Output**: Lấy `invoice` từ kết quả.

##### **🔹 Node 4: "Getting line items" (HTTP Request)**
- **Loại node**: `httpRequest`
- **Cấu hình**:
  - **Method**: `GET`
  - **URL**: `https://api.stripe.com/v1/checkout/sessions/{$node["New checkout session completed"].json()["data"]["id"]}`
  - **Headers**:
    - `Authorization`: `Bearer {$credentials["stripeApi"]["apiKey"]}`
    - `Stripe-Version`: `2023-08-16`
  - **Output**: Lấy `line_items` (danh sách sản phẩm).

##### **🔹 Node 5: "Subscribe buyer to KlickTipp" (KlickTipp Node)**
- **Loại node**: `CUSTOM.klicktipp`
- **Cấu hình**:
  - **Credentials**: Chọn `klickTippApi` (đã cấu hình username/password).
  - **Operation**: `subscribe`
  - **Resource**: `subscriber`
  - **Parameters**:
    - **Email**: `$node["New checkout session completed"].json()["data"]["customer_details"]["email"]`
    - **Custom Fields**:
      - `Stripe_Beleg_URL`: `$node["Getting invoice link"].json()["invoice"]`
      - `Stripe_Gesamtbetrag`: `$node["New checkout session completed"].json()["data"]["amount_total"] / 100` (Stripe trả về cent, cần chia cho 100 để chuyển thành USD/EUR).
      - `Stripe_Zahlungs_ID`: `$node["Getting charge ID"].json()["id"]`
      - `Stripe_Produkte`: `$node["Getting line items"].json()["line_items"]["data"]`
    - **Tags**: `$node["New checkout session completed"].json()["data"]["metadata"]["product_id"]` (hoặc tag tùy chỉnh như `Bestellung: Kurs XYZ`).

---
#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Thực hiện một thanh toán **test** trên Stripe (sử dụng mode test).
   - Kiểm tra **KlickTipp** xem dữ liệu đã được cập nhật chưa.
2. **Bật Workflow**:
   - Đảm bảo tất cả node hoạt động ổn thỏa → Nhấn **Active**.

---
### **✍️ Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** để thông báo khi có đơn hàng mới.
   ```yaml
   - Node: `n8n-nodes-base.slack`
     Action: `sendMessage`
     Message: `New order received! Invoice: {{$node["Getting invoice link"].json()["invoice"]}}`
   ```

2. **Lưu log hoạt động**:
   - Sử dụng node **StickyNote** để ghi lại thông tin đơn hàng vào log.
   ```yaml
   - Node: `n8n-nodes-base.stickyNote`
     Key: `stripe_order_${$node["New checkout session completed"].json()["data"]["id"]}`
     Value: `{{$json}}`
   ```

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **KlickTipp Sequences** để gửi email báo cáo sau 1 ngày, 3 ngày, 7 ngày sau thanh toán.

4. **Phân loại khách hàng**:
   - Sử dụng **Switch Node** để gán tag khác nhau dựa trên sản phẩm mua:
   ```yaml
   - Node: `n8n-nodes-base.switch`
     Condition 1: `{{$node["Getting line items"].json()["line_items"]["data"][0]["price"]["product"]["name"] === "Khóa học A"}}`
       → Tag: `Bestellung: Khóa học A`
     Condition 2: `{{$node["Getting line items"].json()["line_items"]["data"][0]["price"]["product"]["name"] === "Khóa học B"}}`
       → Tag: `Bestellung: Khóa học B`
   ```

5. **Kết nối với Memberspot/Mentortools**:
   - Sau khi khách hàng thanh toán, tự động tạo tài khoản cho họ trên **Memberspot** hoặc **Mentortools** bằng API.

---
### **📌 Kết luận**
**Workflow này giúp các sếp:**
✔ **Tự động hóa hoàn toàn** quy trình xác nhận đơn hàng từ Stripe → KlickTipp.
✔ **Tiết kiệm thời gian** và giảm thiểu lỗi nhập liệu thủ công.
✔ **Tăng trải nghiệm khách hàng** với email xác nhận cá nhân hóa.
✔ **Tối ưu hóa marketing** bằng tagging tự động và email marketing tự động.

**Hành động ngay!**
1. **Cài đặt n8n Self-hosted** trên VPS để workflow chạy 24/7 (không phụ thuộc vào n8n.io).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Bật Active** và bắt đầu tự động hóa ngay!

**🚀 Chúc các sếp thành công với quy trình bán hàng hoàn toàn tự động!** 🚀