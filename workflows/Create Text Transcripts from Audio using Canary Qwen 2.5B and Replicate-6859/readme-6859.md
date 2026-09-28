---
title: "🎙️ Tự Động Chuyển Audio Sang Văn Bản (Transcript) Siêu Tốc Với Canary-Qwen 2.5B & Replicate - Không Cần Code!"
description: "Workflow tự động hóa chuyển đổi âm thanh thành văn bản chính xác 94.37% (WER) bằng mô hình AI Canary-Qwen 2.5B của Replicate, tích hợp hoàn toàn trên n8n. Giúp các sếp tiết kiệm 10+ giờ/tháng ghi chú cuộc họp, podcast hoặc nội dung video."
slug: "tieu-dong-chuyen-audio-sang-van-ban-canary-qwen-2-5b"
tags: [n8n, automation, ai-multimodal, speech-to-text, content-creation, replicate-api]
keywords: [n8n workflow chuyển âm thanh thành văn bản, tự động hóa ghi chú cuộc họp, Canary-Qwen 2.5B, Replicate API, AI speech to text, tiết kiệm thời gian ghi chú]
---

# 🚀 **Tự Động Chuyển Audio Sang Văn Bản (Transcript) Siêu Tốc Với Canary-Qwen 2.5B & Replicate**

### **Giải pháp cho các sếp:**
- **Đã mệt mỏi** phải nghe lại hàng giờ âm thanh (cuộc họp, podcast, video) để ghi chú?
- **Mong muốn** tự động hóa quá trình tạo transcript chính xác, tiết kiệm thời gian và chi phí?
- **Cần** một công cụ AI không cần code để chuyển đổi âm thanh thành văn bản với độ chính xác **94.37% (WER)**?

