---
module: M01
ten_module: Authentication & Account
ma_tai_lieu: FR-M01
phien_ban: 1.6
trang_thai: Đã chốt
ngay: 2026-10-23
tac_gia: Phạm Văn Đức
moc_nguon: DEC-247, QA-444, ISS-382, OPEN-012
steps_completed: [1, 2, 3, 4, 5, 6, 7]
---
# Tài liệu yêu cầu chức năng — M01 Authentication & Account

| Mã tài liệu | FR-M01 |
|---|---|
| Dự án | iShare |
| Module | M01 — Authentication & Account |
| Trạng thái | Đã chốt |
| Phiên bản | 1.6 |
| Ngày | 2026-10-23 |
| Tác giả | Phạm Văn Đức |

<!-- Quy ước chung cho mọi bảng dưới đây:
     - Thân tài liệu không ghi nguồn. Nguồn của mọi ID nằm ở Phụ lục A.
     - Ô không có nội dung ghi "—". Không xóa cột.
     - Mục chưa tới bước làm thì để dòng "(Chưa làm — bước N)". -->

## 1. Tổng quan

### 1.1 Mục đích

Module Authentication & Account giúp học sinh THPT tạo tài khoản iShare bằng email hoặc bằng tài khoản Google,
xác minh email, đăng nhập, đăng xuất và giữ phiên đăng nhập trên nhiều thiết bị, đổi hoặc lấy lại mật khẩu, và tự
vô hiệu hóa rồi xóa tài khoản của mình. Module cũng xác định hai thông tin định danh của mỗi người dùng: tên hiển thị
(display_name) và tên định danh duy nhất (username) dùng để nhắc tên người khác (@mention).

### 1.2 Phạm vi

**Trong phạm vi:**

- Đăng ký bằng email và mật khẩu theo ba bước: nhập email, mật khẩu kèm đồng ý Privacy Policy/ToS; xác minh email
  bằng magic link; thiết lập username, display_name và các thông tin tùy chọn (có thể bỏ qua).
- Đăng ký và đăng nhập bằng Google; tự liên kết với tài khoản đã đăng ký cùng email đã xác minh.
- Gửi lại email xác minh.
- Đăng nhập, đăng xuất; kiểm tra khi đăng nhập theo trạng thái tài khoản và mức xác minh, đưa người dùng về bước
  đăng ký còn dở; hành vi khi tài khoản đang bị khóa (BANNED) đăng nhập.
- Phiên đăng nhập: thời hạn, làm mới, đăng nhập đồng thời trên nhiều thiết bị.
- Đổi mật khẩu khi đã đăng nhập; quên mật khẩu bằng magic link; hành vi khi tài khoản Google dùng chức năng mật khẩu.
- Vô hiệu hóa tài khoản (cách duy nhất để xóa tài khoản), kích hoạt lại trong thời hạn, tự chuyển sang đã xóa sau
  thời hạn, xóa dữ liệu cá nhân khi đã xóa.
- Hiển thị bài viết, bình luận và tên tác giả của tài khoản đã vô hiệu hóa hoặc đã xóa.
- Vòng đời trạng thái tài khoản và mức xác minh.
- Định danh: username (duy nhất, quy tắc ký tự và độ dài) và display_name (tự do, không duy nhất).
- Hệ thống @mention: tìm người được nhắc, thứ tự ưu tiên kết quả, cách hiển thị, ghi nhận người được nhắc theo
  tài khoản, thời điểm gửi thông báo nhắc tên.
- Quy tắc mật khẩu; quy tắc username, display_name khi thiết lập và khi đổi ở trang sửa hồ sơ; giải phóng email và
  giữ username của tài khoản đã xóa.
- Mod, Admin xem bài viết bị ẩn và danh tính thật của tác giả đã vô hiệu hóa tài khoản.
- Hành vi đăng ký, đăng nhập khi bật công tắc tạm dừng đăng ký hoặc chế độ bảo trì; tài khoản tự hết ban tạm thời.
- Trang Privacy Policy/ToS: nội dung bắt buộc, đồng ý khi đăng ký (kèm cam kết cho người dưới 16 tuổi), lưu phiên bản đã
  đồng ý, đồng ý lại khi chính sách đổi phiên bản; danh mục dữ liệu bị xóa và được giữ khi tài khoản bị xóa.

**Ngoài phạm vi:**

- Trang hồ sơ, avatar, bio, Lớp/Khối trên hồ sơ — M02 User Profile. Bước 3 của đăng ký chỉ cho nhập hoặc bỏ qua
  các trường tùy chọn này.
- Chèn @mention trong trình soạn bài viết, bình luận — M03 Post & Content, M04 Comment. Tìm kiếm người dùng — M06 Search.
- Gửi thông báo và email (đổi mật khẩu, cảnh báo trước khi tự xóa, liên kết Google, được nhắc tên) — M07 Notification.
- Cảnh báo, ban, gỡ ban, thời hạn ban — M08 Moderation. Khiếu nại và hạn khiếu nại — M09 Appeal.
- Quản lý vai trò, tài khoản ADMIN gốc, công tắc tạm dừng đăng ký, chế độ bảo trì — M10 Admin Panel.
- Chuyển quyền Owner khi Owner bị vô hiệu hóa, bị xóa hoặc bị ban — M11 Group.
- Nhãn "Tài khoản đã bị khóa" và loại tài khoản BANNED khỏi bảng xếp hạng — M12 Gamification.
- Thống kê tài khoản theo trạng thái và lượt đăng ký mới — M15 Analytics & Stats.
- Hiển thị tin nhắn của tài khoản đã xóa — M16; nhật ký kiểm duyệt — M08; nhật ký AI — M13 (M01 đặt tên thay thế và cách
  liên kết qua username).
- Chức năng tải bản sao dữ liệu (không làm ở MS1) và email liên hệ trên trang chính sách — chốt khi triển khai.
- Hỏi tuổi hoặc xác nhận của phụ huynh khi đăng ký — không làm ở MS1, thay bằng cam kết trong ô đồng ý.
- Đã quyết là không làm: phân biệt tài khoản Giáo viên/Học sinh; nút xóa tài khoản trực tiếp không qua vô hiệu hóa;
  Admin, Mod xóa tài khoản người khác; đăng nhập qua nhà cung cấp khác ngoài Google; hiện lịch sử đổi username;
  sửa nhãn của một @mention đã chèn.

## 2. Thuật ngữ và viết tắt

### 2.1 Thuật ngữ

| Thuật ngữ | Định nghĩa |
|---|---|
| Tài khoản | Danh tính của một người dùng trong iShare. Chỉ có một loại tài khoản; không phân biệt Giáo viên/Học sinh. |
| Tài khoản email | Tài khoản được tạo bằng đăng ký email và mật khẩu. |
| Tài khoản Google | Tài khoản được tạo lần đầu bằng đăng nhập Google. Không có mật khẩu trong iShare. |
| Liên kết Google | Việc một tài khoản email được gắn với tài khoản Google có cùng email, để sau đó đăng nhập được bằng Google. |
| Trạng thái tài khoản | Một trong bốn giá trị: ACTIVE (hoạt động); DEACTIVATED (chủ tài khoản đã tự vô hiệu hóa, còn kích hoạt lại được trong thời hạn vô hiệu hóa); DELETED (đã xóa, không quay lại được, dữ liệu cá nhân đã bị xóa); BANNED (bị Mod hoặc Admin ban, M08). |
| Mức xác minh | Tiến độ đăng ký của tài khoản: NONE (chưa xác minh email), EMAIL_VERIFIED (đã xác minh email, chưa thiết lập xong), SETUP_COMPLETED (đã hoàn tất bước 3). |
| Đăng ký 3 bước | Bước 1: email, mật khẩu, đồng ý Privacy Policy/ToS. Bước 2: xác minh email. Bước 3: thiết lập username, display_name và thông tin tùy chọn. |
| Thông tin tùy chọn | Bio, Lớp/Khối, avatar nhập ở bước 3; bỏ qua được. Quy tắc của từng trường thuộc M02. |
| Magic link | Liên kết gửi tới email của tài khoản; mở liên kết còn hạn để xác minh email hoặc đặt lại mật khẩu. |
| Mã kích hoạt lại (OTP) | Mã 6 chữ số gửi tới email của tài khoản đã vô hiệu hóa, hạn 15 phút, dùng để xác nhận kích hoạt lại. |
| Cổng đăng nhập | Bước kiểm tra khi đăng nhập: trạng thái tài khoản trước, mức xác minh sau, để quyết định cho vào, từ chối hay đưa về bước đăng ký còn dở. |
| Thiết bị | Nơi người dùng đăng nhập. Mỗi lần đăng nhập trên một thiết bị tạo một phiên đăng nhập riêng. |
| Phiên đăng nhập | Trạng thái đã đăng nhập của một tài khoản trên một thiết bị, gồm phiên truy cập và phiên làm mới. |
| Phiên truy cập | Phần của phiên đăng nhập dùng cho từng thao tác; hạn 1 giờ. |
| Phiên làm mới | Phần của phiên đăng nhập dùng để cấp phiên truy cập mới khi phiên truy cập hết hạn; hạn 30 ngày; mỗi lần dùng được thay bằng một phiên làm mới mới, phiên cũ mất hiệu lực. |
| Vô hiệu hóa tài khoản | Việc chủ tài khoản tự đưa tài khoản sang DEACTIVATED. Là cách duy nhất để đi tới xóa tài khoản. |
| Thời hạn vô hiệu hóa | Đủ 14 × 24 giờ kể từ thời điểm vô hiệu hóa; trong thời hạn được kích hoạt lại, hết thời hạn thì tài khoản chuyển sang DELETED. |
| Dữ liệu cá nhân | Thông tin nhận diện người dùng. Danh mục bị xóa khi tài khoản chuyển sang DELETED theo BR-M01-47. |
| Trang Privacy Policy/ToS | Trang công khai gồm Chính sách quyền riêng tư và Điều khoản sử dụng; người đăng ký phải đồng ý. |
| Phiên bản chính sách | Số phiên bản gắn với mỗi bản nội dung của trang Privacy Policy/ToS; đổi khi nội dung trang đổi. |
| Bản ghi đồng ý | Ghi nhận một tài khoản đã đồng ý phiên bản chính sách nào, vào thời điểm nào. |
| username | Tên định danh duy nhất (so không phân biệt chữ hoa, chữ thường), chỉ gồm a–z, A–Z, 0–9 và "_", dùng để nhắc tên, tìm kiếm và trong địa chỉ trang hồ sơ. Không phải tên hiển thị chính. Username của tài khoản DELETED bị giữ vĩnh viễn. |
| display_name | Tên hiển thị chính của người dùng ở mọi nơi; tự do, không duy nhất. |
| Nhắc tên (@mention) | Việc chèn một người dùng vào bài viết hoặc bình luận bằng "@". Lượt nhắc tên ghi nhận theo tài khoản, hiển thị bằng display_name hiện tại. |
| Danh sách gợi ý nhắc tên | Danh sách tối đa 5 người dùng hiện ra khi đang gõ "@" để chọn người được nhắc. |
| Người đang theo dõi (trong nhắc tên) | Người dùng mà người đang soạn nội dung đã theo dõi (Follow). |
| Màn hình tài khoản bị khóa | Màn hình duy nhất tài khoản BANNED thấy sau khi đăng nhập. |
| Thời hạn khiếu nại | Thời gian được gửi khiếu nại một lần ban (M09): ban tạm thời bằng cả thời hạn ban; ban vĩnh viễn 90 ngày từ ngày ban. |
| Công tắc tạm dừng đăng ký | Cấu hình hệ thống do Admin bật, tắt ở M10 để ngừng nhận tài khoản mới. |
| Chế độ bảo trì | Cấu hình hệ thống do Admin bật, tắt ở M10; khi bật, chỉ tài khoản ADMIN đăng nhập và thao tác được. |
| Trang kích hoạt | Trang riêng, dùng khi chưa đăng nhập, nơi chủ tài khoản DEACTIVATED nhập email để nhận mã kích hoạt lại. |
| Trang sửa hồ sơ | Trang của M02 nơi người dùng đổi username, display_name và thông tin hồ sơ; quy tắc của username, display_name do M01 đặt. |
| Tên thay thế | Tên hiển thị thay cho tên tác giả hoặc người được nhắc khi tài khoản không còn hoạt động: "Tài khoản tạm thời vô hiệu hoá" (DEACTIVATED), "[Người dùng đã xóa]" (DELETED). |
| Nội dung hiển thị công khai | Bài viết hoặc bình luận đã qua bước quét trước khi đăng (M03, M04) và người khác xem được. |
| Ký tự | Đơn vị đếm độ dài mật khẩu, username, display_name: mỗi chữ cái (kể cả chữ có dấu), chữ số, khoảng trắng hoặc dấu là một ký tự. |
| Giờ hệ thống | Mọi thời điểm và mốc ngày hiển thị, tính toán theo giờ Việt Nam (UTC+7), không đổi theo mùa. |

### 2.2 Viết tắt

| Viết tắt | Đầy đủ |
|---|---|
| FR | Functional Requirement — yêu cầu chức năng |
| BR | Business Rule — quy tắc nghiệp vụ |
| TBD | To Be Determined — điểm chưa chốt |
| OTP | One-Time Password — mã dùng một lần, ở đây là mã kích hoạt lại |
| PII | Personally Identifiable Information — dữ liệu cá nhân |
| ToS | Terms of Service — điều khoản sử dụng |

## 3. Thông tin đầu vào

### 3.1 Tài liệu đầu vào

| Tài liệu | Phiên bản / mốc |
|---|---|
| Draft: docs/_temp/iShare_modules.md, iShare_specs_general.md | Theo ngày sửa tệp |
| Register: decisions, qa-log, issue-queue, open-issues, glossary, module-registry | DEC-247, QA-444, ISS-382, OPEN-012 (khớp `moc_nguon`) |

### 3.2 Tài liệu liên quan

| Module | Liên quan ở điểm nào |
|---|---|
| M02 User Profile | Dùng username, display_name; nhận các trường tùy chọn nhập ở bước 3 đăng ký. |
| M03 Post & Content | Chèn @mention trong bài viết; bài viết bị ẩn khi tác giả vô hiệu hóa tài khoản. |
| M04 Comment | Chèn @mention trong bình luận; hiển thị tác giả bình luận theo trạng thái tài khoản. |
| M06 Search | Tìm người dùng theo display_name, username, dùng chung cách so khớp với @mention. |
| M07 Notification | Gửi thông báo và email cho các sự kiện tài khoản và @mention. |
| M08 Moderation | Ban, gỡ ban, thời hạn ban làm đổi trạng thái tài khoản. |
| M09 Appeal | Khiếu nại ban từ màn hình tài khoản bị khóa; khiếu nại được chấp nhận đưa tài khoản về hoạt động. |
| M10 Admin Panel | Vai trò, tài khoản ADMIN gốc, công tắc tạm dừng đăng ký, chế độ bảo trì. |
| M11 Group | Chuyển quyền Owner khi tài khoản Owner bị vô hiệu hóa, bị xóa hoặc bị ban. |
| M12 Gamification | Nhãn tài khoản bị khóa, bảng xếp hạng với tài khoản BANNED. |
| M15 Analytics & Stats | Thống kê tài khoản theo trạng thái, lượt đăng ký mới. |
| M05 Topic & Tag | Trang Privacy Policy/ToS nêu việc bài đang soạn được gửi cho nhà cung cấp dịch vụ AI khi bấm "Gợi ý topic"; bài của tài khoản vô hiệu hóa hoặc đã xóa không tính Trending; lượt theo dõi Topic bị xóa và phản hồi gợi ý được giữ khi tài khoản bị xóa. |
| M13 AI Layer | Nhật ký AI của tài khoản đã xóa vẫn tra cứu được qua username. |
| M16 Chat & Messaging | Nhắn tin yêu cầu đăng nhập; tin nhắn của tài khoản đã xóa hiện người gửi "[Người dùng đã xóa]". |

## 4. Tổng quan chức năng

### 4.1 Luật, tiêu chuẩn liên quan

| Luật | Liên quan ở điểm nào |
|---|---|
| Luật Bảo vệ dữ liệu cá nhân 2025 (Luật số 91/2025/QH15, hiệu lực từ 01/01/2026) | Sự đồng ý của người dùng và việc chứng minh sự đồng ý; công khai chính sách xử lý dữ liệu; quyền của người dùng (biết, truy cập, sửa, xóa, rút lại đồng ý); bảo vệ dữ liệu của trẻ em |
| Luật Trẻ em 2016 | Trẻ em là người dưới 16 tuổi: một phần học sinh lớp 10 thuộc nhóm này |

Việc tuân thủ chi tiết cần được kiểm lại khi triển khai thật; MS1 chỉ chạy demo.

### 4.2 Vai trò

| Vai trò | Mô tả trong module này |
|---|---|
| Guest | Người chưa đăng nhập. Đăng ký tài khoản, đăng nhập bằng email hoặc Google, lấy lại mật khẩu. Chủ một tài khoản đã vô hiệu hóa cũng ở vai trò này vì không đăng nhập được; người đó chỉ kích hoạt lại tài khoản của mình. |
| User | Người dùng đã đăng nhập. Hoàn tất các bước đăng ký còn dở, đổi mật khẩu, đăng xuất, vô hiệu hóa tài khoản của mình, nhắc tên người khác khi soạn nội dung. |
| Mod | Có mọi quyền của User trên tài khoản của mình. Không vô hiệu hóa, không xóa tài khoản người khác. Được xem bài viết bị ẩn và danh tính thật của tác giả đã vô hiệu hóa tài khoản. |
| Admin | Như Mod trong module này. Tài khoản ADMIN gốc được tạo sẵn, không qua đăng ký. |
| Chủ tài khoản | Vai trò theo ngữ cảnh: người sở hữu tài khoản đang được thao tác (xác minh email, thiết lập, đổi mật khẩu, vô hiệu hóa, kích hoạt lại). |
| Hệ thống | Tác nhân của việc làm mới phiên đăng nhập, tự chuyển tài khoản vô hiệu hóa quá hạn sang đã xóa, và hiển thị nội dung theo trạng thái tài khoản của tác giả. |

### 4.3 Ma trận quyền

| Hành động | Guest | User | Mod | Admin | Yêu cầu |
|---|---|---|---|---|---|
| Đăng ký tài khoản bằng email và mật khẩu | ✓ | — | — | — | FR-M01-01.01, FR-M01-01.05, FR-M01-01.08 |
| Đăng ký, đăng nhập bằng Google | ✓ | — | — | — | FR-M01-04.01, FR-M01-04.04 |
| Xác minh email, yêu cầu gửi lại email xác minh | — | ✓ (của mình) | — | — | FR-M01-02.01, FR-M01-02.04 |
| Thiết lập username, display_name và thông tin tùy chọn (bước 3) | ✗ | ✓ (của mình) | — | — | FR-M01-03.01, FR-M01-03.09 |
| Đăng nhập bằng email và mật khẩu | ✓ | — | — | — | FR-M01-05.01 |
| Đăng xuất | — | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | FR-M01-07.01 |
| Đổi mật khẩu | ✗ | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | FR-M01-08.01, FR-M01-08.07 |
| Lấy lại mật khẩu qua email | ✓ | — | — | — | FR-M01-09.01 |
| Vô hiệu hóa tài khoản | ✗ | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | FR-M01-10.01, FR-M01-10.06 |
| Kích hoạt lại tài khoản đã vô hiệu hóa | ✓ (của mình) | — | — | — | FR-M01-11.02 |
| Vô hiệu hóa hoặc xóa tài khoản của người khác | ✗ | ✗ | ✗ | ✗ | FR-M01-10.03, FR-M01-10.04 |
| Xem bài viết, bình luận của tài khoản đã vô hiệu hóa hoặc đã xóa theo cách hiển thị thay thế | ✓ | ✓ | ✓ | ✓ | FR-M01-13.01, FR-M01-13.03, FR-M01-13.04 |
| Xem bài viết bị ẩn và danh tính thật của tác giả đã vô hiệu hóa tài khoản | ✗ | ✗ | ✓ | ✓ | FR-M01-13.05, FR-M01-13.01, FR-M01-13.03 |
| Nhắc tên (@mention) người dùng khác khi soạn nội dung | ✗ | ✓ | ✓ | ✓ | FR-M01-14.01, FR-M01-14.11 |
| Xem trang Privacy Policy/ToS | ✓ | ✓ | ✓ | ✓ | FR-M01-15.01 |
| Đồng ý phiên bản chính sách mới | — | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | FR-M01-16.01, FR-M01-16.03 |

<!-- "—" trong ô quyền: không áp dụng — Guest chưa có phiên để đăng xuất; người đã đăng nhập đã có tài khoản nên không đăng ký,
     không đăng nhập lại, không cần lấy lại mật khẩu; Mod, Admin đã hoàn tất đăng ký trước khi được cấp vai trò (ADMIN gốc tạo sẵn);
     kích hoạt lại chỉ làm được khi chưa đăng nhập vì tài khoản vô hiệu hóa không đăng nhập được.
     Ô nói thẳng: hàng 1, 5, 8 cột Guest (Guest được Đăng ký, Đăng nhập); hàng 11 cột Mod, Admin phần "xóa" (Admin, Mod không xóa tài khoản).
     Ô suy ra: hàng 11 cột Mod, Admin phần "vô hiệu hóa" (vô hiệu hóa dẫn tới tự xóa sau 14 ngày; register chỉ trao cho Mod, Admin cảnh báo và ban).
     Ô suy ra: hàng 2 cột Guest (đăng nhập bằng Google là một cách đăng nhập); hàng 4, 7, 9 cột Guest (cần đã đăng nhập);
     hàng 6, 7, 9 cột Mod, Admin (Mod, Admin cũng là chủ tài khoản của mình); hàng 11 cột Guest, User (vai trò cao hơn còn không được);
     hàng 12 (Guest xem được bài viết, bình luận thì vai trò cao hơn cũng xem được); hàng 13 cột Guest, User (nội dung bị ẩn, tên bị thay);
     hàng 14 cột Guest (Guest không đăng bài, bình luận). Hàng 13 cột Mod, Admin: nói thẳng theo câu trả lời Q-03. -->


### 4.4 Danh sách chức năng

| ID | Chức năng | Tác nhân chính | Kích hoạt |
|---|---|---|---|
| FR-M01-01 | Đăng ký tài khoản bằng email | Guest | Guest gửi biểu mẫu đăng ký với email, mật khẩu và đồng ý Privacy Policy/ToS |
| FR-M01-02 | Xác minh email | Chủ tài khoản | Chủ tài khoản mở magic link trong email xác minh, hoặc yêu cầu gửi lại email xác minh |
| FR-M01-03 | Thiết lập tài khoản | Chủ tài khoản | Chủ tài khoản đã xác minh email vào bước 3 để đặt username, display_name và thông tin tùy chọn |
| FR-M01-04 | Đăng ký, đăng nhập bằng Google | Guest | Guest chọn đăng nhập bằng Google và Google trả về tài khoản đã xác thực |
| FR-M01-05 | Đăng nhập bằng email và mật khẩu | Guest | Guest gửi email và mật khẩu để đăng nhập |
| FR-M01-06 | Duy trì phiên đăng nhập | Hệ thống | Phiên truy cập của một thiết bị hết hạn trong khi phiên làm mới còn hiệu lực |
| FR-M01-07 | Đăng xuất | User | Người dùng chọn đăng xuất |
| FR-M01-08 | Đổi mật khẩu | User | Người dùng đã đăng nhập gửi mật khẩu cũ, mật khẩu mới và nhập lại mật khẩu mới |
| FR-M01-09 | Lấy lại mật khẩu | Guest | Guest chọn "Quên mật khẩu" và nhập email |
| FR-M01-10 | Vô hiệu hóa tài khoản | User | Người dùng chọn vô hiệu hóa tài khoản của mình |
| FR-M01-11 | Kích hoạt lại tài khoản | Chủ tài khoản | Chủ tài khoản đã vô hiệu hóa vào trang kích hoạt trong thời hạn |
| FR-M01-12 | Tự xóa tài khoản hết hạn vô hiệu hóa | Hệ thống | Tài khoản ở trạng thái vô hiệu hóa đủ 14 ngày mà chưa kích hoạt lại |
| FR-M01-13 | Hiển thị nội dung của tài khoản đã vô hiệu hóa hoặc đã xóa | Hệ thống | Người xem mở bài viết, bình luận hoặc nơi có tên tác giả của tài khoản đã vô hiệu hóa hoặc đã xóa |
| FR-M01-14 | Nhắc tên người dùng (@mention) | User | Người dùng gõ "@" và ít nhất 1 ký tự khi soạn nội dung |
| FR-M01-15 | Xem trang Privacy Policy/ToS | Guest, User, Mod, Admin | Người dùng mở trang từ luồng đăng ký hoặc chân trang |
| FR-M01-16 | Đồng ý lại khi chính sách đổi | User | Người dùng mở ứng dụng khi phiên bản chính sách hiện hành mới hơn phiên bản họ đã đồng ý |

### 4.5 Mốc và ưu tiên

