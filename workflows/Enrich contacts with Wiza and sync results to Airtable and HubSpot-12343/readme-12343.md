---
title: "🚀 Tự động làm giàu thông tin liên hệ với Wiza, đồng bộ Airtable và HubSpot"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình làm giàu thông tin khách hàng tiềm năng qua Wiza, đồng thời đồng bộ dữ liệu liền mạch vào Airtable và HubSpot."
slug: "tu-dong-lam-giau-thong-tin-lien-he-wiza-hubspot-airtable"
tags: [n8n, automation, no-code, lead-generation, wiza, hubspot, airtable]
keywords: [n8n workflow, làm giàu thông tin lead, wiza n8n, hubspot automation, tự động hóa bán hàng]
---

# 🚀 Tự động làm giàu thông tin liên hệ với Wiza, đồng bộ Airtable và HubSpot

Các sếp trong ngành sales và marketing chắc hẳn luôn cảm thấy mệt mỏi khi phải thủ công đi tìm kiếm email, số điện thoại, rồi lại cặm cụi nhập liệu vào CRM như HubSpot hay Airtable đúng không ạ? Việc này vừa tốn hàng giờ đồng hồ mỗi ngày, vừa dễ xảy ra sai sót nhập liệu.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ mạnh mẽ do tác giả **Mezie** xây dựng. Workflow này sẽ tự động hóa toàn bộ quy trình: nhận thông tin từ form, tìm kiếm và xác thực dữ liệu qua Wiza, xử lý logic rẽ nhánh thông minh, làm sạch dữ liệu bằng Code node, và cuối cùng là đẩy kết quả đồng thời lên Google Sheets, Airtable/DataTable và CRM HubSpot!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo sập giữa chừng, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chỉ cần nhập liệu đầu vào qua form, hệ thống tự lo phần còn lại từ tìm kiếm đến đồng bộ CRM.
- **Dữ liệu sạch và chính xác:** Tận dụng sức mạnh của Wiza để tìm kiếm email, số điện thoại và LinkedIn chuẩn xác, kết hợp logic kiểm tra lỗi.
- **Đồng bộ đa nền tảng:** Dữ liệu được đẩy liền mạch vào Google Sheets, hệ thống nội bộ (DataTable) và HubSpot CRM mà không cần đụng tay.
- **Tiết kiệm thời gian:** Giải phóng đội ngũ sales khỏi công việc nhập liệu thủ công nhàm chán để tập trung vào chốt sales.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản và API Key từ **Wiza** (cho các node Email Finder, Phone Finder, Linkedin Finder).
- Tài khoản **HubSpot** (để lấy Hubspot App Token).
- Tài khoản **Google Sheets** (nếu sử dụng Google Sheets OAuth2 API).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy đoạn mã JSON của workflow này, vào giao diện n8n Editor, chọn **Import from JSON** và dán vào là xong phần khung sườn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:
- **On form submission (`formTrigger`)**: Thiết lập form đầu vào để thu thập thông tin cơ bản của khách hàng tiềm năng (như URL LinkedIn, tên công ty...).
- **Wiza Nodes (`Email Finder`, `Phone Finder`, `Linkedin Finder`)**: Kết nối tài khoản Wiza bằng **Wiza API credentials**. Đảm bảo các tham số (parameters) truyền vào đúng định dạng LinkedIn Profile URL.
- **Switch & Merge Nodes**: Kiểm tra các điều kiện rẽ nhánh (Switch) xem quá trình tìm kiếm dữ liệu từ Wiza có thành công hay không. Nếu thành công sẽ đi tiếp, nếu thất bại sẽ được điều hướng đến form thông báo lỗi (`Failed To Find Enrichment`).
- **Clean Up (`code`)**: Node này dùng Javascript để làm sạch, định dạng lại dữ liệu thô trước khi đẩy vào CRM. Các sếp có thể tùy chỉnh đoạn code bên trong nếu muốn thay đổi cấu trúc trường dữ liệu.
- **Create or update a contact (`hubspot`)**: Chọn **HubSpot App Token** credentials, sau đó map các trường dữ liệu (First Name, Last Name, Email, Phone) từ kết quả đã làm sạch ở trên vào HubSpot.
- **Append or update row in sheet (`googleSheets`)** & **Insert row (`dataTable`)**: Cấu hình file Google Sheets đích và bảng dữ liệu nội bộ để lưu trữ bản ghi backup.

#### 3. Kích hoạt ⚡️
- Chạy thử một vài dữ liệu test (Test run) để kiểm tra từng node xem dữ liệu có chảy đúng hướng không.
- Sau khi mọi thứ xanh mướt (success), các sếp bật công tắc **Active** ở góc trên bên phải để workflow chính thức chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Slack hoặc Telegram vào nhánh thành công hoặc thất bại để đội ngũ sales nhận được thông báo ngay lập tức có lead mới.
- **Xử lý trùng lặp:** Tận dụng tính năng "Upsert" của HubSpot và Google Sheets để tránh tạo ra các contact trùng lặp trong hệ thống.
- **Mở rộng AI:** Kết hợp thêm các mô hình LLM (như OpenAI) sau bước làm sạch dữ liệu để tự động viết email chào hàng (cold email) cá nhân hóa dựa trên thông tin Wiza vừa tìm được.

### 📌 Kết luận
Workflow tích hợp Wiza, Airtable và HubSpot này chính là mảnh ghép hoàn hảo giúp các đội ngũ sales scaling quy trình prospecting mà không cần tốn chi phí thuê nhân sự nhập liệu thủ công. Chúc các sếp cài đặt thành công và "bốt" đơn ngập tràn!