---
layout: default
title: "Bắt đầu với OpenClaw"
nav_exclude: true
---

# Bắt Đầu Với OpenClaw (Dịch Tiếng Việt)

## Mục tiêu

Mục tiêu của phần này là giúp bạn bắt đầu từ con số 0 đến khi có cuộc trò chuyện đầu tiên với OpenClaw một cách nhanh nhất có thể.

## Cách nhanh nhất để trò chuyện

Cách nhanh nhất để trò chuyện mà không cần thiết lập kênh: mở Giao Diện Điều Khiển (Control UI). Chạy lệnh:

```
openclaw dashboard
```

và trò chuyện trong trình duyệt, hoặc mở http://127.0.0.1:18789/ trên máy chủ gateway.

Tài liệu: [Giao Diện Điều Khiển](../index.md) và [Giao Diện Điều Khiển Trình Duyệt](../index.md).

## Cách được khuyến nghị

Sử dụng trình hướng dẫn CLI (openclaw onboard). Trình hướng dẫn này sẽ thiết lập:

- Mô hình/Xác thực (khuyến nghị dùng OAuth)
- Cài đặt gateway
- Kênh (WhatsApp/Telegram/Discord/Mattermost (plugin)/...)
- Thiết lập mặc định để ghé nối an toàn (secure DMs)
- Bootstrap workspace + kỹ năng (skills)
- Dịch vụ nền tùy chọn (optional background service)

Nếu bạn muốn xem các trang tài liệu chi tiết hơn, hãy chuyển đến: [Trình Hướng Dẫn](wizard.md), [Thiết Lập](setup.md), [Ghé Nối](pairing.md), [Bảo Mật](../gateway/security.md).

## Yêu cầu hệ thống

- Node >=22
- pnpm (tùy chọn; khuyến nghị nếu bạn xây dựng từ mã nguồn)
- Khuyến nghị: Khóa API Brave Search để tìm kiếm web. Cách dễ nhất:

```
openclaw configure --section web
```

(lưu trữ tại tools.web.search.apiKey). Xem [Công cụ Web](../tools/web.md).

**macOS**: Nếu bạn định xây dựng ứng dụng, hãy cài đặt Xcode / CLT. Chỉ với CLI + gateway, chỉ cần Node.

**Windows**: sử dụng WSL2 (khuyến nghị Ubuntu). Rất khuyến nghị dùng WSL2; Windows gốc chưa được kiểm thử kỹ, có nhiều vấn đề hơn, và khả năng tương thích công cụ kém hơn. Hãy cài WSL2 trước, sau đó chạy các bước Linux bên trong WSL. Xem [Windows (WSL2)](../../platforms/windows.md).

## Cài đặt CLI (khuyến nghị)

```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```

Các tùy chọn cài đặt (phương pháp cài đặt, không tương tác, từ GitHub): [Cài đặt](../../install.md).

**Windows (PowerShell)**:
```powershell
iwr -useb https://openclaw.ai/install.ps1 | iex
```

Cách thay thế (cài đặt toàn cục):
```bash
npm install -g openclaw@latest
```
hoặc
```bash
pnpm add -g openclaw@latest
```

## Chạy trình hướng dẫn thiết lập (và cài đặt dịch vụ)

```bash
openclaw onboard --install-daemon
```

Những điều bạn sẽ chọn:

- Gateway cục bộ hoặc từ xa
- Xác thực: OpenAI Code (Codex) đăng ký (OAuth) hoặc khóa API. Với Anthropic, chúng tôi khuyến nghị dùng khóa API; cũng hỗ trợ claude setup-token.
- Nhà cung cấp: đăng nhập WhatsApp QR, mã token Telegram/Discord, mã token Mattermost plugin, v.v.
- Dịch vụ nền: cài đặt nền (launchd/systemd; WSL2 dùng systemd)

Chạy: Node (khuyến nghị; bắt buộc cho WhatsApp/Telegram). Không khuyến nghị dùng Bun.

- Mã token Gateway: trình hướng dẫn tạo một mã mặc định (ngay cả khi dùng loopback) và lưu trữ tại gateway.auth.token.

Tài liệu trình hướng dẫn: [Trình Hướng Dẫn](wizard.md)

### Xác thực: nơi lưu trữ (quan trọng)

- Đường dẫn Anthropic được khuyến nghị: đặt khóa API (trình hướng dẫn có thể lưu trữ để sử dụng dịch vụ). Cũng hỗ trợ claude setup-token nếu bạn muốn tái sử dụng thông tin đăng nhập Claude Code.

- Thông tin xác thực OAuth (nhập từ legacy): ~/.openclaw/credentials/oauth.json

