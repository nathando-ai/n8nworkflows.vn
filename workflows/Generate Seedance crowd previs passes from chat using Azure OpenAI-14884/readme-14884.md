---
title: "🚀 Tự động tạo Seedance Crowd Previs Passes từ Chat bằng Azure OpenAI trên n8n"
description: "Hướng dẫn chi tiết workflow n8n giúp tự động hóa quy trình tạo các lượt (passes) dựng hình đám đông (crowd previs) từ chat thông qua Azure OpenAI, tích hợp Slack, Gmail và Google Sheets."
slug: "tu-dong-tao-seedance-crowd-previs-passes-azure-openai-n8n"
tags: [n8n, automation, ai-agent, azure-openai, content-creation, slack, google-sheets]
keywords: [n8n workflow, seedance crowd previs, azure openai n8n, ai chatbot automation, tự động hóa dựng hình 3D, n8n việt nam]
---

# 🚀 Tự động tạo Seedance Crowd Previs Passes từ Chat bằng Azure OpenAI

Trong các dự án đồ họa, hoạt hình hay kỹ xảo điện ảnh (VFX), việc tạo ra các bản dựng hình đám đông sơ bộ (crowd previs passes) theo yêu cầu đạo diễn thường ngốn rất nhiều thời gian thủ công. Các sếp phải liên tục trao đổi, chia nhỏ tác vụ, gửi yêu cầu qua lại giữa các phòng ban, rồi lại ngồi chờ kết quả render từ hệ thống Seedance. Làm thủ công vừa dễ sai sót lại vừa chậm tiến độ dự án.

Workflow n8n này do chuyên gia **Rahul Joshi** thiết kế chính là giải pháp tự động hóa 100% không cần code (No-code/Low-code), giúp các sếp biến các đoạn chat yêu cầu thành một dây chuyền sản xuất crowd previs hoàn chỉnh. Hệ thống sẽ tự động nhận diện brief từ chat, phân rã thành các batch thông minh bằng **Azure OpenAI**, gửi yêu cầu đến Seedance, liên tục kiểm tra tiến độ (polling), lưu trữ dữ liệu vào **Google Sheets**, đồng thời tự động bàn giao kết quả cho đội ngũ Layout qua **Slack** và **Gmail**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Chuyển đổi yêu cầu dạng text từ chat thành các job chạy render đám đông tự động.
- **Tiết kiệm thời gian:** Loại bỏ hoàn toàn các bước thủ công như nhập dữ liệu, theo dõi trạng thái job hay gửi email thông báo thủ công.
- **Quản lý tập trung:** Mọi dữ liệu job được ghi nhận tự động vào Google Sheets để tra cứu bất cứ lúc nào.
- **Phối hợp mượt mà:** Tự động gửi kết quả hoàn chỉnh qua Slack và Gmail cho đội ngũ Layout ngay khi hoàn thành.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance **n8n** đang hoạt động (Self-hosted hoặc Cloud).
- Tài khoản và API Key của **Azure OpenAI** (để cấu hình mô hình chat thông minh).
- API/Endpoint truy cập hệ thống **Seedance** (thông qua HTTP Request).
- Tài khoản **Google Sheets** để lưu log dữ liệu.
- Workspace **Slack** và tài khoản **Gmail** để gửi thông báo tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow từ nguồn cung cấp, sau đó mở n8n Editor, chọn **Add workflow** -> **Import from File / Clipboard** và dán vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node cốt lõi sau:

- **Chat: Receive Crowd Brief & AI Agent & Azure OpenAI Chat Model**: 
  - Kết nối credentials của Azure OpenAI cho mô hình chat.
  - Tinh chỉnh Prompt trong AI Agent để mô hình hiểu đúng định dạng yêu cầu dựng hình đám đông mà các sếp mong muốn.
- **Seedance: Submit Pass & Poll: Job Status (HTTP Request)**: 
  - Cấu hình endpoint API chính xác của hệ thống Seedance.
  - Thêm token xác thực (Bearer Token hoặc API Key) vào phần Header của các HTTP Request này.
- **Wait 20s1 & Done? (Wait & If Nodes)**: 
  - Điều chỉnh thời gian chờ (Wait) cho phù hợp với tốc độ render thực tế của hệ thống Seedance trước khi gọi lệnh kiểm tra trạng thái tiếp theo (Polling).
- **Append The Data in the Sheet (Google Sheets)**: 
  - Chọn đúng file Google Sheet và Sheet Name dùng để lưu lịch sử các pass đã tạo.
- **Slack: Deliver to Layout Team & Email: Layout Guide to Team**: 
  - Kết nối tài khoản Slack và Gmail của workspace.
  - Cấu hình kênh Slack nhận thông báo (ví dụ: `#layout-team`) và danh sách email nhận tài liệu hướng dẫn.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một đoạn chat mẫu vào `Chat: Receive Crowd Brief` để test luồng chạy.
- Sau khi kiểm tra mọi thứ đã trơn tru, các sếp gạt công tắc sang **Active** để hệ thống tự động hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Có thể bổ sung thêm node Telegram hoặc Microsoft Teams nếu đội ngũ của các sếp dùng các nền tảng này thay cho Slack.
- **Cơ chế xử lý lỗi (Error Handling):** Thêm node *Error Trigger* để nếu Seedance gặp lỗi render, hệ thống sẽ tự động bắn tin nhắn cảnh báo về kênh quản lý.
- **Lưu trữ tệp kết quả:** Kết hợp thêm Google Drive hoặc AWS S3 node để tự động tải và lưu trữ các tệp previs passes xuất ra từ Seedance.

### 📌 Kết luận
Workflow tự động hóa tạo Seedance crowd previs passes bằng Azure OpenAI này là một "vũ khí" cực mạnh giúp các studio hoạt hình và kỹ xảo tối ưu hóa năng suất, giảm tải công việc lặp đi lặp lại cho đội ngũ sản xuất. Hãy cài đặt ngay hôm nay để đưa quy trình tự động hóa vào doanh nghiệp của các sếp!