Toàn bộ yêu cầu của module thuộc MS1, ưu tiên **Must** (cột MoSCoW ở dòng M01 của bảng Module List; khớp bảng MoSCoW
Summary: Must gồm M01–M10, M13). Không có yêu cầu ngoại lệ về ưu tiên.

## 5. Yêu cầu chức năng

### 5.1 FR-M01-01 Đăng ký tài khoản bằng email

**Yêu cầu cấp trên:** Hệ thống phải cho phép Guest tạo tài khoản bằng email và mật khẩu khi đồng ý Privacy Policy/ToS, là bước 1 của đăng ký 3 bước.

**Lý do:** Bước đầu chỉ cần hai trường để giảm trở ngại khi đăng ký; phần định danh để sau khi xác minh email. Quyền riêng tư là phần bắt buộc của sản phẩm nên phải đồng ý mới đăng ký được.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M01-01.01 | Khi Guest gửi email, mật khẩu và đồng ý Privacy Policy/ToS, hệ thống phải tạo tài khoản ở trạng thái ACTIVE với mức xác minh NONE. |
| FR-M01-01.02 | Hệ thống phải gán vai trò USER cho mọi tài khoản mới, dù tạo bằng email hay bằng Google. |
| FR-M01-01.03 | Khi tạo tài khoản ở bước 1, hệ thống phải gửi magic link xác minh tới email vừa đăng ký. |
| FR-M01-01.04 | Hệ thống phải hiển thị liên kết tới trang Privacy Policy/ToS trong luồng đăng ký. |
| FR-M01-01.05 | Nếu người đăng ký không đồng ý Privacy Policy/ToS, hệ thống phải từ chối tạo tài khoản. |
| FR-M01-01.06 | Nếu email đã thuộc một tài khoản khác, hệ thống phải từ chối tạo tài khoản. |
| FR-M01-01.07 | Nếu thiếu email hoặc mật khẩu, hệ thống phải từ chối tạo tài khoản. |
| FR-M01-01.08 | Trong khi công tắc tạm dừng đăng ký đang bật, hệ thống phải từ chối tạo tài khoản email mới. |
| FR-M01-01.09 | Trong khi công tắc tạm dừng đăng ký đang bật, hệ thống phải vẫn cho tài khoản đã qua bước 1 làm tiếp bước 2 và bước 3. |
| FR-M01-01.10 | Nếu mật khẩu dài dưới 8 hoặc trên 64 ký tự, hệ thống phải từ chối mật khẩu đó. |
| FR-M01-01.11 | Hệ thống phải chấp nhận mọi ký tự trong mật khẩu, kể cả khoảng trắng và chữ có dấu, không bắt buộc loại ký tự và không tự cắt khoảng trắng. |
| FR-M01-01.12 | Trong khi chế độ bảo trì đang bật, hệ thống phải từ chối tạo tài khoản mới bằng email hoặc bằng Google. |
| FR-M01-01.13 | Hệ thống phải hiển thị ở bước 1 một ô đồng ý với nội dung "Tôi đồng ý với Điều khoản và Chính sách quyền riêng tư. Nếu dưới 16 tuổi, tôi đã được cha mẹ hoặc người giám hộ đồng ý." |
| FR-M01-01.14 | Khi tạo tài khoản, hệ thống phải lưu thời điểm và phiên bản chính sách mà người đăng ký đã đồng ý. |
| FR-M01-01.15 | Hệ thống phải không hỏi ngày sinh hay tuổi khi đăng ký. |


### 5.2 FR-M01-02 Xác minh email

**Yêu cầu cấp trên:** Hệ thống phải xác minh email của tài khoản email bằng magic link có hạn 1 giờ trước khi cho người dùng thiết lập tài khoản.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M01-02.01 | Khi chủ tài khoản mở magic link xác minh còn hạn, hệ thống phải chuyển mức xác minh từ NONE sang EMAIL_VERIFIED. |
| FR-M01-02.02 | Khi xác minh email thành công, hệ thống phải đưa người dùng tới bước 3. |
| FR-M01-02.03 | Nếu magic link xác minh đã quá 1 giờ kể từ khi gửi, hệ thống phải từ chối xác minh. |
| FR-M01-02.04 | Khi chủ tài khoản ở mức NONE yêu cầu gửi lại email xác minh, hệ thống phải gửi một magic link xác minh mới. |
| FR-M01-02.05 | Nếu yêu cầu gửi lại email xác minh đến khi chưa đủ 60 giây từ lần gửi trước, hệ thống phải từ chối gửi. |
| FR-M01-02.06 | Nếu magic link xác minh đã được dùng, hệ thống phải từ chối dùng lại link đó. |
| FR-M01-02.07 | Khi gửi magic link xác minh mới, hệ thống phải làm magic link xác minh trước đó mất hiệu lực. |


### 5.3 FR-M01-03 Thiết lập tài khoản

**Yêu cầu cấp trên:** Hệ thống phải cho phép chủ tài khoản đã xác minh email đặt username, display_name và thông tin tùy chọn để hoàn tất đăng ký.

**Lý do:** Theo thói quen của cộng đồng diễn đàn, tên hiển thị để tự do; còn nhắc tên cần một tên định danh duy nhất, không có khoảng trắng. Phần định danh được để tới sau khi xác minh email.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M01-03.01 | Khi chủ tài khoản ở mức EMAIL_VERIFIED gửi username và display_name hợp lệ, hệ thống phải lưu hai thông tin này và chuyển mức xác minh sang SETUP_COMPLETED. |
| FR-M01-03.02 | Hệ thống phải cho phép bỏ qua bio, Lớp/Khối và avatar ở bước 3. |
| FR-M01-03.03 | Khi chủ tài khoản nhập bio, Lớp/Khối hoặc avatar ở bước 3, hệ thống phải lưu các thông tin đó vào hồ sơ theo quy tắc của M02. |
| FR-M01-03.04 | Nếu thiếu username hoặc display_name, hệ thống phải từ chối hoàn tất bước 3. |
| FR-M01-03.05 | Nếu username dài dưới 3 hoặc trên 20 ký tự, hoặc có ký tự ngoài a–z, A–Z, 0–9 và "_", hệ thống phải từ chối username đó. |
| FR-M01-03.06 | Nếu username trùng username của một tài khoản khác, kể cả tài khoản đã DELETED, khi so không phân biệt chữ hoa, chữ thường, hệ thống phải từ chối username đó. |
| FR-M01-03.07 | Hệ thống phải chấp nhận display_name trùng với display_name của tài khoản khác. |
| FR-M01-03.08 | Nếu mức xác minh của tài khoản là NONE, hệ thống phải từ chối bước 3 và đưa người dùng về bước 2. |
| FR-M01-03.09 | Nếu người gửi chưa đăng nhập, hệ thống phải từ chối bước 3. |
| FR-M01-03.10 | Hệ thống phải dùng display_name làm tên hiển thị chính của người dùng ở mọi nơi tên người dùng xuất hiện. |
| FR-M01-03.11 | Hệ thống phải hiển thị username đúng chữ hoa, chữ thường như người dùng đã nhập. |
| FR-M01-03.12 | Khi lưu display_name, hệ thống phải bỏ khoảng trắng ở đầu và cuối. |
| FR-M01-03.13 | Nếu display_name sau khi bỏ khoảng trắng đầu, cuối bị rỗng hoặc dài quá 50 ký tự, hệ thống phải từ chối display_name đó. |
| FR-M01-03.14 | Nếu display_name có ký tự ngoài chữ cái (kể cả chữ có dấu), chữ số, khoảng trắng và các dấu . , - _ ' ( ), hệ thống phải từ chối display_name đó. |
| FR-M01-03.15 | Khi người dùng đổi username ở trang sửa hồ sơ (M02), hệ thống phải áp dụng các quy tắc username của FR-M01-03.05, FR-M01-03.06 và giải phóng username cũ cho tài khoản khác dùng. |
| FR-M01-03.16 | Khi người dùng đổi display_name ở trang sửa hồ sơ (M02), hệ thống phải áp dụng các quy tắc display_name của FR-M01-03.12 đến FR-M01-03.14. |


### 5.4 FR-M01-04 Đăng ký, đăng nhập bằng Google

**Yêu cầu cấp trên:** Hệ thống phải cho phép Guest đăng ký và đăng nhập bằng tài khoản Google, và tự liên kết Google vào tài khoản email đã xác minh có cùng email.

**Lý do:** Bảo đảm mỗi người một tài khoản, tránh trùng lặp; tự liên kết theo email đã xác minh là cách làm phổ biến. Email Google đã được xác minh nên bỏ qua bước 1 và 2.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M01-04.01 | Khi Guest đăng nhập Google lần đầu với email chưa thuộc tài khoản nào, hệ thống phải tạo tài khoản Google ở trạng thái ACTIVE, mức xác minh EMAIL_VERIFIED, và đưa người dùng tới bước 3. |
| FR-M01-04.02 | Khi tạo tài khoản Google, hệ thống phải điền sẵn display_name ở bước 3 bằng tên lấy từ Google và cho người dùng sửa. |
| FR-M01-04.03 | Khi tạo tài khoản Google, hệ thống phải yêu cầu người dùng tự đặt username ở bước 3. |
| FR-M01-04.04 | Khi Guest đăng nhập Google với email trùng email của một tài khoản email, hệ thống phải liên kết Google vào tài khoản đó mà không yêu cầu xác nhận, dù email của tài khoản đó đã xác minh hay chưa. |
| FR-M01-04.05 | Khi liên kết Google thành công, hệ thống phải thông báo cho chủ tài khoản trong ứng dụng và qua email. |
| FR-M01-04.06 | Khi Guest đăng nhập Google vào một tài khoản đã có, hệ thống phải áp dụng cổng đăng nhập như khi đăng nhập bằng email và mật khẩu. |
| FR-M01-04.07 | Nếu người đăng ký bằng Google chưa đồng ý Privacy Policy/ToS, hệ thống phải từ chối tạo tài khoản. |
| FR-M01-04.08 | Khi đăng nhập Google thành công, hệ thống phải tạo một phiên đăng nhập mới cho thiết bị đang dùng. |
| FR-M01-04.09 | Nếu tài khoản được liên kết đang ở mức xác minh NONE, hệ thống phải chuyển mức xác minh sang EMAIL_VERIFIED khi liên kết và đưa người dùng tới bước 3. |
| FR-M01-04.10 | Trong khi công tắc tạm dừng đăng ký đang bật, hệ thống phải từ chối tạo tài khoản Google mới. |
| FR-M01-04.11 | Trong khi công tắc tạm dừng đăng ký đang bật, hệ thống phải vẫn cho liên kết Google vào tài khoản đã có. |
| FR-M01-04.12 | Khi tạo tài khoản Google, hệ thống phải yêu cầu người đăng ký đánh dấu cùng ô đồng ý như FR-M01-01.13. |
| FR-M01-04.13 | Khi tạo tài khoản Google, hệ thống phải lưu thời điểm và phiên bản chính sách mà người đăng ký đã đồng ý. |


### 5.5 FR-M01-05 Đăng nhập bằng email và mật khẩu

**Yêu cầu cấp trên:** Hệ thống phải cho phép Guest đăng nhập bằng email và mật khẩu, rồi theo trạng thái tài khoản và mức xác minh mà cho vào, từ chối hoặc đưa về bước đăng ký còn dở.

**Lý do:** Tách vòng đời tài khoản khỏi tiến độ đăng ký để mỗi trường chỉ mang một ý nghĩa; người đăng ký dở được đưa về đúng bước còn thiếu.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M01-05.01 | Khi Guest gửi đúng email và mật khẩu của một tài khoản, hệ thống phải xét trạng thái tài khoản trước, rồi mới xét mức xác minh. |
| FR-M01-05.02 | Nếu email hoặc mật khẩu không đúng, hệ thống phải từ chối đăng nhập. |
| FR-M01-05.03 | Nếu tài khoản ở trạng thái DELETED, hệ thống phải từ chối đăng nhập. |
| FR-M01-05.04 | Nếu tài khoản ở trạng thái DEACTIVATED, hệ thống phải từ chối đăng nhập và giữ tài khoản ở trạng thái DEACTIVATED. |
| FR-M01-05.05 | Khi tài khoản BANNED đăng nhập đúng, hệ thống phải tạo phiên đăng nhập và chỉ hiển thị màn hình tài khoản bị khóa. |
| FR-M01-05.06 | Trong khi tài khoản BANNED, hệ thống phải từ chối mọi thao tác của tài khoản đó trừ gửi khiếu nại và đăng xuất. |
| FR-M01-05.07 | Hệ thống phải hiển thị lý do ban và nút OK trên màn hình tài khoản bị khóa. |
| FR-M01-05.08 | Trong khi còn thời hạn khiếu nại, hệ thống phải hiển thị thời gian khiếu nại còn lại và nút khiếu nại trên màn hình tài khoản bị khóa. |
| FR-M01-05.09 | Nếu đã hết thời hạn khiếu nại, hệ thống phải ẩn thời gian khiếu nại và nút khiếu nại trên màn hình tài khoản bị khóa. |
| FR-M01-05.10 | Khi tài khoản ACTIVE ở mức NONE đăng nhập, hệ thống phải đưa người dùng tới bước 2. |
| FR-M01-05.11 | Khi tài khoản ACTIVE ở mức EMAIL_VERIFIED đăng nhập, hệ thống phải đưa người dùng tới bước 3. |
| FR-M01-05.12 | Khi tài khoản ACTIVE ở mức SETUP_COMPLETED đăng nhập, hệ thống phải tạo phiên đăng nhập cho thiết bị đang dùng và cho người dùng vào hệ thống. |
| FR-M01-05.13 | Nếu tài khoản là tài khoản Google, hệ thống phải từ chối đăng nhập bằng mật khẩu. |
| FR-M01-05.14 | Khi Mod hoặc Admin ban một tài khoản ACTIVE, hệ thống phải chuyển tài khoản sang BANNED. |
| FR-M01-05.15 | Khi Mod hoặc Admin gỡ ban một tài khoản BANNED, hệ thống phải chuyển tài khoản về ACTIVE. |
| FR-M01-05.16 | Khi khiếu nại ban của một tài khoản được chấp nhận, hệ thống phải chuyển tài khoản về ACTIVE ngay lúc đó. |
| FR-M01-05.17 | Khi ban tạm thời của một tài khoản hết hạn, hệ thống phải chuyển tài khoản từ BANNED về ACTIVE ngay lúc hết hạn. |
| FR-M01-05.18 | Khi người dùng bấm OK trên màn hình tài khoản bị khóa, hệ thống phải đăng xuất thiết bị đang dùng. |
| FR-M01-05.19 | Trong khi chế độ bảo trì đang bật, hệ thống phải từ chối đăng nhập của tài khoản không có vai trò ADMIN. |
| FR-M01-05.20 | Trong khi chế độ bảo trì đang bật, hệ thống phải từ chối mọi thao tác qua phiên đăng nhập đang có của tài khoản không có vai trò ADMIN. |


### 5.6 FR-M01-06 Duy trì phiên đăng nhập

**Yêu cầu cấp trên:** Hệ thống phải giữ người dùng đăng nhập trên từng thiết bị bằng phiên truy cập hạn 1 giờ và phiên làm mới hạn 30 ngày, thay phiên làm mới sau mỗi lần dùng.

**Lý do:** Cách làm đơn giản, đủ cho quy mô của dự án; thay phiên làm mới sau mỗi lần dùng tăng an toàn mà không cần thêm hạ tầng. Đăng nhập trên nhiều thiết bị không làm phức tạp việc gửi dữ liệu tức thời.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M01-06.01 | Khi phiên truy cập hết hạn mà phiên làm mới còn hạn, hệ thống phải cấp phiên truy cập mới có hạn 1 giờ. |
| FR-M01-06.02 | Khi một phiên làm mới được dùng, hệ thống phải thay nó bằng một phiên làm mới mới và làm phiên làm mới cũ mất hiệu lực. |
| FR-M01-06.03 | Nếu một phiên làm mới đã mất hiệu lực được dùng lại, hệ thống phải từ chối. |
| FR-M01-06.04 | Nếu phiên làm mới đã hết hạn 30 ngày, hệ thống phải từ chối làm mới và yêu cầu đăng nhập lại. |
| FR-M01-06.05 | Hệ thống phải cho một tài khoản đăng nhập đồng thời trên nhiều thiết bị, mỗi thiết bị một phiên đăng nhập riêng. |
| FR-M01-06.06 | Khi phiên đăng nhập của một thiết bị hết hạn, hệ thống phải giữ nguyên phiên đăng nhập của các thiết bị khác. |
| FR-M01-06.07 | Khi cấp một phiên làm mới mới, hệ thống phải đặt hạn 30 ngày tính từ lúc cấp. |


### 5.7 FR-M01-07 Đăng xuất

**Yêu cầu cấp trên:** Hệ thống phải cho phép người dùng đã đăng nhập đăng xuất khỏi thiết bị đang dùng.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M01-07.01 | Khi người dùng đăng xuất, hệ thống phải kết thúc phiên đăng nhập của thiết bị đang dùng. |
| FR-M01-07.02 | Khi người dùng đăng xuất trên một thiết bị, hệ thống phải giữ nguyên phiên đăng nhập trên các thiết bị khác. |


### 5.8 FR-M01-08 Đổi mật khẩu

**Yêu cầu cấp trên:** Hệ thống phải cho phép người dùng đã đăng nhập đổi mật khẩu bằng mật khẩu cũ, mật khẩu mới và nhập lại mật khẩu mới.

**Lý do:** Đổi mật khẩu là cập nhật bình thường, không phải sự kiện bảo mật, nên không kết thúc phiên trên thiết bị khác.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M01-08.01 | Khi người dùng gửi mật khẩu cũ đúng, mật khẩu mới và nhập lại trùng khớp, hệ thống phải thay mật khẩu bằng mật khẩu mới. |
| FR-M01-08.02 | Nếu mật khẩu cũ không đúng, hệ thống phải từ chối đổi mật khẩu. |
| FR-M01-08.03 | Nếu mật khẩu nhập lại không khớp mật khẩu mới, hệ thống phải từ chối đổi mật khẩu. |
| FR-M01-08.04 | Khi đổi mật khẩu thành công, hệ thống phải giữ nguyên phiên đăng nhập trên các thiết bị khác. |
| FR-M01-08.05 | Khi đổi mật khẩu thành công, hệ thống phải gửi thông báo trong ứng dụng và email cho chủ tài khoản. |
| FR-M01-08.06 | Nếu tài khoản là tài khoản Google, hệ thống phải không cung cấp chức năng đổi mật khẩu. |
| FR-M01-08.07 | Nếu người gửi chưa đăng nhập, hệ thống phải từ chối đổi mật khẩu. |
| FR-M01-08.08 | Nếu mật khẩu mới dài dưới 8 hoặc trên 64 ký tự, hệ thống phải từ chối đổi mật khẩu. |
| FR-M01-08.09 | Nếu mật khẩu mới trùng mật khẩu hiện tại, hệ thống phải từ chối đổi mật khẩu. |
| FR-M01-08.10 | Nếu tài khoản không ở trạng thái ACTIVE, hệ thống phải từ chối đổi mật khẩu. |


### 5.9 FR-M01-09 Lấy lại mật khẩu

**Yêu cầu cấp trên:** Hệ thống phải cho phép người quên mật khẩu đặt mật khẩu mới qua magic link gửi tới email, có hạn 15 phút.

**Lý do:** Đặt lại mật khẩu là sự kiện bảo mật nên kết thúc mọi phiên khác; hạn 15 phút thu hẹp khoảng thời gian rủi ro.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M01-09.01 | Khi Guest nhập email của một tài khoản email ACTIVE hoặc BANNED ở "Quên mật khẩu", hệ thống phải gửi magic link đặt lại mật khẩu tới email đó. |
| FR-M01-09.02 | Khi người dùng mở magic link còn hạn và gửi mật khẩu mới cùng nhập lại trùng khớp, hệ thống phải thay mật khẩu bằng mật khẩu mới. |
| FR-M01-09.03 | Khi đặt lại mật khẩu thành công, hệ thống phải kết thúc mọi phiên đăng nhập hiện có của tài khoản. |
| FR-M01-09.04 | Khi đặt lại mật khẩu thành công, hệ thống phải đăng nhập thiết bị đang dùng bằng một phiên đăng nhập mới. |
| FR-M01-09.05 | Nếu magic link đặt lại mật khẩu đã quá 15 phút kể từ khi gửi, hệ thống phải từ chối đặt lại mật khẩu. |
| FR-M01-09.06 | Nếu mật khẩu nhập lại không khớp mật khẩu mới, hệ thống phải từ chối đặt lại mật khẩu. |
| FR-M01-09.07 | Nếu email nhập ở "Quên mật khẩu" thuộc tài khoản Google, hệ thống phải hiển thị "Tài khoản này đăng nhập qua Google, vui lòng dùng Google để đăng nhập" thay cho việc gửi magic link. |
| FR-M01-09.08 | Nếu mật khẩu mới dài dưới 8 hoặc trên 64 ký tự, hệ thống phải từ chối đặt lại mật khẩu. |
| FR-M01-09.09 | Nếu mật khẩu mới trùng mật khẩu hiện tại, hệ thống phải từ chối đặt lại mật khẩu. |
| FR-M01-09.10 | Nếu magic link đặt lại mật khẩu đã được dùng, hệ thống phải từ chối dùng lại link đó. |
| FR-M01-09.11 | Khi gửi magic link đặt lại mật khẩu mới, hệ thống phải làm magic link đặt lại mật khẩu trước đó mất hiệu lực. |
| FR-M01-09.12 | Khi đặt lại mật khẩu thành công, hệ thống phải gửi thông báo "mật khẩu đã đổi" trong ứng dụng và qua email cho chủ tài khoản. |
| FR-M01-09.13 | Khi nhận yêu cầu "Quên mật khẩu" cho email của một tài khoản email ACTIVE hoặc BANNED, hoặc cho email không thuộc tài khoản nào, hệ thống phải hiển thị cùng một câu "Liên kết đã được gửi, vui lòng kiểm tra email của bạn". |
| FR-M01-09.14 | Nếu email nhập ở "Quên mật khẩu" không thuộc tài khoản nào, hệ thống phải không gửi magic link. |
| FR-M01-09.15 | Nếu email nhập ở "Quên mật khẩu" thuộc tài khoản DEACTIVATED, hệ thống phải không gửi magic link và hướng người dùng tới trang kích hoạt lại. |
| FR-M01-09.16 | Trong khi tài khoản BANNED, hệ thống phải cho đặt lại mật khẩu qua magic link để người dùng đăng nhập vào màn hình tài khoản bị khóa. |


### 5.10 FR-M01-10 Vô hiệu hóa tài khoản

**Yêu cầu cấp trên:** Hệ thống phải cho phép người dùng tự vô hiệu hóa tài khoản của mình; đây là cách duy nhất để đi tới xóa tài khoản.

**Lý do:** Thời hạn 14 ngày cân bằng giữa việc cho người dùng đổi ý và việc không giữ tài khoản bỏ hoang mãi; 14 ngày đủ để khôi phục khi lỡ tay vô hiệu hóa.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M01-10.01 | Khi người dùng vô hiệu hóa tài khoản ACTIVE của mình, hệ thống phải chuyển tài khoản sang DEACTIVATED. |
| FR-M01-10.02 | Khi tài khoản chuyển sang DEACTIVATED, hệ thống phải kết thúc mọi phiên đăng nhập của tài khoản. |
| FR-M01-10.03 | Hệ thống phải không có thao tác xóa tài khoản trực tiếp. |
| FR-M01-10.04 | Nếu người thực hiện không là chủ tài khoản, hệ thống phải từ chối vô hiệu hóa, kể cả khi người đó là Mod hoặc Admin. |
| FR-M01-10.05 | Nếu tài khoản đang BANNED, hệ thống phải từ chối vô hiệu hóa. |
| FR-M01-10.06 | Nếu người gửi chưa đăng nhập, hệ thống phải từ chối vô hiệu hóa. |
| FR-M01-10.07 | Hệ thống phải tính thời hạn vô hiệu hóa đủ 14 × 24 giờ kể từ thời điểm vô hiệu hóa. |


### 5.11 FR-M01-11 Kích hoạt lại tài khoản

**Yêu cầu cấp trên:** Hệ thống phải cho phép chủ tài khoản đã vô hiệu hóa kích hoạt lại tài khoản trong thời hạn vô hiệu hóa, qua trang kích hoạt riêng và mã gửi tới email.

