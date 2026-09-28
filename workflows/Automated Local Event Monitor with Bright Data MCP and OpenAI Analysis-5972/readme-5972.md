---
title: "🚀 Tự Động Hóa Theo Dõi Sự Kiện Địa Phương + Phân Tích AI: Tìm Kiếm Sponsorship Chất Lượng Cho Doanh Nghiệp"
description: "Workflow tự động hóa thu thập dữ liệu sự kiện từ 10Times, phân tích cơ hội hợp tác quảng cáo thông minh bằng AI GPT-4, và lưu trữ kết quả vào Google Sheets - Giúp doanh nghiệp tiết kiệm 10+ giờ/tháng và tối ưu hóa chiến lược marketing."
slug: "tieu-dong-hoa-theo-doi-suc-kien-dia-phuong-ai-sponsorship"
tags: [n8n, automation, market-research, ai-summarization, bright-data, google-sheets, openai]
keywords: [tự động hóa n8n, phân tích sự kiện địa phương, AI tìm kiếm sponsorship, Bright Data MCP, Google Sheets tự động, GPT-4 phân tích cơ hội hợp tác]
---

# 🚀 **Tự Động Hóa Theo Dõi Sự Kiện Địa Phương + Phân Tích AI: Tìm Kiếm Sponsorship Chất Lượng Cho Doanh Nghiệp**

## **🔍 Nỗi Đau Của Doanh Nghiệp**
Các sếp thường phải **tốn thời gian thủ công** để:
- **Thu thập** danh sách sự kiện từ các trang web như 10Times, Meetup, hoặc Eventbrite.
- **Phân tích** từng sự kiện để đánh giá tiềm năng **sponsorship** phù hợp với sản phẩm/dịch vụ của mình.
- **Lưu trữ** dữ liệu một cách rối ren, khó theo dõi và cập nhật.

**Kết quả?** Thời gian và nguồn lực bị "chôn vùi" trong công việc lặp đi lặp lại, trong khi cơ hội marketing tiềm năng bị bỏ lỡ.

