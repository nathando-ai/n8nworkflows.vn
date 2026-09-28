---
title: "🚀 Tự động hóa Prompt AI: Lấy Dynamic Prompt từ GitHub và Điền Biến tự động trong n8n"
description: "Hướng dẫn xây dựng workflow n8n giúp tự động kéo prompt từ GitHub, thay thế biến động và truyền thẳng vào AI Agent sử dụng Ollama một cách chuyên nghiệp."
slug: "tu-dong-hoa-prompt-ai-github-ollama-n8n"
tags: [n8n, automation, ai-agent, github, ollama, no-code, prompt-engineering]
keywords: [n8n workflow, github dynamic prompts, ai agent n8n, ollama chat model, tự động hóa prompt, n8n viet nam]
---

# 🚀 Tự động hóa Prompt AI: Lấy Dynamic Prompt từ GitHub và Điền Biến tự động

Các sếp có đang gặp khó khăn trong việc quản lý các câu lệnh (prompt) cho AI? Khi làm các dự án AI lớn, việc hardcode prompt trực tiếp vào n8n khiến mỗi lần chỉnh sửa, tối ưu prompt, các sếp lại phải mò vào từng node, copy/paste vô cùng mất thời gian và dễ xảy ra sai sót. Hơn nữa, việc đồng bộ prompt giữa team kỹ thuật (lưu trên GitHub) và hệ thống n8n gần như phải làm thủ công.

Workflow này từ *RealSimple Solutions* chính là "vị cứu tinh" giúp các sếp giải quyết triệt để bài toán trên: tự động kéo file prompt từ kho lưu trữ GitHub, tự động điền các biến động (dynamic variables) vào prompt, kiểm tra tính hợp lệ và truyền trực tiếp vào AI Agent (sử dụng Ollama) một cách mượt mà, chuyên nghiệp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Quản lý Prompt tập trung:** Lưu trữ prompt trên GitHub, giúp team dễ dàng version control (quản lý phiên bản) và review thay đổi.
- **Tự động hóa hoàn toàn:** Không cần copy/paste thủ công, n8n tự động fetch và mapping các biến vào prompt.
- **Kiểm soát lỗi thông minh:** Tự động kiểm tra xem có bị thiếu biến nào trước khi gọi AI hay không, tránh lỗi lãng phí token hoặc AI hiểu sai ý.
- **Bảo mật & Linh hoạt:** Kết hợp cùng Ollama chạy local hoặc các LLM khác giúp tối ưu chi phí và dữ liệu nội bộ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Khuyên dùng Self-hosted hoặc n8n Cloud).
- **GitHub Account / API Credentials:** Để kết nối node GitHub và lấy file prompt từ repository.
- **Ollama API Credentials:** Đã cấu hình Ollama để làm mô hình ngôn ngữ cho AI Agent.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor, hoặc import file JSON tải từ trang chủ n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần chú ý cấu hình các node cốt lõi sau:
- **Node `GitHub`:** Chọn credential kết nối với tài khoản GitHub của các sếp, cấu hình đúng Repository, Branch và đường dẫn đến file chứa prompt (.txt hoặc .md). Hiện tại workflow đang để public repo mẫu để các sếp test.
- **Node `setVars`:** Đây là nơi các sếp khai báo các biến (variables) sẽ được truyền động vào trong prompt. Ví dụ: `Tên_Khách_Hàng`, `Sản_Phẩm`, `Yêu_Cầu`...
- **Node `replace variables` (Code node) & `Check All Prompt Vars Present`:** Các node code này có nhiệm vụ map các biến từ `setVars` vào nội dung prompt lấy từ GitHub, đồng thời kiểm tra xem có biến nào bị bỏ quên hay không. Nếu thiếu, luồng sẽ chuyển qua node `Stop and Error` để dừng lại an toàn.
- **Node `AI Agent` & `Ollama Chat Model`:** Cấu hình credentials cho Ollama và chọn model phù hợp (ví dụ: *llama3*, *mistral*,...) để nhận prompt đã được hoàn thiện và xử lý.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** để chạy thử với dữ liệu mẫu và kiểm tra kết quả trả về ở node `Prompt Output`.
- Sau khi test thành công, bật **Active** để đưa workflow vào trạng thái sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Webhook/Trigger:** Thay thế node `When clicking ‘Test workflow’` bằng Webhook hoặc Schedule (Cron) để tự động kích hoạt mỗi khi có API request hoặc vào khung giờ cố định.
- **Mở rộng kênh nhận kết quả:** Kết hợp thêm node Slack hoặc Telegram để sau khi AI Agent xử lý xong, kết quả sẽ được tự động bắn về nhóm chat cho team cùng theo dõi.
- **Lưu lịch sử:** Thêm node Google Sheets hoặc Database để ghi log lại các lần chạy prompt, phục vụ việc đánh giá hiệu suất của AI.

### 📌 Kết luận
Việc quản lý prompt qua GitHub kết hợp cùng n8n và AI Agent sẽ giúp quy trình ứng dụng AI của doanh nghiệp trở nên bài bản, chuyên nghiệp và tiết kiệm hàng giờ đồng hồ mỗi tuần. Hãy "lên đồ" ngay cho hệ thống n8n của các sếp thôi nào!