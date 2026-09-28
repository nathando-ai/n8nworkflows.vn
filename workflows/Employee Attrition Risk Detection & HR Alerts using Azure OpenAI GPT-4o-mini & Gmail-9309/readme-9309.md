---
title: "🚀 Tự Động Phát Hiện Rủi Ro Nhân Sự & Cảnh Báo HR Bằng AI Với n8n, Azure OpenAI GPT-4o-mini & Gmail"
description: "Xây dựng hệ thống tự động hóa thông minh giúp phân tích CV nhân sự mới, đánh giá rủi ro nghỉ việc (attrition risk) và gửi email cảnh báo cho bộ phận HR ngay lập tức."
slug: "tu-dong-phat-hien-rui-ro-nhan-su-hr-alerts-azure-openai-gmail"
tags: [n8n, automation, no-code, ai-agent, azure-openai, gmail, hr-automation]
keywords: [n8n workflow, tự động hóa nhân sự, azure openai gpt-4o-mini, hr alerts, google drive trigger, phân tích cv tự động]
---

# 🚀 Tự Động Phát Hiện Rủi Ro Nhân Sự & Cảnh Báo HR Bằng AI

Trong công tác quản trị nhân sự (HR), việc sàng lọc hồ sơ và đánh giá mức độ gắn bó lâu dài của ứng viên thông qua lịch sử làm việc là một bài toán tiêu tốn nhiều thời gian. Nếu làm thủ công, đội ngũ HR dễ bỏ sót các dấu hiệu nhảy việc liên tục hoặc rủi ro biến động nhân sự.

Giải pháp tuyệt vời cho các sếp đây! Bài viết này sẽ hướng dẫn chi tiết cách thiết lập một workflow n8n hoàn toàn tự động: Tự động bắt sự kiện khi có CV mới trên Google Drive, trích xuất văn bản, sử dụng sức mạnh của **Azure OpenAI GPT-4o-mini** kết hợp **AI Agent** để phân tích thời gian làm việc trung bình, đánh giá rủi ro và tự động gửi email cảnh báo chi tiết qua **Gmail** cho bộ phận HR.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Ngay khi ứng viên/headhunter đẩy CV lên Google Drive, hệ thống tự động tiếp nhận mà không cần thao tác tay.
- **AI thông minh phân tích sâu:** Sử dụng Azure OpenAI GPT-4o-mini để bóc tách lịch sử công việc, tính toán thời gian gắn bó trung bình (`Calculate avg span`) và dự báo rủi ro.
- **Phân luồng linh hoạt:** Dùng node `Logic` (If) để kiểm tra các điều kiện rủi ro trước khi đưa ra hành động tiếp theo.
- **Cảnh báo tức thì:** Tự động soạn thảo (`Create email`) và gửi email thông báo chi tiết (`Send email to hr`) đến bộ phận tuyển dụng qua Gmail.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc n8n Cloud).
- **Google Drive Account:** Để cấu hình trigger theo dõi thư mục chứa CV và tải file.
- **Azure OpenAI Account:** Có API Key và mô hình `gpt-4o-mini` sẵn sàng hoạt động.
- **Gmail Account:** Đã kết nối OAuth2 để n8n có quyền gửi email cảnh báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ n8n (ID: `9309` bởi tác giả Rahul Joshi) hoặc copy đoạn JSON và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 9 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Trigger for new resume (`googleDriveTrigger`):** Chọn tài khoản Google Drive credentials, sau đó trỏ đến thư mục cụ thể nơi các sếp (hoặc ứng viên) sẽ upload CV định dạng PDF.
- **Download resume (`googleDrive`):** Đảm bảo thao tác (`operation`) được đặt là `download` để lấy tệp tin từ Google Drive về hệ thống xử lý.
- **Extract text (`extractFromFile`):** Cài đặt thao tác đọc file dạng `pdf` để bóc tách toàn bộ nội dung chữ từ CV.
- **Azure OpenAI Chat Model (`lmChatAzureOpenAi`):** Kết nối Azure OpenAI API credentials và điền thông số model chính xác là `gpt-4o-mini`.
- **Structured Output Parser (`outputParserStructured`) & Calculate avg span (`agent`):** Đảm bảo cấu trúc prompt trong AI Agent yêu cầu trích xuất lịch sử công việc và tính toán chính xác thời gian làm việc trung bình tại mỗi công ty.
- **Logic (`if`):** Thiết lập các điều kiện logic (ví dụ: nếu thời gian trung bình ở mỗi công ty dưới 1 năm -> Rủi ro cao -> Chạy nhánh True).
- **Create email (`code`):** Node JavaScript xử lý dữ liệu đầu vào từ AI để tạo tiêu đề và nội dung email thông báo tuyển dụng/cảnh báo rủi ro một cách mượt mà.
- **Send email to hr (`gmail`):** Kết nối Gmail OAuth2 credentials và cấu hình người nhận là email của bộ phận HR (`hr@yourcompany.com`).

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** từng node hoặc **Execute Workflow** với một file CV mẫu trên Google Drive để kiểm tra toàn bộ luồng chạy.
- Sau khi test thành công không báo lỗi, gạt công tắc sang **Active** để hệ thống tự động hoạt động 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thay vì chỉ gửi email cho HR, các sếp có thể gắn thêm node Slack hoặc Telegram để bắn thông báo ngay lập tức lên group chat nội bộ của team tuyển dụng.
- **Lưu trữ Log vào Google Sheets:** Thêm một node Google Sheets để ghi lại lịch sử phân tích CV, điểm rủi ro của từng ứng viên nhằm phục vụ việc báo cáo định kỳ.
- **Mở rộng định dạng file:** Tùy chỉnh node `Extract text` để hỗ trợ thêm các định dạng file Word (.docx) bên cạnh PDF.

---

### 📌 Kết luận
Việc ứng dụng AI và tự động hóa vào quy trình nhân sự chưa bao giờ dễ dàng đến thế với n8n và Azure OpenAI. Hãy thiết lập ngay workflow này để giải phóng thời gian cho đội ngũ HR, giúp doanh nghiệp nhanh chóng phát hiện các rủi ro nhân sự và đưa ra quyết định tuyển dụng chính xác nhất!