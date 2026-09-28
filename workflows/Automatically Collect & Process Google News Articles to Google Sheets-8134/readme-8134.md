---
title: "📰 Tự Động Thu Thập Tin Tức Google News Vào Google Sheets"
description: "Workflow n8n tự động quét tin tức theo chủ đề từ Google News, lọc trùng lặp và lưu trữ có hệ thống vào Google Sheets. Giải pháp hoàn hảo cho việc nghiên cứu thị trường và theo dõi xu hướng."
slug: "tu-dong-thu-thap-tin-tuc-google-news-vao-sheets"
tags: [n8n, automation, no-code, google-news, google-sheets, data-collection]
keywords: [n8n workflow, tự động hóa tin tức, thu thập dữ liệu google news, lưu tin tức vào sheets, theo dõi xu hướng]
---

# 📰 Tự Động Thu Thập Tin Tức Google News Vào Google Sheets

Việc theo dõi tin tức, xu hướng ngành (industry trends) hoặc đối thủ cạnh tranh thường tốn rất nhiều thời gian. Các sếp phải mở hàng chục tab trình duyệt, đọc lướt qua các trang báo, rồi sao chép link vào bảng tính để phân tích sau. Quy trình thủ công này không chỉ chậm chạp mà còn dễ bỏ sót thông tin quan trọng do sự quá tải về dữ liệu.

Workflow này giải quyết triệt để vấn đề đó bằng cách tự động hóa 100% quy trình: Nó sẽ định kỳ truy cập các nguồn tin tức (RSS) của Google News theo các chủ đề (topic) mà các sếp quan tâm, làm sạch dữ liệu, loại bỏ các bài viết trùng lặp và tự động ghi nhận vào Google Sheets. Kết quả là một cơ sở dữ liệu tin tức sạch sẽ, có cấu trúc, sẵn sàng cho việc phân tích mà không cần tốn một giây nào cho thao tác thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian nghiên cứu:** Tự động gom tin tức hàng tuần, không cần đọc lướt thủ công.
- **Dữ liệu sạch & Không trùng lặp:** Node `Item Lists` đảm bảo mỗi link tin chỉ xuất hiện một lần trong bảng tính.
- **Cá nhân hóa theo chủ đề:** Có thể cấu hình nhiều topic khác nhau (ví dụ: AI, Marketing, Kinh tế) để theo dõi song song.
- **Cơ sở dữ liệu lịch sử:** Xây dựng kho lưu trữ tin tức theo thời gian, hỗ trợ việc so sánh xu hướng qua các tuần/tháng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã cài đặt hoặc sử dụng n8n Cloud.
- **Tài khoản Google:** Để tạo và kết nối Google Sheets.
- **Google Sheets:** Một bảng tính (Spreadsheet) trống hoặc có sẵn các cột tiêu đề (ví dụ: Title, Link, Date, Source).
- **Credentials:** Đã tạo và lưu credentials `googleSheetsOAuth2Api` trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n của các sếp.
2. Chọn **Import from URL** hoặc **Import from File**.
3. Dán link workflow gốc: `https://n8n.io/workflows/8134` hoặc tải file JSON về và import.
4. Workflow sẽ hiện ra với các node được nhóm lại theo các khu vực: *Gather Information*, *Clean & New*, và *Save in Sheets*.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất để workflow hoạt động đúng ý các sếp. Hãy kiểm tra kỹ các node sau:

*   **Node: `Trigger: Monday 09:00` (Cron)**
    *   Mặc định workflow chạy vào thứ Hai lúc 9:00 sáng.
    *   Các sếp có thể chỉnh lại thời gian theo nhu cầu (ví dụ: hàng ngày lúc 8:00 sáng để có tin mới nhất).

