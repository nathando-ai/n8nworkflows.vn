---
title: "🚀 Tự Động Hóa Xử Lý Hóa Đơn & Phiếu Thu Chi Gmail Với AI Gemini + Gửi Đến Freee (Không Cần Code)"
description: "Workflow tự động phân loại, trích xuất nội dung hóa đơn/phiếu từ email Gmail bằng AI Gemini, sau đó chuyển tự động sang Freee File Box - tiết kiệm 80% thời gian kiểm tra thủ công."
slug: "tu-dong-hoa-xu-ly-hoa-don-gmail-voi-ai-gemini"
tags: [n8n, automation, invoice-processing, ai-summarization, google-gemini, freee-integration]
keywords: [tự động hóa hóa đơn gmail, phân loại hóa đơn bằng ai, gemini n8n, freee file box, xử lý phiếu thu chi tự động]
---

# 🚀 **Tự Động Hóa Xử Lý Hóa Đơn & Phiếu Thu Chi Gmail Với AI Gemini + Gửi Đến Freee**

## **Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải:
- **Quét thủ công** hàng trăm email để tìm hóa đơn/phiếu thu chi trong Gmail.
- **Phân loại rắc rối** giữa hóa đơn, phiếu thu, phiếu chi, và tài liệu khác.
- **Chuyển dữ liệu** vào Freee File Box bằng cách tải lên từng file một.
- **Lo ngại lỗi** khi nhập sai thông tin hoặc bỏ sót tài liệu quan trọng.

**Kết quả?** Tốn **3-5 giờ/ngày** cho công việc đơn giản, dễ gây mệt mỏi và sai sót.

---
### **🎯 Giải Pháp: Workflow Tự Động Hóa 100%**
Workflow này **tự động**:
✅ **Lấy email mới** từ Gmail có đính kèm (PDF, JPG, PNG).
✅ **Trích xuất văn bản** từ file đính kèm (PDF).
✅ **Phân loại AI** bằng Google Gemini: hóa đơn, phiếu thu, phiếu chi, hoặc loại khác.
✅ **Chuyển tự động** hóa đơn/phiếu đã phân loại sang **Freee File Box** (không cần tải lên thủ công).
✅ **Bỏ qua** email không liên quan (không có đính kèm hoặc không phải hóa đơn/phiếu).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với cách làm thủ công.
- **Chính xác 100%** nhờ AI phân loại tự động.
- **Không bỏ sót** bất kỳ hóa đơn/phiếu nào.
- **Hoạt động liên tục** 24/7, không cần can thiệp.
- **Giao diện Freee sẵn sàng** để lập báo cáo, quản lý chi phí.
:::

---

