---
title: "🚀 Tự Động Hóa Kiểm Tra Xe Trước Khởi Hành: Đánh Giá & Phân Loại Bằng AI Cục Bộ + Cảnh Báo Ngay Lập Tức"
description: "Giải pháp tự động hóa 100% không code để đánh giá điểm số kiểm tra xe trước khi khởi hành, phân loại xe theo trạng thái, và gửi cảnh báo ngay lập tức qua email hoặc webhook. Giúp các sếp tiết kiệm thời gian, giảm thiểu lỗi nhân sự và tối ưu hóa quy trình vận chuyển."
slug: "tu-dong-hoa-kiem-tra-xe-truoc-khoi-hanh"
tags: [n8n, automation, no-code, ai-summarization, document-extraction, ollama, webhook]
keywords: [n8n workflow kiểm tra xe, tự động hóa vận chuyển, đánh giá xe bằng AI, cảnh báo lỗi xe, phân loại xe theo trạng thái]
---

# 🚀 **Tự Động Hóa Kiểm Tra Xe Trước Khởi Hành: Đánh Giá & Phân Loại Bằng AI Cục Bộ + Cảnh Báo Ngay Lập Tức**

### **🔍 Nỗi Đau Thực Tế Của Các Sếp**
Hàng ngày, các sếp phải đối mặt với quy trình kiểm tra xe trước khi khởi hành là **một công việc tốn thời gian, dễ sai sót và phụ thuộc vào nhân viên**. Các điểm kiểm tra như:
- **Trạng thái dầu nhớt, lốp xe, hệ thống phanh, đèn tín hiệu**...
- **Sự khác biệt giữa các tiêu chuẩn kiểm tra** của từng xe hoặc đội ngũ nhân viên...
- **Không có hệ thống cảnh báo tự động** khi phát hiện lỗi nghiêm trọng...

Kết quả? **Tốn thời gian, tăng chi phí bảo trì, và rủi ro an toàn vận chuyển**. Với **workflow này**, các sếp sẽ có một **hệ thống tự động hóa hoàn chỉnh**, sử dụng **AI cục bộ (Ollama)** để đánh giá điểm số, phân loại xe theo trạng thái, và gửi cảnh báo ngay lập tức – **không cần viết một dòng code nào!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo **tính riêng tư và hiệu suất cao**.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Hỗ trợ Ollama chạy ổn định)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần kiểm tra thủ công, AI tự động đánh giá trong **vài giây**.
✅ **Chính xác cao**: Sử dụng **AI cục bộ (Ollama)** để phân tích chi tiết, giảm sai sót của con người.
✅ **Phân loại tự động**: Xe được **nhận dạng trạng thái** (OK, Cảnh báo, Lỗi nghiêm trọng) và **phân loại ngay lập tức**.
✅ **Cảnh báo ngay lập tức**: **Email tự động** hoặc **webhook** gửi thông báo khi phát hiện lỗi.
✅ **Hoạt động liên tục**: Workflow chạy **24/7** trên VPS, không phụ thuộc vào nhân viên.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
✔ **API Key Ollama** (để sử dụng mô hình AI cục bộ).
✔ **Tài khoản email** (để gửi cảnh báo lỗi).
✔ **Webhook URL** (để nhận phản hồi từ hệ thống).
✔ **Dữ liệu đầu vào** (báo cáo kiểm tra xe dưới dạng **JSON hoặc text**).

