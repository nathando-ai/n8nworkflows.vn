---
title: "🚀 Tự Động Hóa Tạo Bài Đăng LinkedIn Từ Cuộc Hỏi Vấn Fireflies Với GPT-4o-mini, Google Drive & Slack – Không Cần Code!"
description: "Giải pháp tự động hóa 100% cho các CEO, Founder và chuyên gia bán hàng biến mỗi cuộc gọi khách hàng thành bài đăng LinkedIn hấp dẫn, cá nhân hóa và sẵn sàng xuất bản chỉ trong vài giây. Kết hợp AI, Google Drive và Slack để tiết kiệm thời gian lên đến 80% trong content creation."
slug: "tu-dong-hoa-tao-bai-dang-linkedin-tu-fireflies-gpt-4o-mini"
tags: [n8n, automation, content-creation, ai-multimodal, fireflies, google-drive, slack, openai, no-code]
keywords: [n8n workflow linkedin, tự động hóa bài đăng linkedin, fireflies ai, gpt-4o-mini tự động viết bài, google drive tự động hóa, slack tự động hóa content]
---

# 🚀 **Tự Động Hóa Tạo Bài Đăng LinkedIn Từ Cuộc Hỏi Vấn Fireflies – Không Cần Code!**

### **Giải pháp cho các sếp muốn biến mỗi cuộc gọi khách hàng thành bài đăng LinkedIn hấp dẫn, cá nhân hóa và sẵn sàng xuất bản chỉ trong vài giây.**

Hãy tưởng tượng: Sau khi cuộc gọi với khách hàng kết thúc, Fireflies tự động transcribe toàn bộ nội dung, sau đó **GPT-4o-mini** phân tích và viết một bài đăng LinkedIn **chuyên nghiệp, hấp dẫn** với:
✅ **Hook bắt mắt** để người đọc muốn click
✅ **3-5 học hỏi với emoji** từ cuộc gọi thực tế
✅ **Câu hỏi kích thích tương tác** ở cuối bài
✅ **Hashtags phù hợp** để tăng tầm nhìn
✅ **Được lưu trên Google Drive** và **preview trên Slack** trước khi xuất bản

