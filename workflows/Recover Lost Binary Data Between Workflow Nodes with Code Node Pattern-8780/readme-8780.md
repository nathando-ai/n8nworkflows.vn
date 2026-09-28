---
title: "🔄 **Khôi phục Dữ liệu Nhị phân "Mất" Trong Workflow n8n - Kỹ Thuật Code Node Chuyên Nghiệp**"
description: "Hướng dẫn chi tiết cách khôi phục dữ liệu nhị phân (ảnh, PDF, file) trong workflow n8n khi bị mất giữa các node, giúp các sếp tự động hóa xử lý file một cách hoàn chỉnh mà không cần code phức tạp."
slug: "khoi-phuc-du-lieu-nhi-phan-trong-workflow-n8n"
tags: [n8n, automation, no-code, xử lý dữ liệu nhị phân, kỹ thuật code node]
keywords: [n8n khôi phục binary data, tự động hóa xử lý file, lưu trữ dữ liệu nhị phân, n8n code node, giải pháp không code]
---

# 🔄 **Khôi phục Dữ liệu Nhị phân "Mất" Trong Workflow n8n - Kỹ Thuật Code Node Chuyên Nghiệp**

## 🚨 **Nỗi Đau Của Các Sếp Khi Xử Lý File Nhị Phân**
Trong quá trình tự động hóa, các sếp thường gặp vấn đề khi xử lý **ảnh, PDF, hoặc file nhị phân** giữa các node trong workflow n8n. Nhiều node mặc định **không truyền dữ liệu nhị phân** sang node tiếp theo, dẫn đến:
- **Dữ liệu mất** giữa các bước xử lý.
- **Không thể sử dụng** file đã tải xuống hoặc xử lý ở bước trước.
- **Phải tải lại từ đầu**, gây lãng phí thời gian và tài nguyên.

Workflow này **giải quyết vấn đề này hoàn toàn bằng code node**, giúp các sếp **khôi phục và tái sử dụng dữ liệu nhị phân** ngay cả khi nó bị "xóa" bởi node giữa chừng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Khôi phục dữ liệu nhị phân** ngay cả khi bị mất giữa các node.
- **Xử lý file một cách liên tục** (ảnh, PDF, video) mà không cần tải lại.
- **Tiết kiệm thời gian** và giảm thiểu lỗi do dữ liệu bị mất.
- **Áp dụng cho mọi loại file nhị phân**, từ logo công ty đến tài liệu kỹ thuật.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản n8n** (cài đặt trên máy chủ hoặc VPS).
2. **Khả năng truy cập API** (nếu cần kết nối với nguồn dữ liệu bên ngoài).
3. **Hiểu cơ bản về code node** (sẽ có hướng dẫn chi tiết dưới đây).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
```json
{
  "nodes": {
    "1": {
      "parameters": {},
      "name": "Start",
      "type": "manualTrigger",
      "typeVersion": 1,
      "position": {
        "x": 200,
        "y": 200
      }
    },
    "2": {
      "parameters": {
        "method": "GET",
        "url": "https://n8n.io/logo.png"
      },
      "name": "Get n8n Logo (Binary)",
      "type": "httpRequest",
      "typeVersion": 1,
      "position": {
        "x": 200,
        "y": 400
      }
    },
    "3": {
      "parameters": {
        "operation": "set",
        "property": "binaryData",
        "values": "=null"
      },
      "name": "Remove Binary Data",
      "type": "set",
      "typeVersion": 1,
      "position": {
        "x": 400,
        "y": 400
      }
    },
    "4": {
      "parameters": {
        "code": "const previousNodeName = \"Get n8n Logo (Binary)\";\nconst previousNodeData = $(previousNodeName).item;\nthis.helpers.prepareBinaryData(previousNodeData);"
      },
      "name": "Re-Access Binary Data from Previous Node",
      "type": "code",
      "typeVersion": 1,
      "position": {
        "x": 600,
        "y": 400
      }
    }
  },
  "connections": {
    "manualTrigger_1": {
      "destination": "httpRequest_2",
      "source": "trigger"
    },
    "httpRequest_2": {
      "destination": "set_3",
      "source": "json"
    },
    "set_3": {
      "destination": "code_4",
      "source": "main"
    }
  }
}
```

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này bao gồm **4 node chính**, mỗi node có vai trò riêng:
| **Node** | **Loại Node** | **Mô Tả** |
|----------|--------------|------------|
| **Start** | `manualTrigger` | Khởi động workflow thủ công. |
| **Get n8n Logo (Binary)** | `httpRequest` | Tải logo n8n (dữ liệu nhị phân) từ URL. |
| **Remove Binary Data** | `set` | **Xóa dữ liệu nhị phân** để mô phỏng trường hợp "mất dữ liệu". |
| **Re-Access Binary Data** | `code` | **Khôi phục dữ liệu nhị phân** từ node trước đó. |

