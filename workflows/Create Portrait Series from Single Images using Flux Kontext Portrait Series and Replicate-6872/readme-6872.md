---
title: "🎨 Tự Động Tạo Bộ Sưu Tập Ảnh Cổ Điển Từ 1 Ảnh Bằng AI (Flux + Replicate) - N8N"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp tạo ra bộ ảnh chân dung đa dạng từ 1 ảnh đầu vào chỉ với 1 cú nhấp chuột, tiết kiệm thời gian lên đến 90% so với làm thủ công. Sử dụng AI Flux Kontext + API Replicate để sinh ra hàng loạt pose ấn tượng, hoàn toàn không cần kỹ năng code."
slug: "tay-dong-tao-bo-suu-tap-anh-co-dien-tu-1-anh-bang-ai"
tags: [n8n, automation, ai-image-generation, flux-ai, replicate-api, content-creation]
keywords: [n8n workflow tự động tạo ảnh, tạo bộ ảnh chân dung từ 1 ảnh, ai sinh ảnh đa dạng pose, flux kontext portrait series, tự động hóa content creation]
---

# 🚀 **Tự Động Tạo Bộ Ảnh Cổ Điển Từ 1 Ảnh Bằng AI (Flux + Replicate) - Cách Sử Dụng Workflow N8N**

## 🤔 **Nỗi Đau Của Các Sếp Trong Content Creation**
Các sếp thường phải mất **giờ đồng hồ** để tạo ra bộ ảnh chân dung đa dạng từ 1 ảnh gốc để phục vụ:
- **Marketing digital** (banner, quảng cáo mạng xã hội)
- **E-commerce** (hình sản phẩm đa góc độ)
- **Nội dung blog/tiêu đề video** (ảnh thu hút mắt)
- **Nghiên cứu thị trường** (tạo avatar khách hàng)

Với **tay nghề thủ công**, việc này đòi hỏi:
✅ **Sử dụng Photoshop/GIMP** (nếu biết code)
✅ **Mua license ảnh stock** (tốn kém)
✅ **Tìm kiếm và chỉnh sửa ảnh** (tốn thời gian)
✅ **Đảm bảo tính nhất quán** (màu sắc, phong cách)

