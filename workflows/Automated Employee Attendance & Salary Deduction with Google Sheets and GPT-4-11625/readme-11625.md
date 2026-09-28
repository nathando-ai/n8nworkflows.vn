---
title: "🚀 Tự Động Hóa Bảng Chấm Công & Trừ Lương Cho Nhân Viên Với Google Sheets & GPT-4 (Không Cần Code)"
description: "Workflow tự động hóa tính toán chấm công hàng tháng, tính trừ lương dựa trên thời gian làm việc và vắng mặt, tự động tổng hợp báo cáo AI và gửi email cá nhân hóa cho từng nhân viên. Giúp HR tiết kiệm 10+ giờ công mỗi tháng và giảm thiểu sai sót trong tính lương."
slug: "tieu-dong-hoa-bang-cham-cong-tru-luong-google-sheets-gpt-4"
tags: [n8n, automation, hr, google-sheets, ai-summarization, gpt-4, no-code, payroll]
keywords: [tự động hóa bảng chấm công, trừ lương tự động n8n, gpt-4 tổng hợp báo cáo nhân sự, google sheets tính lương, workflow hr không code]
---

# 🚀 **Tự Động Hóa Bảng Chấm Công & Trừ Lương Cho Nhân Viên Với Google Sheets & GPT-4**

### **Giải pháp hoàn hảo cho HR: Tính toán chấm công, trừ lương tự động + báo cáo AI cá nhân hóa**
Hiện nay, việc tính toán chấm công hàng tháng và tính trừ lương cho từng nhân viên vẫn là một công việc **mệt mỏi, dễ sai sót** và tốn nhiều thời gian của bộ phận HR. Các sếp phải:
- **Tính toán thủ công** thời gian làm việc, vắng mặt, và trừ lương cho từng nhân viên.
- **Tạo báo cáo** chi tiết để gửi cho từng người, dễ dẫn đến **sai sót trong số liệu**.
- **Quản lý nhiều file Excel/Google Sheets** khác nhau, khó theo dõi và cập nhật.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động tính toán** thời gian làm việc và trừ lương dựa trên dữ liệu chấm công từ Google Sheets.
✅ **Sử dụng GPT-4** để **tổng hợp báo cáo AI** rõ ràng, cá nhân hóa cho từng nhân viên.
✅ **Gửi email tự động** với báo cáo chi tiết, **giảm thiểu sai sót** trong quá trình tính lương.
✅ **Lưu log toàn bộ quá trình** vào Google Sheets để **theo dõi và kiểm tra** dễ dàng.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ công** mỗi tháng cho bộ phận HR.
- **Giảm thiểu sai sót** trong tính toán trừ lương (không còn tính nhầm giờ làm việc).
- **Báo cáo AI cá nhân hóa** cho từng nhân viên, giúp họ hiểu rõ hơn về lương của mình.
- **Hoạt động tự động hàng tháng** (không cần can thiệp thủ công).
- **Lưu trữ toàn bộ dữ liệu** trong Google Sheets, dễ dàng kiểm tra và phân tích.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** với:
   - **Bảng chấm công** (cột: `Employee ID`, `Date`, `Clock In`, `Clock Out`).
   - **Bảng thông tin nhân viên** (cột: `Employee ID`, `Name`, `Salary`, `Email`).
   - **Bảng lưu log email** (để ghi nhận lịch sử gửi email).
   - **Bảng báo cáo tổng hợp** (để lưu kết quả cuối cùng).
