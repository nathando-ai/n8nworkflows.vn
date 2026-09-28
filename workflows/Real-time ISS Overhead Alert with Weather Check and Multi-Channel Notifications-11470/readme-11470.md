---
title: "🚀 **Hệ Thống Thông Báo Thực Tế ISS & Tiangong + Dự Báo Thời Tiết + Thông Báo Multi-Channel (Tự Động Hóa 100%)**"
description: "Workflow tự động theo dõi vị trí ISS và Tiangong, dự báo thời gian quan sát, kiểm tra điều kiện thời tiết, và gửi thông báo đa kênh (Telegram, Discord, Slack) cùng với trivia AI và báo cáo tuần. Giúp các fan hâm mộ không bỏ lỡ bất kỳ lần xuất hiện nào của trạm không gian!"
slug: "thong-bo-realtime-iss-tiangong-dự-báo-thời-tiết"
tags: [n8n, automation, no-code, api-integration, ai-summarization, space-tracking, google-sheets, openai, telegram, discord, slack]
keywords: [n8n workflow ISS Tiangong, tự động hóa theo dõi vệ tinh, dự báo xuất hiện ISS, thông báo thời gian quan sát, AI trivia không gian, báo cáo tuần tự động, Google Sheets + Calendar, OpenAI GPT-4]
---

# 🚀 **Hệ Thống Thông Báo Thực Tế ISS & Tiangong: Từ Dữ Liệu → Thông Báo → Báo Cáo Tự Động**

