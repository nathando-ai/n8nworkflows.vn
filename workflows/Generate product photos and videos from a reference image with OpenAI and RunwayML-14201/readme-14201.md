---
title: "🚀 Tự động tạo ảnh sản phẩm và video quảng cáo AI từ ảnh gốc với OpenAI & RunwayML"
description: "Hướng dẫn cài đặt workflow n8n tự động hóa toàn bộ quy trình: nhận ảnh sản phẩm qua form, dùng GPT-4.1 viết prompt, tạo ảnh mới bằng OpenAI và dựng video marketing với RunwayML rồi gửi email cho khách."
slug: "tu-dong-tao-anh-video-san-pham-openai-runwayml"
tags: [n8n, automation, ai-video, openai, runwayml, content-creation]
keywords: [n8n workflow, tạo ảnh ai, tạo video ai, runwayml api, openai gpt-4, tự động hóa marketing]
---

# 🚀 Tự động tạo ảnh sản phẩm và video quảng cáo AI với OpenAI & RunwayML

Các sếp làm trong ngành e-commerce, media hoặc agency chắc chắn hiểu cảm giác tốn hàng giờ đồng hồ để chỉnh sửa ảnh sản phẩm và dựng video marketing thủ công cho từng item mới. Việc này không chỉ tốn nhân lực mà còn chậm chạp khi cần scale chiến dịch quảng cáo.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code (No-code): Nhận thông tin từ form khách hàng/nhân sự $\rightarrow$ AI viết prompt chuyên nghiệp $\rightarrow$ Tạo ảnh sản phẩm đột phá bằng OpenAI $\rightarrow$ Dựng video ngắn cực chất bằng RunwayML $\rightarrow$ Tự động gửi kết quả qua Gmail!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Từ form submit đến khi trả kết quả qua email mà không cần can thiệp thủ công.
- **Sức mạnh AI đa phương thức:** Kết hợp linh hoạt giữa GPT-4.1 (phân tích & viết prompt), OpenAI Image (tạo ảnh gốc mới) và RunwayML (dựng video chuyển động mượt mà).
- **Tối ưu thời gian:** Biến một bức ảnh sản phẩm đơn thuần thành trọn bộ tài liệu marketing (ảnh + video) chỉ trong vài phút.
- **Trải nghiệm khách hàng ấn tượng:** Gửi link ảnh và video trực tiếp qua Gmail ngay khi xử lý xong nhờ cơ chế Polling (Wait/If) thông minh.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **OpenAI API Key** (Đã bật quyền truy cập Image Generation cho mô hình `gpt-image-1`).
- **Tài khoản Google Drive** (Để lưu trữ ảnh gốc làm backup).
- **Tài khoản ImgBB** (Miễn phí tại imgbb.com để tạo public URL cho ảnh).
- **RunwayML API Key** (Dùng cho việc render video).
- **Tài khoản Google/Gmail** (Để cấu hình gửi email tự động).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ kho lưu trữ n8n hoặc copy trực tiếp và paste vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các Credentials và thông số sau cho các nodes:

- **A.I Stunning Generator Interface (`formTrigger`):**
  - Node này đóng vai trò là điểm khởi đầu (Form nhận ảnh sản phẩm, tên, vision prompt và email). Khi workflow Active, n8n sẽ cung cấp một Public URL để các sếp chia sẻ cho khách hàng hoặc nội bộ sử dụng. Hỗ trợ định dạng: `.jpeg`, `.jpg`, `.png`, `.webm`.

- **Image Generation Pipeline (`Upload to Google Drive`, `Chat GPT 4.1`, `OpenAi Create Image`...):**
  - **Google Drive:** Kết nối qua `Google Drive OAuth2`. Mở node `Upload to Google Drive` và cập nhật **Folder ID** của thư mục trên Drive của các sếp (lấy đoạn ID trên URL của folder).
  - **OpenAI:** Cấu hình credential dạng `HTTP Header Auth` (Header Name: `Authorization`, Value: `Bearer YOUR_OPENAI_API_KEY`). Gắn credential này cho cả node `Chat GPT 4.1` và `OpenAi Create Image`. Đảm bảo tài khoản OpenAI của các sếp có quyền dùng `gpt-image-1` (kiểm tra tại `platform.openai.com`).

- **Video Generation Pipeline (`Get URL`, `Create Video`, `60 Seconds`, `Send a message`...):**
  - **ImgBB:** Cấu hình credential dạng `HTTP Query Auth` (Parameter name: `key`, Value: `YOUR_IMGBB_API_KEY`) kết nối tới node `Get URL`.
  - **RunwayML:** Cấu hình credential dạng `HTTP Header Auth` (Header Name: `Authorization`, Value: `Bearer YOUR_RUNWAYML_API_KEY`) gắn vào node `Create Video` và node HTTP Request polling trạng thái.
  - ⚠️ **LƯU Ý QUAN TRỌNG:** **Không được thay đổi** header `X-Runway-Version` bên trong các node RunwayML. Nó phải giữ nguyên giá trị `2024-11-06` nếu không API call sẽ thất bại.
  - **Gmail:** Kết nối qua `Google Gmail OAuth2` tại node `Send a message` để gửi email tự động chứa link ảnh và video cho người dùng.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền form mẫu để kiểm tra toàn bộ luồng chạy (từ tạo ảnh đến render video và gửi mail).
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để hệ thống tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram/Slack:** Thêm node gửi thông báo về nhóm chat nội bộ mỗi khi có khách hàng tạo xong video sản phẩm.
- **Lưu trữ database:** Thêm node Google Sheets hoặc Airtable để lưu lại thông tin email, prompt và link kết quả phục vụ việc chăm sóc khách hàng sau này.
- **Mở rộng định dạng video:** Tùy chỉnh tham số trong node RunwayML để tạo các góc quay hoặc thời lượng video khác nhau tùy theo nhu cầu chiến dịch quảng cáo.

### 📌 Kết luận
Workflow tạo ảnh và video sản phẩm bằng AI này là một "vũ khí bí mật" giúp tự động hóa khâu sản xuất content thị giác cho các doanh nghiệp E-commerce. Hãy thiết lập ngay hôm nay để tiết kiệm hàng chục giờ làm việc thủ công và tăng tốc chiến dịch marketing của các sếp!