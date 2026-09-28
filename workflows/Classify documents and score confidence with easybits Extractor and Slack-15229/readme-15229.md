---
title: "📄 **Tự Động Hóa Phân Loại & Đánh Giá Độ Tin Cậy Tài Liệu với easybits + Slack (Không Cần Code!)**"
description: "Giải pháp tự động hóa phân loại tài liệu (PDF/PNG/JPEG) với độ chính xác cao và đánh giá độ tin cậy tự động, chỉ gửi tài liệu nghi ngờ đến Slack để kiểm tra thủ công. Tiết kiệm thời gian và giảm sai sót trong xử lý tài liệu hàng ngày."
slug: "tu-dong-hoa-phan-loai-tai-lieu-easybits-slack"
tags: [n8n, automation, document-extraction, ai-summarization, easybits, slack-integration]
keywords: [n8n workflow phân loại tài liệu, tự động hóa xử lý PDF, AI đánh giá độ tin cậy, easybits n8n, tự động hóa Slack]
---

# 🚀 **Phân Loại Tài Liệu & Đánh Giá Độ Tin Cậy Tự Động với easybits + Slack**

## **Nỗi Đau Của Các Sếp Trong Xử Lý Tài Liệu**
Hàng ngày, các sếp và nhân viên phải mất **giờ đồng hồ** để:
- **Phân loại hàng trăm tài liệu** (hoá đơn y tế, hoá đơn nhà hàng, hoá đơn khách sạn,...) thủ công.
- **Đánh giá độ tin cậy** của kết quả phân loại từ AI, không biết liệu mô hình có chắc chắn hay chỉ đoán.
- **Lưu trữ sai loại** hoặc bỏ qua tài liệu quan trọng do phân loại không chính xác.
- **Phải kiểm tra lại** mỗi tài liệu nghi ngờ, gây lãng phí thời gian và tăng chi phí vận hành.

