---
title: "🚀 Phân tích dữ liệu Google Sheets bằng ngôn ngữ tự nhiên với Google Gemini AI"
description: "Hướng dẫn cấu hình workflow n8n sử dụng Google Gemini AI và Google Sheets để trò chuyện, truy vấn và phân tích dữ liệu trực quan bằng tiếng Việt."
slug: "phan-tich-du-lieu-google-sheets-bang-gemini-ai"
tags: [n8n, automation, google-sheets, google-gemini, ai-agent]
keywords: [n8n workflow, phân tích dữ liệu google sheets, gemini ai n8n, tự động hóa no-code, ai agent google sheets]
---

# 🚀 Phân tích dữ liệu Google Sheets bằng ngôn ngữ tự nhiên với Google Gemini AI

Các sếp có bao giờ cảm thấy mệt mỏi khi phải mò mẫm tạo các câu lệnh Pivot Table phức tạp, viết hàm VLOOKUP dài dằng dặc hay lọc dữ liệu thủ công trên Google Sheets mỗi khi cần báo cáo nhanh không? Việc này vừa tốn thời gian, vừa dễ sai sót, đặc biệt khi sếp không rành về công thức Excel nâng cao.

Giải pháp là đây! Workflow n8n siêu cấp này do chuyên gia **Robert Breen** thiết kế sẽ biến Google Sheets của các sếp thành một cơ sở dữ liệu "biết nói". Nhờ sự trợ giúp của **Google Gemini AI Agent**, các sếp chỉ cần gõ câu hỏi bằng ngôn ngữ tự nhiên (ví dụ: *"Tổng chi phí quảng cáo theo kênh là bao nhiêu?"* hoặc *"Hiển thị số lượng conversion của chiến dịch X"*), hệ thống sẽ tự động truy vấn, xử lý và trả về kết quả chính xác 100% mà không cần chạm tay vào một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Trò chuyện trực tiếp với dữ liệu:** Hỏi đáp mượt mà với bảng tính qua chat bằng tiếng Việt hoặc tiếng Anh.
- **Tự động hóa hoàn toàn các phép toán phức tạp:** Tự động tính Tổng (Sum), Trung bình (Average), Đếm (Count), Lọc giá trị duy nhất (Distinct Count) theo 1 hoặc 2 chiều dữ liệu (Dimensions).
- **Tiết kiệm 90% thời gian làm báo cáo:** Không còn mất công kéo thả Pivot Table hay viết script Google Apps Script thủ công.
- **Hoạt động linh hoạt 24/7:** Dễ dàng nhúng vào các hệ thống chat nội bộ hoặc gọi qua Webhook bất cứ lúc nào cần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Google AI Studio** để lấy Gemini API Key.
- Tài khoản **Google Cloud Console** để cấu hình Google Sheets OAuth2 API.
- File Google Sheets chứa dữ liệu mẫu (có thể dùng sẵn [Sample Marketing Data](https://docs.google.com/spreadsheets/d/19aUQYZq02qHsCelO4eeV4sx_MTJJupC5qe0gDLQBtRA/edit?usp=drivesdk)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ n8n template (ID: 7450), sau đó dán trực tiếp vào giao diện n8n Editor của mình. Workflow này gồm 2 phần chính: **Main Workflow (Query Parser)** và **Sub-Workflow (Data Processor)**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

##### Cấu hình Main Workflow:
- **Google Gemini Chat Model:** 
  1. Truy cập [Google AI Studio](https://aistudio.google.com/) để lấy API Key.
  2. Tại node này trong n8n, tạo mới Credential loại **Google PaLM API** và dán API Key vào.
- **Get Column Info (Google Sheets Tool):**
  1. Tạo dự án trên [Google Cloud Console](https://console.cloud.google.com/), bật **Google Sheets API**.
  2. Tạo OAuth 2.0 Client ID và kết nối tài khoản Google Sheets thông qua Credential **Google Sheets OAuth2 API** tại node này.

##### Cấu hình Sub-Workflow (Data Processor):
- Áp dụng chung credential Google Sheets OAuth2 API và Gemini API cho các node **Get Data** và **Google Gemini Chat Model1**.
- Cập nhật **Sheet ID** của các sếp vào node **Get Data** (trỏ tới sheet dữ liệu chính, ví dụ tab "Data").
- Tại workflow chính, tìm node **Execute Workflow - Summarize Data** và trỏ đường dẫn thực thi đến sub-workflow vừa thiết lập.

#### 3. Kích hoạt ⚡️
- Chạy thử (Test run) với một vài câu hỏi mẫu để kiểm tra khả năng phản hồi của AI Agent.
- Sau khi kiểm tra dữ liệu trả về chính xác, gạt công tắc sang **Active** để vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh chat:** Kết nối Webhook của workflow này với Telegram Bot hoặc Slack để các sếp có thể chat trực tiếp với dữ liệu ngay trên điện thoại.
- **Mở rộng nguồn dữ liệu:** Không chỉ Google Sheets, các sếp có thể bổ sung các tool như Airtable hoặc PostgreSQL vào Agent để phân tích dữ liệu đa nền tảng.
- **Lưu lịch sử truy vấn:** Thêm một node Google Sheets phụ ở cuối workflow để ghi lại lịch sử các câu hỏi và kết quả mà người dùng đã tra cứu.

### 📌 Kết luận
Việc tích hợp AI vào quản trị dữ liệu chưa bao giờ dễ dàng đến thế. Với workflow này, các sếp đã sở hữu ngay một "Data Analyst ảo" sẵn sàng phân tích số liệu bất cứ lúc nào chỉ bằng vài câu lệnh. Lên đồ ngay thôi các sếp ơi!