**Lý do:** Mã qua email là bước xác thực quan trọng: tránh kích hoạt vô tình và bảo đảm chỉ chủ tài khoản khôi phục được.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M01-11.01 | Khi chủ tài khoản nhập email của một tài khoản DEACTIVATED ở trang kích hoạt, hệ thống phải gửi tới email đó một mã kích hoạt lại gồm 6 chữ số. |
| FR-M01-11.02 | Khi chủ tài khoản nhập đúng mã kích hoạt lại trong thời hạn vô hiệu hóa, hệ thống phải chuyển tài khoản về ACTIVE. |
| FR-M01-11.03 | Khi tài khoản được kích hoạt lại, hệ thống phải hiển thị lại bài viết và bình luận của tài khoản với tên và avatar của chủ tài khoản. |
| FR-M01-11.04 | Nếu mã kích hoạt lại không đúng, hệ thống phải từ chối kích hoạt lại. |
| FR-M01-11.05 | Nếu đã hết thời hạn vô hiệu hóa, hệ thống phải từ chối kích hoạt lại. |
| FR-M01-11.06 | Khi kích hoạt lại thành công, hệ thống phải đăng nhập thiết bị đang dùng bằng một phiên đăng nhập mới. |
| FR-M01-11.07 | Nếu mã kích hoạt lại đã quá 15 phút kể từ khi gửi, hệ thống phải từ chối mã đó. |
| FR-M01-11.08 | Khi một mã kích hoạt lại bị nhập sai lần thứ 5, hệ thống phải làm mã đó mất hiệu lực. |
| FR-M01-11.09 | Nếu yêu cầu gửi lại mã kích hoạt lại đến khi chưa đủ 60 giây từ lần gửi trước, hệ thống phải từ chối gửi. |
| FR-M01-11.10 | Nếu email nhập ở trang kích hoạt không thuộc tài khoản DEACTIVATED, hệ thống phải không gửi mã kích hoạt lại. |


### 5.12 FR-M01-12 Tự xóa tài khoản hết hạn vô hiệu hóa

**Yêu cầu cấp trên:** Hệ thống phải tự chuyển tài khoản DEACTIVATED sang DELETED khi hết thời hạn vô hiệu hóa mà chưa kích hoạt lại, và xóa dữ liệu cá nhân của tài khoản.

**Lý do:** Không giữ tài khoản bỏ hoang mãi; xóa dữ liệu cá nhân là trường hợp xóa cứng có lý do rõ ràng (quyền riêng tư).

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M01-12.01 | Khi tài khoản DEACTIVATED hết thời hạn vô hiệu hóa mà chưa kích hoạt lại, hệ thống phải chuyển tài khoản sang DELETED. |
| FR-M01-12.02 | Khi tài khoản chuyển sang DELETED, hệ thống phải xóa dữ liệu cá nhân của tài khoản. |
| FR-M01-12.03 | Khi tài khoản chuyển sang DELETED, hệ thống phải giữ tài khoản ở trạng thái DELETED thay vì xóa hẳn tài khoản. |
| FR-M01-12.04 | Hệ thống phải không cho tài khoản DELETED chuyển sang trạng thái khác. |
| FR-M01-12.05 | Khi còn 24 giờ trước thời điểm tài khoản DEACTIVATED tự chuyển sang DELETED, hệ thống phải gửi một email cảnh báo cho chủ tài khoản. |
| FR-M01-12.06 | Khi tài khoản chuyển sang DELETED, hệ thống phải giải phóng email của tài khoản để email đó đăng ký được tài khoản mới. |
| FR-M01-12.07 | Khi tài khoản chuyển sang DELETED, hệ thống phải giữ username của tài khoản vĩnh viễn và không cho tài khoản khác dùng username đó. |
| FR-M01-12.08 | Khi tài khoản chuyển sang DELETED, hệ thống phải xóa email, mật khẩu, liên kết Google, display_name, avatar, bio, Lớp/Khối, mọi phiên đăng nhập, bookmark, mọi lượt theo dõi người dùng và Topic của tài khoản, mọi lượt người khác theo dõi tài khoản, và bản ghi đồng ý của tài khoản. |
| FR-M01-12.09 | Khi tài khoản chuyển sang DELETED, hệ thống phải giữ các upvote tài khoản đã cho trong điểm của người nhận mà không còn ghi nhận người cho. |
| FR-M01-12.10 | Khi tài khoản chuyển sang DELETED, hệ thống phải giữ liên kết giữa tài khoản đó với nhật ký kiểm duyệt và nhật ký AI qua username, để Mod và Admin tra cứu. |
| FR-M01-12.11 | Khi tài khoản chuyển sang DELETED, hệ thống phải giữ các phản hồi gợi ý Topic (M05) của tài khoản để đánh giá AI, không gắn với danh tính. |


### 5.13 FR-M01-13 Hiển thị nội dung của tài khoản đã vô hiệu hóa hoặc đã xóa

**Yêu cầu cấp trên:** Hệ thống phải hiển thị bài viết, bình luận và tên tác giả của tài khoản đã vô hiệu hóa hoặc đã xóa theo cách thay thế, giữ nguyên luồng thảo luận của người khác.

**Lý do:** Bài viết đứng riêng nên ẩn được an toàn; bình luận là một phần luồng thảo luận của người khác nên được giữ chỗ để luồng còn nguyên vẹn.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M01-13.01 | Trong khi tài khoản ở trạng thái DEACTIVATED hoặc DELETED, hệ thống phải ẩn mọi bài viết của tài khoản đó với người xem, trừ trường hợp ở FR-M01-13.05. |
| FR-M01-13.02 | Nếu người xem mở địa chỉ một bài viết bị ẩn theo FR-M01-13.01, hệ thống phải hiển thị "Nội dung không tồn tại". |
| FR-M01-13.03 | Trong khi tài khoản ở trạng thái DEACTIVATED, hệ thống phải hiển thị bình luận của tài khoản với nội dung gốc, tên tác giả "Tài khoản tạm thời vô hiệu hoá" và avatar mặc định. |
| FR-M01-13.04 | Trong khi tài khoản ở trạng thái DELETED, hệ thống phải hiển thị bình luận của tài khoản với nội dung gốc, tên tác giả "[Người dùng đã xóa]" và avatar mặc định. |
| FR-M01-13.05 | Trong khi tài khoản ở trạng thái DEACTIVATED, hệ thống phải cho Mod và Admin xem các bài viết bị ẩn và danh tính thật của tác giả. |
| FR-M01-13.06 | Trong khi tài khoản ở trạng thái DELETED, hệ thống phải hiển thị tin nhắn của tài khoản đó với nội dung gốc và người gửi "[Người dùng đã xóa]". |


### 5.14 FR-M01-14 Nhắc tên người dùng (@mention)

**Yêu cầu cấp trên:** Hệ thống phải cho phép người dùng nhắc tên người dùng khác khi soạn nội dung bằng cách gõ "@" rồi chọn từ danh sách gợi ý, và ghi nhận lượt nhắc theo tài khoản người được nhắc.

**Lý do:** Nền tảng cộng đồng cần nhắc tên, và nhắc tên cần một tên định danh duy nhất không có khoảng trắng. So khớp theo chuỗi con xử lý tốt tên tiếng Việt và khoảng trắng; tầng ưu tiên đưa người liên quan lên trước; lượt nhắc là một khối liền để tránh sửa nhãn gây hiểu sai.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M01-14.01 | Khi người soạn gõ "@" kèm ít nhất 1 ký tự rồi ngừng gõ 300 mili giây, hệ thống phải hiển thị danh sách gợi ý nhắc tên. |
| FR-M01-14.02 | Hệ thống phải tìm người cho danh sách gợi ý nhắc tên theo cả display_name và username, khớp chuỗi tìm ở bất kỳ vị trí trong tên, không phân biệt chữ hoa, chữ thường, bỏ dấu tiếng Việt khi so, cho khớp gần đúng khi gõ sai nhẹ, và chấp nhận chuỗi tìm có khoảng trắng (BR-M01-26). |
| FR-M01-14.03 | Hệ thống phải hiển thị tối đa 5 người trong danh sách gợi ý nhắc tên, mỗi người kèm avatar, display_name và username hiện mờ. |
| FR-M01-14.04 | Khi người soạn đang soạn nội dung trong một Group, hệ thống phải xếp danh sách gợi ý theo thứ tự: người đang theo dõi, người cùng Group đó, những người còn lại. |
| FR-M01-14.05 | Khi người soạn đang soạn bài viết ngoài Group, hệ thống phải xếp danh sách gợi ý theo thứ tự: người đang theo dõi, người có chung ít nhất một Group với người soạn, những người còn lại. |
| FR-M01-14.06 | Khi người soạn chọn một người trong danh sách gợi ý, hệ thống phải chèn lượt nhắc tên dưới dạng một khối liền ghi nhận theo tài khoản người được nhắc. |
| FR-M01-14.07 | Hệ thống phải hiển thị lượt nhắc tên bằng display_name hiện tại của người được nhắc, có làm nổi bật và không có ký tự "@". |
| FR-M01-14.08 | Hệ thống phải không cho sửa nhãn của lượt nhắc tên. |
| FR-M01-14.09 | Khi người soạn xóa lùi vào một lượt nhắc tên, hệ thống phải xóa cả lượt nhắc tên đó. |
| FR-M01-14.10 | Khi nội dung chứa lượt nhắc tên hiển thị công khai, hệ thống phải gửi thông báo cho người được nhắc, dù lượt nhắc nằm trong bài viết hay bình luận, kể cả khi người đó đã tắt thông báo của bài viết. |
| FR-M01-14.11 | Nếu người soạn chưa đăng nhập, hệ thống phải không hiển thị danh sách gợi ý nhắc tên. |
| FR-M01-14.12 | Khi nhiều người cùng một tầng ưu tiên trong danh sách gợi ý, hệ thống phải xếp người khớp chuỗi tìm nhiều hơn lên trước. |
| FR-M01-14.13 | Khi người soạn nhắc tên trong bình luận, hệ thống phải xếp danh sách gợi ý theo ngữ cảnh của bài viết chứa bình luận. |
| FR-M01-14.14 | Hệ thống phải không đưa vào danh sách gợi ý nhắc tên các tài khoản DEACTIVATED, DELETED, BANNED và tài khoản chưa hoàn tất bước 3. |
| FR-M01-14.15 | Trong khi người được nhắc ở trạng thái DEACTIVATED hoặc DELETED, hệ thống phải hiển thị lượt nhắc tên đó bằng tên thay thế "Tài khoản tạm thời vô hiệu hoá" hoặc "[Người dùng đã xóa]" tương ứng. |
| FR-M01-14.16 | Trong khi người được nhắc ở trạng thái DEACTIVATED hoặc DELETED, hệ thống phải không mở trang hồ sơ khi người xem bấm vào lượt nhắc tên đó. |
| FR-M01-14.17 | Khi nội dung đã công khai được sửa, hệ thống phải chỉ gửi thông báo nhắc tên cho những người mới được nhắc thêm. |


### 5.15 FR-M01-15 Xem trang Privacy Policy/ToS

**Yêu cầu cấp trên:** Hệ thống phải cung cấp một trang Privacy Policy/ToS công khai nêu dữ liệu được thu thập, cách xử lý, quyền của người dùng và điều khoản sử dụng.

**Lý do:** Một trang nội dung tĩnh, chi phí thấp nhưng tăng minh bạch đáng kể, đặc biệt quan trọng vì người dùng là học sinh, có thể là trẻ vị thành niên. Quyền riêng tư là phần bắt buộc của sản phẩm.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M01-15.01 | Hệ thống phải cho mọi người, kể cả Guest, xem trang Privacy Policy/ToS. |
| FR-M01-15.02 | Hệ thống phải hiển thị trang Privacy Policy/ToS gồm các mục của BR-M01-42. |
| FR-M01-15.03 | Hệ thống phải trình bày dữ liệu được thu thập trên trang theo bốn nhóm của BR-M01-43, không liệt kê từng trường dữ liệu. |
| FR-M01-15.04 | Hệ thống phải nêu trên trang rằng nội dung bài viết, bình luận, kể cả bài đang soạn khi bấm "Gợi ý topic", được xử lý bởi nhà cung cấp dịch vụ AI, không nêu tên nhà cung cấp. |
| FR-M01-15.05 | Hệ thống phải nêu trên trang rằng iShare dùng dịch vụ bên ngoài cho đăng nhập, lưu ảnh, gửi email và AI, và không bán dữ liệu của người dùng. |
| FR-M01-15.06 | Hệ thống phải nêu trên trang rằng bình luận, tin nhắn, nhật ký kiểm duyệt và nhật ký AI được giữ lại sau khi xóa tài khoản để bảo đảm an toàn cộng đồng. |
| FR-M01-15.07 | Hệ thống phải nêu trên trang quyền sửa thông tin, quyền xóa tài khoản, cách rút lại sự đồng ý bằng vô hiệu hóa tài khoản, và quyền nhận bản sao dữ liệu. |
| FR-M01-15.08 | Hệ thống phải gắn mỗi bản nội dung của trang Privacy Policy/ToS với một phiên bản chính sách. |
| FR-M01-15.09 | Hệ thống phải chỉ đổi nội dung trang và phiên bản chính sách qua việc đội phát triển triển khai bản mới, không có màn hình chỉnh sửa hay phát hành cho Admin. |

### 5.16 FR-M01-16 Đồng ý lại khi chính sách đổi

**Yêu cầu cấp trên:** Hệ thống phải yêu cầu người dùng đồng ý lại khi Privacy Policy/ToS đổi sang phiên bản mới, và chỉ khi đó.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M01-16.01 | Khi người dùng mở ứng dụng, kể cả khi đang giữ phiên đăng nhập, mà phiên bản chính sách hiện hành mới hơn phiên bản họ đã đồng ý, hệ thống phải yêu cầu họ đồng ý phiên bản hiện hành trước khi dùng tiếp. |
| FR-M01-16.02 | Khi người dùng đồng ý phiên bản chính sách mới, hệ thống phải lưu thời điểm và phiên bản đó. |
| FR-M01-16.03 | Nếu người dùng không đồng ý phiên bản chính sách mới, hệ thống phải chỉ cho người dùng chọn đăng xuất hoặc vô hiệu hóa tài khoản. |
| FR-M01-16.04 | Nếu người dùng chưa đồng ý phiên bản chính sách mới, hệ thống phải hỏi lại ở lần mở ứng dụng kế tiếp. |
| FR-M01-16.05 | Trong khi phiên bản chính sách hiện hành không đổi, hệ thống phải không hỏi lại sự đồng ý của người đã đồng ý phiên bản đó. |

### 5.17 Quy tắc nghiệp vụ

