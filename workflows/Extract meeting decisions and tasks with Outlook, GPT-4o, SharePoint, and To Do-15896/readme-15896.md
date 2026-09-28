---
title: "🚀 Tự động hóa biên bản cuộc họp: Trích xuất quyết định và giao việc với Outlook, GPT-4o, SharePoint và To Do"
description: "Xây dựng hệ thống AI tự động đọc email tóm tắt cuộc họp từ Outlook, trích xuất quyết định và action items bằng GPT-4o, sau đó lưu vào SharePoint và Microsoft To Do."
slug: "tu-dong-hoa-bien-ban-cuoc-hop-outlook-gpt4o-sharepoint-todo"
tags: [n8n, automation, microsoft, openai, ai-summarization, productivity]
keywords: [n8n workflow, tóm tắt cuộc họp tự động, gpt-4o outlook sharepoint, microsoft to do automation, xử lý biên bản họp ai]
---

# 🚀 Tự động hóa biên bản cuộc họp với AI, Outlook, SharePoint & Microsoft To Do

Các sếp có thường xuyên rơi vào cảnh sau mỗi cuộc họp là hàng tá ghi chú lộn xộn, không nhớ ai nhận việc gì và quyết định ra sao? Việc tổng hợp biên bản họp, ghi lại quyết định chiến lược và giao việc thủ công lên hệ thống vừa tốn thời gian, vừa dễ sót việc.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code (No-code/Low-code) do chuyên gia Mychel Garzon thiết kế. Hệ thống sẽ tự động quét email tóm tắt cuộc họp, nhờ **GPT-4o** phân tích thông minh, sau đó tự động ghi nhận quyết định vào **SharePoint** và tạo task giao việc đúng hạn trên **Microsoft To Do**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian thủ công**: Không cần phải đọc lại email dài dòng hay tự tay gõ từng task giao việc.
- **Minh bạch hóa quyết định**: Mọi quyết định chiến lược của cuộc họp được tự động lưu vào SharePoint để tra cứu bất cứ lúc nào.
- **Quản lý task chính xác**: Tự động tạo task trên Microsoft To Do kèm theo deadline và người phụ trách được chuẩn hóa qua múi giờ.
- **Giám sát lỗi thông minh**: Tự động gửi email cảnh báo về cho quản trị viên ngay lập tức nếu có bất kỳ lỗi nào xảy ra trong quá trình chạy.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Microsoft Outlook OAuth2**: Dùng để quét email đến và gửi email báo lỗi.
- **OpenAI API Key**: Sử dụng mô hình `gpt-4o` để trích xuất thông tin thông minh từ nội dung cuộc họp.
- **Microsoft SharePoint**: Nơi lưu trữ danh sách các quyết định cuộc họp (SharePoint List).
- **Microsoft To Do**: Nơi nhận các đầu việc (action items) được tạo tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn JSON của workflow (hoặc tải file từ nguồn) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động mượt mà với môi trường của công ty, các sếp cần cấu hình chính xác các node sau:
- **Outlook Trigger**: Thay thế địa chỉ `bot@yourcompany.com` bằng địa chỉ email thực tế của con bot chuyên gửi bản tóm tắt cuộc họp.
- **Extract Insights via AI (`gpt-4o`)**: Kết nối credentials OpenAI của các sếp.
- **Log to SharePoint List (`microsoftSharePoint`)**: Kết nối tài khoản SharePoint và chọn đúng Site, List đích để lưu biên bản quyết định.
- **Create To Do Tasks (`microsoftToDo`)**: Kết nối tài khoản Microsoft To Do và thay thế `YOUR_TODO_LIST_ID` bằng ID danh sách công việc thực tế của các sếp.
- **Parse & Route Arrays (`code`)**: Kiểm tra cài đặt node này và đảm bảo số lượng đầu ra (outputs) được cấu hình là `2` để chia luồng xử lý chính xác.
- **Normalize Due Date (`code`)**: Mặc định giờ hạn chót (deadline hour) là `14:00 UTC`. Các sếp có thể điều chỉnh hằng số `DEADLINE_HOUR_UTC` trong code cho phù hợp với múi giờ của team mình.
- **Send Error Email (`microsoftOutlook`)**: Kết nối tài khoản Outlook và thay thế `admin@yourcompany.com` bằng email nhận cảnh báo lỗi thực tế của sếp.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test run) với một email mẫu tóm tắt cuộc họp để kiểm tra các nhánh dữ liệu.
- Bật công tắc **Active** để workflow tự động hoạt động ngầm định kỳ (mỗi 15 phút).

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Chatops**: Nối thêm node **Slack** hoặc **Telegram** sau bước trích xuất AI để bắn thông báo tóm tắt cuộc họp nóng hổi lên nhóm chat chung của team.
- **Lưu trữ dữ liệu backup**: Kết hợp thêm node **Google Sheets** hoặc **Airtable** để lưu trữ song song dữ liệu quyết định phòng khi SharePoint gặp sự cố.
- **Phân loại mức độ ưu tiên**: Tinh chỉnh prompt trong node OpenAI để gán nhãn mức độ quan trọng (High, Medium, Low) cho từng task trên To Do.

### 📌 Kết luận
Việc tự động hóa biên bản cuộc họp chưa bao giờ dễ dàng đến thế với sự kết hợp hoàn hảo giữa n8n và sức mạnh của AI GPT-4o. Hãy thiết lập ngay hôm nay để giải phóng thời gian cho đội ngũ và đảm bảo không bỏ sót bất kỳ đầu việc quan trọng nào!