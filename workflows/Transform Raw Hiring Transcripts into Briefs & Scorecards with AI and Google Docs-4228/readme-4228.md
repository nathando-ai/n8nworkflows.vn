---
title: "🚀 Tự động hóa chuyển đổi bản ghi tuyển dụng thô thành hồ sơ và bảng điểm với AI và Google Docs"
description: "Giải pháp tự động hóa 100% không cần code giúp chuyển đổi bản ghi tuyển dụng thô thành hồ sơ tuyển dụng và bảng điểm chuyên nghiệp chỉ trong 1 phút"
slug: "tu-dong-hoa-chuyen-doi-ban-ghi-tuyen-dung-tho"
tags: [n8n, automation, no-code, hr, ai]
keywords: [n8n workflow, tự động hóa tuyển dụng, google docs, openai, hr automation]
---

# 🚀 Tự động hóa chuyển đổi bản ghi tuyển dụng thô thành hồ sơ và bảng điểm với AI và Google Docs

[Đoạn mở đầu: Các sếp thường phải tốn nhiều thời gian và công sức để chuyển đổi bản ghi tuyển dụng thô thành hồ sơ tuyển dụng và bảng điểm chuyên nghiệp. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này chỉ trong 1 phút.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Chuyển đổi từ 1 bản ghi tuyển dụng thô thành hồ sơ và bảng điểm chuyên nghiệp chỉ trong 1 phút
- Tăng tính chuyên nghiệp: Tạo ra hồ sơ tuyển dụng và bảng điểm có định dạng chuẩn, dễ đọc và dễ quản lý
- Tăng hiệu quả: Giảm thiểu sai sót và tăng tính nhất quán trong quá trình tuyển dụng
- Tự động hóa toàn bộ quá trình: Không cần can thiệp thủ công, giảm thiểu công sức và thời gian cho các sếp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI API key (hoặc bất kỳ LLM nào khác)
- Tài khoản Google Drive
- Bản ghi tuyển dụng thô dưới dạng PDF
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/4228](https://n8n.io/workflows/4228)
3. Hoặc copy/paste JSON từ file workflow vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Sending raw hiring brief transcript" (formTrigger)**:
   - Cấu hình form để nhận bản ghi tuyển dụng thô dưới dạng PDF

2. **Node "Extracting text" (extractFromFile)**:
   - Đảm bảo đã chọn operation là "pdf"

3. **Node "Summarizing raw transcript" (openAi)**:
   - Thêm OpenAI API key vào credentials
   - Có thể điều chỉnh prompt để phù hợp với định dạng hồ sơ tuyển dụng mong muốn

4. **Node "Generating scorecards" (openAi)**:
   - Thêm OpenAI API key vào credentials
   - Có thể điều chỉnh prompt để phù hợp với định dạng bảng điểm mong muốn

5. **Node "Creating hiring brief file" (googleDocs)**:
   - Thêm Google Drive credentials
   - Có thể điều chỉnh tên file và thư mục lưu trữ

6. **Node "Adding brief to file" (googleDocs)**:
   - Đảm bảo đã chọn operation là "update"
   - Có thể điều chỉnh nội dung và định dạng của hồ sơ tuyển dụng

7. **Node "Creating Scorecards file" (googleDocs)**:
   - Thêm Google Drive credentials
   - Có thể điều chỉnh tên file và thư mục lưu trữ

8. **Node "Adding scorecards to File" (googleDocs)**:
   - Đảm bảo đã chọn operation là "update"
   - Có thể điều chỉnh nội dung và định dạng của bảng điểm

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng như mong đợi
- Bật Active workflow để tự động hóa toàn bộ quá trình

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để thông báo khi quá trình tự động hóa hoàn thành
- Lưu log các bản ghi tuyển dụng đã xử lý để theo dõi và quản lý
- Gửi báo cáo định kỳ về tiến độ tuyển dụng và hiệu quả của quá trình tự động hóa

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và công sức trong quá trình tuyển dụng, đồng thời tăng tính chuyên nghiệp và hiệu quả của quá trình tuyển dụng. Hãy áp dụng ngay để trải nghiệm sự khác biệt!