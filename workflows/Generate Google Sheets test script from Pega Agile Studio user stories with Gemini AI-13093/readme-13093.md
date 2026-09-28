---
title: "🚀 Tự động hóa tạo kịch bản kiểm thử Google Sheets từ Pega Agile Studio bằng Gemini AI"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa việc lấy User Story từ Pega Agile Studio, sử dụng Gemini AI để phân tích và tạo kịch bản kiểm thử chuyên nghiệp lưu trực tiếp lên Google Sheets."
slug: "tu-dong-hoa-tao-kich-ban-kiem-thu-google-sheets-tu-pega-agile-studio-voi-gemini-ai"
tags: [n8n, automation, no-code, google-sheets, gemini-ai, testing, pega]
keywords: [n8n workflow, pega agile studio, gemini ai, google sheets test script, tự động hóa kiểm thử, ai testing automation]
---

# 🚀 Tự động hóa tạo kịch bản kiểm thử Google Sheets từ Pega Agile Studio bằng Gemini AI

Là một kiểm thử phần mềm (Software Tester) hoặc QA làm việc với nền tảng Pega, các sếp chắc chắn hiểu rõ sự vất vả khi phải đọc hiểu các User Story (US) dài dòng từ **Pega Agile Studio**, sau đó thủ công viết ra các tiêu chí chấp nhận (Acceptance Criteria) và hàng loạt ca kiểm thử (Test Cases) trên Google Sheets. Công việc này chiếm rất nhiều thời gian, dễ bỏ sót và làm chậm tiến độ các Sprint.

Workflow n8n này ra đời để giải quyết triệt để nỗi đau đó! Bằng cách kết hợp sức mạnh của **Gemini AI** và hệ thống tự động hóa n8n, workflow sẽ tự động hóa 100% quy trình: Lấy dữ liệu US từ Pega Agile Studio -> Phân tích tiêu chí chấp nhận -> Yêu cầu AI sinh Test Case -> Định dạng dữ liệu -> Tự động khởi tạo và điền toàn bộ vào một Google Spreadsheet chuẩn chỉnh.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Biến một User Story phức tạp thành bộ Test Script hoàn chỉnh chỉ trong vài giây thông qua khung chat.
- **Tăng độ chính xác & minh bạch:** Tự động tách biệt Acceptance Criteria sang một sheet riêng để đảm bảo tính truy xuất nguồn gốc (traceability).
- **Làm sạch dữ liệu thông minh:** AI tự động sinh test cases và code node tự động lọc bỏ các dòng trùng lặp, trả về bảng tính gọn gàng, chuyên nghiệp.
- **Vận hành trơn tru trong Agile:** Giúp các Tester bắt kịp tốc độ phát triển cực nhanh của các Sprint trong Pega Platform.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Pega Agile Studio:** Tài khoản có quyền truy cập API / OAuth2 để gọi dữ liệu User Story (`Retrieve the US from Pega Agile Studio`).
- **Google Gemini AI API:** Credentials cho Google Gemini (`Google Gemini Chat Model`).
- **Google Sheets API:** Tài khoản Google kết nối OAuth2 để tạo và ghi dữ liệu lên Google Drive/Sheets.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã JSON từ nguồn gốc.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấn vào dấu `...` ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà, các sếp cần cấu hình chính xác các credentials và thông số tại các node trọng điểm sau:

- **When chat message received & Google Gemini Chat Model:** 
  - Kích hoạt chat trigger để nhập User Story theo định dạng mẫu (Ví dụ: `US-1234`).
  - Kết nối `Google Gemini Chat Model` với API Key Google Palm/Gemini hợp lệ.
- **Retrieve the US from Pega Agile Studio (HTTP Request node):** 
  - Cấu hình credentials `oAuth2Api` hoặc `httpBasicAuth` trỏ đến môi trường Pega Agile Studio của doanh nghiệp.
  - Điều chỉnh Endpoint URL phù hợp để lấy thông tin User Story theo mã ID được truyền từ khung chat.
- **Create spreadsheet for the testscript & các Google Sheets nodes:**
  - Cấu hình credentials `googleSheetsOAuth2Api`.
  - Node `Create spreadsheet for the testscript` sẽ tự động tạo một Google Spreadsheet mới trong Google Drive của tài khoản kết nối.
  - Các node `Add column headers...`, `Add acceptance criteria...`, `Add testcases...` và `Add the cleaned testcases...` sẽ tự động đổ dữ liệu vào các sheet tương ứng.
- **Code & Code to remove redundant data nodes:**
  - Các đoạn code JavaScript có sẵn trong workflow sẽ thực hiện nhiệm vụ đánh số thứ tự Acceptance Criteria (`AddNumbersToAccCrit`) và lọc bỏ dữ liệu trùng lặp (`Code to remove redundant data`) do AI sinh ra trước khi đẩy lại vào Google Sheets. Các sếp không cần sửa đổi code trừ khi có nhu cầu tùy chỉnh format riêng.

#### 3. Kích hoạt ⚡️
- Nhấn **Chat with workflow** (biểu tượng chat) để gửi thử một mã User Story mẫu (Ví dụ: `US-1234`).
- Kiểm tra kết quả trả về trong Google Drive xem file Google Spreadsheet đã được tạo và điền dữ liệu đầy đủ chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để đưa workflow vào trạng thái chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Slack/Telegram:** Thêm một node thông báo (Slack/Telegram) ở cuối workflow để gửi link Google Spreadsheet trực tiếp đến kênh của nhóm Scrum mỗi khi tạo xong test script.
- **Lưu log theo dõi:** Kết nối thêm một Google Sheet tổng hợp để lưu lại lịch sử các US đã được tạo test script, giúp Product Owner và Tester dễ dàng quản lý tiến độ.
- **Tùy chỉnh Prompt cho AI:** Tại node `AI: Create testcases` (LangChain Agent), các sếp có thể tinh chỉnh System Prompt để AI viết test case theo chuẩn riêng (Gherkin format Given/When/Then, định dạng ma trận kiểm thử tiếng Việt, v.v.).

### 📌 Kết luận
Việc tối ưu hóa quy trình kiểm thử phần mềm chưa bao giờ dễ dàng và tự động đến thế với sự trợ giúp của n8n và AI. Hãy áp dụng ngay workflow này vào quy trình làm việc Agile của đội ngũ để giải phóng sức lao động thủ công và tập trung vào chất lượng sản phẩm!