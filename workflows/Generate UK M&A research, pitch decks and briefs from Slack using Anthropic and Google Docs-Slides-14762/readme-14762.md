---
title: "🚀 Tự động hóa M&A Anh Quốc: Tạo Nghiên Cứu, Pitch Deck & Briefing từ Slack với AI"
description: "Xây dựng trợ lý AI tài chính chuyên nghiệp trên n8n giúp tự động tra cứu Companies House, tạo tài liệu Google Docs và Google Slides từ Slack."
slug: "tu-dong-hoa-ma-anh-quoc-slack-ai-n8n"
tags: [n8n, automation, ai, slack, google-workspace, finance]
keywords: [n8n workflow, M&A automation, Slack bot AI, Google Slides automation, Companies House API]
---

# 🚀 Trợ lý AI Phân tích M&A Anh Quốc qua Slack

Các sếp trong ngành tài chính, đầu tư hay M&A có thấy mệt mỏi khi mỗi lần cần nghiên cứu doanh nghiệp (UK market) là phải lọ mọ lên *Companies House* tra cứu, tổng hợp tin tức, viết báo cáo trên Google Docs rồi lại cặm cụi làm Pitch Deck trên Google Slides không? Công việc thủ công này ngốn hàng giờ đồng hồ và dễ xảy ra sai sót.

Workflow n8n cực kỳ mạnh mẽ này sinh ra để giải quyết triệt để vấn đề đó. Chỉ với vài câu lệnh đơn giản ngay trên **Slack**, trợ lý AI sẽ thay các sếp làm toàn bộ từ A-Z: tra cứu dữ liệu doanh nghiệp, gọi AI phân tích sâu, tự động tạo thư mục, Google Docs báo cáo, Google Slides pitch deck và lưu trữ vào PostgreSQL / Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 (đặc biệt khi kết hợp AI và các API bên thứ ba), các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 3 nghiệp vụ chính**: Nghiên cứu doanh nghiệp (Research), tạo Pitch Deck (Pitch), và Bản tin ngành (Industry Briefing).
- **Tiết kiệm 90% thời gian**: Tổng hợp dữ liệu từ Companies House, Alpha Vantage, Firecrawl và AI phân tích chỉ trong chưa đầy 2 phút.
- **Đồng bộ đa nền tảng**: Tự động tạo cấu trúc Thư mục trên Google Drive, file Google Docs, Google Slides và cập nhật dữ liệu vào PostgreSQL / Google Sheets.
- **Tương tác mượt mà qua Slack**: Nhận kết quả trực tiếp về thread Slack ngay sau khi xử lý xong.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **Slack App / Bot Token**: Để lắng nghe tin nhắn và gửi phản hồi (`Slack Trigger`, `Send Slack Reply`).
- **OpenRouter API Key / OpenAI API Key**: Dùng cho các node `Intent Classifier`, `Research AI`, `Pitch AI`, `Brief AI`.
- **Companies House API (Miễn phí)**: Tra cứu thông tin pháp lý doanh nghiệp tại Anh Quốc.
- **Firecrawl API**: Thu thập thông tin website và tin tức doanh nghiệp/ngành.
- **Alpha Vantage API (Miễn phí)**: Lấy dữ liệu tài chính thị trường nếu công ty niêm yết.
- **Google Cloud OAuth2 Credential**: Cấp quyền kết nối Google Drive, Google Docs, Google Sheets và Google Slides.
- **PostgreSQL Database**: Lưu trữ bộ nhớ nghiên cứu (Research memory) và thông tin công ty.
- **Tài nguyên mẫu**: [Thư mục tài nguyên mẫu Google Drive](https://drive.google.com/drive/folders/15xftVTrQLGJN0SjyEQsOM96cWVNuJgDl?usp=sharing)
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ nguồn gốc hoặc copy toàn bộ mã JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng ba chấm (`...`) ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Vì workflow có tới 78 nodes, các sếp cần tập trung cấu hình kỹ các nhóm sau:
- **Slack Trigger & Send Slack Reply**: Kết nối tài khoản Slack workspace của công ty, cấu hình đúng channel chuyên trách nhận lệnh phân tích tài chính.
- **Intent Classifier & Các node AI (OpenRouter)**: Đảm bảo các node `Intent Classifier`, `Research AI`, `Pitch AI`, `Brief AI` được cấu hình đúng Credentials (OpenRouter API) và trỏ tới model AI mong muốn (có thể dùng các model tiết kiệm như Claude 3.5 Sonnet hoặc Kimi).
- **Companies House & Financial APIs**: Cấu hình xác thực HTTP Basic Auth / Header Auth cho các node gọi API tra cứu công ty Anh Quốc, Firecrawl và Alpha Vantage.
- **Google Drive / Docs / Slides / Sheets**: Chọn đúng tài khoản Google OAuth2. Đối với node `Copy Slides Template`, hãy trỏ tới ID của file Slide mẫu chuẩn M&A từ thư mục Google Drive đã chuẩn bị.
- **PostgreSQL**: Cấu hình thông tin kết nối database (`postgres`) để lưu vết dữ liệu nghiên cứu phục vụ cho việc tạo Pitch Deck sau đó.

#### 3. Kích hoạt ⚡️
- Chạy thử (Test run) với một câu lệnh mẫu trên Slack (ví dụ: *"Research fintech company Revolut"*).
- Kiểm tra các node xem dữ liệu có chảy qua mượt mà không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow sẵn sàng phục vụ 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Thay thế kênh chat**: Nếu công ty không dùng Slack, các sếp có thể thay thế bằng **Telegram Bot** hoặc một Simple Web Form đơn giản để tối ưu chi phí và dễ setup hơn.
- **Tối ưu chi phí AI**: Sử dụng các mô hình LLM giá rẻ hoặc open-source (thông qua OpenRouter như Kimi k2.7 hoặc Gemini Flash) để giảm thiểu chi phí khi gọi API xử lý văn bản dài.
- **Mở rộng lưu trữ**: Có thể kết hợp thêm Supabase hoặc hoàn toàn lược bỏ bước lưu trữ Postgres nếu các sếp chỉ cần báo cáo tức thời (lưu ý: tính năng tạo Pitch Deck yêu cầu phải có lịch sử nghiên cứu lưu trong DB).

---

### 📌 Kết luận
Workflow "Generate UK M&A research, pitch decks and briefs from Slack" là một giải pháp tự động hóa đỉnh cao dành cho các quỹ đầu tư, công ty tài chính hoặc chuyên gia M&A. Việc tích hợp AI, các API dữ liệu thị trường Anh Quốc và hệ sinh thái Google Workspace giúp tự động hóa hoàn toàn quy trình phân tích tốn kém nhân lực. Hãy triển khai ngay hôm nay để tối ưu hóa năng suất đội ngũ của các sếp!