**Giải pháp này giúp:**
✅ **Phân loại tự động** tài liệu (PDF/PNG/JPEG) với **5 loại chính** (hoá đơn y tế, nhà hàng, khách sạn, thương mại, viễn thông).
✅ **Đánh giá độ tin cậy** (confidence score từ 0.0 đến 1.0) để **lọc bỏ tài liệu không chắc chắn**.
✅ **Gửi tài liệu nghi ngờ** tự động về **Slack** để kiểm tra thủ công.
✅ **Tiết kiệm 80% thời gian** so với cách làm thủ công.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quá trình phân loại** tài liệu, không cần viết code.
- **Độ chính xác cao** nhờ đánh giá độ tin cậy tự động (chỉ tiếp nhận tài liệu có confidence ≥ 0.5).
- **Giảm sai sót** bằng cách chỉ gửi tài liệu nghi ngờ đến Slack (không bỏ qua tài liệu quan trọng).
- **Hoạt động 24/7** trên VPS, không phụ thuộc vào nhân viên.
- **Kết hợp dễ dàng** với Google Drive, Sheets, hoặc các hệ thống ERP khác.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản easybits Extractor**:
   - [Đăng ký miễn phí](https://extractor.easybits.tech/) và tạo **Pipeline mới**.
   - **API Key** và **Pipeline ID** (tìm trong trang quản lý pipeline).
2. **Tài khoản Slack**:
   - **Workspace Slack** và **API Token** (tạo từ [API Slack](https://api.slack.com/apps)).
   - **Channel/Người dùng** để nhận thông báo (ví dụ: `#finance-review`).
3. **VPS cho n8n** (khuyến nghị):
   - Để workflow chạy liên tục 24/7, các sếp nên **self-host n8n** trên VPS.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---
## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow từ File JSON**
:::note[HƯỚNG DẪN CHI TIẾT]
1. **Tải workflow** từ [n8n.io/workflows/15229](https://n8n.io/workflows/15229) (chọn **Export as JSON**).
2. **Mở n8n Editor** (trên VPS hoặc n8n Cloud).
3. **Nhấp vào "Import"** → Dán JSON vào và chọn **Import**.
4. **Tên workflow**: Giữ nguyên hoặc đổi thành **"Phân Loại Tài Liệu + Slack Review"**.
:::

### **2. Cấu Hình Cần Thiết (BẮT BUỘC)**
Sau khi import, các sếp phải **cấu hình 3 node chính**:

#### **A. Node `easybits: Classify & Score`**
- **Tham số cần điền**:
  - **Credentials**: Chọn `easybitsExtractorApi` (tạo mới nếu chưa có).
  - **Pipeline ID**: Copy từ trang quản lý pipeline easybits.
  - **API Key**: Copy từ easybits và dán vào `apiKey`.
  - **File**: Chọn `file` từ node **Form Trigger** (không cần chuyển đổi Base64).
- **Lưu ý**:
  - Nếu **self-hosted**, cài node `@easybits/n8n-nodes-extractor` từ **Settings → Community Nodes**.

#### **B. Node `IF: Empty or Low Confidence`**
- **Cấu hình điều kiện**:
  - **Condition 1**: `document_class` **is empty** (mô hình không phân loại được).
  - **Condition 2**: `confidence_score` **less than 0.5** (mô hình không chắc chắn).
  - **Logic**: **OR** (nếu **bất kỳ điều kiện nào** xảy ra, tài liệu sẽ được gửi Slack).

#### **C. Node `Slack: Notify – Needs Review`**
- **Tham số cần điền**:
  - **Credentials**: Chọn `slackApi` (tạo mới với **Token OAuth** từ Slack).
  - **Channel**: Nhập `#finance-review` (hoặc channel khác).
  - **Message Template**:
    ```json
    {
      "blocks": [
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "*Tài liệu cần kiểm tra* 🚨"
          }
        },
        {
          "type": "divider"
        },
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "📄 Loại tài liệu: <{document_class}|{document_class}> (Độ tin cậy: {confidence_score})"
          }
        },
        {
          "type": "actions",
          "elements": [
            {
              "type": "button",
              "text": {
                "type": "plain_text",
                "text": "Xem tài liệu"
              },
              "url": "{file_url}"
            }
          ]
        }
      ]
    }
    ```
  - **Thay thế `{file_url}`** bằng URL tải tài liệu (ví dụ: từ Google Drive).

---
### **3. Kích Hoạt Workflow**
1. **Test Run**:
   - Nhấp **Run Workflow** và upload một tài liệu mẫu (PDF/PNG/JPEG).
   - Kiểm tra **Output** để đảm bảo:
     - Tài liệu **chính xác** → **tiếp tục workflow**.
     - Tài liệu **nghi ngờ** → **được gửi Slack**.
2. **Bật Active**:
   - Nhấp **Active** ở góc trên bên phải.
3. **Chia sẻ Link Form**:
   - Copy **URL của Form Trigger** và gửi cho nhân viên upload tài liệu.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH LÀM TIẾP THEO]
1. **Lưu log vào Google Sheets**:
   - Thêm node **Google Sheets** sau `Continue Workflow` để ghi lại tất cả tài liệu đã phân loại thành công.
2. **Kết hợp với Google Drive**:
   - Sử dụng node **Google Drive** để tự động lưu tài liệu vào thư mục tương ứng (`medical_invoices/`, `hotel_invoices/`...).
3. **Báo cáo định kỳ**:
   - Thêm node **Email** hoặc **Slack** để gửi báo cáo hàng tuần về số lượng tài liệu đã xử lý và số lượng tài liệu cần review.
4. **Cập nhật danh sách loại tài liệu**:
   - Nếu cần thêm loại mới (ví dụ: `tax_invoice`), cập nhật **prompt** trong easybits và retrain pipeline.
5. **Tự động xóa tài liệu sau review**:
   - Sử dụng node **Slack** để nhận phản hồi từ người review (ví dụ: "Xóa tài liệu này") và kết nối với node **Delete File** (nếu lưu trên Google Drive).
:::

---
## 📌 **Kết Luận & Kêu Gọi Áp Dụng**
Workflow này **giải quyết triệt để** vấn đề phân loại tài liệu thủ công, giúp các sếp:
✔ **Tiết kiệm 80% thời gian** trong việc xử lý tài liệu.
✔ **Giảm sai sót** nhờ đánh giá độ tin cậy tự động.
✔ **Tự động hóa review** với Slack, không phụ thuộc vào nhân viên.
✔ **Kết nối dễ dàng** với các hệ thống khác (Google Drive, ERP, CRM...).

**Hành động ngay hôm nay**:
1. **Đăng ký VPS** để self-host n8n (nếu chưa có).
2. **Import workflow** và cấu hình easybits + Slack.
3. **Test với 10 tài liệu mẫu** để đảm bảo hoạt động ổn định.
4. **Chia sẻ link form** cho nhân viên và **bắt đầu tự động hóa**!

---
**💡 Cần hỗ trợ?**
- **Trang hỗ trợ n8n**: [docs.n8n.io](https://docs.n8n.io/)
- **Community easybits**: [extractor.easybits.tech](https://extractor.easybits.tech/)
- **Góp ý**: Để lại comment dưới bài viết này!