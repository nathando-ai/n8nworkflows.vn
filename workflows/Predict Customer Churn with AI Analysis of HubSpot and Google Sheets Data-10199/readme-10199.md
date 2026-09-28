---
title: "🚀 **Phân Tích Rủi Ro Thoát Khách Hàng (Churn) Với AI - Từ HubSpot & Google Sheets Tự Động Hóa 100% (Không Cần Code!)""
description: "Workflow tự động hóa phân tích rủi ro thoát khách hàng (churn) bằng AI, kết hợp dữ liệu từ HubSpot và Google Sheets. Nhận được điểm số sức khỏe khách hàng, cảnh báo email tự động khi phát hiện nguy cơ thoát, tiết kiệm thời gian và cải thiện trải nghiệm khách hàng."
slug: "phan-tich-churn-ai-hubspot-google-sheets"
tags: [n8n, automation, ai-churn-analysis, hubspot, google-sheets, no-code, ai-agent]
keywords: [tự động hóa phân tích churn, n8n workflow churn prediction, ai phân tích khách hàng thoát, hubspot google sheets automation, cảnh báo thoát khách hàng tự động]
---

# 🚀 **Phân Tích Rủi Ro Thoát Khách Hàng (Churn) Với AI - Giải Pháp Tự Động Hóa Cho Doanh Nghiệp**

### **Nỗi Đau Của Các Sếp: "Khách Hàng Thoát Khỏi Đâu? Tôi Không Thấy Được Dấu Hiệu Sớm!"**
Các sếp đã từng gặp phải tình huống này:
- **Khách hàng không phản hồi** trong nhiều tháng, nhưng bạn không biết lý do.
- **Dữ liệu phân tán** giữa HubSpot (CRM) và Google Sheets (báo cáo sử dụng sản phẩm), khó theo dõi.
- **Phải kiểm tra thủ công** hàng trăm deal mỗi tuần, tốn thời gian và dễ bỏ sót.
- **Không có cảnh báo sớm**, dẫn đến mất khách hàng quan trọng mà không biết cách khắc phục.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Phân tích tình trạng sức khỏe khách hàng** dựa trên 3 yếu tố chính:
   - **Tuổi thọ giao dịch** (deal age > 1 năm).
   - **Sentiment tiêu cực** từ ticket/hỗ trợ.
   - **Sử dụng sản phẩm giảm sút** theo thời gian.
