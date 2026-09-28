---
title: "🔍 **Tự Động Hóa Phát Hiện Đối Tượng Trên Hình Ảnh Với Gemini 2.0 (Prompt-Based Object Detection) - Không Cần Code!**"
description: "Workflow này tự động phát hiện và vẽ khung bao quanh các đối tượng trên hình ảnh theo yêu cầu cụ thể (ví dụ: 'tìm tất cả con thỏ', 'phát hiện xe vi phạm quy định') bằng Gemini 2.0 của Google. Giúp tiết kiệm thời gian kiểm tra thủ công và nâng cao độ chính xác trong phân tích hình ảnh."
slug: "tieu-dong-hoa-phat-hien-doi-tuong-voi-gemini-2-0"
tags: [n8n, automation, ai, gemini-2-0, object-detection, no-code]
keywords: [n8n workflow gemini 2.0, phát hiện đối tượng trên hình ảnh, tự động hóa AI, object detection prompt-based, gemini api n8n]
---

# 🚀 **Tự Động Hóa Phát Hiện Đối Tượng Trên Hình Ảnh Với Gemini 2.0 (Prompt-Based Object Detection)**

### **Giải pháp nào giúp các sếp:**
- **Tìm kiếm và phân tích đối tượng trên hình ảnh chỉ bằng lời nhắc (prompt)** (ví dụ: "tìm tất cả xe ô tô đỗ sai chỗ", "phát hiện mặt người có biểu cảm buồn").
- **Vẽ tự động khung bao quanh đối tượng** trên hình ảnh để đánh giá độ chính xác.
- **Áp dụng cho nhiều trường hợp thực tế**: kiểm tra an toàn giao thông, phân tích hình ảnh y tế, quản lý kho hàng, hoặc thậm chí là phân tích cảm xúc trong hình ảnh.
- **Không cần viết code**: Sử dụng toàn bộ các node của n8n để tự động hóa quy trình.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Thay vì phải kiểm tra từng hình ảnh thủ công, AI sẽ tự động phát hiện và vẽ khung bao quanh đối tượng theo yêu cầu.
✅ **Độ chính xác cao**: Gemini 2.0 có khả năng nhận diện đa dạng đối tượng và bối cảnh, từ vật thể cụ thể đến cảm xúc.
✅ **Cá nhân hóa yêu cầu**: Có thể nhập **prompt tùy chỉnh** để AI tìm kiếm đối tượng phù hợp với nhu cầu (ví dụ: "tìm tất cả trẻ em dưới 12 tuổi trong hình ảnh").
✅ **Hoạt động liên tục 24/7**: Khi cài đặt trên VPS, workflow sẽ tự động chạy mà không cần can thiệp.
✅ **Dễ dàng mở rộng**: Có thể kết nối với Slack/Telegram để thông báo kết quả hoặc lưu log vào Google Sheets.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **API Key của Google Gemini 2.0**:
   - Đăng ký tại [Google AI Studio](https://makersuite.google.com/app/apikey) để lấy `API Key`.
   - Trong n8n, tạo **credentials mới** với tên `googlePalmApi` và gán `API Key` vào trường `Api Key`.

2. **Hình ảnh mẫu** (tải từ URL hoặc upload trực tiếp):
   - Hình ảnh phải rõ nét và không quá phức tạp (tránh quá nhiều đối tượng trùng lặp).
   - **Yêu cầu bắt buộc**: Hình ảnh phải có thông tin chiều rộng và chiều cao (do node `Edit Image` sử dụng).

3. **n8n Self-hosted** (khuyến nghị):
   - Để workflow chạy ổn định 24/7, các sếp nên cài đặt n8n trên **VPS riêng**.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/2649) hoặc copy toàn bộ mã JSON từ trang này.
- Mở **n8n Editor** → Nhấn `Import` → Dán JSON hoặc tải file `.json` lên.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **7 node chính**, các sếp cần chú ý cấu hình sau:

#### **Node 1: Manual Trigger (Bắt đầu workflow)**
- **Không cần chỉnh gì**, chỉ dùng để test workflow.

#### **Node 2: Get Variables (Lấy biến)**
- **Không cần chỉnh**, node này chuẩn bị dữ liệu cho các bước tiếp theo.

