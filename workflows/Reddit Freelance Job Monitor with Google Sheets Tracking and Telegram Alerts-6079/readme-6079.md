---
title: "🚀 Tự Động Hóa Theo Dõi Công Việc Freelance Trên Reddit Với Google Sheets & Telegram Alerts"
description: "Workflow tự động hóa 100% không code để quét, lọc và cảnh báo ngay lập tức các công việc freelance trả lương trên Reddit, đồng thời ghi chép vào Google Sheets để theo dõi hiệu quả. Giúp các sếp tiết kiệm thời gian lên tới 10 giờ/tuần và không bỏ lỡ bất kỳ cơ hội nào."
slug: "tieu-doi-cong-viec-freelance-reddit-google-sheets-telegram"
tags: [n8n, automation, lead-generation, freelance, google-sheets, telegram-bot]
keywords: [tự động hóa freelance, theo dõi công việc reddit, google sheets automation, telegram alert, n8n workflow tự động]
---

# 🚀 **Tự Động Hóa Theo Dõi Công Việc Freelance Trên Reddit Với Google Sheets & Telegram Alerts**

### **Giải pháp cho các sếp không muốn bỏ lỡ cơ hội freelance**
Hàng ngày, các sếp phải dành nhiều giờ để quét các diễn đàn như Reddit để tìm kiếm công việc freelance phù hợp. Tuy nhiên, với lượng thông tin khổng lồ và tính chất không liên tục của các bài đăng, việc theo dõi thủ công không chỉ tốn thời gian mà còn dễ bỏ lỡ cơ hội. **Workflow này tự động hóa toàn bộ quy trình:**
- Quét các bài đăng yêu cầu freelancer trên Reddit.
- Lọc ra những công việc **trả lương** và **mới nhất**.
- Ghi chép vào **Google Sheets** để theo dõi và quản lý.
- **Cảnh báo ngay lập tức** qua Telegram khi có công việc mới phù hợp.

Kết quả? **Tiết kiệm tối thiểu 10 giờ/tuần** và đảm bảo không bỏ lỡ bất kỳ cơ hội nào!

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** và ổn định, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) thay vì dùng phiên bản miễn phí trên cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** lên tới 10 giờ/tuần (không phải quét thủ công Reddit).
✅ **Lọc chính xác** chỉ những công việc **trả lương** và **mới nhất**.
✅ **Theo dõi dễ dàng** với Google Sheets (có thể sắp xếp, phân loại, và chia sẻ với team).
✅ **Cảnh báo tức thời** qua Telegram (không bỏ lỡ bất kỳ cơ hội nào).
✅ **Hoạt động liên tục** 24/7, không phụ thuộc vào thời gian làm việc của cá nhân.
✅ **Mở rộng dễ dàng** (có thể kết nối với Slack, Email, hoặc các công cụ khác).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Reddit** (để quét các bài đăng).
2. **Google Sheets** (để lưu trữ dữ liệu).
   - Một **Sheet** riêng để lưu thông tin công việc (các sếp có thể tạo trước với các cột: *Tên Công Việc, Link, Ngày Bắt Đầu, Lương, Thông Tin Liên Hệ*).
