---
title: "🚀 Tự động hóa Magento 2: Vá lỗi Alt Text hình ảnh sản phẩm bằng tên sản phẩm siêu tốc"
description: "Hướng dẫn sử dụng n8n workflow để tự động quét và cập nhật Alt Text còn thiếu cho hình ảnh sản phẩm trên Magento 2 dựa vào tên sản phẩm, giúp tối ưu SEO Ecommerce không tốn công sức."
slug: "magento-2-auto-fix-missing-image-alt-tags"
tags: [n8n, automation, magento2, ecommerce, seo, content-creation]
keywords: [n8n workflow, magento 2 alt text, tu dong hoa magento, seo hinh anh ecommerce, n8n http request]
---

# 🚀 Tự động hóa Magento 2: Vá lỗi Alt Text hình ảnh sản phẩm bằng tên sản phẩm

Các sếp làm trong ngành thương mại điện tử (E-commerce) chắc chắn đều hiểu tầm quan trọng của SEO hình ảnh. Tuy nhiên, khi quản lý hàng ngàn sản phẩm trên Magento 2, việc để quên hoặc bỏ sót thẻ Alt Text (văn bản thay thế) cho hình ảnh là chuyện cơm bữa, ảnh hưởng nghiêm trọng đến điểm SEO On-page và khả năng tiếp cận khách hàng từ Google Images. 

Việc điền thủ công Alt Text cho hàng nghìn sản phẩm là "cực hình" tốn hàng tá thời gian. Giải pháp là gì? Bài viết này sẽ hướng dẫn các sếp sử dụng một n8n workflow tự động 100%, kết nối trực tiếp với Magento 2 để quét và tự động điền tên sản phẩm làm Alt Text cho những hình ảnh bị thiếu. Không cần code phức tạp, tự động hóa toàn diện!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tối ưu SEO tự động:** Đảm bảo 100% hình ảnh sản phẩm trên Magento 2 đều có Alt Text chuẩn SEO dựa trên tên sản phẩm.
- **Tiết kiệm thời gian tuyệt đối:** Thay vì mất hàng tuần ngồi sửa thủ công trong Admin Panel, workflow xử lý hàng ngàn sản phẩm chỉ trong vài phút.
- **Vận hành trơn tru:** Xử lý dữ liệu dạng phân lô (batching) giúp hệ thống Magento không bị quá tải hay lỗi timeout.
- **Tác giả uy tín:** Workflow được thiết kế bởi Kanaka Kishore Kandregula – Chuyên gia Magento 2 với hơn 10 năm kinh nghiệm.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **Magento 2** đang hoạt động.
- **Magento 2 REST API Credentials** (Integration Token hoặc Admin Token) để n8n có thể giao tiếp và cập nhật dữ liệu sản phẩm.
- n8n instance (Cloud hoặc Self-hosted).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ n8n template (hoặc copy nội dung JSON) và paste trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 7 nodes chính được sắp xếp cực kỳ khoa học. Các sếp cần chú ý cấu hình các node sau:

- **When clicking ‘Execute workflow’ (`manualTrigger`):** Điểm khởi chạy thủ công. Các sếp có thể thay thế bằng *Schedule Trigger* (ví dụ chạy 1 lần/tuần) nếu muốn tự động hóa hoàn toàn.
- **Get All Product Skus (`httpRequest`):** Node này gọi API đến Magento 2 để lấy danh sách toàn bộ SKU sản phẩm và thông tin hình ảnh hiện tại. Cần cấu hình chuẩn Magento Base URL và Header chứa Bearer Token.
- **Loop Over Items (`splitInBatches`):** Giúp chia nhỏ danh sách sản phẩm thành các batch nhỏ để xử lý tuần tự, tránh làm sập server Magento do request quá tải.
- **If (`if`):** Kiểm tra điều kiện xem hình ảnh sản phẩm có đang bị trống (missing) Alt Text hay không. Nếu thiếu, chuyển sang bước xử lý tiếp theo.
- **Code (`code`):** Xử lý logic Javascript để gán tên sản phẩm làm giá trị Alt Text cho hình ảnh tương ứng.
- **Split Out (`splitOut`):** Tách mảng dữ liệu hình ảnh sau khi xử lý để chuẩn bị gửi request cập nhật từng cái một.
- **HTTP Request (`httpRequest` cuối cùng):** Gửi API PUT/POST ngược lại vào Magento 2 để cập nhật Alt Text mới cho hình ảnh sản phẩm.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử với 1-2 sản phẩm mẫu để kiểm tra kết quả trên trang quản trị Magento 2.
- Sau khi test thành công, chuyển trạng thái workflow sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp lịch chạy tự động:** Thay thế node trigger thủ công bằng *Schedule Trigger* để hệ thống tự quét sản phẩm mới mỗi tuần/mỗi tháng.
- **Báo cáo qua Telegram/Slack:** Thêm một node nhắn tin ở cuối workflow để thông báo cho đội ngũ Content/SEO biết hôm nay đã tự động vá lỗi được bao nhiêu hình ảnh sản phẩm.
- **Lưu Log vào Google Sheets:** Ghi lại danh sách các SKU đã được cập nhật Alt Text để dễ dàng theo dõi và kiểm toán.

### 📌 Kết luận
Việc tối ưu SEO on-page cho hàng ngàn sản phẩm trên Magento 2 chưa bao giờ dễ dàng đến thế với n8n. Hãy áp dụng ngay workflow này để tiết kiệm hàng chục giờ công sức và giúp website thương mại điện tử của các sếp thăng hạng trên Google Images nhé!