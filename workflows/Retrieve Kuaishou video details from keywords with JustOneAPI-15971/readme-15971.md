---
title: "🔍 Tự Động Lấy Chi Tiết Video Kuaishou Từ Từ Khóa Với JustOneAPI (N8N) - Không Cần Code!"
description: "Tự động hóa việc tra cứu và lấy thông tin chi tiết video Kuaishou từ từ khóa bằng API JustOneAPI, tiết kiệm thời gian nghiên cứu thị trường lên đến 90%. Workflow hoàn toàn tự động, hoạt động 24/7 trên VPS."
slug: "tu-dong-hoa-lay-thong-tin-video-kuaishou-justoneapi"
tags: [n8n, automation, market-research, justoneapi, api-integration]
keywords: [n8n workflow kuaishou, tự động hóa nghiên cứu thị trường, lấy video kuaishou bằng api, justoneapi n8n, tự động hóa không code]
---

# 🚀 **Tự Động Lấy Chi Tiết Video Kuaishou Từ Từ Khóa Với JustOneAPI (N8N)**

### **Giải pháp cho các sếp muốn nghiên cứu thị trường Kuaishou một cách nhanh chóng, chính xác và không cần viết code**

---

### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Thay vì tra cứu thủ công trên Kuaishou, workflow tự động lấy dữ liệu trong vài giây.
- **Dữ liệu chính xác**: API JustOneAPI cung cấp thông tin video chi tiết (tên, lượt xem, thời lượng, hashtag,...) với độ chính xác cao.
- **Hoạt động liên tục**: Cài đặt trên VPS, workflow chạy 24/7 mà không cần can thiệp.
- **Cá nhân hóa**: Thêm từ khóa hoặc lọc video theo tiêu chí riêng (ví dụ: video mới nhất, video có hashtag nhất định).
- **Dữ liệu sẵn sàng phân tích**: Kết quả được xuất dưới dạng JSON hoặc kết nối với Google Sheets/Excel để phân tích thị trường.
:::

---

