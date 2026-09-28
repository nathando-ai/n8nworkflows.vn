---
title: "🚀 Tự động hóa đăng bài X, Facebook và Threads cực hot với Apify, Gemini và Buffer"
description: "Hướng dẫn cài đặt workflow n8n tự động quét xu hướng (trending), tạo nội dung thu hút bằng AI Gemini và tự động lên lịch đăng lên X, Facebook, Threads thông qua Buffer."
slug: "tu-dong-hoa-dang-bai-social-apify-gemini-buffer"
tags: [n8n, automation, social-media, google-gemini, apify, buffer]
keywords: [n8n workflow, tự động đăng bài facebook x threads, apify trending, google gemini ai content, buffer automation]
---

# 🚀 Tự động hóa đăng bài X, Facebook và Threads cực hot với Apify, Gemini và Buffer

Các sếp có đang chật vật mỗi ngày để tìm ý tưởng, viết bài bắt trend (xu hướng) trên các nền tảng mạng xã hội như X (Twitter), Facebook và Threads không? Việc này tốn rất nhiều thời gian, chưa kể việc kiểm tra xem trend đó đã dùng chưa để tránh lặp nội dung.

Đừng lo! Workflow n8n siêu cấp này sẽ giải quyết triệt để nỗi đau đó. Hệ thống sẽ tự động hóa từ A-Z: quét xu hướng thịnh hành, lọc bỏ các trend đã dùng trong 24h qua, dùng AI thông minh (Gemini) để viết bài theo văn phong mong muốn, và tự động đẩy lên các kênh mạng xã hội qua Buffer. Chạy 100% tự động, không cần đụng tay!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ sập, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần ngồi lướt tìm trend hay vắt óc viết content mỗi ngày.
- **Bắt trend thần tốc:** Tự động chạy định kỳ 3 lần/ngày (8:00, 12:30, 16:30) để luôn dẫn đầu xu hướng.
- **Không bao giờ lặp nội dung:** Cơ chế lưu trữ và lọc thông minh giúp loại bỏ hoàn toàn các trend đã dùng trong 24 giờ qua.
- **Đa nền tảng:** Một mũi tên trúng nhiều đích, tự động phân phối nội dung lên X, Facebook và Threads mượt mà.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Apify Account & API Key:** Dùng để cào dữ liệu xu hướng (trending topics).
- **Google Gemini (Google AI) API Key:** Dùng để xử lý dữ liệu và sáng tạo nội dung bài đăng.
- **Buffer Account & Bearer Token:** Quản lý và đăng bài tự động lên các kênh mạng xã hội (X, Facebook, Threads).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này về máy.
- Mở giao diện n8n Editor, chọn **Add workflow** -> **Import from File** và chọn file JSON vừa tải. Hoặc đơn giản là copy toàn bộ mã JSON và dán trực tiếp vào màn hình workflow.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các thành phần sau để hệ thống nhận diện đúng tài khoản:

- **Thiết lập Data Table (Chạy 1 lần duy nhất):** 
  - Tìm node `Create a data table`. Chạy thủ công node này **1 lần duy nhất** để tạo bảng `trend_table` lưu lịch sử trend trong n8n. Sau khi chạy xong, hãy **Disable (tắt)** node này đi để tránh lỗi tạo trùng lặp ở các lần chạy sau.
- **Apify Nodes (`Run an Actor and get dataset1` & `2`):**
  - Kết nối `apifyApi` credential.
  - *Mẹo tùy chỉnh:* Trong cấu hình node Apify, các sếp có thể thay đổi quốc gia (`country`) nếu muốn bắt trend ở thị trường khác ngoài Nigeria (mặc định của tác giả).
- **Google Gemini Nodes (`trend `, `Get Daily x trends1`, v.v.):**
  - Tạo credential **Google PaLM API** bằng Gemini API Key của sếp và gán vào các node AI. Tuyệt đối không paste trực tiếp token vào ô tham số.
- **Buffer MCP Nodes (`facebook post`, `Thread post`, `Post only tweets`):**
  - Tạo credential **Bearer Auth** với Buffer API token của sếp.
  - Thay thế `YOUR_BUFFER_CHANNEL_ID` bằng Channel ID thực tế của từng tài khoản mạng xã hội (lấy từ Dashboard của Buffer tại mục Channel Settings).
- **Tùy chỉnh số lượng bài viết mỗi chu kỳ:**
  - Tại node `Pick Trend`, tìm đoạn code JavaScript `const picked = items.slice(0, 1);`. 
  - Thay số `1` thành số lượng bài viết các sếp muốn tạo mỗi chu kỳ (Ví dụ: muốn tạo 5 bài/lần thì đổi thành `5`).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để test thử một lượt xem dữ liệu chạy qua các node có mượt mà hay không.
- Nếu mọi thứ xanh ngắt (thành công), hãy gạt công tắc sang **Active** ở góc trên cùng bên phải để workflow tự động chạy theo lịch hẹn từ `Schedule Trigger1`.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm một node Telegram ở cuối luồng để nhận tin nhắn báo cáo mỗi khi AI gen xong bài viết hoặc khi có lỗi xảy ra.
- **Kiểm duyệt thủ công trước khi đăng:** Thay vì đẩy thẳng lên Buffer, các sếp có thể đổi node Buffer thành một thông báo kèm nút bấm Duyệt/Từ chối qua Webhook hoặc Notion để kiểm soát chất lượng content trước khi xuất bản.
- **Đa dạng hóa ngôn ngữ:** Tinh chỉnh Prompt trong các node Gemini để tạo bài viết theo văn phong trang trọng, hài hước, hoặc chuyên gia tùy thuộc vào lĩnh vực kinh doanh của doanh nghiệp.

### 📌 Kết luận
Tự động hóa mạng xã hội chưa bao giờ dễ dàng đến thế! Với sự kết hợp hoàn hảo giữa Apify (săn trend), Gemini AI (viết content) và Buffer (lên lịch), các sếp có thể tiết kiệm hàng chục giờ mỗi tuần mà vẫn giữ cho các kênh social luôn sôi động. Cài đặt ngay hôm nay và tối ưu hóa quy trình marketing của doanh nghiệp thôi nào!