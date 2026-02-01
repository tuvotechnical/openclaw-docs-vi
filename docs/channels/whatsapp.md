---
layout: default
title: "Kết nối WhatsApp"
nav_exclude: true
---

# Kết Nối WhatsApp Với OpenClaw (Dịch Tiếng Việt)

## Tổng quan

OpenClaw hỗ trợ kết nối với WhatsApp thông qua giao thức WhatsApp Web bằng thư viện Baileys. Gateway sẽ quản lý phiên (session) của bạn.

## Thiết lập nhanh (cho người mới)

1. Sử dụng số điện thoại riêng nếu có thể (khuyến nghị)
2. Cấu hình WhatsApp trong ~/.openclaw/openclaw.json
3. Chạy lệnh `openclaw channels login` để quét mã QR (Thiết Bị Đã Kết Nối)
4. Bắt đầu gateway

Cấu hình tối thiểu:
```json
{
  "channels": {
    "whatsapp": {
      "dmPolicy": "allowlist",
      "allowFrom": ["+15551234567"]
    }
  }
}
```

## Mục tiêu

- Hỗ trợ nhiều tài khoản WhatsApp (multi-account) trong một tiến trình Gateway
- Định tuyến xác định: phản hồi quay lại WhatsApp, không cần định tuyến qua mô hình
- Mô hình thấy đủ ngữ cảnh để hiểu các phản hồi trích dẫn (quoted replies)

## Cấu hình (cho phép ghi đè)

Theo mặc định, WhatsApp được phép ghi các cập nhật cấu hình được kích hoạt bởi /config set|unset (cần có commands.config: true).

Tắt bằng:
```json
{
  "channels": { "whatsapp": { "configWrites": false } }
}
```

## Kiến trúc (ai quản lý cái gì)

- Gateway quản lý socket Baileys và vòng lặp hộp thư đến
- CLI / ứng dụng macOS giao tiếp với gateway; không sử dụng Baileys trực tiếp
- Trình lắng nghe hoạt động là bắt buộc cho việc gửi đi; nếu không, gửi thất bại nhanh

## Lấy số điện thoại (hai chế độ)

WhatsApp yêu cầu số điện thoại di động thật để xác minh. Số VoIP và ảo thường bị chặn. Có hai cách được hỗ trợ để chạy OpenClaw trên WhatsApp:

### Số điện thoại riêng (khuyến nghị)

Sử dụng số điện thoại riêng cho OpenClaw. Trải nghiệm người dùng tốt nhất, định tuyến sạch, không có các lỗi tự trò chuyện. Cấu hình lý tưởng: điện thoại Android cũ + eSIM. Để nó bật Wi-Fi và nguồn, và liên kết qua QR.

**WhatsApp Business**: Bạn có thể sử dụng WhatsApp Business trên cùng thiết bị với số khác. Rất tốt để giữ WhatsApp cá nhân riêng biệt - cài đặt WhatsApp Business và đăng ký số OpenClaw ở đó.

Cấu hình mẫu (số điện thoại riêng, danh sách cho phép người dùng đơn):
```json
{
  "channels": {
    "whatsapp": {
      "dmPolicy": "allowlist",
      "allowFrom": ["+15551234567"]
    }
  }
}
```

**Chế độ ghé nối** (tùy chọn):
Nếu bạn muốn ghé nối thay vì danh sách cho phép, đặt `channels.whatsapp.dmPolicy` thành `pairing`. Người gửi chưa biết nhận được mã ghé nối; chấp thuận với:

```
openclaw pairing approve whatsapp <code>
```

### Số điện thoại cá nhân (phương án dự phòng)

Phương án nhanh: chạy OpenClaw trên số điện thoại của bạn. Gửi tin nhắn cho chính mình (WhatsApp "Gửi tin nhắn cho chính bạn") để thử nghiệm để không làm phiền người khác. Mong đợi phải đọc mã xác minh trên điện thoại chính của bạn trong quá trình thiết lập và thử nghiệm. Phải bật chế độ tự trò chuyện.

Khi trình hướng dẫn hỏi số WhatsApp của bạn, hãy nhập số điện thoại bạn sẽ gửi từ (người sở hữu/người gửi), không phải số trợ lý.

