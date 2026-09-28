---
title: "🚀 Tự động hóa tạo chân dung UX Persona dựa trên dữ liệu thực tế với Perplexity, DALL·E 3 & Google Docs"
description: "Hướng dẫn xây dựng workflow n8n tự động nghiên cứu thị trường qua Perplexity, tạo mô tả UX Persona chi tiết, vẽ hình bằng DALL·E 3 và lưu trữ trực tiếp lên Google Docs/Drive."
slug: "tao-ux-persona-tu-dong-voi-perplexity-openai-google-docs"
tags: [n8n, automation, no-code, ai-agent, perplexity, openai, google-docs]
keywords: [n8n workflow, ux persona tự động, tạo persona bằng ai, perplexity sonar, dalle 3 image generation, google docs automation]
---

# 🚀 Tự động hóa tạo chân dung UX Persona chuẩn xác với Perplexity, DALL·E 3 & Google Docs

Việc xây dựng chân dung khách hàng (UX Persona) theo phương pháp thủ công thường tốn rất nhiều thời gian để khảo sát, tổng hợp dữ liệu và phác thảo hình ảnh. Thêm vào đó, các persona này đôi khi thiếu các số liệu thống kê thực tế về quy mô thị trường. 

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách tự động hóa 100%: Nhận yêu cầu từ form -> Nghiên cứu thị trường chuyên sâu qua Perplexity -> Tổng hợp mô tả chi tiết bằng AI Agent -> Vẽ ảnh đại diện bằng DALL·E 3 và lưu trữ toàn bộ vào Google Docs & Google Drive.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Thay vì mất hàng tuần nghiên cứu và thiết kế, hệ thống tự động hoàn thành trong vài phút.
- **Dữ liệu thực tế:** Sử dụng Perplexity để khai thác nguồn dữ liệu đáng tin cậy kèm theo ước tính quy mô thị trường cho từng persona.
- **Đa phương thức (Multimodal):** Tự động tạo mô tả chi tiết kết hợp hình ảnh trực quan sinh động thông qua DALL·E 3.
- **Đồng bộ tập trung:** Lưu trữ toàn bộ kết quả vào Google Docs và Google Drive, sẵn sàng chia sẻ cho đội ngũ sản phẩm.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc n8n Cloud).
- **Perplexity API Key** (Dùng cho node nghiên cứu thị trường).
- **OpenAI API Key** (Dùng cho GPT-4o-mini, GPT-4.1-mini và DALL·E 3).
- **Tài khoản Google** (Để kết nối Google Docs và Google Drive).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow hoặc tải file JSON từ nguồn cung cấp.
- Mở giao diện n8n Editor, chọn **Add workflow** -> **Import from File / Clipboard** và dán dữ liệu vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các credentials và tham số cho các node cốt lõi sau:

- **On form submission1 (`formTrigger`):** Node này tạo một giao diện Web Form đầu vào. Các sếp có thể mở node để xem URL form và tùy chỉnh các trường thông tin đầu vào (như website, khu vực, ngành nghề).
- **🔍 Research (`perplexity`):** Cần kết nối `perplexityApi` và chọn model `sonar-deep-research` để hệ thống tiến hành quét dữ liệu thị trường chất lượng cao.
- **OpenAI Chat Model2 / GPT-4o (`lmChatOpenAi`):** Cần cấu hình `openAiApi` credentials. Các model `gpt-4.1-mini` và `gpt-4o-mini` được sử dụng để tối ưu chi phí và tốc độ xử lý ngữ nghĩa.
- **Generate images (`openAi`):** Đảm bảo credentials OpenAI đã được cấu hình đúng để gọi API DALL·E 3 dựa trên prompt được tạo tự động từ node `Generate Prompts for Images`.
- **Upload images (`googleDrive`) & Update a document1 (`googleDocs`):** Kết nối tài khoản Google OAuth2 để cho phép workflow tự động tạo/cập nhật file Google Docs chứa nội dung Persona và tải ảnh lên Google Drive.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và điền thử nghiệm thông tin trên Web Form để kiểm tra toàn bộ luồng chạy.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để đưa workflow vào trạng thái vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Slack hoặc Telegram ở cuối workflow để bắn thông báo ngay về nhóm khi một bộ Persona mới được tạo xong.
- **Lưu trữ database:** Kết hợp thêm node Airtable hoặc Google Sheets để lưu lại lịch sử các yêu cầu tạo persona phục vụ việc tra cứu sau này.
- **Báo cáo định kỳ:** Tự động gửi email tổng hợp UX Persona trực tiếp cho các Stakeholder qua Gmail node.

### 📌 Kết luận
Workflow tạo UX Persona tự động này là trợ thủ đắc lực cho các Product Manager, Designer và các Agency Marketing. Hãy áp dụng ngay để nâng cao chất lượng nghiên cứu người dùng và tối ưu hóa quy trình phát triển sản phẩm của các sếp!