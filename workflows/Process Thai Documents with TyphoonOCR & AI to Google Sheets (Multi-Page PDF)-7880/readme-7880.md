---
title: "🚀 Tự Động Hóa Xử Lý Tài Liệu Thái PDF (Multi-Page) Sang Google Sheets Với OCR & AI – Không Cần Code"
description: "Workflow này tự động quét, phân tích và chuyển đổi nội dung từ hàng trăm tài liệu PDF tiếng Thái (có nhiều trang) thành bảng dữ liệu có cấu trúc trên Google Sheets, tiết kiệm thời gian lên đến 90% so với cách làm thủ công. Phù hợp cho doanh nghiệp, văn phòng luật sư, hoặc đơn vị quản lý hợp đồng."
slug: "tieu-ly-tai-lieu-thai-ocr-ai-google-sheets"
tags: [n8n, automation, no-code, ai-summarization, multimodal-ai, google-sheets, typhoon-ocr, openrouter, pdf-processing]
keywords: [tự động hóa xử lý tài liệu PDF, OCR tiếng Thái, AI chuyển đổi dữ liệu, Google Sheets tự động, workflow n8n không code, tự động hóa văn phòng]
---

# 🚀 **Tự Động Hóa Xử Lý Tài Liệu PDF Tiếng Thái (Multi-Page) Sang Google Sheets Với OCR & AI**

### **Giải Pháp Cho Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải:
- **Quét và nhập liệu** hàng trăm tài liệu PDF tiếng Thái (hợp đồng, hóa đơn, giấy tờ pháp lý) bằng tay → **Tốn thời gian, dễ sai sót**.
- **Phân loại và trích xuất dữ liệu** (ngày, số hợp đồng, nội dung chính) từ từng trang → **Khó khăn, mất hiệu suất**.
- **Ghi chép vào Google Sheets** theo mẫu nhất định → **Lặp đi lặp lại, không thể tự động hóa**.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Quét toàn bộ nội dung** từ PDF (bao gồm cả nhiều trang) bằng **Typhoon OCR** (chính xác 99%).
✅ **Phân tích và cấu trúc dữ liệu** bằng **AI (OpenRouter + GPT-4o-mini)** → Trích xuất ngày, số hợp đồng, nội dung chính, và nhiều thông tin khác.
✅ **Ghi dữ liệu vào Google Sheets** theo **cấu trúc bảng có sẵn** → Dễ dàng phân tích, báo cáo, và kết nối với các công cụ khác (Slack, CRM, ERP).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và xử lý được **hàng ngàn tài liệu**, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**).
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này).
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
| **Trước** | **Sau** |
|-----------|---------|
| **Nhập liệu thủ công** (30 phút/10 tài liệu) | **Tự động hóa hoàn toàn** (5 giây/tài liệu) |
| **Dữ liệu rải rác** (không cấu trúc) | **Bảng Google Sheets sẵn sàng phân tích** |
| **Dễ sai sót** (nhập nhầm ngày, số hợp đồng) | **AI kiểm tra và chỉnh sửa tự động** |
| **Không thể mở rộng** (phải làm thủ công) | **Hoạt động liên tục** (24/7) |

