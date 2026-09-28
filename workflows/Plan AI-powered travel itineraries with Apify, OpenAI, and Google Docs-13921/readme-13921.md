---
title: "🌍 **Tự Động Hoá Lập Kế Hoạch Du Lịch AI-Powered Với Apify, OpenAI & Google Docs - Không Cần Code!**"
description: "Workflow tự động hóa hoàn toàn giúp các sếp lập kế hoạch du lịch chi tiết, cá nhân hóa từ việc nhập thông tin sân bay, ngày đi, số người đi đến việc tìm kiếm khách sạn, vé máy bay và gợi ý điểm tham quan thông minh - tất cả được tổng hợp vào Google Doc và gửi cho khách hàng chỉ trong vài giây. Giảm thời gian làm thủ công từ 3-5 tiếng xuống còn 1 phút!"
slug: "tieu-dong-hoa-ke-hoach-du-lich-ai-powered-apify-openai-google-docs"
tags: [n8n, automation, no-code, ai-powered, apify, openai, google-docs, du-lich, travel-planning]
keywords: [n8n workflow du lịch, tự động hóa kế hoạch du lịch, apify n8n, openai du lịch, google docs tự động, lập kế hoạch du lịch ai, không cần code]
---

# 🚀 **Tự Động Hoá Lập Kế Hoạch Du Lịch AI-Powered - Từ Form Đến Google Doc Chỉ Với Một Click**

