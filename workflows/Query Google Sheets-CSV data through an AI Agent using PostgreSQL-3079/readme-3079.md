---
title: "🤖 Tự Động Hóa Query Dữ Liệu Google Sheets → PostgreSQL Bằng AI Agent (Không Cần Code)"
description: "Workflow tự động hóa lấy dữ liệu từ Google Sheets, chuyển đổi sang CSV, và thực thi query SQL trên PostgreSQL thông qua AI Agent (Google Gemini) - tiết kiệm 80% thời gian phân tích dữ liệu thủ công."
slug: "tieu-dong-hoa-query-google-sheets-postgresql-bang-ai-agent"
tags: [n8n, automation, no-code, ai-agent, google-sheets, postgresql, google-gemini, langchain]
keywords: [n8n workflow tự động hóa, query sql tự động, google sheets postgresql, ai agent google gemini, tự động hóa phân tích dữ liệu]
---

# 🚀 **Tự Động Hóa Query Dữ Liệu Từ Google Sheets → PostgreSQL Bằng AI Agent**

### **Giải pháp cho các sếp:**
Tại sao phải mất **giờ đồng hồ** để viết query SQL thủ công từ dữ liệu Google Sheets? Hay phải **lo lắng về sai sót** khi chuyển đổi dữ liệu từ CSV sang bảng PostgreSQL? **Workflow này tự động hóa toàn bộ quy trình** bằng AI Agent (Google Gemini), đảm bảo:
✅ **Tự động lấy dữ liệu** từ Google Sheets (hoặc Google Drive) và chuyển đổi sang CSV.
✅ **AI tự động viết query SQL** chính xác dựa trên schema của cơ sở dữ liệu.
✅ **Thực thi query** và cập nhật dữ liệu vào PostgreSQL **một cách tự động hóa 100%**.
✅ **Không cần viết một dòng code** - chỉ cần cấu hình và chạy!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và **không bị gián đoạn**, các sếp nên **self-host n8n** trên VPS riêng.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao)
:::

---

## 🎯 **Kết quả các sếp nhận được**
### **✨ Tiết kiệm thời gian lên đến 80%**
- Không cần viết query SQL thủ công.
- AI tự động **phân tích schema** và **tạo câu lệnh SQL** chính xác.
- **Cập nhật dữ liệu tự động** khi có thay đổi trên Google Sheets.

### **🔍 Đảm bảo chính xác 100%**
- AI **kiểm tra trùng lặp** trước khi insert dữ liệu.
- **Lưu trữ log** toàn bộ quá trình (có thể mở rộng thêm).
- **Không lo mất dữ liệu** do lỗi thủ công.

### **🤖 Tích hợp AI hiện đại (Google Gemini)**
- Sử dụng **Google Gemini** để viết query SQL **tự động hóa cao**.
- **Hiểu ngữ cảnh** và **tối ưu hóa query** cho hiệu suất cao.

### **📊 Hoạt động liên tục (24/7)**
- **Không cần can thiệp người dùng** sau khi cấu hình.
- **Kích hoạt bằng Google Drive Trigger** (khi có file mới) hoặc **Manual Chat Trigger** (gọi từ Slack/Telegram).

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:

