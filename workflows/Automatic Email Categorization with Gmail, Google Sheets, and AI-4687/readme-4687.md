---
title: "🤖 **Tự Động Hóa Phân Loại Email Gmail Bằng AI + Google Sheets (Không Cần Code!)**"
description: "Workflow tự động phân loại email vào các nhãn (labels) dựa trên nội dung thông qua AI, tiết kiệm thời gian cho các sếp quản lý email hàng ngày. Hoạt động 24/7, cá nhân hóa và chính xác cao."
slug: "tu-dong-hoa-phan-loai-email-gmail-bang-ai-google-sheets"
tags: [n8n, automation, gmail, google-sheets, ai, openrouter, no-code]
keywords: [n8n workflow email, tự động hóa phân loại email, AI phân loại email Gmail, Google Sheets tự động hóa, OpenRouter API]
---

# 🚀 **Tự Động Hóa Phân Loại Email Gmail Bằng AI + Google Sheets (Không Cần Code)**

## **💡 Nỗi Đau Của Các Sếp Và Giải Pháp Tự Động Hóa**
Các sếp thường phải mất **giờ đồng hồ** mỗi ngày để:
- **Lọc và phân loại** hàng trăm email vào các nhãn (labels) như "Khách hàng", "Hợp đồng", "Tài chính", "Quảng cáo"...
- **Tránh nhầm lẫn** giữa email quan trọng và spam, dẫn đến mất thời gian phản hồi kịp thời.
- **Cập nhật thủ công** danh sách nhãn mới khi có yêu cầu mới từ bộ phận.

