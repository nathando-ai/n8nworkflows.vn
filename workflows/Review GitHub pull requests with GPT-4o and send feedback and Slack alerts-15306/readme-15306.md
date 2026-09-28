---
title: "🤖 Tự Động Học Review PR GitHub Với GPT-4o & Gửi Feedback + Cảnh Báo Slack (Không Cần Code)"
description: "Workflow tự động hóa đánh giá PR GitHub bằng trí tuệ nhân tạo, gửi phản hồi chi tiết và cảnh báo cấp thiết đến Slack khi phát hiện lỗi nghiêm trọng. Giúp devs tiết kiệm 8+ giờ/ngày và giảm thiểu lỗi trong codebase."
slug: "tieu-dong-hoc-review-pr-github-gpt-4o-slack"
tags: [n8n, automation, devops, ai-summarization, github, slack, openai]
keywords: [tự động hóa github, review code ai, gpt-4o n8n, cảnh báo slack, tự động hóa devops, workflow n8n github]
---

# 🚀 **Tự Động Học Review PR GitHub Với GPT-4o & Gửi Feedback + Cảnh Báo Slack**

### **Giải pháp cho nỗi đau của các sếp DevOps & Team Lead**
Hàng ngày, các sếp phải **quét hàng chục PR**, đọc code, đánh giá chất lượng và gửi feedback cho team. Đây là công việc **mệt mỏi, tốn thời gian (8+ giờ/ngày)** và dễ bị lỗi sót. **Workflow này tự động hóa toàn bộ quy trình** bằng trí tuệ nhân tạo (GPT-4o), giúp:
✅ **Tiết kiệm 8+ giờ/ngày** cho devs và PMs
✅ **Giảm thiểu lỗi nghiêm trọng** bằng cách cảnh báo ngay khi phát hiện vấn đề cấp thiết
✅ **Cung cấp feedback chi tiết** cho PR, giúp devs cải thiện code nhanh chóng
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động review PR** ngay khi mở, không cần chờ devs nhắc nhở.
- **Cảnh báo lỗi nghiêm trọng** (critical severity) ngay trên Slack, giúp team phản ứng kịp thời.
- **Feedback cá nhân hóa** cho mỗi PR, giúp devs học hỏi và cải thiện kỹ năng.
- **Giảm thiểu PR bị reject** do lỗi nhỏ, tăng hiệu suất code review.
- **Hoạt động liên tục** mà không cần can thiệp, tiết kiệm chi phí cho team QA.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản GitHub** với quyền:
   - **Access to repositories** (để đọc PR và gửi comment).
   - **Personal Access Token (PAT)** với quyền `repo`, `admin:org` (nếu review nhiều repo).
