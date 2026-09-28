---
title: "🍽️ **Tự Động Hóa Dự Báo Thừa Thực Đồ Ăn Cho Nhà Hàng Với Gemini AI + Google Sheets - Giảm Thừa Thực 30% Mà Không Cần Code!**"
description: "Workflow tự động hóa dự báo nhu cầu thực phẩm hàng ngày cho nhà hàng bằng AI Gemini, kết hợp với Google Sheets để tối ưu hóa quản lý hàng tồn kho và giảm thiểu thừa thực 30%. Giúp nhà hàng tiết kiệm chi phí, giảm thiểu lãng phí và nâng cao hiệu quả hoạt động."
slug: "tieu-bo-ha-dong-ai-forecast-food-waste-restaurant"
tags: [n8n, automation, ai-gemini, google-sheets, restaurant-management, no-code]
keywords: [tự động hóa nhà hàng, dự báo thừa thực, gemini ai, google sheets tự động, giảm lãng phí nhà hàng, workflow n8n]
---

# 🚀 **Dự Báo Thừa Thực Đồ Ăn Cho Nhà Hàng Với AI Gemini + Google Sheets**

## **🔥 Nỗi Đau Của Nhà Hàng: Thừa Thực Làm Lãng Phí Hàng Trăm Triệu Mỗi Tháng!**
Các sếp nhà hàng thường gặp phải vấn đề **thừa thực** do dự báo nhu cầu không chính xác, dẫn đến:
- **Lãng phí nguyên liệu** (thịt, rau, hải sản...) lên đến **30-50%** hàng tháng.
- **Chi phí quản lý tồn kho cao** vì mua quá nhiều hoặc quá ít.
- **Sản phẩm bị hỏng** do không bán được kịp thời.
- **Thời gian quản lý thủ công** mất nhiều giờ mỗi ngày.