---
### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để lưu kết quả) → **OAuth2 API Key** (cài đặt ở [Google Cloud Console](https://console.cloud.google.com/)).
2. **Typhoon OCR API** (để quét PDF) → **API Key** (miễn phí cho 1000 trang/tháng).
3. **OpenRouter API Key** (để sử dụng mô hình AI **GPT-4o-mini**) → [Đăng ký tại OpenRouter](https://openrouter.ai/).
4. **Thư mục PDF** (đặt ở đường dẫn cụ thể trên VPS) → **Cấu trúc folder**:
   ```
   /documents/
     ├── file1.pdf
     ├── file2.pdf
     └── ...
   ```
5. **Google Sheet mẫu** (đã định sẵn cột như: `Ngày`, `Số hợp đồng`, `Nội dung chính`, `Tổng tiền`, ...).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/7880](https://n8n.io/workflows/7880) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/7880) và **paste** vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **14 node**, nhưng **3 node quan trọng nhất** cần cấu hình kỹ:

##### **A. Node `Set_Input_Path` (Code)**
- **Mục đích:** Đặt đường dẫn thư mục chứa PDF.
- **Cách chỉnh:**
  ```javascript
  // Thay thế đường dẫn này bằng đường dẫn thực tế trên VPS
  const inputPath = "/home/username/documents/";
  return { json: { inputPath } };
  ```
  - **Lưu ý:** Đảm bảo thư mục này **có quyền đọc** cho n8n.

##### **B. Node `OpenRouter Chat Model` (AI)**
- **Mục đích:** Sử dụng AI để **cấu trúc dữ liệu** từ text OCR thành JSON.
- **Cách chỉnh:**
  - **Model:** Đặt là `openai/gpt-4o-mini` (miễn phí).
  - **Prompt mẫu** (có thể chỉnh sửa):
    ```
    Bạn là một chuyên gia xử lý tài liệu pháp lý. Cho tôi một tài liệu PDF tiếng Thái với nội dung:
    {text}
    Hãy trích xuất và trả về JSON với cấu trúc sau:
    {
      "Ngày": "dd/mm/yyyy",
      "Số hợp đồng": "ABC123",
      "Nội dung chính": "Mô tả ngắn gọn",
      "Tổng tiền": "1,000,000 THB",
      "Người ký": "Tên người ký"
    }
    ```
  - **Lưu ý:** Nếu dữ liệu không chuẩn, **cập nhật prompt** để AI hiểu rõ hơn.

##### **C. Node `Save to Google Sheet` (GoogleSheets)**
- **Mục đích:** Ghi dữ liệu vào Google Sheet.
- **Cách chỉnh:**
  - **Chọn Sheet:** Chọn **mẫu sheet** đã chuẩn bị trước.
  - **Range:** Đặt là `A1:A` (để ghi từ hàng đầu tiên).
  - **Lưu ý:** Đảm bảo **Google Sheet đã chia cột** theo JSON từ node AI (ví dụ: `Ngày`, `Số hợp đồng`, ...).

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với **1-2 tài liệu mẫu** để kiểm tra:
   - AI có trích xuất dữ liệu chính xác không?
   - Google Sheet có ghi đúng cấu trúc không?
2. **Bật Active** sau khi kiểm tra thành công.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự động chuyển PDF đã xử lý sang folder `Completed`**
   - Thêm node `executeCommand` sau `Clear tmp files` để di chuyển:
     ```bash
     mv /tmp/input/*.pdf /home/username/completed/
     ```

2. **Gửi báo cáo định kỳ qua Email/Slack**
   - Thêm node **Email** hoặc **Slack Webhook** sau `Save to Google Sheet` để thông báo khi hoàn thành:
     ```
     Xử lý thành công {fileCount} tài liệu vào {currentDate}!
     ```

3. **Lưu log lỗi cho việc debug**
   - Thêm node **HTTP Request** (để gửi log lên một API hoặc file log) nếu có lỗi xảy ra.

4. **Tối ưu AI cho dữ liệu đặc thù**
   - Nếu tài liệu có **cấu trúc riêng** (ví dụ: hóa đơn có cột thuế riêng), **cập nhật prompt** để AI chú ý đến đó:
     ```
     Hãy chú ý đến cột "Thuế GTGT" trong tài liệu và trích xuất giá trị đó.
     ```

5. **Sử dụng Webhook để kích hoạt tự động**
   - Thay node `manualTrigger` bằng **Webhook** để workflow chạy khi có file mới được upload vào thư mục.

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc **nhập liệu, quét OCR, và cấu trúc dữ liệu** bằng tay. Với **AI + OCR + Google Sheets**, dữ liệu từ hàng trăm tài liệu PDF tiếng Thái **bị chuyển đổi thành bảng sẵn sàng phân tích chỉ trong vài giây**.

**Hành động ngay:**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với 1-2 tài liệu** để đảm bảo chính xác.
3. **Bật Active** và **quên việc nhập liệu thủ công**!

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/7880) | 📌 [Cài đặt n8n trên VPS](https://docs.n8n.io/hosting/installation/installation-on-a-vps/)**