| ID | Loại | Quy tắc | Ví dụ |
|---|---|---|---|
| BR-M01-01 | Sự kiện | Hệ thống chỉ có một loại tài khoản; không phân biệt tài khoản Giáo viên và Học sinh. Vai trò của tài khoản là USER, MOD hoặc ADMIN; tài khoản mới đăng ký có vai trò USER. | — |
| BR-M01-02 | Ràng buộc | Đăng ký bằng email đi qua 3 bước theo thứ tự. Bước 1 tạo tài khoản ở trạng thái ACTIVE, mức xác minh NONE. Bước 2 đưa mức xác minh lên EMAIL_VERIFIED. Bước 3 bắt buộc username và display_name; bio, Lớp/Khối, avatar bỏ qua được; xong bước 3 thì mức xác minh là SETUP_COMPLETED. | A gửi email, mật khẩu và đồng ý: tài khoản ACTIVE, NONE. A mở magic link: EMAIL_VERIFIED. A đặt username, display_name, bỏ qua cả 3 trường tùy chọn: SETUP_COMPLETED. |
| BR-M01-03 | Ràng buộc | Mọi tài khoản mới, kể cả tạo bằng Google, chỉ được tạo khi người đăng ký đồng ý rõ ràng với Privacy Policy/ToS. Luồng đăng ký có liên kết tới trang Privacy Policy/ToS. | Không đánh dấu đồng ý: từ chối, không tạo tài khoản. Đánh dấu đồng ý: tiếp tục. |
| BR-M01-04 | Ràng buộc | Mỗi email thuộc tối đa một tài khoản. | Đã có tài khoản với a@gmail.com; người khác đăng ký bằng a@gmail.com: từ chối. |
| BR-M01-05 | Ràng buộc | username bắt buộc, dài 3–20 ký tự, chỉ gồm a–z, A–Z, 0–9 và dấu gạch dưới "_". So trùng không phân biệt chữ hoa, chữ thường, và username của tài khoản DELETED vẫn được tính; khi hiển thị, username giữ đúng chữ hoa, chữ thường như người dùng nhập. | "abc": hợp lệ. "ab", 21 ký tự: từ chối. "Duc_PV": hợp lệ, hiển thị "Duc_PV". Đã có "duc_pv", người khác chọn "DUC_PV": từ chối. "đức_pv", "duc pv", "duc.pv": từ chối. Tài khoản "cuong" đã DELETED, người mới chọn "Cuong": từ chối. |
| BR-M01-06 | Ràng buộc | display_name bắt buộc, được trùng với display_name của tài khoản khác. Sau khi bỏ khoảng trắng ở đầu và cuối, display_name dài 1–50 ký tự và chỉ gồm chữ cái (kể cả chữ có dấu), chữ số, khoảng trắng và các dấu . , - _ ' ( ); không nhận emoji và ký hiệu khác. | "  Minh Anh  ": lưu "Minh Anh". "Anh (12A1)", "N.T.Lan", "Minh-Anh": hợp lệ. "Lan ★", "Lan 😊": từ chối. Chuỗi chỉ gồm khoảng trắng: từ chối. 50 ký tự: hợp lệ; 51 ký tự: từ chối. Hai tài khoản cùng "Minh Anh": hợp lệ. |
| BR-M01-07 | Suy diễn | display_name là tên hiển thị chính ở mọi nơi. username không dùng làm tên hiển thị chính; username dùng để nhắc tên, tìm kiếm, trong địa chỉ trang hồ sơ, và hiện mờ cạnh display_name trong danh sách gợi ý nhắc tên. | Tài khoản display_name "Minh Anh", username "minhanh_12": bài viết hiện tác giả "Minh Anh"; danh sách gợi ý nhắc tên hiện "Minh Anh" kèm "@minhanh_12" mờ. |
| BR-M01-08 | Suy diễn | Đăng nhập Google lần đầu mà email Google chưa thuộc tài khoản nào thì tạo tài khoản Google, bỏ qua bước 1 và 2, mức xác minh bắt đầu ở EMAIL_VERIFIED. Ở bước 3, display_name được điền sẵn từ tên Google và người dùng đổi được; username người dùng tự đặt. | B đăng nhập Google lần đầu với tên Google "Trần Bình": vào thẳng bước 3, display_name điền sẵn "Trần Bình", B sửa thành "Bình Trần" và đặt username "binh_tran". |
| BR-M01-09 | Kích hoạt | Khi đăng nhập Google mà email Google trùng email của một tài khoản email, hệ thống tự liên kết Google vào tài khoản đó, không hỏi xác nhận, dù email đã xác minh hay chưa; nếu chưa, mức xác minh lên EMAIL_VERIFIED. Sau khi liên kết, chủ tài khoản nhận thông báo trong ứng dụng và qua email. | A có tài khoản email a@gmail.com đã xác minh, đăng nhập Google bằng a@gmail.com: vào tài khoản cũ, nhận thông báo và email. A' đăng ký a2@gmail.com nhưng chưa xác minh, đăng nhập Google bằng a2@gmail.com: tài khoản được liên kết, lên EMAIL_VERIFIED, A' được đưa tới bước 3. |
| BR-M01-10 | Ràng buộc | Magic link xác minh email hết hạn sau 1 giờ kể từ khi gửi. Xác minh email là bắt buộc. | Gửi lúc 10:00, mở lúc 10:59: xác minh được. Mở lúc 11:01: hết hạn, không xác minh. |
| BR-M01-11 | Ràng buộc | Người dùng tự yêu cầu gửi lại email xác minh; hai lần gửi cách nhau ít nhất 60 giây. | Gửi lúc 10:00:00; yêu cầu lúc 10:00:45: từ chối. Yêu cầu lúc 10:01:00: gửi. |
| BR-M01-12 | Ràng buộc | Magic link đặt lại mật khẩu hết hạn sau 15 phút kể từ khi gửi. | Gửi lúc 20:00, mở lúc 20:14: đặt lại được. Mở lúc 20:16: hết hạn. |
| BR-M01-13 | Kích hoạt | Khi đặt lại mật khẩu thành công, mọi phiên đăng nhập hiện có của tài khoản bị kết thúc và thiết bị đang đặt lại được đăng nhập bằng một phiên mới. | A đang đăng nhập trên điện thoại và laptop, đặt lại mật khẩu trên máy tính bảng: điện thoại, laptop bị đăng xuất; máy tính bảng được đăng nhập. |
| BR-M01-14 | Ràng buộc | Đổi mật khẩu khi đã đăng nhập cần mật khẩu cũ đúng, mật khẩu mới và nhập lại mật khẩu mới trùng khớp. Đổi mật khẩu không kết thúc phiên trên thiết bị khác. | Mật khẩu cũ sai: từ chối. Nhập lại không khớp: từ chối. Hợp lệ: đổi; laptop đang đăng nhập vẫn giữ phiên. |
| BR-M01-15 | Suy diễn | Tài khoản Google không có chức năng mật khẩu. Khi tài khoản Google dùng "Quên mật khẩu", hệ thống không gửi magic link mà hiện "Tài khoản này đăng nhập qua Google, vui lòng dùng Google để đăng nhập". | B (tài khoản Google) nhập email ở "Quên mật khẩu": hiện thông báo trên, không gửi email. |
| BR-M01-16 | Ràng buộc | Phiên truy cập hết hạn sau 1 giờ. Mỗi lần dùng phiên làm mới, hệ thống cấp phiên làm mới mới có hạn 30 ngày tính từ lúc cấp, và phiên làm mới cũ mất hiệu lực. | Đăng nhập lúc 08:00 ngày 01/10: phiên truy cập hết hạn 09:00, thiết bị làm mới. Làm mới ngày 25/10: phiên làm mới mới hết hạn ngày 24/11. Dùng lại phiên làm mới cũ: từ chối. Không mở ứng dụng từ 25/10 tới 25/11: phải đăng nhập lại. |
| BR-M01-17 | Sự kiện | Một tài khoản được đăng nhập đồng thời trên nhiều thiết bị; mỗi thiết bị có phiên đăng nhập riêng, độc lập với thiết bị khác. | A đăng nhập trên điện thoại và laptop: hai phiên riêng; phiên của điện thoại hết hạn không ảnh hưởng laptop. |
| BR-M01-18 | Suy diễn | Cổng đăng nhập xét trạng thái tài khoản trước: DELETED bị từ chối; DEACTIVATED bị từ chối và đăng nhập không tự kích hoạt lại tài khoản; BANNED được đăng nhập nhưng chỉ vào màn hình tài khoản bị khóa; ACTIVE thì xét tiếp mức xác minh: NONE đưa về bước 2, EMAIL_VERIFIED đưa về bước 3, SETUP_COMPLETED vào hệ thống. | ACTIVE + NONE: về bước 2. ACTIVE + EMAIL_VERIFIED: về bước 3. ACTIVE + SETUP_COMPLETED: vào. BANNED: màn hình bị khóa. DEACTIVATED: từ chối. DELETED: từ chối. |
| BR-M01-19 | Ràng buộc | Trong khi tài khoản BANNED, người dùng chỉ thấy màn hình tài khoản bị khóa và chỉ gửi được khiếu nại; mọi thao tác khác bị từ chối. Màn hình gồm lý do ban, nút OK, và — chỉ khi còn trong thời hạn khiếu nại — thời gian khiếu nại còn lại cùng nút khiếu nại. | Ban tạm thời 30 ngày từ 01/10: ngày 10/10 thấy lý do, còn 21 ngày khiếu nại và nút khiếu nại. Ban vĩnh viễn ngày 01/10: thời hạn khiếu nại tới 30/12; ngày 05/01 chỉ thấy lý do và nút OK. |
| BR-M01-20 | Ràng buộc | Không có thao tác xóa tài khoản trực tiếp; chủ tài khoản muốn xóa phải vô hiệu hóa. Mod và Admin không vô hiệu hóa, không xóa tài khoản người khác; với tài khoản người khác chỉ có cảnh báo và ban (M08). | — |
| BR-M01-21 | Kích hoạt | Tài khoản DEACTIVATED hết thời hạn vô hiệu hóa (đủ 14 × 24 giờ kể từ lúc vô hiệu hóa) mà chưa kích hoạt lại thì tự chuyển sang DELETED: dữ liệu cá nhân bị xóa, email được giải phóng, username bị giữ vĩnh viễn; DELETED không quay lại được. | Vô hiệu hóa lúc 21:00 ngày 01/10: tới 20:59 ngày 15/10 vẫn DEACTIVATED; lúc 21:00 ngày 15/10 chuyển DELETED. Ngày 20/10 có người đăng ký bằng email cũ: được. Người đó chọn username cũ: từ chối. |
| BR-M01-22 | Ràng buộc | Kích hoạt lại chỉ làm được trong thời hạn vô hiệu hóa: chủ tài khoản nhập email ở trang kích hoạt, nhận mã 6 chữ số qua email. Mã hạn 15 phút; một mã bị nhập sai 5 lần thì mất hiệu lực; xin lại mã cách lần trước ít nhất 60 giây. Nhập đúng mã thì tài khoản về ACTIVE và thiết bị được đăng nhập luôn. | Mã gửi 10:00: nhập đúng lúc 10:14 thì ACTIVE và đăng nhập; nhập lúc 10:16 thì hết hạn. Nhập sai 4 lần rồi đúng ở lần 5: thành công. Sai lần thứ 5: mã mất hiệu lực, phải xin mã mới. Xin lại lúc 10:00:40: từ chối; lúc 10:01:00: gửi. |
| BR-M01-23 | Suy diễn | Trong khi tài khoản DEACTIVATED: bài viết của tài khoản bị ẩn, mở địa chỉ bài thấy "Nội dung không tồn tại"; bình luận giữ nguyên nội dung, tên tác giả hiện "Tài khoản tạm thời vô hiệu hoá", avatar hiện ảnh mặc định. | B vô hiệu hóa: bài "Ôn thi THPT" của B không hiện ở đâu; bình luận "Dùng định lý Vi-ét" vẫn hiện, tác giả "Tài khoản tạm thời vô hiệu hoá". |
| BR-M01-24 | Suy diễn | Khi tài khoản DELETED: bài viết của tài khoản vẫn bị ẩn như khi DEACTIVATED; bình luận giữ nguyên nội dung, tên tác giả hiện "[Người dùng đã xóa]", avatar hiện ảnh mặc định. | Tài khoản B sang DELETED: bài "Ôn thi THPT" vẫn ẩn; bình luận "Dùng định lý Vi-ét" vẫn hiện, tác giả "[Người dùng đã xóa]". |
| BR-M01-25 | Suy diễn | Khi tài khoản được kích hoạt lại, bài viết và bình luận của tài khoản hiển thị lại với tên và avatar của chủ tài khoản như trước khi vô hiệu hóa. | B kích hoạt lại ngày 05/10: bài "Ôn thi THPT" hiện lại; bình luận hiện tác giả là display_name của B. |
| BR-M01-26 | Ràng buộc | Danh sách gợi ý nhắc tên mở khi người soạn gõ "@" kèm ít nhất 1 ký tự, và tìm sau khi người soạn ngừng gõ 300 mili giây. Chuỗi tìm được chứa khoảng trắng. Hệ thống tìm theo cả display_name và username, hiện tối đa 5 người; mỗi người hiện avatar, display_name và username. Chuỗi tìm khớp ở bất kỳ vị trí trong display_name hoặc username, không phân biệt chữ hoa, chữ thường, bỏ dấu tiếng Việt khi so, cho khớp gần đúng khi gõ sai nhẹ; cách khớp này dùng chung với tìm người dùng của M06. | Gõ "@": chưa mở. Gõ "@N": mở. Gõ "@Nguyễn Văn": tìm theo cả chuỗi có khoảng trắng. Có 8 người khớp: hiện 5. Gõ "@Nam": có "Nguyễn Văn Nam". Gõ "@nguyen" hoặc "@Nguyên": có "Nguyễn …". |
| BR-M01-27 | Tính toán | Thứ tự trong danh sách gợi ý nhắc tên theo ngữ cảnh. Khi soạn trong Group, hoặc bình luận trên bài viết trong Group: người đang theo dõi, rồi người cùng Group đó, rồi những người còn lại. Khi soạn ngoài Group: người đang theo dõi, rồi người có chung ít nhất một Group với người soạn, rồi những người còn lại. Trong cùng một tầng, người khớp chuỗi tìm nhiều hơn xếp trước. | Bình luận trên bài trong Group "Lớp 12A1", gõ "@Lan": Lan Anh (đang theo dõi), Lan Chi (thành viên 12A1), Lan Hương (không liên quan): thứ tự Lan Anh, Lan Chi, Lan Hương. Tầng cuối có "Lan" và "Hoàng Lan": "Lan" xếp trước. |
| BR-M01-28 | Suy diễn | Lượt nhắc tên được ghi nhận theo tài khoản người được nhắc và hiển thị bằng display_name hiện tại của người đó, có làm nổi bật, không hiện ký tự "@". Người được nhắc đổi display_name thì mọi lượt nhắc cũ hiện tên mới. | Nhắc "Minh Anh" ngày 01/10; ngày 05/10 người đó đổi tên thành "Anh Minh": bài viết hiện "Anh Minh" được làm nổi bật. |
| BR-M01-29 | Ràng buộc | Lượt nhắc tên là một khối liền: không sửa được nhãn; xóa lùi vào lượt nhắc thì xóa cả lượt nhắc. | Đã chèn "Minh Anh", bấm xóa lùi ở cuối: cả "Minh Anh" bị xóa, không còn "Minh An". |
| BR-M01-30 | Kích hoạt | Mỗi lượt nhắc tên sinh một thông báo cho người được nhắc (M07) khi nội dung chứa nó hiển thị công khai, dù trong bài viết hay bình luận, kể cả khi người đó đã tắt thông báo của bài viết. Khi nội dung được sửa, chỉ người mới được nhắc thêm nhận thông báo. | Bài nhắc An và Bình, qua bước quét lúc 10:05: An, Bình nhận thông báo lúc đó. Sửa bài, thêm Chi: chỉ Chi nhận thông báo. |
| BR-M01-31 | Kích hoạt | Khi đổi mật khẩu thành công, chủ tài khoản nhận thông báo trong ứng dụng và qua email (M07). | — |
| BR-M01-32 | Kích hoạt | Còn 24 giờ trước khi tài khoản DEACTIVATED tự chuyển sang DELETED, chủ tài khoản nhận một email cảnh báo (M07); không có thông báo trong ứng dụng vì tài khoản không đăng nhập được. | Vô hiệu hóa lúc 21:00 ngày 01/10: email cảnh báo lúc 21:00 ngày 14/10. |
| BR-M01-33 | Ràng buộc | Trong khi công tắc tạm dừng đăng ký đang bật, không tạo được tài khoản mới bằng email hay bằng đăng nhập Google lần đầu; liên kết Google vào tài khoản có sẵn vẫn làm được; tài khoản đã qua bước 1 vẫn làm tiếp bước 2 và 3. | Admin bật công tắc lúc 09:00. 09:30 Guest gửi bước 1: từ chối. 09:40 người chưa có tài khoản đăng nhập Google: từ chối. 09:45 người có tài khoản email đăng nhập Google: liên kết được. Tài khoản tạo lúc 08:50 mở link xác minh lúc 09:10: xác minh được. |
| BR-M01-34 | Suy diễn | Tài khoản BANNED trở lại ACTIVE khi Mod hoặc Admin gỡ ban (M08), khi khiếu nại ban được chấp nhận (M09), hoặc ngay lúc ban tạm thời hết hạn. | Ban 30 ngày từ 01/10: tự về ACTIVE ngày 31/10. |
| BR-M01-35 | Ràng buộc | Mật khẩu dài 8–64 ký tự; nhận mọi ký tự, kể cả khoảng trắng và chữ có dấu; không bắt buộc loại ký tự; không tự cắt khoảng trắng. Khi đổi hoặc đặt lại, mật khẩu mới phải khác mật khẩu hiện tại. | "1234567": từ chối. "12345678": hợp lệ. 64 ký tự: hợp lệ; 65: từ chối. "mật khẩu của tôi": hợp lệ. Mật khẩu hiện tại "abc12345", đổi sang "abc12345": từ chối. |
| BR-M01-36 | Suy diễn | Đổi username, display_name làm ở trang sửa hồ sơ (M02), không giới hạn số lần, theo BR-M01-05 và BR-M01-06; username cũ được giải phóng ngay khi đổi. Đổi mật khẩu và đổi thông tin chỉ làm được khi tài khoản ACTIVE. | Ngày 10/10 "minhanh_12" đổi thành "MinhAnh": người khác chọn "minhanh_12" được ngay. |
| BR-M01-37 | Ràng buộc | Trong khi chế độ bảo trì đang bật, chỉ tài khoản có vai trò ADMIN đăng nhập và thao tác được; tài khoản khác bị từ chối đăng nhập và phiên đang có không dùng được. | Bảo trì từ 22:00: Admin đăng nhập lúc 22:10 được; User đang đăng nhập từ 21:50, thao tác lúc 22:05: từ chối. |
| BR-M01-38 | Ràng buộc | Mỗi magic link (xác minh email, đặt lại mật khẩu) chỉ dùng được một lần; gửi link mới thì link cùng loại gửi trước mất hiệu lực. | Link xác minh gửi 10:00, gửi lại 10:05: mở link 10:00 lúc 10:06 bị từ chối, link 10:05 dùng được. Mở link 10:05 lần thứ hai: từ chối. |
| BR-M01-39 | Suy diễn | "Quên mật khẩu": email của tài khoản email ACTIVE hoặc BANNED, hoặc email không thuộc tài khoản nào, đều thấy cùng câu "Liên kết đã được gửi, vui lòng kiểm tra email của bạn", và chỉ tài khoản có thật mới nhận link; tài khoản Google nhận thông báo dùng Google (BR-M01-15); tài khoản DEACTIVATED không nhận link, được hướng tới trang kích hoạt lại. Tài khoản BANNED đặt lại xong vẫn chỉ vào màn hình tài khoản bị khóa. | Nhập x@gmail.com chưa đăng ký: hiện câu chung, không gửi gì. E bị ban, quên mật khẩu: nhận link, đặt lại, đăng nhập vào màn hình bị khóa, gửi khiếu nại. |
| BR-M01-40 | Suy diễn | Danh sách gợi ý nhắc tên không gồm tài khoản DEACTIVATED, DELETED, BANNED và tài khoản chưa hoàn tất bước 3. Lượt nhắc đã có tới tài khoản DEACTIVATED, DELETED hiện tên thay thế như bình luận (BR-M01-23, BR-M01-24) và không mở trang hồ sơ khi bấm. | Gõ "@Bình" khi Bình đã vô hiệu hóa: Bình không có trong danh sách. Bài cũ nhắc Bình: hiện "Tài khoản tạm thời vô hiệu hoá", bấm vào không mở trang nào. |
| BR-M01-41 | Ràng buộc | Trong khi tài khoản DEACTIVATED, Mod và Admin xem được bài viết bị ẩn và danh tính thật của tác giả; người dùng khác chỉ thấy cách hiển thị thay thế. Khi DELETED, dữ liệu cá nhân đã bị xóa nên không còn danh tính để xem. | Mod mở báo cáo về bình luận của B (đã vô hiệu hóa): thấy tác giả là B. User thường xem cùng bình luận: thấy "Tài khoản tạm thời vô hiệu hoá". |
| BR-M01-42 | Sự kiện | Trang Privacy Policy/ToS gồm phần Chính sách quyền riêng tư với các mục: dữ liệu thu thập; mục đích sử dụng; dịch vụ bên ngoài; thời gian lưu; quyền của bạn; người dùng dưới 16 tuổi; thay đổi chính sách; liên hệ. Và phần Điều khoản sử dụng với các mục: quy tắc cộng đồng và nội dung bị cấm; kiểm duyệt và cảnh báo; khóa tài khoản và khiếu nại; quyền đối với nội dung đăng. Câu chữ cụ thể viết sau. | — |
| BR-M01-43 | Ràng buộc | Trang trình bày dữ liệu theo bốn nhóm: (1) thông tin tài khoản và hồ sơ, kể cả email và tên nhận từ Google khi đăng nhập Google; (2) nội dung bạn tạo (bài viết, bình luận, tin nhắn, tệp đính kèm, lượt thích, lưu bài); (3) dữ liệu giữ an toàn cộng đồng (báo cáo, cảnh báo, khóa tài khoản, khiếu nại); (4) dữ liệu được xử lý bởi nhà cung cấp dịch vụ AI. Không nêu phiên đăng nhập; không nêu tên nhà cung cấp. | — |
| BR-M01-44 | Kích hoạt | Hệ thống lưu thời điểm và phiên bản chính sách mỗi lần người dùng đồng ý. Người dùng chỉ phải đồng ý lại khi chính sách đổi sang phiên bản mới, ở lần mở ứng dụng kế tiếp, kể cả khi đang giữ phiên đăng nhập. Phiên bản mới chỉ được phát hành khi đội phát triển triển khai bản mới. | A đồng ý bản 1.0 ngày 01/10 và giữ phiên đăng nhập. Bản 1.1 được triển khai ngày 05/10. A mở ứng dụng ngày 05/10 lúc 20:00: phải đồng ý 1.1 trước khi dùng tiếp. Ngày 10/10 A mở lại, chính sách vẫn 1.1: không hỏi. |
| BR-M01-45 | Suy diễn | Rút lại sự đồng ý được thực hiện bằng vô hiệu hóa tài khoản. Người không đồng ý phiên bản chính sách mới không vào được hệ thống, chỉ chọn được đăng xuất hoặc vô hiệu hóa tài khoản, và được hỏi lại ở lần mở ứng dụng sau. | A bấm "Không đồng ý" bản 1.1: chỉ còn hai nút Đăng xuất và Vô hiệu hóa tài khoản. A đăng xuất; lần sau đăng nhập lại được hỏi bản 1.1. |
| BR-M01-46 | Ràng buộc | Hệ thống không hỏi tuổi. Người dưới 16 tuổi cam kết đã được cha mẹ hoặc người giám hộ đồng ý qua chính ô đồng ý ở bước 1; trang có mục riêng cho người dưới 16 tuổi. MS1 không có chức năng tải bản sao dữ liệu; trang nêu quyền này. | H 15 tuổi đăng ký: đánh dấu ô đồng ý (gồm câu cam kết) là đủ, không có bước hỏi tuổi hay xác nhận phụ huynh. |
| BR-M01-47 | Suy diễn | Khi tài khoản DELETED: xóa email (được giải phóng), mật khẩu, liên kết Google, display_name, avatar, bio, Lớp/Khối, mọi phiên đăng nhập, bookmark, mọi lượt theo dõi (người dùng, Topic) của tài khoản và mọi lượt người khác theo dõi tài khoản, bản ghi đồng ý. Giữ: username (khóa vĩnh viễn), trạng thái, vai trò, bài viết (vẫn ẩn), bình luận và tin nhắn (người viết hiện "[Người dùng đã xóa]"), upvote đã cho (không còn biết ai cho), nhật ký kiểm duyệt và nhật ký AI (vẫn gắn qua username), phản hồi gợi ý Topic (không gắn danh tính). | "Minh Anh" có 12 bookmark, theo dõi 30 người, có 50 người theo dõi; sau DELETED: 0 bookmark, 30 người kia bớt một người theo dõi, 50 người kia bớt một người đang theo dõi; tin nhắn cũ với C hiện người gửi "[Người dùng đã xóa]". Minh Anh theo dõi Topic "Toán học": số người theo dõi "Toán học" giảm một. |


### 5.18 Dữ liệu nghiệp vụ

| Thực thể | Thuộc tính nguồn đã nêu | Quan hệ |
|---|---|---|
| Tài khoản | Email (không trùng), mật khẩu (không có ở tài khoản Google), username, display_name, vai trò, trạng thái tài khoản, mức xác minh, liên kết Google, thời điểm vô hiệu hóa | Có nhiều Bản ghi đồng ý, nhiều Phiên đăng nhập; có một hồ sơ (M02); là tác giả bài viết (M03), bình luận (M04); được nhắc trong nhiều Lượt nhắc tên |
| Magic link xác minh email | Tài khoản, thời điểm gửi, hạn 1 giờ | Thuộc một Tài khoản |
| Magic link đặt lại mật khẩu | Tài khoản, thời điểm gửi, hạn 15 phút | Thuộc một Tài khoản |
| Mã kích hoạt lại | Tài khoản | Thuộc một Tài khoản đang DEACTIVATED; gửi qua email |
| Phiên đăng nhập | Tài khoản, thiết bị, phiên truy cập (hạn 1 giờ), phiên làm mới (hạn 30 ngày) | Thuộc một Tài khoản; mỗi thiết bị một phiên |
| Lượt nhắc tên | Người được nhắc, nội dung chứa lượt nhắc | Thuộc một bài viết (M03) hoặc bình luận (M04); trỏ tới một Tài khoản |
| Phiên bản chính sách | Số phiên bản, nội dung trang Privacy Policy/ToS | Tại mỗi thời điểm có một phiên bản hiện hành |
| Bản ghi đồng ý | Tài khoản, phiên bản chính sách, thời điểm đồng ý | Thuộc một Tài khoản; trỏ tới một Phiên bản chính sách |

<!-- "Thời điểm vô hiệu hóa": nguồn không nêu tên thuộc tính, suy ra từ thời hạn 14 ngày tính từ lúc vô hiệu hóa.
     Vai trò: quản lý ở M10, M01 chỉ gán USER khi tạo tài khoản. Thông tin tùy chọn (bio, Lớp/Khối, avatar) thuộc hồ sơ M02. -->

**Ma trận CRUD:**

| Thực thể | Tạo | Đọc | Sửa | Xóa |
|---|---|---|---|---|
| Tài khoản | FR-M01-01.01, FR-M01-04.01 | FR-M01-05.01, FR-M01-13.03, FR-M01-14.02; hồ sơ: M02 | Mức xác minh, username, display_name lần đầu: FR-M01-02.01, FR-M01-03.01, FR-M01-04.02. Liên kết Google: FR-M01-04.04. Mật khẩu: FR-M01-08.01, FR-M01-09.02. Trạng thái: FR-M01-10.01, FR-M01-11.02, FR-M01-12.01; BANNED và gỡ ban: M08, M09. Vai trò: FR-M01-01.02 khi tạo; sau đó M10. Đổi username, display_name sau bước 3: M02 theo FR-M01-03.15, FR-M01-03.16 | Không có (BR-M01-20; DELETED giữ tài khoản, chỉ xóa dữ liệu cá nhân: FR-M01-12.02, FR-M01-12.03) |
| Magic link xác minh email | FR-M01-01.03, FR-M01-02.04 | FR-M01-02.01 | Không có | FR-M01-02.06, FR-M01-02.07; hết hạn theo BR-M01-10 |
| Magic link đặt lại mật khẩu | FR-M01-09.01 | FR-M01-09.02 | Không có | FR-M01-09.10, FR-M01-09.11; hết hạn theo BR-M01-12 |
| Mã kích hoạt lại | FR-M01-11.01 | FR-M01-11.02 | Không có | FR-M01-11.08; hết hạn theo BR-M01-22 |
| Phiên đăng nhập | FR-M01-04.08, FR-M01-05.05, FR-M01-05.12, FR-M01-09.04, FR-M01-11.06 | FR-M01-06.01 | FR-M01-06.02 | FR-M01-07.01, FR-M01-05.18, FR-M01-09.03, FR-M01-10.02 |
| Lượt nhắc tên | FR-M01-14.06 | FR-M01-14.07 | Không có (BR-M01-29) | FR-M01-14.09; M03, M04 khi nội dung bị sửa hoặc xóa |
| Phiên bản chính sách | Không có trong hệ thống (đội phát triển phát hành khi triển khai, FR-M01-15.09) | FR-M01-15.01, FR-M01-16.01 | Không có (mỗi lần đổi nội dung là một phiên bản mới, FR-M01-15.08) | Không có |
| Bản ghi đồng ý | FR-M01-01.14, FR-M01-04.13, FR-M01-16.02 | FR-M01-16.01 | Không có (mỗi lần đồng ý tạo một bản ghi mới) | FR-M01-12.08 |

<!-- Không còn ô "—": các ô đã được trả lời ở Q-09, Q-14, Q-15, Q-27. -->


### 5.19 Chuyển trạng thái

#### Tài khoản — trạng thái tài khoản

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Guest hoàn tất bước 1 của đăng ký email, hoặc đăng nhập Google lần đầu với email chưa có tài khoản | Đồng ý Privacy Policy/ToS; email chưa thuộc tài khoản nào; công tắc tạm dừng đăng ký và chế độ bảo trì đang tắt | ACTIVE | FR-M01-01.01, FR-M01-04.01 |
| ACTIVE | Chủ tài khoản vô hiệu hóa | — | DEACTIVATED | FR-M01-10.01 |
| DEACTIVATED | Chủ tài khoản kích hoạt lại và xác nhận mã kích hoạt lại | Còn trong thời hạn vô hiệu hóa | ACTIVE | FR-M01-11.02 |
| DEACTIVATED | Hết thời hạn vô hiệu hóa | Chưa kích hoạt lại | DELETED | FR-M01-12.01 |
| ACTIVE | Mod hoặc Admin ban (M08) | — | BANNED | FR-M01-05.14 |
| BANNED | Mod hoặc Admin gỡ ban (M08) | — | ACTIVE | FR-M01-05.15 |
| BANNED | Khiếu nại ban được chấp nhận (M09) | — | ACTIVE | FR-M01-05.16 |
| BANNED | Ban tạm thời hết hạn | — | ACTIVE | FR-M01-05.17 |

DELETED là trạng thái kết thúc.

#### Tài khoản — mức xác minh

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Hoàn tất bước 1 của đăng ký email | — | NONE | FR-M01-01.01 |
| (bắt đầu) | Đăng nhập Google lần đầu với email chưa có tài khoản | — | EMAIL_VERIFIED | FR-M01-04.01 |
| NONE | Mở magic link xác minh email | Link còn hạn, chưa dùng, là link mới nhất | EMAIL_VERIFIED | FR-M01-02.01 |
| NONE | Đăng nhập Google với email trùng email của tài khoản | — | EMAIL_VERIFIED | FR-M01-04.09 |
| EMAIL_VERIFIED | Hoàn tất bước 3 | username hợp lệ, có display_name | SETUP_COMPLETED | FR-M01-03.01 |

SETUP_COMPLETED là mức cuối; nguồn không có đường đi ngược lại.

### 5.20 Giao tiếp với module khác

| Hướng | Module | Nội dung ở mức nghiệp vụ | Yêu cầu |
|---|---|---|---|
| Cung cấp | M02 | username, display_name và thông tin tùy chọn nhập ở bước 3; quy tắc username, display_name khi đổi ở trang sửa hồ sơ; trạng thái tài khoản để trang hồ sơ của tài khoản DEACTIVATED, DELETED hiện "người dùng không tồn tại" | FR-M01-03.01, FR-M01-03.03, FR-M01-03.15, FR-M01-03.16, FR-M01-10.01 |
| Dùng | M02 | Quy tắc bio, Lớp/Khối, avatar cho bước 3 đăng ký; avatar, display_name hiển thị ở nơi hiện tác giả, người gửi | FR-M01-03.03 |
| Cung cấp | M03, M04 | Danh sách gợi ý nhắc tên và lượt nhắc tên trong trình soạn; cách hiển thị bài viết, bình luận theo trạng thái tài khoản của tác giả | FR-M01-14.01, FR-M01-14.06, FR-M01-13.01, FR-M01-13.03, FR-M01-13.04 |
| Dùng | M03, M04 | Lưu, sửa, xóa nội dung chứa lượt nhắc tên; lượt nhắc đi theo nội dung | — |
| Cung cấp | M06 | Tìm người dùng theo display_name và username, dùng chung cách so khớp với danh sách gợi ý nhắc tên (BR-M01-26); trạng thái tài khoản và việc đã xong bước 3 để M06 chỉ hiện tài khoản ACTIVE đã xong bước 3; sự kiện đăng xuất để M06 xóa lịch sử tìm kiếm trên trình duyệt | FR-M01-14.02 |
| Cung cấp | M07 | Các sự kiện cần thông báo: liên kết Google, đổi và đặt lại mật khẩu, cảnh báo 24 giờ trước khi tự xóa, nhắc tên khi nội dung công khai | FR-M01-04.05, FR-M01-08.05, FR-M01-09.12, FR-M01-12.05, FR-M01-14.10 |
| Dùng | M07 | Gửi thông báo trong ứng dụng và email; danh sách người đang theo dõi để xếp danh sách gợi ý nhắc tên | FR-M01-14.04, FR-M01-14.05 |
| Dùng | M08 | Ban, gỡ ban, thời hạn ban (hết hạn thì tài khoản tự về ACTIVE) và lý do ban hiển thị trên màn hình tài khoản bị khóa; Mod xử lý báo cáo về nội dung của tác giả đã vô hiệu hóa | FR-M01-05.05, FR-M01-05.07, FR-M01-05.17, FR-M01-13.05 |
| Cung cấp | M09 | Tài khoản BANNED đăng nhập được nhưng chỉ vào màn hình tài khoản bị khóa, nơi chỉ khiếu nại được lệnh ban (nút khiếu nại khi còn thời hạn); đặt lại mật khẩu để vào màn hình đó; đăng nhập trước khi tới trang khiếu nại | FR-M01-05.05, FR-M01-05.08, FR-M01-05.09 |
| Dùng | M09 | Thời hạn khiếu nại và việc gửi khiếu nại từ màn hình tài khoản bị khóa; khiếu nại ban được chấp nhận đưa tài khoản về ACTIVE | FR-M01-05.08, FR-M01-05.09 |
| Dùng | M10 | Công tắc tạm dừng đăng ký, chế độ bảo trì; cấp, thu hồi vai trò; tài khoản ADMIN gốc tạo sẵn không qua đăng ký | FR-M01-01.08, FR-M01-04.10, FR-M01-05.19, FR-M01-01.02 |
| Cung cấp | M10 | Tài khoản mới mang vai trò USER; trạng thái tài khoản và việc đã xong bước 3 để M10 chỉ gửi đề xuất làm Mod, làm Admin cho tài khoản ACTIVE đã xong bước 3 | FR-M01-01.02, FR-M01-03.01 |
| Cung cấp | M11 | Trạng thái tài khoản (vô hiệu hóa, đã xóa, bị ban) để chuyển quyền Owner | FR-M01-10.01, FR-M01-12.01 |
| Dùng | M11 | Thành viên Group để xếp danh sách gợi ý nhắc tên | FR-M01-14.04, FR-M01-14.05 |
| Cung cấp | M12 | Trạng thái BANNED để gắn nhãn "Tài khoản đã bị khóa" và loại khỏi bảng xếp hạng; trạng thái DEACTIVATED (loại khỏi bảng xếp hạng trong thời gian vô hiệu hóa, có lại khi kích hoạt lại) và DELETED (hiện mờ trên bảng đã chốt với nhãn "[Người dùng đã xóa]", sau đó bị loại) (DEC-246) | FR-M01-05.06, FR-M01-10.01, FR-M01-11.02, FR-M01-12.01 |
| Cung cấp | M15 | Trạng thái tài khoản và việc tạo tài khoản mới để thống kê | FR-M01-01.01, FR-M01-04.01 |
| Cung cấp | M05 | Trang Privacy Policy/ToS nêu việc tiêu đề và nội dung bài đang soạn, kể cả chưa đăng, được xử lý bởi nhà cung cấp dịch vụ AI khi bấm "Gợi ý topic" | FR-M01-15.04 |
| Cung cấp | M05 | Trạng thái tài khoản tác giả (bài của tài khoản vô hiệu hóa hoặc đã xóa bị ẩn); dữ liệu của tài khoản đã xóa: upvote giữ, bookmark và lượt theo dõi Topic bị xóa, phản hồi gợi ý Topic giữ | FR-M01-13.01, FR-M01-12.08, FR-M01-12.09, FR-M01-12.11 |
| Cung cấp | M16 | Tên thay thế "[Người dùng đã xóa]" cho người gửi tin nhắn của tài khoản đã xóa | FR-M01-13.06 |
| Cung cấp | M08 | Trạng thái tài khoản: ban chuyển ACTIVE sang BANNED, gỡ ban và khiếu nại ban được chấp nhận đưa về ACTIVE, ban tạm thời hết hạn thì tự về ACTIVE; màn hình tài khoản bị khóa hiển thị lý do ban | FR-M01-05.05, FR-M01-05.07, FR-M01-05.14, FR-M01-05.15, FR-M01-05.17 |
| Cung cấp | M08, M13 | Liên kết nhật ký kiểm duyệt và nhật ký AI với tài khoản đã xóa qua username | FR-M01-12.10 |
| Cung cấp | M12 | Upvote đã cho của tài khoản đã xóa vẫn tính cho người nhận, không còn biết ai cho | FR-M01-12.09 |
| Cung cấp | Mọi module | Phiên đăng nhập xác định người đang dùng là ai và đã đăng nhập hay chưa | FR-M01-05.12, FR-M01-06.01 |

