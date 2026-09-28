---
title: "🚀 Bot Tự Động Cảnh Báo Giá Vé Máy Bay + Trợ Lý AI qua Telegram (N8n)"
description: "Workflow tự động hóa 100% không code giúp các sếp theo dõi giá vé máy bay, nhận cảnh báo khi giá xuống dưới ngưỡng chấp nhận, và tương tác với trợ lý AI thông minh qua Telegram. Giúp tiết kiệm thời gian lên đến 10 giờ/tuần và tránh bỏ lỡ cơ hội mua vé rẻ."
slug: "bot-tu-dong-can-bao-gia-ve-may-bay-ai-telegram-n8n"
tags: [n8n, automation, no-code, ai-chatbot, market-research, telegram-bot, serpapi, google-gemini]
keywords: [n8n workflow tự động hóa giá vé máy bay, bot cảnh báo giá vé rẻ Telegram, AI trợ lý du lịch n8n, tự động hóa du lịch không code, serpapi + google gemini, tự động hóa business travel]
---

# **🚀 Bot Tự Động Cảnh Báo Giá Vé Máy Bay + Trợ Lý AI qua Telegram (N8n)**

## **💥 Nỗi Đau Của Các Sếp Khi Mua Vé Máy Bay**
Mua vé máy bay là một trong những công việc tốn thời gian nhất đối với các sếp và nhân viên du lịch:
- **Phải tra cứu giá hàng ngày** trên nhiều trang web khác nhau (Google Flights, Skyscanner, Kayak...).
- **Không biết khi nào là thời điểm mua giá rẻ nhất**, dẫn đến chi phí không cần thiết.
- **Phải nhớ lại lịch sử tra cứu**, mất nhiều thời gian để so sánh.
- **Không thể tương tác tự nhiên** với một trợ lý AI để tìm kiếm vé phù hợp với nhu cầu cụ thể (ví dụ: "Tìm vé từ Hà Nội đến Đà Nẵng, ngày 15/12, giá dưới 2 triệu, có ghế rộng").

**Giải pháp?** **Workflow này tự động hóa toàn bộ quá trình** với hai chức năng chính:
1. **Cảnh báo giá vé rẻ** theo lịch trình (mỗi 7 ngày 1 lần).
2. **Trợ lý AI thông minh** trả lời mọi câu hỏi về vé máy bay qua Telegram.

---

## **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần** tra cứu giá vé thủ công.
- **Nhận cảnh báo tức thì** khi giá xuống dưới ngưỡng chấp nhận.
- **Tương tác tự nhiên** với AI qua Telegram (không cần biết code).
- **Lưu trữ lịch sử tra cứu**, so sánh giá dễ dàng.
- **Hỗ trợ nhiều tuyến bay**, không giới hạn.
- **Tiết kiệm chi phí** lên đến 30-50% so với mua vé không theo dõi.
:::

---

