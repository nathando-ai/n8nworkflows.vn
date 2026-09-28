---
title: "🚀 Trích xuất thông tin bảo mật từ báo cáo HackerOne tự động bằng Google Gemini và n8n"
description: "Hướng dẫn xây dựng trợ lý AI tự động phân tích báo cáo lỗ hổng từ HackerOne, tóm tắtpayload và kỹ thuật khai thác chuyên sâu cho bug bounty hunter."
slug: "trich-xuat-bao-cao-hackerone-google-gemini-n8n"
tags: [n8n, automation, secops, ai, google-gemini, bug-bounty, hackerone]
keywords: [n8n workflow, hackerone report summarizer, google gemini ai agent, secops automation, bug bounty automation, tóm tắt báo cáo bảo mật]
---

# 🚀 Trích xuất thông tin bảo mật từ báo cáo HackerOne tự động bằng Google Gemini

Các sếp làm trong lĩnh vực bảo mật (SecOps) hay là các Bug Bounty Hunter chắc chắn hiểu cảm giác "ngợp" khi phải đọc qua hàng tá báo cáo disclosure dài dằng dặc trên HackerOne để tìm ra các payload hoặc kỹ thuật khai thác thú vị. Việc đọc thủ công, ghi chép và phân tích từng kỹ thuật tốn rất nhiều thời gian và công sức.

Giải pháp là đây! Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình: chỉ cần ném một URL báo cáo HackerOne vào khung chat, AI Agent tích hợp Google Gemini sẽ tự động gọi API, đọc nội dung, lọc và trích xuất các thông tin bảo mật cực kỳ giá trị (như payload, kỹ thuật tấn công, cách khắc phục) thành một cấu trúc gọn gàng. Không cần code phức tạp, mọi thứ diễn ra trong tích tắc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Biến URL báo cáo thô thành bản tóm tắt kỹ thuật chuyên sâu chỉ sau một câu lệnh chat.
- **Tiết kiệm thời gian nghiên cứu**: Lọc nhanh các payload, POC và kỹ thuật bypass mà không cần đọc hết hàng nghìn chữ.
- **Giao diện chat trực quan**: Tương tác mượt mà thông qua giao diện chat tích hợp sẵn của n8n, hỗ trợ style riêng cho pentester.
- **Trợ lý AI thông minh**: Sử dụng sức mạnh của Google Gemini để phân tích ngữ cảnh bảo mật cực kỳ chính xác.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đã được public webhook (hoặc chạy trên VPS).
- Tài khoản Google AI Studio / Google Cloud để lấy **Google Gemini API Key** (Google PaLM API credentials).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào n8n Editor của mình, hoặc import file JSON trực tiếp thông qua menu quản lý workflow.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 4 nodes chính hoạt động nhịp nhàng với nhau. Các sếp cần chú ý cấu hình các điểm sau:

- **When chat message received (`chatTrigger`)**: 
  - Đây là điểm khởi đầu dưới dạng giao diện chat. Các sếp nhớ cấu hình public URL cho webhook của n8n để có thể truy cập giao diện chat mọi lúc.
  - Khi sử dụng, chỉ cần gửi URL dạng: `https://hackerone.com/reports/ID` (Workflow sẽ tự động chuyển đổi đuôi thành `.json` để fetch dữ liệu).

- **H1 report summarizer (`agent`)**:
  - Node AI Agent đóng vai trò cốt lõi điều phối quy trình phân tích, quyết định thời điểm gọi tool HTTP và định dạng lại kết quả trả về cho các hunter.

- **Google Gemini Chat Model (`lmChatGoogleGemini`)**:
  - Cần cấu hình **Google PaLM API credentials** (sử dụng Gemini API key của các sếp).
  - *Mẹo*: Nên cấu hình sử dụng model `gemini-2.5-pro` để đạt hiệu quả phân tích mã nguồn và báo cáo bảo mật tốt nhất. Có thể thay thế bằng các model LLM khác nếu muốn.

- **GET H1 report (`httpRequestTool`)**:
  - Tool này được Agent tự động gọi để lấy dữ liệu thô từ HackerOne JSON API (`https://hackerone.com/reports/{ID}.json`).
  - Node này không cần hardcode credentials vì dữ liệu HackerOne disclose là Public API, Agent sẽ tự động truyền đúng URL lấy từ khung chat.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Node** hoặc test thử trực tiếp trên giao diện Chat Trigger với một ID báo cáo HackerOne công khai bất kỳ (ví dụ: `https://hackerone.com/reports/123456`).
- Sau khi test thành công, bật trạng thái **Active** cho workflow để sẵn sàng sử dụng 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack / Telegram**: Thay vì chỉ chat qua giao diện web của n8n, các sếp có thể đổi trigger hoặc bổ sung node gửi kết quả tóm tắt thẳng về kênh Telegram/Slack cá nhân mỗi khi nghiên cứu xong một báo cáo hay.
- **Lưu trữ kiến thức (Knowledge Base)**: Kết nối thêm một node Google Sheets hoặc Notion để tự động lưu lại các payload và kỹ thuật hay ho được AI trích xuất, tạo thành một kho tàng "Cheat Sheet" cho riêng mình.
- **Tùy chỉnh Prompt cho Agent**: Thêm các ràng buộc cụ thể trong System Prompt của AI Agent (ví dụ: *"Chỉ tập trung trích xuất XSS payloads"* hoặc *"Phân tích sâu về logic bypass"* ) để phù hợp với ngách săn thưởng của các sếp.

### 📌 Kết luận
Một công cụ nhỏ nhưng có võ giúp tối ưu hóa thời gian nghiên cứu cho cộng đồng bảo mật. Hãy cài đặt ngay lên VPS của các sếp và bắt đầu "bóc tách" các báo cáo HackerOne thông minh hơn ngay hôm nay!