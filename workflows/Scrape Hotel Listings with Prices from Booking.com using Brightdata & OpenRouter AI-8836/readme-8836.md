---
title: "🏨 **Tự Động Hoá Scrape Dữ Liệu Khách Sạn Booking.com + AI Tự Động Hóa Giá Cập Nhật (N8n + Brightdata + OpenRouter AI)**"
description: "Workflow tự động hóa scrape danh sách khách sạn từ Booking.com, lấy giá thực thời, xử lý dữ liệu bằng AI và trả kết quả dưới dạng danh sách sạch sẽ. Giúp tiết kiệm **90% thời gian** so với thủ công, giảm sai sót và tối ưu hóa quyết định mua hàng cho khách hàng."
slug: "tieu-dong-hoa-scrape-booking-com-ai"
tags: [n8n, automation, no-code, web-scraping, ai-multimodal, brightdata, openrouter]
keywords: [n8n scrape booking.com, tự động hóa lấy giá khách sạn, ai xử lý dữ liệu, brightdata api, openrouter chatbot, tự động hóa e-commerce]
---

# 🚀 **Scrape Dữ Liệu Khách Sạn Booking.com + AI Tự Động Hóa Giá Cập Nhật**

## **🔍 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
- **Tốn thời gian**: Phải truy cập Booking.com, copy-paste thông tin khách sạn, giá, và đánh giá thủ công.
- **Giá không chính xác**: Giá trên Booking.com thay đổi liên tục, dẫn đến quyết định mua không chính xác.
- **Không cá nhân hóa**: Khách hàng muốn danh sách khách sạn được sắp xếp theo ưu tiên (giá, vị trí, đánh giá).
- **Khó bảo trì**: Nếu có thay đổi trên Booking.com (captcha, cấu trúc trang), dữ liệu scrape bị lỗi.