## **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Telegram** (để nhận cảnh báo và tương tác với AI).
2. **API Key SerpAPI** (miễn phí 500 request/tháng, [đăng ký tại đây](https://serpapi.com/)).
3. **API Key Google Gemini** (miễn phí 3 tháng, [đăng ký tại đây](https://aistudio.google.com/app/apikey)).
4. **Bot Telegram** (tạo bằng cách chat với [@BotFather](https://t.me/BotFather)).
5. **Ngân sách** (~50k-100k/tháng) để chạy workflow 24/7 trên VPS.

👉 **🎁 Mã giảm giá VPS cho n8n:**
- [TinoHost (39% giảm)](https://tino.vn/vps-n8n?affid=388) (Mã: **VPSN8N**)
- [BNIX (Xeon 4GB chỉ 50k/tháng)](https://my.bnix.one/aff.php?aff=172)
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/12971](https://n8n.io/workflows/12971) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/12971) và paste vào **Import Workflow** trong n8n.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **2 phần chính**:
#### **📅 Phần 1: Cảnh Báo Giá Vé Tự Động (Schedule Trigger)**
| Node | Tên | Yêu Cầu Cấu Hình |
|------|-----|------------------|
| ⏰ **Schedule Trigger** | Khởi động workflow | Thiết lập chạy **mỗi 7 ngày lúc 7:30 AM** (hoặc điều chỉnh theo nhu cầu). |
| ⚙️ **Edit Fields** | Cấu hình tuyến bay | Điền:
- **Departure/Arrival** (Mã sân bay IATA, ví dụ: **HAN** (Hà Nội) → **SGN** (TP.HCM)).
- **Price Threshold** (Ngưỡng giá chấp nhận, ví dụ: **2.000.000 VND**).
- **Telegram ID** (ID của bot Telegram sẽ nhận cảnh báo). |
| ✈️ **Google Flights Search** | Tra cứu giá | Sử dụng **SerpAPI Key** đã đăng ký. |
| 💰 **Extract Best Price** | Lọc giá tốt nhất | Node này tự động xử lý kết quả API. |
| 🔍 **Filter by Price** | Kiểm tra giá | Đặt điều kiện: `price < threshold`. |
| 📱 **Send Alert** | Gửi cảnh báo Telegram | Chọn **Telegram Bot Token** và **Chat ID** (của bot hoặc cá nhân). |

#### **🤖 Phần 2: Trợ Lý AI Tương Tác qua Telegram**
| Node | Tên | Yêu Cầu Cấu Hình |
|------|-----|------------------|
| 💬 **Telegram Trigger** | Nhận tin nhắn | Chọn **Telegram Bot Token** và **Chat ID**. |
| 🤖 **AI Agent** | Xử lý yêu cầu | Node này tự động gọi các công cụ tra cứu. |
| 🧠 **Google Gemini Model** | AI trả lời | Điền **Google Palm API Key**. |
| ✈️ **Round Trip Search** & **One-Way Search** | Tra cứu vé | Cấu hình **SerpAPI Key** và **mã sân bay**. |
| 🧠 **Conversation Memory** | Lưu trữ lịch sử | Giúp AI nhớ các câu hỏi trước đó. |
| 📱 **Send Response** | Trả lời Telegram | Chọn **Telegram Bot Token** và **Chat ID**. |

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Điền **mã sân bay** (ví dụ: **HAN-SGN**).
   - Đặt **ngưỡng giá** (ví dụ: **2.000.000 VND**).
   - Gửi tin nhắn Telegram để kiểm tra AI.
2. **Bật Active** workflow.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH LÀM TIẾP]
- **Thêm nhiều tuyến bay**: Sao chép workflow và thay đổi **Edit Fields** cho mỗi tuyến.
- **Cảnh báo qua Email**: Thêm node **Email** sau **Send Alert**.
- **Lưu log tra cứu**: Sử dụng **Google Sheets** hoặc **Airtable** để lưu lịch sử giá.
- **Tự động trả lời khách hàng**: Kết hợp với **Zalo/Email** để tự động trả lời yêu cầu vé.
- **Dùng Gemini Flash** để giảm chi phí (thay vì Pro).
:::

---

## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc tra cứu giá vé thủ công, đồng thời **tối ưu hóa chi phí** bằng cách nhận cảnh báo khi giá xuống thấp nhất. Ngoài ra, **trợ lý AI** giúp tương tác tự nhiên qua Telegram, trả lời mọi câu hỏi về vé máy bay một cách thông minh.

**🚀 Hành động ngay:**
1. **Đăng ký VPS** để chạy workflow 24/7.
2. **Import workflow** và cấu hình API.
3. **Thiết lập ngưỡng giá** và bắt đầu tiết kiệm!

---
**🔗 Tài liệu tham khảo:**
- [Tutorial chi tiết từ tác giả](https://nguyenthieutoan.com)
- [SerpAPI Documentation](https://serpapi.com/flights-results)
- [Google Gemini API Guide](https://ai.google.dev/gemini-api/docs)