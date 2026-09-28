---
title: "🚀 Tự động tạo tên thương hiệu .com chuẩn SEO và kiểm tra domain với OpenAI, API Ninjas"
description: "Xây dựng hệ thống tự động hóa tìm kiếm và kiểm tra tên miền .com khả dụng dựa trên AI OpenAI và API Ninjas, lưu trữ kết quả trực tiếp vào Google Sheets."
slug: "tu-dong-tao-ten-thuong-hieu-va-kiem-tra-domain-n8n"
tags: [n8n, automation, openai, api-ninjas, google-sheets, market-research]
keywords: [n8n workflow, tạo tên thương hiệu, check domain tự động, openai n8n, api ninjas, google sheets automation]
---

# 🚀 Tự động tạo tên thương hiệu .com chuẩn SEO và kiểm tra domain với OpenAI, API Ninjas

Việc nghĩ ra một tên thương hiệu (brand name) ấn tượng, chưa bị đăng ký bản quyền và còn trống tên miền `.com` luôn là một "cực hình" đối với các nhà sáng lập startup, marketer hay lập trình viên. Việc tra cứu thủ công từng cái tên trên các trang registrar vừa tốn thời gian vừa dễ nản chí. 

Giải pháp? Workflow n8n này sẽ thay các sếp làm toàn bộ công việc nặng nhọc đó: Tự động dùng AI sáng tạo hàng loạt tên miền độc đáo, kiểm tra trạng thái `.com` real-time thông qua API và phân loại gọn gàng vào Google Sheets. Tất cả diễn ra tự động 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 99% thời gian:** Thay vì mất hàng tuần suy nghĩ và check domain thủ công, hệ thống tự động sinh ra hàng chục tên miền mỗi phút.
- **Không sợ trùng lặp:** Workflow ghi nhớ các tên đã check trước đó (thông qua Google Sheets), đảm bảo AI không gợi ý lại các tên cũ.
- **Phân loại thông minh:** Tự động tách biệt tên miền còn trống (Available) và đã có chủ (Closed) vào 2 tab riêng biệt trên Google Sheets.
- **Cơ chế lặp thông minh (Loop):** Tự động lặp lại cho đến khi tìm đủ số lượng tên miền khả dụng mong muốn hoặc đạt ngưỡng giới hạn an toàn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **OpenAI API Key:** Để sử dụng model AI tạo tên thương hiệu.
- **API Ninjas Account:** Lấy `X-Api-Key` miễn phí tại [api-ninjas.com](https://api-ninjas.com) để kiểm tra trạng thái domain.
- **Google Sheets Credentials:** Tài khoản Google OAuth2 để n8n đọc/ghi dữ liệu lên bảng tính.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ n8n template (ID: 13571) và import trực tiếp vào giao diện n8n Editor của các sếp, hoặc sử dụng tính năng copy/paste JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 16 nodes được thiết kế mạch lạc. Các sếp cần cấu hình chính xác các điểm sau:

- **Google Sheets Nodes (`Read sheet available`, `Read sheet closed`, `Append to sheet available`, `Append to sheet closed`):** 
  - Kết nối tài khoản Google Sheets OAuth2.
  - Thay thế `YOUR_GOOGLE_SHEET_ID` thành ID Google Spreadsheet của các sếp.
  - Chuẩn bị 1 Google Sheet có 2 tab tên là `available` và `closed`, mỗi tab có hàng tiêu đề (header) gồm 2 cột: `domain` và `name`.
- **Node `Generate names (OpenAI)`:** 
  - Chọn Credentials OpenAI.
  - Tùy chỉnh Model (khuyên dùng `gpt-4o` hoặc `gpt-4o-mini`) để đạt chất lượng tên gọi tốt nhất.
- **Node `Check domain (API Ninjas)`:** 
  - Thiết lập Header `X-Api-Key` với mã API Key lấy từ trang API Ninjas của các sếp.
- **Node `Prepare prompt` (Tùy chọn nâng cao):** 
  - Chỉnh sửa lại phần mô tả sản phẩm/dịch vụ của các sếp trong đoạn code JS của node này để AI định hướng sáng tạo tên chuẩn xác hơn (lĩnh vực, phong cách, độ dài, từ khóa liên quan...).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** tại `Manual Trigger` để chạy thử nghiệm lần đầu và kiểm tra dữ liệu trả về.
- Sau khi test thành công, bật nút **Active** để sẵn sàng sử dụng bất cứ lúc nào.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node **Telegram** hoặc **Slack** sau bước ghi vào Google Sheets để nhận thông báo ngay lập tức mỗi khi hệ thống tìm được một tên miền `.com` đẹp và còn trống.
- **Mở rộng Đuôi Miền:** Chỉnh sửa node `Normalize to domains` nếu các sếp muốn mở rộng tìm kiếm thêm các đuôi phổ biến khác như `.io`, `.co`, `.net`.
- **Lên lịch tự động:** Thay thế `Manual Trigger` bằng `Schedule Trigger` để chạy ngầm định kỳ hàng tuần, giúp các sếp liên tục cập nhật danh sách ý tưởng thương hiệu mới.

### 📌 Kết luận
Workflow tự động hóa này là trợ thủ đắc lực cho bất kỳ ai đang lên kế hoạch tung sản phẩm mới, xây dựng startup hoặc làm dịch vụ branding. Triển khai ngay hôm nay để biến việc tìm kiếm tên miền trở thành một trò chơi thú vị!