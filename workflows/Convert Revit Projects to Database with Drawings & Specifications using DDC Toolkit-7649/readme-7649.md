---
title: "🚀 Tự Động Hóa Chuyển Dữ Liệu Dự Án Revit Sang Cơ Sở Dữ Liệu Với Biểu Mẫu & Thông Số Chi Tiết (Không Cần Code)"
description: "Workflow này tự động chuyển đổi các dự án Revit thành cơ sở dữ liệu có cấu trúc, bao gồm cả các biểu đồ và thông số kỹ thuật, giúp các sếp tiết kiệm thời gian và giảm thiểu sai sót trong quá trình chuyển đổi thủ công."
slug: "tieu-dong-hoa-chuyen-doi-revit-sang-co-so-du-lieu"
tags: [n8n, automation, engineering, AEC, multimodal-ai, self-hosted]
keywords: [n8n workflow Revit, tự động hóa xây dựng, chuyển đổi Revit sang cơ sở dữ liệu, DDC Toolkit, Revit to database, AEC automation]
---

# 🚀 Tự Động Hóa Chuyển Dữ Liệu Dự Án Revit Sang Cơ Sở Dữ Liệu Với Biểu Mẫu & Thông Số Chi Tiết

### 🔍 **Nỗi Đau Của Các Sếp Trong Quá Trình Chuyển Dổi Revit**
Các sếp trong ngành xây dựng và kỹ thuật thường phải đối mặt với việc chuyển đổi dữ liệu từ các dự án Revit sang cơ sở dữ liệu thủ công. Quá trình này không chỉ tốn thời gian mà còn dễ gây ra sai sót, đặc biệt khi phải xử lý hàng loạt dự án với các biểu đồ, thông số kỹ thuật và cấu trúc phức tạp. Hơn nữa, việc này thường đòi hỏi kiến thức chuyên sâu về Revit và công cụ chuyển đổi, khiến nhiều người cảm thấy khó khăn trong việc tối ưu hóa quy trình.

