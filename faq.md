---
layout: page
title: Câu Hỏi Thường Gặp
permalink: /faq/
---

# Câu Hỏi Thường Gặp (FAQ) - OpenClaw Tiếng Việt

## Tổng Quan

### OpenClaw là gì?

OpenClaw là một nền tảng gateway cho phép các tác nhân AI (AI agents) tương tác với thế giới thông qua nhiều kênh truyền thông như WhatsApp, Telegram, Discord, và iMessage. Nó không chỉ là một công cụ chatbot đơn thuần mà là một hệ thống hoàn chỉnh giúp AI thực hiện các tác vụ thực tế trên máy tính và tương tác với các dịch vụ bên ngoài.

### OpenClaw khác gì so với các chatbot thông thường?

Khác biệt lớn nhất là OpenClaw không chỉ trả lời câu hỏi mà còn có thể:
- Thực hiện tác vụ trên máy tính (đọc/gửi email, quản lý tệp tin, chạy ứng dụng)
- Tương tác với các dịch vụ web (tìm kiếm, đăng nhập, xử lý dữ liệu)
- Kết nối với nhiều kênh truyền thông cùng lúc
- Tự động hóa quy trình phức tạp

### Ai nên sử dụng OpenClaw?

- Người muốn xây dựng trợ lý AI cá nhân mạnh mẽ
- Lập trình viên muốn tích hợp AI vào hệ thống của mình
- Doanh nghiệp muốn tự động hóa quy trình
- Nhà nghiên cứu muốn thử nghiệm với AI agents
- Bất kỳ ai quan tâm đến công nghệ AI và tự động hóa

## Cài Đặt & Cấu Hình

### Yêu cầu hệ thống để chạy OpenClaw là gì?

- **Hệ điều hành**: Linux, macOS, hoặc Windows (thông qua WSL2)
- **Node.js**: Phiên bản 22 trở lên
- **pnpm**: Được khuyến nghị để quản lý gói
- **RAM**: Tối thiểu 4GB (khuyến nghị 8GB trở lên)
- **Dung lượng đĩa**: 1GB trở lên

### Có thể cài OpenClaw trên Windows không?

Có thể, nhưng được khuyến nghị sử dụng WSL2 (Windows Subsystem for Linux) để có trải nghiệm tốt nhất. WSL2 cung cấp môi trường Linux chạy trên Windows, giúp OpenClaw hoạt động ổn định hơn.

### Tôi cần tài khoản gì để sử dụng OpenClaw?

Bạn cần tài khoản từ các nhà cung cấp mô hình AI như:
- **OpenAI**: Để sử dụng GPT
- **Anthropic**: Để sử dụng Claude
- **Các nhà cung cấp khác**: Tùy theo mô hình bạn muốn sử dụng

Ngoài ra, nếu bạn muốn kết nối với các kênh như Telegram hoặc Discord, bạn cần tạo bot trên các nền tảng đó.

## Kênh Truyền Thông

### Tôi có thể kết nối OpenClaw với những kênh nào?

OpenClaw hỗ trợ nhiều kênh truyền thông:
- **WhatsApp**: Qua giao thức WhatsApp Web
- **Telegram**: Qua Bot API
- **Discord**: Qua Bot API
- **iMessage**: Trên macOS
- **Mattermost**: Qua Bot API
- **Signal**: Qua signal-cli
- **Google Chat**: Qua API
- Và nhiều kênh khác thông qua plugin

### Kết nối WhatsApp có an toàn không?

OpenClaw sử dụng thư viện Baileys để kết nối với WhatsApp Web, giống như cách bạn sử dụng WhatsApp Web trên trình duyệt. Tuy nhiên, bạn nên:
- Sử dụng số điện thoại riêng cho OpenClaw
- Cấu hình chính sách bảo mật phù hợp (ghé nối/danh sách cho phép)
- Không chia sẻ số điện thoại OpenClaw với người không đáng tin cậy

## Bảo Mật

### Làm thế nào để bảo vệ OpenClaw khỏi truy cập trái phép?

OpenClaw có nhiều lớp bảo mật:
- **Mã token**: Sử dụng mã token để xác thực kết nối
- **Danh sách cho phép**: Chỉ người trong danh sách mới được tương tác
- **Chế độ ghé nối**: Người chưa biết cần được xác nhận trước khi tương tác
- **Mô phỏng (Sandbox)**: Chạy các tác vụ trong môi trường an toàn
- **Phân quyền công cụ**: Giới hạn hành động của tác nhân AI

### Tác nhân AI có thể làm hại hệ thống của tôi không?