#### **Node 3: Get Test Image (Tải hình ảnh)**
- **Chỉnh URL hình ảnh**:
  - Thay đổi giá trị trong `Request URL` thành đường dẫn hình ảnh của các sếp (ví dụ: `https://example.com/image.jpg`).
  - **Lưu ý**: Hình ảnh phải có chiều rộng và chiều cao (node `Edit Image` sẽ sử dụng thông tin này).

#### **Node 4: Gemini 2.0 Object Detection (Phát hiện đối tượng)**
- **Chọn credentials**:
  - Trong `Credentials`, chọn `googlePalmApi` (đã tạo trước đó).
- **Chỉnh Prompt**:
  - Thay đổi nội dung trong `Body` để yêu cầu AI phát hiện đối tượng cụ thể. Ví dụ:
    ```json
    {
      "contents": [
        {
          "parts": [
            {
              "text": "Find all bunnies in this image and return their bounding boxes."
            },
            {
              "inlineData": {
                "mimeType": "image/jpeg",
                "data": "{{ $json.image.data }}"
              }
            }
          ]
        }
      ]
    }
    ```
  - **Lưu ý**: Thay `{{ $json.image.data }}` bằng biến chứa hình ảnh (nếu cần).

#### **Node 5: Scale Normalised Coords (Điều chỉnh tọa độ)**
- **Không cần chỉnh**, node này tự động tính toán tọa độ dựa trên chiều rộng/chiều cao của hình ảnh.

#### **Node 6: Draw Bounding Boxes (Vẽ khung bao quanh)**
- **Không cần chỉnh gì**, node này tự động vẽ khung bao quanh các đối tượng đã phát hiện.

#### **Node 7: Get Image Info (Lấy thông tin hình ảnh)**
- **Không cần chỉnh**, node này lấy chiều rộng/chiều cao để node `Scale Normalised Coords` sử dụng.

---
### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn `Run Workflow` để kiểm tra kết quả.
   - Kiểm tra hình ảnh đầu ra có khung bao quanh đối tượng không.
2. **Bật Active**:
   - Sau khi test thành công, chuyển trạng thái workflow sang `Active`.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁCH ÁP DỤNG THỰC TẾ]
1. **Kết nối với Slack/Telegram**:
   - Sau khi workflow hoàn thành, thêm node `Slack` hoặc `Telegram Bot` để gửi kết quả (hình ảnh có khung bao) về chat nhóm.

2. **Lưu log vào Google Sheets**:
   - Thêm node `Google Sheets` để ghi lại kết quả phát hiện (ví dụ: danh sách đối tượng, tọa độ, độ tin cậy).

3. **Tự động xử lý nhiều hình ảnh**:
   - Sử dụng node `HTTP Request` để tải nhiều hình ảnh từ một thư mục (ví dụ: Google Drive) và chạy workflow cho từng hình.

4. **Tối ưu Prompt**:
   - Thử các prompt khác nhau để cải thiện độ chính xác:
     - `"Detect all cars parked illegally in this image."`
     - `"Find faces with sad expressions and draw bounding boxes."`
     - `"Highlight all products with defects in this inventory photo."`

5. **Dùng cho phân tích y tế**:
   - Prompt: `"Detect all abnormal cells in this medical image."` (cần kiểm tra với chuyên gia y tế).
:::

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần tự động hóa việc phân tích hình ảnh mà không cần viết code. Từ **kiểm tra an toàn giao thông** đến **quản lý kho hàng**, hoặc thậm chí là **phân tích cảm xúc**, Gemini 2.0 cùng n8n sẽ giúp tiết kiệm thời gian và nâng cao hiệu quả công việc.

**Hãy thử ngay!**
1. Import workflow vào n8n của mình.
2. Chỉnh sửa Prompt và hình ảnh mẫu.
3. Nhấn `Run` và xem AI làm việc như thế nào!

---
**Cần hỗ trợ?**
- **Discord n8n**: [https://discord.com/invite/XPKeKXeB7d](https://discord.com/invite/XPKeKXeB7d)
- **Forum n8n**: [https://community.n8n.io/](https://community.n8n.io/)

**Happy Hacking!** 🚀