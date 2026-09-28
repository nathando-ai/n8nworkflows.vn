---
title: "🎒 **Tự Động Hóa Quản Lý Email Học Sinh Với AI, Google Calendar & Google Drive - Không Cần Code!**"
description: "Workflow này tự động phân loại, lưu trữ và nhắc nhở các thông báo học đường từ email, đồng bộ hóa lịch học và danh sách đồ mang theo vào Google Calendar & Drive. Giúp các bậc phụ huynh không bao giờ bỏ lỡ thông báo quan trọng."
slug: "tieu-dong-hoa-quan-ly-email-hoc-sinh-voi-ai-google-calendar-va-google-drive"
tags: [n8n, tự động hóa học đường, AI phân loại email, Google Calendar, Google Drive, quản lý thông báo học sinh]
keywords: [n8n workflow học đường, tự động hóa email học sinh, AI quản lý lịch học, lưu trữ thông báo học đường, nhắc nhở đồ mang theo]
---

# 🎒 **Tự Động Hóa Quản Lý Email Học Sinh Với AI, Google Calendar & Google Drive**

## **🔥 Nỗi Đau Của Các Bậc Phụ Huynh Hiện Nay**
Hàng ngày, các bậc phụ huynh phải:
- **Làm thủ công** lọc email từ trường học giữa hàng trăm tin nhắn rối loạn.
- **Quên nhớ** các sự kiện quan trọng như ngày thi, buổi họp phụ huynh, hoặc đồ mang theo.
- **Tốn thời gian** sao chép thông tin từ email vào lịch hoặc lưu vào Google Drive.
- **Lo lắng** rằng có thể bỏ lỡ thông báo quan trọng về sức khỏe, hoạt động ngoại khóa, hoặc thay đổi lịch học.

**Workflow này giải quyết tất cả đó!** Với AI và tự động hóa, mọi thông tin từ email học đường sẽ được **phân loại, lưu trữ, đồng bộ và nhắc nhở** một cách hoàn hảo.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** lên đến **90%** trong việc xử lý email học đường.
✅ **Không bao giờ bỏ lỡ** thông báo quan trọng nhờ AI phân loại chính xác.
✅ **Lịch học và đồ mang theo** tự động đồng bộ vào Google Calendar.
✅ **Tất cả thông tin** được lưu trữ sạch sẽ trong Google Drive.
✅ **Nhắc nhở hàng ngày** về các sự kiện cần chuẩn bị đồ mang theo.
✅ **Dễ dàng tra cứu** thông tin qua Google Drive hoặc lịch Google.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google** (Gmail, Google Calendar, Google Drive) với quyền truy cập đầy đủ.
2. **API Key OpenAI** (để sử dụng AI phân loại email).
3. **Folder trong Google Drive** để lưu trữ:
   - Thông báo (Notices).
   - Danh sách đồ mang theo (What to Bring).
   - Ảnh đính kèm (Photos).
   - Danh sách liên lạc (Contacts).
