---
title: "🚀 Xây dựng hệ thống Phân loại Ảnh tự động với thuật toán KNN và Qdrant Vector Database trên n8n"
description: "Hướng dẫn chi tiết cách tự động phân loại ảnh vệ tinh (land use) cực kỳ chính xác bằng thuật toán KNN kết hợp Voyage AI Embedding và Qdrant Vector Database trong n8n."
slug: "phan-loai-anh-tu-dong-knn-qdrant-n8n"
tags: [n8n, automation, ai, qdrant, machine-learning, knn]
keywords: [n8n workflow, phan loai anh, qdrant vector database, knn classifier, voyage ai, tu dong hoa ai]
---

# 🚀 Xây dựng hệ thống Phân loại Ảnh tự động với thuật toán KNN và Qdrant Vector Database trên n8n

Các sếp có bao giờ gặp khó khăn khi phải phân loại thủ công hàng ngàn bức ảnh vệ tinh hoặc hình ảnh phong phú của doanh nghiệp? Việc này không chỉ tốn hàng đống thời gian, dễ gây nhầm lẫn mà còn đòi hỏi chi phí huấn luyện mô hình Machine Learning phức tạp. 

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code (No-code AI), giúp phân loại chính xác các đối tượng trong ảnh dựa trên thuật toán K-Nearest Neighbors (KNN) kết hợp với **Qdrant Vector Database** và mô hình đa phương thức từ **Voyage.ai**. Điểm đặc biệt là giải pháp này đạt độ chính xác lên tới **93.24%** trên tập test mà không cần fine-tuning phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Nhận URL ảnh đầu vào qua API/Trigger và trả về nhãn phân loại (class) ngay lập tức.
- **Độ chính xác cao:** Đạt hơn 93% dựa trên tập dữ liệu ảnh mẫu (Landuse Scene Classification).
- **Thuật toán thông minh xử lý đồng hạng (Tie Loop):** Tự động tăng giới hạn hàng xóm (`limitKNN`) nếu kết quả bình chọn (Majority Vote) bị hòa, đảm bảo luôn tìm ra đáp án chính xác.
- **Linh hoạt thích ứng:** Có thể áp dụng cho bất kỳ tập dữ liệu ảnh nào của doanh nghiệp (sản phẩm, tài liệu, cảnh quan...).
:::

### 📦 Các loại cảnh quan hệ thống hỗ trợ sẵn (Land Types)
Workflow này được thiết kế để phân loại các dạng ảnh vệ tinh bao gồm:
`agricultural`, `airplane`, `baseballdiamond`, `beach`, `buildings`, `chaparral`, `denseresidential`, `forest`, `freeway`, `golfcourse`, `harbor`, `intersection`, `mediumresidential`, `mobilehomepark`, `overpass`, `parkinglot`, `river`, `runway`, `sparseresidential`, `storagetanks`, `tenniscourt`.

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI LÊN ĐỒ]
- **Tài khoản n8n:** Đã thiết lập sẵn sàng để import workflow.
- **Qdrant Cloud Account:** Tạo một cluster miễn phí trên [Qdrant Cloud](https://qdrant.tech/documentation/quickstart-cloud/) và chuẩn bị API Key.
- **Voyage AI API Key:** Dùng để gọi mô hình Multimodal Embeddings (`Embed image` node).
- **Tập dữ liệu (Dataset):** Đã tải [Lands Dataset từ Kaggle](https://www.kaggle.com/datasets/apollo2506/landuse-scene-classification) và upload lên Qdrant collection của sếp.
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ kho lưu trữ n8n.
- Trong giao diện n8n, chọn **Add workflow** -> **Import from File** (hoặc copy toàn bộ JSON và dán trực tiếp vào màn hình làm việc của n8n).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm các nodes chính sau cần được cấu hình thông số kỹ thuật chính xác:

- **Execute Workflow Trigger (`Execute Workflow Trigger`):** Điểm khởi chạy nhận URL ảnh đầu vào từ các workflow khác hoặc hệ thống bên ngoài.
- **Embed image (`httpRequest`):** 
  - Cần cấu hình thông tin xác thực (`httpHeaderAuth`) với API của Voyage.ai để chuyển đổi ảnh đầu thành dạng vector embedding.
- **Query Qdrant (`httpRequest`):**
  - Sử dụng thông tin xác thực `qdrantApi`.
  - Trỏ đến Qdrant Collection của các sếp chứa dữ liệu mẫu đã được gán nhãn sẵn từ trước.
- **Majority Vote (`code` node):** 
  - Node này dùng mã Javascript để quét payloads từ các hàng xóm gần nhất (nearest neighbours) và tính toán tên lớp xuất hiện nhiều nhất.
- **Check tie & Propagate loop variables / Increase limitKNN (`if` & `set` nodes):** 
  - Xử lý kịch bản hòa phiếu (ví dụ: 5 ảnh "forest" và 5 ảnh "harbor"). Node sẽ tự động cộng thêm 5 hàng xóm vào `limitKNN` và lặp lại quá trình cho đến khi tìm ra kết quả hoặc chạm mốc kiểm tra 100 hàng xóm.
- **Return class (`set`):** Trả về kết quả tên lớp cuối cùng cho workflow gọi tới.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một URL ảnh mẫu bất kỳ thuộc nhóm danh mục được hỗ trợ.
- Kiểm tra kết quả trả về ở node cuối cùng.
- Bật công tắc **Active** để đưa workflow vào vận hành tự động thực tế.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kết nối thông báo:** Thêm node Telegram hoặc Slack ngay sau node `Return class` để bắn thông báo kết quả phân loại ảnh về nhóm chat làm việc của team theo thời gian thực.
- **Lưu lịch sử (Logging):** Lưu các kết quả phân loại vào Google Sheets hoặc Airtable để làm dữ liệu thống kê hoặc kiểm định mô hình về sau.
- **Tùy biến Dataset:** Sếp hoàn toàn có thể thay thế tập dữ liệu ảnh vệ tinh bằng tập ảnh sản phẩm E-commerce hoặc phân loại lỗi sản phẩm (Anomaly Detection) của nhà máy.

---

### 📌 Kết luận
Hệ thống phân loại ảnh tự động dựa trên KNN và Qdrant Vector Database là một "vũ khí" cực kỳ mạnh mẽ giúp tối ưu hóa các bài toán xử lý hình ảnh phức tạp mà không tốn chi phí huấn luyện AI nặng nhọc. Hãy import ngay workflow này vào hệ thống n8n của các sếp và bắt đầu tự động hóa quy trình ngay hôm nay!