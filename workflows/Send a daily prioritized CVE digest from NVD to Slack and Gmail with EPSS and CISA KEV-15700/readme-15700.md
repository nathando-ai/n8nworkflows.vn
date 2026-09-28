---
title: "🚀 Gửi bản tóm tắt CVE hàng ngày ưu tiên tới Slack và Gmail với EPSS và CISA KEV"
description: "Tự động thu thập CVE mới, enrich EPSS, KEV, lọc, dedup, và gửi digest tới Slack và Gmail – giải pháp tự động hóa 100% không cần code."
slug: "cve-daily-digest-automation"
tags: [n8n, automation, no-code, cyber-security, vulnerability-management]
keywords: [n8n workflow, tự động hóa, CVE, EPSS, CISA KEV, vulnerability intelligence]
---

# 🚀 Gửi bản tóm tắt CVE hàng ngày ưu tiên tới Slack và Gmail với EPSS và CISA KEV

Bạn đang phải lướt qua hàng trăm CVE mới mỗi ngày, lọc thủ công, đánh giá mức độ nguy hiểm và gửi báo cáo cho team?  
Workflow này sẽ **đánh trúng mục tiêu**: tự động thu thập CVE mới, enrich EPSS & KEV, dedup, ưu tiên, và gửi digest tới Slack và Gmail – **không cần viết code**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần lướt qua từng CVE, workflow tự động làm việc 24/7.  
- **Chính xác & nhất quán**: Định dạng digest chuẩn, ưu tiên theo EPSS & KEV.  
- **Cá nhân hóa**: Định nghĩa watchlist, severity filter, kênh thông báo riêng cho từng tech.  
- **Hoạt động liên tục**: Được trigger hàng ngày, không phụ thuộc vào người dùng.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **NVD API Key**: Để fetch CVE mới.  
- **Gmail Credentials**: Để gửi email digest.  
- **Slack Credentials**: Để gửi Slack digest (chọn channel).  
- **URL CSV Watchlist**: Định dạng CSV như mẫu dưới đây.  
- **GitHub Mirror URL** (để fetch CISA KEV) – không cần key.  
- **EPSS API** (FIRST.org) – không cần key.  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON từ [n8n.io/workflows/15700](https://n8n.io/workflows/15700).  
2. Trong n8n Editor, chọn **Import** → **Upload JSON** → chọn file.  
3. Hoặc copy toàn bộ JSON và paste vào **Import JSON**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Tham số cần cấu hình |
|------|-------|---------------------|
| **Schedule Trigger** | Chạy hàng ngày | `Cron` hoặc `Daily` |
| **Read Watchlist CSV** | Đọc CSV watchlist | `File URL` (đổi sang URL của bạn) |
| **Fetch Technology Watchlist CSV** | Tải CSV (đối với Google Sheet) | `URL` |
| **Fetch Recent CVEs from NVD** | Lấy CVE mới | `API Key` |
| **Send Email Digest** | Gửi email | `Gmail Credentials`, `To`, `Subject` |
| **Send Slack Digest** | Gửi Slack | `Slack Credentials`, `Channel` |
| **Fetch EPSS** | Lấy EPSS | `URL` (FIRST.org) |
| **Fetch KEV from GitHub Mirror** | Lấy KEV | `URL` (GitHub mirror) |
| **Code nodes** (`Match CVEs to Watchlist`, `Deduplicate Alerts`, `Prioritize & Build Digest`, `Prepare EPSS Lookup`, `Attach EPSS Score`, `Attach KEV`) | Xử lý logic | Không cần credential, chỉ cần kiểm tra code logic. |

> **Tip**: Kiểm tra **Credentials** trong n8n → **Credentials** → tạo mới Gmail, Slack, HTTP Request (nếu cần).

### 3. Kích hoạt ⚡️
1. Chạy **Test** với dữ liệu mẫu (bấm **Execute Workflow**).  
2. Kiểm tra log, xem email & Slack.  
3. Nếu mọi thứ ổn, bật **Active**.

## ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram**: Thêm node Slack hoặc Telegram để gửi alert ngay khi CVE xuất hiện.  
- **Lưu log**: Dùng node **Write Binary File** để lưu JSON log vào Google Drive hoặc S3.  
- **Báo cáo định kỳ**: Thêm node **Schedule Trigger** khác để gửi báo cáo tuần/tháng.  
- **Tích hợp Jira**: Tạo ticket tự động khi CVE có mức độ cao.  
- **Alert tùy chỉnh**: Sử dụng webhook để gửi tới hệ thống SIEM của bạn.

## 📌 Kết luận
Workflow này là **đối tượng chuẩn** cho các team SecOps muốn có một nguồn thông tin CVE nhanh, chính xác và dễ dàng tùy chỉnh.  
Hãy **đăng ký VPS**, **đặt credentials**, **đưa vào workflow** và **bật nó** – ngay hôm nay, bạn sẽ nhận được bản tóm tắt CVE hàng ngày, ưu tiên theo EPSS và KEV, tới Slack và Gmail mà không cần viết một dòng code.

---