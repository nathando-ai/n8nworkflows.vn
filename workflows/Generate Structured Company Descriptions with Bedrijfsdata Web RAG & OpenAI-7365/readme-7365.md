---
title: "🚀 Tạo Mô Tả Công Ty Tự Động Chuẩn SEO với Bedrijfsdata Web RAG & OpenAI trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu web qua Web RAG, kết hợp OpenAI LLM và cấu trúc hóa dữ liệu để cập nhật trực tiếp vào HubSpot CRM."
slug: "tao-mo-ta-cong-ty-tu-dong-voi-bedrijfsdata-rag-va-openai"
tags: [n8n, automation, ai, openai, hubspot, web-rag]
keywords: [n8n workflow, bedrock rag, openai chat model, hubspot automation, tự động hóa marketing, trích xuất dữ liệu web]
keywords: [n8n workflow, tự động hóa, bedrifjsdata, openai, hubspot crm, web rag]
---

# 🚀 Tạo Mô Tả Công Ty Tự Động Chuẩn SEO với Bedrijfsdata Web RAG & OpenAI

Việc thu thập thông tin chi tiết về khách hàng tiềm năng (leads) để làm giàu dữ liệu (data enrichment) cho CRM thường tốn rất nhiều thời gian nếu làm thủ công. Các sếp thường phải mất hàng giờ lướt website của từng công ty, đọc hiểu và tóm tắt lại để nhập vào CRM. 

Quá trình thủ công này không chỉ chậm chạp mà còn dễ sai sót và thiếu đồng bộ. Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n tự động hóa 100% quy trình: Nhận tên miền $\rightarrow$ Cào dữ liệu web thông minh qua Bedrijfsdata RAG $\rightarrow$ Tổng hợp và cấu trúc hóa bằng OpenAI $\rightarrow$ Cập nhật tự động vào HubSpot CRM.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% Data Enrichment:** Chỉ cần cung cấp tên miền, hệ thống tự động cào thông tin web, tóm tắt và phân tích mô hình kinh doanh của doanh nghiệp.
- **Cấu trúc dữ liệu chuẩn xác:** Sử dụng **Structured Output Parser** kết hợp OpenAI để ép AI trả về dữ liệu đúng định dạng mong muốn (JSON).
- **Đồng bộ CRM mượt mà:** Tự động đẩy kết quả phân tích vào HubSpot (hoặc CRM tùy chỉnh) mà không cần can thiệp thủ công.
- **Xử lý lỗi thông minh:** Tích hợp các nhánh xử lý lỗi riêng biệt cho từng công đoạn (Invalid input, RAG error, LLM error, HubSpot error) giúp hệ thống không bị crash giữa chừng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (phiên bản Cloud hoặc Self-hosted).
- **Tài khoản & API Key:**
  - **Bedrijfsdata.nl API:** Dịch vụ lấy dữ liệu web RAG (`bedrijfsdataApi`).
  - **OpenAI API Key:** Dành cho model `gpt-4o-mini` hoặc tương đương (`openAiApi`).
  - **HubSpot CRM:** Tài khoản có quyền kết nối OAuth2 (`hubspotOAuth2Api`).
- **ProspectPro API (Tùy chọn):** Nếu lấy dữ liệu từ hệ thống ProspectPro (`prospectproApi`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ n8n template hoặc copy toàn bộ JSON.
- Tại giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng menu (3 chấm) -> **Import from File** hoặc dán trực tiếp (Paste JSON).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 15 nodes được thiết kế chặt chẽ. Các sếp cần lưu ý cấu hình các điểm sau:
- **When Executed by Another Workflow (`executeWorkflowTrigger`):** Đảm bảo workflow nhận đầu vào là một `domain` (tên miền website công ty cần phân tích).
- **Company domain is required (`if`):** Kiểm tra xem tên miền có tồn tại hay bị trống trước khi thực hiện các bước tiếp theo. Chuyển hướng sang node **Error type 1: invalid input** nếu thiếu.
- **Get RAG domain & Get rag search (`@bedrijfsdatanl/n8n-nodes-bedrijfsdata.bedrijfsdata`):** Kết nối tài khoản `bedrijfsdataApi` để hệ thống tiến hành cào nội dung website và kết quả tìm kiếm.
- **OpenAI Chat Model (`lmChatOpenAi`):** Chọn model AI phù hợp (khuyên dùng `gpt-4o-mini` để tối ưu chi phí và tốc độ). Kết nối với `openAiApi` credentials.
- **Structured Output Parser (`outputParserStructured`):** Định nghĩa schema JSON đầu ra (ví dụ: tóm tắt công ty, sản phẩm/dịch vụ chính, đối tượng khách hàng mục tiêu).
- **Update company description (`hubspot`):** Chọn đúng kết nối HubSpot OAuth2, ánh xạ trường dữ liệu mô tả công ty từ kết quả phân tích của LLM vào trường tương ứng trên HubSpot Company.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với một tên miền mẫu (ví dụ: `apple.com` hoặc `tino.vn`) để test luồng chạy.
- Kiểm tra kết quả ở node HubSpot xem dữ liệu đã được cập nhật chính xác chưa.
- Gạt công tắc sang **Active** để đưa workflow vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ lưu vào HubSpot, các sếp có thể nối thêm node Telegram hoặc Slack để gửi thông báo tóm tắt về doanh nghiệp mới ngay vào group chat nội bộ.
- **Lưu lịch sử lỗi:** Kết nối các node `Error type...` (NoOp) vào Google Sheets hoặc cơ sở dữ liệu để ghi log, giúp dễ dàng debug khi website đối tác chặn bot cào dữ liệu.
- **Tùy biến Prompt AI:** Thay đổi prompt trong Basic LLM Chain để yêu cầu AI phân tích sâu hơn theo nhu cầu đặc thù của ngành (ví dụ: xác định công ty có phải là B2B SaaS hay không, phân tích thị phần...).

### 📌 Kết luận
Workflow **Generate Structured Company Descriptions with Bedrijfsdata Web RAG & OpenAI** là một giải pháp cực kỳ mạnh mẽ giúp tự động hóa khâu nghiên cứu khách hàng, tiết kiệm hàng trăm giờ làm việc thủ công cho đội ngũ Sales và Marketing. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa quy trình kinh doanh!