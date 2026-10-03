# Báo cáo ngày 04/10

## 1\. Thông tin cá nhân

* Họ và tên: Nguyễn Thị Bình
* Vai trò: Developer
* Branch Git: `binh`
* Dự án: QuanLyNhaTro

### Phạm vi công việc

Tôi phụ trách các module:

* Quản lý Phòng trọ
* Tiện nghi
* Sự cố
* Thông báo

Theo đặc tả dự án, phần công việc của tôi liên quan đến các bảng
`rooms`, `room\_types`, `amenities`, `room\_amenities`,
`maintenance\_requests` và `notifications`.

\---

# 2\. Xây dựng hệ thống với sự trợ giúp của AI Agent

## 2.1. Công cụ sử dụng

Trong quá trình phát triển, tôi sử dụng:

* Figma để thiết kế và tham khảo giao diện.
* Figma Make để hỗ trợ tạo và chỉnh sửa code bằng AI Agent.
* VS Code/code editor để kiểm tra và chỉnh sửa source code.
* Git và GitHub để quản lý source code và theo dõi quá trình phát
triển.

Tech stack của project gồm ReactJS + TypeScript / HTML5, CSS3, JS + Bootstrap / Tailwind CSS ở frontend; Node.js/Express
ở backend và MySQL ở database.

## 2.2. Quy trình làm việc với AI Agent

Tôi không sử dụng AI Agent theo cách yêu cầu AI tạo toàn bộ project rồi
nhận kết quả cuối cùng. Tôi chia công việc thành từng module và từng
giai đoạn để dễ kiểm soát.

Quy trình hiện tại:


Đặc tả nghiệp vụ
       ↓
Thiết kế Figma
       ↓
Phân tích chức năng
       ↓
Viết prompt cho AI Agent
       ↓
Agent tạo/chỉnh sửa code
       ↓
Tôi đọc và kiểm tra code
       ↓
Chạy chương trình
       ↓
Kiểm tra giao diện + chức năng
       ↓
Phát hiện lỗi
       ↓
Yêu cầu Agent sửa đúng phạm vi
       ↓
Kiểm tra lại
       ↓
Commit / Push

## 2.3. Cách tôi kiểm soát Agent

Khi yêu cầu Agent làm một module, tôi xác định rõ:

* Module nào được phép sửa.
* File nào có thể tạo hoặc chỉnh sửa.
* Chức năng nào cần triển khai.
* Chức năng nào không được thêm.
* Không được sửa module của thành viên khác.
* Không được tự ý thay đổi framework hoặc cấu trúc project nếu chưa
yêu cầu.

Ví dụ khi chỉnh Module Sự cố, tôi yêu cầu Agent chỉ sửa Module Sự cố,
không sửa Phòng trọ, Tiện nghi hoặc Thông báo.

## 2.4. Chia nhỏ chức năng

Module Phòng trọ được chia thành các phase:

### Phase 1 Danh sách

* Danh sách phòng.
* Menu thao tác.
* Empty state.

### Phase 2 CRUD và trạng thái

* Thêm phòng.
* Sửa phòng.
* Xem chi tiết.
* Thay đổi trạng thái.
* Cảnh báo thay đổi trạng thái.
* Xóa phòng.
* Cảnh báo xóa.

### Phase 3 Tiện nghi

* Danh sách tiện nghi.
* Sửa tiện nghi.
* Xóa tiện nghi.
* Gán tiện nghi cho phòng.
* Thêm tiện nghi.
* Cảnh báo xóa.

Việc chia phase giúp hạn chế Agent thay đổi quá nhiều code trong một lần
và dễ xác định lỗi nếu có vấn đề.

# 3\. Kỹ năng kiểm soát code

## 3.1. Kiểm soát tính năng

### Module Phòng trọ

Các chức năng tôi đã triển khai ở frontend gồm:

* Xem danh sách phòng.
* Lọc danh sách.
* Thêm phòng.
* Sửa phòng.
* Xem chi tiết phòng.
* Thay đổi trạng thái phòng.
* Xóa phòng.
* Quản lý tiện nghi.

Khi có lỗi ở một chức năng, tôi phải xác định được:


Màn hình
   ↓
Page
   ↓
Component
   ↓
State
   ↓
Event handler / function
   ↓
Logic xử lý

Ví dụ nếu cần thay đổi validation của chức năng thêm phòng, tôi phải tìm
được component xử lý form ADD, phần state của form và phần xử lý submit,
thay vì yêu cầu Agent sửa toàn bộ module.

