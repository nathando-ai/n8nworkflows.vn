---
title: "📊 Tự Động Hóa Báo Cáo Lịch Kinh Tế PDF Gửi Telegram Mỗi Tuần"
description: "Workflow n8n tự động lấy dữ liệu lịch kinh tế, lọc tin tức quan trọng, tạo báo cáo PDF chuyên nghiệp và gửi qua Telegram mỗi 7 ngày mà không cần code."
slug: "tu-dong-hoa-bao-cao-lich-kinh-te-pdf-telegram"
tags: [n8n, automation, no-code, finance, telegram, pdf-generation]
keywords: [n8n workflow, lịch kinh tế, tự động hóa báo cáo, telegram bot, rapidapi]
---

# 📊 Tự Động Hóa Báo Cáo Lịch Kinh Tế PDF Gửi Telegram Mỗi Tuần

Trong thế giới tài chính và đầu tư, việc theo dõi lịch kinh tế (Economic Calendar) là bắt buộc. Tuy nhiên, việc thủ công kiểm tra từng sự kiện, tổng hợp tin tức, định dạng lại thành báo cáo đẹp mắt và gửi cho team hoặc khách hàng là một quy trình tốn kém thời gian và dễ xảy ra sai sót.

Workflow này giải quyết hoàn toàn bài toán đó. Nó tự động chạy mỗi 7 ngày, truy vấn API để lấy dữ liệu lịch kinh tế sắp tới, lọc ra những sự kiện có tác động trung bình và cao (Medium & High Impact), sau đó sử dụng dịch vụ tạo PDF để biến dữ liệu thô thành một báo cáo chuyên nghiệp và gửi thẳng vào kênh Telegram của bạn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian thủ công:** Không cần mở lịch kinh tế, copy-paste hay chỉnh sửa file Word/PDF mỗi tuần.
- **Độ chính xác cao:** Dữ liệu được lấy trực tiếp từ API và lọc tự động theo mức độ quan trọng, tránh bỏ sót tin tức quan trọng.
- **Trình bày chuyên nghiệp:** Báo cáo PDF được tạo từ template có sẵn, sẵn sàng để chia sẻ với đối tác hoặc khách hàng.
- **Giao tiếp tức thì:** Nhận báo cáo ngay trên Telegram, tiện lợi cho việc theo dõi trên di động.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản RapidAPI:** Đăng ký tại [RapidAPI](https://rapidapi.com/) và tìm kiếm các API liên quan đến "Economic Calendar" hoặc "Financial News" (workflow gốc thường dùng các API như *Economic Calendar* hoặc *NewsAPI* tùy phiên bản).
2. **Tài khoản dịch vụ tạo PDF:** Workflow sử dụng một HTTP Request để "Edit & Update Template" và "Download PDF". Các sếp cần có API key cho một dịch vụ như *Documint*, *PDF.co*, hoặc một service tương tự cho phép tạo PDF từ dữ liệu JSON/HTML.
3. **Telegram Bot Token:** Tạo bot qua @BotFather và lấy Token.
4. **Telegram Chat ID:** ID của kênh hoặc nhóm nơi bạn muốn nhận báo cáo.
5. **n8n Instance:** Đã cài đặt và chạy (Cloud hoặc Self-hosted).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from File** hoặc **Import from URL**.
3. Dán link workflow gốc: [https://n8n.io/workflows/9025](https://n8n.io/workflows/9025) hoặc tải file JSON về và import.
4. Workflow sẽ hiển thị 10 nodes chính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Dưới đây là các node quan trọng cần cấu hình lại theo thông tin của bạn:

*   **Node: `Set API Key for RapidAPI & Dates`**
    *   Đây là node `Set` dùng để định nghĩa biến.
    *   **Tham số cần sửa:**
        *   `rapidApiKey`: Điền API Key của bạn từ RapidAPI.
        *   `startDate` / `endDate`: Mặc định workflow có thể tính toán động, nhưng nếu cần cố định khoảng thời gian (ví dụ: 7 ngày tới), các sếp có thể chỉnh logic ở đây hoặc để node `Dynamically Sets the Date` xử lý.

*   **Node: `Gets Upcoming News`**
    *   Node `HTTP Request` gọi API lịch kinh tế.
    *   **Tham số cần sửa:**
        *   **URL:** Đảm bảo URL đúng với API bạn đã đăng ký trên RapidAPI.
        *   **Headers:** Kiểm tra trường `X-RapidAPI-Key` có được map đúng từ node `Set` ở trên không.
        *   **Body/Query Params:** Chỉnh các tham số như `country`, `currency`, hoặc `importance` nếu API hỗ trợ để lọc dữ liệu ngay từ đầu.

*   **Node: `Filter Medium & High Impact News`**
    *   Node `Code` dùng JavaScript để lọc dữ liệu.
    *   **Lưu ý:** Kiểm tra logic trong code. Thông thường, nó sẽ lọc các item có `impact` là "Medium" hoặc "High". Nếu API của bạn dùng tên khác (ví dụ: "Moderate" thay vì "Medium"), các sếp cần sửa điều kiện trong code block này.

*   **Node: `Edit & Update Template`**
    *   Node `HTTP Request` gọi dịch vụ tạo PDF.
    *   **Tham số cần sửa:**
        *   **URL:** Endpoint của dịch vụ PDF (ví dụ: `https://api.pdf.co/...` hoặc service tương tự).
        *   **Headers:** `Authorization` hoặc `X-Api-Key` của dịch vụ PDF.
        *   **Body:** Đây là phần quan trọng nhất. Nó chứa JSON data được map từ node `Organize Data for API Template`. Các sếp cần đảm bảo cấu trúc JSON khớp với template PDF mà bạn đã tạo trên dịch vụ đó.

*   **Node: `Download PDF Report`**
    *   Node `HTTP Request` tải file PDF về.
    *   **Lưu ý:** Đảm bảo response type là `File` hoặc `Binary` để node Telegram có thể đọc được.

*   **Node: `Send Economic Calendar Events PDF to Telegram`**
    *   Node `Telegram`.
    *   **Credentials:** Chọn hoặc tạo mới credentials Telegram Bot.
    *   **Chat ID:** Điền Chat ID của kênh/nhóm đích.
    *   **Document:** Map output từ node `Download PDF Report` vào trường `Document`.
    *   **Caption:** Có thể thêm caption mô tả ngắn gọn (ví dụ: "Báo cáo lịch kinh tế tuần này").

#### 3. Kích hoạt ⚡️
1. **Test Run:** Nhấn nút **Execute Workflow** để chạy thử.
    *   Kiểm tra xem node `Gets Upcoming News` có trả về dữ liệu không.
    *   Kiểm tra node `Filter` có giữ lại đúng các tin quan trọng không.
    *   Kiểm tra node `Download PDF` có tạo ra file PDF hợp lệ không.
    *   Kiểm tra Telegram có nhận được file không.
2. **Bật Active:** Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải. Workflow sẽ tự động chạy theo lịch `Schedule Every 7 Days`.

### ✍️ Mẹo & gợi ý nâng cao

*   **Tùy chỉnh Template PDF:** Thay vì dùng template mặc định, các sếp có thể thiết kế template PDF riêng trên dịch vụ PDF (như PDF.co, Documint) với logo công ty, màu sắc thương hiệu để báo cáo trông chuyên nghiệp hơn.
*   **Gửi thêm Email:** Thêm một node `Gmail` hoặc `SMTP` sau node Telegram để gửi bản sao báo cáo vào email cho các thành viên quan trọng trong team.
*   **Lọc theo Quốc gia/Currency:** Nếu các sếp chỉ quan tâm đến lịch kinh tế của Mỹ, Việt Nam hoặc một cặp tiền tệ cụ thể (như USD/VND), hãy chỉnh tham số trong node `Gets Upcoming News` để lọc ngay từ nguồn, giúp báo cáo ngắn gọn và tập trung hơn.
*   **Thêm AI Summary:** Kết hợp thêm một node `OpenAI` hoặc `Anthropic` để tóm tắt ngắn gọn ý nghĩa của từng sự kiện kinh tế trước khi đưa vào PDF. Điều này sẽ biến báo cáo từ dạng "liệt kê" thành "phân tích".

### 📌 Kết luận

Với workflow này, các sếp có thể biến quy trình theo dõi lịch kinh tế từ một công việc thủ công, lặp lại mỗi tuần thành một quy trình tự động hoàn toàn. Chỉ với vài phút cấu hình ban đầu, bạn sẽ nhận được báo cáo PDF chuyên nghiệp, chính xác và kịp thời ngay trên Telegram. Hãy import và tùy chỉnh ngay để tối ưu hóa quy trình làm việc tài chính của mình!