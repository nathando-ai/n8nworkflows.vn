---
title: "🚀 Tự động làm giàu dữ liệu khách hàng HubSpot với ExactBuyer qua n8n"
description: "Hướng dẫn thiết lập workflow n8n tự động bổ sung thông tin liên hệ và công ty từ ExactBuyer ngay khi có contact mới trên HubSpot, giúp tối ưu hóa đội ngũ Sales và Marketing."
slug: "tu-dong-lam-giau-du-lieu-hubspot-exactbuyer"
tags: [n8n, automation, no-code, hubspot, exactbuyer, sales-automation, crm]
keywords: [n8n workflow, hubspot enrichment, exactbuyer api, tu dong hoa crm, lam giau du lieu khach hang]
---

# 🚀 Tự động làm giàu dữ liệu khách hàng HubSpot với ExactBuyer qua n8n

Trong quy trình Sales và Marketing hiện đại, việc sở hữu một profile khách hàng đầy đủ thông tin (số điện thoại, email, mạng xã hội, thông tin công ty...) là chìa khóa quyết định tỷ lệ chốt sale. Tuy nhiên, việc thủ công tra cứu từng khách hàng mới vừa tốn thời gian, vừa dễ bỏ sót.

Giải pháp là gì? Workflow n8n này sẽ tự động hóa 100% quy trình: Ngay khi có một contact mới được tạo trên HubSpot, hệ thống sẽ gọi API sang ExactBuyer để lấy toàn bộ thông tin chi tiết và tự động cập nhật ngược lại vào HubSpot. Đội ngũ của các sếp sẽ luôn có sẵn dữ liệu chất lượng cao mà không cần đụng tay vào bất kỳ thao tác thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Lập tức làm giàu dữ liệu (data enrichment) ngay khoảnh khắc contact vừa đổ về HubSpot.
- **Dữ liệu toàn diện:** Bổ sung chính xác profile mạng xã hội, số điện thoại, email mở rộng và thông tin định danh vị trí từ ExactBuyer.
- **Tiết kiệm thời gian cho Sales:** Nhân sự kinh doanh không còn mất thời gian tra cứu thủ công, tập trung 100% vào việc gọi điện và chốt đơn.
- **Cá nhân hóa chiến dịch Marketing:** Dữ liệu đầy đủ giúp phân nhóm khách hàng hiệu quả hơn bao giờ hết.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản HubSpot** với quyền Developer/Admin để cấu hình Trigger và API.
- **Tài khoản ExactBuyer** và khóa API (API Key) để gọi dịch vụ dữ liệu.
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy toàn bộ mã nguồn JSON của workflow này và paste trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node cốt lõi sau:

- **Node `On contact created` (HubSpot Trigger):**
  - Cần thiết lập `HubSpot Developer API` credentials.
  - **Lưu ý cực kỳ quan trọng:** Scopes cấp quyền cho App phải hoàn toàn khớp với tài liệu hướng dẫn chính thức của n8n cho HubSpot Trigger. Nếu thiếu scope, trigger sẽ không nhận được sự kiện contact mới.

- **Node `Get HubSpot contact` (HubSpot):**
  - Sử dụng thao tác `get` để lấy chi tiết thông tin contact vừa tạo.
  - Node này yêu cầu một bộ credentials `HubSpot OAuth2 API` riêng biệt (khác với credentials của Trigger ở bước trên). Chú ý cấp đúng scopes theo tài liệu n8n.

- **Node `Enrich user from ExactBuyer` (HTTP Request):**
  - Sử dụng phương thức xác thực `HTTP Header Auth` bằng API Key từ ExactBuyer.
  - Tham khảo tài liệu [ExactBuyer Contact Enrichment API](https://docs.exactbuyer.com/contact-enrichment/enrichment) để truyền đúng tham số định danh (thường là email của contact) vào body hoặc query của request.

- **Node `if found email` & `Set keys`:**
  - Kiểm tra xem ExactBuyer có trả về dữ liệu dựa trên email hay không. Nếu tìm thấy, workflow sẽ tiếp tục tiến trình chuẩn hóa dữ liệu. Nếu không, luồng sẽ chuyển sang nhánh `Could not find user` (NoOp) để kết thúc an toàn.

- **Node `Update contact from Hubspot` (HubSpot):**
  - Sử dụng chung credentials OAuth2 với node lấy contact (`Get HubSpot contact`).
  - Mapping các trường dữ liệu trả về từ ExactBuyer (như số điện thoại, công ty, vị trí, mạng xã hội) vào đúng các trường tương ứng trên HubSpot CRM.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một email contact mẫu trên HubSpot để kiểm tra xem ExactBuyer có trả về đúng dữ liệu không.
- Kiểm tra kết quả trên HubSpot xem contact đã được cập nhật đầy đủ chưa.
- Sau khi test thành công, gạt công tắc sang chế độ **Active** để hệ thống tự động chạy 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm kênh thông báo:** Kết nối thêm một node Telegram hoặc Slack ở nhánh `Could not find user` để đội ngũ sales biết khi nào một contact mới không thể tìm thấy thông tin trên ExactBuyer.
- **Lưu trữ Log:** Ghi lại lịch sử làm giàu dữ liệu vào Google Sheets hoặc cơ sở dữ liệu nội bộ để theo dõi tỷ lệ thành công (Enrichment Rate).
- **Xử lý Rate Limit:** Nếu số lượng contact tạo mới quá lớn, hãy cấu hình thêm tính năng Retry hoặc Error Handling trong n8n để tránh bị chặn API từ phía ExactBuyer.

---

### 📌 Kết luận
Việc tự động hóa quy trình làm giàu dữ liệu khách hàng từ HubSpot qua ExactBuyer không chỉ giúp tiết kiệm hàng giờ thao tác thủ công mỗi ngày mà còn đảm bảo dữ liệu CRM của các sếp luôn sạch, sâu và sẵn sàng cho mọi chiến dịch chuyển đổi. Áp dụng ngay hôm nay để tối ưu hóa năng suất đội ngũ Sales của mình nhé!