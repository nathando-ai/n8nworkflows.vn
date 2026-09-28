---
title: "🔄 **Hướng Dẫn Chi Tiết: Lặp Lại Dữ Liệu Trong n8n – Từ Cơ Bản Đến Nâng Cao**"
description: "Workflow này giúp các sếp n8n mới bắt đầu hiểu rõ cách n8n xử lý **lặp lại (iteration)** dữ liệu, so sánh giữa **lặp tự động** và **lặp thủ công** với **Loop Over Items**. Kết quả: Tiết kiệm thời gian xử lý dữ liệu, tối ưu hóa quy trình tự động hóa, và dễ dàng mở rộng cho các dự án phức tạp."
slug: "huong-dan-looping-danh-sach-trong-n8n"
tags: [n8n, automation, no-code, looping, split-array, beginner-friendly]
keywords: [n8n looping over items, tự động hóa lặp lại dữ liệu, split array trong n8n, cách xử lý danh sách trong n8n, node loop over items]
---

# 🔄 **Lặp Lại Dữ Liệu Trong n8n: Từ Cơ Bản Đến Nâng Cao**

## **🚨 Nỗi Đau Của Các Sếp Khi Xử Lý Dữ Liệu Thô**
Có bao giờ các sếp phải **nhập tay** danh sách URL, email, hoặc dữ liệu khác vào các công cụ khác nhau? Hoặc phải **lặp lại** cùng một quy trình trên từng mục trong danh sách? Điều này không chỉ **tốn thời gian** mà còn dễ gây **lỗi nhân sự** khi có nhiều mục cần xử lý.

Với **n8n**, các sếp có thể **tự động hóa hoàn toàn** quy trình này bằng cách **lặp lại** dữ liệu một cách **chính xác và hiệu quả**. Workflow này sẽ giúp các sếp:
✅ **Hiểu rõ cách n8n xử lý lặp lại dữ liệu** (built-in vs. explicit looping).
✅ **Tách danh sách thành các mục riêng biệt** để xử lý từng phần.
✅ **Thêm thông tin bổ sung** vào từng mục trong quá trình lặp lại.
✅ **Tối ưu hóa thời gian** bằng cách **bỏ qua lặp lại** khi không cần thiết.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Không cần nhập tay hoặc lặp lại thủ công.
- **Chính xác 100%**: Tránh sai sót khi xử lý từng mục.
- **Tùy chỉnh linh hoạt**: Thêm thông tin bổ sung vào từng mục trong quá trình lặp lại.
- **Hoạt động liên tục**: Workflow chạy tự động, không phụ thuộc vào thời gian làm việc của nhân viên.
- **Dễ dàng mở rộng**: Có thể kết hợp với **Slack, Email, hoặc API** để tự động hóa thêm các bước.
:::

---

## 🛠️ **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Để workflow này hoạt động, các sếp **không cần** bất kỳ API key hoặc tài khoản nào ngoài **n8n Editor** (cả phiên bản **n8n.cloud** hoặc **self-hosted** đều được). Tuy nhiên, để **lên đồ** ổn định 24/7, các sếp nên **cài n8n trên VPS riêng** (Self-hosted).

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**).
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**.
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import** workflow này từ file JSON hoặc **copy/paste** JSON vào **n8n Editor**.

