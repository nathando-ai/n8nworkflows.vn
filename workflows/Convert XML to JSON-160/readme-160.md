---
title: "🚀 Convert XML to JSON – Tự động chuyển đổi XML sang JSON nhanh chóng"
description: "Chuyển đổi dữ liệu XML sang JSON một cách nhanh chóng, chính xác, giúp tiết kiệm thời gian và giảm lỗi trong quy trình xử lý dữ liệu."
slug: "convert-xml-to-json"
tags: [n8n, automation, no-code, xml, json, data-processing]
keywords: [n8n workflow, tự động hóa, chuyển đổi XML sang JSON, dữ liệu, no-code]
---

# 🚀 Convert XML to JSON – Tự động chuyển đổi XML sang JSON nhanh chóng

Bạn đang phải xử lý hàng trăm dòng XML mỗi ngày, chuyển đổi thủ công sang JSON để nhập vào hệ thống khác? Việc này không chỉ tốn thời gian mà còn dễ gây lỗi. Workflow **Convert XML to JSON** của n8n giúp bạn thực hiện công việc này chỉ với một cú nhấp chuột, hoàn toàn không cần viết code.

:::info[Hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Chuyển đổi ngay khi nhấn nút, không cần thao tác thủ công.  
- **Độ chính xác cao**: Tránh lỗi nhập liệu, dữ liệu JSON luôn đồng nhất.  
- **Tự động hoá 100%**: Không cần lập trình, chỉ cần cấu hình một vài trường.  
- **Dễ dàng mở rộng**: Thêm bước gửi email, Slack, hoặc lưu trữ vào Google Sheet chỉ vài click.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Không cần tài khoản hoặc API key**: Workflow này chỉ sử dụng các node nội bộ của n8n.  
- **Dữ liệu XML mẫu**: Bạn có thể copy vào node Set dưới dạng chuỗi.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow từ trang gốc: <https://n8n.io/workflows/160> hoặc copy nội dung JSON.  
2. Mở n8n Editor → **Import** → **Import from JSON** → dán nội dung JSON.  
3. Nhấn **Import** và workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên | Mô tả | Cấu hình cần chỉnh |
|------|-----|-------|---------------------|
| 1 | **On clicking 'execute'** | `manualTrigger` | Không cần cấu hình thêm. |
| 2 | **Set** | Định nghĩa dữ liệu XML cần chuyển đổi. | - Trong tab **Values**: chọn **Add Value** → **Add Expression** → nhập chuỗi XML (hoặc tham chiếu tới trường dữ liệu). |
| 3 | **XML** | Chuyển đổi XML thành JSON. | - **Operation**: `XML to JSON` (đã được chọn mặc định). <br> - **XML**: chọn trường chứa XML (thường là `{{ $json["xml"] }}` nếu bạn đặt tên trường là `xml`). |

> **Tip**: Đặt tên trường trong node Set là `xml` để dễ tham chiếu trong node XML.

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn nút **Execute Workflow** trong n8n Editor, nhập dữ liệu XML mẫu vào node Set, xem kết quả JSON trong node XML.  
2. **Bật Active**: Sau khi xác nhận kết quả đúng, chuyển trạng thái workflow sang **Active** để tự động chạy khi có trigger.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi kết quả qua Email**: Thêm node `Send Email` sau node XML, cấu hình SMTP và gửi JSON dưới dạng attachment hoặc nội dung body.  
- **Thông báo Slack**: Thêm node `Slack` để gửi tin nhắn kèm JSON vào kênh.  
- **Lưu trữ vào Google Sheet**: Sử dụng node `Google Sheets` để ghi dữ liệu JSON vào bảng tính, giúp theo dõi lịch sử chuyển đổi.  
- **Lưu log**: Thêm node `Write Binary File` để lưu JSON vào file trên server, tiện cho audit trail.  

### 📌 Kết luận
Workflow **Convert XML to JSON** là công cụ đơn giản nhưng mạnh mẽ giúp các sếp tiết kiệm thời gian, giảm lỗi và tăng tính tự động hoá trong quy trình xử lý dữ liệu. Hãy thử ngay, và nếu muốn mở rộng, chỉ cần thêm một vài node nữa – không cần viết code!