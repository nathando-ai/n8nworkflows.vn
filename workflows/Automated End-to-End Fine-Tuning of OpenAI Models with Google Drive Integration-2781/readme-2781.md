---
title: "🚀 Tự Động Hoá Fine-Tuning Mô Hình OpenAI Tối Ưu Với Google Drive - Không Cần Code!"
description: "Workflow tự động hóa hoàn chỉnh để fine-tuning mô hình OpenAI bằng dữ liệu từ Google Drive, tiết kiệm thời gian và tối ưu hóa hiệu suất AI cho doanh nghiệp. Kết quả: Mô hình cá nhân hóa, hoạt động liên tục 24/7, và tích hợp API dễ dàng."
slug: "tieu-dong-hoa-fine-tuning-openai-google-drive"
tags: [n8n, automation, ai, openai, google-drive, fine-tuning, no-code]
keywords: [tự động hóa fine-tuning OpenAI, n8n workflow AI, tích hợp Google Drive với OpenAI, tự động hóa mô hình chatbot, tối ưu hóa mô hình GPT, tự động hóa không cần code]
---

# 🚀 **Tự Động Hoá Fine-Tuning Mô Hình OpenAI Với Google Drive - Giải Pháp AI Cho Doanh Nghiệp**

### **🔥 Nỗi Đau Của Các Sếp Khi Fine-Tuning Mô Hình AI**
Hiện nay, việc **fine-tuning mô hình OpenAI** để phù hợp với nhu cầu cụ thể của doanh nghiệp thường tốn thời gian và phức tạp:
- **Tạo file `.jsonl`** theo định dạng chính xác để huấn luyện mô hình.
- **Upload file lên OpenAI** và chờ quá trình training hoàn tất.
- **Quản lý mô hình mới** sau khi fine-tuning, bao gồm kiểm tra và tích hợp API.

Với **workflow này**, các sếp sẽ **tự động hóa toàn bộ quy trình** từ tải file từ Google Drive đến fine-tuning và kích hoạt mô hình mới, **không cần viết một dòng code nào!**

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa từ tải file đến fine-tuning, giảm thiểu công việc thủ công.
- **Mô hình cá nhân hóa**: Fine-tuning mô hình OpenAI theo nhu cầu cụ thể của doanh nghiệp (ví dụ: hỗ trợ du lịch, khách hàng, hoặc chuyên ngành).
- **Hoạt động liên tục 24/7**: Workflow chạy tự động khi có file mới được upload lên Google Drive.
- **Tích hợp API dễ dàng**: Mô hình fine-tuned sẵn sàng sử dụng trong các ứng dụng, chatbot, hoặc hệ thống AI.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** với API Key (để fine-tuning và upload file).
2. **Tài khoản Google Drive** với OAuth 2.0 API (để tải file `.jsonl` từ Google Drive).
3. **File `.jsonl` chuẩn** (định dạng như ví dụ dưới đây) được upload lên Google Drive trước khi chạy workflow.
   ```json
   {
     "messages": [
       {"role": "system", "content": "Bạn là trợ lý du lịch chuyên nghiệp."},
       {"role": "user", "content": "Tôi cần biết thủ tục nhập cảnh Mỹ."},
       {"role": "assistant", "content": "Để nhập cảnh Mỹ, bạn cần hộ chiếu và giấy phép ESTA. Xác minh thêm theo quốc tịch của bạn."}
     ]
   }
   ```
