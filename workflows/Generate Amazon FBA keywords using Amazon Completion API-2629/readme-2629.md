---
title: "🚀 Tự động tạo bộ từ khóa Amazon FBA miễn phí với n8n và Amazon Completion API"
description: "Hướng dẫn xây dựng công cụ nghiên cứu từ khóa Amazon FBA tự động 100% không cần code, kết nối Airtable và Amazon Completion API qua n8n."
slug: "tu-dong-tao-tu-khoa-amazon-fba-voi-n8n"
tags: [n8n, automation, no-code, amazon-fba, seo, airtable]
keywords: [n8n workflow, amazon fba keywords, amazon completion api, tự động hóa airtable, nghiên cứu từ khóa amazon]
---

# 🚀 Tự động tạo bộ từ khóa Amazon FBA miễn phí với n8n và Amazon Completion API

Nghiên cứu từ khóa thủ công cho gian hàng Amazon FBA luôn là một "cực hình" ngốn rất nhiều thời gian của các nhà bán hàng. Việc phải ngồi gõ từng từ khóa vào thanh tìm kiếm của Amazon để lấy các gợi ý (suggested keywords) rồi copy-paste vào Excel vô cùng tẻ nhạt và kém hiệu quả.

Đừng lo, các sếp hoàn toàn có thể tự xây dựng một công cụ nghiên cứu từ khóa "xịn sò" không thua kém các phần mềm trả phí hàng tháng, nhờ vào workflow n8n tự động hóa 100% kết nối trực tiếp với **Amazon Completion API** và **Airtable**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Gửi từ khóa gốc và nhận lại hàng loạt từ khóa gợi ý từ Amazon ngay lập tức.
- **Tiết kiệm chi phí**: Không cần tốn tiền mua các tool nghiên cứu từ khóa Amazon đắt đỏ.
- **Quản lý tập trung**: Toàn bộ từ khóa được lưu trữ gọn gàng, khoa học trên Airtable để dễ dàng phân tích.
- **Hoạt động 24/7**: Kích hoạt bất cứ lúc nào qua Webhook trực tiếp từ cơ sở dữ liệu của các sếp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n**: Đã cài đặt sẵn (Cloud hoặc Self-hosted).
- **Tài khoản Airtable**: Dùng để lưu trữ từ khóa gốc và nhận danh sách từ khóa gợi ý trả về.
- **Amazon Completion API**: Endpoint công khai từ Amazon (không cần API key phức tạp).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp hãy sao chép mã JSON của workflow (hoặc tải file từ nguồn cung cấp) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 8 nodes chính, các sếp cần chú ý cấu hình kỹ các node sau:

- **Receive Keyword (Webhook)**: Node nhận yêu cầu từ bên ngoài (ví dụ: từ Airtable gửi sang). Các sếp nhớ lấy URL Webhook này cấu hình vào hệ thống gửi dữ liệu của mình.
- **Get airtable data (Airtable)**: Cấu hình credentials `airtableTokenApi`, chọn đúng Base và Table chứa từ khóa hạt giống (seed keywords) của các sếp. *(Có thể tham khảo mẫu Airtable tại [đây](https://airtable.com/invite/l?inviteId=invgv9FzNB258bm5Z&inviteToken=6f820e142d3324318254c1768fa57809b3ef0bcb7212ea27730fd2d140c69ad5))*
- **Get Amazon keywords (HTTP Request)**: Node này gọi trực tiếp đến Amazon Completion API để lấy các gợi ý tìm kiếm dựa trên từ khóa gốc.
- **Format output & Aggregate keywords & Combine into string (SplitOut, Code, Set)**: Các nodes trung gian làm sạch dữ liệu, lọc các định dạng JSON trả về từ Amazon và gộp chúng thành một chuỗi hoàn chỉnh.
- **Save keywords (Airtable)**: Cấu hình cập nhật (update) ngược lại vào Airtable, lưu danh sách từ khóa đã được tổng hợp xong xuôi cho từng sản phẩm.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Execute Node** hoặc **Test Workflow**) với một từ khóa mẫu để kiểm tra luồng dữ liệu.
- Sau khi dữ liệu đổ về Airtable chuẩn chỉnh, các sếp bấm nút **Active** để đưa workflow vào trạng thái chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Telegram/Slack**: Thêm một node thông báo để mỗi khi workflow chạy xong và lưu từ khóa vào Airtable, hệ thống sẽ bắn một tin nhắn báo cáo về Telegram cho các sếp.
- **Mở rộng thị trường**: Tinh chỉnh lại thông số quốc gia trong Amazon Completion API (ví dụ: `.com` cho Mỹ, `.co.uk` cho Anh, `.de` cho Đức) để nghiên cứu từ khóa đa quốc gia.
- **Lên lịch chạy định kỳ (Cron/Schedule)**: Thay vì dùng Webhook thủ công, các sếp có thể kết hợp thêm Schedule Trigger để tự động quét từ khóa mới hàng tuần.

### 📌 Kết luận
Với workflow n8n này, việc nghiên cứu từ khóa Amazon FBA trở nên nhanh chóng, tự động và hoàn toàn miễn phí. Hãy triển khai ngay hôm nay để tối ưu hóa chiến dịch SEO và PPC trên Amazon của các sếp!