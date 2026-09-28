---
title: "🚀 Tự Động Hóa Cảnh Báo Hành Tinh Bay Lên Trái Đất Từ NASA Sang LINE Với AI (OpenAI + DeepL)"
description: "Workflow tự động hóa 24/7 cảnh báo hành tinh nguy hiểm từ NASA đến LINE với cảnh báo khoa học viễn tưởng (Sci-Fi) và dịch thuật tự động. Giúp các sếp theo dõi an toàn hành tinh một cách thông minh, không cần code."
slug: "tu-dong-hoa-can-bao-hanh-tinh-nasa-sang-line-voi-ai"
tags: [n8n, automation, no-code, ai, nasa, line-notify, openai, deepl, khoa-hoc-vien-tang]
keywords: [n8n workflow cảnh báo hành tinh, tự động hóa NASA LINE, cảnh báo nguy hiểm hành tinh, OpenAI DeepL n8n, tự động hóa an toàn hành tinh]
---

# 🚀 **Tự Động Hóa Cảnh Báo Hành Tinh Bay Lên Trái Đất Từ NASA Đến LINE Với AI (OpenAI + DeepL)**

## **🔥 Nỗi Đau Của Các Sếp: "Làm Thế Nào Để Biết Được Nếu Một Hành Tinh Bay Lên Trái Đất?"**
Trong thế giới hiện đại, các sếp không chỉ lo về email, báo cáo hoặc dự án mà còn lo về **an toàn hành tinh**! NASA cung cấp dữ liệu về các hành tinh nguy hiểm (NEOs - Near-Earth Objects) nhưng phải **quét thủ công hàng ngày** để kiểm tra. Nếu không may, một hành tinh nguy hiểm bay gần Trái Đất, các sếp sẽ phải **tìm kiếm tin tức trên Google, đọc báo cáo NASA, và cảnh báo đồng nghiệp** – một quá trình **tốn thời gian, dễ bỏ lỡ và không hiệu quả**.

