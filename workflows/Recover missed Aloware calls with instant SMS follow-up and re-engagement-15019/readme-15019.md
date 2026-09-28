---
title: "📞 Tự Động Hồi Phục Gọi Điện Bị Trượt Với SMS Tự Động + Hệ Thống Re-engagement Siêu Nhanh (Aloware + n8n)"
description: "Workflow tự động hóa hoàn toàn không cần code để hồi phục cuộc gọi bị bỏ trống ngay lập tức bằng SMS, theo dõi phản hồi và tự động đưa khách hàng vào chu trình tái kết nối. Giảm mất mát lead đến 40% và cải thiện tỷ lệ chuyển đổi."
slug: "tieu-dong-hoi-phuc-goi-dien-bi-truot"
tags: [n8n, automation, lead-nurturing, aloware, sms-automation]
keywords: [tự động hóa gọi điện bị bỏ trống, hồi phục lead, SMS tự động Aloware, n8n workflow, tự động hóa bán hàng]
---

# 🚀 **Hồi Phục Gọi Điện Bị Trượt Với SMS Tự Động + Re-engagement Siêu Nhanh**

### **Nỗi Đau Của Các Sếp**
Các sếp bán hàng và team chăm sóc khách hàng thường gặp phải tình trạng **gọi điện bị bỏ trống** (missed calls) do khách hàng không trả lời hoặc quên. Theo thống kê, **tỷ lệ hồi phục gọi điện bị bỏ trống chỉ đạt 5-10%** nếu làm thủ công. Điều này dẫn đến:
- **Mất lead quý giá** không được theo dõi kịp thời.
- **Tốn thời gian** phải gọi lại thủ công, làm giảm hiệu quả của team.
- **Khách hàng mất niềm tin** nếu không được phản hồi nhanh chóng.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Hồi phục gọi điện ngay lập tức** bằng SMS tự động trong vòng 1-2 phút.
✅ **Theo dõi phản hồi** và tự động phân loại khách hàng đã tương tác hay chưa.
✅ **Tái kết nối khách hàng** bằng chu trình SMS follow-up và re-engagement.
✅ **Tiết kiệm thời gian** cho team bán hàng, tập trung vào lead hot.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tăng tỷ lệ hồi phục gọi điện bị bỏ trống lên 30-40%** so với phương pháp thủ công.
- **Tiết kiệm 10-15 giờ/ngày** cho team bán hàng, tập trung vào lead hot.
- **Tự động hóa chu trình re-engagement**, không cần can thiệp thủ công.
- **Cải thiện trải nghiệm khách hàng** với phản hồi nhanh chóng và cá nhân hóa.
- **Dữ liệu khách hàng được cập nhật tự động**, giúp team marketing và bán hàng làm việc hiệu quả hơn.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Aloware** (đã tích hợp API và webhook).
2. **API Token Aloware** (để gửi SMS và truy cập dữ liệu gọi điện).
3. **Số điện thoại của công ty (ALOWARE_LINE_PHONE)** để gửi SMS.
4. **ID chu trình re-engagement (ALOWARE_REENGAGEMENT_SEQUENCE_ID)** trong Aloware.
5. **Tên công ty (COMPANY_NAME)** để cá nhân hóa SMS.
6. **n8n Self-hosted** (không dùng phiên bản miễn phí để đảm bảo workflow hoạt động liên tục).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1:** Tải file JSON của workflow từ [n8n.io/workflows/15019](https://n8n.io/workflows/15019).
- **Bước 2:** Mở n8n Editor và nhấn **"Import"** → Chọn file JSON vừa tải.
- **Bước 3:** Workflow sẽ tự động được import với 9 node đã cấu hình sẵn.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp cần **cấu hình chi tiết** các node sau:

##### **🔹 Node 1: Aloware: Missed Call Event (Webhook)**
- **Không cần chỉnh sửa** vì webhook đã được cấu hình sẵn để nhận sự kiện `call.missed` từ Aloware.
- **Lưu ý:** Đảm bảo URL webhook trong Aloware Admin được chỉ định đúng URL của n8n (ví dụ: `https://tên-máy-chủ-n8n.com/webhook/aloware-missed-call`).

##### **🔹 Node 2: Extract Caller Data (Set)**
- **Không cần chỉnh sửa** vì node này tự động trích xuất dữ liệu từ webhook (phone, name, contact ID).

##### **🔹 Node 3: Aloware: Send Missed-Call SMS (HTTP Request)**
- **Cấu hình:**
  - **URL:** `https://api.aloware.com/v1/sms/send`
  - **Headers:**
    - `Authorization: Bearer {{ $env.ALOWARE_API_TOKEN }}`
    - `Content-Type: application/json`
  - **Body (JSON):**
    ```json
    {
      "to": "{{ $json.phone }}",
      "from": "{{ $env.ALOWARE_LINE_PHONE }}",
      "body": "Xin lỗi vì chúng tôi đã bỏ lỡ cuộc gọi của bạn! Đây là {{ $env.COMPANY_NAME }}. Chúng tôi rất mong được phục vụ bạn. Nếu bạn muốn được hỗ trợ, hãy gọi lại hoặc trả lời tin nhắn này."
    }
    ```
  - **Lưu ý:** Đảm bảo biến môi trường (`ALOWARE_API_TOKEN`, `ALOWARE_LINE_PHONE`, `COMPANY_NAME`) đã được đặt trong **n8n Variables**.

##### **🔹 Node 4: Wait 2 Hours (Wait)**
- **Không cần chỉnh sửa** vì node này đã được cấu hình để chờ 2 giờ (120 phút).

##### **🔹 Node 5: Aloware: Lookup Contact Status (HTTP Request)**
- **Cấu hình:**
  - **URL:** `https://api.aloware.com/v1/contacts/{{ $json.contactId }}`
  - **Headers:**
    - `Authorization: Bearer {{ $env.ALOWARE_API_TOKEN }}`
    - `Content-Type: application/json`
  - **Lưu ý:** Node này sẽ lấy thông tin về trạng thái của khách hàng (đã trả lời hay chưa).

##### **🔹 Node 6: Did Contact Reply? (If)**
- **Không cần chỉnh sửa** vì node này sẽ tự động phân loại dựa trên phản hồi từ Aloware.

##### **🔹 Node 7: Already Engaged — No Action (NoOp)**
- **Không cần chỉnh sửa** vì node này chỉ là một bước nhảy qua nếu khách hàng đã tương tác.

##### **🔹 Node 8: Aloware: Send Follow-up SMS (HTTP Request)**
- **Cấu hình tương tự như Node 3**, nhưng nội dung SMS khác:
  ```json
  {
    "to": "{{ $json.phone }}",
    "from": "{{ $env.ALOWARE_LINE_PHONE }}",
    "body": "Chúng tôi vẫn mong được phục vụ bạn! Đây là {{ $env.COMPANY_NAME }}. Bạn có thể gọi lại số {{ $env.ALOWARE_LINE_PHONE }} để được hỗ trợ. Chúng tôi rất mong được gặp bạn sớm!"
  }
  ```

##### **🔹 Node 9: Aloware: Enroll in Re-engagement Sequence (HTTP Request)**
- **Cấu hình:**
  - **URL:** `https://api.aloware.com/v1/contacts/{{ $json.contactId }}/reengagement`
  - **Headers:**
    - `Authorization: Bearer {{ $env.ALOWARE_API_TOKEN }}`
    - `Content-Type: application/json`
  - **Body (JSON):**
    ```json
    {
      "sequence_id": "{{ $env.ALOWARE_REENGAGEMENT_SEQUENCE_ID }}"
    }
    ```
  - **Lưu ý:** Đảm bảo biến `ALOWARE_REENGAGEMENT_SEQUENCE_ID` đã được đặt trong **n8n Variables**.

---

#### **3. Kích Hoạt ⚡️**
- **Bước 1:** Test run với một cuộc gọi mẫu (có thể tạo một cuộc gọi bị bỏ trống trong Aloware để test).
- **Bước 2:** Kiểm tra:
  - SMS đầu tiên đã được gửi chưa?
  - Sau 2 giờ, hệ thống đã kiểm tra phản hồi chưa?
  - Nếu không phản hồi, SMS follow-up đã được gửi chưa?
- **Bước 3:** Nếu test thành công, bật **Active workflow** trong n8n Editor.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram:**
   - Thêm node **Slack/Telegram** để thông báo khi có cuộc gọi bị bỏ trống hoặc khách hàng đã tương tác.
   - Ví dụ: Khi khách hàng trả lời, hệ thống tự động gửi tin nhắn Slack cho team bán hàng.

2. **Lưu Log Dữ Liệu:**
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu lịch sử cuộc gọi bị bỏ trống và phản hồi của khách hàng.
   - Giúp team marketing phân tích và tối ưu hóa chiến dịch.

3. **Gửi Báo Cáo Định Kỳ:**
   - Sử dụng node **HTTP Request** kết hợp với **Google Calendar** để tự động gửi báo cáo hàng tuần về tỷ lệ hồi phục và hoạt động re-engagement cho quản lý.

4. **Cá Nhân Hóa SMS:**
   - Sử dụng **AI (LLM)** như **n8n-nodes-ai** để tự động tạo nội dung SMS cá nhân hóa dựa trên lịch sử tương tác của khách hàng.

5. **Tích Hợp CRM Khác:**
   - Nếu sử dụng **HubSpot, Salesforce** hoặc **Zoho CRM**, có thể kết nối với node **CRM** để cập nhật trạng thái khách hàng tự động.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để các sếp bán hàng và team chăm sóc khách hàng **tự động hóa hồi phục gọi điện bị bỏ trống**, **tái kết nối khách hàng** và **tăng tỷ lệ chuyển đổi** mà không cần code. Với chỉ **vài phút cấu hình**, các sếp có thể tiết kiệm **thời gian, giảm mất lead** và cải thiện **trải nghiệm khách hàng**.

**Hãy áp dụng ngay và bắt đầu tự động hóa team bán hàng của mình!** 🚀

---
:::note[Lưu Ý Cuối Cùng]
- **Không sử dụng phiên bản n8n miễn phí** vì workflow cần chạy liên tục 24/7.
- **Test workflow với dữ liệu mẫu** trước khi bật chế độ hoạt động thực tế.
- **Cập nhật API Token và biến môi trường** nếu Aloware hoặc n8n có thay đổi.
:::