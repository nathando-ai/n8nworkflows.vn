---
title: "📄 Tự Động Hóa Hóa Đơn PDF Tự Gmail → QuickBooks Với AI OpenAI (Không Cần Code)"
description: "Workflow tự động hóa hoàn toàn chuyển đổi hóa đơn PDF từ email vào QuickBooks Online với AI OpenAI để trích xuất dữ liệu chính xác, tạo hóa đơn tự động và gắn file PDF gốc. Giúp tiết kiệm 10+ giờ/tháng cho bộ phận kế toán và giảm thiểu lỗi nhập liệu."
slug: "tieu-dong-hoa-hoa-don-pdf-tu-gmail-den-quickbooks-voi-ai"
tags: [n8n, automation, invoice processing, ai-summarization, quickbooks, openai, no-code]
keywords: [tự động hóa hóa đơn PDF, n8n workflow QuickBooks, AI trích xuất dữ liệu hóa đơn, tự động hóa kế toán, giảm thời gian nhập liệu]
---

# 🚀 **Tự Động Hóa Hóa Đơn PDF Từ Email → QuickBooks Online Với AI OpenAI**

### **Giải pháp hoàn toàn tự động hóa cho bộ phận kế toán**
Hãy tưởng tượng một ngày không cần phải:
- **Tải xuống** hàng chục hóa đơn PDF từ email.
- **Nhập liệu** từng số liệu vào QuickBooks Online.
- **Tìm kiếm** tên nhà cung cấp trong danh sách QuickBooks.
- **Gắn file** hóa đơn gốc vào hóa đơn đã tạo.

Workflow này **xử lý tất cả công việc trên chỉ trong vài giây**, với độ chính xác cao hơn 95% nhờ AI OpenAI và tích hợp hoàn hảo với QuickBooks Online.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** cho bộ phận kế toán (tương đương 1 nhân viên toàn thời gian).
- **Giảm thiểu lỗi nhập liệu** đến 90% nhờ AI tự động trích xuất dữ liệu.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.
- **Gắn file PDF gốc** vào hóa đơn QuickBooks để tra cứu dễ dàng.
- **Xử lý lỗi tự động** (hóa đơn không phải hóa đơn, nhà cung cấp không tìm thấy) với thông báo cho bộ phận AP.
- **Cá nhân hóa** bằng cách gửi email xác nhận cho người gửi hóa đơn (tùy chọn).
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (để lấy email hóa đơn):
   - Tài khoản phải có quyền truy cập vào thư mục email chứa hóa đơn.
   - **Khuyến nghị**: Tạo một tài khoản riêng chỉ dùng cho automation (ví dụ: `invoice-processor@doanhnghiep.com`).

