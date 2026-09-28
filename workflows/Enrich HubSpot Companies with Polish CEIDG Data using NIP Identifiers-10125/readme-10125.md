---
title: "🚀 Tự động làm giàu dữ liệu doanh nghiệp Ba Lan trong HubSpot với CEIDG API"
description: "Hướng dẫn chi tiết cách sử dụng n8n để tự động đồng bộ và làm giàu thông tin công ty Ba Lan từ cơ quan thuế CEIDG vào HubSpot dựa trên mã số thuế NIP."
slug: "tu-dong-lam-giau-du-lieu-hubspot-ceidg-nip"
tags: [n8n, automation, hubspot, crm, lead-generation, api]
keywords: [n8n workflow, hubspot ceidg, tich hop hubspot ceidg, tu dong hoa crm, nip ba lan]
---

# 🚀 Tự động làm giàu dữ liệu doanh nghiệp Ba Lan trong HubSpot với CEIDG API

Các sếp làm sales, marketing hay quản trị CRM tại các thị trường châu Âu (đặc biệt là Ba Lan) chắc chắn đã quá ngán ngẩm cảnh phải tra cứu thủ công từng mã số thuế (NIP) trên cổng thông tin chính phủ, sau đó copy-paste từng dòng tên công ty, địa chỉ, số điện thoại vào HubSpot. Vừa mất thời gian, vừa dễ sai sót dữ liệu.

Workflow n8n này sinh ra để giải quyết triệt để nỗi đau đó! Hệ thống sẽ tự động bắt sự kiện khi một mã NIP được thêm hoặc cập nhật trên HubSpot, gọi trực tiếp vào cơ sở dữ liệu chính phủ Ba Lan (CEIDG) và điền toàn bộ thông tin chuẩn chỉnh vào CRM một cách tự động 100% không cần code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian nhập liệu:** Tạm biệt công việc copy-paste thủ công nhàm chán.
- **Dữ liệu CRM luôn chuẩn xác:** Lấy dữ liệu chính thống trực tiếp từ cơ quan đăng ký kinh doanh Ba Lan (CEIDG).
- **Cá nhân hóa tự động:** Tự động điền tên công ty, địa chỉ đầy đủ, số điện thoại, website, số NIP/REGON và ngày thành lập.
- **Xử lý ngoại lệ thông minh:** Tự động đánh dấu lỗi hoặc ghi chú vào HubSpot nếu mã NIP không hợp lệ hoặc không tìm thấy.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n instance**: Bản self-hosted hoặc n8n Cloud.
- **Tài khoản HubSpot**: Đã tạo sẵn custom property `nip` (kiểu Single-line text) và `ceidg_notes` (kiểu Multi-line text).
- **CEIDG API Token**: Đăng ký tài khoản miễn phí tại [dane.biznes.gov.pl](https://dane.biznes.gov.pl/) để lấy API token.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc copy toàn bộ mã JSON của workflow rồi paste thẳng vào màn hình làm việc của n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 7 nodes chính phối hợp nhịp nhàng:

- **When NIP property changes (`hubspotTrigger`)**: Cấu hình kết nối HubSpot Credentials. Chọn property để trigger là `nip`. Khi có thông tin NIP được thêm hoặc thay đổi, workflow sẽ tự động kích hoạt.
- **Check if NIP exists (`if`)**: Node điều kiện kiểm tra xem trường NIP có bị trống hay không. Nếu trống, workflow dừng lại để tránh lãng phí API call.
- **Fetch company data from CEIDG (`httpRequest`)**: Gọi API đến hệ thống CEIDG. Các sếp cần cấu hình Header Authentication sử dụng Bearer Token với API Key đã lấy từ `dane.biznes.gov.pl`.
- **Check if data retrieved (`if`)**: Kiểm tra kết quả trả về từ API. Nếu tìm thấy dữ liệu (`count > 0`), đi tiếp nhánh thành công; ngược lại chuyển sang nhánh lỗi.
- **Transform data for HubSpot (`code`)**: Node JavaScript giúp chuẩn hóa và map các trường dữ liệu từ CEIDG sang đúng định dạng mà HubSpot yêu cầu (Tên công ty, địa chỉ, số điện thoại, website, REGON...).
- **Update company in HubSpot (`hubspot`)**: Thực hiện cập nhật toàn bộ thông tin đã làm giàu vào bản ghi Company tương ứng trên HubSpot.
- **Mark error in HubSpot (`hubspot`)**: Nếu NIP sai hoặc không tồn tại, node này sẽ tự động thêm một ghi chú (note) vào profile công ty trên HubSpot để đội ngũ sales dễ dàng nắm bắt.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một mã NIP mẫu của một doanh nghiệp Ba Lan để kiểm tra dòng dữ liệu chạy qua từng node.
- Sau khi kiểm tra thành công, gạt công tắc sang **Active** để hệ thống tự động hóa hoàn toàn 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Thêm node Slack hoặc Telegram sau node cập nhật thành công để bắn thông báo cho team sales khi có lead doanh nghiệp mới được làm giàu.
- **Mở rộng nguồn dữ liệu**: Nếu doanh nghiệp các sếp làm việc cả với công ty cổ phần (sp. z o.o.), có thể tích hợp thêm KRS API bên cạnh CEIDG API.
- **Ghi log hoạt động**: Kết nối thêm một Google Sheets node để lưu lại lịch sử các lần tra cứu và làm giàu dữ liệu phục vụ việc báo cáo định kỳ.

### 📌 Kết luận
Workflow tự động hóa làm giàu dữ liệu HubSpot bằng CEIDG API chính là mảnh ghép hoàn hảo giúp các đội ngũ sales làm việc tại thị trường Ba Lan tối ưu hóa hiệu suất, loại bỏ thao tác thủ công và sở hữu một cơ sở dữ liệu CRM luôn sạch sẽ, chính xác. "Lên đồ" và cài đặt ngay hôm nay các sếp nhé!