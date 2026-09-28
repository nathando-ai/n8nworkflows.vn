---
title: "🚀 Tự động nhận lịch IPO qua Telegram với Finnhub API và Gemini AI"
description: "Hướng dẫn cài đặt workflow n8n tự động lấy lịch IPO và báo cáo tài chính từ Finnhub API, phân tích thông minh bằng Google Gemini AI và gửi thông báo trực tiếp qua Telegram mỗi tuần."
slug: "tu-dong-nhan-lich-ipo-telegram-finnhub-gemini"
tags: [n8n, automation, no-code, finnhub, gemini-ai, telegram, crypto-trading]
keywords: [n8n workflow, tu dong hoa, finnhub api, google gemini ai, telegram bot, lich ipo, crypto trading]
---

# 🚀 Tự động nhận lịch IPO qua Telegram với Finnhub API và Gemini AI

Việc theo dõi lịch IPO (phát hành cổ phiếu lần đầu ra công chúng) và các báo cáo tài chính quan trọng trên thị trường chứng khoán/crypto thường ngốn rất nhiều thời gian của các nhà đầu tư. Nếu cứ phải lướt web thủ công mỗi tuần, các sếp rất dễ bỏ lỡ những cơ hội vàng. 

Giải pháp hoàn hảo là đây: Workflow n8n tự động hoàn toàn giúp gom dữ liệu từ **Finnhub API**, nhờ **Google Gemini AI** phân tích, tổng hợp và bắn thẳng tin tức cực kỳ dễ đọc về **Telegram** của các sếp đúng lịch hẹn hàng tuần mà không cần chạm tay vào code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Chạy định kỳ mỗi tuần, không cần thao tác thủ công.
- **AI thông minh:** Sử dụng Google Gemini AI để lọc, định dạng và tóm tắt thông tin IPO rườm rà thành các gạch đầu dòng ngắn gọn, dễ hiểu.
- **Thông báo tức thì:** Nhận tin nhắn cập nhật trực tiếp qua Telegram cá nhân hoặc group làm việc.
- **Không bỏ lỡ cơ hội:** Nắm bắt lịch IPO và sự kiện tài chính nóng hổi ngay trong tầm tay.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Finnhub API Key:** Tài khoản miễn phí tại [Finnhub.io](https://finnhub.io/) để lấy dữ liệu tài chính.
- **Google Gemini API Key:** Key kết nối mô hình ngôn ngữ lớn từ Google AI Studio.
- **Telegram Bot Token:** Tạo một Bot thông qua `@BotFather` trên Telegram để gửi tin nhắn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này (hoặc copy toàn bộ mã JSON từ kho lưu trữ) và dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 9 nodes phối hợp nhịp nhàng. Các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Schedule Every 7 Days (`Schedule Trigger`):** 
  - Node này mặc định kích hoạt lịch chạy mỗi tuần. Các sếp có thể đổi khung giờ hoặc chu kỳ chạy theo ý muốn (ví dụ: chạy vào thứ Hai hàng tuần).
- **Set API Key for Finhubb & Dates (`Set`):** 
  - Điền `Finnhub API Key` của các sếp vào phần thông số cấu hình của node này.
- **Dynamically Sets the Date & Organizes Input (`Code`):** 
  - Các node JavaScript này tự động tính toán khoảng thời gian (từ ngày này đến ngày kia) để gọi dữ liệu API. Không cần sửa gì nếu không muốn đổi khoảng thời gian.
- **Gets Upcoming Earnings (`HTTP Request`):** 
  - Node này gọi API của Finnhub để lấy dữ liệu. Hãy đảm bảo URL endpoint và header chứa đúng API Key được truyền từ node `Set`.
- **Google Gemini Chat Model & AI Agent (`LangChain Nodes`):** 
  - Cấu hình Credentials cho Google Gemini bằng API Key của Google.
  - Node `Structured Output Parser` sẽ ép AI trả về dữ liệu đúng định dạng JSON mà hệ thống mong muốn.
- **Send Upcoming IPO Calendar Updates via Telegram (`Telegram`):** 
  - Kết nối tài khoản Telegram của các sếp (Chat ID và Bot Token). Nội dung tin nhắn sẽ tự động lấy từ kết quả phân tích của AI Agent để gửi đi.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** để chạy thử xem Telegram có nhận được tin nhắn hay không.
- Nếu mọi thứ mượt mà, gạt công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin:** Thay vì chỉ gửi qua Telegram, các sếp có thể nối thêm node Slack hoặc Discord để team cùng theo dõi.
- **Lưu trữ dữ liệu:** Thêm node Google Sheets ở cuối luồng để lưu lịch sử các mã IPO vào bảng Excel tiện tra cứu lại sau này.
- **Tùy chỉnh Prompt cho AI:** Trong node AI Agent, các sếp có thể yêu cầu Gemini viết thêm đánh giá rủi ro hoặc chỉ lọc ra các mã IPO lớn trên thị trường Mỹ.

### 📌 Kết luận
Với workflow n8n tích hợp Finnhub API và Gemini AI này, việc theo dõi thị trường tài chính chưa bao giờ nhàn hạ đến thế. Hãy "lên đồ" ngay cho hệ thống của mình để không bỏ lỡ bất kỳ con sóng IPO tiềm năng nào nhé các sếp!