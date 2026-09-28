---
title: "🏠 Tự Động So Sánh Giá Thương Mại Cho Thương Mại Nhà Đất Từ Zillow, HUD FMR & Rentometer Với GPT-4.1"
description: "Workflow tự động hóa so sánh giá thuê nhà từ 3 nguồn uy tín (Zillow, HUD FMR, Rentometer) và tổng hợp báo cáo chi tiết bằng trí tuệ nhân tạo, giúp các sếp tiết kiệm thời gian nghiên cứu thị trường và đưa ra quyết định chính xác hơn chỉ trong vài giây."
slug: "tieu-dong-so-sanh-gia-thue-nhat-dat"
tags: [n8n, automation, ai-chatbot, market-research, no-code]
keywords: [tự động hóa so sánh giá thuê nhà, n8n workflow, AI phân tích thị trường bất động sản, Zillow API, HUD FMR API, Rentometer API]
---

# 🚀 **Tự Động So Sánh Giá Thương Mại Cho Thương Mại Nhà Đất Với AI**

### **Giải Phóng Tay Các Sếp Từ Công Việc So Sánh Giá Thuê Nhà Bằng Tay!**
Hiện nay, khi muốn đánh giá giá trị thuê nhà cho một địa chỉ cụ thể, các sếp phải mất thời gian quét qua **Zillow, Rentometer, và HUD Fair Market Rent** để so sánh dữ liệu. Quá trình này không chỉ tốn thời gian mà còn dễ mắc sai sót do thiếu thống nhất hoặc thiếu thông tin chi tiết. **Workflow này tự động hóa toàn bộ quy trình**, giúp bạn nhận được **báo cáo so sánh giá thuê nhà chính xác, được tổng hợp bởi GPT-4.1** chỉ sau khi nhập địa chỉ nhà.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 mà không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng. Đây là giải pháp tối ưu nhất để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần quét qua nhiều trang web thủ công.
- **Dữ liệu chính xác**: So sánh từ **3 nguồn uy tín** (Zillow, HUD FMR, Rentometer).
- **Báo cáo tự động hóa**: AI tổng hợp thành **bảng so sánh chi tiết** với định dạng sạch sẽ.
- **Cập nhật liên tục**: Hoạt động 24/7, không phụ thuộc vào giờ làm việc.
- **Tối ưu quyết định**: Giúp các sếp **lựa chọn địa chỉ thuê nhà phù hợp** với ngân sách và nhu cầu.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **API Key Zillow** (sử dụng `maxcopell/zillow-detail-scraper` trên Apify).
2. **API Key HUD** (đăng ký miễn phí tại [huduser.gov](https://www.huduser.gov/hudapi/public/register)).
3. **API Key Rentometer** (đăng ký tại [Rentometer API](https://www.rentometer.com/api)).
4. **API Key OpenAI** (để sử dụng GPT-4.1 trong quá trình phân tích).

:::warning[⚠️ LƯU Ý QUAN TRỌNG]
**Không thể chạy workflow nếu thiếu bất kỳ API Key nào!** AI Agent sẽ **không hoạt động** hoặc trả về kết quả không đầy đủ.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Mở **n8n Workflow Editor**.
2. Nhấn **Import** và chọn file JSON đã tải xuống từ [n8n.io/workflows/15472](https://n8n.io/workflows/15472).
   *Hoặc* copy toàn bộ JSON và dán vào **Import Workflow** trong Editor.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này bao gồm **7 node chính**, các sếp cần cấu hình kỹ lưỡng như sau:

##### **🔹 Node "When chat message received" (chatTrigger)**
- **Chức năng**: Nhận địa chỉ nhà từ người dùng qua chat (Slack, Telegram, Discord...).
- **Cấu hình**:
  - Chọn **credentials** phù hợp (ví dụ: Slack Webhook hoặc Telegram Bot Token).
  - Đảm bảo **message format** là JSON với trường `address`.

##### **🔹 Node "AI Agent1" (agent)**
- **Chức năng**: Quản lý toàn bộ quy trình gọi API và tổng hợp kết quả.
- **Cấu hình**:
  - **Không cần thay đổi** (AI Agent sẽ tự động gọi các tool theo thứ tự Zillow → CBSA → HUD → Rentometer).

##### **🔹 Node "OpenAI Chat Model1" (lmChatOpenAi)**
- **Chức năng**: Sử dụng GPT-4.1 để tổng hợp báo cáo cuối cùng.
- **Cấu hình**:
  - **Model**: Đặt `gpt-4.1-mini` (có thể nâng cấp lên `gpt-4` nếu cần chất lượng cao hơn).
  - **API Key**: Điền **OpenAI API Key** vào **Credentials** của node này.

##### **🔹 Node "Zillow Rent1" (httpRequestTool)**
- **Chức năng**: Trích xuất giá thuê từ Zillow.
- **Cấu hình**:
  - **URL**: `https://api.apify.com/v2/actors/maxcopell%2Fzillow-detail-scraper/runs`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_APIFY_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body**:
    ```json
    {
      "input": {
        "address": "$node['When chat message received'].json()['address']"
      }
    }
    ```

##### **🔹 Node "Zipcode-to-cbsa1" (httpRequestTool)**
- **Chức năng**: Chuyển đổi mã zipcode thành CBSA code (dùng cho HUD API).
- **Cấu hình**:
  - **URL**: `https://geocoding.geo.census.gov/geocoder/geographies/address?benchmark=Public_AR_Current&vintage=Current&address=${zipcode}`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_HUD_API_KEY"
    }
    ```

##### **🔹 Node "HUD Fair Market Rent1" (httpRequestTool)**
- **Chức năng**: Lấy giá thuê trung bình từ HUD theo CBSA code.
- **Cấu hình**:
  - **URL**: `https://api.huduser.gov/api/fmr/2023/fmr/area?county=${CBSA_CODE}`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_HUD_API_KEY"
    }
    ```

##### **🔹 Node "Rentometer1" (httpRequestTool)**
- **Chức năng**: So sánh giá thuê từ Rentometer.
- **Cấu hình**:
  - **URL**: `https://api.rentometer.com/v1/comps?address=${address}&radius=0.5`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_RENTOMETER_API_KEY"
    }
    ```

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhập một **địa chỉ mẫu** (ví dụ: `123 Main St, New York, NY 10001`) vào chat.
   - Kiểm tra kết quả trả về có đầy đủ không (giá Zillow, HUD, Rentometer + báo cáo AI).
2. **Bật Active**:
   - Nhấn **Active** trên workflow để chạy liên tục.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Sử dụng **Slack App** hoặc **Telegram Bot** để người dùng có thể gửi địa chỉ qua chatbot dễ dàng.
2. **Lưu Log Dữ Liệu**:
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu lịch sử so sánh giá thuê.
3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Scheduler** để tự động gửi báo cáo so sánh hàng tuần cho đội ngũ.
4. **Nâng Cấp Model AI**:
   - Thay `gpt-4.1-mini` thành `gpt-4` nếu cần **báo cáo chi tiết hơn** (tăng chi phí một chút).

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần **tự động hóa phân tích thị trường bất động sản** mà không cần viết code. Bằng cách kết hợp **3 nguồn dữ liệu uy tín** và **trí tuệ nhân tạo**, bạn sẽ **tiết kiệm thời gian, giảm sai sót, và đưa ra quyết định thông minh** chỉ trong vài giây.

**Hãy áp dụng ngay và bắt đầu tự động hóa quy trình của mình!** 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/15472)**
**📌 [Hướng dẫn đăng ký API Key](https://docs.n8n.io/integrations/basics/credentials/)**