### 5.21 AI hỗ trợ và hành vi khi tắt AI

Không áp dụng. Module không dùng AI.

### 5.22 Yêu cầu HMI

Chưa có — chờ giai đoạn thiết kế.

### 5.23 Chuyển màn hình

Chưa có — chờ giai đoạn thiết kế.

## 6. Lịch sử sửa đổi

| Phiên bản | Ngày | Nội dung | Người sửa |
|---|---|---|---|
| 0.1 | 2026-10-08 | Tạo mới | Phạm Văn Đức |
| 0.2 | 2026-10-11 | Hoàn thành bước 1–6; ghi register DEC-147–153, QA-292–308, ISS-232–248 | Phạm Văn Đức |
| 0.3 | 2026-10-11 | Bổ sung quyền riêng tư theo DEC-154–157 (OPEN-008 thu hẹp): trang Privacy Policy/ToS, đồng ý lại khi chính sách đổi (DEC-158), dữ liệu xóa khi DELETED | Phạm Văn Đức |
| 1.0 | 2026-10-11 | Chốt sau 7 bước; ghi register DEC-147–158, QA-292–318, ISS-232–258; OPEN-008 thu hẹp | Phạm Văn Đức |
| 1.1 | 2026-10-11 | Đối chiếu với FR-M05: xóa cả lượt theo dõi Topic, bài viết khi DELETED; giữ phản hồi gợi ý Topic (DEC-159); bổ sung giao tiếp với M05. Chốt bản 1.1 | Phạm Văn Đức |
| 1.2 | 2026-10-15 | Đối chiếu với FR-M08: thêm dòng "Cung cấp M08" (trạng thái tài khoản khi ban, gỡ ban, ban hết hạn) ở mục Giao tiếp với module khác; không đổi yêu cầu. Chốt bản 1.2 | Phạm Văn Đức |
| 1.3 | 2026-10-20 | Đối chiếu với FR-M06: @mention khớp tên như tìm người dùng M06 (DEC-214); giao tiếp với M06 thêm trạng thái tài khoản, sự kiện đăng xuất. Chốt bản 1.3 | Phạm Văn Đức |
| 1.4 | 2026-10-21 | Đối chiếu với FR-M07 (DEC-215): khi DELETED chỉ xóa lượt theo dõi người dùng, Topic; bỏ "bài viết" (FR-M01-12.08, BR-M01-47, C.2). Chốt bản 1.4 | Phạm Văn Đức |
| 1.5 | 2026-10-21 | Đối chiếu với FR-M10 (DEC-221, DEC-228): thêm dòng "Cung cấp M10" (vai trò USER khi tạo, trạng thái tài khoản và bước 3 cho đề xuất làm Mod, Admin); DEC-007 sửa một phần (chỉ ADMIN gốc cấp, thu hồi Admin). Không đổi yêu cầu. Chốt bản 1.5 | Phạm Văn Đức |
| 1.6 | 2026-10-23 | Rà lại với register tới DEC-247: dòng Cung cấp M12 thêm trạng thái DEACTIVATED, DELETED cho bảng xếp hạng (DEC-246); thêm dòng Dùng M02 khớp FR-M02, dòng Cung cấp M09 khớp FR-M09. Không đổi yêu cầu. Chốt bản 1.6 | Phạm Văn Đức |

## Phụ lục A. Truy vết

| ID | Nguồn | Căn cứ | Ghi chú |
|---|---|---|---|
| FR-M01-01 | DM-1.1, DEC-014, DEC-131, DEC-138, QA-011, DG-2, MR-M01, DEC-092 | Nói thẳng | Bước 1 của đăng ký 3 bước; DEC-092 (M10) là công tắc tạm dừng đăng ký |
| FR-M01-01.01 | DEC-014, DEC-018 | Nói thẳng | — |
| FR-M01-01.02 | DG-2, DEC-007 | Suy ra | Vai trò MOD, ADMIN chỉ có qua cấp quyền (M10, DEC-007) ⇒ tài khoản mới là USER (BR-M01-01) |
| FR-M01-01.03 | DEC-014 | Nói thẳng | — |
| FR-M01-01.04 | DEC-131, DEC-138 | Nói thẳng | — |
| FR-M01-01.05 | DEC-138 | Nói thẳng | — |
| FR-M01-01.06 | DEC-010 | Suy ra | BR-M01-04: liên kết theo email để tránh trùng tài khoản ⇒ một email chỉ thuộc một tài khoản |
| FR-M01-01.07 | DEC-014 | Suy ra | Bước 1 gồm email và mật khẩu ⇒ thiếu một trong hai bị từ chối |
| FR-M01-01.08 | DEC-092, DEC-152 | Nói thẳng | — |
| FR-M01-01.09 | DEC-152 | Nói thẳng | — |
| FR-M01-01.10 | DEC-148 | Nói thẳng | — |
| FR-M01-01.11 | DEC-148 | Nói thẳng | — |
| FR-M01-01.12 | DEC-092, DEC-152 | Suy ra | Bảo trì "locks site to admin-only access", chỉ ADMIN dùng được ⇒ không ai tạo được tài khoản mới |
| FR-M01-01.13 | DEC-157 | Nói thẳng | — |
| FR-M01-01.14 | DEC-155 | Nói thẳng | — |
| FR-M01-01.15 | DEC-157 | Nói thẳng | — |
| FR-M01-02 | DM-1.1, DEC-014, DEC-016, DEC-018, MR-M01 | Nói thẳng | Bước 2; gồm gửi lại email xác minh |
| FR-M01-02.01 | DEC-014, DEC-018 | Nói thẳng | — |
| FR-M01-02.02 | DEC-014 | Nói thẳng | — |
| FR-M01-02.03 | DEC-014, DEC-016 | Suy ra | Magic link hạn 1 giờ ⇒ link quá hạn bị từ chối |
| FR-M01-02.04 | DEC-016 | Nói thẳng | — |
| FR-M01-02.05 | DEC-016 | Suy ra | Thời gian chờ 60 giây ⇒ yêu cầu sớm hơn bị từ chối |
| FR-M01-02.06 | DEC-151 | Nói thẳng | — |
| FR-M01-02.07 | DEC-151 | Nói thẳng | — |
| FR-M01-03 | DEC-014, DEC-015, DEC-018, QA-053 | Nói thẳng | Bước 3 |
| FR-M01-03.01 | DEC-014, DEC-018, DEC-015 | Nói thẳng | — |
| FR-M01-03.02 | DEC-014 | Nói thẳng | — |
| FR-M01-03.03 | DEC-014 | Nói thẳng | Quy tắc từng trường thuộc M02 |
| FR-M01-03.04 | DEC-014 | Suy ra | username, display_name "required" ⇒ thiếu bị từ chối |
| FR-M01-03.05 | DEC-015, DEC-148 | Nói thẳng | — |
| FR-M01-03.06 | DEC-015, DEC-148 | Nói thẳng | — |
| FR-M01-03.07 | DEC-015 | Nói thẳng | — |
| FR-M01-03.08 | DEC-014, DEC-018 | Suy ra | Bước 3 chỉ sau khi xác minh; cổng đăng nhập đưa về bước còn dở ⇒ NONE về bước 2 |
| FR-M01-03.09 | DEC-014 | Suy ra | Bước 3 thao tác trên tài khoản của chính mình ⇒ cần đã đăng nhập |
| FR-M01-03.10 | DEC-015 | Nói thẳng | "display_name shown everywhere" |
| FR-M01-03.11 | DEC-148 | Nói thẳng | — |
| FR-M01-03.12 | DEC-148 | Nói thẳng | — |
| FR-M01-03.13 | DEC-148 | Nói thẳng | — |
| FR-M01-03.14 | DEC-148 | Nói thẳng | Không nhận emoji và ký hiệu khác |
| FR-M01-03.15 | DEC-148 | Nói thẳng | — |
| FR-M01-03.16 | DEC-148 | Nói thẳng | — |
| FR-M01-04 | DEC-010, DEC-014, DEC-018, QA-053, QA-011, MR-M01, DEC-065 | Nói thẳng | Gồm tự liên kết theo email đã xác minh; thông báo sau liên kết theo Q-01 |
| FR-M01-04.01 | DEC-014, DEC-018 | Nói thẳng | Điều kiện "email chưa thuộc tài khoản nào" suy ra từ DEC-010 |
| FR-M01-04.02 | QA-053, DEC-014 | Nói thẳng | — |
| FR-M01-04.03 | DEC-014, QA-053 | Nói thẳng | — |
| FR-M01-04.04 | DEC-010, DEC-147 | Nói thẳng | — |
| FR-M01-04.05 | DEC-010, DEC-147 | Nói thẳng | — |
| FR-M01-04.06 | DEC-018, DEC-014 | Suy ra | Cổng đăng nhập áp dụng cho mọi lần đăng nhập; DEC-018 nêu riêng mức xác minh của tài khoản Google |
| FR-M01-04.07 | DEC-138 | Suy ra | BR-M01-03: "cannot register unless they explicitly consent" ⇒ áp dụng cả khi tạo bằng Google |
| FR-M01-04.08 | DEC-017 | Suy ra | Mỗi lần đăng nhập trên một thiết bị là một phiên riêng |
| FR-M01-04.09 | DEC-147 | Nói thẳng | — |
| FR-M01-04.10 | DEC-152 | Nói thẳng | — |
| FR-M01-04.11 | DEC-152 | Nói thẳng | — |
| FR-M01-04.12 | DEC-157, DEC-138 | Suy ra | BR-M01-03 áp dụng cho mọi cách tạo tài khoản; DEC-157 quy định nội dung ô đồng ý |
| FR-M01-04.13 | DEC-155 | Nói thẳng | — |
| FR-M01-05 | DM-1.1, DEC-014, DEC-018, DEC-019, DEC-085, QA-018, QA-011, DEC-086 | Nói thẳng | Gồm cổng đăng nhập và màn hình tài khoản bị khóa |
| FR-M01-05.01 | DEC-018 | Nói thẳng | — |
| FR-M01-05.02 | DM-1.1 | Suy ra | Đăng nhập bằng email và mật khẩu ⇒ sai thông tin bị từ chối |
| FR-M01-05.03 | DEC-018 | Nói thẳng | — |
| FR-M01-05.04 | QA-018, DEC-065 | Nói thẳng | QA-018 "Login khi DEACTIVATED không tự kích hoạt lại"; DEC-065 "can't login" |
| FR-M01-05.05 | DEC-085, QA-019 | Nói thẳng | — |
| FR-M01-05.06 |  DEC-085, DEC-152  | Nói thẳng | — |
| FR-M01-05.07 | DEC-019, DEC-085 | Nói thẳng | — |
| FR-M01-05.08 | DEC-019, DEC-085, DEC-086 | Nói thẳng | Thời hạn khiếu nại theo DEC-086 (M09) |
| FR-M01-05.09 | DEC-019 | Nói thẳng | "appeal button (if within window)" |
| FR-M01-05.10 | DEC-014 | Nói thẳng | — |
| FR-M01-05.11 | DEC-014 | Nói thẳng | — |
| FR-M01-05.12 | DEC-014, DEC-017 | Nói thẳng | — |
| FR-M01-05.13 | DEC-016 | Suy ra | Tài khoản Google không có chức năng mật khẩu (BR-M01-15) ⇒ không đăng nhập bằng mật khẩu được |
| FR-M01-05.14 | QA-018, QA-019 | Nói thẳng | Thao tác ban thuộc M08; M01 giữ trạng thái tài khoản |
| FR-M01-05.15 | QA-018, QA-019 | Nói thẳng | Thao tác gỡ ban thuộc M08 |
| FR-M01-05.16 | DEC-089 | Nói thẳng | Việc duyệt khiếu nại thuộc M09 |
| FR-M01-05.17 | DEC-152 | Nói thẳng | — |
| FR-M01-05.18 | DEC-152 | Nói thẳng | — |
| FR-M01-05.19 | DEC-152 | Nói thẳng | — |
| FR-M01-05.20 | DEC-152 | Nói thẳng | — |
| FR-M01-06 | DEC-017, MR-M01 | Nói thẳng | — |
| FR-M01-06.01 | DEC-017 | Nói thẳng | — |
| FR-M01-06.02 | DEC-017 | Nói thẳng | — |
| FR-M01-06.03 | DEC-017 | Suy ra | "old invalidated" ⇒ dùng lại bị từ chối |
| FR-M01-06.04 | DEC-017, DEC-151 | Suy ra | Hạn 30 ngày tính từ lúc cấp (FR-M01-06.07) ⇒ quá hạn bị từ chối |
| FR-M01-06.05 | DEC-017 | Nói thẳng | — |
| FR-M01-06.06 | DEC-017 | Suy ra | "each device independent" ⇒ phiên của thiết bị này không ảnh hưởng thiết bị khác |
| FR-M01-06.07 | DEC-151 | Nói thẳng | — |
| FR-M01-07 | DM-1.1 | Nói thẳng | Chỉ draft nói tới đăng xuất |
| FR-M01-07.01 | DM-1.1, DEC-017 | Suy ra | Draft có Logout; mỗi thiết bị một phiên ⇒ đăng xuất kết thúc phiên của thiết bị đó |
| FR-M01-07.02 | DEC-017 | Suy ra | "each device independent" |
| FR-M01-08 | DM-1.1, DEC-016, DEC-065 | Nói thẳng | — |
| FR-M01-08.01 | DEC-016 | Nói thẳng | — |
| FR-M01-08.02 | DEC-016 | Suy ra | Cần mật khẩu cũ ⇒ sai bị từ chối |
| FR-M01-08.03 | DEC-016 | Suy ra | Có trường nhập lại ⇒ không khớp bị từ chối |
| FR-M01-08.04 | DEC-016 | Nói thẳng | — |
| FR-M01-08.05 | DEC-065 | Nói thẳng | — |
| FR-M01-08.06 | DEC-016 | Nói thẳng | "Google OAuth accounts: no password flow" |
| FR-M01-08.07 | DEC-016 | Suy ra | Đổi mật khẩu "logged in" ⇒ chưa đăng nhập bị từ chối |
| FR-M01-08.08 | DEC-148 | Nói thẳng | — |
| FR-M01-08.09 | DEC-148 | Nói thẳng | — |
| FR-M01-08.10 | DEC-151 | Nói thẳng | — |
| FR-M01-09 | DM-1.1, DEC-016, QA-061, MR-M01 | Nói thẳng | — |
| FR-M01-09.01 |  DEC-016, DEC-151  | Nói thẳng | — |
| FR-M01-09.02 | DEC-016 | Nói thẳng | — |
| FR-M01-09.03 | DEC-016 | Nói thẳng | — |
| FR-M01-09.04 | DEC-016 | Nói thẳng | — |
| FR-M01-09.05 | DEC-016 | Suy ra | Hạn 15 phút ⇒ quá hạn bị từ chối |
| FR-M01-09.06 | DEC-016 | Suy ra | Có trường nhập lại ⇒ không khớp bị từ chối |
| FR-M01-09.07 | QA-061, DEC-016 | Nói thẳng | — |
| FR-M01-09.08 | DEC-148 | Nói thẳng | — |
| FR-M01-09.09 | DEC-148 | Nói thẳng | — |
| FR-M01-09.10 | DEC-151 | Nói thẳng | — |
| FR-M01-09.11 | DEC-151 | Nói thẳng | — |
| FR-M01-09.12 | DEC-151 | Nói thẳng | — |
| FR-M01-09.13 | DEC-151 | Nói thẳng | Tài khoản Google (FR-M01-09.07) và DEACTIVATED (FR-M01-09.15) có cách xử lý riêng |
| FR-M01-09.14 | DEC-151 | Suy ra | Không có tài khoản ⇒ không có gì để đặt lại; email của tài khoản DELETED đã được giải phóng (DEC-148) |
| FR-M01-09.15 | DEC-151 | Nói thẳng | — |
| FR-M01-09.16 | DEC-151, DEC-085 | Nói thẳng | Ngoại lệ hẹp để giữ quyền khiếu nại; sau khi đặt lại vẫn chỉ có màn hình bị khóa (FR-M01-05.05, FR-M01-05.06) |
| FR-M01-10 | DEC-019, QA-018, MR-M01 | Nói thẳng | — |
| FR-M01-10.01 | DEC-019, QA-018 | Nói thẳng | — |
| FR-M01-10.02 | QA-018, DEC-065 | Suy ra | Tài khoản DEACTIVATED không đăng nhập được ⇒ phiên đang có phải kết thúc |
| FR-M01-10.03 | DEC-019, QA-018 | Nói thẳng | — |
| FR-M01-10.04 | QA-018, DEC-019 | Suy ra | QA-018 "Admin/Mod không có quyền xóa tài khoản"; vô hiệu hóa dẫn tới tự xóa ⇒ chỉ chủ tài khoản (đã xác nhận ở bước 3) |
| FR-M01-10.05 | DEC-085 | Suy ra | Tài khoản BANNED chỉ gửi được khiếu nại ⇒ thao tác khác bị từ chối |
| FR-M01-10.06 | DEC-019 | Suy ra | Vô hiệu hóa tài khoản của mình ⇒ cần đã đăng nhập |
| FR-M01-10.07 | DEC-149 | Nói thẳng | — |
| FR-M01-11 | QA-018, DEC-019 | Nói thẳng | Chỉ QA-018 nói cách kích hoạt lại (OTP email); DEC-019 nói thời hạn 14 ngày |
| FR-M01-11.01 | QA-018, DEC-149 | Nói thẳng | — |
| FR-M01-11.02 | QA-018, DEC-019, DEC-149 | Nói thẳng | — |
| FR-M01-11.03 | DEC-019 | Suy ra | BR-M01-25: "accidental deactivation recovery" ⇒ khôi phục hiển thị như trước |
| FR-M01-11.04 | QA-018 | Suy ra | Cần xác nhận mã ⇒ mã sai bị từ chối |
| FR-M01-11.05 | QA-018, DEC-019, DEC-149 | Suy ra | Kích hoạt lại chỉ trong 14 × 24 giờ; DELETED không quay lại ⇒ quá hạn bị từ chối |
| FR-M01-11.06 | DEC-149 | Nói thẳng | — |
| FR-M01-11.07 | DEC-149 | Nói thẳng | — |
| FR-M01-11.08 | DEC-149 | Nói thẳng | — |
| FR-M01-11.09 | DEC-149 | Nói thẳng | — |
| FR-M01-11.10 | DEC-149, QA-018 | Suy ra | Chỉ tài khoản DEACTIVATED được kích hoạt lại ⇒ email khác không nhận mã |
| FR-M01-12 | DEC-019, QA-018, DEC-129, DEC-065, MR-M01 | Nói thẳng | Gồm xóa dữ liệu cá nhân; email cảnh báo trước khi tự xóa do M07 gửi |
| FR-M01-12.01 | DEC-019, QA-018, DEC-149 | Nói thẳng | — |
| FR-M01-12.02 | DEC-019, DEC-129, DEC-156 | Nói thẳng | Danh mục cụ thể ở FR-M01-12.08 |
| FR-M01-12.03 | QA-018 | Nói thẳng | "Xóa tài khoản = soft delete, không hard delete" |
| FR-M01-12.04 | QA-018 | Nói thẳng | "DELETED (auto, vĩnh viễn)" |
| FR-M01-12.05 | DEC-065, DEC-149 | Nói thẳng | Không có thông báo trong ứng dụng vì tài khoản không đăng nhập được |
| FR-M01-12.06 | DEC-148 | Nói thẳng | — |
| FR-M01-12.07 | DEC-148 | Nói thẳng | — |
| FR-M01-12.08 | DEC-156, DEC-159, DEC-215 | Nói thẳng | — |
| FR-M01-12.09 | DEC-156 | Nói thẳng | — |
| FR-M01-12.10 | DEC-156, DEC-129 | Nói thẳng | — |
| FR-M01-12.11 | DEC-159 | Nói thẳng | — |
| FR-M01-13 | DEC-019, QA-066, QA-018 | Nói thẳng | Phần bình luận sau khi xóa theo Q-02 |
| FR-M01-13.01 |  DEC-019, QA-066, DEC-150  | Nói thẳng | — |
| FR-M01-13.02 | DEC-019 | Nói thẳng | — |
| FR-M01-13.03 | DEC-019 | Nói thẳng | — |
| FR-M01-13.04 | DEC-019, QA-066, DEC-149 | Nói thẳng | — |
| FR-M01-13.05 | DEC-150 | Nói thẳng | — |
| FR-M01-13.06 | DEC-156 | Nói thẳng | — |
| FR-M01-14 | DEC-020, DEC-015, DEC-045, MR-M01 | Nói thẳng | — |
| FR-M01-14.01 | DEC-020 | Nói thẳng | — |
| FR-M01-14.02 | DEC-020, DEC-148, DEC-214 | Nói thẳng | — |
| FR-M01-14.03 | DEC-020, DEC-015 | Nói thẳng | — |
| FR-M01-14.04 | DEC-020 | Nói thẳng | — |
| FR-M01-14.05 | DEC-020 | Nói thẳng | — |
| FR-M01-14.06 | DEC-020 | Nói thẳng | — |
| FR-M01-14.07 | DEC-020 | Nói thẳng | — |
| FR-M01-14.08 | DEC-020 | Nói thẳng | — |
| FR-M01-14.09 | DEC-020 | Nói thẳng | — |
| FR-M01-14.10 | DEC-045, DEC-070, DEC-153 | Nói thẳng | Việc gửi do M07 thực hiện |
| FR-M01-14.11 | QA-011 | Suy ra | Guest không đăng bài, bình luận ⇒ không nhắc tên |
| FR-M01-14.12 | DEC-153 | Nói thẳng | — |
| FR-M01-14.13 | DEC-153 | Nói thẳng | — |
| FR-M01-14.14 | DEC-153 | Nói thẳng | — |
| FR-M01-14.15 | DEC-153 | Nói thẳng | — |
| FR-M01-14.16 | DEC-153 | Nói thẳng | — |
| FR-M01-14.17 | DEC-153 | Nói thẳng | — |
| FR-M01-15 | DEC-131, DEC-138, DEC-154 | Nói thẳng | Lý do lấy từ DEC-131, DEC-138 |
| FR-M01-15.01 | DEC-131 | Nói thẳng | "A public Privacy Policy / Terms of Service page" |
| FR-M01-15.02 | DEC-154 | Nói thẳng | — |
| FR-M01-15.03 | DEC-154 | Nói thẳng | — |
| FR-M01-15.04 | DEC-154 | Nói thẳng | Phần "Gợi ý topic" do DEC-146 (M05) đặt, DEC-154 giữ lại |
| FR-M01-15.05 | DEC-154 | Nói thẳng | — |
| FR-M01-15.06 | DEC-156 | Nói thẳng | — |
| FR-M01-15.07 | DEC-155, DEC-157 | Nói thẳng | — |
| FR-M01-15.08 | DEC-155 | Suy ra | "records the time and the policy version" ⇒ mỗi bản nội dung có một phiên bản |
| FR-M01-15.09 | DEC-158 | Nói thẳng | — |
| FR-M01-16 |  DEC-155, DEC-158  | Nói thẳng | — |
| FR-M01-16.01 |  DEC-155, DEC-158  | Nói thẳng | — |
| FR-M01-16.02 | DEC-155 | Nói thẳng | — |
| FR-M01-16.03 | DEC-155 | Nói thẳng | — |
| FR-M01-16.04 |  DEC-155, DEC-158  | Nói thẳng | — |
| FR-M01-16.05 | DEC-155 | Nói thẳng | "only when the policy changes to a new version" |
| BR-M01-01 | DEC-001, DG-2, DG-8, DEC-007 | Suy ra | Vai trò MOD, ADMIN chỉ có qua cấp quyền (M10, DEC-007) ⇒ tài khoản mới có vai trò USER |
| BR-M01-02 | DEC-014, DEC-018, DM-1.1 | Nói thẳng | — |
| BR-M01-03 | DEC-138, DEC-131 | Suy ra | DEC-138 "cannot register unless they explicitly consent" ⇒ áp dụng cho mọi cách tạo tài khoản, kể cả Google |
| BR-M01-04 | DEC-010 | Suy ra | DEC-010 liên kết theo email để "tránh duplicate" ⇒ một email chỉ thuộc một tài khoản |
| BR-M01-05 | DEC-015, DEC-014, DEC-148 | Nói thẳng | — |
| BR-M01-06 | DEC-015, DEC-014, DEC-148 | Nói thẳng | — |
| BR-M01-07 | DEC-015, DEC-023, DEC-020 | Nói thẳng | Địa chỉ trang hồ sơ theo DEC-023 |
| BR-M01-08 | DEC-014, DEC-018, QA-053 | Nói thẳng | Điều kiện "email chưa thuộc tài khoản nào" suy ra từ DEC-010 (email trùng thì liên kết) |
| BR-M01-09 | DEC-010, DEC-147 | Nói thẳng | — |
| BR-M01-10 | DEC-014, DEC-016 | Nói thẳng | — |
| BR-M01-11 | DEC-016 | Nói thẳng | — |
| BR-M01-12 | DEC-016 | Nói thẳng | — |
| BR-M01-13 | DEC-016 | Nói thẳng | — |
| BR-M01-14 | DEC-016 | Nói thẳng | — |
| BR-M01-15 | DEC-016, QA-061 | Nói thẳng | — |
| BR-M01-16 | DEC-017, DEC-151 | Nói thẳng | — |
| BR-M01-17 | DEC-017 | Nói thẳng | — |
| BR-M01-18 | DEC-018, DEC-085, DEC-014, QA-018, DEC-065 | Nói thẳng | DEACTIVATED bị từ chối: QA-018, DEC-065 "can't login"; BANNED theo DEC-085 |
| BR-M01-19 | DEC-085, DEC-019, DEC-086 | Nói thẳng | Thời hạn khiếu nại theo DEC-086 (M09) |
| BR-M01-20 | DEC-019, QA-018 | Nói thẳng | Phần Mod, Admin không vô hiệu hóa tài khoản người khác là suy ra (bước 3) |
| BR-M01-21 | DEC-019, QA-018, DEC-129, DEC-148, DEC-149 | Nói thẳng | — |
| BR-M01-22 | QA-018, DEC-019, DEC-149 | Nói thẳng | — |
| BR-M01-23 | DEC-019 | Nói thẳng | — |
| BR-M01-24 | DEC-019, QA-066, DEC-149 | Nói thẳng | — |
| BR-M01-25 | DEC-019, QA-018 | Suy ra | DEC-019 "14 days sufficient for accidental deactivation recovery" ⇒ kích hoạt lại khôi phục hiển thị như trước |
| BR-M01-26 | DEC-020, DEC-214 | Nói thẳng | — |
| BR-M01-27 | DEC-020, DEC-153 | Nói thẳng | — |
| BR-M01-28 | DEC-020 | Nói thẳng | — |
| BR-M01-29 | DEC-020 | Nói thẳng | — |
| BR-M01-30 | DEC-045, DEC-070, DEC-153 | Nói thẳng | — |
| BR-M01-31 | DEC-065 | Nói thẳng | — |
| BR-M01-32 | DEC-065, DEC-149 | Nói thẳng | — |
| BR-M01-33 | DEC-092, DEC-152 | Nói thẳng | — |
| BR-M01-34 | QA-019, DEC-089, DEC-152 | Nói thẳng | — |
| BR-M01-35 | DEC-148 | Nói thẳng | — |
| BR-M01-36 | DEC-148, DEC-151 | Nói thẳng | — |
| BR-M01-37 | DEC-152 | Nói thẳng | — |
| BR-M01-38 | DEC-151 | Nói thẳng | — |
| BR-M01-39 | DEC-151 | Nói thẳng | — |
| BR-M01-40 | DEC-153 | Nói thẳng | — |
| BR-M01-41 | DEC-150 | Nói thẳng | — |
| BR-M01-42 | DEC-154 | Nói thẳng | — |
| BR-M01-43 | DEC-154 | Nói thẳng | — |
| BR-M01-44 |  DEC-155, DEC-158  | Nói thẳng | — |
| BR-M01-45 |  DEC-155, DEC-158  | Nói thẳng | — |
| BR-M01-46 | DEC-157 | Nói thẳng | — |
| BR-M01-47 | DEC-156, DEC-159, DEC-148, DEC-149, DEC-129, DEC-215 | Nói thẳng | — |