### Quy tắc nghiệp vụ đã kiểm soát

Đối với Phòng trọ, tôi đã xác định rõ một số quy tắc:

* Phòng mới được thêm vào cuối danh sách.
* Không tự động sort lại danh sách.
* Sau CRUD vẫn giữ filter hiện tại nếu filter còn hợp lệ.
* Form ADD/EDIT phải kiểm tra trường bắt buộc.
* Trường số phải là số hợp lệ và không âm khi nghiệp vụ không cho phép
âm.
* Khi validation lỗi phải giữ lại dữ liệu người dùng nhập.
* Modal phải được căn giữa viewport.
* Dropdown phải nằm ngay dưới field tương ứng, không bung ra cuối màn
hình.

### Module Sự cố

Theo đặc tả:


Người thuê
   ↓
Gửi yêu cầu báo hỏng
   ↓
maintenance\_requests
   ↓
Chủ trọ nhận yêu cầu
   ↓
Xem chi tiết
   ↓
Cập nhật trạng thái
   ↓
Ghi nhận chi phí sửa chữa


Các trạng thái sự cố:

* `TIEP\_NHAN`
* `DANG\_XU\_LY`
* `HOAN\_THANH`

Đặc tả dự án xác định người thuê tạo yêu cầu sửa chữa, còn chủ trọ cập
nhật tiến độ xử lý và ghi nhận chi phí.

### Module Thông báo

Chủ trọ có thể gửi thông báo:

* Cho toàn hệ thống.
* Cho một người dùng cụ thể.

Tôi cũng triển khai luồng xóa thông báo có bước xác nhận:


Xóa
 ↓
Popup xác nhận
 ├── Hủy → giữ nguyên
 └── Xác nhận → xóa


### Quản lý cấu trúc code

Trong quá trình sử dụng Figma Make, tôi kiểm tra cấu trúc thư mục để đảm
bảo code của mình thống nhất với project.

Các module của tôi được tổ chức theo `pages`, ví dụ:


src/
└── pages/
    ├── Issues/
    │   └── IssuesPage.tsx
    ├── Notifications/
    │   └── NotificationPage.tsx
    └── Rooms/
        ├── components/
        └── RoomPage.tsx


Khi refactor cấu trúc, tôi phải kiểm tra lại các import path và đảm bảo
không tạo hai phiên bản của cùng một module.

Mục tiêu là thay đổi cấu trúc nhưng không làm thay đổi logic nghiệp vụ.



# 3.2. Kỹ năng sử dụng skill và công cụ hỗ trợ

Tôi đang làm quen với cách kết hợp AI Agent với các skill/công cụ hỗ trợ
viết code.

Các công cụ tôi đã sử dụng trong quá trình hiện tại:

* Figma
* Figma Make
* Git
* GitHub
* VS Code/code editor

Figma Make được sử dụng để:

* Chuyển thiết kế thành giao diện React.
* Tạo component.
* Chỉnh sửa component.
* Refactor code.
* Sửa lỗi dropdown.
* Sửa lỗi modal.
* Căn chỉnh layout.
* Hỗ trợ kiểm tra và thay đổi cấu trúc code.

# 3.3. Git Log, Git Diff và kiểm soát hiệu quả làm việc

## a. Git Log

Tôi sử dụng Git Log để xem lịch sử thay đổi:

``` bash
git log --oneline
```

Thông qua log có thể biết:

* Thành viên commit khi nào.
* Commit nào được thực hiện trước/sau.
* Nội dung công việc được mô tả trong commit.
* Quá trình phát triển có diễn ra liên tục hay không.

## b. Git Diff

Tôi chưa sử dụng git diff nhưng theo những gì đã tìm hiểu :

``` bash
git diff
```

để kiểm tra các thay đổi trước khi commit.

Các nội dung cần kiểm tra:

* File nào đã thay đổi?
* Những dòng code nào đã thay đổi?
* Có sửa nhầm module khác không?
* Có xóa code cũ ngoài yêu cầu không?
* Có thêm chức năng không được yêu cầu không?
* Thay đổi có đúng với task được giao không?

## c. Vai trò của Leader

Theo tôi, Leader không nên đánh giá hiệu quả thành viên chỉ dựa vào số
lượng commit.

Có thể đánh giá dựa trên các tiêu chí:

#### \- Tính liên tục

Thành viên có commit trong suốt quá trình phát triển hay chỉ đưa toàn bộ
source code lên ở cuối?

