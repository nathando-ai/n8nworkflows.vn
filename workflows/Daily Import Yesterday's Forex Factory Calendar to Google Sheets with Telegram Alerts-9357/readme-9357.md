---
title: "📊 Tự Động Nhập Lịch Kinh Tế Forex Factory Hôm Trước Vào Google Sheets Với Thông Báo Telegram Tự Động"
description: "Workflow tự động hóa nhập dữ liệu lịch kinh tế Forex Factory hàng ngày vào Google Sheets, phân loại theo mức độ ảnh hưởng và gửi cảnh báo Telegram cho các tin tức quan trọng. Giúp các nhà đầu tư và trader theo dõi thị trường 24/7 mà không cần làm thủ công."
slug: "tu-dong-nhap-lich-kinh-te-forex-into-google-sheets-telegram"
tags: [n8n, automation, forex, trading, google-sheets, telegram-alerts, api-integration]
keywords: [tự động hóa forex, nhập dữ liệu forex factory, cảnh báo telegram, google sheets automation, n8n workflow forex]
---

# 🚀 Tự Động Nhập Lịch Kinh Tế Forex Factory Hôm Trước Vào Google Sheets Với Thông Báo Telegram

### 🔍 **Nỗi Đau Của Các Nhà Đầu Tư Forex**
Hàng ngày, các nhà đầu tư và trader phải dành thời gian quét qua **Forex Factory Calendar** để theo dõi các tin tức kinh tế quan trọng như:
- **Thông tin dự báo và thực tế** về chỉ số GDP, lãi suất, tỷ giá...
- **Mức độ ảnh hưởng** (High/Medium/Low) của mỗi tin tức đến thị trường.
- **Thời gian và ngày** xuất bản để lập kế hoạch giao dịch.

