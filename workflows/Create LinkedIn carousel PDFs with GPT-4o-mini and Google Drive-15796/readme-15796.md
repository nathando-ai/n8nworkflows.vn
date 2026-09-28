---
title: "🚀 Tự Động Hoàn Thành Carousel PDF LinkedIn Với GPT-4o-mini + Google Drive – Không Cần Code!"
description: "Workflow tự động hóa tạo carousel PDF LinkedIn chuyên nghiệp từ 1 chủ đề duy nhất, với nội dung AI sinh tạo, thiết kế branding cá nhân hóa và tự động upload lên Google Drive. Giúp các sếp tiết kiệm 10+ giờ/lần so với cách làm thủ công."
slug: "tieu-dong-hoan-thanh-carousel-pdf-linkedin-gpt-4o-mini"
tags: [n8n, automation, content-creation, ai-multimodal, google-drive, linkedin-automation]
keywords: [n8n workflow linkedin, tự động hóa content marketing, tạo carousel pdf ai, gpt-4o-mini n8n, google drive automation, template linkedin post]
---

# 🚀 **Tự Động Hoàn Thành Carousel PDF LinkedIn Với GPT-4o-mini – Từ Chủ Đề Đến Post Chỉ Với 1 Clic!**

Hãy tưởng tượng: Bạn chỉ cần nhập **1 chủ đề** (ví dụ: *"Tại sao AI sẽ thay đổi ngành marketing trong 5 năm tới?"*), chọn **brand name**, **đối tượng mục tiêu**, và **tone** (chuyên nghiệp, thân thiện, hài hước...), workflow sẽ tự động:
✅ **Sinh tạo nội dung** cho carousel với **GPT-4o-mini** (mô hình AI mới nhất của OpenAI).
✅ **Thiết kế PDF** với **branding cá nhân hóa** (màu sắc, font, logo, background).
✅ **Upload tự động** lên **Google Drive** và **ghi log** vào Google Sheets.
✅ **Gửi email** với link download và hướng dẫn post trên LinkedIn.

