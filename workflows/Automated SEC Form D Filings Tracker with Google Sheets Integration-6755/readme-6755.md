---
title: "🚀 Tự Động Theo Dõi SEC Form D Filings - Giải Pháp Tiết Kiệm Thời Gian Cho Nhà Đầu Tư & VC"
description: "Workflow tự động hóa theo dõi các Form D của SEC (Cục Giám Đốc Chứng Khoán Mỹ) về các giao dịch tư nhân và vốn hóa mới, giúp các nhà đầu tư và quỹ đầu tư (VC) cập nhật thông tin mới nhất chỉ trong 10 phút/lần, tránh bỏ lỡ cơ hội đầu tư. Kết quả: Tiết kiệm 20+ giờ/tháng, dữ liệu chính xác 100%, và khả năng cá nhân hóa theo CIK số."
slug: "tieu-dong-theo-doi-sec-form-d"
tags: [n8n, automation, crypto-trading, sec-edgar, google-sheets, no-code]
keywords: [tự động hóa theo dõi SEC Form D, n8n workflow crypto, theo dõi giao dịch tư nhân, tự động hóa đầu tư VC, SEC Edgar RSS feed, Google Sheets API]
---

# 🚀 **Tự Động Theo Dõi SEC Form D Filings - Giải Pháp Cho Nhà Đầu Tư & Quỹ VC**

### **Nỗi Đau Của Các Sếp**
Các nhà đầu tư và quỹ VC (Venture Capital) thường phải mất **giờ đồng hồ hàng tuần** để thủ công theo dõi các **Form D** của SEC (Cục Giám Đốc Chứng Khoán Mỹ). Những báo cáo này chứa thông tin về **giao dịch tư nhân, vốn hóa mới, và các hoạt động đầu tư** của các công ty. Nếu bỏ lỡ thông tin này, các sếp có thể:
- **Bỏ lỡ cơ hội đầu tư** vào các startup sớm.
- **Tốn thời gian** tra cứu dữ liệu trên trang SEC Edgar.
- **Rủi ro sai sót** khi ghi chép thủ công.

