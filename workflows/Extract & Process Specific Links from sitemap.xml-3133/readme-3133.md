---
title: "🚀 Tự động trích xuất và lọc danh sách liên kết từ Sitemap.xml với n8n"
description: "Hướng dẫn xây dựng workflow n8n giúp tự động tải, chuyển đổi và lọc các URL mong muốn từ sitemap.xml một cách nhanh chóng và chính xác."
slug: "trich-xuat-va-loc-lien-ket-tu-sitemap-xml-n8n"
tags: [n8n, automation, no-code, sitemap, seo, data-extraction]
keywords: [n8n workflow, trích xuất sitemap, lọc URL sitemap, tự động hóa n8n, xml to json n8n]
---

# 🚀 Tự động trích xuất và lọc danh sách liên kết từ Sitemap.xml với n8n

Việc quản lý, kiểm tra hoặc quét dữ liệu từ các website lớn đòi hỏi các sếp phải xử lý hàng ngàn URL có trong file `sitemap.xml`. Nếu làm thủ công bằng cách mở từng file XML hay copy/paste, các sếp sẽ mất rất nhiều thời gian và dễ bỏ sót thông tin. 

Đừng lo, workflow n8n được thiết kế bởi **Audun** này sẽ giúp các sếp tự động hóa 100% quy trình: tải sitemap, chuyển đổi dữ liệu từ XML sang JSON và lọc ra chính xác các liên kết cần thiết (như file PDF, bài viết chuyên mục, hoặc landing page) mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chỉ với 1 cú click (hoặc chạy lịch trình), toàn bộ sitemap được phân tích.
- **Lọc thông minh:** Dễ dàng tìm kiếm chính xác các định dạng file (PDF, hình ảnh) hoặc các URL chứa từ khóa cụ thể.
- **Tiết kiệm thời gian:** Thay vì rà soát thủ công hàng ngàn dòng XML, hệ thống lọc sẵn danh sách trong vài giây.
- **Linh hoạt mở rộng:** Dữ liệu đầu ra dạng JSON sẵn sàng để chuyển tiếp sang Google Sheets, Notion, hoặc gửi về Telegram/Slack.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động (Cloud hoặc Self-hosted).
- Đường dẫn (URL) của file `sitemap.xml` cần xử lý.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp copy đoạn mã JSON của workflow này hoặc tải file JSON từ nguồn gốc.
- Mở n8n Editor, chọn **Add workflow** -> Nhấn vào dấu `...` ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 6 nodes chính, các sếp cần chú ý cấu hình 2 node quan trọng sau:

- **Node `Set sitemap URL` (Set):** 
  - Mở node này lên và tìm đến trường chứa URL.
  - Thay thế đường dẫn mẫu bằng đường dẫn `sitemap.xml` thực tế của website mà các sếp muốn phân tích.
- **Node `Filter URLs` (Filter):**
  - Theo mặc định ban đầu, workflow được thiết lập để lọc ra các tài liệu có định dạng `.pdf`.
  - Các sếp cần chỉnh sửa điều kiện lọc (Conditions) trong node này cho phù hợp với mục đích cá nhân (ví dụ: lọc các URL chứa từ khóa `/blog/`, định dạng `.jpg`, hoặc bắt đầu bằng một tiền tố cụ thể).

#### 3. Các node hỗ trợ trong luồng:
- **`‘Test workflow’ trigger` (manualTrigger):** Dùng để kích hoạt test thủ công khi xây dựng.
- **`Get Sitemap` (httpRequest):** Gửi yêu cầu HTTP GET để tải nội dung thô của file `sitemap.xml`.
- **`Convert Sitemap to JSON` (xml):** Chuyển đổi dữ liệu XML nhận được thành định dạng JSON để các node sau dễ dàng xử lý.
- **`Split Out` (splitOut):** Tách mảng dữ liệu URL lớn thành các item riêng lẻ để hệ thống dễ dàng lọc và xử lý tuần tự.

#### 4. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** để kiểm tra kết quả trả về ở node cuối cùng (`Filter URLs`).
- Sau khi kiểm tra dữ liệu đã chính xác như kỳ vọng, hãy gạt công tắc sang **Active** để sẵn sàng sử dụng bất cứ lúc nào.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Google Sheets / Notion:** Thêm một node Google Sheets ở cuối workflow để tự động lưu danh sách URL đã lọc vào bảng tính, phục vụ cho việc kiểm tra SEO hoặc audit website.
- **Cảnh báo qua Telegram/Slack:** Nếu tìm thấy các URL mới hoặc lỗi, các sếp có thể tích hợp thêm node gửi thông báo về chatwork/Telegram để nắm bắt kịp thời.
- **Chạy tự động định kỳ:** Thay thế node `manualTrigger` bằng `Schedule Trigger` để n8n tự động quét sitemap mỗi tuần/mỗi tháng nhằm theo dõi sự thay đổi cấu trúc website.

### 📌 Kết luận
Workflow "Extract & Process Specific Links from sitemap.xml" là một công cụ cực kỳ hữu ích dành cho anh em làm SEO, Marketer và Developer để quản lý tài nguyên website. Hãy áp dụng ngay vào hệ thống n8n của các sếp để tối ưu hóa công việc hàng ngày nhé!