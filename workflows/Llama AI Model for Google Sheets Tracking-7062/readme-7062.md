---
title: "🚀 Tự động hóa Trích xuất tài liệu & Theo dõi Google Sheets bằng Llama AI trên n8n"
description: "Hướng dẫn xây dựng workflow n8n sử dụng AI Agent (Llama qua OpenRouter) để trích xuất nội dung website/PDF, xử lý thông tin và cập nhật tự động vào Google Sheets."
slug: "tu-dong-hoa-trich-xuat-tai-lieu-google-sheets-llama-ai"
tags: [n8n, automation, no-code, AI Agent, Google Sheets, OpenRouter, Llama]
keywords: [n8n workflow, trích xuất PDF AI, Llama AI Google Sheets, OpenRouter n8n, tự động hóa tài liệu]
---

# 🚀 Tự động hóa Trích xuất tài liệu & Theo dõi Google Sheets bằng Llama AI

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thủ công lướt web, tải các file PDF tài liệu, đọc hiểu và nhập dữ liệu tóm tắt vào Google Sheets không? Công việc lặp đi lặp lại này không chỉ ngốn hàng giờ đồng hồ mà còn dễ xảy ra sai sót. 

Workflow n8n này do tác giả **Cristian Baño Belchí** phát triển chính là giải pháp tự động hóa 100% không cần code. Hệ thống sẽ kết hợp sức mạnh của **AI Agent (sử dụng mô hình Llama qua OpenRouter)** để tự động trích xuất nội dung từ website/PDF, phân tích thông tin, cập nhật vào Google Sheets và thông báo kết quả qua Discord.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Không cần đụng tay vào việc cào dữ liệu web, đọc PDF hay nhập liệu thủ công.
- **Trí tuệ nhân tạo thông minh:** AI Agent (Llama model) tự động tóm tắt, trích xuất dữ liệu chính xác theo đúng cấu trúc yêu cầu.
- **Đồng bộ dữ liệu liền mạch:** Tự động ghi nhận, cập nhật trạng thái (append/update) vào Google Sheets và đánh dấu các URL đã xử lý.
- **Cảnh báo thời gian thực:** Tự động gửi thông báo kết quả vào kênh Discord cá nhân hoặc nhóm của đội ngũ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Google Cloud / Google Drive / Google Sheets** (để quản lý file và bảng tính).
- **Tài khoản OpenRouter** (để lấy API Key kết nối với các mô hình AI như `meta-llama/llama-4-maverick`).
- **Webhook Discord** (để nhận thông báo tự động).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy toàn bộ mã JSON của workflow từ nguồn cung cấp, sau đó trong giao diện n8n Editor, chọn **New Workflow** -> Bấm vào dấu `...` ở góc trên bên phải -> Chọn **Import from JSON** và dán mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Schedule Trigger / When clicking ‘Execute workflow’**: 
  - Cấu hình tần suất chạy tự động (Schedule Trigger) theo ý muốn (ví dụ chạy hàng ngày, hàng giờ) hoặc dùng nút bấm thủ công để test.
- **HTTP Request & HTTP Request1 / HTML / Extract from File (PDF)**: 
  - Trỏ đến website hoặc nguồn tài liệu PDF mục tiêu mà các sếp muốn hệ thống cào dữ liệu và trích xuất.
- **Google Connection (Nodes: `Get row(s) in sheet`, `Update row in sheet`, `Append or update row in sheet`)**: 
  - Cần kết nối tài khoản Google thông qua Google Cloud API (bật sẵn Google Drive và Google Sheets). 
  - Tạo một Google Sheet trên Drive, sau đó cấu hình ID bảng tính và tên Sheet tương ứng vào các node này để hệ thống đọc/ghi dữ liệu.
- **OpenRouter Chat Model & AI Agent**: 
  - Tạo tài khoản trên [OpenRouter](https://openrouter.ai/), lấy API Key và kết nối vào node `OpenRouter Chat Model` (mặc định cấu hình mô hình `meta-llama/llama-4-maverick`).
  - Truy cập vào `AI Agent` để tùy chỉnh lại câu lệnh (Prompt) sao cho AI trích xuất đúng các trường dữ liệu mà các sếp mong muốn.
- **Discord**: 
  - Tạo một kênh riêng trên Discord, vào phần Cài đặt kênh (Channel Settings) -> Integrations -> Tạo Webhook và dán URL vào node `Discord` để nhận thông báo.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để chạy thử với dữ liệu mẫu, kiểm tra kỹ lưỡng các bước đọc file, gọi AI và ghi vào Google Sheets.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Kết hợp thêm node **Telegram** hoặc **Slack** bên cạnh Discord để đa dạng hóa kênh nhận báo cáo.
- **Xử lý lỗi (Error Handling):** Thêm Error Trigger để nếu quá trình cào PDF hoặc gọi AI gặp lỗi mạng, hệ thống sẽ tự động gửi cảnh báo về cho quản trị viên.
- **Lưu log chi tiết:** Bổ sung thêm các bước ghi log trạng thái chi tiết vào một sheet riêng để dễ dàng audit lịch sử chạy của AI.

### 📌 Kết luận
Workflow tích hợp Llama AI và Google Sheets này là một "vũ khí" cực kỳ mạnh mẽ giúp tối ưu hóa quy trình xử lý tài liệu phi cấu trúc thành dữ liệu có cấu trúc. Hãy triển khai ngay hôm nay để tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần cho đội ngũ của các sếp!