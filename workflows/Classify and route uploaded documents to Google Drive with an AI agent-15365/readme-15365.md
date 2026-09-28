---
title: "🤖 Tự Động Hóa Xếp Loại & Phân Loại Tệp Tài Liệu Sáng Tạo Bằng AI (Google Drive + Slack)"
description: "Giải pháp tự động hóa 100% không code giúp các sếp phân loại và chuyển nhượng tự động hóa các tệp PDF/PNG/JPEG vào Google Drive theo danh mục (Y tế, Khách sạn, Điện thoại,...) và cảnh báo qua Slack khi cần đánh giá. Tiết kiệm 8+ giờ/tháng cho bộ phận hành chính!"
slug: "tieu-dong-hoa-xep-loai-tai-lieu-ai-google-drive-slack"
tags: [n8n, automation, ai-agent, google-drive, slack-integration, no-code]
keywords: [tự động hóa xếp loại tài liệu, AI phân loại tệp, Google Drive tự động, Slack cảnh báo tự động, workflow n8n AI]
---

# 🚀 **Tự Động Hóa Xếp Loại & Phân Loại Tệp Tài Liệu Sáng Tạo Bằng AI (Google Drive + Slack)**

### **📌 Nỗi Đau Của Các Sếp**
Hàng ngày, bộ phận hành chính phải mất **8-10 giờ** để:
- **Tải lên** hàng trăm tệp tài liệu (PDF, hình ảnh) từ email, Slack hay máy in.
- **Xếp loại thủ công** từng tệp vào các thư mục khác nhau (Y tế, Khách sạn, Điện thoại,...) theo tiêu chuẩn nội bộ.
- **Đánh giá lại** những tệp không rõ ràng, gây ra **lỗi phân loại** và **tốn thời gian kiểm tra sau**.
- **Quên hoặc bỏ qua** những tệp cần review, dẫn đến **rủi ro pháp lý** (ví dụ: hóa đơn y tế không được lưu đúng danh mục).

