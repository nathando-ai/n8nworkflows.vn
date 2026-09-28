---
title: "🚀 Tự Động Hóa Tìm Kiếm & Phân Tích Hội Nghị Với AI (Eventbrite + ScrapeGraphAI)"
description: "Workflow n8n tự động quét các sự kiện hội nghị trên Eventbrite, phân tích diễn giả và lịch trình bằng AI để tạo ra chiến lược networking tối ưu, giúp các sếp không bỏ lỡ cơ hội kinh doanh."
slug: "tu-dong-hoa-tim-kiem-phan-tich-hoi-nghi-ai"
tags: [n8n, automation, no-code, ai, lead-generation, eventbrite]
keywords: [n8n workflow, tự động hóa hội nghị, scrapegraphai, phân tích diễn giả, tìm kiếm khách hàng tiềm năng]
---

# 🚀 Tự Động Hóa Tìm Kiếm & Phân Tích Hội Nghị Với AI (Eventbrite + ScrapeGraphAI)

Trong thế giới kinh doanh hiện đại, các hội nghị và sự kiện (conferences) không chỉ là nơi học hỏi mà còn là "mỏ vàng" cho việc mở rộng mạng lưới quan hệ (networking) và tìm kiếm khách hàng tiềm năng. Tuy nhiên, việc theo dõi hàng trăm sự kiện mới được đăng ký mỗi tuần, đọc kỹ lịch trình, và nghiên cứu từng diễn giả để chuẩn bị câu hỏi hay chiến lược tiếp cận là một công việc cực kỳ tốn thời gian và dễ gây nhầm lẫn nếu làm thủ công.

