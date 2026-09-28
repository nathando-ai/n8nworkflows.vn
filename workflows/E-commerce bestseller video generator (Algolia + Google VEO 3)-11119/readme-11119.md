---
title: "🚀 Tự Động Hóa Tạo Video Sản Phẩm Bán Chạy Nhất E-commerce với Algolia & Google VEO 3"
description: "Hướng dẫn chi tiết workflow n8n tự động quét sản phẩm bán chạy hàng tuần từ Algolia, kiểm tra hình ảnh và dùng AI Google VEO 3 tạo video quảng cáo Cinematic lưu trữ vào Supabase."
slug: "tu-dong-hoa-tao-video-san-pham-algolia-google-veo-3"
tags: [n8n, automation, e-commerce, ai-video, google-veo, algolia]
keywords: [n8n workflow, tạo video sản phẩm tự động, algolia automation, google veo 3, e-commerce video generator]
---

# 🚀 Tự Động Hóa Tạo Video Sản Phẩm Bán Chạy Nhất E-commerce với Algolia & Google VEO 3

Các sếp làm e-commerce chắc chắn hiểu cảm giác đau đầu khi mỗi tuần phải tốn hàng giờ đồng hồ để tìm ra sản phẩm bán chạy nhất, sau đó loay hoay dựng video quảng cáo, upload lên web. Công việc thủ công này vừa nhàm chán, tốn nhân sự lại vừa chậm trễ xu hướng thị trường.

Đừng lo, bài toán này sẽ được giải quyết triệt để 100% tự động với workflow n8n cực đỉnh này do **Emir Belkahia** xây dựng. Hệ thống sẽ tự động quét sản phẩm "hot" nhất qua **Algolia**, kiểm tra hình ảnh, kích hoạt AI **Google VEO 3.0** để "phù phép" bức ảnh tĩnh thành video quảng cáo cinematic chuyên nghiệp, lưu trữ tại Supabase và cập nhật ngược lại vào kho hàng Algolia mà không cần sự can thiệp thủ công của con người!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các file media nặng, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn 100%**: Chạy định kỳ mỗi thứ Hai hàng tuần hoặc kích hoạt thủ công khi cần.
- **Bắt trend kịp thời**: Tự động nhận diện sản phẩm best-seller dựa trên dữ liệu thật từ Algolia custom ranking.
- **Sản xuất video AI chuyên nghiệp**: Biến ảnh tĩnh sản phẩm thành video quảng cáo sinh động bằng Google VEO 3.0 mà không tốn chi phí dựng phim.
- **Xử lý lỗi thông minh**: Tự động gửi email cảnh báo qua Gmail nếu sản phẩm không có ảnh hoặc link ảnh bị hỏng (broken image).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và dịch vụ sau:
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Algolia Account**: Có index sản phẩm và cấu hình custom ranking (dựa trên `inStock` và `popularity`).
- **Google Cloud / Vertex AI**: Đã cấp quyền truy cập Google VEO 3.0 API và Google Cloud Storage bucket (bắt buộc vì file video base64 từ VEO quá lớn đối với n8n trực tiếp).
- **Supabase Account**: Tạo sẵn storage bucket để lưu trữ file MP4 đầu ra (giúp tối ưu chi phí và dễ tích hợp frontend).
- **Gmail Account**: Để nhận email thông báo khi có lỗi phát sinh về hình ảnh sản phẩm.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cấp.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc copy toàn bộ JSON và paste trực tiếp vào màn hình workflow).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần chú ý cấu hình kỹ lưỡng các node trọng điểm sau:
- **Every week on monday morning** & **Test Trigger**: Dùng để cấu hình thời gian chạy định kỳ (mặc định thứ Hai hàng tuần) hoặc test nhanh thủ công bằng nút `Test Trigger while building the workflow`.
- **Get weekly bestseller from Algolia**: Điền thông tin kết nối `httpBearerAuth` hoặc `httpCustomAuth` kèm App ID, API Key và Index Name của Algolia.
- **Check image availability** & **Image URL is present**: Đảm bảo URL hình ảnh sản phẩm trả về status code 200 hợp lệ. Nếu lỗi, luồng sẽ rẽ nhánh sang node **Gmail** (`Tell admin that bestseller has no image` / `Tell admin that bestseller has broken image`) để báo cáo cho đội ngũ vận hành.
- **Convert image to base64 for VEO 3**: Sử dụng node `extractFromFile` để chuyển đổi hình ảnh sản phẩm sang định dạng chuẩn trước khi đẩy vào AI.
- **Generate video with Google VEO 3**: Cấu hình các API credentials của Google Vertex AI / Palm / OAuth2 để gọi model VEO 3.0 tạo video.
- **Downloading the MP4 file** & **Drop video in Supabase Bucket**: Kết nối Google Cloud Storage để lấy file video gốc do VEO xuất ra, sau đó upload file MP4 này lên Supabase Bucket thông qua `supabaseApi`.
- **Index in Algolia**: Cập nhật lại bản ghi sản phẩm trên Algolia với URL video mới để tự động hiển thị video lên trang thương mại điện tử của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** bằng `Test Trigger while building the workflow` để chạy thử nghiệm xem toàn bộ chuỗi xử lý (gọi Algolia -> tạo video qua VEO -> lưu Supabase) có mượt mà không.
- Sau khi test thành công, bật nút **Active** ở góc trên bên phải để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo nội bộ**: Thay vì chỉ nhận email khi sản phẩm lỗi hoặc hoàn thành, các sếp có thể gắn thêm node Telegram hoặc Slack để team Marketing nhận thông báo ngay lập tức trên điện thoại.
- **Lưu trữ Log chiến dịch**: Tạo thêm một bước ghi log vào Google Sheets hoặc Airtable để thống kê xem tuần qua hệ thống đã tạo video cho những sản phẩm nào, giúp dễ dàng theo dõi hiệu quả chạy quảng cáo.
- **Mở rộng định dạng**: Có thể tinh chỉnh prompt trong node gọi Google VEO 3 để tạo ra nhiều phong cách video khác nhau (cinematic, 3D render, phong cách tối giản...) phù hợp với từng ngành hàng.

### 📌 Kết luận
Workflow "E-commerce bestseller video generator" là một giải pháp tự động hóa đỉnh cao, giúp tối ưu hóa toàn bộ quy trình sản xuất nội dung video marketing từ kho dữ liệu thực tế. Hãy triển khai ngay hôm nay để tự động hóa cửa hàng trực tuyến của các sếp và bứt phá doanh thu!