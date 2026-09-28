---
title: "🚀 Tự động hóa chuyển đổi dữ liệu Excel thành vector AI với OpenAI và Supabase"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình chuyển đổi dữ liệu Excel thành vector AI sử dụng OpenAI và Supabase, giúp tối ưu hóa lưu trữ và truy xuất thông tin."
slug: "tu-dong-hoa-chuyen-doi-du-lieu-excel-thanh-vector-ai"
tags: [n8n, automation, no-code, AI, RAG, Multimodal AI]
keywords: [n8n workflow, tự động hóa, AI, RAG, Multimodal AI, OpenAI, Supabase]
---

# 🚀 Tự động hóa chuyển đổi dữ liệu Excel thành vector AI với OpenAI và Supabase

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi phải xử lý dữ liệu Excel thủ công và giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quá trình chuyển đổi dữ liệu Excel thành vector AI.
- Tiết kiệm thời gian và công sức cho nhân viên.
- Tăng tính chính xác và nhất quán trong quá trình xử lý dữ liệu.
- Tích hợp dễ dàng với hệ thống lưu trữ dữ liệu hiện tại.
- Hỗ trợ tìm kiếm và truy xuất thông tin hiệu quả hơn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI với API key.
- Tài khoản Supabase với thông tin kết nối.
- File Excel chứa dữ liệu cần chuyển đổi.
- Kiến thức cơ bản về cấu trúc dữ liệu và quản lý cơ sở dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **When clicking ‘Execute workflow’**: Node này kích hoạt workflow khi người dùng nhấn nút "Execute workflow". Không cần cấu hình gì thêm.

- **Remove HTML**: Node này loại bỏ các thẻ HTML và thực thể HTML khỏi các trường văn bản trong dữ liệu đầu vào. Không cần cấu hình gì thêm.

- **Loop Over Items**: Node này lặp qua từng mục trong dữ liệu đầu vào để xử lý từng mục một. Không cần cấu hình gì thêm.

- **Switch**: Node này đánh giá các điều kiện và xác định đường dẫn thực thi dựa trên các quy tắc được cung cấp. Cần cấu hình các quy tắc để đánh giá các trường `has_Question` và `has_Answer`.

- **Merge**: Node này kết hợp các luồng dữ liệu đầu vào thành một luồng dữ liệu đầu ra duy nhất. Không cần cấu hình gì thêm.

- **Merge import Data**: Node này kết hợp hai tập dữ liệu dựa trên các trường khớp nhau. Cần cấu hình các trường khớp nhau và các tùy chọn kết hợp.

- **Code "Question"**: Node này xử lý trường "Customer Question" từ dữ liệu đầu vào và chuẩn bị thông tin cho việc nhúng với OpenAI. Không cần cấu hình gì thêm.

- **Code "Answer"**: Node này xử lý trường "Customer Answer" từ dữ liệu đầu vào và chuẩn bị thông tin cho việc nhúng với OpenAI. Không cần cấu hình gì thêm.

- **Embeddings OpenAI Answer**: Node này gửi yêu cầu HTTP đến API OpenAI để tạo ra các vector nhúng cho câu trả lời. Cần cấu hình các thông tin xác thực và các tham số yêu cầu.

- **Embeddings OpenAI Question**: Node này gửi yêu cầu HTTP đến API OpenAI để tạo ra các vector nhúng cho câu hỏi. Cần cấu hình các thông tin xác thực và các tham số yêu cầu.

- **Merge fields for database insert**: Node này kết hợp các trường dữ liệu để chuẩn bị cho việc chèn vào cơ sở dữ liệu. Không cần cấu hình gì thêm.

- **Write row to database**: Node này chèn một hàng mới vào bảng cơ sở dữ liệu được chỉ định. Cần cấu hình các trường dữ liệu và các thông tin kết nối cơ sở dữ liệu.

- **Retrieve existing rows**: Node này truy xuất tất cả các hàng hiện có từ bảng cơ sở dữ liệu được chỉ định. Cần cấu hình các thông tin kết nối cơ sở dữ liệu.

- **Build table in Supabase**: Node này xây dựng bảng trong Supabase để lưu trữ dữ liệu. Cần cấu hình các thông tin kết nối cơ sở dữ liệu và các tham số truy vấn.

- **Get rows from sheet**: Node này truy xuất các hàng từ bảng tính Excel được chỉ định. Cần cấu hình các thông tin kết nối và các tham số truy vấn.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với các công cụ khác như Slack hoặc Telegram để thông báo khi workflow hoàn thành.
- Lưu log các hoạt động của workflow để theo dõi và kiểm tra.
- Gửi báo cáo định kỳ về tiến độ và kết quả của workflow.

### 📌 Kết luận
Workflow này cung cấp một giải pháp tự động hóa hoàn chỉnh để chuyển đổi dữ liệu Excel thành vector AI sử dụng OpenAI và Supabase. Với các bước cấu hình đơn giản và các lưu ý quan trọng, các sếp có thể triển khai workflow này một cách dễ dàng và hiệu quả.