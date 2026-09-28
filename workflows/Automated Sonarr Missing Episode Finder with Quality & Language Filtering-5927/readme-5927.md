---
title: "📺 Tự Động Tìm & Tải Tập Phim Thiếu với Sonarr (Lọc Chất Lượng & Ngôn Ngữ)"
description: "Workflow n8n tự động quét Sonarr, tìm các tập phim bị thiếu, kiểm tra chất lượng và ngôn ngữ, sau đó tự động thêm vào hàng đợi tải về mà không cần can thiệp thủ công."
slug: "tu-dong-tim-tai-tap-phim-thieu-sonarr"
tags: [n8n, automation, sonarr, media-server, home-lab]
keywords: [n8n workflow sonarr, tự động hóa phim, tìm tập phim thiếu, sonarr api, media automation]
---

# 📺 Tự Động Tìm & Tải Tập Phim Thiếu với Sonarr (Lọc Chất Lượng & Ngôn Ngữ)

Các sếp có bao giờ gặp tình trạng này chưa? Bạn đã cài đặt Sonarr và thêm một bộ phim vào danh sách, nhưng vì lý do nào đó (server chậm, lỗi mạng, hoặc đơn giản là bạn quên), một vài tập phim quan trọng lại bị "lọt" và không được tải về. Việc phải mở Sonarr, tìm từng tập, kiểm tra xem tập đó có sẵn trên các indexers không, rồi mới bấm nút "Search" là một quy trình thủ công, tốn thời gian và dễ gây nhầm lẫn.

Workflow **Automated Sonarr Missing Episode Finder** này chính là giải pháp "chữa cháy" hoàn hảo. Nó hoạt động như một người quản lý thư viện phim tự động: định kỳ quét toàn bộ danh sách phim trong Sonarr, phát hiện các tập bị thiếu, đối chiếu với các nguồn tìm kiếm (indexers) để đảm bảo tập phim đó có sẵn với đúng chất lượng và ngôn ngữ mong muốn, và cuối cùng tự động thêm vào hàng đợi tải về. Các sếp chỉ cần ngồi xem phim, mọi thứ còn lại để workflow lo!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và đảm bảo độ trễ thấp khi gọi API Sonarr, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần mở giao diện Sonarr để kiểm tra thủ công. Workflow tự chạy theo lịch (ví dụ: mỗi 1 giờ hoặc mỗi ngày).
- **Đảm bảo chất lượng & ngôn ngữ:** Workflow không tải bừa. Nó kiểm tra kỹ lưỡng xem tập phim có khớp với cài đặt chất lượng (ví dụ: 1080p, 2160p) và ngôn ngữ (ví dụ: Tiếng Việt, Tiếng Anh) mà các sếp đã cấu hình trong Sonarr không.
- **Tiết kiệm băng thông & thời gian:** Chỉ tải những tập thực sự bị thiếu và khả dụng, tránh việc tải lại các tập đã có hoặc tải các tập không phù hợp.
- **Hoạt động liên tục:** Với Schedule Trigger, workflow sẽ tự động "chữa lành" thư viện phim của các sếp mọi lúc mọi nơi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Server Sonarr:** Đã được cài đặt và chạy ổn định (có thể là Docker container).
2. **Sonarr API Key:** Lấy từ *Settings > General > API Keys* trong Sonarr.
3. **Cấu hình Indexers:** Sonarr của các sếp cần đã được cấu hình các indexers (như Prowlarr, Jackett, hoặc các tracker riêng) để workflow có thể truy vấn tìm kiếm.
4. **Cài đặt n8n:** Một instance n8n đang chạy (có thể là local hoặc VPS).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from File** hoặc dán trực tiếp JSON của workflow vào editor.
3. Sau khi import, các sếp sẽ thấy 10 nodes được kết nối theo luồng logic: từ Schedule Trigger đến các bước kiểm tra và HTTP Request.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần cấu hình chi tiết các node sau:

*   **Node: `Schedule Trigger`**
    *   Mặc định workflow có thể chạy theo chu kỳ nhất định. Các sếp nên chỉnh tần suất phù hợp (ví dụ: mỗi 1 giờ, mỗi 6 giờ, hoặc hàng ngày) để cân bằng giữa việc cập nhật nhanh và tải trọng API.

