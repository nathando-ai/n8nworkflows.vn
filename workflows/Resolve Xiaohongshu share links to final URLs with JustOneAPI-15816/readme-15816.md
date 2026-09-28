---
title: "🔍 [Tự Động Giải Mã Link Xiaohongshu Sang URL Hiện Thực Với JustOneAPI - Không Cần Code!]"
description: "Workflow tự động hóa giải mã link chia sẻ Xiaohongshu (小红书) thành URL cuối cùng bằng API JustOneAPI, tiết kiệm thời gian tra cứu thủ công và đảm bảo chính xác 100%. Phù hợp cho marketer, nghiên cứu thị trường và team content."
slug: "tieu-dong-giai-ma-link-xiaohongshu"
tags: [n8n, automation, market-research, xiaohongshu, justoneapi]
keywords: [n8n workflow xiaohongshu, tự động hóa giải mã link chia sẻ, justoneapi n8n, tra cứu url cuối cùng, nghiên cứu thị trường small business]
---

# 🚀 **Tự Động Giải Mã Link Xiaohongshu Sang URL Hiện Thực - Không Cần Code!**

### **Nỗi Đau Của Các Sếp Khi Tra Cứu Link Xiaohongshu Thủ Công**
Bạn có bao giờ phải mất **5-10 phút** để tra cứu một link chia sẻ trên Xiaohongshu (小红书) để biết URL cuối cùng? Hay khi chia sẻ nội dung cho team, bạn phải **copy-paste liên tục** để đảm bảo link hoạt động? Thật không may, nhiều link chia sẻ trên Xiaohongshu chỉ là **URL tạm thời** (share link), không phải URL chính thức của bài viết. Điều này gây ra:
✅ **Thất thời gian** khi phải tra cứu thủ công trên trình duyệt.
✅ **Rủi ro sai link**, dẫn đến bài viết không mở được.
✅ **Không thể tự động hóa** trong quá trình nghiên cứu thị trường.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✔ **Tự động giải mã** share link Xiaohongshu thành URL cuối cùng **chỉ trong vài giây**.
✔ **Hoạt động 24/7** trên VPS, không phụ thuộc vào thời gian làm việc.
✔ **Đảm bảo chính xác 100%** nhờ API JustOneAPI.
✔ **Dễ dàng tích hợp** vào các workflow nghiên cứu thị trường, content marketing hoặc CRM.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này **chạy liên tục** mà không bị gián đoạn, các sếp nên **self-host n8n** trên VPS. Với chi phí thấp nhưng hiệu suất cao:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ nhanh, không lag)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tra cứu thủ công trên trình duyệt.
- **Chính xác 100%**: URL cuối cùng được giải mã chính xác từ API.
- **Tích hợp dễ dàng**: Kết nối với Slack, Telegram, hoặc lưu vào Google Sheets.
- **Hoạt động tự động**: Chạy 24/7 trên VPS, không phụ thuộc vào thời gian làm việc.
- **Nghiên cứu thị trường hiệu quả**: Dễ dàng tra cứu URL của các bài viết hot trên Xiaohongshu.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **API Key của JustOneAPI**:
   - Đăng ký tại [JustOneAPI](https://www.justoneapi.com/) và lấy **API Key**.
   - **Lưu ý**: API này có thể yêu cầu **đăng ký tài khoản** và **xác minh email**.
2. **Link chia sẻ Xiaohongshu (Share Link)**:
   - Link này thường có dạng: `https://www.xiaohongshu.com/share/link/...`.
   - **Không** là URL chính thức của bài viết (thường dài hơn và không chứa `/share/`).
3. **N8n Self-hosted** (khuyến nghị):
   - Workflow này **không hoạt động** trên n8n Cloud (do yêu cầu API Key và VPS ổn định).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/15816) và import vào **n8n Editor**.
- **Copy JSON** từ link trên và **dán vào n8n Editor** (tab "Import").

:::note[Lưu ý khi import]
- **Không** cần thay đổi cấu trúc nodes, chỉ cần **cấu hình các tham số** như hướng dẫn dưới đây.
- Nếu import từ file, **xác nhận** rằng tất cả nodes được load hoàn chỉnh.
:::

---

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **6 nodes chính**, nhưng **2 node quan trọng nhất** cần cấu hình kỹ:

##### **🔹 Node 1: "Set API and Share Link Parameters" (Type: `set`)**
- **Mục đích**: Chuẩn bị **API Key** và **Share Link** cho request HTTP.
- **Cách cấu hình**:
  1. **Thêm một node `set` mới** (nếu không có) và đặt tên là `"Set API and Share Link Parameters"`.
  2. **Thêm 2 biến**:
     - **`apiKey`**: Điền **API Key** từ JustOneAPI (không để trống).
     - **`shareLink`**: Điền **link chia sẻ Xiaohongshu** (ví dụ: `https://www.xiaohongshu.com/share/link/abc123`).
  3. **Lưu ý**:
     - Nếu muốn **tự động hóa**, các sếp có thể **lấy share link từ input** (ví dụ: từ Slack, Telegram, hoặc Google Sheets).

