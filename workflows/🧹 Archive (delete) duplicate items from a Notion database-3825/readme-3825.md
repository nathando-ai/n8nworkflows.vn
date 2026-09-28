---
title: "🧹 Tự động dọn dẹp dữ liệu trùng lặp trong Notion Database với n8n"
description: "Workflow n8n tự động phát hiện và archive (xóa) các bản ghi trùng lặp trong Notion Database dựa trên một property tùy chọn, giữ lại duy nhất 1 bản ghi sạch sẽ."
slug: "tu-dong-xoa-duplicate-notion-database-n8n"
tags: [n8n, automation, no-code, notion, database, it-ops, cleanup]
keywords: [n8n workflow, tự động hóa, xóa trùng lặp notion, notion database, archive duplicate, dọn dẹp dữ liệu]
---

# 🧹 Tự động dọn dẹp dữ liệu trùng lặp trong Notion Database với n8n

Các sếp có bao giờ mở Notion Database lên và "choáng" vì hàng trăm dòng dữ liệu trùng lặp không? Khách hàng bị nhập 2-3 lần, đơn hàng bị ghi lại nhiều bản, hay form đăng ký bị submit lặp do người dùng bấm nút nhiều lần? Việc ngồi lọc thủ công từng dòng một không chỉ tốn thời gian mà còn dễ sai sót, đặc biệt khi database có hàng nghìn bản ghi.

Workflow này chính là "cây chổi thần" cho Notion của các sếp: nó tự động quét toàn bộ database, phát hiện các bản ghi trùng lặp dựa trên một property mà các sếp chỉ định (ví dụ: Email, Số điện thoại, Mã đơn hàng...), và **archive** (tương đương xóa) các bản ghi dư thừa — chỉ giữ lại duy nhất 1 bản ghi sạch. Toàn bộ quá trình diễn ra tự động 100%, không cần viết code, không cần ngồi "lọc tay" mệt mỏi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm hàng giờ đồng hồ**: Không còn phải ngồi lọc tay từng dòng trùng lặp trong Notion, đặc biệt với database lớn.
- **Chính xác tuyệt đối**: Thuật toán so sánh dựa trên property chỉ định, loại bỏ hoàn toàn yếu tố "người nhập sai".
- **Linh hoạt 2 chế độ kích hoạt**: Tự động chạy mỗi khi có page mới được thêm vào, hoặc chạy định kỳ hàng ngày theo lịch.
- **An toàn dữ liệu**: Dùng thao tác "Archive" thay vì xóa vĩnh viễn — các sếp vẫn có thể khôi phục từ thùng rác Notion nếu cần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Notion** có quyền truy cập vào database cần dọn dẹp (quyền Edit/Update).
- **Notion Integration Token** (Internal Integration) đã được share với database mục tiêu. Các sếp tạo tại [notion.so/my-integrations](https://www.notion.so/my-integrations).
- **n8n instance** đang chạy (self-hosted hoặc cloud).
- **Xác định trước property dùng để check trùng** (ví dụ: `Email`, `Phone`, `Order ID`...) — đây là "chìa khóa" để workflow hoạt động đúng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import theo 2 cách:
- **Cách 1 (từ file JSON)**: Tải file JSON của workflow về máy → Mở n8n Editor → Menu **Workflows** → **Import from File** → chọn file JSON vừa tải.
- **Cách 2 (copy/paste)**: Mở n8n Editor → Nhấn `Ctrl + V` (hoặc `Cmd + V` trên Mac) trực tiếp vào canvas sau khi copy nội dung JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Workflow gồm 7 nodes, trong đó có **3 node quan trọng** các sếp bắt buộc phải cấu hình:

**🔹 Node `Get pages from database` (Notion)**
- Chọn **Credential Notion** vừa tạo ở bước chuẩn bị.
- Chọn **Database** cần dọn dẹp trùng lặp từ dropdown.
- Giữ nguyên operation `Get All` / resource `Database Page`.

**🔹 Node `Format items properly` (Set)**
- Đây là node "linh hồn" của workflow. Các sếp cần **kéo-thả property** muốn check trùng từ panel bên trái vào field có tên `property_to_check`.
- Ví dụ: Nếu muốn xóa trùng theo Email → kéo field `Email` vào `property_to_check`.
- 💡 **Mẹo**: Dùng tính năng drag-and-drop của n8n để tránh gõ sai tên property (Notion phân biệt chữ hoa/thường).

**🔹 Node `Archive pages` (Notion)**
- Chọn cùng **Credential Notion** như node `Get pages from database`.
- Node này sẽ tự động nhận `page_id` từ node `Filter duplicates` và archive các bản ghi dư.

**🔹 Hai node Trigger (tùy chọn bật/tắt)**
- `When a page is added to the database` (Notion Trigger): Chạy ngay khi có page mới được thêm vào database.
- `Every day` (Schedule Trigger): Chạy định kỳ mỗi ngày 1 lần để "tổng vệ sinh".
- Các sếp có thể **disable** trigger không cần dùng bằng cách click chuột phải → **Deactivate**, hoặc chỉnh giờ chạy trong Schedule Trigger.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test với dữ liệu mẫu. Kiểm tra output của node `Filter duplicates` xem có đúng các bản ghi trùng cần xóa không.
- Nếu kết quả đúng → Gạt công tắc **Active** ở góc trên bên phải để workflow chạy tự động.
- Vào Notion kiểm tra lại database: các bản ghi trùng sẽ biến mất khỏi view (vẫn nằm trong Trash nếu cần khôi phục).

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi thông báo qua Slack/Telegram**: Thêm node Slack hoặc Telegram sau node `Archive pages` để nhận báo cáo "Đã dọn dẹp X bản ghi trùng lặp" mỗi lần chạy.
- **Lưu log vào Google Sheets**: Ghi lại danh sách các page_id đã bị archive để có "nhật ký" đối soát khi cần.
- **Kết hợp nhiều property check trùng**: Sửa node `Filter duplicates` để so sánh theo tổ hợp (ví dụ: `Email + Số điện thoại`) thay vì chỉ 1 field.
- **Chạy theo lịch tuần/tháng**: Đổi Schedule Trigger từ "Every day" sang "Every week" để giảm tải API Notion nếu database ít thay đổi.
- **Backup trước khi xóa**: Thêm node Notion `Get All` phụ để export dữ liệu ra file CSV trước khi archive — phòng trường hợp cần phục hồi.

### 📌 Kết luận
Với 7 nodes gọn nhẹ nhưng cực kỳ hiệu quả, workflow này là "vũ khí" không thể thiếu cho bất kỳ ai đang vận hành Notion Database làm CRM, quản lý đơn hàng hay form đăng ký. Thay vì mất hàng giờ mỗi tuần để dọn dẹp thủ công, các sếp chỉ cần setup một lần và để n8n "cày" 24/7 — dữ liệu luôn sạch, báo cáo luôn chuẩn, và team có thêm thời gian cho việc quan trọng hơn.

👉 **Hãy import workflow ngay hôm nay** và trải nghiệm cảm giác Notion Database "sạch bong kin kít" mà không cần tốn một giọt mồ hôi!