### **Nỗi Đau Của Các Sếp Trong Ngành Du Lịch**
Các sếp trong ngành du lịch hoặc các dịch vụ tổ chức tour phải chịu những thách thức lớn khi phải:
- **Lập kế hoạch du lịch thủ công** cho từng khách hàng, mất từ **30 phút đến 2 tiếng** cho mỗi đơn hàng.
- **Tìm kiếm và so sánh khách sạn/vé máy bay** trên nhiều trang web khác nhau, dễ bị lỗi hoặc thiếu thông tin chính xác.
- **Không có gợi ý cá nhân hóa** về điểm tham quan, nhà hàng, hoặc lịch trình chi tiết, khiến khách hàng cảm thấy không hài lòng.
- **Không thể tự động hóa** quá trình này vì thiếu kiến thức về code hoặc API.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa 100% quá trình** từ khi khách hàng nhập thông tin đến khi nhận được kế hoạch du lịch hoàn chỉnh.
✅ **Sử dụng AI (OpenAI GPT-4o-mini)** để gợi ý điểm tham quan, nhà hàng, và lịch trình chi tiết dựa trên sở thích và yêu cầu của khách hàng.
✅ **Scrape dữ liệu khách sạn và vé máy bay** từ Booking.com và Google Flights **mà không cần API chính thức** (thông qua Apify).
✅ **Tổng hợp tất cả thông tin vào một Google Doc** với định dạng chuyên nghiệp, dễ đọc và chia sẻ.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm thời gian lên đến 90%** so với cách làm thủ công (giảm từ 3-5 tiếng xuống còn **1 phút** cho mỗi đơn hàng).
- **Tăng trải nghiệm khách hàng** với kế hoạch du lịch **cá nhân hóa**, bao gồm gợi ý AI về điểm tham quan, nhà hàng, và lịch trình chi tiết.
- **Chính xác và cập nhật** vì dữ liệu được scrape từ nguồn chính (Booking.com, Google Flights) và xử lý bởi AI.
- **Hoạt động liên tục** mà không cần can thiệp của nhân viên, giảm thiểu lỗi và tăng hiệu suất.
- **Dễ dàng mở rộng** cho nhiều khách hàng đồng thời, phù hợp với các tour operator hoặc dịch vụ du lịch lớn.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi Bắt Đầu**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Apify** (miễn phí hoặc trả phí):
   - [Đăng ký Apify](https://apify.com/) và lấy **API Token**.
   - Thêm token này vào n8n với **credentials**:
     - `apifyApi` (dùng cho node `Booking.com Scraper` và `Google Flights Scraper`).
     - `httpQueryAuth` (parameter `token`).
2. **API Key OpenAI**:
   - [Đăng ký OpenAI](https://platform.openai.com/) và lấy **API Key**.
   - Thêm vào n8n với **credentials**: `openAiApi`.
3. **Tài khoản Google**:
   - [Kết nối Google Docs](https://docs.google.com/) với OAuth2 trong n8n.
   - Cập nhật `folderId` trong node `Create Document` (tham khảo [hướng dẫn kết nối Google Docs](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.googledocs/)).
4. **VPS cho n8n (khuyến nghị)**:
   - Để workflow chạy 24/7 ổn định, các sếp nên **self-host n8n** trên VPS.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải workflow JSON** từ [link gốc](https://n8n.io/workflows/13921) hoặc copy toàn bộ JSON từ trang này.
- Trong **n8n Editor**, chọn **Import Workflow** và dán JSON vào.
- Hoặc tải file JSON đã download và import trực tiếp.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **15 node**, nhưng các bước quan trọng cần chú ý:

##### **A. Cấu Hình Credentials (Bắt Buộc)**
| **Node**               | **Credentials Cần Thiết**               | **Lưu Ý**                                                                 |
|------------------------|----------------------------------------|---------------------------------------------------------------------------|
| Booking.com Scraper    | `apifyApi`                             | Điền **API Token Apify** (từ tài khoản Apify).                           |
| Google Flights Scraper| `apifyApi`                             | Cùng token với Booking.com.                                               |
| HTTP Request Hotels    | `httpQueryAuth` (parameter `token`)   | Sử dụng **API Token Apify** như trên.                                     |
| HTTP Request Flights   | `httpQueryAuth` (parameter `token`)   | Cùng token với HTTP Request Hotels.                                       |
| OpenAI Recommendations | `openAiApi`                            | Điền **API Key OpenAI**.                                                  |
| Google Docs            | `googleDocsOAuth2Api`                  | Kết nối Google Docs và cập nhật `folderId` trong node `Create Document`. |

##### **B. Cấu Hình Node Quan Trọng**
1. **Node `Set Variables`**:
   - Đảm bảo biến `departureAirport`, `destinationAirport`, `dates`, và `travelers` được truyền từ form đến các node scrape và AI.
2. **Node `Apify` (Booking.com & Google Flights)**:
   - Các node này scrape **top 5 khách sạn** (Booking.com) và **top 3 vé máy bay** (Google Flights) dựa trên thông tin từ form.
   - **Lưu ý**: Apify có giới hạn scrape, các sếp nên kiểm tra [điều khoản sử dụng](https://apify.com/docs/api/usage-limits) để tránh bị block.
3. **Node `OpenAI Recommendations`**:
   - Sử dụng mô hình **GPT-4o-mini** để tạo gợi ý về:
     - Điểm tham quan (attractions).
     - Nhà hàng (restaurants).
     - Lịch trình chi tiết (itinerary).
   - **Prompt mẫu** (có thể chỉnh sửa trong node `Prepare Document Content`):
     ```
     Tóm tắt một kế hoạch du lịch 3 ngày cho {travelers} người từ {departureAirport} đến {destinationAirport} trong khoảng ngày {dates}.
     Gợi ý 3 điểm tham quan nổi bật, 2 nhà hàng phù hợp với ngân sách trung bình, và một lịch trình chi tiết mỗi ngày.
     ```
4. **Node `Google Docs`**:
   - **Cập nhật `folderId`**: Mở Google Drive, chọn folder muốn lưu file, copy `folderId` từ URL và điền vào node `Create Document`.
   - **Định dạng văn bản**: Node `Prepare Document Content` (type `code`) sẽ format dữ liệu thành văn bản dễ đọc. Các sếp có thể chỉnh sửa mã JavaScript trong node này để thay đổi định dạng.

##### **C. Test Run & Kích Hoạt**
1. **Test với dữ liệu mẫu**:
   - Nhập thông tin vào form (ví dụ: sân bay Hà Nội → Đà Nẵng, ngày 15-18/10/2024, 2 người).
   - Chạy workflow và kiểm tra Google Doc được tạo có đầy đủ thông tin không.
2. **Bật Active**:
   - Sau khi test thành công, bật **Active** cho workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Slack/Telegram Notification**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo cho khách hàng khi kế hoạch du lịch đã hoàn thành.
   - **Cách làm**:
     - Thêm node `Slack` hoặc `Telegram Bot` sau node `Create Document`.
     - Gửi tin nhắn chứa link Google Doc và thông tin khuyến mãi (nếu có).
   ```json
   {
     "jsonata": "$documentLink"
   }
   ```

2. **Lưu Log Hoạt Động**:
   - Thêm node **Sticky Note** hoặc **Google Sheets** để ghi lại lịch sử các yêu cầu du lịch.
   - **Cách làm**:
     - Sau node `Merge All Data`, thêm node `Sticky Note` để lưu thông tin vào log.
     - Hoặc sử dụng node `Google Sheets` để tự động ghi dữ liệu vào bảng Excel.

3. **Tự Động Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Cron Trigger** để gửi báo cáo tổng hợp cho khách hàng hàng tháng.
   - **Cách làm**:
     - Tạo một workflow mới với **Cron Trigger** (ví dụ: ngày 1 của mỗi tháng).
     - Sử dụng node `Google Sheets` để lấy dữ liệu du lịch trong tháng và tạo báo cáo.
     - Gửi báo cáo qua email hoặc Slack.

4. **Cải Thiện Gợi Ý AI**:
   - Chỉnh sửa **prompt** trong node `OpenAI Recommendations` để phù hợp với khách hàng mục tiêu.
   - Ví dụ:
     - Đối với khách du lịch trẻ: Gợi ý nhiều điểm vui chơi.
     - Đối với khách du lịch giàu: Gợi ý khách sạn 5 sao và nhà hàng cao cấp.

---

### 📌 **Kết Luận: Áp Dụng Ngay Để Tăng Hiệu Suất!**
Workflow này là **giải pháp hoàn hảo** cho các sếp trong ngành du lịch muốn:
✔ **Tự động hóa 100% quá trình lập kế hoạch du lịch**.
✔ **Cung cấp trải nghiệm cá nhân hóa** cho khách hàng với AI.
✔ **Giảm thời gian làm việc** từ giờ xuống phút.
✔ **Hoạt động 24/7** mà không cần nhân viên.

**Hành động ngay hôm nay:**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình credentials** theo hướng dẫn trên.
3. **Test với dữ liệu mẫu** và bật Active.
4. **Chia sẻ link form** với khách hàng và **nhận phản hồi ngay lập tức!**

---
**💡 Cần hỗ trợ thêm?**
- Trở thành thành viên [n8n Discord](https://discord.com/invite/XPKeKXeB7d) để hỏi đáp.
- Tham gia [Forum n8n](https://community.n8n.io/) để chia sẻ kinh nghiệm.

**Happy Automating!** 🚀