Workflow này sẽ **tự động hóa hoàn toàn** quá trình chuyển đổi âm thanh thành văn bản bằng mô hình **Canary-Qwen 2.5B** của Replicate, tích hợp trên nền tảng **n8n** (self-hosted). Bạn chỉ cần **click một nút**, workflow sẽ xử lý tất cả và trả về kết quả dưới dạng văn bản sẵn sàng sử dụng!

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng**: Không cần nghe lại âm thanh để ghi chú.
- **Độ chính xác cao**: 94.37% (WER) – gần như không sai sót.
- **Tích hợp AI nâng cao**: Tích hợp timestamps và khả năng phân tích văn bản (LLM).
- **Hoạt động liên tục**: Chạy tự động 24/7 trên VPS, không cần can thiệp.
- **Cá nhân hóa**: Thêm prompt tùy chỉnh cho kết quả phù hợp với mục đích sử dụng.
- **Dữ liệu sẵn sàng sử dụng**: Kết quả trả về dưới dạng văn bản, sẵn để copy-paste hoặc xuất file.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Replicate**:
   - Đăng ký tại [replicate.com](https://replicate.com) và lấy **API Token**.
   - [Hướng dẫn lấy API Token](https://replicate.com/docs/api-tokens).
2. **File âm thanh**:
   - File âm thanh dưới dạng `.mp3`, `.wav`, hoặc `.ogg` (không quá 500MB).
3. **n8n Self-hosted**:
   - Workflow này yêu cầu **n8n chạy trên VPS** để hoạt động 24/7.
   - [Cài đặt n8n trên VPS](https://docs.n8n.io/hosting/installation/installation-on-vps/) (hướng dẫn chi tiết).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/6859](https://n8n.io/workflows/6859).
2. Trên giao diện n8n, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create Workflow** để thêm vào dự án.

#### **Phương pháp 2: Copy/Paste JSON**
1. Tải workflow từ [n8n.io/workflows/6859](https://n8n.io/workflows/6859) và sao chép JSON.
2. Trên n8n, nhấn **Create Workflow** → Chọn **Import from JSON** → Dán JSON và nhấn **Import**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **a. Cấu hình API Token**
- **Node**: *Set API Token*
  - Thay thế `YOUR_REPLICATE_API_TOKEN` bằng **API Token** của bạn từ Replicate.
  - **Lưu ý**: Không chia sẻ API Token với ai!

#### **b. Cấu hình tham số âm thanh**
- **Node**: *Set Text Parameters*
  - **Tham số bắt buộc**:
    - `audio`: Đường dẫn đến file âm thanh (ví dụ: `https://example.com/audio.mp3`).
  - **Tham số tùy chọn** (cấu hình theo nhu cầu):
    - `llm_prompt`: Thêm prompt để AI phân tích văn bản (ví dụ: *"Tóm tắt nội dung chính của cuộc họp"*).
    - `show_confidence`: Bật (`true`) để hiển thị độ tin cậy của AI (mặc định: `false`).
    - `include_timestamps`: Bật (`true`) để thêm timestamps vào transcript (mặc định: `true`).

#### **c. Kiểm tra kết nối API**
- **Node**: *Create Text Prediction*
  - Nếu gặp lỗi, kiểm tra lại **API Token** và **đường dẫn file âm thanh**.
  - Thử **test run** với một file âm thanh nhỏ trước khi chạy toàn bộ.

#### **d. Cấu hình thời gian chờ**
- **Node**: *Wait 5s* và *Wait 10s*
  - Thời gian chờ này giúp workflow **kiểm tra trạng thái** của API Replicate.
  - Nếu quá trình xử lý lâu, có thể tăng thời gian chờ (nhưng không nên quá lâu để tránh tốn tài nguyên).

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Manual Trigger** để chạy workflow với file âm thanh mẫu.
   - Kiểm tra **log** để đảm bảo không có lỗi.
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động khi kích hoạt.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp Slack/Telegram**:
   - Sau khi workflow hoàn thành, gửi kết quả transcript về **Slack** hoặc **Telegram** để thông báo.
   - **Cách làm**: Thêm node **Slack** hoặc **Telegram Bot** sau *Display Result*.

2. **Lưu log tự động**:
   - Sử dụng node **Google Sheets** hoặc **Database** để lưu lịch sử transcript.
   - **Ưu điểm**: Dễ dàng theo dõi và tra cứu lại sau này.

3. **Tự động tạo báo cáo định kỳ**:
   - Kết hợp với **Google Calendar** hoặc **n8n Scheduler** để chạy workflow vào giờ cố định (ví dụ: sáng mỗi ngày).

4. **Tối ưu hóa prompt**:
   - Nếu muốn **tóm tắt** hoặc **phân tích** nội dung, thêm prompt như:
     ```json
     "llm_prompt": "Tóm tắt nội dung chính và đề xuất 3 điểm quan trọng trong cuộc họp."
     ```

5. **Xử lý âm thanh nhiều file**:
   - Sử dụng **node HTTP Request** để upload nhiều file âm thanh từ một thư mục.
   - **Cách làm**: Thêm node **HTTP Request** với method `POST` và gửi danh sách file.

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quá trình chuyển đổi âm thanh thành văn bản **không cần code**, với **độ chính xác cao** và **tích hợp AI nâng cao**. Bằng cách tích hợp trên **n8n self-hosted**, workflow sẽ hoạt động **liên tục 24/7**, tiết kiệm thời gian và nâng cao hiệu suất làm việc.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n trên VPS** (nếu chưa có).
2. **Import workflow** và cấu hình API Token.
3. **Test với file âm thanh** và bắt đầu tự động hóa!

---
**🔗 Liên hệ hỗ trợ**:
- **Yaron Been** (Tác giả): [LinkedIn](https://www.linkedin.com/in/yaronbeen/) | [YouTube](https://www.youtube.com/@YaronBeen/videos)
- **Hỗ trợ kỹ thuật n8n**: [Docs.n8n.io](https://docs.n8n.io/)

---
**🚀 Chúc các sếp thành công với việc tự động hóa!** 🎧→📝