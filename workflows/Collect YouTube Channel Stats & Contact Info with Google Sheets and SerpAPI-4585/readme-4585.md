---
title: "🚀 Tự Động Hóa Thông Tin & Thống Kê Channel YouTube + Email Liên Lạc (Không Cần Code)"
description: "Workflow tự động hóa thu thập dữ liệu chi tiết về channel YouTube (số lượng subscriber, video mới, lượt xem) và tìm kiếm email liên lạc công khai từ trang 'About' bằng SerpAPI, cập nhật tự động vào Google Sheets. Giúp các sếp marketing, PR hoặc doanh nghiệp nhanh chóng đánh giá và liên hệ với influencer/inboxer một cách chuyên nghiệp."
slug: "tu-dong-hoa-thong-tin-channel-youtube-google-sheets-serpapi"
tags: [n8n, automation, marketing, youtube, serpapi, google-sheets, no-code]
keywords: [tự động hóa youtube, thu thập dữ liệu channel youtube, serpapi email, google sheets automation, workflow n8n marketing, tự động hóa liên hệ influencer]
---

# 🚀 **Tự Động Hóa Thu Thập Thông Tin Channel YouTube + Email Liên Lạc (Không Cần Code)**

Bạn là một chuyên gia marketing, PR, hoặc doanh nghiệp cần **tự động hóa việc thu thập thông tin chi tiết về channel YouTube** (số lượng subscriber, video mới, lượt xem) và **tìm kiếm email liên lạc công khai** để liên hệ? Hoặc bạn đang phải **làm thủ công** việc này bằng cách copy-paste thông tin từ trang About của channel, mất thời gian và dễ sai sót?