Workflow **Conference Networking Intelligence** được thiết kế để giải quyết triệt để nỗi đau này. Bằng cách kết hợp sức mạnh của **ScrapeGraphAI** (AI chuyên trích xuất dữ liệu từ web) và logic xử lý thông minh, quy trình này sẽ tự động quét các sự kiện mới, phân tích sâu về diễn giả và lịch trình, sau đó tạo ra một bản đồ chiến lược networking chi tiết. Các sếp chỉ cần chờ nhận báo cáo, không cần tốn công sức "săn" sự kiện hay đọc từng trang web.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt là khi cần scrape dữ liệu từ nhiều nguồn web, các sếp nên cài n8n trên VPS riêng (Self-hosted) để đảm bảo hiệu năng và quyền kiểm soát.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần**: Tự động hóa hoàn toàn quá trình tìm kiếm và tổng hợp thông tin sự kiện.
- **Chiến lược Networking chính xác**: AI phân tích và xếp hạng ưu tiên các diễn giả dựa trên giá trị kinh doanh (C-level, Thought Leaders...).
- **Tối ưu hóa thời gian tham dự**: Xác định các phiên (session) bắt buộc phải tham gia và các khoảng thời gian vàng để giao lưu.
- **Dữ liệu có cấu trúc**: Thay vì các trang web lộn xộn, các sếp nhận được dữ liệu sạch, dễ đọc và sẵn sàng để đưa vào CRM hoặc gửi email.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n**: Chạy local hoặc trên VPS.
2. **API Key ScrapeGraphAI**: Đăng ký tại [scrapegraphai.com](https://scrapegraphai.com/) để lấy API key. Workflow sử dụng node `n8n-nodes-scrapegraphai` nên cần cấu hình credentials.
3. **URL nguồn dữ liệu**: Các sếp cần xác định URL cụ thể của các trang liệt kê sự kiện (ví dụ: trang sự kiện của Eventbrite, Meetup, hoặc trang hội nghị ngành dọc cụ thể) để điền vào node Scraper.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow từ link gốc: [n8n.io/workflows/6568](https://n8n.io/workflows/6568).
2. Mở n8n Editor, chọn **Import from File** hoặc dán trực tiếp JSON vào editor.
3. Lưu workflow với tên dễ nhớ, ví dụ: `AI Conference Intelligence`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 5 nodes chính, các sếp cần cấu hình kỹ từng bước:

**1. Schedule Trigger (⏰)**
- Mặc định chạy hàng tuần (thứ Hai 9:00 AM).
- Các sếp có thể chỉnh lại tần suất (Daily, Bi-weekly) tùy theo tốc độ ra mắt sự kiện trong ngành của mình.

**2. Conference Scraper (🔍)**
- **Node**: `n8n-nodes-scrapegraphai.scrapegraphAi`
- **Cấu hình**:
    - Chọn **Credentials**: Chọn API key ScrapeGraphAI đã tạo.
    - **URL**: Điền URL của trang liệt kê sự kiện (ví dụ: `https://www.eventbrite.com/d/.../conferences/`).
    - **Prompt/Schema**: Đảm bảo prompt yêu cầu trích xuất: Tên hội nghị, Ngày, Địa điểm, Giá vé, Người tổ chức.
    - *Lưu ý*: ScrapeGraphAI hoạt động tốt nhất với các trang có cấu trúc rõ ràng. Nếu trang web quá phức tạp, các sếp có thể cần tinh chỉnh prompt để AI hiểu đúng dữ liệu cần lấy.

**3. Speaker Analyzer (🎤)**
- **Node**: `n8n-nodes-scrapegraphai.scrapegraphAi`
- **Chức năng**: Lấy danh sách diễn giả từ trang chi tiết của hội nghị.
- **Cấu hình**:
    - URL cần là link chi tiết của sự kiện (có thể lấy từ bước trước nếu workflow được thiết kế để loop qua từng sự kiện, hoặc các sếp cần hardcode URL mẫu nếu chỉ test 1 sự kiện).
    - **Prompt**: Yêu cầu AI phân tích: Họ tên, Chức vụ, Công ty, LinkedIn, và đánh giá mức độ ưu tiên (High/Medium/Low) dựa trên vị trí (C-level = High).

**4. Agenda Parser (📅)**
- **Node**: `n8n-nodes-scrapegraphai.scrapegraphAi`
- **Chức năng**: Trích xuất lịch trình chi tiết.
- **Cấu hình**:
    - **Prompt**: Yêu cầu liệt kê: Tên phiên, Thời gian, Diễn giả, Phòng họp, và loại hình (Talk, Workshop, Panel).
    - Mục tiêu là xác định các "Networking Breaks" (nghỉ giải lao, ăn trưa) để các sếp biết khi nào nên đi giao lưu.

**5. Networking Opportunity Finder (🤝)**
- **Node**: `n8n-nodes-base.code`
- **Chức năng**: Đây là "bộ não" xử lý dữ liệu. Node này sẽ tổng hợp dữ liệu từ 3 bước trên (Sự kiện, Diễn giả, Lịch trình) và tạo ra chiến lược.
- **Cấu hình**:
    - Kiểm tra code trong node này. Nó thường sẽ thực hiện các logic như:
        - Lọc các diễn giả có mức ưu tiên "High".
        - Gán các diễn giả đó vào các phiên họ tham gia.
        - Tạo ra một bảng tổng hợp: "Ai cần gặp", "Gặp ở phiên nào", "Câu hỏi gợi ý".
    - Các sếp có thể tùy chỉnh logic ở đây để thêm các tiêu chí riêng (ví dụ: chỉ tập trung vào các công ty đối thủ, hoặc chỉ các diễn giả từ khu vực địa lý cụ thể).

#### 3. Kích hoạt ⚡️
1. **Test Run**: Chạy thử workflow với dữ liệu mẫu. Kiểm tra xem dữ liệu từ ScrapeGraphAI có được trích xuất đúng không (đặc biệt là phần JSON output).
2. **Kiểm tra Code Node**: Đảm bảo không có lỗi JavaScript khi xử lý dữ liệu rỗng hoặc định dạng khác nhau.
3. **Bật Active**: Sau khi test thành công, bật nút **Active** để workflow tự động chạy theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối với CRM/Email**: Thêm node **Send Email** hoặc **HubSpot/Salesforce** ở cuối workflow để tự động gửi báo cáo chiến lược networking vào email hoặc tạo deal mới trong CRM.
- **Cảnh báo qua Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** để nhận thông báo ngay khi phát hiện một sự kiện lớn hoặc một diễn giả nổi tiếng sắp tham gia.
- **Lưu trữ lịch sử**: Thêm node **Google Sheets** hoặc **Airtable** để lưu lại lịch sử các sự kiện đã phân tích, giúp các sếp theo dõi xu hướng và so sánh giữa các năm.
- **Tinh chỉnh Prompt AI**: ScrapeGraphAI rất mạnh nhưng cần prompt rõ ràng. Các sếp nên thử nghiệm với các prompt khác nhau để AI trích xuất đúng các trường thông tin quan trọng nhất cho ngành của mình.

### 📌 Kết luận
Workflow **Conference Networking Intelligence** là công cụ "vũ khí" đắc lực giúp các sếp chuyển từ việc "săn" sự kiện thủ công sang việc "quản lý" cơ hội kinh doanh một cách chủ động và thông minh. Với sự kết hợp giữa khả năng scrape web mạnh mẽ của ScrapeGraphAI và logic phân tích AI, các sếp sẽ không bao giờ bỏ lỡ một mối quan hệ tiềm năng nào. Hãy import và tùy chỉnh ngay hôm nay để bắt đầu tối ưu hóa chiến lược networking của mình!