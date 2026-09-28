---
title: "🚀 Tự động chấm điểm bài khảo sát ứng viên và cập nhật Google Sheets với Azure GPT-4o-mini trong n8n"
description: "Xây dựng hệ thống tuyển dụng tự động 100%: tự động phát hiện câu trả lời khảo sát, dùng AI chấm điểm chuyên sâu và cập nhật điểm tổng hợp vào Google Sheets."
slug: "tu-dong-cham-diem-phong-van-azure-gpt-4o-mini-google-sheets"
tags: [n8n, automation, ai-agent, azure-openai, google-sheets, hr-automation]
keywords: [n8n workflow, chấm điểm ứng viên tự động, azure openai gpt-4o-mini, google sheets automation, tuyển dụng AI]
---

# 🚀 Tự động hóa đánh giá phỏng vấn và cập nhật điểm với Azure GPT-4o-mini & Google Sheets

Các sếp làm trong ngành Nhân sự (HR) hoặc Quản lý tuyển dụng có thấy quen thuộc với cảnh tượng: Mỗi mùa tuyển dụng đến, hòm thư và file Google Sheets ngập tràn bài khảo sát, bài test của ứng viên. Việc đọc thủ công từng bài, chấm điểm theo cảm tính, cộng dồn điểm cũ từ vòng hồ sơ và nhập liệu lại vào Google Sheets ngốn hàng tá thời gian, chưa kể dễ bỏ sót hoặc sai sót?

Đừng lo, workflow n8n cực đỉnh này do chuyên gia **Rahul Joshi** thiết kế sẽ thay thế các sếp làm toàn bộ quy trình đó một cách tự động, thông minh và chớp nhoáng nhờ sức mạnh của AI!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Ngay khi ứng viên submit form, hệ thống lập tức bắt tín hiệu và xử lý mà không cần con người nhúng tay.
- **Đánh giá khách quan & chuẩn xác:** AI (GPT-4o-mini) phân tích độ sâu kiến thức, khả năng giải quyết vấn đề và sự rõ ràng trong văn phong theo tiêu chuẩn thống nhất (0-30 điểm).
- **Hợp nhất dữ liệu thông minh:** Tự động tra cứu hồ sơ cũ (Resume store), cộng dồn điểm bài khảo sát với điểm đánh giá trước đó để ra Điểm tổng kết (Final Score).
- **Cập nhật database mượt mà:** Tự động đồng bộ kết quả vào Google Sheets theo thời gian thực dựa trên tên ứng viên.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Sheets Credentials**: Tài khoản Google chứa 2 bảng:
  1. Bảng thu thập câu trả lời khảo sát (`BD Questionarie` - sheet `Form Responses 1`).
  2. Bảng cơ sở dữ liệu ứng viên (`Resume store` - Sheet2).
- **Azure OpenAI API Key**: Kết nối mô hình `gpt-4o-mini` để làm "giám khảo" AI.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn hoặc sao chép mã JSON, sau đó dán trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node sau để workflow chạy mượt mà:
- **Monitor New Questionnaire Responses (`googleSheetsTrigger`)**: Kết nối tài khoản Google Sheets của các sếp, chọn đúng file bảng tính `BD Questionarie` và sheet `Form Responses 1`. Node này sẽ quét dữ liệu mới mỗi phút.
- **Azure OpenAI GPT-4 Model (`lmChatAzureOpenAi`)**: Nhập thông tin Azure Endpoint, Deployment Name và API Key của sếp. Đảm bảo model được chọn là `gpt-4o-mini` để tối ưu chi phí và tốc độ.
- **AI Questionnaire Evaluator (`agent`)**: Kiểm tra lại prompt hệ thống, định nghĩa tiêu chí chấm điểm (Knowledge depth, Problem-solving, Communication) với thang điểm từ 0-30 và yêu cầu trả về định dạng JSON thuần túy.
- **Lookup Candidate Profile Data (`googleSheets`)**: Cấu hình kết nối tới bảng `Resume store` để hệ thống kéo dữ liệu điểm cũ của ứng viên ra đối chiếu.
- **Update Candidate Database (`googleSheets`)**: Thiết lập operation là `appendOrUpdate`, chọn khóa định danh là tên ứng viên (`name`) để hệ thống biết chính xác dòng nào cần cập nhật `Questionarie Score` và `Final Score`.

#### 3. Kích hoạt ⚡️
- Chạy thử một bản ghi mẫu (Test run) để kiểm tra luồng JSON từ AI qua node **Parse AI Evaluation Results** (`code`) và node **Calculate Combined Scores** (`set`).
- Sau khi thấy mọi thứ chạy xanh mướt, bật công tắc **Active** lên để hệ thống tự động túc trực 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Nối thêm một node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay về nhóm tuyển dụng khi có ứng viên hoàn thành bài test xuất sắc (ví dụ: Final Score > 80).
- **Lưu lịch sử chi tiết:** Tích hợp thêm một bảng Google Sheets chuyên lưu log lỗi nếu bài nộp của ứng viên gặp vấn đề về định dạng.
- **Mở rộng câu hỏi:** Các sếp có thể dễ dàng thay đổi bộ câu hỏi chuyên môn trong prompt của AI Agent tùy theo vị trí tuyển dụng (Developer, Marketing, Sales...).

### 📌 Kết luận
Việc tối ưu hóa khâu tuyển dụng chưa bao giờ dễ dàng đến thế! Với workflow kết hợp n8n và Azure GPT-4o-mini này, các sếp vừa tiết kiệm được hàng chục giờ đồng hồ lọc hồ sơ, vừa đảm bảo tính công bằng và tốc độ phản hồi nhanh chóng cho ứng viên. Hãy cài đặt ngay hôm nay để nâng cấp hệ thống tuyển dụng của doanh nghiệp mình nhé!