---
title: "🚀 Tự động săn việc làm Remote chất lượng cao với OpenAI, Decodo và Google Sheets"
description: "Xây dựng hệ thống tự động tìm kiếm, phân tích và chấm điểm công việc remote từ RemoteOK, so sánh với hồ sơ cá nhân và gửi Top 5 cơ hội tốt nhất qua Gmail."
slug: "tu-dong-san-viec-lam-remote-openai-decodo-google-sheets"
tags: [n8n, automation, no-code, openai, google-sheets, ai-agent]
keywords: [n8n workflow, tự động hóa tìm việc, remote jobs, openai gpt-4o-mini, decodo scraper, google sheets automation]
---

# 🚀 Tự động săn việc làm Remote chất lượng cao với OpenAI, Decodo và Google Sheets

Việc tìm kiếm một công việc remote (làm việc từ xa) phù hợp với kỹ năng, mức lương kỳ vọng và định hướng sự nghiệp thường tiêu tốn rất nhiều thời gian lướt các trang tuyển dụng. Các sếp có thấy mệt mỏi khi mỗi ngày phải lục lọi hàng trăm tin tuyển dụng trôi nổi, đọc mô tả công việc dài dòng mà chưa chắc đã hợp? 

Workflow n8n này do tác giả **Kevin Meneses** phát triển chính là giải pháp tự động hóa 100% giúp các sếp giải quyết triệt để vấn đề trên. Hệ thống sẽ tự động quét tin tuyển dụng, dùng AI (OpenAI) chấm điểm mức độ phù hợp dựa trên profile cá nhân của các sếp, lưu trữ kết quả và gửi ngay bảng tổng hợp Top 5 công việc xuất sắc nhất vào hòm thư mỗi ngày!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm tối đa thời gian:** Không cần thủ công tìm kiếm và lọc hàng trăm job mỗi tuần.
- **AI chấm điểm chuẩn xác:** Tự động đối chiếu kỹ năng, kinh nghiệm, mức lương, và lĩnh vực thông qua OpenAI.
- **Cá nhân hóa Top 5:** Lọc ra những cơ hội phù hợp nhất và tổng hợp thành một email HTML đẹp mắt gửi thẳng vào Gmail.
- **Hoạt động tự động 24/7:** Chạy theo lịch trình định sẵn (Schedule Trigger) mỗi ngày mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow này chạy mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và dịch vụ sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Sheets:** Nơi lưu trữ thông tin Candidate Profile (hồ sơ cá nhân) và lưu kết quả job matching.
- **Decodo Account:** Dịch vụ Web Scraper hỗ trợ fetch dữ liệu tin tuyển dụng từ RemoteOK (đăng ký qua [Decodo](https://visit.decodo.com/raqXGD)).
- **OpenAI API Key:** Sử dụng model `gpt-4o-mini` để chấm điểm công việc.
- **Gmail Account:** Để gửi email tổng hợp Top 5 việc làm chất lượng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ n8n (Link gốc: [Find high-quality remote jobs](https://n8n.io/workflows/12304)) và import trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các thành phần cốt lõi sau:
- **Load candidate profile (Google Sheets):** Kết nối tài khoản Google Sheets của các sếp, chọn đúng Spreadsheet và Sheet chứa profile cá nhân (kỹ năng, mức lương kỳ vọng, sở thích...).
- **Fetch RemoteOK HTML (Decodo):** Kết nối với tài khoản Decodo để hệ thống lấy dữ liệu thô từ trang tuyển dụng remote.
- **OpenAI Chat Model:** Cấu hình credentials cho OpenAI và đảm bảo model đang chọn là `gpt-4o-mini` để tối ưu chi phí và tốc độ.
- **Check whether the fit score is greater than X (IF Node):** Tùy chỉnh điều kiện điểm số (ví dụ: điểm phù hợp ≥ 90%) để lọc ra các job thực sự chất lượng.
- **Send Top 5 email (Gmail):** Kết nối tài khoản Gmail cá nhân để hệ thống có quyền gửi email báo cáo.
- **Save matches to Google Sheets:** Cấu hình trỏ đến Google Sheet dùng để lưu nhật ký các job đã khớp.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (`Execute Workflow`) một lần để kiểm tra luồng dữ liệu từ việc quét job, AI chấm điểm cho đến gửi email.
- Sau khi test thành công, bật nút **Active** ở góc trên cùng bên phải để hệ thống tự động chạy theo lịch của `Daily trigger (job scan)`.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm thông báo:** Có thể nối thêm node Telegram hoặc Slack sau bước lọc kết quả để nhận thông báo nóng ngay khi có job "ngon" vừa xuất hiện.
- **Mở rộng nguồn dữ liệu:** Không chỉ dừng lại ở RemoteOK, các sếp có thể bổ sung thêm các trang web tuyển dụng khác bằng cách dùng Decodo hoặc các node HTTP Request.
- **Tùy biến Prompt AI:** Trong node `Score fit with AI`, các sếp có thể tinh chỉnh prompt để AI đánh giá khắt khe hơn về văn hóa doanh nghiệp hoặc công nghệ đặc thù mà các sếp muốn hướng tới.

### 📌 Kết luận
Workflow này là một cỗ máy tự động hoàn hảo cho những ai đang tìm kiếm cơ hội làm việc từ xa mà không muốn bỏ lỡ bất kỳ vị trí hấp dẫn nào. Hãy thiết lập ngay hôm nay để để AI làm thay phần việc tìm kiếm nặng nhọc cho các sếp!