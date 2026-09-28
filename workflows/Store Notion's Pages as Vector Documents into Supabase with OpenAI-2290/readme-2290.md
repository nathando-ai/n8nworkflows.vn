---
title: "🚀 Tự động lưu trữ nội dung Notion thành vector documents trong Supabase với OpenAI"
description: "Hướng dẫn tự động hóa lưu trữ nội dung Notion vào cơ sở dữ liệu vector Supabase để tối ưu hóa tìm kiếm và phân tích dữ liệu với công nghệ AI"
slug: "tu-dong-luu-tru-notion-supabase-openai"
tags: [n8n, automation, no-code, Notion, Supabase, AI, OpenAI]
keywords: [n8n workflow, tự động hóa, Notion, Supabase, OpenAI, vector database]
---

# 🚀 Tự động lưu trữ nội dung Notion thành vector documents trong Supabase với OpenAI

[Các sếp đang gặp khó khăn khi phải thủ công sao chép nội dung từ Notion sang cơ sở dữ liệu để phân tích dữ liệu hoặc xây dựng hệ thống tìm kiếm thông minh. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này chỉ trong vài bước đơn giản.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa toàn bộ quá trình lưu trữ nội dung Notion vào cơ sở dữ liệu vector
- Tiết kiệm thời gian và công sức thủ công
- Tạo cơ sở dữ liệu vector mạnh mẽ cho các ứng dụng tìm kiếm và phân tích dữ liệu
- Tích hợp liền mạch với OpenAI để tạo embeddings chất lượng cao
- Hệ thống hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Notion với cơ sở dữ liệu chứa nội dung cần lưu trữ
- Dự án Supabase với bảng có cột vector (theo hướng dẫn [tại đây](https://supabase.com/docs/guides/ai/vector-columns))
- API Key của OpenAI
- Tài khoản n8n đã được cài đặt và cấu hình
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang workflow gốc: [https://n8n.io/workflows/2290](https://n8n.io/workflows/2290)
2. Click vào nút "Import" để tải file JSON về máy
3. Trong n8n Editor, click vào menu "Workflow" > "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Notion - Page Added Trigger**:
   - Cấu hình credentials cho Notion
   - Chọn cơ sở dữ liệu Notion chứa nội dung cần lưu trữ
   - Đảm bảo cơ sở dữ liệu này chỉ chứa các trang bạn muốn tự động hóa

2. **Notion - Retrieve Page Content**:
   - Đảm bảo node này được kết nối với node "Notion - Page Added Trigger"
   - Không cần cấu hình thêm tham số

3. **Filter Non-Text Content**:
   - Node này sẽ tự động loại bỏ các block không phải text (image, video)
   - Không cần cấu hình thêm tham số

4. **Summarize - Concatenate Notion's blocks content**:
   - Node này sẽ kết hợp tất cả các block text thành một nội dung duy nhất
   - Không cần cấu hình thêm tham số

5. **Create metadata and load content**:
   - Node này sẽ tạo metadata từ nội dung Notion
   - Không cần cấu hình thêm tham số

6. **Token Splitter**:
   - Cấu hình kích thước chunk (mặc định là 512 tokens)
   - Có thể điều chỉnh theo nhu cầu của dự án

7. **Embeddings OpenAI**:
   - Cấu hình credentials cho OpenAI
   - Chọn model phù hợp (mặc định là "text-embedding-ada-002")
   - Đảm bảo tài khoản OpenAI có đủ credit để tạo embeddings

8. **Supabase Vector Store**:
   - Cấu hình credentials cho Supabase
   - Chọn bảng và cột vector trong Supabase
   - Đảm bảo bảng này đã được cấu hình đúng theo hướng dẫn [tại đây](https://supabase.com/docs/guides/ai/vector-columns)

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Execute Workflow" để test với dữ liệu mẫu
2. Kiểm tra kết quả trong bảng Supabase để đảm bảo nội dung đã được lưu trữ đúng
3. Nếu kết quả đúng, click vào nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp với Slack/Telegram**: Thêm node gửi thông báo khi có nội dung mới được lưu trữ
2. **Lưu log hoạt động**: Thêm node ghi log các hoạt động quan trọng của workflow
3. **Tự động gửi báo cáo**: Thiết lập gửi báo cáo định kỳ về số lượng nội dung đã được lưu trữ
4. **Xử lý lỗi nâng cao**: Thêm node xử lý lỗi và gửi cảnh báo khi có vấn đề xảy ra

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình lưu trữ nội dung Notion vào cơ sở dữ liệu vector Supabase, tạo nền tảng mạnh mẽ cho các ứng dụng tìm kiếm và phân tích dữ liệu. Với việc tích hợp OpenAI, các sếp có thể tạo ra các embeddings chất lượng cao để tối ưu hóa tìm kiếm và phân tích dữ liệu. Hãy áp dụng ngay workflow này để tiết kiệm thời gian và công sức trong quá trình xử lý dữ liệu!