Workflow này **giải quyết vấn đề này hoàn toàn tự động hóa**, giúp các sếp chuyển đổi dự án Revit sang cơ sở dữ liệu có cấu trúc một cách nhanh chóng, chính xác và không cần viết một dòng code nào.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định 24/7, các sếp nên cài đặt n8n trên một **VPS riêng** (Self-hosted) để đảm bảo tính liên tục và bảo mật.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Chuyển đổi hàng loạt dự án Revit chỉ trong vài phút thay vì nhiều giờ làm thủ công.
- **Chính xác cao**: Giảm thiểu sai sót trong quá trình chuyển đổi dữ liệu, đặc biệt là với các thông số kỹ thuật và biểu đồ.
- **Cấu trúc dữ liệu rõ ràng**: Dữ liệu được chuyển đổi thành cơ sở dữ liệu có cấu trúc, dễ dàng tích hợp với các hệ thống khác (ERP, BI, CRM).
- **Tùy biến linh hoạt**: Chọn chế độ xuất dữ liệu phù hợp (basic, standard, complete, custom) và thêm các tùy chọn như xuất bảng tính, PDF, hoặc lịch trình.
- **Hoạt động liên tục**: Workflow có thể chạy tự động khi có yêu cầu mới, không cần can thiệp của con người.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow này, các sếp cần chuẩn bị:
1. **DDC Toolkit (DDC_Converter_Revit)**:
   - Tải xuống từ [GitHub của DataDrivenConstruction](https://github.com/datadrivenconstruction/cad2data-Revit-IFC-DWG-DGN-pipeline-with-conversion-validation-qto).
   - Đảm bảo có file `RvtExporter.exe` nằm trong thư mục `datadrivenlibs` (ví dụ: `C:\DDC_Converter_Revit\datadrivenlibs\RvtExporter.exe`).

2. **Tài khoản n8n**:
   - Một tài khoản n8n đã cài đặt trên máy chủ riêng (Self-hosted) hoặc sử dụng phiên bản miễn phí trên [n8n.io](https://n8n.io/).

3. **File Revit (.rvt)**:
   - Các file dự án Revit cần chuyển đổi. File này sẽ được chỉ định trong quá trình cấu hình.

4. **Thư viện Python (nếu sử dụng chế độ custom)**:
   - Nếu chọn chế độ `custom`, cần có file định nghĩa danh mục (category file) để xác định cấu trúc xuất dữ liệu.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### 1. **Import Workflow 📥**
Workflow này có thể được import từ file JSON hoặc copy/paste JSON vào **n8n Editor**. Dưới đây là các bước cụ thể:

- **Tải file JSON**:
  - Tải workflow từ [n8n.io/workflows/7649](https://n8n.io/workflows/7649) hoặc sử dụng file JSON đã cung cấp.
- **Import vào n8n**:
  1. Mở **n8n Editor** trên máy chủ của bạn.
  2. Nhấp vào **"Import"** ở góc trên bên phải.
  3. Chọn file JSON và nhấp **"Import"**.
  4. Workflow sẽ xuất hiện trên canvas với 4 node chính.

#### 2. **Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm 4 node chính, mỗi node đều cần cấu hình kỹ lưỡng:

##### **Node 1: Form UI (n8n-nodes-base.formTrigger)**
- **Mục đích**: Tạo một biểu mẫu web cho người dùng nhập thông tin cần thiết (đường dẫn đến `RvtExporter.exe`, đường dẫn file Revit, và tùy chọn xuất).
- **Cách sử dụng**:
  - Bật node này bằng cách nhấp vào **"Active"** ở góc trên bên phải.
  - Khi nhấp vào nút **"Open Form"**, một cửa sổ popup sẽ mở ra (nếu bị chặn popup, tham khảo phần **Troubleshooting** dưới đây).
  - Nhập các thông tin sau:
    - **Converter Path**: Đường dẫn chính xác đến `RvtExporter.exe` (ví dụ: `C:\DDC_Converter_Revit\datadrivenlibs\RvtExporter.exe`).
    - **Revit File Path**: Đường dẫn đến file `.rvt` cần chuyển đổi.
    - **Export Mode**: Chọn chế độ xuất (`basic`, `standard`, `complete`, hoặc `custom`).
    - **Options**: Nhập các tùy chọn tùy chỉnh (ví dụ: `bbox schedule sheets2pdf`).

##### **Node 2: Manual Trigger (n8n-nodes-base.manualTrigger) (Tùy Chọn)**
- **Mục đích**: Cho phép kích hoạt workflow thủ công mà không cần sử dụng biểu mẫu.
- **Cách sử dụng**:
  - Nhấp vào nút **"Execute"** ở node này để chạy workflow với các biến đã được cài đặt trước trong **Node 3**.

##### **Node 3: Set the Conversion Variables (n8n-nodes-base.set)**
- **Mục đích**: Cấu hình các biến cần thiết cho quá trình chuyển đổi, bao gồm đường dẫn đến executable và tùy chọn xuất.
- **Cách cấu hình**:
  - Mở node này và chỉnh sửa các biến như sau:
    ```json
    {
      "converterPath": "C:\\DDC_Converter_Revit\\datadrivenlibs\\RvtExporter.exe",
      "revitFilePath": "C:\\Dự Án\\Dự Án_123.rvt",
      "options": "complete bbox schedule"
    }
    ```
  - **Lưu ý**:
    - Đảm bảo đường dẫn `converterPath` **trùng khớp với vị trí thực tế của `RvtExporter.exe`**.
    - Tham số `options` là **case-sensitive** và có thể kết hợp nhiều tùy chọn bằng cách cách nhau bằng dấu cách.

##### **Node 4: Converting the Project into a Structured Form (n8n-nodes-base.executeCommand)**
- **Mục đích**: Thực hiện lệnh chuyển đổi bằng cách gọi `RvtExporter.exe` với các biến đã được thiết lập.
- **Cách cấu hình**:
  - Node này sẽ tự động chạy lệnh sau khi nhận được đầu vào từ **Node 3**:
    ```
    "command": "cmd.exe",
    "arguments": [
      "/C",
      "{{$node['Set the conversion variables'].json['converterPath']}}",
      "{{$node['Set the conversion variables'].json['revitFilePath']}}",
      "{{$node['Set the conversion variables'].json['options']}}"
    ]
    ```
  - **Lưu ý**:
    - Nếu gặp lỗi **"Executable Path Issues"**, hãy kiểm tra lại đường dẫn trong **Node 3** và đảm bảo nó trỏ đến thư mục `datadrivenlibs`.

#### 3. **Kích Hoạt ⚡️ Workflow**
- **Test Run**:
  1. Chọn **Node 4** (Converting the Project).
  2. Nhấp vào **"Execute"** để chạy workflow với dữ liệu mẫu.
  3. Kiểm tra kết quả xuất ra (thường là file `.xlsx`, `.dae`, hoặc các định dạng khác tùy thuộc vào tùy chọn).
- **Bật Active**:
  - Sau khi test thành công, nhấp vào **"Active"** ở góc trên bên phải của workflow để kích hoạt nó.

---

### ⚠️ **Troubleshooting (Giải Quyết Vấn Đề Thường Gặp)**

#### **1. Browser Popup Issues (Lỗi Popup Trên Trình Duyệt)**
Nếu biểu mẫu không mở:
1. Kiểm tra biểu tượng **popup blocker** ở thanh địa chỉ của trình duyệt (thường là hình chìa khóa hoặc dấu chấm than).
2. Nhấp vào biểu tượng đó và chọn **"Always allow popups from this site"**.
3. Tải lại trang và thử lại.

#### **2. Executable Path Issues (Lỗi Đường Dẫn Executable)**
Nếu quá trình chuyển đổi thất bại:
- **Đường dẫn sai**:
  - **Sai**: `C:\Community\DDC_Converter_Revit\RvtExporter.exe`
  - **Đúng**: `C:\DDC_Converter_Revit\datadrivenlibs\RvtExporter.exe`
- **Giải pháp**:
  - Đảm bảo `RvtExporter.exe` nằm trong thư mục `datadrivenlibs` và đường dẫn trong **Node 3** trùng khớp.

#### **3. Lỗi Tùy Chọn (Options)**
- Nếu chọn chế độ `custom`, **bắt buộc phải có file định nghĩa danh mục** (category file) và nhập đường dẫn đến file này trong `options` (ví dụ: `[custom_categories.txt]`).
- Các tùy chọn **case-sensitive**, ví dụ: `bbox` (đúng) ≠ `BBOX` (sai).

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**

#### **1. Tích Hợp Với Slack/Telegram để Báo Lỗi**
- Sử dụng node **Slack** hoặc **Telegram Bot** để gửi thông báo khi workflow hoàn thành hoặc gặp lỗi.
- Cấu hình node này sau **Node 4** để nhận kết quả và gửi thông báo tự động.

#### **2. Lưu Log Lịch Sử Chuyển Đổi**
- Sử dụng node **Google Sheets** hoặc **Airtable** để lưu trữ lịch sử các lần chuyển đổi, bao gồm:
  - Tên dự án.
  - Thời gian chuyển đổi.
  - Chế độ xuất và tùy chọn sử dụng.
  - Kết quả (thành công/thất bại).

#### **3. Chạy Tự Động Định Kỳ**
- Sử dụng **n8n Cron Trigger** để chạy workflow hàng ngày hoặc hàng tuần để chuyển đổi các dự án mới tự động.

#### **4. Tích Hợp Với Power BI/Tableau**
- Sau khi chuyển đổi, dữ liệu có thể được tích hợp với **Power BI** hoặc **Tableau** để tạo báo cáo trực quan về dự án.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp trong ngành xây dựng và kỹ thuật muốn tự động hóa quá trình chuyển đổi dữ liệu từ Revit sang cơ sở dữ liệu. Với việc chỉ cần nhập đường dẫn và chọn chế độ xuất, các sếp có thể tiết kiệm **hàng giờ làm việc thủ công** mỗi tuần, đồng thời đảm bảo **độ chính xác cao** trong dữ liệu.

**Hãy thử ngay và tối ưu hóa quy trình của bạn!** Nếu có bất kỳ câu hỏi nào, hãy tham khảo tài liệu gốc từ [DataDrivenConstruction](https://github.com/datadrivenconstruction/cad2data-Revit-IFC-DWG-DGN-pipeline-with-conversion-validation-qto) hoặc liên hệ với cộng đồng n8n.

---
**🎁 Đăng ký VPS cho n8n với ưu đãi đặc biệt:**
👉 [TinoHost](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N**)
👉 [BNIX](https://my.bnix.one/aff.php?aff=172) (VPS Xeon 4GB chỉ 50k/tháng)