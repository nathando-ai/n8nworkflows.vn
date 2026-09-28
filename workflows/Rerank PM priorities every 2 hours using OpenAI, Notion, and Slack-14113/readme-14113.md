---
title: "🚀 **Tự Động Hạng Bậc Ưu Tiên PM Mỗi 2 Giây Với OpenAI, Notion & Slack – Không Cần Code!**"
description: "Workflow tự động hóa xếp hạng lại ưu tiên dự án hàng ngày bằng AI (OpenAI) dựa trên tín hiệu mới từ Notion, Slack và email, giúp các Product Manager tiết kiệm 10+ giờ/tháng và luôn tập trung vào những nhiệm vụ có giá trị cao nhất."
slug: "tieu-dong-hang-bac-uu-tien-pm-moi-2-gio"
tags: [n8n, automation, product-management, ai-summarization, notion, slack, openai, no-code]
keywords: [tự động hóa n8n, xếp hạng ưu tiên dự án, ai cho product manager, tự động hóa notion, tự động hóa slack, workflow n8n cho pm]
---

# 🚀 **Tự Động Hạng Bậc Ưu Tiên PM Mỗi 2 Giây – Không Cần Code!**

### **Nỗi Đau Của Các Sếp Product Manager**
Các sếp đã bao giờ phải **làm thủ công** việc xếp hạng lại ưu tiên dự án hàng ngày? Đánh giá lại các nhiệm vụ dựa trên:
- **Tín hiệu mới** từ Slack, email, hoặc cuộc họp?
- **Thay đổi ưu tiên** do deadline mới hoặc sự kiện bất ngờ?
- **Tính năng mới** cần được ưu tiên hơn?

