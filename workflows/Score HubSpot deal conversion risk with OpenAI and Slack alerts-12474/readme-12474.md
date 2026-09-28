---
title: "🚀 Tự Động Xếp Loại Rủi Ro Chuyển Đổi Deal HubSpot Bằng OpenAI + Cảnh Báo Slack (Không Cần Code)"
description: "Workflow tự động phân tích rủi ro chuyển đổi deal trong HubSpot bằng AI OpenAI, cảnh báo ngay trên Slack khi có dấu hiệu nguy cơ cao. Giúp các sếp CRM giảm thiểu lỗ lỗ và tối ưu hóa pipeline bán hàng 24/7."
slug: "tieu-dong-xep-loai-rui-ro-chuyen-doi-deal-hubspot"
tags: [n8n, automation, crm, ai, openai, slack, hubspot, no-code, sales-funnel]
keywords: [tự động hóa hubspot, phân tích rủi ro deal, ai openai trong crm, cảnh báo slack tự động, workflow n8n crm, tối ưu pipeline bán hàng]
---

# 🚀 **Tự Động Xếp Loại Rủi Ro Chuyển Đổi Deal HubSpot Bằng AI + Cảnh Báo Slack**

### **🔍 Nỗi Đau Của Các Sếp CRM**
Hàng ngày, các sếp CRM phải mất thời gian **quét thủ công** pipeline để tìm các deal có nguy cơ bị "chết yên" (stuck) hoặc chuyển đổi chậm. Thông thường, các dấu hiệu như:
- **Thời gian phản hồi dài** từ khách hàng
- **Sự thay đổi trong hành vi** (ví dụ: không mở email, không tương tác)
- **Thông tin deal không đầy đủ** (missing details)
- **Lịch trình bị trì hoãn** không được cập nhật kịp thời

