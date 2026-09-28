---
title: "🔍 **Tự Động Theo Dõi Giá Thương Mại Thể Thao Competitor Với Bright Data MCP & Google Sheets (N8n)**"
description: "Workflow tự động hóa 24/7 giúp các sếp theo dõi giá sản phẩm từ các đối thủ cạnh tranh (Nike, Adidas,...) trên mạng, lưu trữ dữ liệu vào Google Sheets và nhận thông báo email khi có thay đổi mới nhất. Giúp tiết kiệm thời gian, tối ưu chiến lược giá và cạnh tranh hiệu quả."
slug: "tieu-dong-thoi-gia-competitor-voi-n8n"
tags: [n8n, automation, market-research, ai-summarization, bright-data, google-sheets]
keywords: [n8n workflow tự động hóa, theo dõi giá competitor, Bright Data MCP, Google Sheets tự động, AI scraping, tự động hóa marketing]
---

# 🚀 **Tự Động Theo Dõi Giá Thương Mại Thể Thao Competitor Với Bright Data MCP & Google Sheets**

## **Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải **tốn thời gian thủ công** để:
- **So sánh giá** sản phẩm thể thao (giày, áo Nike, Adidas,...) trên nhiều trang web khác nhau.
- **Lưu trữ dữ liệu** vào Excel/Google Sheets một cách rườm rà.
- **Không biết kịp thời** khi đối thủ giảm giá, mất cơ hội cạnh tranh.
- **Phải chịu rủi ro** khi bị chặn bởi hệ thống chống bot (CAPTCHA, IP blocking) khi scrap dữ liệu.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Scrape giá** từ các trang web động (Nike, Adidas,...) **mỗi ngày/tuần**.
✅ **Lưu dữ liệu** vào Google Sheets với định dạng sạch sẽ.
✅ **Gửi email thông báo** khi có dữ liệu mới.
✅ **Không cần code**, chỉ cần cấu hình đơn giản.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10-15 giờ/tháng** so với cách làm thủ công.
- **Cập nhật giá thời gian thực**, không bỏ lỡ cơ hội giảm giá của đối thủ.
- **Dữ liệu sạch sẽ** trong Google Sheets, dễ dàng phân tích bằng biểu đồ.
- **Không bị chặn bot**, nhờ Bright Data MCP (dịch vụ proxy chuyên nghiệp).
- **Cá nhân hóa** theo từng sản phẩm, không giới hạn số lượng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Bright Data MCP** (để scrape dữ liệu từ các trang web động):
   - 👉 [Đăng ký Bright Data MCP](https://get.brightdata.com/1tndi4600b25) (mã giảm giá: **N8NBRIGHT**).
   - **API Key** của MCP sẽ được sử dụng trong node `MCP Client`.
2. **Tài khoản Google Sheets** (để lưu trữ dữ liệu):
   - **File Google Sheets** đã tạo sẵn với cột: `Product Name`, `Price`, `Description`, `URL`.
   - **Credentials OAuth2** của Google Sheets (cấu hình trong n8n).
3. **Tài khoản Gmail** (để gửi email thông báo):
   - **Credentials OAuth2** của Gmail (cấu hình trong n8n).
4. **Tài khoản OpenAI** (để sử dụng AI trong quá trình scrape):
   - **API Key** của OpenAI (cấu hình trong node `OpenAI Chat Model`).
5. **VPS Self-hosted n8n** (để workflow chạy 24/7):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N**).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/5959).
- Trong n8n Editor, nhấn **Import** và chọn file JSON.
- **Hoặc** copy toàn bộ JSON và paste vào **Import Workflow** trong n8n.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **📅 Node: Run Weekly Check (Schedule Trigger)**
- **Cấu hình lịch chạy**:
  - Chọn **Weekly** (mỗi tuần) hoặc **Daily** (hàng ngày).
  - Thời gian chạy: **Giờ mà các sếp muốn scrape** (ví dụ: 8h sáng để tránh đỉnh lưu lượng).

#### **🛒 Node: Product Page URL (Edit Fields)**
- **Điền URL sản phẩm** cần theo dõi:
  - Ví dụ: `https://www.nike.com/...`, `https://www.adidas.com/...`.
  - Nếu muốn theo dõi nhiều sản phẩm, **chỉnh sửa JSON** trong node này để thêm nhiều URL.

#### **🤖 Node: Scrape Competitor Prices (MCP Agent)**
- **Không cần chỉnh sửa** (n8n sẽ tự động scrape dữ liệu).
- **Lưu ý**:
  - Nếu scrape thất bại, kiểm tra **Bright Data MCP API Key** có đúng không.
  - Nếu trang web có CAPTCHA, **Bright Data MCP sẽ tự động giải quyết**.