##### **Cách Cấu Hình Node `code` (Quá Trình "Magic")**
Node này sử dụng **cú pháp đặc biệt** để lấy lại dữ liệu nhị phân từ node trước:
```javascript
const previousNodeName = "Get n8n Logo (Binary)"; // Tên node chứa dữ liệu nhị phân
const previousNodeData = $(previousNodeName).item; // Lấy toàn bộ dữ liệu từ node đó
this.helpers.prepareBinaryData(previousNodeData); // Khôi phục dữ liệu nhị phân
```
- **`$(previousNodeName).item`**: Lấy toàn bộ item từ node trước đó.
- **`this.helpers.prepareBinaryData()`**: Chuẩn bị lại dữ liệu nhị phân cho node hiện tại.

:::warning[LƯU Ý QUAN TRỌNG]
- **Không thay đổi tên node** trong code nếu muốn workflow hoạt động ổn định.
- **Nếu muốn áp dụng cho node khác**, chỉ cần thay đổi `previousNodeName` thành tên node chứa dữ liệu nhị phân.
:::

#### **3. Kích Hoạt ⚡️**
1. **Chạy thử (Test Run)**:
   - Nhấn **Run Workflow** để kiểm tra dữ liệu nhị phân có được khôi phục không.
   - Kiểm tra output của node `Re-Access Binary Data` để xem dữ liệu đã được tái sử dụng.
2. **Bật Active**:
   - Sau khi test thành công, bật **Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Áp dụng cho file PDF/Ảnh**:
   - Thay đổi URL trong node `httpRequest` để tải file khác (ví dụ: `https://tino.vn/logo.pdf`).
2. **Lưu log dữ liệu**:
   - Thêm node `stickyNote` hoặc `set` để lưu lại dữ liệu nhị phân vào cơ sở dữ liệu (Supabase, Google Sheets).
3. **Kết hợp với Slack/Telegram**:
   - Sau khi khôi phục dữ liệu, gửi thông báo đến Slack/Telegram bằng node `slack` hoặc `telegramBot`.
4. **Tự động hóa báo cáo định kỳ**:
   - Sử dụng node `setSchedule` để chạy workflow hàng ngày/tuần để xử lý file mới.

---

### 📌 **Kết Luận**
Workflow này **giải quyết vấn đề mất dữ liệu nhị phân** trong n8n một cách **đơn giản và hiệu quả**, giúp các sếp tự động hóa xử lý file một cách **liên tục và không cần code phức tạp**. **Hãy áp dụng ngay** để tiết kiệm thời gian và tăng hiệu suất!

:::success[Hành Động Tiếp Theo]
- **Thử nghiệm workflow** trên môi trường test trước khi áp dụng vào sản phẩm thực tế.
- **Tùy chỉnh URL và node** để phù hợp với dự án của các sếp.
- **Đăng ký VPS** để chạy workflow 24/7 (liên kết dưới đây).
:::

---
**Happy Automating!** 🚀