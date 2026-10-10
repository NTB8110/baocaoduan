# BÁO CÁO THỰC HÀNH CÁ NHÂN
## Vận dụng AI Agent, kiểm soát code và kiểm thử phần mềm
- **Dự án:** Hệ thống quản lý nhà trọ (QuanLyNhaTro)
- **Nhánh Git:** `binh`
- **Phạm vi:** Phòng trọ, Tiện nghi, Sự cố và Thông báo
## Ý 1. Vận dụng AI Agent
- **Xác định yêu cầu:** Chủ động đưa ra ý tưởng và chức năng cần triển khai, sau đó trao đổi với AI Copilot để làm rõ yêu cầu và xây dựng prompt chi tiết.
- **Kiểm duyệt prompt:** Kiểm tra các quy tắc, phạm vi tệp được phép chỉnh sửa và yêu cầu nghiệp vụ; bổ sung hoặc yêu cầu AI chỉnh sửa nếu prompt chưa hợp lý.
- **Triển khai có kiểm soát:** Chỉ cho phép Agent thực hiện khi prompt đáp ứng yêu cầu, đồng thời hạn chế thay đổi đến các module không liên quan.
- **Ví dụ 1:** Khi phát triển module Phòng trọ, yêu cầu giữ nguyên giao diện đã thiết kế, đồng thời triển khai các chức năng thêm, sửa, xóa và thay đổi trạng thái phòng.
## Ý 2. Kiểm soát code
### a. Tìm hiểu và chỉnh sửa code
- Phân chia code thành các thành phần phù hợp như `pages`, `components`, `services`, `types` và dữ liệu mẫu để dễ quản lý.
- **Ví dụ:** Tách kiểu dữ liệu `TenantNotification` khỏi trang hiển thị thông báo và các component popup để code rõ ràng, dễ bảo trì.
### b. Tìm hiểu và sử dụng Skills
- Tìm hiểu vai trò của Skills trong việc hướng dẫn AI Agent thực hiện nhiệm vụ theo quy trình và quy tắc cụ thể.
- Hiện chưa triển khai Skills thực tế trong dự án; cần tiếp tục tìm hiểu cách cài đặt, lựa chọn và áp dụng Skill phù hợp.
- **Hướng áp dụng:** Sử dụng Skills để hỗ trợ đọc hiểu cấu trúc dự án, tuân thủ quy ước viết code và kiểm tra những thay đổi do Agent tạo ra.
- Khi áp dụng thực tế, cần kiểm tra kết quả của Skill và xác minh code thay đổi thay vì mặc định mọi đề xuất của AI đều chính xác.
### c. Kiểm soát code bằng Git và đánh giá công việc
- Sử dụng `git status` để kiểm tra trạng thái tệp, `git diff` để xem nội dung chỉnh sửa và `git log` để xem lịch sử commit.
- Kiểm tra thay đổi trước và sau khi Agent thực hiện nhằm phát hiện các tệp bị sửa ngoài phạm vi.
- **Ví dụ:** Trên nhánh `binh`, xem diff sau khi chỉnh sửa module Thông báo để xác định các thay đổi có đúng yêu cầu hay không.
- Đánh giá công việc của các thành viên dựa trên mức độ hoàn thành yêu cầu, chất lượng code, kết quả kiểm thử và tiến độ, không chỉ dựa vào số dòng code hoặc số commit.
## Ý 3. Kiểm thử phần mềm
### Ý tưởng kiểm thử
- **Kiểm tra chức năng:** Chạy thử các thao tác và đối chiếu kết quả với yêu cầu ban đầu.
- **Kiểm tra dữ liệu:** Thử dữ liệu hợp lệ, dữ liệu thiếu hoặc sai để xác minh khả năng xử lý lỗi.
- **Kiểm tra kết nối:** Kiểm tra dữ liệu API trả về và cách giao diện xử lý khi backend gặp lỗi.
- **Kiểm thử hồi quy:** Kiểm tra các chức năng liên quan sau khi chỉnh sửa để hạn chế lỗi phát sinh.
- **Xử lý lỗi:** Khi phát hiện lỗi, cung cấp thông tin cụ thể cho AI để phân tích nguyên nhân, chỉnh sửa đúng vị trí và kiểm tra lại.
- Chỉ xác nhận chức năng hoàn thành sau khi đã kiểm tra kết quả thực tế; build thành công không đồng nghĩa với toàn bộ chức năng hoạt động chính xác.
## Kết luận
- Vận dụng AI Copilot và AI Agent để hỗ trợ phân tích yêu cầu, xây dựng prompt và phát triển chức năng.
- Chủ động kiểm duyệt prompt, kiểm soát phạm vi chỉnh sửa và sử dụng Git để bảo vệ code của dự án nhóm.
- Tìm hiểu Skills để tiếp tục nâng cao hiệu quả sử dụng Agent.
- Kết hợp kiểm thử chức năng và kiểm tra code nhằm phát hiện lỗi, nâng cao chất lượng phần mềm và hạn chế ảnh hưởng đến các module khác.