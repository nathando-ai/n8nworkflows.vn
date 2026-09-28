---
title: "🚀 Tự động hóa tạo Roto Mattes đa luồng với Seedance AI, QC và Nuke Handoff trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình tạo Roto Mattes đa luồng bằng Seedance AI, kiểm duyệt chất lượng (QC) và bàn giao sang Nuke cho kỹ sư VFX."
slug: "tu-dong-hoa-seedance-ai-roto-mattes-nuke-n8n"
tags: [n8n, automation, no-code, vfx, seedance-ai, ai-agent]
keywords: [n8n workflow, seedance ai, roto mattes, vfx automation, nuke handoff, qc gate, tự động hóa vfx]
---

# 🚀 Tự động hóa tạo Roto Mattes đa luồng với Seedance AI, QC và Nuke Handoff

Trong ngành sản xuất VFX (Visual Effects) và hậu kỳ phim ảnh, việc tách nền, vẽ roto (rotoscoping) thủ công luôn là "cực hình" ngốn rất nhiều thời gian và nhân lực. Các nghệ sĩ phải mất hàng giờ để bóc tách từng khung hình, làm chậm tiến độ dự án. 

Workflow n8n được thiết kế bởi **Rahul Joshi** này chính là giải pháp tự động hóa 100% không cần code (No-code), giúp kết nối **Seedance AI** để xử lý tạo multi-pass roto mattes, tự động kiểm định chất lượng (QC Gate) và chuyển giao trực tiếp dữ liệu sang phần mềm **Nuke** để các nghệ sĩ compositing làm việc tiếp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow xử lý các tác vụ AI và render nặng chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 4 luồng Roto Pass song song**: Tiết kiệm 80% thời gian bóc tách thủ công nhờ sức mạnh của Seedance AI.
- **Hệ thống QC tự động (Quality Control)**: Tự động chấm điểm chất lượng khung hình, lọc ra các pass đạt chuẩn hoặc đẩy thẳng sang Slack yêu cầu xử lý thủ công nếu điểm số quá thấp.
- **Tích hợp liền mạch với Nuke**: Tự động sinh template Roto Nuke và tải xuống các asset video phục vụ trực tiếp cho pipeline hậu kỳ.
- **Thông báo đa kênh thông minh**: Báo cáo trạng thái tức thì qua Slack, Telegram, Gmail và tạo Task tự động trên Jira cho team review.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Self-hosted hoặc Cloud).
- API Key truy cập Seedance AI service.
- Tài khoản và Credentials kết nối:
  - Google Sheets (Dùng làm Trigger đầu vào chứa danh sách task/brief).
  - Slack Bot Token (Gửi cảnh báo lỗi và yêu cầu manual roto).
  - Jira API Token (Tạo task review).
  - Gmail & Telegram (Gửi thông báo kết quả).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cấp hoặc copy toàn bộ mã JSON, sau đó mở n8n Editor chọn **Add workflow** -> **Import from File / Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình kỹ các node trọng điểm sau:
- **Google Sheets Trigger**: Kết nối tài khoản Google của bạn, trỏ tới file Sheet chứa yêu cầu (Roto Brief) đầu vào.
- **Validate & Extract Roto Brief & Fan-Out: 4 Roto Passes (Code nodes)**: Kiểm tra cấu trúc dữ liệu đầu vào và chia nhỏ thành 4 luồng xử lý roto song song.
- **Seedance: Generate Roto Pass & Poll: Check Roto Job Status (HTTP Request nodes)**: Cấu hình Endpoint API của Seedance AI, điền Bearer Token hoặc Header xác thực tương ứng.
- **Wait 20s**: Node chờ để hệ thống AI kịp thời gian render (có thể tinh chỉnh thời gian tùy thuộc vào dung lượng video).
- **QC Gate: Passes Threshold? (IF node)**: Thiết lập điều kiện điểm số QC (ví dụ: điểm đạt >= 85), nếu đạt sẽ đi tiếp, nếu không sẽ rẽ nhánh sang Slack cảnh báo.
- **Jira: Create Review Task & Slack nodes**: Trỏ đúng Project ID trên Jira và Channel ID trên Slack của team VFX để nhận thông báo chính xác.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thử với 1 dòng dữ liệu mẫu từ Google Sheets để kiểm tra toàn bộ chuỗi phản hồi (API Call -> Polling -> QC -> Nuke Template).
- Sau khi test thành công, bật công tắc **Active** góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Nâng cấp & gợi ý mở rộng
- **Tích hợp Webhook nhận diện hoàn thành**: Thay thế node **Wait 20s** và **Poll** bằng Webhook callback từ Seedance AI nếu hệ thống của họ hỗ trợ, giúp tối ưu tốc độ phản hồi.
- **Lưu trữ Cloud Storage**: Kết nối thêm node AWS S3 hoặc Google Drive để lưu trữ các file Roto Pass video vừa tải về (`Download Roto Pass Video`).
- **Báo cáo định kỳ**: Thiết lập thêm một nhánh gửi báo cáo tổng kết cuối ngày qua Slack về tổng số lượng Roto Passes đã hoàn thành.

### 📌 Kết luận
Workflow Seedance AI Roto Mattes này là một "vũ khí tối tân" giúp các studio VFX tự động hóa hoàn toàn khâu bóc tách nền và quản lý chất lượng. Hãy triển khai ngay lên hệ thống n8n của các sếp để tối ưu hóa năng suất cho team kỹ thuật nhé!