---
title: "🌍 **Tự Động Hoàn Thành Chuyến Đi & Gửi Xác Nhận Email Với Gemini AI - Không Cần Code!**"
description: "Workflow này tự động phân tích yêu cầu du lịch từ khách hàng, tìm kiếm vé máy bay, khách sạn, hoạt động, và gửi email xác nhận chi tiết với Gemini AI - tiết kiệm thời gian lên đến 80% cho bộ phận du lịch!"
slug: "tieu-dong-hoan-thanh-chuyen-di-voi-gemini-ai"
tags: [n8n, automation, no-code, gemini-ai, du-lich, email-automation]
keywords: [n8n workflow du lịch, tự động hóa du lịch, gemini ai n8n, gửi email xác nhận du lịch tự động, api du lịch n8n]
---

# 🚀 **Tự Động Hoàn Thành Chuyến Đi & Gửi Xác Nhận Email Với Gemini AI**

### **Giải pháp hoàn hảo cho các sếp quản lý du lịch**
Hiện nay, việc thủ công xử lý yêu cầu du lịch của khách hàng - từ phân tích yêu cầu, tìm kiếm vé máy bay, khách sạn, đến soạn email xác nhận - tiêu tốn thời gian và dễ gây lỗi. **Workflow này tự động hóa toàn bộ quy trình với Gemini AI**, giúp các sếp:
- **Tiết kiệm 80% thời gian** so với làm thủ công
- **Tránh sai sót** trong quá trình tìm kiếm và soạn email
- **Cung cấp trải nghiệm cá nhân hóa** cho khách hàng
- **Hoạt động 24/7** mà không cần can thiệp

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động phân tích yêu cầu du lịch** từ tin nhắn khách hàng (Slack, Telegram, email...)
✅ **Tìm kiếm vé máy bay, khách sạn, hoạt động** bằng API (không cần code)
✅ **Tạo itinerary chi tiết** với Gemini AI, bao gồm lịch trình, địa điểm, thời gian
✅ **Gửi email xác nhận tự động** với nội dung chuyên nghiệp, cá nhân hóa
✅ **Hoạt động liên tục** mà không cần can thiệp thủ công
✅ **Giảm chi phí** do tiết kiệm thời gian và giảm sai sót
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
- **Tài khoản Google** (để kết nối với **Google Gemini API** và **Gmail**)
- **API Key của Google Gemini** (truy cập [Google AI Studio](https://makersuite.google.com/app/apikey))
- **Credentials cho API tìm kiếm vé máy bay/khách sạn** (ví dụ: [UsersAPI](https://usersapi.co/) hoặc dịch vụ tương tự)
- **Tài khoản Slack/Telegram** (để nhận tin nhắn kích hoạt workflow)
- **Tài khoản Gmail** (để gửi email xác nhận)
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/8881](https://n8n.io/workflows/8881) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **15 node** với các chức năng chính sau. Các sếp **phải cấu hình kỹ lưỡng** các node sau:

##### **🔹 Node "When chat message received" (Trigger)**
- **Lựa chọn kênh kích hoạt**: Slack, Telegram, hoặc email (tùy thuộc vào cách khách hàng gửi yêu cầu).
- **Lưu ý**: Nếu sử dụng Slack/Telegram, cần kết nối với bot và cấu hình webhook.

##### **🔹 Node "Google Gemini Chat Model" (3 node)**
- **Điền API Key**:
  - Truy cập [Google AI Studio](https://makersuite.google.com/app/apikey) để lấy **Google Palm API Key**.
  - Trong node, chọn **Credentials → googlePalmApi** và dán API Key.
- **Prompt mẫu**:
  - Các sếp có thể điều chỉnh prompt để phù hợp với yêu cầu cụ thể (ví dụ: yêu cầu khách hàng nhập ngày đi, điểm đến, ngân sách...).

##### **🔹 Node "httpRequestTool" (4 node: Accommodations, Accommodation Details, Activities, Flight booking)**
- **Cấu hình API**:
  - Các node này gọi API để lấy dữ liệu vé máy bay, khách sạn, hoạt động.
  - **Ví dụ**: Nếu sử dụng [UsersAPI](https://usersapi.co/), cần điền:
    - **URL**: `https://usersapi.co/GET/...` (tùy thuộc vào API cụ thể)
    - **Headers**: Thêm `Authorization: Bearer {API_KEY}`
    - **Query Parameters**: Điền các tham số như `destination`, `dates`, `budget`.
  - **Lưu ý**: Nếu API yêu cầu xác thực, chọn **httpQueryAuth** và điền credentials.

##### **🔹 Node "gmail" (Send a message)**
- **Kết nối Gmail**:
  - Trong n8n, thêm **Credentials mới** → Chọn **Gmail OAuth2**.
  - Đăng nhập tài khoản Gmail và cấp quyền cho n8n.
- **Cấu hình email**:
  - **From**: Điền địa chỉ email gửi (ví dụ: `dulich@congty.com`).
  - **To**: Địa chỉ email khách hàng (có thể lấy từ tin nhắn đầu vào).
  - **Subject**: "Xác nhận chuyến đi của bạn: [Destination]"
  - **Body**: Nội dung email sẽ được tự động tạo bởi **Email Agent**.

##### **🔹 Node "Structured Output Parser" (3 node)**
- **Không cần chỉnh sửa** (n8n tự động phân tích và định dạng dữ liệu từ Gemini AI).

##### **🔹 Node "Agent" (3 node: Extract User Request, Planner Agent, Email Agent)**
- **Không cần cấu hình thêm**, chỉ cần đảm bảo các node liên kết trước đó hoạt động.

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi một tin nhắn mẫu (ví dụ: *"Tôi muốn đi du lịch Hà Nội trong 3 ngày, từ ngày 15/10, ngân sách 5 triệu"*) đến kênh kích hoạt (Slack/Telegram).
   - Kiểm tra các node hoạt động có lỗi không.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Slack/Telegram**:
   - Thay vì sử dụng webhook, các sếp có thể tạo **bot Slack/Telegram** và kết nối với node **chatTrigger** để khách hàng dễ dàng gửi yêu cầu.

2. **Lưu lịch trình vào Google Sheets/Notion**:
   - Thêm node **Google Sheets** hoặc **Notion** sau node **Planner Agent** để lưu lịch trình cho khách hàng và quản lý nội bộ.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng node **Set Interval** để gửi email tổng hợp các chuyến đi đã xác nhận cho bộ phận quản lý.

4. **Cải thiện prompt cho Gemini AI**:
   - Nếu kết quả không chính xác, các sếp có thể điều chỉnh **prompt** trong node **Google Gemini Chat Model** để yêu cầu AI trả về dữ liệu chi tiết hơn.

5. **Xử lý lỗi API**:
   - Thêm node **Set** hoặc **If** để xử lý trường hợp API trả về lỗi (ví dụ: không tìm thấy vé máy bay).
:::

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp quản lý du lịch muốn tự động hóa toàn bộ quy trình từ nhận yêu cầu đến gửi email xác nhận. **Không cần code**, chỉ cần cấu hình các node và kết nối API, các sếp sẽ tiết kiệm thời gian và giảm thiểu sai sót.

**Hãy áp dụng ngay và nâng cao hiệu suất bộ phận du lịch của mình!** 🚀
Nếu có vấn đề trong quá trình setup, các sếp có thể tham khảo [hướng dẫn chi tiết của n8n](https://docs.n8n.io/) hoặc liên hệ với cộng đồng n8n trên [Discord](https://n8n.io/discord).

---
**🔹 Bạn có thể tùy chỉnh workflow này để phù hợp với yêu cầu cụ thể của công ty!** 🔹