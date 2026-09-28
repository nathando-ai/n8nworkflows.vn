---
title: "🚀 Tự động trích xuất thông tin Instagram Profile với Apify và Google Sheets trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu tài khoản Instagram (followers, bio, website...) qua Apify và lưu trữ trực tiếp vào Google Sheets không cần code."
slug: "tu-dong-trich-xuat-thong-tin-instagram-profile-voi-apify-va-google-sheets"
tags: [n8n, automation, no-code, apify, instagram-scraper, google-sheets, marketing]
keywords: [n8n workflow, cào dữ liệu instagram, apify instagram scraper, google sheets automation, marketing automation]
---

# 🚀 Tự động trích xuất thông tin Instagram Profile với Apify và Google Sheets

Các sếp làm marketing, influencer outreach hay nghiên cứu thị trường chắc chắn đã tốn rất nhiều thời gian để thủ công tìm kiếm, copy các thông tin từ tài khoản Instagram như số lượng người theo dõi (followers), tiểu sử (bio), website hay ảnh đại diện vào file Excel. 

Việc làm thủ công này không chỉ cực kỳ tốn thời gian mà còn dễ sai sót. Giải pháp là gì? Bài viết này sẽ hướng dẫn các sếp thiết lập một **workflow n8n tự động hóa 100%**, giúp nhận tên tài khoản Instagram qua biểu mẫu, cào dữ liệu thời gian thực bằng **Apify** và tự động đồng bộ hóa toàn bộ vào **Google Sheets**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần copy-paste thủ công thông tin từng Influencer hay đối thủ.
- **Dữ liệu luôn cập nhật:** Lấy thông tin chính xác theo thời gian thực (real-time) thông qua Apify API.
- **Lưu trữ khoa học:** Tự động sắp xếp gọn gàng vào Google Sheets để làm chiến dịch outreach, phân tích CRM.
- **Vận hành tự động 24/7:** Kích hoạt qua Form nhanh chóng, hoạt động mượt mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Apify:** Cần có Apify API Token và Task ID của Actor cào Instagram Profile.
- **Tài khoản Google:** Đã kết nối Google Sheets OAuth2 với n8n để cấp quyền ghi dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ JSON cấu trúc workflow hoặc sử dụng tính năng import file JSON vào giao diện n8n Editor. Workflow bao gồm 4 nodes chính:
- `Provide Usernames` (`formTrigger`)
- `Scrape Instagram Profile via Apify` (`httpRequest`)
- `Format Instagram Profile Data` (`set`)
- `Append Profile to Google Sheet` (`googleSheets`)

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy thành công, các sếp cần cấu hình chính xác các điểm sau:

- **Node `Provide Usernames` (Form Trigger):** Node này hoạt động như điểm khởi đầu. Sếp có thể nhập trực tiếp username cần cào hoặc nhúng form này vào trang web để khách hàng/nhân sự nhập vào. Input mẫu:
  ```json
  {
    "username": "influencer_1"
  }
  ```

- **Node `Scrape Instagram Profile via Apify` (HTTP Request):** 
  - Đổi phương thức thành `POST`.
  - Cấu hình URL với Task ID và Token của sếp:
    `https://api.apify.com/v2/actor-tasks/<TASK_ID>/run-sync-get-dataset-items?token=<API_TOKEN>`
  - Body Parameters truyền vào:
    ```json
    {
      "input": {
        "usernames": ["={{ $json.username }}"]
      }
    }
    ```

- **Node `Format Instagram Profile Data` (Set):** 
  Node này giúp làm sạch dữ liệu trả về từ Apify để khớp với các cột trên Google Sheets của sếp:
  - `Username` ➜ `{{$json.username}}`
  - `Full Name` ➜ `{{$json.fullName}}`
  - `Followers` ➜ `{{$json.followersCount}}`
  - `Following` ➜ `{{$json.followsCount}}`
  - `Bio` ➜ `{{$json.biography}}`
  - `Profile Pic URL` ➜ `{{$json.profilePicUrl}}`
  - `Website` ➜ `{{$json.externalUrl}}`

- **Node `Append Profile to Google Sheet` (Google Sheets):**
  - Chọn Credentials Google Sheets OAuth2.
  - Đặt tên Sheet chính xác là: `Scraped_Influencer_Data`.
  - Đảm bảo các cột trong Google Sheet khớp với các trường dữ liệu: *Username, Full Name, Followers, Following, Bio, Profile Pic URL, Website*.

#### 3. Kích hoạt ⚡️
- Chạy thử (Test step / Execute node) với một username mẫu để kiểm tra dữ liệu trả về.
- Sau khi test thành công, bật công tắc **Active** để workflow sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Đọc danh sách từ Google Sheets:** Thay vì dùng Form nhập từng tài khoản, sếp có thể cấu hình n8n đọc một danh sách hàng trăm username từ Google Sheets rồi chạy vòng lặp (Loop) tự động cào hàng loạt.
- **Chống trùng lặp:** Thêm một node `IF` để kiểm tra xem username đã tồn tại trong Sheet hay chưa trước khi gọi API Apify, giúp tiết kiệm chi phí credit.
- **Gửi thông báo:** Tích hợp thêm node Slack hoặc Telegram để nhận thông báo ngay lập tức mỗi khi một profile mới được cào và lưu trữ thành công.
- **Bộ lọc thông minh:** Thêm điều kiện lọc chỉ lưu những tài khoản có số lượng followers lớn hơn một mức nhất định (ví dụ > 10,000 followers).

### 📌 Kết luận
Workflow tự động hóa cào Instagram profile này là một trợ đắc lực giúp các nhà tiếp thị, nhà sáng tạo nội dung và doanh nghiệp tiết kiệm hàng giờ đồng hồ thao tác tay. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa hiệu suất công việc nhé!