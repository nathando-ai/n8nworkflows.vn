---
title: "🚀 Tự Động Hóa Xử Lý Đơn Hàng + Kiểm Tra Kho + Thông Báo Slack (N8n + Google Sheets)"
description: "Giải pháp tự động hóa 100% không code để kiểm tra tồn kho thực thời, phát hiện thiếu hàng ngay lập tức, và thông báo tự động cho quản lý qua Slack. Giảm thiểu rủi ro thiếu hàng và tối ưu hóa quy trình bán hàng."
slug: "tieu-dong-hoa-xu-ly-don-hang-kiem-tra-kho-slack"
tags: [n8n, automation, ecommerce, crm, google-sheets, slack, logistics]
keywords: [n8n workflow đơn hàng, tự động hóa kiểm tra tồn kho, alert thiếu hàng Slack, n8n google sheets, tự động hóa bán hàng không code]
---

# 🚀 **Tự Động Hóa Xử Lý Đơn Hàng, Kiểm Tra Tồn Kho & Thông Báo Slack (N8n + Google Sheets)**

### **Nỗi Đau Của Các Sếp?**
Hàng ngày, các sếp phải:
✅ **Kiểm tra thủ công** tồn kho sau mỗi đơn hàng mới → Tốn thời gian, dễ lỡ sót.
✅ **Phản hồi chậm** khi khách hàng đặt hàng sản phẩm hết hàng → Mất uy tín, giảm doanh thu.
✅ **Không theo dõi lịch sử** xử lý đơn hàng → Khó phân tích và cải tiến quy trình.