2. **API Key OpenAI** (để sử dụng GPT-4o):
   - Mua tại [OpenAI Platform](https://platform.openai.com/) (từ **$20/month** cho 1M token).
   - **Lưu ý**: Workflow này **không tự động tạo API key**, các sếp phải **cài đặt thủ công** trong n8n.
3. **Webhook URL của Slack** (để gửi cảnh báo):
   - Tạo **Incoming Webhook** trong Slack (Settings > Apps & Integrations > Incoming Webhooks).
   - **Lưu URL** này để kết nối với n8n.
4. **n8n Self-hosted** (không dùng n8n.cloud):
   - **Tại sao?** Workflow này **không nên chạy trên cloud** vì:
     - **Chi phí cao** (OpenAI API + Slack Webhook).
     - **Bảo mật cao** (API Key OpenAI không nên lưu trên cloud).
   - **👉 Đăng ký VPS TinoHost** (giảm 39% với mã **VPSN8N**):
     [https://tino.vn/vps-n8n?affid=388](https://tino.vn/vps-n8n?affid=388)
   - **👉 Đăng ký VPS Xeon 4GB chỉ 50k/tháng**:
     [https://my.bnix.one/aff.php?aff=172](https://my.bnix.one/aff.php?aff=172)
:::

---
## 🚀 **Cách Import & Lưu ý khi "Lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/15306](https://n8n.io/workflows/15306) (chọn **Download JSON**).
2. Trên **n8n Editor**, nhấn **Import** > Chọn file JSON vừa tải.
3. **Xác nhận** và workflow sẽ xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/15306](https://n8n.io/workflows/15306).
2. Trên **n8n Editor**, nhấn **Import** > Chọn **Paste JSON**.
3. **Xác nhận** và workflow sẽ được tạo.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Node 1: "When PR Opened" (githubTrigger)**
- **Cấu hình**:
  - **Repository**: Chọn repo cần review (hoặc để trống để review tất cả).
  - **Event**: Chọn **Pull Request** (default).
  - **Filter**: Chỉ **opened** (không cần chỉnh).
- **Lưu ý**:
  - Nếu muốn review **nhiều repo**, cần **cấu hình PAT với quyền `repo`** trong GitHub.

#### **🔹 Node 2: "Check PR Open" (if)**
- **Điều kiện**: `{{ $json.payload.action }} === "opened"` (default, không cần chỉnh).

#### **🔹 Node 3: "Fetch PR Diff" (httpRequest)**
- **URL**: `{{ $json.payload.pull_request.diff_url }}` (auto fill).
- **Headers**:
  - `Accept: application/vnd.github.v3.diff`.
- **Lưu ý**:
  - Nếu PR có **diff quá lớn**, GPT-4o có thể **không xử lý được**. Các sếp nên **cắt diff** bằng regex trong node **Format PR Diff** (node 4).

#### **🔹 Node 4: "Format PR Diff" (code)**
- **Mã JavaScript** (cần chỉnh nếu diff quá dài):
  ```javascript
  // Cắt diff thành 10.000 ký tự đầu (GPT-4o có giới hạn input ~8KB)
  const diff = $input.all()[0].json.diff;
  const maxLength = 10000;
  const formattedDiff = diff.substring(0, maxLength);

  return {
    json: {
      diff: formattedDiff,
      prNumber: $input.all()[0].json.payload.pull_request.number,
      prTitle: $input.all()[0].json.payload.pull_request.title,
      prUrl: $input.all()[0].json.payload.pull_request.html_url
    }
  };
  ```
- **Lưu ý**:
  - Nếu diff **quá dài**, GPT-4o sẽ **bỏ lỡ phần code quan trọng**. Các sếp nên **tùy chỉnh maxLength** theo nhu cầu.

#### **🔹 Node 5: "AI Code Review with GPT-4o" (openAi)**
- **Cấu hình**:
  - **API Key**: Điền **API Key OpenAI** (từ OpenAI Platform).
  - **Model**: Chọn **gpt-4o** (mới nhất, hiệu suất cao).
  - **Prompt** (cần chỉnh để phù hợp với team):
    ```json
    {
      "role": "system",
      "content": "You are a senior software engineer reviewing GitHub pull requests. Your task is to analyze the code diff and provide detailed feedback. Follow this format:

      ### Review Summary
      - **Overall Quality**: [Good/Fair/Poor]
      - **Critical Issues**: [List any critical bugs or security issues]
      - **Suggestions for Improvement**: [List improvements]

      ### Detailed Feedback
      [Provide line-by-line feedback on the changes]

      ### Code Quality Score (1-10): [Score]

      ---

      **PR Details**:
      - Title: {{ $input.all()[0].json.prTitle }}
      - URL: {{ $input.all()[0].json.prUrl }}
      - Diff: {{ $input.all()[0].json.diff }}"
    }
    ```
  - **Temperature**: 0.7 (giá trị mặc định, không cần chỉnh).
  - **Max Tokens**: 1000 (đủ cho feedback chi tiết).
- **Lưu ý**:
  - **Chi phí**: GPT-4o tính theo **token**, ~$0.005/1K tokens. Các sếp nên **monitor chi phí** trong OpenAI Dashboard.

#### **🔹 Node 6: "Build Comment for GitHub" (code)**
- **Mã JavaScript** (auto build comment từ output của GPT-4o):
  ```javascript
  const review = $input.all()[0].json;
  const prNumber = $input.all()[0].json.prNumber;

  return {
    json: {
      body: `### AI Code Review Summary for PR #${prNumber}

      **PR Title**: ${review.choices[0].message.content.split("---")[0].split("### Review Summary")[1].trim()}

      **Overall Quality**: ${extractQuality(review.choices[0].message.content)}
      **Critical Issues**: ${extractCriticalIssues(review.choices[0].message.content)}
      **Suggestions**: ${extractSuggestions(review.choices[0].message.content)}
      **Code Quality Score**: ${extractScore(review.choices[0].message.content)}

      **Full Review**:
      ${review.choices[0].message.content.split("---")[1].trim()}

      ---

      *This comment was auto-generated by n8n AI Reviewer.*`,
      prNumber: prNumber
    }
  };

  function extractQuality(content) {
    const match = content.match(/Overall Quality: (Good|Fair|Poor)/);
    return match ? match[1] : "Unknown";
  }

  function extractCriticalIssues(content) {
    const match = content.match(/Critical Issues: (.*)/s);
    return match ? match[1].replace(/^[\n ]+|[\n ]+$/g, '') : "None";
  }

  function extractSuggestions(content) {
    const match = content.match(/Suggestions for Improvement: (.*)/s);
    return match ? match[1].replace(/^[\n ]+|[\n ]+$/g, '') : "None";
  }

  function extractScore(content) {
    const match = content.match(/Code Quality Score \(1-10\): (\d+)/);
    return match ? match[1] : "N/A";
  }
  ```
- **Lưu ý**:
  - Nếu GPT-4o **trả về format sai**, các sếp cần **tùy chỉnh regex** trong code.

#### **🔹 Node 7: "Post Comment to GitHub" (github)**
- **Cấu hình**:
  - **Repository**: Chọn repo tương ứng.
  - **Operation**: `createComment`.
  - **PR Number**: `{{ $input.all()[0].json.prNumber }}`.
  - **Comment Body**: `{{ $input.all()[0].json.body }}`.
- **Lưu ý**:
  - Nếu **PAT không đủ quyền**, comment sẽ **không được gửi**. Các sếp cần **kiểm tra lại quyền PAT**.

#### **🔹 Node 8: "Check Critical Severity" (if)**
- **Điều kiện** (cần chỉnh theo logic team):
  ```json
  {
    "condition": {
      "expression": "{{ $json.body.includes('Critical Issues') && $json.body.includes('Poor') }}"
    }
  }
  ```
  - **Lưu ý**: Các sếp nên **tùy chỉnh điều kiện** để phù hợp với mức độ nghiêm trọng của team.

#### **🔹 Node 9: "Alert Critical Issues to Slack" (slack)**
- **Cấu hình**:
  - **Webhook URL**: Điền **URL Slack Webhook** (từ bước chuẩn bị).
  - **Message**:
    ```json
    {
      "text": "🚨 **CRITICAL ISSUE DETECTED IN PR #{{ $input.all()[0].json.prNumber }}**",
      "blocks": [
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": `*PR Title:* ${$input.all()[0].json.prTitle}\n*URL:* ${$input.all()[0].json.prUrl}\n*Critical Issues:* ${extractCriticalIssues($input.all()[0].json.body)}`
          }
        },
        {
          "type": "actions",
          "elements": [
            {
              "type": "button",
              "text": {
                "type": "plain_text",
                "text": "View PR"
              },
              "url": "{{ $input.all()[0].json.prUrl }}"
            }
          ]
        }
      ]
    }
    ```
  - **Lưu ý**:
    - **Không nên gửi toàn bộ feedback** vào Slack (tránh spam).
    - **Tùy chỉnh message** để phù hợp với team.

#### **🔹 Node 10: "Share Review Summary on Slack" (slack)**
- **Cấu hình**:
  - **Webhook URL**: Điền **URL Slack Webhook** (giống node 9).
  - **Message**:
    ```json
    {
      "text": "📝 **AI Review Summary for PR #{{ $input.all()[0].json.prNumber }}**",
      "blocks": [
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": `*PR:* ${$input.all()[0].json.prTitle}\n*Score:* ${extractScore($input.all()[0].json.body)}\n*Quality:* ${extractQuality($input.all()[0].json.body)}`
          }
        },
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": `*Suggestions:*\n${$input.all()[0].json.body.split("Suggestions for Improvement:")[1].split("Code Quality Score")[0].replace(/^[\n ]+|[\n ]+$/g, '')}`
          }
        },
        {
          "type": "actions",
          "elements": [
            {
              "type": "button",
              "text": {
                "type": "plain_text",
                "text": "View PR"
              },
              "url": "{{ $input.all()[0].json.prUrl }}"
            }
          ]
        }
      ]
    }
    ```
- **Lưu ý**:
  - **Không nên gửi feedback dài** vào Slack (tránh spam).
  - **Tùy chỉnh blocks** để phù hợp với layout Sl