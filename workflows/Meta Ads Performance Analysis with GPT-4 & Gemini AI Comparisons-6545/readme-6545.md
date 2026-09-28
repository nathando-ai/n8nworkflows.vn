---
title: "🚀 Tự động phân tích hiệu suất Meta Ads với GPT-4 & Gemini AI trong n8n"
description: "Hướng dẫn xây dựng hệ thống tự động trích xuất dữ liệu quảng cáo Facebook, so sánh chuẩn benchmark và nhờ AI (OpenAI & Google Gemini) phân tích, đưa ra lời khuyên tối ưu."
slug: "tu-dong-phan-tich-hieu-suat-meta-ads-gpt-4-gemini-ai"
tags: [n8n, automation, meta-ads, openai, google-gemini, ai-marketing]
keywords: [n8n workflow, phân tích meta ads bằng ai, openai vs gemini ads analysis, tự động hóa marketing, facebook ads automation]
---

# 🚀 Tự động phân tích hiệu suất Meta Ads với GPT-4 & Gemini AI

Các sếp chạy quảng cáo Facebook chắc chắn hiểu cảm giác "đau đầu" khi mỗi ngày phải ngồi soi hàng đống chỉ số (CTR, CPC, ROAS...), so sánh với số liệu cũ và tự hỏi: *Nên scale, nên tối ưu hay nên tắt ad này?* Việc này vừa tốn thời gian, vừa dễ bỏ sót insight.

Đừng lo nữa các sếp! Bài viết này sẽ hướng dẫn chi tiết cách vận hành một workflow n8n cực kỳ mạnh mẽ do **Kirill Khatkevich** thiết kế. Workflow này sẽ tự động hóa 100% quy trình lấy dữ liệu từ **Meta Ads**, kết hợp với sức mạnh của **OpenAI (GPT-4)** và **Google Gemini** để chấm điểm, phân tích và đưa ra đề xuất hành động (*Scale, Optimize, Stop*) cho từng creative.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Desktup VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **So sánh song song AI:** Chạy đồng thời phân tích từ cả OpenAI và Google Gemini giúp các sếp đối chiếu kết quả, tìm ra góc nhìn tối ưu nhất từ AI.
- **Tiết kiệm 90% thời gian:** Tự động hóa hoàn toàn từ bước lấy data, xử lý chỉ số đến ghi kết quả vào Google Sheets.
- **Đề xuất hành động rõ ràng:** AI đóng vai trò như một Media Buyer chuyên nghiệp, tự động đưa ra các quyết định: *Scale (tăng ngân sách), Optimize (tối ưu), Stop (tắt).*
- **Lưu trữ minh bạch:** Dữ liệu thô và kết quả phân tích được lưu trực tiếp vào Google Sheets, đảm bảo không bị mất mát ngay cả khi AI gặp lỗi mạng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và credentials sau trong n8n:
- **Meta Ads (Facebook Graph API) Credentials:** Để lấy thông tin Campaign, Ads và Insights.
- **OpenAI API Key:** Cho node xử lý GPT-4 / Nano.
- **Google Palm API / Gemini Credentials:** Cho Google Gemini Chat Model.
- **Google Sheets OAuth2 API Credentials:** Để đọc/ghi dữ liệu vào bảng tính Google Sheets.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ n8n.io (Link gốc: [Meta Ads Performance Analysis](https://n8n.io/workflows/6545)), sau đó dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần chú ý cấu hình các node cốt lõi sau:

- **Node `Set parameters` (Main Configuration):** 
  Đây là trung tâm điều khiển của workflow:
  - Chọn `source`: Điền `"Meta"` nếu muốn quét toàn bộ campaign (cần cung cấp thêm `campaign_id`), hoặc điền `"sheets"` nếu muốn lấy danh sách `AdID` từ Google Sheets (dùng kèm node `Get Ads from Sheet`).
  - Thêm dữ liệu chuẩn `benchmarks_data`: Dán dữ liệu các mẫu quảng cáo chạy hiệu quả nhất của các sếp (định dạng CSV xuất từ Ads Manager) vào đây để AI có cơ sở so sánh.
- **Node `Set Metrics`:** Nơi bóc tách các chỉ số từ Meta API (Spend, Impressions, Clicks, Actions...). Các sếp có thể cấu hình thêm các custom conversions hoặc chỉ số riêng của doanh nghiệp tại đây.
- **Node `Send data to 4.1-NANO` & `Send data to Gemini`:** Cấu hình prompt cho AI. Đừng ngần ngại thử nghiệm các prompt khác nhau để AI hiểu đúng ngữ cảnh và KPI kinh doanh của các sếp!
- **Các node Google Sheets (`Ad metrics`, `Ad data from Gemini`, `Ad data from OpenAI`, `Get Ads from Sheet`):** Trỏ đến các file Google Sheets thực tế của các sếp để ghi log chỉ số thô và kết quả phân tích từ AI.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Test step / Test workflow**) để kiểm tra luồng dữ liệu từ Meta sang Google Sheets và AI.
- Sau khi test thành công, bật công tắc **Active** để workflow chạy tự động theo lịch của `Schedule Trigger`.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp cảnh báo:** Thêm node **Telegram** hoặc **Slack** vào cuối workflow để bắn tin nhắn thông báo ngay khi AI đề xuất "Stop" hoặc "Scale" một chiến dịch lớn.
- **Lưu lịch sử dài hạn:** Thiết lập Google Sheets lưu trữ theo từng tháng để có dữ liệu huấn luyện benchmark cho các chiến dịch sau.
- **Tinh chỉnh Prompt:** Chất lượng phân tích phụ thuộc 80% vào prompt. Hãy bổ sung thêm mô tả về biên lợi nhuận, AOV (giá trị đơn trung bình) vào prompt của AI để nhận về lời khuyên sát thực tế nhất.

### 📌 Kết luận
Việc tối ưu quảng cáo Meta Ads không còn là cuộc chiến dò dẫm trong đêm nhờ có sự trợ giúp của AI. Hãy cài đặt ngay workflow này lên hệ thống n8n của các sếp để tự động hóa toàn bộ quy trình phân tích và nâng cao hiệu suất chiến dịch ngay hôm nay!