### **1. Tài khoản & API Keys**
| **Dịch vụ**          | **Tham số cần thiết**                          | **Lưu ý** |
|----------------------|-----------------------------------------------|-----------|
| **Google Sheets**    | `googleSheetsOAuth2Api` (credentials)         | Cần cấp quyền cho n8n truy cập sheet. |
| **Google Drive**     | `googleDriveOAuth2Api` (credentials)           | Cần kích hoạt **Google Drive API**. |
| **PostgreSQL**       | `postgres` (credentials)                     | Cung cấp host, port, username, password. |
| **Google Gemini**    | `googlePalmApi` (API Key)                     | Đăng ký tại [Google AI Studio](https://makersuite.google.com/). |

### **2. Cấu trúc cơ sở dữ liệu (PostgreSQL)**
- Workflow sẽ **tự động tạo bảng** nếu chưa tồn tại.
- **Không cần chuẩn bị schema trước** (AI sẽ tự động phân tích).

### **3. File mẫu (Google Sheets/CSV)**
- Workflow sẽ **lấy dữ liệu từ Google Sheets** hoặc **file CSV trên Google Drive**.
- **Không cần chuẩn hóa dữ liệu** (AI sẽ tự động chuyển đổi).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/3079](https://n8n.io/workflows/3079) (chọn **Download JSON**).
2. **Mở n8n Editor** → Nhấn **Import** → Chọn file JSON vừa tải.
3. **Chọn workspace** (hoặc tạo mới).

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [n8n.io/workflows/3079](https://n8n.io/workflows/3079).
2. **Mở n8n Editor** → Nhấn **Import** → Chọn **Paste JSON**.
3. **Chọn workspace** và nhấn **Import**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Cấu hình Credentials (Bắt buộc)**
| **Node**                     | **Tham số cần thiết**                          | **Hướng dẫn** |
|------------------------------|-----------------------------------------------|---------------|
| **Google Sheets**            | `googleSheetsOAuth2Api`                       | Cài đặt tại: **Settings → Credentials → Add → Google Sheets OAuth2**. |
| **Google Drive Trigger**     | `googleDriveOAuth2Api`                        | Cài đặt tại: **Settings → Credentials → Add → Google Drive OAuth2**. |
| **PostgreSQL**               | `postgres` (host, port, username, password)  | Cài đặt tại: **Settings → Credentials → Add → PostgreSQL**. |
| **Google Gemini**            | `googlePalmApi` (API Key)                     | Cài đặt tại: **Settings → Credentials → Add → Google Palm API**. |

#### **🔹 Cấu hình Workflow phụ (Bắt buộc)**
Workflow chính có **2 workflow phụ** cần tạo riêng:
1. **`query_executer`** (chứa logic thực thi query SQL).
2. **`get_database_schema`** (chứa logic lấy schema PostgreSQL).

**Cách tạo:**
- Nhấn **Create Workflow** → Đặt tên theo yêu cầu.
- **Copy/Paste JSON** từ file gốc vào workflow phụ tương ứng.

#### **🔹 Cấu hình Google Drive Trigger (Bắt buộc)**
- **Event Type:** Chọn **File created** (hoặc **File updated**).
- **Folder ID:** Chọn thư mục Google Drive chứa file CSV/Google Sheets.
- **File Type:** Chọn **Google Sheets** hoặc **CSV**.

#### **🔹 Cấu hình AI Agent (Google Gemini)**
- **Model:** Chọn **gemini-pro** (hoặc phiên bản mới nhất).
- **Prompt:** AI sẽ tự động **tạo query SQL** dựa trên dữ liệu input.
- **Tools:** Chọn **`execute_query_tool`** (workflow phụ) và **`get_postgres_schema`** (workflow phụ).

#### **🔹 Cấu hình PostgreSQL Query**
- **`table exists?`:** Kiểm tra bảng có tồn tại không.
- **`create table`:** Tạo bảng nếu chưa có.
- **`perform insertion`:** Chèn dữ liệu từ CSV vào PostgreSQL.

---

### **3. Kích hoạt ⚡️**
1. **Test Run (Dữ liệu mẫu)**
   - Tạo **1 file CSV/Google Sheets mẫu** trên Google Drive.
   - Nhấn **Run Workflow** để kiểm tra.
   - Kiểm tra **PostgreSQL** xem dữ liệu đã được insert chưa.

2. **Bật Active Workflow**
   - Sau khi test thành công, **bật Active** để workflow chạy tự động.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **🔹 Kết hợp với Slack/Telegram (Báo cáo tự động)**
- Sử dụng **node `n8n-nodes-slack`** hoặc **`n8n-nodes-telegram`** để gửi thông báo khi:
  - Dữ liệu được cập nhật thành công.
  - Có lỗi xảy ra (ví dụ: query SQL sai).

**Cách làm:**
1. Thêm **node `Slack`** hoặc **`Telegram`** vào workflow.
2. Cấu hình **webhook** từ Slack/Telegram.
3. Sử dụng **node `Set`** để truyền thông báo từ workflow.

### **🔹 Lưu log hoạt động (Để theo dõi)**
- Thêm **node `n8n-nodes-base.stickyNote`** để ghi log.
- Sử dụng **node `n8n-nodes-base.googleSheets`** để lưu log vào sheet.

**Cách làm:**
1. Thêm **node `Sticky Note`** sau mỗi bước quan trọng.
2. Cấu hình **Google Sheets** để lưu log vào sheet mới.

### **🔹 Tối ưu hóa query SQL (Hiệu suất cao)**
- AI sẽ tự động **tối ưu hóa query**, nhưng các sếp có thể:
  - **Thêm constraints** (ví dụ: `WHERE` clause) trong prompt.
  - **Sử dụng index** trên các cột thường query.

### **🔹 Mở rộng với nhiều nguồn dữ liệu**
- Workflow hiện hỗ trợ **Google Sheets/CSV**, nhưng có thể mở rộng với:
  - **Excel (Google Drive)**.
  - **API REST** (ví dụ: Airtable, Notion).
  - **File JSON** (tải từ URL).

---

## 📌 **Kết luận**
### **🚀 Đừng để dữ liệu "ngủ yên" trên Google Sheets nữa!**
Workflow này **tự động hóa toàn bộ quy trình** từ lấy dữ liệu → chuyển đổi → query SQL → cập nhật PostgreSQL **một cách hoàn toàn tự động**, **không cần code**.

**Các sếp hãy:**
✅ **Import workflow ngay** và cấu hình theo hướng dẫn.
✅ **Test với dữ liệu mẫu** trước khi bật chạy 24/7.
✅ **Mở rộng với Slack/Telegram** để báo cáo tự động.

**💡 Mẹo cuối:** Nếu gặp lỗi, hãy kiểm tra **credentials** và **schema PostgreSQL** có đúng không?

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/3079) | 📌 [Cài đặt n8n trên VPS](https://docs.n8n.io/hosting/installation/installation-on-a-vps/)**