**➡️ Kết quả?** Thời gian và chi phí **lên đến 10x** so với giải pháp tự động hóa!

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ **60 phút** xuống còn **30 giây** cho 1 bộ ảnh 4 pose.
- **Chất lượng chuyên nghiệp**: AI Flux Kontext sinh ra ảnh **đa dạng, tự nhiên**, không cần chỉnh sửa.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công, hoạt động **24/7** nếu self-hosted.
- **Cá nhân hóa cao**: Chỉ cần **1 ảnh gốc**, AI tự động tạo ra **hàng loạt pose** khác nhau.
- **Dễ dàng mở rộng**: Kết hợp với **Slack/Email** để thông báo kết quả, hoặc **lưu log** cho quản lý.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Replicate API**:
   - Đăng ký tại [replicate.com](https://replicate.com) và lấy **API Token**.
   - **Mã giảm giá**: Sử dụng mã `N8NAI` để giảm **20% phí đầu tiên** (nếu có).
2. **Ảnh đầu vào** (format: **JPEG, PNG, GIF, WEBP**).
3. **n8n Self-hosted** (khuyến nghị) hoặc **n8n Cloud** (miễn phí cho thử nghiệm).
4. **Thời gian**: ~5-10 giây cho 1 bộ ảnh 4 pose.
:::

---
### 🚀 **Cách Import & Cấu Hình Workflow**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/6872) hoặc copy toàn bộ JSON dưới đây vào **n8n Editor**:
  ```json
  {
    "nodes": [
      {
        "parameters": {},
        "name": "Manual Trigger",
        "type": "n8n-nodes-base.manualTrigger",
        "typeVersion": 1,
        "position": {
          "x": 200,
          "y": 200
        }
      },
      {
        "parameters": {
          "property": "REPLICATE_API_TOKEN"
        },
        "name": "Set API Token",
        "type": "n8n-nodes-base.set",
        "typeVersion": 1,
        "position": {
          "x": 200,
          "y": 400
        }
      },
      {
        "parameters": {
          "values": {
            "input_image": "https://example.com/input.jpg",
            "background": "white",
            "num_images": 4,
            "output_format": "png",
            "randomize_images": false,
            "safety_tolerance": 2
          }
        },
        "name": "Set Image Parameters",
        "type": "n8n-nodes-base.set",
        "typeVersion": 1,
        "position": {
          "x": 200,
          "y": 600
        }
      },
      {
        "parameters": {
          "method": "POST",
          "url": "https://api.replicate.com/v1/predictions",
          "body": {
            "input": {
              "input_image": "{{$node["Set Image Parameters"].json["input_image"]}}",
              "background": "{{$node["Set Image Parameters"].json["background"]}}",
              "num_images": "{{$node["Set Image Parameters"].json["num_images"]}}",
              "output_format": "{{$node["Set Image Parameters"].json["output_format"]}}",
              "randomize_images": "{{$node["Set Image Parameters"].json["randomize_images"]}}",
              "safety_tolerance": "{{$node["Set Image Parameters"].json["safety_tolerance"]}}"
            }
          },
          "headers": {
            "Authorization": "Token {{$node["Set API Token"].json["REPLICATE_API_TOKEN"]}}",
            "Content-Type": "application/json"
          }
        },
        "name": "Create Image Prediction",
        "type": "n8n-nodes-base.httpRequest",
        "typeVersion": 1,
        "position": {
          "x": 200,
          "y": 800
        }
      },
      // ... (các node còn lại)
    ],
    "connections": {}
  }
  ```
- **Lưu ý**: Nếu import từ file JSON, **không cần copy toàn bộ**, chỉ cần tải file `.json` từ link trên và **import vào n8n Editor**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **A. Cấu Hình Node "Set API Token"**
- **Tham số `REPLICATE_API_TOKEN`**:
  - Điền **API Token** từ tài khoản Replicate của bạn.
  - **Lưu ý an ninh**: **Không** chia sẻ token này với ai, và **không** commit vào code public.
  - **Mẹo**: Sử dụng **n8n Credentials** để quản lý token an toàn:
    ```json
    {
      "auth": {
        "type": "apiKey",
        "key": "Authorization",
        "value": "{{$credentials["REPLICATE_API_TOKEN"]}}"
      }
    }
    ```

##### **B. Cấu Hình Node "Set Image Parameters"**
- **Tham số bắt buộc**:
  - `input_image`: **URL hoặc đường dẫn file ảnh** (format: JPEG/PNG/GIF/WEBP).
    - **Ví dụ**: `https://tino.vn/images/example.jpg` hoặc `file:///path/to/local.jpg`.
  - **Lưu ý**: Nếu ảnh quá lớn (>5MB), **nén ảnh** trước khi upload.
- **Tham số tùy chọn**:
  - `num_images`: Số lượng pose sinh ra (mặc định **4**).
  - `background`: Màu nền (mặc định `"white"`).
  - `randomize_images`: **true** để pose ngẫu nhiên, **false** để giống nhau (mặc định `false`).
  - `output_format`: Định dạng xuất (mặc định `"png"`).

##### **C. Node "Create Image Prediction"**
- **Kiểm tra URL API**:
  - Đảm bảo `url` trong node là `https://api.replicate.com/v1/predictions`.
- **Headers**:
  - **Authorization** phải chứa token từ node `Set API Token`.

##### **D. Node "Wait & Status Checking"**
- **Thời gian chờ**:
  - Node `Wait 5s` và `Wait 10s` được thiết kế để **tránh quá tải API**.
  - **Không cần chỉnh** trừ khi API Replicate trả về thời gian xử lý khác.

##### **E. Node "Success/Error Response"**
- **Lưu kết quả**:
  - Kết quả thành công sẽ trả về **URL download ảnh**.
  - **Mẹo**: Kết nối node này với **Slack/Email** để thông báo tự động:
    ```json
    {
      "parameters": {
        "message": "🎨 Bộ ảnh đã tạo thành công! Download tại: {{$json["urls"]}}",
        "channel": "#content-creation"
      },
      "name": "Notify Slack",
      "type": "n8n-nodes-base.slack",
      "position": {
        "x": 600,
        "y": 1200
      }
    }
    ```

#### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run**:
   - Nhấn **Run** trên node `Manual Trigger` với **dữ liệu mẫu**:
     ```json
     {
       "input_image": "https://example.com/test.jpg",
       "num_images": 2
     }
     ```
   - Kiểm tra **log** để đảm bảo không có lỗi.
2. **Bật Active**:
   - Sau khi test thành công, **bật workflow** để hoạt động tự động.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
#### **1. Tự Động Tải Ảnh Về Local**
- Sử dụng **n8n-nodes-base.httpRequest** để tải ảnh từ URL và lưu vào **Google Drive/Dropbox**:
  ```json
  {
    "parameters": {
      "method": "GET",
      "url": "{{$json["urls"][0]}}",
      "destination": "/path/to/save/image.png"
    },
    "name": "Download Image",
    "type": "n8n-nodes-base.httpRequest",
    "position": {
      "x": 600,
      "y": 1000
    }
  }
  ```

#### **2. Gửi Báo Cáo Định Kỳ**
- Kết nối với **Google Sheets** để **lưu lịch sử tạo ảnh**:
  ```json
  {
    "parameters": {
      "sheetName": "Portrait_Series",
      "row": {
        "Timestamp": "{{$node["Log Request"].json["timestamp"]}}",
        "Input_Image": "{{$node["Set Image Parameters"].json["input_image"]}}",
        "Status": "{{$node["Is Complete?"].json["status"]}}",
        "URLs": "{{$json["urls"]}}"
      }
    },
    "name": "Log to Google Sheets",
    "type": "n8n-nodes-base.googleSheets",
    "position": {
      "x": 800,
      "y": 1200
    }
  }
  ```

#### **3. Kết Hợp Với LLM (AI Chatbot)**
- Sử dụng **n8n-nodes-ai.ollama** để **tự động mô tả ảnh** hoặc **tạo caption** cho bộ ảnh:
  ```json
  {
    "parameters": {
      "model": "llama3",
      "prompt": "Tóm tắt 3 điểm nổi bật của bộ ảnh này: {{$json["urls"]}}",
      "temperature": 0.7
    },
    "name": "Generate Caption",
    "type": "n8n-nodes-ai.ollama",
    "position": {
      "x": 1000,
      "y": 1000
    }
  }
  ```

#### **4. Optimize API Cost**
- **Giảm `num_images`** khi thử nghiệm (mặc định là 4).
- **Sử dụng `safety_tolerance: 1`** (thay vì 2) để tiết kiệm token API.

---
### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần **tạo bộ ảnh chân dung đa dạng, chuyên nghiệp và nhanh chóng** mà **không cần kỹ năng code**. Với **AI Flux Kontext** và **API Replicate**, bạn có thể:
✅ **Tiết kiệm thời gian** lên đến **90%** so với làm thủ công.
✅ **Tự động hóa hoàn toàn** với n8n self-hosted.
✅ **Mở rộng dễ dàng** bằng các node bổ sung (Slack, Google Sheets, LLM...).

**🚀 Hành động ngay!**
1. **Cài n8n trên VPS** (khuyến nghị) để workflow hoạt động **24/7**:
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
2. **Import workflow** và **cấu hình API Token**.
3. **Nhấn Manual Trigger** và **nhận bộ ảnh hoàn hảo** chỉ trong vài giây!

**🔗 Tài liệu tham khảo**:
- [Flux Kontext Portrait Series](https://replicate.com/flux-kontext-apps/portrait-series)
- [Replicate API Docs](https://replicate.com/docs)
- [n8n Self-hosted Guide](https://docs.n8n.io/hosting/self-hosting/)

**💬 Có thắc mắc?** Liên hệ với tác giả Yaron Been qua:
📩 Email: [Yaron@nofluff.online](mailto:Yaron@nofluff.online)
📺 YouTube: [@YaronBeen](https://www.youtube.com/@YaronBeen)
💼 LinkedIn: [Yaron Been](https://www.linkedin.com/in/yaronbeen/)