3. **Bot Telegram** (để nhận cảnh báo).
   - Tạo bot qua [@BotFather](https://t.me/BotFather) và lấy **API Token**.
4. **API Key của Reddit** (nếu muốn tăng tốc độ quét).
   - Đăng ký tại [Reddit API](https://www.reddit.com/prefs/apps) để tạo ứng dụng và lấy **Client ID & Secret**.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/6079) (hoặc sao chép từ link trên).
- Trong **n8n Editor**, nhấn **Import** và dán JSON vào.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **10 node**, nhưng các node quan trọng nhất cần cấu hình kỹ như sau:

##### **A. Node "Look for freelance requirement posts" (HTTP Request)**
- **URL**: `https://www.reddit.com/r/freelance/search.json?q=freelance+hire&sort=new&t=day`
  - Đây là URL quét các bài đăng mới nhất trong subreddit `freelance` (có thể thay đổi theo nhu cầu).
- **Headers**:
  - `User-Agent`: `Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36`
  - **Nếu dùng API Reddit**, thêm `Authorization: Bearer {API_KEY}`.

##### **B. Node "Check present Rows" (Google Sheets)**
- **Credentials**: Chọn tài khoản Google đã kết nối với n8n.
- **Sheet Name**: Điền tên **exact** của Sheet đã tạo trước (ví dụ: `Freelance_Jobs`).
- **Range**: `Sheet1!A:Z` (hoặc cột cụ thể nếu đã định dạng trước).

##### **C. Node "Inform User in telegram" (Telegram Bot)**
- **Credentials**: Chọn bot Telegram đã tạo.
- **Chat ID**: Lấy từ [@userinfobot](https://t.me/userinfobot) và gửi tin nhắn cho bot (bot sẽ trả về Chat ID).
- **Message Template**:
  ```json
  "🚀 **Công việc freelance mới được phát hiện!** 🚀\n\n🔹 **Tên**: {{ $node["Extract Post Metadata"].json["data"]["title"] }}\n🔹 **Link**: {{ $node["Extract Post Metadata"].json["data"]["url"] }}\n🔹 **Lương**: {{ $node["Extract Post Metadata"].json["data"]["selftext"] | regexMatch('(?i)(?:lương|pay|budget): ([^\\n]+)' ) | first }}\n🔹 **Ngày đăng**: {{ $node["Get UTC of Post"].json["UTC"] }}"
  ```
  - **Lưu ý**: Nếu bài đăng không có thông tin lương, có thể bỏ phần `Lương` hoặc sử dụng logic mặc định.

##### **D. Node "Filter Unique Posts" (Code)**
- **JavaScript Code**:
  ```javascript
  // Lọc bỏ trùng lặp bằng cách so sánh URL
  const seen = new Set();
  return $input.all().filter(item => {
    const url = item.json.data.url;
    if (!seen.has(url)) {
      seen.add(url);
      return true;
    }
    return false;
  });
  ```
  - **Lý do**: Tránh ghi chép trùng lặp cùng một công việc nhiều lần.

##### **E. Node "Save in sheets" (Google Sheets)**
- **Credentials**: Giống như node "Check present Rows".
- **Range**: `Sheet1!A2` (đảm bảo bắt đầu từ hàng 2 để tránh trùng với tiêu đề cột).
- **Values**: Sử dụng cấu trúc dữ liệu từ node trước:
  ```json
  [
    ["Tên Công Việc", $node["Extract Post Metadata"].json["data"]["title"]],
    ["Link", $node["Extract Post Metadata"].json["data"]["url"]],
    ["Lương", $node["Extract Post Metadata"].json["data"]["selftext"] | regexMatch('(?i)(?:lương|pay|budget): ([^\\n]+)' ) | first },
    ["Ngày Đăng", $node["Get UTC of Post"].json["UTC"]]
  ]
  ```

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Chạy workflow với **dữ liệu mẫu** (nếu có) để kiểm tra các node hoạt động như thế nào.
  - Kiểm tra **Google Sheets** và **Telegram** để xác nhận cảnh báo được gửi đúng.
- **Bật Active**:
  - Sau khi kiểm tra thành công, chuyển trạng thái workflow sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tăng tốc độ quét**:
   - Thay đổi URL trong node `HTTP Request` để quét nhiều subreddit khác (ví dụ: `r/forhire`, `r/WorkOnline`).
   - Nếu có **API Key Reddit**, tăng tốc độ và giảm giới hạn request.

2. **Cải thiện lọc công việc**:
   - Sử dụng **node `Filter`** để lọc thêm các từ khóa như "remote", "full-time", "high-paying".
   - Ví dụ:
     ```javascript
     // Node Filter (JavaScript)
     return $input.all().filter(item => {
       const text = item.json.data.selftext.toLowerCase();
       return text.includes("remote") || text.includes("full-time") || text.includes("high-paying");
     });
     ```

3. **Gửi báo cáo định kỳ**:
   - Kết hợp với **node `Schedule Trigger`** để gửi báo cáo tổng hợp hàng tuần qua Email hoặc Telegram.
   - Ví dụ: "Tổng số công việc mới trong tuần: 15, trong đó 5 công việc cao lương".

4. **Kết nối với Slack**:
   - Thay thế node `Telegram` bằng `Slack` để cảnh báo trong kênh team.

5. **Lưu log hoạt động**:
   - Sử dụng **node `StickyNote`** để ghi lại lỗi hoặc thông tin debug.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa việc theo dõi công việc freelance trên Reddit mà **không cần viết một dòng code**. Với việc chỉ cần **cấu hình vài node quan trọng**, các sếp sẽ:
✔ **Tiết kiệm thời gian** đáng kể.
✔ **Không bỏ lỡ bất kỳ cơ hội nào** nhờ cảnh báo tức thời.
✔ **Quản lý dễ dàng** với Google Sheets.

**Hãy import workflow ngay hôm nay và bắt đầu tự động hóa công việc của mình!** 🚀

---
**💡 Cần hỗ trợ thêm?**
- Đăng ký **VPS n8n** để workflow chạy 24/7: [TinoHost](https://tino.vn/vps-n8n?affid=388)
- Trao đổi trên **community n8n**: [n8n.io/community](https://n8n.io/community)