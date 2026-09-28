---
title: "🚀 Tự Động Hóa Cảnh Báo & Khắc Phục Lead HubSpot Giảm Điểm (Slack + Gmail + Google Sheets)"
description: "Workflow tự động hóa 100% không code để phát hiện và xử lý leads HubSpot có điểm số thấp, gửi cảnh báo cá nhân hóa đến sales team, tạo task theo dõi và gửi email khôi phục liên lạc. Giúp doanh nghiệp không bỏ lỡ khách hàng tiềm năng và tối ưu hóa quy trình bán hàng."
slug: "tieu-dong-hoa-can-bao-lead-hubspot-giam-diem"
tags: [n8n, automation, HubSpot, CRM, Slack, Gmail, GoogleSheets, sales-funnel, no-code]
keywords: [n8n workflow HubSpot, tự động hóa cảnh báo lead, khắc phục lead giảm điểm, Slack alert sales, Gmail tự động hóa email, Google Sheets log CRM]
---

# 🚀 **Tự Động Hóa Cảnh Báo & Khắc Phục Lead HubSpot Giảm Điểm (Slack + Gmail + Google Sheets)**

### **Giải pháp cho nỗi lo "Bỏ lỡ khách hàng tiềm năng vì không theo dõi kịp thời"**
Các sếp đang gặp phải tình trạng này chưa?
- **Lead điểm số thấp** bị bỏ qua trong hệ thống, dẫn đến mất cơ hội chuyển đổi.
- **Sales team** phải thủ công kiểm tra hàng ngày, tốn thời gian và dễ bỏ sót.
- **Khách hàng không tương tác** sau nhiều tháng, nhưng không ai biết cách khôi phục liên lạc.
- **Dữ liệu lặp lại** trong cảnh báo, làm team mệt mỏi và mất tập trung.

