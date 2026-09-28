---
title: "🤖 Tự Động Đổi Tên File Đính Kèm Gmail Bằng GPT-4o + Lưu Trên Google Drive (Không Cần Code)"
description: "Workflow tự động hóa đổi tên file đính kèm Gmail bằng trí tuệ nhân tạo (GPT-4o), đồng thời lưu trữ lên Google Drive với tên mô tả chính xác. Giúp các sếp tiết kiệm thời gian, tránh mất mát file và tổ chức thư mục hiệu quả."
slug: "tự-dộng-đổi-ten-file-gmail-bằng-gpt-4o"
tags: [n8n, automation, no-code, ai-summarization, google-drive, gmail-automation]
keywords: [n8n workflow gmail, tự động hóa đổi tên file, GPT-4o tự động hóa, lưu file đính kèm Google Drive, tự động hóa email AI]
---

# 🚀 **Tự Động Đổi Tên File Đính Kèm Gmail Bằng GPT-4o + Lưu Trên Google Drive**

### **🔍 Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải mất thời gian quét qua hàng chục email có file đính kèm với tên như *"file1.pdf"*, *"document_2024.pdf"* hoặc *"lời mời_12345.docx"*. Kết quả?
- **Tốn thời gian**: Phải mở từng file để xác định nội dung trước khi đổi tên.
- **Rủi ro mất mát**: File đính kèm không được lưu trữ theo tên mô tả → khó tìm kiếm sau này.
- **Không chuyên nghiệp**: Thư mục Google Drive lộn xộn, mất thời gian tổ chức.

