---
title: "🚀 Tự Động Thu Thập Bài Viết Twitter & Lưu Về Airtable Không Cần Code"
description: "Workflow n8n giúp các sếp tự động quét các bài viết mới trên Twitter theo từ khóa, lọc trùng lặp và lưu ngay vào Airtable để quản lý dữ liệu marketing hiệu quả."
slug: "tu-dong-thu-thap-twitter-luu-airtable"
tags: [n8n, automation, no-code, twitter, airtable, social-listening]
keywords: [n8n workflow, tự động hóa twitter, lưu dữ liệu airtable, social listening, marketing automation]
---

# 🚀 Tự Động Thu Thập Bài Viết Twitter & Lưu Về Airtable Không Cần Code

Trong kỷ nguyên của Social Listening, việc theo dõi các cuộc hội thoại, xu hướng và phản hồi của khách hàng trên Twitter (X) là cực kỳ quan trọng. Tuy nhiên, làm thủ công bằng cách copy-paste từng bài viết vào Excel hay Airtable không chỉ tốn thời gian mà còn dễ bỏ sót dữ liệu quan trọng.

Workflow này được thiết kế để giải quyết triệt để nỗi đau đó. Nó hoạt động như một "người gác cổng" thông minh: quét các bài viết mới trên Twitter theo từ khóa bạn định nghĩa, so sánh với dữ liệu đã có trong Airtable để loại bỏ các tweet trùng lặp, và chỉ lưu những bài viết hoàn toàn mới vào bảng dữ liệu của bạn. Toàn bộ quá trình diễn ra tự động, không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Loại bỏ hoàn toàn thao tác copy-paste thủ công, giúp team marketing tập trung vào phân tích thay vì nhập liệu.
- **Dữ liệu sạch & Không trùng lặp:** Node Merge đảm bảo chỉ những tweet mới thực sự mới được thêm vào Airtable, tránh việc bảng dữ liệu bị "bloat" (phình to) do dữ liệu lặp lại.
- **Quản lý tập trung:** Tất cả dữ liệu social media được gom về một mối trong Airtable, dễ dàng tạo dashboard, lọc theo ngày, tác giả, hoặc nội dung.
- **Độ chính xác cao:** Tự động hóa quy trình thu thập giúp giảm thiểu lỗi con người trong quá trình ghi nhận dữ liệu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Bản miễn phí hoặc Self-hosted.
2. **Tài khoản Twitter (X):** Cần có API Key và API Secret (có thể lấy từ Twitter Developer Portal). Lưu ý: Twitter hiện có chính sách API mới, hãy đảm bảo tài khoản của bạn có quyền truy cập Search API.
3. **Tài khoản Airtable:** Tạo một Base và một Table (ví dụ: "Twitter Posts") với các cột phù hợp (ví dụ: Tweet ID, Content, Author, Date, Link).
4. **Airtable API Key:** Lấy từ Settings -> Integrations -> API trong Airtable.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Vào trang [n8n.io/workflows/1403](https://n8n.io/workflows/1403).
2. Nhấn nút **"Copy JSON"** hoặc tải file JSON về.
3. Mở n8n Editor của bạn, nhấn nút **"Import from File"** (hoặc dán trực tiếp JSON vào editor nếu bạn đã copy).
4. Workflow sẽ hiện ra với 7 nodes chính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần click vào từng node và cấu hình như sau:

*   **Node: `Twitter`**
    *   **Credentials:** Chọn hoặc tạo credentials Twitter mới.
    *   **Operation:** Chọn `Search`.
    *   **Query:** Nhập từ khóa bạn muốn theo dõi (ví dụ: `#n8n`, `AI marketing`, `brand_name`).
    *   **Limit:** Đặt số lượng tweet tối đa muốn lấy mỗi lần chạy (ví dụ: 20-50).
    *   *Lưu ý:* Đảm bảo bạn đã cấu hình đúng API version nếu Twitter yêu cầu.

*   **Node: `Set_AT_list`**
    *   Node này thường dùng để chuẩn bị dữ liệu cho bước merge. Kiểm tra xem nó có đang map đúng các trường dữ liệu từ Twitter (như `id`, `text`, `created_at`) không. Nếu cấu trúc dữ liệu đầu vào thay đổi, các sếp có thể cần chỉnh lại mapping ở đây.

*   **Node: `get airtable list`**
    *   **Credentials:** Chọn credentials Airtable đã tạo ở bước chuẩn bị.
    *   **Base ID:** Chọn Base bạn muốn lưu dữ liệu.
    *   **Table:** Chọn Table cụ thể (ví dụ: "Twitter Posts").
    *   **Operation:** Mặc định là `List`. Đảm bảo nó lấy về toàn bộ dữ liệu hiện có trong bảng để so sánh.

*   **Node: `set twitter data`**
    *   Tương tự `Set_AT_list`, node này chuẩn bị dữ liệu từ Twitter để đưa vào bước Merge. Hãy chắc chắn rằng các trường dữ liệu (đặc biệt là **Tweet ID**) được map chính xác.

*   **Node: `Leave only new tweets` (Merge Node)**
    *   **Mode:** Chọn `Append` hoặc `Combine` tùy thuộc vào logic cụ thể, nhưng thường là so sánh để giữ lại các item không tồn tại trong danh sách Airtable.
    *   **Join By:** Chọn trường dùng để so sánh, thường là **Tweet ID**.
    *   **Logic:** Đảm bảo logic merge được thiết lập để chỉ giữ lại các tweet có ID **không có** trong danh sách Airtable (tức là tweet mới).

*   **Node: `Append new tweets to airtable`**
    *   **Credentials:** Chọn credentials Airtable.
    *   **Base ID & Table:** Chọn đúng Base và Table như node `get airtable list`.
    *   **Operation:** Chọn `Append`.
    *   **Mapping:** Map các trường dữ liệu từ Twitter (Content, Author, Date, Link) vào các cột tương ứng trong Airtable.

#### 3. Kích hoạt ⚡️
1. Nhấn nút **"Test Workflow"** để chạy thử với dữ liệu mẫu.
2. Kiểm tra xem các tweet mới có được thêm vào Airtable không và có bị trùng lặp không.
3. Nếu mọi thứ ổn, nhấn nút **"Active"** ở góc trên bên phải để bật workflow.
4. *Gợi ý:* Để tự động hóa hoàn toàn, các sếp nên thay node `On clicking 'execute'` (Manual Trigger) bằng node **Cron** (ví dụ: chạy mỗi 15 phút hoặc 1 giờ) để workflow tự động quét và cập nhật dữ liệu liên tục.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bộ lọc cảm xúc (Sentiment Analysis):** Sau khi lấy dữ liệu từ Twitter, các sếp có thể thêm một node OpenAI hoặc LLM khác để phân tích cảm xúc (tích cực/tiêu cực) của tweet và lưu thêm một cột "Sentiment" vào Airtable.
- **Gửi cảnh báo qua Slack/Telegram:** Nếu tweet chứa từ khóa quan trọng (ví dụ: "lỗi", "khó chịu"), hãy thêm một điều kiện (IF node) để gửi thông báo ngay lập tức qua Slack hoặc Telegram cho team CSKH.
- **Tạo Dashboard Airtable:** Sử dụng dữ liệu đã thu thập trong Airtable để tạo các biểu đồ (Chart) theo thời gian, theo tác giả, hoặc theo chủ đề, giúp báo cáo marketing trực quan hơn.
- **Lưu trữ dài hạn:** Nếu dữ liệu tăng quá nhanh, hãy cân nhắc thêm một node để xuất dữ liệu cũ ra Google Sheets hoặc database khác sau 30-60 ngày để giữ Airtable luôn nhẹ và nhanh.

### 📌 Kết luận
Việc tự động hóa quy trình thu thập dữ liệu từ Twitter vào Airtable không chỉ giúp các sếp tiết kiệm hàng giờ làm việc thủ công mỗi tuần mà còn đảm bảo tính toàn vẹn và chính xác của dữ liệu. Với workflow này, các sếp có thể tập trung vào việc phân tích và ra quyết định dựa trên dữ liệu thực tế, thay vì loay hoay với việc nhập liệu. Hãy import, cấu hình và bắt đầu xây dựng hệ thống Social Listening chuyên nghiệp của riêng bạn ngay hôm nay!