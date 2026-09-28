---
title: "🚀 Tự động hóa tạo Thư mời nhận việc và Hợp đồng nhân sự với AI và Google Docs"
description: "Hướng dẫn xây dựng workflow n8n tự động trích xuất thông tin ứng viên từ CV, tích hợp GPT-4o-mini điền mẫu hợp đồng/offer letter và lưu trực tiếp vào Google Docs."
slug: "tu-dong-hoa-tao-thu-moi-nhan-viec-va-hop-dong-nhan-su-n8n"
tags: [n8n, automation, hr, ai, google-docs, openai]
keywords: [n8n workflow, tạo hợp đồng tự động, hr automation, gpt-4-mini, google docs integration]
---

# 🚀 Tự động hóa tạo Thư mời nhận việc và Hợp đồng nhân sự với AI và Google Docs

Các sếp làm trong ngành Nhân sự (HR) chắc chắn hiểu được nỗi khổ mỗi khi tuyển được nhân sự mới: phải cúp cuống copy-paste thông tin ứng viên từ CV và Căn cước công dân vào mẫu Thư mời nhận việc (Offer Letter) hoặc Hợp đồng lao động, rà soát lại từng con số mức lương, ngày vào làm, chức vụ... Chỉ cần sơ suất nhỏ là tài liệu sai sót, vừa mất chuyên nghiệp lại tốn rất nhiều thời gian.

Giải pháp ở đây là gì? Workflow n8n này sẽ tự động hóa **100%** quy trình trên. Bộ phận HR chỉ cần điền một form duy nhất, tải lên CV và giấy tờ tùy thân của ứng viên, phần việc còn lại để AI và hệ thống lo!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Giảm từ 30 phút nhập liệu thủ công xuống chỉ còn vài giây gửi form.
- **Độ chính xác tuyệt đối:** AI trích xuất thông tin chính xác từ tài liệu gốc (CV & Giấy tờ tùy thân) và điền vào template chuẩn.
- **Linh hoạt đa loại tài liệu:** Tự động nhận diện và chuyển đổi linh hoạt giữa việc tạo Thư mời nhận việc hoặc Hợp đồng lao động dựa trên lựa chọn của HR.
- **Đồng bộ đám mây liền mạch:** Tài liệu hoàn thiện được lưu ngay vào Google Docs, sẵn sàng để xem xét và gửi đi bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản OpenAI** (Cần có OpenAI API Key để sử dụng model `gpt-4.1-mini`).
- **Tài khoản Google** (Để cấp quyền truy cập Google Docs thông qua OAuth2).
- Các file mẫu (Template) Thư mời nhận việc và Hợp đồng được lưu sẵn trên Google Docs.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor, hoặc import file JSON đã tải về từ kho lưu trữ n8n (Workflow ID: 13241).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các node cốt lõi sau:

- **Receive Candidate Details via Form (`formTrigger`):** Node này cung cấp một đường link form để HR nhập thông tin ứng viên (Họ tên, Vị trí công việc, Mức lương, loại tài liệu cần tạo và file đính kèm gồm Căn cước/Aadhar và CV).
- **Extract Text from Aadhar and Resume (`extractFromFile`):** Node này có nhiệm vụ đọc file PDF được tải lên, trích xuất toàn bộ dữ liệu dạng text để phục vụ cho các bước phân tích tiếp theo.
- **Split Documents and Calculate Dates (`code`):** Node code JavaScript giúp bóc tách dữ liệu tài liệu, tính toán tự động ngày bắt đầu nhận việc dựa trên cấu hình.
- **Check Document Type Selection (`if`):** Kiểm tra xem HR chọn tạo "Offer Letter" hay "Contract" để định tuyến luồng xử lý phù hợp.
- **Load Offer Letter Template & Load Contract Template (`set`):** Chứa nội dung mẫu (template) của từng loại tài liệu với các placeholder chờ điền.
- **OpenAI GPT-4.1 Mini Model (`lmChatOpenAi`) & Fill Template with AI (`agent`):** Node LangChain Agent kết hợp với mô hình OpenAI `gpt-4.1-mini` cực kỳ thông minh. AI sẽ đọc nội dung từ CV/Giấy tờ, map vào các placeholder trong template mà vẫn giữ nguyên format định dạng ban đầu.
- **Save Document to Google Docs (`googleDocs`):** Node kết nối Google Docs OAuth2. Các sếp nhớ cấu hình **Operation** là `update` và trỏ đúng đường dẫn (URL) tới file tài liệu Google Docs mẫu trên drive của mình.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** và thử gửi một bản ghi mẫu qua form để kiểm tra dữ liệu trả về trong Google Docs.
- Sau khi test thành công, bật công tắc **Active** để đưa workflow vào trạng thái chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Thông báo:** Thêm node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay vào nhóm HR: *"Đã tạo xong hợp đồng cho ứng viên [Tên] - Link tài liệu: [URL Google Docs]"*.
- **Gửi Email tự động:** Kết hợp thêm node Gmail hoặc SendGrid để tự động gửi bản nháp hợp đồng tới cấp quản lý phê duyệt hoặc gửi trực tiếp cho ứng viên.
- **Lưu trữ Log:** Đẩy toàn bộ thông tin ứng viên sau khi tạo thành công vào một dòng mới trên Google Sheets để làm báo cáo tuyển dụng hàng tháng.

### 📌 Kết luận
Tự động hóa quy trình tuyển dụng không chỉ giúp bộ phận HR giải phóng khỏi những công việc lặp đi lặp lại nhàm chán mà còn nâng cao trải nghiệm ứng viên nhờ sự chuyên nghiệp và tốc độ phản hồi nhanh chóng. Hãy áp dụng ngay workflow này vào hệ thống của doanh nghiệp các sếp nhé!