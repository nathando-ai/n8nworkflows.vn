---
title: "🌦️ Tự Động Hóa Thông Tin Thời Tiết Cho Bất Kỳ Thành Phố - Không Cần Code!"
description: "Workflow này giúp các sếp nhận thông tin thời tiết chính xác từ bất kỳ thành phố nào chỉ bằng một request webhook, tiết kiệm thời gian và tránh sai sót khi tra cứu thủ công."
slug: "tieu-dong-hoa-thong-tin-thoi-tiet"
tags: [n8n, automation, no-code, api-integration, openweathermap, webhook]
keywords: [n8n workflow thời tiết, tự động hóa tra cứu thời tiết, API OpenWeatherMap, webhook n8n, tra cứu thời tiết tự động]
---

# 🌦️ **Tự Động Hóa Thông Tin Thời Tiết Cho Bất Kỳ Thành Phố - Không Cần Code!**

### **Nỗi Đau Của Các Sếp Khi Tra Cứu Thời Tiết Thủ Công**
Hàng ngày, các sếp phải mất thời gian tra cứu thời tiết cho nhiều thành phố khác nhau trên Google, AccuWeather hay các ứng dụng khác. Thông tin có thể lỗi thời, không chính xác, hoặc mất nhiều thời gian để tổng hợp. **Workflow này giải quyết vấn đề đó bằng cách tự động hóa toàn bộ quá trình chỉ với một request webhook!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7 và không bị gián đoạn, các sếp nên **self-host n8n** trên một VPS ổn định.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** – Không cần tra cứu thủ công trên nhiều trang web.
✅ **Thông tin chính xác** – Dữ liệu thời tiết từ API **OpenWeatherMap** (chất lượng cao).
✅ **Tự động hóa hoàn toàn** – Chỉ cần gửi request webhook, workflow sẽ trả về kết quả ngay lập tức.
✅ **Dễ dàng mở rộng** – Có thể kết hợp với Slack, Telegram hoặc gửi email báo cáo thời tiết hàng ngày.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
- **API Key của OpenWeatherMap** (miễn phí hoặc trả phí tùy chọn).
- **Tài khoản n8n** (cài đặt trên máy chủ hoặc VPS).

:::info[Lấy API Key OpenWeatherMap]
1. Đăng ký tài khoản tại [OpenWeatherMap](https://openweathermap.org/api).
2. Mua hoặc sử dụng **API Key miễn phí** (có giới hạn request).
3. Thêm API Key vào **Credentials** của n8n (cấu hình sau khi import workflow).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/807](https://n8n.io/workflows/807) hoặc copy toàn bộ JSON từ link trên.
- Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON và chọn **"Import"**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **3 node chính**, các sếp cần cấu hình như sau:

##### **🔹 Node Webhook (Nhận Request)**
- **Tên node:** `Webhook`
- **Path:** `45690b6a-2b01-472d-8839-5e83a74858e5` (không cần thay đổi).
- **Lưu ý:**
  - Các sếp có thể thay đổi **Method** (GET/POST) tùy nhu cầu.
  - **Payload** sẽ chứa thông tin thành phố cần tra cứu (ví dụ: `{"city": "Hà Nội"}`).

##### **🔹 Node OpenWeatherMap (Tra Cứu Thời Tiết)**
- **Tên node:** `OpenWeatherMap`
- **Credentials:** Chọn `"openWeatherMapApi"` (phải tạo trước khi import).
  - **Cách tạo Credentials:**
    1. Trong n8n Editor → **"Credentials"** → **"Add"** → Chọn **"OpenWeatherMap"**.
    2. Điền **API Key** từ OpenWeatherMap vào trường **"Api Key"**.
- **Parameters cần điền:**
  - **City:** `$node["Webhook"]["json"]["city"]` (lấy từ request webhook).
  - **Units:** `"metric"` (đơn vị Celsius) hoặc `"imperial"` (Fahrenheit).
  - **Lang:** `"vi"` (ngôn ngữ tiếng Việt) hoặc `"en"` (tiếng Anh).

##### **🔹 Node Set (Lưu Trả Về)**
- **Tên node:** `Set`
- **Lưu ý:**
  - Node này **không cần cấu hình thêm**, chỉ dùng để **lưu kết quả** từ OpenWeatherMap.
  - Kết quả sẽ trả về dưới dạng JSON, bao gồm:
    ```json
    {
      "city": "Hà Nội",
      "temperature": 28.5,
      "description": "Nắng gay gắt",
      "humidity": 65
    }
    ```

#### **3. Kích Hoạt ⚡️**
- **Test Run:**
  - Gửi một request webhook với payload:
    ```json
    {
      "city": "Hồ Chí Minh"
    }
    ```
  - Kiểm tra kết quả trong **Execution View** của n8n.
- **Bật Active:**
  - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Hợp Với Slack/Telegram**
   - Sử dụng **node Slack** hoặc **Telegram Bot** để gửi thông báo thời tiết tự động.
   - Ví dụ: Khi thời tiết nóng hơn 35°C, gửi cảnh báo qua Slack.

2. **Lưu Log & Báo Cáo Định Kỳ**
   - Sử dụng **node Google Sheets** hoặc **node Database** để lưu lịch sử thời tiết.
   - Tự động gửi **báo cáo hàng tuần** về thời tiết trung bình của các thành phố.

3. **Tự Động Hóa Tra Cứu Thời Tiết Cho Nhiều Thành Phố**
   - Sử dụng **node Set** để lưu danh sách thành phố cần tra cứu.
   - Sử dụng **node Loop** để chạy workflow cho tất cả thành phố trong danh sách.

4. **Cập Nhật Thời Tiết Định Kỳ**
   - Sử dụng **node Schedule** để chạy workflow hàng giờ/lần để cập nhật thời tiết tự động.

---

### 📌 **Kết Luận**
Workflow này giúp các sếp **tự động hóa tra cứu thời tiết chỉ với một request webhook**, tiết kiệm thời gian và đảm bảo dữ liệu chính xác. **Hãy import ngay và áp dụng vào công việc hàng ngày!**

:::tip[Gợi Ý Sử Dụng]
- Dùng cho **dự báo thời tiết tự động** trong ứng dụng nội bộ.
- **Tích hợp vào website** để người dùng tra cứu thời tiết một cách nhanh chóng.
- **Kết hợp với AI** (n8n + LLM) để dự báo thời tiết theo khu vực.
:::

**Bắt đầu tự động hóa ngay hôm nay!** 🚀