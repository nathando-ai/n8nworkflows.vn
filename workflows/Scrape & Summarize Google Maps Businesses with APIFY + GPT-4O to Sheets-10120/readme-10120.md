---
title: "🚀 Tự Động Hóa Scrape & Tóm Tắt Thông Tin Doanh Nghiệp Google Maps Với AI (Không Cần Code)"
description: "Workflow này tự động scrape dữ liệu doanh nghiệp từ Google Maps, tóm tắt thông tin bằng GPT-4o, và lưu vào Google Sheets - tiết kiệm hàng giờ nghiên cứu thủ công cho lead generation và outreach."
slug: "tieu-dong-hoa-scrape-google-maps-voi-gpt-4o"
tags: [n8n, automation, lead-generation, ai-summarization, google-maps-scraping]
keywords: [n8n workflow scrape google maps, tự động hóa lead generation, tóm tắt thông tin doanh nghiệp bằng AI, google sheets automation, apify + openai]
---

# 🚀 **Tự Động Hóa Scrape & Tóm Tắt Thông Tin Doanh Nghiệp Google Maps Với AI (Không Cần Code)**

### **Giải pháp hoàn hảo cho các sếp muốn:**
- **Tiết kiệm 10-20 giờ/ngày** nghiên cứu thủ công doanh nghiệp trên Google Maps.
- **Tự động hóa lead generation** cho sales, marketing, hoặc recruitment.
- **Lưu trữ dữ liệu sạch** vào Google Sheets, sẵn sàng cho outreach hoặc CRM.
- **Không cần viết một dòng code** nhờ công nghệ no-code của n8n + Apify + OpenAI.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tốc độ và tính riêng tư.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ scrape nhanh)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Scrape và tóm tắt hàng trăm doanh nghiệp chỉ trong vài phút.
✅ **Dữ liệu sạch**: Loại bỏ trùng lặp tự động, lưu trữ duy nhất.
✅ **Tóm tắt bằng AI**: GPT-4o tự động viết đoạn tóm tắt chuyên nghiệp cho mỗi doanh nghiệp.
✅ **Sẵn sàng cho outreach**: Dữ liệu được lưu vào Google Sheets, dễ dàng export vào CRM (HubSpot, Salesforce...).
✅ **Hoạt động liên tục**: Chạy tự động mỗi khi cần, không phụ thuộc vào nhân sự.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
📌 **Tài khoản Apify** (để scrape Google Maps):
   - Một **actor Google Maps Scraper** (hoặc tự tạo).
   - **API Token** và **Dataset ID** của actor.
   - [Tutorial cài đặt Apify](https://docs.apify.com/platform/actors/overview) (nếu chưa có).

📌 **Tài khoản OpenAI** (để tóm tắt bằng AI):
   - **API Key** của OpenAI (đăng ký tại [OpenAI Platform](https://platform.openai.com/)).
   - Model **GPT-4o** (được khuyến nghị cho chất lượng/cost tốt nhất).

📌 **Google Sheets**:
   - Một **Google Sheet** để lưu kết quả (cấu trúc cột sẽ được hướng dẫn sau).
   - **OAuth 2.0 Credentials** của Google Sheets (cài đặt trong n8n).

📌 **n8n Workflow**:
   - Tài khoản n8n (cài đặt [Self-hosted](https://n8n.io/) hoặc dùng phiên bản cloud).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/10120](https://n8n.io/workflows/10120) (chọn "Download JSON").
2. **Mở n8n Editor** (trang chủ của workflow).
3. Nhấn **"Import"** → Chọn file JSON vừa tải → **"Import"**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở file JSON từ link trên.
2. Trong n8n Editor, nhấn **"Import"** → Chọn **"Paste JSON"** → Dán nội dung file → **"Import"**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **🔹 Node 1: Manual Trigger (Bắt đầu workflow)**
- **Không cần cấu hình**: Chỉ cần nhấn **"Execute Workflow"** khi muốn chạy.

#### **🔹 Node 2 & 5: Apify (Scrape Google Maps)**
- **Cấu hình Apify API**:
  - Trong **credentials**, chọn **"apifyApi"** → Điền:
    - **Token**: API Token từ Apify.
    - **Actor ID**: ID của actor Google Maps Scraper (vd: `google-maps-scraper`).
  - **Key Parameters**:
    - **Resource**: `Datasets` (để lấy dataset từ Apify).
    - **Dataset ID**: ID của dataset chứa kết quả scrape (vd: `dataset_abc123`).
  - **Lưu ý**:
    - Nếu chưa có dataset, chạy actor trước để tạo dataset.
    - Thay đổi **query** trong actor để scrape theo khu vực/ngành nghề cụ thể (vd: `keyword: cafe Hanoi`).

#### **🔹 Node 3: Remove Duplicates**
- **Không cần cấu hình**: Node này tự động loại bỏ trùng lặp dựa trên trường `name` hoặc `googleMapsUrl`.

#### **🔹 Node 4: Loop Over Items (splitInBatches)**
- **Không cần cấu hình**: Node này chia dữ liệu thành batch để xử lý từng doanh nghiệp một.

#### **🔹 Node 6: OpenAI (Tóm tắt bằng AI)**
- **Cấu hình OpenAI API**:
  - Trong **credentials**, chọn **"openAiApi"** → Điền **API Key**.
  - **Key Parameters**:
    - **Model**: `gpt-4o` (hoặc `gpt-4` nếu không có).
    - **Prompt**: Sử dụng template mặc định (có thể tùy chỉnh):
      ```plaintext
      Tóm tắt thông tin doanh nghiệp {name} ({category}) ở {address}, {city}.
      Đảm bảo bao gồm:
      - Địa chỉ chi tiết: {address}, {city}, {country}
      - Số điện thoại: {phone}
      - Website: {website}
      - Link Google Maps: {googleMapsUrl}
      - Mô tả ngắn gọn về doanh nghiệp (nếu có).
      ```
    - **Temperature**: `0.7` (để kết quả tự nhiên).
    - **Max Tokens**: `256` (đủ cho tóm tắt ngắn gọn).

#### **🔹 Node 7: Google Sheets (Lưu dữ liệu)**
- **Cấu hình Google Sheets**:
  - Trong **credentials**, chọn **"googleSheetsOAuth2Api"** → Đăng nhập Google và cho phép quyền truy cập.
  - **Key Parameters**:
    - **Operation**: `append` (thêm dữ liệu mới vào sheet).
    - **Sheet Name**: Tên sheet muốn lưu (vd: `Doanh Nghiệp Google Maps`).
    - **Range**: `A1` (để ghi từ ô A1).
  - **Cấu trúc cột cần thiết** (xem hình dưới):
    ```
    | Name          | Category       | Address               | City  | Phone       | Website      | Google Maps URL | Summary (AI)                     |
    |---------------|----------------|-----------------------|-------|-------------|--------------|-----------------|----------------------------------|
    | Café Paris    | Café           | 123 Nguyễn Trãi, HN   | HN    | 0987654321  | cafeparis.vn  | ...             | "Café Paris ở Hà Nội... (tóm tắt)" |
    ```

#### **🔹 Node 8: Wait (Pause cho rate limit)**
- **Không bắt buộc**: Nếu scrape quá nhanh bị chặn, thêm delay (vd: `5000ms` = 5 giây).

---
### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Execute Workflow"** → Chọn **"Test Run"** với dataset mẫu.
   - Kiểm tra kết quả trong Google Sheets (cột `Summary` phải có tóm tắt AI).
2. **Bật Active**:
   - Sau khi test thành công, chuyển trạng thái workflow sang **"Active"**.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tùy chỉnh query scrape**
- Mở **Apify Actor** → Thay đổi **searchQuery** để scrape theo:
  - **Khu vực**: `keyword: nhà hàng Hà Nội`.
  - **Ngành nghề**: `category: cafe OR restaurant`.
  - **Khoảng cách**: `location: 5000m@HaNoi`.

### **2. Cải thiện tóm tắt AI**
- **Tùy chỉnh prompt** trong node OpenAI để:
  - **Độ dài**: Thêm `"Tóm tắt trong 3 câu"`.
  - **Tôn chỉ**: `"Tóm tắt theo phong cách chuyên nghiệp cho outreach"`.

### **3. Lưu log và báo cáo**
- Thêm **node `n8n-nodes-base.telegram`** để gửi kết quả scrape qua Telegram.
- Sử dụng **node `n8n-nodes-base.email`** để báo cáo hàng tuần.

### **4. Chạy tự động định kỳ**
- Sử dụng **node `n8n-nodes-base.cron`** để chạy workflow hàng ngày/lần tuần.

### **5. Xử lý lỗi**
- Thêm **node `n8n-nodes-base.if`** để kiểm tra lỗi scrape (vd: nếu `phone` trống, bỏ qua).

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa lead generation từ Google Maps **không cần code**. Với sự kết hợp giữa **Apify (scrape)**, **OpenAI (tóm tắt AI)**, và **Google Sheets (lưu trữ)**, bạn sẽ tiết kiệm **hàng giờ nghiên cứu thủ công** mỗi ngày và có được **dữ liệu sạch, sẵn sàng cho outreach**.

👉 **Bắt đầu ngay!**
1. Import workflow.
2. Cấu hình Apify, OpenAI, và Google Sheets.
3. Chạy và xem kết quả xuất hiện trong Google Sheets.

**Nếu gặp khó khăn**, các sếp có thể liên hệ tác giả qua:
🔗 [LinkedIn](https://www.linkedin.com/in/jaures-nya-83a033270/)
🔗 [YouTube](https://www.youtube.com/@jauresnya)
🔗 [Skool](https://www.skool.com/gaia-4903/about)

---
**Chúc các sếp thành công với tự động hóa!** 🚀