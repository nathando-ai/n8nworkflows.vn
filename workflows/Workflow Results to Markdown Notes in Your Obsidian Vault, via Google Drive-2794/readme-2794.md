---
title: "🚀 Tự động lưu kết quả workflow thành ghi chú Markdown trong Obsidian qua Google Drive"
description: "Hướng dẫn chi tiết cách tự động hóa việc lưu kết quả từ bất kỳ workflow nào thành ghi chú Markdown trong Obsidian Vault thông qua Google Drive, tiết kiệm thời gian và nâng cao hiệu suất làm việc."
slug: "tu-dong-luu-ket-qua-workflow-thanh-ghi-chu-markdown-trong-obsidian-qua-google-drive"
tags: [n8n, automation, no-code, obsidian, google-drive]
keywords: [n8n workflow, tự động hóa, obsidian, google drive, markdown]
---

# 🚀 Tự động lưu kết quả workflow thành ghi chú Markdown trong Obsidian qua Google Drive

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải chuyển đổi kết quả từ các workflow thành ghi chú Markdown thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quá trình chuyển đổi kết quả workflow thành ghi chú Markdown.
- Tiết kiệm thời gian đáng kể khi không cần phải chuyển đổi thủ công.
- Tích hợp liền mạch với Obsidian Vault thông qua Google Drive.
- Hỗ trợ lưu trữ và quản lý tệp đính kèm một cách hiệu quả.
- Tùy chọn sử dụng AI để tự động tạo tiêu đề, YAML Frontmatter và nội dung ghi chú.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive với quyền truy cập đầy đủ.
- Tài khoản OpenAI để sử dụng các tính năng AI (nếu áp dụng).
- Obsidian Vault đã cài đặt trên máy tính.
- Google Drive Desktop đã được cài đặt và đồng bộ hóa.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/2794).
2. Click vào nút "Import" và sao chép JSON workflow.
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Node "Receive results from any workflow" (executeWorkflowTrigger)**:
  - Không cần cấu hình gì thêm, chỉ cần kết nối với các workflow khác.

- **Node "Save Markdown file" (googleDrive)**:
  - Chọn credentials "googleDriveOAuth2Api".
  - Cấu hình các tham số:
    - Operation: `createFromText`
    - Parent Folder: Chọn thư mục trong Google Drive để lưu trữ ghi chú.
    - File Name: `{{ $json.title }}.md` (hoặc tên tùy chỉnh).
    - File Content: Nội dung ghi chú Markdown (có thể bao gồm YAML Frontmatter).

- **Node "If the input has binary attachment" (if)**:
  - Không cần cấu hình gì thêm, chỉ cần kết nối với các node xử lý tệp đính kèm.

- **Node "Save attachment" (googleDrive)**:
  - Chọn credentials "googleDriveOAuth2Api".
  - Cấu hình các tham số:
    - Operation: `uploadFile`
    - Parent Folder: Chọn thư mục trong Google Drive để lưu trữ tệp đính kèm.
    - File Name: `{{ $json.attachmentName }}`.

- **Node "OpenAI Chat Model" và "OpenAI Chat Model1" (lmChatOpenAi)**:
  - Chọn credentials "openAiApi".
  - Cấu hình các tham số:
    - Model: Chọn mô hình OpenAI phù hợp (ví dụ: gpt-3.5-turbo).
    - Temperature: Điều chỉnh nhiệt độ (mặc định: 0.7).
    - Prompt: Nhập prompt cho mô hình AI (ví dụ: "Tạo tiêu đề cho ghi chú từ nội dung sau: {{ $json.content }}").

- **Node "Write Zettlekasten note from input1" và "Write YAML Frontmatter" (agent)**:
  - Không cần cấu hình gì thêm, chỉ cần kết nối với các node xử lý dữ liệu.

- **Node "Structured Output Parser" và "Structured Output Parser1" (outputParserStructured)**:
  - Không cần cấu hình gì thêm, chỉ cần kết nối với các node xử lý dữ liệu.

- **Node "Restructure JSON" (set)**:
  - Không cần cấu hình gì thêm, chỉ cần kết nối với các node xử lý dữ liệu.

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình các node, click vào nút "Activate" để kích hoạt workflow.
2. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
3. Kiểm tra thư mục trong Google Drive để xác nhận rằng ghi chú và tệp đính kèm đã được lưu trữ đúng cách.

### ✍️ Mẹo & gợi ý nâng cao
- **Tạo Symlink để tích hợp với Obsidian Vault**:
  - Mở Command Prompt với quyền Administrator.
  - Sử dụng lệnh `mklink /D "Target Path" "Source Path"` để tạo symlink giữa thư mục Google Drive và thư mục trong Obsidian Vault.
  - Ví dụ: `mklink /D "C:\Users\YourName\Vault\OtherFolder" "C:\Users\YourName\Google Drive\MyFolder"`.

- **Sử dụng AI để tự động tạo tiêu đề và YAML Frontmatter**:
  - Thay vì sử dụng trực tiếp các tham số JSON, các sếp có thể sử dụng các node AI để tự động tạo tiêu đề, YAML Frontmatter và nội dung ghi chú.
  - Điều này giúp nâng cao chất lượng và tính nhất quán của ghi chú.

- **Tùy chỉnh nội dung ghi chú**:
  - Các sếp có thể tùy chỉnh nội dung ghi chú bằng cách chỉnh sửa các node xử lý dữ liệu và các node AI.

- **Lưu trữ và quản lý tệp đính kèm**:
  - Các sếp có thể lưu trữ và quản lý tệp đính kèm một cách hiệu quả bằng cách sử dụng các node xử lý tệp đính kèm.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình chuyển đổi kết quả từ các workflow thành ghi chú Markdown trong Obsidian Vault thông qua Google Drive. Với các tính năng tự động hóa và tích hợp liền mạch, workflow này giúp tiết kiệm thời gian đáng kể và nâng cao hiệu suất làm việc. Các sếp chỉ cần cấu hình các node và kích hoạt workflow, sau đó hệ thống sẽ tự động xử lý và lưu trữ kết quả một cách hiệu quả.