✅ **Cảnh báo email tự động** khi phát hiện nguy cơ thoát.
✅ **Xuất báo cáo lên Google Sheets** để theo dõi và hành động kịp thời.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng. Với chi phí thấp nhưng hiệu suất ổn định:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**).
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow AI).
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải kiểm tra từng deal thủ công, AI làm tất cả trong vài phút.
- **Chính xác cao**: Phân tích dựa trên **dữ liệu thực tế** từ HubSpot và sử dụng sản phẩm (Google Sheets).
- **Cảnh báo sớm**: Nhận email cảnh báo khi khách hàng có **rủi ro thoát**, kịp thời can thiệp.
- **Báo cáo tự động**: Dữ liệu được xuất lên **Google Sheets**, dễ theo dõi và phân tích dài hạn.
- **Cá nhân hóa hành động**: AI không chỉ cảnh báo mà còn **gợi ý nguyên nhân** (ví dụ: "Khách hàng này không sử dụng tính năng X trong 3 tháng").
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản HubSpot** (để lấy dữ liệu giao dịch - *Deals*).
2. **Google Sheets** (để lưu trữ dữ liệu sử dụng sản phẩm và kết quả phân tích).
3. **API Key OpenAI** (để sử dụng AI trong phân tích sentiment và cảnh báo).
4. **Tài khoản Email SMTP** (để gửi cảnh báo thoát khách hàng).
5. **Webhook URL** (để nhận dữ liệu ticket từ HubSpot hoặc hệ thống hỗ trợ khác).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/10199](https://n8n.io/workflows/10199) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/10199) và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **23 node** phức tạp, nhưng chỉ cần chú ý đến **các node quan trọng sau**:

##### **A. Cấu Hình Credentials (Bắt Buộc)**
| **Node**                          | **Tham Số Cần Điền**                          | **Lưu Ý**                                                                 |
|-----------------------------------|-----------------------------------------------|---------------------------------------------------------------------------|
| **HubSpot: Get All Deals**        | API Key HubSpot                               | Lấy từ **Settings > Integrations > API Keys** trong HubSpot.               |
| **Config: Set LLM for Agent**     | OpenAI API Key                                | Điền vào **Settings > Credentials** trong n8n.                             |
| **Tool: Get Feature Usage**       | Google Sheets Document ID                     | ID Sheet được chia sẻ với n8n (cần quyền đọc).                          |
| **Email: Send Churn Alert**       | SMTP Credentials (From/To email)              | Cấu hình SMTP từ nhà cung cấp email (Gmail, Outlook, SendGrid...).         |

##### **B. Cấu Hình Webhook & Tool**
- **Trigger: Receive Tickets for Scoring**:
  - **Path**: Giá trị mặc định (`9696956a-460a-4c45-aa3c-e5f83ce95e54`) **không thay đổi**.
  - **HTTP Method**: Để mặc định là `POST`.
- **Tool: Calculate Sentiment Score**:
  - **Webhook URL**: Điền **URL Webhook** của workflow này (có thể lấy từ **Settings > Webhooks** trong n8n).
- **Tool: Get HubSpot Data**:
  - **Endpoint URL**: Điền **URL API MCP** của HubSpot (thường là `https://api.hubapi.com/mcp/v1/objects/deals`).

##### **C. Cấu Hình Google Sheets**
- Trong **Tool: Get Feature Usage from Sheets**:
  - **Sheet Name**: Điền tên **tab** trong Google Sheets (ví dụ: `Feature_Usage`).
  - **Range**: Điền phạm vi dữ liệu (ví dụ: `A1:Z1000`).

##### **D. Cấu Hình Email Cảnh Báo**
- Trong **Email: Send Churn Alert**:
  - **From Email**: Điền địa chỉ email gửi (ví dụ: `support@doanhnghiep.com`).
  - **To Email**: Điền địa chỉ email nhận cảnh báo (ví dụ: `team@doanhnghiep.com`).
  - **Subject**: Có thể chỉnh lại (ví dụ: **"CẢNH BÁO: Khách hàng [Deal Name] có nguy cơ thoát!"**).

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chạy **Manual Trigger** (`Manual Trigger: Run Churn Analysis`) với **1-2 deal mẫu** để kiểm tra.
   - Kiểm tra **Google Sheets** và **email** xem có nhận được kết quả không.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật Active** workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm **node Slack/Telegram** sau **Email: Send Churn Alert** để cảnh báo ngay khi phát hiện rủi ro.
2. **Lưu Log Dữ Liệu**:
   - Sử dụng **node StickyNote** để ghi lại lịch sử phân tích, giúp theo dõi khách hàng đã được cảnh báo.
3. **Tự động Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **node Schedule** (n8n Pro) để chạy workflow hàng tuần/month và gửi báo cáo tổng hợp.
4. **Cải Thiện AI Prompt**:
   - Trong **AI Chain: Analyze for Churn Risk**, có thể **tùy chỉnh prompt** để AI phân tích sâu hơn (ví dụ: thêm yêu cầu phân tích chi tiết về **tính năng nào bị bỏ qua**).

---
### 📌 **Kết Luận: Áp Dụng Ngay Để Tránh Mất Khách Hàng!**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công, đồng thời **giảm thiểu rủi ro thoát khách hàng** bằng cách:
✔ **Phân tích tự động** dựa trên dữ liệu thực tế.
✔ **Cảnh báo sớm** trước khi khách hàng thoát.
✔ **Xuất báo cáo** để theo dõi và hành động kịp thời.

**Hành động ngay!**
1. Import workflow và cấu hình theo hướng dẫn.
2. Test với **1-2 deal** để đảm bảo hoạt động.
3. **Bật Active** và theo dõi kết quả!

---
**Cần hỗ trợ thêm?**
- Liên hệ tác giả: [thomas@pollup.net](mailto:thomas@pollup.net) (nếu cần chỉnh sửa workflow).
- **Tự host n8n** với chi phí thấp: [TinoHost](https://tino.vn/vps-n8n?affid=388) hoặc [BNIX](https://my.bnix.one/aff.php?aff=172).

**Chúc các sếp thành công với chiến lược giữ chân khách hàng hiệu quả!** 🚀