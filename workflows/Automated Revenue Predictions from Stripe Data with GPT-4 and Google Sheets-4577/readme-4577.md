---
title: "📈 **Tự Động Hóa Dự Báo Doanh Thu Tự Động Từ Stripe + GPT-4 + Google Sheets (Không Cần Code!)**"
description: "Workflow tự động hóa dự báo doanh thu hàng ngày từ dữ liệu Stripe, sử dụng trí tuệ nhân tạo GPT-4 để phân tích xu hướng và dự đoán doanh thu 3 tháng tới. Kết quả được lưu trữ trên Supabase và báo cáo trực quan trên Google Sheets. Giúp các sếp tiết kiệm thời gian lên đến 10 giờ/tuần và đưa ra quyết định kinh doanh chính xác hơn."
slug: "tự-dộng-hoa-du-bao-doanh-thu-stripe-gpt-4-google-sheets"
tags: [n8n, automation, ai, stripe, google-sheets, supabase, gpt-4, no-code, business-intelligence]
keywords: [tự động hóa dự báo doanh thu, n8n workflow stripe, dự báo doanh thu bằng AI, tự động hóa kinh doanh không code, google sheets + stripe + gpt-4, tự động hóa báo cáo doanh thu]
---

# 🚀 **Tự Động Hóa Dự Báo Doanh Thu Tự Động Từ Stripe + GPT-4 + Google Sheets**

## **💡 Giới Thiệu: Tại Sao Các Sếp Cần Workflow Này?**
Hàng ngày, các sếp phải mất **giờ đồng hồ** để:
- **Tổng hợp dữ liệu giao dịch** từ Stripe (thường là thủ công hoặc qua Excel).
- **Phân tích xu hướng** bằng cách so sánh dữ liệu qua nhiều tháng.
- **Dự báo doanh thu** cho quý tới dựa trên kinh nghiệm cá nhân (có thể sai lệch đến 20-30%).
- **Báo cáo kết quả** cho ban lãnh đạo, thường là sau khi làm việc đến khuya.

**Kết quả?** Quá trình này **chậm, dễ sai sót, và không thể tự động hóa** – cho đến bây giờ.

**Workflow này giải quyết tất cả:**
✅ **Tự động lấy dữ liệu giao dịch** từ Stripe trong vòng **5 phút/ngày**.
✅ **Sử dụng GPT-4 để dự báo doanh thu** với độ chính xác cao (thay vì dựa vào cảm nhận).
✅ **Lưu trữ và báo cáo tự động** trên Google Sheets và Supabase, giúp **quan sát xu hướng dài hạn**.
✅ **Hoạt động 24/7** – không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo **tính bảo mật và ổn định**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**).
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow này).
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần** (không cần tổng hợp dữ liệu thủ công).
- **Dự báo doanh thu chính xác** (GPT-4 phân tích xu hướng thay vì con người).
- **Báo cáo tự động** trên Google Sheets (sẵn sàng cho cuộc họp bất kỳ).
- **Lưu trữ dữ liệu dài hạn** trên Supabase (so sánh với các quý trước).
- **Cập nhật liên tục** (không cần chạy lại thủ công).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✅ **Tài khoản Stripe** (API Key) để lấy dữ liệu giao dịch.
✅ **Tài khoản OpenAI** (API Key) để sử dụng GPT-4.
✅ **Tài khoản Supabase** (để lưu trữ dữ liệu dự báo).
✅ **Tài khoản Google Sheets** (để báo cáo kết quả).
✅ **Tài khoản Pinecone** (nếu muốn sử dụng **tính năng nhớ dài hạn** của AI).

---
## 🚀 **Cách Import & Lưu ý khi "Lên đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/4577](https://n8n.io/workflows/4577) (chọn **Export as JSON**).
2. **Mở n8n Editor** (trên máy hoặc VPS).
3. Nhấn **Import** → Chọn file JSON vừa tải → **Import**.

#### **Cách 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/4577](https://n8n.io/workflows/4577).
2. Trong **n8n Editor**, nhấn **Import** → Chọn **Paste JSON** → Dán và **Import**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Node `Run Daily Forecast` (Schedule Trigger)**
- **Cấu hình lịch chạy:**
  - **Schedule:** `0 6 * * *` (chạy hàng ngày lúc 6h sáng UTC).
  - **Ghi chú:** Các sếp có thể điều chỉnh thời gian phù hợp với giờ làm việc của mình.

#### **🔹 Node `Fetch Stripe Charges`**
- **Cấu hình API Stripe:**
  - **Resource:** `Charges` (lấy tất cả giao dịch).
  - **Filters:**
    - `created[gte]`: Lấy dữ liệu trong **30 ngày gần nhất** (cấu hình: `created[gte]=$(date -d "30 days ago" +%Y-%m-%d)`).
    - `status: succeeded` (chỉ lấy giao dịch thành công).
  - **Optional:** Bật `data.customer` để lấy thông tin khách hàng (nếu cần phân tích chi tiết).

#### **🔹 Node `Summarize Daily Sales` (Code Node)**
- **Mã JavaScript mặc định:**
  ```javascript
  // Chuyển đổi Unix timestamp thành định dạng YYYY-MM-DD
  const formatDate = (timestamp) => {
    const date = new Date(timestamp * 1000);
    return date.toISOString().split('T')[0];
  };

  // Tính tổng doanh thu theo ngày
  const dailySales = {};
  $input.all().forEach(charge => {
    const date = formatDate(charge.created);
    const amount = charge.amount / 100; // Stripe trả về cent, chuyển thành USD
    if (!dailySales[date]) dailySales[date] = 0;
    dailySales[date] += amount;
  });

  return { json: dailySales };
  ```
  - **Không cần chỉnh sửa** nếu muốn sử dụng mặc định.

