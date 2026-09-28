---
title: "🚀 Tự động hóa phát hiện bất thường với Qdrant và n8n: Cài đặt trung tâm cụm và ngưỡng"
description: "Hướng dẫn chi tiết cách tự động hóa việc thiết lập trung tâm cụm và ngưỡng phát hiện bất thường bằng workflow n8n kết hợp Qdrant, Voyage AI và Google Cloud Storage"
slug: "tu-dong-hoa-phat-hien-bat-thuong-qdrant-n8n"
tags: [n8n, automation, no-code, Qdrant, AI, SecOps]
keywords: [n8n workflow, tự động hóa, phát hiện bất thường, Qdrant, AI]
---

# 🚀 Tự động hóa phát hiện bất thường với Qdrant và n8n: Cài đặt trung tâm cụm và ngưỡng

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải phân tích thủ công hàng nghìn hình ảnh nông sản để phát hiện bất thường. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quá trình thiết lập trung tâm cụm và ngưỡng phát hiện bất thường
- Tiết kiệm thời gian xử lý hàng nghìn hình ảnh nông sản
- Phát hiện bất thường chính xác hơn với hai phương pháp khác nhau
- Hệ thống hoạt động liên tục 24/7 mà không cần can thiệp thủ công
- Kết quả được lưu trữ và quản lý trong Qdrant Cloud
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Qdrant Cloud (có thể sử dụng Free Tier)
- API key cho Qdrant Cloud
- API key cho Voyage AI
- Tài khoản Google Cloud Storage với bucket chứa dataset nông sản
- Dataset nông sản từ Kaggle (hoặc dataset tương tự)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào [n8n.io/workflows/2655](https://n8n.io/workflows/2655)
2. Click vào nút "Import" ở góc trên bên phải
3. Trong n8n Editor, click vào "Import from URL" và dán link trên
4. Hoặc copy toàn bộ JSON workflow và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "When clicking ‘Test workflow’" (manualTrigger)**
   - Không cần cấu hình gì, chỉ cần kích hoạt khi test workflow

2. **Node "Total Points in Collection" (httpRequest)**
   - Cấu hình credentials: Chọn "qdrantApi" đã tạo trước đó
   - URL: `https://<your-cluster-url>/collections/<your-collection-name>/points/count`
   - Method: POST
   - Headers: `Content-Type: application/json`

3. **Node "Cluster Distance Matrix" (httpRequest)**
   - Cấu hình credentials: Chọn "qdrantApi" đã tạo trước đó
   - URL: `https://<your-cluster-url>/collections/<your-collection-name>/points/distance`
   - Method: POST
   - Headers: `Content-Type: application/json`
   - Body: JSON với các tham số cần thiết (xem hướng dẫn gốc)

4. **Node "Scipy Sparse Matrix" (code)**
   - Cần cài đặt thư viện scipy trong n8n (nếu chưa có)
   - Code xử lý ma trận thưa sẽ được cung cấp trong workflow

5. **Node "Set medoid id" (httpRequest)**
   - Cấu hình credentials: Chọn "qdrantApi" đã tạo trước đó
   - URL: `https://<your-cluster-url>/collections/<your-collection-name>/points/payload`
   - Method: PUT
   - Headers: `Content-Type: application/json`

6. **Node "Get Medoid Vector" (httpRequest)**
   - Cấu hình credentials: Chọn "qdrantApi" đã tạo trước đó
   - URL: `https://<your-cluster-url>/collections/<your-collection-name>/points`
   - Method: POST
   - Headers: `Content-Type: application/json`

7. **Node "Prepare for Searching Threshold" (set)**
   - Cấu hình các biến cần thiết cho quá trình tìm ngưỡng

8. **Node "Searching Score" (httpRequest)**
   - Cấu hình credentials: Chọn "qdrantApi" đã tạo trước đó
   - URL: `https://<your-cluster-url>/collections/<your-collection-name>/points/search`
   - Method: POST
   - Headers: `Content-Type: application/json`

9. **Node "Threshold Score" (set)**
   - Cấu hình biến lưu trữ ngưỡng phát hiện bất thường

10. **Node "Set medoid threshold score" (httpRequest)**
    - Cấu hình credentials: Chọn "qdrantApi" đã tạo trước đó
    - URL: `https://<your-cluster-url>/collections/<your-collection-name>/points/payload`
    - Method: PUT
    - Headers: `Content-Type: application/json`

11. **Node "Textual (visual) crop descriptions" (set)**
    - Cập nhật mô tả văn bản cho từng loại cây trồng

12. **Node "Embed text" (httpRequest)**
    - Cấu hình credentials: Chọn "httpHeaderAuth" đã tạo trước đó
    - URL: `https://api.voyageai.com/v1/embeddings`
    - Method: POST
    - Headers: `Content-Type: application/json` và `Authorization: Bearer <your-api-key>`

13. **Node "Get Medoid by Text" (httpRequest)**
    - Cấu hình credentials: Chọn "qdrantApi" đã tạo trước đó
    - URL: `https://<your-cluster-url>/collections/<your-collection-name>/points/search`
    - Method: POST
    - Headers: `Content-Type: application/json`

14. **Node "Set text medoid id" (httpRequest)**
    - Cấu hình credentials: Chọn "qdrantApi" đã tạo trước đó
    - URL: `https://<your-cluster-url>/collections/<your-collection-name>/points/payload`
    - Method: PUT
    - Headers: `Content-Type: application/json`

15. **Node "Prepare for Searching Threshold1" (set)**
    - Cấu hình các biến cần thiết cho quá trình tìm ngưỡng

16. **Node "Threshold Score1" (set)**
    - Cấu hình biến lưu trữ ngưỡng phát hiện bất thường

17. **Node "Searching Text Medoid Score" (httpRequest)**
    - Cấu hình credentials: Chọn "qdrantApi" đã tạo trước đó
    - URL: `https://<your-cluster-url>/collections/<your-collection-name>/points/search`
    - Method: POST
    - Headers: `Content-Type: application/json`

18. **Node "Medoids Variables" (set)**
    - Cấu hình các biến liên quan đến trung tâm cụm

19. **Node "Text Medoids Variables" (set)**
    - Cấu hình các biến liên quan đến trung tâm cụm văn bản

20. **Node "Qdrant cluster variables" (set)**
    - Cấu hình các biến liên quan đến cụm Qdrant

21. **Node "Info About Crop Clusters" (set)**
    - Cấu hình thông tin về các cụm cây trồng

22. **Node "Crop Counts" (httpRequest)**
    - Cấu hình credentials: Chọn "qdrantApi" đã tạo trước đó
    - URL: `https://<your-cluster-url>/collections/<your-collection-name>/points/facet`
    - Method: POST
    - Headers: `Content-Type: application/json`

23. **Node "Set text medoid threshold score" (httpRequest)**
    - Cấu hình credentials: Chọn "qdrantApi" đã tạo trước đó
    - URL: `https://<your-cluster-url>/collections/<your-collection-name>/points/payload`
    - Method: PUT
    - Headers: `Content-Type: application/json`

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Test workflow" để kiểm tra
2. Kiểm tra kết quả đầu ra của từng node để đảm bảo dữ liệu được xử lý đúng
3. Khi đã kiểm tra xong, click vào nút "Active workflow" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- 1. **Tối ưu hóa hiệu suất**: Các sếp có thể điều chỉnh tham số `sample` và `limit` trong node "Cluster Distance Matrix" để giảm thời gian xử lý cho các tập dữ liệu lớn.
- 2. **Kết hợp với Slack**: Thêm node Slack để nhận thông báo khi workflow hoàn thành hoặc gặp lỗi.
- 3. **Lưu log hoạt động**: Sử dụng node "File" để lưu log hoạt động của workflow cho việc audit sau này.
- 4. **Tự động hóa báo cáo**: Kết hợp với Google Sheets để tự động tạo báo cáo hàng ngày về các điểm bất thường được phát hiện.

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa quá trình thiết lập trung tâm cụm và ngưỡng phát hiện bất thường trong các tập dữ liệu hình ảnh nông sản. Với hai phương pháp phát hiện khác nhau (dựa trên ma trận khoảng cách và mô hình nhúng đa phương tiện), các sếp có thể phát hiện bất thường một cách chính xác và hiệu quả. Hãy áp dụng ngay workflow này để tiết kiệm thời gian và nâng cao hiệu suất phân tích dữ liệu của doanh nghiệp!