#### **Cách Import Từ File JSON:**
1. Tải file JSON từ [đây](https://n8n.io/workflows/2896) (hoặc copy JSON dưới đây).
2. Trong **n8n Editor**, nhấn **Import** (icon **↑** ở góc trên bên phải).
3. Chọn file JSON và **import**.

#### **Cách Copy/Paste JSON:**
```json
{
  "nodes": {
    "1": {
      "parameters": {},
      "name": "Paste JSON into this node",
      "type": "manualTrigger",
      "typeVersion": 1,
      "position": {
        "x": 200,
        "y": 200
      }
    },
    "2": {
      "parameters": {
        "property": "urls"
      },
      "name": "Split Array of Strings into Array of Objects",
      "type": "splitOut",
      "typeVersion": 1,
      "position": {
        "x": 400,
        "y": 200
      }
    },
    "3": {
      "parameters": {
        "batchSize": 1,
        "loopMode": "loop"
      },
      "name": "Loop over Items 1",
      "type": "splitInBatches",
      "typeVersion": 1,
      "position": {
        "x": 200,
        "y": 400
      }
    },
    "4": {
      "parameters": {
        "batchSize": 1,
        "loopMode": "loop"
      },
      "name": "Loop over Items 2",
      "type": "splitInBatches",
      "typeVersion": 1,
      "position": {
        "x": 600,
        "y": 400
      }
    },
    "5": {
      "parameters": {
        "code": "return [{\"param1\": \"value\"}];"
      },
      "name": "Add param1 to output1",
      "type": "code",
      "typeVersion": 1,
      "position": {
        "x": 200,
        "y": 600
      }
    },
    "6": {
      "parameters": {
        "code": "return [{\"param1\": \"value\"}];"
      },
      "name": "Add param1 to output2",
      "type": "code",
      "typeVersion": 1,
      "position": {
        "x": 600,
        "y": 600
      }
    },
    "7": {
      "parameters": {
        "code": "return [{\"param1\": \"value\"}];"
      },
      "name": "Add param1 to output3",
      "type": "code",
      "typeVersion": 1,
      "position": {
        "x": 600,
        "y": 800
      }
    },
    "8": {
      "parameters": {
        "code": "return [{\"param1\": \"value\"}];"
      },
      "name": "Add param1 to output4",
      "type": "code",
      "typeVersion": 1,
      "position": {
        "x": 600,
        "y": 1000
      }
    },
    "9": {
      "parameters": {
        "time": 1000
      },
      "name": "Wait one second(just for show)",
      "type": "wait",
      "typeVersion": 1,
      "position": {
        "x": 600,
        "y": 700
      }
    },
    "10": {
      "parameters": {},
      "name": "Result1",
      "type": "noOp",
      "typeVersion": 1,
      "position": {
        "x": 200,
        "y": 800
      }
    },
    "11": {
      "parameters": {},
      "name": "Result2",
      "type": "noOp",
      "typeVersion": 1,
      "position": {
        "x": 600,
        "y": 1200
      }
    },
    "12": {
      "parameters": {},
      "name": "Result3",
      "type": "noOp",
      "typeVersion": 1,
      "position": {
        "x": 600,
        "y": 1400
      }
    },
    "13": {
      "parameters": {},
      "name": "Result4",
      "type": "noOp",
      "typeVersion": 1,
      "position": {
        "x": 600,
        "y": 1600
      }
    },
    "14": {
      "parameters": {},
      "name": "Result5",
      "type": "noOp",
      "typeVersion": 1,
      "position": {
        "x": 200,
        "y": 1200
      }
    }
  },
  "connections": {
    "manualTrigger_1": [
      "splitOut_2",
      "splitInBatches_3"
    ],
    "splitOut_2": [
      "splitInBatches_4"
    ],
    "splitInBatches_3": [
      "code_5",
      "noOp_10"
    ],
    "code_5": [
      "noOp_14"
    ],
    "splitInBatches_4": [
      "code_6",
      "wait_9"
    ],
    "wait_9": [
      "code_7"
    ],
    "code_7": [
      "code_8"
    ],
    "code_8": [
      "noOp_11"
    ],
    "noOp_10": [
      "noOp_14"
    ]
  }
}
```

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Sau khi import, các sếp cần **cấu hình** các node quan trọng như sau:

#### **🔹 Node "Paste JSON into this node" (Manual Trigger)**
- **Điền dữ liệu mẫu** như sau:
  ```json
  {
    "urls": [
      "https://www.reddit.com",
      "https://www.n8n.io/",
      "https://n8n.io/",
      "https://supabase.com/",
      "https://duckduckgo.com/"
    ]
  }
  ```
- **Cách thực hiện**:
  1. **Double-click** vào node này.
  2. Nhấn **"Edit Output"** (góc trên bên phải).
  3. **Paste** JSON trên và **Save**.
  4. Node sẽ **đổi màu thành purple**, nghĩa là đã **đính kèm dữ liệu test**.

#### **🔹 Node "Split Array of Strings into Array of Objects" (Split Out)**
- **Chọn `property` = "urls"** để tách danh sách URL thành các đối tượng riêng biệt.

#### **🔹 Node "Loop over Items 1" & "Loop over Items 2" (Split In Batches)**
- **Loop Over Items 1**:
  - **Xử lý danh sách chưa tách** → **được xem như 1 mục duy nhất**.
  - **Kết quả**: Node `Result1` và `Result5` sẽ hiển thị **dữ liệu chưa tách**.
- **Loop Over Items 2**:
  - **Xử lý danh sách đã tách** → **mỗi URL là 1 mục riêng biệt**.
  - **Kết quả**: Node `Result2`, `Result3`, `Result4` sẽ hiển thị **từng URL một**.

#### **🔹 Node "Wait one second(just for show)" (Wait)**
- **Thời gian chờ**: 1 giây/mục (có thể **bỏ qua** nếu không cần).

#### **🔹 Node "Add param1 to outputX" (Code)**
- **Mục đích**: Thêm trường `param1` vào từng mục trong quá trình lặp lại.
- **Code mẫu**:
  ```javascript
  return [{ "param1": "value" }];
  ```
  - Các sếp có thể **thay đổi giá trị** của `param1` tùy ý.

#### **🔹 Node "Result1", "Result2", ..., "Result5" (NoOp)**
- **Chức năng**: Hiển thị **kết quả** tại từng bước để **kiểm tra**.
- **Lưu ý**:
  - `Result1` & `Result5` → **Danh sách chưa tách** → Xử lý như 1 mục.
  - `Result2`, `Result3`, `Result4` → **Danh sách đã tách** → Xử lý từng mục.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu đã điền.
2. **Bật Active** workflow.
3. **Kiểm tra kết quả** tại các node `Result1` đến `Result5`.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**CÁCH MỞ RỘNG THÊM**]
1. **Kết hợp với Slack/Telegram**:
   - Sau khi lặp lại, **gửi kết quả** vào Slack/Telegram thông qua **node Webhook** hoặc **Slack API**.
   - **Ví dụ**: Gửi thông báo khi xử lý xong từng URL.