*   **Node: `RSS Read — Google News (TOPIC_1)` & `RSS Read — Google News (TOPIC_2)`**
    *   Đây là các node lấy dữ liệu thô.
    *   **Lưu ý quan trọng:** Các sếp cần thay đổi URL RSS trong phần cấu hình của node này.
    *   *Cách lấy URL RSS Google News:*
        1. Mở Google News trên trình duyệt.
        2. Tìm kiếm từ khóa hoặc chủ đề cần quan tâm (ví dụ: "Artificial Intelligence").
        3. Xem URL trên thanh địa chỉ. Nó sẽ có dạng: `https://news.google.com/rss/search?q=Artificial+Intelligence&hl=vi&gl=VN&ceid=VN:vi`.
        4. Copy URL này và dán vào trường `Url` của node RSS.
    *   Nếu muốn theo dõi nhiều hơn 2 chủ đề, các sếp có thể nhân bản (duplicate) node này và thêm vào node `Merge Feeds (Append)`.

*   **Node: `Set (Clean URL + Fields)`**
    *   Node này giúp chuẩn hóa dữ liệu trước khi lưu.
    *   Kiểm tra các trường dữ liệu (fields) được ánh xạ: `Title`, `Link`, `Date`, `Source`.
    *   Đảm bảo các trường này khớp với tiêu đề cột trong Google Sheets của các sếp.

*   **Node: `Item Lists: Unique by URL`**
    *   Node này tự động loại bỏ các bài viết có cùng URL.
    *   Đảm bảo tham số `operation` đang được đặt là `removeDuplicates` và trường so sánh là `Link` (hoặc trường chứa URL tin tức).

*   **Node: `Append new Links` (Google Sheets)**
    *   **Credentials:** Chọn credentials `googleSheetsOAuth2Api` mà các sếp đã tạo.
    *   **Document ID:** Dán ID của Google Sheet mà các sếp muốn lưu dữ liệu.
    *   **Sheet Name:** Chọn tên tab (sheet) trong file tính.
    *   **Operation:** Mặc định là `appendOrUpdate`. Các sếp nên giữ nguyên hoặc chọn `append` nếu muốn chỉ thêm mới.
    *   **Mapping:** Đảm bảo các cột trong n8n (Title, Link, Date...) được ánh xạ đúng vào các cột tương ứng trong Google Sheets.

#### 3. Kích hoạt ⚡️
1. Nhấn nút **Execute Workflow** để chạy thử với dữ liệu mẫu.
2. Kiểm tra xem dữ liệu có được đưa vào Google Sheets đúng không.
3. Nếu mọi thứ ổn, bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy theo lịch đã định.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp AI để tóm tắt:** Thêm một node `OpenAI` hoặc `Anthropic` sau bước lọc để tóm tắt nội dung tin tức và lưu thêm cột "Summary" vào Sheets.
- **Gửi báo cáo qua Email/Slack:** Sau khi lưu vào Sheets, thêm node `Send Email` hoặc `Slack` để gửi link bảng tính hoặc tóm tắt nhanh các tin nổi bật nhất trong tuần cho team.
- **Lọc theo nguồn tin:** Sử dụng node `Filter` để chỉ giữ lại tin từ các nguồn uy tín (ví dụ: chỉ lấy tin từ VnExpress, Tuổi Trẻ, TechCrunch...) bằng cách kiểm tra trường `Source`.
- **Phân tích cảm xúc (Sentiment Analysis):** Kết nối với API phân tích cảm xúc để đánh giá tin tức là tích cực, tiêu cực hay trung lập, giúp hiểu rõ hơn về dư luận.

### 📌 Kết luận
Việc tự động hóa thu thập tin tức không chỉ giúp các sếp tiết kiệm hàng giờ mỗi tuần mà còn đảm bảo không bỏ lỡ bất kỳ xu hướng quan trọng nào. Với workflow này, các sếp có thể tập trung vào việc phân tích và ra quyết định thay vì mất thời gian tìm kiếm và sao chép dữ liệu. Hãy import và tùy chỉnh ngay để bắt đầu xây dựng hệ thống theo dõi thông tin chuyên nghiệp của riêng mình!