**Làm thủ công?** Tốn thời gian, dễ bỏ lỡ tin tức quan trọng, và không thể theo dõi liên tục 24/7. **Workflow này giải quyết tất cả!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần quét thủ công Forex Factory hàng ngày.
- **Phân loại tự động**: Tin tức **High/Medium** được gửi Telegram, **Low** được lưu vào Google Sheets riêng biệt.
- **Dữ liệu chính xác**: Dữ liệu được lấy trực tiếp từ API Forex Factory, không sai sót.
- **Hoạt động liên tục**: Workflow chạy tự động hàng ngày, ngay cả khi các sếp ngủ.
- **Tích hợp hoàn hảo**: Dữ liệu sẵn sàng để phân tích trên Google Sheets hoặc kết nối với các tool khác (TradingView, MetaTrader...).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Forex Factory API** (đăng ký tại [RapidAPI](https://rapidapi.com/api/forex-factory-calendar)).
2. **Tài khoản Google Sheets** với quyền chỉnh sửa:
   - **2 Sheet riêng biệt**:
     - *High Impact Sheet* (để tin tức **High/Medium**).
     - *Low Impact Sheet* (để tin tức **Low**).
   - **Mã API Google Sheets** (tạo tại [Google Cloud Console](https://console.cloud.google.com/)).
3. **Tài khoản Telegram**:
   - **Chat ID** (tạo tại [@BotFather](https://t.me/BotFather)).
   - **Token API Telegram** (để workflow gửi thông báo).
4. **VPS hoặc máy chủ n8n** (để workflow chạy 24/7).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/9357](https://n8n.io/workflows/9357).
- **Mở n8n Editor** và chọn **Import Workflow** → Chọn file JSON vừa tải.
- **Hoặc copy/paste** JSON từ file vào Editor (đảm bảo không có lỗi cú pháp).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này gồm **9 node** quan trọng, các sếp cần cấu hình như sau:

##### **A. Node "Schedule Trigger: Daily Triggers"**
- **Thiết lập thời gian chạy**: Chọn **00:00 UTC** (hoặc thời gian phù hợp) để workflow chạy hàng ngày vào **giờ mở cửa thị trường** (khoảng 8h sáng UTC+7).
- **Lưu ý**: Nếu chạy trên VPS tại Việt Nam, hãy điều chỉnh UTC để phù hợp với giờ Việt Nam (UTC+7).

##### **B. Node "Get calendar from Forex Factory" (HTTP Request)**
- **URL API**: `https://api.rapidapi.com/forex_factory_calendar/calendar`
- **Headers**:
  - `x-rapidapi-key`: Điền **API Key** từ RapidAPI (mua tại [RapidAPI](https://rapidapi.com/api/forex-factory-calendar)).
  - `x-rapidapi-host`: `forex-factory-calendar.p.rapidapi.com`.
- **Tham số (Query Parameters)**:
  - `date`: `{{ $node["Schedule Trigger: Daily Triggers"].json()["date"] }}` (để lấy ngày hôm trước).

##### **C. Node "Convert month name to number" (Code)**
- **Mã JavaScript**:
  ```javascript
  // Chuyển tháng từ dạng "January" thành số (1-12)
  const monthMap = {
    "January": 1, "February": 2, "March": 3, "April": 4, "May": 5, "June": 6,
    "July": 7, "August": 8, "September": 9, "October": 10, "November": 11, "December": 12
  };
  const monthName = $input.all()[0].date.split('-')[1];
  $output.all() = [{
    ...$input.all()[0],
    monthNumber: monthMap[monthName]
  }];
  ```
- **Lưu ý**: Node này chuyển đổi tháng từ dạng văn bản (ví dụ: "January") thành số (1) để dễ xử lý trong Google Sheets.

##### **D. Node "Filter High Impact News" (Filter)**
- **Cấu hình**:
  - **Condition**: `$item.impact === "High" || $item.impact === "Medium"`.
  - **Action**: Chỉ giữ lại tin tức có **impact = High/Medium**.

##### **E. Node "Telegram"**
- **Thiết lập**:
  - **Credentials**: Chọn `telegramApi` (đã cấu hình trước).
  - **Message Template**:
    ```
    🚨 **High Impact News Alert!** 🚨
    **Date:** {{ $node["Aggregate"].json()["date"] }}
    **Currency:** {{ $node["Aggregate"].json()["currency"] }}
    **Time:** {{ $node["Aggregate"].json()["time"] }}
    **Impact:** {{ $node["Aggregate"].json()["impact"] }}
    **News:** {{ $node["Aggregate"].json()["newsTitle"] }}
    ```
  - **Chat ID**: Điền **Chat ID** của bot Telegram (tạo tại [@BotFather](https://t.me/BotFather)).

##### **F. Node "Append to Google Sheets" (2 node)**
- **High Impact Sheet**:
  - **Credentials**: Chọn `googleApi`.
  - **Sheet Name**: Điền tên **High Impact Sheet**.
  - **Range**: `A1` (để dữ liệu bắt đầu từ ô A1).
  - **Values**: Chọn **JSON to Rows** và cấu hình:
    ```json
    [
      ["Date", "Time", "Currency", "Impact", "News Title", "Forecast", "Actual", "Previous"]
    ]
    ```
- **Low Impact Sheet**:
  - **Credentials**: Chọn `googleApi`.
  - **Sheet Name**: Điền tên **Low Impact Sheet**.
  - **Range**: `A1`.
  - **Values**: Cấu hình tương tự, nhưng chỉ lấy tin tức **impact = Low**.

##### **G. Node "Aggregate"**
- **Thiết lập**:
  - **Group By**: `currency` (để nhóm tin tức theo đồng tiền).
  - **Output**: Chọn **JSON Path** để lấy dữ liệu đầy đủ.

##### **H. Node "If" (Lọc tin tức)**
- **Condition**:
  - Nếu `item.impact === "High"` → Gửi Telegram.
  - Nếu `item.impact === "Low"` → Append vào Low Impact Sheet.
  - Nếu `item.impact === "Medium"` → Append vào High Impact Sheet.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Chọn **Run Workflow** và kiểm tra:
    - Dữ liệu có được lấy từ Forex Factory không?
    - Telegram có nhận được thông báo không?
    - Google Sheets có cập nhật dữ liệu không?
- **Bật Active**:
  - Sau khi kiểm tra thành công, **bật Active** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp với TradingView/Pine Script**:
   - Sau khi dữ liệu được lưu vào Google Sheets, các sếp có thể **kết nối với TradingView** để tự động vẽ biểu đồ dựa trên tin tức kinh tế.
   - Ví dụ: Sử dụng **Google Apps Script** để gửi dữ liệu từ Sheets vào TradingView.

2. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Schedule Trigger** để gửi **báo cáo tuần/month** về các tin tức quan trọng qua Email hoặc Telegram.
   - Cấu hình node **Email** hoặc **Telegram** với template báo cáo chi tiết.

3. **Lưu Log Dữ Liệu**:
   - Thêm node **Google Drive** hoặc **AWS S3** để lưu **log lịch sử** của workflow.
   - Giúp các sếp theo dõi và phân tích dữ liệu lâu dài.

4. **Cảnh Báo Trước Thời Gian**:
   - Sử dụng **n8n Webhook** để nhận thông báo từ Forex Factory về các tin tức sắp tới (ví dụ: 1 giờ trước tin tức quan trọng).
   - Cấu hình node **HTTP Request** để lấy dữ liệu và gửi cảnh báo sớm.

5. **Tích Hợp với MetaTrader 4/5**:
   - Sau khi dữ liệu được lưu vào Sheets, các sếp có thể **kết nối với MetaTrader** để tự động mở/đóng vị thế dựa trên tin tức kinh tế.
   - Sử dụng **API MetaTrader** hoặc **Google Apps Script** để tự động hóa.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các nhà đầu tư và trader, giúp họ **tự động hóa việc theo dõi tin tức Forex** mà không cần làm thủ công. Với **cảnh báo Telegram** và **dữ liệu phân loại** trên Google Sheets, các sếp có thể:
✅ **Đầu tư thông minh** với dữ liệu chính xác.
✅ **Không bỏ lỡ tin tức quan trọng** nhờ cảnh báo tự động.
✅ **Tiết kiệm thời gian** để tập trung vào chiến lược giao dịch.

**Hãy import workflow ngay hôm nay và bắt đầu tự động hóa Forex của mình!** 🚀

---
**💡 Gợi ý thêm**: Nếu các sếp muốn **cải tiến workflow**, có thể thêm node **LLM (AI)** để tự động phân tích **tác động của tin tức** đến thị trường và gửi báo cáo chi tiết.