2. **Lưu Log vào Google Sheets/Notion**:
   - Sử dụng **node Google Sheets** hoặc **Notion API** để **ghi lại lịch sử** các mục đã xử lý.

3. **Tự động gửi Email báo cáo**:
   - Kết hợp **node Email** (Gmail/SMTP) để **gửi báo cáo định kỳ** về kết quả lặp lại.

4. **Bỏ qua lặp lại khi không cần**:
   - Trong **Loop Over Items**, có thể **chọn `Run Once For All Items`** để **không lặp lại** (như trong `Result4`).

5. **Tăng tốc độ với Batch Processing**:
   - Thay vì **lặp lại từng mục**, các sếp có thể **tăng `batchSize`** trong **Split In Batches** để xử lý nhiều mục cùng lúc.
:::

---

## 📌 **Kết Luận**
Workflow này là **cơ sở** để các sếp **hiểu rõ cách lặp lại dữ liệu** trong n8n, từ **lặp tự động** (built-in) đến **lặp thủ công** (Loop Over Items). Với kiến thức này, các sếp có thể:
✔ **Tự động hóa xử lý danh sách** (URL, email, sản phẩm, ...).
✔ **Tối ưu hóa thời gian** bằng cách **tách và xử lý từng mục**.
✔ **Mở rộng** cho các dự án phức tạp hơn (ví dụ: **scraping website, CRM, hoặc E-commerce**).

**🚀 Hãy thử ngay và tự động hóa quy trình của mình!**

---
**💡 Lưu ý cuối cùng**:
- Nếu các sếp muốn **self-host n8n**, hãy **lựa chọn VPS ổn định** để workflow chạy **24/7** mà không gián đoạn.
- **Không cần lo về bảo mật** khi self-host