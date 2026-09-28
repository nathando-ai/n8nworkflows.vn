---
title: "🚀 Tự động tạo nội dung chuẩn SEO bằng Google Gemini và đẩy lên PrestaShop với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động đọc dữ liệu sản phẩm từ Google Sheets, sử dụng AI Agent tạo nội dung chuẩn SEO và cập nhật trực tiếp lên PrestaShop."
slug: "tu-dong-tao-noi-dung-seo-prestashop-google-gemini-n8n"
tags: [n8n, automation, prestashop, google-gemini, ai-agent, e-commerce]
keywords: [n8n workflow, prestashop seo, google gemini ai agent, tự động hóa e-commerce, google sheets n8n]
---

# 🚀 Tự động tạo nội dung chuẩn SEO bằng Google Gemini và đẩy lên PrestaShop với n8n

Viết mô tả sản phẩm và tối ưu chuẩn SEO (Meta Title, Description, Slug, Long Description...) cho hàng trăm, hàng ngàn sản phẩm trên sàn thương mại điện tử như PrestaShop là một "nỗi ác mộng" tốn hàng tá thời gian của các nhà quản lý website. Làm thủ công vừa chậm, vừa dễ sót ý, lại khó đảm bảo tính đồng nhất.

Workflow n8n này sinh ra để giải quyết triệt để bài toán đó! Được thiết kế bởi chuyên gia tự động hóa **Salman Mehboob**, hệ thống sẽ tự động quét danh sách sản phẩm chưa cập nhật từ Google Sheets, nhờ **Google Gemini AI** nghiên cứu và viết nội dung chuẩn SEO cực kỳ chi tiết, sau đó tự động đẩy (push) trực tiếp lên cửa hàng PrestaShop qua API và ghi log lại trạng thái một cách hoàn toàn tự động.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh ngồi viết tay hàng trăm mô tả sản phẩm.
- **Chuẩn SEO chuyên nghiệp:** AI tự động phân tích và tạo Meta Title, Meta Description, Short/Long Description chuẩn chỉnh.
- **Đồng bộ hóa mượt mà:** Tự động cập nhật trực tiếp lên PrestaShop và ghi log trạng thái ngược lại Google Sheets.
- **Vận hành an toàn:** Cơ chế chia batch (lô) thông minh kết hợp thời gian chờ (Wait) giúp tránh bị chặn API do quá tải.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Sheets:** Tài khoản kết nối Google Sheets OAuth2 và một file Google Sheet chuẩn bị sẵn với các cột: `Address`, `Previous`, `Title`, `Short Description`, `Long Description`, `Meta Title`, `Meta Description`, `Slug`, `Update`.
- **Google Gemini API:** API Key kết nối với Google Palm/Gemini API.
- **PrestaShop API:** Bearer Token hoặc Webservice Key để gọi API cập nhật sản phẩm từ PrestaShop.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, sau đó vào giao diện n8n Editor, chọn **Add workflow** -> Nhấn tổ hợp phím `Ctrl + V` (hoặc `Cmd + V`) để dán trực tiếp vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần cấu hình chính xác các node sau:

- **Get Products & Log In Sheet (Google Sheets Nodes):** Kết nối tài khoản Google Sheets của các sếp qua OAuth2, sau đó chọn đúng file Google Sheet và Sheet Name chứa dữ liệu sản phẩm.
- **Google Gemini Chat Model:** Thêm Credentials API của Google Gemini để AI Agent có "não" hoạt động.
- **Arrange Data (Set Node):** ⚠️ **CỰC KỲ QUAN TRỌNG:** Các sếp phải điền PrestaShop Bearer API Token vào trường `API_Key` trong node này để có quyền gọi API cập nhật sản phẩm.
- **Get Product ID (Code Node):** Node này sử dụng Regex để bóc tách ID sản phẩm từ URL PrestaShop trong cột `Address`. Đảm bảo URL sản phẩm trong sheet đúng định dạng.
- **Update Product (HTTP Request Node):** Kiểm tra lại endpoint API PATCH của PrestaShop để chắc chắn rằng dữ liệu gửi đi khớp với cấu trúc hệ thống của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử với 1-2 dòng dữ liệu mẫu đầu tiên (thông qua nút **Mannual Trigger**).
- Kiểm tra kết quả trên Google Sheets và PrestaShop xem đã cập nhật đúng ý chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để hệ thống sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Thông báo:** Thêm node Telegram hoặc Slack ở cuối luồng để nhận thông báo tổng kết sau khi workflow xử lý xong 50 sản phẩm (ví dụ: *"Đã tối ưu xong SEO cho 50 sản phẩm trên PrestaShop!"*).
- **Mở rộng Đa ngôn ngữ:** Tinh chỉnh prompt trong **AI Agent** để yêu cầu AI tạo nội dung bằng tiếng Anh, tiếng Tây Ban Nha hoặc tiếng Việt tùy theo thị trường mục tiêu của cửa hàng.
- **Tự động hóa theo lịch (Cron):** Thay thế node `Mannual Trigger` bằng `Schedule Trigger` để workflow tự động chạy vào khung giờ thấp điểm hàng ngày (ví dụ 2:00 sáng).

### 📌 Kết luận
Tự động hóa việc tối ưu nội dung SEO sản phẩm cho PrestaShop với Google Gemini không chỉ giúp tiết kiệm thời gian khổng lồ mà còn nâng cao chất lượng hiển thị trên các công cụ tìm kiếm. Hãy cài đặt ngay workflow này để tối ưu hóa hiệu suất kinh doanh thương mại điện tử của các sếp!