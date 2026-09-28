---
title: "📈 **Tự Động Hóa Tin Tức Thị Trường Tài Chính Định Kì Từ Finnhub Đến Telegram - Không Cần Code!**"
description: "Workflow này tự động lấy tin tức thị trường tài chính mới nhất từ Finnhub và gửi cập nhật định kỳ (mỗi 4 giờ) đến Telegram của các sếp. Giúp các nhà đầu tư và quản lý thị trường luôn cập nhật thông tin thời gian thực mà không tốn thời gian tra cứu thủ công."
slug: "tu-dong-hoa-tin-tuc-thi-truong-tai-chinh-finnhub-telegram"
tags: [n8n, automation, no-code, finnhub, telegram, tài chính, thị trường chứng khoán]
keywords: [n8n workflow tài chính, tự động hóa tin tức thị trường, Finnhub Telegram, cập nhật định kỳ, tự động hóa không code]
---

# 🚀 **Tự Động Hóa Tin Tức Thị Trường Tài Chính Định Kì Từ Finnhub Đến Telegram**

### **Giải pháp cho các sếp muốn luôn cập nhật tin tức thị trường mà không tốn thời gian tra cứu thủ công**
Hàng ngày, các nhà đầu tư và quản lý thị trường phải mất nhiều thời gian để tra cứu tin tức mới nhất về thị trường tài chính, cổ phiếu, tiền điện tử hay các sự kiện kinh tế lớn. Với **workflow này**, các sếp sẽ **tự động nhận được tin tức mới nhất từ Finnhub (một API uy tín về dữ liệu thị trường tài chính) và được gửi trực tiếp đến Telegram mỗi 4 giờ**, giúp tiết kiệm thời gian và tăng cường hiệu quả quyết định.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và không bị giới hạn bởi phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần tra cứu thủ công mỗi ngày.
✅ **Cập nhật thời gian thực**: Nhận tin tức mới nhất từ Finnhub (API uy tín).
✅ **Tự động hóa hoàn toàn**: Chỉ cần thiết lập 1 lần, workflow sẽ hoạt động liên tục.
✅ **Cá nhân hóa**: Chọn tin tức theo ngành nghề (cổ phiếu, tiền điện tử, thị trường toàn cầu...).
✅ **Giao diện thân thiện**: Tin tức được gửi trực tiếp đến Telegram với định dạng dễ đọc.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **API Key Finnhub**:
   - Đăng ký tại [Finnhub](https://finnhub.io/) và lấy **API Key** (miễn phí cho các sếp sử dụng trong phạm vi hợp lý).
   - Lưu ý: API Key này sẽ được sử dụng để lấy dữ liệu tin tức từ Finnhub.

2. **Bot Telegram**:
   - Tạo một bot Telegram mới tại [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Thêm bot vào nhóm hoặc chat cá nhân của các sếp để nhận tin tức.

3. **Tham số tùy chọn (nếu muốn gửi hình ảnh)**:
   - Nếu muốn gửi hình ảnh kèm theo tin tức, các sếp cần cung cấp **URL của hình ảnh** (có thể lấy từ Finnhub hoặc nguồn khác).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow theo hai cách:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/5109) và import vào n8n Editor.
- **Copy/Paste JSON** từ link trên vào n8n Editor (đảm bảo không có lỗi syntax).

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này bao gồm **7 node chính**, các sếp cần chú ý cấu hình như sau:

##### **a. Set API Key for Finnhub**
- **Node**: `Set API Key for Finnhub` (type: `set`)
- **Cách cấu hình**:
  - Trong tab **Credentials**, chọn **Add Credential** và nhập:
    - **Name**: `Finnhub API Key` (hoặc tên tùy ý).
    - **Value**: Dán **API Key** từ Finnhub vào trường `apiKey`.
  - Lưu credential và chọn nó trong node `Get Latest News`.

##### **b. Get Latest News**
- **Node**: `Get Latest News` (type: `httpRequest`)
- **Cách cấu hình**:
  - **Method**: `GET`
  - **URL**: `https://finnhub.io/api/v1/news?category=general` (hoặc thay đổi theo danh mục tin tức mong muốn, ví dụ: `category=stocks` cho tin tức cổ phiếu).
  - **Headers**:
    - `Authorization`: `Bearer {apiKey}` (sử dụng credential `Finnhub API Key` đã thiết lập).
    - `Content-Type`: `application/json`
  - **Response Format**: Chọn `JSON`.

##### **c. Code (Xử lý dữ liệu)**
- **Node**: `Code` (type: `code`)
- **Cách cấu hình**:
  - Sử dụng JavaScript để lọc và định dạng tin tức. Ví dụ:
    ```javascript
    // Lấy tin tức mới nhất
    const news = $input.all();
    const latestNews = news[0].json?.result || [];

    // Lọc tin tức mới nhất (ví dụ: 3 tin tức đầu tiên)
    const filteredNews = latestNews.slice(0, 3);

    // Định dạng tin tức
    const formattedNews = filteredNews.map(item => {
      return {
        title: item.headline,
        summary: item.summary,
        url: item.url,
        image: item.image || null
      };
    });

    return { json: { news: formattedNews } };
    ```
  - Các sếp có thể tùy chỉnh logic này để phù hợp với nhu cầu (ví dụ: lọc theo ngành nghề cụ thể).

##### **d. Schedule Trigger - Every 4 Hours**
- **Node**: `Schedule Trigger - Every 4 Hours` (type: `scheduleTrigger`)
- **Cách cấu hình**:
  - Chọn **Cron Expression**: `0 0 */4 * * *` (chạy mỗi 4 giờ).
  - Các sếp có thể điều chỉnh thời gian chạy theo nhu cầu (ví dụ: `0 0 8-16/4 * * *` để chạy từ 8h đến 16h mỗi ngày).

##### **e. Download Image (optional)**
- **Node**: `Download Image (optional)` (type: `httpRequest`)
- **Cách cấu hình**:
  - Chỉ cần thiết lập nếu muốn gửi hình ảnh kèm theo tin tức.
  - **Method**: `GET`
  - **URL**: `{ $node["Code"].json.news[].image }` (lấy từ node `Code`).
  - **Response Format**: `Binary`.

##### **f. Send Text Updates via Telegram**
- **Node**: `Send Text Updates via Telegram` (type: `telegram`)
- **Cách cấu hình**:
  - **Credentials**: Chọn credential Telegram bot (đã tạo trước đó).
  - **Chat ID**: Nhập **ID của chat/nhóm Telegram** (có thể lấy từ `@userinfobot` hoặc `@rawdata_bot`).
  - **Message**: Sử dụng **Expression** để định dạng tin tức:
    ```plaintext
    {{ $node["Code"].json.news.map(item =>
      `📰 **${item.title}**\n\n${item.summary}\n\n🔗 ${item.url}\n\n---
    `).join('') }}
    ```

##### **g. Send Image (with text update) - Optional**
- **Node**: `Send Image (with text update) - Optional` (type: `telegram`)
- **Cách cấu hình**:
  - Chỉ kích hoạt nếu muốn gửi hình ảnh.
  - **Credentials**: Telegram bot.
  - **Chat ID**: Giống như node trước.
  - **Message**: Giống như node `Send Text Updates`.
  - **Media**: Chọn **Binary Data** từ node `Download Image`.

---

#### **3. Kích hoạt ⚡️**
- **Test Run**: Chạy workflow với **dữ liệu mẫu** để kiểm tra kết quả.
- **Bật Active**: Sau khi xác nhận workflow hoạt động ổn định, bật **Active** để chạy tự động theo lịch trình.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tùy chỉnh danh mục tin tức**:
   - Thay đổi tham số `category` trong URL của node `Get Latest News` để lấy tin tức theo ngành:
     - `category=stocks` (cổ phiếu).
     - `category=crypto` (tiền điện tử).
     - `category=forex` (forex).

2. **Gửi báo cáo định kỳ**:
   - Kết hợp với node **Google Sheets** hoặc **Email** để lưu lịch sử tin tức vào bảng tính hoặc gửi báo cáo hàng tuần.

3. **Kết hợp với Slack**:
   - Thay vì Telegram, các sếp có thể gửi tin tức đến **Slack** bằng node `slack` với cấu hình tương tự.

4. **Lưu log hoạt động**:
   - Sử dụng node **Sticky Note** để ghi lại lịch sử chạy workflow và các lỗi nếu có.

5. **Tăng cường tính cá nhân hóa**:
   - Sử dụng **AI (LLM)** để tóm tắt tin tức dài thành ngắn gọn hơn trước khi gửi.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa việc cập nhật tin tức thị trường tài chính** mà không tốn thời gian tra cứu thủ công. Với **cấu hình đơn giản** và **không cần code**, các sếp chỉ cần thiết lập 1 lần là workflow sẽ hoạt động liên tục, giúp **tăng cường hiệu quả quyết định** và **giảm thiểu rủi ro bỏ lỡ tin tức quan trọng**.

**Hãy áp dụng ngay và bắt đầu tự động hóa công việc của mình!** 🚀
Nếu có bất kỳ câu hỏi hoặc gặp khó khăn trong quá trình thiết lập, các sếp có thể tham khảo [hướng dẫn chi tiết của Finnhub](https://finnhub.io/docs/api) hoặc liên hệ cộng đồng n8n tại [n8n Community](https://community.n8n.io/).