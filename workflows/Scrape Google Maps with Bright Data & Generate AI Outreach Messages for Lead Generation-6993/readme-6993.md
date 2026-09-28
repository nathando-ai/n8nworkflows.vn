---
title: "🚀 Tự Động Hoá Trích Xuất Dữ Liệu Google Maps + Tạo Tin Nhắn Outreach AI Cho Lead Generation (Không Cần Code)"
description: "Workflow này tự động trích xuất thông tin doanh nghiệp từ Google Maps bằng Bright Data, phân tích AI và lưu trữ vào cơ sở dữ liệu Supabase để hỗ trợ chiến dịch cold outreach hiệu quả. Giúp các sếp tiết kiệm 10-15 giờ/tháng làm thủ công."
slug: "tieu-dong-hoa-trich-xuat-google-maps-ai-outreach"
tags: [n8n, automation, lead-generation, bright-data, ai-outreach, no-code, supabase, google-maps-scraping]
keywords: [n8n workflow lead generation, tự động hóa trích xuất Google Maps, AI tạo tin nhắn outreach, Bright Data MCP, Supabase tự động hóa, cold outreach tự động]
---

# 🚀 **Tự Động Hoá Trích Xuất Dữ Liệu Google Maps + Tạo Tin Nhắn Outreach AI Cho Lead Generation**

## **🔍 Nỗi Đau Của Các Sếp Trong Lead Generation**
Hàng ngày, các sếp phải:
- **Làm thủ công** tìm kiếm và trích xuất thông tin doanh nghiệp từ Google Maps (tốn 10-15 giờ/tháng).
- **Tạo tin nhắn outreach** cá nhân hóa cho từng lead, mất thời gian và dễ sai sót.
- **Quản lý dữ liệu** rải rác trên Excel, khó theo dõi và cập nhật.
- **Không có hệ thống tự động** để liên tục cập nhật lead mới khi có thay đổi.

