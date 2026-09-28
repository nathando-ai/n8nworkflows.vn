---
title: "🚀 Tạo nhạc AI tự động với Suno V3.5, KIE.ai API và giao diện Form trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa hoàn toàn quy trình tạo nhạc AI chất lượng cao sử dụng mô hình Suno V3.5 và KIE.ai API thông qua Web Form."
slug: "tao-nhac-ai-tu-dong-suno-v35-kie-ai-n8n"
tags: [n8n, automation, ai-music, suno-ai, kie-ai, no-code]
keywords: [n8n workflow, tạo nhạc ai, suno v3.5 api, kie.ai, tự động hóa no-code]
---

# 🚀 Tạo nhạc AI tự động với Suno V3.5, KIE.ai API và giao diện Form trong n8n

Các sếp là nhạc sĩ, nhà sáng tạo nội dung (Content Creator) hay lập trình viên đang tìm cách tự động hóa việc sáng tác âm nhạc theo ý muốn? Việc phải thao tác thủ công trên các nền tảng tạo nhạc AI, chờ đợi và tải file về tốn rất nhiều thời gian và ngắt quãng mạch sáng tạo. 

Giải pháp là đây! Workflow n8n này cung cấp một giao diện Web Form thân thiện để các sếp nhập mô tả (prompt), thể loại và tiêu đề. Hệ thống sẽ tự động gửi yêu cầu đến **KIE.ai API (mô hình Suno V3.5)**, liên tục theo dõi trạng thái xử lý theo thời gian thực và trả về kết quả file nhạc hoàn chỉnh ngay trên trình duyệt mà không cần động tay viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Từ khâu nhập thông tin qua form đến khi nhận file nhạc hoàn chỉnh.
- **Tiết kiệm thời gian:** Không cần truy cập thủ công vào web tạo nhạc, hệ thống tự động poll (kiểm tra) trạng thái mỗi 10 giây cho đến khi xong.
- **Giao diện trực quan:** Cung cấp Web Form sẵn có để bất kỳ ai trong team cũng có thể tự tạo nhạc theo ý muốn.
- **Chất lượng cao:** Sử dụng mô hình Suno V3.5 mạnh mẽ thông qua KIE.ai API với khả năng kiểm soát chi tiết về phong cách, tiêu đề và lời bài hát.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động (Self-hosted hoặc Cloud).
- Tài khoản và API Key tại [KIE.ai](https://kie.ai/).
- Sự am hiểu cơ bản về cách viết Prompt cho nhạc AI (mô tả tâm trạng, nhạc cụ, nhịp điệu...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Sao chép đoạn mã JSON của workflow này.
- Mở n8n Editor, chọn **Add workflow** -> **Import from JSON** và dán mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 6 nodes chính hoạt động nhịp nhàng với nhau:
- **Submit Music Generation Parameters (`formTrigger`):** Tạo giao diện Web Form cho phép người dùng nhập các trường:
  - `prompt`: Mô tả nội dung/lời bài hát (tối đa 3000 ký tự). Ví dụ: *"A calm and relaxing piano track with soft melodies"*.
  - `style`: Thể loại nhạc (ví dụ: *Classical, Jazz, Pop, Electronic, Rock* - tối đa 200 ký tự).
  - `title`: Tiêu đề bài hát (tối đa 80 ký tự).
  - `api_key`: Khóa API lấy từ tài khoản KIE.ai của sếp.
- **Send Music Generation Request to KIE.ai API (`httpRequest`):** Node này nhận dữ liệu từ Form và thực hiện gọi API POST đến KIE.ai để khởi tạo tiến trình tạo nhạc với Suno V3.5. Cần đảm bảo truyền đúng biến `api_key` vào header xác thực.
- **Wait for Music Processing (`wait`):** Tạm dừng luồng xử lý trong giây lát trước khi tiến hành kiểm tra trạng thái.
- **Poll Music Generation Status (`httpRequest`):** Gửi yêu cầu GET liên tục để kiểm tra tiến độ tạo nhạc của hệ thống AI.
- **Check if Music Generation Complete (`if`):** Kiểm tra xem quá trình tạo nhạc đã hoàn tất hay chưa. Nếu chưa, vòng lặp sẽ quay lại bước chờ; nếu rồi, chuyển sang bước tiếp theo.
- **Format and Display Music Results (`set`):** Xử lý dữ liệu đầu ra, định dạng lại kết quả để hiển thị link nghe nhạc trực tiếp hoặc tải file trên giao diện hoàn tất.

#### 3. Kích hoạt ⚡️
- Click nút **"Execute Workflow"** để chạy thử nghiệm form.
- Truy cập vào URL Form được cung cấp, điền thông tin và bấm Submit.
- Theo dõi log n8n để thấy quá trình hệ thống tự động gọi API và chờ kết quả.
- Khi mọi thứ hoạt động trơn tru, hãy bật công tắc **Active** góc trên bên phải để đưa workflow vào trạng thái vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Mở rộng workflow bằng cách kết nối thêm node Telegram hoặc Slack để gửi bản nhạc hoàn thành thẳng vào nhóm chat của team.
- **Lưu trữ tự động:** Thêm node Google Sheets hoặc Airtable để lưu lại lịch sử các prompt, thể loại và link nhạc đã tạo phục vụ cho việc quản lý nội dung.
- **Mẹo viết Prompt:** Kết hợp mô tả cảm xúc, nhịp điệu, nhạc cụ cụ thể để Suno V3.5 trả về kết quả ấn tượng nhất (Ví dụ: *"A peaceful piano meditation track with gentle waves in the background"*).

### 📌 Kết luận
Với workflow n8n tích hợp KIE.ai và Suno V3.5 này, các sếp đã sở hữu ngay một "phòng thu AI" tự động hóa thu nhỏ. Hãy import ngay vào hệ thống của mình và bắt đầu sáng tạo những giai điệu độc bản ngay hôm nay!