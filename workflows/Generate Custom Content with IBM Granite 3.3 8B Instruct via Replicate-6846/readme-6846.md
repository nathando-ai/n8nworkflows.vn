---
title: "🚀 Tự động tạo nội dung cá nhân hóa với IBM Granite 3.3 8B Instruct qua Replicate trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tích hợp mô hình ngôn ngữ lớn IBM Granite 3.3 8B Instruct thông qua Replicate API để tạo nội dung tự động, thông minh."
slug: "tao-noi-dung-ibm-granite-replicate-n8n"
tags: [n8n, automation, ai, replicate, ibm-granite, content-creation]
keywords: [n8n workflow, ibm granite 3.3, replicate api, tự động hóa nội dung, ai agents]
---

# 🚀 Tự động tạo nội dung cá nhân hóa với IBM Granite 3.3 8B Instruct qua Replicate

Các sếp có đang gặp khó khăn khi phải viết nội dung thủ công lặp đi lặp lại, tốn nhiều thời gian nhưng chất lượng đôi khi không đồng đều? Việc tích hợp các mô hình AI mã nguồn mở mạnh mẽ vào quy trình làm việc thường đòi hỏi lập trình phức tạp. 

Đừng lo! Bài viết này sẽ hướng dẫn các sếp cách thiết lập một workflow n8n tự động hóa 100%, kết nối trực tiếp với mô hình **IBM Granite 3.3 8B Instruct** thông qua **Replicate API** để tạo ra các nội dung chất lượng cao, lập luận sắc bén và tuân thủ chặt chẽ các chỉ dẫn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tạo nội dung tức thì**: Tận dụng mô hình 8 tỷ tham số với ngữ cảnh lên đến 128K token để xử lý các yêu cầu phức tạp.
- **Quy trình khép kín tự động**: Tự động gửi request, theo dõi trạng thái xử lý (polling status), và trả về kết quả mà không cần can thiệp thủ công.
- **Xử lý lỗi thông minh**: Tích hợp logic kiểm tra và vòng lặp chờ (`Wait`, `If`) giúp hệ thống bền bỉ, hạn chế tối đa tình trạng gián đoạn API.
- **Sẵn sàng mở rộng**: Dễ dàng tùy chỉnh tham số (`temperature`, `max_tokens`, `top_p`) và kết nối với Google Sheets, Slack hoặc Telegram để tự động hóa toàn diện.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Replicate**: Đăng ký tại [replicate.com](https://replicate.com) và lấy API Token cá nhân.
- **Workflow JSON**: Tải hoặc import template workflow có sẵn (tổng cộng 13 nodes cơ bản từ Trigger đến các khối xử lý logic API).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy đoạn JSON từ nguồn cung cấp.
- Trong giao diện n8n Editor, nhấn **Add workflow** -> Chọn **Import from File** hoặc dán trực tiếp vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 13 nodes, trong đó các sếp cần chú ý đặc biệt đến các node sau để hệ thống chạy mượt mà:
- **Set API Token**: Tại node này, thay thế chuỗi mẫu `'YOUR_REPLICATE_API_TOKEN'` bằng mã API Token thực tế của các sếp lấy từ tài khoản Replicate.
- **Set Text Parameters**: Nơi các sếp cấu hình nội dung prompt muốn AI xử lý (`prompt`), độ dài tối đa (`max_tokens`), độ sáng tạo (`temperature`),... Có thể điều chỉnh tùy theo mục đích sử dụng thực tế (viết bài PR, tóm tắt tài liệu, viết mã...).
- **Create Text Prediction & Check Status (HTTP Request nodes)**: Các node này thực hiện việc gọi API tới endpoint `https://api.replicate.com/v1/predictions` của model `ibm-granite/granite-3.3-8b-instruct`. Đảm bảo Header chứa đúng Authorization Token từ biến đã đặt ở bước trên.
- **Is Complete? / Has Failed? (If nodes)**: Kiểm tra trạng thái hoàn thành của tiến trình AI (vì các mô hình lớn đôi khi cần vài giây để suy luận). Kết hợp với các node `Wait 5s` và `Wait 10s` để tối ưu hóa thời gian chờ.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** thông qua **Manual Trigger** để chạy thử nghiệm với dữ liệu mẫu.
- Kiểm tra kết quả trả về ở node **Display Result** và xem log chi tiết tại node **Log Request**.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để đưa workflow vào trạng thái vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Google Sheets**: Thay vì dùng Manual Trigger, hãy kết nối node Google Sheets để đọc danh sách prompt từ file Excel/Google Sheets hàng loạt.
- **Nhận thông báo qua Telegram/Slack**: Thêm node Telegram hoặc Slack ở nhánh **Success Response** để tự động bắn kết quả vừa tạo về group chat của team.
- **Lưu lịch sử nội dung**: Tích hợp thêm node Airtable hoặc Notion để lưu trữ toàn bộ lịch sử các bài viết/nội dung mà IBM Granite đã tạo ra phục vụ việc kiểm tra sau này.

### 📌 Kết luận
Việc tích hợp IBM Granite 3.3 8B Instruct qua Replicate vào n8n mở ra cánh cửa tự động hóa nội dung cực kỳ mạnh mẽ và tiết kiệm chi phí cho các cá nhân và doanh nghiệp. Hãy áp dụng ngay workflow này để tối ưu hóa hiệu suất công việc của các sếp ngay hôm nay!