Không nếu bạn cấu hình đúng cách. OpenClaw có hệ thống bảo mật mạnh mẽ:
- Các công cụ nguy hiểm được giới hạn quyền
- Có thể cấu hình mô phỏng để cách ly tác nhân
- Tất cả hành động đều được ghi nhật ký
- Có thể thiết lập chính sách phân quyền chi tiết

## Sử Dụng Thực Tế

### Tôi có thể làm gì với OpenClaw?

Các khả năng phổ biến bao gồm:
- **Tự động hóa công việc**: Kiểm tra email, xử lý tệp tin, lập lịch
- **Tìm kiếm thông tin**: Truy vấn web, tổng hợp dữ liệu
- **Quản lý dự án**: Theo dõi tiến độ, nhắc nhở, báo cáo
- **Hỗ trợ khách hàng**: Trả lời câu hỏi, xử lý yêu cầu
- **Phân tích dữ liệu**: Đọc báo cáo, phân tích xu hướng
- **Tích hợp hệ thống**: Kết nối các dịch vụ khác nhau

### Có thể chạy nhiều tác nhân AI cùng lúc không?

Có thể! OpenClaw hỗ trợ đa tác nhân, cho phép bạn:
- Chạy nhiều tác nhân riêng biệt với mục đích khác nhau
- Cô lập phiên làm việc giữa các tác nhân
- Gán các kênh khác nhau cho từng tác nhân
- Sử dụng mô hình và cấu hình khác nhau cho mỗi tác nhân

## Vấn Đề Thường Gặp

### Gateway bị ngắt kết nối thường xuyên

Đây là vấn đề phổ biến với kết nối kênh như WhatsApp hoặc Telegram:
- Kiểm tra kết nối internet ổn định
- Đảm bảo phiên gateway vẫn đang chạy
- Có thể cấu hình lại chính sách kết nối lại trong tệp cấu hình
- Kiểm tra nhật ký để biết nguyên nhân cụ thể

### Tác nhân AI không phản hồi

Các nguyên nhân phổ biến:
- Chưa cấu hình xác thực (API key, OAuth)
- Mô hình ngôn ngữ không khả dụng
- Tác nhân bị giới hạn quyền truy cập
- Lỗi kết nối gateway

### Hiệu suất chậm

Cách cải thiện hiệu suất:
- Sử dụng mô hình nhanh hơn (ví dụ: GPT-3.5 thay cho GPT-4)
- Tối ưu hóa tệp cấu hình
- Kiểm tra tài nguyên hệ thống (RAM, CPU)
- Giảm số lượng công cụ đồng thời

## Phát Triển & Mở Rộng

### Tôi có thể tạo kỹ năng riêng không?

Có thể! OpenClaw hỗ trợ tạo kỹ năng tùy chỉnh:
- Viết mã để thực hiện chức năng chuyên biệt
- Đóng gói thành kỹ năng tái sử dụng
- Chia sẻ với cộng đồng
- Tích hợp với các dịch vụ bên ngoài

### Có thể tích hợp với dịch vụ của tôi không?

Rất có thể! OpenClaw được thiết kế để tích hợp:
- Sử dụng công cụ exec để chạy script hệ thống
- Sử dụng công cụ web_fetch để gọi API
- Viết kỹ năng tùy chỉnh để kết nối với dịch vụ
- Sử dụng webhook để phản ứng với sự kiện

## Hỗ Trợ & Cộng Đồng

### Tôi có thể nhận hỗ trợ ở đâu?

- **Tài liệu chính thức**: docs.openclaw.ai
- **GitHub**: Issues và Discussions
- **Cộng đồng người dùng**: Các nhóm và diễn đàn liên quan
- **Cộng đồng tiếng Việt**: Dự án tài liệu này và các kênh liên quan

### Tôi có thể đóng góp cho dự án không?

Hoàn toàn có thể! Bạn có thể:
- Báo cáo lỗi và vấn đề
- Góp ý cải thiện tài liệu
- Viết mã và gửi pull request
- Dịch tài liệu sang ngôn ngữ khác
- Viết hướng dẫn và ví dụ thực tế

---

## Câu Hỏi Khác?

Nếu bạn không tìm thấy câu trả lời cho câu hỏi của mình, vui lòng:
- [Tạo issue trên GitHub](https://github.com/yourusername/openclaw-docs-vi/issues)
- Kiểm tra tài liệu chính thức tại [docs.openclaw.ai](https://docs.openclaw.ai)
- Tham gia cộng đồng thảo luận

💡 **Lưu ý**: Đây là tài liệu FAQ, không phải tài liệu tham khảo đầy đủ. Để biết thông tin chi tiết, vui lòng tham khảo các phần tương ứng trong tài liệu.