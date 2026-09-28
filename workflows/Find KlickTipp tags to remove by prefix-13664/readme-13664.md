---
title: "🚀 Tự Động Lọc Và Xác Định Thẻ KlickTipp Cần Xóa Theo Tiền Tố (Prefix) với n8n"
description: "Hướng dẫn xây dựng sub-workflow n8n giúp tự động so sánh và tìm ra các thẻ (tags) KlickTipp cần gỡ bỏ dựa theo tiền tố và danh sách thẻ cần giữ lại."
slug: "tim-va-loc-the-klicktipp-can-xoa-theo-tien-to-n8n"
tags: [n8n, automation, no-code, klicktipp, crm, marketing-automation]
keywords: [n8n workflow, klicktipp tags, tu dong hoa crm, quan ly tag klicktipp, n8n sub workflow]
---

# 🚀 Tự Động Lọc Và Xác Định Thẻ KlickTipp Cần Xóa Theo Tiền Tố (Prefix) với n8n

Các sếp làm marketing chắc hẳn đều đau đầu khi đồng bộ dữ liệu khách hàng từ các hệ thống bên thứ ba (như CRM, hệ thống webinar,...) về KlickTipp. Việc các thẻ (tags) cũ cứ tích tụ dần, không được dọn dẹp theo đúng ngữ cảnh hay tiền tố (prefix) quản lý sẽ làm tài khoản CRM trở nên lộn xộn, gây sai lệch trong các chiến dịch automation tiếp theo.

Giải pháp thủ công kiểm tra và gỡ bỏ từng thẻ là cực hình và tốn thời gian. Workflow n8n này sinh ra để giải quyết triệt để bài toán đó: tự động hóa 100% quy trình đối chiếu, so sánh và trả về danh sách các thẻ cần gỡ bỏ dựa trên tiền tố quản lý.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và đồng bộ CRM mượt mà, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Không cần thủ công kiểm tra xem contact đang dính thẻ nào cũ cần dọn dẹp.
- **Chính xác tuyệt đối:** Thuật toán so sánh dựa trên tiền tố (`prefix`) và danh sách nguồn chân lý (`source of truth`) đảm bảo không xóa nhầm thẻ quan trọng.
- **Tối ưu Sub-workflow:** Thiết kế dưới dạng sub-workflow, dễ dàng gọi từ bất kỳ luồng xử lý contact chính nào.
- **Hoạt động 24/7:** Chạy ngầm liên tục, giữ cho hệ thống KlickTipp của các sếp luôn sạch sẽ, gọn gàng.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **KlickTipp Account & API Credentials:** Để kết nối node `List all tags` lấy danh sách thẻ hiện tại trên hệ thống.
- **Dữ liệu đầu vào (Trigger):** Cần cung cấp 2 tham số chính:
  - `prefix` (chuỗi tiền tố, ví dụ: `Zoho |`)
  - `setTags[]` (mảng danh sách các thẻ cần giữ lại từ hệ thống bên thứ ba).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp tải file JSON của workflow từ n8n.io (Link: `https://n8n.io/workflows/13664`).
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc Paste trực tiếp mã JSON vào).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 8 nodes chính hoạt động nhịp nhàng:
- **`Input: Prefix + Tags to keep` (Execute Workflow Trigger):** Nhận dữ liệu đầu vào từ workflow cha truyền xuống. Các sếp cần đảm bảo workflow cha truyền đúng cấu trúc biến `prefix` và `setTags[]`.
- **`List all tags` (KlickTipp Node):** Node này gọi API của KlickTipp để lấy toàn bộ danh sách thẻ. Các sếp cần tạo và chọn đúng **KlickTipp API Credentials** tại đây.
- **`Keep only tags with prefix` (Filter Node):** Lọc ra các thẻ trên KlickTipp có tên bắt đầu bằng `prefix` được truyền vào (ví dụ: chỉ quét các thẻ bắt đầu bằng `Zoho |`).
- **`Split prefixed tags` & `Build prefixed tag names` (SplitOut & Set Nodes):** Xử lý mảng thẻ cần giữ (`setTags[]`) và chuẩn hóa lại tên thẻ theo đúng định dạng tiền tố để so sánh công bằng.
- **`Match keep vs all tags` & `Collect tags to remove` (Merge & Aggregate Nodes):** Thực hiện phép toán đối chiếu: Lấy toàn bộ thẻ thuộc phạm vi tiền tố trên KlickTipp trừ đi danh sách thẻ cần giữ, từ đó gom lại thành mảng duy nhất `tagNamesToRemove[]`.
- **`Set tagNamesToRemove` (Set Node):** Đóng gói kết quả cuối cùng để trả về cho workflow gọi nó.

#### 3. Kích hoạt ⚡️
- Tạo một workflow test để truyền thử dữ liệu mẫu (`prefix: "Zoho |"`, `setTags: ["Webinar", "Newsletter"]`) vào sub-workflow này và chạy thử (Test Step).
- Kiểm tra kết quả đầu ra xem mảng `tagNamesToRemove[]` đã trả về chính xác các thẻ thừa chưa.
- Sau khi test thành công, lưu lại và sử dụng trong hệ thống automation chính.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp workflow gỡ thẻ thực tế:** Sub-workflow này chỉ *tính toán* ra danh sách cần xóa. Các sếp nên tạo thêm một workflow phía sau nhận mảng `tagNamesToRemove[]` này và dùng KlickTipp node để thực hiện hành động gỡ thẻ (`Remove Tag from Contact`) hàng loạt.
- **Thêm bước Log/Notification:** Gắn thêm node Telegram hoặc Slack vào cuối để bắn thông báo mỗi khi có quá nhiều thẻ cũ được dọn dẹp, giúp team theo dõi sát sao biến động dữ liệu.
- **Lên lịch chạy định kỳ (Cron):** Có thể kết hợp Schedule Trigger để dọn dẹp định kỳ hàng tuần cho toàn bộ danh sách khách hàng trong hệ thống.

### 📌 Kết luận
Việc tự động hóa quản lý thẻ trên CRM như KlickTipp giúp tiết kiệm hàng tá giờ làm việc thủ công và giữ cho data luôn sạch sẽ, chuẩn chỉnh. Hãy áp dụng ngay workflow này vào hệ thống của các sếp để tối ưu hóa quy trình marketing automation ngay hôm nay!