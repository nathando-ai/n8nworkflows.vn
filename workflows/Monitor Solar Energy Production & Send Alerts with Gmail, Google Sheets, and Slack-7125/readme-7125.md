---
title: "☀️ Tự Động Giám Sát Năng Lượng Mặt Trời & Cảnh Báo Sản Lượng Thấp Bằng n8n"
description: "Hướng dẫn cấu hình workflow n8n tự động lấy dữ liệu điện mặt trời từ API, kiểm tra hiệu suất, ghi nhận vào Google Sheets và gửi cảnh báo qua Gmail, Slack."
slug: "tu-dong-giam-sat-nang-luong-mat-troi-n8n"
tags: [n8n, automation, solar-energy, google-sheets, gmail, slack]
keywords: [n8n workflow, tự động hóa năng lượng mặt trời, monitor solar energy, giám sát điện mặt trời, n8n gmail slack]
---

# ☀️ Tự Động Giám Sát Năng Lượng Mặt Trời & Cảnh Báo Sản Lượng Thấp Bằng n8n

Việc vận hành hệ thống năng lượng mặt trời đòi hỏi sự theo dõi sát sao để phát hiện kịp thời các sự cố giảm sản lượng, suy hao hiệu suất tấm pin hoặc lỗi từ inverter. Nếu các sếp cứ phải kiểm tra thủ công các cổng thông tin năng lượng hoặc API mỗi vài tiếng một lần, chắc chắn sẽ tốn rất nhiều thời gian và dễ bỏ lỡ các khung giờ vàng sản lượng thấp.

Workflow n8n này do **WeblineIndia** phát triển sẽ giúp tự động hóa toàn bộ quy trình: Định kỳ lấy dữ liệu sản xuất điện mặt trời, phân tích ngưỡng sản lượng, tự động gửi email cảnh báo khi có bất thường, đồng thời lưu trữ dữ liệu hợp lệ vào Google Sheets và tổng kết báo cáo lên Slack. 100% tự động, không cần code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Cảnh báo tức thời:** Tự động gửi email qua Gmail ngay lập tức khi phát hiện sản lượng điện mặt trời sụt giảm bất thường so với ngưỡng định mức.
- **Lưu trữ lịch sử thông minh:** Tự động đồng bộ và cập nhật dữ liệu sản lượng chuẩn vào Google Sheets để tiện theo dõi, vẽ biểu đồ.
- **Báo cáo team linh hoạt:** Gửi bản tóm tắt trạng thái sản xuất định kỳ lên kênh Slack của đội ngũ kỹ thuật.
- **Vận hành 24/7:** Chạy ngầm liên tục mỗi 2 giờ mà không cần sự can thiệp thủ công của con người.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn n8n (Cloud hoặc Self-hosted).
- **Tài khoản Gmail:** Có kết nối Credentials (OAuth2) để gửi email cảnh báo.
- **Tài khoản Google Sheets:** Đã tạo sẵn một file Google Sheet để ghi log dữ liệu.
- **Workspace Slack:** Đã cấu hình Slack Bot/App và có quyền post tin nhắn lên kênh (Channel) chỉ định.
- **API Năng lượng mặt trời:** Endpoint API (ví dụ: Energidataservice API hoặc tương đương) để lấy dữ liệu sản xuất theo giờ.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow này dán trực tiếp vào trình soạn thảo (n8n Editor) hoặc sử dụng file JSON tải về từ nguồn cấp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 7 nodes chính được liên kết chặt chẽ. Các sếp cần cấu hình các điểm mấu chốt sau:

- **Trigger: Every 2 Hours (`scheduleTrigger`):** 
  - Mặc định chạy mỗi 2 giờ. Các sếp có thể thay đổi tần suất (chạy hàng giờ hoặc 4 tiếng/lần) tùy theo nhu cầu thực tế của hệ thống.
- **Fetch Solar Production Data (`httpRequest`):** 
  - Điền URL của API cung cấp dữ liệu sản lượng điện mặt trời (ví dụ: Energidataservice API). Thêm các Header xác thực (API Key, Token) nếu nhà cung cấp yêu cầu.
- **Filter Low Production Entries (`code`):** 
  - Node JavaScript này giúp lọc ra các bản ghi có sản lượng dưới ngưỡng tối thiểu cho phép. Các sếp có thể tuỳ chỉnh con số ngưỡng (threshold) trực tiếp trong đoạn code bên trong node này.
- **Check for Low Production (`if`):** 
  - Node điều kiện kiểm tra xem danh sách lọc có bản ghi nào bị lỗi sản lượng không.
- **Send Email Alert (Low Production) (`gmail`):** 
  - Chọn Credentials Gmail OAuth2 của các sếp.
  - Điền địa chỉ email người nhận (ví dụ: bộ phận kỹ thuật, quản lý vận hành) và tùy chỉnh nội dung thông báo.
- **Log Valid Production Data (`googleSheets`):** 
  - Chọn Credentials `googleSheetsOAuth2Api`.
  - Chỉ định đúng **Spreadsheet ID** và **Sheet Name**.
  - Cấu hình operation là `appendOrUpdate` để ghi mới hoặc cập nhật dữ liệu sản xuất hợp lệ.
- **Post Summary to Slack (`slack`):** 
  - Chọn Credentials `slackApi`.
  - Chọn Channel muốn gửi tin nhắn tóm tắt dữ liệu cuối ngày hoặc sau mỗi lần quét.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để test thủ công lần đầu, đảm bảo các node HTTP Request, Google Sheets và Gmail chạy mượt mà không báo lỗi đỏ.
- Nếu mọi thứ xanh mướt, hãy gạt công tắc sang **Active** để workflow chính thức tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram:** Bên cạnh Slack và Gmail, các sếp có thể nối thêm một node Telegram Bot để bắn tin nhắn cảnh báo ngay vào group chat điện thoại di động cho tiện theo dõi khi đang di chuyển.
- **Lưu log lỗi vào Notion/Airtable:** Ngoài Google Sheets, có thể tạo thêm một nhánh lưu các sự cố sản lượng thấp vào cơ sở dữ liệu Notion để lập biên bản sự cố tự động.
- **Gửi báo cáo tổng kết cuối ngày:** Sử dụng thêm một Schedule Trigger chạy lúc 20:00 hàng ngày để tổng hợp toàn bộ sản lượng trong ngày gửi vào Slack.

### 📌 Kết luận
Workflow giám sát năng lượng mặt trời này là một giải pháp hoàn hảo giúp tự động hóa khâu quản lý kỹ thuật, tiết kiệm hàng giờ kiểm tra thủ công mỗi tuần và giúp phát hiện sớm các sự cố hao hụt điện năng. Hãy "lên đồ" ngay cho hệ thống của các sếp nhé!