- Hồ sơ xác thực (OAuth + khóa API): ~/.openclaw/agents//agent/auth-profiles.json

**Mẹo cho máy chủ/headless**: thực hiện OAuth trên máy bình thường trước, sau đó sao chép oauth.json sang máy chủ gateway.

## Bắt đầu Gateway

Nếu bạn đã cài đặt dịch vụ trong quá trình hướng dẫn, Gateway đã nên đang chạy:

```bash
openclaw gateway status
```

Chạy thủ công (foreground):

```bash
openclaw gateway --port 18789 --verbose
```

Giao diện điều khiển (local loopback): http://127.0.0.1:18789/

Nếu một mã token được cấu hình, dán nó vào cài đặt Giao Diện Điều Khiển (lưu trữ dưới connect.params.auth.token).

⚠️ **Cảnh báo Bun (WhatsApp + Telegram)**: Bun có các vấn đề đã biết với các kênh này. Nếu bạn dùng WhatsApp hoặc Telegram, hãy chạy Gateway với Node.

## Kiểm tra nhanh (2 phút)

```bash
openclaw status
openclaw health
openclaw security audit --deep
```

## Ghé nối + kết nối bề mặt trò chuyện đầu tiên

### WhatsApp (đăng nhập QR)

```bash
openclaw channels login
```

Quét qua WhatsApp → Cài đặt → Thiết Bị Đã Kết Nối.

Tài liệu WhatsApp: [WhatsApp](../channels/whatsapp.md)

### Telegram / Discord / các nền tảng khác

Trình hướng dẫn có thể tự động ghi mã token/cấu hình cho bạn. Nếu bạn muốn cấu hình thủ công, bắt đầu với:

- Telegram: [Telegram](../channels/telegram.md)
- Discord: [Discord](../channels/discord.md)
- Mattermost (plugin): [Mattermost](../channels/mattermost.md)

**Mẹo DM Telegram**: tin nhắn DM đầu tiên của bạn sẽ trả về một mã ghé nối. Chấp thuận nó (xem bước tiếp theo) nếu không bot sẽ không phản hồi.

## Bảo mật DM (chấp thuận ghé nối)

Tư thế mặc định: DM chưa biết sẽ nhận một mã ngắn và tin nhắn sẽ không được xử lý cho đến khi được chấp thuận.

Nếu tin nhắn DM đầu tiên của bạn không nhận được phản hồi, hãy chấp thuận ghé nối:

```bash
openclaw pairing list whatsapp
openclaw pairing approve whatsapp <code>
```

Tài liệu ghé nối: [Ghé Nối](pairing.md)

## Kiểm tra từ đầu đến cuối

Trong một cửa sổ lệnh mới, gửi một tin nhắn thử:

```bash
openclaw message send --target +15555550123 --message "Xin chào từ OpenClaw"
```

Nếu openclaw health hiển thị "no auth configured", hãy quay lại trình hướng dẫn và đặt xác thực OAuth/khóa - agent sẽ không thể phản hồi nếu không có nó.

**Mẹo**: openclaw status --all là báo cáo gỡ lỗi đọc được tốt nhất.

## Các bước tiếp theo (tùy chọn, nhưng tuyệt vời)

- Ứng dụng thanh menu macOS + đánh thức bằng giọng nói: [Ứng dụng macOS](../../platforms/macos.md)
- Nút iOS/Android (Canvas/máy ảnh/giọng nói): [Nút](../../nodes/index.md)
- Truy cập từ xa (SSH tunnel / Tailscale Serve): [Truy cập từ xa](../gateway/remote.md) và [Tailscale](../gateway/tailscale.md)
- Thiết lập luôn bật / VPN: [Truy cập từ xa](../gateway/remote.md), [exe.dev](../../platforms/exe-dev.md), [Hetzner](../../platforms/hetzner.md), [macOS từ xa](../../platforms/mac/remote.md)

---

## Gợi ý cho người mới

💡 **Mẹo quan trọng**: Nếu bạn là người mới bắt đầu, hãy làm theo trình hướng dẫn (wizard) vì nó sẽ giúp bạn thiết lập mọi thứ một cách chính xác mà không cần phải hiểu hết các khái niệm phức tạp ngay từ đầu.

💡 **Lỗi thường gặp**: Đảm bảo rằng bạn đang sử dụng Node.js phiên bản >=22 và không sử dụng Bun nếu bạn định dùng WhatsApp hoặc Telegram.

💡 **Bảo mật**: Luôn sử dụng mã token để bảo vệ gateway của bạn, ngay cả khi chỉ chạy trên máy cục bộ.