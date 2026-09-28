---
title: "🚀 Tự Động Hóa Sáng Lập Nhiệm Vụ Từ Mẫu (Blueprint) Với Baserow + Lịch Trình Hợp Lý (Không Cần Code)"
description: "Workflow tự động hóa 100% không code để chuyển đổi các bước trong mẫu (blueprint) thành nhiệm vụ cá nhân hóa, tự động tính toán hạn chót và tránh lịch vào cuối tuần. Giúp quản lý dự án, HR và vận hành tiết kiệm thời gian lên đến 80% so với thủ công."
slug: "tu-dong-hoa-sang-lap-nhiem-vu-tu-mau-baserow"
tags: [n8n, automation, baserow, project-management, no-code, workflow-automation]
keywords: [n8n workflow baserow, tự động hóa nhiệm vụ, quản lý dự án không code, baserow api, lịch trình tự động]
---

# 🚀 **Tự Động Hóa Sáng Lập Nhiệm Vụ Từ Mẫu (Blueprint) Với Baserow + Lịch Trình Hợp Lý**

### **Giải pháp cho các sếp:**
Bạn đã từng phải **ghi chép lại hàng chục nhiệm vụ** từ một mẫu (blueprint) thủ công, tính toán hạn chót, phân công cho nhân viên và lo lắng về việc **nhiệm vụ rơi vào cuối tuần**? Hay phải **quản lý quy trình tái diễn** như onboarding nhân viên, kiểm tra bảo trì, hoặc thủ tục SOPs một cách rườm rà? **Workflow này sẽ tự động hóa toàn bộ quá trình chỉ với một cú nhấp chuột!**

Dùng **n8n + Baserow**, bạn có thể:
✅ **Tạo nhiệm vụ từ mẫu** (blueprint) một cách tự động, với thông tin cá nhân hóa (người phụ trách, hạn chót, ghi chú).
✅ **Tính toán hạn chót thông minh**, tránh rơi vào cuối tuần (thứ 7, chủ nhật) bằng cách tự động điều chỉnh sang thứ Hai đầu tiên.
✅ **Nhập batch nhiệm vụ** vào Baserow một lúc, thay vì một nhiệm vụ một, tiết kiệm thời gian lên đến **80%**.
✅ **Kết hợp với Baserow Application Builder** để kích hoạt workflow từ giao diện người dùng, không cần viết code.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải nhập liệu thủ công hàng tuần/month cho các quy trình tái diễn.
- **Chính xác 100%**: Tránh sai sót trong tính toán hạn chót hoặc phân công nhiệm vụ.
- **Lịch trình hợp lý**: Nhiệm vụ **không bao giờ rơi vào cuối tuần** nhờ tính năng tự động điều chỉnh.
- **Cá nhân hóa**: Mỗi nhiệm vụ được gắn thông tin người phụ trách, ghi chú và hạn chót riêng.
- **Hoạt động 24/7**: Workflow chạy tự động khi có yêu cầu, không phụ thuộc vào giờ làm việc của bạn.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Baserow** (cloud hoặc self-hosted).
2. **Cấu trúc cơ sở dữ liệu Baserow** với các bảng sau:
   - **`Assignee`** (bảng người phụ trách): Chứa thông tin nhân viên (ID, tên, email...).
   - **`Master`** (bảng mẫu/quy trình): Chứa thông tin chung của mỗi mẫu (ví dụ: quy trình xử lý khiếu nại).
   - **`Details`** (bảng chi tiết bước): Mỗi bước trong mẫu sẽ được chuyển thành một nhiệm vụ riêng. **Bắt buộc có trường `Days to complete`** để tính toán hạn chót.
   - **`Tasks`** (bảng nhiệm vụ): Chứa nhiệm vụ cuối cùng với người phụ trách và hạn chót.
