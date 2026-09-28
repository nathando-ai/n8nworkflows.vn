---
title: "🚨 **Hệ Thống Dò Tìm Khủng Hoảng Giá Dầu Thời Thực Với AI Qwen-32B & Cảnh Báo Multi-Channel**"
description: "Workflow tự động hóa 24/7 cảnh báo khủng hoảng giá dầu từ dữ liệu thị trường, báo cáo OPEC, vận tải biển và tin tức thời sự. Sử dụng AI Qwen-32B phân tích nguy cơ geopolitical, tính điểm nguy cơ và gửi cảnh báo tức thời qua Email, Slack và Dashboard. Giảm thiểu thời gian phản ứng 90% so với cách thủ công."
slug: "huyet-thong-dau-khung-hoang-ai-qwen-32b"
tags: [n8n, automation, crypto-trading, ai-summarization, alert-system, oil-price, geopolitical-risk]
keywords: [n8n workflow giá dầu, cảnh báo khủng hoảng dầu mỏ, tự động hóa phân tích thị trường, AI Qwen-32B, cảnh báo Slack Email, dữ liệu OPEC vận tải biển]
---

# 🚨 **Hệ Thống Dò Tìm Khủng Hoảng Giá Dầu Thời Thực Với AI Qwen-32B & Cảnh Báo Multi-Channel**

## **🔥 Nỗi Đau Của Các Sếp Trong Thị Trường Dầu Mỏ**
Giá dầu là một trong những chỉ số kinh tế nhạy cảm nhất thế giới, ảnh hưởng trực tiếp đến giá xăng dầu, sản xuất công nghiệp và thậm chí là ổn định chính trị. Tuy nhiên, việc theo dõi **giá dầu thời thực, báo cáo OPEC, dữ liệu vận tải biển và tin tức thời sự** để phát hiện **khủng hoảng sắp xảy ra** là một công việc **mệt mỏi, tốn thời gian và dễ bỏ lỡ dấu hiệu cảnh báo**.