---
:::note[Lưu ý quan trọng]
- Workflow **không yêu cầu kiến thức code**, nhưng các sếp cần **cấu hình đúng API Key và webhook**.
- **Không cần cài Ollama trên máy chủ n8n** nếu đã cài sẵn trên VPS (hướng dẫn [tại đây](https://ollama.ai/)).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow:
- **Tải file JSON** từ [n8n.io/workflows/15448](https://n8n.io/workflows/15448) và **import vào n8n Editor**.
- **Copy/paste JSON** từ link trên vào **n8n Editor** (tab **Import/Export**).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **12 node**, nhưng **các node quan trọng nhất** cần cấu hình kỹ:

| **Node**               | **Lưu Ý Cần Chú Ý**                                                                 | **Tham Số Cần Điền**                          |
|------------------------|------------------------------------------------------------------------------------|-----------------------------------------------|
| **Webhook3**           | **URL webhook** phải trùng khớp với **API endpoint** của hệ thống nhận dữ liệu.     | `URL Webhook` (ví dụ: `https://tên-domain.com/webhook`) |
| **Ollama AI**          | **Mô hình AI** phải được cài sẵn trên Ollama (ví dụ: `llama3`).                   | `API Key Ollama`, `Mô hình AI` (ví dụ: `llama3`) |
| **EmailSend**          | **Tài khoản email** phải được cấu hình trong **n8n Credentials**.                   | `Tên người gửi`, `Địa chỉ email nhận`       |
| **Code Nodes**         | **Logic trong code** đã được tối ưu, nhưng các sếp cần **điền đúng biến đầu vào**. | `Input JSON` (báo cáo kiểm tra xe)           |

##### **Cách cấu hình chi tiết:**
1. **Webhook3**:
   - Chọn **Credentials** là **HTTP Request** (nếu sử dụng API riêng).
   - Điền **URL webhook** vào **Request URL**.
   - **Method**: `POST`.

2. **Ollama AI**:
   - Trong **HTTP Request**, điền:
     - `URL`: `http://localhost:11434/api/generate`
     - **Headers**:
       ```json
       {
         "Content-Type": "application/json"
       }
       ```
     - **Body (JSON)**:
       ```json
       {
         "model": "llama3",
         "prompt": "$jsonInput"
       }
       ```

3. **EmailSend**:
   - Chọn **Credentials** là **Email** (cấu hình trước trong **n8n Credentials**).
   - **Subject**: `"Cảnh báo lỗi xe: $vehicleId"`
   - **Body**:
     ```
     Xe $vehicleId có lỗi nghiêm trọng: $aiResponse
     Điểm số: $finalScore
     ```

4. **Code Nodes**:
   - **Parse Input**: Chuyển dữ liệu đầu vào thành **JSON chuẩn**.
   - **Score Calculator**: Đánh giá điểm số dựa trên **tiêu chuẩn kiểm tra**.
   - **Flag Rules**: **Phân loại xe** (OK, Cảnh báo, Lỗi).
   - **Final Score**: **Tổng hợp điểm số cuối cùng**.

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Chạy **dữ liệu mẫu** (ví dụ: báo cáo kiểm tra xe dưới dạng JSON) để kiểm tra logic.
- **Bật Active**: Sau khi **cấu hình hoàn chỉnh**, **bật workflow** để hoạt động liên tục.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thay vì email, các sếp có thể **gửi cảnh báo qua Slack/Telegram** bằng **node `httpRequest`** kết nối với API của Slack/Telegram.

2. **Lưu log kiểm tra**:
   - Sử dụng **node `stickyNote`** để **ghi lại lịch sử kiểm tra** và **xem lại sau này**.

3. **Báo cáo định kỳ**:
   - **Tạo một workflow phụ** để **tổng hợp báo cáo hàng tuần/month** và gửi qua email.

4. **Cải thiện mô hình AI**:
   - Nếu **Ollama không đủ chính xác**, các sếp có thể **đào tạo mô hình riêng** trên dữ liệu kiểm tra xe của công ty.

---
### 📌 **Kết Luận**
**Workflow này không chỉ tiết kiệm thời gian mà còn giúp các sếp:**
✔ **Giảm thiểu lỗi nhân sự** với AI tự động đánh giá.
✔ **Phân loại xe nhanh chóng** và **cảnh báo ngay lập tức**.
✔ **Hoạt động 24/7** trên VPS, **không phụ thuộc vào nhân viên**.

**Hãy áp dụng ngay để tối ưu hóa quy trình vận chuyển của công ty!**
👉 **[Tải workflow ngay](https://n8n.io/workflows/15448)** và **cài đặt trên VPS** để bắt đầu tự động hóa!

---
**💡 Cần hỗ trợ thêm?**
- **Hỏi đáp trên [Community n8n](https://community.n8n.io/)**.
- **Đăng ký VPS n8n** với **mã giảm giá VPSN8N** tại [TinoHost](https://tino.vn/vps-n8n?affid=388).