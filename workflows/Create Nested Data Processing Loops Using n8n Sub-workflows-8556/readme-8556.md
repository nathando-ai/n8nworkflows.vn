---
title: "🚀 Tạo Vòng Lặp Lồng Nhau với Sub‑Workflow trong n8n"
description: "Giải pháp tự động hóa 100% không cần code để xử lý dữ liệu lồng nhau trong n8n, giảm thời gian và lỗi thủ công."
slug: "tua-vong-lap-lon-nho-sub-workflow-n8n"
tags: [n8n, automation, no-code, sub-workflow, loops, engineering]
keywords: [n8n workflow, tự động hóa, vòng lặp lồng nhau, sub-workflow, n8n engineering]
---

# 🚀 Tạo Vòng Lặp Lồng Nhau với Sub‑Workflow trong n8n

Bạn đang phải xử lý hai danh sách dữ liệu lồng nhau, ví dụ: **một danh sách màu sắc** và **một danh sách số nguyên**. Việc lặp qua từng màu rồi lặp qua từng số nguyên trong mỗi màu thường gây lỗi khi dùng các node **Loop** mặc định của n8n. Đừng lo, workflow này sẽ giúp bạn **tự động hóa hoàn toàn** mà không cần viết code, chỉ cần cấu hình một vài node và chạy.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động lặp qua hai danh sách mà không cần viết script.
- **Độ chính xác cao**: Tránh lỗi khi lặp lồng nhau, dữ liệu luôn được xử lý đầy đủ.
- **Mô-đun dễ bảo trì**: Sub‑workflow có thể tái sử dụng trong nhiều workflow khác.
- **Tự động 24/7**: Khi được kích hoạt qua webhook hoặc trigger, workflow chạy liên tục mà không cần can thiệp.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **n8n** đã được cài đặt và chạy (Self‑hosted hoặc n8n.cloud).
- **Không cần API keys** vì workflow này chỉ dùng các node nội bộ (manualTrigger, code, splitInBatches, executeWorkflow, executeWorkflowTrigger, set).
- Nếu muốn gửi dữ liệu ra ngoài (email, Slack, …) thì cần cấu hình credentials tương ứng, nhưng không bắt buộc cho ví dụ này.
:::

## 🚀 Cách import & Lưu ý khi “lên đồ”

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/8556) hoặc sao chép nội dung JSON.
2. Trong n8n Editor, chọn **Import** → **Import from JSON** → dán nội dung JSON → **Import**.
3. Workflow sẽ xuất hiện với 8 node đã được cấu hình sẵn.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cấu hình cần chỉnh |
|------|-------|---------------------|
| **When clicking ‘Execute workflow’** | Trigger thủ công | Không cần chỉnh |
| **Colors** (code) | Tạo mảng màu | Đảm bảo mảng có ít nhất 2-3 màu |
| **Loop Over Colors** (splitInBatches) | Lặp qua từng màu | `Batch size` = 1 (mặc định) |
| **When Executed by Another Workflow** (executeWorkflowTrigger) | Trigger cho sub‑workflow | Không cần chỉnh |
| **Integers** (code) | Tạo mảng số nguyên | Đảm bảo mảng có ít nhất 2-3 số |
| **Loop Over Integers** (splitInBatches) | Lặp qua từng số | `Batch size` = 1 |
| **Edit Fields** (set) | Thêm dữ liệu vào mỗi lần lặp | Đặt các trường cần truyền sang sub‑workflow (ví dụ: `color`, `integer`) |
| **Execute Sub-workflow** (executeWorkflow) | Gọi sub‑workflow | **Cần cập nhật** trường **Sub‑workflow** → chọn workflow đã tạo ở bước 3 |

> **Lưu ý**: Sub‑workflow phải được tạo riêng (bắt đầu từ node **Execute Sub-workflow Trigger**) và lưu lại. Sau đó, trong node **Execute Sub-workflow** của workflow chính, chọn sub‑workflow vừa tạo.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow thủ công bằng cách click nút **Execute workflow**. Kiểm tra log để đảm bảo vòng lặp lồng nhau hoạt động đúng.
2. **Bật Active**: Khi đã chắc chắn, chuyển workflow sang trạng thái **Active** để nó tự động chạy khi trigger được kích hoạt.

## ✍️ Mẹo & gợi ý nâng cao
- **Gửi kết quả qua Slack**: Thêm node **Slack** sau node **Execute Sub-workflow** để thông báo kết quả mỗi lần lặp.
- **Lưu log vào Google Sheet**: Dùng node **Google Sheets** để ghi lại từng kết quả lặp, giúp theo dõi lịch sử.
- **Thêm trigger webhook**: Thay vì trigger thủ công, dùng node **Webhook** để workflow chạy khi nhận request từ bên ngoài.
- **Tối ưu batch size**: Nếu danh sách lớn, tăng `Batch size` trong `splitInBatches` để giảm số lần gọi sub‑workflow.

## 📌 Kết luận
Với workflow này, các sếp có thể **tự động hóa hoàn toàn** việc xử lý dữ liệu lồng nhau mà không cần viết code. Chỉ cần một vài bước cấu hình và bạn đã có thể chạy vòng lặp lồng nhau một cách chính xác, nhanh chóng và dễ bảo trì. Hãy thử ngay và cảm nhận sự khác biệt!

---