... đều là **dấu hiệu rủi ro** nhưng lại bị bỏ qua trong quá trình theo dõi thủ công. Kết quả? **Lỗ lỗ doanh thu** vì không phát hiện kịp thời để can thiệp.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Phân tích tự động rủi ro deal** bằng AI OpenAI (LangChain) với độ chính xác cao.
- **Cảnh báo ngay trên Slack** khi deal có nguy cơ chuyển đổi thấp (ví dụ: <50%).
- **Tiết kiệm 10+ giờ/tuần** cho team CRM bằng việc loại bỏ công việc thủ công.
- **Cá nhân hóa cảnh báo** với thông tin chi tiết (lý do, đề xuất hành động).
- **Hoạt động 24/7** mà không cần can thiệp người dùng.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản HubSpot** (API Key hoặc OAuth 2.0 Credentials).
2. **API Key OpenAI** (đăng ký tại [OpenAI](https://platform.openai.com/)).
3. **Slack Workspace** và **Bot Token** (để gửi cảnh báo).
4. **Google Sheets** (để lưu lịch sử phân tích, *tùy chọn*).
5. **N8n Self-hosted** (không dùng phiên bản cloud để đảm bảo dữ liệu an toàn).
:::

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/12474) hoặc sao chép mã JSON từ editor n8n.
- Mở **n8n Editor** → Nhấn **"Import"** → Chọn file JSON hoặc dán mã.
- **Lưu workflow** với tên **"HubSpot Deal Risk Analyzer"** để dễ quản lý.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **7 node chính** cần cấu hình cẩn thận:

##### **A. Node `ScheduleTrigger` (Động cơ lịch)**
- **Cấu hình:**
  - **Frequency:** Chọn **"Every 24 hours"** (hoặc tùy chỉnh theo nhu cầu).
  - **Timezone:** Đặt theo giờ của team (ví dụ: `Asia/Ho_Chi_Minh`).
- **Lưu ý:** Nếu muốn chạy thường xuyên hơn, giảm thời gian xuống **6 giờ/lần**.

##### **B. Node `HubSpot` (Lấy Deal từ HubSpot)**
- **Cấu hình:**
  - **Credentials:** Chọn **HubSpot OAuth** (đã cấu hình trước).
  - **Operation:** Chọn **"Get deals"** (hoặc **"Get deals by filter"** nếu muốn lọc deal mới).
  - **Filter:** Thêm điều kiện như:
    ```json
    {
      "properties": {
        "dealstage": "closedwon" // Loại bỏ deal đã đóng
      },
      "operator": "notIn"
    }
    ```
- **Lưu ý:** Nếu pipeline lớn, **lọc deal mới** (ví dụ: `createdAt > 7 days ago`) để tăng hiệu suất.

##### **C. Node `SplitInBatches` (Chia batch deal)**
- **Cấu hình:**
  - **Batch Size:** Đặt **50 deal/lần** (tránh quá tải API).
  - **Parallel:** Bật **"Yes"** để xử lý song song.
- **Lưu ý:** Nếu deal quá nhiều, tăng batch size lên **100**.

##### **D. Node `LangChain Agent` (Phân tích AI)**
- **Cấu hình:**
  - **Model:** Chọn **"gpt-4"** (hoặc **"gpt-3.5-turbo"** nếu tiết kiệm chi phí).
  - **Prompt Template:** Sử dụng mã mặc định từ workflow, nhưng **cập nhật** để phù hợp với ngữ cảnh HubSpot:
    ```plaintext
    Analyze the deal data and assign a risk score (1-100) based on:
    - Customer engagement (email opens, calls, meetings)
    - Deal stage progress (is it stuck?)
    - Missing information (e.g., no budget, no decision maker)
    - Time since last interaction
    Provide a summary and recommended actions.
    ```
  - **API Key:** Điền **API Key OpenAI** từ tài khoản.
- **Lưu ý:**
  - **Test prompt** với 1-2 deal mẫu trước khi chạy toàn bộ.
  - Nếu AI trả lời không chính xác, **cập nhật prompt** để rõ ràng hơn.

##### **E. Node `Code` (Xử lý dữ liệu)**
- **Cấu hình:**
  - **JavaScript Code:** Sử dụng mã mặc định để **lọc deal có rủi ro cao** (risk score < 50).
  - **Lưu ý:** Nếu muốn thay đổi ngưỡng rủi ro, chỉnh số **50** trong mã thành **60** (hoặc khác).

##### **F. Node `Slack` (Gửi cảnh báo)**
- **Cấu hình:**
  - **Credentials:** Chọn **Slack Webhook** (đã cấu hình trước).
  - **Message Format:** Sử dụng **template mặc định**, nhưng **cập nhật** để rõ ràng:
    ```plaintext
    :rotating_light: **ALERT: High-Risk Deal Detected!**
    Deal ID: {{ $node["HubSpot"].json["id"] }}
    Deal Name: {{ $node["HubSpot"].json["name"] }}
    Risk Score: {{ $node["Code"].json["riskScore"] }}/100
    Reason: {{ $node["LangChain Agent"].json["summary"] }}
    Recommended Action: {{ $node["LangChain Agent"].json["recommendedActions"] }}
    ```
  - **Channel:** Chọn **#sales-alerts** (hoặc channel phù hợp).
- **Lưu ý:**
  - **Test send** với 1 deal mẫu trước để đảm bảo format đúng.
  - Nếu muốn **gửi email thay vì Slack**, thay thế node này bằng **Node `Email`**.

##### **G. Node `Google Sheets` (Lưu lịch sử, *tùy chọn*)**
- **Cấu hình:**
  - **Credentials:** Chọn **Google Sheets API**.
  - **Sheet Name:** Đặt tên là **"HubSpot Deal Risk Log"**.
  - **Append Row:** Bật **"Yes"** để ghi dữ liệu mới vào cuối bảng.
- **Lưu ý:**
  - **Tạo cột** trong Google Sheets trước để phù hợp với dữ liệu:
    `Deal ID | Deal Name | Risk Score | Summary | Timestamp`.

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Chọn **1 deal mẫu** → Nhấn **"Execute"** để kiểm tra workflow.
- **Bật Active:** Sau khi test thành công, **bật workflow** và **đợi lịch chạy tự động**.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
1. **Kết hợp với ZoomInfo/Apollo** để lấy thông tin khách hàng chi tiết hơn.
2. **Gửi báo cáo định kỳ** (từ Google Sheets) qua **Email** hoặc **Slack** hàng tuần.
3. **Tự động cập nhật deal** trong HubSpot nếu rủi ro cao (sử dụng **Node `HubSpot Update`**).
4. **Dùng StickyNote** để ghi chú lý do deal bị rủi ro (dễ theo dõi sau này).
5. **Tích hợp với Notion** để tạo **dashboard theo dõi pipeline** tự động.
:::

---
### **📌 Kết Luận**
Workflow này **giải phóng team CRM** khỏi công việc thủ công, **giảm thiểu rủi ro chuyển đổi deal** bằng AI, và **cảnh báo kịp thời** qua Slack. **Chỉ cần 1 giờ setup**, các sếp sẽ tiết kiệm **trăm giờ công việc** mỗi tháng!

**🚀 Hành động ngay:**
1. **Cài n8n Self-hosted** trên VPS (để an toàn và ổn định).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật chạy** và **nhận cảnh báo AI** trong Slack!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💬 Cần hỗ trợ?** Đăng ký tư vấn miễn phí với [iTechNotion](https://itechnotion.com) để xây dựng workflow phù hợp với pipeline của doanh nghiệp!