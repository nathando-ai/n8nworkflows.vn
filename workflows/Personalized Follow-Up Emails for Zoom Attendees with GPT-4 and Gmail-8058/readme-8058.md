---
title: "🚀 Tự Động Hóa Email Theo Dõi Cá Nhân Hóa Cho Tham Gia Zoom Với GPT-4 & Gmail (Không Cần Code)"
description: "Workflow tự động gửi email theo dõi cá nhân hóa cho tất cả người tham gia Zoom sau buổi họp, sử dụng trí tuệ nhân tạo GPT-4 để tạo nội dung độc đáo. Giảm thời gian làm thủ công 90%, tăng tỷ lệ tương tác 40-60%."
slug: "tieu-dong-hoa-email-theo-doi-zoom-gpt4-gmail"
tags: [n8n, automation, lead-nurturing, gpt-4, gmail, zoom, no-code]
keywords: [tự động hóa email zoom, gpt-4 tự động hóa, email theo dõi cá nhân hóa, n8n workflow zoom, gửi email tự động sau zoom]
---

# 🚀 Tự Động Hóa Email Theo Dõi Cá Nhân Hóa Cho Tham Gia Zoom Với GPT-4 & Gmail

## 💡 Bạn đang gặp vấn đề gì?
Sau mỗi buổi họp Zoom, các sếp thường phải:
- **Làm thủ công** ghi chép thông tin tham gia của từng người
- **Tạo email theo dõi** riêng cho từng khách hàng/đối tác
- **Đảm bảo nội dung cá nhân hóa** để tăng tỷ lệ tương tác
- **Quên gửi email** hoặc gửi muộn vì quá tải công việc

Kết quả? **Thời gian lãng phí, tỷ lệ chuyển đổi thấp**, và mất cơ hội kết nối sâu với khách hàng.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ Nhận danh sách tham gia từ Zoom
✅ Sử dụng GPT-4 tạo email theo dõi **cá nhân hóa 100%**
✅ Gửi email qua Gmail **một cách tự động**
✅ **Không cần viết code** - chỉ cần cấu hình

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** và không bị gián đoạn, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) thay vì dùng phiên bản miễn phí trên cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) với **mã giảm giá VPSN8N** (giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) - **Đảm bảo tốc độ cao, không lag**
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** so với làm thủ công
- **Tỷ lệ tương tác tăng 40-60%** nhờ nội dung cá nhân hóa
- **Không quên gửi email** - hoạt động tự động 24/7
- **Nội dung chuyên nghiệp** do GPT-4 tạo ra, không cần viết
- **Dễ dàng mở rộng** cho nhiều buổi họp khác nhau
:::

---