**Kết quả?** Một **carousel PDF LinkedIn hoàn chỉnh**, sẵn sàng upload chỉ trong **vài giây**, thay vì mất **10+ giờ** để viết, thiết kế và upload thủ công.

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
- **Tiết kiệm thời gian**: Từ **10+ giờ** viết thiết kế thành **1 phút** nhập form.
- **Nội dung chuyên nghiệp**: AI sinh tạo **cấu trúc logic**, **tôn chỉ phù hợp**, và **CTA hiệu quả**.
- **Branding thống nhất**: PDF được thiết kế với **màu sắc, font, và logo** của brand.
- **Hoạt động 24/7**: Workflow chạy tự động, không cần can thiệp thủ công.
- **Dễ dàng chia sẻ**: PDF được upload lên **Google Drive** và gửi qua **email** với link trực tiếp.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** (để sử dụng GPT-4o-mini):
   - [Đăng ký tài khoản OpenAI](https://platform.openai.com/signup) (mã giảm giá: **N8NOPENAI** - giảm 20% phí đầu tiên).
   - **API Key** để kết nối với node `OpenAI — GPT-4o-mini Model`.

2. **Tài khoản Google** (để sử dụng Google Drive và Google Sheets):
   - [Đăng ký Google Workspace](https://workspace.google.com/) (nếu chưa có).
   - **OAuth2 Credential** cho:
     - **Google Drive** (để upload PDF).
     - **Google Sheets** (để ghi log).

3. **Tài khoản Gmail** (để nhận email chứa PDF và link download).

4. **Server n8n Self-hosted** (không dùng n8n.cloud):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - **Cài đặt n8n** theo hướng dẫn [n8n.io](https://docs.n8n.io/).
   - **Cài đặt thư viện `html-pdf-node`** trên server:
     ```bash
     npm install html-pdf-node
     ```
     (Nếu dùng Docker: `docker exec -it n8n npm install html-pdf-node`).

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/15796) và import vào **n8n Editor**.
- **Copy JSON** từ link trên và **paste** vào **Import Workflow** trong n8n.

:::note[**Lưu ý quan trọng**]
- **Không dùng n8n.cloud** vì workflow cần **server self-hosted** để chạy `html-pdf-node`.
- **Không xóa node nào** trong workflow, chỉ chỉnh sửa các tham số sau.
:::

---

### **2. Các Lưu Ý Bắt Buộc Phải Chỉnh 📌**

#### **A. Cấu Hình Credentials**
Các node quan trọng cần **cấu hình kỹ lưỡng**:

| **Node**                          | **Thao Tác Cần Làm**                                                                 | **Tham Số Cần Điền**                          |
|-----------------------------------|--------------------------------------------------------------------------------------|-----------------------------------------------|
| **1. Form — Carousel Topic + Details** | Không cần chỉnh, chỉ nhập dữ liệu khi chạy.                                   | -                                             |
| **2. AI Agent — Generate Slide Content** | Kết nối **OpenAI Credential** (đã tạo ở bước chuẩn bị).                     | -                                             |
| **OpenAI — GPT-4o-mini Model**     | Chọn **model: gpt-4o-mini** (đã mặc định).                                       | -                                             |
| **3. Code — Parse Slides JSON**    | **Không cần chỉnh**, chỉ chạy thử để kiểm tra.                                | -                                             |
| **4. Code — Build HTML Slides**    | **Cập nhật BRAND SETTINGS** ở phần code:                                      | `BRAND_COLOR`: Màu hex của brand (ví dụ: `#FF5733`).<br>`FONT`: Font phù hợp (ví dụ: `'Arial'`). |
| **5. Code — Generate PDF**         | **Không cần chỉnh**, chỉ chạy thử để kiểm tra.                                | -                                             |
| **6. Google Drive — Upload PDF**   | Kết nối **Google Drive OAuth2 Credential** và điền:                            | `YOUR_GDRIVE_FOLDER_ID`: ID của folder muốn upload.<br>**Lấy ID folder**:<br>1. Mở Google Drive.<br>2. Chọn folder.<br>3. URL sẽ là: `https://drive.google.com/drive/folders/FOLDER_ID` → **copy `FOLDER_ID`**. |
| **7. Google Sheets — Log Carousel** | Kết nối **Google Sheets OAuth2 Credential** và điền:                          | `YOUR_GOOGLE_SHEET_ID`: ID của sheet (lấy tương tự folder).<br>**Tạo tab "Carousel Log"** với 9 cột:<br>`Date, Topic, Brand Name, Slide Count, File Name, Drive Link, Drive File ID, PDF Size (bytes), Generated On`. |
| **8. Gmail — Email PDF to You**    | Kết nối **Gmail OAuth2 Credential** và điền:                                    | `YOUR_EMAIL_ADDRESS`: Email nhận PDF.          |

#### **B. Kiểm Tra Code Node (Nếu Cần Chỉnh Sửa)**
Nếu muốn **thay đổi thiết kế PDF**, các sếp có thể chỉnh sửa **Code Node 4** (`Build HTML Slides`). Ví dụ:
```javascript
// BRAND SETTINGS (chỉnh ở đây)
const BRAND_COLOR = "#FF5733"; // Màu hex của brand
const FONT = "'Arial', sans-serif"; // Font
```
**Lưu ý**: Chỉ chỉnh **BRAND_COLOR** và **FONT** để tránh lỗi.

---

### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhập vào **Form**:
     - **Topic**: *"Tại sao AI sẽ thay đổi ngành marketing trong 5 năm tới?"*
     - **Brand Name**: *"BrandName"*
     - **Target Audience**: *"Marketing Manager"*
     - **Tone**: *"Chuyên nghiệp"*
     - **Slide Count**: *"5"*
   - Chạy **Test Run** để kiểm tra:
     - AI có sinh tạo nội dung không?
     - PDF có được tạo và upload lên Drive không?
     - Email có được gửi không?

2. **Bật Active**:
   - Sau khi test thành công, **bật Active** workflow.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Tối Ưu Hóa AI Prompt**
Nếu muốn **nội dung chuyên sâu hơn**, các sếp có thể **cập nhật prompt** trong **AI Agent Node**:
```json
"prompt": "Tạo một carousel LinkedIn với {{topic}} dành cho {{targetAudience}} với tone {{tone}}. Mỗi slide phải có: headline, emoji, subtitle, và 3 điểm chính. Đảm bảo kết thúc với CTA mạnh mẽ."
```
**Ví dụ**:
```json
"prompt": "Tạo một carousel LinkedIn về 'Tại sao AI sẽ thay đổi ngành marketing trong 5 năm tới?' dành cho 'Marketing Manager' với tone 'Chuyên nghiệp'. Mỗi slide phải có headline, emoji, subtitle, và 3 điểm chính. Đảm bảo kết thúc với CTA mạnh mẽ như 'Bắt đầu triển khai AI ngay hôm nay!'"
```

### **2. Tự Động Gửi Carousel Đến Slack/Telegram**
Thay vì email, các sếp có thể **thêm node Slack/Telegram** để thông báo khi PDF sẵn sàng:
1. **Thêm node `Slack`** (nếu dùng Slack) hoặc `Telegram Bot` (nếu dùng Telegram).
2. **Kết nối credential** và cấu hình:
   - **Message**: `"Carousel PDF đã sẵn sàng! Link: {{driveLink}}"`.
   - **Attachments**: Gửi **PDF** hoặc **link preview**.

### **3. Lưu Log Lịch Sử Tất Cả Carousel**
Thay vì chỉ ghi vào **Google Sheets**, các sếp có thể:
- **Thêm node `Google Drive — Create Folder`** để tạo **folder mới** cho mỗi carousel.
- **Thêm node `StickyNote`** để lưu **lịch sử chạy** (ví dụ: ngày tạo, chủ đề, link).

### **4. Chia Sẻ Workflow Cho Đội Ngũ**
- **Export workflow** thành file JSON và chia sẻ cho **nhóm content**.
- **Tạo form riêng** cho mỗi người dùng với **brand name khác nhau**.

---
## 📌 **Kết Luận: Hãy Tự Động Hóa Content Marketing Ngay Hôm Nay!**

Workflow này **giải phóng thời gian** cho các sếp từ việc viết, thiết kế, và upload carousel LinkedIn thủ công. **Chỉ với 1 form**, bạn có ngay:
✔ **Nội dung AI sinh tạo** (logic, chuyên nghiệp).
✔ **Thiết kế branding** (màu sắc, font, logo).
✔ **Upload tự động** lên Google Drive.
✔ **Email tự động** với link download.

**Hành động ngay!**
1. **Chuẩn bị tài khoản** (OpenAI, Google, Gmail).
2. **Cài đặt n8n + html-pdf-node** trên VPS.
3. **Import workflow** và **cấu hình credentials**.
4. **Test run** và **bật Active**.

**👉 [Tải workflow ngay](https://n8n.io/workflows/15796) và bắt đầu tự động hóa content marketing của mình!**

---
**💡 Mẹo cuối**: Nếu gặp lỗi, hãy **check log** trong **StickyNote Node** hoặc **Google Sheets Log** để debug. Nếu cần hỗ trợ, comment bên dưới hoặc liên hệ [Incrementors](https://incrementors.com/).