**Kết quả?** Các sếp tiết kiệm **80% thời gian** viết bài, tăng **tỷ lệ tương tác 3x** và **cải thiện chất lượng content** nhờ AI.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng** (Self-hosted) để tránh giới hạn của phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** – giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao cho AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** viết bài LinkedIn (AI tự động phân tích và viết từ transcript).
- **Cá nhân hóa 100%** mỗi bài đăng dựa trên cuộc gọi thực tế.
- **Chất lượng content cao** với cấu trúc chuyên nghiệp (hook + học hỏi + CTA).
- **Lưu trữ tự động** trên Google Drive và **preview trên Slack** trước khi xuất bản.
- **Hoạt động liên tục** 24/7, không cần can thiệp thủ công.
- **Tăng tương tác** nhờ bài đăng được tối ưu với emoji, hashtags và câu hỏi kích thích.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Fireflies** (đã cấu hình Webhook).
✔ **API Key của Fireflies** (tìm trong **Settings > Developer Settings**).
✔ **Tài khoản Google Drive** (để lưu bài đăng).
✔ **Tài khoản Slack** (để preview bài đăng trước khi xuất bản).
✔ **Tài khoản OpenAI** (để sử dụng GPT-4o-mini).
✔ **Thông tin cá nhân** (tên tác giả, chức vụ, công ty).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15040](https://n8n.io/workflows/15040) hoặc copy toàn bộ JSON từ **View Code** trên canvas.
- Mở **n8n Editor**, nhấn **Import Workflow** và dán JSON vào.
- **Không thay đổi cấu trúc** của workflow, chỉ cần **cấu hình các node** sau.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **🔹 Node 1: Webhook — Fireflies Transcript Done**
- **Không cần cấu hình gì** (n8n sẽ tự động nhận webhook từ Fireflies).
- **Lưu ý:** Đảm bảo Fireflies đã cấu hình webhook với **URL này** (sau khi import).

##### **🔹 Node 5: Set — Config Values**
**ĐIỀN THAM SỐ CẦN THIẾT:**
| Tham số | Giá trị cần thay đổi |
|---------|----------------------|
| `FIREFLIES_API_KEY` | API Key từ Fireflies (tìm trong **Settings > Developer Settings**) |
| `GOOGLE_DRIVE_FOLDER_ID` | ID của folder Google Drive muốn lưu bài đăng (lấy từ liên kết folder) |
| `SLACK_CHANNEL` | Tên channel Slack muốn preview bài đăng (ví dụ: `#content-review`) |
| `AUTHOR_NAME` | Tên tác giả (ví dụ: "John Doe") |
| `AUTHOR_TITLE` | Chức vụ (ví dụ: "Founder, TechStart") |
| `COMPANY_NAME` | Tên công ty (ví dụ: "TechStart") |

**Cách lấy `GOOGLE_DRIVE_FOLDER_ID`:**
1. Mở Google Drive, chọn folder muốn lưu bài đăng.
2. Copy liên kết folder (nhấn **Share > Copy link**).
3. Link sẽ có dạng: `https://drive.google.com/drive/folders/[FOLDER_ID]` → **Lấy phần `[FOLDER_ID]`**.

##### **🔹 Node 11: OpenAI — GPT-4o-mini Model**
- **Kết nối credential OpenAI**:
  1. Nhấn **Add** trong node.
  2. Chọn **OpenAI** và đăng nhập tài khoản.
  3. Chọn **gpt-4o-mini** như mô hình mặc định.

##### **🔹 Node 13: Google Drive — Save LinkedIn Post**
- **Kết nối OAuth2 Google Drive**:
  1. Nhấn **Add** trong node.
  2. Chọn **Google Drive** và đăng nhập tài khoản.
  3. Chọn quyền **Drive** và **Documents**.

##### **🔹 Node 14: Slack — Send Post Preview**
- **Kết nối OAuth2 Slack**:
  1. Nhấn **Add** trong node.
  2. Chọn **Slack** và đăng nhập tài khoản.
  3. Chọn **channel** muốn preview bài đăng (đã điền trong **Node 5**).
  4. **Thêm bot vào channel** (nếu chưa có).

##### **🔹 Node 2 & 3: Code — Extract Meeting ID & IF — Valid Meeting ID?**
- **Không cần chỉnh sửa**, n8n sẽ tự động xử lý.

##### **🔹 Node 6: HTTP — Fetch Transcript**
- **Không cần cấu hình**, n8n sẽ tự động gọi API Fireflies với `FIREFLIES_API_KEY` từ **Node 5**.

##### **🔹 Node 7: Code — Process Transcript Data**
- **Không cần chỉnh sửa**, node này tự động phân tích transcript.

##### **🔹 Node 10: AI Agent — Write LinkedIn Post**
- **Không cần cấu hình**, AI sẽ tự động viết bài dựa trên transcript.

##### **🔹 Node 12: Code — Build Doc and Slack Message**
- **Không cần chỉnh sửa**, node này tự động xây dựng nội dung Google Doc và preview Slack.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với một cuộc gọi mẫu:
   - Gọi một cuộc họp với Fireflies, chờ transcript hoàn tất.
   - Kiểm tra **Slack** xem có preview bài đăng không.
   - Kiểm tra **Google Drive** xem bài đăng đã được lưu chưa.
2. **Bật Active workflow** sau khi test thành công.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động xuất bản trên LinkedIn**:
   - Sử dụng **n8n-node-linkedin** để xuất bản bài đăng từ Google Doc.
   - Cài thêm node này vào cuối workflow.

2. **Lưu log hoạt động**:
   - Thêm **node `n8n-nodes-base.email`** để gửi báo cáo hàng tuần về email.

3. **Tối ưu AI với Prompt Engineering**:
   - Trong **Node 10 (AI Agent)**, chỉnh sửa **prompt** để AI viết bài phù hợp với **ngôn ngữ mục tiêu** (Việt Nam, Anh, Nhật...).

4. **Kết hợp với Notion**:
   - Thay vì Google Drive, sử dụng **n8n-node-notion** để lưu bài đăng vào Notion.

5. **Xử lý lỗi tự động**:
   - Thêm **node `n8n-nodes-base.set`** sau **Node 9 (IF — Transcript Not Ready?)** để gửi thông báo lỗi về Slack.

---

### 📌 **Kết luận**
**Workflow này giúp các sếp:**
✅ **Tiết kiệm 80% thời gian** viết bài LinkedIn.
✅ **Tăng chất lượng content** nhờ AI phân tích cuộc gọi.
✅ **Hoạt động tự động 24/7** mà không cần can thiệp.
✅ **Preview trước khi xuất bản** trên Slack.

**Hành động ngay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình các node** theo hướng dẫn.
3. **Test với một cuộc gọi mẫu**.
4. **Bật workflow** và bắt đầu tự động hóa content!

**🚀 Cùng n8n biến mỗi cuộc gọi thành bài đăng LinkedIn hấp dẫn!** 🚀