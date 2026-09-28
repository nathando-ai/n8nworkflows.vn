---
title: "🚀 Tự Động Tạo Tin Nhắn Chăm Sóc Khách Hàng Từ Fireflies Transcript Bằng Google Gemini & Google Drive"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy lịch họp từ Google Calendar, truy vấn transcript từ Fireflies qua GraphQL, phân tích bằng AI Gemini và lưu kết quả vào Google Drive."
slug: "tu-dong-tao-follow-up-sales-tu-fireflies-transcript-gemini-google-drive"
tags: [n8n, automation, ai-agent, google-gemini, google-drive, fireflies]
keywords: [n8n workflow, chăm sóc khách hàng tự động, fireflies transcript, google gemini, AI agent n8n, sales follow up]
---

# 🚀 Tự Động Tạo Tin Nhắn Chăm Sóc Khách Hàng Từ Fireflies Transcript Bằng Google Gemini & Google Drive

Việc viết nội dung chăm sóc khách hàng (Sales Follow-up) sau mỗi cuộc họp thường ngốn rất nhiều thời gian của đội ngũ sales. Bạn phải nghe lại bản ghi, ghi chú các điểm chính và tự tay soạn thảo từng tin nhắn cá nhân hóa. Nếu làm thủ công cho hàng chục cuộc họp mỗi ngày, nguy cơ sót việc và giảm chất lượng chăm sóc là rất cao.

Được phát triển bởi **Websensepro**, workflow n8n này sẽ giải quyết triệt để bài toán trên bằng cách tự động hóa 100% quy trình: Lấy lịch hẹn từ Google Calendar $\rightarrow$ Truy vấn bản ghi cuộc họp (transcript) từ Fireflies $\rightarrow$ Dùng AI Agent (Google Gemini) phân tích và viết 12 tin nhắn follow-up siêu cá nhân hóa $\rightarrow$ Lưu trữ trực tiếp vào Google Drive. Các sếp không cần tốn một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn phải ngồi đọc lại toàn bộ bản ghi cuộc họp dài hàng tiếng đồng hồ.
- **Cá nhân hóa đỉnh cao:** AI tự động phân tích ngữ cảnh, điểm đau (pain points) và nhu cầu của khách hàng để tạo ra 12 mẫu tin nhắn tiếp cận phù hợp nhất.
- **Lưu trữ khoa học:** Tự động tạo tệp chứa nội dung chăm sóc và lưu thẳng vào thư mục Google Drive đã chỉ định, sẵn sàng để đội ngũ sales sử dụng bất cứ lúc nào.
- **Hoạt động tự động 24/7:** Chạy ngầm mỗi khi có lịch hẹn mới được tạo trên Google Calendar mà không cần con người can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Calendar Credentials** (để kích hoạt trigger khi có lịch họp).
- **Fireflies API Key / HTTP Header Auth** (để gọi GraphQL truy vấn transcript cuộc họp).
- **Google Gemini API Key** (Google Palm/Gemini API) cho AI Agent xử lý nội dung.
- **Google Drive Credentials** (OAuth2) để tạo file văn bản tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ [n8n.io Templates (10926)](https://n8n.io/workflows/10926), sau đó chọn **Import from File** hoặc copy trực tiếp mã JSON và dán vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 7 nodes chính hoạt động nhịp nhàng, các sếp cần lưu ý cấu hình kỹ các điểm sau:

- **Google Calendar Trigger**: Kết nối tài khoản Google Calendar của sếp. Node này sẽ làm nhiệm vụ lắng nghe và kích hoạt quy trình ngay khi có sự kiện lịch hẹn mới.
- **Edit Fields**: Dùng để chuẩn hóa dữ liệu đầu vào (ví dụ: lấy email của khách mời từ sự kiện lịch) trước khi truyền sang bước tiếp theo.
- **Filter ("Skip if Empty")**: Đảm bảo workflow chỉ tiếp tục chạy nếu tìm thấy thông tin khách hàng hợp lệ, tránh lãng phí tài nguyên gọi API khi không có dữ liệu.
- **GraphQL**: Cấu hình kết nối với Fireflies API (sử dụng `httpHeaderAuth`). Node này sẽ dùng email của khách mời để truy vấn và lấy toàn bộ bản ghi cuộc họp (transcript) từ hệ thống Fireflies.
- **AI Agent & Google Gemini Chat Model**: 
  - Chọn credentials cho **Google Gemini Chat Model** (`googlePalmApi`).
  - Trong **AI Agent**, thiết lập prompt hệ thống để hướng dẫn AI đọc hiểu transcript và tạo ra chính xác 12 thông điệp chăm sóc khách hàng cá nhân hóa dựa trên nội dung trao đổi thực tế.
- **Google Drive**: Cấu hình tài khoản `googleDriveOAuth2Api`, chọn thao tác `createFromText` để tự động tạo file tài liệu mới chứa 12 mẫu tin nhắn vừa được AI tạo ra và lưu vào thư mục chỉ định trên Google Drive.

#### 3. Kích hoạt ⚡️
- Nhấp vào **Execute Workflow** để chạy thử với dữ liệu mẫu từ lịch gần nhất, kiểm tra xem nội dung trả về Google Drive đã chính xác chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình sales automation này, các sếp có thể mở rộng thêm:
1. **Tích hợp Slack hoặc Telegram:** Thêm node gửi thông báo ngay lập tức về nhóm chat của đội Sales kèm link Google Drive chứa file tin nhắn vừa tạo.
2. **Gửi email tự động:** Kết hợp node Gmail để gửi trực tiếp bản nháp chăm sóc cho chính nhân viên sales phụ trách khách hàng đó.
3. **Lưu log vào Google Sheets:** Thêm node Google Sheets để ghi nhận lịch sử các cuộc họp đã được AI xử lý, giúp dễ dàng thống kê và quản lý hiệu suất.

### 📌 Kết luận
Workflow tích hợp Fireflies, Gemini và Google Drive là một "vũ khí bí mật" giúp đội ngũ sales tối ưu hóa thời gian sau họp và nâng cao tỷ lệ chốt đơn nhờ sự chăm sóc nhanh chóng, cá nhân hóa. Hãy cài đặt ngay hôm nay để tự động hóa toàn bộ khâu hậu kỳ cuộc họp của doanh nghiệp các sếp nhé!