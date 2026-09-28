---
title: "🔍 Query Dữ liệu PostgreSQL bằng Tiếng Việt Thông Thường với GPT-4o-mini (Không Cần SQL!)"
description: "Hướng dẫn tự động hóa việc truy vấn cơ sở dữ liệu PostgreSQL bằng cách nhập câu hỏi tiếng Việt thông thường, nhận kết quả phân tích và biểu đồ tự động. Giúp các sếp tiết kiệm thời gian lên đến 80% so với cách thủ công."
slug: "query-postgresql-voi-gpt4o-mini"
tags: [n8n, automation, no-code, ai-chatbot, postgresql, google-sheets, openai]
keywords: [n8n workflow postgresql, tự động hóa truy vấn cơ sở dữ liệu, chatbot ai với postgresql, query postgresql bằng tiếng việt, gpt-4o-mini với n8n]
---

# 🚀 Query PostgreSQL bằng Tiếng Việt Thông Thường với GPT-4o-mini

### **Giải pháp hoàn hảo cho các sếp muốn:**
- **Truy vấn dữ liệu PostgreSQL chỉ bằng câu hỏi tiếng Việt** (không cần viết SQL).
- **Nhận kết quả phân tích và biểu đồ tự động** trong một workflow duy nhất.
- **Tiết kiệm thời gian lên đến 80%** so với cách thủ công.
- **Cập nhật và đồng bộ dữ liệu từ Google Sheets** vào PostgreSQL một cách tự động.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7 với hiệu suất tối ưu, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) thay vì phiên bản cloud. Với VPS, các sếp có thể:
- **Tùy chỉnh tài nguyên** (CPU, RAM) theo nhu cầu.
- **Bảo mật cao** (không phụ thuộc vào cloud).
- **Tiết kiệm chi phí dài hạn**.

