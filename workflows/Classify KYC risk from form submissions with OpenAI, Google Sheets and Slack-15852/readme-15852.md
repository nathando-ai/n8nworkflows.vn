---
title: "🚨 Tự Động Hóa Xác Định Rủi Ro KYC Từ Form Nộp Bằng OpenAI, Google Sheets & Slack – Không Cần Code!"
description: "Tự động phân loại rủi ro KYC từ form nộp tự động bằng AI, lưu dữ liệu vào Google Sheets và cảnh báo cao rủi ro trên Slack. Giúp các sếp tiết kiệm thời gian kiểm tra thủ công, giảm thiểu rủi ro và cải thiện trải nghiệm khách hàng."
slug: "tu-dong-hoa-xac-dinh-rui-ro-kyc-bang-openai-google-sheets-slack"
tags: [n8n, automation, KYC, OpenAI, Google Sheets, Slack, AI risk assessment, no-code]
keywords: [tự động hóa KYC, phân loại rủi ro KYC, OpenAI n8n, Google Sheets tự động, cảnh báo Slack, workflow tự động hóa tài chính]
---

# 🚀 **Tự Động Hóa Xác Định Rủi Ro KYC Từ Form Nộp Bằng AI, Google Sheets & Slack**

### **Giải pháp cho các sếp ngân hàng, fintech và doanh nghiệp tài chính**
Khi các sếp phải kiểm tra thủ công hàng trăm form nộp KYC hàng ngày, việc phân loại rủi ro trở thành công việc mệt mỏi và dễ gây lỗi. **Workflow này tự động hóa toàn bộ quy trình:**
- **Nhận form nộp KYC** từ khách hàng.
- **Xác minh dữ liệu** (đảm bảo đầy đủ và hợp lệ).
- **Phân loại rủi ro** bằng AI (OpenAI) với độ chính xác cao.
- **Lưu dữ liệu** vào Google Sheets theo dạng cấu trúc.
- **Cảnh báo cao rủi ro** trên Slack để các sếp xử lý kịp thời.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian:** Không cần kiểm tra thủ công từng form, giảm thiểu sai sót.
- **Chính xác cao:** AI phân loại rủi ro với độ chính xác gần như con người.
- **Cảnh báo tức thời:** Nhận thông báo Slack khi có khách hàng cao rủi ro cần xử lý.
- **Dữ liệu sạch:** Tất cả form hợp lệ được lưu vào Google Sheets theo cấu trúc rõ ràng.
- **Hoạt động 24/7:** Workflow chạy tự động, không phụ thuộc vào giờ làm việc.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
✅ **Tài khoản n8n Self-hosted** (để chạy 24/7 ổn định).
✅ **Form KYC** với các trường dữ liệu chính xác (đảm bảo tên trường trùng khớp với workflow).
✅ **API Key OpenAI** (để kết nối với AI phân loại rủi ro).
✅ **Google Sheets** với bảng tính đã tạo sẵn (cấu trúc sẽ được định nghĩa trong workflow).
✅ **Credentials Slack** (để gửi cảnh báo cao rủi ro).
✅ **N8n Node OpenAI** (cần cài đặt từ [n8n Community](https://flow.n8n.io/)).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [n8n.io/workflows/15852](https://n8n.io/workflows/15852).
- **Mở n8n Editor** → Nhấn **Import** → Chọn file JSON.
- **Hoặc copy toàn bộ JSON** và dán vào **Import Workflow** trong n8n.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **10 node** chính, các sếp cần chú ý cấu hình các node sau:

#### **🔹 Node "KYC Form Submission" (formTrigger)**
- **Cấu hình:**
  - Chọn **Form URL** (địa chỉ form khách hàng nộp).
  - Đảm bảo **tên trường trong form** trùng khớp với mã trong workflow (ví dụ: `fullName`, `idNumber`, `address`).
  - **Test run** bằng cách gửi form mẫu để kiểm tra dữ liệu đầu vào.

#### **🔹 Node "Validate KYC Input" (code)**
- **Mục đích:** Xác minh dữ liệu đầu vào có đầy đủ và hợp lệ không.
- **Lưu ý:**
  - Các sếp **không cần chỉnh sửa mã** (nếu không biết code), vì nó đã được tối ưu sẵn.
  - Nếu form có trường bắt buộc, node này sẽ **bỏ qua** form không hợp lệ.

#### **🔹 Node "Ai Assign The Risk Category" (openAi)**
- **Cấu hình:**
  - **Credentials:** Chọn `openAiApi` (đã cấu hình trước).
  - **Prompt:** Workflow đã sử dụng **prompt mặc định** để phân loại rủi ro (Low/Medium/High).
  - **Lưu ý:**
    - Nếu muốn **cải thiện độ chính xác**, các sếp có thể chỉnh sửa prompt trong node này.
    - Ví dụ:
      ```json
      "prompt": "Analyze the KYC form data and classify the risk level as Low, Medium, or High based on the following criteria: [Điền tiêu chí cụ thể]. Return the result in JSON format: { 'riskCategory': 'Low/Medium/High', 'reason': '...' }"
      ```

#### **🔹 Node "Check High Risk" (if)**
- **Cấu hình:**
  - **Condition:** Kiểm tra `riskCategory === "High"`.
  - **Lưu ý:** Node này quyết định **lưu vào Sheets** hay **gửi cảnh báo Slack**.

#### **🔹 Node "Send High Risk Alert" (slack)**
- **Cấu hình:**
  - **Credentials:** Chọn `slackWebhook` (đã cấu hình trước).
  - **Message:** Workflow sẽ tự động tạo thông báo với thông tin khách hàng cao rủi ro.
  - **Lưu ý:**
    - Đảm bảo **webhook Slack** được cấu hình đúng (cần tạo từ **Apps Slack** → **Incoming Webhooks**).

#### **🔹 Node "Save High Risk Record" & "Save Normal Risk Record" (googleSheets)**
- **Cấu hình:**
  - **Credentials:** Chọn `googleSheetsApi` (đã cấu hình trước).
  - **Spreadsheet ID:** Điền ID của bảng Google Sheets đã tạo.
  - **Sheet Name:** Đặt tên sheet (ví dụ: `High_Risk_Records`, `Normal_Risk_Records`).
  - **Lưu ý:**
    - **Cấu trúc bảng Sheets** phải trùng khớp với dữ liệu được format trong node `Format Final Data`.
    - Ví dụ:
      | fullName | idNumber | riskCategory | reason |
      |----------|----------|--------------|--------|
      | Nguyễn Văn A | 12345678 | High | Rủi ro tài chính cao |

---
### **3. Kích hoạt ⚡️**
- **Test run:** Gửi **form mẫu** để kiểm tra workflow hoạt động như thế nào.
- **Bật Active:** Sau khi kiểm tra thành công, nhấn **Active** để workflow chạy tự động.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[**CẢI THIỆN & MỞ RỘNG**]
- **Kết hợp với Telegram:** Thay vì Slack, các sếp có thể cấu hình **Telegram Bot** để nhận cảnh báo.
- **Lưu log hoạt động:** Sử dụng **n8n Node Database** (PostgreSQL/MySQL) để lưu lịch sử form đã xử lý.
- **Gửi báo cáo định kỳ:** Tạo một **workflow báo cáo** tự động gửi tổng hợp rủi ro hàng tuần qua email.
- **Cải thiện AI:** Nếu muốn **tăng độ chính xác**, các sếp có thể:
  - **Huấn luyện mô hình riêng** bằng **Fine-tuning OpenAI**.
  - **Sử dụng prompt động** (dynamic prompt) dựa trên ngành nghề của khách hàng.
- **Tích hợp với CRM:** Lưu dữ liệu KYC vào **HubSpot, Salesforce** thay vì Google Sheets.
:::

---
## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc kiểm tra form KYC thủ công, đồng thời **giảm thiểu rủi ro** bằng AI và **cảnh báo tức thời** cho các trường hợp cao rủi ro. **Chỉ cần import, cấu hình và bật Active**, workflow sẽ hoạt động 24/7 mà không cần can thiệp.

👉 **Hãy áp dụng ngay và tự động hóa quy trình KYC của doanh nghiệp!**

---
:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Cần hỗ trợ thêm?** Đăng ký **hỗ trợ chuyên nghiệp** từ [WeblineIndia](https://www.weblineindia.com/) để tối ưu workflow! 🚀