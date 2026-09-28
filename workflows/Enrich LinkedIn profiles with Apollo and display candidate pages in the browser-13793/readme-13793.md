---
title: "🚀 Tự động hóa làm giàu hồ sơ LinkedIn với Apollo và hiển thị trực tiếp trên trình duyệt"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình enrich thông tin ứng viên/khách hàng từ LinkedIn sử dụng Apollo API và hiển thị kết quả trực quan trên trình duyệt."
slug: "tu-dong-hoa-lam-giau-ho-so-linkedin-apollo-n8n"
tags: [n8n, automation, no-code, apollo, lead-generation, linkedin]
keywords: [n8n workflow, apollo io, linkedin enrich, tự động hóa lead generation, n8n việt nam]
---

# 🚀 Tự động hóa làm giàu hồ sơ LinkedIn với Apollo và hiển thị trực tiếp trên trình duyệt

Việc tìm kiếm, tổng hợp và "làm giàu" (enrich) thông tin ứng viên hoặc khách hàng tiềm năng từ LinkedIn theo cách thủ công thường ngốn rất nhiều thời gian của các đội ngũ tuyển dụng (HR) và Sales. Các sếp thường phải copy từng đường link LinkedIn, tra cứu chéo trên các nền tảng dữ liệu rồi mới tổng hợp lại. 

Được sáng tạo bởi chuyên gia tự động hóa **Rahul Joshi**, workflow n8n này sẽ giải quyết triệt để bài toán trên bằng cách tự động hóa 100% quy trình kết nối với **Apollo API** để trích xuất thông tin chi tiết từ URL LinkedIn và trả kết quả hiển thị trực quan ngay trên trình duyệt web chỉ trong vài giây.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần tra cứu thủ công từng profile LinkedIn, hệ thống tự động xử lý hàng loạt.
- **Dữ liệu chính xác và sâu hơn:** Khai thác tối đa các trường thông tin chất lượng cao từ cơ sở dữ liệu của Apollo.io.
- **Trải nghiệm trực quan:** Kết quả được trả về và định dạng đẹp mắt ngay trên giao diện trình duyệt web nhờ Webhook Response.
- **Vận hành linh hoạt:** Dễ dàng tích hợp vào các hệ thống CRM hoặc quy trình tuyển dụng hiện tại của doanh nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản và **API Key từ Apollo.io** để thực hiện các truy vấn dữ liệu làm giàu hồ sơ (Enrichment).
- Các URL profile LinkedIn cần xử lý đầu vào.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp tải file JSON của workflow từ nguồn chính thức hoặc copy đoạn mã JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dùng tổ hợp phím `Ctrl + V` để dán trực tiếp vào màn hình làm việc).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow vận hành trơn tru, các sếp cần chú ý cấu hình các node cốt lõi sau:
- **Webhook Node:** Đóng vai trò là điểm tiếp nhận dữ liệu đầu vào (URL LinkedIn). Hãy cấu hình Method (POST/GET) phù hợp với cách các sếp muốn gửi request.
- **HTTP Request Node (Apollo API):** 
  - Cần thiết lập Authentication bằng Apollo API Key của các sếp.
  - Trỏ endpoint đúng chuẩn của Apollo API dùng để enrich profile dựa trên LinkedIn URL.
  - Đảm bảo truyền tham số `linkedin_url` từ dữ liệu đầu vào của Webhook vào body hoặc query parameters của request.
- **Code Node:** Dùng để xử lý, làm sạch dữ liệu JSON nhận về từ Apollo trước khi hiển thị.
- **Respond to Webhook Node:** Cấu hình trả về định dạng HTML hoặc JSON thân thiện để hiển thị trực tiếp kết quả lên trình duyệt của người dùng.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một request test chứa URL LinkedIn để kiểm tra dữ liệu trả về.
- Sau khi kiểm tra mọi thứ hoạt động chính xác, bật công tắc **Active** ở góc trên bên phải để đưa workflow vào trạng thái hoạt động tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Kết hợp thêm node Telegram hoặc Slack để nhận thông báo ngay lập tức mỗi khi có một profile được enrich thành công.
- **Lưu trữ tự động:** Thêm Google Sheets hoặc Airtable node để lưu lại lịch sử các profile đã tra cứu, phục vụ việc chăm sóc khách hàng hoặc lưu trữ hồ sơ ứng viên.
- **Xử lý hàng loạt (Batch Processing):** Nâng cấp workflow để nhận danh sách file CSV chứa hàng trăm link LinkedIn và xử lý tuần tự tự động.

### 📌 Kết luận
Workflow tự động hóa làm giàu hồ sơ LinkedIn với Apollo này là trợ thủ đắc lực giúp tối ưu hóa hiệu suất cho đội ngũ Sales và HR. Hãy triển khai ngay trên hệ thống n8n của các sếp để nâng tầm tự động hóa doanh nghiệp!