### 🔧 Yêu cầu cần thiết
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Zoom** với quyền **bật webhook**
2. **API Key OpenAI** (để sử dụng GPT-4)
3. **Tài khoản Gmail** (đã kích hoạt OAuth 2.0)
4. **Workflow Webhook URL** (sẽ được tạo khi import)

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow bằng cách:
- **Tải file JSON** từ [n8n.io/workflows/8058](https://n8n.io/workflows/8058) và import vào **n8n Editor**
- **Copy/paste** JSON từ file vào **Import Workflow** trong n8n

:::note[Lưu ý]
- **Không cần chỉnh sửa code** trong node "Normalize Participants" - nó đã được tối ưu sẵn.
- **Không cần cài thêm node** - workflow chỉ sử dụng 4 node cơ bản.
:::

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

##### **A. Cấu hình Zoom Webhook**
1. **Mở Zoom App** → **Settings** → **Advanced** → **Webhooks**
2. **Tạo mới 1 webhook** với:
   - **Event:** `meeting.ended`
   - **URL:** **Workflow Webhook URL** (copy từ n8n)
   - **Payload:** Chọn **Include participant details** (đảm bảo có email/name)
3. **Kiểm tra** bằng cách tổ chức 1 buổi họp thử và xem liệu webhook có gửi dữ liệu không.

##### **B. Cấu hình Gmail**
1. Trong n8n, vào **Gmail Node** → **Add Credential**
2. **Chọn OAuth 2.0** và đăng nhập tài khoản Gmail
3. **Chọn tài khoản** muốn gửi email từ
4. **Kiểm tra** bằng cách gửi 1 email thử (dùng dữ liệu mẫu)

##### **C. Cấu hình OpenAI (GPT-4)**
1. Vào **OpenAI Node** → **Add Credential**
2. **Paste API Key** từ [OpenAI Platform](https://platform.openai.com/account/api-keys)
3. **Chọn model:** `gpt-4` (đảm bảo tài khoản có đủ credit)
4. **Test run** với 1 prompt mẫu:
   ```json
   {
     "role": "system",
     "content": "You are a professional email writer. Draft a personalized follow-up email for a Zoom meeting attendee. Include their name, the meeting topic, and 2-3 key takeaways from the discussion. Keep it concise and engaging."
   }
   ```

##### **D. Cấu hình Node "Normalize Participants"**
- **Không cần chỉnh sửa** - node này tự động xử lý dữ liệu từ Zoom thành định dạng phù hợp cho GPT-4.
- **Nếu cần debug**, các sếp có thể mở **StickyNote Node** để xem dữ liệu đầu vào.

#### 3. Kích hoạt ⚡️
1. **Test Run** với dữ liệu mẫu từ Zoom (nếu có)
2. **Bật Active** workflow
3. **Kiểm tra email** trong Gmail để xác nhận đã gửi thành công

---

### ✍️ Mẹo & gợi ý nâng cao
1. **Thêm Slack/Telegram Notification**
   - Sử dụng **Slack Node** hoặc **Telegram Bot Node** để thông báo khi email được gửi thành công/lỗi.
   - Ví dụ: *"Email follow-up đã được gửi cho [Tên Khách Hàng] sau buổi họp [Tên Buổi Hợp]"*

2. **Lưu Log Dữ liệu**
   - Thêm **Google Sheets Node** để lưu lịch sử email đã gửi (email, tên người nhận, nội dung, thời gian).
   - Cách cấu hình:
     ```json
     {
       "operation": "createRow",
       "resource": "sheets",
       "sheetName": "Zoom_FollowUp_Log",
       "data": {
         "Email": "{{$node["Send Email"].json["email"]}}",
         "Name": "{{$node["Normalize Participants"].json["name"]}}",
         "Meeting Topic": "{{$node["Zoom Meeting Webhook"].json["topic"]}}",
         "Sent At": "{{$node["Send Email"].json["sentAt"]}}"
       }
     }
     ```

3. **Tự động Gửi Báo Cáo Hàng Tuần**
   - Sử dụng **Set Interval Node** để gửi báo cáo tổng hợp về số lượng email đã gửi, tỷ lệ mở, phản hồi.
   - Ví dụ: *"Tổng cộng 50 email đã được gửi trong tuần qua, tỷ lệ mở trung bình 35%."*

4. **Cá nhân hóa thêm với CRM**
   - Nếu sử dụng **HubSpot** hoặc **Salesforce**, thêm **CRM Node** để cập nhật trạng thái khách hàng sau khi gửi email.

---

### 📌 Kết luận
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào việc **kết nối sâu** với khách hàng thay vì làm thủ công. Với **GPT-4**, email không chỉ được gửi mà còn **cá nhân hóa cao độ**, tăng tỷ lệ chuyển đổi đáng kể.

**Bắt đầu ngay!**
1. Import workflow
2. Cấu hình Zoom, Gmail, OpenAI
3. **Bật Active** và để nó làm việc tự động

**Nếu gặp vấn đề**, hãy liên hệ với tác giả David Olusola qua [david@daexai.com](mailto:david@daexai.com) để hỗ trợ tối ưu hóa.

---