2. **API Key OpenAI** (để sử dụng GPT-4).
3. **Thông tin SMTP** (để gửi email tự động, có thể dùng Gmail hoặc SMTP khác).
4. **Dữ liệu mẫu** (nếu muốn test trước khi chạy thực tế).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào n8n Editor:
- **Tải file JSON** từ [n8n.io/workflows/11625](https://n8n.io/workflows/11625) (nếu có quyền).
- **Hoặc copy toàn bộ JSON** từ link trên và dán vào **n8n Editor** → **Import Workflow**.

:::note[LƯU Ý]
- **Không copy/paste trực tiếp từ trang web** (do có ký tự đặc biệt), mà phải **tải file JSON** hoặc **sử dụng công cụ như Postman** để lấy JSON sạch.
- Nếu import từ file, **đảm bảo file JSON không bị hỏng**.
:::

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình Credentials (Tài khoản)**
Các sếp cần **cấu hình các credentials** sau trong n8n:
1. **Google API** (để kết nối với Google Sheets):
   - **Loại tài khoản**: OAuth 2.0 (đăng ký tại [Google Cloud Console](https://console.cloud.google.com/)).
   - **Scopes cần thiết**:
     - `https://www.googleapis.com/auth/spreadsheets`
     - `https://www.googleapis.com/auth/drive`
   - **Lưu ý**: Tạo **Service Account** và cấp quyền chỉnh sửa cho các bảng Google Sheets.

2. **OpenAI API** (để sử dụng GPT-4):
   - **API Key**: Mua tại [OpenAI Platform](https://platform.openai.com/) (mô hình `gpt-4.1-mini` được sử dụng).
   - **Lưu ý**: Đảm bảo tài khoản có **ngân sách đủ** để chạy AI.

3. **SMTP Credentials** (để gửi email tự động):
   - **Loại SMTP**: Gmail (hoặc SMTP khác như Zoho Mail, SendGrid).
   - **Thông tin cần thiết**:
     - **Host**: `smtp.gmail.com`
     - **Port**: `465` (hoặc `587` nếu dùng TLS).
     - **Username & Password**: Tài khoản email của bộ phận HR.
     - **Lưu ý**: **Bật "Dùng ứng dụng ít an toàn"** trong Gmail (nếu dùng Gmail).

---

#### **B. Cấu hình các Node quan trọng**
Các sếp cần **điều chỉnh các node sau** để phù hợp với dữ liệu của mình:

| **Node** | **Cần chỉnh sửa gì?** | **Ghi chú** |
|----------|------------------------|------------|
| **Schedule Trigger** | Thiết lập **thời gian chạy** (ví dụ: **ngày 1 hàng tháng**). | Nếu muốn chạy khác, chỉnh `cron` (ví dụ: `0 0 1 1 *` = ngày 1 hàng tháng). |
| **Employees Attendant Sheet** | **Điền link Google Sheet** chứa dữ liệu chấm công. | Cấu trúc cột: `Employee ID`, `Date`, `Clock In`, `Clock Out`. |
| **Employees Salary Sheet** | **Điền link Google Sheet** chứa thông tin nhân viên. | Cấu trúc cột: `Employee ID`, `Name`, `Salary`, `Email`. |
| **OpenAI Chat Model** | **Không cần chỉnh** (sử dụng `gpt-4.1-mini` mặc định). | Nếu muốn thay đổi mô hình, chỉnh `model` trong `keyParameters`. |
| **Adding the report to new sheet** | **Điền link Google Sheet** để lưu báo cáo cuối cùng. | Cấu trúc cột tự động tạo (không cần chỉnh). |
| **Save Email Log to Sheet** | **Điền link Google Sheet** để lưu log email. | Cấu trúc cột tự động tạo (không cần chỉnh). |
| **Send Salary Deduction Report Email** | **Chỉnh template email** (nếu muốn). | Có thể chỉnh nội dung email trong `emailSend` node. |

---

#### **C. Code Nodes (Cần kiểm tra)**
Workflow có **2 node Code** cần **không sửa** (nếu không biết lập trình):
1. **Calculate hours per day** (tính giờ làm việc).
2. **Calculate Salary Deduction** (tính trừ lương).
3. **Convert the result to JSON format** (định dạng dữ liệu).

:::warning[LƯU Ý]
- **Không chỉnh sửa code** nếu không hiểu, sẽ làm workflow **không hoạt động**.
- Nếu muốn **thay đổi công thức tính lương**, cần **hiểu rõ logic** trong code.
:::

---

### **3. Kích hoạt ⚡️**
1. **Test Run** (để kiểm tra dữ liệu mẫu):
   - Chọn **Test Tab** → **Run Workflow**.
   - Kiểm tra **log** để đảm bảo không có lỗi.
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** để workflow chạy tự động.

---
## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Cập nhật dữ liệu chấm công thường xuyên**
- Đảm bảo **bảng chấm công Google Sheets** được cập nhật **hàng ngày** để workflow tính toán chính xác.

### **2. Thêm báo cáo định kỳ cho quản lý**
- **Mở rộng workflow** để gửi **báo cáo tổng hợp cho quản lý** (ví dụ: tổng trừ lương, số nhân viên vắng mặt).
- **Sử dụng node `emailSend`** để gửi báo cáo cho bộ phận HR.

### **3. Lưu log chi tiết hơn**
- **Thêm cột** như `Status` (Đã gửi/Thất bại) và `Time Sent` vào bảng log email.
- **Sử dụng node `stickyNote`** để ghi chú lỗi nếu workflow bị ngắt.

### **4. Kết hợp với Slack/Telegram**
- **Thêm node `slackSend`** để thông báo khi workflow chạy thành công/thất bại.
- Ví dụ: **"Workflow trừ lương tháng 5 đã hoàn tất!"** hoặc **"Lỗi: Không tìm thấy dữ liệu cho nhân viên ABC"**.

### **5. Tự động gửi báo cáo cho bộ phận tài chính**
- **Thêm node `emailSend`** để gửi báo cáo tổng hợp cho bộ phận kế toán.

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa tính toán chấm công và trừ lương** mà **không cần viết code**. Với sự hỗ trợ của **Google Sheets, GPT-4 và email tự động**, bộ phận HR sẽ **tiết kiệm thời gian, giảm sai sót và cải thiện trải nghiệm của nhân viên**.

**Hành động ngay hôm nay:**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Import workflow** và **cấu hình credentials**.
3. **Test Run** và **bật Active** để tự động hóa quá trình tính lương!

---
:::success[💡 **Mẹo cuối cùng**]
Nếu gặp khó khăn trong quá trình cấu hình, **hãy liên hệ với cộng đồng n8n** tại [n8n Community](https://community.n8n.io/) hoặc **đăng ký VPS** để tự host n8n ổn định:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::