4. **Mô hình OpenAI** (ví dụ: `gpt-4o-mini`) để fine-tuning.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/2781](https://n8n.io/workflows/2781) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này bao gồm **7 node** chính, mỗi node cần cấu hình kỹ lưỡng:

##### **🔹 Node 1: Manual Trigger (Kích Hoạt Bằng Tay)**
- **Chức năng**: Bắt đầu workflow khi nhấn **"Test workflow"**.
- **Lưu ý**: Sau khi import, **không cần thay đổi** node này.

##### **🔹 Node 2: Google Drive (Tải File `.jsonl`)**
- **Cấu hình**:
  - **Credentials**: Chọn `googleDriveOAuth2Api` (đã cấu hình trước khi import).
  - **Operation**: Đặt là `download`.
  - **File ID**: Điền **ID file `.jsonl`** từ Google Drive (lấy từ liên kết chia sẻ file).
    *Ví dụ*: Nếu file có liên kết `https://drive.google.com/file/d/1AbCdEfGhIjKlMnOp/view?usp=sharing`, thì **File ID** là `1AbCdEfGhIjKlMnOp`.
  - **Folder Path**: Nếu file ở trong folder, điền đường dẫn tương đối (ví dụ: `FolderName/`).

##### **🔹 Node 3: AI Agent (Agent Trợ Lý AI)**
- **Chức năng**: Xử lý logic giữa các node (không cần chỉnh sửa).
- **Lưu ý**: Node này **không yêu cầu cấu hình thêm**, chỉ cần kết nối với node **OpenAI Chat Model**.

##### **🔹 Node 4: Chat Trigger (Kích Hoạt Khi Nhận Tin Nhắn)**
- **Chức năng**: Khởi động workflow khi có tin nhắn (không bắt buộc, có thể bỏ qua nếu sử dụng **Manual Trigger**).
- **Lưu ý**: Nếu không cần, **xóa node này** và kết nối **Node 2 (Google Drive)** trực tiếp với **Node 5 (OpenAI Chat Model)**.

##### **🔹 Node 5: OpenAI Chat Model (Mô Hình Fine-Tuned)**
- **Cấu hình**:
  - **Credentials**: Chọn `openAiApi` (API Key đã cấu hình trước).
  - **Model**: Đặt là `ft:gpt-4o-mini-2024-07-18:n3w-italia::AsVfsl7B` (hoặc mô hình fine-tuned của bạn).
    *Lưu ý*: Nếu chưa có mô hình fine-tuned, **bước này sẽ không hoạt động**. Các sếp cần **tạo mô hình mới** trước (xem hướng dẫn dưới đây).
  - **Prompt**: Nếu cần, điền **prompt mặc định** (ví dụ: `"You are a travel assistant. Answer in Vietnamese."`).

##### **🔹 Node 6: Upload File (Upload File `.jsonl` Lên OpenAI)**
- **Cấu hình**:
  - **Credentials**: Chọn `openAiApi`.
  - **File**: Chọn file `.jsonl` đã tải từ Google Drive (tự động lấy từ **Node 2**).
  - **Resource**: Đặt là `file`.
  - **Purpose**: Chọn `fine-tune`.

##### **🔹 Node 7: Create Fine-Tuning Job (Tạo Job Fine-Tuning)**
- **Cấu hình**:
  - **Credentials**: Chọn `httpHeaderAuth` (nếu cần, cấu hình header như `Authorization: Bearer {API_KEY}`).
  - **URL**: Đặt là `https://api.openai.com/v1/fine-tunes`.
  - **Method**: `POST`.
  - **Headers**:
    ```
    Content-Type: application/json
    Authorization: Bearer {API_KEY}
    ```
  - **Body**:
    ```json
    {
      "training_file": "file-{ID từ Node 6}",
      "model": "gpt-4o-mini"
    }
    ```
    *Lưu ý*: Thay `{ID từ Node 6}` bằng **ID file** từ OpenAI (lấy từ response của Node 6).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Test workflow"** và chọn **file `.jsonl`** từ Google Drive.
   - Kiểm tra **Node 6** và **Node 7** để đảm bảo file được upload và job fine-tuning được tạo thành công.
2. **Bật Active**:
   - Sau khi test thành công, **bật workflow** để chạy tự động khi có file mới.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH TẠO MÔ HÌNH FINE-TUNED MỚI]
1. **Tạo file `.jsonl`**:
   - Sử dụng định dạng như ví dụ trên (ví dụ: hỗ trợ du lịch, y tế, hoặc chuyên ngành).
   - Upload lên **Google Drive** và chia sẻ với quyền **đọc**.
2. **Chạy workflow**:
   - Workflow sẽ tự động tải file từ Google Drive và tạo **job fine-tuning** trên OpenAI.
3. **Kiểm tra mô hình mới**:
   - Sau khi fine-tuning hoàn tất (thời gian ~5-30 phút), OpenAI sẽ trả về **ID mô hình mới** (ví dụ: `ft:gpt-4o-mini-2024-07-18:n3w-italia::AsVfsl7B`).
   - **Cập nhật Node 5** với mô hình mới để sử dụng.
:::

:::tip[TÍCH HỢP VỚI SLACK/TELEGRAM]
- Sử dụng **node Slack/Telegram** để thông báo khi:
  - File `.jsonl` được tải thành công.
  - Job fine-tuning bắt đầu/hoàn tất.
  - Mô hình mới sẵn sàng sử dụng.
:::

:::note[LƯU LOG & BÁO CÁO]
- Sử dụng **node Sticky Note** hoặc **Google Sheets** để lưu lịch sử fine-tuning:
  - Ngày upload file.
  - Thời gian hoàn tất job.
  - ID mô hình mới.
  - Kết quả test mô hình.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công phức tạp trong fine-tuning mô hình OpenAI. **Chỉ cần upload file `.jsonl` lên Google Drive**, workflow sẽ tự động:
✅ Tải file từ Google Drive.
✅ Upload lên OpenAI.
✅ Tạo job fine-tuning.
✅ Kích hoạt mô hình mới.

**🚀 Hãy áp dụng ngay và tối ưu hóa mô hình AI cho doanh nghiệp của mình!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::