---
title: "🚀 Gửi lời mời kết nối LinkedIn từ Airtable qua Unipile tự động theo lịch"
description: "Tự động gửi lời mời kết nối LinkedIn cho danh sách liên hệ trong Airtable mỗi tuần, giảm 100% công việc thủ công và tăng tỷ lệ tiếp cận."
slug: "gui-loi-moi-lien-ket-linkedin-tu-airtable-qua-unipile"
tags: [n8n, automation, no-code, lead-nurturing, linkedin, airtable]
keywords: [n8n workflow, tự động hóa, LinkedIn invitation, Airtable integration, Unipile API]
---

# 🚀 Gửi lời mời kết nối LinkedIn từ Airtable qua Unipile tự động theo lịch

Bạn có bao giờ phải **chép chép danh sách liên hệ từ Airtable, đăng nhập LinkedIn, rồi thủ công gửi lời mời kết nối**?  
Công việc này không chỉ tốn hàng giờ mỗi tuần mà còn dễ gây lỗi, mất cơ hội và làm giảm năng suất của đội sales.

**Workflow này** sẽ giải quyết hoàn toàn vấn đề trên: mỗi **thứ Hai lúc 10h** (hoặc thời gian bạn tùy chỉnh) n8n sẽ tự động:

1. Lấy danh sách các contact chưa được mời từ Airtable.  
2. Giới hạn số lượng gửi mỗi lần (mặc định 100).  
3. Dùng **Unipile API** lấy session LinkedIn hợp lệ cho từng contact.  
4. Gửi lời mời kết nối LinkedIn thay mặt bạn.  
5. Cập nhật trạng thái “Invited” hoặc “Error” ngay trong Airtable.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Không còn thao tác thủ công, chỉ cần một lần thiết lập.  
- **Độ chính xác 100%**: Không còn lỗi nhập sai dữ liệu hay bỏ sót contact.  
- **Tăng tỷ lệ phản hồi**: Lời mời được gửi ngay trong khung giờ “vàng” của LinkedIn.  
- **Hoạt động liên tục**: Workflow chạy tự động mỗi tuần, không cần giám sát.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản Airtable** + API token (`airtableTokenApi`).  
- **Base & Table** chứa danh sách contact (cần trường: email/LinkedIn profile, status).  
- **Unipile API**: Domain (ví dụ `your-unipile.dns`) và API key (đặt trong **HTTP Header Auth**).  
- **n8n** đã cài đặt và có quyền truy cập internet để gọi API Unipile.  
- **Quyền ghi** trên bảng Airtable để cập nhật trạng thái “Invited” / “Error”.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Vào **n8n → Workflows → Import**.  
2. Tải file JSON của workflow (hoặc copy toàn bộ JSON từ trang gốc) và nhấn **Import**.  
3. Đặt tên cho workflow, ví dụ: `Send LinkedIn invites from Airtable`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Cấu hình cần thay đổi | Ghi chú |
|------|----------------------|---------|
| **Every Monday at 10am** (`scheduleTrigger`) | Thay đổi tần suất nếu muốn (daily, hourly, custom cron). | Đảm bảo múi giờ phù hợp với khu vực làm việc. |
| **Fetch Contacts from Airtable** (`airtable`) | - Chọn **Credentials** → `airtableTokenApi`.<br>- Base ID, Table Name.<br>- Filter: chỉ lấy các record có trường “Invite Sent” = false. | Đảm bảo trường filter đúng để tránh gửi lại. |
| **Limit to 100 Contacts** (`limit`) | Thiết lập **Maximum Items** (mặc định 100). | Điều chỉnh tùy theo hạn mức LinkedIn / quota Unipile. |
| **Loop Over Contacts** (`splitInBatches`) | Batch size = 1 (để xử lý từng contact một). | Giữ batch size 1 để tránh đồng thời gửi quá nhiều request. |
| **Fetch LinkedIn User Session** (`httpRequest`) | - URL: `https://<YourUnipileDNS>/session`.<br>- Method: GET.<br>- Header: `Authorization: Bearer <Your_Unipile_API_Key>`. | Kiểm tra phản hồi có `sessionId` hợp lệ. |
| **Send LinkedIn Invitation** (`httpRequest`) | - URL: `https://<YourUnipileDNS>/invite`.<br>- Method: POST.<br>- Body (JSON): `{ "sessionId": {{$json["sessionId"]}}, "profileUrl": {{$json["LinkedInProfile"]}} }`.<br>- Header: `Authorization: Bearer <Your_Unipile_API_Key>`.<br>- Content-Type: `application/json`. | Đảm bảo mapping đúng trường `LinkedInProfile` từ Airtable. |
| **Update Invite Sent in Airtable** (`airtable`) | - Chọn **Credentials** → `airtableTokenApi`.<br>- Base/Table same as fetch.<br>- Record ID: `{{$json["id"]}}`.<br>- Field to update: `Invite Sent` = true, `Status` = “Invited”. | Đường dẫn trường phải khớp với cấu trúc bảng. |
| **Update Error Status in Airtable** (`airtable`) | Tương tự node trên, nhưng cập nhật `Status` = “Error” và lưu `Error Message` nếu có. | Dùng cho nhánh **Error** của HTTP Request. |

> **Lưu ý:** Các node **HTTP Request** đều cần **Credentials → httpHeaderAuth** chứa header `Authorization`. Nếu bạn chưa tạo credential này, vào **Credentials → New Credential → HTTP Header Auth** và nhập key/value.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** lần đầu với **Run Once** để kiểm tra dữ liệu mẫu.  
2. Kiểm tra bảng Airtable: các record đã được đánh dấu “Invited” hoặc “Error”.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi góc phải trên). Workflow sẽ tự động chạy theo lịch đã định.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi báo cáo tuần**: Thêm node **Gmail** hoặc **Slack** để gửi summary số lời mời thành công / lỗi sau mỗi lần chạy.  
- **Kiểm soát quota LinkedIn**: Thêm node **Delay** giữa các lời mời (ví dụ 30 giây) để tránh bị block.  
- **Lưu log chi tiết**: Kết nối **Google Sheets** hoặc **MongoDB** để lưu toàn bộ payload request/response cho mục đích audit.  
- **Mở rộng nguồn dữ liệu**: Thay Airtable bằng **Notion**, **HubSpot** hoặc **Pipedrive** chỉ bằng cách đổi node nguồn và mapping trường.

### 📌 Kết luận
Với workflow này, các sếp sẽ **loại bỏ hoàn toàn công đoạn gửi lời mời LinkedIn thủ công**, giảm thiểu lỗi và tăng tốc độ tiếp cận khách hàng tiềm năng. Hãy **import, cấu hình nhanh**, bật **Active** và để n8n làm việc thay bạn 24/7. Nếu cần tùy chỉnh sâu hơn hoặc muốn xây dựng automation doanh nghiệp toàn diện, đừng ngần ngại **liên hệ Allan Vaccarizi** – chuyên gia n8n sẵn sàng hỗ trợ! 🚀