**Workflow này giải quyết tất cả!** Với **AI + Bright Data MCP**, các sếp sẽ:
✅ **Tự động** thu thập dữ liệu sự kiện từ 10Times (New York hoặc bất kỳ thành phố nào).
✅ **AI GPT-4** phân tích từng sự kiện và **đánh giá tiềm năng sponsorship** dựa trên ngành nghề của doanh nghiệp.
✅ **Lưu trữ tự động** tất cả dữ liệu vào Google Sheets, sẵn sàng để **báo cáo và phân tích**.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng**: Không cần thủ công thu thập và phân tích dữ liệu.
- **Cơ hội sponsorship chất lượng**: AI đánh giá sự kiện dựa trên **ngành nghề, quy mô, và tiềm năng tiếp cận khách hàng**.
- **Dữ liệu sạch và cấu trúc**: Tất cả thông tin được **lưu vào Google Sheets** với định dạng chuẩn, dễ dàng **export và chia sẻ**.
- **Hoạt động 24/7**: Workflow chạy tự động, không phụ thuộc vào giờ làm việc của nhân viên.
- **Cập nhật liên tục**: Theo dõi sự kiện mới xuất hiện trên 10Times mà không cần can thiệp thủ công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Bright Data MCP** (để scrape dữ liệu):
   - [Đăng ký Bright Data MCP](https://get.brightdata.com/1tndi4600b25) (🎁 Mã giảm giá: **N8NBRIGHT** - giảm 20%).
   - **API Key** từ Bright Data MCP (được gọi là `mcpClientApi` trong workflow).
2. **Tài khoản OpenAI** (để sử dụng AI GPT-4):
   - [Đăng ký OpenAI](https://platform.openai.com/signup) và lấy **API Key** (được gọi là `openAiApi`).
3. **Google Sheets** (để lưu trữ kết quả):
   - **File Google Sheets** đã cấu trúc sẵn (các sếp có thể tạo mới với các cột: `Tên Sự Kiện`, `Ngày Thực Hiện`, `Địa Điểm`, `Mô Tả`, `Tiềm Năng Sponsorship`, `Đánh Giá AI`).
   - **Credentials OAuth2** của Google Sheets (được gọi là `googleSheetsOAuth2Api`).
4. **URL của trang sự kiện** (ví dụ: [10Times New York](https://www.10times.com/new-york)).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/5972](https://n8n.io/workflows/5972) (chọn **Export as JSON**).
2. **Mở n8n Editor** (trên máy chủ self-hosted hoặc n8n.cloud).
3. Nhấn **Import** và chọn file JSON vừa tải.
4. **Chọn Workspace** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải JSON** từ link trên và copy toàn bộ nội dung.
2. Trong **n8n Editor**, nhấn **Import** → **Paste JSON** và dán nội dung.
3. **Chọn Workspace** và nhấn **Import**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **4 phần chính**, mỗi phần đều cần **cấu hình kỹ lưỡng**:

#### **🔘 Section 1: Khởi Động Workflow + Đặt URL**
- **Node: `🔘 Trigger: Manual Execution`**
  - **Lưu ý**: Workflow này **không tự động chạy**, các sếp phải **nhấn "Execute"** mỗi khi muốn cập nhật dữ liệu mới.
  - **Không cần chỉnh sửa gì** ngoài việc **nhấn "Run"** khi cần.

- **Node: `🌐 Set URL for 10Times New York Events`**
  - **Chỉnh sửa URL** để scrape sự kiện ở **thành phố mong muốn** (ví dụ: `https://www.10times.com/vietnam` cho Hà Nội/TP.HCM).
  - **Định dạng URL**:
    ```json
    {
      "url": "https://www.10times.com/new-york/events"
    }
    ```

---

#### **🤖 Section 2: Scrape Dữ Liệu Sự Kiện từ 10Times**
- **Node: `🤖 Agent: Scrape Event Data (10Times)`**
  - **Không cần chỉnh sửa** nội bộ agent, nhưng **cần đảm bảo**:
    - **Bright Data MCP API Key** (`mcpClientApi`) đã được **cấu hình trong Credentials** của n8n.
    - **AI Model trong Agent** (`💬 AI Model: Process Event Data`) sử dụng **GPT-4.1-mini** (đã mặc định).

- **Node: `🌐 MCP Client: Scrape Events from 10Times`**
  - **Không cần chỉnh sửa** nếu sử dụng cấu hình mặc định.
  - **Lưu ý quan trọng**:
    - Bright Data MCP có **hạn chế request** (tùy thuộc vào gói đăng ký).
    - Nếu scrape nhiều trang, **cần tăng timeout** trong **Advanced Settings** của node này (thêm `timeout: 30000`).

- **Node: `📝 Parse Scraped Data into JSON Format`**
  - **Không cần chỉnh sửa** nếu dữ liệu scrape ra đúng định dạng.
  - **Nếu dữ liệu rối**: Mở **Code Node** (`🔀 Split Events into Separate Items`) và chỉnh sửa logic **split** nếu cần.

---

#### **🔀 Section 3: Phân Tích Cơ Hội Sponsorship Bằng AI**
- **Node: `🔀 Split Events into Individual Listings`**
  - **Mở Code Node** và kiểm tra logic **split**:
    ```javascript
    // Ví dụ mã split mặc định (có thể chỉnh sửa nếu dữ liệu không đúng định dạng)
    return $input.all();
    ```
  - **Nếu dữ liệu scrape ra là mảng JSON**, có thể cần **chuyển đổi thành danh sách đối tượng** bằng:
    ```javascript
    return $input.all().map(item => ({
      json: item.json,
      metadata: item.metadata
    }));
    ```

- **Node: `💬 AI: Sponsorship Opportunity Analysis`**
  - **Prompt AI** đã được **cấu hình sẵn** để đánh giá sự kiện dựa trên **ngành project management**.
  - **Nếu muốn thay đổi ngành nghề**, chỉnh sửa **Prompt** trong node này:
    ```json
    {
      "model": "gpt-4.1-mini",
      "messages": [
        {
          "role": "system",
          "content": "Bạn là chuyên gia phân tích sponsorship cho doanh nghiệp chuyên về [NGÀNH CỦA DOANH NGHIỆP]. Hãy đánh giá sự kiện dựa trên các tiêu chí sau:\n1. Tiềm năng tiếp cận khách hàng mục tiêu.\n2. Phù hợp với sản phẩm/dịch vụ của doanh nghiệp.\n3. Quy mô sự kiện (số lượng tham gia dự kiến).\n4. Đánh giá từ 1-10 về tiềm năng sponsorship."
        },
        {
          "role": "user",
          "content": "{{$json.event_description}}"
        }
      ]
    }
    ```
  - **Thêm biến `$json`** để AI sử dụng dữ liệu scrape ra (ví dụ: `$json.event_name`, `$json.date`).

---

#### **📥 Section 4: Lưu Trữ Dữ Liệu vào Google Sheets**
- **Node: `📥 Save Events and Sponsorship Ratings to Google Sheets`**
  - **Chọn Sheet** và **Range** trong Google Sheets:
    - **Sheet Name**: `Sponsorship Analysis` (hoặc tên khác).
    - **Range**: `A1` (hoặc `A2` nếu đã có dữ liệu).
  - **Cấu trúc cột phải khớp với dữ liệu**:
    | Cột A | Cột B | Cột C | Cột D | Cột E | Cột F |
    |--------|--------|--------|--------|--------|--------|
    | Tên Sự Kiện | Ngày Thực Hiện | Địa Điểm | Mô Tả | Tiềm Năng Sponsorship | Đánh Giá AI |
  - **Nếu dữ liệu không khớp**, mở **Code Node** trước node Google Sheets và **chuyển đổi dữ liệu** thành định dạng phù hợp.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run với Dữ Liệu Mẫu**:
   - Nhấn **Execute** và **chọn "Test"** để chạy workflow với URL mẫu.
   - Kiểm tra **Google Sheets** xem dữ liệu có được lưu không.
   - **Sửa lỗi** nếu có (ví dụ: dữ liệu scrape không đầy đủ, AI không phân tích được).

2. **Bật Active Workflow**:
   - Sau khi test thành công, **nhấn "Active"** để workflow chạy tự động khi nhấn **Execute**.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH TIẾP CẬN THÊM]
1. **Tự Động Chạy Hàng Ngày**
   - Thay vì **manual trigger**, các sếp có thể **cài đặt cron job** để workflow chạy tự động hàng ngày:
     ```yaml
     # Cài đặt trong n8n (Settings > Workflows > Cron)
     0 8 * * *  # Chạy lúc 8h sáng hàng ngày
     ```
   - **Lưu ý**: Bright Data MCP có **hạn chế request**, nên **không nên chạy quá nhiều lần/ngày**.

2. **Gửi Báo Cáo Định Kỳ qua Email/Slack**
   - **Thêm node Email/Slack** sau node Google Sheets để **gửi báo cáo tự động**:
     - **Node Email**: `@n8n/nodes-base.email` (cấu hình SMTP).
     - **Node Slack**: `@n8n/nodes-base.slack` (cấu hình webhook).
   - **Ví dụ cấu hình Email**:
     ```json
     {
       "to": "sop@doanhnghiep.com",
       "subject": "Báo cáo Sponsorship - Ngày {{ $json.date }}",
       "html": "Xin chào,\n\nDưới đây là danh sách sự kiện mới được phân tích:\n{{ $json.events | join('\n') }}"
     }
     ```

3. **Lưu Log Dữ Liệu**
   - **Thêm node `n8n-nodes-base.manualTrigger`** để **lưu log** của mỗi lần chạy:
     ```json
     {
       "name": "📝 Log Workflow Execution",
       "type": "set",
       "parameters": {
         "data": {
           "timestamp": "{{ $execution.date }}",
           "url_scraped": "{{ $input.url }}",
           "events_found": "{{ $input.events.length }}"
         }
       }
     }
     ```
   - **Lưu vào Google Sheets hoặc cơ sở dữ liệu** để theo dõi lịch sử.

4. **Tối Ưu Hóa AI**
   - **Thay đổi model AI** từ `gpt-4.1-mini` sang `gpt-4` (nếu có budget):
     ```json
     {
       "model": "gpt-4",
       "messages": [...]
     }
     ```
   - **Tùy chỉnh Prompt** để AI **phân tích chi tiết hơn** về:
     - **Khách hàng mục tiêu** của sự kiện.
     - **Cơ hội cross-promotion** với sản phẩm của doanh nghiệp.
     - **Giá trị ước tính** của sponsorship.

5. **Scrape Nhiều Thành Phố**
   - **Tạo một workflow riêng** cho mỗi thành phố (Hà Nội, TP.HCM, Đà Nẵng...).
   - **Sử dụng node `n8n-nodes-base.parallelSet`** để chạy song song:
     ```json
     {
       "name": "🌍 Scrape Multiple Cities",
       "type": "parallelSet",
       "parameters": {
         "data": [
           { "url": "https://www.10times.com/hanoi", "city": "Hà Nội" },
           { "url": "https://www.10times.com/ho-chi-minh-city", "city": "TP.HCM" }
         ]
       }
     }
     ```

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp khỏi công việc thủ công **thu thập và phân tích sự kiện**, đồng thời **tối ưu hóa chiến lược sponsorship** bằng **AI GPT-4**. Với **Google Sheets** làm trung tâm, dữ liệu luôn **cập nhật, sạch sẽ và dễ dàng chia sẻ**.

**Bắt đầu ngay!**
1. **Đăng ký Bright Data MCP** và **Open