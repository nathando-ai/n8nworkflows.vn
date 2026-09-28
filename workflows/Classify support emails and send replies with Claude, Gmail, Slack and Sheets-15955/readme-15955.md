---
title: "🤖 **Tự Động Hóa Phân Loại & Trả Lời Email Hỗ Trợ với Claude AI, Gmail, Slack & Google Sheets**"
description: "Workflow tự động phân loại email hỗ trợ, phân loại độ ưu tiên, trả lời tự động và báo cáo toàn bộ vào Google Sheets - giúp đội ngũ hỗ trợ tiết kiệm 80% thời gian phản hồi."
slug: "tieu-dong-hoa-phan-loai-email-ho-tro-voi-claude-ai"
tags: [n8n, automation, ai-claude, gmail, slack, google-sheets, ticket-management]
keywords: [n8n workflow hỗ trợ khách hàng, tự động hóa email Claude AI, phân loại ticket tự động, trả lời email tự động, Slack báo cáo ưu tiên cao]
---

# 🚀 **Tự Động Hóa Phân Loại Email Hỗ Trợ với AI Claude + Gmail, Slack & Google Sheets**

### **Giải pháp cho đội ngũ hỗ trợ bị ngập email**
Các sếp đã từng phải làm gì khi nhận hàng chục email hỗ trợ mỗi ngày? Đọc từng tin nhắn, phân loại theo độ ưu tiên, viết trả lời và ghi log vào bảng Excel? **Workflow này tự động hóa toàn bộ quy trình** với AI Claude phân loại, trả lời tự động và báo cáo 24/7 – **không cần viết một dòng code nào!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động ổn định 24/7, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) để tránh giới hạn của phiên bản Cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian phản hồi**: AI Claude phân loại và trả lời email tự động trong giây lát.
- **Phân loại ưu tiên chính xác**: Tickets ưu tiên cao được báo cáo ngay Slack và ghi log chi tiết.
- **Báo cáo toàn diện**: Tất cả email được lưu vào Google Sheets với thời gian, nội dung và độ ưu tiên.
- **Trả lời tự động cho tickets trung bình**: Khách hàng nhận phản hồi ngay lập tức, giảm thời gian chờ.
- **Hoạt động 24/7**: Workflow hoạt động liên tục, không cần can thiệp của con người.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
- **Tài khoản Gmail chính thức** (để kết nối với Gmail Trigger và Gmail Draft).
- **API Key Anthropic** (để sử dụng Claude AI):
  👉 [Đăng ký API Key Claude](https://console.anthropic.com/) (miễn phí 100k token/month).
- **Tài khoản Slack** (để báo cáo ưu tiên cao).
- **Google Sheets** (để lưu log tất cả tickets).
- **Danh sách các danh mục hỗ trợ** (ví dụ: "Billing", "Technical Issue", "Feature Request").

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/15955) và import vào n8n Editor.
- **Copy/paste JSON** từ file vào n8n Editor (đường dẫn: `https://n8n.io/editor`).

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **A. Cấu hình Gmail Trigger**
- **Kết nối tài khoản Gmail**:
  - Vào node **Gmail Trigger** → **Add Connection** → Chọn tài khoản Gmail chính thức.
  - **Lưu ý**: Chọn **OAuth 2.0** và cấp quyền cho n8n truy cập inbox.
- **Thiết lập poll interval**:
  - Mặc định là **1 phút** (có thể điều chỉnh trong **Configure Settings**).

#### **B. Cấu hình Claude AI (Anthropic)**
- **Thêm API Key**:
  - Vào node **Claude Sonnet Model** → **Add Connection** → Nhập **API Key** từ Anthropic.
  - **Model mặc định**: `claude-sonnet-4-6` (có thể thay đổi trong **keyParameters**).
- **Build Prompt**:
  - Node này định dạng email thành cấu trúc mà Claude hiểu. Các sếp có thể chỉnh sửa **các biến** như:
    ```javascript
    const emailSubject = $input.all().subject;
    const emailBody = $input.all().body;
    ```
  - **Mẹo**: Thêm các **danh mục cụ thể** cho ngành nghề của doanh nghiệp (ví dụ: "Payment Issue", "Account Locked").

