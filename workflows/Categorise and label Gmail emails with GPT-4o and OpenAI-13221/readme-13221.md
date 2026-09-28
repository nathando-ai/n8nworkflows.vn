---
title: "🤖 **Tự Động Hóa Gmail: Phân Loại & Nhãn Email Bằng AI GPT-4o (Không Cần Code!)**"
description: "Workflow tự động phân loại và nhãn email Gmail bằng AI OpenAI, giúp các sếp loại bỏ email không quan trọng khỏi Inbox, tiết kiệm thời gian và tổ chức inbox hiệu quả 24/7."
slug: "tieu-dong-hoa-gmail-phan-loai-nhan-email-ai-gpt-4o"
tags: [n8n, automation, gmail, ai, openai, no-code, email-management]
keywords: [tự động hóa gmail, phân loại email bằng ai, nhãn email tự động, gpt-4o n8n, giảm thiểu email rác, tổ chức inbox]
---

# 🚀 **Tự Động Hóa Gmail: Phân Loại & Nhãn Email Bằng AI GPT-4o (Không Cần Code!)**

### **Nỗi Đau Của Các Sếp**
Hàng ngày, Inbox của các sếp bị ngập tràn email: **quảng cáo, tin nhắn không quan trọng, yêu cầu không ưu tiên**... Phải mất **giờ đồng hồ** để phân loại, nhãn và chuyển email vào các folder phù hợp. Kết quả? **Thời gian làm việc hiệu quả giảm 30-50%**, và nguy cơ bỏ lỡ email quan trọng tăng cao.

