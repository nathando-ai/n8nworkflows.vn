---
title: "🚀 Tự động tạo và chỉnh sửa ảnh đỉnh cao với Havis AI GPT Image 2 trên n8n"
description: "Hướng dẫn cài đặt workflow n8n tích hợp Havis AI GPT Image 2 giúp tự động hóa quy trình tạo ảnh, chỉnh sửa ảnh qua form và trả về kết quả nhanh chóng."
slug: "tu-dong-tao-chinh-sua-anh-havis-ai-gpt-image-2-n8n"
tags: [n8n, automation, no-code, havis-ai, ai-image-generation, content-creation]
keywords: [n8n workflow, havis ai, gpt image 2, tao anh ai tu dong, n8n form trigger]
---

# 🚀 Tự động tạo và chỉnh sửa ảnh đỉnh cao với Havis AI GPT Image 2 trên n8n

Việc tạo và chỉnh sửa hình ảnh bằng các mô hình AI tiên tiến thường đòi hỏi nhiều thao tác thủ công trên giao diện web, khó tích hợp vào hệ thống nội bộ hoặc quy trình làm việc của đội ngũ marketing. 

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách cung cấp một giao diện Form trực tuyến cho phép người dùng nhập yêu cầu (prompt), cấu hình thông số và tự động gọi đến **Havis AI (GPT Image 2)** để xử lý, kiểm tra trạng thái (polling) và trả về kết quả hoàn chỉnh mà không cần can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Người dùng chỉ cần điền Form, hệ thống tự động gửi yêu cầu, chờ xử lý và trả kết quả ảnh.
- **Tiết kiệm thời gian:** Không cần thao tác thủ công trên nhiều nền tảng, hệ thống tự động kiểm tra trạng thái (polling) cho đến khi ảnh hoàn thành.
- **Linh hoạt cấu hình:** Hỗ trợ đa dạng tham số như prompt, chế độ (mode), tỷ lệ khung hình (aspect_ratio), độ phân giải và hình ảnh đầu vào để chỉnh sửa.
- **Kiểm soát chi phí:** Theo dõi số credit tiêu thụ qua metadata trả về sau mỗi lần tạo ảnh.
:::

### 📦 Các thành phần chính trong Workflow
Workflow bao gồm 10 nodes phối hợp nhịp nhàng:
1. **Form - GPT Image 2 (`formTrigger`):** Giao diện thu thập API key và các thông số tạo/chỉnh sửa ảnh từ người dùng.
2. **Build Payload (`code`):** Xử lý dữ liệu, loại bỏ giá trị trống và đóng gói thành JSON chuẩn cho API.
3. **Submit - Havis API (`httpRequest`):** Gửi yêu cầu khởi tạo tác vụ tới Havis AI.
4. **Wait 8s (`wait`):** Chờ trong giây lát trước khi kiểm tra trạng thái tác vụ.
5. **Check Task Status (`httpRequest`):** Kiểm tra tiến độ xử lý của tác vụ dựa trên `task_id`.
6. **Is Completed? (`if`):** Kiểm tra xem tác vụ đã hoàn thành hay chưa.
7. **Is Failed? (`if`):** Kiểm tra xem tác vụ có gặp lỗi hay không.
8. **Wait 8s (loop) (`wait`):** Vòng lặp chờ nếu tác vụ đang trong quá trình xử lý.
9. **Return Result (`set`):** Trả về kết quả thành công kèm URL hình ảnh.
10. **Return Error (`set`):** Trả về thông báo lỗi nếu tác vụ thất bại.

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản và API Key tại [Havis AI](https://havis.ai/manager/profile) (đảm bảo tài khoản có đủ credit).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc sao chép mã JSON từ nguồn.
- Mở n8n Editor, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp vào giao diện.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Form - GPT Image 2 (`formTrigger`):** Sau khi kích hoạt workflow, hãy mở URL của Form được cung cấp để kiểm tra các trường đầu vào như `prompt`, `mode`, `aspect_ratio`, `resolution`, `image_url_1`,...
- **Submit - Havis API (`httpRequest`):** Đảm bảo endpoint trỏ tới `https://havis.ai/api/gpt-image-2` và xác thực bằng Bearer Token từ Havis API Key do người dùng nhập qua form.
- **Check Task Status (`httpRequest`):** Cấu hình đúng endpoint kiểm tra trạng thái `https://havis.ai/api/task/{task_id}` để hệ thống thực hiện vòng lặp polling chính xác.
- **Thời gian chờ (Wait nodes):** Có thể điều chỉnh thời gian chờ (mặc định 8 giây) nếu cần tốc độ kiểm tra nhanh hơn hoặc chậm hơn tùy thuộc vào tải của hệ thống AI.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền thông tin vào Form.
- Kiểm tra kết quả trả về ở node **Return Result**.
- Bật công tắc **Active** góc trên bên phải để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack sau node **Return Result** để tự động gửi ảnh vừa tạo về nhóm chat của team.
- **Lưu trữ tự động:** Kết hợp với node Google Drive hoặc Supabase để lưu trữ vĩnh viễn các hình ảnh AI tạo ra.
- **Quản lý lịch sử:** Lưu metadata và URL ảnh vào Google Sheets hoặc Airtable để dễ dàng tra cứu lại cácprompt đã sử dụng.

### 📌 Kết luận
Workflow tạo và chỉnh sửa ảnh với Havis AI GPT Image 2 là giải pháp tuyệt vời để tối ưu hóa quy trình sáng tạo nội dung hình ảnh cho cá nhân và doanh nghiệp. Hãy triển khai ngay hôm nay để tiết kiệm thời gian và nâng cao hiệu suất công việc!