---
title: "🤖 Tự Động Tạo Tóm Tắt Cuộc Họp AI từ Fireflies + Dart: Giảm 90% Thời Gian Ghi Chép"
description: "Workflow tự động hóa hoàn toàn chuyển đổi phiên bản ghi âm Fireflies thành tóm tắt AI chi tiết, tạo tài liệu Dart và nhiệm vụ theo dõi tự động - không cần code. Giúp các sếp tiết kiệm 5+ giờ/tuần và đảm bảo không bỏ sót bất kỳ điểm quan trọng nào trong cuộc họp."
slug: "tieu-dong-tat-cuoc-hop-ai-fireflies-dart"
tags: [n8n, automation, no-code, ai-summarization, fireflies-ai, dart-project-management, google-gemini]
keywords: [tự động hóa ghi chép cuộc họp, tóm tắt cuộc họp AI, fireflies ai n8n, dart project management, google gemini chatbot, workflow tự động hóa cuộc họp]
---

# 🚀 **Tự Động Tạo Tóm Tắt Cuộc Họp AI từ Fireflies + Dart: Giải Pháp "Không Cần Code" cho Các Sếp Bận Rộn**

### **Nỗi Đau Của Các Sếp Hiện Nay**
Các sếp và quản lý thường phải mất **30-60 phút** sau mỗi cuộc họp để:
- **Ghi chép tay** hoặc tìm kiếm phiên bản ghi âm Fireflies
- **Tóm tắt nội dung** một cách chính xác
- **Tạo tài liệu** và **nhiệm vụ theo dõi** trên Dart
- **Phân loại thông tin** (điểm quan trọng, hành động, kế hoạch tiếp theo)

Kết quả? **Thời gian quý giá bị "chôn vùi" trong công việc thủ công**, và **rủi ro bỏ sót thông tin** vẫn tồn tại.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✅ **Tiết kiệm 5+ giờ/tuần** (không cần ghi chép thủ công)
✅ **Tóm tắt chính xác 100%** với AI Gemini (Google)
✅ **Tự động tạo tài liệu Dart** với cấu trúc chuyên nghiệp
✅ **Nhiệm vụ theo dõi tự động** trên Dart, liên kết với phiên bản ghi âm Fireflies
✅ **Cập nhật liên tục** ngay sau khi cuộc họp kết thúc (không cần nhắc nhở)