Workflow này **tự động hóa toàn bộ quy trình**, giúp các sếp **cập nhật dữ liệu mới nhất chỉ trong 10 phút/lần**, **không cần code**, và **tránh bỏ lỡ bất kỳ thông tin quan trọng nào**.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 20+ giờ/tháng** so với cách thủ công.
- **Dữ liệu chính xác 100%** (không sai sót như khi copy-paste).
- **Cập nhật liên tục** (chỉ trong 10 phút/lần, chỉ trong giờ làm việc).
- **Dữ liệu sẵn sàng trên Google Sheets** để phân tích nhanh.
- **Không phụ thuộc vào thời gian làm việc của SEC** (do chạy tự động).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để lưu trữ dữ liệu).
2. **API Key OAuth 2.0 của Google Sheets** (cài đặt trong n8n).
3. **Không cần API Key đặc biệt của SEC** (do workflow tự động lấy dữ liệu từ RSS feed công khai).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import workflow từ file JSON** hoặc **copy/paste JSON** vào **n8n Editor**:
1. **Tải file JSON** từ [đây](https://n8n.io/workflows/6755) (hoặc copy toàn bộ JSON từ link trên).
2. Trong **n8n Editor**, chọn **"Import"** → **"From JSON"** và dán nội dung.
3. **Hoặc** copy toàn bộ JSON và paste vào **n8n Editor** → **"Import"** → **"From JSON"**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **6 node chính**, nhưng **các bước sau đây phải được điều chỉnh**:

##### **🔹 Node 1: Schedule Trigger (Lịch Trình Tự Động)**
- **Thời gian chạy**: Mặc định là **mỗi 10 phút trong giờ làm việc (6 AM - 9 PM EST, thứ 2 - thứ 6)**.
- **Lưu ý**:
  - Nếu các sếp muốn **chạy liên tục 24/7**, hãy thay đổi thành `*/10 * * * *` (mỗi 10 phút).
  - Nếu muốn **chỉ chạy vào giờ Việt Nam**, hãy điều chỉnh theo **UTC+7** (ví dụ: `0 0/10 * * *` từ 7 AM - 9 PM).

##### **🔹 Node 2: Fetch SEC Form D Filings (Lấy Dữ liệu từ SEC)**
- **URL mặc định**: `https://www.sec.gov/Archives/edgar/rss/CIK000004.rss` (lấy 40 Form D mới nhất).
- **Lưu ý**:
  - **Bắt buộc phải thêm header `User-Agent`** (SEC yêu cầu):
    ```json
    {
      "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36"
    }
    ```
  - Nếu muốn lấy dữ liệu của **một công ty cụ thể**, thay đổi `CIK000004` thành **CIK số của công ty** (ví dụ: `CIK000123456` cho Tesla).

##### **🔹 Node 3: Parse SEC RSS Feed (Xử Lý XML)**
- **Node này tự động chuyển dữ liệu từ XML sang JSON**.
- **Không cần chỉnh sửa**, chỉ cần **đảm bảo Node 2 trả về dữ liệu XML đầy đủ**.

##### **🔹 Node 4: Extract & Format Filing Data (Trích Xuất & Định Dạng)**
- **Node Code này trích xuất thông tin quan trọng** như:
  - **CIK Number** (Số mã công ty SEC).
  - **Title** (Tiêu đề Form D).
  - **Form Type** (Loại Form, ví dụ: "Form D").
  - **Links** (Link tải file HTML & TXT).
  - **Date** (Ngày nộp).
- **Lưu ý**:
  - **Không cần chỉnh sửa mã code** (nếu không muốn).
  - Nếu muốn **thêm trường dữ liệu khác**, các sếp có thể mở node này và **sửa code** (ví dụ: thêm `companyName` từ tiêu đề).

##### **🔹 Node 5: Filter New Filings Only (Lọc Bỏ Trùng Lặp)**
- **Node này loại bỏ dữ liệu đã tồn tại** trong các lần chạy trước.
- **Không cần chỉnh sửa**, chỉ cần **đảm bảo Node 6 (Google Sheets) có Sheet ID đúng**.

##### **🔹 Node 6: Save to SEC Data Sheet (Lưu Trữ vào Google Sheets)**
- **Bắt buộc phải cấu hình**:
  1. **Tạo một bản sao của Template Google Sheets** từ [đây](https://docs.google.com/spreadsheets/d/1VoGfVpk1mMrqKIc5hsO7peYuLx0SwhsbW7uUeYJCmrU/edit?usp=sharing).
  2. **Chia sẻ Sheet với tài khoản n8n** (cài đặt OAuth 2.0 trong n8n).
  3. **Điền Sheet ID vào Node 6**:
     - Mở Sheet → **File → Sheet Settings** → **Share** → **Copy Link**.
     - Link sẽ có dạng: `https://docs.google.com/spreadsheets/d/[SHEET_ID]/edit`.
     - **Chỉ cần lấy phần `[SHEET_ID]`** và dán vào **field `Sheet ID`** của Node 6.
  4. **Chọn Sheet Name**: `SEC Data` (hoặc tên tùy chỉnh).
  5. **Chọn Operation**: `Append` (thêm dữ liệu mới vào cuối).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chọn **Node 1 (Schedule Trigger)** → **Run Workflow**.
   - Kiểm tra **Node 6 (Google Sheets)** để xem dữ liệu đã được lưu chưa.
2. **Bật Active Workflow**:
   - Chuyển **switch Active** sang **ON** (nút màu xanh).

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Slack/Telegram**:
   - Thêm **Node Slack/Telegram** sau Node 6 để **đăng báo cáo mới** vào kênh chat.
   - Ví dụ: Khi có Form D mới, gửi tin nhắn: *"🚨 Form D mới từ CIK [CIK_NUMBER] - [TITLE]"* vào Slack.

2. **Lưu Log vào Google Drive**:
   - Thêm **Node Google Drive** để **lưu file XML gốc** của Form D vào một folder.

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **Node Email** (ví dụ: Gmail) để **gửi báo cáo tuần/month** về các Form D mới nhất cho team.

4. **Tích Hợp với Notion/ClickUp**:
   - Thay vì Google Sheets, các sếp có thể **lưu dữ liệu vào Notion/ClickUp** để quản lý dễ dàng hơn.

5. **Tự động Xóa Dữ liệu Cũ**:
   - Thêm **Node Google Sheets (Delete)** sau Node 6 để **xóa dữ liệu cũ** (ví dụ: >30 ngày).
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các nhà đầu tư và VC để tập trung vào **quyết định đầu tư** thay vì **làm thủ công**. Với **tự động hóa hoàn toàn**, các sếp sẽ:
✅ **Không bỏ lỡ bất kỳ Form D nào**.
✅ **Cập nhật dữ liệu nhanh chóng**.
✅ **Tiết kiệm thời gian và giảm sai sót**.

**Hãy áp dụng ngay và bắt đầu theo dõi SEC Form D một cách thông minh!** 🚀

---
:::note[CHÚ Ý CUỐI CÙNG]
- **Nếu gặp lỗi**, hãy kiểm tra:
  - **Header User-Agent** trong Node 2.
  - **Sheet ID** trong Node 6.
  - **Thời gian chạy** trong Node 1 (đảm bảo không trùng với giờ nghỉ của SEC).
- **Nếu muốn tùy chỉnh**, các sếp có thể **mở Node Code** và **sửa logic** theo nhu cầu.
:::