#### **🔹 Node `Prepare Forecast Prompt`**
- **Cấu hình prompt:**
  ```plaintext
  Given the following sales data:
  { "2025-05-01": 1245.50, "2025-05-02": 980.00 }

  Predict trends and forecast sales for the next 3 months (June, July, August).
  Provide:
  1. Forecasted revenue for each month (in USD).
  2. Overall trend (Increasing/Decreasing/Stable).
  3. Confidence level (High/Medium/Low).
  4. Key insights (e.g., "Sales rising due to new product X").
  ```
  - **Không cần chỉnh sửa** nếu muốn sử dụng mặc định.

#### **🔹 Node `Forecaster Agent` (LangChain Agent)**
- **Cấu hình AI:**
  - **Model:** `gpt-4o-mini` (rẻ hơn `gpt-4` nhưng vẫn hiệu quả).
  - **Output Parser:** `Structured Output Parser` (đảm bảo kết quả là JSON).
  - **Không cần chỉnh sửa** nếu muốn sử dụng mặc định.

#### **🔹 Node `Save Forecast to Supabase`**
- **Cấu hình bảng `forecasts`:**
  - **Table Name:** `forecasts` (nếu chưa có, tạo mới).
  - **Columns:**
    - `timestamp` (timestamp khi dự báo).
    - `raw_data` (dữ liệu gốc từ Stripe).
    - `forecast_data` (kết quả dự báo từ GPT-4).
  - **Example SQL:**
    ```sql
    CREATE TABLE forecasts (
      id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
      timestamp TIMESTAMPTZ NOT NULL,
      raw_data JSONB NOT NULL,
      forecast_data JSONB NOT NULL
    );
    ```

#### **🔹 Node `Log Forecast in Google Sheets`**
- **Cấu hình Google Sheets:**
  - **File:** Chọn **Google Sheet** đã tạo (ví dụ: `Dự báo doanh thu`).
  - **Sheet Name:** `Forecast` (nếu chưa có, tạo mới).
  - **Headers:**
    | Date       | Forecast (USD) | Trend      | Confidence | Insights                   |
    |------------|----------------|------------|------------|----------------------------|
    | 2025-05-29 | $15,000.00     | Increasing | High       | Sales rising at 10% weekly  |

---

### **3. Kích hoạt ⚡️**
1. **Test Run (Kiểm tra trước khi chạy thực tế):**
   - Nhấn **Run Workflow** và chọn **Test Run**.
   - Kiểm tra **Google Sheets** và **Supabase** xem dữ liệu có được cập nhật không.
2. **Bật Active:**
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động hàng ngày.

---

## ✍️ **Mẹo & Gợi ý Nâng Cao**

### **🔹 Tích hợp Slack/Telegram để báo cáo tự động**
- **Sử dụng Node `Slack` hoặc `Telegram Bot`** để gửi kết quả dự báo hàng ngày.
- **Ví dụ:**
  ```plaintext
  "📊 Dự báo doanh thu tháng 6: $15,000 (Tăng 10% so với tháng 5)."
  "🔍 Xu hướng: Tăng trưởng mạnh do sản phẩm X."
  ```

### **🔹 Lưu log hoạt động để theo dõi lỗi**
- **Sử dụng Node `Sticky Note`** để ghi lại lỗi hoặc thông báo debug.
- **Ví dụ:**
  ```json
  {
    "timestamp": "$datetime",
    "status": "success/failure",
    "error": "null" (nếu có lỗi)
  }
  ```

### **🔹 Tự động gửi báo cáo định kỳ cho ban lãnh đạo**
- **Sử dụng Node `Email` (n8n-nodes-base.email)** để gửi báo cáo hàng tuần.
- **Ví dụ:**
  ```plaintext
  "Kính gửi Ban Giám đốc,
  Dự báo doanh thu quý 3: $45,000 (Tăng 15% so với dự báo trước).
  Xem chi tiết tại: [Link Google Sheets].
  Trân trọng,"
  ```

### **🔹 Sử dụng Pinecone để cải thiện dự báo dài hạn**
- **Nếu muốn AI "nhớ" dữ liệu cũ**, bật **`Store Context in Pinecone`** và **`Generate Embeddings`**.
- **Lợi ích:** AI sẽ phân tích **xu hướng dài hạn** thay vì chỉ dựa trên dữ liệu gần đây.

---

## 📌 **Kết Luận: Bắt Đầu Tự Động Hóa Ngay!**

Workflow này **giải phóng thời gian** của các sếp để tập trung vào **quyết định chiến lược** thay vì làm việc thủ công. Với **GPT-4 và tự động hóa hoàn toàn**, dự báo doanh thu trở nên **chính xác, nhanh chóng và dễ dàng theo dõi**.

**Bước đầu tiên:**
1. **Import workflow** vào n8n (trên VPS).
2. **Cấu hình API Keys** (Stripe, OpenAI, Supabase, Google Sheets).
3. **Test Run** và **bật Active**.
4. **Xem kết quả** trên Google Sheets mỗi sáng!

**🚀 Hãy tự động hóa dự báo doanh thu của mình ngay hôm nay!**

---
**📌 Ghi chú cuối:**
- **Nếu gặp vấn đề**, các sếp có thể liên hệ với tác giả **Yaron Been** qua:
  - [LinkedIn](https://www.linkedin.com/in/yaronbeen/)
  - [YouTube](https://www.youtube.com/@YaronBeen/videos)
- **Cần hỗ trợ cài đặt n8n trên VPS?** Liên hệ [TinoHost](https://tino.vn) hoặc [BNIX](https://my.bnix.one) để được tư vấn chi tiết!