---
title: "🎯 Tự Động Gắn Thẻ Sự Kiện Eventbrite Trên KlickTipp (Không Cần Code)"
description: "Hướng dẫn tự động phân loại và gắn thẻ người tham dự/sự kiện bỏ lỡ từ Eventbrite sang KlickTipp, tiết kiệm thời gian quản lý danh sách tham dự và tối ưu hóa chiến dịch marketing. Hoạt động 24/7 với độ chính xác 100%."
slug: "tieu-dong-gan-the-eventbrite-klicktipp"
tags: [n8n, automation, eventbrite, klicktipp, marketing-automation, no-code]
keywords: [tự động hóa eventbrite, gắn thẻ sự kiện, klicktipp automation, tự động phân loại tham dự, marketing automation, workflow n8n]
---

# 🚀 **Tự Động Gắn Thẻ Sự Kiện Eventbrite Trên KlickTipp (Không Cần Code)**

### **Giải quyết vấn đề gì?**
Các sếp tổ chức sự kiện, marketer hoặc người dùng KlickTipp thường phải **làm thủ công** việc kiểm tra danh sách tham dự từ Eventbrite và gắn thẻ cho từng người trong KlickTipp. Điều này **tốn thời gian**, dễ xảy ra lỗi, và không thể hoạt động liên tục. **Workflow này tự động hóa toàn bộ quy trình** bằng cách:
✅ **Lấy danh sách tham dự từ Eventbrite** (tự động cập nhật mỗi 15 phút).
✅ **Phân loại người tham dự vs. bỏ lỡ** dựa trên trạng thái `checked_in`.
✅ **Gắn thẻ tự động** vào KlickTipp với hai thẻ:
   - `Eventbrite | Participated` (đã tham dự).
   - `Eventbrite | Not participated` (bỏ lỡ).
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần kiểm tra danh sách thủ công hàng ngày.
- **Chính xác 100%**: Dựa trên dữ liệu thực tế từ Eventbrite (quét barcode hoặc app tổ chức).
- **Tối ưu hóa marketing**: Gắn thẻ tự động cho phân khúc `Participated` và `Not participated` để chạy chiến dịch cá nhân hóa.
- **Hoạt động liên tục**: Cập nhật dữ liệu mỗi 15 phút (hoặc thời gian tự chọn).
- **Tích hợp GDPR**: KlickTipp hỗ trợ tuân thủ quy định bảo mật dữ liệu.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Eventbrite** với **OAuth2 credentials** (đã cấp quyền đọc danh sách tham dự).
2. **Tài khoản KlickTipp** với **API access** (tên người dùng và mật khẩu).
3. **Hai thẻ đã cấu hình trong KlickTipp**:
   - `Eventbrite | Participated` (đã tham dự).
   - `Eventbrite | Not participated` (bỏ lỡ).
4. **Sự kiện Eventbrite** đã được tạo và có **ID sự kiện** (sẽ cần trong bước cấu hình).