3. **Token API Baserow**: Để n8n có thể tương tác với Baserow. [Hướng dẫn tạo token](https://baserow.io/user-docs/personal-api-tokens).
4. **ID của các bảng và trường** trong Baserow (sẽ được hướng dẫn cụ thể trong phần **Cấu hình**).
5. **Mẫu (blueprint) chuẩn**: Dùng mẫu **Standard Operating Procedures (SOP)** của Baserow làm ví dụ, hoặc tự tạo theo cấu trúc tương tự.
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [link gốc](https://n8n.io/workflows/8602) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/8602) và dán vào **Import Workflow** trong n8n.

:::note[LƯU Ý]
- **Không** sử dụng phiên bản n8n cloud miễn phí vì nó **không hỗ trợ webhook** (node `webhook` là core của workflow này).
- **Khuyến nghị**: Cài n8n trên **VPS riêng** để workflow chạy 24/7 ổn định.
:::

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình `Trigger task creation` (Webhook)**
- **Địa chỉ Webhook**: `https://[your-n8n-instance]/webhook/create-tasks-for-template`
  (Thay `[your-n8n-instance]` bằng địa chỉ VPS của bạn, ví dụ: `https://n8n.tinohost.vn`).
- **Phương thức**: POST.
- **Giới hạn**: Không giới hạn (để cho phép request lớn khi nhập batch nhiệm vụ).

#### **B. Cấu hình `Configure settings and ids` (Set)**
Điền các thông tin sau vào **Properties** của node này:
| Thông tin cần điền | Giá trị | Ghi chú |
|----------------------|---------|---------|
| **API host** | `https://api.baserow.io` (nếu dùng cloud) hoặc `https://[your-baserow-instance]/api` (self-hosted) | Địa chỉ API của Baserow. |
| **Token** | Token API Baserow của bạn | Tạo theo [hướng dẫn](https://baserow.io/user-docs/personal-api-tokens). |
| **Database ID** | ID cơ sở dữ liệu Baserow | Lấy từ URL: `https://baserow.io/d/[database-id]/` |
| **Detail template table ID** | ID bảng `Details` | Lấy từ URL: `https://baserow.io/d/[db-id]/t/[table-id]/` |
| **Link to master template field ID** | ID trường liên kết đến `Master` trong bảng `Details` | Ví dụ: trường `master_template` |
| **Task table ID** | ID bảng `Tasks` | Lấy từ URL: `https://baserow.io/d/[db-id]/t/[table-id]/` |
| **assignee_id** | `{$.json["assignee_id"]}` | Tham chiếu từ request webhook. |
| **template_id** | `{$.json["template_id"]}` | Tham chiếu từ request webhook. |
| **schedule_date** | `{$.json["schedule_date"]}` | Tham chiếu từ request webhook. |
| **note** | `{$.json["note"]}` | Tham chiếu từ request webhook. |

#### **C. Cấu hình `Calculate deadlines for each step` (Set)**
Node này **bắt buộc** phải điều chỉnh **tên trường** để khớp với cấu trúc bảng `Tasks` của bạn. Ví dụ:
```json
{
  "assignee": "{{$node["Configure settings and ids"].json["assignee_id"]}}",
  "title": "Thực hiện bước {{$node["Get all template steps"].json["title"]}}",
  "deadline": "{{$node["Avoid scheduling during the weekend"].json["deadline"]}}",
  "note": "{{$node["Configure settings and ids"].json["note"]}}",
  "status": "Chưa hoàn thành"
}
```
- **Lưu ý**:
  - `title`, `deadline`, `note`, `status` phải **khớp với tên trường** trong bảng `Tasks` của Baserow.
  - Nếu bảng `Tasks` có trường khác (ví dụ: `priority`, `created_at`), thêm vào đây.

#### **D. Cấu hình `Avoid scheduling during the weekend` (Code)**
Node này sử dụng **JavaScript** để điều chỉnh hạn chót tránh vào cuối tuần. **Không cần chỉnh sửa** nội dung code mặc định, nhưng nếu muốn thêm logic (ví dụ: tránh ngày lễ), bạn có thể mở rộng như sau:
```javascript
// Kiểm tra nếu hạn chót là thứ 7 hoặc chủ nhật
const deadline = new Date($node["Calculate deadlines for each step"].json["deadline"]);

// Nếu là thứ 7, điều chỉnh sang thứ Hai tiếp theo
if (deadline.getDay() === 0) { // 0 = Chủ nhật
  deadline.setDate(deadline.getDate() + 2);
}
// Nếu là thứ 6, điều chỉnh sang thứ Hai tiếp theo
else if (deadline.getDay() === 6) { // 6 = Thứ 7
  deadline.setDate(deadline.getDate() + 1);
}

return {
  deadline: deadline.toISOString().split('T')[0] // Trả về định dạng YYYY-MM-DD
};
```

#### **E. Kiểm tra `Generate tasks in batch` (HTTP Request)**
- **URL**: `https://api.baserow.io/api/database/rows/table/{task-table-id}/batch/`
  (Thay `{task-table-id}` bằng ID bảng `Tasks` từ bước trước).
- **Headers**:
  - `Authorization`: `Token {token}`
  - `Content-Type`: `application/json`
- **Body**: `{ "items": {{$node["Aggregate tasks for insert"].json["items"]}} }`
  (Node này sẽ tự động tạo danh sách nhiệm vụ từ dữ liệu trước đó).

---
### **3. Kích hoạt ⚡️**
1. **Test run** với dữ liệu mẫu:
   - Gửi request POST đến webhook với payload:
     ```json
     {
       "assignee_id": 123,
       "template_id": 456,
       "schedule_date": "2025-10-01",
       "note": "Xử lý khiếu nại khách hàng #12345"
     }
     ```
   - Kiểm tra **log** trong n8n để xác nhận nhiệm vụ được tạo thành công.
2. **Bật Active workflow** khi đã kiểm tra xong.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Thêm thông báo Slack/Email**:
   - Sau khi tạo nhiệm vụ thành công, gửi thông báo đến người phụ trách qua **Slack** hoặc **Email** bằng node `slack` hoặc `email`.
   - Ví dụ: `"Nhiệm vụ: {{title}} đã được tạo với hạn chót: {{deadline}}"`.
2. **Lưu log hoạt động**:
   - Sử dụng node `stickyNote` hoặc `googleSheets` để ghi lại lịch sử tạo nhiệm vụ (ngày giờ, người tạo, template sử dụng).
3. **Kết hợp với Google Calendar**:
   - Tự động tạo sự kiện trong Google Calendar cho mỗi nhiệm vụ với hạn chót.
4. **Hỗ trợ ngày lễ**:
   - Mở rộng node `Avoid scheduling during the weekend` để tránh ngày lễ (ví dụ: Tết, Giáng sinh) bằng cách gọi API **Google Calendar API** hoặc **Public Holidays API**.
5. **Phân quyền tự động**:
   - Nếu bảng `Assignee` có trường `department`, tự động phân công nhiệm vụ cho nhóm phù hợp (ví dụ: IT, Marketing).
6. **Báo cáo định kỳ**:
   - Tạo một workflow riêng để gửi **báo cáo nhiệm vụ chưa hoàn thành** hàng tuần qua Email.
:::

---
## 📌 **Kết luận**
Workflow này **giải phóng bạn khỏi công việc nhập liệu thủ công** và **tự động hóa toàn bộ quy trình tạo nhiệm vụ từ mẫu (blueprint)**. Bằng cách kết hợp **n8n + Baserow**, bạn có thể:
✔ **Tiết kiệm thời gian** lên đến 80% cho các quy trình tái diễn.
✔ **Tránh sai sót** trong tính toán hạn chót và phân công.
✔ **Hoạt động 24/7** mà không cần can thiệp thủ công.

**Hành động ngay!**
1. **Cài n8n trên VPS** (để workflow chạy ổn định).
2. **Chuẩn bị Baserow** với cấu trúc bảng như hướng dẫn.
3. **Import workflow** và **cấu hình** theo bước trên.
4. **Test run** và **bật Active** để tự động hóa ngay!

👉 **Bắt đầu tự động hóa ngay hôm nay!** Nếu có vấn đề, hãy để lại comment bên dưới hoặc liên hệ với **Frederik Duchi** (tác giả workflow) qua [GitHub](https://github.com/frederikduchi).

---
:::note[CHÚ Ý CUỐI CÙNG]
- **Không cần biết code**: Workflow này **không yêu cầu kiến thức lập trình**.
- **Dễ dàng mở rộng**: Bạn có thể thêm logic mới vào node `code` hoặc `set` để phù hợp với nhu cầu cụ thể.
- **Miễn phí**: Tất cả các node trong workflow đều **miễn phí** (n8n Community Edition).
:::

---
**🚀 Cảm ơn các sếp đã đọc đến cuối!** Chúc các sếp thành công với việc tự động hóa! 🎉