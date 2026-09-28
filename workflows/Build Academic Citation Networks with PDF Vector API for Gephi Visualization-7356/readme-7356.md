---
title: "🚀 Xây dựng Mạng Liên Kết Tài Liệu Học Thuật với PDF Vector API cho Gephi"
description: "Tự động thu thập, xây dựng và xuất dữ liệu mạng trích dẫn từ các tài liệu học thuật, giúp trực quan hóa nhanh chóng trong Gephi."
slug: "xay-dung-mang-lien-ket-tai-liệu-hoc-thuat"
tags: [n8n, automation, no-code, pdfvector, gephi, academic]
keywords: [n8n workflow, tự động hóa, PDF Vector, mạng trích dẫn, Gephi, xuất dữ liệu, khoa học dữ liệu]
---

# 🚀 Xây dựng Mạng Liên Kết Tài Liệu Học Thuật với PDF Vector API cho Gephi

Bạn đang muốn phân tích mối quan hệ giữa các bài báo khoa học, nhưng việc thu thập dữ liệu trích dẫn thủ công là một công việc tốn thời gian và dễ sai sót. Workflow này giúp bạn **tự động** lấy dữ liệu từ PDF Vector, xây dựng mạng trích dẫn và xuất ra định dạng GEXF – chuẩn của Gephi – hoàn toàn **không cần viết code**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ làm thủ công thành vài phút tự động.  
- **Chính xác cao**: Dữ liệu được lấy trực tiếp từ API, tránh lỗi nhập liệu.  
- **Cá nhân hóa**: Định nghĩa độ sâu (depth) và danh sách ID tùy ý.  
- **Hoạt động liên tục**: Workflow có thể chạy theo lịch hoặc qua webhook.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Tài khoản PDF Vector**: Đăng ký API key tại https://pdfvector.com.  
- **Node PDF Vector**: Cài đặt `n8n-nodes-pdfvector` trong n8n.  
- **Đường dẫn lưu file**: Định nghĩa thư mục ghi file JSON/GEXF (ví dụ: `/tmp`).  
- **Gephi**: Cài đặt Gephi để mở file GEXF và trực quan hóa.  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON từ link gốc: https://n8n.io/workflows/7356  
2. Trong n8n, vào **Workflows** → **Import** → **Upload JSON**.  
3. Hoặc copy toàn bộ JSON và dán vào **Editor** → **Import**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Tham số cần cấu hình |
|------|-------|----------------------|
| **Set Parameters** | Đặt các tham số đầu vào: `paperIds`, `depth`, `outputPath`. | `paperIds` (mảng DOI/PMID), `depth` (số cấp), `outputPath` (đường dẫn file GEXF). |
| **Split Paper IDs** | Chia danh sách ID thành từng phần cho vòng lặp. | Không cần cấu hình thêm. |
| **PDF Vector – Fetch Papers** | Lấy thông tin bài báo gốc. | **API Key** trong credentials, `operation: fetch`, `resource: academic`. |
| **Fetch Citing Papers** | Tìm các bài báo trích dẫn. | **API Key** trong credentials, `operation: search`, `resource: academic`. |
| **Build Network Data** | Xây dựng dữ liệu node/edge từ kết quả fetch. | Không cần cấu hình thêm. |
| **Combine Network** | Kết hợp các mạng lưới cấp độ khác nhau. | Không cần cấu hình thêm. |
| **Export Network JSON** | Ghi dữ liệu JSON ra file. | `File Name` (ví dụ: `network.json`), `Binary Property` (đặt `data`). |
| **Generate GEXF** | Chuyển đổi JSON sang định dạng GEXF cho Gephi. | `outputPath` (đường dẫn file GEXF). |
| **StickyNote** | Ghi chú, không ảnh hưởng tới workflow. | Không cần cấu hình. |

> **Lưu ý**: Đảm bảo **PDF Vector API Key** đã được lưu trong **Credentials** của n8n. Nếu chưa, vào **Credentials** → **New Credential** → chọn **PDF Vector** và nhập API key.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (`paperIds`: ["10.1038/s41586-020-2649-2"], `depth`: 2).  
2. Kiểm tra file `network.json` và `network.gexf` trong thư mục đã chỉ định.  
3. Mở file GEXF bằng Gephi để xem mạng trích dẫn.  
4. Khi mọi thứ ổn, bật **Active** để workflow tự động chạy theo lịch hoặc qua webhook.

## ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram**: Thêm node Slack/Telegram để gửi thông báo khi workflow hoàn thành.  
- **Lưu log chi tiết**: Sử dụng node `Write Binary File` để ghi log JSON của từng bước.  
- **Báo cáo định kỳ**: Đặt workflow chạy hàng ngày/tuần để cập nhật mạng trích dẫn mới.  
- **Phân tích độ sâu**: Thử nghiệm với `depth` 1, 2, 3 để xem ảnh hưởng tới kích thước mạng.  

## 📌 Kết luận
Workflow này giúp các sếp nhanh chóng **tạo mạng trích dẫn** từ các bài báo khoa học mà không cần viết code. Bạn chỉ cần cung cấp danh sách ID và độ sâu, để lại công việc tự động cho n8n và PDF Vector. Hãy thử ngay và mở rộng thêm các tính năng tùy chỉnh để phù hợp với quy trình nghiên cứu của mình!