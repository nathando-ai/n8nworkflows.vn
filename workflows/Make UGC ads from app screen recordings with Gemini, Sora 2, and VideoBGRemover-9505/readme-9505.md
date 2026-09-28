---
title: "🚀 Tự động hóa tạo video quảng cáo UGC từ màn hình ứng dụng với Gemini, Sora 2 và VideoBGRemover"
description: "Biến video quay màn hình app thành video quảng cáo UGC chuyên nghiệp hoàn toàn tự động bằng AI, tích hợp Gemini phân tích, Sora 2 tạo diễn viên và VideoBGRemover ghép nền."
slug: "tao-ugc-ads-tu-man-hinh-app-gemini-sora2-videobgremover"
tags: [n8n, automation, ai-video, gemini, sora2, google-drive]
keywords: [n8n workflow, tạo UGC ads tự động, Gemini AI video, Sora 2 fal ai, VideoBGRemover]
---

# 🚀 Tự động hóa tạo video quảng cáo UGC từ màn hình ứng dụng với Gemini, Sora 2 và VideoBGRemover

Các sếp đang tốn bao nhiêu thời gian và tiền bạc để thuê diễn viên, quay dựng video quảng cáo UGC (User Generated Content) cho ứng dụng di động hay sản phẩm SaaS của mình? Việc sản xuất thủ công vừa tốn kém, mất thời gian, lại khó scale số lượng lớn.

Với workflow n8n cực đỉnh này, các sếp có thể **tự động hóa 100% quy trình tạo video quảng cáo UGC** chỉ bằng một đường dẫn (URL) video quay màn hình app. Hệ thống sẽ tự động dùng **Gemini AI** để phân tích và lên kịch bản, **Sora 2 (qua fal.ai)** để tạo video diễn viên AI, và **VideoBGRemover** để xóa phông, ghép diễn viên chồng lên video màn hình app, cuối cùng lưu trực tiếp kết quả vào **Google Drive**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 (vì quá trình render video mất khoảng 5-8 phút), các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Biến video quay màn hình thô thành video quảng cáo UGC hoàn chỉnh chỉ trong 5-8 phút mà không cần đụng tay vào dựng phim.
- **Kịch bản thông minh:** Gemini tự động phân tích tính năng app, sinh ra cấu trúc chuẩn quảng cáo (Hook, Problem, Solution, CTA).
- **Diễn viên AI chân thực:** Sử dụng Sora 2 tạo biểu cảm, cử chỉ tay tự nhiên như người thật.
- **Đồng bộ đa kênh:** Kết quả tự động lưu lên Google Drive và có thể trigger qua Webhook từ hệ thống khác.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ API KEYS & TÀI KHOẢN]
Các sếp cần chuẩn bị sẵn các API Key sau và lưu vào n8n Settings → Variables:
1. **Gemini API Key**: Lấy tại [Google AI Studio](https://aistudio.google.com/apikey) -> Đặt biến: `GEMINI_KEY`
2. **FAL AI Key (cho Sora 2)**: Lấy tại [fal.ai dashboard](https://fal.ai/dashboard/keys) -> Đặt biến: `FAL_KEY`
3. **VideoBGRemover API Key**: Lấy tại [videobgremover.com](https://videobgremover.com/api-management) -> Đặt biến: `VIDEOBGREMOVER_KEY`
4. **Google Drive**: Kết nối tài khoản trực tiếp trên node `Upload to Google Drive`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ JSON từ nguồn.
- Mở n8n Editor, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp vào giao diện.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 28 nodes được chia thành các khu vực rõ ràng:
- **Webhook Trigger & Manual Trigger**: Cho phép test thủ công qua node `Sample Input (Edit Here)` hoặc nhận request tự động từ hệ thống bên ngoài qua Webhook endpoint `ugc-screenshot-video`.
- **Gemini – Analyze & Plan**: Node thực hiện gọi API Gemini để phân tích video màn hình app và trả về cấu trúc kịch bản (Hook, Problem, Solution, CTA, visual details...).
- **Sora 2 – Submit (fal.ai)** & các node check status: Gửi prompt đã build sang fal.ai để render video diễn viên AI, sử dụng cơ chế vòng lặp `Wait 20s` và `Sora Completed?` để đợi render xong.
- **VBR – Create Job** & **VBR – Start Composition**: Xóa phông nền diễn viên, ghép đè (composition) lên góc phải màn hình của video app, đồng thời trộn âm thanh (30% background + 100% foreground).
- **Upload to Google Drive**: Cần click vào node này, chọn tài khoản Google Drive của các sếp để cấp quyền lưu file MP4 xuất ra.

#### 3. Kích hoạt ⚡️
- Chạy thử thủ công bằng cách điền thông tin vào node `Sample Input (Edit Here)` với URL video màn hình 9:16 (độ dài khuyến nghị 4-12 giây).
- Kiểm tra kết quả trong Google Drive sau 5-8 phút.
- Bật công tắc **Active** để chính thức đưa workflow vào vận hành tự động qua Webhook.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Notification:** Thêm node Telegram hoặc Slack ở cuối workflow để bắn thông báo kèm link Google Drive ngay khi video render xong cho team Marketing.
- **Lưu Database:** Lưu thông tin metadata và link video vào Google Sheets hoặc Airtable để quản lý chiến dịch quảng cáo.
- **Tối ưu video input:** Nên sử dụng video màn hình có tỉ lệ 9:16 (dọc), thời gian ngắn gọn từ 4 đến 12 giây để Sora 2 xử lý mượt mà và chính xác nhất.

### 📌 Kết luận
Workflow này là "vũ khí bí mật" giúp các nhà phát triển ứng dụng, đội ngũ marketing và các Digital agency sản xuất hàng loạt video UGC quảng cáo chạy Ads vô cùng chuyên nghiệp và tiết kiệm chi phí. Áp dụng ngay để tối ưu hóa hiệu suất marketing của các sếp!