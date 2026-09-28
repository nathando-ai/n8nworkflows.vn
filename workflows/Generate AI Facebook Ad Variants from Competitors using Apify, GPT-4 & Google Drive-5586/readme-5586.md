---
title: "🚀 Tự động tạo biến thể Quảng cáo Facebook từ đối thủ bằng Apify, GPT-4 & Google Drive"
description: "Khám phá cách tự động hóa quy trình nghiên cứu quảng cáo đối thủ qua Apify, phân tích và viết nội dung, tạo hình ảnh bằng AI và lưu trữ tự động trên Google Drive."
slug: "tao-bien-the-quang-cao-facebook-ai-apify-gpt4"
tags: [n8n, automation, no-code, facebook-ads, openai, apify, ai-content]
keywords: [n8n workflow, tao quang cao facebook ai, apify facebook ads scraper, gpt-4 quang cao, tu dong hoa marketing]
---

# 🚀 Tự động tạo biến thể Quảng cáo Facebook từ đối thủ bằng Apify, GPT-4 & Google Drive

Các sếp có bao giờ mất hàng giờ để "soi" quảng cáo của đối thủ trên Facebook Ad Library, sau đó vắt óc nghĩ ý tưởng viết bài và thiết kế banner mới không? Công việc này không chỉ tốn thời gian mà còn dễ kiệt quệ ý tưởng sáng tạo. 

Đừng lo, bài toán này sẽ được giải quyết 100% tự động với workflow n8n cực đỉnh từ tác giả Electrabot. Workflow này sẽ thay các sếp cào dữ liệu quảng cáo đối thủ, phân tích bằng GPT-4, tạo các biến thể nội dung & hình ảnh mới, rồi gom tất cả vào Google Drive và Google Sheets một cách ngăn nắp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian nghiên cứu:** Tự động thu thập quảng cáo từ Facebook Ad Library thông qua Apify mà không cần làm thủ công.
- **Sáng tạo vô tận với AI:** Sử dụng sức mạnh của OpenAI GPT-4 để phân tích và "spin" ra các biến thể nội dung quảng cáo độc đáo, thu hút hơn bản gốc.
- **Tự động hóa hình ảnh:** Tải asset gốc và tự động tạo hình ảnh/biến thể trực quan phục vụ cho chiến dịch.
- **Quản lý khoa học:** Tự động tạo thư mục trên Google Drive và lưu trữ toàn bộ dữ liệu, hình ảnh, cùng bảng theo dõi chi tiết trên Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Apify Account:** Tài khoản và API Token để chạy Actor quét Facebook Ad Library (`Run Ad Library Scraper`).
- **OpenAI API Key:** Tài khoản OpenAI để sử dụng các node `OpenAI` và `Spin Prompts` (GPT-4).
- **Google Account:** Kết nối Google Drive (để lưu trữ folder và asset) và Google Sheets (để lưu data quản lý).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy mã JSON của workflow này, vào giao diện n8n Editor, chọn **New Workflow**, nhấn tổ hợp phím `Ctrl + V` (hoặc `Cmd + V`) để dán toàn bộ các node vào bảng làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 26 nodes, các sếp cần tập trung cấu hình kỹ các điểm sau:
- **Run Ad Library Scraper (HTTP Request):** Cấu hình API endpoint của Apify và điền Apify API Token của các sếp vào header, cùng với từ khóa hoặc trang Facebook cần quét.
- **OpenAI & Spin Prompts (OpenAI nodes):** Chọn credentials OpenAI hợp lệ. Tinh chỉnh lại System Prompt nếu muốn văn phong phù hợp hơn với tệp khách hàng của sản phẩm.
- **Google Drive (Create Asset Parent Folder, Create Child Source Folder, Create Child Spun Folder...):** Chọn tài khoản Google Drive, trỏ đúng thư mục gốc (Parent Folder) nơi các sếp muốn hệ thống tự động tạo cấu trúc cây thư mục chứa ảnh và tài nguyên quảng cáo.
- **Google Sheets, Google Sheets1, Google Sheets2:** Kết nối tài khoản Google Sheets và chuẩn bị sẵn một file Google Sheets với các cột tương ứng để lưu thông tin chi tiết về các biến thể quảng cáo được sinh ra.

#### 3. Kích hoạt ⚡️
- Nhấn nút **When clicking ‘Execute workflow’** (hoặc node `manualTrigger`) để test chạy thử với dữ liệu mẫu xem hệ thống có tạo file, gọi OpenAI và đẩy dữ liệu lên Google Drive/Sheets thành công hay không.
- Sau khi test ngon lành, gạt công tắc sang **Active** để workflow sẵn sàng hoạt động tự động bất cứ lúc nào.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối thông báo:** Thêm node Telegram hoặc Slack ở cuối luồng để nhận thông báo ngay khi AI hoàn thành việc tạo một bộ biến thể quảng cáo mới.
- **Mở rộng nguồn dữ liệu:** Kết hợp thêm các công cụ cào dữ liệu TikTok Ad Library hoặc LinkedIn Ad Library để đa dạng hóa ý tưởng đa nền tảng.
- **Báo cáo định kỳ:** Thiết lập Cron trigger chạy hàng tuần để tự động tổng hợp các xu hướng quảng cáo mới nhất từ đối thủ vào một file báo cáo chung.

### 📌 Kết luận
Việc tối ưu hóa quy trình sáng tạo nội dung quảng cáo chưa bao giờ dễ dàng đến thế khi kết hợp sức mạnh của n8n, Apify và OpenAI. Hãy áp dụng ngay workflow này để vượt mặt đối thủ về tốc độ ra mắt các chiến dịch marketing chất lượng cao nhé các sếp!