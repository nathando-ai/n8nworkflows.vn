---
title: "🚀 Tự động lấy báo cáo Meta Ads và lưu vào Google Sheets bằng n8n"
description: "Hướng dẫn thiết lập workflow n8n tự động hóa kéo dữ liệu quảng cáo từ Meta Ads (Facebook Ads) và đồng bộ vào Google Sheets mỗi ngày cực kỳ nhanh chóng."
slug: "tu-dong-lay-bao-cao-meta-ads-va-luu-google-sheets"
tags: [n8n, automation, no-code, marketing, facebook-ads, google-sheets]
keywords: [n8n workflow, meta ads insights, google sheets automation, facebook graph api, tu dong hoa marketing]
---

# 🚀 Tự động lấy báo cáo Meta Ads và lưu vào Google Sheets

Các sếp chạy quảng cáo Facebook chắc chắn đã quá ngán ngẩm cảnh mỗi sáng phải mở Trình quản lý quảng cáo (Ads Manager), xuất file Excel thủ công, rồi copy-paste vào Google Sheets để làm báo cáo cho sếp lớn hoặc team. Việc này không chỉ tốn thời gian mà còn dễ dẫn đến sai sót số liệu.

Đừng lo, bài viết này sẽ hướng dẫn các sếp cách "lên đồ" một workflow n8n cực đỉnh giúp tự động hóa 100% quy trình: lấy số liệu chi tiết từ **Meta Ads** và đổ thẳng vào **Google Sheets** hàng ngày mà không cần chạm tay vào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm hàng giờ đồng hồ mỗi tuần:** Không còn cảnh xuất báo cáo thủ công mỗi sáng.
- **Dữ liệu luôn thời gian thực (Real-time):** Số liệu được cập nhật tự động lúc 3h sáng mỗi ngày, sẵn sàng cho team xem lúc bắt đầu làm việc.
- **Phân tách chi tiết thông minh:** Workflow tự động phân loại rõ ràng các chỉ số chung, hành động chuyển đổi dạng tiền tệ (Monetary) và phi tiền tệ (Non-Monetary) vào các sheet riêng biệt.
- **Chính xác tuyệt đối:** Loại bỏ hoàn toàn rủi ro sai sót do copy-paste nhầm số liệu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị sẵn các "vũ khí" sau:
1. **Tài khoản n8n** (Cloud hoặc Self-hosted).
2. **Meta Business Account & Facebook Graph API Credentials** (AccessToken có quyền đọc Ads Insights).
3. **Google Sheets Account** (Tạo sẵn 1 file Google Sheets với các tab phù hợp để lưu dữ liệu).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này từ nguồn chính thức của tác giả Solomon và import trực tiếp vào n8n Editor của mình thông qua tính năng **Add from File** hoặc copy/paste trực tiếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công, các sếp cần cấu hình lại các node cốt lõi sau để hệ thống chạy trơn tru:

- **Trigger Nodes (`Everyday at 3am` / `When clicking ‘Test workflow’`):** 
  - Node `Everyday at 3am` (`scheduleTrigger`) sẽ tự động kích hoạt workflow chạy vào 3 giờ sáng hàng ngày. Các sếp có thể đổi lại múi giờ cho phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).
- **Facebook Graph API Nodes (`Ad insights from yesterday`, `Ad insights from any date period`):**
  - Cần kết nối tài khoản thông qua **Meta Graph API Credentials** (OAuth2 hoặc Access Token).
  - Điền đúng **Ad Account ID** của chiến dịch quảng cáo.
  - Cấu hình khoảng thời gian lấy dữ liệu (mặc định lấy ngày hôm qua cho báo cáo tự động).
- **Data Processing Nodes (`data column only`, `split actions`, `split action values`, các node `filter`):**
  - Các node này làm nhiệm vụ bóc tách, lọc dữ liệu (lọc theo action type, chỉ lấy hành động quy đổi ra tiền tệ hoặc phi tiền tệ). Các sếp giữ nguyên logic cấu hình của tác giả, chỉ kiểm tra lại xem cấu trúc JSON trả về từ Meta API có khớp hay không.
- **Google Sheets Nodes (`Add General Metrics`, `Add Non-Monetary actions`, `Add Monetary actions`):**
  - Kết nối tài khoản Google Sheets của các sếp.
  - Chọn đúng **Document** (File Google Sheets) và **Sheet Name** tương ứng cho từng loại dữ liệu: Chỉ số chung, Hành động phi tiền tệ, và Hành động có giá trị tiền tệ.
  - Map lại các cột dữ liệu (Columns) từ đầu ra của các node phía trước vào đúng các cột trên Google Sheets.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** để chạy thử nghiệm với node `When clicking ‘Test workflow’` nhằm kiểm tra xem dữ liệu có được đẩy về Google Sheets chuẩn chỉnh chưa.
- Sau khi test thành công, gạt công tắc sang **Active** để workflow tự động chạy ngầm mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa hệ thống báo cáo Marketing của doanh nghiệp, các sếp có thể mở rộng workflow này bằng cách:
1. **Thêm node Telegram / Slack:** Gửi thông báo tóm tắt chi phí, doanh thu, ROAS vào nhóm chat của team ngay sau khi chạy xong lúc 3h sáng.
2. **Lưu log lỗi:** Thêm nhánh Error Trigger để nếu Meta API lỗi hoặc token hết hạn, hệ thống sẽ bắn tin nhắn cảnh báo cho quản lý kỹ thuật.
3. **Mở rộng đa tài khoản:** Nhân bản nhánh lấy dữ liệu nếu công ty chạy nhiều tài khoản quảng cáo Meta khác nhau và gom chung về một Master Google Sheets.

### 📌 Kết luận
Việc tự động hóa báo cáo Meta Ads vào Google Sheets là bước đầu tiên cực kỳ quan trọng để chuyển đổi doanh nghiệp sang mô hình vận hành dựa trên dữ liệu (Data-driven). Hãy cài đặt ngay workflow này để giải phóng sức lao động cho team marketing của các sếp!