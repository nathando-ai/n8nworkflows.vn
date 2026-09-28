---
title: "🎨 Tự Động Hóa Tạo Hình Ảnh Cổ Trang & Glam với AI Paige (n8n + Replicate) - Không Cần Code!"
description: "Workflow tự động hóa hoàn toàn để tạo hình ảnh 3D cổ trang, glam, fantasy với AI Paige của PaigeDutchers2 trên Replicate API. Giúp các sếp tiết kiệm thời gian lên đến 80% so với thủ công, với chất lượng chuyên nghiệp và cá nhân hóa cao."
slug: "tạo-hình-ảnh-ai-paige-n8n-replicate"
tags: [n8n, automation, ai-generative, content-creation, replicate-api]
keywords: [n8n workflow tạo hình ảnh AI, tự động hóa tạo ảnh 3D glam, Paige AI, Replicate API n8n, tự động hóa không code]
---

# 🚀 **Tự Động Hóa Tạo Hình Ảnh Cổ Trang & Glam với AI Paige (PaigeDutchers2) - Không Cần Code!**

### **💡 Nỗi Đau Của Các Sếp Trong Nền Tạo Nội Dung AI**
Bạn là một **content creator**, **marketing manager**, hay **designer** phải tạo hàng chục, hàng trăm hình ảnh 3D, cổ trang, glam, fantasy cho các dự án? Thời gian và công sức để:
- **Tìm kiếm và viết prompt** phù hợp?
- **Chờ đợi kết quả** từ các mô hình AI truyền thống (thường mất từ 5-30 phút)?
- **Lọc và chỉnh sửa** hình ảnh không phù hợp?
- **Quản lý API key** và ngân sách Replicate?