#### **💬 Node: OpenAI Chat Model (AI Parser)**
- **Không cần chỉnh sửa** (sử dụng mô hình `gpt-4o-mini`).
- **Lưu ý**:
  - Nếu muốn cải thiện độ chính xác, **cập nhật Prompt** trong node này (ví dụ: yêu cầu AI trả về định dạng JSON cụ thể).

#### **📧 Node: Notify: Prices Logged in Sheet (Gmail)**
- **Cấu hình email**:
  - **Địa chỉ nhận email**: Điền email của mình hoặc team.
  - **Tiêu đề email**: Cố định là **"New Competitor Pricing Data"** hoặc tùy chỉnh.
  - **Nội dung email**: Sử dụng **template mặc định** hoặc chỉnh sửa để thêm link trực tiếp đến Google Sheets.

#### **🧹 Node: Format Products for Google Sheets (Code)**
- **Không cần chỉnh sửa** (n8n sẽ tự động chuyển đổi dữ liệu thành định dạng phù hợp với Google Sheets).
- **Lưu ý**:
  - Nếu dữ liệu scrape không đầy đủ, **mở node này** và chỉnh sửa script để extra các trường cần thiết.

#### **📄 Node: Save to Google Sheets (Competitor Pricing Log)**
- **Chọn Sheet và Range**:
  - **File Google Sheets**: Chọn file đã tạo sẵn.
  - **Range**: Chọn **Sheet Name** và **Range** (ví dụ: `Sheet1!A1`).
  - **Operation**: Đảm bảo chọn **Append** (thêm dữ liệu mới vào cuối sheet).

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** và kiểm tra:
     - Dữ liệu có scrape được không?
     - Email có được gửi không?
     - Dữ liệu có được lưu vào Google Sheets không?
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** để workflow chạy tự động theo lịch.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Theo Dõi Nhiều Sản Phẩm Khác Nhau**
- **Cách 1**: Sử dụng **node `Edit Fields`** để thêm nhiều URL vào một lần.
- **Cách 2**: **Tạo nhiều workflow** riêng cho từng danh mục sản phẩm (ví dụ: Workflow 1 cho giày, Workflow 2 cho áo).

### **2. Thêm Báo Cáo Định Kỳ**
- **Sử dụng node `Schedule Trigger`** để chạy workflow **mỗi tháng** và gửi **báo cáo tổng hợp** về giá.
- **Cấu hình email** để gửi **biểu đồ so sánh giá** (sử dụng Google Sheets Charts).

### **3. Kết Nối Với Slack/Telegram**
- Thay vì email, **thêm node `Slack` hoặc `Telegram`** để nhận thông báo tức thì.
- **Cách làm**:
  - Cài **n8n Slack/Telegram Node**.
  - Kết nối với **credentials OAuth2** của Slack/Telegram.
  - Thay thế node `Gmail` bằng `Slack` hoặc `Telegram`.

### **4. Lưu Log Dữ Liệu**
- **Thêm node `StickyNote`** để lưu **log lỗi** nếu scrape thất bại.
- **Cách làm**:
  - Cài **n8n StickyNote Node**.
  - Kết nối với **credentials** và cấu hình để lưu log vào **Google Drive** hoặc **Google Sheets Log**.

### **5. Cập Nhật Giá Thời Gian Thực**
- **Sử dụng node `Schedule Trigger` chạy hàng giờ** (ví dụ: 2h/lần) để cập nhật giá **mỗi ngày nhiều lần**.
- **Lưu ý**: Bright Data MCP có giới hạn request, nên **không nên chạy quá nhiều lần/ngày**.

---

## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tự động hóa việc theo dõi giá competitor** mà không cần code.
✔ **Lưu trữ dữ liệu sạch sẽ** trong Google Sheets.
✔ **Nhận thông báo tức thì** khi có thay đổi.
✔ **Cạnh tranh hiệu quả** với đối thủ bằng dữ liệu chính xác.

**🚀 Hãy áp dụng ngay và tiết kiệm thời gian cho mình!**
Nếu có vấn đề, liên hệ với **Yaron Been** qua:
- [LinkedIn](https://www.linkedin.com/in/yaronbeen/)
- [YouTube](https://www.youtube.com/@YaronBeen/videos)

---
**💡 Mẹo cuối**: Nếu muốn **tăng tốc độ scrape**, các sếp có thể **upgrade Bright Data MCP** để tăng số lượng request/month.