### **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản JustOneAPI**:
   - Đăng ký tại [JustOneAPI](https://www.justoneapi.com/) và lấy **API Key**.
   - Đăng ký **plan** phù hợp (ví dụ: "Kuaishou Search" và "Kuaishou Video Detail").
   - Tham khảo [đường dẫn API Kuaishou](https://www.justoneapi.com/api/kuaishou) để lấy endpoint chính xác.

2. **VPS cho n8n (Self-hosted)**:
   - Để workflow chạy 24/7 ổn định, các sếp nên cài n8n trên **VPS riêng**.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

3. **N8N Credentials**:
   - Trong n8n Editor, tạo **credentials** mới với tên `JustOneAPI` và gán **API Key** từ JustOneAPI.
   - Cấu hình **base URL** của API Kuaishou (ví dụ: `https://api.justoneapi.com/kuaishou`).

---

### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/15971) hoặc copy toàn bộ JSON từ trang này.
- Trong **n8n Editor**, nhấn **Import Workflow** và dán JSON vào.
- **Lưu workflow** với tên **`Kuaishou Video Research`**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **10 node** chính, các sếp cần chú ý cấu hình các node sau:

##### **🔹 Node 1: Manual Trigger Start**
- **Không cần chỉnh**, chỉ dùng để kích hoạt workflow thủ công.

##### **🔹 Node 2: Prepare API and Research Fields (Set)**
- **Thêm từ khóa tra cứu** vào trường `keyword` (ví dụ: `máy tính xách tay`).
- **Cấu hình các tham số API** (nếu cần):
  - `page`: Trang kết quả (mặc định là 1).
  - `limit`: Số video trả về (mặc định là 10).
  - Thêm các **filter** tùy chọn (ví dụ: `publish_time` để lấy video mới nhất).

##### **🔹 Node 3: Search Kuaishou Videos via API (HTTP Request)**
- **URL**: `https://api.justoneapi.com/kuaishou/search?keyword={{ $json["keyword"] }}&page={{ $json["page"] }}&limit={{ $json["limit"] }}`
- **Headers**:
  - `Authorization`: `Bearer {{ $credentials["JustOneAPI"]["apiKey"] }}`
  - `Content-Type`: `application/json`
- **Method**: `GET`
- **Lưu ý**: Nếu API yêu cầu thêm tham số, thêm vào URL hoặc body request.

##### **🔹 Node 4: Extract Video IDs with Code (Code)**
- **Mã JavaScript**:
  ```javascript
  // Lấy danh sách video IDs từ kết quả search
  const videoIds = [];
  $json["data"].forEach(video => {
    videoIds.push(video.id);
  });
  return { videoIds };
  ```
- **Kiểm tra**: Nếu kết quả search trống, workflow sẽ dừng ở node **If Video ID Exists**.

##### **🔹 Node 5: If Video ID Exists (If)**
- **Điều kiện**: `$json["videoIds"].length > 0`
- Nếu **true**, workflow tiếp tục lấy chi tiết video; nếu **false**, kết thúc workflow.

##### **🔹 Node 6: Fetch Video Details via API (HTTP Request)**
- **URL**: `https://api.justoneapi.com/kuaishou/video?id={{ $json["videoIds"][0] }}`
- **Headers** (giống Node 3).
- **Method**: `GET`
- **Lưu ý**: Nếu muốn lấy chi tiết cho **tất cả video**, sử dụng **Loop** hoặc **Set** để xử lý danh sách.

##### **🔹 Node 7: Build Video Details with Code (Code)**
- **Mã JavaScript** (cập nhật theo cấu trúc dữ liệu API):
  ```javascript
  // Kết hợp dữ liệu video chi tiết
  const videoDetails = {
    id: $json["id"],
    title: $json["title"],
    views: $json["views"],
    duration: $json["duration"],
    hashtags: $json["hashtags"],
    publishTime: $json["publishTime"],
    // Thêm các trường khác theo cần thiết
  };
  return { videoDetails };
  ```
- **Kiểm tra**: Đảm bảo các trường trong mã phù hợp với API JustOneAPI.

##### **🔹 Node 8: Output Video Details List (Set)**
- **Dữ liệu đầu ra** sẽ chứa danh sách video chi tiết dưới dạng JSON.
- **Lưu ý**: Nếu muốn xuất ra **Google Sheets**, thêm node **Google Sheets** và cấu hình.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** và nhập từ khóa (ví dụ: `sản phẩm mới`).
   - Kiểm tra kết quả ở **Node 8** để đảm bảo dữ liệu chính xác.

2. **Bật Active**:
   - Chuyển trạng thái workflow từ **Draft** sang **Active**.

---

### **✍️ Mẹo & gợi ý nâng cao**
:::info[CÁCH LÀM THÊM]
1. **Lưu kết quả vào Google Sheets/Excel**:
   - Thêm node **Google Sheets** sau **Node 8** và cấu hình để ghi dữ liệu vào sheet mới.
   - Cấu hình **credentials** Google Sheets trong n8n.

2. **Gửi báo cáo định kỳ qua Email/Slack**:
   - Thêm node **Email** (n8n-nodes-base.email) hoặc **Slack** (n8n-nodes-base.slack) để gửi kết quả tự động.
   - Ví dụ: Gửi báo cáo hàng tuần về video mới nhất.

3. **Lọc video theo tiêu chí**:
   - Trong **Node 2**, thêm các filter như:
     - `publish_time`: Lấy video mới nhất trong 7 ngày.
     - `hashtags`: Chỉ lấy video có hashtag `#sản phẩm`.

4. **Tự động hóa tra cứu định kỳ**:
   - Thay **Manual Trigger** bằng **Schedule Trigger** (n8n-nodes-base.scheduleTrigger) để chạy workflow hàng ngày/lần tuần.

5. **Xử lý lỗi API**:
   - Thêm node **Error Handling** (n8n-nodes-base.if) để xử lý trường hợp API trả về lỗi (ví dụ: từ khóa không hợp lệ).
   - Ví dụ:
     ```javascript
     if ($json["error"]) {
       return { error: $json["error"] };
     }
     ```

---

### **📌 Kết luận**
Workflow này giúp các sếp **tự động hóa việc nghiên cứu thị trường Kuaishou một cách nhanh chóng và chính xác**, tiết kiệm thời gian lên đến **90%** so với cách làm thủ công. Bằng cách kết nối với **JustOneAPI** và cài đặt trên **VPS**, workflow sẽ hoạt động **24/7** mà không cần can thiệp.

**🚀 Hành động ngay!**
1. **Cài đặt n8n trên VPS** (sử dụng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình API Key JustOneAPI.
3. **Test với từ khóa** và bắt đầu nghiên cứu thị trường!

---
**💡 Cần hỗ trợ?** Đăng ký tư vấn miễn phí tại [n8n.io](https://n8n.io/) hoặc liên hệ với cộng đồng n8n tại [Discord](https://discord.gg/n8n).