Kết quả? **Thời gian bị lãng phí**, quyết định không chính xác, và **sự mệt mỏi** khi phải làm việc này hàng ngày. **Workflow này giải quyết tất cả!**

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ xử lý nhanh cho AI)
:::

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10+ giờ/tháng** – Không phải làm thủ công xếp hạng ưu tiên.
✅ **Xếp hạng chính xác hơn** – AI phân tích **tín hiệu mới** (email, cuộc họp, blocker) để điều chỉnh ưu tiên.
✅ **Cập nhật tự động** – Nếu ưu tiên thay đổi, Notion và Slack sẽ **tự động cập nhật** mà không cần can thiệp.
✅ **Quản lý dự án thông minh** – Luôn tập trung vào **những nhiệm vụ có giá trị cao nhất** dựa trên dữ liệu mới nhất.
✅ **Kiểm soát toàn diện** – **Log audit** được lưu trữ trong Notion để theo dõi lịch sử thay đổi.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi **lên đồ**, các sếp cần chuẩn bị:
✔ **Tài khoản Notion** (để lưu trữ ưu tiên, tín hiệu, cuộc họp, email và blocker).
✔ **API Key OpenAI** (để AI phân tích và xếp hạng).
✔ **Webhook Slack** (để thông báo khi ưu tiên thay đổi).
✔ **Dữ liệu ban đầu** trong Notion:
   - **Database "Open Priorities"** (những nhiệm vụ đang mở).
   - **Database "Signals"** (tín hiệu mới từ Slack/email).
   - **Database "Meetings"** (quyết định từ cuộc họp).
   - **Database "Emails"** (email ưu tiên).
   - **Database "Blockers"** (những việc đang bị chặn).
   - **Database "Audit Log"** (để lưu lịch sử thay đổi).

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import** workflow từ file JSON hoặc **copy/paste** JSON vào **n8n Editor**:
1. Tải file JSON từ [n8n.io/workflows/14113](https://n8n.io/workflows/14113).
2. Mở **n8n Editor** → Nhấn **"Import"** → Chọn file JSON.
3. **Hoặc** copy toàn bộ JSON và paste vào **"Import from JSON"** trong Editor.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **A. Cấu Hình Notion (Trước Tất Cả)**
- **Tất cả các node Notion** (`Read Settings`, `Get Open Priorities`, `Get Recent Signals`, `Get Meeting Decisions`, `Get Urgent Emails`, `Get Blocked Actions`, `Update Notion Priority`, `Create Audit Log`) **cần kết nối với cùng một tài khoản Notion**.
- **Database Name** phải khớp với tên database trong Notion của các sếp:
  - `Open Priorities` → Database chứa các nhiệm vụ đang mở.
  - `Signals` → Database chứa tín hiệu mới.
  - `Meetings` → Database chứa quyết định cuộc họp.
  - `Emails` → Database chứa email ưu tiên.
  - `Blockers` → Database chứa những việc đang bị chặn.
  - `Audit Log` → Database để lưu lịch sử thay đổi.

#### **B. Cấu Hình OpenAI (AI Pass 1, 2, 3)**
- **API Key OpenAI** phải được thêm vào **Credentials** trong n8n:
  1. Mở **Settings** → **Credentials** → **Add Credential** → Chọn **OpenAI**.
  2. Điền **API Key** từ tài khoản OpenAI.
  3. Trong các node `AI Pass 1 - Impact`, `AI Pass 2 - Urgency`, `AI Pass 3 - Final Rank`, chọn **Credentials** là OpenAI vừa thêm.

#### **C. Cấu Hình Slack (Thông Báo Thay Đổi)**
- **Webhook Slack** phải được thêm vào **Credentials**:
  1. Tạo **Incoming Webhook** trong Slack (Settings → Apps → Incoming Webhooks).
  2. Copy **Webhook URL** và thêm vào **Credentials** trong n8n (chọn **Slack**).
  3. Trong node `Post Ranking Change` và `Slack No Changes`, chọn **Credentials** là Slack.

#### **D. Cấu Hình Schedule Trigger**
- **Thời gian chạy**: Workflow sẽ chạy **mỗi 2 giờ** trong ngày làm việc (Thứ 2 - Thứ 6).
- **Không chạy vào cuối tuần** (để tiết kiệm tài nguyên AI).
- **Cấu hình trong node `Rerank Trigger`**:
  - `Schedule`: `0 */2 * * 1-5` (mỗi 2 giờ, từ thứ 2 đến thứ 6).

#### **E. Các Node Quan Trọng Khác**
| **Node** | **Lưu Ý** |
|----------|-----------|
| `Normalize Priorities`, `Normalize Signals`, `Normalize Meetings`, `Normalize Emails`, `Normalize Blockers` | Các node này **chuyển đổi dữ liệu** sang định dạng chuẩn để AI phân tích. **Không cần chỉnh sửa** nếu dữ liệu Notion đã chuẩn. |
| `AI Pass 1 - Impact`, `AI Pass 2 - Urgency`, `AI Pass 3 - Final Rank` | **Prompt AI** đã được tối ưu sẵn. Nếu muốn **cải thiện kết quả**, các sếp có thể chỉnh sửa code trong node `Parse Impact`, `Parse Urgency`, `Parse Ranking`. |
| `CompareDatasets` | So sánh **ranking cũ vs mới**. Nếu có thay đổi, workflow sẽ **cập nhật Notion và Slack**. |
| `Batch Updates` | **Tối ưu hiệu suất** khi cập nhật nhiều ưu tiên cùng lúc. |

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy **manual test** để kiểm tra:
     - AI có phân tích đúng không?
     - Slack có thông báo thay đổi không?
     - Notion có cập nhật ưu tiên không?
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật Active** cho workflow.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Tối Ưu Hiệu Suất AI**
- **Chỉnh sửa Prompt** trong các node `AI Pass` để phù hợp với **ngôn ngữ và quy trình** của team.
- **Giảm số lượng ưu tiên** nếu AI chạy chậm (sử dụng node `Limit` để lấy ít hơn 20 ưu tiên).

### **2. Thêm Log Chi Tiết**
- **Tạo database "Execution Log"** trong Notion để lưu:
  - Thời gian chạy.
  - Số lượng ưu tiên được xếp hạng.
  - Thời gian xử lý của AI.

### **3. Kết Nối Với Trello/Asana**
- **Thay thế Notion bằng Trello/Asana** bằng cách:
  - Sử dụng **node Trello/Asana** thay cho Notion.
  - Cập nhật ưu tiên trên **board Trello** thay vì Notion.

### **4. Thông Báo Trên Email**
- **Thêm node Email** để gửi báo cáo hàng ngày về **ưu tiên mới** cho team.

### **5. Xử Lý Dữ Liệu Trùng Lặp**
- **Sử dụng node `Remove Duplicates`** để loại bỏ trùng lặp trong tín hiệu hoặc cuộc họp.

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp Product Manager để tập trung vào **các quyết định chiến lược** thay vì làm thủ công xếp hạng ưu tiên. **Với AI và tự động hóa**, các sếp sẽ luôn có **danh sách ưu tiên chính xác nhất**, cập nhật theo thời gian thực.

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n.
2. **Cấu hình Notion, OpenAI và Slack**.
3. **Bật Active** và **nhận danh sách ưu tiên tự động hàng ngày!**

🚀 **Tự động hóa quản lý dự án – không còn phụ thuộc vào con người!**