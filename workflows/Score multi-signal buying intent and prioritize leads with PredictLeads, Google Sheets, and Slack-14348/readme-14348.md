---
title: "🚀 Tự Động Hóa Đánh Giá Tiềm Năng Mua Hàng Multi-Signal & Ưu Tiên Lead với PredictLeads, Google Sheets & Slack"
description: "Workflow tự động hóa đánh giá tiềm năng mua hàng từ nhiều tín hiệu (hiring, tech stack, news) và ưu tiên lead cho sales, tiết kiệm 10+ giờ/tháng cho các sếp marketing/sales. Kết quả: Dữ liệu chính xác, cá nhân hóa, hoạt động liên tục 24/7."
slug: "tieu-dong-hoa-danh-gia-tien-nang-mua-hang-multi-signal"
tags: [n8n, automation, lead-generation, ai-summarization, sales-prioritization, google-sheets, slack-integration, predictleads]
keywords: [n8n workflow tự động hóa, đánh giá tiềm năng mua hàng, prioritize leads, PredictLeads API, tự động hóa sales, Google Sheets automation, Slack alert]
---

# 🚀 **Tự Động Hóa Đánh Giá Tiềm Năng Mua Hàng Multi-Signal & Ưu Tiên Lead Cho Sales**

### **Giải pháp cho các sếp marketing/sales:**
Bạn đã từng phải mất **giờ đồng hồ** để phân tích hàng trăm lead, đánh giá tiềm năng mua hàng từ nhiều nguồn (tin tức, việc làm mới, thay đổi công nghệ) và quyết định ưu tiên ai? **Workflow này tự động hóa toàn bộ quy trình đó chỉ trong vài giây mỗi ngày!**

