---
title: "🚀 Tự Động Hoà Quả Quảng Cáo Sản Phẩm Thời Trang Với AI Gemini - Không Cần Code!"
description: "Workflow này tự động tạo quảng cáo sản phẩm thời trang chuyên nghiệp với hình ảnh mô hình AI, chỉ với một hình ảnh sản phẩm đầu vào. Giúp các sếp tiết kiệm thời gian lên tới 80% trong việc tạo nội dung quảng cáo cá nhân hóa."
slug: "tieu-dong-hoa-quang-cao-san-pham-thoi-trang-voi-gemini-ai"
tags: [n8n, automation, no-code, content-creation, multimodal-ai, google-gemini, openrouter]
keywords: [tự động hóa quảng cáo thời trang, tạo quảng cáo AI, n8n workflow, Gemini AI, OpenRouter API, quảng cáo sản phẩm thời trang tự động]
---

# 🚀 **Tự Động Hoà Quảng Cáo Sản Phẩm Thời Trang Với AI Gemini - Không Cần Code!**

### **Giải pháp cho các sếp thời trang:**
Hãy tưởng tượng một ngày không phải mất hàng giờ để lên hình ảnh mô hình cho quảng cáo sản phẩm thời trang! Bây giờ, với **n8n + AI Gemini**, chỉ với một hình ảnh sản phẩm đầu vào, workflow này sẽ tự động tạo ra quảng cáo chuyên nghiệp với mô hình thời trang đẹp mắt, hoàn toàn cá nhân hóa và sẵn sàng chia sẻ trên mạng xã hội hoặc website.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên tới 80%** so với việc tạo quảng cáo thủ công.
- **Cá nhân hóa hoàn toàn**: Mô hình thời trang tự động phù hợp với sản phẩm đầu vào.
- **Chất lượng chuyên nghiệp**: Sử dụng mô hình AI Gemini của Google, đảm bảo hình ảnh đẹp mắt và chuyên nghiệp.
- **Hoạt động liên tục**: Workflow tự động hóa, không cần can thiệp của con người.
- **Tích hợp dễ dàng**: Hoàn toàn không cần viết code, chỉ cần cấu hình đơn giản.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản OpenRouter** ([Đăng ký miễn phí](https://openrouter.ai/)) và **API Key** của OpenRouter.
2. **Hình ảnh sản phẩm thời trang** (để sử dụng làm đầu vào cho workflow).
3. **N8n Editor** (cài đặt trên máy hoặc VPS).
4. **Nghiên cứu về mô hình AI Gemini** (nếu muốn tối ưu hóa kết quả).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải file JSON của workflow từ [đây](https://n8n.io/workflows/8193) hoặc sao chép JSON từ canvas.
- **Bước 2**: Mở **n8n Editor** và chọn **"Import"** từ menu.
- **Bước 3**: Dán JSON vào và chọn **"Import"**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này bao gồm **7 node** chính, nhưng các sếp cần chú ý đặc biệt đến các node sau:

##### **🔹 Node "On form submission" (formTrigger)**
- **Lưu ý**: Cấu hình form để nhận **hình ảnh sản phẩm** và **thông tin mô hình** (nếu có).
  - Thêm các trường như:
    - **Product Image** (Upload file).
    - **Character Model** (Nếu muốn chỉ định kiểu dáng mô hình).
  - **Kiểu dữ liệu**: Chọn **"File"** cho trường hình ảnh.

##### **🔹 Node "Nano 🍌" (httpRequest)**
- **Lưu ý**: Đây là node kết nối với **OpenRouter API** để gọi mô hình AI Gemini.
  - **Tham số quan trọng**:
    - **Credentials**: Chọn **"openRouterApi"** (cần tạo trước trong n8n).
    - **URL**: `https://openrouter.ai/api/v1/chat/completions` (mặc định).
    - **Headers**:
      ```
      {
        "Authorization": "Bearer YOUR_OPENROUTER_API_KEY",
        "HTTP-Referer": "https://openrouter.ai",
        "Content-Type": "application/json"
      }
      ```
    - **Body (JSON)**:
      ```json
      {
        "model": "google/gemini-pro-vision",
        "messages": [
          {
            "role": "user",
            "content": [
              {
                "type": "image_url",
                "image_url": {
                  "url": "{{ $node["Convert to File"].json["fileUrl"] }}"
                }
              },
              {
                "type": "text",
                "text": "Generate a professional fashion ad featuring a model wearing the product. The model should look stylish and confident. Output in a high-quality image format."
              }
            ]
          }
        ]
      }
      ```
  - **Lưu ý**: Thay thế `YOUR_OPENROUTER_API_KEY` bằng API Key của các sếp.

##### **🔹 Node "Code" (code)**
- **Lưu ý**: Node này xử lý **chuyển đổi dữ liệu** từ binary sang dạng JSON để AI xử lý.
  - **Mã mặc định** (không cần chỉnh sửa nếu đã import từ file):
    ```javascript
    return {
      json: {
        image: $input.all()[0].binary,
        prompt: "Generate a professional fashion ad featuring a model wearing the product. The model should look stylish and confident."
      }
    };
    ```

##### **🔹 Node "Form" (form)**
- **Lưu ý**: Cấu hình form kết quả để người dùng **tải xuống** quảng cáo đã tạo.
  - Thêm trường **"Download"** với kiểu **"File"**.
  - **Lưu ý**: Node này sẽ hiển thị kết quả cuối cùng cho người dùng.

#### **3. Kích hoạt ⚡️**
- **Bước 1**: **Test Run** với một hình ảnh mẫu để kiểm tra workflow.
- **Bước 2**: Chọn **"Active"** để bật workflow.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tối ưu hóa mô hình AI**:
   - Thay đổi **prompt** trong node `Code` để điều chỉnh phong cách mô hình (ví dụ: "mô hình trẻ trung" hoặc "mô hình sang trọng").
   - Thử nghiệm với các mô hình khác của OpenRouter (nếu có).

2. **Tích hợp với Slack/Telegram**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo kết quả cho team.
   - Ví dụ: Khi workflow hoàn thành, gửi tin nhắn thông báo với link tải quảng cáo.

3. **Lưu log và báo cáo**:
   - Sử dụng node **Google Sheets** hoặc **Airtable** để lưu lịch sử các quảng cáo đã tạo.
   - Tạo báo cáo định kỳ về số lượng quảng cáo được tạo và thời gian xử lý.

4. **Cá nhân hóa thêm**:
   - Thêm trường **"Brand Name"** hoặc **"Product Name"** vào form đầu vào để AI tạo quảng cáo phù hợp với thương hiệu.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp thời trang muốn tự động hóa việc tạo quảng cáo với chất lượng cao, không cần viết code. Với **AI Gemini** và **n8n**, các sếp có thể tiết kiệm thời gian, tăng hiệu suất và tạo nội dung cá nhân hóa một cách dễ dàng.

**Hãy thử ngay và biến quảng cáo của mình thành chuyên nghiệp hơn!** 🚀

---
**🔗 [Xem video hướng dẫn chi tiết](https://youtu.be/UGf01FYaAzY?si=xaO5N1xeXotZ0tYN)** (Tutorial từ Zakwan)