## Phụ lục B. Câu hỏi, giả định và TBD

### B.1 Câu hỏi đã hỏi

| Mã | Loại | Câu hỏi | Trả lời | Ghi vào register |
|---|---|---|---|---|
| Q-01 | Mâu thuẫn | Khi tài khoản Google được tự liên kết vào tài khoản đã đăng ký cùng email, hệ thống có gửi thông báo cho người dùng không, và gửi qua kênh nào? DEC-010 nói có gửi; danh sách sự kiện đầy đủ của DEC-065 không có sự kiện này. | A — giữ thông báo, gửi trong ứng dụng và email, cùng nhóm bảo mật với đổi mật khẩu. | QA-292, DEC-147 |
| Q-02 | Mâu thuẫn | Bình luận của tài khoản đã chuyển sang DELETED hiển thị thế nào: giữ nội dung và chỉ đổi tên tác giả thành "[Người dùng đã xóa]" (cách đọc DEC-019, QA-066), hay thay cả nội dung bằng "[Bình luận từ tài khoản đã xóa]" (QA-018)? | A — giữ nội dung, tên tác giả "[Người dùng đã xóa]", avatar mặc định. | QA-293, DEC-149 |
| Q-03 | Cần cân nhắc | (Mở rộng phạm vi) Khi tác giả vô hiệu hóa tài khoản, bài viết bị ẩn và tên trên bình luận bị thay bằng "Tài khoản tạm thời vô hiệu hoá". Mod, Admin có xem được bài viết bị ẩn và danh tính thật của tác giả (ví dụ khi xử lý báo cáo về bình luận đó) không? | A — có, trong khi tài khoản DEACTIVATED (mở rộng phạm vi, đã chấp nhận; CC-01). | QA-294, DEC-150 |
| Q-04 | Thiếu chi tiết | Mật khẩu khi đăng ký, đổi và đặt lại có quy tắc gì: độ dài tối thiểu, tối đa, có bắt buộc chữ hoa, chữ số, ký tự đặc biệt không? | 8–64 ký tự; nhận mọi ký tự, không bắt buộc loại ký tự, không cắt khoảng trắng; mật khẩu mới khác mật khẩu hiện tại. | QA-295, DEC-148 |
| Q-05 | Mơ hồ | username "alphanumeric + underscore": có nhận chữ tiếng Việt có dấu không ("đức_pv")? So trùng có phân biệt chữ hoa, chữ thường không ("Duc_PV" và "duc_pv")? display_name có giới hạn độ dài, có được để toàn khoảng trắng không? | username chỉ a–z, A–Z, 0–9, "_"; so trùng không phân biệt hoa thường, hiển thị giữ nguyên. display_name 1–50 ký tự, chữ (có dấu), số, khoảng trắng, . , - _ ' ( ); không emoji. | QA-296, DEC-148 |
| Q-06 | Thiếu chi tiết | Đăng nhập Google mà email Google trùng một tài khoản email chưa xác minh (mức NONE) thì xử lý thế nào? | A — vẫn liên kết, chuyển email thành đã xác minh (chấp nhận rủi ro). | QA-297, DEC-147 |
| Q-07 | Mơ hồ | Phiên làm mới 30 ngày, xoay vòng: phiên làm mới mới có hạn 30 ngày tính từ lúc làm mới, hay giữ hạn của lần đăng nhập đầu? Ví dụ đăng nhập 01/10, làm mới ngày 25/10: hết hạn 24/11 hay 31/10? | 30 ngày tính lại từ mỗi lần làm mới. | QA-298, DEC-151 |
| Q-08 | Mơ hồ | Thời hạn vô hiệu hóa 14 ngày tính thế nào? Ví dụ vô hiệu hóa 01/10 lúc 21:00: chuyển DELETED lúc 15/10 21:00 (đủ 14 × 24 giờ), hay ngay đầu ngày 15/10, hay hết ngày 15/10? | Đủ 14 × 24 giờ từ lúc vô hiệu hóa. | QA-299, DEC-149 |
| Q-09 | Thiếu chi tiết | Mã kích hoạt lại: hạn dùng bao lâu, được nhập sai bao nhiêu lần, gửi lại được không và cách nhau bao lâu? Ở trang kích hoạt, người dùng xác định tài khoản bằng gì (email, hay email và mật khẩu)? Kích hoạt lại xong có được đăng nhập luôn không? | Chỉ nhập email; mã 6 chữ số, hạn 15 phút, sai tối đa 5 lần, xin lại cách 60 giây; kích hoạt xong đăng nhập luôn. | QA-300, DEC-149 |
| Q-10 | Thiếu chi tiết | Danh sách gợi ý nhắc tên: trong cùng một tầng ưu tiên xếp theo gì; khi nhắc tên trong bình luận thì dùng ngữ cảnh của bài viết chứa bình luận phải không; tài khoản DEACTIVATED, DELETED, BANNED có hiện trong danh sách không, và lượt nhắc tên đã có tới những tài khoản đó hiển thị thế nào? Thông báo nhắc tên gửi lúc nội dung được gửi hay lúc nội dung được đăng công khai, và sửa nội dung có gửi lại không? | Trong tầng xếp theo mức khớp; bình luận dùng ngữ cảnh bài; không hiện DEACTIVATED, DELETED, BANNED, chưa xong bước 3; nhắc cũ hiện tên thay thế, không mở trang hồ sơ; thông báo khi nội dung công khai, sửa chỉ báo người mới. | QA-301, DEC-153 |
| Q-11 | Thiếu chi tiết | Email cảnh báo trước khi tự xóa gửi lúc nào (ví dụ trước 1 ngày, hay ngay khi vô hiệu hóa)? Đặt lại mật khẩu qua "Quên mật khẩu" có gửi thông báo "mật khẩu đã đổi" như đổi mật khẩu không? | Email cảnh báo một lần, 24 giờ trước khi xóa; đặt lại mật khẩu cũng gửi "mật khẩu đã đổi". | QA-302, DEC-149, DEC-151 |
| Q-12 | Thiếu chi tiết | Khi công tắc tạm dừng đăng ký bật: đăng nhập Google lần đầu (sẽ tạo tài khoản mới) có bị chặn không; tài khoản đã qua bước 1 có tiếp tục bước 2, 3 được không? Khi bật chế độ bảo trì, người không phải Admin có đăng nhập được không? | Tạm dừng đăng ký chặn cả tài khoản Google mới, liên kết vẫn được, đăng ký dở làm tiếp được; bảo trì chỉ ADMIN đăng nhập và thao tác. | QA-303, DEC-152 |
| Q-13 | Thiếu chi tiết | Ban tạm thời (30 hoặc 90 ngày) hết hạn thì tài khoản tự trở về ACTIVE ngay lúc hết hạn phải không? | Có, tự về ACTIVE ngay lúc hết hạn. | QA-304, DEC-152 |
| Q-14 | Thiếu chi tiết | Sau khi thiết lập xong, người dùng có đổi được username, display_name không (DEC-026 ngụ ý username đổi được), nếu có thì ở đâu và có giới hạn gì? Username và email của tài khoản đã DELETED có được tài khoản mới dùng lại không? | Đổi được cả hai ở trang sửa hồ sơ, không giới hạn; username cũ giải phóng khi đổi. DELETED: email giải phóng, username giữ vĩnh viễn. | QA-305, DEC-148 |
| Q-15 | Thiếu chi tiết | Magic link (xác minh email, đặt lại mật khẩu) dùng được một lần hay nhiều lần trong hạn? Gửi link mới thì link cũ còn hiệu lực không? | Một lần; gửi link mới thì link cũ mất hiệu lực. | QA-306, DEC-151 |
| Q-16 | Thiếu chi tiết | Trên màn hình tài khoản bị khóa, bấm nút OK thì hệ thống làm gì (đăng xuất, hay ở lại màn hình)? | Đăng xuất. | QA-307, DEC-152 |
| Q-17 | Thiếu chi tiết | Ở "Quên mật khẩu": nhập email không thuộc tài khoản nào thì hệ thống báo gì? Tài khoản DEACTIVATED, BANNED, DELETED có dùng được "Quên mật khẩu" không? | Câu chung "Liên kết đã được gửi, vui lòng kiểm tra email của bạn"; DEACTIVATED hướng tới trang kích hoạt; BANNED được đặt lại để vào màn hình bị khóa và khiếu nại. | QA-308, DEC-151 |
| Q-18 | Thiếu chi tiết | (Quyền riêng tư P1) Danh mục dữ liệu cá nhân và cách trình bày trên trang Privacy Policy? | Bốn nhóm, không liệt kê chi tiết, gộp tài khoản và hồ sơ, không nêu phiên đăng nhập. | QA-309, DEC-154 |
| Q-19 | Thiếu chi tiết | (P1b) Có lưu việc đồng ý, khi nào phải đồng ý lại? | Lưu thời điểm và phiên bản; chỉ đồng ý lại khi chính sách đổi phiên bản. | QA-310, DEC-155 |
| Q-20 | Thiếu chi tiết | (P2) Khi DELETED xóa gì, giữ gì? | Theo đề xuất (BR-M01-47). | QA-311, DEC-156 |
| Q-21 | Thiếu chi tiết | (P3) Tin nhắn và nhật ký của người đã xóa tài khoản? | A — giữ nội dung, người gửi "[Người dùng đã xóa]", nhật ký tra cứu qua username. | QA-312, DEC-156 |
| Q-22 | Thiếu chi tiết | (Nhóm 4) Nêu việc xử lý bởi AI thế nào? | "Xử lý bởi nhà cung cấp dịch vụ AI", không nêu tên. | QA-313, DEC-154 |
| Q-23 | Thiếu chi tiết | (P6, P7) Cơ sở xử lý và các mục của trang? | Theo đề xuất; email liên hệ chốt khi triển khai. | QA-314, DEC-154 |
| Q-24 | Cần cân nhắc | (P4, mở rộng phạm vi) Có chức năng tải bản sao dữ liệu, rút lại đồng ý thế nào? | Không làm chức năng ở MS1; rút lại đồng ý bằng vô hiệu hóa. | QA-315, DEC-155, DEC-157 |
| Q-25 | Cần cân nhắc | (P5) Người dùng dưới 16 tuổi? | A — tự cam kết trong ô đồng ý, không hỏi tuổi. | QA-316, DEC-157 |
| Q-26 | Mơ hồ | "Đồng ý lại ở lần đăng nhập kế tiếp": người đang giữ phiên đăng nhập (phiên làm mới 30 ngày) có được hỏi ngay khi mở ứng dụng, hay chỉ khi đăng nhập lại? | A — hỏi ở lần mở ứng dụng kế tiếp, kể cả khi đang giữ phiên đăng nhập. | QA-317, DEC-158 |
| Q-27 | Thiếu chi tiết | Ai phát hành phiên bản chính sách mới và bằng cách nào (Admin trên giao diện, hay đội phát triển khi triển khai bản mới)? | A — đội phát triển, khi triển khai bản mới; không có màn hình Admin. | QA-318, DEC-158 |
| Q-28 | Thiếu chi tiết | (Đối chiếu M05) Lượt theo dõi Topic, bài viết của tài khoản đã xóa? | Xóa cùng các quan hệ theo dõi khác. | QA-319, DEC-159 |
| Q-29 | Thiếu chi tiết | (Đối chiếu M05) Phản hồi gợi ý Topic của tài khoản đã xóa? | Giữ như nhật ký AI, không gắn danh tính. | QA-320, DEC-159 |

### B.2 TBD

| ID | Nội dung | Ảnh hưởng | Lý do chưa chốt |
|---|---|---|---|
| TBD-M01-01 | Email liên hệ trên trang Privacy Policy/ToS và cách người dùng yêu cầu bản sao dữ liệu. | Thấp | OPEN-008 (đã thu hẹp bởi DEC-154–157) hoãn có chủ đích, chốt khi triển khai. |

### B.3 Cần cân nhắc (ngoài dữ liệu hiện có)

| Mã | Điểm cần cân nhắc | Vì sao cần | Quyết định |
|---|---|---|---|
| CC-01 | Mod, Admin xem bài viết bị ẩn và danh tính thật của tác giả đã vô hiệu hóa tài khoản (Q-03) | Chạm tới quyền: nếu không có, vô hiệu hóa tài khoản thành cách né xử lý vi phạm | Chấp nhận — DEC-150 (FR-M01-13.05) |
| CC-02 | Liên kết Google vào tài khoản email chưa xác minh (Q-06) | Chạm tới an toàn tài khoản: người đăng ký trước bằng email của người khác giữ được mật khẩu | Chấp nhận rủi ro, ưu tiên thuận tiện — DEC-147 (FR-M01-04.04, FR-M01-04.09) |

## Phụ lục C. Sổ nguồn

**Owner keywords:** M01, đăng ký, register, registration, onboarding, đăng nhập, login, logout, đăng xuất, mật khẩu, password, forgot password, quên mật khẩu, change password, đổi mật khẩu, magic link, OTP, verify email, email verification, xác thực email, xác minh email, verify_level, EMAIL_VERIFIED, SETUP_COMPLETED, OAuth, Google OAuth, account linking, auto-link, JWT, refresh token, access token, refresh_tokens, session, multi-device, account_state, DEACTIVATED, deactivate, deactivated, deactivation, vô hiệu hoá, vô hiệu hóa, DELETED, username, display_name, mention, @mention, tombstone, PII, tài khoản, account, xóa tài khoản, login gate, temporary ban, permanent ban
**Dependency keywords:** profile, hồ sơ, avatar, bio, grade_level, BANNED, ban, appeal, khiếu nại, notification, thông báo, email, SSE, post, bài viết, comment, admin, role, MODERATOR, maintenance, Privacy Policy, ToS, timezone, audit log, consent, guest
**Mục draft của module:** DM-1 (gồm DM-1.1–1.3)
**Loại khỏi bảng nguồn (khớp nhầm):** DEC-011, DEC-012, DEC-021, DEC-031, DEC-038, DEC-105, DEC-113, DEC-141, DEC-145, DM-2.1, QA-028, QA-071, QA-082, QA-097, F-POST-06 ("deleted" của bài viết, bình luận, group, Topic, avatar); DEC-043, ISS-074, ISS-158, QA-214 ("tombstone" của bình luận, tin nhắn); DEC-081, ISS-216, QA-276 ("vô hiệu hóa" Tag); DG-x01 ("đăng ký đồ án"); QA-257, QA-265 ("register" là tệp register); QA-258 (mật khẩu SMTP); QA-015 (Anonymous Post, "account" chỉ nhắc qua)

### C.1 Bảng nguồn