**Workflow này giải quyết vấn đề bằng cách:**
✅ **Tự động phân loại email** bằng AI GPT-4o (OpenAI) với độ chính xác cao.
✅ **Loại bỏ email không cần thiết** ra khỏi Inbox, giữ gìn sạch sẽ.
✅ **Áp dụng nhãn tự động** theo chủ đề (ví dụ: "Quảng cáo", "Yêu cầu", "Dự án X").
✅ **Hoạt động liên tục 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo **tính riêng tư và tốc độ tối ưu**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-10 giờ/tuần** không phải phân loại email thủ công.
- **Inbox luôn sạch sẽ**, chỉ giữ lại email **quan trọng và cần xử lý**.
- **Tự động nhãn email** theo chủ đề, giúp tìm kiếm nhanh chóng sau này.
- **AI học tập và cải thiện** dựa trên dữ liệu email mới.
- **Hoạt động tự động**, không cần can thiệp thủ công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (đã kích hoạt API Gmail).
2. **API Key OpenAI** (đăng ký tại [OpenAI](https://platform.openai.com/)).
3. **Nhãn Gmail đã tạo** cho các danh mục phân loại (ví dụ: "Quảng cáo", "Yêu cầu", "Dự án").
4. **n8n Self-hosted** (cài đặt trên VPS hoặc máy chủ riêng).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13221](https://n8n.io/workflows/13221).
- **Mở n8n Editor** → Chọn **Import** → Chọn file JSON vừa tải.
- **Hoặc copy/paste** JSON từ file vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **7 node chính**, các sếp cần cấu hình kỹ lưỡng như sau:

##### **A. Cấu Hình Gmail Trigger (Node: "Gmail Trigger")**
- **Chọn tài khoản Gmail** đã kết nối trong n8n.
- **Chọn operation**: `watch` (để theo dõi email mới).
- **Lưu ý**:
  - Nếu chưa kết nối Gmail, nhấn vào node → **Authenticate** → Đăng nhập tài khoản Gmail.
  - **Không chọn "getAll"** vì sẽ lấy tất cả email cũ, gây quá tải.

##### **B. Cấu Hình AI Phân Loại (Node: "Categorize Email")**
- **Chọn OpenAI API Key** (đã đăng ký trước).
- **Model**: Chọn **GPT-4o** (hoặc GPT-4 nếu không có).
- **Prompt mặc định** (có thể tùy chỉnh):
  ```plaintext
  Analyze the email content and categorize it into one of these labels:
  - "Quảng cáo" (Advertisement)
  - "Yêu cầu" (Request)
  - "Dự án" (Project)
  - "Khác" (Other)

  Return only the label name in JSON format: {"label": "Quảng cáo"}
  ```
- **Lưu ý**:
  - **Không cần chỉnh sửa** nếu muốn sử dụng mặc định.
  - **Nâng cao độ chính xác** bằng cách thêm **ví dụ email** vào prompt (ví dụ: `"Email này là yêu cầu vì có từ 'xin vui lòng' và 'deadline'."`).

##### **C. Cấu Hình Nhãn Gmail (Node: "Get many labels")**
- **Chạy node này trước** để lấy **ID của nhãn** đã tạo.
- **Kết quả output** sẽ hiển thị danh sách nhãn và **ID** (ví dụ: `Label_123456789`).
- **Sao chép ID** và **điền vào node "Add to folder"** (cần chỉnh sau).

##### **D. Chỉnh Sửa Node "Add to folder"**
- Mở node này → **Chọn operation**: `addLabels`.
- **Thêm các ID nhãn** vào trường `labels` (ví dụ: `["Label_123456789", "Label_987654321"]`).
- **Lưu ý**:
  - **Không để trống** trường này, nếu không email sẽ không được nhãn.
  - **Kiểm tra lại ID nhãn** để tránh lỗi.

##### **E. Node "Remove from Inbox" (Lọc Email Không Cần Thiết)**
- **Chỉnh node "Not Worthwhile" (Filter)**:
  - **Chọn condition**: `jsonpath("$.label") === "Khác"` (hoặc nhãn email không cần thiết).
  - **Kết quả**: Email được đánh nhãn "Khác" sẽ được **xóa khỏi Inbox** và chuyển vào nhãn tương ứng.

##### **F. Kiểm Tra Node "Add to folder"**
- **Chọn nhãn** muốn áp dụng cho email (ví dụ: "Quảng cáo" → `Label_123456789`).
- **Lưu ý**:
  - Nếu email không được nhãn, **hãy kiểm tra lại ID nhãn** và **prompt AI**.

#### **3. Kích Hoạt ⚡️**
- **Test Run** với **email mẫu** (ví dụ: email quảng cáo, yêu cầu) để kiểm tra:
  - AI phân loại chính xác không?
  - Email được nhãn và chuyển folder đúng không?
- **Bật Active** nếu test thành công.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tùy Chỉnh Danh Mục Phân Loại**
   - Mở node **"Categorize Email"** → **Chỉnh sửa prompt** để thêm/loại bỏ danh mục.
   - **Ví dụ**:
     ```plaintext
     - "Hỗ trợ khách hàng" (Support)
     - "Tin tức" (News)
     - "Tài chính" (Finance)
     ```

2. **Gửi Báo Cáo Định Kỳ**
   - **Thêm node Slack/Telegram** sau node **"Add to folder"** để báo cáo:
     - **"Email mới được phân loại: [Tên nhãn]"** (ví dụ: "Email mới được phân loại: Quảng cáo").
   - **Cài đặt** trên n8n: `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram`.

3. **Lưu Log Email**
   - **Thêm node "Sticky Note"** để ghi lại lịch sử phân loại:
     - **Dùng để debug** nếu AI phân loại sai.
     - **Cấu hình**: `n8n-nodes-base.stickyNote`.

4. **Tăng Độ Chính Xác AI**
   - **Thêm ví dụ email** vào prompt (ví dụ: `"Email này là yêu cầu vì có từ 'xin vui lòng' và 'deadline'."`).
   - **Sử dụng hệ thống nhãn rõ ràng** (ví dụ: "Quảng cáo" vs "Email marketing").

5. **Tự Động Xóa Email Cũ**
   - **Thêm node "Gmail" với operation: "delete"** để xóa email cũ không cần thiết.
   - **Lưu ý**: Chỉ áp dụng cho email **trên 30 ngày tuổi**.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc phân loại email thủ công, đồng thời **tổ chức inbox hiệu quả** bằng AI. **Chỉ cần 10 phút cấu hình**, các sếp sẽ có một **Inbox sạch sẽ và tự động hóa hoàn toàn**.

**Hành động ngay!**
1. **Import workflow** từ [n8n.io/workflows/13221](https://n8n.io/workflows/13221).
2. **Cấu hình Gmail + OpenAI API**.
3. **Chạy test** và **bật tự động hóa**!

**Nếu gặp vấn đề**, hãy để lại comment bên dưới hoặc liên hệ admin để hỗ trợ! 🚀