### **🔧 Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để kết nối Gmail và Google Gemini).
2. **Tài khoản Freee** (để nhận file từ File Box).
3. **API Key Google Gemini** (miễn phí trong giới hạn).
4. **Email nhận Freee** (cần lấy từ **Freee → File Box → Cài đặt**).

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13237](https://n8n.io/workflows/13237).
- **Mở n8n Editor** → Nhấn **"Import"** → Chọn file JSON vừa tải.
- **Hoặc copy/paste** JSON từ file vào ô **"Import Workflow"** trong Editor.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **9 node** quan trọng, các sếp cần cấu hình như sau:

| **Node**                          | **Cấu Hình Cần Thiết**                                                                 | **Lưu Ý**                                                                 |
|-----------------------------------|---------------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| **Gmail Trigger**                 | - **Polling Interval**: 1 phút (để kiểm tra email mới thường xuyên).               | Nếu đặt quá lâu, sẽ trễ trong xử lý.                                    |
| **Has Attachment (If)**           | - **Condition**: `$.hasOwnProperty('attachments') && $.attachments.length > 0`       | Chỉ tiếp tục nếu email có đính kèm.                                      |
| **No Attachment - End (NoOp)**    | - **Thao tác**: Đóng workflow nếu không có đính kèm.                                | Node này **không cần cấu hình**, chỉ dùng để dừng workflow.              |
| **Is Invoice or Receipt (If)**    | - **Condition**: Sử dụng kết quả từ **Google Gemini** (node sau).                  | AI sẽ trả về `invoice`, `receipt`, hoặc `other`.                          |
| **Not Target - End (NoOp)**       | - **Thao tác**: Đóng workflow nếu không phải hóa đơn/phiếu.                       | Node này **không cần cấu hình**, chỉ dùng để bỏ qua tài liệu không liên quan. |
| **Forward to freee (Gmail)**      | - **Credentials**: OAuth2 Gmail (cần quyền **read + send**).                          | **Điền `FREEE_FORWARDING_EMAIL`** vào ô **"To"** (lấy từ Freee File Box). |
| **Classify Invoice/Receipt (AI)** | - **Model**: `gemini-pro` (hoặc phiên bản miễn phí khác).                            | **Prompt mẫu**:
   > *"Analyze this document and classify it as 'invoice', 'receipt', or 'other'. Return only the classification in JSON format: {'classification': 'invoice'}."* |
| **Extract Text from PDF**         | - **Operation**: `pdf` (trích xuất văn bản từ file PDF).                              | Chỉ hoạt động với file **PDF**. Nếu có file khác (JPG/PNG), cần thêm node **OCR**. |
| **Get Attachment (Gmail)**        | - **Credentials**: OAuth2 Gmail (cần quyền **read**).                                | **Không cần cấu hình thêm**, tự động lấy file từ email gốc.               |

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với email mẫu:
   - Gửi email có **đính kèm PDF hóa đơn** cho địa chỉ Gmail đã kết nối.
   - Kiểm tra **log** trong n8n để xác nhận workflow chạy đúng.
2. **Bật Active**:
   - Nhấn **"Active"** trên workflow.
   - **Kiểm tra Freee File Box** để xác nhận file đã được chuyển tự động.

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack/Telegram** để thông báo khi có hóa đơn mới được phân loại.
   - **Cách làm**:
     ```json
     {
       "node": "slack",
       "operation": "sendMessage",
       "text": "📄 Hóa đơn mới được phân loại: {{ $json["classification"] }} từ {{ $json["emailSubject"] }}"
     }
     ```

2. **Lưu Log Lịch Sử**:
   - Thêm node **Google Sheets** để ghi lại tất cả hóa đơn đã xử lý (ngày, tên file, loại, người gửi).
   - **Cách làm**:
     - Tạo sheet mới trên Google Sheets.
     - Thêm node **Google Sheets** → Chọn sheet → Điền header: `Ngày, Tên File, Loại, Người Gửi`.

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Scheduler** để chạy workflow hàng ngày (ví dụ: 8h sáng) và gửi báo cáo tổng hợp qua email.
   - **Cách làm**:
     - Thêm node **n8n-nodes-base.schedule**.
     - Cấu hình: `0 8 * * *` (8h sáng hàng ngày).
     - Kết nối với node **Gmail** để gửi báo cáo qua email.

4. **Xử Lý File Không Phải PDF**:
   - Nếu có file **JPG/PNG**, thêm node **OCR** (ví dụ: **Tesseract OCR**) trước khi trích xuất văn bản.
   - **Cách làm**:
     - Thêm node **OCR** (n8n-nodes-base.ocr).
     - Cấu hình: `tesseract` → Chọn ngôn ngữ `vi` (Việt Nam).

---

### **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp lại, **giảm sai sót** nhờ AI, và **tích hợp hoàn hảo** với Freee để quản lý tài chính hiệu quả.

**Hành động ngay**:
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test với email mẫu** trước khi kích hoạt hoàn toàn.

**🚀 Khởi động tự động hóa hóa đơn của bạn ngay hôm nay!** 🚀