---
title: "🚀 Truy xuất dữ liệu phân cấp đa tầng từ Airtable cực đỉnh bằng n8n"
description: "Hướng dẫn chi tiết cách tự động lấy bản ghi Airtable kèm theo cấu trúc dữ liệu con đa tầng (Level 2 và Level 3) dưới dạng JSON lồng nhau chuẩn xác."
slug: "truy-xuat-du-lieu-phan-cap-da-tang-tu-airtable-voi-n8n"
tags: [n8n, automation, airtable, no-code, api-integration]
keywords: [n8n workflow, airtable hierarchical data, tự động hóa airtable, n8n airtable nested records]
---

# 🚀 Truy xuất dữ liệu phân cấp đa tầng từ Airtable cực đỉnh bằng n8n

Các sếp có bao giờ gặp khó khăn khi muốn kéo dữ liệu liên kết (linked records) từ Airtable lên các hệ thống khác chưa? Airtable mặc định chỉ trả về ID của các bản ghi con, khiến các sếp phải viết code phức tạp hoặc gọi API liên tục để "bóc tách" từng tầng dữ liệu (cha -> con -> cháu). 

Giải pháp nằm ngay đây! Workflow n8n này sẽ tự động hóa toàn bộ quá trình **truy xuất dữ liệu phân cấp lên tới 3 cấp độ** (Multi-level Relationships) từ Airtable và gom chúng thành một cấu trúc JSON lồng nhau (nested JSON) hoàn chỉnh. Không cần code phức tạp, tự động 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Đồng bộ dữ liệu đa tầng**: Tự động kéo bản ghi chính (Level 1), bản ghi con (Level 2) và bản ghi cháu (Level 3) chỉ trong một lần chạy.
- **Tối ưu hiệu suất**: Cho phép chọn lọc linh hoạt trường Level 3 cần lấy để tránh quá tải API.
- **Xử lý định dạng thông minh**: Tự động chuyển đổi các trường Rich Text (pseudo-markdown) sang HTML sạch sẽ.
- **Cấu trúc JSON gọn gàng**: Trả về dữ liệu dạng cây (hierarchical tree) sẵn sàng để đẩy sang CRM, Webhook hoặc hiển thị lên Web App.
:::

### 📦 Cấu trúc Input đầu vào
Workflow nhận đầu vào dưới dạng một JSON array với cấu trúc như sau:
```json
[
  {
    "base_id": "appN8nPMGoLNuzUbY",
    "table_id": "tblLVOwpYIe0fGQ52", 
    "record_id": "reczMh1Pp5l94HdYf",
    "level_3": [
      "fldRaFra1rLta66cD",
      "fld3FxCaYk8AVaEHt"
    ],
    "to_html": true
  }
]
```
* **`base_id`**: ID của Base Airtable.
* **`table_id`**: ID của Table chứa bản ghi chính.
* **`record_id`**: ID bản ghi cụ thể cần lấy.
* **`level_3`** *(Tùy chọn)*: Mảng chứa các ID trường liên kết của Level 2 mà các sếp muốn tiếp tục bóc sâu xuống Level 3.
* **`to_html`** *(Tùy chọn)*: Chuyển đổi Rich Text sang HTML (mặc định là `false`). *Lưu ý: Tính năng này yêu cầu cài đặt thư viện `marked` npm package trong n8n.*

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản **Airtable** và **Airtable Personal Access Token** có quyền đọc (Read) các Base/Table liên quan.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy toàn bộ mã JSON của workflow (hoặc tải file JSON từ nguồn).
- Mở n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng 3 chấm ở góc trên bên phải -> Chọn **Import from File / Clipboard** và dán dữ liệu vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần chú ý cấu hình các node cốt lõi sau để workflow chạy mượt mà:
- **Airtable Schema**, **Airtable - Get Target Record**, **Get Linked records without Link To fields Except for Level 3**, **Get L3 Linked records without reverse Link To fields**, và **Get Airtable Comments**: 
  - Tại các node này, các sếp phải cấu hình **Credential** bằng cách kết nối tài khoản Airtable của mình sử dụng `airtableTokenApi`.
- **Node Code (Markdown to Html)**: Nếu sử dụng tính năng chuyển đổi Markdown sang HTML (`to_html: true`), hãy đảm bảo môi trường n8n self-hosted của các sếp đã cấu hình cho phép sử dụng module `marked` thông qua biến môi trường `NODE_FUNCTION_ALLOW_EXTERNAL=marked`. Nếu không dùng tính năng này, các sếp có thể bỏ qua hoặc xóa nhóm node liên quan.

#### 3. Kích hoạt ⚡️
- Tạo một bản ghi mẫu dựa trên cấu trúc Input hướng dẫn ở trên và đưa vào node **Inputs**.
- Nhấn **Execute Workflow** để test thử nghiệm và kiểm tra kết quả trả về ở node cuối cùng.
- Sau khi test ngon lành, hãy gạt công tắc sang **Active** để đưa vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Webhook**: Các sếp có thể đặt một Webhook Trigger ở đầu workflow để biến nó thành một API endpoint riêng biệt, cho phép các hệ thống bên ngoài gọi và lấy dữ liệu phân cấp bất cứ lúc nào.
- **Lưu trữ kết quả**: Kết hợp thêm node Google Sheets, Supabase hoặc PostgreSQL ở cuối workflow để lưu trữ lại bản dữ liệu phân cấp phục vụ việc báo cáo.
- **Gửi thông báo lỗi**: Thêm nhánh Error Trigger để gửi tin nhắn cảnh báo qua Telegram/Slack nếu Airtable API trả về lỗi (ví dụ: sai ID hoặc mất kết nối).

### 📌 Kết luận
Với workflow này, việc xử lý các mối quan hệ dữ liệu phức tạp đa tầng trong Airtable không còn là nỗi ác mộng. Hãy import ngay vào n8n của các sếp để tối ưu hóa quy trình quản trị dữ liệu ngay hôm nay!