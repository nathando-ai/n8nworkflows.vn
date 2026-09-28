---
title: "🚀 Tự động theo dõi thay đổi công việc trên LinkedIn bằng Airtop và n8n"
description: "Hướng dẫn xây dựng workflow tự động trích xuất thông tin thay đổi công việc của kết nối LinkedIn, phân loại chức vụ và tối ưu hóa quy trình Sales, HR."
slug: "theo-doi-thay-doi-cong-viec-linkedin-airtop"
tags: [n8n, automation, linkedin, airtop, sales, hr]
keywords: [n8n workflow, theo dõi linkedin, airtop api, tự động hóa sales, cập nhật hr]
---

# 🚀 Tự động theo dõi thay đổi công việc trên LinkedIn với Airtop

Việc theo dõi thủ công sự thay đổi công việc của khách hàng tiềm năng, đối tác hay nhân sự trên LinkedIn cực kỳ tốn thời gian. Các Salesman hay nhà tuyển dụng (HR) thường bỏ lỡ "thời điểm vàng" để tiếp cận khi họ vừa chuyển sang một vị trí mới hoặc công ty mới. 

Workflow n8n này sẽ giúp các sếp giải quyết triệt để vấn đề đó bằng cách tự động hóa 100% quy trình quét, trích xuất và phân loại thông tin thay đổi công việc từ LinkedIn mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Tự động hóa hoàn toàn việc rà soát bảng tin "Job Changes" trên LinkedIn, gom lại 5 kết quả chất lượng mỗi lần chạy.
- **Dữ liệu chuẩn hóa:** Trích xuất rõ ràng Tên, Vị trí mới, Link Profile LinkedIn và phân loại chức vụ (Marketing, Sales, HR, Executive...).
- **Kịp thời tương tác:** Nắm bắt ngay cơ hội outreach chúc mừng hoặc chào bán dịch vụ khi đối tác vừa đổi sếp/đổi vị trí.
- **Dễ dàng mở rộng:** Dữ liệu JSON sạch sẽ sẵn sàng để đẩy thẳng vào CRM, Slack hoặc Email.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Airtop:** Cần tạo tài khoản tại [Airtop Portal](https://portal.airtop.ai/browser-profiles) và kết nối sẵn profile với tài khoản LinkedIn của các sếp.
- **Airtop API Key:** Để kết nối node Airtop trong n8n.
- **Tài khoản LinkedIn:** Có nguồn cấp dữ liệu “Job Changes” hoạt động bình thường.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow này và dán trực tiếp vào n8n Editor là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow cực kỳ tinh gọn với 3 nodes chính, các sếp cần chú ý cấu hình kỹ:
- **Node `Extract Job Changes` (Airtop):** 
  - Chọn hoặc thêm mới **Credentials** loại `airtopApi` bằng cách nhập API Key lấy từ trang quản trị Airtop.
  - Kiểm tra lại phần `Prompt`: Workflow đã được thiết lập sẵn câu lệnh (prompt) bằng tiếng Anh để yêu cầu Airtop trích xuất 5 thay đổi công việc kèm theo tên, vị trí mới, link LinkedIn và phân loại chức vụ. Các sếp có thể tinh chỉnh lại prompt này nếu muốn trích xuất số lượng nhiều hơn hoặc yêu cầu chi tiết hơn.
- **Node `Edit Fields` (Set):** 
  - Dùng để chuẩn hóa lại định dạng dữ liệu đầu ra (JSON) giúp các bước tiếp theo xử lý mượt mà hơn.

#### 3. Kích hoạt ⚡️
- Nhấn nút **"Test workflow"** tại node `When clicking ‘Test workflow’` để chạy thử và kiểm tra dữ liệu trả về ở bảng điều khiển bên phải.
- Sau khi kiểm tra dữ liệu đã chính xác, bật công tắc **Active** để workflow sẵn sàng hoạt động tự động theo lịch trình (nếu các sếp cấu hình thêm Schedule Trigger).

### ✍️ Mẹo & gợi ý nâng cao
Để biến workflow này thành một cỗ máy kiếm khách hàng tự động thực thụ, các sếp có thể mở rộng thêm:
- **Tích hợp thông báo:** Nối thêm node **Slack** hoặc **Telegram** để bắn tin nhắn thông báo ngay lập tức về máy của đội ngũ Sales/HR mỗi khi có người thay đổi công việc.
- **Đẩy về CRM:** Tự động cập nhật trạng thái hoặc tạo Lead mới trong HubSpot, Airtable, Google Sheets.
- **Gửi Email tự động:** Kết hợp cùng AI node để soạn sẵn email chúc mừng mang tính cá nhân hóa cao dựa trên vị trí mới của họ.

### 📌 Kết luận
Workflow "Monitoring Job Changes on LinkedIn with Airtop" là trợ thủ đắc lực giúp các sếp không bỏ lỡ bất kỳ cơ hội networking hay tuyển dụng quan trọng nào. Hãy áp dụng ngay hôm nay để tối ưu hóa hiệu suất làm việc với sức mạnh của AI và Automation!