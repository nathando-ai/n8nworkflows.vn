---
title: "🚀 Tự động tạo khách hàng QuickBooks Online & Phiếu bán khi nhận thanh toán Stripe"
description: "Giải pháp tự động 100% không cần code: khi Stripe nhận thanh toán mới, QuickBooks Online sẽ tự động tạo khách hàng và ghi nhận phiếu bán, giúp doanh nghiệp tiết kiệm thời gian và giảm sai sót."
slug: "tuy-chinh-tao-khach-hang-quickbooks-online-khi-nhan-thanh-toan-stripe"
tags: [n8n, automation, no-code, finance, quickbooks, stripe]
keywords: [n8n workflow, tự động hóa, QuickBooks, Stripe, sales receipt]
---

# 🚀 Tự động tạo khách hàng QuickBooks Online & Phiếu bán khi nhận thanh toán Stripe

Bạn đang phải nhập dữ liệu thủ công vào QuickBooks mỗi khi có giao dịch mới từ Stripe? Việc này không chỉ tốn thời gian mà còn dễ dẫn đến lỗi khi sao chép dữ liệu. Workflow **Create QuickBooks Online Customers With Sales Receipts For New Stripe Payments** của Artur giúp bạn tự động:

- Kiểm tra khách hàng Stripe đã tồn tại trong QuickBooks chưa.
- Nếu chưa, tạo khách hàng mới trong QuickBooks.
- Ghi nhận phiếu bán (Sales Receipt) dựa trên thông tin thanh toán Stripe.
- Hoàn toàn không cần viết code, chỉ cần cấu hình một vài credential.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhập dữ liệu thủ công, giảm 90% công việc lặp đi lặp lại.
- **Chính xác hơn**: Dữ liệu được đồng bộ ngay lập tức, tránh sai sót khi chuyển đổi giữa Stripe và QuickBooks.
- **Cá nhân hóa**: Tự động tạo khách hàng với thông tin đầy đủ (email, tên, địa chỉ) từ Stripe.
- **Hoạt động liên tục**: Workflow chạy 24/7, ngay khi Stripe nhận thanh toán mới.
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
| Dịch vụ | Credential cần thiết | Mô tả |
|---------|----------------------|-------|
| **Stripe** | `stripeApi` | API Key (Publishable & Secret) lấy từ Dashboard Stripe. |
| **QuickBooks Online** | `quickBooksOAuth2Api` | Client ID, Client Secret, Redirect URI (đăng ký ứng dụng QuickBooks Developer). |
| **QuickBooks API (GET)** | `httpCustomAuth` | Custom Auth (OAuth2) để truy cập endpoint lấy khách hàng. |
| **n8n** | - | Đăng ký tài khoản n8n (Self-hosted hoặc n8n.cloud). |

> **Lưu ý**: Đảm bảo các credential được lưu trong **Credentials** của n8n và được gán đúng node.

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Truy cập link gốc: <https://n8n.io/workflows/2807>.
2. Nhấn **Export** → **Download JSON**.
3. Trong n8n Editor, chọn **Import** → **Upload JSON** và tải file vừa tải về.

> Bạn cũng có thể copy toàn bộ JSON và dán vào ô **Import**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên node | Cấu hình chính | Credential | Tham số cần điền |
|------|----------|-----------------|------------|------------------|
| 1 | `New Payment` | Stripe Trigger | `stripeApi` | - |
| 2 | `Get Stripe Customer` | Lấy thông tin khách hàng Stripe | `stripeApi` | `resource: customer` |
| 3 | `If Customer Exists` | Kiểm tra tồn tại QuickBooks | - | `{{ $json["quickbooksCustomerId"] }}` |
| 4 | `Use Stripe Customer` | Merge dữ liệu Stripe | - | - |
| 5 | `Create QuickBooks Customer` | Tạo khách hàng mới | `quickBooksOAuth2Api` | `operation: create` |
| 6 | `GET Quickbooks Customer` | Lấy khách hàng QuickBooks | `httpCustomAuth`, `quickBooksOAuth2Api` | `customerId` từ node trước |
| 7 | `Merge Stripe and QuickBooks Data` | Kết hợp dữ liệu | - | - |
| 8 | `Merge Payment and QuickBooks Customer` | Kết hợp thanh toán + khách hàng | - | - |
| 9 | `POST Sales Receipt To QuickBooks` | Gửi phiếu bán | `quickBooksOAuth2Api` | `operation: create` |
| 10 | `POST Sales Receipt` | (Duplicate, có thể bỏ qua) | `quickBooksOAuth2Api` | - |

#### Cấu hình chi tiết từng node
- **Stripe Trigger**: Chọn **Event** = `payment_intent.succeeded`. Đặt **Webhook URL** (n8n sẽ tự tạo).
- **Get Stripe Customer**: Truyền `customer` ID từ payload của trigger (`$json["data"]["object"]["customer"]`).
- **If Customer Exists**: Sử dụng biểu thức `{{ $json["quickbooksCustomerId"] !== undefined }}` để kiểm tra.
- **Create QuickBooks Customer**: Chọn **Customer** object, điền fields: `DisplayName`, `PrimaryEmailAddr`, `BillAddr`, v.v. (sử dụng dữ liệu từ Stripe).
- **GET Quickbooks Customer**: Đặt URL: `https://sandbox-quickbooks.api.intuit.com/v3/company/{{ $json["companyId"] }}/customer/{{ $json["quickbooksCustomerId"] }}`.
- **POST Sales Receipt To QuickBooks**: Đặt body JSON theo schema của QuickBooks Sales Receipt, bao gồm `CustomerRef`, `Line`, `TotalAmt`, v.v.

> **Tip**: Sử dụng **Set** node trước khi gửi HTTP Request để chuẩn bị payload.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (bấm **Execute Workflow**).
2. Kiểm tra log: Đảm bảo không có lỗi, khách hàng được tạo và phiếu bán được ghi nhận.
3. Bật **Active**: Đánh dấu workflow là “Active” để nó tự động chạy khi có webhook mới.

## ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack**: Thêm node `Slack` sau khi tạo Sales Receipt để gửi tin nhắn thông báo cho team bán hàng.
- **Lưu log vào Google Sheet**: Sử dụng node `Google Sheets` để ghi lại mọi giao dịch, giúp theo dõi lịch sử.
- **Gửi email xác nhận**: Thêm node `Email` để gửi email cho khách hàng khi phiếu bán được tạo.
- **Định kỳ báo cáo**: Sử dụng node `Cron` để gửi báo cáo doanh thu hàng ngày/tuần tới QuickBooks hoặc email.

## 📌 Kết luận
Workflow này giúp bạn **tự động hóa hoàn toàn** quy trình nhập dữ liệu từ Stripe sang QuickBooks Online, giảm thiểu sai sót và tiết kiệm thời gian. Hãy thử ngay, cài đặt credential, import workflow và bật “Active” – bạn sẽ thấy công việc kế toán của mình trở nên nhẹ nhàng hơn bao giờ hết. Nếu cần hỗ trợ, đừng ngần ngại liên hệ với cộng đồng n8n hoặc đặt câu hỏi tại diễn đàn. Chúc các sếp thành công!