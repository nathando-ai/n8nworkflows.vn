---
title: "🚀 Tự Động Tạo Báo Cáo ROI Chiến Dịch Marketing với Google Sheets, GPT-4o và Email"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động trích xuất dữ liệu marketing từ Google Sheets, phân tích hiệu suất bằng OpenAI GPT-4o và gửi báo cáo chi tiết qua email."
slug: "tu-dong-tao-bao-cao-roi-marketing-google-sheets-gpt4o-email"
tags: [n8n, automation, ai-agent, google-sheets, openai, marketing-roi]
keywords: [n8n workflow, tự động hóa marketing, báo cáo ROI marketing, GPT-4o AI agent, Google Sheets n8n]
---

# 🚀 Tự Động Tạo Báo Cáo ROI Chiến Dịch Marketing với GPT-4o và n8n

Các sếp làm marketing chắc hẳn đều quen thuộc với cảnh "đau đầu" mỗi cuối tuần hoặc cuối tháng: Phải hì hục tải dữ liệu từ Google Ads, Facebook Ads, tính toán chi phí, đo lường chuyển đổi, rồi lọ mọ viết báo cáo ROI (Return on Investment) gửi sếp lớn. Việc này không chỉ tốn hàng giờ đồng hồ mà đôi khi còn dễ nhầm lẫn số liệu.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n tự động hóa 100% do chuyên gia **Robert Breen** thiết kế. Workflow này sẽ thay các sếp "gánh" trọn vẹn quy trình: tự động đọc dữ liệu từ Google Sheets, tổng hợp số liệu theo chiến dịch và kênh, nhờ AI thông minh **GPT-4o** phân tích sâu sắc, và trả về một bản báo cáo chuyên nghiệp, mạch lạc.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn phải thủ công copy/paste số liệu hay tự tính toán ROI nữa.
- **Phân tích chuyên sâu từ AI:** Tận dụng sức mạnh của GPT-4o để đánh giá hiệu suất, phát hiện điểm sáng và điểm nghẽn của từng chiến dịch marketing.
- **Báo cáo chuẩn chỉnh, nhất quán:** Dữ liệu được cấu trúc rõ ràng, mạch lạc, sẵn sàng gửi đi cho cấp trên hoặc team.
- **Linh hoạt mở rộng:** Dễ dàng thay thế Google Sheets bằng Airtable, Notion hoặc bất kỳ cơ sở dữ liệu nào khác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Google** (để kết nối Google Sheets).
- **OpenAI API Key** (đã nạp tiền vào tài khoản để sử dụng mô hình `gpt-4o`).
- **File Google Sheets mẫu**: Các sếp có thể tham khảo [Sample Marketing Sheet](https://docs.google.com/spreadsheets/d/1UDWt0-Z9fHqwnSNfU3vvhSoYCFG6EG3E-ZewJC_CLq4/edit?usp=sharing) (hàng đầu tiên là tên cột, dữ liệu từ hàng 2 đến 100).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, sau đó vào giao diện n8n Editor, chọn **Add workflow** -> Click vào dấu `...` ở góc trên bên phải -> Chọn **Import from JSON** và dán đoạn mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 11 nodes chính, các sếp cần tập trung cấu hình kỹ các điểm sau:

- **Node `Get Data` (Google Sheets):**
  - Chọn Credentials: Tạo mới `Google Sheets OAuth2 API` và đăng nhập tài khoản Google của các sếp.
  - Chọn đúng file Spreadsheet chứa dữ liệu marketing và chọn Sheet tương ứng.
- **Các node tính toán (`Sum Campaigns`, `Sum Channels`, `Combine`, `Combine `, `Merge Results`, `Convert to Text`):**
  - Các node này làm nhiệm vụ gom nhóm và chuẩn bị dữ liệu thô. Các sếp có thể giữ nguyên cấu hình mặc định nếu cấu trúc file Google Sheets giống với bản mẫu.
- **Node `OpenAI Chat Model1`:**
  - Chọn model: `gpt-4o`.
  - Cấu hình Credentials: Thêm `OpenAI API` key của các sếp vào đây.
- **Node `Analyze Marketing Data` (AI Agent & Structured Output Parser):**
  - Agent sẽ nhận dữ liệu đã được xử lý từ các bước trước, kết hợp với GPT-4o để phân tích ROI và xuất ra kết quả theo định dạng chuẩn xác đã được định nghĩa ở `Structured Output Parser1`.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** (hoặc dùng `Start Workflow` dạng Manual Trigger) để chạy thử nghiệm với dữ liệu mẫu xem kết quả trả về đã chính xác chưa.
- Sau khi test thành công, gạt công tắc sang **Active** để bật chế độ tự động hóa hoàn toàn.

---

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình marketing của doanh nghiệp, các sếp có thể mở rộng workflow này bằng cách:
1. **Tích hợp kênh thông báo:** Thay vì chỉ nhận kết quả trên n8n, hãy gắn thêm node **Slack** hoặc **Telegram** để AI tự động bắn báo cáo ROI vào group chat của team vào mỗi thứ Hai hàng tuần.
2. **Lưu lịch sử báo cáo:** Thêm một node Google Sheets hoặc Airtable ở cuối workflow để tự động ghi lại lịch sử phân tích của AI theo ngày/tháng, tiện cho việc tracking xu hướng dài hạn.
3. **Cài đặt Trigger tự động:** Thay thế node `Start Workflow` (Manual) bằng **Schedule Trigger** (ví dụ: Chạy lúc 8:00 sáng mỗi thứ Hai hàng tuần) để hệ thống tự động làm việc mà không cần con người nhúng tay.

---

### 📌 Kết luận
Việc ứng dụng AI và tự động hóa vào báo cáo marketing không còn là xu hướng của tương lai mà là chìa khóa giúp doanh nghiệp tối ưu vận hành ngay hôm nay. Hãy import ngay workflow này, kết nối với Google Sheets của team và tận hưởng sự thảnh thơi mà n8n mang lại nhé các sếp!