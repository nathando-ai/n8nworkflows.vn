---
title: "🏡 **Tự Động Hóa Xác Minh & Phân Loại Lead Đất Đai Với AI Claude, MLS-CRM & Google Sheets**"
description: "Workflow tự động hóa 100% không code giúp các sếp đất đai nhanh chóng phân loại lead từ nhiều nguồn (MLS, email, CRM) bằng AI, phân loại theo độ ưu tiên và gán cho nhân viên phù hợp, tiết kiệm thời gian lên đến 75%. Kết quả: tăng tỷ lệ chuyển đổi và giảm lead response time."
slug: "tieu-dong-hoa-xac-minh-phan-loai-lead-dat-dai"
tags: [n8n, automation, real-estate, ai-claude, google-sheets, lead-generation, no-code]
keywords: [tự động hóa lead đất đai, AI phân loại lead, n8n workflow đất đai, Claude Sonnet phân tích lead, CRM tự động hóa, MLS lead routing]
---

# 🚀 **Tự Động Hóa Xác Minh & Phân Loại Lead Đất Đai Với AI Claude, MLS-CRM & Google Sheets**

### **Giải pháp nào giúp các sếp đất đai:**
- **Tiết kiệm 75% thời gian** trong việc phân loại lead thủ công?
- **Chuyển đổi lead nhanh chóng** bằng AI phân tích ý định mua, ngân sách và ưu tiên?
- **Gán lead cho nhân viên phù hợp** tự động, không cần can thiệp?
- **Theo dõi và báo cáo** tất cả hoạt động trên Google Sheets?

