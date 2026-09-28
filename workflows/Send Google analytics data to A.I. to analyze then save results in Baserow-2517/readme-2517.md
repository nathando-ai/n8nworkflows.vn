---
title: "🚀 Tự động hóa phân tích Google Analytics bằng AI và lưu kết quả vào Baserow"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy dữ liệu Google Analytics so sánh tuần, gửi cho AI phân tích xu hướng SEO và lưu kết quả gọn gàng vào Baserow."
slug: "tu-dong-hoa-phan-tich-google-analytics-bang-ai-baserow"
tags: [n8n, automation, google-analytics, ai, baserow, marketing]
keywords: [n8n workflow, google analytics ai, baserow automation, phân tích seo bằng ai, tự động hóa marketing n8n]
---

# 🚀 Tự động hóa phân tích Google Analytics bằng AI và lưu kết quả vào Baserow

Các sếp làm Martech hay SEO chắc chắn đều hiểu cảm giác "ngợp thở" khi phải liên tục kéo báo cáo Google Analytics, so sánh số liệu tuần này với tuần trước, sau đó ngồi phân tích xem traffic tăng giảm do đâu, từ khóa nào lên ngôi. Công việc thủ công này ngốn rất nhiều thời gian mà lại dễ bỏ sót các biến động quan trọng.

Đừng lo, workflow n8n được thiết kế bởi chuyên gia **Keith Rumjahn** này sẽ giúp các sếp giải phóng 100 sức lao động. Hệ thống sẽ tự động trích xuất dữ liệu Google Analytics (engagement, search console, country views), đối chiếu tuần này với tuần trước, chuyển giao cho AI phân tích chuyên sâu và tự động lưu báo cáo vào cơ sở dữ liệu Baserow.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần thủ công xuất file Excel hay copy/paste số liệu hàng tuần.
- **Phân tích chuyên sâu từ AI**: AI sẽ đóng vai trò chuyên gia SEO, tự động chỉ ra các điểm bất thường, xu hướng tăng trưởng về lượt xem trang, từ khóa và quốc gia truy cập.
- **Lưu trữ khoa học**: Mọi kết quả phân tích được tự động đồng bộ vào bảng Baserow giúp dễ dàng theo dõi theo thời gian.
- **Hoạt động liên tục 24/7**: Lên lịch chạy định kỳ (Schedule Trigger) để các sếp luôn có báo cáo mới mỗi đầu tuần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n**: Đã cài đặt hoặc đang sử dụng n8n Cloud.
- **Google Analytics account**: Tài khoản đã có quyền truy cập Property ID cần phân tích.
- **AI API (OpenRouter hoặc tương đương)**: Tài khoản và API Key để gọi model AI phân tích dữ liệu.
- **Baserow account**: Tài khoản và API/Credentials để kết nối và lưu dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ n8n hoặc import trực tiếp file JSON vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Schedule Trigger / When clicking ‘Test workflow’**: Quyết định thời gian chạy tự động định kỳ (ví dụ: mỗi tuần chạy 1 lần vào thứ Hai).
- **Các node Google Analytics (`Get Page Engagement Stats`, `Get Google Search Results`, `Get Country views data`)**: 
  - Tạo và kết nối [Google Analytics Credentials](https://docs.n8n.io/integrations/builtin/credentials/google/oauth-single-service/).
  - Điền chính xác **Property ID** của website cần lấy dữ liệu vào các node này (bao gồm cả dữ liệu tuần này và tuần trước để so sánh).
- **Các node Code (`Parse data from Google Analytics`, `Parse GA data`, v.v.)**: Các node này dùng JavaScript thuần để làm sạch, cấu trúc lại dữ liệu thô từ GA trước khi gửi đi, không cần sửa đổi gì thêm trừ khi các sếp muốn custom lại format.
- **Các node AI Request (`Send page data to A.I.`, `Send page Search data to A.I.`, `Send country view data to A.I.`)**: 
  - Cấu hình kết nối HTTP Request trỏ tới OpenRouter (hoặc OpenAI/Anthropic tùy chọn).
  - Sử dụng Header Auth với:
    - *Username*: `Authorization`
    - *Password*: `Bearer {insert your API key}` *(Nhớ chừa 1 khoảng trắng sau chữ Bearer).*
  - Tùy chỉnh Prompt trong body của HTTP Request nếu muốn AI tập trung vào các chỉ số cụ thể của doanh nghiệp.
- **Node `Save A.I. output to Baserow`**:
  - Tạo sẵn một bảng (Table) trong Baserow với các cột chuẩn bị sẵn:
    - `Name`
    - `Country Views`
    - `Page Views`
    - `Search Report`
    - `Blog` (Nhập tên website của các sếp vào trường này).
  - Kết nối Baserow Credentials và map các trường dữ liệu từ AI trả về vào đúng cột tương ứng.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** để chạy thử nghiệm xem dữ liệu có chảy mượt từ GA qua AI rồi ghi vào Baserow hay không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Thêm node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay lập tức vào nhóm chat khi AI phân tích xong báo cáo tuần.
- **Lưu lịch sử**: Thay vì ghi đè, hãy cấu hình Baserow thêm cột `Date` để lưu trữ chuỗi thời gian, giúp vẽ biểu đồ tăng trưởng theo tháng/quý cực kỳ trực quan.
- **Đa dạng hóa AI Model**: Thử nghiệm các model AI khác nhau trên OpenRouter (như Claude 3.5 Sonnet hoặc GPT-4o) để có góc nhìn phân tích SEO sắc bén nhất.

### 📌 Kết luận
Tự động hóa quy trình phân tích dữ liệu marketing chưa bao giờ dễ dàng đến thế. Với sự kết hợp giữa Google Analytics, AI và Baserow, các sếp vừa tiết kiệm được hàng giờ đồng hồ mỗi tuần, vừa có được những insights giá trị để tối ưu hóa chiến lược nội dung. Áp dụng ngay thôi nào các sếp ơi!