| Nguồn | Nhãn | Trạng thái | Dùng ở | Ghi chú |
|---|---|---|---|---|
| DM-1 | Nhắc tới | Hiện hành | Không áp dụng: Tiêu đề mục draft "User Module" | Nhóm A. Tiêu đề mục draft "User Module" |
| DM-1.1 | Sở hữu | Hiện hành | FR-M01-01, FR-M01-02, FR-M01-05, FR-M01-05.02, FR-M01-07, FR-M01-07.01, FR-M01-08, FR-M01-09, BR-M01-02 | Nhóm A. Draft: Register, Login/Logout, Forgot/Change password, Email verification |
| DM-1.2 | Phụ thuộc | Hiện hành | Chuyển M02, M01 | Nhóm A. Chuyển M02. Draft xếp Username vào Profile; register đặt username ở M01 (DEC-014, DEC-015) |
| DM-1.3 | Phụ thuộc | Hiện hành | Chuyển M10 | Nhóm A. Vai trò USER/MOD/ADMIN; quản lý vai trò thuộc M10, quyền thuộc từng module |
| ISS-054 | Nhắc tới | Hiện hành | Không áp dụng: Đã có QA-048–QA-056 | Nhóm A. Đã có QA-048–QA-056 |
| ISS-055 | Nhắc tới | Hiện hành | Không áp dụng: Đã có QA-057, QA-058 | Nhóm A. Đã có QA-057, QA-058 |
| ISS-056 | Nhắc tới | Hiện hành | Không áp dụng: Đã có QA-059–QA-061 | Nhóm A. Đã có QA-059–QA-061 |
| ISS-057 | Nhắc tới | Hiện hành | Không áp dụng: Đã có QA-062–QA-066 | Nhóm A. Đã có QA-062–QA-066 |
| QA-048 | Sở hữu | Trùng với DEC-014 | — | Nhóm A. Trường bắt buộc khi đăng ký |
| QA-049 | Sở hữu | Trùng với DEC-014, DEC-018 | — | Nhóm A. Xác minh email bắt buộc; Google coi như đã xác minh |
| QA-050 | Sở hữu | Trùng với DEC-015 | — | Nhóm A. display_name tự do, không duy nhất |
| QA-051 | Sở hữu | Trùng với DEC-015 | — | Nhóm A. username duy nhất, 3–20 ký tự |
| QA-052 | Sở hữu | Trùng với DEC-015 | — | Nhóm A. Chỉ username duy nhất |
| QA-053 | Sở hữu | Hiện hành | FR-M01-03, FR-M01-04, FR-M01-04.02, FR-M01-04.03, BR-M01-08 | Nhóm A. Tài khoản Google vẫn phải đặt username. Cùng nội dung DEC-014, thêm ý display_name lấy từ Google đổi được — giữ Hiện hành |
| QA-054 | Sở hữu | Trùng với DEC-020 | — | Nhóm A. @mention: tìm theo cả hai trường, ưu tiên theo ngữ cảnh. DEC-214 sửa phần khớp tên |
| QA-055 | Sở hữu | Trùng với DEC-020 | — | Nhóm A. @mention: hiển thị, lưu theo người dùng |
| QA-056 | Sở hữu | Trùng với DEC-020 | — | Nhóm A. @mention: nhãn không sửa được |
| QA-057 | Sở hữu | Trùng với DEC-017 | — | Nhóm A. Thời hạn phiên, token làm mới xoay vòng |
| QA-058 | Sở hữu | Trùng với DEC-017 | — | Nhóm A. Nhiều thiết bị; phần SSE là kỹ thuật |
| QA-059 | Sở hữu | Trùng với DEC-016 | — | Nhóm A. Đổi mật khẩu khi đã đăng nhập |
| QA-060 | Sở hữu | Trùng với DEC-016 | — | Nhóm A. Quên mật khẩu |
| QA-061 | Sở hữu | Hiện hành | FR-M01-09, FR-M01-09.07, BR-M01-15 | Nhóm A. Tài khoản Google bấm Quên mật khẩu. Cùng nội dung DEC-016, thêm câu thông báo cụ thể — giữ Hiện hành |
| QA-062 | Sở hữu | Trùng với DEC-018 | — | Nhóm A. Hai trường trạng thái; thứ tự kiểm khi đăng nhập |
| QA-063 | Sở hữu | Trùng với DEC-019 | — | Nhóm A. Màn hình tài khoản BANNED |
| QA-064 | Sở hữu | Trùng với DEC-019 | — | Nhóm A. Vô hiệu hóa 14 ngày; không xóa trực tiếp |
| QA-065 | Sở hữu | Trùng với DEC-019 | — | Nhóm A. Hiển thị bài, bình luận của tài khoản vô hiệu hóa |
| QA-066 | Sở hữu | Hiện hành | FR-M01-13, FR-M01-13.01, FR-M01-13.04, BR-M01-24 | Nhóm A. Hiển thị bình luận sau khi tự xóa; xóa PII. Cùng nội dung DEC-019, thêm ý bài viết vẫn ẩn sau khi xóa — giữ Hiện hành |
| MR-M01 | Sở hữu | Sửa một phần bởi DEC-147, DEC-148, DEC-149, DEC-150, DEC-151, DEC-152, DEC-153 | FR-M01-01, FR-M01-02, FR-M01-04, FR-M01-06, FR-M01-09, FR-M01-10, FR-M01-12, FR-M01-14 | Nhóm A. Dòng registry của M01; cột MoSCoW đọc được (Must) |
| DEC-147 | Sở hữu | Hiện hành | FR-M01-04.04, FR-M01-04.05, FR-M01-04.09, BR-M01-09 | Nhóm A. Liên kết Google |
| DEC-148 | Sở hữu | Hiện hành | FR-M01-01.10, FR-M01-01.11, FR-M01-03.05, FR-M01-03.06, FR-M01-03.11, FR-M01-03.12, FR-M01-03.13, FR-M01-03.14, FR-M01-03.15, FR-M01-03.16, FR-M01-08.08, FR-M01-08.09, FR-M01-09.08, FR-M01-09.09, FR-M01-12.06, FR-M01-12.07, FR-M01-14.02, BR-M01-05, BR-M01-06, BR-M01-21, BR-M01-35, BR-M01-36, BR-M01-47 | Nhóm A. Mật khẩu, username, display_name, đổi tên, email và username khi DELETED |
| DEC-149 | Sở hữu | Hiện hành | FR-M01-10.07, FR-M01-11.01, FR-M01-11.02, FR-M01-11.05, FR-M01-11.06, FR-M01-11.07, FR-M01-11.08, FR-M01-11.09, FR-M01-11.10, FR-M01-12.01, FR-M01-12.05, FR-M01-13.04, BR-M01-21, BR-M01-22, BR-M01-24, BR-M01-32, BR-M01-47 | Nhóm A. Thời hạn vô hiệu hóa, kích hoạt lại, email cảnh báo, bình luận sau khi xóa |
| DEC-150 | Sở hữu | Hiện hành | FR-M01-13.01, FR-M01-13.05, BR-M01-41 | Nhóm A. Mod, Admin xem tác giả đã vô hiệu hóa (mở rộng phạm vi) |
| DEC-151 | Sở hữu | Hiện hành | FR-M01-02.06, FR-M01-02.07, FR-M01-06.04, FR-M01-06.07, FR-M01-08.10, FR-M01-09.01, FR-M01-09.10, FR-M01-09.11, FR-M01-09.12, FR-M01-09.13, FR-M01-09.14, FR-M01-09.15, FR-M01-09.16, BR-M01-16, BR-M01-36, BR-M01-38, BR-M01-39 | Nhóm A. Phiên làm mới, magic link, quên mật khẩu |
| DEC-152 | Sở hữu | Hiện hành | FR-M01-01.08, FR-M01-01.09, FR-M01-01.12, FR-M01-04.10, FR-M01-04.11, FR-M01-05.06, FR-M01-05.17, FR-M01-05.18, FR-M01-05.19, FR-M01-05.20, BR-M01-33, BR-M01-34, BR-M01-37 | Nhóm A. Tạm dừng đăng ký, bảo trì, ban hết hạn, nút OK |
| DEC-153 | Sở hữu | Hiện hành | FR-M01-14.10, FR-M01-14.12, FR-M01-14.13, FR-M01-14.14, FR-M01-14.15, FR-M01-14.16, FR-M01-14.17, BR-M01-27, BR-M01-30, BR-M01-40 | Nhóm A. Nhắc tên |
| DEC-154 | Sở hữu | Hiện hành | FR-M01-15, FR-M01-15.02, FR-M01-15.03, FR-M01-15.04, FR-M01-15.05, BR-M01-42, BR-M01-43 | Nhóm A. Trang Privacy Policy/ToS |
| DEC-155 | Sở hữu | Sửa một phần bởi DEC-158 | FR-M01-01.14, FR-M01-04.13, FR-M01-15.07, FR-M01-15.08, FR-M01-16, FR-M01-16.01, FR-M01-16.02, FR-M01-16.03, FR-M01-16.04, FR-M01-16.05, BR-M01-44, BR-M01-45 | Nhóm A. Bản ghi đồng ý, đồng ý lại |
| DEC-156 | Sở hữu | Sửa một phần bởi DEC-159 | FR-M01-12.02, FR-M01-12.08, FR-M01-12.09, FR-M01-12.10, FR-M01-13.06, FR-M01-15.06, BR-M01-47 | Nhóm A. Dữ liệu khi DELETED |
| DEC-157 | Sở hữu | Hiện hành | FR-M01-01.13, FR-M01-01.15, FR-M01-04.12, FR-M01-15.07, BR-M01-46 | Nhóm A. Bản sao dữ liệu, dưới 16 tuổi |
| DEC-158 | Sở hữu | Hiện hành | FR-M01-15.09, FR-M01-16, FR-M01-16.01, FR-M01-16.04, BR-M01-44, BR-M01-45 | Nhóm A. Thời điểm hỏi đồng ý lại, phát hành phiên bản chính sách |
| DEC-159 | Sở hữu | Sửa một phần bởi DEC-215 | FR-M01-12.08, FR-M01-12.11, BR-M01-47 | Nhóm A. Theo dõi Topic, bài viết và phản hồi gợi ý khi DELETED |
| ISS-259 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-159 | Nhóm A. Đã có DEC-159 |
| ISS-260 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-159 | Nhóm A. Đã có DEC-159 |
| QA-319 | Sở hữu | Trùng với DEC-159 | — | Nhóm A. Lời trả lời của stakeholder (đối chiếu M05) |
| QA-320 | Sở hữu | Trùng với DEC-159 | — | Nhóm A. Lời trả lời của stakeholder (đối chiếu M05) |
| ISS-257 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-158 | Nhóm A. Đã có DEC-158 |
| ISS-258 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-158 | Nhóm A. Đã có DEC-158 |
| QA-317 | Sở hữu | Trùng với DEC-158 | — | Nhóm A. Lời trả lời của stakeholder (quyền riêng tư) |
| QA-318 | Sở hữu | Trùng với DEC-158 | — | Nhóm A. Lời trả lời của stakeholder (quyền riêng tư) |
| ISS-249 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-154 | Nhóm A. Đã có DEC-154 |
| ISS-250 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-155 | Nhóm A. Đã có DEC-155 |
| ISS-251 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-156 | Nhóm A. Đã có DEC-156 |
| ISS-252 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-156 | Nhóm A. Đã có DEC-156 |
| ISS-253 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-154 | Nhóm A. Đã có DEC-154 |
| ISS-254 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-154 | Nhóm A. Đã có DEC-154 |
| ISS-255 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-155, DEC-157 | Nhóm A. Đã có DEC-155, DEC-157 |
| ISS-256 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-157 | Nhóm A. Đã có DEC-157 |
| QA-309 | Sở hữu | Trùng với DEC-154 | — | Nhóm A. Lời trả lời của stakeholder (quyền riêng tư) |
| QA-310 | Sở hữu | Trùng với DEC-155 | — | Nhóm A. Lời trả lời của stakeholder (quyền riêng tư) |
| QA-311 | Sở hữu | Trùng với DEC-156 | — | Nhóm A. Lời trả lời của stakeholder (quyền riêng tư) |
| QA-312 | Sở hữu | Trùng với DEC-156 | — | Nhóm A. Lời trả lời của stakeholder (quyền riêng tư) |
| QA-313 | Sở hữu | Trùng với DEC-154 | — | Nhóm A. Lời trả lời của stakeholder (quyền riêng tư) |
| QA-314 | Sở hữu | Trùng với DEC-154 | — | Nhóm A. Lời trả lời của stakeholder (quyền riêng tư) |
| QA-315 | Sở hữu | Trùng với DEC-155, DEC-157 | — | Nhóm A. Lời trả lời của stakeholder (quyền riêng tư) |
| QA-316 | Sở hữu | Trùng với DEC-157 | — | Nhóm A. Lời trả lời của stakeholder (quyền riêng tư) |
| ISS-232 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-147 | Nhóm A. Đã có DEC-147 |
| ISS-233 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-149 | Nhóm A. Đã có DEC-149 |
| ISS-234 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-150 | Nhóm A. Đã có DEC-150 |
| ISS-235 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-148 | Nhóm A. Đã có DEC-148 |
| ISS-236 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-148 | Nhóm A. Đã có DEC-148 |
| ISS-237 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-147 | Nhóm A. Đã có DEC-147 |
| ISS-238 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-151 | Nhóm A. Đã có DEC-151 |
| ISS-239 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-149 | Nhóm A. Đã có DEC-149 |
| ISS-240 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-149 | Nhóm A. Đã có DEC-149 |
| ISS-241 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-153 | Nhóm A. Đã có DEC-153 |
| ISS-242 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-149, DEC-151 | Nhóm A. Đã có DEC-149, DEC-151 |
| ISS-243 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-152 | Nhóm A. Đã có DEC-152 |
| ISS-244 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-152 | Nhóm A. Đã có DEC-152 |
| ISS-245 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-148 | Nhóm A. Đã có DEC-148 |
| ISS-246 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-151 | Nhóm A. Đã có DEC-151 |
| ISS-247 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-152 | Nhóm A. Đã có DEC-152 |
| ISS-248 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-151 | Nhóm A. Đã có DEC-151 |
| QA-292 | Sở hữu | Trùng với DEC-147 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| QA-293 | Sở hữu | Trùng với DEC-149 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| QA-294 | Sở hữu | Trùng với DEC-150 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| QA-295 | Sở hữu | Trùng với DEC-148 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| QA-296 | Sở hữu | Trùng với DEC-148 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| QA-297 | Sở hữu | Trùng với DEC-147 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| QA-298 | Sở hữu | Trùng với DEC-151 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| QA-299 | Sở hữu | Trùng với DEC-149 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| QA-300 | Sở hữu | Trùng với DEC-149 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| QA-301 | Sở hữu | Trùng với DEC-153 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| QA-302 | Sở hữu | Trùng với DEC-149, DEC-151 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| QA-303 | Sở hữu | Trùng với DEC-152 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| QA-304 | Sở hữu | Trùng với DEC-152 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| QA-305 | Sở hữu | Trùng với DEC-148 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| QA-306 | Sở hữu | Trùng với DEC-151 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| QA-307 | Sở hữu | Trùng với DEC-152 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| QA-308 | Sở hữu | Trùng với DEC-151 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| DEC-001 | Sở hữu | Hiện hành | BR-M01-01 | Nhóm B. Không có loại tài khoản Giáo viên — ngoài phạm vi |
| DEC-007 | Phụ thuộc | Sửa một phần bởi DEC-221 | FR-M01-01.02, BR-M01-01 | Nhóm B. M10: ADMIN gốc tạo sẵn, không qua đăng ký; ADMIN cấp quyền ADMIN. DEC-221 (đối chiếu FR-M10): chỉ tài khoản ADMIN gốc cấp, thu hồi vai trò Admin; ADMIN gốc không bị thu hồi |
| DEC-010 | Sở hữu | Sửa một phần bởi DEC-147 | FR-M01-01.06, FR-M01-04, FR-M01-04.04, FR-M01-04.05, BR-M01-04, BR-M01-09 | Nhóm B. Liên kết tài khoản Google theo email đã xác minh. Phần thông báo sau liên kết: Q-01 trả lời A, giữ thông báo (DEC-147) |
| DEC-014 | Sở hữu | Sửa một phần bởi DEC-138 | FR-M01-01, FR-M01-01.01, FR-M01-01.03, FR-M01-01.07, FR-M01-02, FR-M01-02.01, FR-M01-02.02, FR-M01-02.03, FR-M01-03, FR-M01-03.01, FR-M01-03.02, FR-M01-03.03, FR-M01-03.04, FR-M01-03.08, FR-M01-03.09, FR-M01-04, FR-M01-04.01, FR-M01-04.02, FR-M01-04.03, FR-M01-04.06, FR-M01-05, FR-M01-05.10, FR-M01-05.11, FR-M01-05.12, BR-M01-02, BR-M01-05, BR-M01-06, BR-M01-08, BR-M01-10, BR-M01-18 | Nhóm B. Đăng ký 3 bước; cổng đăng nhập đưa về bước còn dở |
| DEC-015 | Sở hữu | Sửa một phần bởi DEC-023, DEC-148 | FR-M01-03, FR-M01-03.01, FR-M01-03.05, FR-M01-03.06, FR-M01-03.07, FR-M01-03.10, FR-M01-14, FR-M01-14.03, BR-M01-05, BR-M01-06, BR-M01-07 | Nhóm B. display_name và username |
| DEC-016 | Sở hữu | Sửa một phần bởi DEC-151 | FR-M01-02, FR-M01-02.03, FR-M01-02.04, FR-M01-02.05, FR-M01-05.13, FR-M01-08, FR-M01-08.01, FR-M01-08.02, FR-M01-08.03, FR-M01-08.04, FR-M01-08.06, FR-M01-08.07, FR-M01-09, FR-M01-09.01, FR-M01-09.02, FR-M01-09.03, FR-M01-09.04, FR-M01-09.05, FR-M01-09.06, FR-M01-09.07, BR-M01-10, BR-M01-11, BR-M01-12, BR-M01-13, BR-M01-14, BR-M01-15 | Nhóm B. Xác minh email, quên mật khẩu, đổi mật khẩu |
| DEC-017 | Sở hữu | Sửa một phần bởi DEC-151 | FR-M01-04.08, FR-M01-05.12, FR-M01-06, FR-M01-06.01, FR-M01-06.02, FR-M01-06.03, FR-M01-06.04, FR-M01-06.05, FR-M01-06.06, FR-M01-07.01, FR-M01-07.02, BR-M01-16, BR-M01-17 | Nhóm B. Phiên đăng nhập, nhiều thiết bị |
| DEC-018 | Sở hữu | Sửa một phần bởi DEC-085 | FR-M01-01.01, FR-M01-02, FR-M01-02.01, FR-M01-03, FR-M01-03.01, FR-M01-03.08, FR-M01-04, FR-M01-04.01, FR-M01-04.06, FR-M01-05, FR-M01-05.01, FR-M01-05.03, BR-M01-02, BR-M01-08, BR-M01-18 | Nhóm B. account_state và verify_level; cổng đăng nhập |
| DEC-019 | Sở hữu | Sửa một phần bởi DEC-148, DEC-149, DEC-156 | FR-M01-05, FR-M01-05.07, FR-M01-05.08, FR-M01-05.09, FR-M01-10, FR-M01-10.01, FR-M01-10.03, FR-M01-10.04, FR-M01-10.06, FR-M01-11, FR-M01-11.02, FR-M01-11.03, FR-M01-11.05, FR-M01-12, FR-M01-12.01, FR-M01-12.02, FR-M01-13, FR-M01-13.01, FR-M01-13.02, FR-M01-13.03, FR-M01-13.04, BR-M01-19, BR-M01-20, BR-M01-21, BR-M01-22, BR-M01-23, BR-M01-24, BR-M01-25 | Nhóm B. Vô hiệu hóa, tự xóa, hiển thị nội dung, màn hình BANNED. Phần bình luận sau khi tài khoản bị xóa: Q-02 trả lời A, xác nhận cách đọc giữ nội dung (DEC-149) |
| DEC-020 | Sở hữu | Sửa một phần bởi DEC-153, DEC-214 | FR-M01-14, FR-M01-14.01, FR-M01-14.02, FR-M01-14.03, FR-M01-14.04, FR-M01-14.05, FR-M01-14.06, FR-M01-14.07, FR-M01-14.08, FR-M01-14.09, BR-M01-07, BR-M01-26, BR-M01-27, BR-M01-28, BR-M01-29 | Nhóm B. Hệ thống @mention |
| DEC-023 | Nhắc tới | Hiện hành | BR-M01-07 | Nhóm B. M02 dùng username trong địa chỉ trang hồ sơ |
| DEC-026 | Phụ thuộc | Hiện hành | Chuyển M02 | Nhóm B. M02: không hiện lịch sử đổi username — ngụ ý username đổi được |
| DEC-039 | Nhắc tới | Hiện hành | Không áp dụng: M04: trình soạn bình luận có @mention | Nhóm B. M04: trình soạn bình luận có @mention |
| DEC-040 | Nhắc tới | Hiện hành | Không áp dụng: M04: dùng @mention khi trả lời | Nhóm B. M04: dùng @mention khi trả lời |
| DEC-045 | Phụ thuộc | Sửa một phần bởi DEC-153 | FR-M01-14, FR-M01-14.10, BR-M01-30 | Nhóm B. M04/M07: @mention dùng logic chung của M01, luôn sinh thông báo |
| DEC-053 | Nhắc tới | Hiện hành | Không áp dụng: M06: tìm User dùng chung cách so khớp với @mention | Nhóm B. M06: tìm User dùng chung cách so khớp với @mention |
| DEC-065 | Phụ thuộc | Sửa một phần bởi DEC-147, DEC-151 | FR-M01-04, FR-M01-05.04, FR-M01-08, FR-M01-08.05, FR-M01-10.02, FR-M01-12, FR-M01-12.05, BR-M01-18, BR-M01-31, BR-M01-32 | Nhóm B. M07: thông báo đổi mật khẩu (kèm email), email cảnh báo trước khi tự xóa. Thiếu sự kiện liên kết Google: Q-01 trả lời A, đã bổ sung ở DEC-147 |
| DEC-070 | Nhắc tới | Hiện hành | FR-M01-14.10, BR-M01-30 | Nhóm B. M07: @mention vẫn thông báo khi tắt thông báo bài |
| DEC-080 | Phụ thuộc | Sửa một phần bởi DEC-152 | Chuyển M08 | Nhóm B. M08: loại ban và thời hạn 30/90 ngày/vĩnh viễn |
| DEC-085 | Sở hữu | Hiện hành | FR-M01-05, FR-M01-05.05, FR-M01-05.06, FR-M01-05.07, FR-M01-05.08, FR-M01-09.16, FR-M01-10.05, BR-M01-18, BR-M01-19 | Nhóm B. Tài khoản BANNED vẫn đăng nhập, chỉ thấy màn hình bị khóa (section M09) |
| DEC-086 | Phụ thuộc | Hiện hành | FR-M01-05, FR-M01-05.08, BR-M01-19 | Nhóm B. M09: hạn khiếu nại — hiện trên màn hình BANNED |
| DEC-089 | Phụ thuộc | Hiện hành | FR-M01-05.16, BR-M01-34 | Nhóm B. M09: khiếu nại ban được chấp nhận → ACTIVE |
| DEC-090 | Nhắc tới | Hiện hành | Không áp dụng: M10: phạm vi Admin/Mod | Nhóm B. M10: phạm vi Admin/Mod. Cạnh lineage DEC-141 (Topic) đúng nhưng không chạm M01 |
| DEC-092 | Phụ thuộc | Sửa một phần bởi DEC-152 | FR-M01-01, FR-M01-01.08, FR-M01-01.12, BR-M01-33 | Nhóm B. M10: công tắc tạm dừng đăng ký, chế độ bảo trì |
| DEC-107 | Nhắc tới | Hiện hành | Không áp dụng: M11: Owner bị ban/vô hiệu hóa/xóa → chuyển quyền Owner | Nhóm B. M11: Owner bị ban/vô hiệu hóa/xóa → chuyển quyền Owner |
| DEC-122 | Phụ thuộc | Hiện hành | Chuyển M12 | Nhóm B. M12: nhãn "Tài khoản đã bị khóa" cho tài khoản BANNED. Cạnh lineage ISS-154 bác bỏ: ISS-154 là issue sinh ra DEC-122 |
| DEC-126 | Nhắc tới | Hiện hành | Không áp dụng: M14: quyền của Guest trong Feed | Nhóm B. M14: quyền của Guest trong Feed |
| DEC-129 | Phụ thuộc | Sửa một phần bởi DEC-156 | FR-M01-12, FR-M01-12.02, FR-M01-12.10, BR-M01-21, BR-M01-47 | Nhóm B. Nguyên tắc chỉ xóa cứng khi an toàn; xác nhận xóa PII khi DELETED |
| DEC-131 | Sở hữu | Sửa một phần bởi DEC-138, DEC-154 | FR-M01-01, FR-M01-01.04, FR-M01-15, FR-M01-15.01, BR-M01-03 | Nhóm B. Trang Privacy Policy/ToS gắn vào luồng đăng ký. DEC-146 sửa nội dung trang (thêm Topic Suggestion), không chạm hành vi M01 |
| DEC-136 | Nhắc tới | Hiện hành | Không áp dụng: Cách gửi email (magic link, OTP kích hoạt lại) — kỹ thuật | Nhóm B. Cách gửi email (magic link, OTP kích hoạt lại) — kỹ thuật |
| DEC-137 | Nhắc tới | Hiện hành | Không áp dụng: Tech stack | Nhóm B. Tech stack |
| DEC-138 | Sở hữu | Sửa một phần bởi DEC-155, DEC-157 | FR-M01-01, FR-M01-01.04, FR-M01-01.05, FR-M01-04.07, FR-M01-04.12, FR-M01-15, BR-M01-03 | Nhóm B. Bắt buộc đồng ý Privacy Policy/ToS khi đăng ký |
| DG-2 | Sở hữu | Hiện hành | FR-M01-01, FR-M01-01.02, BR-M01-01 | Nhóm B. Draft: người dùng duy nhất là học sinh THPT; ba cấp quyền |
| DG-4 | Nhắc tới | Hiện hành | Không áp dụng: Bản đồ module | Nhóm B. Bản đồ module |
| DG-5 | Nhắc tới | Hiện hành | Không áp dụng: Nguyên tắc; ý không phân biệt Giáo viên/Học sinh trùng DG-8 | Nhóm B. Nguyên tắc; ý không phân biệt Giáo viên/Học sinh trùng DG-8 |
| DG-8 | Sở hữu | Hiện hành | BR-M01-01 | Nhóm B. Không làm: phân biệt tài khoản Giáo viên/Học sinh |
| DM-10.2 | Phụ thuộc | Sửa một phần bởi DEC-080 | Chuyển M08 | Nhóm B. M08: Mod/Admin suspend, ban account |
| DM-10.3 | Phụ thuộc | Sửa một phần bởi QA-018, DEC-080 | Chuyển M10 | Nhóm B. M10: Admin disable, suspend, ban account |
| DM-4.2 | Nhắc tới | Hiện hành | Không áp dụng: M04: Mention trong bình luận | Nhóm B. M04: Mention trong bình luận |
| DM-8.1 | Phụ thuộc | Hiện hành | Chuyển M07 | Nhóm B. M07: sự kiện thông báo Mention |
| DM-9.4 | Nhắc tới | Hiện hành | Không áp dụng: M12: không có leaderboard theo loại tài khoản | Nhóm B. M12: không có leaderboard theo loại tài khoản |
| DM-x03 | Nhắc tới | Hiện hành | Không áp dụng: Ngoài phạm vi dự án; trùng DG-8 | Nhóm B. Ngoài phạm vi dự án; trùng DG-8 |
| ISS-037 | Nhắc tới | Hiện hành | Không áp dụng: Đã có QA-018 | Nhóm B. Đã có QA-018 |
| ISS-043 | Nhắc tới | Hiện hành | Không áp dụng: Đã có QA-026, DEC-010 | Nhóm B. Đã có QA-026, DEC-010 |
| ISS-060 | Nhắc tới | Hiện hành | Không áp dụng: M02: lịch sử đổi username | Nhóm B. M02: lịch sử đổi username |
| ISS-061 | Nhắc tới | Hiện hành | Không áp dụng: M02: địa chỉ trang hồ sơ | Nhóm B. M02: địa chỉ trang hồ sơ |
| ISS-070 | Nhắc tới | Hiện hành | Không áp dụng: M04: trình soạn bình luận | Nhóm B. M04: trình soạn bình luận |
| ISS-077 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-045 | Nhóm B. Đã có DEC-045 |
| ISS-104 | Nhắc tới | Hiện hành | Không áp dụng: M08: báo cáo cần đăng nhập | Nhóm B. M08: báo cáo cần đăng nhập |
| ISS-114 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-085 | Nhóm B. Đã có DEC-085 |
| ISS-115 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-086 | Nhóm B. Đã có DEC-086 |
| ISS-119 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-090 | Nhóm B. Đã có DEC-090 |
| ISS-121 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-092 | Nhóm B. Đã có DEC-092 |
| ISS-130 | Nhắc tới | Hiện hành | Không áp dụng: M11: tạo group cần đăng nhập | Nhóm B. M11: tạo group cần đăng nhập |
| ISS-154 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-122 | Nhóm B. Đã có DEC-122 |
| ISS-162 | Nhắc tới | Hiện hành | Không áp dụng: M16: nhắn tin cần đăng nhập | Nhóm B. M16: nhắn tin cần đăng nhập |
| ISS-166 | Nhắc tới | Hiện hành | Không áp dụng: M14: Guest xem Feed | Nhóm B. M14: Guest xem Feed |
| ISS-179 | Nhắc tới | Hiện hành | Không áp dụng: M15: thống kê tài khoản theo trạng thái | Nhóm B. M15: thống kê tài khoản theo trạng thái |
| ISS-188 | Nhắc tới | Hiện hành | Không áp dụng: M14: tab Group | Nhóm B. M14: tab Group |
| ISS-191 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-129 | Nhóm B. Đã có DEC-129 |
| ISS-193 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-131 | Nhóm B. Đã có DEC-131 |
| ISS-199 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-136 | Nhóm B. Đã có DEC-136 |
| ISS-203 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-137 | Nhóm B. Đã có DEC-137 |
| ISS-204 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-138, OPEN-008 | Nhóm B. Đã có DEC-138, OPEN-008 |
| OPEN-008 | Sở hữu | Sửa một phần bởi DEC-154, DEC-155, DEC-156, DEC-157 | TBD-M01-01 | Nhóm B. Privacy; đã thu hẹp bởi DEC-154–157, còn email liên hệ và cách nhận bản sao dữ liệu |
| QA-009 | Phụ thuộc | Trùng với DEC-007 | — | Nhóm B. M10: cùng nội dung DEC-007 |
| QA-011 | Sở hữu | Sửa một phần bởi DEC-208 | FR-M01-01, FR-M01-04, FR-M01-05, FR-M01-14.11 | Nhóm B. Guest được Đăng ký, Đăng nhập |
| QA-013 | Phụ thuộc | Hiện hành | Chuyển M10, M08 | Nhóm B. M10/M08: MOD bị ban thì tự mất vai trò |
| QA-017 | Nhắc tới | Hiện hành | Không áp dụng: Tác nhân hệ thống; Notification Worker gửi mention | Nhóm B. Tác nhân hệ thống; Notification Worker gửi mention |
| QA-018 | Sở hữu | Sửa một phần bởi DEC-018, DEC-019, QA-019, DEC-149, DEC-246 | FR-M01-05, FR-M01-05.04, FR-M01-05.14, FR-M01-05.15, FR-M01-10, FR-M01-10.01, FR-M01-10.02, FR-M01-10.03, FR-M01-10.04, FR-M01-11, FR-M01-11.01, FR-M01-11.02, FR-M01-11.04, FR-M01-11.05, FR-M01-11.10, FR-M01-12, FR-M01-12.01, FR-M01-12.03, FR-M01-12.04, FR-M01-13, BR-M01-18, BR-M01-20, BR-M01-21, BR-M01-22, BR-M01-25 | Nhóm B. Phase 2: máy trạng thái tài khoản, kích hoạt lại bằng OTP email, hiển thị nội dung |
| QA-019 | Phụ thuộc | Hiện hành | FR-M01-05.05, FR-M01-05.14, FR-M01-05.15, BR-M01-34 | Nhóm B. M08: ban; tài khoản BANNED vẫn đăng nhập |
| QA-020 | Nhắc tới | Hiện hành | Không áp dụng: M08: tài khoản bị warn vẫn hoạt động bình thường | Nhóm B. M08: tài khoản bị warn vẫn hoạt động bình thường |
| QA-023 | Nhắc tới | Hiện hành | Không áp dụng: M16 | Nhóm B. M16 |
| QA-026 | Sở hữu | Trùng với DEC-010 | — | Nhóm B. Google OAuth, tự liên kết theo email đã xác minh |
| QA-036 | Nhắc tới | Hiện hành | Không áp dụng: M06: lý do dùng so khớp chuỗi con cho tên | Nhóm B. M06: lý do dùng so khớp chuỗi con cho tên |
| QA-067 | Nhắc tới | Hiện hành | Không áp dụng: M02: thông tin trang hồ sơ | Nhóm B. M02: thông tin trang hồ sơ |
| QA-070 | Nhắc tới | Hiện hành | Không áp dụng: M02: lịch sử đổi username | Nhóm B. M02: lịch sử đổi username |
| QA-075 | Nhắc tới | Hiện hành | Không áp dụng: M02: địa chỉ trang hồ sơ | Nhóm B. M02: địa chỉ trang hồ sơ |
| QA-092 | Nhắc tới | Hiện hành | Không áp dụng: M04: trình soạn bình luận | Nhóm B. M04: trình soạn bình luận |
| QA-099 | Phụ thuộc | Trùng với DEC-045 | — | Nhóm B. M04/M07: @mention trong bình luận luôn sinh thông báo |
| QA-110 | Nhắc tới | Sửa một phần bởi DEC-209 | Không áp dụng: M06: tìm User dùng chung với @mention | Nhóm B. M06: tìm User dùng chung với @mention; DEC-209 chốt cách khớp và phạm vi tài khoản |
| QA-123 | Phụ thuộc | Trùng với DEC-065 | — | Nhóm B. M07: danh sách sự kiện gồm mật khẩu, vô hiệu hóa, mention |
| QA-124 | Phụ thuộc | Trùng với DEC-065 | — | Nhóm B. M07: sự kiện có email |
| QA-135 | Nhắc tới | Hiện hành | Không áp dụng: M08: Guest không báo cáo được | Nhóm B. M08: Guest không báo cáo được |
| QA-152 | Phụ thuộc | Hiện hành | Chuyển M09 | Nhóm B. M09: link khiếu nại trong email ban đi qua đăng nhập |
| QA-153 | Phụ thuộc | Trùng với DEC-086 | — | Nhóm B. M09: hạn khiếu nại |
| QA-154 | Nhắc tới | Hiện hành | Không áp dụng: M09: lý do giới hạn hạn khiếu nại | Nhóm B. M09: lý do giới hạn hạn khiếu nại |
| QA-164 | Phụ thuộc | Trùng với DEC-092 | — | Nhóm B. M10: danh sách cấu hình hệ thống |
| QA-179 | Nhắc tới | Hiện hành | Không áp dụng: M11 | Nhóm B. M11 |
| QA-185 | Nhắc tới | Hiện hành | Không áp dụng: M11: chuyển quyền Owner | Nhóm B. M11: chuyển quyền Owner |
| QA-204 | Phụ thuộc | Trùng với DEC-122 | — | Nhóm B. M12: tài khoản BANNED trên leaderboard, hồ sơ, bài viết |
| QA-205 | Phụ thuộc | Hiện hành | Chuyển M12 | Nhóm B. M12: nhãn bị khóa, phân biệt với nhãn vô hiệu hóa của DEC-019 |
| QA-223 | Nhắc tới | Hiện hành | Không áp dụng: M16: không gửi email tin nhắn | Nhóm B. M16: không gửi email tin nhắn |
| QA-227 | Nhắc tới | Hiện hành | Không áp dụng: M14: Guest | Nhóm B. M14: Guest |
| QA-230 | Nhắc tới | Hiện hành | Không áp dụng: M14: tab Group | Nhóm B. M14: tab Group |
| QA-236 | Nhắc tới | Hiện hành | Không áp dụng: M14: Trending với tài khoản BANNED | Nhóm B. M14: Trending với tài khoản BANNED |
| QA-242 | Nhắc tới | Hiện hành | Không áp dụng: M15: thống kê tài khoản | Nhóm B. M15: thống kê tài khoản |
| QA-250 | Phụ thuộc | Trùng với DEC-129 | — | Nhóm B. Cùng nội dung DEC-129 |
| QA-252 | Sở hữu | Trùng với DEC-131 | — | Nhóm B. Cùng nội dung DEC-131 |
| QA-259 | Nhắc tới | Hiện hành | Không áp dụng: M10: nơi lưu cờ AI | Nhóm B. M10: nơi lưu cờ AI |
| QA-263 | Nhắc tới | Hiện hành | Không áp dụng: Tech stack | Nhóm B. Tech stack |
| QA-264 | Sở hữu | Trùng với DEC-138 | — | Nhóm B. Lời stakeholder cho DEC-138, OPEN-008 |
| MR-A01 | Nhắc tới | Hiện hành | Không áp dụng: Tóm tắt M16 | Nhóm B. Tóm tắt M16 |
| MR-A03 | Nhắc tới | Hiện hành | Không áp dụng: Tóm tắt M15 | Nhóm B. Tóm tắt M15 |
| MR-A04 | Nhắc tới | Hiện hành | Không áp dụng: Tóm tắt Phase 6 | Nhóm B. Tóm tắt Phase 6 |
| MR-A05 | Nhắc tới | Hiện hành | Không áp dụng: Tóm tắt tech stack | Nhóm B. Tóm tắt tech stack |
| MR-M02 | Nhắc tới | Hiện hành | Không áp dụng: M02 dùng username | Nhóm B. M02 dùng username |
| MR-M04 | Nhắc tới | Hiện hành | Không áp dụng: M04 có @mention | Nhóm B. M04 có @mention |
| MR-M10 | Phụ thuộc | Hiện hành | Chuyển M10 | Nhóm B. M10: công tắc đăng ký |
| MR-M11 | Nhắc tới | Hiện hành | Không áp dụng: M11 phụ thuộc M01 | Nhóm B. M11 phụ thuộc M01 |
| MR-M12 | Nhắc tới | Hiện hành | Không áp dụng: M12 phụ thuộc M01 | Nhóm B. M12 phụ thuộc M01 |
| MR-M15 | Nhắc tới | Hiện hành | Không áp dụng: M15 phụ thuộc M01 | Nhóm B. M15 phụ thuộc M01 |
| MR-M16 | Nhắc tới | Hiện hành | Không áp dụng: M16 phụ thuộc M01 | Nhóm B. M16 phụ thuộc M01 |
| DEC-127 | Phụ thuộc | Hiện hành | Mục 2.1 | Nhóm D. Múi giờ cho các mốc 1 giờ, 15 phút, 14 ngày, 30 ngày |
| DEC-128 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M01 | Nhóm D. Dùng chung; không quy định hành vi M01 |
| DEC-130 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M01 | Nhóm D. Dùng chung; không quy định hành vi M01 |
| DEC-132 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M01 | Nhóm D. Dùng chung; không quy định hành vi M01. Bị DEC-141, DEC-144 sửa phần Topic, không chạm M01 |
| DEC-133 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M01 | Nhóm D. Dùng chung; không quy định hành vi M01 |
| DEC-134 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M01 | Nhóm D. Dùng chung; không quy định hành vi M01 |
| DEC-135 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M01 | Nhóm D. Dùng chung; không quy định hành vi M01 |
| ISS-189 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M01 | Nhóm D. Dùng chung; không quy định hành vi M01 |
| ISS-190 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M01 | Nhóm D. Dùng chung; không quy định hành vi M01 |
| ISS-192 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M01 | Nhóm D. Dùng chung; không quy định hành vi M01 |
| ISS-194 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M01 | Nhóm D. Dùng chung; không quy định hành vi M01 |
| ISS-195 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M01 | Nhóm D. Dùng chung; không quy định hành vi M01 |
| ISS-196 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M01 | Nhóm D. Dùng chung; không quy định hành vi M01 |
| ISS-197 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M01 | Nhóm D. Dùng chung; không quy định hành vi M01 |
| ISS-198 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M01 | Nhóm D. Dùng chung; không quy định hành vi M01 |
| ISS-200 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M01 | Nhóm D. Dùng chung; không quy định hành vi M01 |
| ISS-201 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M01 | Nhóm D. Dùng chung; không quy định hành vi M01 |
| ISS-202 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M01 | Nhóm D. Dùng chung; không quy định hành vi M01 |
| QA-248 | Phụ thuộc | Trùng với DEC-127 | — | Nhóm D. Cùng nội dung DEC-127 |
| QA-249 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M01 | Nhóm D. Dùng chung; không quy định hành vi M01 |
| QA-251 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M01 | Nhóm D. Dùng chung; không quy định hành vi M01 |
| QA-253 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M01 | Nhóm D. Dùng chung; không quy định hành vi M01 |
| QA-254 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M01 | Nhóm D. Dùng chung; không quy định hành vi M01 |
| QA-255 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M01 | Nhóm D. Dùng chung; không quy định hành vi M01 |
| QA-256 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M01 | Nhóm D. Dùng chung; không quy định hành vi M01 |
| QA-260 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M01 | Nhóm D. Dùng chung; không quy định hành vi M01 |
| QA-261 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M01 | Nhóm D. Dùng chung; không quy định hành vi M01 |
| QA-262 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M01 | Nhóm D. Dùng chung; không quy định hành vi M01 |
| DEC-214 | Sở hữu | Hiện hành | FR-M01-14.02, BR-M01-26 | Nhóm B. Thêm ở bản 1.3. @mention khớp tên như tìm người dùng M06 (DEC-209) |
| QA-404 | Sở hữu | Trùng với DEC-214 | — | Nhóm B. Thêm ở bản 1.3. Câu trả lời của stakeholder, nội dung nằm trong DEC-214 |
| ISS-344 | Nhắc tới | Trùng với DEC-214 | — | Nhóm B. Thêm ở bản 1.3. Câu hỏi đã có DEC-214 trả lời |
| DEC-209 | Phụ thuộc | Hiện hành | Chuyển M06 | Nhóm B. Thêm ở bản 1.3. M06: cách khớp tên dùng chung; tìm người dùng chỉ gồm tài khoản ACTIVE đã xong bước 3 |
| DEC-213 | Phụ thuộc | Hiện hành | Chuyển M06 | Nhóm B. Thêm ở bản 1.3. M06: đăng xuất thì xóa lịch sử tìm kiếm trên trình duyệt; ghi ở Giao tiếp |
| DEC-215 | Phụ thuộc | Hiện hành | FR-M01-12.08, BR-M01-47 | Nhóm B (đối chiếu FR-M07). M07: bỏ theo dõi bài viết, nên khi DELETED chỉ còn lượt theo dõi người dùng, Topic để xóa |
| DEC-221 | Phụ thuộc | Hiện hành | Chuyển M10 | Nhóm B (đối chiếu FR-M10). M10: tài khoản ADMIN gốc; chỉ gốc cấp (qua đề xuất), thu hồi vai trò Admin |
| DEC-228 | Phụ thuộc | Hiện hành | Chuyển M10 | Nhóm B (đối chiếu FR-M10). M10: đề xuất chỉ gửi cho tài khoản ACTIVE đã xong bước 3 (M01 cung cấp trạng thái) |
| DEC-246 | Phụ thuộc | Hiện hành | Chuyển M12 | Nhóm B (rà lại 1.6). M12: tài khoản DEACTIVATED bị loại khỏi bảng xếp hạng; tài khoản đã xóa hiện mờ với nhãn "[Người dùng đã xóa]" trên bảng đã chốt; sửa phần bảng xếp hạng của QA-018 |