**Workflow này giải quyết vấn đề đó bằng cách:**
✅ **Tự động lấy dữ liệu** từ NASA hàng ngày.
✅ **Lọc và phân tích** các hành tinh nguy hiểm.
✅ **Tạo cảnh báo khoa học viễn tưởng** (Sci-Fi) bằng OpenAI.
✅ **Dịch thuật tự động** sang ngôn ngữ mong muốn (Việt Nam, Anh, Nhật,...) bằng DeepL.
✅ **Gửi cảnh báo ngay lập tức** qua LINE Notify (hoặc Slack, Email, Telegram).

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải quét thủ công NASA hàng ngày.
- **Cảnh báo tức thời**: Nhận thông báo ngay khi có hành tinh nguy hiểm.
- **Cá nhân hóa cảnh báo**: Dịch thuật sang ngôn ngữ mong muốn.
- **Hiệu quả 24/7**: Chạy tự động hàng ngày, không cần can thiệp.
- **Thú vị với Sci-Fi**: Cảnh báo được viết bằng phong cách khoa học viễn tưởng.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản NASA API**:
   - Đăng ký miễn phí tại [NASA API](https://api.nasa.gov/) và lấy **API Key**.
2. **Tài khoản OpenAI**:
   - Đăng ký tại [OpenAI](https://platform.openai.com/) và lấy **API Key**.
3. **Tài khoản DeepL** (nếu muốn dịch thuật):
   - Đăng ký tại [DeepL](https://www.deepl.com/pro-api) và lấy **API Key**.
4. **LINE Notify Token**:
   - Tạo token tại [LINE Notify](https://notify-bot.line.me/) để gửi thông báo.
   *(Lưu ý: Có thể thay thế bằng Slack, Discord, Email nếu muốn.)*
5. **n8n Self-hosted** (khuyến nghị):
   - Để workflow chạy 24/7 ổn định, các sếp nên cài n8n trên **VPS riêng**.
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import từ file JSON** hoặc **copy/paste JSON vào n8n Editor**:
1. Tải workflow từ [n8n.io/workflows/11304](https://n8n.io/workflows/11304).
2. Trong n8n Editor, nhấn **Import** và chọn file JSON.
3. Hoặc **copy toàn bộ JSON** và dán vào **Import Workflow** (Ctrl+V).

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **8 node chính**, các sếp cần cấu hình kỹ lưỡng như sau:

#### **🔹 Node 1: Daily Schedule1 (scheduleTrigger)**
- **Cấu hình**:
  - **Schedule**: Chọn **"Daily"** và thời gian mong muốn (ví dụ: 8h sáng).
  - **Time Zone**: Chọn **UTC+7** (hoặc khu vực của các sếp).

#### **🔹 Node 2: Get Asteroid Data1 (nasa)**
- **Cấu hình**:
  - **API Key**: Điền **NASA API Key** từ tài khoản NASA.
  - **Resource**: Để mặc định là **"asteroidNeoFeed"**.
  - **Parameters**:
    - `start_date`: `today` (hoặc ngày cụ thể).
    - `end_date`: `today` (hoặc ngày cụ thể).
    - `size_meters`: `140` (lọc hành tinh có đường kính >140m).

#### **🔹 Node 3: Filter & Calculate Distance1 (code)**
- **Cấu hình**:
  - **Script JavaScript** (sử dụng mặc định từ workflow):
    ```javascript
    // Lọc hành tinh nguy hiểm và tính khoảng cách so với Mặt Trăng
    const hazardousAsteroids = $input.all().filter(asteroid =>
      asteroid.is_potentially_hazardous_asteroid === true
    );

    hazardousAsteroids.forEach(asteroid => {
      const moonDistance = 384400; // Km (khoảng cách Trái Đất-Mặt Trăng)
      const distanceToEarth = asteroid.distance_au * 149597870.7; // AU -> Km
      const distanceToMoon = Math.abs(distanceToEarth - moonDistance);

      asteroid.distance_to_moon_km = distanceToMoon;
      asteroid.is_closer_than_moon = distanceToMoon < moonDistance;
    });

    return { hazardousAsteroids };
    ```
  - **Lưu ý**: Node này **lọc hành tinh nguy hiểm** và tính **khoảng cách so với Mặt Trăng**.

#### **🔹 Node 4: Check Threat Level1 (switch)**
- **Cấu hình**:
  - **Condition**: Chọn **"is_closer_than_moon"** (nếu hành tinh bay gần Mặt Trăng).
  - **True Path**: Đi đến **Generate SF Alert1** (cảnh báo nguy hiểm).
  - **False Path**: Đi đến **Send Peace Report1** (báo cáo an toàn).

#### **🔹 Node 5: Generate SF Alert1 (openAi)**
- **Cấu hình**:
  - **API Key**: Điền **OpenAI API Key**.
  - **Model**: Chọn **"gpt-3.5-turbo"** (hoặc mới nhất).
  - **Prompt** (cần chỉnh sửa để phù hợp):
    ```json
    {
      "role": "system",
      "content": "You are a sci-fi writer. Write a dramatic alert about a dangerous asteroid approaching Earth. Include details like size, distance, and potential impact."
    },
    {
      "role": "user",
      "content": "Asteroid name: {{ $node["Get Asteroid Data1"].json["name"] }}\nSize: {{ $node["Get Asteroid Data1"].json["estimated_diameter_meters"]["estimated_diameter_min"] }}m\nDistance to Earth: {{ $node["Get Asteroid Data1"].json["distance_au"] }} AU\nPotentially Hazardous: {{ $node["Get Asteroid Data1"].json["is_potentially_hazardous_asteroid"] }}"
    }
    ```
  - **Lưu ý**: Cần **điền biến `{{ $node["Get Asteroid Data1"].json["..."] }}`** chính xác.

#### **🔹 Node 6: Translate Alert1 (deepL)**
- **Cấu hình**:
  - **API Key**: Điền **DeepL API Key**.
  - **Target Language**: Chọn ngôn ngữ muốn dịch (ví dụ: **Vietnamese**).
  - **Text**: Sử dụng **output từ node OpenAI**.

#### **🔹 Node 7 & 8: Send Danger Alert1 & Send Peace Report1 (line)**
- **Cấu hình**:
  - **Token**: Điền **LINE Notify Token**.
  - **Message**:
    - **Send Danger Alert1**:
      ```json
      {
        "message": "🚨 **CẢNH BÁO HÀNH TINH NỮY HẠN!**\n\n{{ $node["Translate Alert1"].json["translatedText"] }}"
      }
      ```
    - **Send Peace Report1**:
      ```json
      {
        "message": "🌍 **BÁO CÁO AN TOÀN HÀNH TINH**\n\nKhông có hành tinh nguy hiểm bay gần Trái Đất hôm nay! 😊"
      }
      ```
  - **Lưu ý**: Có thể thay thế LINE bằng **Slack, Discord, Email** bằng cách thay đổi node.

---
### **⚡️ Kích Hoạt Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Chạy **manual run** để kiểm tra các node hoạt động.
2. **Bật Active**:
   - Đánh dấu workflow thành **"Active"** để chạy tự động hàng ngày.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Thay thế LINE bằng Slack/Email**:
   - Thay node `line` bằng `slack` hoặc `email` để gửi cảnh báo.
2. **Lưu log cảnh báo**:
   - Thêm node **Google Sheets** hoặc **Notion** để ghi lại lịch sử cảnh báo.
3. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n Schedule Trigger** để gửi báo cáo tuần/month.
4. **Tích hợp với Telegram**:
   - Thay LINE bằng **Telegram Bot** để cảnh báo trên nhóm.
5. **Cải thiện prompt OpenAI**:
   - Thử viết prompt khác để cảnh báo **hài hước hơn** hoặc **căng thẳng hơn**.
:::

---
## 📌 **Kết Luận**
Workflow này không chỉ **giúp các sếp theo dõi an toàn hành tinh** mà còn **thú vị với cảnh báo khoa học viễn tưởng** và **dịch thuật tự động**. Với **tự động hóa 24/7**, các sếp sẽ **không bao giờ bỏ lỡ một hành tinh nguy hiểm** nữa!

**Hãy áp dụng ngay và trở thành "Chuyên gia Bảo Vệ Hành Tinh" của mình!** 🚀🌍

---
### **🔗 Tài Liệu Tham Khảo**
- [NASA API Documentation](https://api.nasa.gov/)
- [OpenAI API Guide](https://platform.openai.com/docs)
- [DeepL API](https://www.deepl.com/pro-api)
- [LINE Notify](https://notify-bot.line.me/)