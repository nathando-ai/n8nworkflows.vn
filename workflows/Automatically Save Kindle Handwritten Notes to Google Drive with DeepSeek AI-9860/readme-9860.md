---
title: "📚 Tự Động Lưu Ghi Chú Sách Kindle (Ghi Chép Tay) Vào Google Drive Với AI DeepSeek - Không Cần Code!"
description: "Giải pháp tự động hóa hoàn toàn để tự động lấy PDF ghi chú Kindle (Scribe) từ email, tách URL tải xuống bằng AI DeepSeek, và lưu vào Google Drive 24/7. Tiết kiệm thời gian, tránh mất dữ liệu và truy cập dễ dàng mọi lúc."
slug: "tieu-dong-luu-ghi-chu-kindle-vao-google-drive"
tags: [n8n, automation, no-code, ai-summarization, google-drive, kindle, deepseek]
keywords: [tự động hóa kindle, lưu ghi chú kindle vào google drive, ai deepseek n8n, tự động hóa email pdf, lưu trữ ghi chú sách]
---

# 🚀 **Tự Động Lưu Ghi Chú Sách Kindle (Ghi Chép Tay) Vào Google Drive Với AI DeepSeek**

### **Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Các sếp đang sử dụng **Kindle Scribe** (hoặc các mẫu Kindle hỗ trợ ghi chú tay) nhưng gặp khó khăn khi muốn lưu trữ ghi chú lâu dài? Hiện tại, Amazon **không cung cấp API hoặc kho lưu trữ trung tâm** cho các file PDF export từ ghi chú Kindle. Khi bạn yêu cầu export ghi chú, Amazon sẽ gửi email chứa **một liên kết tải xuống tạm thời** (không phải là file đính kèm). Quá trình này yêu cầu:
✅ **Mở email** → **Tìm liên kết** → **Tải PDF** → **Lưu vào Google Drive/OneDrive** → **Xóa email** (để tránh mất liên kết).
→ **Tốn thời gian, dễ quên, và rủi ro mất dữ liệu** nếu không lưu kịp thời.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✔ **Tự động nhận email export từ Kindle** (không cần can thiệp).
✔ **Sử dụng AI DeepSeek** để **tự động tìm và tách URL tải PDF** (không cần regex phức tạp).
✔ **Tải PDF và lưu vào Google Drive** một cách tự động.
✔ **Gửi thông báo thành công qua email** khi hoàn tất.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần mở email, copy URL, tải PDF thủ công.
- **Tránh mất dữ liệu**: Lưu trữ tự động vào Google Drive, không phụ thuộc vào email.
- **Truy cập dễ dàng**: Tất cả ghi chú Kindle được **sắp xếp theo thư mục** trong Google Drive.
- **Không cần kỹ thuật**: Chỉ cần cấu hình 1 lần, workflow chạy **một mình** 24/7.
- **Chính xác cao**: AI DeepSeek **tự động tìm URL** trong email, không cần regex.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✅ **Tài khoản Kindle Scribe** (hoặc Kindle hỗ trợ ghi chú tay).
✅ **Email Gmail** (để Kindle gửi export PDF).
✅ **Tài khoản Google Drive** (để lưu trữ ghi chú).
✅ **API Key DeepSeek** (miễn phí, đăng ký tại [deepseek.ai](https://deepseek.ai/)).
✅ **Thư mục Google Drive** đã tạo sẵn (ví dụ: `Kindle Notes Backup`).

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/9860](https://n8n.io/workflows/9860) (chọn **Export as JSON**).
2. **Mở n8n Editor** (trên VPS hoặc n8n.cloud).
3. **Nhấp vào "Import"** → **Chọn file JSON** → **Nhấp "Import"**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/9860](https://n8n.io/workflows/9860).
2. **Mở n8n Editor** → **Nhấp "Import"** → **Chọn "Paste JSON"** → **Nhấp "Import"**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **7 node chính**, các sếp cần **cấu hình kỹ lưỡng** các phần sau:

#### **🔹 Node 1: Email Ingestion (Gmail Trigger)**
- **Cấu hình:**
  - **Credentials:** Chọn `gmailOAuth2` (đã cấu hình trước).
  - **Label:** `Kindle Notes Export` (để workflow chỉ lấy email có nhãn này).
  - **From:** `amazon@kindle.com` (hoặc địa chỉ email của Kindle gửi export).
  - **Subject:** Chứa từ khóa như `"Your Kindle Notes Export"` (các sếp có thể điều chỉnh theo email thực tế).

#### **🔹 Node 2: Convert Email to HTML**
- **Không cần chỉnh sửa**, node này **tự động chuyển email thành HTML** để AI dễ dàng phân tích.

#### **🔹 Node 3: DeepSeek Chat Model (Trích Xuất URL)**
- **Cấu hình:**
  - **Credentials:** Chọn `deepSeekApi` (đã đăng ký API Key).
  - **Model:** `deepseek-reasoner` (mặc định).
  - **Prompt:** (Không cần chỉnh sửa, AI sẽ tự động tìm URL trong email).
  - **Lưu ý:**
    - Nếu **DeepSeek API bị giới hạn**, các sếp có thể thử **mô hình khác** như `deepseek-coder` (nếu cần).
    - **Không cần regex**, AI sẽ **tự động trích xuất URL** trong email.

#### **🔹 Node 4: HTTP Request (Tải PDF)**
- **Cấu hình:**
  - **URL:** `{$.json.url}` (URL được trích xuất từ Node 3).
  - **Method:** `GET`.
  - **Headers:** `Accept: application/pdf`.
  - **Lưu ý:**
    - Nếu URL **hết hạn**, workflow sẽ **bị lỗi**. Để tránh, các sếp nên **lưu PDF ngay lập tức** sau khi tải.

#### **🔹 Node 5: Upload PDF to Google Drive**
- **Cấu hình:**
  - **Credentials:** Chọn `googleDriveOAuth2Api`.
  - **Folder:** Chọn thư mục đã tạo sẵn (ví dụ: `Kindle Notes Backup`).
  - **File Name:** `{$.json.filename}` (hoặc `{$.json.subject}` nếu email có subject là tên file).
  - **Lưu ý:**
    - Nếu **Google Drive không cho phép upload**, kiểm tra **quyền truy cập** của OAuth2.

#### **🔹 Node 6: Success Notification (Email)**
- **Cấu hình:**
  - **Credentials:** Chọn `gmailOAuth2`.
  - **To:** Email của các sếp.
  - **Subject:** `📄 Kindle Notes Backup Success!`.
  - **Body:** `File đã được lưu thành công vào Google Drive: [LINK]`.

#### **🔹 Node 7: AI Agent (Link Extraction)**
- **Không cần chỉnh sửa**, node này **tự động xử lý** để trích xuất URL từ email.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** (để kiểm tra):
   - **Gửi email mẫu** từ Kindle (hoặc mô phỏng email export).
   - **Chạy workflow** và kiểm tra:
     - AI có trích xuất URL không?
     - PDF có tải và lưu vào Google Drive không?
     - Email thông báo có gửi được không?
2. **Bật Active**:
   - Sau khi test thành công, **nhấp "Active"** để workflow chạy tự động.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Tự Động Xóa Email Sau Lưu Trữ**
- **Thêm Node Gmail Delete** sau Node 5 để **xóa email đã xử lý** (tránh tích lũy email).
- **Cấu hình:**
  - **Credentials:** `gmailOAuth2`.
  - **Message ID:** `{$.json.id}` (ID email từ Node 1).

### **2. Lưu Log Lịch Sử vào Google Sheets**
- **Thêm Node Google Sheets** để **ghi lại lịch sử backup**:
  - **Credentials:** `googleSheetsOAuth2`.
  - **Sheet Name:** `Kindle Notes Log`.
  - **Dữ liệu ghi:** `Tên file, Ngày giờ, Email gửi`.

### **3. Gửi Báo Cáo Định Kỳ (Hàng Tháng)**
- **Sử dụng Node Schedule** (n8n Pro) để **gửi email báo cáo** tổng hợp:
  - **Danh sách file đã lưu**.
  - **Số lượng ghi chú mới**.
  - **Liên kết truy cập Google Drive**.

### **4. Kết Hợp Với Slack/Telegram**
- **Thêm Node Slack/Telegram** để **thông báo tức thời** khi có ghi chú mới:
  - **Message:** `📚 New Kindle Notes Backup: [FILE_NAME]`.

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp khỏi việc **làm thủ công** với ghi chú Kindle, đồng thời **tránh mất dữ liệu** và **tăng tính chuyên nghiệp** trong quản lý tài liệu. **Chỉ cần cấu hình 1 lần**, workflow sẽ **chạy tự động** mọi lúc, giúp các sếp **tập trung vào công việc quan trọng hơn**.

**Hành động ngay hôm nay:**
1. **Cài đặt n8n trên VPS** (nếu chưa có).
2. **Import workflow** và **cấu hình các credentials**.
3. **Test và bật Active** để **tự động hóa ngay từ bây giờ!**

---
**💡 Cần hỗ trợ?** Đăng ký **khóa học tự động hóa n8n** tại [n8n.vn](https://n8n.vn) để học cách **tạo workflow tự động hóa hiệu quả**!