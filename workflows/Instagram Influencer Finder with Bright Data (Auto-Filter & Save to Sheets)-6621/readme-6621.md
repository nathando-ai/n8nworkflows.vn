---
title: "🚀 Tự động tìm kiếm và lọc Influencer Instagram với Bright Data & n8n"
description: "Hướng dẫn xây dựng hệ thống tự động quét profile Instagram, lọc tài khoản chất lượng cao theo tiêu chí marketing và lưu vào Google Sheets với n8n."
slug: "tu-dong-tim-kiem-va-loc-instagram-influencer-bright-data-n8n"
tags: [n8n, automation, instagram, bright-data, lead-generation, google-sheets]
keywords: [n8n workflow, lọc instagram influencer, bright data n8n, tự động hóa marketing, scrape instagram profile]
---

# 🚀 Tự động tìm kiếm và lọc Influencer Instagram với Bright Data & n8n

Việc tìm kiếm và sàng lọc các Influencer (KOL/KOC) chất lượng trên Instagram để làm marketing, hợp tác truyền thông hay nghiên cứu thị trường thường tiêu tốn rất nhiều thời gian. Các sếp thường phải thủ công kiểm tra lượng follower, tỷ lệ tương tác (engagement rate), loại tài khoản xem có chuẩn business hay không. 

Quên cách làm thủ công đó đi! Bài viết này sẽ hướng dẫn các sếp triển khai một **n8n workflow hoàn toàn tự động** kết hợp với **Bright Data** để quét dữ liệu profile, tự động lọc theo các tiêu chí vàng và lưu ngay danh sách khách hàng tiềm năng vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn phải check tay từng profile Instagram xem có đủ điều kiện hợp tác hay không.
- **Lọc chuẩn xác:** Hệ thống tự động áp dụng các tiêu chí khắt khe (Follower > 10k, có tích xanh, tài khoản doanh nghiệp, tương tác tốt).
- **Database gọn gàng:** Chỉ những tài khoản thực sự chất lượng mới được ghi nhận vào Google Sheets.
- **Dễ dàng mở rộng:** Có thể nâng cấp để quét hàng loạt danh sách dài hoặc tích hợp thêm các bước gửi email outreach tự động.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã hoạt động (Self-hosted hoặc Cloud).
- **Tài khoản Bright Data:** Cần có API Key/Credentials để sử dụng dịch vụ cào dữ liệu Instagram ([Đăng ký Bright Data tại đây](https://get.brightdata.com/1tndi4600b25)).
- **Google Sheets:** Chuẩn bị sẵn một file Google Sheets để lưu lead (có thể tham khảo mẫu template tại [đây](https://docs.google.com/spreadsheets/d/1hZFawprfr_a6JC26-0LCQUoz-VuX58A2YxlphQ9Kn_0/edit?usp=sharing)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ JSON của workflow hoặc sử dụng file template được cung cấp bởi tác giả Yaron Been để dán trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 6 nodes chính được chia làm 3 phần quan trọng:

* **Trigger - Start Manually (`manualTrigger`) & Set Instagram Profile URL (`set`):**
  - Node `Set` dùng để nhập thủ công URL profile Instagram cần kiểm tra. Các sếp có thể thay đổi nguồn dữ liệu này để nhận URL từ Google Sheets, Form đăng ký, Airtable hoặc Webhook tùy nhu cầu.
* **Bright Data - Scrape IG Profile (`@brightdata/n8n-nodes-brightdata.brightData`):**
  - Cần cấu hình **Credentials** cho Bright Data bằng API Key của sếp.
  - Node này sẽ gửi URL profile sang Bright Data để lấy dữ liệu cấu trúc thời gian thực gồm: Số lượng follower, engagement rate, trạng thái tài khoản (cá nhân/doanh nghiệp), tích xanh,...
* **Filter - Qualified Profile? (`if`):**
  - Node điều kiện kiểm tra 4 tiêu chí vàng của profile:
    - **✔ Verified Account** (Đã xác thực / có tích xanh)
    - **👥 Follower count > 10,000**
    - **💬 Engagement rate > 0.5%**
    - **💼 Is a Professional/Business account** (Tài khoản chuyên nghiệp/doanh nghiệp)
  - Chỉ những profile vượt qua **tất cả** điều kiện này mới được đi tiếp.
* **Save to Google Sheet (`googleSheets`) & Skip - Unqualified Profile (`noOp`):**
  - Tại node `Save to Google Sheet`, cấu hình kết nối **Google Sheets OAuth2 API**, chọn đúng File và Sheet Name tương ứng.
  - Các thông tin như Username, số followers, engagement, bio, contact sẽ được tự động ghi vào bảng.
  - Nếu profile không đạt điều kiện, node `Skip` sẽ kết thúc luồng êm ái mà không làm rác database.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (`Test workflow`) với một vài URL Instagram mẫu để kiểm tra dữ liệu trả về từ Bright Data và việc ghi nhận vào Google Sheets.
- Sau khi test thành công, bật nút **Active** để đưa workflow vào trạng thái hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng nguồn đầu vào:** Thay vì nhập tay từng URL ở node `Set`, hãy kết nối với một Google Sheets chứa danh sách hàng trăm tài khoản để n8n tự động chạy vòng lặp (Loop/Split In Batches).
- **Tự động hóa tiếp cận:** Sau bước `Save to Google Sheet`, có thể gắn thêm node gửi tin nhắn qua Telegram, Slack hoặc gửi Email mời hợp tác nếu profile đạt chuẩn.
- **Lưu log lỗi:** Thêm các nhánh Error Trigger để ghi lại các trường hợp lỗi kết nối API từ Bright Data nhằm xử lý kịp thời.

### 📌 Kết luận
Với sự kết hợp mạnh mẽ giữa n8n và Bright Data, các sếp giờ đây đã sở hữu một "cỗ máy" tìm kiếm và sàng lọc Influencer tự động 100%. Áp dụng ngay để tối ưu hóa chiến dịch Influencer Marketing của doanh nghiệp mình nhé!