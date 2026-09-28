---
title: "📋 Tự Động Lưu & Ghi Log Nội Dung Clipboard từ macOS vào Google Sheets - Không Cần Code!"
description: "Giải pháp tự động hóa hoàn toàn miễn phí giúp các sếp lưu tất cả nội dung copy-paste từ máy Mac vào Google Sheets một cách tự động, tiết kiệm thời gian và tránh mất mát dữ liệu quan trọng. Hỗ trợ Shortcuts App và hoạt động 24/7."
slug: "tieu-dong-luu-ghi-log-clipboard-macos-google-sheets"
tags: [n8n, automation, macos, google-sheets, shortcuts-app, no-code]
keywords: [tự động hóa clipboard macos, lưu clipboard google sheets, tự động hóa không code, lưu dữ liệu clipboard, n8n workflow clipboard]
---

# 🚀 **Tự Động Lưu & Ghi Log Nội Dung Clipboard từ macOS vào Google Sheets**

### **Nỗi đau của các sếp khi làm thủ công**
Các sếp đã bao giờ gặp tình huống này chưa?
- **Mất mát dữ liệu quan trọng** vì quên copy nội dung từ website, email hay tài liệu vào nơi an toàn.
- **Phải làm thủ công** mỗi khi cần lưu trữ thông tin từ clipboard, tốn thời gian và dễ xảy ra lỗi.
- **Không có hệ thống ghi log** để theo dõi lịch sử copy-paste, làm giảm hiệu quả làm việc.

**Workflow này giải quyết tất cả!** Dùng **n8n + Shortcuts App** để tự động lưu mọi nội dung copy-paste từ macOS vào **Google Sheets**, đồng thời ghi log chi tiết thời gian, nguồn gốc và nội dung. **Không cần code, chỉ cần 5 phút setup!**

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải copy thủ công nữa, mọi nội dung copy-paste tự động lưu vào Sheets.
- **Tránh mất mát dữ liệu**: Ghi log toàn bộ lịch sử clipboard với thời gian, nguồn gốc và nội dung.
- **Tự động hóa hoàn toàn**: Hoạt động 24/7, không phụ thuộc vào người dùng.
- **Dễ dàng truy xuất**: Dữ liệu được sắp xếp rõ ràng trong Google Sheets, có thể lọc, tìm kiếm và phân tích.
- **Hỗ trợ Shortcuts App**: Sử dụng tính năng **Copy-Paste** trên macOS để kích hoạt workflow một cách nhanh chóng.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Máy Mac** (cần cài đặt **Shortcuts App** - có sẵn trên macOS 12+).
2. **Tài khoản Google** (để tạo Google Sheets và API Key).
3. **Tài khoản n8n** (có thể **self-hosted** trên VPS để ổn định hơn).
4. **Google Sheets** (một bảng mới để lưu log clipboard).
5. **API Key của Google Sheets**:
   - Tạo **Service Account** trong [Google Cloud Console](https://console.cloud.google.com/).
   - Cấp quyền **Editor** cho bảng Sheets tương ứng.
   - Sao chép **Client Email** và **Private Key** (JSON) để cấu hình trong n8n.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. **Tải workflow** từ [đây](https://n8n.io/workflows/4063) (nút "Download").
2. Trong **n8n Editor**, nhấn **"Import"** và chọn file JSON tải xuống.
   *Hoặc* copy toàn bộ JSON và dán vào **"Import from JSON"** trong Editor.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **3 node chính**, các sếp cần cấu hình như sau:

##### **Node 1: Clipboard Webhook (n8n-nodes-base.webhook)**
- **Tên node**: `Clipboard Webhook`
- **Cấu hình**:
  - **Path**: `copy-paste` (không thay đổi).
  - **HTTP Method**: `POST` (không thay đổi).
  - **Credentials**: Không cần (webhook sẽ nhận dữ liệu từ Shortcuts App).

##### **Node 2: Data Formatter (n8n-nodes-base.set)**
- **Tên node**: `Data Formatter`
- **Cấu hình**:
  - **Thêm các trường dữ liệu** (nếu cần) như:
    - `timestamp`: `${{ $now }}` (thời gian hiện tại).
    - `source`: `"macOS Clipboard"` (nguồn dữ liệu).
  - **Kết quả**: Dữ liệu sẽ được định dạng trước khi gửi vào Google Sheets.

##### **Node 3: Clipboard Logger Sheet (n8n-nodes-base.googleSheets)**
- **Tên node**: `Clipboard Logger Sheet`
- **Cấu hình**:
  - **Credentials**: Chọn `"googleApi"` (đã cấu hình trước khi import).
  - **Operation**: `appendOrUpdate` (thêm hoặc cập nhật dữ liệu).
  - **Google Sheets**:
    - **Spreadsheet ID**: Sao chép từ URL của bảng Sheets (ví dụ: `1AbC...XYZ`).
    - **Sheet Name**: Tên sheet muốn lưu dữ liệu (ví dụ: `Clipboard Log`).
    - **Range**: `A1` (để dữ liệu bắt đầu từ ô A1).
  - **Data**: Chọn `JSON` từ node `Data Formatter`.

#### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Trong **n8n Editor**, nhấn **"Execute"** để kiểm tra workflow.
   - Sau đó, **copy một đoạn văn bản** trên macOS và kích hoạt Shortcuts App.
2. **Bật Active workflow**:
   - Sau khi test thành công, chuyển workflow sang **Active** để hoạt động liên tục.

---

### **📱 Cách kích hoạt từ Shortcuts App (macOS)**
1. Mở **Shortcuts App** trên macOS.
2. Tạo một **Shortcut mới** với tên `"Save Clipboard to Google Sheets"`.
3. Thêm **Action** `"Run Shell Script"` và nhập lệnh sau:
   ```bash
   curl -X POST "YOUR_N8N_WEBHOOK_URL/copy-paste" -H "Content-Type: application/json" -d '{"clipboard": "'$(pbpaste)'"}'
   ```
   - Thay `YOUR_N8N_WEBHOOK_URL` bằng URL webhook của node `Clipboard Webhook` (có thể tìm trong **n8n Editor** > **Webhooks**).
4. Lưu Shortcuts và gán **tắt/nút hotkey** (ví dụ: `⌘ + Shift + S`) để kích hoạt nhanh.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động hóa báo cáo hàng ngày**:
   - Sử dụng **n8n Trigger** (ví dụ: `cron`) để gửi báo cáo tổng hợp clipboard vào email hoặc Slack hàng ngày.
2. **Lọc dữ liệu theo nguồn**:
   - Thêm cột `source` trong Google Sheets để phân loại dữ liệu (ví dụ: "Website", "Email", "Tài liệu").
3. **Gửi thông báo khi có dữ liệu mới**:
   - Kết nối với **Slack/Telegram** để nhận thông báo khi có nội dung mới được lưu.
4. **Xóa dữ liệu cũ**:
   - Sử dụng **Google Apps Script** để tự động xóa dữ liệu cũ hơn 30 ngày trong Sheets.

---

### 📌 **Kết luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn quá trình lưu clipboard**, tránh mất mát dữ liệu và tiết kiệm thời gian quý báu. **Không cần code, chỉ cần 5 phút setup!**

**Hãy áp dụng ngay và bắt đầu tự động hóa ngay từ hôm nay!**
👉 [Tải workflow](https://n8n.io/workflows/4063) và bắt đầu!

---
**Cần hỗ trợ?** Đăng ký VPS n8n ổn định với [TinoHost](https://tino.vn/vps-n8n?affid=388) và [BNIX](https://my.bnix.one/aff.php?aff=172) để workflow chạy 24/7!