---
:::note[LƯU Ý QUAN TRỌNG]
- **Dữ liệu gốc phải tồn tại trong KlickTipp**: Các sếp cần **đã đồng bộ danh sách đăng ký từ Eventbrite sang KlickTipp** trước bằng workflow ["Subscribe Eventbrite orders to KlickTipp"](https://n8n.io/workflows/10027).
- **Eventbrite phải quét tham dự**: Để workflow chính xác, các sếp cần sử dụng **Eventbrite Organizer App** hoặc **quét barcode** để ghi nhận người tham dự.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và mở **n8n Editor**.
2. Nhấn **Import** và chọn file JSON (hoặc paste JSON từ [đây](https://n8n.io/workflows/10028)).
3. Chọn **Create Workflow** để tạo mới.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **6 node chính**, các sếp cần cấu hình kỹ lưỡng như sau:

##### **A. Node "Trigger every 15min" (n8n-nodes-base.scheduleTrigger)**
- **Lưu ý**: Thời gian mặc định là **15 phút**, các sếp có thể điều chỉnh:
  - **Thời gian thực tế**: Đặt **5 phút** trong giờ sự kiện để cập nhật nhanh.
  - **Sau sự kiện**: Đặt **1 giờ/lần** để kiểm tra cuối cùng.
- **Cách chỉnh**:
  - Nhấn vào node → Tab **Settings** → Chọn **Every 5 minutes** (hoặc thời gian khác).

##### **B. Node "List Eventbrite attendees from event" (n8n-nodes-base.httpRequest)**
- **Yêu cầu**:
  - **Credentials**: Chọn `eventbriteOAuth2Api` (đã cấu hình OAuth2 trong n8n).
  - **URL**: Cần thay đổi từ mẫu `/events/{event_id}/attendees/` thành **ID sự kiện cụ thể** của sếp.
    - Ví dụ: `https://www.eventbriteapi.com/v3/events/{YOUR_EVENT_ID}/attendees/` (thay `{YOUR_EVENT_ID}` bằng ID sự kiện của sếp).
  - **Headers**:
    - `Authorization`: `Bearer {YOUR_OAUTH2_TOKEN}` (lấy từ OAuth2 credentials).
    - `Content-Type`: `application/json`.
- **Cách lấy ID sự kiện**:
  1. Mở sự kiện trên Eventbrite → URL sẽ có dạng: `https://www.eventbrite.com/e/{YOUR_EVENT_ID}-...` → Copy `{YOUR_EVENT_ID}`.

##### **C. Node "Split attendee list" (n8n-nodes-base.splitOut)**
- **Lưu ý**: Node này **chia danh sách tham dự thành hai nhóm**:
  - Nhóm 1: `checked_in = true` (đã tham dự).
  - Nhóm 2: `checked_in = false` (bỏ lỡ).
- **Không cần chỉnh sửa**, workflow tự động phân loại dựa trên trường `checked_in`.

##### **D. Node "Tag contact for attendance" & "Tag contact for non attendance" (n8n-nodes-klicktipp.klicktipp)**
- **Yêu cầu**:
  - **Credentials**: Chọn `klickTippApi` (đã cấu hình tên người dùng/mật khẩu).
  - **Resource**: `contact-tagging` (không cần chỉnh).
  - **Tham số quan trọng**:
    - **Tag ID**: Các sếp cần **mapping Tag ID** từ KlickTipp vào node này.
      - Ví dụ:
        - Node `Tag contact for attendance` → Chọn thẻ `Eventbrite | Participated`.
        - Node `Tag contact for non attendance` → Chọn thẻ `Eventbrite | Not participated`.
    - **Cách lấy Tag ID**:
      1. Mở KlickTipp → **Tags** → Chọn thẻ cần dùng → ID sẽ hiển thị trong URL hoặc tab **Settings**.
      2. Điền ID vào trường `tagId` trong node tương ứng.

##### **E. Node "Attendance check" (n8n-nodes-base.switch)**
- **Lưu ý**: Node này **kiểm tra giá trị `checked_in`** và phân luồng sang node gắn thẻ tương ứng.
- **Không cần chỉnh**, workflow tự động xử lý.

---

#### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Nhấn **Execute Workflow** để chạy thử với dữ liệu mẫu.
   - Kiểm tra **log** để đảm bảo:
     - Danh sách tham dự được lấy từ Eventbrite.
     - Thẻ được gắn đúng vào KlickTipp.
2. **Bật Active workflow**:
   - Nhấn **Active** ở góc trên bên phải.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH TIẾP CẬN THÊM]
1. **Chỉnh thời gian sync theo sự kiện**:
   - Trong giờ sự kiện: **5 phút/lần** để cập nhật nhanh.
   - Sau sự kiện: **1 giờ/lần** để kiểm tra cuối cùng.

2. **Xử lý nhiều sự kiện cùng lúc**:
   - **Duplicate workflow** và thay đổi **Event ID** trong node `httpRequest`.
   - Sử dụng **node `Set`** để lưu trữ nhiều Event ID và **loop** qua chúng.

3. **Gắn thẻ thêm thông tin**:
   - Thêm **thẻ cho loại vé** (VIP, Early Bird) hoặc **trạng thái hoàn tiền**.
   - Ví dụ: Nếu Eventbrite có trường `ticket_class`, thêm node `Set` để gắn thẻ `VIP` cho người mua vé VIP.

4. **Tích hợp Slack/Telegram báo cáo**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** sau node `Tag contact` để thông báo:
     - `X người đã tham dự sự kiện Y`.
     - `X người bỏ lỡ sự kiện Y`.

5. **Tạo báo cáo tự động**:
   - Sử dụng **node `Google Sheets`** hoặc **KlickTipp Reports** để lưu trữ dữ liệu thống kê:
     - Số lượng tham dự vs. bỏ lỡ.
     - Tỷ lệ chuyển đổi từ đăng ký sang tham dự.
   - Ví dụ: Báo cáo hàng tuần tự động gửi qua email.

6. **Chiến dịch marketing tự động hóa**:
   - **Cho người tham dự (`Participated`)**:
     - Gửi email cảm ơn + link download tài liệu sự kiện.
     - Mời tham gia sự kiện tương lai.
   - **Cho người bỏ lỡ (`Not participated`)**:
     - Gửi replay video hoặc link đăng ký lại.
     - Đề xuất nội dung liên quan (webinar, blog).

7. **Kết hợp với workflow hoàn tiền**:
   - Nếu Eventbrite có trường `refunded`, thêm node **check `refunded`** và gắn thẻ `Eventbrite | Refunded` để theo dõi người hoàn tiền.
   - Tích hợp với workflow hoàn tiền để **không gửi email mời lại** cho người đã hoàn tiền.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc quản lý danh sách tham dự thủ công, đồng thời **tối ưu hóa chiến dịch marketing** bằng cách phân khúc khách hàng chính xác. **Bắt đầu tự động hóa ngay** và tập trung vào việc **tăng doanh thu** và **cải thiện trải nghiệm khách hàng**!

:::success[HÀNH ĐỘNG NGÀY HÔM NAY]
1. **Cài đặt n8n trên VPS** (nếu chưa có).
2. **Import workflow** và cấu hình **Event ID** + **Tag ID**.
3. **Test run** và bật **Active**.
4. **Tích hợp Slack/Telegram** để theo dõi kết quả.
5. **Tạo báo cáo tự động** để phân tích hiệu quả sự kiện.
:::

---
**🚀 Cần hỗ trợ?** Đăng ký [VPS n8n](https://tino.vn/vps-n8n?affid=388) với mã giảm giá **VPSN8N** và liên hệ với team KlickTipp để tối ưu hóa workflow!