👉 **[Đăng ký VPS TinoHost với mã giảm giá VPSN8N (giảm 39%)](https://tino.vn/vps-n8n?affid=388)**
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**
:::

---

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Không cần viết SQL**: GPT-4o-mini tự động chuyển câu hỏi tiếng Việt thành câu lệnh SQL an toàn.
- **Truy vấn động**: Hệ thống nhớ bảng đã chọn trong phiên chat, không cần nhập lại.
- **Biểu đồ tự động**: Kết quả truy vấn được chuyển thành biểu đồ (QuickChart) để phân tích nhanh.
- **Đồng bộ dữ liệu**: Cập nhật dữ liệu từ Google Sheets vào PostgreSQL một cách tự động.
- **An toàn tuyệt đối**: Workflow chỉ sử dụng các cột hợp lệ từ schema, tránh lỗi SQL injection.
:::

---

## 🔧 Yêu cầu cần thiết
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản PostgreSQL**:
   - Địa chỉ server, tên người dùng, mật khẩu, và tên cơ sở dữ liệu.
   - Bảng cần truy vấn phải nằm trong **schema `public`** (hoặc cấu hình lại trong node `Manage Table Name`).
2. **API Key OpenAI**:
   - Đăng ký tại [OpenAI](https://platform.openai.com/) và thêm vào n8n dưới **credentials `openAiApi`**.
3. **(Không bắt buộc)** Tài khoản Google Sheets OAuth2:
   - Nếu muốn đồng bộ dữ liệu từ Google Sheets vào PostgreSQL.
4. **Node QuickChart**:
   - Để tạo biểu đồ từ kết quả truy vấn (nếu cần).

---

## 🚀 Cách import & Lưu ý khi "lên đồ"

### **1. Import Workflow 📥**
Các sếp có thể import workflow theo hai cách:
- **Tải file JSON** từ [n8n.io/workflows/14057](https://n8n.io/workflows/14057) và import vào n8n Editor.
- **Copy JSON** và paste vào **Import Workflow** trong n8n.

:::note[Lưu ý]
- **Không xóa node `Truncate Table`** nếu không muốn dữ liệu bị xóa khi đồng bộ từ Google Sheets.
- **Cấu hình lại tên bảng** trong node `Manage Table Name` nếu bảng của các sếp không nằm trong `public`.
:::

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình PostgreSQL**
1. **Thêm credentials PostgreSQL**:
   - Vào **Credentials** → **Add Credential** → Chọn **PostgreSQL**.
   - Điền:
     - **Host**: `your-postgres-server.com`
     - **Database**: `your-database-name`
     - **User**: `your-username`
     - **Password**: `your-password`
     - **Port**: `5432` (mặc định).

2. **Kiểm tra node `Fetch Schema`**:
   - Node này lấy schema của bảng để GPT-4o-mini biết các cột hợp lệ.
   - **Lưu ý**: Nếu bảng không nằm trong `public`, chỉnh sửa node `Manage Table Name` để thêm `schema` vào query.

#### **B. Cấu hình OpenAI**
1. **Thêm API Key OpenAI**:
   - Vào **Credentials** → **Add Credential** → Chọn **OpenAI**.
   - Điền **API Key** từ tài khoản OpenAI.
   - Chọn **model `gpt-4o-mini`** trong node `OpenAI GPT-4o-mini`.

#### **C. Cấu hình Google Sheets (nếu sử dụng)**
1. **Thêm credentials Google Sheets**:
   - Vào **Credentials** → **Add Credential** → Chọn **Google Sheets OAuth2**.
   - Theo hướng dẫn để kết nối với Google Sheets.
2. **Chỉnh node `Fetch Google Sheet`**:
   - Điền **Sheet ID** và **Sheet Name** từ Google Sheets.

#### **D. Cấu hình QuickChart (nếu muốn biểu đồ)**
1. **Thêm credentials QuickChart**:
   - Nếu chưa có, thêm vào **Credentials** → **QuickChart**.
   - Các sếp có thể sử dụng phiên bản miễn phí hoặc nâng cấp.

---

### **3. Kích hoạt ⚡️**
1. **Test run với dữ liệu mẫu**:
   - Chọn node `Manual Trigger` và nhấn **Execute**.
   - Nhập câu hỏi như: *"Hãy lấy danh sách khách hàng mới trong tháng 6"*.
   - Kiểm tra kết quả và biểu đồ (nếu cấu hình QuickChart).

2. **Bật Active workflow**:
   - Chuyển trạng thái workflow từ **Inactive** sang **Active**.
   - Các sếp có thể tương tác qua **Chat Trigger** (ví dụ: Slack, Discord, hoặc Webhook).

---

## ✍️ Mẹo & gợi ý nâng cao

### **1. Tăng tính cá nhân hóa**
- **Thêm hệ thống prompt tùy chỉnh**:
  - Chỉnh sửa node `Unified Analytics Agent` để thêm hoặc loại bỏ các quy tắc SQL.
  - Ví dụ: *"Chỉ trả về kết quả có giá trị > 1000"*.

### **2. Đồng bộ dữ liệu định kỳ**
- **Sử dụng node `Manual Trigger` + Cron Job**:
  - Cài đặt một **Cron Job** để chạy node `Fetch Google Sheet` và `Insert Rows to Postgres` hàng ngày.
  - Ví dụ: `0 0 * * *` (lúc 00:00 hàng ngày).

### **3. Tích hợp với Slack/Telegram**
- **Sử dụng node `Webhook`**:
  - Thêm node **Webhook** vào workflow và gửi kết quả về Slack/Telegram.
  - Cấu hình trong **Credentials** → **Webhook**.

### **4. Lưu log truy vấn**
- **Thêm node `StickyNote`**:
  - Lưu lịch sử truy vấn vào một bảng log để theo dõi.

### **5. Hỗ trợ nhiều schema**
- **Chỉnh node `Manage Table Name`**:
  - Thêm logic để chọn schema khác nhau (ví dụ: `schema: sales`, `schema: analytics`).

---

## 📌 Kết luận
Workflow này giúp các sếp **tự động hóa truy vấn PostgreSQL bằng tiếng Việt**, tiết kiệm thời gian và giảm thiểu lỗi. Với sự hỗ trợ của **GPT-4o-mini**, các sếp có thể:
✅ **Truy vấn dữ liệu một cách tự nhiên** (không cần SQL).
✅ **Nhận kết quả phân tích và biểu đồ** trong một workflow.
✅ **Đồng bộ dữ liệu từ Google Sheets** một cách tự động.
✅ **Tùy chỉnh và mở rộng** theo nhu cầu.

**Hãy thử ngay và tự động hóa công việc của mình!** 🚀

---
**Ghi chú cuối:**
- Nếu gặp vấn đề, các sếp có thể tham khảo [hướng dẫn chính thức của n8n](https://docs.n8n.io/) hoặc liên hệ cộng đồng n8n trên [Discord](https://n8n.io/community).
- **Không xóa node `Truncate Table`** nếu không muốn mất dữ liệu khi đồng bộ từ Google Sheets.