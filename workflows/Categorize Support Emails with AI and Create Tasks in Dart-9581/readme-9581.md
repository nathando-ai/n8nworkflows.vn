---
title: "🤖 **Tự Động Hóa Email Hỗ Trợ với AI + Tạo Nhiệm Vụ trong Dart (Không Cần Code!)**"
description: "Workflow này tự động phân loại email hỗ trợ vào 7 danh mục khác nhau bằng AI, gán độ ưu tiên và tạo nhiệm vụ trong Dart với metadata chi tiết. Giúp đội ngũ hỗ trợ tiết kiệm 80% thời gian triệt lý email thủ công."
slug: "tieu-dong-hoa-email-ho-tro-voi-ai-tao-nhiem-vu-dart"
tags: [n8n, automation, dart, ai, gmail, no-code, support-ticket]
keywords: [tự động hóa email hỗ trợ, phân loại email với AI, tạo nhiệm vụ Dart tự động, n8n workflow, triệt lý email không code]
---

# 🚀 **Tự Động Hóa Email Hỗ Trợ với AI + Tạo Nhiệm Vụ trong Dart (Không Cần Code!)**

### **Giải pháp cho đội ngũ hỗ trợ bị ngập dưới email**
Hàng ngày, các sếp phải mất **30-60 phút** để triệt lý email hỗ trợ: phân loại, gán độ ưu tiên, chuyển đổi thành nhiệm vụ và theo dõi. **Workflow này tự động hóa toàn bộ quy trình** bằng AI, giúp:
- **Phân loại email** vào 7 danh mục chính xác (Tiền lương, Yêu cầu tính năng, Báo lỗi,...) chỉ trong **5 giây**.
- **Gán độ ưu tiên tự động** dựa trên nội dung và ngữ cảnh.
- **Tạo nhiệm vụ trong Dart** với metadata chi tiết (tóm tắt, lý do phân loại, độ tin cậy AI).
- **Tiết kiệm 80% thời gian** cho đội ngũ hỗ trợ, giảm thiểu sai sót và tăng hiệu suất.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao cho AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Từ 30-60 phút/ngày xuống **5 phút** để review nhiệm vụ tự động tạo.
✅ **Chính xác cao**: AI phân loại với độ tin cậy **>90%** (có thể điều chỉnh).
✅ **Cá nhân hóa nhiệm vụ**: Mỗi nhiệm vụ có **tóm tắt, lý do phân loại, và độ ưu tiên** chi tiết.
✅ **Hoạt động liên tục**: Workflow chạy **24/7** ngay cả khi sếp nghỉ ngơi.
✅ **Tích hợp Dart**: Nhiệm vụ tự động xuất hiện trong **Dartboard** của sếp, sẵn sàng xử lý.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Dart** (đăng ký tại [dart.ai](https://dart.ai)) và **API Key** của Dart.
2. **Tài khoản Gmail** (để trigger workflow khi nhận email hỗ trợ).
3. **API Key OpenAI** (để sử dụng mô hình AI `gpt-4.1-mini` hoặc khác).
4. **Dartboard ID** (ID của bảng nhiệm vụ trong Dart nơi sẽ tạo nhiệm vụ mới).
5. **Email nhấn nhận hỗ trợ** (cần thiết để trigger workflow).

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/9581](https://n8n.io/workflows/9581) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/9581) và dán vào **Create Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **8 node** quan trọng, các sếp cần cấu hình như sau:

##### **A. Cấu hình Gmail Trigger (Launch workflow on email receive)**
- **Node**: `gmailTrigger`
- **Thao tác**:
  - Đăng nhập tài khoản Gmail vào **credentials `gmailOAuth2`**.
  - **Filter**:
    - **Subject**: Đặt tên email nhấn nhận hỗ trợ (ví dụ: `support@tên-doanh-nghiệp.com`).
    - **Sender**: Nếu email đến từ **Google Group**, chọn **Filter: "Sender"** và nhập tên nhóm.
  - **Test**: Gửi 1 email mẫu để kiểm tra trigger hoạt động.

##### **B. Cấu hình Dart API (Retrieve an existing dartboard & Create task)**
- **Node**: `dart` (3 node: `Retrieve an existing dartboard`, `Create a new task`, `Create a new comment`)
- **Thao tác**:
  - Đăng ký **credentials `dartApi`** với:
    - **API Key** từ Dart.
    - **Base URL**: `https://api.dart.ai`.
  - **Node `Retrieve an existing dartboard`**:
    - Thay thế `resource` từ `Dartboard` thành **ID của Dartboard** của sếp (lấy từ [Dart Workspace](https://dart.ai)).
  - **Node `Create a new task`**:
    - Đảm bảo **credentials `dartApi`** đã được cấu hình.
    - **Test**: Gửi 1 email mẫu để kiểm tra nhiệm vụ được tạo thành công.

##### **C. Cấu hình OpenAI (OpenAI Chat Model)**
- **Node**: `lmChatOpenAi`
- **Thao tác**:
  - Đăng ký **credentials `openAiApi`** với:
    - **API Key** từ OpenAI.
    - **Model**: Đặt mặc định là `gpt-4.1-mini` (có thể thay đổi thành `gpt-4` nếu muốn chất lượng cao hơn).
  - **Test**: Gửi 1 email mẫu để kiểm tra AI phân loại chính xác.

##### **D. Cấu hình Code Nodes (Cleaning up full text of email & Parsing stage)**
- **Node `Cleaning up full text of email`**:
  - Chức năng **strip HTML tags** và chuyển email thành **plain text** để AI xử lý dễ dàng.
  - **Không cần chỉnh sửa** (n8n tự động thực hiện).
- **Node `Parsing stage for logic result`**:
  - Chuyển kết quả AI từ **text thành JSON** để tạo nhiệm vụ.
  - **Không cần chỉnh sửa** (n8n tự động phân tích).

---

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Gửi **1 email mẫu** (ví dụ: "Tôi muốn biết cách thanh toán tiền lương tháng này").
  - Kiểm tra:
    - Email có được **phân loại** vào danh mục `Billing` không?
    - Nhiệm vụ có được tạo trong Dart không?
    - Metadata (tóm tắt, độ tin cậy, lý do phân loại) có đầy đủ không?
- **Bật Active**:
  - Sau khi test thành công, **bật workflow** để hoạt động liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tùy chỉnh danh mục phân loại**:
   - Mở node `Email triage assistant logic` (type `agent`) và chỉnh sửa **prompt AI** để thêm/bỏ danh mục.
   - Ví dụ: Thêm danh mục `Customer Feedback` hoặc loại bỏ `Task Updates` nếu không cần.

2. **Sử dụng mô hình AI khác**:
   - Thay đổi `model` trong node `OpenAI Chat Model` từ `gpt-4.1-mini` thành `gpt-4` (tốn kém hơn nhưng chính xác hơn) hoặc `gpt-3.5-turbo`.

3. **Gửi báo cáo định kỳ**:
   - Thêm node **Slack/Telegram** để thông báo nhiệm vụ mới được tạo.
   - Ví dụ: "🚀 Nhiệm vụ mới được tạo: [Tên nhiệm vụ] (Danh mục: Billing, Độ ưu tiên: Cao)".

4. **Lưu log email**:
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu lịch sử email và nhiệm vụ đã xử lý.

5. **Kết hợp với Zapier/Make**:
   - Nếu sếp muốn **triển khai nhanh hơn**, có thể import workflow này vào **Zapier** hoặc **Make (Integromat)**.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp quản lý đội ngũ hỗ trợ bị ngập email. **Chỉ cần import, cấu hình 5 phút và bật hoạt động** – AI sẽ tự động:
✔ Phân loại email vào **7 danh mục chính xác**.
✔ Gán **độ ưu tiên tự động**.
✔ Tạo **nhiệm vụ trong Dart** với metadata chi tiết.
✔ **Tiết kiệm 80% thời gian** cho đội ngũ.

**Hành động ngay!**
1. **Import workflow** từ [n8n.io/workflows/9581](https://n8n.io/workflows/9581).
2. **Cấu hình Gmail, Dart và OpenAI** theo hướng dẫn trên.
3. **Test với 1 email mẫu** và bật workflow.

**🚀 Cùng tự động hóa email hỗ trợ ngay hôm nay!** 🚀