---
## **🔧 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| **Dịch Vụ**       | **Thông Tin Cần Thiết**                          | **Liên Hệ Để Lấy**                          |
|-------------------|------------------------------------------------|---------------------------------------------|
| **Fireflies AI**  | API Key (PROD)                                  | [Tạo API Key](https://docs.fireflies.ai/fundamentals/authorization) |
| **Dart**          | API Key (Workspace + Folder/Dartboard Access)   | [Cài đặt API](https://dart.ai/docs/api/)     |
| **Google Gemini** | API Key (Google Cloud)                          | [Bật API Gemini](https://makersuite.google.com/) |

### **2. Thông Tin Cấu Hình**
- **Folder ID** trong Dart (để lưu tài liệu)
- **Dartboard ID** trong Dart (để tạo nhiệm vụ)
- **Webhook URL** của Fireflies (để nhận thông báo khi cuộc họp kết thúc)

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow từ File JSON**
1. **Tải workflow** từ [n8n.io/workflows/10851](https://n8n.io/workflows/10851) hoặc copy JSON dưới đây.
2. **Mở n8n Editor** → **Import Workflow** → Dán JSON hoặc tải file `.json`.
3. **Kích hoạt workflow** bằng cách bật nút **Active** ở góc trên bên phải.

```json
// (JSON sẽ được cung cấp đầy đủ sau khi import)
```

### **2. Cấu Hình Cần Thiết (BẮT BUỘC)**
#### **🔹 Node 1: Webhook (Trigger)**
- **Địa chỉ Webhook**: Đã được cung cấp (`437a1a60-35af-4c81-9058-176d825b7173`).
- **Cấu hình Fireflies**:
  - Đăng ký Webhook trong **Fireflies API Settings** ([Hướng dẫn](https://docs.fireflies.ai/graphql-api/webhooks)).
  - Chọn **POST** và gán URL: `https://[your-n8n-domain]/webhook/437a1a60-35af-4c81-9058-176d825b7173`.

#### **🔹 Node 2-5: Dart API (Lấy Folder & Dartboard)**
- **Thay thế ID placeholder**:
  - **Folder ID**: Tìm trong Dart → **Workspace** → **Folder Settings**.
  - **Dartboard ID**: Tìm trong Dart → **Boards** → **Board Settings**.
- **Credentials**: Chọn `dartApi` (đã cấu hình trước).

#### **🔹 Node 6: Fireflies Transcript**
- **API Key**: Điền vào `firefliesApi` (tạo từ [Fireflies Dashboard](https://app.fireflies.ai/)).
- **Endpoint**: Chọn `Get Transcript` và chọn phiên bản ghi âm mới nhất.

#### **🔹 Node 7: Google Gemini Chat Model**
- **API Key**: Điền vào `googlePalmApi` (tạo từ [Google Cloud](https://cloud.google.com/)).
- **Prompt mẫu** (có thể tùy chỉnh):
  ```json
  {
    "role": "user",
    "content": "Tóm tắt cuộc họp theo cấu trúc sau:
    - Overview: Tóm tắt ngắn gọn cuộc họp.
    - Key Items: Điểm quan trọng nhất.
    - Action Items: Hành động cần thực hiện.
    - Next Steps: Kế hoạch tiếp theo."
  }
  ```

#### **🔹 Node 8: Parsing Stage (Code)**
- **Logic mặc định** đã phân tích JSON từ Gemini.
- **Không cần chỉnh sửa** trừ khi muốn thay đổi cấu trúc output.

#### **🔹 Node 9: Fireflies Auto-Summary (Agent)**
- **Model**: Chọn `Google Gemini` (hoặc thay thế bằng LLM khác).
- **Prompt**: Đã được tối ưu cho cấu trúc tóm tắt chuyên nghiệp.

---
### **3. Kích Hoạt Workflow**
1. **Test Run**:
   - Gửi một cuộc họp mẫu qua Fireflies → Kiểm tra output.
   - Đảm bảo tài liệu Dart và nhiệm vụ được tạo đúng.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, bật **Active** để workflow hoạt động 24/7.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **1. Tùy Chỉnh AI Prompt**
- **Thêm yêu cầu cụ thể** (ví dụ: "Tóm tắt theo phong cách Dart").
- **Bỏ các phần không cần thiết** (nếu không muốn AI liệt kê "Next Steps").

### **2. Kết Nối với Slack/Telegram**
- Thêm **Node Slack/Telegram** sau khi tạo tài liệu Dart để thông báo kết quả.
- **Mẫu thông báo**:
  > *"📝 Tóm tắt cuộc họp [Tên Cuộc Họp] đã được tạo tại: [Link Dart] 🔗"*

### **3. Lưu Log & Báo Cáo**
- Thêm **Node Logbook** để lưu lịch sử tóm tắt.
- **Báo cáo định kỳ**: Tạo workflow riêng để gửi tổng hợp tóm tắt hàng tuần.

### **4. Sử Dụng AI Khác**
- Thay thế **Google Gemini** bằng **Mistral AI** hoặc **Claude** nếu muốn thử nghiệm.

---
## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **quản lý chiến lược** thay vì công việc thủ công. Với **AI Gemini** và **Dart**, bạn sẽ:
✔ **Không bao giờ bỏ sót điểm quan trọng** trong cuộc họp.
✔ **Tự động hóa toàn bộ chu trình** từ ghi âm đến hành động.
✔ **Cải thiện hiệu suất đội nhóm** với tài liệu và nhiệm vụ được cấu trúc rõ ràng.

**🚀 Hành động ngay!**
1. **Cài đặt n8n Self-hosted** trên VPS (để workflow chạy 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (Mã giảm **VPSN8N**)
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và bắt đầu tự động hóa!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Lưu ý cuối cùng**: Nếu gặp vấn đề, hãy kiểm tra **log của n8n** và **credentials** của các node. Nếu cần hỗ trợ, liên hệ [Dart Support](https://dart.ai/support) hoặc [n8n Community](https://community.n8n.io/).