**Giải pháp này tự động hóa toàn bộ quy trình đó chỉ trong 3 bước đơn giản!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và **không bị gián đoạn**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)** với tài nguyên mạnh mẽ.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ xử lý AI nhanh)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 8+ giờ/tháng** cho bộ phận hành chính (không cần xếp loại thủ công).
✅ **Chính xác 95%+** nhờ AI Gemini phân loại tự động (không cần quy tắc thủ công).
✅ **Cảnh báo tự động** qua Slack khi tệp không rõ ràng, giúp **không bỏ qua bất kỳ tài liệu nào**.
✅ **Hoạt động liên tục** 24/7, không phụ thuộc vào nhân viên.
✅ **Dễ dàng mở rộng** cho các danh mục mới (ví dụ: thêm "Điện tử" hoặc "Vận tải").
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** (đã kích hoạt **Google Drive API**).
2. **Tài khoản Slack** (đã tạo **Bot Token** với quyền `chat:write`).
3. **API Key cho Gemini (Google Palm API)** hoặc mô hình AI khác hỗ trợ **function calling** (ví dụ: GPT-4o, Claude).
4. **6 thư mục Google Drive** đã tạo sẵn:
   - **Incoming** (tạm thời lưu tệp mới tải lên).
   - **Y tế (Medical)**.
   - **Khách sạn (Hotel)**.
   - **Nhà hàng (Restaurant)**.
   - **Công trình (Trades)**.
   - **Điện thoại (Telecom)**.
   - **Cần đánh giá (Needs Review)**.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/15365](https://n8n.io/workflows/15365) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON và **paste** vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này gồm **11 node**, nhưng **5 node quan trọng nhất** cần cấu hình kỹ:

##### **A. Node "Document Upload" (Bắt đầu)**
- **Không cần chỉnh sửa gì** (sẵn sàng nhận tệp PDF/PNG/JPEG từ form web).

##### **B. Node "Upload to Incoming Folder" (Google Drive)**
- **Chọn credential:** `googleDriveOAuth2Api` (đã tạo trước).
- **Chọn thư mục:** `Incoming` (đã tạo sẵn).
- **Lưu ý:** Node này **không xử lý nội dung tệp**, chỉ lưu tạm và trả về **File ID** cho AI phân loại.

##### **C. Node "AI Agent: Classify & Route" (Agent LangChain)**
- **Cấu hình AI:**
  - **Model:** Chọn `Gemini 1.5 Pro` (hoặc GPT-4o, Claude).
  - **Prompt mẫu (cần chỉnh sửa):**
    ```plaintext
    Bạn là một chuyên gia phân loại tài liệu. Dựa vào tên tệp và nội dung, hãy xác định loại tài liệu này thuộc danh mục nào trong:
    - medical_invoice (Y tế)
    - restaurant_invoice (Nhà hàng)
    - hotel_invoice (Khách sạn)
    - trades_invoice (Công trình)
    - telecom_invoice (Điện thoại)

    Nếu không chắc chắn, trả lời "needs_review" và giải thích lý do.
    ```
  - **Thêm biến `fileId` và `fileName`** vào prompt để AI dựa vào thông tin này.

- **Cấu hình Tools (Function Calling):**
  - Thêm **6 tool** tương ứng với 6 node `move_to_*` (Y tế, Khách sạn,...).
  - Thêm **1 tool** `move_to_review` (để chuyển tệp cần đánh giá).
  - Thêm **1 tool** `send_review_alert` (để gửi cảnh báo Slack).

##### **D. Node "Gemini Chat Model" (lmChatGoogleGemini)**
- **Chọn credential:** `googlePalmApi` (đã tạo trước).
- **Không cần chỉnh sửa gì** (sẵn sàng gọi API Gemini).

##### **E. Các Node "move_to_*" (Google Drive Tool)**
- **Mỗi node** (`move_to_medical`, `move_to_restaurant`,...) cần:
  - **Chọn credential:** `googleDriveOAuth2Api`.
  - **Chọn thư mục đích** (ví dụ: `move_to_medical` → thư mục **Y tế**).
  - **Điền `fileId`** từ node trước (biến `json.fileId`).

##### **F. Node "send_review_alert" (Slack Tool)**
- **Chọn credential:** `slackApi` (đã tạo trước).
- **Chọn channel:** `#document-review` (đã tạo sẵn).
- **Message mẫu (cần chỉnh sửa):**
  ```plaintext
  🚨 **Tài liệu cần đánh giá:**
  - Tên: {{ $node["Document Upload"].json["fileName"] }}
  - Lý do: {{ $node["AI Agent: Classify & Route"].json["reason"] }}
  - Link: [Liên kết Google Drive](https://drive.google.com/file/d/{{ $node["Upload to Incoming Folder"].json["fileId"] }}/view)
  ```

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với tệp mẫu:
   - Tải lên **form web** (URL từ node `Document Upload`).
   - Chọn tệp PDF/PNG/JPEG liên quan đến **Y tế** (ví dụ: hóa đơn khám bệnh).
   - Kiểm tra **Execution Log** để xác nhận:
     - Tệp được tải lên `Incoming`.
     - AI phân loại thành `medical_invoice`.
     - Tệp được chuyển đến thư mục **Y tế**.
2. **Bật Active** workflow.
3. **Test với tệp không rõ ràng** (ví dụ: tệp không liên quan) để kiểm tra **Slack alert**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tăng độ chính xác AI:**
   - **Đổi tên tệp** trước khi upload (ví dụ: `HOADON_YTE_20240515.pdf` thay vì `file1.pdf`).
   - **Thêm prompt chi tiết hơn** trong AI Agent, ví dụ:
     ```plaintext
     Nếu tệp chứa từ khóa "bệnh viện", "bác sĩ", "thuốc" → medical_invoice.
     Nếu có "restaurant", "bills", "food" → restaurant_invoice.
     ```

2. **Kết hợp với Slack/Telegram:**
   - Thay vì Slack, có thể **gửi thông báo qua Telegram** bằng node `telegramBot`.
   - **Tự động gửi báo cáo hàng tuần** về số lượng tệp được phân loại thành công/được review.

3. **Lưu log tự động:**
   - Thêm node **Google Sheets** để ghi lại lịch sử phân loại (tên tệp, ngày upload, danh mục, người review).
   - **Tự động xóa tệp trong `Incoming` sau 7 ngày** bằng node `googleDriveTool` với `operation: delete`.

4. **Mở rộng cho nhiều danh mục:**
   - Thêm **thư mục mới** (ví dụ: `electronics_invoice`).
   - **Cập nhật prompt AI** để hỗ trợ danh mục mới.

---

### 📌 **Kết Luận**
Workflow này **giải phóng bộ phận hành chính** khỏi công việc lặp lại, **giảm thiểu lỗi phân loại**, và **tăng cường tính minh bạch** với hệ thống cảnh báo Slack. **Chỉ cần 30 phút setup**, các sếp đã có một **hệ thống tự động hóa AI hoàn chỉnh** hoạt động 24/7.

**🚀 Hành động ngay:**
1. **Cài n8n trên VPS** (đăng ký mã giảm giá [VPSN8N](https://tino.vn/vps-n8n?affid=388)).
2. **Import workflow** và **cấu hình theo hướng dẫn**.
3. **Test với tệp mẫu** và **bật Active**!

**💡 Lưu ý:** Nếu cần **phân loại chi tiết hơn** (ví dụ: trích xuất số hóa đơn, ngày hiệu lực), các sếp có thể kết hợp với **n8n Extractor** (công cụ trích xuất dữ liệu từ tệp) để nâng cao hiệu suất.

---
**📢 Cần hỗ trợ?** Đăng câu hỏi trên [n8n Community](https://community.n8n.io/) hoặc liên hệ với **Felix (Marketing Lead)** qua email: felix@n8n.io.