4. **Email nhận nhắc nhở** (để nhận thông báo hàng ngày về đồ mang theo).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/11529](https://n8n.io/workflows/11529) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ file và dán vào **Import Workflow** trong n8n.
- **Cách 3:** Tạo workflow mới và sao chép từng node theo thứ tự trong danh sách dưới đây.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **19 node** và được chia thành **3 phần chính**:
- **Phần 1: Phân loại email** (AI + Gmail).
- **Phần 2: Lưu trữ và đồng bộ** (Google Drive + Calendar).
- **Phần 3: Nhắc nhở hàng ngày** (Schedule Trigger).

##### **🔹 Phần 1: Phân Loại Email (AI + Gmail)**
| Node | Tên | Cấu Hình Cần Chỉnh |
|------|-----|---------------------|
| **When Email Arrives** | `gmailTrigger` | Chọn **Gmail** và **label** (ví dụ: "School Emails"). |
| **Get a message** | `gmail` | Chọn **operation: get** và liên kết với `When Email Arrives`. |
| **Extract Email Info** | `informationExtractor` | Cấu hình **prompt AI** để trích xuất:
   - Ngày sự kiện.
   - Tên học sinh.
   - Danh sách đồ mang theo.
   - Thông tin liên lạc. |
| **OpenAI Chat Model** | `lmChatOpenAi` | Điền **API Key OpenAI** và chọn mô hình `gpt-4.1-mini`. |
| **Route by Category** | `switch` | Cấu hình các điều kiện phân loại:
   - **Schedule** (lịch học).
   - **What to Bring** (đồ mang theo).
   - **Notice** (thông báo).
   - **Contacts** (liên lạc). |

##### **🔹 Phần 2: Lưu Trữ & Đồng Bộ (Google Drive + Calendar)**
| Node | Tên | Cấu Hình Cần Chỉnh |
|------|-----|---------------------|
| **Workflow Configuration** | `set` | Điền:
   - **Folder ID Google Drive** (để lưu thông báo, đồ mang theo, ảnh).
   - **Calendar ID Google Calendar** (để đồng bộ lịch). |
| **Save Notice to Drive** | `googleDrive` | Chọn **operation: createFromText** và liên kết với folder "Notices". |
| **Prepare Calendar Event** | `set` | Cấu hình tiêu đề, ngày giờ, mô tả (đồ mang theo). |
| **Add to Calendar** | `googleCalendar` | Chọn **calendar ID** từ `Workflow Configuration`. |
| **Get Email Attachments** | `gmail` | Chọn **operation: get** và lọc file đính kèm. |
| **Filter Photos Only** | `filter` | Lọc chỉ các file có định dạng `image/*`. |
| **Save Photos to Drive** | `googleDrive` | Chọn folder "Photos" và **operation: createFile**. |
| **Extract Contacts** | `set` | Trích xuất tên, email, số điện thoại từ email. |
| **Save Contacts to Drive** | `googleDrive` | Lưu vào file "Contacts.txt" với định dạng:
   ```
   Tên: Email | Số điện thoại
   ```

##### **🔹 Phần 3: Nhắc Nhở Hàng Ngày**
| Node | Tên | Cấu Hình Cần Chỉnh |
|------|-----|---------------------|
| **Daily Reminder Check** | `scheduleTrigger` | Chọn **thời gian chạy hàng ngày** (ví dụ: 7h sáng). |
| **Get Tomorrow's Events** | `googleCalendar` | Chọn **operation: getAll** và lọc ngày mai. |
| **Filter What to Bring Events** | `filter` | Lọc sự kiện có mô tả chứa từ khóa **"đồ mang theo"**, **"what to bring"**, **"持ち物"**. |
| **Send Reminder Email** | `gmail` | Điền **email nhận nhắc nhở** và cấu hình nội dung email. |

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với 1-2 email mẫu từ trường học.
2. Kiểm tra:
   - Email có được phân loại chính xác không?
   - Lịch và Drive có đồng bộ không?
   - Nhắc nhở hàng ngày có hoạt động không?
3. **Bật Active** workflow sau khi kiểm tra thành công.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Google Sheets**
   - Thêm node `googleSheets` để lưu trữ lịch sử email vào bảng tính.
   - Cấu hình **auto-refresh** để theo dõi tất cả thông báo.

2. **Nhắc Nhở qua Slack/Telegram**
   - Thêm node `slack` hoặc `telegramBot` vào phần nhắc nhở hàng ngày.
   - Cấu hình **webhook** từ Slack/Telegram để nhận thông báo.

3. **Lưu Log Cho Dễ Dàng Debug**
   - Thêm node `stickyNote` để ghi lại lỗi hoặc thông tin debug.
   - Sử dụng **Google Drive** để lưu log chi tiết.

4. **Tùy Chỉnh AI Phân Loại**
   - Cập nhật **prompt** trong node `informationExtractor` để phù hợp với cách viết email của trường.
   - Ví dụ: Nếu trường thường dùng từ **"chú ý"** thay vì **"notice"**, cập nhật điều kiện phân loại.

5. **Tự Động Xóa Email Sau Xử Lý**
   - Thêm node `gmail` với **operation: delete** sau khi xử lý xong email.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các bậc phụ huynh, giúp họ **không bao giờ bỏ lỡ thông báo quan trọng** từ trường học. Với sự kết hợp giữa **AI phân loại, Google Calendar và Google Drive**, mọi thông tin đều được **tự động hóa, sắp xếp và nhắc nhở** một cách hoàn hảo.

**🚀 Hãy áp dụng ngay và trải nghiệm sự tiện lợi mà tự động hóa mang lại!**
Nếu có vấn đề, hãy để lại comment bên dưới hoặc liên hệ với cộng đồng n8n để được hỗ trợ.

---
**🔗 [Tải workflow gốc tại đây](https://n8n.io/workflows/11529)** | **📌 [Cài đặt n8n Self-hosted](https://docs.n8n.io/)**