#### **C. Cấu hình Google Sheets**
- **Thêm kết nối Google**:
  - Vào node **Log Urgent Ticket**, **Log Normal Ticket**, **Log Low Priority Ticket** → **Add Connection** → Kết nối tài khoản Google.
- **Thiết lập Sheet ID**:
  - Vào node **Configure Settings** → Thay thế `YOUR_GOOGLE_SHEET_ID` bằng **ID của sheet** (tìm trong URL Google Sheets).
  - **Cấu trúc sheet**:
    | Timestamp       | Subject          | Priority | Category       | Sender Email       | Summary                          | Draft Reply                     |
    |-----------------|------------------|----------|----------------|--------------------|----------------------------------|----------------------------------|
    | 2024-05-20 10:00| Billing Issue    | High     | Payment        | user@example.com   | Khách hàng yêu cầu hoàn tiền... | "Chúng tôi sẽ xử lý ngay..."     |

#### **D. Cấu hình Slack**
- **Thêm kết nối Slack**:
  - Vào node **Alert Support Team** → **Add Connection** → Kết nối workspace Slack.
- **Thay đổi channel**:
  - Vào node **Configure Settings** → Thay thế `YOUR_SLACK_CHANNEL_ID` bằng **ID channel** (tìm trong URL Slack).

#### **E. Cấu hình Support Email**
- Vào node **Configure Settings** → Thay thế `YOUR_SUPPORT_EMAIL` bằng **email chính thức** của doanh nghiệp.

#### **F. Kích hoạt Workflow**
- **Test Run**:
  - Nhấn **Run Workflow** với một email mẫu (ví dụ: email về "Payment Issue").
  - Kiểm tra:
    - Claude có phân loại đúng không?
    - Slack có báo cáo ưu tiên cao không?
    - Google Sheets có ghi log không?
- **Bật Active**:
  - Sau khi kiểm tra thành công, chuyển trạng thái workflow sang **Active**.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Tối ưu Claude Prompt**:
   - Thêm **các rule cụ thể** cho ngành nghề (ví dụ: "Nếu khách hàng yêu cầu hoàn tiền, hãy phân loại là 'High Priority'").
   - Sử dụng **template** như:
     ```json
     {
       "instruction": "Phân loại email này vào danh mục nào? Danh sách: [Billing, Technical, Feature Request]. Nếu có từ khóa 'urgent', hãy đánh giá độ ưu tiên là 'High'.",
       "email": "$emailBody"
     }
     ```

2. **Kết hợp với Zapier/Integromat**:
   - Nếu cần báo cáo thêm vào **Notion** hoặc **Airtable**, các sếp có thể thêm node **HTTP Request** để gọi API của dịch vụ đó.

3. **Lưu log chi tiết hơn**:
   - Thêm node **Set** trước khi ghi vào Google Sheets để thêm **thông tin bổ sung** như:
     ```javascript
     {
       "timestamp": new Date().toISOString(),
       "status": "Resolved" // hoặc "Pending"
     }
     ```

4. **Báo cáo định kỳ**:
   - Sử dụng **n8n + Google Apps Script** để tự động gửi báo cáo hàng tuần vào email của quản lý.

5. **Cập nhật danh mục tự động**:
   - Thay vì chỉnh sửa code, các sếp có thể sử dụng **Google Sheets** để lưu danh sách danh mục và gọi API để cập nhật.

---

## 📌 **Kết luận**
Workflow này **giải phóng đội ngũ hỗ trợ** khỏi công việc lặp lại, giúp họ tập trung vào việc giải quyết vấn đề phức tạp. **Không cần viết code, không cần kiến thức kỹ thuật sâu** – chỉ cần import và cấu hình theo hướng dẫn.

**Hành động ngay!**
1. **Import workflow** từ [đây](https://n8n.io/workflows/15955).
2. **Cấu hình các node** theo hướng dẫn trên.
3. **Bật Active** và bắt đầu tự động hóa!

👉 **Cần hỗ trợ?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để workflow chạy ổn định 24/7!