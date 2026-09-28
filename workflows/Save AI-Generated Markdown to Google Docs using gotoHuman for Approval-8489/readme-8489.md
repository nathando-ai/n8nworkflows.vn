---
title: "🤖 Tự Động Hóa Tạo Nội Dung AI + Xác Nhận Con Người Trước Khi Cập Nhật Google Docs (GotoHuman)"
description: "Workflow tự động hóa sử dụng AI (GPT-4) tạo nội dung Markdown, gửi yêu cầu duyệt qua GotoHuman, và chỉ cập nhật Google Docs khi được phê duyệt. Giảm thiểu sai sót, đảm bảo chất lượng nội dung và tiết kiệm thời gian cho các sếp."
slug: "tieu-dong-hoa-tao-noi-dung-ai-duyet-con-nguoi-googledocs"
tags: [n8n, automation, ai-content-generation, gotoHuman, google-docs, no-code]
keywords: [n8n workflow tự động hóa, tạo nội dung AI, duyệt nội dung con người, Google Docs tự động, GotoHuman n8n]
---

# 🚀 **Tự Động Hóa Tạo Nội Dung AI + Duyệt Con Người Trước Khi Cập Nhật Google Docs**

### **Giải pháp cho các sếp:**
Bạn đã từng phải mất **ngày tháng** để viết, chỉnh sửa và phê duyệt nội dung marketing, chiến lược kinh doanh hay báo cáo nội bộ? Hay phải lo lắng rằng **AI tạo ra nội dung không phù hợp với brand** của công ty? Workflow này sẽ **tự động hóa toàn bộ quy trình**, từ tạo nội dung bằng AI đến **xác nhận con người** trước khi cập nhật vào Google Docs.