Cấu hình mẫu (số điện thoại cá nhân, chế độ tự trò chuyện):
```json
{
  "whatsapp": {
    "selfChatMode": true,
    "dmPolicy": "allowlist",
    "allowFrom": ["+15551234567"]
  }
}
```

Phản hồi tự trò chuyện mặc định là [{identity.name}] khi được đặt (nếu không là [openclaw])
nếu messages.responsePrefix chưa được đặt. Đặt nó rõ ràng để tùy chỉnh hoặc tắt
tiền tố (sử dụng "" để loại bỏ nó).

### Mẹo lấy số điện thoại

- eSIM địa phương từ nhà mạng của bạn (đáng tin cậy nhất)
  - Áo: [hot.at](https://www.hot.at)
  - Vương quốc Anh: [giffgaff](https://www.giffgaff.com) - SIM miễn phí, không hợp đồng
- SIM trả trước - rẻ, chỉ cần nhận một SMS để xác minh
- Tránh: TextNow, Google Voice, hầu hết các dịch vụ "SMS miễn phí" - WhatsApp chặn các dịch vụ này một cách tích cực

**Mẹo**: Số chỉ cần nhận một SMS xác minh. Sau đó, phiên WhatsApp Web tiếp tục tồn tại qua creds.json.

## Tại sao không dùng Twilio?

- Các bản dựng OpenClaw ban đầu hỗ trợ tích hợp WhatsApp Business của Twilio.
- Số WhatsApp Business là lựa chọn tồi cho một trợ lý cá nhân.
- Meta thực thi cửa sổ phản hồi 24 giờ; nếu bạn chưa phản hồi trong 24 giờ qua, số doanh nghiệp không thể bắt đầu tin nhắn mới.
- Sử dụng với khối lượng cao hoặc "nói chuyện nhiều" kích hoạt chặn tích cực, vì tài khoản doanh nghiệp không dành để gửi hàng tá tin nhắn trợ lý cá nhân.
- Kết quả: giao hàng không đáng tin cậy và chặn thường xuyên, vì vậy hỗ trợ đã bị xóa bỏ.

## Đăng nhập + thông tin xác thực

- Lệnh đăng nhập: `openclaw channels login` (QR qua Thiết Bị Đã Kết Nối)
- Đăng nhập nhiều tài khoản: `openclaw channels login --account` ( = accountId)
- Tài khoản mặc định (khi --account bị bỏ qua): mặc định nếu có, nếu không là tài khoản đầu tiên được cấu hình (được sắp xếp)
- Thông tin xác thực được lưu trữ trong ~/.openclaw/credentials/whatsapp//creds.json
- Bản sao lưu tại creds.json.bak (được khôi phục khi bị hỏng)
- Tương thích cũ: các bản cài đặt cũ hơn lưu trữ các tệp Baileys trực tiếp trong ~/.openclaw/credentials/
- Đăng xuất: `openclaw channels logout` (hoặc --account ) xóa trạng thái xác thực WhatsApp (nhưng giữ oauth.json chung)
- Socket đăng xuất => lỗi hướng dẫn liên kết lại

## Luồng nhận vào (DM + nhóm)

- Sự kiện WhatsApp đến từ messages.upsert (Baileys)
- Trình lắng nghe hộp thư đến bị ngắt kết nối khi tắt để tránh tích lũy trình xử lý sự kiện trong các lần thử nghiệm/khởi động lại
- Trò chuyện trạng thái/phát sóng bị bỏ qua
- Trò chuyện trực tiếp sử dụng E.164; nhóm sử dụng nhóm JID
- Chính sách DM: `channels.whatsapp.dmPolicy` kiểm soát quyền truy cập trò chuyện trực tiếp (mặc định: ghé nối)

**Ghé nối**: người gửi chưa biết nhận được mã ghé nối (chấp thuận qua `openclaw pairing approve whatsapp`; mã hết hạn sau 1 giờ).

**Mở**: yêu cầu `channels.whatsapp.allowFrom` bao gồm "*".

Số WhatsApp được liên kết của bạn được tin tưởng ngầm, vì vậy tin nhắn tự gửi bỏ qua các kiểm tra `channels.whatsapp.dmPolicy` và `channels.whatsapp.allowFrom`.

### Chế độ số điện thoại cá nhân (phương án dự phòng)

Nếu bạn chạy OpenClaw trên số WhatsApp cá nhân của mình, hãy bật `channels.whatsapp.selfChatMode` (xem mẫu ở trên).

Hành vi:
- DM gửi đi không bao giờ kích hoạt phản hồi ghé nối (ngăn làm phiền người liên hệ)
- Người gửi chưa biết nhận được `channels.whatsapp.dmPolicy`
- Chế độ tự trò chuyện (allowFrom bao gồm số của bạn) tránh xác nhận đã đọc tự động và bỏ qua ID đề cập
- Xác nhận đã đọc được gửi cho DM không tự trò chuyện

## Xác nhận đã đọc

Theo mặc định, gateway đánh dấu tin nhắn WhatsApp đến là đã đọc (dấu xanh) khi chúng được chấp nhận.

Tắt toàn cầu:
```json
{
  "channels": { "whatsapp": { "sendReadReceipts": false } }
}
```

Tắt theo tài khoản:
```json
{
  "channels": {
    "whatsapp": {
      "accounts": {
        "personal": { "sendReadReceipts": false }
      }
    }
  }
}
```

Ghi chú:
- Chế độ tự trò chuyện luôn bỏ qua xác nhận đã đọc

## Câu hỏi thường gặp về WhatsApp: gửi tin nhắn + ghé nối

**Câu hỏi**: OpenClaw có gửi tin nhắn cho người liên hệ ngẫu nhiên khi tôi liên kết WhatsApp không?

**Trả lời**: Không. Chính sách DM mặc định là ghé nối, vì vậy người gửi chưa biết chỉ nhận được mã ghé nối và tin nhắn của họ không được xử lý. OpenClaw chỉ phản hồi các cuộc trò chuyện mà nó nhận được, hoặc các tin nhắn gửi mà bạn kích hoạt rõ ràng (tác nhân/CLI).

**Câu hỏi**: Ghé nối hoạt động như thế nào trên WhatsApp?

**Trả lời**: Ghé nối là cổng truy cập DM cho người gửi chưa biết:
- DM đầu tiên từ người gửi mới trả về mã ngắn (tin nhắn không được xử lý)
- Chấp thuận với: `openclaw pairing approve whatsapp` (liệt kê với `openclaw pairing list whatsapp`)
- Mã hết hạn sau 1 giờ; yêu cầu đang chờ bị giới hạn ở 3 mỗi kênh

**Câu hỏi**: Nhiều người có thể sử dụng các phiên OpenClaw khác nhau trên một số WhatsApp không?

**Trả lời**: Có, bằng cách định tuyến mỗi người gửi đến một tác nhân khác nhau thông qua ràng buộc (binding) (loại peer: "dm", người gửi E.164 như +15551234567). Phản hồi vẫn đến từ cùng tài khoản WhatsApp, và trò chuyện trực tiếp sụp đổ thành phiên chính của mỗi tác nhân, vì vậy hãy sử dụng một tác nhân mỗi người. Kiểm soát truy cập DM (dmPolicy/allowFrom) là toàn cục mỗi tài khoản WhatsApp. Xem [Định tuyến Đa Tác Nhân](../concepts/multi-agent.md).

**Câu hỏi**: Tại sao bạn hỏi số điện thoại của tôi trong trình hướng dẫn?

**Trả lời**: Trình hướng dẫn sử dụng nó để thiết lập danh sách cho phép/sở hữu của bạn để các DM của bạn được phép. Nó không được sử dụng để gửi tự động. Nếu bạn chạy trên số WhatsApp cá nhân của mình, hãy sử dụng cùng số đó và bật `channels.whatsapp.selfChatMode`.

## Chuẩn hóa tin nhắn (những gì mô hình thấy)

- Nội dung là nội dung tin nhắn hiện tại với bao bì
- Ngữ cảnh phản hồi trích dẫn luôn được đính kèm:
```
[Đang phản hồi +1555 id:ABC123]
>
[/Đang phản hồi]
```

- Siêu dữ liệu phản hồi cũng được đặt:
  - ReplyToId = stanzaId
  - ReplyToBody = nội dung trích dẫn hoặc trình giữ chỗ phương tiện
  - ReplyToSender = E.164 khi đã biết
- Tin nhắn chỉ có phương tiện đến sử dụng trình giữ chỗ

## Nhóm

- Nhóm ánh xạ đến phiên `agent::whatsapp:group:`.
- Chính sách nhóm: `channels.whatsapp.groupPolicy` = open|disabled|allowlist (mặc định allowlist)
- Chế độ kích hoạt:
  - mention (mặc định): yêu cầu @đề cập hoặc khớp regex
  - always: luôn kích hoạt
  - `/activation mention|always` là chỉ chủ sở hữu và phải được gửi dưới dạng tin nhắn độc lập
- Chủ sở hữu = `channels.whatsapp.allowFrom` (hoặc tự E.164 nếu chưa đặt)
- Tiêm lịch sử (chỉ đang chờ xử lý): 
  - Tin nhắn chưa xử lý gần đây (mặc định 50) được chèn dưới:
  - [Tin nhắn trò chuyện kể từ phản hồi cuối cùng của bạn - để có ngữ cảnh] (tin nhắn đã có trong phiên không được chèn lại)
  - Tin nhắn hiện tại dưới:
  - [Tin nhắn hiện tại - phản hồi cái này]
  - Hậu tố người gửi được thêm vào: [từ: Tên (+E164)]
  - Siêu dữ liệu nhóm được lưu vào cache 5 phút (chủ đề + người tham gia)

## Gửi phản hồi (luồng)

- WhatsApp Web gửi tin nhắn tiêu chuẩn (không có luồng phản hồi trích dẫn trong gateway hiện tại)
- Thẻ phản hồi bị bỏ qua trên kênh này

## Phản ứng xác nhận (tự động phản ứng khi nhận)

WhatsApp có thể tự động gửi phản ứng emoji cho tin nhắn đến ngay khi nhận, trước khi bot tạo phản hồi. Điều này cung cấp phản hồi ngay lập tức cho người dùng rằng tin nhắn của họ đã được nhận.

Cấu hình:
```json
{
  "whatsapp": {
    "ackReaction": {
      "emoji": "👀",
      "direct": true,
      "group": "mentions"
    }
  }
}
```

Tùy chọn:
- emoji (chuỗi): Emoji để sử dụng cho xác nhận (ví dụ: "👀", "✅", "📨"). Trống hoặc chưa đặt = tính năng bị tắt
- direct (boolean, mặc định: true): Gửi phản ứng trong trò chuyện trực tiếp/DM
- group (chuỗi, mặc định: "mentions"): Hành vi trò chuyện nhóm:
  - "always": Phản ứng với tất cả tin nhắn nhóm (kể cả không @đề cập)
  - "mentions": Chỉ phản ứng khi bot được @đề cập
  - "never": Không bao giờ phản ứng trong nhóm

Ghi đè theo tài khoản:
```json
{
  "whatsapp": {
    "accounts": {
      "work": {
        "ackReaction": {
          "emoji": "✅",
          "direct": false,
          "group": "always"
        }
      }
    }
  }
}
```

Ghi chú hành vi:
- Phản ứng được gửi ngay khi nhận tin nhắn, trước khi chỉ báo đang gõ hoặc phản hồi bot
- Trong nhóm với requireMention: false (activation: always), group: "mentions" sẽ phản ứng với tất cả tin nhắn (không chỉ @đề cập)
- Gửi và quên: lỗi phản ứng được ghi nhật ký nhưng không ngăn bot phản hồi
- ID người tham gia được bao gồm tự động cho phản ứng nhóm
- WhatsApp bỏ qua messages.ackReaction; sử dụng channels.whatsapp.ackReaction thay thế

## Công cụ tác nhân (phản ứng)

- Công cụ: whatsapp với hành động react (chatJid, messageId, emoji, tùy chọn remove)
- Tùy chọn: participant (người gửi nhóm), fromMe (phản ứng với tin nhắn của bạn), accountId (nhiều tài khoản)
- Ngữ nghĩa xóa phản ứng: xem [/tools/reactions](../tools/reactions.md)
- Kiểm soát công cụ: channels.whatsapp.actions.reactions (mặc định: được bật)

## Giới hạn

- Văn bản gửi đi được chia nhỏ đến channels.whatsapp.textChunkLimit (mặc định 4000)
- Chia nhỏ theo dòng mới tùy chọn: đặt channels.whatsapp.chunkMode="newline" để chia theo dòng trống (ranh giới đoạn) trước khi chia theo độ dài
- Lưu phương tiện đến bị giới hạn bởi channels.whatsapp.mediaMaxMb (mặc định 50 MB)
- Mục phương tiện gửi đi bị giới hạn bởi agents.defaults.mediaMaxMb (mặc định 5 MB)

## Gửi đi (văn bản + phương tiện)

- Sử dụng trình lắng nghe web hoạt động; lỗi nếu gateway không chạy
- Chia nhỏ văn bản: 4k tối đa mỗi tin nhắn (có thể cấu hình qua channels.whatsapp.textChunkLimit, tùy chọn channels.whatsapp.chunkMode)
- Phương tiện:
  - Hỗ trợ hình ảnh/video/âm thanh/tài liệu
  - Âm thanh được gửi dưới dạng PTT; audio/ogg => audio/ogg; codecs=opus
  - Phụ đề chỉ trên mục phương tiện đầu tiên
  - Hỗ trợ tìm nạp phương tiện HTTP(S) và đường dẫn cục bộ
  - GIF động: WhatsApp mong đợi MP4 với gifPlayback: true cho vòng lặp nội tuyến
  - CLI: openclaw message send --media --gif-playback
  - Gateway: gửi tham số bao gồm gifPlayback: true

## Ghi chú giọng nói (PTT âm thanh)

WhatsApp gửi âm thanh dưới dạng ghi chú giọng nói (bong bóng PTT).

- Kết quả tốt nhất: OGG/Opus. OpenClaw viết lại audio/ogg thành audio/ogg; codecs=opus
- [[audio_as_voice]] bị bỏ qua cho WhatsApp (âm thanh đã được gửi dưới dạng ghi chú giọng nói)
- Giới hạn gửi đi mặc định: 5 MB (mỗi mục phương tiện)
- Ghi đè: agents.defaults.mediaMaxMb
- Hình ảnh được tự động tối ưu thành JPEG dưới giới hạn (thay đổi kích thước + quét chất lượng)
- Phương tiện quá lớn => lỗi; phản hồi phương tiện quay lại cảnh báo văn bản

## Nhịp tim

- Nhật ký nhịp tim gateway kiểm tra sức khỏe kết nối (web.heartbeatSeconds, mặc định 60s)
- Nhịp tim tác nhân có thể được cấu hình mỗi tác nhân (agents.list[].heartbeat) hoặc toàn cục
qua agents.defaults.heartbeat (dự phòng khi không có mục nào theo tác nhân được đặt)

Sử dụng lời nhắc nhịp tim được cấu hình (mặc định: Đọc HEARTBEAT.md nếu nó tồn tại (ngữ cảnh không gian làm việc). Làm theo nó một cách nghiêm ngặt. Đừng suy luận hoặc lặp lại các nhiệm vụ cũ từ cuộc trò chuyện trước. Nếu không cần chú ý gì, phản hồi HEARTBEAT_OK.) + hành vi bỏ qua HEARTBEAT_OK.

- Giao hàng mặc định đến kênh đã sử dụng cuối cùng (hoặc đích được cấu hình)

## Hành vi kết nối lại

- Chính sách lùi: web.reconnect:
  - initialMs, maxMs, factor, jitter, maxAttempts
- Nếu đạt maxAttempts, giám sát web dừng (giảm cấp)
- Đăng xuất => dừng và yêu cầu liên kết lại

## Bản đồ cấu hình nhanh

- channels.whatsapp.dmPolicy (chính sách DM: ghé nối/danh sách cho phép/mở/bị tắt)
- channels.whatsapp.selfChatMode (thiết lập số điện thoại giống nhau; bot sử dụng số WhatsApp cá nhân của bạn)
- channels.whatsapp.allowFrom (danh sách cho phép DM). WhatsApp sử dụng số điện thoại E.164 (không có tên người dùng)
- channels.whatsapp.mediaMaxMb (giới hạn lưu phương tiện đến)
- channels.whatsapp.ackReaction (phản ứng tự động khi nhận tin nhắn: {emoji, direct, group})
- channels.whatsapp.accounts..* (cài đặt theo tài khoản + tùy chọn authDir)
- channels.whatsapp.accounts..mediaMaxMb (giới hạn phương tiện đến theo tài khoản)
- channels.whatsapp.accounts..ackReaction (ghi đè phản ứng xác nhận theo tài khoản)
- channels.whatsapp.groupAllowFrom (danh sách cho phép người gửi nhóm)
- channels.whatsapp.groupPolicy (chính sách nhóm)
- channels.whatsapp.historyLimit / channels.whatsapp.accounts..historyLimit (ngữ cảnh lịch sử nhóm; 0 tắt)
- channels.whatsapp.dmHistoryLimit (giới hạn lịch sử DM theo người dùng). Ghi đè theo người dùng: channels.whatsapp.dms[""].historyLimit
- channels.whatsapp.groups (danh sách cho phép nhóm + cổng đề cập mặc định; sử dụng "*" để cho phép tất cả)
- channels.whatsapp.actions.reactions (cổng công cụ phản ứng WhatsApp)
- agents.list[].groupChat.mentionPatterns (hoặc messages.groupChat.mentionPatterns)
- messages.groupChat.historyLimit
- channels.whatsapp.messagePrefix (tiền tố đến; theo tài khoản: channels.whatsapp.accounts..messagePrefix; lỗi thời: messages.messagePrefix)
- messages.responsePrefix (tiền tố gửi đi)
- agents.defaults.mediaMaxMb
- agents.defaults.heartbeat.every
- agents.defaults.heartbeat.model (ghi đè tùy chọn)
- agents.defaults.heartbeat.target
- agents.defaults.heartbeat.to
- agents.defaults.heartbeat.session
- agents.list[].heartbeat.* (ghi đè theo tác nhân)
- session.* (phạm vi, nghỉ, lưu trữ, mainKey)
- web.enabled (tắt khởi động kênh khi sai)
- web.heartbeatSeconds
- web.reconnect.*

## Nhật ký + gỡ lỗi

- Hệ thống con: whatsapp/inbound, whatsapp/outbound, web-heartbeat, web-reconnect
- Tệp nhật ký: /tmp/openclaw/openclaw-YYYY-MM-DD.log (có thể cấu hình)
- Hướng dẫn gỡ lỗi: [Gateway troubleshooting](../gateway/troubleshooting.md)

## Gỡ lỗi (nhanh)

### Chưa được liên kết / yêu cầu đăng nhập QR

- Triệu chứng: channels status hiển thị linked: false hoặc cảnh báo "Not linked"
- Sửa: chạy openclaw channels login trên máy chủ gateway và quét mã QR (WhatsApp → Cài đặt → Thiết Bị Đã Kết Nối)

### Được liên kết nhưng bị ngắt kết nối / vòng lặp kết nối lại

- Triệu chứng: channels status hiển thị đang chạy, bị ngắt kết nối hoặc cảnh báo "Linked but disconnected"
- Sửa: openclaw doctor (hoặc khởi động lại gateway). Nếu tiếp tục, liên kết lại qua channels login và kiểm tra openclaw logs --follow

### Runtime Bun

- Bun không được khuyến nghị. WhatsApp (Baileys) và Telegram không đáng tin cậy trên Bun.
Chạy gateway với Node. (Xem ghi chú runtime trong Bắt Đầu.)

---

## Gợi ý cho người mới

💡 **Lưu ý quan trọng**: Khi thiết lập WhatsApp, hãy chắc chắn rằng bạn sử dụng số điện thoại thật, không phải số ảo hoặc VoIP vì WhatsApp thường chặn các loại số này.

💡 **Bảo mật**: Sử dụng chính sách ghé nối (pairing) hoặc danh sách cho phép (allowlist) để kiểm soát ai có thể tương tác với bot của bạn.

💡 **Hiệu suất**: Nếu bạn có kế hoạch sử dụng cho nhiều người, hãy cân nhắc thiết lập nhiều tác nhân để cách ly phiên làm việc.