2. **API Key OpenAI**:
   - Đăng ký tại [OpenAI Platform](https://platform.openai.com/) và tạo API key.
   - **Mô hình AI**: Workflow sử dụng `gpt-4o` (mô hình mới nhất của OpenAI).

3. **Tài khoản QuickBooks Online**:
   - **Company ID (realmId)**: Tìm tại **Settings → Account and Settings → Company**.
   - **OAuth2 Credentials**: Cấu hình OAuth2 cho QuickBooks (hướng dẫn [đây](https://developer.intuit.com/app/developer/qbo/docs/develop/api/get-started/authentication)).
   - **Mã ID tài khoản chi phí mặc định** (ví dụ: "Accounts Payable", "Office Supplies").

4. **Dịch vụ n8n**:
   - **Self-hosted n8n** (khuyến nghị) để workflow hoạt động 24/7.
   - **N8n Cloud** (nếu không muốn tự host, nhưng có giới hạn tài nguyên).

5. **Thư mục lưu trữ** (nếu cần):
   - Nếu muốn lưu log hoặc file tạm thời, chuẩn bị một thư mục trên máy chủ VPS.
:::

---
## 🚀 **Cách Import & Lưu ý khi "Lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/14085](https://n8n.io/workflows/14085) (chọn **Export as JSON**).
2. **Mở n8n Editor** trên trang web hoặc máy chủ self-hosted.
3. **Nhấp vào "Import"** (icon "↑" ở góc trên bên phải).
4. **Dán JSON** và nhấp **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải file JSON** từ link trên.
2. **Mở file** bằng Notepad++/VS Code và **copy toàn bộ nội dung**.
3. **Trên n8n Editor**, nhấp vào **Import** → **Paste JSON** → **Import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Cấu hình Credentials (Bắt buộc)**
| **Node**               | **Credentials cần thiết**               | **Hướng dẫn cấu hình**                                                                 |
|------------------------|-----------------------------------------|----------------------------------------------------------------------------------------|
| **Gmail Trigger**      | `gmailOAuth2`                           | Cấu hình OAuth2 cho Gmail (hướng dẫn [đây](https://docs.n8n.io/integrations/builtins/n8n-nodes-base.gmail/#authentication)). |
| **OpenAI Chat Model**  | `openAiApi`                             | Điền `sk-...` từ OpenAI API key. Chọn mô hình `gpt-4o`.                                |
| **QuickBooks**         | `quickBooksOAuth2Api`                   | Cấu hình OAuth2 QuickBooks (hướng dẫn [đây](https://docs.n8n.io/integrations/builtins/n8n-nodes-base.quickbooks/#authentication)). |

#### **🔹 Cấu hình Node "Config" (Bắt buộc)**
Node này chứa **các tham số toàn cục** cho workflow. Các sếp phải chỉnh:
```json
{
  "realmId": "YOUR_QUICKBOOKS_REALM_ID",          // Tìm tại Settings → Account
  "apTeamEmail": "ap-team@doanhnghiep.com",       // Email bộ phận AP nhận thông báo lỗi
  "sendConfirmation": true,                      // Bật/tắt email xác nhận cho người gửi
  "defaultExpenseAccountId": "123456789",        // ID tài khoản chi phí mặc định (tìm tại Chart of Accounts)
  "binary": {                                     // Tham số cho file PDF
    "attachment_0": "$('Gmail Trigger').item.attachment_0"  // Lấy file PDF từ email
  }
}
```
**Lưu ý**:
- `realmId` và `defaultExpenseAccountId` **phải chính xác**, nếu sai sẽ gây lỗi.
- **Không chỉnh sửa** các tham số khác trừ khi biết rõ ý nghĩa.

#### **🔹 Cấu hình Gmail Trigger**
1. **Chọn tài khoản Gmail** đã cấu hình OAuth2.
2. **Bật "Simplify"** thành `false` (để lấy cả header và file đính kèm).
3. **Lọc email** (tùy chọn):
   - **Label**: Chỉ lấy email có nhãn "Invoice".
   - **Sender**: Chỉ lấy từ danh sách nhà cung cấp (ví dụ: `nccorp@email.com`).

#### **🔹 Cấu hình AI Extraction (Information Extractor)**
- Workflow sử dụng **OpenAI GPT-4o** để:
  - **Phân loại** file PDF là hóa đơn hay không (`is_invoice`).
  - **Trích xuất** dữ liệu cấu trúc như:
    - `vendor_name`, `invoice_number`, `amount`, `currency`, `due_date`, `line_items`.
- **Không cần chỉnh sửa** node này, chỉ cần đảm bảo `openAiApi` được cấu hình đúng.

#### **🔹 Cấu hình QuickBooks**
1. **Node "Search vendor"** sẽ tìm kiếm nhà cung cấp trong QuickBooks.
   - Nếu không tìm thấy, workflow sẽ gửi email báo lỗi cho bộ phận AP.
2. **Node "Create Bill"** tạo hóa đơn với:
   - **Mô tả**: Kết hợp `invoice_number` và `vendor_name`.
   - **Số tiền**: Tổng từ `amount`.
   - **Ngày**: `due_date` và `txn_date` từ AI.
3. **Node "Upload PDF to Bill"** gắn file PDF gốc vào hóa đơn.

---
### **3. Kích hoạt ⚡️ Workflow**
1. **Test Run** với một email mẫu:
   - Gửi một hóa đơn PDF cho email đã cấu hình.
   - Kiểm tra **log** trong n8n để đảm bảo workflow chạy đúng.
2. **Bật Active**:
   - Nhấp vào **Active** ở góc trên bên phải.
   - Workflow sẽ **chạy liên tục** và xử lý tất cả email mới có PDF.

---
## ✍️ **Mẹo & Gợi ý Nâng Cao**

### **1. Lọc email hiệu quả**
- **Tạo nhãn Gmail** cho email hóa đơn (ví dụ: "Invoice") và chỉ lấy email có nhãn này.
- **Lọc theo sender**: Chỉ lấy email từ danh sách nhà cung cấp thường xuyên (ví dụ: `nccorp@email.com`, `supplier2@email.com`).

### **2. Xử lý lỗi nâng cao**
- **Log lỗi**: Sử dụng node **StickyNote** để lưu log lỗi vào một file CSV hoặc Google Sheets.
- **Slack/Telegram Notifications**: Thêm node **Slack** hoặc **Telegram** để thông báo lỗi ngay khi xảy ra.

### **3. Gửi báo cáo định kỳ**
- **Tạo báo cáo hàng tháng**: Sử dụng node **Google Sheets** hoặc **Excel Online** để lưu lịch sử hóa đơn đã xử lý.
- **Email báo cáo**: Gửi email tổng hợp cho bộ phận quản lý.

### **4. Tích hợp với nhiều tài khoản QuickBooks**
- Nếu doanh nghiệp quản lý nhiều công ty QuickBooks, **tạo một workflow riêng** cho mỗi công ty và sử dụng `realmId` khác nhau.

### **5. Optimize AI Extraction**
- **Tùy chỉnh prompt**: Nếu AI trích xuất sai, có thể chỉnh sửa **node "OpenAI Chat Model"** để cải thiện độ chính xác.
- **Dữ liệu huấn luyện**: Nếu cần, có thể thêm dữ liệu huấn luyện cho **Information Extractor** để phù hợp với định dạng hóa đơn riêng của doanh nghiệp.

---
## 📌 **Kết luận**
Workflow này **giải phóng bộ phận kế toán** khỏi công việc nhàn nhạt, **giảm thiểu lỗi** và **tăng tốc độ xử lý hóa đơn** lên gấp 10 lần. Với chỉ **vài phút cấu hình**, các sếp có thể tự động hóa toàn bộ quy trình từ email đến QuickBooks, **không cần viết một dòng code nào**.

### **Bắt đầu ngay!**
1. **Cài đặt n8n** trên VPS (khuyến nghị) hoặc sử dụng **n8n Cloud**.
2. **Import workflow** và cấu hình credentials.
3. **Test với một email mẫu** và bật Active.
4. **Xem kết quả** trong vài giây: Hóa đơn PDF tự động chuyển thành hóa đơn QuickBooks với file gốc gắn liền!

---
:::note[💡 **Lời khuyên cuối cùng**]
- **Không tự host?** Sử dụng **n8n Cloud** (miễn phí cho 1 workflow).
- **Cần hỗ trợ?** Trên [n8n Community](https://community.n8n.io/) hoặc [Discord](https://n8n.io/discord) có nhiều người dùng chia sẻ kinh nghiệm.
- **Cập nhật thường xuyên**: Workflow này sử dụng các node mới nhất của n8n, nên các sếp nên cập nhật phiên bản n8n định kỳ.

**Hãy tự động hóa kế toán của mình ngay hôm nay!** 🚀