### C.2 Chuỗi quyết định

| Chuỗi | Nội dung hiện hành |
|---|---|
| DEC-014 → DEC-138 → DEC-152 | Bước 1 của đăng ký gồm email, mật khẩu và bắt buộc đồng ý Privacy Policy/ToS. Bước 2, bước 3 và luồng Google giữ nguyên DEC-014. Khi công tắc tạm dừng đăng ký bật, không tạo được tài khoản mới bằng email hay Google lần đầu; đăng ký đã qua bước 1 làm tiếp được. |
| DEC-131 → DEC-138 → DEC-154 → DEC-155 → DEC-157 → DEC-158 (→ DEC-146) | Trang Privacy Policy/ToS công khai thuộc M01, gồm các mục của BR-M01-42, trình bày dữ liệu theo bốn nhóm, ghi "xử lý bởi nhà cung cấp dịch vụ AI" không nêu tên, một mục chung cho dịch vụ bên ngoài và cam kết không bán dữ liệu. Người đăng ký bắt buộc đồng ý qua một ô đồng ý kèm cam kết cho người dưới 16 tuổi; không hỏi tuổi. Hệ thống lưu thời điểm và phiên bản đã đồng ý; chỉ hỏi lại khi chính sách đổi phiên bản, ở lần mở ứng dụng kế tiếp kể cả khi đang giữ phiên đăng nhập; phiên bản mới chỉ do đội phát triển phát hành khi triển khai; không đồng ý thì chỉ đăng xuất hoặc vô hiệu hóa. Rút lại đồng ý bằng vô hiệu hóa. Không có chức năng tải bản sao dữ liệu ở MS1. OPEN-008 còn email liên hệ và cách nhận bản sao dữ liệu (TBD-M01-01). |
| DEC-015 → DEC-023 → DEC-148 | display_name là tên hiển thị chính, không duy nhất, 1–50 ký tự sau khi bỏ khoảng trắng đầu cuối, gồm chữ (có dấu), số, khoảng trắng và . , - _ ' ( ). username duy nhất (so không phân biệt hoa thường, hiển thị giữ nguyên), 3–20 ký tự a–z, A–Z, 0–9, "_"; dùng cho nhắc tên, tìm kiếm và địa chỉ trang hồ sơ (DEC-023). Cả hai đổi được ở trang sửa hồ sơ; username cũ được giải phóng khi đổi. Mật khẩu 8–64 ký tự, mật khẩu mới khác mật khẩu hiện tại. |
| QA-018 → DEC-018 → DEC-085 → DEC-152 | Hai trường: trạng thái tài khoản (ACTIVE, DEACTIVATED, DELETED, BANNED; không có WARNED) và mức xác minh (NONE, EMAIL_VERIFIED, SETUP_COMPLETED). Cổng đăng nhập xét trạng thái trước: DELETED và DEACTIVATED bị từ chối; BANNED đăng nhập được nhưng chỉ có màn hình tài khoản bị khóa, nút OK đăng xuất. Khi bật chế độ bảo trì, chỉ ADMIN đăng nhập và thao tác được. |
| QA-018 → DEC-019 → DEC-149 → DEC-148 | Vô hiệu hóa là cách duy nhất để xóa tài khoản. Thời hạn đủ 14 × 24 giờ; trong thời hạn kích hoạt lại bằng email và mã 6 chữ số (hạn 15 phút, sai tối đa 5 lần, xin lại cách 60 giây), xong thì đăng nhập luôn. Email cảnh báo gửi 24 giờ trước khi tự xóa. Hết thời hạn thì DELETED: dữ liệu cá nhân bị xóa, email được giải phóng, username giữ vĩnh viễn. Bài viết của tài khoản DEACTIVATED, DELETED bị ẩn; bình luận giữ nội dung với tên "Tài khoản tạm thời vô hiệu hoá" hoặc "[Người dùng đã xóa]" và avatar mặc định (DEC-149 thay tombstone của QA-018). Hồ sơ "người dùng không tồn tại", bảng xếp hạng, badge của tài khoản đã xóa (QA-018) thuộc M02, M12. |
| DEC-150 | Trong khi tài khoản DEACTIVATED, Mod và Admin xem được bài viết bị ẩn và danh tính thật của tác giả. |
| QA-018 → QA-019 → DEC-089 → DEC-152 | BANNED → ACTIVE khi Mod hoặc Admin gỡ ban, khi khiếu nại ban được chấp nhận, hoặc ngay lúc ban tạm thời hết hạn. |
| DEC-010 → DEC-147 (→ DEC-065) | Đăng nhập Google với email trùng email của một tài khoản email thì tự liên kết, không hỏi xác nhận, dù email đã xác minh hay chưa; nếu chưa thì mức xác minh lên EMAIL_VERIFIED. Sau khi liên kết, chủ tài khoản nhận thông báo trong ứng dụng và email; DEC-065 có thêm sự kiện này. |
| DEC-016 → DEC-151 (→ DEC-065) | Magic link xác minh hạn 1 giờ, đặt lại mật khẩu hạn 15 phút, mỗi link dùng một lần, link mới làm link cũ mất hiệu lực. Đặt lại mật khẩu kết thúc mọi phiên khác, tự đăng nhập, và gửi thông báo "mật khẩu đã đổi". "Quên mật khẩu" hiện câu chung "Liên kết đã được gửi, vui lòng kiểm tra email của bạn"; DEACTIVATED được hướng tới trang kích hoạt; BANNED được đặt lại để vào màn hình bị khóa và khiếu nại. Đổi mật khẩu, đổi thông tin chỉ khi ACTIVE. |
| DEC-017 → DEC-151 | Phiên truy cập 1 giờ; mỗi lần làm mới cấp phiên làm mới mới hạn 30 ngày tính từ lúc cấp, phiên cũ mất hiệu lực; nhiều thiết bị độc lập. |
| DEC-020 → DEC-045 → DEC-153 → DEC-214 | Danh sách gợi ý nhắc tên: gõ "@" kèm 1 ký tự, chờ 300 ms, tối đa 5 người, khớp ở bất kỳ vị trí trong display_name hoặc username, bỏ dấu, không phân biệt hoa thường, gần đúng (DEC-214, dùng chung với tìm người dùng M06, DEC-209), theo ba tầng ngữ cảnh, trong tầng xếp theo mức khớp; bình luận dùng ngữ cảnh bài chứa nó; không gồm DEACTIVATED, DELETED, BANNED, chưa xong bước 3. Lượt nhắc là khối liền, hiện display_name hiện tại; tới tài khoản DEACTIVATED, DELETED thì hiện tên thay thế, không mở trang hồ sơ. Thông báo gửi khi nội dung công khai; sửa nội dung chỉ báo người mới được nhắc. |
| DM-10.2, DM-10.3 → QA-018, DEC-080 | Admin, Mod không vô hiệu hóa hay xóa tài khoản người khác, chỉ cảnh báo hoặc ban. Register không có hình thức "Suspend account" riêng; khóa có thời hạn chỉ có dạng ban tạm thời 30 hoặc 90 ngày (DEC-080). |
| DEC-019 → DEC-129 → DEC-156 → DEC-159 → DEC-215 | Khi DELETED, xóa dữ liệu cá nhân theo danh mục của BR-M01-47 (email được giải phóng); giữ username, trạng thái, vai trò, bài viết ẩn, bình luận và tin nhắn với người viết "[Người dùng đã xóa]", upvote đã cho không còn biết người cho. Tin nhắn, nhật ký kiểm duyệt, nhật ký AI giữ vĩnh viễn (DEC-129) và gắn với tài khoản đã xóa qua username. DEC-159: xóa cả lượt theo dõi Topic của tài khoản (DEC-215 bỏ theo dõi bài viết); giữ phản hồi gợi ý Topic (M05) không gắn danh tính. |
| QA-019 → DEC-187, DEC-189; DEC-023 → DEC-170; DEC-065 → DEC-180; QA-011 → DEC-171, DEC-206, DEC-208; QA-110 → DEC-209; DEC-085 → DEC-197; DEC-086, DEC-089 → DEC-199, DEC-201 | Chỉ sửa phần thuộc module khác. QA-019: lần vi phạm thứ 7 thành yêu cầu ban, chỉ Admin ban Mod (DEC-187, DEC-189, M08); M01 vẫn chỉ giữ trạng thái tài khoản khi ban, gỡ ban. DEC-170, DEC-171 (M02), DEC-180 (M04) không đổi nội dung M01. DEC-208 (M06) chỉ làm rõ Guest tìm bài bằng full-text; DEC-209 (M06) chốt cách khớp tên và phạm vi tài khoản của tìm người dùng — M01 cung cấp trạng thái tài khoản cho việc này. DEC-206 (M13): tóm tắt AI chỉ cho người đã đăng nhập. DEC-197, DEC-199, DEC-201 (M09): khi BANNED chỉ khiếu nại được chính lệnh ban (khớp FR-M01-05.06, việc chọn đối tượng khiếu nại thuộc M09); thời hạn khiếu nại cảnh cáo; Mod bị ban được gỡ ban thì về ACTIVE với vai trò USER (vai trò thuộc M09, M10) — FR-M01-05.16 vẫn đúng. |
| DEC-065 → DEC-215, DEC-218, DEC-221; DEC-070 → DEC-219, DEC-220 (đối chiếu FR-M07, FR-M10) | Phần thuộc M07: thêm sự kiện "người bạn theo dõi có bài mới", quy tắc người nhận; tắt thông báo Chat chỉ ẩn popup, công tắc tắt thông báo bài có trên mọi bài. Không đổi yêu cầu của module này. |
| DEC-007 → DEC-221; DEC-092 → DEC-152, DEC-225, DEC-226, DEC-228 (đối chiếu FR-M10) | Tài khoản ADMIN gốc vẫn tạo sẵn, không qua đăng ký; chỉ tài khoản gốc cấp, thu hồi vai trò Admin (M10). Tạm dừng đăng ký, chế độ bảo trì không đổi đối với M01; DEC-225, DEC-226, DEC-228 chỉ thêm cờ tính năng, banner, giá trị khởi tạo (tạm dừng đăng ký, bảo trì khởi tạo ở Tắt) thuộc M10. M01 cung cấp trạng thái tài khoản và bước 3 để M10 chọn đối tượng đề xuất. |
| QA-018 → DEC-246 | Trên bảng xếp hạng (M12): tài khoản DEACTIVATED bị loại trong thời gian vô hiệu hóa; tài khoản đã xóa hiện mờ với nhãn "[Người dùng đã xóa]" trên bảng đã chốt, bảng Toàn thời gian loại ngay. |
