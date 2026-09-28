---
title: "🚀 Tự Động Hoàn Thành CV Chuyên Nghiệp Từ File PDF - Google Sheet Cấu Trúc (Không Cần Code)"
description: "Upload CV PDF vào form, workflow tự động trích xuất và phân loại thông tin (kinh nghiệm, học vấn, kỹ năng, liên lạc) vào Google Sheet chuyên dụng - tiết kiệm 80% thời gian soạn thảo CV cho các sếp HR và ứng viên. Hoạt động 24/7 trên VPS riêng."
slug: "tieu-dong-hoan-thanh-cv-google-sheet"
tags: [n8n, automation, no-code, google-sheets, ai-summarization, cv-automation, easybits]
keywords: [tự động hóa cv, trích xuất cv pdf, google sheet cv, n8n workflow cv, tự động hóa ứng tuyển việc làm, easybits n8n]
---

# 🚀 **Tự Động Hoàn Thành CV Chuyên Nghiệp Từ File PDF - Google Sheet Cấu Trúc**

### **Giải pháp cho các sếp HR và ứng viên:**
Sao chép, dán, chỉnh sửa lại thông tin từ hàng chục CV PDF vào Google Sheet để quản lý? **Đã quá thời đại!** Workflow này tự động trích xuất **kinh nghiệm làm việc, học vấn, kỹ năng, và thông tin liên lạc** từ CV PDF của ứng viên, sau đó **cấu trúc lại thành 4 tab riêng biệt** trong Google Sheet. Kết quả? Một **CV Master Database** sẵn sàng tái sử dụng cho việc **tùy chỉnh ứng tuyển, theo dõi hồ sơ, phân tích kĩ năng** mà không cần viết một dòng code nào.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7** và xử lý hàng loạt CV, các sếp nên **self-host** n8n trên VPS riêng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian** soạn thảo CV: Không cần sao chép thủ công từ PDF sang Sheet.
✅ **Dữ liệu chính xác & cấu trúc**: Trích xuất **kinh nghiệm, học vấn, kỹ năng** theo định dạng chuẩn.
✅ **Tái sử dụng linh hoạt**: Dữ liệu trong Google Sheet có thể **kết nối với Slack/Telegram** để thông báo, hoặc **tích hợp với CRM** để theo dõi ứng viên.
✅ **Hoạt động liên tục**: Chạy tự động 24/7 trên VPS, không phụ thuộc vào thời gian làm việc.
✅ **Tùy chỉnh dễ dàng**: Thêm/loại tab trong Google Sheet mà không cần sửa code.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để tạo Google Sheet và kết nối API).
2. **Tài khoản easybits** ([đăng ký miễn phí](https://easybits.tech)) để lấy **API Key**.
3. **Google Sheet có tên "Master CV"** với **4 tab** (cấu trúc chi tiết dưới đây).
4. **VPS hoặc n8n Cloud** (nếu self-host, cần cài đặt **@easybits/n8n-nodes-extractor**).

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15528](https://n8n.io/workflows/15528) hoặc copy/paste JSON vào **n8n Editor**.
- **Nếu self-host**, cài đặt **easybits Extractor** qua **Settings → Community Nodes** và nhập `@easybits/n8n-nodes-extractor`.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **A. Cấu trúc Google Sheet "Master CV"**
Tạo **1 Google Sheet** với **4 tab** sau (đặt tên chính xác như dưới đây):
| **Tab**       | **Cột**               | **Mô tả**                                                                 |
|---------------|-----------------------|---------------------------------------------------------------------------|
| **Master CV** | `role`, `company`, `dates`, `bullets`, `skills` | Dữ liệu kinh nghiệm làm việc.                                           |
| **Education** | `degree`, `institution`, `dates`, `details`   | Dữ liệu học vấn (trường, ngành, năm học).                                |
| **Skills**    | `skill`               | Danh sách kỹ năng (không trùng lặp, không bao gồm soft skills).          |
| **Summary**   | `full_name`, `email`, `linkedin_url`, `location`, `summary`, `languages`, `links` | Thông tin tổng quan và liên lạc của ứng viên.                          |

- **Không để dữ liệu nào dưới header** (workflow sẽ tự động append).
- **Mở quyền chia sẻ** cho Google Sheets API (Settings → Share → "Anyone with the link can view").

#### **B. Cấu hình Node `easybits: Extract CV`**
- **Đăng nhập easybits** và lấy **API Key** từ [easybits.tech](https://easybits.tech).
- Trong node này, **cấu hình 10 trường trích xuất** (đọc hướng dẫn chi tiết [ở đây](#4-configure-the-extraction-pipeline)).
- **Lưu ý**:
  - Trường `experiences` và `education` phải là **mảng JSON** (mỗi mục là 1 object).
  - Trường `skills` **không trùng lặp** và **không bao gồm soft skills** (ví dụ: "teamwork").

#### **C. Cấu hình Node `Append` (Google Sheets)**
- Mở từng node `Append` (Master CV, Education, Skills, Summary).
- **Chọn credential Google Sheets** đã cấu hình trước.
- **Điền ID của Google Sheet** (tìm trong URL: `https://docs.google.com/spreadsheets/d/[ID]/edit`).
- **Chọn tab tương ứng** (ví dụ: `Master CV` → tab `Master CV`).

#### **D. Node `Fan-out` (Code)**
- **Không cần chỉnh sửa** (node này tự động phân tách dữ liệu từ easybits thành 4 dạng riêng biệt).
- **Nếu gặp lỗi**, kiểm tra rằng **dữ liệu từ easybits** có định dạng đúng (JSON, không phải string).

#### **E. Node `Show Completion Screen`**
- **Không cần cấu hình thêm**, node này tự động hiển thị **bảng thống kê** sau khi hoàn thành (ví dụ: "Đã trích xuất 3 kinh nghiệm, 2 học vấn, 10 kỹ năng").

---

### **3. Kích hoạt ⚡️**
1. **Test run** với 1 CV mẫu (PDF/PNG/JPEG).
2. **Kiểm tra 4 tab** trong Google Sheet:
   - Nếu có lỗi (ví dụ: trùng lặp, thiếu dữ liệu), **sửa cấu trúc trong easybits Extractor**.
3. **Bật Active** workflow và chia sẻ **link form upload** cho ứng viên.

---
## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tích hợp với Slack/Telegram**
- **Thêm node `Slack`** sau `Merge` để gửi thông báo khi trích xuất thành công:
  ```json
  {
    "operation": "sendMessage",
    "message": "CV của {{ $input.json.data.full_name }} đã được trích xuất thành công!"
  }
  ```

### **2. Lưu log hoạt động**
- **Thêm node `Set`** trước `Merge` để lưu dữ liệu vào **Google Sheets Log**:
  ```json
  {
    "operation": "append",
    "sheetName": "Log",
    "columns": ["timestamp", "full_name", "status"]
  }
  ```

### **3. Tùy chỉnh easybits Extractor**
- Nếu **easybits không trích xuất chính xác**, thử:
  - **Upload CV khác định dạng** (PDF chứ không phải PNG).
  - **Cập nhật cấu trúc trong easybits** (ví dụ: thay đổi cách định dạng `dates` trong `experiences`).

### **4. Tạo báo cáo định kỳ**
- **Sử dụng node `Google Sheets` + `Schedule`** để tự động **tạo báo cáo tổng hợp** hàng tuần:
  ```json
  {
    "operation": "create",
    "sheetName": "Báo cáo tuần",
    "columns": ["tổng kinh nghiệm", "tổng kỹ năng", "người mới nhất"]
  }
  ```

---

## 📌 **Kết luận**
Workflow này **giải phóng các sếp HR khỏi công việc thủ công** và **tạo ra một CV Master Database** sẵn sàng tái sử dụng. **Không cần code, không cần kiến thức kỹ thuật** - chỉ cần **upload CV PDF**, workflow sẽ tự động **trích xuất, cấu trúc và lưu trữ** dữ liệu vào Google Sheet.

👉 **Bắt đầu ngay!**
1. **Import workflow** từ [n8n.io/workflows/15528](https://n8n.io/workflows/15528).
2. **Cấu hình Google Sheet và easybits** theo hướng dẫn.
3. **Bật workflow** và chia sẻ link upload cho ứng viên.

**Hãy tự động hóa CV của bạn hôm nay!** 🚀