**Giải pháp?** Một **workflow tự động hóa AI** dự báo nhu cầu thực phẩm hàng ngày, tối ưu hóa mua hàng và giảm thiểu thừa thực **mà không cần viết một dòng code nào!**

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
✅ **Giảm thừa thực 30%** – Dự báo chính xác nhu cầu hàng ngày.
✅ **Tiết kiệm chi phí nguyên liệu** – Mua đúng lượng, không thừa không thiếu.
✅ **Báo cáo tự động hàng ngày** – Email tổng hợp dự báo gửi trực tiếp cho quản lý.
✅ **Hoạt động 24/7** – Không cần can thiệp thủ công, chạy tự động mỗi ngày.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
- **Tài khoản Google Sheets** (để lưu dữ liệu lịch sử và dự báo).
- **Tài khoản Gmail** (để gửi báo cáo email tự động).
- **API Key Google Palm API** (để kết nối với **Gemini AI**).
- **Dữ liệu lịch sử bán hàng** (cần nhập vào Google Sheets trước khi chạy workflow).

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên **self-host n8n** trên VPS.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow từ JSON**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/5982](https://n8n.io/workflows/5982) và import vào **n8n Editor**.
- **Copy & Paste JSON** vào **Create Workflow** trong n8n.

### **2. Các Bước Cấu Hình Quan Trọng (BẮT BUỘC ĐIỀN)**

#### **🔹 Node 1: Daily Trigger (Động cơ kích hoạt hàng ngày)**
- **Cấu hình:** Chọn **Run every day at 8:00 AM** (hoặc thời gian phù hợp).

#### **🔹 Node 2 & 6: Google Sheets (Lấy dữ liệu & Lưu dự báo)**
- **Credentials:** Chọn **googleApi** (cần cấu hình trước trong n8n).
- **Sheet Name:** Điền tên **Google Sheet** chứa dữ liệu lịch sử bán hàng.
- **Range:** Điền **A1:Z1000** (hoặc phạm vi dữ liệu của bạn).
- **Operation (Node 6):** Chọn **Append** (thêm dữ liệu mới vào cuối sheet).

#### **🔹 Node 3: Format Data for AI Forecasting (Chuẩn hóa dữ liệu)**
- **Code cần chỉnh sửa (nếu cần):**
  ```javascript
  // Dữ liệu đầu vào từ Google Sheets
  const data = $input.all();

  // Chuẩn hóa dữ liệu thành format AI hiểu được
  const formattedData = {
    historicalSales: data.map(item => ({
      date: item.date,
      foodItem: item.foodItem,
      quantitySold: item.quantitySold
    })),
    currentDate: new Date().toISOString().split('T')[0]
  };

  return formattedData;
  ```

#### **🔹 Node 4 & 8: AI Forecast Generator (Dự báo nhu cầu với Gemini AI)**
- **Credentials:** Chọn **googlePalmApi** (cần API Key từ Google).
- **Prompt AI (cần chỉnh sửa):**
  ```plaintext
  "Bạn là một chuyên gia dự báo nhu cầu thực phẩm cho nhà hàng.
  Dựa trên dữ liệu lịch sử bán hàng (historicalSales), dự báo nhu cầu cho ngày {currentDate}.
  Trả về kết quả dưới dạng JSON với:
  - foodItem: Tên món ăn
  - predictedQuantity: Số lượng dự báo
  - wasteReductionTip: Gợi ý giảm thừa thực"
  ```

#### **🔹 Node 5: Clean & Structure AI Output (Chuẩn hóa kết quả AI)**
- **Code cần chỉnh sửa:**
  ```javascript
  // Lấy dữ liệu từ AI
  const aiResponse = $input.all()[0].json;

  // Chuẩn hóa thành format dễ đọc
  const structuredData = {
    date: new Date().toISOString().split('T')[0],
    predictions: aiResponse.predictions.map(item => ({
      foodItem: item.foodItem,
      predictedQuantity: item.predictedQuantity,
      wasteReductionTip: item.wasteReductionTip
    }))
  };

  return structuredData;
  ```

#### **🔹 Node 7: Send Email Forecast Report (Gửi báo cáo email tự động)**
- **Credentials:** Chọn **gmailOAuth2** (cần cấu hình OAuth 2.0 trong n8n).
- **Email To:** Điền địa chỉ email của quản lý nhà hàng.
- **Subject:** "Dự báo nhu cầu thực phẩm ngày {date}"
- **Body (HTML):**
  ```html
  <h2>Dự báo nhu cầu thực phẩm ngày {{ $json.date }}</h2>
  <table>
    <tr>
      <th>Món ăn</th>
      <th>Số lượng dự báo</th>
      <th>Gợi ý giảm thừa thực</th>
    </tr>
    {% for item in $json.predictions %}
    <tr>
      <td>{{ item.foodItem }}</td>
      <td>{{ item.predictedQuantity }}</td>
      <td>{{ item.wasteReductionTip }}</td>
    </tr>
    {% endfor %}
  </table>
  ```

---

### **⚡ Kích Hoạt Workflow**
1. **Test Run** với dữ liệu mẫu (đảm bảo tất cả node hoạt động).
2. **Bật Active** và workflow sẽ chạy tự động hàng ngày.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Kết Nối Với Slack/Telegram (Báo cáo thực thời)**
- Thêm **Node Slack/Telegram Webhook** sau **Node 7** để gửi thông báo ngay khi có dự báo mới.

### **2. Lưu Log Dự Báo (Để theo dõi hiệu quả)**
- Thêm **Node StickyNote** để ghi lại lịch sử dự báo và so sánh với thực tế.

### **3. Tự Động Cập Nhật Dữ Liệu (API Integration)**
- Nếu nhà hàng sử dụng **POS System** (như **Square, Toast**), có thể kết nối API để lấy dữ liệu bán hàng tự động.

### **4. Tối Ưu Hóa Prompt AI (Để Dự Báo Chính Xác Hơn)**
- Thử các **prompt khác nhau** để AI dự báo tốt hơn:
  ```plaintext
  "Dự báo dựa trên xu hướng mùa vụ, ngày lễ, và thời tiết (nếu có)."
  ```

---

## **📌 Kết Luận: Giảm Thừa Thực 30% Với AI – Không Cần Code!**
Workflow này **giải quyết vấn đề thừa thực** cho nhà hàng bằng cách:
✔ **Dự báo nhu cầu chính xác** với **Gemini AI**.
✔ **Tối ưu hóa mua hàng** để không thừa không thiếu.
✔ **Gửi báo cáo tự động** cho quản lý mỗi ngày.
✔ **Hoạt động 24/7** mà không cần can thiệp thủ công.

**🚀 Hành động ngay!**
1. **Import workflow** vào n8n.
2. **Cấu hình Google Sheets, Gmail và API Key**.
3. **Bật Active** và bắt đầu **giảm thừa thực 30% từ hôm nay!**

---
**💡 Cần hỗ trợ thêm?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để workflow chạy ổn định 24/7!