👉 **Kết quả:**
- **Tiết kiệm 80% thời gian** so với viết thủ công.
- **Đảm bảo nội dung phù hợp brand** nhờ duyệt con người.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.
- **Cập nhật tự động** khi nội dung được phê duyệt.

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tạo nội dung chuyên nghiệp** bằng AI (GPT-4) với ngữ cảnh từ Google Docs hiện có.
✅ **Duyệt nội dung trước khi cập nhật** qua **GotoHuman** (giao diện dễ dùng, hỗ trợ chỉnh sửa trực tiếp).
✅ **Chỉ cập nhật Google Docs khi được phê duyệt** → Tránh nội dung sai lệch hoặc không phù hợp.
✅ **Hoạt động tự động** (hoặc kích hoạt thủ công) mà không cần can thiệp.
✅ **Lưu trữ lịch sử chỉnh sửa** để theo dõi và cải tiến.
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản GotoHuman** (để duyệt nội dung con người).
✔ **API Key OpenAI** (để sử dụng GPT-4 tạo nội dung).
✔ **Tài khoản Google Workspace** (Google Docs/Drive).
✔ **Template "Strategy agent" trong GotoHuman** (ID: `F4sbcPEpyhNKBKbG9C1d`).
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [đây](https://n8n.io/workflows/8489) (nút "Import").
2. **Mở n8n Editor** (Cloud hoặc Self-hosted).
3. **Nhấn "Import"** và chọn file JSON vừa tải.
4. **Chọn "Import"** để workflow xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [đây](https://n8n.io/workflows/8489).
2. **Mở n8n Editor** → **Nhấn "Import"** → **Chọn "Paste JSON"**.
3. **Xác nhận import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **11 node**, nhưng **các node quan trọng cần cấu hình** như sau:

#### **🔹 Node 1: Manual Trigger (Bắt đầu workflow)**
- **Không cần chỉnh sửa**, chỉ kích hoạt khi cần chạy.

#### **🔹 Node 2: AI Agent (Tạo nội dung Markdown)**
- **Cấu hình:**
  - **Input:** Đọc từ **Google Docs** (các node `Get company strategy` và `Get company description`).
  - **Model:** Sử dụng **GPT-4.1** (đã được cấu hình trong node `OpenAI Chat Model`).
  - **Prompt:** AI sẽ tự động tạo nội dung Markdown dựa trên ngữ cảnh từ Google Docs.

#### **🔹 Node 3 & 4: Get company strategy & Get company description (Google Docs Tool)**
- **Cấu hình:**
  - **Credentials:** Chọn **Google OAuth 2.0** đã cấu hình trước.
  - **File ID:** Điền **ID của Google Doc** bạn muốn lấy ngữ cảnh (thông tin này tìm được trong URL của Google Docs).
  - **Operation:** Đặt là **"get"** (lấy nội dung).

#### **🔹 Node 5: OpenAI Chat Model (GPT-4.1)**
- **Cấu hình:**
  - **API Key:** Điền **API Key OpenAI** (tạo tại [OpenAI Platform](https://platform.openai.com/)).
  - **Model:** Đã chọn **gpt-4.1** (không cần thay đổi).
  - **Prompt:** AI sẽ tự động tạo nội dung Markdown dựa trên ngữ cảnh từ Google Docs.

#### **🔹 Node 6: Structured Output Parser**
- **Không cần chỉnh sửa**, node này **chuyển đổi output của AI thành định dạng Markdown**.

#### **🔹 Node 7: Send review request and wait for response (GotoHuman)**
- **Cấu hình:**
  - **Credentials:** Chọn **GotoHuman OAuth 2.0** đã cấu hình.
  - **Template:** Chọn **template "Strategy agent"** (ID: `F4sbcPEpyhNKBKbG9C1d`).
  - **Content:** Auto-filled từ output của AI.

#### **🔹 Node 8: Approved? (If Condition)**
- **Cấu hình:**
  - **Condition:** Kiểm tra **trạng thái duyệt** từ GotoHuman.
  - **Nếu Approved:** Chuyển sang node `Update file`.
  - **Nếu Rejected:** **Workflow dừng lại** (có thể thêm node khác để xử lý).

#### **🔹 Node 9: Update file (Google Drive)**
- **Cấu hình:**
  - **Credentials:** Chọn **Google OAuth 2.0**.
  - **File ID:** Điền **ID của Google Doc** muốn cập nhật.
  - **Content:** Auto-filled từ nội dung đã duyệt.

#### **🔹 Node 10 & 11: Convert to File & Set file type as markdown (Code)**
- **Không cần chỉnh sửa**, node này **chuyển đổi nội dung thành file Markdown** trước khi cập nhật.

---
### **3. Kích hoạt ⚡️**
1. **Test Run (Kiểm tra thử):**
   - Nhấn **"Execute"** trên node **Manual Trigger**.
   - Kiểm tra **AI tạo nội dung như mong muốn**.
   - **Gửi yêu cầu duyệt** qua GotoHuman.
   - **Chờ phản hồi** (Approved/Rejected).

2. **Bật Active Workflow:**
   - Sau khi test thành công, **bật "Active"** trên node **Manual Trigger**.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC TỐI ƯU NÂNG CAO]
🔹 **Chạy tự động theo lịch:**
   - Thay thế **Manual Trigger** bằng **Schedule Trigger** (n8n Cloud) hoặc **Google Calendar Trigger** (Self-hosted).

🔹 **Thêm nhiều ngữ cảnh cho AI:**
   - Lấy dữ liệu từ **Google Sheets, Notion, hoặc API** khác để AI tạo nội dung chính xác hơn.

🔹 **Gửi thông báo Slack/Email khi duyệt:**
   - Thêm node **Slack/Email** sau node **GotoHuman** để thông báo kết quả duyệt.

🔹 **Lưu lịch sử chỉnh sửa:**
   - Thêm node **Google Sheets** để ghi lại **lịch sử duyệt** và **người duyệt**.

🔹 **Kết hợp với nhiều AI Agent:**
   - Sau khi duyệt, chạy **AI Agent khác** để thực hiện hành động dựa trên nội dung mới (ví dụ: tạo bài blog, email marketing).
:::

---

## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc viết và duyệt nội dung thủ công, đồng thời **đảm bảo chất lượng** nhờ sự can thiệp của con người. **Chỉ cần cấu hình 1 lần**, workflow sẽ **hoạt động tự động** mỗi khi cần cập nhật nội dung.

👉 **Hành động ngay:**
1. **Cài đặt n8n Self-hosted** (để workflow chạy 24/7).
2. **Import workflow** và cấu hình các credentials.
3. **Test và bật Active** để bắt đầu tự động hóa!

🚀 **Nếu cần hỗ trợ thêm**, các sếp có thể tham khảo:
- [Tutorial GotoHuman](https://docs.gotohuman.com/)
- [n8n Google Docs Node](https://docs.n8n.io/integrations/builtins/google-drive/)
- [OpenAI API Guide](https://platform.openai.com/docs/api-reference)

---
**Chúc các sếp thành công với quy trình tự động hóa mới!** 💪