**Workflow này giải quyết tất cả!** Với **n8n**, các sếp có thể tự động:
✔ **Nhận đơn hàng** từ website, app, hoặc API.
✔ **Kiểm tra tồn kho** ngay lập tức từ Google Sheets.
✔ **Phát cảnh báo Slack** khi thiếu hàng (hoặc thành công).
✔ **Lưu log toàn bộ quá trình** để theo dõi và phân tích.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5+ giờ/ngày** kiểm tra tồn kho thủ công.
- **Giảm thiểu rủi ro thiếu hàng** với cảnh báo tự động.
- **Cải thiện trải nghiệm khách hàng** bằng phản hồi nhanh chóng.
- **Lưu trữ log toàn bộ** để phân tích và tối ưu hóa.
- **Hoạt động 24/7** mà không cần can thiệp người dùng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản n8n Self-hosted** (để workflow hoạt động liên tục).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **Google Sheets** với cấu trúc dữ liệu tồn kho (sử dụng mẫu [WMS Data Demo](https://docs.google.com/spreadsheets/d/1sgTaHwbTWrVCDiSwuvqFVJr0-Ez2t3LTlJaLU4cBcuU/edit?usp=sharing)).
   - **Quyền truy cập**: Cấp quyền cho n8n (n8n-nodes-base.googleSheets) để đọc/thêm dữ liệu.

3. **Tài khoản Slack** với **channel "warehouse"** (hoặc cập nhật tên channel trong node Slack).
   - **Credentials**: API Key của Slack (tạo từ [Slack API](https://api.slack.com/apps)).

4. **Webhook URL** từ n8n (sẽ được tạo tự động khi import workflow).
   - Các sếp cần **cấu hình API endpoint** trên hệ thống bán hàng (website, app, CRM) để gửi dữ liệu đơn hàng đến URL này.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/10899](https://n8n.io/workflows/10899) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **13 node** quan trọng, các sếp cần cấu hình kỹ lưỡng:

##### **A. Node Webhook (Order Webhook)**
- **Định danh**: `ecom-order` (đường dẫn API).
- **Phương thức**: `POST`.
- **Lưu ý**:
  - Sau khi import, **copy URL Webhook** từ node này và **cấu hình trên hệ thống bán hàng** (website, app) để gửi đơn hàng.
  - **Dữ liệu mẫu** phải theo format JSON:
    ```json
    {
      "id": "ORDER1001",
      "customer": {
        "name": "Customer",
        "email": "customer@example.com"
      },
      "items": [
        {
          "sku": "SKU001",
          "quantity": 2,
          "name": "Product A",
          "price": 5000
        },
        {
          "sku": "SKU002",
          "quantity": 2,
          "name": "Product C",
          "price": 10000
        }
      ],
      "total": 30000
    }
    ```

##### **B. Node Google Sheets (Get Inventories & Save logs)**
- **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước khi import).
- **Node `Get Inventories`**:
  - **Operation**: `lookup` (tìm kiếm tồn kho theo SKU).
  - **Sheet Name**: Đảm bảo tên sheet trong Google Sheets **khớp với cấu trúc** trong node `Mapping data`.
- **Node `Save logs`**:
  - **Operation**: `append` (thêm log mới vào sheet).
  - **Sheet Name**: Sử dụng sheet khác (ví dụ: `Order_Logs`) để lưu lịch sử.

##### **C. Node Slack (Slack notification)**
- **Credentials**: Chọn `slackOAuth2Api`.
- **Channel**: Đặt tên channel là `warehouse` (hoặc cập nhật trong node).
- **Message Template**:
  - **Thành công**: `✅ Order #{{$node["Order Webhook"].json["id"]}} processed successfully!`
  - **Thiếu hàng**: `⚠️ Stock shortage for {{$node["Item and quantity"].json["name"]}} (SKU: {{$node["Item and quantity"].json["sku"]}}).`

##### **D. Node If (enough stock?)**
- **Cấu hình điều kiện**:
  - Nếu `available_quantity >= ordered_quantity` → Chuyển sang branch **OK**.
  - Nếu `available_quantity < ordered_quantity` → Chuyển sang branch **Stock shortage**.

##### **E. Node Function (Check Order, Request Info, Create Invoice, Logs)**
- Các node này **không cần chỉnh sửa** (đã viết sẵn logic trong workflow).
- **Lưu ý**:
  - Node `Create Invoice` sẽ tự động tính tổng tiền từ `total` trong đơn hàng.
  - Node `create data logs` sẽ ghi chi tiết vào Google Sheets.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Gửi **dữ liệu mẫu** (JSON trên) đến Webhook để kiểm tra.
   - Kiểm tra:
     - Slack có thông báo không?
     - Google Sheets có log không?
     - Tồn kho có được kiểm tra chính xác không?

2. **Bật Active**:
   - Sau khi test thành công, **bật Active** workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CẢNH BÁO & TIẾP CẬN]
- **Kết hợp với CRM**: Nếu sử dụng Shopify, WooCommerce, hoặc BigCommerce, các sếp có thể **tích hợp Webhook từ hệ thống này** thay vì gửi thủ công.
- **Lưu log chi tiết hơn**: Thêm cột `status` (Đơn hàng thành công/thất bại) và `timestamp` vào Google Sheets.
- **Gửi báo cáo hàng ngày**: Sử dụng **n8n + Google Sheets + Email** để tự động gửi báo cáo tồn kho cho quản lý.
- **Thêm AI Chatbot**: Kết hợp với **n8n + LLM** (ví dụ: Mistral, Llama) để tự động trả lời khách hàng khi hàng hết.
- **Backup dữ liệu**: Đặt lịch **backup Google Sheets** hàng tuần để tránh mất dữ liệu.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc kiểm tra tồn kho thủ công, đồng thời **giảm thiểu rủi ro thiếu hàng** với cảnh báo tự động. **Chỉ cần 10 phút cấu hình**, các sếp đã có một hệ thống **tự động hóa hoàn chỉnh** cho quản lý đơn hàng và kho hàng.

**Hành động ngay!**
1. **Cài đặt n8n Self-hosted** trên VPS (để workflow hoạt động 24/7).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test với dữ liệu mẫu** và bật Active.

**🚀 N8n không chỉ tự động hóa, mà còn tối ưu hóa toàn bộ quy trình bán hàng của các sếp!**