**Workflow này giải quyết tất cả!** Với **AI Paige** (mô hình được huấn luyện đặc biệt với phong cách "Barbie meets boss" - **bold, curvy, confident**), các sếp có thể **tự động hóa toàn bộ quy trình** từ viết prompt đến download ảnh, chỉ với **một cú nhấp chuột**.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 80%** so với thủ công: Không cần chờ đợi, không cần viết prompt từ đầu.
- **Chất lượng chuyên nghiệp**: Hình ảnh 3D cao cấp, phong cách **glam, fantasy, seductive** phù hợp với content marketing, influencer, hoặc thương hiệu.
- **Cá nhân hóa hoàn toàn**: Thay đổi prompt, kích thước, hoặc tham số AI một cách dễ dàng.
- **Hoạt động 24/7**: Cài đặt trên **VPS tự host** để workflow chạy liên tục, không phụ thuộc vào thời gian làm việc.
- **Kiểm soát chi phí**: API Replicate được tối ưu hóa, tránh lãng phí token.
- **Lưu trữ và quản lý**: Kết quả được trả về dưới dạng URL hoặc file, dễ dàng tích hợp vào hệ thống nội dung.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Replicate**:
   - Đăng ký tại [replicate.com](https://replicate.com) và lấy **API Token** (để cấu hình trong workflow).
   - **Mã giảm giá**: Sử dụng mã `N8NAI` để giảm **10% phí đầu tiên** khi mua credits (nếu cần).
2. **VPS cho n8n (khuyến nghị)**:
   - Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng** (self-hosted).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
3. **Tham số AI Paige**:
   - **Prompt**: Ví dụ: *"A glamorous fantasy portrait of a confident businesswoman in a vintage dress, hyper-detailed, 8k, trending on ArtStation"* (có thể thêm từ khóa như `CharacterPGE` để kích hoạt phong cách đặc biệt).
   - **Tham số tùy chọn**: `width`, `height`, `seed` (để tái sinh ảnh giống nhau), `go_fast` (tăng tốc độ nhưng giảm chất lượng).
4. **N8n Editor**:
   - Tài khoản miễn phí tại [n8n.io](https://n8n.io/) hoặc tự host trên VPS.
---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/6851) hoặc copy toàn bộ JSON dưới đây vào **n8n Editor**:
  ```json
  {
    "nodes": [
      {
        "parameters": {},
        "name": "Manual Trigger",
        "type": "n8n-nodes-base.manualTrigger",
        "typeVersion": 1,
        "position": [250, 300]
      },
      {
        "parameters": {
          "property": "REPLICATE_API_TOKEN",
          "value": "YOUR_REPLICATE_API_TOKEN"
        },
        "name": "Set API Token",
        "type": "n8n-nodes-base.set",
        "typeVersion": 1,
        "position": [250, 450]
      },
      {
        "parameters": {
          "properties": [
            {
              "key": "prompt",
              "value": "A glamorous fantasy portrait of a confident businesswoman in a vintage dress, hyper-detailed, 8k, trending on ArtStation"
            },
            {
              "key": "width",
              "value": "1024"
            },
            {
              "key": "height",
              "value": "1024"
            },
            {
              "key": "model",
              "value": "dev"
            }
          ]
        },
        "name": "Set Other Parameters",
        "type": "n8n-nodes-base.set",
        "typeVersion": 1,
        "position": [250, 600]
      },
      {
        "parameters": {
          "method": "POST",
          "url": "https://api.replicate.com/v1/predictions",
          "headers": {
            "Authorization": "Bearer $REPLICATE_API_TOKEN"
          },
          "body": {
            "type": "json",
            "json": {
              "input": {
                "prompt": "$prompt",
                "width": "$width",
                "height": "$height",
                "model": "$model"
              }
            }
          }
        },
        "name": "Create Other Prediction",
        "type": "n8n-nodes-base.httpRequest",
        "typeVersion": 1,
        "position": [600, 450]
      },
      {
        "parameters": {
          "time": 5000
        },
        "name": "Wait 5s",
        "type": "n8n-nodes-base.wait",
        "typeVersion": 1,
        "position": [600, 600]
      },
      {
        "parameters": {
          "method": "GET",
          "url": "https://api.replicate.com/v1/predictions/$prediction_id",
          "headers": {
            "Authorization": "Bearer $REPLICATE_API_TOKEN"
          }
        },
        "name": "Check Status",
        "type": "n8n-nodes-base.httpRequest",
        "typeVersion": 1,
        "position": [950, 500]
      },
      {
        "parameters": {
          "condition": {
            "json": {
              "status": "succeeded"
            }
          }
        },
        "name": "Is Complete?",
        "type": "n8n-nodes-base.if",
        "typeVersion": 1,
        "position": [1300, 400]
      },
      {
        "parameters": {
          "condition": {
            "json": {
              "status": "failed"
            }
          }
        },
        "name": "Has Failed?",
        "type": "n8n-nodes-base.if",
        "typeVersion": 1,
        "position": [1300, 600]
      },
      {
        "parameters": {
          "time": 10000
        },
        "name": "Wait 10s",
        "type": "n8n-nodes-base.wait",
        "typeVersion": 1,
        "position": [950, 700]
      },
      {
        "parameters": {
          "property": "output_url",
          "value": "$$.json.output_url"
        },
        "name": "Success Response",
        "type": "n8n-nodes-base.set",
        "typeVersion": 1,
        "position": [1600, 400]
      },
      {
        "parameters": {
          "property": "error",
          "value": "$$.json.error"
        },
        "name": "Error Response",
        "type": "n8n-nodes-base.set",
        "typeVersion": 1,
        "position": [1600, 600]
      },
      {
        "parameters": {
          "property": "result",
          "value": "$output_url"
        },
        "name": "Display Result",
        "type": "n8n-nodes-base.set",
        "typeVersion": 1,
        "position": [1600, 800]
      },
      {
        "parameters": {
          "code": "console.log('Request sent:', $$.json);"
        },
        "name": "Log Request",
        "type": "n8n-nodes-base.code",
        "typeVersion": 1,
        "position": [250, 800]
      }
    ],
    "connections": {
      "Manual Trigger": {
        "main": [
          [
            {
              "node": "Set API Token",
              "type": "main",
              "index": 0
            }
          ]
        ]
      },
      "Set API Token": {
        "main": [
          [
            {
              "node": "Set Other Parameters",
              "type": "main",
              "index": 0
            }
          ]
        ]
      },
      "Set Other Parameters": {
        "main": [
          [
            {
              "node": "Create Other Prediction",
              "type": "main",
              "index": 0
            }
          ]
        ]
      },
      "Create Other Prediction": {
        "main": [
          [
            {
              "node": "Wait 5s",
              "type": "main",
              "index": 0
            }
          ]
        ]
      },
      "Wait 5s": {
        "main": [
          [
            {
              "node": "Check Status",
              "type": "main",
              "index": 0
            }
          ]
        ]
      },
      "Check Status": {
        "main": [
          [
            {
              "node": "Is Complete?",
              "type": "main",
              "index": 0
            }
          ]
        ]
      },
      "Is Complete?": {
        "true": [
          [
            {
              "node": "Success Response",
              "type": "main",
              "index": 0
            }
          ]
        ],
        "false": [
          [
            {
              "node": "Wait 10s",
              "type": "main",
              "index": 0
            }
          ]
        ]
      },
      "Wait 10s": {
        "main": [
          [
            {
              "node": "Check Status",
              "type": "main",
              "index": 0
            }
          ]
        ]
      },
      "Has Failed?": {
        "true": [
          [
            {
              "node": "Error Response",
              "type": "main",
              "index": 0
            }
          ]
        ]
      },
      "Success Response": {
        "main": [
          [
            {
              "node": "Display Result",
              "type": "main",
              "index": 0
            }
          ]
        ]
      },
      "Error Response": {
        "main": [
          [
            {
              "node": "Display Result",
              "type": "main",
              "index": 0
            }
          ]
        ]
      },
      "Display Result": {
        "main": [
          [
            {
              "node": "Log Request",
              "type": "main",
              "index": 0
            }
          ]
        ]
      }
    }
  }
  ```
  - **Lưu ý**: Nếu copy từ editor, **không sao chép dấu `**` ở đầu và cuối JSON**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
##### **A. Cấu Hình API Token**
- Trong node **"Set API Token"**, thay thế `YOUR_REPLICATE_API_TOKEN` bằng **API Token** của bạn từ Replicate.
- **Lưu ý an ninh**: Không chia sẻ token này với ai!

##### **B. Tham Số AI Paige**
- Trong node **"Set Other Parameters"**, các sếp có thể **tùy chỉnh**:
  - **Prompt**: Thay đổi để phù hợp với nội dung cần tạo (ví dụ: *"A fantasy portrait of a cyberpunk queen in a futuristic gown"*).
  - **Kích thước ảnh**: `width` và `height` (giá trị mặc định là 1024x1024, có thể tăng lên 1536x1536 cho chất lượng cao hơn).
  - **Model**: Giá trị mặc định là `"dev"` (mô hình phát triển, chất lượng cao nhất).
  - **Tham số tùy chọn**:
    - `seed`: Để tái sinh ảnh giống nhau (ví dụ: `12345`).
    - `go_fast`: Đặt `true` để tăng tốc độ (nhưng chất lượng giảm).

##### **C. Node "Create Other Prediction"**
- **URL API**: Đã cấu hình sẵn là `https://api.replicate.com/v1/predictions`.
- **Headers**: Đã tự động thêm `Authorization` từ token.
- **Body**: Dữ liệu input sẽ được truyền từ node **"Set Other Parameters"**.

##### **D. Node "Check Status"**
- **URL**: Sử dụng `$prediction_id` (ID dự đoán từ API Replicate).
- **Lưu ý**: Node này **lặp lại** cho đến khi trạng thái là `succeeded` hoặc `failed`.

##### **E. Node "Is Complete?" và "Has Failed?"**
- **Điều kiện**:
  - `Is Complete?`: Kiểm tra `status === "succeeded"`.
  - `Has Failed?`: Kiểm tra `status === "failed"`.
- **Lưu ý**: Nếu trạng thái không phải `succeeded` hoặc `failed`, workflow sẽ **chờ thêm 10s** và kiểm tra lại.

##### **F. Node "Display Result"**
- **Output**: Trả