---
title: "🚨 Tự Động Hóa Cảnh Báo Cứu Hỏa Thực Tế Sang Tin Nhắn iMessage Với Tóm Tắt AI - Giúp Bạn Không Bỏ Lỡ Mọi Thông Tin Cứu Hỏa"
description: "Workflow này tự động lấy cảnh báo khẩn cấp từ PulsePoint, tóm tắt bằng AI và gửi tin nhắn iMessage thực thời đến điện thoại cá nhân của bạn. Giúp bạn luôn cập nhật nhanh chóng về các sự kiện khẩn cấp trong khu vực, tiết kiệm thời gian và giảm thiểu lo lắng."
slug: "tu-dong-hoa-can-bao-cuu-hoa-sang-iMessage-voi-AI"
tags: [n8n, automation, no-code, AI, PulsePoint, iMessage, OpenAI, emergency-alerts]
keywords: [n8n workflow, tự động hóa cảnh báo khẩn cấp, PulsePoint API, OpenAI tóm tắt văn bản, gửi tin nhắn iMessage tự động, AI cho công việc cá nhân]
---

# 🚨 **Tự Động Hóa Cảnh Báo Cứu Hỏa Thực Tế Sang Tin Nhắn iMessage Với Tóm Tắt AI**

### **Bạn đã bao giờ lo lắng khi không kịp thời cập nhật về các sự kiện khẩn cấp xung quanh mình?**
Cảnh báo từ PulsePoint thường rất chi tiết và phức tạp, khiến bạn phải mất thời gian để hiểu rõ nội dung. Với **Workflow này**, bạn sẽ **tự động nhận cảnh báo khẩn cấp** từ PulsePoint, được **tóm tắt bằng AI** (OpenAI) và **gửi trực tiếp qua iMessage** (hoặc SMS qua Blooio) vào điện thoại của mình. Không cần code, không cần kỹ thuật, chỉ cần **cài đặt và chạy** là xong!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) để tránh giới hạn của phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Cập nhật tức thời** – Không bỏ lỡ bất kỳ cảnh báo khẩn cấp nào trong khu vực.
✅ **Tóm tắt bằng AI** – Cảnh báo dài dòng được rút gọn thành **văn bản dễ đọc**, tiết kiệm thời gian.
✅ **Gửi tin nhắn tự động** – Không cần mở ứng dụng, cảnh báo **được gửi trực tiếp qua iMessage/SMS**.
✅ **Hoạt động liên tục** – Workflow chạy **24/7** mà không cần can thiệp của bạn.
✅ **Cá nhân hóa** – Bạn có thể **lọc và tùy chỉnh** cảnh báo theo nhu cầu.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
🔹 **Tài khoản PulsePoint** – Đăng ký tại [web.pulsepoint.org](https://web.pulsepoint.org) và lấy **Agency ID**.
🔹 **API Key Blooio** – Đăng ký tại [blooio.com](https://blooio.com) để gửi tin nhắn (SMS/iMessage).
🔹 **API Key OpenAI** – Lấy tại [platform.openai.com](https://platform.openai.com/account/api-keys).
🔹 **Số điện thoại cá nhân** – Đăng ký trong định dạng quốc tế (ví dụ: `+841234567890`).
🔹 **Tài khoản iMessage/SMS** – Đảm bảo số điện thoại đã được liên kết với tài khoản Apple (nếu gửi qua iMessage).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [liên kết gốc](https://n8n.io/workflows/5533) hoặc sao chép mã JSON từ trang này.
- Mở **n8n Editor** và nhấn **Import Workflow** → Chọn file JSON hoặc dán mã JSON vào ô nhập.
- **Kích hoạt workflow** bằng cách bật nút **Active** ở góc trên bên phải.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **8 node chính**, các sếp cần **cấu hình kỹ lưỡng** các phần sau:

##### **🔹 Node "Get alerts" (Lấy cảnh báo)**
- Đây là **node Code** (n8n-nodes-base.code) lấy dữ liệu từ **PulsePoint API**.
- **Cần chỉnh sửa mã JavaScript** để lấy **Agency ID** của bạn:
  ```javascript
  const agencyId = "YOUR_PULSEPOINT_AGENCY_ID"; // Thay bằng Agency ID của bạn
  const url = `https://api.pulsepoint.org/v1/alerts?agencyId=${agencyId}`;
  ```
- **Lưu ý**:
  - Nếu PulsePoint không cung cấp API công khai, bạn có thể **tìm hiểu cách lấy dữ liệu** từ trang web của họ hoặc sử dụng **web scraping** (nếu cần, có thể thêm node **HTTP Request** để lấy dữ liệu từ trang PulsePoint).
  - Nếu không chắc chắn, liên hệ với **PulsePoint Support** để xác nhận cách lấy dữ liệu.

##### **🔹 Node "OpenAI Chat Model" (Tóm tắt bằng AI)**
- **Model AI mặc định**: `o4-mini` (mô hình nhỏ, tiết kiệm chi phí).
- **Prompt mẫu** (có thể chỉnh sửa trong node):
  ```
  Tóm tắt cảnh báo khẩn cấp này thành văn bản ngắn gọn, dễ hiểu, không quá 100 từ.
  Nếu có thông tin về vị trí, thời gian và hành động cần thực hiện, hãy nhấn mạnh.
  ```
- **Cấu hình OpenAI API**:
  - Đăng ký **API Key** tại [OpenAI](https://platform.openai.com/account/api-keys).
  - Trong node **OpenAI Chat**, chọn **credentials** là `openAiApi` và điền **API Key**.

##### **🔹 Node "Merge all" (Gộp dữ liệu)**
- Node **Code** này **gộp dữ liệu** từ PulsePoint và kết quả tóm tắt của AI.
- **Mã mặc định** đã sẵn sàng, nhưng các sếp có thể **chỉnh sửa** để phù hợp với cấu trúc dữ liệu của mình.

##### **🔹 Node "If" (Kiểm tra điều kiện)**
- **Điều kiện mặc định**: Kiểm tra xem có cảnh báo mới không.
- **Cấu hình**:
  - Nếu `$.json.alerts.length > 0` → **Thực hiện gửi tin nhắn**.
  - Nếu không → **Bỏ qua**.

##### **🔹 Node "Send Message" (Gửi tin nhắn)**
- **Cấu hình HTTP Request** để gửi tin nhắn qua **Blooio API**:
  | Thông tin | Giá trị |
  |------------|---------|
  | **Method** | `POST` |
  | **URL** | `https://api.blooio.com/send-message` |
  | **Headers** | `Accept: application/json`, `Authorization: Bearer YOUR_BLOOIO_API_KEY`, `Content-Type: application/json` |
  | **Body (JSON)** | ```json { "to": "+841234567890", "message": "{{ $json.summary }}" } ``` |
- **Lưu ý**:
  - Thay `YOUR_BLOOIO_API_KEY` bằng **API Key** của bạn.
  - Thay `+841234567890` bằng **số điện thoại** muốn nhận tin nhắn.
  - Nếu muốn gửi qua **iMessage**, đảm bảo số điện thoại đã được liên kết với **iCloud** và **Blooio hỗ trợ iMessage**.

##### **🔹 Node "Schedule Trigger" (Khởi động định kỳ)**
- **Cấu hình lịch chạy**:
  - Ví dụ: `0 0 * * *` (gửi cảnh báo mới mỗi ngày lúc 00:00).
  - Hoặc `*/5 * * * *` (gửi mỗi 5 phút để cập nhật tức thời).
- **Lưu ý**: Nếu muốn **gửi tức thời khi có cảnh báo mới**, có thể **bỏ node này** và sử dụng **Manual Trigger** (`When clicking ‘Execute workflow’`).

##### **🔹 Node "AI Agent" (Tùy chọn nâng cao)**
- Node này **có thể tự động hóa quy trình** hơn, nhưng trong workflow này, nó **không được sử dụng** (có thể bỏ qua hoặc xóa).

---

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Nhấn **Execute Workflow** để **kiểm tra dữ liệu mẫu**.
  - Kiểm tra **cảnh báo** từ PulsePoint có được lấy đúng không?
  - Kiểm tra **tóm tắt AI** có hợp lý không?
  - Kiểm tra **tin nhắn** có được gửi thành công không?
- **Bật Active**:
  - Sau khi kiểm tra xong, **bật nút Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NÀY ĐỂ TĂNG CƯỜNG HỆ THỐNG]
1. **Lưu log cảnh báo**:
   - Thêm **node Google Sheets** hoặc **node Notion** để **lưu lịch sử cảnh báo**.
   - Ví dụ: `n8n-nodes-base.googleSheets` với **credentials** là tài khoản Google của bạn.

2. **Gửi cảnh báo qua Slack/Telegram**:
   - Thêm **node Slack** (`n8n-nodes-base.slack`) hoặc **node Telegram** (`n8n-nodes-base.telegram`) để **báo động ngay khi có cảnh báo mới**.

3. **Tùy chỉnh prompt AI**:
   - Nếu muốn **tóm tắt chi tiết hơn**, chỉnh sửa prompt trong node **OpenAI Chat**:
     ```
     Tóm tắt cảnh báo khẩn cấp này thành văn bản ngắn gọn, bao gồm:
     - Vị trí cụ thể (địa chỉ, quận/huyện).
     - Loại cảnh báo (hỏa hoạn, tai nạn, thiên tai...).
     - Thời gian xảy ra.
     - Hành động cần thực hiện (đi đến địa điểm này, gọi số này...).
     Nếu có thông tin về người bị ảnh hưởng, hãy nhấn mạnh.
     ```

4. **Sử dụng Webhook để nhận cảnh báo từ bên ngoài**:
   - Thêm **node Webhook** (`n8n-nodes-base.webhook`) để **nhận cảnh báo từ ứng dụng khác** (ví dụ: từ một trang web cảnh báo khẩn cấp).

5. **Báo động âm thanh**:
   - Kết hợp với **node IFTTT** hoặc **node Telegram Bot** để **gửi tin nhắn có âm thanh báo động**.
:::

---

### 📌 **Kết luận**
Workflow này **giúp bạn không bỏ lỡ bất kỳ cảnh báo khẩn cấp nào** trong khu vực, với **tóm tắt AI** và **gửi tin nhắn tự động** ngay vào điện thoại. **Không cần code, không cần kỹ thuật**, chỉ cần **cài đặt và chạy** là xong!

🚀 **Hành động ngay hôm nay**:
1. **Chuẩn bị tài khoản** (PulsePoint, Blooio, OpenAI).
2. **Import workflow** và **cấu hình các node**.
3. **Test Run** và **bật Active**.
4. **Tận hưởng sự an toàn và tiện lợi** khi nhận cảnh báo khẩn cấp **tức thời và dễ hiểu**!

---
**Nếu có vấn đề gì trong quá trình cài đặt, hãy để lại bình luận bên dưới hoặc liên hệ với cộng đồng n8n tại [n8n.io/community](https://n8n.io/community) để được hỗ trợ!** 🛠️💡