**Workflow này giải quyết tất cả!** Sử dụng **GPT-4o** để tự động **đổi tên file** dựa trên nội dung trong email, đồng thời **lưu trữ lên Google Drive** với tên mô tả rõ ràng. **Không cần code, chỉ cần cấu hình!**

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy 24/7 mà không gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần thủ công đổi tên file mỗi ngày.
✅ **Tên mô tả chính xác**: GPT-4o tự động phân tích nội dung email để đặt tên file logic (ví dụ: *"Báo cáo doanh thu Q2 2024.pdf"* thay vì *"file1.pdf"*).
✅ **Lưu trữ tự động**: File được tải xuống và lưu vào Google Drive ngay lập tức.
✅ **Hoạt động liên tục**: Workflow chạy theo lịch trình (ví dụ: mỗi ngày 8h sáng) mà không cần can thiệp.
✅ **Giảm rủi ro mất file**: Không bao giờ quên đổi tên file hoặc quên lưu trữ.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để kết nối Gmail và Google Drive).
2. **API Key OpenAI** (để sử dụng GPT-4o):
   - Đăng ký tại [OpenAI API](https://platform.openai.com/) và tạo một **API Key**.
   - **Lưu ý**: Workflow sử dụng mô hình **gpt-4o-mini** (rẻ hơn gpt-4o nhưng vẫn hiệu quả).
3. **Thư mục Google Drive** để lưu file tự động (ví dụ: *"Automated Uploads"*).
4. **N8n Self-hosted** (không dùng phiên bản miễn phí trên cloud).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/7585](https://n8n.io/workflows/7585) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này gồm **10 node**, nhưng các node quan trọng nhất cần cấu hình kỹ:

##### **A. Cấu Hình API Key OpenAI**
- **Node**: `OpenAI Chat Model` (gpt-4o-mini)
  - Đi đến **Credentials** → Tạo mới **OpenAI API Key**.
  - Điền **API Key** từ OpenAI vào trường `apiKey`.
  - **Lưu ý**: Nếu không có API Key, workflow sẽ **không chạy được** phần AI.

##### **B. Kết Nối Gmail**
- **Node**: `Get Unread Messages with Attachments` và `Download Attachments`
  - Đi đến **Credentials** → Tạo mới **Gmail**.
  - Chọn **Use OAuth 2.0** và đăng nhập tài khoản Gmail.
  - **Lưu ý**:
    - Workflow sẽ **lấy tất cả email chưa đọc có file đính kèm**.
    - Sau khi xử lý, email sẽ được **đánh dấu là đã đọc** (node `Mark message as read`).

##### **C. Cấu Hình Google Drive**
- **Node**: `Upload file`
  - Đi đến **Credentials** → Tạo mới **Google Drive**.
  - Chọn **Use OAuth 2.0** và đăng nhập tài khoản Google.
  - **Lưu ý**:
    - Chọn **thư mục đích** (ví dụ: *"Automated Uploads"*) để lưu file.
    - Workflow sẽ **tải file từ Gmail lên Google Drive** với tên mới.

##### **D. Cấu Hình AI Agent (GPT-4o)**
- **Node**: `AI Agent` và `OpenAI Chat Model`
  - **Prompt mẫu** (cần chỉnh sửa để phù hợp):
    ```
    Tóm tắt nội dung email và đề xuất tên file phù hợp cho file đính kèm.
    Ví dụ:
    - Nếu email nói về "Báo cáo doanh thu Q2 2024", tên file nên là "Báo cáo doanh thu Q2 2024.pdf".
    - Nếu email là "Lời mời hội nghị", tên file nên là "Lời mời hội nghị 15-06-2024.pdf".
    ```
  - **Lưu ý**:
    - Nếu GPT-4o trả về tên không phù hợp, các sếp có thể **cập nhật prompt** để chính xác hơn.

##### **E. Thời gian chạy (Schedule Trigger)**
- **Node**: `Schedule Trigger`
  - Chọn **lịch trình chạy** (ví dụ: **mỗi ngày 8h sáng**).
  - **Lưu ý**: Workflow sẽ chạy tự động theo lịch này mà không cần kích hoạt thủ công.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Chọn **Run Workflow** và kiểm tra với **1-2 email mẫu**.
  - Kiểm tra:
    - File được tải xuống và đổi tên đúng không?
    - File được lưu vào Google Drive đúng thư mục không?
    - Email đã được đánh dấu là đã đọc không?
- **Bật Active**:
  - Sau khi test thành công, chuyển **Active** sang **ON**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack/Telegram** để thông báo khi workflow hoàn thành.
   - Ví dụ: *"File đã được đổi tên và lưu trữ thành công: [Tên file]"*.

2. **Lưu Log Lịch Sử**:
   - Thêm node **Google Sheets** để ghi lại lịch sử đổi tên file (tên file cũ, tên file mới, ngày giờ xử lý).

3. **Xử Lý File Nhiều Lớn**:
   - Nếu file đính kèm quá lớn (ví dụ: video, file Excel lớn), có thể **tách node `Extract from Attachments`** để xử lý riêng.

4. **Tùy Chỉnh Prompt AI**:
   - Nếu GPT-4o không đổi tên chính xác, các sếp có thể **cập nhật prompt** để rõ ràng hơn:
     ```
     Tôi muốn tên file phải bao gồm:
     1. Chủ đề chính của email (ví dụ: "Báo cáo", "Lời mời", "Hợp đồng").
     2. Ngày tháng (nếu có).
     3. Loại file (PDF, DOCX, XLSX).
     ```

5. **Sử Dụng Mô Hình GPT-4o Mini**:
   - Workflow đã sử dụng **gpt-4o-mini** (rẻ hơn gpt-4o) nhưng vẫn hiệu quả. Nếu cần độ chính xác cao hơn, có thể **cập nhật thành gpt-4o** (tăng chi phí).

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp khỏi công việc thủ công đổi tên file, đồng thời **tăng tính chuyên nghiệp** cho thư mục Google Drive. **Chỉ cần cấu hình 1 lần**, workflow sẽ **hoạt động tự động hàng ngày** mà không cần can thiệp.

**Hãy áp dụng ngay và trải nghiệm sự khác biệt!**
👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/7585) và **self-host n8n** để bắt đầu!

---
**💡 Chia sẻ ý kiến**: Các sếp có thể **cập nhật prompt AI** hoặc **thêm node mới** để phù hợp với nhu cầu cụ thể. Hãy thử nghiệm và tối ưu hóa workflow của mình!