---
title: "🚀 Tự Động Hóa Gửi Tin Nhắn WhatsApp Bulk Từ Google Sheets Với WasenderAPI – Không Cần Code!"
description: "Workflow này giúp các sếp tự động gửi **nghìn tin nhắn WhatsApp** từ Google Sheets chỉ với số điện thoại cá nhân, tiết kiệm chi phí API cao của WhatsApp Business. Hoạt động 24/7, cập nhật trạng thái tự động, và tuân thủ giới hạn API để tránh bị chặn."
slug: "tieu-dong-hoa-gui-tin-nhan-whatsapp-bulk-tu-google-sheets"
tags: [n8n, automation, no-code, whatsapp-bulk, google-sheets, wasenderapi]
keywords: [n8n workflow whatsapp, tự động hóa tin nhắn whatsapp, gửi bulk whatsapp từ google sheets, wasenderapi, tiết kiệm chi phí whatsapp api]
---

# 🚀 **Tự Động Hóa Gửi Tin Nhắn WhatsApp Bulk Từ Google Sheets – Không Cần Code!**

## **Nỗi Đau Của Các Sếp Khi Gửi Tin Nhắn WhatsApp Thủ Công**
Gửi tin nhắn WhatsApp bulk cho khách hàng, nhân viên hoặc khách hàng tiềm năng là một công việc **mệt mỏi, tốn thời gian và dễ sai sót**. Các giải pháp truyền thống như:
- **Gửi thủ công từng tin nhắn** (tốn thời gian, không hiệu quả).
- **Sử dụng WhatsApp Business API** (chi phí cao, từ **$0.005/tin nhắn** trở lên).
- **Dùng các tool third-party** (phức tạp, không linh hoạt).