Dựa trên **3 tín hiệu chính** (hiring, tech stack, news events) từ **PredictLeads**, workflow sẽ:
✅ **Đánh giá tiềm năng mua hàng** với hệ thống điểm số chính xác.
✅ **Lọc và ưu tiên lead** cao nhất cho sales team.
✅ **Gửi báo cáo Slack** và **lưu dữ liệu vào Google Sheets** để theo dõi.
✅ **Hoạt động tự động** hàng ngày, không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo dữ liệu an toàn và không bị giới hạn.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao cho workflow)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Không cần phân tích thủ công hàng trăm lead mỗi ngày.
- **Dữ liệu chính xác:** Đánh giá tiềm năng dựa trên **3 tín hiệu thực tế** (hiring, tech stack, news).
- **Ưu tiên lead hiệu quả:** Sales team chỉ tập trung vào lead có **tiềm năng cao nhất**.
- **Hoạt động liên tục:** Workflow chạy tự động hàng ngày, không bỏ lỡ bất kỳ tín hiệu nào.
- **Tích hợp Slack & Google Sheets:** Báo cáo và dữ liệu được cập nhật ngay lập tức.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản PredictLeads** ([predictleads.com](https://predictleads.com)) để lấy **API Key**.
✔ **Google Sheets** với:
   - **Sheet đầu vào** (cột `domain` chứa danh sách công ty prospect).
   - **Sheet đầu ra** (để lưu lead đã lọc, với cột: `domain`, `hiring_signal`, `tech_signal`, `news_signal`, `intent_score`).
✔ **Slack Workspace** và **API Token** để gửi alert.
✔ **N8n Self-hosted** (không dùng phiên bản cloud để đảm bảo dữ liệu an toàn).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/14348) hoặc copy toàn bộ mã JSON từ đây.
- Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON và nhấn **"Import"**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **10 node** chính, các sếp cần cấu hình như sau:

##### **🔹 Node "Daily Prospect Scan Trigger" (ScheduleTrigger)**
- **Cấu hình:** Chọn **"Daily"** và thời gian **8h sáng** (hoặc thời gian phù hợp).
- **Lưu ý:** Workflow sẽ chạy hàng ngày tại thời gian này.

##### **🔹 Node "Get Prospect List" (Google Sheets)**
- **Chọn Credential:** Lựa chọn tài khoản Google Sheets đã kết nối.
- **Chọn Sheet:** Chọn **sheet đầu vào** (cột `domain` chứa danh sách công ty).
- **Lưu ý:** Đảm bảo cột `domain` có **dữ liệu hợp lệ** (ví dụ: `google.com`, `microsoft.com`).

##### **🔹 Node "Fetch Tech Stack", "Fetch Job Openings", "Fetch News Events" (PredictLeads)**
- **Thêm Credential PredictLeads:**
  - Vào **Credentials** → **"Add"** → Chọn **"PredictLeads"**.
  - Điền **API Key** từ tài khoản PredictLeads.
- **Lưu ý:**
  - Các node này **không cần cấu hình thêm** (sử dụng mặc định).
  - Đảm bảo **API Key** còn hiệu lực.

##### **🔹 Node "Normalize Data and Score" (Code)**
- **Mã mặc định đã sẵn sàng**, nhưng các sếp có thể **tùy chỉnh trọng số** (weights) cho từng tín hiệu:
  - `hiring x5` (việc làm mới có ảnh hưởng lớn nhất).
  - `tech x3` (thay đổi công nghệ).
  - `news x2` (tin tức mới).
- **Lưu ý:** Nếu muốn thay đổi, mở node **Code** → Sửa phần `intentScore = (hiring * 5) + (tech * 3) + (news * 2)`.

##### **🔹 Node "Filter High Intent Leads" (If)**
- **Cấu hình điều kiện:**
  - **Intent Score > 20** (mặc định).
  - **Lưu ý:** Nếu muốn **lọc chặt chẽ hơn**, giảm số này (ví dụ: `> 30`).

##### **🔹 Node "Rank Leads by Intent Score" (Sort)**
- **Sắp xếp theo:** `intent_score` (giảm dần).
- **Lưu ý:** Lead có điểm cao nhất sẽ được **ưu tiên đầu tiên**.

##### **🔹 Node "Save Qualified Leads to Sheet" (Google Sheets)**
- **Chọn Sheet đầu ra** (đã tạo trước đó).
- **Chọn Operation:** **"Append"** (thêm dữ liệu mới vào sheet).
- **Lưu ý:** Đảm bảo **cột trong sheet đầu ra khớp** với cột trong workflow (`domain`, `hiring_signal`, `tech_signal`, `news_signal`, `intent_score`).

##### **🔹 Node "Send Slack Alert" (Slack)**
- **Chọn Credential Slack** đã kết nối.
- **Chọn Channel** muốn gửi alert.
- **Lưu ý:** Thiết kế message có thể tùy chỉnh (ví dụ: thêm emoji, link, hoặc format khác).

---

#### **3. Kích hoạt ⚡️**
- **Test Run:**
  - Nhấn **"Execute"** để chạy thử với **dữ liệu mẫu**.
  - Kiểm tra **Slack** và **Google Sheets** để đảm bảo dữ liệu được gửi và lưu đúng.
- **Bật Active:**
  - Sau khi kiểm tra thành công, **bật workflow** để chạy tự động hàng ngày.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp thêm Email Alert:**
   - Sử dụng **node `n8n-nodes-base.email`** để gửi báo cáo hàng tuần cho sales team.

2. **Lưu Log Dữ liệu:**
   - Thêm **node `n8n-nodes-base.stickyNote`** để ghi lại lịch sử chạy workflow.

3. **Tùy chỉnh Threshold:**
   - Nếu muốn **lọc lead chặt chẽ hơn**, giảm **intent score threshold** (ví dụ: từ `20` xuống `30`).

4. **Kết hợp với CRM:**
   - Sau khi lọc lead, **tích hợp với HubSpot, Salesforce** để cập nhật thông tin vào CRM.

5. **Báo cáo Định Kỳ:**
   - Sử dụng **node `n8n-nodes-base.scheduleTrigger`** để gửi báo cáo **tùy chỉnh** (ví dụ: hàng tháng).

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp marketing/sales để tập trung vào **quá trình bán hàng thực tế** thay vì phân tích lead thủ công. Với **3 tín hiệu chính** (hiring, tech stack, news), nó **đánh giá tiềm năng mua hàng chính xác** và **ưu tiên lead hiệu quả nhất**.

**🚀 Hành động ngay:**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình các credential** (Google Sheets, PredictLeads, Slack).
3. **Bật workflow** và **nhận lead ưu tiên hàng ngày**!

**Cần hỗ trợ?** Liên hệ với tác giả [Yaron Been](https://www.linkedin.com/in/yaronbeen/) hoặc tham khảo [Youtube Channel](https://www.youtube.com/@YaronBeen/videos) để học thêm!

---
**Chúc các sếp thành công với tự động hóa sales!** 💪🚀