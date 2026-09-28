---
title: "🚀 Tự động định vị địa lý IP và quét cổng HTTP với Google Sheets trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy thông tin định vị địa lý (Geolocation) và quét trạng thái các cổng HTTP khi có IP mới được thêm vào Google Sheets."
slug: "tu-dong-dinh-vi-ip-va-quet-cong-http-google-sheets"
tags: [n8n, automation, secops, google-sheets, network-monitoring, ip-geolocation]
keywords: [n8n workflow, ip geolocation, http port scanning, google sheets trigger, bảo mật mạng, tự động hóa n8n]
---

# 🚀 Tự động định vị địa lý IP và quét cổng HTTP với Google Sheets

Các sếp làm trong lĩnh vực bảo mật (SecOps), quản trị mạng hay phân tích hệ thống chắc chắn đã quen thuộc với việc thủ công tra cứu thông tin IP và kiểm tra các cổng (port) mở. Công việc này vừa nhàm chán, tốn thời gian lại dễ bỏ sót khi số lượng IP cần kiểm tra lớn.

Giải pháp là gì? Workflow n8n này sẽ tự động hóa 100% quy trình: Ngay khi các sếp thêm một địa chỉ IP mới vào Google Sheets, hệ thống sẽ tự động truy vấn thông tin định vị địa lý (Geolocation) và tiến hành quét các cổng HTTP phổ biến, sau đó cập nhật trực tiếp kết quả ngược lại vào bảng tính. Không cần code phức tạp, chạy mượt mà và tự động hoàn toàn!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chỉ cần nhập IP mới vào Google Sheet, mọi việc còn lại n8n lo.
- **Làm giàu dữ liệu (Data Enrichment):** Tự động thu thập thông tin Geolocation (quốc gia, thành phố, ISP, v.v.) của IP.
- **Kiểm tra trạng thái cổng (Port Scanning):** Quét nhanh chóng các cổng HTTP quan trọng xem đang mở (open) hay đóng (closed).
- **Lưu trữ tập trung:** Toàn bộ kết quả được đồng bộ thẳng về Google Sheets giúp dễ dàng theo dõi và báo cáo.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản Google có quyền truy cập Google Sheets.
- Một Google Sheet mẫu (các sếp có thể tham khảo cấu trúc tại [Sample Google Sheet](https://docs.google.com/spreadsheets/d/19MSjNyjzs1FeRI5_QLiVk8Hi9JNt5HD1bNulfpB6SzI/edit?usp=sharing)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow (hoặc tải từ [n8n Template #8674](https://n8n.io/workflows/8674)) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 8 nodes chính, các sếp cần chú ý cấu hình kỹ các node sau:

- **Google Sheets Trigger:** 
  - Kết nối tài khoản Google Sheets của các sếp (OAuth2).
  - Chọn đúng file Spreadsheet và Sheet chứa danh sách IP cần theo dõi. Node này sẽ kích hoạt ngay khi có một dòng mới được thêm vào.
- **GetIP_Info (HTTP Request):** 
  - Node này gọi API định vị địa lý để lấy thông tin chi tiết về IP. Các sếp đảm bảo endpoint API (như ipapi, ipinfo hoặc tương tự) được cấu hình đúng chuẩn nhận tham số IP từ Google Sheets.
- **Update_IP_Info_row (Google Sheets):** 
  - Cấu hình thao tác `update` để ghi đè hoặc bổ sung thông tin Geolocation vừa lấy được vào các cột tương ứng trong dòng của Google Sheet.
- **Split Out & Edit Fields (Set):** 
  - Định nghĩa danh sách các cổng HTTP cần quét (ví dụ: `80`, `443`, `8080`, `8443`,...). Node `Split Out` sẽ tách mảng các cổng thành các item riêng biệt để quét tuần tự hoặc song song.
- **CheckHttpPort (HTTP Request):** 
  - Thực hiện kiểm tra kết nối tới từng cổng HTTP của IP đó.
- **PutAll_in_OneItem (Code) & Update_HTTP_Ports_State (Google Sheets):** 
  - Tổng hợp kết quả quét các cổng (mở/đóng) và cập nhật trạng thái chi tiết này trở lại Google Sheets.

#### 3. Kích hoạt ⚡️
- Thử nghiệm bằng cách nhập một địa chỉ IP mẫu vào Google Sheet và bấm **Test step** hoặc **Execute Workflow** trên n8n để kiểm tra dữ liệu luân chuyển.
- Sau khi chắc chắn mọi thứ hoạt động trơn tru, hãy bật công tắc **Active** ở góc trên bên phải màn hình n8n.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp cảnh báo Telegram/Slack:** Thêm một node Telegram hoặc Slack ngay sau khi quét xong. Nếu phát hiện cổng nhạy cảm mở bất thường (ví dụ: SSH 22 hoặc Telnet 23), hệ thống sẽ bắn tin nhắn cảnh báo ngay lập tức.
- **Lên lịch định kỳ (Cron):** Thay vì chỉ trigger khi thêm mới, các sếp có thể kết hợp thêm `Schedule Trigger` để quét lại toàn bộ danh sách IP trong Sheet hàng tuần/hàng tháng nhằm kiểm tra sự thay đổi trạng thái bảo mật.

### 📌 Kết luận
Với workflow n8n này, việc quản lý và trinh sát thông tin IP, cổng mạng chưa bao giờ dễ dàng đến thế. Hãy áp dụng ngay vào hệ thống của các sếp để tiết kiệm hàng giờ thao tác thủ công mỗi ngày!