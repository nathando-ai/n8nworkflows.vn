---
title: "🚀 Tự động tạo Test Case QA từ Figma Design sang Google Sheets bằng AI"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình viết test case từ bản thiết kế Figma sử dụng OpenAI GPT-4o-mini và đồng bộ trực tiếp vào Google Sheets."
slug: "tu-dong-hoa-tao-qa-test-cases-tu-figma-sang-google-sheets-n8n"
tags: [n8n, automation, ai, figma, google-sheets, openai]
keywords: [n8n workflow, figma to test cases, tự động hóa QA, openai gpt-4o-mini, google sheets automation]
---

# 🚀 Tự động tạo Test Case QA từ Figma Design sang Google Sheets bằng AI

Các sếp làm QA hoặc Product Manager có thấy cảnh viết test case thủ công dựa trên bản thiết kế Figma cực kỳ tốn thời gian không? Mỗi lần dev giao design mới là lại cặm cụi soi từng frame, từng nút bấm, viết từng bước test case đến mỏi tay mà vẫn dễ bỏ sót các edge case hoặc kiểm tra khả năng truy cập (accessibility).

Giải pháp cho các sếp đây: Workflow n8n tích hợp AI sẽ tự động "đọc" thiết kế Figma, phân tích luồng người dùng và tự động sinh ra hàng loạt test case chuẩn chỉnh, sau đó đẩy thẳng vào Google Sheets. Tiết kiệm ngay **2-3 tiếng** cho mỗi lần review thiết kế!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Không cần thủ công copy/paste hay mò mẫm từng layer trên Figma nữa.
- **AI thông minh**: Sử dụng OpenAI GPT-4o-mini phân tích giao diện, tương tác, edge cases và kiểm tra WCAG 2.1 (accessibility).
- **Đồng bộ mượt mà**: Toàn bộ kết quả (tiêu đề và các bước thực hiện) được lưu trữ gọn gàng vào Google Sheets.
- **Hoạt động linh hoạt**: Kích hoạt thủ công qua `Manual Start` bất cứ lúc nào các sếp cần phân tích file thiết kế mới.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Figma Personal Access Token**: Để gọi Figma API lấy cấu trúc file design.
- **OpenAI API Key**: Sử dụng model `gpt-4o-mini` (vừa thông minh, vừa siêu tiết kiệm, chỉ tốn khoảng $0.02 - $0.05 mỗi lần chạy).
- **Google Tài khoản & Google Sheets**: Kết nối qua OAuth2 để ghi dữ liệu test case.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào n8n Editor, hoặc import file JSON thông qua giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 8 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:
- **Fetch Figma Design Data (`httpRequest`)**: 
  - Cần tạo credentials loại `Header Auth` với tên header là `X-Figma-Token` và giá trị là Figma Personal Access Token của các sếp.
  - Cấu hình file ID động lấy từ input: `={{$json.figmaFileId}}`.
- **OpenAI GPT-4o-mini (`lmChatOpenAi`) & AI Test Case Generator (`agent`)**:
  - Thêm OpenAI API key vào Credentials.
  - Chọn model: `gpt-4o-mini`.
  - Nhiệt độ (Temperature) đặt khoảng `0.7` để AI có độ sáng tạo linh hoạt khi sinh test case.
- **JSON Output Schema (`outputParserStructured`)**: Định dạng đầu ra của AI thành JSON cấu trúc chuẩn gồm mảng các test case.
- **Parse and Format Test Cases (`code`)**: Node xử lý code JavaScript để bóc tách mảng `test_cases` từ AI output, ánh xạ đúng định dạng cho Google Sheets.
- **Export to Google Sheets (`googleSheets`)**:
  - Chọn thao tác `append` (thêm dòng mới).
  - Chỉ định đúng file Google Sheet và Sheet Name.
  - Cấu hình auto-map các cột: `title` và `steps`.

#### 3. Kích hoạt ⚡️
- Chạy thử (`Test workflow`) với một `figmaFileId` mẫu để kiểm tra kết quả trả về trong Google Sheets.
- Sau khi kiểm tra mọi thứ chạy mượt mà, các sếp có thể sẵn sàng sử dụng.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Kết nối thêm node Telegram hoặc Slack ở cuối workflow để bot tự động gửi thông báo *"Đã tạo xong X test cases cho design mới!"* kèm link Google Sheet.
- **Lưu log & Quản lý lỗi**: Thêm node Error Trigger để bắt sự cố nếu Figma API lỗi hoặc token hết hạn.
- **Mở rộng schema**: Có thể yêu cầu AI trả về thêm cột `Priority` (High/Medium/Low) hoặc `Expected Result` để bản test plan chuyên nghiệp hơn.

### 📌 Kết luận
Việc tự động hóa quy trình viết test case từ Figma không chỉ giúp đội ngũ QA giải phóng thời gian mà còn đảm bảo độ bao phủ test cực tốt cho sản phẩm ngay từ giai đoạn thiết kế. Hãy áp dụng ngay workflow này vào quy trình của các sếp để tối ưu hóa năng suất lập tức!