Workflow này sẽ **giải quyết tất cả vấn đề đó** bằng cách:
- **Thu thập dữ liệu tự động** từ YouTube API (số lượng subscriber, video mới, lượt xem).
- **Tìm kiếm email liên lạc** từ trang About của channel (bằng SerpAPI để vượt qua CAPTCHA).
- **Cập nhật dữ liệu vào Google Sheets** một cách tự động, giúp bạn **luôn có một bản dashboard thông minh** để đánh giá và liên hệ với influencer/inboxer một cách chuyên nghiệp.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần copy-paste thủ công từ YouTube, giảm thời gian thu thập dữ liệu từ **30 phút/channel** xuống **vài giây**.
- **Dữ liệu chính xác và cập nhật**: Thu thập từ API chính thức của YouTube và SerpAPI, tránh sai sót như khi đọc từ trang web.
- **Liên hệ hiệu quả**: Nhận email liên lạc công khai (nếu có) để **outreach** một cách chuyên nghiệp.
- **Dashboard thông minh**: Google Sheets tự động cập nhật, giúp bạn **so sánh và lựa chọn** channel phù hợp cho chiến dịch marketing.
- **Hoạt động 24/7**: Workflow chạy tự động mỗi khi có channel mới được thêm vào Google Sheets.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để lưu trữ dữ liệu và trigger).
2. **API Key của SerpAPI** (để tìm kiếm email từ trang About của channel).
   - Đăng ký miễn phí tại: [https://serpapi.com/](https://serpapi.com/)
   - Mua gói phù hợp (gói free chỉ cho phép 100 query/tháng).
3. **Google Cloud Project** (để sử dụng YouTube Data API).
   - Tạo dự án tại [Google Cloud Console](https://console.cloud.google.com/).
   - Bật **YouTube Data API v3** và tạo **API Key**.
4. **Credentials cho n8n**:
   - **Google Sheets OAuth2** (để cập nhật dữ liệu).
   - **SerpAPI API Key** (để tìm kiếm email).
   - **YouTube API Key** (để thu thập dữ liệu channel).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### 1. **Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/4585](https://n8n.io/workflows/4585) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ file và dán vào **Import Workflow** trong n8n.
- **Cách 3**: Sử dụng link trực tiếp:
  ```bash
  https://n8n.io/workflows/4585
  ```

#### 2. **Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này được chia thành **4 phần chính**, các sếp cần chú ý cấu hình các node sau:

##### **🔹 PHẦN 1: Trigger & Thu thập ID Channel**
- **Node: `New Channel Added` (Google Sheets Trigger)**
  - Chọn **Google Sheets OAuth2Api** đã cấu hình trước.
  - Chọn **Sheet và Range** (ví dụ: `Sheet1!A2:A` để lưu URL channel).
  - **Lưu ý**: Cột này phải có tiêu đề là **"Channel URL"** (hoặc cấu hình lại trong node `Set` sau).

- **Node: `Get Channel ID from URL` (HTTP Request)**
  - **URL**: `https://www.googleapis.com/youtube/v3/channels?part=snippet&forUsername={channelUsername}&key={YOUR_YOUTUBE_API_KEY}`
    - Thay `{channelUsername}` bằng giá trị từ cột **Channel URL** (ví dụ: `https://www.youtube.com/@channelname` → `channelname`).
    - Thay `{YOUR_YOUTUBE_API_KEY}` bằng API Key của bạn.
  - **Method**: `GET`.
  - **Response Format**: `JSON`.

##### **🔹 PHẦN 2: Thu thập Thống Kê Channel**
- **Node: `Get Channel Stats` (HTTP Request)**
  - **URL**: `https://www.googleapis.com/youtube/v3/channels?part=statistics&id={channelId}&key={YOUR_YOUTUBE_API_KEY}`
    - Thay `{channelId}` bằng giá trị từ node trước (trong `id` của response).
  - **Method**: `GET`.
  - **Response Format**: `JSON`.
  - **Lưu ý**: Dữ liệu thu thập được bao gồm:
    - `subscriberCount` (số lượng subscriber).
    - `videoCount` (số lượng video).
    - `viewCount` (tổng lượt xem).

- **Node: `Get Recent Video IDs` (HTTP Request)**
  - **URL**: `https://www.googleapis.com/youtube/v3/search?part=id&channelId={channelId}&maxResults=5&order=date&key={YOUR_YOUTUBE_API_KEY}`
    - Thay `{channelId}` bằng giá trị từ node `Get Channel Stats`.
  - **Method**: `GET`.
  - **Response Format**: `JSON`.
  - **Lưu ý**: Node này lấy **5 video mới nhất** của channel.

##### **🔹 PHẦN 3: Tính Tổng Lượt Xem Video Mới**
- **Node: `Prepare views to sum` (Set)**
  - Cấu hình để **trích xuất danh sách video ID** từ response của node `Get Recent Video IDs`.
  - Ví dụ:
    ```json
    {
      "videoIds": $node["Get Recent Video IDs"].json.item.id.videoId
    }
    ```

- **Node: `Sum Video Views` (Code)**
  - **Mã JavaScript**:
    ```javascript
    // Lấy danh sách video ID từ node trước
    const videoIds = $input.all().map(item => item.videoIds);

    // Tính tổng lượt xem cho mỗi video
    const sumViews = async (videoIds) => {
      let totalViews = 0;
      for (const id of videoIds) {
        const response = await $http.request({
          method: 'GET',
          url: `https://www.googleapis.com/youtube/v3/videos?part=statistics&id=${id}&key=${process.env.YOUTUBE_API_KEY}`
        });
        const viewCount = response.json.items[0].statistics.viewCount;
        totalViews += parseInt(viewCount);
      }
      return totalViews;
    };

    // Gọi hàm tính tổng
    const result = await sumViews(videoIds[0]);

    // Trả về kết quả
    return [
      {
        "totalViews": result
      }
    ];
    ```
  - **Lưu ý**:
    - Thêm biến môi trường `YOUTUBE_API_KEY` trong **n8n Settings > Environment Variables**.
    - Node này sẽ **tính tổng lượt xem** của 5 video mới nhất.

##### **🔹 PHẦN 4: Tìm Email Liên Lạc (SerpAPI)**
- **Node: `Get Channel Email (SerpAPI)` (HTTP Request)**
  - **URL**: `https://serpapi.com/search.json?engine=google&q=site%3Ahttps://www.youtube.com/@{channelUsername}&api_key={YOUR_SERPAPI_KEY}`
    - Thay `{channelUsername}` bằng tên channel (ví dụ: `channelname`).
    - Thay `{YOUR_SERPAPI_KEY}` bằng API Key của SerpAPI.
  - **Method**: `GET`.
  - **Response Format**: `JSON`.
  - **Lưu ý**:
    - SerpAPI sẽ tìm kiếm trên trang About của channel để lấy email công khai.
    - Nếu không tìm thấy email, node sẽ trả về `null`.

