---
title: "🚀 Tự động hóa tìm kiếm & làm giàu dữ liệu cá nhân (Skip-Trace) từ Form vào Notion với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa hoàn toàn quy trình nhận thông tin từ form, gọi API ScraperCity để tra cứu thông tin (Skip-Trace), xử lý dữ liệu trùng lặp và lưu trữ trực tiếp vào Notion database."
slug: "tu-dong-hoa-skip-trace-scrapercity-notion-n8n"
tags: [n8n, automation, scrapercity, notion, lead-generation, no-code]
keywords: [n8n workflow, scrapercity api, notion database, skip-trace automation, lead generation no code, tim kiem thong tin ca nhan]
---

# 🚀 Tự động hóa tìm kiếm & làm giàu dữ liệu cá nhân (Skip-Trace) vào Notion

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thủ công tra cứu thông tin cá nhân (skip-trace), tìm kiếm email, số điện thoại từ các yêu cầu trên form, sau đó lại cặm cụi copy-paste từng dòng dữ liệu vào Notion không? Công việc lặp đi lặp lại này vừa ngốn thời gian, vừa dễ sai sót, lại làm giảm năng suất đội ngũ sales và marketing.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ mạnh mẽ do chuyên gia **Alex Berman** sáng tạo. Workflow này sẽ tự động hóa từ A-Z: nhận form yêu cầu, gửi dữ liệu sang hệ thống **ScraperCity API** để tra cứu, định kỳ kiểm tra trạng thái, tải kết quả về, lọc trùng lặp và đẩy thẳng thành các trang (pages) sạch sẽ vào **Notion** database!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo bị ngắt kết nối hay quá tải, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Biến một quy trình thủ công kéo dài hàng giờ thành một dòng chảy dữ liệu tự động chỉ sau một cú click submit form.
- **Dữ liệu sạch & chuẩn hóa:** Tự động parse, format lại dữ liệu trả về từ API và loại bỏ các bản ghi trùng lặp (`Remove Duplicate People`).
- **Lưu trữ chuyên nghiệp:** Quản lý toàn bộ thông tin lead/người dùng tập trung, trực quan ngay trên Notion database.
- **Hoạt động không nghỉ:** Cơ chế polling thông minh tự động kiểm tra tiến độ xử lý của job mà không làm nghẽn hệ thống.
:::

### 📥 Các loại Nodes có trong Workflow
Workflow này bao gồm **12 nodes** phối hợp nhịp nhàng với nhau:
1. **People Finder Form** (`formTrigger`): Tiếp nhận thông tin đầu vào (tên, email, số điện thoại...).
2. **Configure Search Defaults** (`set`): Cấu hình các tham số mặc định cho việc tìm kiếm.
3. **Submit People Finder Job** (`httpRequest`): Gửi yêu cầu tìm kiếm đến ScraperCity API.
4. **Store Run ID** (`run ID` / `set`): Lưu lại mã định danh của tiến trình (Run ID).
5. **Loop Controller** (`splitInBatches`): Điều phối vòng lặp kiểm tra trạng thái.
6. **Wait 60 Seconds Before Poll** (`wait`): Tạm dừng 60 giây giữa các lần gọi kiểm tra trạng thái.
7. **Check Scrape Job Status** (`httpRequest`): Kiểm tra xem quá trình cào dữ liệu đã hoàn tất chưa.
8. **Is Scrape Complete?** (`if`): Rẽ nhánh kiểm tra điều kiện hoàn thành.
9. **Download Enriched Results** (`httpRequest`): Tải kết quả dữ liệu đã được làm giàu về sau khi hoàn tất.
10. **Parse and Format Records** (`code`): Xử lý, bóc tách và định dạng lại các trường dữ liệu bằng đoạn mã tùy chỉnh.
11. **Remove Duplicate People** (`removeDuplicates`): Lọc bỏ các bản ghi trùng lặp.
12. **Save Person Record to Notion** (`notion`): Tạo trang mới lưu thông tin vào Notion Database.

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance **n8n** đang hoạt động.
- Tài khoản **ScraperCity** và **API Key** hợp lệ cho endpoint people-finder.
- Tài khoản **Notion** đã tạo sẵn một Database để chứa thông tin lead, cùng với một **Notion Integration (API Token)** được cấp quyền truy cập vào database đó.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow từ nguồn gốc hoặc tải file JSON về máy.
- Mở n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng menu (3 chấm) ở góc trên bên phải -> Chọn **Import from File** hoặc dán trực tiếp JSON vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các thành phần sau:
- **Cấu hình ScraperCity Credentials (`httpHeaderAuth`):** Áp dụng cho các node `Submit People Finder Job`, `Check Scrape Job Status`, và `Download Enriched Results`. Hãy điền API Key chính xác của ScraperCity vào phần Header Authentication.
- **Cấu hình Notion Credentials (`notionApi`):** Áp dụng cho node `Save Person Record to Notion`. Kết nối tài khoản Notion và chọn đúng Database đích.
- **Mapping dữ liệu trong Notion Node:** Kiểm tra và ánh xạ (map) các trường dữ liệu từ kết quả sau khi qua bước code (`Parse and Format Records`) tương ứng với các cột trong Notion database (Họ tên, Email, Số điện thoại...).
- **Tinh chỉnh thông số tìm kiếm:** Xem xét node `Configure Search Defaults` để điều chỉnh `max_results` hoặc các giá trị mặc định khác cho phù hợp với nhu cầu thực tế của chiến dịch.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền form thông qua URL của node `People Finder Form`.
- Theo dõi các node chạy qua để đảm bảo không gặp lỗi xác thực hay lỗi cú pháp.
- Khi mọi thứ đã chạy trơn tru, hãy chuyển trạng thái workflow sang **Active**.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Thêm node Telegram hoặc Slack ngay sau node `Save Person Record to Notion` để bắn thông báo về máy mỗi khi có lead mới hoàn thành quá trình skip-trace.
- **Thêm bộ lọc chất lượng:** Đặt một node `IF` hoặc `Filter` ngay sau bước khử trùng lặp để lọc ra những bản ghi đạt tiêu chuẩn dữ liệu tối thiểu (ví dụ: bắt buộc phải có số điện thoại hoặc email) trước khi lưu vào Notion.
- **Tùy chỉnh thời gian chờ:** Tăng hoặc giảm thời gian ở node `Wait 60 Seconds Before Poll` tùy thuộc vào thời gian xử lý trung bình của ScraperCity API đối với từng lượng data lớn nhỏ.

### 📌 Kết luận
Tự động hóa quy trình skip-trace và quản lý lead chưa bao giờ dễ dàng đến thế với sự kết hợp giữa n8n, ScraperCity và Notion. Hãy triển khai ngay hôm nay để tiết kiệm hàng chục giờ làm việc thủ công và tối ưu hóa hiệu suất kinh doanh cho đội ngũ của bạn!