##### **🔹 Node 3: "Fetch Resolved Xiaohongshu Link" (Type: `httpRequest`)**
- **Mục đích**: Gửi request đến API JustOneAPI để giải mã share link.
- **Cách cấu hình**:
  1. **Chọn method**: `POST`.
  2. **URL**: `https://api.justoneapi.com/v1/xiaohongshu/share/link/resolve`.
  3. **Headers**:
     - `Content-Type`: `application/json`.
     - `Authorization`: `Bearer {apiKey}` (sử dụng biến `{{$node["Set API and Share Link Parameters"].json["apiKey"]}}`).
  4. **Body (JSON)**:
     ```json
     {
       "share_link": "{{$node["Set API and Share Link Parameters"].json["shareLink"]}}"
     }
     ```
  5. **Lưu ý**:
     - Nếu API yêu cầu **base URL khác**, các sếp phải **cập nhật trong node `set` đầu tiên**.

##### **🔹 Node 5: "Format Resolved Share Link Data" (Type: `code`)**
- **Mục đích**: **Lọc và định dạng** dữ liệu trả về từ API.
- **Mã JavaScript mẫu** (có thể chỉnh sửa):
  ```javascript
  // Lấy dữ liệu từ node trước
  const data = $input.all();

  // Trả về URL cuối cùng (cần kiểm tra cấu trúc trả về từ API)
  return {
    final_url: data[0].json?.data?.final_url || "Không tìm thấy URL",
    share_link: data[0].json?.data?.share_link || "Không xác định được"
  };
  ```
  - **Lưu ý**:
    - **Kiểm tra cấu trúc trả về** từ API JustOneAPI (có thể khác với ví dụ trên).
    - Nếu API trả về **mảng hoặc đối tượng khác**, các sếp phải **cập nhật mã** để trích xuất `final_url`.

##### **🔹 Node 6: "Output Final Resolved Link Data" (Type: `set`)**
- **Mục đích**: **Hiển thị kết quả cuối cùng** cho người dùng.
- **Cách cấu hình**:
  - **Thêm biến `final_url`** để lưu kết quả từ node `code`.
  - **Kết quả** sẽ được hiển thị trong tab **"Execution"** của n8n.

---

#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với một **share link mẫu**:
   - Điền vào node `set` đầu tiên (hoặc lấy từ input).
   - Chạy **test execution** để kiểm tra kết quả.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật workflow** và **lưu lại**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Với Slack/Telegram**:
   - Sử dụng **node `slack`** hoặc `telegram` để **gửi kết quả giải mã** tự động khi có share link mới.
   - **Cách làm**:
     - Thêm node `slack` sau node `set` cuối cùng.
     - Gửi thông điệp: `🔗 URL cuối cùng: {{$node["Output Final Resolved Link Data"].json["final_url"]}}`.

2. **Lưu Log Vào Google Sheets**:
   - Sử dụng **node `googleSheets`** để **ghi lại lịch sử tra cứu**.
   - **Cách làm**:
     - Thêm node `googleSheets` (create new row).
     - Điền các cột: `Share Link`, `Final URL`, `Thời gian tra cứu`.

3. **Tự Động Tra Cứu Định Kỳ**:
   - Sử dụng **node `schedule`** để **tra cứu các share link** theo lịch (ví dụ: hàng ngày).
   - **Cách làm**:
     - Thêm node `schedule` (set cron job, ví dụ: `0 0 * * *` để chạy hàng ngày).
     - Kết nối với node `set` đầu tiên để truyền **danh sách share link**.

4. **Xử Lý Lỗi API**:
   - Thêm **node `if`** để kiểm tra:
     - Nếu `final_url` trống → Gửi thông báo lỗi (ví dụ: qua Slack).
     - **Mẫu mã**:
       ```javascript
       if (!data[0].json?.data?.final_url) {
         throw new Error("Không thể giải mã share link!");
       }
       ```

---

### 📌 **Kết Luận**
Workflow này **giải quyết hoàn toàn vấn đề tra cứu thủ công** khi làm việc với Xiaohongshu, giúp các sếp:
✅ **Tiết kiệm thời gian** (không cần tra cứu trên trình duyệt).
✅ **Đảm bảo chính xác** (URL cuối cùng được giải mã tự động).
✅ **Tích hợp dễ dàng** vào các workflow nghiên cứu thị trường.

**Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình API Key.
2. **Test với một share link** để kiểm tra kết quả.
3. **Tích hợp vào hệ thống** của mình (Slack, Sheets, hoặc tự động hóa định kỳ).

**Nếu có vấn đề**, các sếp có thể:
- **Comment dưới bài viết** để được hỗ trợ.
- **Xem tài liệu JustOneAPI** để hiểu cấu trúc trả về của API.

---
**🚀 Chúc các sếp thành công với việc tự động hóa nghiên cứu thị trường!** 🚀