#### \- Nội dung commit

Commit có thể hiện đúng công việc được giao không?

#### \- Git Diff

Code thực tế có đúng với nội dung commit và task không?

#### \- Chất lượng chức năng

Chức năng có chạy đúng và đáp ứng yêu cầu không?

#### \- Không ảnh hưởng thành viên khác

Thành viên có vô tình sửa hoặc làm hỏng module của người khác không?

#### \- Khả năng giải thích code

Khi được hỏi:

> "Chức năng này nằm ở đâu?"

thành viên phải xác định được file, component, state và logic xử lý.

#### \- Khả năng sửa lỗi

Khi có bug, thành viên phải biết cách tìm nguyên nhân và sửa đúng vị
trí.

# 4. Kết hợp các công cụ test tính năng

Ở giai đoạn hiện tại, tôi đang thực hiện kiểm thử frontend theo quy
trình:


Viết code
   ↓
Chạy chương trình
   ↓
Thao tác trực tiếp
   ↓
Kiểm tra kết quả
   ↓
Kiểm tra trường hợp lỗi
   ↓
Sửa lỗi
   ↓
Chạy lại



Các nội dung đã kiểm tra gồm:

### Phòng trọ

* Thêm phòng.
* Sửa phòng.
* Xem chi tiết.
* Thay đổi trạng thái.
* Xóa phòng.
* Lọc phòng.
* Validation form.
* Gán tiện nghi.

### Sự cố

* Hiển thị danh sách.
* Lọc trạng thái.
* Xem chi tiết.
* Cập nhật trạng thái.
* Kiểm tra dropdown trạng thái.
* Kiểm tra dữ liệu sự cố.

### Thông báo

* Hiển thị danh sách.
* Gửi thông báo.
* Chọn người nhận.
* Gửi cho tất cả.
* Chọn người cụ thể.
* Xóa thông báo.
* Xác nhận trước khi xóa.

Giai đoạn tiếp theo tôi sẽ tiếp tục kết hợp kiểm thử frontend với API,
database và integration test.



# 5. Git và yêu cầu commit liên tục

Branch cá nhân của tôi: binh

Tôi sẽ duy trì việc commit liên tục trong quá trình phát triển thay vì
chỉ commit source code cuối cùng.

Mỗi commit nên thể hiện một thay đổi có ý nghĩa, ví dụ:
feat: quanlyphongtro
feat: quanlythongbao
feat: quanlysuco

Mục đích:

* Có lịch sử phát triển rõ ràng.
* Có thể kiểm tra từng thay đổi.
* Có thể quay lại phiên bản trước khi cần.
* Chứng minh quá trình thực hiện project.
* Giúp Leader kiểm tra công việc của từng thành viên.

# 6. Những kinh nghiệm rút ra

Qua quá trình sử dụng AI Agent, tôi nhận thấy AI giúp tăng tốc độ phát
triển nhưng không thay thế việc hiểu source code.

Tôi cần kiểm soát được:

* AI đã sửa file nào.
* Chức năng nằm ở đâu.
* Component nào xử lý chức năng.
* State được quản lý ở đâu.
* Logic xử lý nằm ở đâu.
* Thay đổi có đúng yêu cầu không.
* Có ảnh hưởng module khác không.
* Cách kiểm tra và sửa code khi Agent tạo sai.

Vì vậy, mục tiêu của tôi không chỉ là:

> "Dùng AI để viết code."

mà là:

> "Dùng AI để tăng tốc độ phát triển nhưng bản thân vẫn hiểu và kiểm soát được toàn bộ code mình phụ trách."



# 7. Tiến độ hiện tại

### Đã thực hiện

* Phân tích đặc tả module được giao.
* Thiết kế giao diện bằng Figma.
* Sử dụng Figma Make hỗ trợ viết frontend.
* Module Phòng trọ.
* Module Tiện nghi.
* Module Sự cố.
* Module Thông báo.
* Kiểm tra và sửa lỗi UI.
* Kiểm soát cấu trúc thư mục.
* Làm việc trên branch `binh`.
* Sử dụng Git Log để kiểm soát thay đổi.

### Tiếp tục thực hiện

* Hoàn thiện phần UI đối với người thuê
* Hoàn thiện kết nối Backend/API.
* Kiểm thử với database.
* Integration Test.
* Kiểm thử nâng cao.
* Tìm hiểu và áp dụng thêm skill hỗ trợ coding.
* Duy trì commit liên tục trên GitHub.