**Workflow này giải quyết tất cả!** Nó tự động scrape danh sách khách sạn từ Booking.com, lấy giá thực thời, xử lý dữ liệu bằng AI để trả kết quả **sạch sẽ, có logic**, và **cập nhật động** khi có yêu cầu.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
✅ **Tiết kiệm 90% thời gian** so với thủ công (không cần copy-paste, không cần kiểm tra lại).
✅ **Dữ liệu chính xác 100%**: Giá được scrape từ nguồn Booking.com, không bị lỗi.
✅ **AI tự động hóa xử lý**: Dữ liệu được sắp xếp, lọc, và trình bày dưới dạng danh sách **mạnh mẽ, dễ đọc**.
✅ **Hoạt động 24/7**: Không cần người quản lý, workflow chạy tự động khi có yêu cầu.
✅ **Cá nhân hóa kết quả**: Khách hàng có thể yêu cầu danh sách theo tiêu chí riêng (giá thấp nhất, khách sạn 5 sao...).
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI CHẠY**]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Bright Data** (để scrape Booking.com):
   - [Đăng ký miễn phí Bright Data](https://get.brightdata.com/unstoppable) (API key sẽ được yêu cầu).
   - **Lưu ý**: Bright Data cung cấp **proxy và web scraper** để tránh bị chặn bởi Booking.com.
2. **API Key OpenRouter** (để sử dụng AI xử lý dữ liệu):
   - [Đăng ký OpenRouter](https://openrouter.ai/) và lấy API key.
3. **N8n Self-hosted** (để workflow chạy 24/7):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/8836](https://n8n.io/workflows/8836) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n.
- **Cách 3**: Sử dụng **n8n CLI** để import:
  ```bash
  n8n import workflow.json --name "Booking Hotels Scraper"
  ```

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **14 node**, nhưng các node quan trọng nhất cần cấu hình kỹ:

##### **🔹 Node Bright Data (Scrape Booking.com)**
- **Node 1**: `Initiate batch extraction from URL`
  - **Cấu hình**:
    - Tham số `url`: Đặt URL Booking.com của thành phố cần scrape (ví dụ: `https://www.booking.com/searchresults.en-gb.html?ss=Hanoi`).
    - **Credentials**: Chọn `brightdataApi` (đã cấu hình trước khi import).
    - **Lưu ý**: Bright Data sẽ tự động **bypass captcha** và scrape dữ liệu.

- **Node 2**: `Check the status of a batch extraction`
  - **Cấu hình**:
    - Sử dụng `snapshotId` từ node trước để theo dõi tiến độ scrape.
    - **Credentials**: `brightdataApi`.

- **Node 3**: `Download the snapshot content`
  - **Cấu hình**:
    - Chọn `snapshotId` tương ứng từ node kiểm tra trạng thái.
    - **Credentials**: `brightdataApi`.

##### **🔹 Node AI OpenRouter (Xử Lý Dữ Liệu)**
- **Node 4**: `OpenRouter Chat Model2`
  - **Cấu hình**:
    - **Credentials**: `openRouterApi` (API key đã đăng ký).
    - **Prompt**: Sử dụng mặc định (AI sẽ tự động **lọc, sắp xếp, và trình bày** dữ liệu khách sạn).
    - **Lưu ý**: Nếu muốn tùy chỉnh, chỉnh sửa prompt ở đây:
      ```json
      "prompt": "Tôi có danh sách khách sạn từ Booking.com. Hãy sắp xếp chúng theo giá tăng dần, loại bỏ khách sạn dưới 3 sao, và trả kết quả dưới dạng danh sách có tiêu đề 'Top 10 Khách Sạn Giá Rẻ Tại {City}'."
      ```

##### **🔹 Node ChatTrigger (Kích Hoạt Bằng Chat)**
- **Node 5**: `When chat message received`
  - **Cấu hình**:
    - Nếu muốn kích hoạt bằng **Slack/Telegram**, cấu hình credentials tương ứng.
    - **Lưu ý**: Workflow này có thể được kích hoạt bằng **webhook** hoặc **chatbot** (ví dụ: khi khách hàng gửi tin nhắn "Scrape khách sạn Hà Nội").

##### **🔹 Node Agent & Calculator (Tính Toán & Tối Ưu Hóa)**
- **Node 6**: `Human Friendly Results` (Agent)
  - **Cấu hình**: Sử dụng mặc định (AI sẽ tự động **tối ưu hóa** kết quả).
- **Node 7**: `Calculator`
  - **Cấu hình**: Nếu cần tính toán giá trung bình, chiết khấu, hoặc so sánh giá, chỉnh sửa ở đây.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Chạy **manual execution** với một URL mẫu (ví dụ: `https://www.booking.com/searchresults.en-gb.html?ss=Hanoi`).
  - Kiểm tra kết quả ở node `Human Friendly Results` để đảm bảo AI xử lý đúng.
- **Bật Active**:
  - Sau khi test thành công, **bật Active** workflow và cấu hình **trigger** (webhook/Slack/Telegram).

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**Cách Tối Ưu Hóa Workflow**]
1. **Lưu Log Dữ Liệu**:
   - Thêm node **n8n-nodes-base.httpRequest** để lưu kết quả scrape vào **Google Sheets** hoặc **Airtable** để theo dõi lịch sử.
   - **Cú pháp**:
     ```json
     {
       "operation": "post",
       "url": "https://api.airtable.com/v0/{BASE_ID}/{TABLE_NAME}",
       "credentials": {
         "type": "apiKey",
         "name": "airtableApi"
       },
       "body": {
         "fields": {
           "Hotel Name": "$node['Download the snapshot content'].json()['hotel_name']",
           "Price": "$node['Download the snapshot content'].json()['price']",
           "Rating": "$node['Download the snapshot content'].json()['rating']"
         }
       }
     }
     ```

2. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n-nodes-base.schedule** để chạy scrape hàng ngày và gửi báo cáo qua **Email** hoặc **Slack**.
   - **Cú pháp**:
     ```json
     {
       "cron": "0 0 * * *", // Chạy hàng ngày lúc 00:00
       "node": {
         "parameters": {
           "url": "https://www.booking.com/searchresults.en-gb.html?ss=Hanoi"
         }
       }
     }
     ```

3. **Kết Hợp Với Slack/Telegram**:
   - Thêm node **n8n-nodes-base.slack** hoặc **n8n-nodes-base.telegram** để thông báo kết quả scrape ngay khi có.
   - **Cú pháp Slack**:
     ```json
     {
       "channel": "#hotel-scraper",
       "text": "Kết quả scrape khách sạn Hà Nội:\n$node['Human Friendly Results'].json()"
     }
     ```

4. **Tùy Chỉnh AI Prompt**:
   - Nếu muốn AI **lọc khách sạn theo tiêu chí riêng**, chỉnh sửa prompt ở node `OpenRouter Chat Model2`:
     ```json
     "prompt": "Tôi muốn danh sách khách sạn có phòng từ 2 người trở lên, giá dưới 1 triệu, và có bể bơi. Hãy sắp xếp theo giá tăng dần và trả kết quả dưới dạng danh sách có tiêu đề 'Khách Sạn Phù Hợp'."
     ```
:::

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc scrape thủ công, đồng thời **tối ưu hóa quyết định mua hàng** cho khách hàng bằng dữ liệu **chính xác, sạch sẽ và cá nhân hóa**.

**🚀 Hãy áp dụng ngay!**
- **Bước 1**: Chuẩn bị **Bright Data API** và **OpenRouter API**.
- **Bước 2**: Import workflow và cấu hình **URL scrape**.
- **Bước 3**: Test và **bật Active** để tự động hóa!

**Nếu cần hỗ trợ**, liên hệ với tác giả [Phil](https://inforeole.fr) để **tư vấn tự động hóa quy trình** của doanh nghiệp!

---
**🔥 Cảm ơn các sếp đã đọc đến cuối!** Chúc các sếp thành công với việc tự động hóa scrape Booking.com! 🏨✨