---
title: "🏡 **Tự Động Hóa Quá Trình Dọn Dẹp & Sửa Chữa Di Chuyển Nhà: Từ Google Sheets → Slack → Email → AI Claude**"
description: "Workflow tự động hóa hoàn toàn quản lý nhiệm vụ dọn dẹp và sửa chữa di chuyển nhà, kết hợp Google Sheets, Slack, email và AI Claude để tối ưu hóa thời gian, giảm thiểu lỗi và cải thiện trải nghiệm cho chủ nhà. Giúp các sếp tiết kiệm 10+ giờ/tháng và giảm 90% công việc thủ công."
slug: "tieu-dong-hoa-qua-trinh-don-dep-di-chuyen-nha"
tags: [n8n, automation, no-code, google-sheets, slack, email, ai-claude, property-management]
keywords: [tự động hóa di chuyển nhà, quản lý dọn dẹp sửa chữa, n8n workflow, ai Claude, google sheets tự động, slack tự động hóa, email tự động hóa]
---

# 🚀 **Tự Động Hóa Quá Trình Dọn Dẹp & Sửa Chữa Di Chuyển Nhà: Từ Google Sheets → Slack → Email → AI Claude**

### **Nỗi Đau Của Các Sếp Trong Quản Lý Di Chuyển Nhà**
Quá trình di chuyển nhà là một trong những giai đoạn phức tạp nhất trong quản lý bất động sản. Các sếp thường phải:
- **Lập danh sách nhiệm vụ dọn dẹp và sửa chữa** cho từng căn hộ một cách thủ công trên Google Sheets, dễ bị lỗi hoặc quên.
- **Gửi yêu cầu đến các nhà thầu** (dọn dẹp, sửa chữa) qua email hoặc Slack, nhưng không có hệ thống theo dõi tự động, dẫn đến trễ hạn hoặc thiếu thông tin.
- **Phản hồi chậm chạp** khi nhà thầu không hoàn thành nhiệm vụ kịp thời, gây mất tin tưởng của chủ nhà.
- **Không có báo cáo tổng hợp** về tiến độ, khiến việc đánh giá hiệu suất trở nên khó khăn.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa toàn bộ quy trình** từ nhận yêu cầu đến theo dõi hoàn thành.
✅ **Sử dụng AI Claude** để phân loại nhiệm vụ và đề xuất hành động theo dõi.
✅ **Kết nối Google Sheets, Slack và Email** để thông báo và theo dõi thực thời.
✅ **Gửi báo cáo tự động** về tiến độ cho quản lý và chủ nhà.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 10+ giờ/tháng** cho việc lập danh sách và theo dõi nhiệm vụ.
- **Giảm 90% lỗi thủ công** nhờ tự động hóa và AI phân loại.
- **Cải thiện trải nghiệm chủ nhà** với phản hồi nhanh chóng và thông tin minh bạch.
- **Theo dõi tiến độ thực thời** qua Google Sheets và Slack.
- **Báo cáo tự động** về nhiệm vụ hoàn thành và những nhiệm vụ cần theo dõi.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để lưu trữ thông tin chủ nhà, căn hộ và nhiệm vụ).
2. **Credentials OAuth 2.0 cho Google Sheets** (cài đặt trong n8n).
3. **Tài khoản Slack** (để thông báo và theo dõi nhiệm vụ).
4. **Tài khoản Gmail** (để gửi email đến nhà thầu).
5. **API Key của Claude (Anthropic)** (để sử dụng AI phân loại và đề xuất hành động).
6. **Webhook URL** (để nhà thầu gửi xác nhận hoàn thành nhiệm vụ).
7. **Dữ liệu mẫu** (các bản ghi trong Google Sheets về chủ nhà, căn hộ và nhiệm vụ cần thực hiện).
:::

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/12429](https://n8n.io/workflows/12429) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** và chọn **Import Workflow** → Dán JSON hoặc tải file JSON.
- **Không cần chỉnh sửa cấu trúc**, chỉ cần điền thông tin credentials và tham số.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **14 node** quan trọng, các sếp cần chú ý đến:

##### **🔹 Node "Get Tenant & Property Info" (Google Sheets)**
- **Chọn credentials**: `googleSheetsOAuth2Api` (đã cài đặt trước).
- **Điền tham số**:
  - **Sheet Name**: Tên bảng chứa dữ liệu chủ nhà và căn hộ (ví dụ: `Tenant_Info`).
  - **Query**: Câu truy vấn để lấy dữ liệu (ví dụ: `SELECT * FROM Sheet1 WHERE status = 'Pending'`).
  - **Range**: Phạm vi dữ liệu (ví dụ: `Sheet1!A1:Z100`).

##### **🔹 Node "Generate Move-Out Instructions" (Agent AI)**
- **Điền Prompt**: Tùy chỉnh câu lệnh AI để sinh hướng dẫn dọn dẹp/sửa chữa phù hợp với loại căn hộ (ví dụ: *"Tạo danh sách chi tiết các bước dọn dẹp và sửa chữa cho căn hộ loại [Loại Căn Hộ]"*).
- **Kết nối với Node "Anthropic Chat Model"**: Chọn model `claude-sonnet-4-5-20250929`.

##### **🔹 Node "Send Email to Vendors" (Gmail)**
- **Chọn credentials**: `gmailOAuth2Api` (cài đặt trước).
- **Điền thông tin**:
  - **To**: Email của nhà thầu (ví dụ: `vendor@example.com`).
  - **Subject**: Tiêu đề email (ví dụ: *"Yêu cầu dọn dẹp căn hộ [Mã Căn Hộ]"*).
  - **Body**: Nội dung email tự động sinh từ AI (kết nối với node trước).

##### **🔹 Node "Notify Property Management Team" (Slack)**
- **Chọn credentials**: `slackWebhook` (cài đặt trong Slack).
- **Điền thông tin**:
  - **Channel**: Tên kênh Slack để thông báo (ví dụ: `#property-management`).
  - **Message**: Nội dung thông báo (ví dụ: *"Nhiệm vụ [Tên Nhiệm Vụ] đã được gửi đến nhà thầu"*).

##### **🔹 Node "Vendor Confirmation Webhook" (Webhook)**
- **Cấu hình Webhook**:
  - **Path**: `vendor-confirmation` (không đổi).
  - **HTTP Method**: `POST`.
  - **URL**: Địa chỉ Webhook của nhà thầu (cần đăng ký trước).
- **Lưu ý**: Nhà thầu phải gửi dữ liệu xác nhận dưới dạng JSON đến URL này khi hoàn thành nhiệm vụ.

##### **🔹 Node "Check Task Delays" (If)**
- **Điều kiện kiểm tra**: Nếu nhiệm vụ quá hạn (`delay > 24h`), chuyển sang node "Suggest Follow-Up Actions".

##### **🔹 Node "Log Task Completion" (Google Sheets)**
- **Chọn credentials**: `googleSheetsOAuth2Api`.
- **Điền tham số**:
  - **Operation**: `appendOrUpdate` (cập nhật hoặc thêm mới).
  - **Range**: Phần dữ liệu cần cập nhật (ví dụ: `Sheet1!D1:D100`).

##### **🔹 Node "Suggest Follow-Up Actions" (Agent AI)**
- **Điền Prompt**: Tùy chỉnh câu lệnh AI để đề xuất hành động theo dõi (ví dụ: *"Đề xuất các bước xử lý cho nhiệm vụ trễ hạn [Tên Nhiệm Vụ]"*).

##### **🔹 Node "Send Follow-Up Alert" (Slack)**
- **Chọn credentials**: `slackWebhook`.
- **Điền thông tin**:
  - **Channel**: `#property-alerts`.
  - **Message**: Thông báo cảnh báo trễ hạn (ví dụ: *"Nhiệm vụ [Tên] đã quá hạn 24h, cần xử lý!"*).

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chọn node **Schedule Trigger** và chạy thử với một bản ghi mẫu trong Google Sheets.
   - Kiểm tra email, Slack và Google Sheets để đảm bảo thông tin được gửi và cập nhật đúng.
2. **Bật Active**:
   - Sau khi test thành công, chuyển trạng thái workflow sang **Active**.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**CÁC Ý TƯỞNG MỞ RỘNG**]