## **🔍 Nỗi Đau Của Các Fan Hâm Mộ Không Gian**
Bạn đã bao giờ **bỏ lỡ** lần xuất hiện của ISS hoặc Tiangong vì không biết thời gian chính xác? Hay phải **tìm kiếm thủ công** trên nhiều trang web khác nhau để biết điều kiện thời tiết, vị trí vệ tinh, và thời gian quan sát lý tưởng? Với **Workflow này**, các sếp sẽ **tự động nhận thông báo** khi ISS/Tiangong xuất hiện gần địa phương, **kiểm tra điều kiện thời tiết**, **tính toán điểm quan sát tốt nhất**, và **gửi báo cáo tuần** với **trivia AI** – **không cần viết một dòng code nào!**

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
✅ **Thông báo thực tế 5 phút/lần** về vị trí ISS/Tiangong, điểm quan sát, và điều kiện thời tiết.
✅ **Dự báo 7 ngày** xuất hiện vệ tinh với **độ cao tối ưu** (≥40°) và **gợi ý thời gian quan sát**.
✅ **Báo cáo tuần tự động** với **thống kê quan sát**, **phân tích thành công**, và **gợi ý cải thiện**.
✅ **Trivia AI bằng GPT-4** về không gian, **cập nhật theo thời gian thực**.
✅ **Thông báo đa kênh** (Telegram, Discord, Slack) với **định dạng giàu hình ảnh**.
✅ **Lưu lịch sử quan sát** trên **Google Sheets** và **đăng ký sự kiện** vào **Google Calendar**.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi Lên Đồ**]
Các sếp cần **cài đặt và cấu hình** các dịch vụ sau:
1. **N2YO API** (miễn phí) – Dữ liệu vệ tinh chi tiết (ISS + Tiangong).
2. **OpenWeatherMap API** (miễn phí) – Dữ liệu thời tiết.
3. **OpenAI API** – Sử dụng **GPT-4o-mini** để tạo **trivia** và **báo cáo AI**.
4. **Google Sheets** – Lưu lịch sử quan sát (cần **ID Sheet**).
5. **Google Calendar** – Tự động tạo sự kiện quan sát.
6. **Telegram/Discord/Slack** – Kênh thông báo (cần **Chat ID** hoặc **Channel ID**).
7. **Môi trường biến môi trường** (Environment Variables):
   - `USER_LAT`, `USER_LON`, `USER_LOCATION_NAME` (vị trí của bạn).
   - `N2YO_API_KEY` (mã API từ N2YO).
   - `GOOGLE_SHEET_ID` (ID của Sheet Google).
   - `TELEGRAM_CHAT_ID` (ID chat Telegram).
   - `SLACK_CHANNEL` (Channel Slack).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/11470](https://n8n.io/workflows/11470) hoặc **copy/paste** JSON vào **n8n Editor**.
- **Nhấp vào "Import"** và chọn **Self-hosted** (nếu tự cài đặt trên VPS).

#### **2. Các Lưu Ý Bắt Buộc Chỉnh 📌**
Workflow này gồm **3 flow chính**:
- **🔄 Thực Tế (5 phút/lần)**: Kiểm tra vị trí vệ tinh → Thời tiết → AI Trivia → Thông báo.
- **🔮 Dự Báo Hàng Ngày (6h sáng)**: Lấy dự báo 7 ngày → Format báo cáo → Đăng ký vào Calendar.
- **📊 Báo Cáo Tuần (Chủ Nhật 20h)**: Tính thống kê → AI phân tích → Gửi báo cáo.

##### **🔹 Cấu Hình Cần Thiết**
| **Node** | **Lưu Ý** | **Cách Chỉnh** |
|----------|-----------|---------------|
| **ScheduleTrigger** | Thiết lập thời gian chạy | - Thực tế: **5 phút/lần** <br> - Dự báo: **6h sáng hàng ngày** <br> - Báo cáo: **Chủ Nhật 20h** |
| **HTTP Request (N2YO, OpenWeatherMap)** | Điền `API Key` | - Tạo tại [N2YO](https://www.n2yo.com/) và [OpenWeatherMap](https://openweathermap.org/). |
| **Google Sheets** | Chọn Sheet và Sheet Name | - **Operation**: `append` (thêm dữ liệu mới). <br> - **Columns**: `timestamp, satellite, distance_km, ...` (đã định sẵn). |
| **OpenAI (GPT-4o-mini)** | Điền `API Key` | - Tạo tại [OpenAI](https://platform.openai.com/). <br> - **Prompt**: Đã tối ưu sẵn cho trivia và báo cáo. |
| **Telegram/Discord/Slack** | Điền `Chat ID`/`Channel ID` | - **Telegram**: Tạo bot và lấy `Chat ID` bằng `/get_id`. <br> - **Discord**: Lấy `Channel ID` từ URL. <br> - **Slack**: Lấy `Channel ID` từ `https://slack.com/team/{ID}/channels/{CHANNEL_ID}`. |
| **Google Calendar** | Chọn Calendar | - Chọn **Calendar** của bạn trong danh sách. |

##### **🔹 Node Quan Trọng Khác**
- **"Calculate All Satellites" (Code)**: Sử dụng **Haversine formula** để tính khoảng cách và hướng.
- **"Format Rich Notification" (Code)**: Xây dựng thông báo giàu hình ảnh với **Markdown**.
- **"Generate Space Trivia" (ChainLlm)**: AI tạo **trivia không gian** bằng tiếng Nhật (có thể thay đổi ngôn ngữ).

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Chạy **manual** với dữ liệu mẫu để kiểm tra.
- **Active Workflow**: Bật **toggle "Active"** để chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**Tối Ưu Hiệu Quả**]
🔹 **Thêm kênh thông báo khác**:
   - **Email**: Sử dụng **n8n-nodes-base.email** để gửi báo cáo tuần qua email.
   - **Push Notification**: Kết nối với **Firebase Cloud Messaging** (FCM).

🔹 **Lưu log chi tiết**:
   - Thêm **n8n-nodes-base.stickyNote** để ghi chú lỗi hoặc cập nhật.

🔹 **Tự động chia sẻ trên mạng xã hội**:
   - Sử dụng **n8n-nodes-base.twitter** hoặc **Facebook API** để chia sẻ thông báo quan sát.

🔹 **Cập nhật thông tin thiên văn**:
   - Thêm **node HTTP Request** để lấy dữ liệu từ **NASA API** hoặc **Celestrak** để mở rộng vệ tinh theo dõi.
:::

---

### 📌 **Kết Luận**
Workflow này **không chỉ đơn giản là tự động hóa**, mà còn **tạo ra một hệ thống thông minh** giúp các sếp:
✔ **Không bỏ lỡ** bất kỳ lần xuất hiện nào của ISS/Tiangong.
✔ **Tiết kiệm thời gian** với **báo cáo tự động** và **thông báo đa kênh**.
✔ **Học hỏi** với **trivia AI** và **báo cáo tuần** phân tích chi tiết.

**🚀 Hãy import ngay và bắt đầu theo dõi không gian từ trên trần nhà!**

---
:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)**.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**
:::

---
**💡 Lưu ý cuối cùng**: Nếu gặp lỗi, hãy kiểm tra **API Key** và **credentials** của các dịch vụ. Nếu cần hỗ trợ, comment bên dưới hoặc liên hệ tác giả [@suzuki](https://n8n.io/workflows/11470) trên n8n! 🚀