**Workflow này giải quyết tất cả!** Sử dụng công nghệ **Bright Data** để scrape Google Maps, **AI (OpenAI/Gemini)** để tạo tin nhắn outreach cá nhân hóa, và **Supabase** để lưu trữ dữ liệu một cách an toàn và hiệu quả.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất tối ưu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Trích xuất và phân tích lead chỉ trong vài phút thay vì nhiều giờ.
✅ **Tin nhắn outreach cá nhân hóa**: AI tạo nội dung phù hợp với từng doanh nghiệp, tăng tỷ lệ phản hồi.
✅ **Dữ liệu đồng bộ hóa**: Tất cả lead và tin nhắn được lưu vào **Supabase**, dễ dàng truy cập và phân tích.
✅ **Hoạt động liên tục**: Workflow chạy tự động khi có dữ liệu mới, không cần can thiệp thủ công.
✅ **Tăng hiệu suất outreach**: Dữ liệu chính xác và tin nhắn AI giúp tăng tỷ lệ chuyển đổi lên **30-50%**.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Bright Data**:
   - [Đăng ký Bright Data](https://brightdata.com/) và lấy **API Key** (để cấu hình trong `brightdataApi`).
   - **Dataset ID** cho Google Maps Scraper: `gd_m8ebnr0q2qlklc02fz` (được cung cấp trong workflow).
   - **Zoom Level** (điều chỉnh bán kính tìm kiếm, ví dụ: `12` cho khu vực thành phố).

2. **Tài khoản LLM (AI Chatbot)**:
   - **OpenAI** (API Key cho `openAiApi`) hoặc **Google Gemini** (API Key cho `googlePalmApi`).
   - Chọn mô hình AI phù hợp (ví dụ: `gpt-4.1-mini` hoặc `gemini-1.0`).

3. **Cơ sở dữ liệu Supabase (hoặc PostgreSQL)**:
   - Tạo bảng `leads` với các cột: `id`, `name`, `address`, `phone`, `website`, `description`, `outreach_message`, `status`.
   - **Lưu ý**: Workflow sử dụng **Postgres credentials** để kết nối với Supabase.

4. **Tài khoản n8n**:
   - Cài đặt **n8n Community Edition** hoặc **n8n Enterprise** (nếu cần tính năng nâng cao).
   - Cài đặt **n8n nodes** cần thiết:
     - `@n8n/n8n-nodes-langchain` (cho AI).
     - `@brightdata/n8n-nodes-brightdata` (cho Bright Data).
     - `@n8n/n8n-nodes-base` (nodes cơ bản).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/6993](https://n8n.io/workflows/6993) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import** → Dán JSON và nhấn **Import**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này có **27 nodes**, nhưng các bước quan trọng nhất cần chú ý:

##### **A. Cấu Hình Bright Data**
- **Node `Bright Data | Request data`**:
  - Điền **API Key** vào `brightdataApi` (tạo trong **Credentials** → **Add** → **Bright Data**).
  - Tham số `dataset_id`: `gd_m8ebnr0q2qlklc02fz` (Google Maps Scraper).
  - Tham số `zoom_level`: Điều chỉnh theo khu vực muốn scrape (ví dụ: `12` cho thành phố).

- **Node `Check status of data extraction` và `Download the snapshot content`**:
  - Bright Data sẽ tự động **monitor và download** dữ liệu khi scrape xong.
  - **Retry logic**: Workflow sẽ tự động retry nếu scrape thất bại (điều này đã được cấu hình trong `Reached retry limit`).

##### **B. Cấu Hình AI (OpenAI/Gemini)**
- **Node `OpenAI Chat Model` hoặc `Google Gemini Chat Model`**:
  - Chọn mô hình AI phù hợp (ví dụ: `gpt-4.1-mini`).
  - Điền **API Key** vào `openAiApi` (hoặc `googlePalmApi`).
  - **Prompt mặc định** đã được tối ưu để tạo tin nhắn outreach cá nhân hóa.

##### **C. Cấu Hình Supabase (PostgreSQL)**
- **Node `Create Table` và `Supabase | Upsert row`**:
  - Đảm bảo **Postgres credentials** đã được cấu hình trong `n8n` (Credentials → Add → PostgreSQL).
  - **Query SQL** trong `Create Table` sẽ tự động tạo bảng `leads` nếu chưa tồn tại.
  - **Upsert** giúp cập nhật lead mới hoặc cập nhật thông tin cũ.

##### **D. Cấu Hình Form Trigger (Nếu Sử Dụng)**
- **Node `On form submission`**:
  - Nếu muốn chạy workflow từ **form**, các sếp cần tạo một **form HTML** (ví dụ bằng **n8n Form Trigger**) và kết nối với node này.
  - **Yêu cầu đầu vào**:
    - `location` (vị trí Google Maps).
    - `keyword` (từ khóa tìm kiếm).
    - `country` (quốc gia).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Execute Workflow** (node `When clicking ‘Execute workflow’`) với dữ liệu mẫu.
   - Kiểm tra **Supabase** để xác nhận lead đã được lưu.

2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tối ưu hóa AI Prompt**:
   - Thay đổi **prompt** trong node `Message Generator` để phù hợp với ngành nghề của các sếp.
   - Ví dụ: Nếu outreach cho **doanh nghiệp SaaS**, có thể thêm yêu cầu về **giá trị độc đáo** của sản phẩm.

2. **Lưu Log & Monitoring**:
   - Thêm **node `Set`** sau `Supabase | Upsert row` để lưu **log thành công/thất bại** vào cơ sở dữ liệu.
   - Sử dụng **n8n Dashboard** để theo dõi tiến độ scrape và AI.

3. **Kết hợp với Slack/Telegram**:
   - Thêm **node `Slack`** hoặc `Telegram Bot` để thông báo khi workflow hoàn thành.
   - Ví dụ: Gửi tin nhắn như: *"🚀 Scrape xong 50 lead mới! AI đã tạo outreach cho tất cả."*

4. **Lọc Lead Theo Đặc Trưng**:
   - Sử dụng **node `If`** để lọc lead có **website** hoặc **số điện thoại** trước khi tạo tin nhắn outreach.

5. **Automate Cold Outreach**:
   - Sau khi lưu lead vào Supabase, các sếp có thể kết nối với **n8n Email Node** hoặc **Zapier** để tự động gửi tin nhắn outreach.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa **lead generation** từ Google Maps, đồng thời **tạo tin nhắn outreach AI** cá nhân hóa. Bằng cách kết hợp **Bright Data** (scrape), **AI (OpenAI/Gemini)** (tạo nội dung), và **Supabase** (lưu trữ), các sếp sẽ tiết kiệm **thời gian, tăng hiệu suất outreach**, và có dữ liệu chính xác để quyết định kinh doanh.

**💡 Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với dữ liệu mẫu** và điều chỉnh prompt AI.
3. **Bật Active** và bắt đầu tự động hóa lead generation!

**Nếu cần hỗ trợ**, liên hệ với tác giả Solomon qua:
- [Telegram](https://t.me/salomaoguilherme)
- [LinkedIn](https://www.linkedin.com/in/guisalomao/)
- Email: [automations.solomon@gmail.com](mailto:automations.solomon@gmail.com)

---
**🔥 Xem thêm workflow của Solomon tại [n8n.io/creators/solomon](https://n8n.io/creators/solomon/)**!