1. **Kết nối với Telegram**:
   - Thêm node Telegram để thông báo cho quản lý khi có nhiệm vụ mới hoặc trễ hạn.
2. **Lưu Log Tự Động**:
   - Sử dụng node **StickyNote** để lưu lịch sử thông báo và hành động đã thực hiện.
3. **Báo Cáo Định Kỳ**:
   - Thêm node **Schedule Trigger** chạy hàng tuần để gửi báo cáo tổng hợp về tiến độ cho quản lý.
4. **Tích Hợp với CRM**:
   - Nếu sử dụng CRM như HubSpot hoặc Zoho, kết nối node Google Sheets với CRM để cập nhật thông tin chủ nhà tự động.
5. **Tùy Chỉnh AI**:
   - Đào tạo model Claude với dữ liệu cụ thể của công ty để AI sinh hướng dẫn và đề xuất hành động chính xác hơn.
:::

---
### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp quản lý bất động sản muốn **tự động hóa toàn bộ quy trình di chuyển nhà**, từ lập danh sách nhiệm vụ đến theo dõi và báo cáo. Với sự kết hợp của **Google Sheets, Slack, Email và AI Claude**, các sếp sẽ:
✔ **Tiết kiệm thời gian** và giảm thiểu lỗi thủ công.
✔ **Cải thiện trải nghiệm chủ nhà** với phản hồi nhanh chóng.
✔ **Theo dõi tiến độ thực thời** và xử lý kịp thời những nhiệm vụ trễ hạn.

**Hãy áp dụng ngay workflow này và chuyển từ quản lý thủ công sang tự động hóa hoàn toàn!** 🚀

---
:::note[**LƯU Ý CUỐI CUNG**]
- **Đăng ký VPS để chạy 24/7**:
  👉 [VPS TinoHost (Mã giảm giá: **VPSN8N**)](https://tino.vn/vps-n8n?affid=388) (giảm tới 39%)
  👉 [VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
- **Cập nhật thường xuyên**: Workflow này sử dụng API của Claude, đảm bảo đã cài đặt phiên bản mới nhất của `@n8n/n8n-nodes-langchain`.
:::