##### **🔹 PHẦN 5: Chuẩn bị & Cập Nhật Dữ liệu vào Google Sheets**
- **Node: `Prepare Sheet Data` (Set)**
  - Cấu hình để **ghép tất cả dữ liệu** từ các node trước thành một object duy nhất.
  - Ví dụ:
    ```json
    {
      "channelUrl": $input.all()[0].json.snippet.channelUrl,
      "channelName": $input.all()[0].json.snippet.title,
      "subscriberCount": $input.all()[0].json.statistics.subscriberCount,
      "videoCount": $input.all()[0].json.statistics.videoCount,
      "totalViews": $input.all()[0].json.statistics.viewCount,
      "recentVideoViews": $input.all()[1].json.totalViews,
      "email": $input.all()[2].json.email || "Không tìm thấy email"
    }
    ```

- **Node: `Update Channel Insights` (Google Sheets)**
  - Chọn **Google Sheets OAuth2Api** đã cấu hình.
  - **Range**: Cột tương ứng với cột **Channel URL** (ví dụ: `Sheet1!B2:H2`).
  - **Operation**: `update`.
  - **Lưu ý**:
    - Dữ liệu sẽ được cập nhật vào **cột B đến H** (hoặc cấu hình lại theo ý muốn).
    - Cột **A** phải là **Channel URL** (để trigger workflow).

---

#### 3. **Kích hoạt ⚡️**
1. **Test Run** với một channel mẫu (ví dụ: `@n8nworkflows`).
2. Kiểm tra **Google Sheets** để xem dữ liệu có được cập nhật không.
3. **Bật Active workflow** nếu test thành công.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CẢI TIẾN TRONG QUÁ TRÌNH SỬ DỤNG]
- **Thêm cột "Status"** vào Google Sheets để đánh dấu channel đã được **outreach** hay chưa.
- **Kết hợp với Slack/Telegram**: Sử dụng node **Slack Webhook** hoặc **Telegram Bot** để thông báo khi workflow hoàn thành.
- **Lưu log lỗi**: Thêm node **Set** hoặc **Code** để ghi log lỗi (ví dụ: khi SerpAPI không tìm thấy email) vào Google Sheets.
- **Báo cáo định kỳ**: Sử dụng **n8n Cron Trigger** để chạy workflow hàng tuần và gửi báo cáo tổng hợp qua email (node **Email**).
- **Tự động xóa channel cũ**: Thêm logic để xóa dữ liệu của channel đã không hoạt động trong 6 tháng (sử dụng node **Code** để kiểm tra ngày cập nhật cuối cùng).
:::

---

### 📌 **Kết luận**
Workflow này giúp **tự động hóa hoàn toàn** quá trình thu thập thông tin channel YouTube và tìm kiếm email liên lạc, **giúp các sếp tiết kiệm thời gian và nâng cao hiệu quả outreach**. Bằng cách **cấu hình đơn giản** và **chạy 24/7**, bạn sẽ luôn có một **bản dashboard thông minh** để đánh giá và liên hệ với influencer/inboxer một cách chuyên nghiệp.

**Hãy áp dụng ngay và tự động hóa công việc marketing của mình!** 🚀

---
:::note[LƯU Ý CUỐI CÙNG]
- Nếu gặp lỗi **CORS** hoặc **quota exceeded** với YouTube API, hãy kiểm tra lại **API Key** và **quota** tại [Google Cloud Console](https://console.cloud.google.com/).
- Đối với SerpAPI, nếu dùng gói free, hạn chế số lượng channel thu thập (mỗi query chỉ cho phép 100 lần/tháng).
- Nếu cần hỗ trợ, liên hệ với tác giả Yaron Been qua:
  - [LinkedIn](https://www.linkedin.com/in/yaronbeen/)
  - [YouTube](https://www.youtube.com/@YaronBeen/videos)
  - Email: Yaron@nofluff.online
:::

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::