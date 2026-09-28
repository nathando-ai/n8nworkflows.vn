---
title: "🚀 Tự động tạo video AI HeyGen từ Google Sheets – Không cần code!"
description: "Chuyển nhanh các kịch bản trong Google Sheets thành video AI chất lượng cao bằng HeyGen, giảm thời gian chỉnh sửa và tăng tính chuyên nghiệp cho nội dung."
slug: "tua-dong-tao-video-ai-heygen-tu-google-sheets"
tags: [n8n, automation, no-code, content-creation, multimodal-ai]
keywords: [n8n workflow, tự động hóa, HeyGen, video AI, Google Sheets, content creation]
---

# 🚀 Tự động tạo video AI HeyGen từ Google Sheets – Không cần code!

Bạn đang phải mất hàng giờ để chuyển đổi kịch bản viết tay thành video? Bạn muốn nội dung của mình nhanh chóng xuất hiện trên YouTube, TikTok hay trang web mà không cần phải học phần mềm dựng video?  
Workflow **Convert Google Sheets scripts into HeyGen AI videos** của Panth1823 sẽ giúp bạn **tự động 100%**: từ khi nhập kịch bản vào Google Sheets, hệ thống sẽ **định dạng, gửi lên HeyGen, theo dõi trạng thái, và ghi lại link video** ngay vào bảng tính. Kết quả: tiết kiệm thời gian, giảm sai sót, và tăng tính chuyên nghiệp cho nội dung.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ chỉnh sửa video xuống chỉ vài phút.  
- **Độ chính xác cao**: Đảm bảo kịch bản không bị lỗi JSON, video được render đúng nội dung.  
- **Tự động hóa liên tục**: Khi thêm dòng mới vào Google Sheets, workflow sẽ tự động chạy mà không cần can thiệp.  
- **Tùy biến linh hoạt**: Thay đổi avatar, giọng nói, hoặc định dạng video chỉ qua một vài tham số.  
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Google Sheets**: Tài khoản Google và quyền truy cập vào bảng tính cần tạo video.  
- **HeyGen API Key**: Đăng ký tài khoản HeyGen và lấy API key.  
- **Avatar ID & Voice ID** (tùy chọn): ID của avatar và giọng nói muốn sử dụng trong video.  
- **Google Sheets Trigger**: Cấu hình Document ID và Sheet Name trong node.  
- **HTTP Request**: Cấu hình URL endpoint của HeyGen và truyền API key trong header.  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/14804) hoặc sao chép nội dung JSON.  
2. Mở n8n Editor, chọn **Import Workflow** → **Upload JSON** hoặc **Paste JSON**.  
3. Nhấn **Import** và workflow sẽ xuất hiện trong danh sách workflow của bạn.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Tham số cần cấu hình |
|------|-------|----------------------|
| **Google Sheets Trigger** | Gửi dữ liệu khi có dòng mới hoặc cập nhật | `Document ID`, `Sheet Name`, `Trigger on` |
| **Has Script?** | Kiểm tra có trường `Script` không | `Conditions` |
| **Process One at a Time** | Xử lý từng dòng một | `Batch Size = 1` |
| **Sanitize Script** | Loại bỏ ký tự gây lỗi JSON | `Code` (đã được cung cấp) |
| **Generate Video** | Gửi yêu cầu tạo video tới HeyGen | `URL`, `Headers` (API key), `Body` (script, avatar, voice) |
| **If** | Kiểm tra phản hồi đầu tiên | `Conditions` |
| **Wait** | Đợi trước khi kiểm tra trạng thái | `Duration` (tùy chỉnh) |
| **Video Status** | Kiểm tra trạng thái video | `URL`, `Headers` |
| **Is Complete?1** | Kiểm tra xem video đã hoàn thành | `Conditions` |
| **Update Sheet with Video1** | Ghi URL video vào Google Sheets | `Operation = Update`, `Sheet ID`, `Range` |
| **Wait Before Retry1** | Đợi trước khi thử lại nếu chưa hoàn thành | `Duration` |

> **Lưu ý**: Mỗi node có thể cần **Credentials** riêng. Đảm bảo đã tạo và gán đúng credentials trong phần **Credentials** của n8n.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (đảm bảo Google Sheet có ít nhất một dòng chưa có video).  
2. Kiểm tra log: Xem các node đã thực thi thành công.  
3. Khi mọi thứ ổn, bật **Active** cho workflow. Workflow sẽ tự động chạy mỗi khi có dòng mới.

## ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram notifications**: Thêm node Slack hoặc Telegram để nhận thông báo khi video được tạo xong.  
- **Lưu log vào Google Sheets**: Dùng node `Google Sheets` để ghi lại thời gian, trạng thái, và lỗi (nếu có).  
- **Scheduled runs**: Nếu muốn kiểm tra trạng thái video định kỳ, thêm node `Cron` để gọi lại node `Video Status`.  
- **Tùy chỉnh avatar/voice**: Thêm node `Set` ở đầu workflow để dễ dàng thay đổi ID avatar và voice mà không cần chỉnh node `Generate Video`.  

## 📌 Kết luận
Workflow này giúp các sếp **tự động hóa hoàn toàn quy trình tạo video AI** từ Google Sheets, giảm bớt công việc thủ công và tăng năng suất nội dung. Hãy thử ngay, tùy chỉnh theo nhu cầu và chia sẻ phản hồi để cộng đồng n8n ngày càng mạnh mẽ hơn!