Nếu câu trả lời là **Có**, thì workflow này là **công cụ vàng** cho các sếp đất đai, nhà môi giới, hoặc đội ngũ marketing muốn **tự động hóa quy trình lead qualification** một cách thông minh và hiệu quả.

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm thời gian**: AI phân tích lead trong vài giây thay vì mất giờ làm thủ công.
✅ **Chuyển đổi lead cao**: Lead ưu tiên được gán cho nhân viên phù hợp ngay lập tức.
✅ **Tối ưu hóa nguồn lực**: Nhân viên tập trung vào lead có tiềm năng cao nhất.
✅ **Báo cáo tự động**: Dữ liệu lead và hoạt động được ghi lại trên Google Sheets.
✅ **Hoạt động 24/7**: Workflow chạy tự động theo lịch trình, không cần can thiệp.
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Trước khi bắt đầu, các sếp cần chuẩn bị:
- **Tài khoản Anthropic API** (để sử dụng AI Claude Sonnet).
- **API Key của MLS/Real Estate Portal** (ví dụ: Realtor.com, Zillow, hoặc MLS địa phương).
- **API Key của CRM/Email** (ví dụ: HubSpot, Salesforce, hoặc Gmail API).
- **Tài khoản Google Sheets** (để lưu trữ và theo dõi lead).
- **VPS Self-hosted n8n** (để workflow chạy 24/7 ổn định).
:::

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào **n8n Editor**:
1. Tải workflow từ [n8n.io/workflows/12996](https://n8n.io/workflows/12996).
2. Nhấn **Import** trong n8n Editor.
3. Hoặc **copy toàn bộ JSON** và dán vào **Create Workflow** → **Import JSON**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **14 node**, nhưng các node **quan trọng nhất** cần cấu hình kỹ là:

#### **🔹 Node 1: Schedule Trigger (Kích hoạt theo lịch)**
- **Cấu hình**:
  - Chọn **thời gian chạy** (ví dụ: hàng ngày 8h sáng).
  - **Lưu ý**: Nếu muốn chạy **ngay lập tức**, chọn **Manual Trigger**.

#### **🔹 Node 2 & 3: Fetch Leads from MLS/Portals & CRM/Email (Lấy lead từ nhiều nguồn)**
- **Cấu hình**:
  - **Fetch Leads from MLS/Portals**:
    - Điền **URL API** của MLS (ví dụ: `https://api.mls.com/leads`).
    - Thêm **Headers** (nếu cần) và **Authentication** (API Key).
  - **Fetch Leads from CRM/Email**:
    - Nếu dùng **Gmail API**, cần **OAuth2** và **API Key**.
    - Nếu dùng **HubSpot/Salesforce**, điền **URL API** và **Credentials**.

#### **🔹 Node 4: Aggregate All Leads (Kết hợp lead từ nhiều nguồn)**
- **Lưu ý**: Node này **tự động ghép lead** từ 2 nguồn trên thành **1 dataset duy nhất**.

#### **🔹 Node 5: Split Leads for Processing (Chia lead để xử lý song song)**
- **Lưu ý**: Node này **chia lead thành nhiều batch** để AI xử lý nhanh hơn.

#### **🔹 Node 6: AI Lead Enrichment Agent (Phân tích lead bằng AI Claude)**
- **Cấu hình**:
  - **Anthropic API Key**: Điền vào **Credentials** (tạo ở [Anthropic Developer Portal](https://www.anthropic.com/api)).
  - **Model**: Chọn **claude-sonnet-4-5-20250929** (đã cấu hình sẵn).
  - **Prompt**: AI sẽ phân tích:
    - **Ý định mua** (buying intent).
    - **Ngân sách** (budget capacity).
    - **Ưu tiên** (urgency).
    - **Thông tin nhà đất** (property preferences).

#### **🔹 Node 7: Structured Output Parser (Định dạng kết quả AI)**
- **Lưu ý**: Node này **chuyển kết quả AI thành định dạng structured** (JSON) để dễ phân loại.

#### **🔹 Node 8: Check Lead Priority (Phân loại lead theo độ ưu tiên)**
- **Cấu hình**:
  - **Điều kiện**:
    - Nếu **score > 80** → **High Priority**.
    - Nếu **score < 80** → **Standard Priority**.

#### **🔹 Node 9 & 10: Route to Best-Fit Agent (Gán lead cho nhân viên phù hợp)**
- **Cấu hình**:
  - **High Priority**: Gán cho **nhân viên top** (ví dụ: `agent1@example.com`).
  - **Standard Priority**: Gán cho **nhân viên khác** (ví dụ: `agent2@example.com`).
  - **Lưu ý**: Các sếp cần **cập nhật email** của nhân viên trong **Set Node**.

#### **🔹 Node 11 & 12: Track Engagement (Theo dõi lead trên Google Sheets)**
- **Cấu hình**:
  - **Google Sheets OAuth2 API Key**: Đăng ký ở [Google Cloud Console](https://console.cloud.google.com/).
  - **Sheet Name**: Điền tên **Google Sheet** muốn lưu lead (ví dụ: `Lead_Tracking`).
  - **Operation**: Chọn **appendOrUpdate** (thêm hoặc cập nhật lead).
  - **Lưu ý**: Các sếp cần **chia sẻ Google Sheet** với n8n (quyền chỉnh sửa).

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với **dữ liệu mẫu** (nếu có).
2. **Bật Active** workflow.
3. **Kiểm tra Google Sheets** để xem lead đã được ghi lại chưa.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[**CÁCH TIẾP CẬN THÊM**]
🔹 **Kết nối với Slack/Telegram**: Gửi thông báo khi lead mới được phân loại.
🔹 **Lưu log hoạt động**: Sử dụng **n8n-nodes-base.stickyNote** để ghi lại lỗi hoặc tiến trình.
🔹 **Báo cáo định kỳ**: Tạo **workflow báo cáo hàng tuần** từ Google Sheets.
🔹 **Tối ưu AI**: Cập nhật **prompt** để phù hợp với thị trường địa phương.
:::

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp đất đai muốn:
✔ **Tự động hóa lead qualification** một cách thông minh.
✔ **Tiết kiệm thời gian** và **tăng tỷ lệ chuyển đổi**.
✔ **Theo dõi lead** một cách chuyên nghiệp.

**Hãy áp dụng ngay và bắt đầu tự động hóa đội ngũ của mình!** 🚀

---
**💡 Cần hỗ trợ thêm?**
- **Liên hệ tác giả**: [Dr. Cheng Siong CHIN](https://n8n.io/workflows/12996) (để custom hóa workflow).
- **Hỏi đáp**: Trên [n8n Community](https://community.n8n.io/) hoặc [Facebook Group n8n Việt Nam](https://www.facebook.com/groups/n8nvietnam).