**Workflow này tự động hóa toàn bộ quy trình:**
✅ **Phát hiện** leads HubSpot có điểm số dưới ngưỡng (cảnh báo hoặc cấp thiết).
✅ **Cảnh báo cá nhân hóa** đến sales owner qua Slack (DM + channel).
✅ **Tạo task theo dõi** trong HubSpot để team hành động kịp thời.
✅ **Gửi email khôi phục liên lạc** tự động qua Gmail.
✅ **Lưu log toàn bộ hoạt động** trên Google Sheets để theo dõi và báo cáo.
✅ **Tránh lặp lại cảnh báo** bằng cơ chế deduplicate 24h.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và ổn định.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10-15 giờ/tuần** của sales team (không cần kiểm tra thủ công).
- **Tăng tỷ lệ chuyển đổi** bằng cách khôi phục liên lạc với leads "lạnh".
- **Cảnh báo chính xác và cá nhân hóa** (Slack DM đến owner lead).
- **Dữ liệu toàn diện** trên Google Sheets để phân tích xu hướng.
- **Không bỏ sót lead nào** nhờ cơ chế deduplicate 24h.
- **Hoạt động liên tục** 24/7, không phụ thuộc vào nhân viên.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản và API Keys**:
   - HubSpot (tạo API Key tại **Settings > Integrations > API Keys**).
   - Slack (tạo **OAuth Token** tại [Slack API](https://api.slack.com/apps)).
   - Gmail (tạo **App Password** nếu sử dụng 2FA).
   - Google Sheets (tạo **Service Account** và chia sẻ file với email service account).

2. **Google Sheets**:
   - Tạo **1 file mới** với **2 sheet tab**:
     - **Sheet 1**: `Lead Score Alerts` (cột: `Timestamp`, `Contact ID`, `Contact Name`, `Email`, `Score`, `Urgency`, `Owner Email`, `Lead Status`).
     - **Sheet 2**: `Alert Dedup Log` (cột: `contact_id`, `last_alerted`).
   - **Chia sẻ file** với email của **Google Service Account** (để n8n có quyền ghi dữ liệu).

3. **Slack Channel**:
   - Chuẩn bị **1 channel** để gửi cảnh báo (ví dụ: `#sales-alerts`).

4. **Gmail**:
   - Chuẩn bị **1 email từ** (ví dụ: `no-reply@doanhnghiep.com`) để gửi email khôi phục.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [liên kết gốc](https://n8n.io/workflows/16003) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ file và dán vào **Create Workflow** → **Import JSON** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **17 node**, các sếp cần chú ý cấu hình sau:

##### **A. Cấu hình Credentials (Tất cả node)**
- **HubSpot**:
  - **API Key**: Điền vào `Credentials` của node `HubSpot — Get Low Score Contacts` và `HubSpot — Get Contact Owner`.
  - **Domain**: Chọn domain của bạn (ví dụ: `mycompany.hubspot.com`).
  - **Low Score Threshold**:
    - **Critical**: Điểm < 20 (cảnh báo cấp thiết).
    - **Warning**: Điểm < 50 (cảnh báo thông thường).
    *(Thay đổi trong node `IF — Critical or Warning?` nếu cần.)*

- **Slack**:
  - **Token**: Điền vào `Credentials` của tất cả node Slack.
  - **Channel**: Thay đổi `channel` trong node `Slack — Critical Alert to Channel` và `Slack — Warning Alert to Channel` (ví dụ: `#sales-alerts`).
  - **DM Owner**: Node `Slack — DM to Contact Owner` sẽ tự động gửi DM đến email của owner (không cần cấu hình thêm).

- **Gmail**:
  - **Email**: Điền địa chỉ email từ trong node `Gmail — Re-Engagement Email to Contact`.
  - **Password**: Điền **App Password** (nếu sử dụng 2FA).
  - **Template Email**: Thay đổi nội dung email trong node `Gmail — Re-Engagement Email to Contact` (ví dụ:
    ```html
    <p>Chào {{$json["contact"]["properties"]["first_name"]}},</p>
    <p>Chúng tôi nhận thấy điểm số của bạn đang giảm. Chúng tôi muốn hỗ trợ bạn!</p>
    <p>Xin vui lòng liên hệ với <a href="mailto:{{$json["contact"]["properties"]["email"]}}">{{$json["contact"]["properties"]["email"]}}</a> để được hỗ trợ.</p>
    <p>Trân trọng,</p>
    <p>Đội ngũ {{$json["company"]}}</p>
    ```

- **Google Sheets**:
  - **Service Account Email**: Điền email của **Google Service Account** trong `Credentials` của node `Google Sheets — Read Dedup Log` và `Google Sheets — Log Alert`.
  - **File ID**: Lấy từ liên kết Google Sheets (ví dụ: `https://docs.google.com/spreadsheets/d/FILE_ID/edit` → `FILE_ID` là phần sau `/edit`).
  - **Sheet Name**:
    - `Read Dedup Log`: Điền `Alert Dedup Log`.
    - `Log Alert`: Điền `Lead Score Alerts`.

##### **B. Cấu hình Node Code (2 node)**
1. **Node `Code — Deduplicate & Enrich`**:
   - **Logic**: Kiểm tra `contact_id` trong `Alert Dedup Log` và loại bỏ leads đã cảnh báo trong 24h.
   - **Không cần chỉnh sửa** (n8n tự động xử lý).

2. **Node `Code — Merge Owner & Build Alert`**:
   - **Logic**: Xây dựng thông điệp cảnh báo dựa trên điểm số (critical/warning).
   - **Không cần chỉnh sửa** (n8n tự động phân loại).

##### **C. Cấu hình Node IF (2 node)**
- **Node `IF — Any Contacts Left?`**:
  - Nếu không có leads nào dưới ngưỡng, workflow sẽ **dừng lại** (node `Code — No New Contacts (Exit)`).
- **Node `IF — Critical or Warning?`**:
  - **Critical**: Điểm < 20 → Gửi cảnh báo cấp thiết.
  - **Warning**: Điểm < 50 → Gửi cảnh báo thông thường.

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chọn **Schedule Trigger** → Nhấn **Run Workflow** để kiểm tra.
   - Kiểm tra:
     - Slack có nhận được cảnh báo không?
     - Email có được gửi không?
     - Google Sheets có ghi log không?

2. **Bật Active**:
   - Sau khi test thành công, chuyển **Schedule Trigger** sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tăng cường cá nhân hóa email**:
   - Thêm **dynamic content** như:
     ```html
     <p>Chúng tôi thấy bạn đã tương tác với sản phẩm <strong>{{$json["contact"]["properties"]["product_interested"]}}</strong> trước đó.</p>
     <p>Hãy liên hệ với chúng tôi để được hỗ trợ!</p>
     ```
   - Lấy dữ liệu từ HubSpot trong node `Gmail — Re-Engagement Email to Contact`.

2. **Gửi báo cáo định kỳ**:
   - Thêm **node `Schedule Trigger`** mới (ví dụ: chạy hàng tuần) để gửi báo cáo tổng hợp trên Slack/Email.
   - Sử dụng node `Google Sheets — Query` để lấy dữ liệu từ `Lead Score Alerts` và gửi qua Gmail/Slack.

3. **Kết hợp với AI (LLM)**:
   - Thêm node `n8n-nodes-base.llm` để tự động **tạo nội dung email** dựa trên lịch sử tương tác của lead.
   - Ví dụ:
     ```javascript
     // Node Code trước khi gửi email
     const prompt = `Tạo một email khôi phục liên lạc thân thiện cho lead ${json["contact"]["properties"]["first_name"]} có điểm số ${json["score"]}. Dữ liệu tham khảo:
     - Lịch sử tương tác: ${json["contact"]["properties"]["last_activity"]}
     - Sản phẩm quan tâm: ${json["contact"]["properties"]["product_interested"]}
     - Email trước đó: ${json["contact"]["properties"]["email"]}`;
     ```
     Sau đó gọi API OpenAI (n8n-nodes-base.llm) để tạo nội dung.

4. **Lưu log chi tiết hơn**:
   - Thêm cột `Action Taken` vào `Lead Score Alerts` để ghi lại:
     - `Email sent` (nếu đã gửi email).
     - `Task created` (nếu đã tạo task).
     - `Owner replied` (nếu owner đã phản hồi).

5. **Cảnh báo lỗi tự động**:
   - Thêm node `n8n-nodes-base.email` để gửi **email cảnh báo admin** khi workflow lỗi (thay vì chỉ Slack).

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để các sếp:
✔ **Tự động hóa toàn bộ quy trình khắc phục lead giảm điểm**.
✔ **Tiết kiệm thời gian** và tăng hiệu suất bán hàng.
✔ **Tránh bỏ sót khách hàng** nhờ cơ chế deduplicate và cảnh báo cá nhân hóa.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test run** và điều chỉnh nếu cần.
3. **Bật Active** và để nó hoạt động 24/7!

**Nếu có vấn đề**, các sếp có thể:
- **Tạo issue** tại [GitHub n8n](https://github.com/n8n-io/n8n/issues).
- **Trao đổi** với cộng đồng n8n tại [Forum](https://community.n8n.io/).
- **Liên hệ** với tôi để hỗ trợ cấu hình chi tiết!

---
**🚀 Chúc các sếp thành công với quy trình tự động hóa CRM hiệu quả!**