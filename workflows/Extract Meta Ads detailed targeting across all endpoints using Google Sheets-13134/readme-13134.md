---
title: "🚀 Tự động trích xuất Meta Ads Detailed Targeting qua tất cả Endpoint với Google Sheets"
description: "Hướng dẫn chi tiết sử dụng workflow n8n tự động hóa khai thác dữ liệu nhắm mục tiêu chi tiết Meta Ads qua Facebook Graph API và lưu trữ trực tiếp vào Google Sheets."
slug: "trich-xuat-meta-ads-detailed-targeting-google-sheets"
tags: [n8n, automation, no-code, facebook-ads, marketing-automation, google-sheets]
keywords: [n8n workflow, meta ads targeting, facebook graph api, tự động hóa marketing, google sheets n8n]
---

# 🚀 Tự động trích xuất Meta Ads Detailed Targeting qua tất cả Endpoint với Google Sheets

Các nhà quảng cáo và chuyên gia Media Buyer thường mất hàng giờ đồng hồ để tìm kiếm, gợi ý và xác thực các sở thích (interests), nhân khẩu học hay hành vi nhắm mục tiêu (Detailed Targeting) trên Meta Ads Manager. Việc làm thủ công này vừa tốn thời gian, khó lưu trữ hệ thống, lại không tiện cho việc phân tích số lượng lớn.

Giải pháp là gì? Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình gọi **Facebook Graph API** thông qua Google Sheets. Chỉ cần nhập yêu cầu vào Google Sheet, hệ thống sẽ tự động bóc tách qua 4 endpoint khác nhau (`search`, `suggestions`, `browse`, `validation`) và trả kết quả về đúng các trang tính tương ứng một cách mượt mà!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần thao tác thủ công trên Trình quản lý quảng cáo, chỉ cần kích hoạt qua Google Sheets Trigger hoặc Manual.
- **Đa dạng hóa Endpoint**: Hỗ trợ đồng thời 4 tính năng mạnh mẽ của Meta API: Tìm kiếm (Search), Gợi ý (Suggestions), Duyệt (Browse) và Xác thực (Validation).
- **Lưu trữ khoa học**: Tự động phân loại và ghi kết quả vào 4 sheet riêng biệt (`search_results`, `suggestions_results`, `browse_results`, `validation_results`).
- **Giữ nguyên ngữ cảnh**: Kết hợp thông minh giữa response từ API và request ban đầu, giúp dễ dàng tra cứu xem dữ liệu nào phục vụ cho chiến dịch/tài khoản quảng cáo nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Account** đã kết nối Credentials với n8n (`Google Sheets OAuth2 API`).
- **Meta (Facebook) Developer Account & App** có quyền truy cập Facebook Graph API với quyền quảng cáo hợp lệ (`Facebook Graph API Credentials`).
- Một Google Sheet chuẩn bị sẵn các bảng tính theo yêu cầu bên dưới.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n.io (Link gốc: [Workflow #13134](https://n8n.io/workflows/13134)) hoặc sao chép toàn bộ mã JSON và dán trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các thành phần sau:

- **Chuẩn bị cấu trúc Google Sheets**: 
  Tạo một Google Sheet chứa các sheet (trang tính) sau:
  1. `targeting_requests`: Chứa các cột điều kiện như `endpoint` (`search` | `suggestions` | `browse` | `validation`), `ad_account_id`, và các tham số phụ trợ như `q`, `targeting_list`, `limit_type`, `limit`, `locale`.
  2. `search_results`
  3. `suggestions_results`
  4. `browse_results`
  5. `validation_results`

- **Cấu hình Document ID**: 
  Truy cập vào các node **Read Input (Google Sheets)**, **Google Sheets Trigger**, và toàn bộ 4 node lưu dữ liệu (**Save search_results**, **Save suggestions_results**, **Save browse_results**, **Save validation_results**), sau đó trỏ chúng về cùng một Spreadsheet ID của Google Sheet vừa tạo.

- **Kết nối Credentials**:
  - Gán tài khoản Google Sheets vào các node Google Sheets và Google Sheets Trigger.
  - Gán Facebook Graph API Token vào các node API (`API Search`, `API Suggestions`, `API Browse`, `API Validation`).

- **Định dạng dữ liệu đầu vào đặc biệt**:
  - Đối với các yêu cầu **Suggestions** và **Validation**: Cột `targeting_list` phải có định dạng là một JSON array chuẩn, ví dụ: `[{"type":"interests","id":"6003263791114"}]`.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** trên node **Manual Trigger** để test thử với một vài dòng dữ liệu mẫu trong sheet `targeting_requests`.
- Kiểm tra kết quả trả về ở các sheet tương ứng.
- Sau khi mọi thứ chạy ổn định, bật công tắc **Active** để kích hoạt **Google Sheets Trigger** (tự động chạy mỗi khi có dòng mới được thêm vào sheet).

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Thêm node Telegram hoặc Slack ở cuối workflow để nhận thông báo ngay khi quá trình quét và trích xuất targeting hoàn tất.
- **Lưu log lỗi**: Thêm node `Error Trigger` để bắt lỗi trong quá trình gọi API (ví dụ token hết hạn hoặc tài khoản bị giới hạn) và gửi cảnh báo về email hoặc chatwork.
- **Tự động hóa định kỳ**: Thay vì chỉ dùng Google Sheets Trigger, các sếp có thể kết hợp thêm node `Schedule Trigger` để tự động cập nhật danh sách target mỗi tuần/tháng.

### 📌 Kết luận
Workflow này là một "vũ khí bí mật" giúp các Media Buyer và đội ngũ マーケティング (Marketing) tối ưu hóa thời gian nghiên cứu đối tượng quảng cáo trên Meta Ads. Hãy áp dụng ngay vào hệ thống n8n của các sếp để nâng tầm hiệu suất chiến dịch!