*   **Node: `Check for Missing Episodes` (HTTP Request)**
    *   **Method:** GET
    *   **URL:** `[Sonarr Base URL]/api/v3/episode/missing`
    *   **Headers:** Thêm header `X-Api-Key` với giá trị là **API Key** của Sonarr.
    *   *Lưu ý:* Đảm bảo URL base chính xác (ví dụ: `http://localhost:8989` hoặc IP của server Sonarr).

*   **Node: `Filter Series` (Code Node)**
    *   Node này dùng JavaScript để lọc dữ liệu. Các sếp có thể chỉnh sửa logic ở đây nếu muốn loại trừ một số series cụ thể hoặc chỉ tập trung vào các series đang "Wanted" (đang muốn tải).
    *   Kiểm tra biến `items` để đảm bảo nó xử lý đúng cấu trúc trả về từ API Sonarr.

*   **Node: `Interactive search for all episodes in this season` (HTTP Request)**
    *   **Method:** POST
    *   **URL:** `[Sonarr Base URL]/api/v3/command`
    *   **Body:** Cần cấu hình JSON body để gửi lệnh tìm kiếm tương tác (interactive search) cho từng series/season.
    *   **Headers:** Thêm `X-Api-Key`.

*   **Node: `Validate Quality and Language Match` (IF Node)**
    *   Đây là "bộ lọc" thông minh. Node này so sánh kết quả tìm kiếm với các tiêu chí:
        *   **Quality Profile:** Tập phim có đạt chuẩn chất lượng không?
        *   **Language:** Tập phim có đúng ngôn ngữ mong muốn không?
    *   Các sếp cần đảm bảo các điều kiện trong node IF này khớp với logic mà các sếp muốn (ví dụ: chỉ tải nếu `qualityProfileId` khớp và `language` là "Vietnamese" hoặc "English").

*   **Node: `Override and add to download queue` (HTTP Request)**
    *   **Method:** POST
    *   **URL:** `[Sonarr Base URL]/api/v3/command`
    *   **Body:** Gửi lệnh để thêm tập phim vào hàng đợi tải về (download queue).
    *   **Headers:** Thêm `X-Api-Key`.
    *   *Lưu ý:* Đây là bước thực thi cuối cùng. Chỉ những tập phim vượt qua bước Validate mới được gửi đến node này.

*   **Node: `Loop Over Items` (Split In Batches)**
    *   Node này giúp xử lý từng item (tập phim) một cách tuần tự, tránh quá tải API Sonarr nếu có quá nhiều tập bị thiếu cùng lúc. Các sếp có thể chỉnh `Batch Size` nếu cần.

#### 3. Kích hoạt ⚡️
1. **Test Run:** Bấm nút **Execute Workflow** để chạy thử.
2. Kiểm tra kết quả:
    *   Mở Sonarr, vào mục **Activity** hoặc **Wanted** để xem có tập phim nào được thêm vào hàng đợi tải về không.
    *   Kiểm tra log trong n8n để xem có lỗi API nào không (ví dụ: 401 Unauthorized nếu sai API Key).
3. **Bật Active:** Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy theo lịch.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node **Telegram** hoặc **Slack** sau bước `Override and add to download queue` để gửi thông báo cho các sếp khi có tập phim mới được thêm vào hàng đợi tải về.
- **Log chi tiết:** Thêm node **Google Sheets** hoặc **Database** để lưu lịch sử các tập phim đã được tìm thấy và tải về, giúp các sếp dễ dàng theo dõi và debug.
- **Lọc theo Genre:** Chỉnh sửa node `Filter Series` để chỉ tự động tìm và tải các tập phim thuộc thể loại mà các sếp yêu thích (ví dụ: chỉ tải phim Hành động, Phiêu lưu).
- **Tối ưu hóa lịch chạy:** Nếu các sếp có nhiều series, hãy cân nhắc chạy workflow vào giờ thấp điểm (ví dụ: 2 giờ sáng) để tránh ảnh hưởng đến hiệu suất server khi đang xem phim.

### 📌 Kết luận
Workflow **Automated Sonarr Missing Episode Finder** là một công cụ không thể thiếu cho những ai muốn xây dựng một hệ thống media server tự động và hiệu quả. Với khả năng tự động phát hiện, kiểm tra và tải về các tập phim bị thiếu, workflow này giúp các sếp tiết kiệm hàng giờ mỗi tuần và đảm bảo thư viện phim luôn đầy đủ, chất lượng cao. Hãy import và cấu hình ngay hôm nay để trải nghiệm sự tiện lợi mà nó mang lại!