---
title: "🚀 Tự động tạo liên hệ mới trong Agile CRM chỉ với 1 click"
description: "Giải pháp tự động hóa 100% không cần code giúp doanh nghiệp tạo liên hệ mới trong Agile CRM nhanh chóng và chính xác."
slug: "tua-dong-tao-lien-he-moi-trong-agile-crm"
tags: [n8n, automation, no-code, agile-crm, sales]
keywords: [n8n workflow, tự động hóa, Agile CRM, tạo liên hệ, bán hàng]
---

# 🚀 Tự động tạo liên hệ mới trong Agile CRM chỉ với 1 click

Bạn đang phải nhập thủ công hàng trăm liên hệ vào Agile CRM mỗi ngày? Mỗi lần nhập sai một trường dữ liệu, bạn sẽ mất thời gian chỉnh sửa và rủi ro mất dữ liệu quan trọng. Workflow này sẽ giúp bạn **đưa quy trình tạo liên hệ vào Agile CRM lên 100% tự động** – không cần viết code, chỉ cần nhấn nút “Execute” và dữ liệu sẽ được gửi ngay tới hệ thống CRM của bạn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 <https://tino.vn/vps-n8n?affid=388> (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 <https://my.bnix.one/aff.php?aff=172> (VPS Xeon 4GB chỉ 50k/tháng)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài phút nhập thủ công xuống vài giây tự động.  
- **Độ chính xác cao**: Không còn lỗi nhập dữ liệu do con người.  
- **Tích hợp linh hoạt**: Dễ dàng kết nối với các nguồn dữ liệu khác (Google Sheets, Slack, Email).  
- **Hoạt động liên tục**: Khi workflow được kích hoạt, nó sẽ chạy bất cứ khi nào có dữ liệu mới.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Tài khoản Agile CRM**: Đăng ký tại <https://www.agilecrm.com/>.  
- **API Key**: Tạo API Key trong phần *Settings → API* của Agile CRM.  
- **Credentials n8n**: Tạo credential `agileCrmApi` trong n8n với API Key vừa lấy.  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON của workflow từ <https://n8n.io/workflows/474> hoặc sao chép nội dung JSON.  
2. Mở **n8n Editor**, chọn **Import** → **Import from JSON** và dán nội dung.  
3. Nhấn **Import** để workflow xuất hiện trong danh sách workflow.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên node | Hướng dẫn cấu hình |
|------|----------|---------------------|
| 1 | **On clicking 'execute'** | Đây là node *manualTrigger*. Không cần cấu hình gì thêm. Khi bạn nhấn nút **Execute Workflow** trong n8n, node này sẽ kích hoạt workflow. |
| 2 | **AgileCRM** | - **Credentials**: Chọn credential `agileCrmApi` đã tạo. <br>- **Operation**: Đã được đặt sẵn là **create**. <br>- **Data**: Node này sẽ nhận dữ liệu từ node trước (manualTrigger). Bạn có thể thêm *Set* node giữa để định dạng dữ liệu (ví dụ: `firstName`, `lastName`, `email`). |

> **Tip**: Nếu muốn gửi dữ liệu từ một nguồn khác (ví dụ Google Sheets), hãy chèn một node *Google Sheets* trước *AgileCRM* và cấu hình trường dữ liệu tương ứng.

### 3. Kích hoạt ⚡️

1. **Test run**: Nhấn nút **Execute Workflow** trong n8n, nhập dữ liệu mẫu (ví dụ: `firstName: "Nguyễn", lastName: "Văn A", email: "vana@example.com"`).  
2. Kiểm tra kết quả trong Agile CRM – liên hệ mới sẽ xuất hiện.  
3. Khi mọi thứ ổn, bật **Active** cho workflow để nó tự động chạy khi có dữ liệu mới.

## ✍️ Mẹo & gợi ý nâng cao

- **Gửi email xác nhận**: Thêm node *Email* sau *AgileCRM* để gửi email cho khách hàng khi liên hệ được tạo.  
- **Thông báo Slack**: Thêm node *Slack* để gửi tin nhắn vào kênh khi liên hệ mới được thêm.  
- **Lưu log vào Google Sheets**: Thêm node *Google Sheets* để ghi lại thông tin liên hệ đã tạo, giúp theo dõi lịch sử.  
- **Kết hợp với Zapier**: Nếu bạn muốn mở rộng quy trình, có thể kết nối n8n với Zapier để kích hoạt các workflow khác.  

## 📌 Kết luận

Workflow “Create a new contact in Agile CRM” là một công cụ đơn giản nhưng mạnh mẽ, giúp doanh nghiệp giảm thiểu công việc thủ công, tăng độ chính xác và tối ưu thời gian. Hãy **đưa nó vào thực tiễn ngay hôm nay** và cảm nhận sự khác biệt trong quy trình bán hàng của mình!