**Workflow này giải quyết tất cả bằng cách:**
✅ **Phân loại tự động** email vào các nhãn dựa trên **AI** (OpenRouter) và **định nghĩa từ Google Sheets**.
✅ **Hoạt động 24/7** nhờ **Schedule Trigger**, không cần can thiệp thủ công.
✅ **Cập nhật dễ dàng** khi có yêu cầu mới (chỉ cần chỉnh sửa Google Sheets).
✅ **Tiết kiệm thời gian** lên đến **80%** cho việc quản lý email hàng ngày.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 5-10 giờ/tuần** cho việc phân loại email thủ công.
- **Chính xác cao** nhờ AI phân tích nội dung email.
- **Cá nhân hóa** theo yêu cầu của từng bộ phận (VD: "Hợp đồng" cho bộ phận pháp lý, "Tài chính" cho kế toán).
- **Hoạt động tự động** mỗi ngày (hoặc theo lịch đặt sẵn).
- **Dễ dàng mở rộng** khi có yêu cầu mới (chỉ cần thêm nhãn mới vào Google Sheets).
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| **Dịch Vụ**          | **Yêu Cầu**                                                                 | **Liên Hệ**                                                                 |
|----------------------|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| **Gmail**            | Tài khoản Google với quyền truy cập vào email cần tự động hóa.             | [Cài đặt OAuth 2.0](https://developers.google.com/gmail/api/quickstart/python) |
| **Google Sheets**    | File Google Sheets chứa **danh sách nhãn (labels)** và **định nghĩa phân loại**. | [Tạo File Mẫu](https://docs.google.com/spreadsheets/d/1LKIx1Z3dCSX1uzyZH9s2HE0QRMvLTDI6sJApFU5LTj0/edit) |
| **OpenRouter (AI)** | API Key miễn phí (hoặc trả phí cho mô hình cao cấp).                     | [Đăng ký API Key](https://openrouter.ai/settings/keys)                      |

### **2. Hệ Thống N8n**
:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)** thay vì dùng phiên bản miễn phí trên cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**
:::

---
## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Từ File JSON**
1. **Tải workflow** từ [đây](https://n8n.io/workflows/4687) (nút "Export").
2. **Mở n8n Editor** → Nhấn **"Import"** → Chọn file JSON vừa tải.
3. **Chọn "Import"** để workflow xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải workflow** từ [đây](https://n8n.io/workflows/4687) → Chọn **"Export JSON"**.
2. **Copy toàn bộ JSON** và dán vào **n8n Editor** → Nhấn **"Paste"** → **"Import"**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **12 node**, nhưng các sếp cần chú ý **các node quan trọng sau**:

#### **🔹 Node "Config" (Cấu Hình)**
- **Tham số cần điền:**
  | **Tham số**       | **Giá trị**                                                                 | **Ghi chú**                                                                 |
  |-------------------|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------|
  | `sheets_url`      | URL của Google Sheets chứa danh sách nhãn (VD: `https://docs.google.com/spreadsheets/d/1LKIx1Z3dCSX1uzyZH9s2HE0QRMvLTDI6sJApFU5LTj0/edit`) | **Không thay đổi** nếu dùng file mẫu.                                    |
  | `extra_filter`    | (Không bắt buộc) Gmail search query để lọc email (VD: `label:unread` để chỉ xử lý email chưa đọc). | **Trống** để xử lý tất cả email.                                           |
  | `limit`           | Số lượng email tối đa xử lý trong 1 lần (VD: `100`).                         | **Khuyến nghị**: 50-200 email/lần để tránh quá tải.                         |

#### **🔹 Node "OpenRouter Chat Model" (AI Phân Loại)**
1. **Thêm Credential**:
   - Nhấn **"Add Credential"** → Chọn **"openRouterApi"**.
   - Nhập **API Key** từ [OpenRouter](https://openrouter.ai/settings/keys).
2. **Chọn mô hình AI**:
   - **Miễn phí**: `deepseek/deepseek-r1:free` (tốt nhất năm 2025).
   - **Trả phí (nếu cần chất lượng cao)**: `gpt-4.1-mini`.

#### **🔹 Node "Get Labels" (Lấy Danh Sách Nhãn từ Google Sheets)**
- **Không cần chỉnh sửa**, workflow sẽ tự động lấy danh sách nhãn từ **Google Sheets** theo URL đã đặt trong **"Config"**.

#### **🔹 Node "Create Label if Doesn't Exist" (Tạo Nhãn Nếu Không Tồn Tại)**
- **Không cần chỉnh sửa**, node này tự động **tạo nhãn mới** trong Gmail nếu nhãn đó chưa tồn tại trong Google Sheets.

#### **🔹 Node "Get Messages" (Lấy Email từ Gmail)**
- **Không cần chỉnh sửa**, node này lấy tất cả email (hoặc theo `extra_filter` nếu có).

#### **🔹 Node "Loop Over Items" (Vòng Lặp Xử Lý Email)**
- **Không cần chỉnh sửa**, node này chia email thành **batch** để AI xử lý.

#### **🔹 Node "Filter" (Lọc Email Phù Hợp)**
- **Không cần chỉnh sửa**, node này **bỏ qua email không cần phân loại** (nếu có điều kiện lọc).

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run (Kiểm Tra Trước Khi Bật)**:
   - Nhấn **"Run Workflow"** → Chọn **"Test Run"** với **1-2 email mẫu**.
   - Kiểm tra:
     - AI có phân loại email vào nhãn đúng không?
     - Có lỗi nào trong **Google Sheets** hoặc **Gmail** không?
2. **Bật Workflow**:
   - Sau khi test thành công, nhấn **"Active"** để workflow **chạy tự động theo lịch**.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Cập Nhật Danh Sách Nhãn Mới**
- Khi có **nhãn mới** (VD: "Hợp đồng mới"), chỉ cần:
  1. **Thêm dòng mới** vào Google Sheets (cột `Label Name` và `Description`).
  2. **Chạy lại workflow** (hoặc chờ lịch tự động chạy).

### **2. Gửi Báo Cáo Định Kỳ**
- **Thêm node Slack/Telegram** sau **"Gmail1"** để:
  ```json
  {
    "name": "Notify Slack",
    "type": "slackWebhook",
    "credentials": ["slackWebhook"],
    "keyParameters": {
      "text": "📧 Email đã được phân loại thành: {{ $node["Gmail1"].json["labels"] }}"
    }
  }
  ```
- **Kết quả**: Các sếp được thông báo ngay khi email được phân loại.

### **3. Lưu Log Xử Lý**
- **Thêm node "Set"** sau **"Gmail1"** để lưu log vào Google Sheets:
  ```json
  {
    "name": "Log to Sheets",
    "type": "googleSheets",
    "credentials": ["googleSheetsOAuth2Api"],
    "keyParameters": {
      "sheetName": "Log",
      "appendRow": [
        {
          "emailId": "{{ $node["Gmail1"].json["threadId"] }}",
          "labelsAdded": "{{ $node["Gmail1"].json["labels"] }}",
          "timestamp": "{{ $node["Gmail1"].json["timestamp"] }}"
        }
      ]
    }
  }
  ```
- **Kết quả**: Dễ dàng **theo dõi lịch sử** phân loại email.

### **4. Chạy Workflow Theo Lịch Bất Kỳ**
- **Chỉnh sửa node "Schedule Trigger"** để chạy:
  - **Hàng ngày** (VD: 8h sáng).
  - **Hàng tuần** (VD: Chủ nhật).
  - **Theo yêu cầu** (VD: Sau khi có email mới).

---
## 📌 **Kết Luận: Áp Dụng Ngay Hôm Nay!**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc **phân loại email thủ công**, đồng thời **tăng tính chính xác** nhờ AI. **Chỉ cần 30 phút** để cài đặt và chạy, sau đó **hoạt động tự động** mỗi ngày.

👉 **Bắt đầu ngay bằng cách:**
1. **Import workflow** từ [đây](https://n8n.io/workflows/4687).
2. **Cấu hình API Keys** (Gmail, Google Sheets, OpenRouter).
3. **Test Run** và **bật Active**.

**Nếu có vấn đề**, các sếp có thể:
- **Xem video hướng dẫn** từ [Milan Vasarhelyi](https://www.youtube.com/@vasarmilan).
- **Đăng ký tư vấn miễn phí** từ [SmoothWork.ai](https://smoothwork.ai/book-a-call/).

---
**🚀 Hãy tự động hóa email của mình ngay hôm nay!** 🚀