- **Thời gian phản ứng chậm**: Các sếp thường phải **quét qua hàng chục nguồn dữ liệu** (API, báo cáo, tin tức) để phát hiện bất thường.
- **Rủi ro geopolitical**: Các xung đột, lệnh cấm vận hoặc thay đổi chính sách của OPEC có thể **làm giật giá dầu trong vài phút**, nhưng khó phát hiện nếu không có hệ thống tự động.
- **Dữ liệu phân tán**: Giá dầu trên các sàn giao dịch khác nhau, dữ liệu vận tải biển, và tin tức từ nhiều nguồn khác nhau **không được tích hợp**, dẫn đến phân tích không đầy đủ.
- **Không có cảnh báo tức thời**: Khi giá dầu **bất ngờ tăng/giảm**, các sếp thường **muộn màng** trong việc điều chỉnh chiến lược.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động thu thập dữ liệu** từ API giá dầu, báo cáo OPEC, vận tải biển và tin tức **mỗi 5 phút**.
✅ **Phân tích AI Qwen-32B** để đánh giá **nguy cơ geopolitical** và tính điểm nguy cơ khủng hoảng.
✅ **Cảnh báo tức thời** qua **Email, Slack và Dashboard** khi có dấu hiệu bất thường.
✅ **Lưu lịch sử cảnh báo** để theo dõi xu hướng và tối ưu hóa quyết định.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Giảm thời gian phản ứng 90%** so với cách thủ công (không cần quét dữ liệu mỗi ngày).
- **Phát hiện khủng hoảng sớm** nhờ phân tích **giá dầu, vận tải biển và tin tức** đồng thời.
- **Cảnh báo tức thời** khi giá dầu bất ngờ biến động (được AI phân tích nguy cơ geopolitical).
- **Tối ưu hóa quyết định** với **điểm nguy cơ tự động** (thấp, trung bình, cao, khẩn cấp).
- **Lưu trữ lịch sử cảnh báo** để phân tích sau này và tránh lặp lại sai lầm.
- **Tích hợp đa kênh** (Email, Slack, Dashboard) để phản ứng nhanh chóng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI SỬ DỤNG**]
Để workflow hoạt động, các sếp cần chuẩn bị:
✔ **API Key cho các nguồn dữ liệu:**
   - **API giá dầu** (ví dụ: [Coingecko](https://www.coingecko.com/en/api), [Kraken](https://www.kraken.com/))
   - **Báo cáo OPEC** (có thể lấy từ [OPEC Website](https://www.opec.org/))
   - **Dữ liệu vận tải biển** (API như [MarineTraffic](https://www.marinetraffic.com/))
   - **Tin tức thời sự** (API như [NewsAPI](https://newsapi.org/))

✔ **API Key cho AI Qwen-32B** (trên [OpenRouter](https://openrouter.ai/))
✔ **Credentials cho Email & Slack:**
   - **Gmail OAuth2** (để gửi Email cảnh báo)
   - **Slack OAuth2** (để gửi tin nhắn cảnh báo)
✔ **Database PostgreSQL** (để lưu lịch sử cảnh báo)
✔ **Dashboard API** (nếu muốn hiển thị cảnh báo trên bảng điều khiển)
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow từ file JSON** hoặc **copy/paste JSON vào n8n Editor**:
- **Tải file JSON** từ [n8n.io/workflows/10763](https://n8n.io/workflows/10763) (nếu link vẫn hoạt động).
- **Nếu không tải được**, các sếp có thể **copy toàn bộ JSON từ canvas** và dán vào **n8n Editor** (trong tab "Import").

:::note[**Lưu ý khi import**]
- **Không thay đổi tên node** (nếu không muốn lỗi kết nối).
- **Kiểm tra lại cấu hình credentials** sau khi import (xem phần sau).
:::

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node "OpenRouter Chat Model" (AI Qwen-32B)**
- **Cấu hình API Key**:
  - Đi đến **Settings > Credentials** trong n8n.
  - Tạo **mới một credential** với tên `openRouterApi`.
  - Điền **API Key** từ [OpenRouter](https://openrouter.ai/) vào trường `apiKey`.
  - Chọn **model**: `qwen/qwq-32b` (đã được cấu hình sẵn trong workflow).

- **Prompt AI**:
  - Workflow đã cấu hình sẵn **prompt** để AI phân tích **nguy cơ geopolitical** và **tính điểm nguy cơ**.
  - **Không cần chỉnh sửa** trừ khi các sếp muốn **tùy chỉnh logic phân tích**.

#### **🔹 Node "Fetch Oil Price Data (API)"**
- **Cấu hình URL API**:
  - Thay đổi **URL** trong node này thành **API giá dầu** mà các sếp đang sử dụng (ví dụ: `https://api.coingecko.com/api/v3/simple/price?ids=bitcoin&vs_currencies=usd`).
  - **Response Format**: Đảm bảo API trả về **giá dầu spot, futures** dưới dạng JSON.

#### **🔹 Node "Fetch OPEC Reports"**
- **Nguồn dữ liệu OPEC**:
  - Các sếp có thể lấy **báo cáo PDF/JSON** từ [OPEC Website](https://www.opec.org/).
  - Nếu API không sẵn có, có thể **scrape dữ liệu** bằng Python và **gửi qua HTTP Request**.

#### **🔹 Node "Fetch Shipping Data"**
- **API MarineTraffic**:
  - Đăng ký API key tại [MarineTraffic](https://www.marinetraffic.com/en/api).
  - Thay đổi **URL** trong node thành:
    ```json
    https://api.marinetraffic.com/data/read/api/vshiptracking/v3/json/VesselPositions?vesselName=**NAME**&token=**API_KEY**
    ```

#### **🔹 Node "Fetch News Feed"**
- **API NewsAPI**:
  - Đăng ký API key tại [NewsAPI](https://newsapi.org/).
  - Thay đổi **URL** trong node thành:
    ```json
    https://newsapi.org/v2/everything?q=dầu+mỏ&apiKey=**API_KEY**
    ```

#### **🔹 Node "PostgreSQL" (Lưu lịch sử cảnh báo)**
- **Cấu hình kết nối**:
  - Tạo **một database PostgreSQL** mới.
  - Thêm **table** với các cột:
    ```sql
    CREATE TABLE alert_history (
      id SERIAL PRIMARY KEY,
      timestamp TIMESTAMP,
      alert_level VARCHAR(20),
      reason TEXT,
      data JSONB
    );
    ```
  - Trong node **PostgreSQL**, điền:
    - **Host**: `localhost` (hoặc IP VPS nếu self-hosted)
    - **Port**: `5432`
    - **Database**: Tên database của bạn
    - **User & Password**: Credentials PostgreSQL

#### **🔹 Node "Send Email Alert" & "Send Slack Alert"**
- **Gmail OAuth2**:
  - Đăng nhập vào **Settings > Credentials** trong n8n.
  - Tạo **mới credential** với tên `gmailOAuth2`.
  - Chọn **Gmail** và **đăng nhập tài khoản Email** để gửi cảnh báo.
- **Slack OAuth2**:
  - Tạo **App Slack** tại [Slack API](https://api.slack.com/apps).
  - Chọn **Bot Token** và **đăng ký credential** trong n8n với tên `slackOAuth2Api`.

#### **🔹 Node "Route by Alert Level" (Switch)**
- **Cấu hình ngưỡng cảnh báo**:
  - Workflow đã định nghĩa **4 mức cảnh báo**:
    - **1-2**: Thông báo (Email)
    - **3-4**: Cảnh báo (Slack + Dashboard)
    - **5-6**: Cảnh báo cao (Slack + Email)
    - **7-10**: Khẩn cấp (Slack + Email + Dashboard)
  - **Không cần chỉnh sửa** trừ khi các sếp muốn **đổi ngưỡng**.

#### **🔹 Node "Schedule Every 5 Minutes"**
- **Không cần chỉnh sửa** (đã cấu hình sẵn).
- **Lưu ý**: Nếu self-hosted trên VPS, **đảm bảo n8n chạy 24/7**.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với **dữ liệu mẫu**:
   - Chạy **manual execution** để kiểm tra:
     - Dữ liệu API được fetch đúng không?
     - AI phân tích nguy cơ có logic không?
     - Cảnh báo được gửi đến Email/Slack không?
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật workflow** để chạy tự động mỗi **5 phút**.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **🔹 Tích Hợp với Dashboard (Power BI / Grafana)**
- **Gửi dữ liệu cảnh báo** đến **Power BI** hoặc **Grafana** để **hiển thị biểu đồ xu hướng giá dầu và nguy cơ**.
- **Cách làm**:
  - Thay đổi node **"Send to Dashboard API"** thành **API của Power BI/Grafana**.
  - Ví dụ:
    ```json
    POST https://api.powerbi.com/v1.0/myorg/groups/{groupId}/datasets/{datasetId}/rows
    ```

### **🔹 Gửi Cảnh Báo qua Telegram**
- **Thêm node Telegram Bot**:
  - Tạo **bot Telegram** tại [BotFather](https://t.me/BotFather).
  - Thêm **node HTTP Request** mới để gửi tin nhắn:
    ```json
    POST https://api.telegram.org/bot{TOKEN}/sendMessage?chat_id={CHAT_ID}&text={{$json["message"]}}
    ```

### **🔹 Lưu Log Cảnh Báo vào Google Sheets**
- **Thêm node Google Sheets**:
  - Tạo **một sheet mới** với các cột: `Timestamp, Alert Level, Reason, Data`.
  - Thêm **node Google Sheets** và cấu hình:
    - **Spreadsheet ID**: ID của sheet bạn tạo.
    - **Sheet Name**: Tên sheet (ví dụ: `Alert_Log`).
    - **Range**: `A1` (để ghi dữ liệu từ hàng 1).

### **🔹 Tự động Gửi Báo Cáo Định Kỳ (Hàng Tuần)**
- **Thêm node Schedule Trigger mới**:
  - Cấu hình **run hàng tuần** (ví dụ: Chủ Nhật 8h sáng).
  - **Gửi Email tổng kết** với:
    - **Danh sách cảnh báo gần đây**.
    - **Xu hướng giá dầu trong tuần**.
    - **Điểm nguy cơ cao nhất**.

### **🔹 Tùy Chỉnh AI Qwen-32B**
- **Nếu muốn cải thiện logic phân tích**:
  - Chỉnh sửa **prompt** trong node `OpenRouter Chat Model` để:
    - **Tăng trọng số** cho một loại nguy cơ nhất định (ví dụ: xung đột Trung Đông).
    - **Thêm dữ liệu mới** (ví dụ: giá xăng dầu, dự trữ dầu thế giới).

---

## 📌 **Kết Luận: Áp Dụng Ngay Để Tránh Thiệt Hại**

Workflow này **không chỉ cảnh báo khi giá dầu biến động**, mà còn **phân tích nguyên nhân** (geopolitical, vận tải, tin tức) và **đánh giá nguy cơ** bằng AI Qwen-32B. **Kết quả:**
✔ **Traders** có thể **điều chỉnh vị thế** trước khi thị trường sụp đổ.
✔ **Doanh nghiệp** tránh **thiệt hại từ biến động giá xăng dầu**.
✔ **Công ty vận tải** dự đoán **đường hàng hải bị gián đoạn**.
✔ **Cơ quan chính phủ** **phát hiện nguy cơ khủng hoảng sớm**.

**🚀 Hành động ngay:**
1. **Self-host n8n trên VPS** (để workflow chạy 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
2. **Import workflow** và