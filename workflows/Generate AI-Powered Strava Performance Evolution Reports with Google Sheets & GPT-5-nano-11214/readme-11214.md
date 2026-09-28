---
title: "🚀 Tự động hóa báo cáo hiệu suất tập luyện Strava với AI và Google Sheets"
description: "Xây dựng hệ thống tự động phân tích dữ liệu chạy bộ/đạp xe trên Strava bằng OpenAI, lưu trữ qua Google Sheets và gửi báo cáo chi tiết qua Gmail."
slug: "tu-dong-hoa-bao-cao-hieu-suat-strava-ai-google-sheets"
tags: [n8n, automation, no-code, strava, openai, google-sheets, ai-summarization]
keywords: [n8n workflow, tự động hóa strava, phân tích tập luyện ai, openai n8n, google sheets n8n]
---

# 🚀 Tự động hóa báo cáo hiệu suất tập luyện Strava với AI và Google Sheets

Các sếp là vận động viên, người đam mê chạy bộ hay đạp xe và đang sử dụng Strava? Việc tự tổng hợp thông số quãng đường, tốc độ, nhịp tim và tự đánh giá sự tiến bộ (performance evolution) mỗi tuần/tháng thường tốn rất nhiều thời gian và thiếu góc nhìn chuyên sâu. 

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách kết nối trực tiếp tài khoản **Strava** với **OpenAI** và **Google Sheets**. Hệ thống sẽ tự động lấy dữ liệu hoạt động, nhờ AI phân tích độ cường độ, tiến trình tập luyện, sau đó lưu trữ bài bản và gửi báo cáo trực quan qua **Gmail** hoàn toàn tự động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Báo cáo chuyên sâu từ AI:** Tự động đánh giá cường độ tập luyện, mức độ tiến bộ qua từng buổi tập mà không cần phân tích thủ công.
- **Lưu trữ dữ liệu thông minh:** Toàn bộ lịch sử hoạt động và báo cáo được đồng bộ hóa gọn gàng lên Google Sheets.
- **Thông báo tự động:** Nhận báo cáo định kỳ qua Gmail ngay sau khi có lịch chạy được kích hoạt hoặc theo lịch trình (Schedule).
- **Vận hành 24/7:** Tự động hóa toàn bộ quy trình từ lúc lấy dữ liệu Strava đến khi gửi email báo cáo mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Tài khoản Strava** (Cần thiết lập Strava API Credentials).
- **Tài khoản OpenAI API Key** (Dùng cho các node `Message a model2` và `IA Intensity`).
- **Google Account** (Để kết nối Google Sheets và Gmail).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn hoặc copy trực tiếp mã JSON, sau đó dán vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các thông số sau để workflow chạy mượt mà:
- **Strava Nodes (`Get all activities`, `Get manual activity`):** Kết nối tài khoản Strava thông qua OAuth2 để n8n có quyền truy cập vào dữ liệu hoạt động của các sếp.
- **OpenAI Nodes (`Message a model2`, `IA Intensity`):** Điền OpenAI API Key và chọn model phù hợp (ví dụ: GPT-4o-mini hoặc các model tối ưu chi phí) để AI tiến hành phân tích chỉ số tập luyện.
- **Google Sheets Nodes (`Clear sheet`, `Get row(s) in sheet`, `Append row in sheet`, `Informe de seguimiento`):** Trỏ tới file Google Sheet chuẩn bị sẵn của các sếp, cấu hình đúng Sheet ID và tên cột để lưu trữ dữ liệu hoạt động và báo cáo tiến độ.
- **Gmail Nodes (`Send a message`, `Send a message1`):** Kết nối tài khoản Gmail để hệ thống có quyền gửi email báo cáo trực tiếp đến hộp thư của các sếp.
- **Trigger Nodes (`Schedule Trigger`, `Activity ID`, `When clicking ‘Execute workflow’`):** Lựa chọn cách kích hoạt phù hợp (chạy thủ công bằng nút bấm, theo lịch trình định kỳ hoặc qua Form trigger).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng nút `When clicking ‘Execute workflow’` hoặc `Activity ID` để kiểm tra luồng dữ liệu từ Strava sang OpenAI và Google Sheets.
- Kiểm tra kết quả trên Google Sheets và hộp thư Gmail xem đã nhận được báo cáo chính xác chưa.
- Bật công tắc **Active** để workflow chạy tự động theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot:** Kết hợp thêm node Telegram hoặc Slack để nhận thông báo tổng kết nhanh ngay khi hoàn thành một buổi chạy.
- **Lưu log lỗi:** Sử dụng các node `Stop and Error` để cấu hình gửi tin nhắn cảnh báo nếu tài khoản Strava hết hạn token hoặc lỗi API OpenAI.
- **Báo cáo định kỳ hàng tuần:** Cấu hình `Schedule Trigger` chạy vào Chủ Nhật hàng tuần để tổng hợp toàn bộ hiệu suất tập luyện trong 7 ngày.

### 📌 Kết luận
Workflow này là trợ lý ảo hoàn hảo cho những ai muốn theo dõi sát sao hành trình thể thao của mình bằng sức mạnh của AI. Hãy cài đặt ngay để nâng tầm trải nghiệm tập luyện của các sếp nhé!