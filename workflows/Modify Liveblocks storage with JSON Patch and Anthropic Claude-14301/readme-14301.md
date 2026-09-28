---
title: "🚀 Tự động hóa chỉnh sửa Liveblocks Storage bằng JSON Patch và Anthropic Claude trong n8n"
description: "Hướng dẫn tích hợp AI Anthropic Claude với Liveblocks Storage qua n8n, cho phép AI tự động cập nhật tài liệu cộng tác real-time bằng JSON Patch cực kỳ mạnh mẽ."
slug: "chinh-sua-liveblocks-storage-voi-json-patch-va-anthropic-claude"
tags: [n8n, automation, ai, liveblocks, anthropic, json-patch, collaboration]
keywords: [n8n workflow, liveblocks storage, anthropic claude, json patch, ai agent, tự động hóa tài liệu real-time]
---

# 🚀 Tự động hóa chỉnh sửa Liveblocks Storage bằng JSON Patch và Anthropic Claude

Các sếp có bao giờ nghĩ đến việc để AI trực tiếp thao tác, chỉnh sửa các tài liệu cộng tác thời gian thực (như bản vẽ Figma, bảng trắng Miro, hay tài liệu chung) dựa trên yêu cầu ngôn ngữ tự nhiên chưa? Việc viết code thủ công để phân tích yêu cầu, tạo cấu trúc JSON Patch và cập nhật dữ liệu đồng thời thường rất phức tạp và dễ phát sinh lỗi.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code, kết hợp sức mạnh của **Liveblocks Storage** (hạ tầng đồng bộ dữ liệu thời gian thực) và **Anthropic Claude** (AI mô hình ngôn ngữ lớn). AI sẽ đọc trạng thái phòng, hiểu yêu cầu của người dùng, tạo ra các thao tác JSON Patch chính xác và áp dụng lên tài liệu, đồng thời hiển thị trạng thái hoạt động (presence) của AI ngay trên giao diện ứng dụng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa thông minh**: Chuyển đổi yêu cầu văn bản thành các thao tác JSON Patch tiêu chuẩn một cách chính xác.
- **Cộng tác Real-time**: Mọi thay đổi do AI thực hiện sẽ được cập nhật ngay lập tức trên trình duyệt của tất cả người dùng đang cộng tác.
- **Trải nghiệm trực quan (AI Presence)**: Hiển thị avatar/trạng thái của AI trong phòng làm việc khi nó đang xử lý công việc và tự động ẩn đi khi hoàn tất.
- **Tối ưu vận dụng AI**: Kết hợp LangChain Agent với mô hình Claude tiên tiến và Structured Output Parser để đảm bảo dữ liệu đầu ra luôn đúng định dạng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản và API Key của **Liveblocks** (`liveblocksApi`).
- Tài khoản và API Key của **Anthropic (Claude)** (`anthropicApi`).
- n8n Editor (phiên bản Cloud hoặc Self-hosted có hỗ trợ LangChain nodes).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy mã JSON của workflow này, dán thẳng vào không gian làm việc (n8n Editor) hoặc import file JSON trực tiếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 11 nodes được chia thành các phần chính, các sếp cần chú ý cấu hình kỹ các điểm sau:
- **Create a room & Get room storage / Patch room storage**: 
  - Chọn đúng Credentials của **Liveblocks** (`liveblocksApi`).
  - Cấu hình ID phòng (`Room ID`) hoặc để workflow tự tạo phòng mới bằng node `Create a room` cho việc test.
- **AI Agent & Anthropic Chat Model**:
  - Chọn Credentials **Anthropic** (`anthropicApi`).
  - Đảm bảo model được chọn là `Claude Sonnet 4.6` (hoặc phiên bản tương đương hỗ trợ tốt xử lý cấu trúc JSON).
- **Structured Output Parser**: 
  - Cấu hình schema để AI trả về đúng định dạng JSON Patch mà Liveblocks Storage yêu cầu (giúp cập nhật tài liệu chính xác mà không làm hỏng cấu trúc dữ liệu shapes/objects hiện tại).
- **Set presence in a room / Set presence in a room1**:
  - Cấu hình thông tin presence của AI (ví dụ: hiển thị tên "AI Assistant" và bật/tắt thời gian chờ expire sau 2 giây).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** từ node `When clicking ‘Execute workflow’` để chạy thử nghiệm thủ công và kiểm tra kết quả trả về ở các bước Get/Patch storage.
- Sau khi kiểm tra mọi thứ chạy mượt mà, các sếp có thể thay thế Trigger thủ công bằng Webhook, Chat Trigger hoặc Schedule để phục vụ hệ thống thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chat Interface**: Kết hợp workflow này với một Chat Trigger hoặc Webhook kết nối từ Telegram/Slack để người dùng có thể chat trực tiếp yêu cầu chỉnh sửa bản vẽ hoặc tài liệu chung.
- **Log lịch sử thay đổi**: Thêm một node Google Sheets hoặc Database để lưu lại lịch sử các câu lệnh mà AI đã thực thi lên Liveblocks room.
- **Xử lý lỗi (Error Handling)**: Thêm Error Trigger để thông báo qua Slack/Telegram nếu AI trả về JSON Patch không hợp lệ hoặc lỗi kết nối API Liveblocks.

### 📌 Kết luận
Workflow này mở ra khả năng vô tận trong việc xây dựng các ứng dụng cộng tác thông minh tích hợp AI (như bảng trắng, công cụ thiết kế, trình soạn thảo tài liệu chung). Hãy áp dụng ngay để nâng cấp hệ thống của các sếp lên một tầm cao mới!