**Workflow này giải quyết tất cả!** Các sếp có thể:
✅ **Gửi hàng ngàn tin nhắn WhatsApp** chỉ với **số điện thoại cá nhân** (không cần API đắt đỏ).
✅ **Tự động cập nhật trạng thái** (đã gửi, thất bại) trên Google Sheets.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.
✅ **Tuân thủ giới hạn API** của WhatsApp để tránh bị chặn.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Gửi **nghìn tin nhắn chỉ trong vài phút** thay vì nhiều giờ.
- **Tiết kiệm chi phí**: Không cần mua API WhatsApp Business (chi ~$6/tháng cho WasenderAPI).
- **Chính xác & tự động**: Không sai sót, cập nhật trạng thái ngay lập tức.
- **Hoạt động liên tục**: Workflow chạy **24/7** mà không cần người quản lý.
- **Linh hoạt**: Dễ dàng cập nhật nội dung tin nhắn từ Google Sheets.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Số điện thoại WhatsApp cá nhân** (không cần là số Business).
✔ **Tài khoản WasenderAPI** ([Đăng ký miễn phí](https://www.wasenderapi.com/)) (~$6/tháng).
✔ **Google Sheets** với **cấu trúc dữ liệu chuẩn** (hướng dẫn dưới đây).
✔ **API Key của WasenderAPI** (mua trên trang chủ).
✔ **Credentials Google Sheets OAuth2** trong n8n (cài đặt trong **n8n Settings > Credentials**).
:::

---
## **📄 Cấu Trúc Google Sheets (Mẫu Đính Kèm)**
Google Sheets phải có **3 cột chính**:
| **WhatsApp No** (Số điện thoại) | **Message** (Nội dung tin nhắn) | **Status** (Trạng thái) |
|----------------------------------|----------------------------------|--------------------------|
| +84123456789                     | "Xin chào! Đây là tin nhắn tự động từ SpaGreen." | **pending** (chờ gửi) |

> **Lưu ý**:
> - **Cột `Status` phải có giá trị `pending`** để workflow chỉ gửi tin nhắn cho những hàng chưa được xử lý.
> - **Số điện thoại phải có định dạng quốc tế** (ví dụ: `+84123456789` thay vì `0123456789`).

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow Từ File JSON 📥**
Các sếp có thể:
- **Tải workflow từ [n8n.io](https://n8n.io/workflows/6175)** và import vào n8n Editor.
- **Copy JSON dưới đây** và dán vào **n8n Editor > Import Workflow**.

```json
{
  "nodes": [
    {
      "parameters": {
        "operation": "get",
        "sheetName": "Sheet1",
        "range": "A:D",
        "filter": "Status = 'pending'"
      },
      "name": "Fetch All Pending Queries for Messaging",
      "type": "n8n-nodes-base.googleSheets",
      "credentials": {
        "googleSheetsOAuth2Api": "googleSheetsOAuth2Api"
      }
    },
    {
      "parameters": {
        "batchSize": 5,
        "mergeStrategy": "flatten"
      },
      "name": "Loop Over Items",
      "type": "n8n-nodes-base.splitInBatches"
    },
    {
      "parameters": {
        "waitTime": 5000
      },
      "name": "Wait",
      "type": "n8n-nodes-base.wait"
    },
    {
      "parameters": {
        "limit": 10
      },
      "name": "Limit",
      "type": "n8n-nodes-base.limit"
    },
    {
      "parameters": {
        "cronTime": "*/5 * * * *"
      },
      "name": "Trigger Every 5 Minute",
      "type": "n8n-nodes-base.scheduleTrigger"
    },
    {
      "parameters": {
        "method": "post",
        "url": "https://app.wasenderapi.com/api/send-message",
        "headers": {
          "Content-Type": "application/json",
          "Authorization": "{{ $credentials.httpBearerAuth.token }}"
        },
        "body": {
          "type": "json",
          "json": {
            "number": "{{ $node["Loop Over Items"].json["WhatsApp No"] }}",
            "message": "{{ $node["Loop Over Items"].json["Message"] }}"
          }
        }
      },
      "name": "Send Message Using HTTP Request",
      "type": "n8n-nodes-base.httpRequest",
      "credentials": {
        "httpBearerAuth": "httpBearerAuth"
      }
    },
    {
      "parameters": {
        "operation": "update",
        "sheetName": "Sheet1",
        "range": "A:D",
        "updateValues": {
          "Status": "sent"
        }
      },
      "name": "Change State of Rows in Sent",
      "type": "n8n-nodes-base.googleSheets",
      "credentials": {
        "googleSheetsOAuth2Api": "googleSheetsOAuth2Api"
      }
    }
  ],
  "connections": {
    "googleSheets1": ["splitInBatches1"],
    "splitInBatches1": ["wait1"],
    "wait1": ["httpRequest1"],
    "httpRequest1": ["googleSheets2"],
    "scheduleTrigger1": ["googleSheets1"]
  }
}
```

---
### **2. Các Bước Cấu Hình Quan Trọng 📌**

#### **🔹 Node 1: Fetch All Pending Queries (Lấy Dữ liệu Chờ Gửi)**
- **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cài đặt trước).
- **Sheet Name**: Nhập tên sheet (ví dụ: `Sheet1`).
- **Range**: `A:D` (các cột chứa dữ liệu).
- **Filter**: `Status = 'pending'` (chỉ lấy hàng có trạng thái `pending`).

#### **🔹 Node 2: Loop Over Items (Lặp Qua Các Hàng)**
- **Batch Size**: Đặt **5 hàng/lần** (giúp tránh bị chặn bởi WhatsApp).
- **Merge Strategy**: `flatten` (để dữ liệu được truyền tiếp tục).

#### **🔹 Node 3: Wait (Đợi 5 Giây Trước Mỗi Tin Nhắn)**
- **Wait Time**: **5000ms** (5 giây) để tránh bị chặn bởi WhatsApp.

#### **🔹 Node 4: Limit (Giới Hạn Số Lượng Tin Nhắn)**
- **Limit**: **10 tin nhắn/lần** (để an toàn).

#### **🔹 Node 5: Send Message Using HTTP Request (Gửi Tin Nhắn)**
- **Method**: `POST`.
- **URL**: `https://app.wasenderapi.com/api/send-message`.
- **Headers**:
  - `Content-Type: application/json`
  - `Authorization: Bearer {{ API_KEY }}` (điền **API Key của WasenderAPI** vào **Credentials** trong n8n).
- **Body (JSON)**:
  ```json
  {
    "number": "{{ $node["Loop Over Items"].json["WhatsApp No"] }}",
    "message": "{{ $node["Loop Over Items"].json["Message"] }}"
  }
  ```
  - **Lưu ý**: Đảm bảo **API Key** được đặt trong **Credentials** (`httpBearerAuth`) trong **n8n Settings > Credentials**.

#### **🔹 Node 6: Change State of Rows in Sent (Cập Nhật Trạng Thái)**
- **Credentials**: `googleSheetsOAuth2Api`.
- **Operation**: `update`.
- **Range**: `A:D`.
- **Update Values**:
  - `Status: sent` (cập nhật trạng thái thành `sent` sau khi gửi thành công).

#### **🔹 Node 7: Trigger Every 5 Minute (Khởi Động Lặp Lại Mỗi 5 Phút)**
- **Cron Time**: `*/5 * * * *` (chạy mỗi 5 phút).

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với **dữ liệu mẫu** để kiểm tra:
   - Tin nhắn có được gửi thành công không?
   - Trạng thái trên Google Sheets có được cập nhật không?
2. **Bật Active** workflow để nó chạy tự động mỗi 5 phút.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[MỘT SỐ Ý TƯỞNG TIẾP THEO]
- **Gửi báo cáo định kỳ**: Sử dụng **n8n-nodes-base.email** hoặc **Slack** để thông báo khi workflow hoàn thành.
- **Lưu log gửi tin nhắn**: Thêm **n8n-nodes-base.chronolog** để theo dõi lịch sử gửi.
- **Kết hợp với CRM**: Nếu sử dụng **HubSpot, Zoho CRM**, có thể tự động lấy danh sách khách hàng từ đó.
- **Tự động gửi tin nhắn nhắc nhở**: Ví dụ, gửi tin nhắn nhắc nhở khách hàng về đơn hàng sau 3 ngày.
- **Dùng Telegram/Slack báo lỗi**: Thêm **n8n-nodes-base.telegram** hoặc **n8n-nodes-base.slack** để thông báo khi có lỗi.
:::

---
## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc gửi tin nhắn WhatsApp thủ công, đồng thời **tiết kiệm chi phí API** so với các giải pháp truyền thống. **Chỉ cần 10 phút setup**, workflow sẽ hoạt động **24/7**, tự động gửi tin nhắn và cập nhật trạng thái.

**👉 Hãy áp dụng ngay và tự động hóa công việc của mình!**

---
### **🔥 Cài Đặt Hạ Tầng Cho n8n (Self-Hosted) – Để Workflow Chạy 24/7**
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định **không bị gián đoạn**, các sếp nên **self-host n8n** trên **VPS** thay vì dùng phiên bản miễn phí trên cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**).
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho n8n + WasenderAPI).

**Lợi ích**:
✔ **Không bị giới hạn tài nguyên** (so với phiên bản cloud).
✔ **Chạy 24/7** mà không bị ngắt kết nối.
✔ **An toàn và riêng tư** (không cần lo về dữ liệu).
:::

---
**🚀 Bắt đầu tự động hóa ngay hôm nay!** 🚀