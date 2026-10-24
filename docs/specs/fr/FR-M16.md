---
module: M16
ten_module: Chat & Messaging
ma_tai_lieu: FR-M16
phien_ban: 1.0
trang_thai: Đã chốt
ngay: 2026-10-24
tac_gia: Phạm Văn Đức
moc_nguon: DEC-257, QA-455, ISS-393, OPEN-012
steps_completed: [1, 2, 3, 4, 5, 6, 7]
---
# Tài liệu yêu cầu chức năng — M16 Chat & Messaging

| Mã tài liệu | FR-M16 |
|---|---|
| Dự án | iShare |
| Module | M16 — Chat & Messaging |
| Trạng thái | Đã chốt |
| Phiên bản | 1.0 |
| Ngày | 2026-10-24 |
| Tác giả | Phạm Văn Đức |

<!-- Quy ước chung cho mọi bảng dưới đây:
     - Thân tài liệu không ghi nguồn. Nguồn của mọi ID nằm ở Phụ lục A.
     - Ô không có nội dung ghi "—". Không xóa cột.
     - Mục chưa tới bước làm thì để dòng "(Chưa làm — bước N)". -->

## 1. Tổng quan

### 1.1 Mục đích

Chat & Messaging cho phép người dùng đã đăng nhập nhắn tin văn bản với nhau theo thời gian thực: trò chuyện 1-1 với
bất kỳ người dùng nào mà không cần theo dõi trước, và nhóm chat nhiều người (từ 3 người) do người dùng tự tạo, độc lập
với Group (M11), có thể mời người khác bằng cách thêm thẳng hoặc gửi link mời. Tin nhắn chỉ gồm văn bản và emoji; người
gửi thu hồi được tin trong thời gian ngắn; người trong cuộc trò chuyện thấy ai đã xem tin nhắn mới nhất.

### 1.2 Phạm vi

**Trong phạm vi:**

- Trò chuyện 1-1: người dùng đã đăng nhập nhắn cho bất kỳ người dùng nào khác, không cần theo dõi, không có bước yêu
  cầu nhắn tin; mỗi cặp người dùng có đúng một cuộc 1-1.
- Nhóm chat: mọi người dùng đã đăng nhập tạo được, từ 3 thành viên khi tạo, tối đa 100; tên nhóm bắt buộc; vai trò
  Admin (người tạo) và Member; thêm thành viên thẳng hoặc qua link mời và xin gia nhập; công tắc duyệt thành viên mới do
  Admin bật tắt và Admin duyệt; Admin xóa thành viên; mọi thành viên đổi tên nhóm; rời nhóm; Admin phải chuyển quyền
  trước khi rời (trừ khi là thành viên cuối cùng); vào lại nhóm; xử lý khi Admin không còn khôi phục được tài khoản.
- Gửi tin nhắn văn bản và emoji, nhận tin nhắn theo thời gian thực; giới hạn độ dài và tần suất gửi.
- Không sửa tin nhắn; thu hồi tin nhắn trong thời hạn, cho cả hai phía, để lại dòng "Tin nhắn đã bị thu hồi"; thu hồi
  là xóa mềm.
- Trạng thái Đã gửi, Đã xem; mốc đã đọc của từng thành viên; khi nào hệ thống đánh dấu đã đọc; hiển thị người đã xem ở
  tin nhắn mới nhất và cập nhật tức thời cho các thành viên khác.
- Hộp thư Chat và lịch sử cuộc trò chuyện: tải dần, xem được tới tin đầu tiên; thành viên cũ xem lại lịch sử tới lúc
  rời.
- Nhắn tin với tài khoản đang bị ban, đang vô hiệu hóa hoặc đã xóa.
- Cung cấp cho M07: sự kiện tin nhắn mới, thành viên cuộc trò chuyện, mốc đã đọc, cuộc trò chuyện người dùng đang xem.
- Tin nhắn được giữ lâu dài; hành vi của module khi cờ tính năng Chat tắt.

**Ngoài phạm vi:**

- Popup tin nhắn mới, số trên biểu tượng Tin nhắn, tắt thông báo từng cuộc trò chuyện và toàn bộ Chat — M07 Notification.
- Bật, tắt cờ tính năng Chat — M10 Admin Panel.
- Tên thay thế "[Người dùng đã xóa]" cho người gửi của tài khoản đã xóa — M01 Authentication & Account; avatar,
  display_name hiện ở người gửi — M02 User Profile.
- Trạng thái tài khoản và màn hình khóa khi bị ban — M01, M08 Moderation; khiếu nại — M09 Appeal.
- Group (cộng đồng) và mọi tính năng của nhóm — M11 Group; nhóm chat không gắn với Group.
- Đã quyết không làm ở MS1: gọi thoại, gọi video, gửi tệp hoặc ảnh đính kèm; sửa tin nhắn; xóa tin "chỉ ở phía tôi";
  chặn (Block) và báo cáo tin nhắn (hoãn có chủ đích); xem nội dung tin đã thu hồi; quét AI nội dung tin nhắn; email cho
  tin nhắn mới; yêu cầu nhắn tin (message request); trạng thái online/offline, "đang gõ"; hệ thống tự chuyển quyền Admin
  nhóm chat; danh sách chặn của nhóm chat; thu hồi, tạo lại link mời; thông báo "được mời" vào nhóm chat.

## 2. Thuật ngữ và viết tắt

### 2.1 Thuật ngữ

| Thuật ngữ | Định nghĩa |
|---|---|
| Cuộc trò chuyện | Nơi các thành viên nhắn tin văn bản cho nhau. Có hai loại: trò chuyện 1-1 và nhóm chat. |
| Trò chuyện 1-1 | Cuộc trò chuyện giữa đúng hai người dùng khác nhau; mỗi cặp người dùng có tối đa một cuộc; không có vai trò quản trị. |
| Nhóm chat | Cuộc trò chuyện nhiều người do một người dùng tạo (từ 3 thành viên khi tạo, tối đa 100); có tên; độc lập với Group (M11). |
| Tên nhóm chat | Tên bắt buộc của nhóm chat, 1–100 ký tự sau khi bỏ khoảng trắng đầu và cuối; được trùng với nhóm chat khác. |
| Thành viên cuộc trò chuyện | Người dùng đang thuộc một cuộc trò chuyện: một trong hai người của trò chuyện 1-1, hoặc một thành viên nhóm chat. |
| Thành viên cũ | Người đã tự rời hoặc bị Admin nhóm chat xóa khỏi một nhóm chat và chưa vào lại. |
| Thời điểm rời | Lúc thành viên tự rời hoặc bị xóa khỏi nhóm chat; thành viên cũ chỉ xem các tin gửi trước thời điểm này. |
| Admin nhóm chat | Thành viên quản trị một nhóm chat; ban đầu là người tạo; mỗi nhóm chat có tối đa một Admin nhóm chat. Khác vai trò hệ thống ADMIN. |
| Member (nhóm chat) | Thành viên nhóm chat không phải Admin nhóm chat. |
| Admin nhóm chat không thể khôi phục | Tài khoản Admin nhóm chat không còn có thể trở lại hoạt động: đã bị xóa (DELETED); hoặc bị ban vĩnh viễn và đã hết 90 ngày khiếu nại mà không khiếu nại; hoặc khiếu nại lệnh ban vĩnh viễn bị bác. Mọi trường hợp khác (đang vô hiệu hóa trong 14 ngày, ban tạm thời, ban vĩnh viễn còn trong hạn khiếu nại hoặc khiếu nại chưa có kết quả) là còn khôi phục được. |
| Hộp thư Chat | Nơi người dùng thấy các cuộc trò chuyện của mình, kể cả nhóm chat mình là thành viên cũ; biểu tượng Tin nhắn (M07) dẫn tới đây. |
| Tin nhắn | Một lần gửi nội dung văn bản (kèm emoji) của một thành viên trong một cuộc trò chuyện. |
| Từ (tin nhắn) | Đơn vị đếm độ dài tin nhắn: một chuỗi ký tự ngăn cách bởi khoảng trắng. |
| Thời điểm gửi | Lúc hệ thống nhận tin nhắn. Mốc tính thời hạn thu hồi, giới hạn tần suất và thứ tự tin trong cuộc trò chuyện. |
| Tin nhắn mới nhất | Tin nhắn có thời điểm gửi sau cùng trong một cuộc trò chuyện, kể cả tin đã thu hồi. |
| 60 giây gần nhất | Các tin có thời điểm gửi sau mốc (thời điểm gửi của tin đang xét − 60 giây); tin gửi đúng 60 giây trước không còn được tính. Dùng cho giới hạn 30 tin. |
| Thu hồi | Người gửi gỡ tin nhắn của mình trong thời hạn; mọi thành viên thấy dòng "Tin nhắn đã bị thu hồi" ở đúng vị trí tin đó. Là xóa mềm: nội dung gốc được giữ, không hiện với ai. |
| 5 phút (thu hồi) | 5 × 60 giây tính từ thời điểm gửi; thu hồi được khi thời gian đã trôi qua không vượt quá 5 phút. |
| Mốc đã đọc | Tin nhắn gần nhất mà một thành viên đã đọc trong một cuộc trò chuyện; mỗi thành viên mỗi cuộc có một mốc. Thành viên đã đọc mọi tin không mới hơn mốc của mình. |
| Đã gửi, Đã xem | Hai trạng thái hiển thị của tin nhắn mới nhất, suy ra từ mốc đã đọc, không lưu trên tin: Đã gửi khi chưa có thành viên nào khác người gửi đọc tới tin đó; Đã xem khi đã có. |
| Đang xem ở cuối cuộc trò chuyện | Thành viên đang mở cuộc trò chuyện, cửa sổ đang hiển thị (không bị ẩn) và danh sách tin đang ở cuối, không cuộn lên đọc tin cũ. |
| Công tắc duyệt thành viên mới | Cài đặt của nhóm chat do Admin nhóm chat bật, tắt; Tắt khi tạo nhóm. Khi bật, người do Member thêm và người xin gia nhập qua link phải được Admin nhóm chat duyệt mới vào nhóm. |
| Link mời nhóm chat | Link chung duy nhất của một nhóm chat; mọi thành viên lấy được để gửi cho người khác qua kênh bất kỳ; không hết hạn, không thu hồi, không tạo lại. |
| Đề nghị thêm thành viên | Việc Member thêm một người vào nhóm chat trong lúc công tắc duyệt đang bật; chờ Admin nhóm chat duyệt. Trạng thái: Chờ duyệt, Đã chấp nhận, Đã từ chối. |
| Yêu cầu gia nhập | Việc một người mở link mời và chọn "Xin gia nhập" trong lúc công tắc duyệt đang bật; chờ Admin nhóm chat duyệt. Trạng thái: Chờ duyệt, Đã chấp nhận, Đã từ chối. |
| Người chờ duyệt | Người có đề nghị thêm thành viên hoặc yêu cầu gia nhập đang Chờ duyệt ở một nhóm chat. Không tính vào giới hạn 100 thành viên. Thứ tự chờ tính theo lúc đề nghị hoặc yêu cầu được tạo. |
| Cờ tính năng Chat | Công tắc cấu hình (M10) bật hoặc tắt cả module Chat. |
| Giờ Việt Nam | Múi giờ Asia/Ho_Chi_Minh (UTC+7); mọi thời điểm hiển thị trong module tính theo múi giờ này. |

### 2.2 Viết tắt

| Viết tắt | Đầy đủ |
|---|---|
| FR | Functional Requirement — yêu cầu chức năng |
| BR | Business Rule — quy tắc nghiệp vụ |
| TBD | To Be Determined — điểm chưa chốt |

## 3. Thông tin đầu vào

### 3.1 Tài liệu đầu vào

| Tài liệu | Phiên bản / mốc |
|---|---|
| Draft: docs/_temp/iShare_modules.md, iShare_specs_general.md | Theo ngày sửa tệp |
| Register: decisions, qa-log, issue-queue, open-issues, glossary, module-registry | DEC-257, QA-455, ISS-393, OPEN-012 (khớp `moc_nguon`) |

### 3.2 Tài liệu liên quan

| Module | Liên quan ở điểm nào |
|---|---|
| M01 Authentication & Account | Nhắn tin cần đăng nhập; trạng thái tài khoản (bị ban, vô hiệu hóa, đã xóa) quyết định bắt đầu 1-1, thêm vào nhóm, gửi tin và cách hiện người gửi; người gửi của tài khoản đã xóa hiện "[Người dùng đã xóa]". |
| M02 User Profile | Avatar, display_name hiện ở người gửi tin nhắn, ở hộp thư và ở danh sách người đã xem; nút "Nhắn tin" trên hồ sơ. |
| M07 Notification | Thông báo tin nhắn mới trong ứng dụng (không email), popup, biểu tượng Tin nhắn đếm số cuộc có tin chưa đọc theo mốc đã đọc của M16, tắt thông báo Chat. |
| M08 Moderation | Tin nhắn chưa báo cáo được ở MS1; không quét AI tin nhắn. |
| M09 Appeal | Tài khoản bị ban chỉ khiếu nại được; hạn và kết quả khiếu nại lệnh ban vĩnh viễn quyết định Admin nhóm chat còn khôi phục được không. |
| M10 Admin Panel | Cờ tính năng Chat. |
| M11 Group | Nhóm chat độc lập với Group, không phụ thuộc thành viên nhóm; link mời theo cùng cách với link mời của Group. |
| M13 AI Layer | Lớp AI không chấm điểm, không quét tin nhắn chat. |

## 4. Tổng quan chức năng

### 4.1 Luật, tiêu chuẩn liên quan

Không có.

### 4.2 Vai trò

| Vai trò | Mô tả trong module này |
|---|---|
| Guest | Người chưa đăng nhập. Không dùng được Chat; mở link mời thì phải đăng nhập. |
| User | Người dùng đã đăng nhập. Bắt đầu trò chuyện 1-1 với bất kỳ người dùng nào khác, không cần theo dõi; tạo nhóm chat; xin gia nhập nhóm chat qua link mời. Với cuộc trò chuyện mình không thuộc, User không xem và không nhắn được, trừ phần lịch sử của nhóm chat mình là thành viên cũ. Trong một cuộc trò chuyện cụ thể, User mang một vai trò theo ngữ cảnh bên dưới. |
| Thành viên cuộc trò chuyện | Vai trò theo ngữ cảnh: một trong hai người của cuộc trò chuyện 1-1, hoặc một thành viên của nhóm chat. Xem cuộc trò chuyện và toàn bộ lịch sử, gửi tin, thu hồi tin của mình; trong nhóm chat còn thêm thành viên, lấy link mời, đổi tên nhóm, rời nhóm. |
| Thành viên cũ | Vai trò theo ngữ cảnh: người đã rời hoặc bị xóa khỏi một nhóm chat. Giữ nhóm trong hộp thư, chỉ đọc lịch sử tới thời điểm rời; không gửi tin, không thấy tin sau đó. |
| Admin nhóm chat | Vai trò theo ngữ cảnh: thành viên quản trị một nhóm chat, ban đầu là người tạo; mỗi nhóm chat có tối đa một Admin nhóm chat. Có quyền của thành viên, thêm: bật, tắt duyệt thành viên mới, duyệt người chờ vào nhóm, xóa thành viên, chuyển quyền cho thành viên khác. Phải chuyển quyền trước khi rời, trừ khi là thành viên cuối cùng. Khác vai trò hệ thống ADMIN. |
| Mod | Vai trò hệ thống MODERATOR. Trong Chat có quyền như User; không xem được cuộc trò chuyện mình không thuộc, không kiểm duyệt tin nhắn. |
| Admin | Vai trò hệ thống ADMIN. Có quyền như Mod trong Chat; vẫn dùng được Chat khi cờ tính năng Chat tắt. |
| Hệ thống | Giao tin nhắn, thu hồi và trạng thái đã xem tới các thành viên ngay khi có; ghi mốc đã đọc; giới hạn tần suất gửi; tự tắt duyệt khi Admin nhóm chat không thể khôi phục; chặn thao tác khi cờ Chat tắt hoặc khi tài khoản bị ban. |

### 4.3 Ma trận quyền

Cột Thành viên, Admin nhóm chat là vai trò của người dùng trong chính cuộc trò chuyện đang xét; cột User, Mod, Admin là
tài khoản đã đăng nhập nhưng không thuộc cuộc trò chuyện đó.

| Hành động | Guest | User | Thành viên | Admin nhóm chat | Mod | Admin | Yêu cầu |
|---|---|---|---|---|---|---|---|
| Bắt đầu trò chuyện 1-1 với người dùng khác | ✗ | ✓ | — | — | ✓ | ✓ | FR-M16-01.01, FR-M16-01.03 |
| Tạo nhóm chat | ✗ | ✓ | — | — | ✓ | ✓ | FR-M16-02.01, FR-M16-02.06 |
| Xem hộp thư Chat | ✗ | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | FR-M16-03.01, FR-M16-03.02 |
| Xem cuộc trò chuyện và lịch sử tin nhắn | ✗ | ✗ | ✓ | ✓ | ✗ | ✗ | FR-M16-04.01, FR-M16-04.08 |
| Xem lại lịch sử nhóm chat mình đã rời hoặc bị xóa (tới thời điểm rời) | — | ✓ (của mình) | — | — | ✓ (của mình) | ✓ (của mình) | FR-M16-04.10 |
| Gửi tin nhắn | ✗ | ✗ | ✓ | ✓ | ✗ | ✗ | FR-M16-05.01, FR-M16-05.06 |
| Thu hồi tin nhắn (trong 5 phút từ lúc gửi) | ✗ | ✗ | ✓ (của mình) | ✓ (của mình) | ✗ | ✗ | FR-M16-06.01, FR-M16-06.04 |
| Sửa tin nhắn đã gửi | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | FR-M16-05.07 |
| Thêm thành viên vào nhóm chat | ✗ | ✗ | ✓ | ✓ | ✗ | ✗ | FR-M16-08.01, FR-M16-08.06 |
| Lấy link mời nhóm chat | ✗ | ✗ | ✓ | ✓ | ✗ | ✗ | FR-M16-08.10, FR-M16-08.12 |
| Xin gia nhập nhóm chat qua link mời | ✗ | ✓ | — | — | ✓ | ✓ | FR-M16-16.03, FR-M16-16.02 |
| Bật, tắt duyệt thành viên mới | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ | FR-M16-09.01, FR-M16-09.02 |
| Duyệt người chờ vào nhóm chat | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ | FR-M16-10.01, FR-M16-10.04 |
| Xóa thành viên khỏi nhóm chat | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ | FR-M16-11.01, FR-M16-11.02 |
| Đổi tên nhóm chat | ✗ | ✗ | ✓ | ✓ | ✗ | ✗ | FR-M16-12.01, FR-M16-12.02 |
| Chuyển quyền Admin nhóm chat | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ | FR-M16-13.01, FR-M16-13.02 |
| Rời nhóm chat | — | — | ✓ | ✓ (sau khi chuyển quyền, hoặc khi là thành viên cuối cùng) | — | — | FR-M16-14.01, FR-M16-14.02, FR-M16-14.04 |
| Mọi thao tác Chat khi tài khoản đang bị ban | — | ✗ | ✗ | ✗ | ✗ | ✗ | FR-M16-03.03 |
| Dùng Chat khi cờ tính năng Chat tắt | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | FR-M16-15.01, FR-M16-15.04 |

<!-- Ô nói thẳng: hàng 1 (QA-011 Guest không nhắn tin; QA-220, ISS-162 mọi người dùng đã đăng nhập nhắn cho bất kỳ ai);
     hàng 2 (QA-221 ai cũng tạo được; QA-011); hàng 4, 6 cột Thành viên, Admin nhóm chat (DM-6.1, DM-6.2);
     hàng 5 (DEC-249 thành viên cũ đọc lịch sử tới lúc rời); hàng 7 (QA-214–216 thu hồi tin của mình);
     hàng 8 (QA-213); hàng 9, 12–17 cột Thành viên, Admin nhóm chat (QA-222); hàng 10 (DEC-251 mọi thành viên lấy
     link); hàng 11 (DEC-251 người mở link xin gia nhập, Guest phải đăng nhập); hàng 17 cột Admin nhóm chat (DEC-249
     thành viên cuối cùng); hàng 18 (ISS-114, DEC-197); hàng 19 (DEC-225, DEC-256).
     Ô suy ra: hàng 1, 2, 11 cột Mod, Admin (Mod, Admin cũng là người dùng đã đăng nhập); hàng 3 (hộp thư là nơi biểu
     tượng Tin nhắn dẫn tới, DEC-067, mỗi người có hộp thư của mình; Guest không dùng Chat, QA-011); hàng 4, 6, 9, 10,
     15 cột User, Mod, Admin (chat là kênh riêng tư 1-1/nhóm nhỏ, không thuộc kiểm duyệt, QA-214, QA-217; chỉ thành
     viên trong cuộc); hàng 7 cột Admin nhóm chat chỉ "của mình" (QA-222 liệt kê đủ quyền của Admin nhóm chat, không có
     thu hồi tin người khác); hàng 12–14, 16 cột User, Mod, Admin (chỉ Admin nhóm chat, QA-222); hàng 19 cột Guest
     (QA-011).
     "—": hàng 1, 2, 11 cột vai trò trong cuộc (bắt đầu, tạo, xin gia nhập không gắn với cuộc đang xét); hàng 5 cột
     vai trò trong cuộc (người đang là thành viên xem toàn bộ, hàng 4); hàng 17 người không thuộc nhóm chat; hàng 18
     Guest không có tài khoản. -->

### 4.4 Danh sách chức năng

| ID | Chức năng | Tác nhân chính | Kích hoạt |
|---|---|---|---|
| FR-M16-01 | Bắt đầu trò chuyện 1-1 | User | Người dùng chọn nhắn tin cho một người dùng khác |
| FR-M16-02 | Tạo nhóm chat | User | Người dùng chọn tạo nhóm chat, đặt tên và chọn thành viên |
| FR-M16-03 | Xem hộp thư Chat | User | Người dùng mở hộp thư Chat (kể cả qua biểu tượng Tin nhắn của M07) |
| FR-M16-04 | Xem cuộc trò chuyện và lịch sử tin nhắn | Thành viên cuộc trò chuyện | Thành viên (hoặc thành viên cũ) mở một cuộc trò chuyện hoặc cuộn lên để xem tin cũ hơn |
| FR-M16-05 | Gửi tin nhắn | Thành viên cuộc trò chuyện | Thành viên gửi một tin nhắn trong cuộc trò chuyện |
| FR-M16-06 | Thu hồi tin nhắn | Thành viên cuộc trò chuyện | Người gửi chọn thu hồi một tin nhắn của mình |
| FR-M16-07 | Ghi nhận đã đọc và hiển thị Đã xem | Hệ thống | Thành viên mở cuộc trò chuyện, gửi tin, hoặc có tin mới tới khi thành viên đang xem ở cuối cuộc trò chuyện |
| FR-M16-08 | Thêm, mời thành viên vào nhóm chat | Thành viên cuộc trò chuyện | Thành viên nhóm chat chọn thêm người dùng vào nhóm hoặc lấy link mời |
| FR-M16-09 | Bật, tắt duyệt thành viên mới | Admin nhóm chat | Admin nhóm chat đổi cài đặt duyệt thành viên mới |
| FR-M16-10 | Duyệt người chờ vào nhóm chat | Admin nhóm chat | Có người được Member thêm hoặc xin gia nhập qua link khi nhóm đang bật duyệt |
| FR-M16-11 | Xóa thành viên khỏi nhóm chat | Admin nhóm chat | Admin nhóm chat chọn xóa một thành viên |
| FR-M16-12 | Đổi tên nhóm chat | Thành viên cuộc trò chuyện | Thành viên nhóm chat đổi tên nhóm |
| FR-M16-13 | Chuyển quyền Admin nhóm chat | Admin nhóm chat | Admin nhóm chat chọn chuyển quyền cho một thành viên khác |
| FR-M16-14 | Rời nhóm chat | Thành viên cuộc trò chuyện | Thành viên chọn rời nhóm chat |
| FR-M16-15 | Chặn thao tác Chat khi cờ tính năng tắt | Hệ thống | Người dùng thao tác với Chat trong lúc cờ tính năng Chat tắt |
| FR-M16-16 | Xin gia nhập nhóm chat qua link mời | User | Người dùng mở link mời của một nhóm chat và chọn "Xin gia nhập" |
| FR-M16-17 | Tự tắt duyệt khi Admin nhóm chat không thể khôi phục | Hệ thống | Tài khoản Admin nhóm chat trở thành không thể khôi phục |

### 4.5 Mốc và ưu tiên

Toàn bộ yêu cầu của module thuộc MS1 (MS1 gồm đủ chức năng của mọi module), ưu tiên **Should** (dòng M16 của bảng
Module List và bảng MoSCoW Summary của module-registry khớp nhau: Should gồm M11, M12, M16). Không có yêu cầu ngoại lệ về
ưu tiên.

## 5. Yêu cầu chức năng

### 5.1 FR-M16-01 Bắt đầu trò chuyện 1-1

**Yêu cầu cấp trên:** Hệ thống phải cho phép người dùng đã đăng nhập bắt đầu trò chuyện 1-1 với bất kỳ người dùng nào khác, không cần theo dõi nhau và không qua bước yêu cầu nhắn tin; mỗi cặp người dùng có đúng một cuộc 1-1.

**Lý do:** Nhắn tin 1-1 mở hoàn toàn, không cần follow, không có message request; rủi ro người lạ nhắn tin được chấp nhận vì đã có giới hạn tần suất làm lớp chặn tối thiểu.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M16-01.01 | Khi người dùng đã đăng nhập chọn nhắn tin cho một người dùng khác, hệ thống phải cho bắt đầu trò chuyện 1-1 với người đó mà không yêu cầu hai người theo dõi nhau (BR-M16-02). |
| FR-M16-01.02 | Khi người dùng gửi tin đầu tiên trong trò chuyện 1-1, hệ thống phải giao tin tới người nhận mà không chờ người nhận chấp nhận (BR-M16-02). |
| FR-M16-01.03 | Nếu Guest chọn nhắn tin cho một người dùng, hệ thống phải từ chối (BR-M16-02). |
| FR-M16-01.04 | Khi một trò chuyện 1-1 được bắt đầu, hệ thống phải đặt đúng hai người dùng làm thành viên của cuộc (BR-M16-01). |
| FR-M16-01.05 | Khi người dùng chọn nhắn tin cho người đã có trò chuyện 1-1 với mình, hệ thống phải mở cuộc đã có với toàn bộ lịch sử thay vì tạo cuộc mới (BR-M16-24). |
| FR-M16-01.06 | Nếu người dùng chọn nhắn tin cho chính mình, hệ thống phải từ chối (BR-M16-24). |
| FR-M16-01.07 | Nếu người dùng chọn nhắn tin cho một tài khoản đang bị ban, đang vô hiệu hóa hoặc đã xóa mà hai người chưa có trò chuyện 1-1, hệ thống phải từ chối bắt đầu cuộc mới (BR-M16-25). |

### 5.2 FR-M16-02 Tạo nhóm chat

**Yêu cầu cấp trên:** Hệ thống phải cho phép người dùng đã đăng nhập tạo nhóm chat có tên, từ 3 tới 100 thành viên, độc lập với Group, và đặt người tạo làm Admin nhóm chat.

**Lý do:** Group Chat là cuộc trò chuyện nhiều người hoàn toàn độc lập, ai cũng tạo được, không liên quan tới việc có chung Group nào; giới hạn 100 thành viên đủ cho nhóm lớp, CLB, nhóm ôn thi mà không biến nhóm chat thành kênh phát tin một chiều.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M16-02.01 | Khi người dùng đã đăng nhập tạo nhóm chat và chọn các người dùng khác, hệ thống phải tạo nhóm chat gồm người tạo và những người được chọn (BR-M16-01). |
| FR-M16-02.02 | Khi tạo nhóm chat, hệ thống phải đặt người tạo làm Admin nhóm chat và những người được chọn làm Member (BR-M16-04). |
| FR-M16-02.03 | Hệ thống phải cho chọn thành viên nhóm chat mà không đòi họ theo dõi người tạo hay cùng thuộc một Group nào (BR-M16-01). |
| FR-M16-02.04 | Nếu tổng số thành viên, gồm cả người tạo, ít hơn 3, hệ thống phải từ chối tạo nhóm chat (BR-M16-03). |
| FR-M16-02.05 | Nếu tổng số thành viên, gồm cả người tạo, nhiều hơn 100, hệ thống phải từ chối tạo nhóm chat (BR-M16-03). |
| FR-M16-02.06 | Nếu Guest chọn tạo nhóm chat, hệ thống phải từ chối (BR-M16-02). |
| FR-M16-02.07 | Nếu tên nhóm chat trống hoặc dài hơn 100 ký tự sau khi bỏ khoảng trắng đầu và cuối, hệ thống phải từ chối tạo nhóm chat (BR-M16-32). |
| FR-M16-02.08 | Khi tạo nhóm chat, hệ thống phải đặt công tắc duyệt thành viên mới ở trạng thái Tắt (BR-M16-06). |
| FR-M16-02.09 | Nếu người được chọn đang bị ban, đang vô hiệu hóa hoặc đã xóa, hệ thống phải từ chối đưa người đó vào nhóm chat (BR-M16-25). |

### 5.3 FR-M16-03 Xem hộp thư Chat

**Yêu cầu cấp trên:** Hệ thống phải cho phép người dùng đã đăng nhập xem các cuộc trò chuyện của mình trong hộp thư Chat, mới nhất trước, có đánh dấu cuộc chưa đọc.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M16-03.01 | Khi người dùng đã đăng nhập mở hộp thư Chat, hệ thống phải liệt kê các cuộc trò chuyện mà người đó là thành viên hoặc thành viên cũ, không liệt kê cuộc của người khác (BR-M16-31). |
| FR-M16-03.02 | Nếu Guest mở hộp thư Chat, hệ thống phải từ chối (BR-M16-02). |
| FR-M16-03.03 | Nếu tài khoản đang bị ban thao tác bất kỳ với Chat, kể cả mở hộp thư, hệ thống phải từ chối (BR-M16-22). |
| FR-M16-03.04 | Hệ thống phải xếp các cuộc trong hộp thư theo thời điểm gửi của tin nhắn mới nhất, mới nhất trước; với nhóm chat mình là thành viên cũ thì theo tin cuối cùng mình còn thấy (BR-M16-31). |
| FR-M16-03.05 | Hệ thống phải hiển thị ở mỗi dòng: tên nhóm chat, hoặc display_name và avatar của người kia với trò chuyện 1-1; nội dung tin mới nhất ("Tin nhắn đã bị thu hồi" nếu tin đó đã thu hồi); thời điểm gửi của tin đó (BR-M16-31). |
| FR-M16-03.06 | Hệ thống phải đánh dấu chưa đọc cuộc có tin nhắn mới hơn mốc đã đọc của người xem trong số tin người đó thấy được (thành viên cũ: tin gửi trước thời điểm rời), theo cùng cách đếm với biểu tượng Tin nhắn (BR-M16-31). |
| FR-M16-03.07 | Hệ thống phải không đưa vào hộp thư trò chuyện 1-1 chưa có tin nhắn nào (BR-M16-31). |
| FR-M16-03.08 | Hệ thống phải tải hộp thư 20 cuộc mỗi lần, cuộn xuống tải tiếp, không giới hạn tổng số cuộc (BR-M16-31). |

### 5.4 FR-M16-04 Xem cuộc trò chuyện và lịch sử tin nhắn

**Yêu cầu cấp trên:** Hệ thống phải cho phép thành viên xem một cuộc trò chuyện, tải dần lịch sử tới tin đầu tiên và thấy tin mới ngay khi có; thành viên cũ chỉ đọc lịch sử tới thời điểm rời.

**Lý do:** Người dùng phải cuộn được tới tận tin nhắn đầu tiên của cuộc trò chuyện; lịch sử chat không có khái niệm hết mức liên quan như kết quả tìm kiếm.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M16-04.01 | Khi thành viên mở một cuộc trò chuyện, hệ thống phải hiển thị 20 tin nhắn mới nhất của cuộc (BR-M16-17). |
| FR-M16-04.02 | Khi thành viên cuộn lên tới tin cũ nhất đang hiển thị, hệ thống phải tải thêm 20 tin cũ hơn kế tiếp (BR-M16-17). |
| FR-M16-04.03 | Hệ thống phải cho thành viên tải tiếp cho tới tin đầu tiên của cuộc, không giới hạn tổng số tin, kể cả với thành viên mới vào hoặc vào lại nhóm chat (BR-M16-17, BR-M16-27). |
| FR-M16-04.04 | Hệ thống phải hiển thị với mỗi tin nhắn: người gửi, nội dung và thời điểm gửi theo giờ Việt Nam. |
| FR-M16-04.05 | Trong khi thành viên đang mở cuộc trò chuyện, hệ thống phải hiển thị tin nhắn mới của cuộc ngay khi có, không cần tải lại trang (BR-M16-16). |
| FR-M16-04.06 | Nếu có tin mới tới trong lúc thành viên đang cuộn lên đọc tin cũ, hệ thống phải giữ nguyên vị trí đang đọc và hiện nhãn "tin nhắn mới" (BR-M16-14). |
| FR-M16-04.07 | Hệ thống phải hiển thị tin nhắn của tài khoản đã xóa với nội dung giữ nguyên và người gửi "[Người dùng đã xóa]" (BR-M16-19). |
| FR-M16-04.08 | Nếu người không là thành viên và không là thành viên cũ của cuộc trò chuyện, kể cả Guest, Mod và Admin, mở cuộc đó, hệ thống phải từ chối. |
| FR-M16-04.09 | Hệ thống phải cung cấp cho M07 cuộc trò chuyện mà mỗi người dùng đang mở, để M07 không hiện popup tin mới của chính cuộc đó. |
| FR-M16-04.10 | Khi thành viên cũ mở nhóm chat mình đã rời hoặc bị xóa, hệ thống phải chỉ hiển thị các tin gửi trước thời điểm rời của người đó, chỉ để đọc (BR-M16-27). |
| FR-M16-04.11 | Hệ thống phải hiển thị người gửi của tài khoản đang vô hiệu hóa là "Tài khoản tạm thời vô hiệu hoá" với avatar mặc định (BR-M16-26). |
| FR-M16-04.12 | Hệ thống phải hiển thị người gửi của tài khoản đang bị ban như tài khoản bình thường (BR-M16-26). |

### 5.5 FR-M16-05 Gửi tin nhắn

**Yêu cầu cấp trên:** Hệ thống phải cho phép thành viên gửi tin nhắn văn bản (kèm emoji) trong cuộc trò chuyện, giao tới các thành viên khác ngay khi có, trong giới hạn độ dài và tần suất.

**Lý do:** Nhắn tin chỉ dạng văn bản vì gọi thoại, gọi video, gửi tệp đòi hỏi hạ tầng media vượt năng lực team 2 người. Giới hạn tần suất để chặn spam, bot gửi dồn, bảo vệ máy chủ, và là lớp chặn tối thiểu khi chưa có chặn, báo cáo tin nhắn; tính theo từng cuộc để chặn đúng việc một người spam một đối tượng mà không cản họ nhắn ở cuộc khác.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M16-05.01 | Khi thành viên gửi một tin nhắn văn bản, có thể kèm emoji, hệ thống phải thêm tin vào cuộc trò chuyện với người gửi và thời điểm gửi (BR-M16-08). |
| FR-M16-05.02 | Khi một tin nhắn được gửi, hệ thống phải giao tin tới các thành viên khác đang mở cuộc ngay khi có (BR-M16-16). |
| FR-M16-05.03 | Khi một tin nhắn được gửi, hệ thống phải báo sự kiện tin nhắn mới cho M07 để gửi thông báo trong ứng dụng tới các thành viên khác của cuộc, không gửi email (BR-M16-21). |
| FR-M16-05.04 | Nếu thành viên đính kèm ảnh hoặc tệp vào tin nhắn, hệ thống phải từ chối (BR-M16-08). |
| FR-M16-05.05 | Nếu người gửi đã gửi 30 tin vào cùng một cuộc trò chuyện trong 60 giây gần nhất, hệ thống phải từ chối tin kế tiếp của người đó trong cuộc đó và báo người gửi đã gửi quá nhanh (BR-M16-09). |
| FR-M16-05.06 | Nếu người không là thành viên của cuộc trò chuyện, kể cả thành viên cũ, Guest, Mod và Admin, gửi tin vào cuộc đó, hệ thống phải từ chối. |
| FR-M16-05.07 | Hệ thống phải không cho bất kỳ ai sửa nội dung tin nhắn đã gửi (BR-M16-10). |
| FR-M16-05.08 | Hệ thống phải giữ tin nhắn vĩnh viễn, không tự xóa theo thời gian (BR-M16-18). |
| FR-M16-05.09 | Hệ thống phải không gửi nội dung tin nhắn đi quét AI (BR-M16-20). |
| FR-M16-05.10 | Hệ thống phải không có thao tác báo cáo tin nhắn và chặn người dùng trong Chat ở MS1 (BR-M16-20). |
| FR-M16-05.11 | Nếu tin nhắn trống hoặc chỉ gồm khoảng trắng, hệ thống phải từ chối gửi (BR-M16-08). |
| FR-M16-05.12 | Nếu tin nhắn dài hơn 1.000 từ, hệ thống phải từ chối gửi (BR-M16-08). |
| FR-M16-05.13 | Nếu thành viên gửi tin trong trò chuyện 1-1 với một tài khoản đã xóa, hệ thống phải từ chối (BR-M16-25). |
| FR-M16-05.14 | Khi thành viên gửi tin trong trò chuyện 1-1 đã có với một tài khoản đang bị ban hoặc đang vô hiệu hóa, hệ thống phải nhận tin để người đó đọc khi tài khoản hoạt động trở lại (BR-M16-25). |

### 5.6 FR-M16-06 Thu hồi tin nhắn

**Yêu cầu cấp trên:** Hệ thống phải cho phép người gửi thu hồi tin nhắn của mình trong 5 phút kể từ lúc gửi, với mọi thành viên của cuộc trò chuyện; thu hồi là xóa mềm.

**Lý do:** 5 phút đủ để xử lý tình huống thường gặp nhất là gửi nhầm người hoặc nhầm nội dung, và đủ ngắn để không phá mạch hội thoại khi tin đã được đọc, phản hồi. Dòng "Tin nhắn đã bị thu hồi" giữ vị trí trong luồng chat, quen với học sinh qua Messenger, Zalo, tránh hụt ngữ cảnh hội thoại. Nội dung gốc được giữ vì tin nhắn chat không bị xóa cứng, nhất quán với nội dung nhóm (M11).

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M16-06.01 | Khi người gửi chọn thu hồi một tin nhắn của mình mà thời gian từ thời điểm gửi chưa quá 5 phút, hệ thống phải thu hồi tin đó với mọi thành viên của cuộc (BR-M16-11). |
| FR-M16-06.02 | Khi một tin nhắn bị thu hồi, hệ thống phải hiển thị dòng "Tin nhắn đã bị thu hồi" ở đúng vị trí của tin đó cho mọi thành viên (BR-M16-12). |
| FR-M16-06.03 | Nếu thời gian từ thời điểm gửi đã quá 5 phút, hệ thống phải từ chối thu hồi (BR-M16-11). |
| FR-M16-06.04 | Nếu người không phải người gửi, kể cả Admin nhóm chat, chọn thu hồi một tin nhắn, hệ thống phải từ chối (BR-M16-11). |
| FR-M16-06.05 | Hệ thống phải chỉ có một kiểu thu hồi áp cho mọi thành viên, không có xóa tin chỉ ở phía người gửi (BR-M16-11). |
| FR-M16-06.06 | Nếu tin nhắn đã bị thu hồi, hệ thống phải từ chối thu hồi lần nữa. |
| FR-M16-06.07 | Khi thu hồi một tin nhắn, hệ thống phải gắn cờ đã thu hồi và giữ nội dung gốc, không hiển thị nội dung đó với bất kỳ ai, kể cả Mod và Admin (BR-M16-12). |
| FR-M16-06.08 | Khi một tin nhắn bị thu hồi, hệ thống phải cập nhật dòng giữ chỗ ngay cho các thành viên đang mở cuộc, không cần tải lại trang (BR-M16-12). |
| FR-M16-06.09 | Khi tin nhắn mới nhất bị thu hồi, hệ thống phải giữ dòng giữ chỗ làm tin nhắn mới nhất, mang trạng thái Đã gửi, Đã xem (BR-M16-12). |

### 5.7 FR-M16-07 Ghi nhận đã đọc và hiển thị Đã xem

**Yêu cầu cấp trên:** Hệ thống phải ghi mốc đã đọc của từng thành viên trong mỗi cuộc trò chuyện và hiển thị người đã xem ở tin nhắn mới nhất, cập nhật ngay cho các thành viên khác.

**Lý do:** "Đã xem" là quan hệ giữa tin nhắn và người đọc, không phải thuộc tính của tin. Mốc đã đọc không lùi để một lần ghi đến lệch thứ tự không làm lùi mốc. Chỉ hiện ở tin mới nhất vì tin mới nhất luôn có sẵn khi mở cuộc. Phải cập nhật ngay cho người khác, nếu không avatar "đã xem" phía người khác không tự đổi, phải tải lại trang mới thấy.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M16-07.01 | Khi thành viên mở một cuộc trò chuyện, hệ thống phải ghi mốc đã đọc của thành viên tới tin nhắn mới nhất của cuộc (BR-M16-14). |
| FR-M16-07.02 | Khi có tin mới tới trong lúc thành viên đang xem ở cuối cuộc trò chuyện, hệ thống phải ghi mốc đã đọc của thành viên tới tin đó (BR-M16-14). |
| FR-M16-07.03 | Trong khi cửa sổ cuộc trò chuyện đang bị ẩn, hệ thống phải hoãn ghi mốc cho tin mới tới khi cửa sổ hiển thị lại (BR-M16-14). |
| FR-M16-07.04 | Khi thành viên đang đọc tin cũ cuộn xuống tới cuối cuộc trò chuyện, hệ thống phải ghi mốc đã đọc tới tin nhắn mới nhất (BR-M16-14). |
| FR-M16-07.05 | Khi ghi mốc đã đọc, hệ thống phải giữ tin mới hơn giữa mốc hiện tại và tin vừa đọc, không để mốc lùi (BR-M16-13). |
| FR-M16-07.06 | Hệ thống phải hiển thị dưới tin nhắn mới nhất avatar của các thành viên đã đọc tới tin đó, gộp khi có nhiều người, trừ người gửi tin đó và chính người đang xem (BR-M16-15). |
| FR-M16-07.07 | Hệ thống phải hiển thị Đã gửi ở tin nhắn mới nhất khi chưa có thành viên nào khác người gửi đọc tới tin đó (BR-M16-15). |
| FR-M16-07.08 | Hệ thống phải không hiển thị trạng thái Đã gửi, Đã xem ở các tin cũ hơn tin nhắn mới nhất, và không hiển thị avatar của thành viên chưa đọc tới tin nhắn mới nhất (BR-M16-15). |
| FR-M16-07.09 | Khi một thành viên có mốc đã đọc mới, hệ thống phải cập nhật hiển thị đã xem cho các thành viên khác đang mở cuộc ngay, không cần tải lại trang (BR-M16-16). |
| FR-M16-07.10 | Hệ thống phải cung cấp cho M07 mốc đã đọc của từng người trong mỗi cuộc trò chuyện và việc cuộc đó có tin chưa đọc mà người đó thấy được hay không (thành viên cũ chỉ tính tin gửi trước thời điểm rời), để M07 đếm số cuộc có tin chưa đọc trên biểu tượng Tin nhắn. |
| FR-M16-07.11 | Khi thành viên gửi một tin nhắn, hệ thống phải ghi mốc đã đọc của người gửi tới tin đó (BR-M16-13). |

### 5.8 FR-M16-08 Thêm, mời thành viên vào nhóm chat

**Yêu cầu cấp trên:** Hệ thống phải cho phép thành viên nhóm chat thêm thẳng người dùng khác vào nhóm hoặc lấy link mời của nhóm để gửi cho người khác; người do Member thêm phải qua duyệt khi công tắc duyệt bật.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M16-08.01 | Khi thành viên nhóm chat thêm một người dùng trong lúc công tắc duyệt thành viên mới đang tắt, hệ thống phải đưa người đó vào nhóm làm Member ngay (BR-M16-06). |
| FR-M16-08.02 | Khi Admin nhóm chat thêm một người dùng, hệ thống phải đưa người đó vào nhóm làm Member ngay, kể cả khi công tắc duyệt đang bật (BR-M16-06). |
| FR-M16-08.03 | Khi Member thêm một người dùng trong lúc công tắc duyệt đang bật, hệ thống phải tạo đề nghị thêm thành viên ở trạng thái Chờ duyệt thay vì đưa người đó vào nhóm (BR-M16-06). |
| FR-M16-08.04 | Hệ thống phải cho thêm người dùng mà không đòi người đó theo dõi người thêm hay cùng thuộc một Group nào (BR-M16-01). |
| FR-M16-08.05 | Nếu nhóm chat đã có 100 thành viên, hệ thống phải từ chối đưa thêm người vào nhóm (BR-M16-03). |
| FR-M16-08.06 | Nếu người không là thành viên của nhóm chat, kể cả thành viên cũ, Guest, Mod và Admin, thêm người vào nhóm, hệ thống phải từ chối (BR-M16-05). |
| FR-M16-08.07 | Nếu người được thêm đã là thành viên của nhóm chat, hệ thống phải không thêm lần nữa. |
| FR-M16-08.08 | Khi thành viên thêm một thành viên cũ của nhóm, hệ thống phải xử lý như thêm người dùng mới, theo công tắc duyệt hiện tại (BR-M16-28). |
| FR-M16-08.09 | Nếu người được thêm đang bị ban, đang vô hiệu hóa hoặc đã xóa, hệ thống phải từ chối thêm (BR-M16-25). |
| FR-M16-08.10 | Khi thành viên nhóm chat lấy link mời, hệ thống phải đưa ra link mời chung duy nhất của nhóm (BR-M16-29). |
| FR-M16-08.11 | Hệ thống phải giữ link mời của nhóm chat không hết hạn và không cho thu hồi hay tạo lại (BR-M16-29). |
| FR-M16-08.12 | Nếu người không là thành viên của nhóm chat lấy link mời, hệ thống phải từ chối (BR-M16-29). |
| FR-M16-08.13 | Hệ thống phải không gửi thông báo "được mời" khi thành viên thêm người hay gửi link mời (BR-M16-29). |

### 5.9 FR-M16-09 Bật, tắt duyệt thành viên mới

**Yêu cầu cấp trên:** Hệ thống phải cho phép Admin nhóm chat bật, tắt công tắc duyệt thành viên mới của nhóm.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M16-09.01 | Khi Admin nhóm chat bật hoặc tắt công tắc duyệt thành viên mới, hệ thống phải áp cài đặt mới cho các lần thêm thành viên và xin gia nhập sau đó (BR-M16-06). |
| FR-M16-09.02 | Nếu Member hoặc người không là thành viên của nhóm chat đổi công tắc duyệt, hệ thống phải từ chối (BR-M16-05). |
| FR-M16-09.03 | Khi Admin nhóm chat tắt công tắc duyệt, hệ thống phải chấp nhận ngay người chờ duyệt của nhóm theo thứ tự bắt đầu chờ, sớm nhất trước, cho tới khi nhóm đủ 100 thành viên (BR-M16-33). |
| FR-M16-09.04 | Khi công tắc duyệt được tắt mà nhóm không đủ chỗ cho mọi người chờ duyệt, hệ thống phải chuyển những người không vào được sang Đã từ chối (BR-M16-33). |

### 5.10 FR-M16-10 Duyệt người chờ vào nhóm chat

**Yêu cầu cấp trên:** Hệ thống phải cho phép Admin nhóm chat chấp nhận hoặc từ chối người chờ duyệt: người được Member đề nghị thêm và người xin gia nhập qua link mời.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M16-10.01 | Khi Admin nhóm chat chấp nhận một đề nghị thêm thành viên hoặc yêu cầu gia nhập đang Chờ duyệt, hệ thống phải đưa người đó vào nhóm làm Member và chuyển đề nghị, yêu cầu sang Đã chấp nhận (BR-M16-06). |
| FR-M16-10.02 | Khi Admin nhóm chat từ chối một đề nghị thêm thành viên hoặc yêu cầu gia nhập đang Chờ duyệt, hệ thống phải chuyển đề nghị, yêu cầu sang Đã từ chối và không đưa người đó vào nhóm (BR-M16-06). |
| FR-M16-10.03 | Nếu Admin nhóm chat chấp nhận khi nhóm đã có 100 thành viên, hệ thống phải từ chối thao tác (BR-M16-03). |
| FR-M16-10.04 | Nếu Member hoặc người không là thành viên của nhóm chat chấp nhận hoặc từ chối người chờ duyệt, hệ thống phải từ chối (BR-M16-05). |
| FR-M16-10.05 | Hệ thống phải hiển thị cho Admin nhóm chat các đề nghị thêm thành viên và yêu cầu gia nhập đang Chờ duyệt của nhóm. |
| FR-M16-10.06 | Nếu đề nghị hoặc yêu cầu không còn ở trạng thái Chờ duyệt, hệ thống phải từ chối chấp nhận hoặc từ chối nó. |
| FR-M16-10.07 | Hệ thống phải không tính người chờ duyệt vào giới hạn 100 thành viên; giới hạn được kiểm lúc người đó vào nhóm (BR-M16-03). |

### 5.11 FR-M16-11 Xóa thành viên khỏi nhóm chat

**Yêu cầu cấp trên:** Hệ thống phải cho phép Admin nhóm chat xóa một thành viên khỏi nhóm chat.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M16-11.01 | Khi Admin nhóm chat xóa một Member, hệ thống phải đưa người đó ra khỏi nhóm với trạng thái Bị xóa và giữ nhóm trong hộp thư của người đó như thành viên cũ (BR-M16-05, BR-M16-27). |
| FR-M16-11.02 | Nếu Member hoặc người không là thành viên của nhóm chat xóa thành viên, hệ thống phải từ chối (BR-M16-05). |
| FR-M16-11.03 | Khi nhóm chat còn dưới 3 thành viên sau khi có người bị xóa, hệ thống phải giữ nhóm hoạt động bình thường (BR-M16-03). |

### 5.12 FR-M16-12 Đổi tên nhóm chat

**Yêu cầu cấp trên:** Hệ thống phải cho phép mọi thành viên nhóm chat đổi tên nhóm.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M16-12.01 | Khi một thành viên nhóm chat đổi tên nhóm, hệ thống phải áp tên mới cho nhóm với mọi thành viên (BR-M16-05). |
| FR-M16-12.02 | Nếu người không là thành viên của nhóm chat, kể cả thành viên cũ, Guest, Mod và Admin, đổi tên nhóm, hệ thống phải từ chối (BR-M16-05). |
| FR-M16-12.03 | Nếu tên mới trống hoặc dài hơn 100 ký tự sau khi bỏ khoảng trắng đầu và cuối, hệ thống phải từ chối (BR-M16-32). |

### 5.13 FR-M16-13 Chuyển quyền Admin nhóm chat

**Yêu cầu cấp trên:** Hệ thống phải cho phép Admin nhóm chat chủ động chuyển quyền quản trị cho một thành viên khác; hệ thống không tự chuyển quyền.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M16-13.01 | Khi Admin nhóm chat chuyển quyền cho một Member, hệ thống phải đặt Member đó làm Admin nhóm chat và người chuyển làm Member (BR-M16-07). |
| FR-M16-13.02 | Nếu Member hoặc người không là thành viên của nhóm chat chuyển quyền Admin nhóm chat, hệ thống phải từ chối (BR-M16-05). |
| FR-M16-13.03 | Hệ thống phải không tự chuyển quyền Admin nhóm chat cho thành viên nào, kể cả khi Admin nhóm chat bị ban, vô hiệu hóa hoặc xóa tài khoản (BR-M16-07, BR-M16-30). |

### 5.14 FR-M16-14 Rời nhóm chat

**Yêu cầu cấp trên:** Hệ thống phải cho phép thành viên tự rời nhóm chat; Admin nhóm chat chỉ rời được sau khi chuyển quyền, trừ khi là thành viên cuối cùng.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M16-14.01 | Khi Member chọn rời nhóm chat, hệ thống phải đưa người đó ra khỏi nhóm với trạng thái Đã rời và giữ nhóm trong hộp thư của người đó như thành viên cũ (BR-M16-05, BR-M16-27). |
| FR-M16-14.02 | Nếu Admin nhóm chat chọn rời nhóm còn thành viên khác khi chưa chuyển quyền, hệ thống phải từ chối (BR-M16-07). |
| FR-M16-14.03 | Hệ thống phải phân biệt thành viên tự rời nhóm với thành viên bị Admin nhóm chat xóa (BR-M16-05). |
| FR-M16-14.04 | Khi Admin nhóm chat là thành viên cuối cùng chọn rời, hệ thống phải cho rời mà không cần chuyển quyền; nhóm không còn thành viên nào gửi được tin (BR-M16-07). |
| FR-M16-14.05 | Khi nhóm chat còn dưới 3 thành viên sau khi có người rời, hệ thống phải giữ nhóm hoạt động bình thường (BR-M16-03). |

### 5.15 FR-M16-15 Chặn thao tác Chat khi cờ tính năng tắt

**Yêu cầu cấp trên:** Hệ thống phải từ chối thao tác của người dùng không phải Admin với Chat trong lúc cờ tính năng Chat tắt, giữ nguyên dữ liệu và lối vào.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M16-15.01 | Trong khi cờ tính năng Chat tắt, nếu người dùng không phải Admin thao tác với Chat, hệ thống phải từ chối với thông báo "Hệ thống đang bận, vui lòng thử lại sau" (BR-M16-23). |
| FR-M16-15.02 | Trong khi cờ tính năng Chat tắt, hệ thống phải giữ nguyên các lối vào Chat (BR-M16-23). |
| FR-M16-15.03 | Trong khi cờ tính năng Chat tắt, hệ thống phải không xóa hay đổi dữ liệu của Chat (BR-M16-23). |
| FR-M16-15.04 | Trong khi cờ tính năng Chat tắt, hệ thống phải cho Admin dùng Chat như khi cờ bật (BR-M16-23). |
| FR-M16-15.05 | Khi cờ tính năng Chat được bật lại, hệ thống phải không làm bù thao tác đã bị từ chối trong lúc cờ tắt (BR-M16-23). |
| FR-M16-15.06 | Trong khi cờ tính năng Chat tắt, hệ thống phải từ chối theo FR-M16-15.01 các thao tác: mở hộp thư, mở cuộc trò chuyện, bắt đầu trò chuyện 1-1, tạo nhóm chat, gửi tin, thu hồi tin, thêm thành viên, xóa thành viên, duyệt người chờ, đổi tên nhóm, chuyển quyền Admin nhóm chat, rời nhóm, bật tắt duyệt, lấy link mời, xin gia nhập (BR-M16-23). |
| FR-M16-15.07 | Trong khi cờ tính năng Chat tắt, hệ thống phải vẫn hiển thị biểu tượng Tin nhắn cùng số chưa đọc (M07) và nút "Nhắn tin" trên hồ sơ (BR-M16-23). |
| FR-M16-15.08 | Trong khi cờ tính năng Chat tắt, hệ thống phải vẫn tự tắt duyệt khi Admin nhóm chat không thể khôi phục (FR-M16-17) và vẫn tính hạn thu hồi 5 phút theo thời gian thực (BR-M16-23). |

### 5.16 FR-M16-16 Xin gia nhập nhóm chat qua link mời

**Yêu cầu cấp trên:** Hệ thống phải cho phép người dùng đã đăng nhập mở link mời của một nhóm chat và xin gia nhập; vào ngay khi duyệt tắt, chờ Admin nhóm chat duyệt khi duyệt bật.

**Lý do:** Lời mời vào nhóm chat có hai cách: thành viên thêm thẳng, hoặc gửi link để người kia tự xin gia nhập; link mời theo cùng cách với link mời của Group.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M16-16.01 | Khi người dùng đã đăng nhập mở link mời của một nhóm chat, hệ thống phải hiển thị tên nhóm chat và nút "Xin gia nhập", không hiển thị tin nhắn của nhóm (BR-M16-29). |
| FR-M16-16.02 | Nếu Guest mở link mời, hệ thống phải yêu cầu đăng nhập trước khi xin gia nhập (BR-M16-29). |
| FR-M16-16.03 | Khi người dùng xin gia nhập trong lúc công tắc duyệt đang tắt, hệ thống phải đưa người đó vào nhóm làm Member ngay (BR-M16-06). |
| FR-M16-16.04 | Khi người dùng xin gia nhập trong lúc công tắc duyệt đang bật, hệ thống phải tạo yêu cầu gia nhập ở trạng thái Chờ duyệt (BR-M16-06). |
| FR-M16-16.05 | Nếu nhóm chat đã có 100 thành viên, hệ thống phải từ chối xin gia nhập (BR-M16-29). |
| FR-M16-16.06 | Nếu người dùng đang có một yêu cầu gia nhập Chờ duyệt tới cùng nhóm chat, hệ thống phải từ chối gửi thêm yêu cầu (BR-M16-29). |
| FR-M16-16.07 | Khi yêu cầu gia nhập của một người bị từ chối, hệ thống phải cho người đó gửi yêu cầu mới ngay, không giới hạn số lần (BR-M16-29). |
| FR-M16-16.08 | Khi thành viên cũ xin gia nhập lại qua link mời, hệ thống phải xử lý như người dùng mới, theo công tắc duyệt hiện tại (BR-M16-28). |

### 5.17 FR-M16-17 Tự tắt duyệt khi Admin nhóm chat không thể khôi phục

**Yêu cầu cấp trên:** Hệ thống phải tự tắt công tắc duyệt thành viên mới của nhóm chat khi Admin nhóm chat không thể khôi phục, và không đổi gì trong lúc Admin còn khôi phục được.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M16-17.01 | Trong khi tài khoản Admin nhóm chat còn khôi phục được, hệ thống phải giữ nguyên Admin và mọi cài đặt của nhóm chat (BR-M16-30). |
| FR-M16-17.02 | Khi Admin nhóm chat trở thành không thể khôi phục và công tắc duyệt đang bật, hệ thống phải tắt công tắc duyệt và xử lý người chờ duyệt như FR-M16-09.03, FR-M16-09.04 (BR-M16-30, BR-M16-33). |
| FR-M16-17.03 | Khi Admin nhóm chat trở thành không thể khôi phục, hệ thống phải để nhóm chat không có Admin nhóm chat (BR-M16-30). |

### 5.18 Quy tắc nghiệp vụ

| ID | Loại | Quy tắc | Ví dụ |
|---|---|---|---|
| BR-M16-01 | Sự kiện | Chat có hai loại cuộc trò chuyện: trò chuyện 1-1 giữa đúng hai người dùng, và nhóm chat nhiều người. Nhóm chat độc lập với Group (M11): ai cũng tạo được, không đòi các thành viên cùng thuộc một nhóm nào. | A, B, C không chung Group nào → A vẫn tạo được nhóm chat với B, C. |
| BR-M16-02 | Ràng buộc | Mọi người dùng đã đăng nhập bắt đầu được trò chuyện 1-1 với bất kỳ người dùng nào khác, không cần theo dõi nhau, không có bước yêu cầu nhắn tin chờ người nhận chấp nhận. Guest không dùng được Chat. | A không theo dõi B, B không theo dõi A → A nhắn B được, tin tới B ngay. Guest bấm nhắn tin → bị từ chối. |
| BR-M16-03 | Ràng buộc | Nhóm chat phải có từ 3 thành viên (gồm người tạo) khi tạo, và có tối đa 100 thành viên ở mọi lúc. Quy tắc "từ 3" chỉ kiểm khi tạo: nhóm còn 2 hoặc 1 thành viên sau khi có người rời, bị xóa vẫn là nhóm chat bình thường, vẫn nhắn và thêm người được. Người chờ duyệt không tính vào 100; giới hạn được kiểm lúc người đó vào nhóm. | A tạo nhóm với B, C → được. A chọn chỉ B → bị từ chối. C rời → A, B vẫn nhắn, thêm D được. Nhóm có 100 thành viên và 5 người chờ duyệt → hợp lệ; Admin chấp nhận 1 người → bị từ chối. |
| BR-M16-04 | Sự kiện | Nhóm chat có hai vai trò: Admin nhóm chat và Member. Người tạo là Admin nhóm chat đầu tiên; mỗi nhóm chat có tối đa một Admin nhóm chat. | A tạo nhóm với B, C → A là Admin nhóm chat; B, C là Member. |
| BR-M16-05 | Ràng buộc | Quyền trong nhóm chat: mọi thành viên thêm được người khác, lấy được link mời, đổi tên nhóm, tự rời nhóm; chỉ Admin nhóm chat bật, tắt công tắc duyệt thành viên mới, duyệt người chờ, xóa thành viên, chuyển quyền Admin nhóm chat. Rời nhóm (thành viên tự làm) và bị xóa (Admin nhóm chat làm) là hai thao tác tách biệt. | Member B thêm D → được. Member B xóa C → bị từ chối. Member B đổi tên nhóm thành "Ôn thi Lý" → được. |
| BR-M16-06 | Kích hoạt | Công tắc duyệt thành viên mới là Tắt khi tạo nhóm. Khi công tắc bật: người do Member thêm thành đề nghị thêm thành viên, người xin qua link mời thành yêu cầu gia nhập, cả hai chờ Admin nhóm chat chấp nhận hoặc từ chối; người do Admin nhóm chat thêm vào ngay. Khi công tắc tắt: người được thêm hay xin qua link đều vào ngay. Admin nhóm chat tắt công tắc thì người chờ duyệt được chấp nhận ngay theo BR-M16-33. | Công tắc bật: Member B thêm D → D chờ; E xin qua link → E chờ; Admin A thêm F → F vào ngay. A tắt công tắc → D, E vào ngay. Công tắc tắt: B thêm G → G vào ngay. |
| BR-M16-07 | Ràng buộc | Admin nhóm chat muốn rời nhóm còn thành viên khác phải chủ động chuyển quyền cho một thành viên khác trước; chưa chuyển thì không rời được. Admin nhóm chat là thành viên cuối cùng thì rời không cần chuyển quyền; nhóm không còn thành viên nào gửi được tin. Hệ thống không tự chuyển quyền Admin nhóm chat (khác kế nhiệm Owner của Group M11). Sau khi chuyển, người nhận là Admin nhóm chat, người chuyển là Member. | Nhóm A (Admin), B, C: A bấm rời → bị từ chối; A chuyển cho B → B là Admin, A là Member; A rời → được. Nhóm chỉ còn A → A rời được ngay. |
| BR-M16-08 | Ràng buộc | Nội dung tin nhắn là văn bản, có thể kèm emoji; tối đa 1.000 từ; không trống, không chỉ gồm khoảng trắng. Không gửi được ảnh, tệp đính kèm; không có gọi thoại, gọi video. | "Mai thi nhé 😀" → gửi được. Tin 1.000 từ → được; 1.001 từ → bị từ chối. Tin chỉ có ba dấu cách → bị từ chối. Đính kèm ảnh bài tập → bị từ chối. |
| BR-M16-09 | Ràng buộc | Mỗi người gửi được tối đa 30 tin nhắn trong 60 giây gần nhất trong cùng một cuộc trò chuyện; giới hạn tính riêng cho từng cuộc của người đó. Tin vượt giới hạn bị từ chối và người gửi được báo đã gửi quá nhanh. | Tin #1 vào cuộc X lúc 10:00:00, tin #30 lúc 10:00:40 → tin #31 lúc 10:00:59 bị từ chối; lúc 10:01:00 được (tin #1 đã ra khỏi 60 giây). Cùng lúc 10:00:59 gửi vào cuộc Y → được. |
| BR-M16-10 | Ràng buộc | Tin nhắn đã gửi không sửa được dưới bất kỳ hình thức nào. | A gửi "Phòng 12" rồi muốn sửa thành "Phòng 21" → không có thao tác sửa; A chỉ thu hồi được (nếu còn hạn) rồi gửi tin mới. |
| BR-M16-11 | Ràng buộc | Người gửi thu hồi được tin nhắn của mình khi thời gian từ thời điểm gửi tới lúc thu hồi không quá 5 phút. Chỉ có một kiểu thu hồi, áp cho mọi thành viên của cuộc trò chuyện; không có xóa "chỉ ở phía tôi". Quá 5 phút thì tin không xóa hay ẩn được nữa. | Gửi 20:00:00 → thu hồi 20:04:59 được; 20:05:00 được (đúng 5 phút); 20:05:01 bị từ chối. B thu hồi tin của A → bị từ chối. |
| BR-M16-12 | Kích hoạt | Thu hồi là xóa mềm: tin được gắn cờ đã thu hồi, nội dung gốc được giữ nhưng không hiện với ai, kể cả Mod, Admin, ở MS1. Mọi thành viên thấy dòng "Tin nhắn đã bị thu hồi" ở đúng vị trí cũ; thành viên đang mở cuộc thấy ngay. Tin mới nhất bị thu hồi thì dòng giữ chỗ vẫn là tin mới nhất và mang trạng thái Đã gửi, Đã xem. | Cuộc có #10, #11, #12; A thu hồi #11 → mọi người thấy #10, "Tin nhắn đã bị thu hồi", #12; nội dung #11 vẫn lưu, không ai xem được. A thu hồi #12 (mới nhất) → dưới dòng giữ chỗ vẫn hiện avatar người đã xem. |
| BR-M16-13 | Tính toán | Mỗi thành viên có một mốc đã đọc trong mỗi cuộc trò chuyện. Khi ghi mốc mới, mốc lấy tin mới hơn trong hai tin: mốc hiện tại và tin vừa đọc; mốc không bao giờ lùi. Một tin được coi là thành viên đã đọc khi tin đó không mới hơn mốc của thành viên. Gửi một tin thì mốc của người gửi được đưa tới tin đó. | Mốc của B là tin #40. Một lần ghi đến muộn mang tin #38 → mốc giữ #40. Ghi tin #45 → mốc thành #45. B gửi #46 → mốc B = #46. |
| BR-M16-14 | Kích hoạt | Hệ thống ghi mốc đã đọc của thành viên tới tin nhắn mới nhất khi: (1) thành viên mở cuộc trò chuyện; hoặc (2) có tin mới tới trong lúc thành viên đang xem ở cuối cuộc trò chuyện. Nếu cửa sổ đang ẩn thì đợi tới khi cửa sổ hiển thị lại mới ghi. Nếu thành viên đang cuộn lên đọc tin cũ thì danh sách không tự cuộn xuống, hệ thống hiện nhãn "tin nhắn mới" và chỉ ghi mốc khi thành viên cuộn xuống tới cuối. | B mở cuộc X lúc tin mới nhất là #40 → mốc B = #40. B đang xem ở cuối, A gửi #41 → mốc B = #41. B chuyển sang tab khác, A gửi #42 → mốc giữ #41; B quay lại tab → mốc #42. B cuộn lên đọc #10, A gửi #43 → hiện "tin nhắn mới", mốc giữ #42; B cuộn xuống cuối → mốc #43. |
| BR-M16-15 | Suy diễn | Trạng thái hiển thị của tin nhắn suy ra từ mốc đã đọc, không lưu trên tin. Chỉ tin nhắn mới nhất mang trạng thái: dưới tin đó hiện avatar của các thành viên đã đọc tới tin đó, trừ người gửi tin đó và chính người đang xem, gộp khi có nhiều người; có thành viên khác người gửi đã đọc thì là Đã xem, chưa có thì là Đã gửi. Thành viên chưa đọc tới tin mới nhất không hiện avatar ở đâu; các tin cũ hơn không hiện trạng thái. Trò chuyện 1-1 dùng cùng cơ chế. | Nhóm A, B, C, D; tin mới nhất #50 do A gửi; mốc A = #50, B = #50, C = #50, D = #47. A xem → dưới #50 hiện avatar B, C; C xem → hiện avatar B; D không hiện ở đâu; #49 không hiện gì. Trò chuyện 1-1 A–B, A gửi #8, mốc B = #7 → A thấy Đã gửi; B đọc → A thấy avatar B. |
| BR-M16-16 | Kích hoạt | Tin nhắn mới và mốc đã đọc mới tới các thành viên đang mở cuộc trò chuyện ngay khi có, không cần tải lại trang. Không có trạng thái online/offline, không có "đang gõ". | C và D đang mở cuộc; B đọc tới #50 → dưới #50 trên màn hình của C, D thêm avatar B ngay. |
| BR-M16-17 | Ràng buộc | Lịch sử cuộc trò chuyện tải 20 tin mỗi lần, mới nhất trước; cuộn lên tải tiếp 20 tin cũ hơn; không giới hạn tổng số tin, cuộn được tới tin đầu tiên của cuộc. | Cuộc có 45 tin: mở → tin #26–#45; cuộn lên → #6–#25; cuộn lên → #1–#5; hết tin. |
| BR-M16-18 | Sự kiện | Tin nhắn được giữ vĩnh viễn, kể cả nội dung tin đã thu hồi; không tự xóa theo thời gian. | Tin gửi năm 2026 vẫn xem được năm 2030. |
| BR-M16-19 | Kích hoạt | Tài khoản người gửi bị xóa (DELETED, M01): tin nhắn của tài khoản đó giữ nguyên nội dung và vị trí; người gửi hiện "[Người dùng đã xóa]". | B xóa tài khoản; trong nhóm chat, tin "Mai thi nhé" của B hiện người gửi "[Người dùng đã xóa]". |
| BR-M16-20 | Sự kiện | Tin nhắn không bị AI quét và không thuộc kiểm duyệt; ở MS1 không có chặn (Block) người dùng và không báo cáo được tin nhắn (TBD-M16-01). | — |
| BR-M16-21 | Sự kiện | Tin nhắn mới tạo thông báo trong ứng dụng (M07) cho các thành viên khác của cuộc trò chuyện; không gửi email. | — |
| BR-M16-22 | Ràng buộc | Tài khoản đang bị ban: mọi thao tác Chat bị chặn; tài khoản chỉ khiếu nại được chính lệnh ban (M09). | B bị ban 7 ngày từ 01/11 → ngày 03/11 B không mở được hộp thư, không gửi tin. |
| BR-M16-23 | Kích hoạt | Trong khi cờ tính năng Chat tắt: các thao tác của người dùng với Chat (mở hộp thư, mở cuộc, bắt đầu 1-1, tạo nhóm chat, gửi, thu hồi, thêm, xóa thành viên, duyệt, đổi tên, chuyển quyền, rời nhóm, bật tắt duyệt, lấy link mời, xin gia nhập) bị từ chối với thông báo "Hệ thống đang bận, vui lòng thử lại sau". Vẫn hiển thị: biểu tượng Tin nhắn và số chưa đọc (M07), nút "Nhắn tin" trên hồ sơ. Vẫn chạy: tự tắt duyệt khi Admin nhóm chat không thể khôi phục; hạn thu hồi 5 phút vẫn trôi. Dữ liệu không bị xóa hay đổi; bật lại cờ thì không làm bù. Admin vẫn dùng được Chat. | Cờ tắt lúc 08:00: User B mở hộp thư lúc 08:05 → "Hệ thống đang bận, vui lòng thử lại sau"; Admin mở hộp thư của mình → được. Tin B gửi lúc 07:58 → cờ bật lại lúc 08:10 thì B không thu hồi được nữa (quá 5 phút). |
| BR-M16-24 | Ràng buộc | Mỗi cặp người dùng có đúng một trò chuyện 1-1. Bắt đầu lại 1-1 với người đã có cuộc thì mở cuộc cũ với toàn bộ lịch sử. Người dùng không nhắn cho chính mình. | Tháng 10 An nhắn Bình 30 tin; tháng 11 An bấm "Nhắn tin" ở hồ sơ Bình → mở lại cuộc có 30 tin cũ. An bấm "Nhắn tin" ở hồ sơ của chính mình → bị từ chối. |
| BR-M16-25 | Ràng buộc | Với tài khoản đang bị ban, đang vô hiệu hóa hoặc đã xóa: không bắt đầu được trò chuyện 1-1 mới, không thêm được vào nhóm chat. Trong trò chuyện 1-1 đã có, gửi tin tới tài khoản bị ban hoặc vô hiệu hóa được (người đó đọc khi hoạt động lại), tới tài khoản đã xóa thì không. Các tài khoản này vẫn là thành viên các nhóm chat đang có. | Bình bị ban: An chưa từng nhắn Bình → bấm "Nhắn tin" bị từ chối; Chi đã có cuộc với Bình → gửi được; Dũng thêm Bình vào nhóm → bị từ chối; Bình vẫn ở các nhóm chat cũ. Em đã xóa tài khoản: Chi gửi tin trong cuộc 1-1 với Em → bị từ chối. |
| BR-M16-26 | Suy diễn | Người gửi của tin nhắn hiện theo trạng thái tài khoản: đang hoạt động hoặc bị ban — như bình thường; đang vô hiệu hóa — "Tài khoản tạm thời vô hiệu hoá" với avatar mặc định; đã xóa — "[Người dùng đã xóa]" (BR-M16-19). | Bình tự vô hiệu hóa ngày 01/11 → tin cũ của Bình hiện "Tài khoản tạm thời vô hiệu hoá"; Bình kích hoạt lại ngày 05/11 → hiện lại tên Bình. |
| BR-M16-27 | Suy diễn | Thành viên cũ (đã rời hoặc bị xóa) giữ nhóm chat trong hộp thư, chỉ đọc các tin gửi trước thời điểm rời; không gửi tin, không thấy tin sau đó. Thành viên mới, kể cả người vào lại, đọc được toàn bộ lịch sử từ tin đầu tiên. | Nhóm có 60 tin; Bình rời lúc 21:00 sau tin #60; nhóm có thêm #61–#80 → Bình thấy nhóm trong hộp thư, đọc #1–#60. Bình được thêm lại sau #80 → đọc #1–#80 và các tin sau. |
| BR-M16-28 | Kích hoạt | Thành viên cũ vào lại nhóm chat theo luồng thường: được thành viên thêm thẳng hoặc xin gia nhập qua link mời, qua duyệt nếu công tắc bật. Nhóm chat không có danh sách chặn. | Chi bị Admin xóa; công tắc tắt, Member B thêm lại Chi → Chi vào ngay. Công tắc bật, Chi xin qua link → chờ Admin duyệt. |
| BR-M16-29 | Ràng buộc | Mỗi nhóm chat có một link mời chung; mọi thành viên lấy được; link không hết hạn, không thu hồi hay tạo lại được; không có thông báo "được mời". Mở link: người đã đăng nhập thấy tên nhóm chat và nút "Xin gia nhập", không thấy tin nhắn; Guest phải đăng nhập. Xin gia nhập: theo công tắc duyệt (BR-M16-06); nhóm đã đủ 100 thì bị từ chối; người đang có yêu cầu Chờ duyệt tới nhóm không gửi thêm; bị từ chối thì gửi lại ngay được, không giới hạn số lần. | Bình gửi link nhóm "Ôn thi HSG Hóa" cho Dũng qua Zalo; Dũng mở → thấy tên nhóm, bấm "Xin gia nhập"; công tắc bật → chờ; Admin từ chối lúc 10:00 → Dũng xin lại lúc 10:01 được. Dũng xin lần nữa lúc 10:02 khi yêu cầu 10:01 còn chờ → bị từ chối. |
| BR-M16-30 | Kích hoạt | Khi tài khoản Admin nhóm chat còn khôi phục được, nhóm chat giữ nguyên. Khi Admin nhóm chat trở thành không thể khôi phục: nếu công tắc duyệt đang bật thì hệ thống tắt, người chờ duyệt được xử lý theo BR-M16-33; nhóm chat không còn Admin nhóm chat. Hệ thống không tự chuyển quyền trong mọi trường hợp. | Công tắc bật, Admin An bị ban vĩnh viễn ngày 01/11 → không đổi, Dũng vẫn chờ. An không khiếu nại, hạn khiếu nại hết ngày 30/01 → công tắc tắt, Dũng vào ngay; sau đó Member Bình thêm Em → Em vào ngay. Nếu An bị ban 7 ngày → nhóm không đổi gì. |
| BR-M16-31 | Ràng buộc | Hộp thư Chat liệt kê các cuộc mà người xem là thành viên hoặc thành viên cũ, xếp theo tin mới nhất (với thành viên cũ: tin cuối cùng mình còn thấy), mới nhất trước. Mỗi dòng hiện: tên nhóm chat, hoặc display_name và avatar của người kia với 1-1; nội dung tin mới nhất ("Tin nhắn đã bị thu hồi" nếu đã thu hồi); thời điểm gửi tin đó. Cuộc có tin mới hơn mốc đã đọc, trong số tin người xem thấy được, được đánh dấu chưa đọc. Trò chuyện 1-1 chưa có tin không hiện. Tải 20 cuộc mỗi lần, không giới hạn tổng. | An có: 1-1 với Bình (tin cuối 21:05, đã đọc), nhóm "Ôn thi Lý" (tin cuối 21:30, chưa đọc), 1-1 với Chi (chưa có tin) → hộp thư hiện "Ôn thi Lý" (đánh dấu chưa đọc) rồi "Bình"; không có dòng Chi. |
| BR-M16-32 | Ràng buộc | Tên nhóm chat bắt buộc khi tạo, 1–100 ký tự sau khi bỏ khoảng trắng đầu và cuối, được trùng với nhóm chat khác. Đổi tên theo cùng quy tắc. | Tên "  Ôn thi Lý  " → lưu "Ôn thi Lý" (9 ký tự). Tên 100 ký tự → được; 101 ký tự → bị từ chối; tên trống → bị từ chối. Hai nhóm cùng tên "Nhóm Văn" → được. |
| BR-M16-33 | Kích hoạt | Khi công tắc duyệt được tắt (Admin nhóm chat tắt, hoặc hệ thống tự tắt theo BR-M16-30), người chờ duyệt vào nhóm theo thứ tự bắt đầu chờ, sớm nhất trước, cho tới khi nhóm đủ 100 thành viên; những người không vào được chuyển sang Đã từ chối và vào lại được theo luồng thường (BR-M16-28). | Nhóm có 98 thành viên, 5 người chờ từ 01/11, 02/11, 03/11, 04/11, 05/11; Admin tắt duyệt → người chờ từ 01/11, 02/11 vào nhóm (đủ 100); ba người còn lại Đã từ chối. Nhóm có 50 thành viên, 5 người chờ → cả 5 vào. |

### 5.19 Dữ liệu nghiệp vụ

| Thực thể | Thuộc tính nguồn đã nêu | Quan hệ |
|---|---|---|
| Cuộc trò chuyện | Loại (trò chuyện 1-1, nhóm chat); tên (nhóm chat; bắt buộc, 1–100 ký tự, được trùng); công tắc duyệt thành viên mới (nhóm chat; Bật, Tắt; mặc định Tắt); Admin nhóm chat (nhóm chat; có thể không còn); link mời (nhóm chat; một link chung, không hết hạn) | Trò chuyện 1-1 có đúng 2 thành viên, mỗi cặp người dùng tối đa một cuộc; nhóm chat có tối đa 100 thành viên; có nhiều tin nhắn; nhóm chat có nhiều đề nghị thêm thành viên và yêu cầu gia nhập |
| Thành viên cuộc trò chuyện | Người dùng; cuộc trò chuyện; vai trò (Admin nhóm chat, Member — chỉ ở nhóm chat); trạng thái (đang là thành viên, Đã rời, Bị xóa — chỉ ở nhóm chat); mốc đã đọc; thời điểm rời (khi đã rời hoặc bị xóa) | Một người dùng thuộc nhiều cuộc trò chuyện; mỗi cuộc một mốc đã đọc |
| Tin nhắn | Cuộc trò chuyện; người gửi; nội dung (văn bản, emoji; tối đa 1.000 từ); thời điểm gửi; đã thu hồi (cờ; nội dung gốc được giữ) | Thuộc một cuộc trò chuyện; người gửi là thành viên của cuộc đó |
| Đề nghị thêm thành viên | Nhóm chat; người được đề nghị; người đề nghị (Member); trạng thái (Chờ duyệt, Đã chấp nhận, Đã từ chối) | Thuộc một nhóm chat |
| Yêu cầu gia nhập | Nhóm chat; người xin; trạng thái (Chờ duyệt, Đã chấp nhận, Đã từ chối) | Thuộc một nhóm chat; một người có tối đa một yêu cầu Chờ duyệt tới một nhóm |

**Ma trận CRUD:**

| Thực thể | Tạo | Đọc | Sửa | Xóa |
|---|---|---|---|---|
| Cuộc trò chuyện | FR-M16-01.01, FR-M16-02.01 | FR-M16-03.01, FR-M16-04.01, FR-M16-16.01 | Tên: FR-M16-12.01; công tắc duyệt: FR-M16-09.01, FR-M16-17.02; Admin nhóm chat: FR-M16-13.01, FR-M16-17.03; link mời: Không có (BR-M16-29) | Không có (BR-M16-18 tin nhắn giữ vĩnh viễn; nguồn không có chức năng xóa cuộc trò chuyện) |
| Thành viên cuộc trò chuyện | FR-M16-01.04, FR-M16-02.02, FR-M16-08.01, FR-M16-08.02, FR-M16-10.01, FR-M16-16.03 | FR-M16-03.01, FR-M16-07.06 | Vai trò: FR-M16-13.01; mốc đã đọc: FR-M16-07.01, FR-M16-07.02, FR-M16-07.04, FR-M16-07.05, FR-M16-07.11; vào lại: FR-M16-08.08, FR-M16-16.08 | Rời: FR-M16-14.01, FR-M16-14.04; bị xóa: FR-M16-11.01 (giữ làm thành viên cũ, BR-M16-27) |
| Tin nhắn | FR-M16-05.01 | FR-M16-04.01, FR-M16-04.02, FR-M16-04.10 | Không có (BR-M16-10, FR-M16-05.07); thu hồi: FR-M16-06.01, FR-M16-06.07 | Không có (BR-M16-12 thu hồi là xóa mềm; BR-M16-18) |
| Đề nghị thêm thành viên | FR-M16-08.03 | FR-M16-10.05 | Trạng thái: FR-M16-10.01, FR-M16-10.02, FR-M16-09.03, FR-M16-09.04, FR-M16-17.02 | Không có (giữ trạng thái Đã chấp nhận, Đã từ chối) |
| Yêu cầu gia nhập | FR-M16-16.04 | FR-M16-10.05 | Trạng thái: FR-M16-10.01, FR-M16-10.02, FR-M16-09.03, FR-M16-09.04, FR-M16-17.02 | Không có (giữ trạng thái Đã chấp nhận, Đã từ chối) |

### 5.20 Chuyển trạng thái

#### Thành viên cuộc trò chuyện (nhóm chat)

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Người dùng tạo nhóm chat | Là người tạo | Admin nhóm chat | FR-M16-02.02 |
| (bắt đầu) | Người dùng được chọn khi tạo nhóm chat | — | Member | FR-M16-02.02 |
| (bắt đầu) | Được thêm vào nhóm chat | Công tắc duyệt tắt, hoặc người thêm là Admin nhóm chat; nhóm chưa đủ 100 | Member | FR-M16-08.01, FR-M16-08.02 |
| (bắt đầu) | Xin gia nhập qua link mời | Công tắc duyệt tắt; nhóm chưa đủ 100 | Member | FR-M16-16.03 |
| (bắt đầu) | Đề nghị thêm thành viên hoặc yêu cầu gia nhập được chấp nhận | Admin nhóm chat chấp nhận, hoặc công tắc duyệt bị tắt; nhóm chưa đủ 100 | Member | FR-M16-10.01, FR-M16-09.03, FR-M16-17.02 |
| Admin nhóm chat | Chuyển quyền cho thành viên khác | — | Member | FR-M16-13.01 |
| Member | Nhận quyền từ Admin nhóm chat | — | Admin nhóm chat | FR-M16-13.01 |
| Member | Tự rời nhóm | — | Đã rời | FR-M16-14.01 |
| Admin nhóm chat | Tự rời nhóm | Là thành viên cuối cùng | Đã rời | FR-M16-14.04 |
| Member | Bị Admin nhóm chat xóa | — | Bị xóa | FR-M16-11.01 |
| Đã rời | Được thêm lại, hoặc xin gia nhập lại được chấp nhận | Như người dùng mới (BR-M16-28) | Member | FR-M16-08.08, FR-M16-16.08 |
| Bị xóa | Được thêm lại, hoặc xin gia nhập lại được chấp nhận | Như người dùng mới (BR-M16-28) | Member | FR-M16-08.08, FR-M16-16.08 |

#### Tin nhắn

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Thành viên gửi tin | Trong giới hạn độ dài, tần suất (BR-M16-08, BR-M16-09) | Bình thường | FR-M16-05.01 |
| Bình thường | Người gửi thu hồi | Không quá 5 phút từ thời điểm gửi (BR-M16-11) | Đã thu hồi | FR-M16-06.01, FR-M16-06.07 |

#### Đề nghị thêm thành viên

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Member thêm người khi công tắc duyệt bật | — | Chờ duyệt | FR-M16-08.03 |
| Chờ duyệt | Admin nhóm chat chấp nhận | Nhóm chưa đủ 100 | Đã chấp nhận | FR-M16-10.01 |
| Chờ duyệt | Công tắc duyệt bị tắt (Admin tắt hoặc tự tắt) | Tới lượt theo thứ tự chờ, nhóm chưa đủ 100 | Đã chấp nhận | FR-M16-09.03, FR-M16-17.02 |
| Chờ duyệt | Admin nhóm chat từ chối | — | Đã từ chối | FR-M16-10.02 |
| Chờ duyệt | Công tắc duyệt bị tắt (Admin tắt hoặc tự tắt) | Nhóm đã đủ 100 trước khi tới lượt | Đã từ chối | FR-M16-09.04, FR-M16-17.02 |

#### Yêu cầu gia nhập

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Người dùng xin gia nhập qua link mời khi công tắc duyệt bật | Nhóm chưa đủ 100; chưa có yêu cầu Chờ duyệt tới nhóm | Chờ duyệt | FR-M16-16.04 |
| Chờ duyệt | Admin nhóm chat chấp nhận | Nhóm chưa đủ 100 | Đã chấp nhận | FR-M16-10.01 |
| Chờ duyệt | Công tắc duyệt bị tắt (Admin tắt hoặc tự tắt) | Tới lượt theo thứ tự chờ, nhóm chưa đủ 100 | Đã chấp nhận | FR-M16-09.03, FR-M16-17.02 |
| Chờ duyệt | Admin nhóm chat từ chối | — | Đã từ chối | FR-M16-10.02 |
| Chờ duyệt | Công tắc duyệt bị tắt (Admin tắt hoặc tự tắt) | Nhóm đã đủ 100 trước khi tới lượt | Đã từ chối | FR-M16-09.04, FR-M16-17.02 |

### 5.21 Giao tiếp với module khác

| Hướng | Module | Nội dung ở mức nghiệp vụ | Yêu cầu |
|---|---|---|---|
| Dùng | M01 | Người dùng đã đăng nhập (Guest không dùng Chat); trạng thái tài khoản bị ban, đang vô hiệu hóa, đã xóa (chặn bắt đầu 1-1, thêm vào nhóm, gửi tin; cách hiện người gửi); tên thay thế "[Người dùng đã xóa]" | FR-M16-01.03, FR-M16-01.07, FR-M16-03.02, FR-M16-03.03, FR-M16-04.07, FR-M16-04.11, FR-M16-05.13, FR-M16-08.09 |
| Dùng | M02 | Avatar, display_name của người gửi, của người kia trong hộp thư và của người đã xem; nút "Nhắn tin" trên hồ sơ | FR-M16-03.05, FR-M16-04.04, FR-M16-07.06, FR-M16-15.07 |
| Cung cấp | M07 | Sự kiện tin nhắn mới (thông báo trong ứng dụng, không email) cho các thành viên khác của cuộc | FR-M16-05.03 |
| Cung cấp | M07 | Thành viên cuộc trò chuyện và mốc đã đọc của từng người, để đếm số cuộc có tin chưa đọc trên biểu tượng Tin nhắn | FR-M16-07.10 |
| Cung cấp | M07 | Cuộc trò chuyện người dùng đang mở, để không hiện popup tin mới của chính cuộc đó | FR-M16-04.09 |
| Cung cấp | M07 | Hộp thư Chat là nơi biểu tượng Tin nhắn dẫn tới | FR-M16-03.01 |
| Cung cấp | M08 | Tin nhắn không bị quét AI, chưa báo cáo được, chưa có chặn người dùng ở MS1; nội dung tin thu hồi được giữ cho phase sau | FR-M16-05.09, FR-M16-05.10, FR-M16-06.07 |
| Dùng | M09 | Tài khoản bị ban chỉ khiếu nại được chính lệnh ban; hạn khiếu nại và kết quả khiếu nại lệnh ban vĩnh viễn, để biết Admin nhóm chat không thể khôi phục | FR-M16-03.03, FR-M16-17.02 |
| Dùng | M10 | Cờ tính năng Chat | FR-M16-15.01, FR-M16-15.04 |
| Dùng | M13 | Lớp AI không chấm điểm tin nhắn chat | FR-M16-05.09 |

### 5.22 AI hỗ trợ và hành vi khi tắt AI

Không áp dụng. Chat không gọi AI và tin nhắn không bị AI quét (FR-M16-05.09).

### 5.23 Yêu cầu HMI

Chưa có — chờ giai đoạn thiết kế.

### 5.24 Chuyển màn hình

Chưa có — chờ giai đoạn thiết kế.

## 6. Lịch sử sửa đổi

| Phiên bản | Ngày | Nội dung | Người sửa |
|---|---|---|---|
| 0.1 | 2026-10-23 | Tạo mới | Phạm Văn Đức |
| 1.0 | 2026-10-24 | Chốt sau 7 bước; câu trả lời bước 6 ghi ở DEC-248–DEC-257, QA-445–QA-455, ISS-383–ISS-393; thêm FR-M16-16 Xin gia nhập nhóm chat qua link mời (mở rộng phạm vi) và FR-M16-17; đóng TBD-M16-02; đối chiếu chéo với M01, M02, M07, M08, M09, M10, M11, M13 | Phạm Văn Đức |

## Phụ lục A. Truy vết

| ID | Nguồn | Căn cứ | Ghi chú |
|---|---|---|---|
| FR-M16-01 | ISS-162, QA-220, QA-011, DM-6.1, MR-M16, DEC-252 | Nói thẳng | — |
| FR-M16-01.01 | QA-220, ISS-162 | Nói thẳng | — |
| FR-M16-01.02 | QA-220 | Nói thẳng | — |
| FR-M16-01.03 | QA-011 | Nói thẳng | — |
| FR-M16-01.04 | DM-6.1 | Nói thẳng | — |
| FR-M16-01.05 | DEC-252 | Nói thẳng | — |
| FR-M16-01.06 | DEC-252 | Nói thẳng | — |
| FR-M16-01.07 | DEC-253 | Nói thẳng | — |
| FR-M16-02 | QA-221, QA-222, QA-023, DM-6.1, MR-M16, DEC-255 | Nói thẳng | — |
| FR-M16-02.01 | QA-221, QA-023 | Nói thẳng | — |
| FR-M16-02.02 | QA-222 | Nói thẳng | — |
| FR-M16-02.03 | QA-221, QA-222 | Nói thẳng | — |
| FR-M16-02.04 | QA-221, MR-M16, DEC-249 | Suy ra | "3+ members" kiểm khi tạo (DEC-249) là tối thiểu ⇒ dưới 3 thành viên lúc tạo bị từ chối |
| FR-M16-02.05 | QA-222 | Suy ra | "100 thành viên/Group Chat" là tối đa ⇒ quá 100 bị từ chối |
| FR-M16-02.06 | QA-011 | Nói thẳng | — |
| FR-M16-02.07 | DEC-255 | Nói thẳng | — |
| FR-M16-02.08 | DEC-255 | Nói thẳng | — |
| FR-M16-02.09 | DEC-253 | Nói thẳng | — |
| FR-M16-03 | DEC-067, DEC-220, DEC-254 | Nói thẳng | — |
| FR-M16-03.01 | DEC-254, DEC-067, QA-214 | Suy ra | Biểu tượng Tin nhắn dẫn tới hộp thư của người dùng; DEC-254 giữ cả nhóm chat mình đã rời; chat là kênh riêng tư ⇒ không liệt kê cuộc của người khác |
| FR-M16-03.02 | QA-011 | Nói thẳng | — |
| FR-M16-03.03 | ISS-114, DEC-197, DEC-152 | Nói thẳng | — |
| FR-M16-03.04 | DEC-254 | Nói thẳng | — |
| FR-M16-03.05 | DEC-254 | Nói thẳng | — |
| FR-M16-03.06 | DEC-254, DEC-220, DEC-249 | Suy ra | DEC-254 đánh dấu cuộc có tin mới hơn mốc đã đọc; DEC-249 thành viên cũ không thấy tin sau thời điểm rời ⇒ chỉ tính tin người xem thấy được |
| FR-M16-03.07 | DEC-254 | Nói thẳng | — |
| FR-M16-03.08 | DEC-254 | Nói thẳng | — |
| FR-M16-04 | QA-224, QA-210, DEC-135, QA-046, DM-6.2, DEC-249 | Nói thẳng | — |
| FR-M16-04.01 | QA-224 | Nói thẳng | — |
| FR-M16-04.02 | QA-224 | Nói thẳng | — |
| FR-M16-04.03 | QA-224, DEC-249 | Nói thẳng | — |
| FR-M16-04.04 | DM-6.2, DEC-156, DEC-127 | Suy ra | Draft nêu nội dung, thời gian gửi; DEC-156 nêu người gửi hiện kèm tin; mọi thời điểm hiển thị theo giờ Việt Nam (DEC-127) |
| FR-M16-04.05 | DEC-135, QA-046 | Nói thẳng | — |
| FR-M16-04.06 | QA-210 | Nói thẳng | — |
| FR-M16-04.07 | DEC-156, OPEN-008 | Nói thẳng | — |
| FR-M16-04.08 | QA-214, QA-217, DEC-249 | Suy ra | Chat là kênh riêng tư 1-1/nhóm nhỏ, không thuộc kiểm duyệt ⇒ người ngoài cuộc, kể cả Mod, Admin, không xem được; ngoại lệ là thành viên cũ (DEC-249) |
| FR-M16-04.09 | DEC-219 | Suy ra | M07 không hiện popup khi thành viên đang xem đúng cuộc đó ⇒ M16 cung cấp cuộc đang mở |
| FR-M16-04.10 | DEC-249 | Nói thẳng | — |
| FR-M16-04.11 | DEC-253 | Nói thẳng | — |
| FR-M16-04.12 | DEC-253 | Nói thẳng | — |
| FR-M16-05 | DM-6, DM-6.2, DEC-002, QA-217, QA-219, DEC-135, QA-046, DG-8, DEC-255 | Nói thẳng | — |
| FR-M16-05.01 | DM-6.2, DM-6, QA-217, DEC-002, DG-4, DM-x02 | Nói thẳng | — |
| FR-M16-05.02 | DEC-135, QA-046 | Nói thẳng | — |
| FR-M16-05.03 | DEC-065, QA-223, QA-124, DM-8.1 | Nói thẳng | — |
| FR-M16-05.04 | DEC-002, QA-217, DG-5, DG-8, DM-x03 | Suy ra | Tin nhắn chỉ văn bản, đính kèm ngoài phạm vi ⇒ đính kèm bị từ chối |
| FR-M16-05.05 | QA-219, DEC-255 | Suy ra | "30 tin nhắn/phút" là tối đa, tính trong 60 giây gần nhất (DEC-255) ⇒ tin thứ 31 trong cùng cuộc bị từ chối |
| FR-M16-05.06 | QA-214, QA-217, DEC-249 | Suy ra | Như FR-M16-04.08: chỉ thành viên trong cuộc; thành viên cũ không gửi được (DEC-249) |
| FR-M16-05.07 | QA-213 | Nói thẳng | — |
| FR-M16-05.08 | DEC-129 | Nói thẳng | — |
| FR-M16-05.09 | QA-217 | Nói thẳng | — |
| FR-M16-05.10 | QA-218, OPEN-003, DM-10.1 | Nói thẳng | — |
| FR-M16-05.11 | DEC-255 | Nói thẳng | — |
| FR-M16-05.12 | DEC-255 | Nói thẳng | — |
| FR-M16-05.13 | DEC-253 | Nói thẳng | — |
| FR-M16-05.14 | DEC-253 | Nói thẳng | — |
| FR-M16-06 | QA-213, QA-214, QA-215, QA-216, DEC-248 | Nói thẳng | — |
| FR-M16-06.01 | QA-215, QA-216 | Nói thẳng | — |
| FR-M16-06.02 | QA-214 | Nói thẳng | — |
| FR-M16-06.03 | QA-216 | Nói thẳng | — |
| FR-M16-06.04 | QA-216, QA-222 | Suy ra | Thu hồi là của người gửi tin (QA-216 "gửi nhầm"); QA-222 liệt kê đủ quyền Admin nhóm chat, không có gỡ tin người khác ⇒ người khác bị từ chối |
| FR-M16-06.05 | QA-215 | Nói thẳng | — |
| FR-M16-06.06 | QA-214 | Suy ra | Tin đã thu hồi chỉ còn dòng giữ chỗ (trạng thái Đã thu hồi không có chuyển tiếp) ⇒ thu hồi lần nữa bị từ chối |
| FR-M16-06.07 | DEC-248 | Nói thẳng | — |
| FR-M16-06.08 | DEC-255 | Nói thẳng | — |
| FR-M16-06.09 | DEC-255 | Nói thẳng | — |
| FR-M16-07 | QA-208, QA-209, QA-210, QA-211, QA-212, ISS-155, DM-6.2, DEC-255 | Nói thẳng | — |
| FR-M16-07.01 | ISS-155 | Nói thẳng | — |
| FR-M16-07.02 | QA-210 | Nói thẳng | — |
| FR-M16-07.03 | QA-210 | Nói thẳng | — |
| FR-M16-07.04 | QA-210 | Nói thẳng | — |
| FR-M16-07.05 | QA-209 | Nói thẳng | — |
| FR-M16-07.06 | QA-211, DEC-255 | Nói thẳng | — |
| FR-M16-07.07 | QA-208, DEC-255 | Nói thẳng | — |
| FR-M16-07.08 | QA-208, QA-211 | Nói thẳng | — |
| FR-M16-07.09 | QA-212, DEC-135 | Nói thẳng | — |
| FR-M16-07.10 | DEC-220, DEC-067, DEC-249 | Suy ra | DEC-220 đếm theo mốc đã đọc của M16; DEC-249 thành viên cũ không thấy tin sau thời điểm rời ⇒ không tính tin đó là chưa đọc |
| FR-M16-07.11 | DEC-255 | Nói thẳng | — |
| FR-M16-08 | QA-222, DEC-251 | Nói thẳng | — |
| FR-M16-08.01 | QA-222 | Nói thẳng | — |
| FR-M16-08.02 | QA-222 | Suy ra | "bật thì thêm thành viên mới cần Admin duyệt (không phải Member)": Admin là người duyệt ⇒ người Admin thêm không cần duyệt |
| FR-M16-08.03 | QA-222 | Nói thẳng | — |
| FR-M16-08.04 | QA-222, QA-221 | Nói thẳng | — |
| FR-M16-08.05 | QA-222 | Suy ra | Tối đa 100 thành viên ⇒ thêm người thứ 101 bị từ chối |
| FR-M16-08.06 | QA-222, QA-214, DEC-249 | Suy ra | "Add: cả 2 role đều add được" ⇒ người không là thành viên, kể cả thành viên cũ, bị từ chối |
| FR-M16-08.07 | QA-222 | Suy ra | Mỗi thành viên mang một vai trò trong nhóm (BR-M16-04) ⇒ không thêm trùng |
| FR-M16-08.08 | DEC-249 | Nói thẳng | — |
| FR-M16-08.09 | DEC-253 | Nói thẳng | — |
| FR-M16-08.10 | DEC-251 | Nói thẳng | — |
| FR-M16-08.11 | DEC-251 | Nói thẳng | — |
| FR-M16-08.12 | DEC-251 | Suy ra | "Every member can get the link" ⇒ người không là thành viên bị từ chối |
| FR-M16-08.13 | DEC-251 | Nói thẳng | — |
| FR-M16-09 | QA-222 | Nói thẳng | — |
| FR-M16-09.01 | QA-222, DEC-251 | Nói thẳng | — |
| FR-M16-09.02 | QA-222 | Suy ra | "Admin bật/tắt toggle" ⇒ người khác bị từ chối |
| FR-M16-09.03 | DEC-255, DEC-257 | Nói thẳng | — |
| FR-M16-09.04 | DEC-257 | Nói thẳng | — |
| FR-M16-10 | QA-222, DEC-251 | Nói thẳng | — |
| FR-M16-10.01 | QA-222, DEC-251 | Nói thẳng | — |
| FR-M16-10.02 | QA-222, DEC-251 | Nói thẳng | — |
| FR-M16-10.03 | QA-222, DEC-255 | Suy ra | Tối đa 100 thành viên, kiểm lúc vào nhóm (DEC-255) ⇒ chấp nhận khi đã đủ 100 bị từ chối |
| FR-M16-10.04 | QA-222 | Nói thẳng | — |
| FR-M16-10.05 | QA-222, DEC-251 | Suy ra | Admin duyệt người chờ ⇒ Admin phải thấy các đề nghị, yêu cầu đang chờ |
| FR-M16-10.06 | QA-222 | Suy ra | Chỉ đề nghị, yêu cầu Chờ duyệt mới có chuyển tiếp (bảng trạng thái) ⇒ duyệt lại bị từ chối |
| FR-M16-10.07 | DEC-255 | Nói thẳng | — |
| FR-M16-11 | QA-222 | Nói thẳng | — |
| FR-M16-11.01 | QA-222, DEC-249 | Nói thẳng | — |
| FR-M16-11.02 | QA-222 | Nói thẳng | — |
| FR-M16-11.03 | DEC-249 | Nói thẳng | — |
| FR-M16-12 | QA-222 | Nói thẳng | — |
| FR-M16-12.01 | QA-222 | Nói thẳng | — |
| FR-M16-12.02 | QA-222, QA-214 | Suy ra | "Đổi tên nhóm: mọi thành viên" ⇒ người không là thành viên bị từ chối |
| FR-M16-12.03 | DEC-255 | Nói thẳng | — |
| FR-M16-13 | QA-222 | Nói thẳng | — |
| FR-M16-13.01 | QA-222 | Suy ra | Người nhận thành Admin nhóm chat; người chuyển thành Member vì mỗi nhóm có tối đa một Admin nhóm chat (BR-M16-04) |
| FR-M16-13.02 | QA-222 | Suy ra | Chuyển quyền là hành động của Admin ⇒ người khác bị từ chối |
| FR-M16-13.03 | QA-222, DEC-250 | Nói thẳng | — |
| FR-M16-14 | QA-222, DEC-249 | Nói thẳng | — |
| FR-M16-14.01 | QA-222, DEC-249 | Nói thẳng | — |
| FR-M16-14.02 | QA-222 | Nói thẳng | — |
| FR-M16-14.03 | QA-222 | Nói thẳng | — |
| FR-M16-14.04 | DEC-249 | Nói thẳng | — |
| FR-M16-14.05 | DEC-249 | Nói thẳng | — |
| FR-M16-15 | DEC-225, DEC-092, DEC-256 | Nói thẳng | — |
| FR-M16-15.01 | DEC-225 | Nói thẳng | — |
| FR-M16-15.02 | DEC-225 | Nói thẳng | — |
| FR-M16-15.03 | DEC-225 | Nói thẳng | — |
| FR-M16-15.04 | DEC-225, DEC-256 | Nói thẳng | — |
| FR-M16-15.05 | DEC-225 | Nói thẳng | — |
| FR-M16-15.06 | DEC-256 | Nói thẳng | — |
| FR-M16-15.07 | DEC-256 | Nói thẳng | — |
| FR-M16-15.08 | DEC-256 | Nói thẳng | — |
| FR-M16-16 | DEC-251 | Nói thẳng | — |
| FR-M16-16.01 | DEC-251 | Nói thẳng | — |
| FR-M16-16.02 | DEC-251 | Nói thẳng | — |
| FR-M16-16.03 | DEC-251 | Nói thẳng | — |
| FR-M16-16.04 | DEC-251 | Nói thẳng | — |
| FR-M16-16.05 | DEC-251 | Nói thẳng | — |
| FR-M16-16.06 | DEC-251 | Nói thẳng | — |
| FR-M16-16.07 | DEC-251 | Nói thẳng | — |
| FR-M16-16.08 | DEC-249 | Nói thẳng | — |
| FR-M16-17 | DEC-250 | Nói thẳng | — |
| FR-M16-17.01 | DEC-250 | Nói thẳng | — |
| FR-M16-17.02 | DEC-250, DEC-257 | Nói thẳng | — |
| FR-M16-17.03 | DEC-250 | Nói thẳng | — |
| BR-M16-01 | DM-6.1, QA-221, QA-023, MR-M16, MR-A01 | Nói thẳng | — |
| BR-M16-02 | QA-220, ISS-162, QA-011 | Nói thẳng | — |
| BR-M16-03 | QA-221, QA-222, DEC-249, DEC-255 | Nói thẳng | — |
| BR-M16-04 | QA-222, DEC-249 | Suy ra | "Role: Admin (người tạo) + Member" và "Admin rời: bắt buộc chuyển quyền cho người khác" ⇒ một nhóm có một Admin nhóm chat; DEC-249, DEC-250 cho phép nhóm không còn Admin ⇒ "tối đa một" |
| BR-M16-05 | QA-222, DEC-251 | Nói thẳng | — |
| BR-M16-06 | QA-222, DEC-251, DEC-255 | Suy ra | "bật thì thêm thành viên mới cần Admin duyệt (không phải Member)" ⇒ người do Admin nhóm chat thêm không cần duyệt (Admin là người duyệt); phần còn lại nói thẳng ở DEC-251, DEC-255 |
| BR-M16-07 | QA-222, DEC-249 | Suy ra | "Admin rời: bắt buộc chủ động chuyển quyền… không có auto-promote" ⇒ người chuyển thành Member vì mỗi nhóm tối đa một Admin nhóm chat (BR-M16-04); ngoại lệ thành viên cuối cùng nói thẳng ở DEC-249 |
| BR-M16-08 | DEC-002, QA-217, DM-6, DG-8, DM-x03, DEC-255 | Nói thẳng | — |
| BR-M16-09 | QA-219, DEC-255 | Nói thẳng | — |
| BR-M16-10 | QA-213 | Nói thẳng | — |
| BR-M16-11 | QA-215, QA-216 | Nói thẳng | — |
| BR-M16-12 | QA-214, DEC-248, DEC-255 | Nói thẳng | — |
| BR-M16-13 | QA-209, QA-208, DEC-255 | Nói thẳng | — |
| BR-M16-14 | QA-210, ISS-155 | Nói thẳng | — |
| BR-M16-15 | QA-208, QA-211, DM-6.2, DEC-255 | Nói thẳng | — |
| BR-M16-16 | QA-212, DEC-135, QA-257, QA-046 | Nói thẳng | — |
| BR-M16-17 | QA-224 | Nói thẳng | — |
| BR-M16-18 | DEC-129, DEC-248 | Nói thẳng | — |
| BR-M16-19 | DEC-156, DEC-129 | Nói thẳng | — |
| BR-M16-20 | QA-217, QA-218, OPEN-003 | Nói thẳng | — |
| BR-M16-21 | QA-223, DEC-065, QA-124, DM-8.1 | Nói thẳng | — |
| BR-M16-22 | ISS-114, DEC-197, DEC-152 | Nói thẳng | — |
| BR-M16-23 | DEC-225, DEC-092, DEC-256 | Nói thẳng | — |
| BR-M16-24 | DEC-252 | Nói thẳng | — |
| BR-M16-25 | DEC-253 | Nói thẳng | — |
| BR-M16-26 | DEC-253, DEC-156 | Nói thẳng | — |
| BR-M16-27 | DEC-249 | Nói thẳng | — |
| BR-M16-28 | DEC-249 | Nói thẳng | — |
| BR-M16-29 | DEC-251 | Nói thẳng | — |
| BR-M16-30 | DEC-250 | Nói thẳng | — |
| BR-M16-31 | DEC-254 | Nói thẳng | — |
| BR-M16-32 | DEC-255 | Nói thẳng | — |
| BR-M16-33 | DEC-257 | Nói thẳng | — |

## Phụ lục B. Câu hỏi, giả định và TBD

### B.1 Câu hỏi đã hỏi

| Mã | Loại | Câu hỏi | Trả lời | Ghi vào register |
|---|---|---|---|---|
| Q-01 | Mâu thuẫn | Thu hồi tin nhắn xóa hẳn nội dung (QA-214) hay chỉ xóa mềm, giữ nội dung (DEC-129; QA-343, OPEN-011)? | Xóa mềm: gắn cờ, giữ nội dung, không ai xem được ở MS1 | ISS-383, QA-445, DEC-248 |
| Q-02 | Thiếu chi tiết | Người đã rời hoặc bị xóa khỏi nhóm chat còn thấy nhóm trong hộp thư và xem lại lịch sử không? | Cả hai giữ nhóm trong hộp thư, chỉ đọc lịch sử tới lúc rời hoặc bị xóa | ISS-384, QA-446, DEC-249 |
| Q-03 | Thiếu chi tiết | "3+" chỉ áp khi tạo hay luôn đúng? Nhóm còn 2 hoặc 1 thành viên thì sao? | Chỉ kiểm khi tạo; nhóm vẫn hoạt động; Admin là thành viên cuối cùng rời được không cần chuyển quyền | ISS-385, QA-447, DEC-249 |
| Q-04 | Thiếu chi tiết | Công tắc duyệt mặc định; người chờ khi tắt công tắc; người chờ có tính vào 100? | Mặc định Tắt; tắt thì người chờ vào ngay (trong giới hạn 100); người chờ không tính vào 100 | ISS-392, QA-454, DEC-255 |
| Q-05 | Thiếu chi tiết | Admin nhóm chat bị ban, vô hiệu hóa hoặc xóa tài khoản thì sao? | Không tự chuyển quyền; còn khôi phục được thì không đổi; không thể khôi phục thì duyệt tự tắt, người chờ vào ngay | ISS-386, QA-448, DEC-250 |
| Q-06 | Thiếu chi tiết | Độ dài tối đa của tin; tin trống? | Tối đa 1.000 từ; không trống, không chỉ khoảng trắng | ISS-392, QA-454, DEC-255 |
| Q-07 | Mơ hồ | "1 phút" trượt hay theo phút đồng hồ; người bị chặn thấy gì? | 60 giây gần nhất; báo đã gửi quá nhanh, câu chữ do thiết kế | ISS-392, QA-454, DEC-255 |
| Q-08 | Mơ hồ | Gửi tin có đưa mốc của người gửi; avatar người gửi, người xem có hiện? | Có đưa mốc; không hiện avatar người gửi tin đó và người đang xem | ISS-392, QA-454, DEC-255 |
| Q-09 | Thiếu chi tiết | Danh sách thao tác bị chặn, vẫn chạy khi cờ Chat tắt | Theo đề xuất (cùng khuôn DEC-236, DEC-245) | ISS-391, QA-453, DEC-256 |
| Q-10 | Thiếu chi tiết | Mỗi cặp người dùng một hay nhiều cuộc 1-1; nhắn cho chính mình? | Đúng một cuộc 1-1 mỗi cặp; không tự nhắn | ISS-388, QA-450, DEC-252 |
| Q-11 | Thiếu chi tiết | Tên nhóm chat bắt buộc không, độ dài? | Bắt buộc, 1–100 ký tự sau khi bỏ khoảng trắng đầu cuối, được trùng | ISS-392, QA-454, DEC-255 |
| Q-12 | Thiếu chi tiết | Người đã rời hoặc bị xóa có được thêm lại không? | Được, theo luồng thường; không có danh sách chặn; thành viên mới xem toàn bộ lịch sử | ISS-392, QA-454, DEC-249 |
| Q-13 | Thiếu chi tiết | Nhắn tin với tài khoản đang bị ban, vô hiệu hóa, đã xóa | Theo bảng đề xuất A | ISS-389, QA-451, DEC-253 |
| Q-14 | Thiếu chi tiết | Hộp thư: thứ tự, nội dung dòng, đánh dấu chưa đọc | Theo đề xuất H1–H6 | ISS-390, QA-452, DEC-254 |
| Q-15 | Thiếu chi tiết | Thu hồi có cập nhật ngay; tin mới nhất bị thu hồi thì trạng thái ở đâu? | Cập nhật ngay; dòng giữ chỗ vẫn là tin mới nhất, mang trạng thái | ISS-392, QA-454, DEC-255 |
| Q-16 | Cần cân nhắc | Mở rộng phạm vi: link mời nhóm chat và xin gia nhập (L1–L8) | Đồng ý | ISS-387, QA-449, DEC-251 |
| Q-17 | Thiếu chi tiết | FR-M16-09.03, FR-M16-17.02 (DEC-250, DEC-255 "everyone waiting joins at once, up to the 100-member limit"): khi người chờ duyệt được tự chấp nhận mà nhóm không đủ chỗ cho tất cả, ai vào trước và những người còn lại ra sao? | Chờ trước vào trước; người không đủ chỗ chuyển Đã từ chối | ISS-393, QA-455, DEC-257 |

### B.2 TBD

| ID | Nội dung | Ảnh hưởng | Lý do chưa chốt |
|---|---|---|---|
| TBD-M16-01 | Chặn (Block) người dùng và báo cáo tin nhắn chưa có ở MS1; cần xét lại trước khi mở rộng chat ra ngoài phạm vi nhỏ, riêng tư hiện tại. | Thấp | OPEN-003 hoãn có chủ đích. |
| TBD-M16-02 | (Đã đóng ở phiên bản 0.1 — DEC-248: thu hồi là xóa mềm, nội dung giữ, không ai xem được ở MS1) | Thấp | — |

### B.3 Cần cân nhắc (ngoài dữ liệu hiện có)

| Mã | Điểm cần cân nhắc | Vì sao cần | Quyết định |
|---|---|---|---|
| Q-16 | Mở rộng phạm vi: link mời nhóm chat và xin gia nhập | Stakeholder nêu "lời mời vào nhóm" có hai cách (thêm thẳng, gửi link để người kia xin gia nhập); nguồn M16 chỉ có thêm thẳng | Có (DEC-251) |

## Phụ lục C. Sổ nguồn

**Owner keywords:** M16, MSG, Chat, chat, chats, Messaging, messaging, nhắn tin, tin nhắn, message, messages, DM, DMs, direct message, conversation, conversations, cuộc trò chuyện, cuộc hội thoại, hội thoại, Group Chat, group chat, nhóm chat, conversation_members, last_read_message_id, mốc đọc, mốc đã đọc, đã xem, đã đọc, read receipt, read_receipt, mark-as-read, thu hồi, recall, tombstone, hộp thư, inbox, Tin nhắn mới, new message, locked screen, locked-screen
**Dependency keywords:** notification, thông báo, popup, unread, badge, SSE, real-time, realtime, WebSocket, pub/sub, report, báo cáo, block, chặn, rate limit, feature flag, cờ tính năng, deleted, đã xóa, Người dùng đã xóa, DELETED, BANNED, ban, deactivate, deactivated, avatar, display_name, profile, hồ sơ, login, đăng nhập, Guest, privacy, PII, Group, M11, emoji, email, AI, moderation, kiểm duyệt, audit log, timezone, retention
**Mục draft của module:** DM-6 (gồm DM-6.1–6.4)
**Loại khỏi bảng nguồn (khớp nhầm):** DEC-169, DEC-180, DEC-187, DEC-203, DEC-206, DEC-215, DEC-243, ISS-272, ISS-273, ISS-277, ISS-324 ("DM" là mã mục draft DM-x.y); DEC-016, DEC-068, DEC-084, DEC-151, DEC-208, DEC-211, ISS-113, QA-150 ("message" là nội dung email, khiếu nại, câu nhắc giao diện); DEC-128 ("messages" là chuỗi giao diện); DEC-019, DEC-043, DEC-149, ISS-074, QA-018, QA-066, QA-204, MR-M04 ("tombstone" của bình luận, tài khoản); DEC-007, ISS-143, ISS-352, QA-192, QA-412 ("thu hồi" vai trò Admin, huy hiệu); DG-6, DM-11.5, GL:Feedback / Evaluation Loop ("recall" là chỉ số đánh giá AI); QA-408 ("đã đọc" của chuông thông báo); QA-004 (chat Facebook/Zalo là bối cảnh cạnh tranh); QA-097 (QA-224 trích "pattern Search QA-097" nhưng QA-097 là xóa bình luận — trích nhầm mã)

### C.1 Bảng nguồn

| Nguồn | Nhãn | Trạng thái | Dùng ở | Ghi chú |
|---|---|---|---|---|
| DM-6 | Sở hữu | Hiện hành | FR-M16-05, FR-M16-05.01, BR-M16-08 | Nhóm A. Chat 1-1 và group chat, chỉ văn bản; không gọi thoại, video, gửi file |
| DM-6.1 | Sở hữu | Hiện hành | FR-M16-01, FR-M16-01.04, FR-M16-02, BR-M16-01 | Nhóm A. Cuộc trò chuyện: 1-1 giữa 2 người, group chat nhiều thành viên |
| DM-6.2 | Sở hữu | Sửa một phần bởi QA-208 | FR-M16-04, FR-M16-04.04, FR-M16-05, FR-M16-05.01, FR-M16-07, BR-M16-15 | Nhóm A. Tin nhắn: nội dung văn bản, thời gian gửi, đã đọc/chưa đọc |
| DM-6.3 | Sở hữu | Bị thay bởi QA-218 | — | Nhóm A. Báo cáo tin nhắn tái dùng Report chung (M08); nghi khác QA-218 (không báo cáo ở MS1) |
| DM-6.4 | Sở hữu | Bị thay bởi DEC-135 | — | Nhóm A. Kênh real-time riêng bằng WebSocket; nghi bị thay bởi DEC-135 (SSE) |
| ISS-155 | Sở hữu | Hiện hành | FR-M16-07, FR-M16-07.01, BR-M16-14 | Nhóm A. Trạng thái Đã gửi/Đã xem, mốc đã đọc, khi nào đánh dấu đã đọc, avatar đã xem ở nhóm |
| ISS-158 | Sở hữu | Trùng với QA-213, QA-214, QA-215, QA-216 | — | Nhóm A. Không sửa tin; thu hồi trong 5 phút, cả hai phía, hiện "Tin nhắn đã bị thu hồi" |
| ISS-159 | Sở hữu | Trùng với QA-217 | — | Nhóm A. Nội dung văn bản + emoji; không đính kèm; không quét AI |
| ISS-160 | Sở hữu | Trùng với QA-218 | — | Nhóm A. Không chặn (Block), không báo cáo tin nhắn ở MS1 → OPEN-003 |
| ISS-161 | Sở hữu | Trùng với QA-219 | — | Nhóm A. Giới hạn 30 tin/phút theo (người gửi, cuộc trò chuyện) |
| ISS-162 | Sở hữu | Hiện hành | FR-M16-01, FR-M16-01.01, BR-M16-02 | Nhóm A. Nhắn 1-1 mở: người đã đăng nhập nhắn được cho bất kỳ ai, không cần theo dõi |
| ISS-163 | Sở hữu | Trùng với QA-221 | — | Nhóm A. Group Chat độc lập với Group (M11), ai cũng tạo được |
| ISS-164 | Sở hữu | Trùng với QA-222 | — | Nhóm A. Quản trị Group Chat: Admin/Member, thêm, xóa, duyệt thành viên, đổi tên, rời, chuyển quyền, tối đa 100 |
| ISS-165 | Sở hữu | Trùng với QA-223, QA-224 | — | Nhóm A. Không email tin nhắn mới; tải lịch sử 20 tin/lần, cuộn tới tin đầu tiên |
| QA-208 | Sở hữu | Hiện hành | FR-M16-07, FR-M16-07.07, FR-M16-07.08, BR-M16-13, BR-M16-15 | Nhóm A. Đã xem suy ra từ mốc đọc; Đã xem chỉ hiện ở tin mới nhất |
| QA-209 | Sở hữu | Hiện hành | FR-M16-07, FR-M16-07.05, BR-M16-13 | Nhóm A. Mốc đã đọc theo tin nhắn, một mốc cho mỗi người mỗi cuộc, không lùi |
| QA-210 | Sở hữu | Hiện hành | FR-M16-04, FR-M16-04.06, FR-M16-07, FR-M16-07.02, FR-M16-07.03, FR-M16-07.04, BR-M16-14 | Nhóm A. Đánh dấu đã đọc khi đang xem cửa sổ và ở cuối danh sách; đang đọc tin cũ thì hiện nhãn "tin nhắn mới" |
| QA-211 | Sở hữu | Sửa một phần bởi DEC-255 | FR-M16-07, FR-M16-07.06, FR-M16-07.08, BR-M16-15 | Nhóm A. Group chat: avatar người đã đọc tin mới nhất dưới tin đó; 1-1 dùng chung cơ chế |
| QA-212 | Sở hữu | Hiện hành | FR-M16-07, FR-M16-07.09, BR-M16-16 | Nhóm A. Cập nhật đã xem tức thời cho các thành viên khác |
| QA-213 | Sở hữu | Hiện hành | FR-M16-05.07, FR-M16-06, BR-M16-10 | Nhóm A. Không sửa tin nhắn |
| QA-214 | Sở hữu | Sửa một phần bởi DEC-248 | FR-M16-03.01, FR-M16-04.08, FR-M16-05.06, FR-M16-06, FR-M16-06.02, FR-M16-06.06, FR-M16-08.06, FR-M16-12.02, BR-M16-12 | Nhóm A. Thu hồi: xóa hẳn nội dung, giữ chỗ "Tin nhắn đã bị thu hồi"; liên quan OPEN-011 |
| QA-215 | Sở hữu | Hiện hành | FR-M16-06, FR-M16-06.01, FR-M16-06.05, BR-M16-11 | Nhóm A. Chỉ một kiểu thu hồi, cho cả hai phía |
| QA-216 | Sở hữu | Hiện hành | FR-M16-06, FR-M16-06.01, FR-M16-06.03, FR-M16-06.04, BR-M16-11 | Nhóm A. Thu hồi trong 5 phút kể từ lúc gửi; sau đó không xóa được |
| QA-217 | Sở hữu | Hiện hành | FR-M16-04.08, FR-M16-05, FR-M16-05.01, FR-M16-05.04, FR-M16-05.06, FR-M16-05.09, BR-M16-08, BR-M16-20 | Nhóm A. Văn bản + emoji; không đính kèm; không quét AI |
| QA-218 | Sở hữu | Hiện hành | FR-M16-05.10, BR-M16-20 | Nhóm A. Không chặn, không báo cáo tin nhắn ở MS1 (OPEN-003) |
| QA-219 | Sở hữu | Sửa một phần bởi DEC-255 | FR-M16-05, FR-M16-05.05, BR-M16-09 | Nhóm A. 30 tin/phút theo (người gửi, cuộc trò chuyện) |
| QA-220 | Sở hữu | Sửa một phần bởi DEC-252, DEC-253 | FR-M16-01, FR-M16-01.01, FR-M16-01.02, BR-M16-02 | Nhóm A. Nhắn 1-1 mở hoàn toàn, không có yêu cầu nhắn tin |
| QA-221 | Sở hữu | Sửa một phần bởi DEC-249 | FR-M16-02, FR-M16-02.01, FR-M16-02.03, FR-M16-02.04, FR-M16-08.04, BR-M16-01, BR-M16-03 | Nhóm A. Group Chat độc lập, 3+ người, ai cũng tạo được |
| QA-222 | Sở hữu | Sửa một phần bởi DEC-249, DEC-250, DEC-251 | FR-M16-02, FR-M16-02.02, FR-M16-02.03, FR-M16-02.05, FR-M16-06.04, FR-M16-08, FR-M16-08.01, FR-M16-08.02, FR-M16-08.03, FR-M16-08.04, FR-M16-08.05, FR-M16-08.06, FR-M16-08.07, FR-M16-09, FR-M16-09.01, FR-M16-09.02, FR-M16-10, FR-M16-10.01, FR-M16-10.02, FR-M16-10.03, FR-M16-10.04, FR-M16-10.05, FR-M16-10.06, FR-M16-11, FR-M16-11.01, FR-M16-11.02, FR-M16-12, FR-M16-12.01, FR-M16-12.02, FR-M16-13, FR-M16-13.01, FR-M16-13.02, FR-M16-13.03, FR-M16-14, FR-M16-14.01, FR-M16-14.02, FR-M16-14.03, BR-M16-03, BR-M16-04, BR-M16-05, BR-M16-06, BR-M16-07 | Nhóm A. Quản trị Group Chat: vai trò, thêm, xóa, duyệt, đổi tên, rời, chuyển quyền Admin, 100 thành viên |
| QA-223 | Sở hữu | Hiện hành | FR-M16-05.03, BR-M16-21 | Nhóm A. Không gửi email cho tin nhắn mới, chỉ trong ứng dụng |
| QA-224 | Sở hữu | Hiện hành | FR-M16-04, FR-M16-04.01, FR-M16-04.02, FR-M16-04.03, BR-M16-17 | Nhóm A. Cuộn lên tải tin cũ, 20 tin/lần, không giới hạn tổng; trích "pattern Search QA-097" nhưng QA-097 là xóa bình luận |
| MR-A01 | Sở hữu | Hiện hành | BR-M16-01 | Nhóm A. Đợt sửa M16: Group Chat độc lập; bỏ phụ thuộc M11; còn OPEN-003 |
| MR-M16 | Sở hữu | Sửa một phần bởi DEC-251 | FR-M16-01, FR-M16-02, FR-M16-02.04, BR-M16-01 | Nhóm A. Dòng module: Should, phụ thuộc M01; DM mở + Group Chat 3+ người |
| DEC-002 | Sở hữu | Hiện hành | FR-M16-05, FR-M16-05.01, FR-M16-05.04, BR-M16-08 | Nhóm B. Nhắn tin chỉ văn bản, không file/thoại/video |
| DEC-065 | Phụ thuộc | Hiện hành | FR-M16-05.03, BR-M16-21 | Nhóm B. M07: tin nhắn 1-1/nhóm là sự kiện thông báo trong ứng dụng, không email |
| DEC-067 | Phụ thuộc | Sửa một phần bởi DEC-217, DEC-220, DEC-254 | FR-M16-03, FR-M16-03.01, FR-M16-07.10 | Nhóm B. M07: biểu tượng Tin nhắn riêng, số chưa đọc riêng, dẫn tới hộp thư Chat |
| DEC-070 | Phụ thuộc | Sửa một phần bởi DEC-219 | Chuyển M07 | Nhóm B. M07: tắt thông báo từng cuộc trò chuyện và toàn bộ Chat |
| DEC-092 | Phụ thuộc | Sửa một phần bởi DEC-225 | FR-M16-15, BR-M16-23 | Nhóm B. M10: cờ tính năng cho Chat |
| DEC-129 | Sở hữu | Sửa một phần bởi DEC-156, DEC-248 | FR-M16-05.08, BR-M16-18, BR-M16-19 | Nhóm B. Tin nhắn chat giữ vĩnh viễn, không xóa cứng |
| DEC-135 | Sở hữu | Hiện hành | FR-M16-04, FR-M16-04.05, FR-M16-05, FR-M16-05.02, FR-M16-07.09, BR-M16-16 | Nhóm B. Nhận tin và đã xem tức thời qua SSE, không WebSocket; không có trạng thái online/offline |
| DEC-152 | Phụ thuộc | Hiện hành | FR-M16-03.03, BR-M16-22 | Nhóm B. M01: màn hình khóa khi bị ban |
| DEC-154 | Nhắc tới | Hiện hành | Không áp dụng: M01: trang chính sách liệt kê tin nhắn trong nhóm dữ liệu "nội dung bạn tạo" | Nhóm B. M01: trang chính sách liệt kê tin nhắn trong nhóm dữ liệu "nội dung bạn tạo" |
| DEC-156 | Phụ thuộc | Hiện hành | FR-M16-04.04, FR-M16-04.07, BR-M16-19, BR-M16-26 | Nhóm B. M01: tài khoản bị xóa — tin nhắn giữ nội dung, người gửi "[Người dùng đã xóa]" |
| DEC-179 | Nhắc tới | Hiện hành | Không áp dụng: M04: xóa mềm bình luận; nhóm và chat xem OPEN-011 | Nhóm B. M04: xóa mềm bình luận; nhóm và chat xem OPEN-011 |
| DEC-197 | Phụ thuộc | Hiện hành | FR-M16-03.03, BR-M16-22 | Nhóm B. M09: khi BANNED chỉ khiếu nại được lệnh ban |
| DEC-217 | Nhắc tới | Hiện hành | Không áp dụng: M07: số chưa đọc của chuông không tính tin nhắn chat | Nhóm B. M07: số chưa đọc của chuông không tính tin nhắn chat |
| DEC-219 | Phụ thuộc | Hiện hành | FR-M16-04.09 | Nhóm B. M07: popup tin nhắn mới, trừ khi đang xem đúng cuộc đó; tắt thông báo chỉ ẩn popup |
| DEC-220 | Phụ thuộc | Hiện hành | FR-M16-03, FR-M16-03.06, FR-M16-07.10 | Nhóm B. M07: số trên biểu tượng Tin nhắn = số cuộc có tin chưa đọc theo mốc đã đọc của M16 |
| DEC-225 | Sở hữu | Sửa một phần bởi DEC-256 | FR-M16-15, FR-M16-15.01, FR-M16-15.02, FR-M16-15.03, FR-M16-15.04, FR-M16-15.05, BR-M16-23 | Nhóm B. M10: cờ Chat tắt thì chặn thao tác người dùng; danh sách chặn/chạy ngầm thuộc FR M16 |
| DEC-239 | Nhắc tới | Hiện hành | Không áp dụng: M11: phần M16 của OPEN-011 vẫn mở | Nhóm B. M11: phần M16 của OPEN-011 vẫn mở |
| DG-1 | Nhắc tới | Hiện hành | Không áp dụng: Tổng quan dự án có nhắn tin | Nhóm B. Tổng quan dự án có nhắn tin |
| DG-4 | Sở hữu | Hiện hành | FR-M16-05.01 | Nhóm B. Bản đồ module: nhắn tin 1-1 và group chat, chỉ văn bản |
| DG-5 | Sở hữu | Sửa một phần bởi DEC-135, QA-218 | FR-M16-05.04 | Nhóm B. Nguyên tắc: chỉ văn bản; kênh real-time riêng (WebSocket); báo cáo tin nhắn tái dùng Report chung |
| DG-7 | Nhắc tới | Sửa một phần bởi DEC-135 | Không áp dụng: Kiến trúc: nhắn tin dùng WebSocket (kỹ thuật) | Nhóm B. Kiến trúc: nhắn tin dùng WebSocket (kỹ thuật) |
| DG-8 | Sở hữu | Hiện hành | FR-M16-05, FR-M16-05.04, BR-M16-08 | Nhóm B. Không làm: gọi thoại, video, gửi file trong nhắn tin |
| DM-10.1 | Phụ thuộc | Sửa một phần bởi QA-218 | FR-M16-05.10 | Nhóm B. M08: tin nhắn trong danh sách đối tượng báo cáo được (draft); nghi khác QA-218 |
| DM-13 | Nhắc tới | Sửa một phần bởi DEC-135 | Không áp dụng: Sơ đồ kiến trúc: Nhắn tin kênh real-time riêng | Nhóm B. Sơ đồ kiến trúc: Nhắn tin kênh real-time riêng |
| DM-8.1 | Phụ thuộc | Hiện hành | FR-M16-05.03, BR-M16-21 | Nhóm B. M07: sự kiện thông báo "Tin nhắn mới" |
| DM-x02 | Sở hữu | Hiện hành | FR-M16-05.01 | Nhóm B. Trong phạm vi: nhắn tin 1-1, group chat, chỉ văn bản |
| DM-x03 | Sở hữu | Hiện hành | FR-M16-05.04, BR-M16-08 | Nhóm B. Ngoài phạm vi: gọi thoại, video, gửi file trong nhắn tin |
| DM-x04 | Nhắc tới | Sửa một phần bởi DEC-135 | Không áp dụng: Nguyên tắc kiến trúc: nhắn tin real-time riêng (kỹ thuật) | Nhóm B. Nguyên tắc kiến trúc: nhắn tin real-time riêng (kỹ thuật) |
| ISS-041 | Nhắc tới | Trùng với QA-023 | — | Nhóm B. Phạm vi chat: DM + Group Chat (QA-023) |
| ISS-053 | Nhắc tới | Trùng với QA-046 | — | Nhóm B. Kiến trúc chat (QA-046) |
| ISS-099 | Nhắc tới | Trùng với DEC-067 | — | Nhóm B. M07: biểu tượng Tin nhắn riêng (DEC-067) |
| ISS-101 | Nhắc tới | Trùng với DEC-070 | — | Nhóm B. M07: tắt thông báo theo cuộc và toàn bộ Chat (DEC-070) |
| ISS-114 | Phụ thuộc | Sửa một phần bởi DEC-197 | FR-M16-03.03, BR-M16-22 | Nhóm B. M09: tài khoản bị ban vẫn đăng nhập, mọi thao tác bị chặn trừ khiếu nại |
| ISS-191 | Nhắc tới | Trùng với DEC-129 | — | Nhóm B. Lưu giữ tin nhắn chat (DEC-129) |
| ISS-198 | Nhắc tới | Trùng với DEC-135 | — | Nhóm B. Kênh real-time thống nhất SSE (DEC-135) |
| ISS-252 | Nhắc tới | Trùng với DEC-156 | — | Nhóm B. Tin nhắn của tài khoản đã xóa (DEC-156) |
| ISS-350 | Nhắc tới | Trùng với DEC-219 | — | Nhóm B. M07: tắt thông báo Chat (DEC-219) |
| ISS-351 | Nhắc tới | Trùng với DEC-220 | — | Nhóm B. M07: số chưa đọc Tin nhắn (DEC-220) |
| OPEN-003 | Sở hữu | Hiện hành | FR-M16-05.10, BR-M16-20 | Nhóm B. Chưa có chặn/báo cáo tin nhắn ở MS1 — hoãn có chủ đích |
| OPEN-008 | Phụ thuộc | Sửa một phần bởi DEC-154 | FR-M16-04.07 | Nhóm B. Privacy: dữ liệu chat khi xóa tài khoản (đã chốt phần lớn bởi DEC-154–157) |
| OPEN-011 | Sở hữu | Bị thay bởi DEC-248 | — | Nhóm B. Xét áp xóa mềm cho tin nhắn thu hồi — phần M16 còn mở; phần M16 đóng bởi DEC-248 |
| QA-011 | Sở hữu | Hiện hành | FR-M16-01, FR-M16-01.03, FR-M16-02.06, FR-M16-03.02, BR-M16-02 | Nhóm B. Guest không có quyền nhắn tin (MSG: Không) |
| QA-023 | Sở hữu | Sửa một phần bởi QA-221 | FR-M16-02, FR-M16-02.01, BR-M16-01 | Nhóm B. Phạm vi chat DM + Group Chat; phần "Group Chat trong Group" đã sửa bởi QA-221 |
| QA-046 | Sở hữu | Hiện hành | FR-M16-04, FR-M16-04.05, FR-M16-05, FR-M16-05.02, BR-M16-16 | Nhóm B. Gửi tin qua yêu cầu thường, nhận tin đẩy từ máy chủ (kỹ thuật) |
| QA-123 | Nhắc tới | Trùng với DEC-065 | — | Nhóm B. M07: danh sách sự kiện gồm chat |
| QA-129 | Nhắc tới | Trùng với DEC-067 | — | Nhóm B. M07: biểu tượng Tin nhắn riêng |
| QA-132 | Nhắc tới | Trùng với DEC-070 | — | Nhóm B. M07: tắt thông báo chat |
| QA-234 | Nhắc tới | Sửa một phần bởi DEC-134 | Không áp dụng: M14: phân trang feed nhất quán với Chat | Nhóm B. M14: phân trang feed nhất quán với Chat |
| QA-239 | Nhắc tới | Hiện hành | Không áp dụng: M14: banner dùng polling, khác Chat | Nhóm B. M14: banner dùng polling, khác Chat |
| QA-250 | Sở hữu | Trùng với DEC-129 | — | Nhóm B. Tin nhắn chat giữ vĩnh viễn (cùng nội dung DEC-129) |
| QA-257 | Sở hữu | Hiện hành | BR-M16-16 | Nhóm B. SSE cho chat; bỏ trạng thái online/offline |
| QA-264 | Nhắc tới | Hiện hành | Không áp dụng: Privacy: câu hỏi giữ chat vĩnh viễn so với xóa PII (OPEN-008) | Nhóm B. Privacy: câu hỏi giữ chat vĩnh viễn so với xóa PII (OPEN-008) |
| QA-312 | Phụ thuộc | Trùng với DEC-156 | — | Nhóm B. M01: tin nhắn của tài khoản đã xóa giữ nội dung, người gửi "[Người dùng đã xóa]" |
| QA-343 | Nhắc tới | Hiện hành | Không áp dụng: M04: nguyên tắc xóa mềm; M16 để bàn sau (OPEN-011) | Nhóm B. M04: nguyên tắc xóa mềm; M16 để bàn sau (OPEN-011) |
| QA-410 | Phụ thuộc | Trùng với DEC-219 | — | Nhóm B. M07: popup tin nhắn, tắt thông báo Chat |
| QA-411 | Phụ thuộc | Trùng với DEC-220 | — | Nhóm B. M07: (X5) biểu tượng Tin nhắn đếm số cuộc có tin chưa đọc |
| QA-417 | Phụ thuộc | Trùng với DEC-225 | — | Nhóm B. M10: Chat có cờ tính năng |
| QA-432 | Nhắc tới | Trùng với DEC-239 | — | Nhóm B. M11: phần M16 của OPEN-011 vẫn mở |
| F-GRP-05 | Nhắc tới | Hiện hành | Không áp dụng: Group Chat đã bỏ khỏi tính năng Group | Nhóm B. Group Chat đã bỏ khỏi tính năng Group |
| MR-A03 | Nhắc tới | Hiện hành | Không áp dụng: Tổng kết Phase 5: còn OPEN-003 | Nhóm B. Tổng kết Phase 5: còn OPEN-003 |
| MR-A04 | Nhắc tới | Hiện hành | Không áp dụng: Tổng kết Phase 6: giữ chat vĩnh viễn (DEC-129) | Nhóm B. Tổng kết Phase 6: giữ chat vĩnh viễn (DEC-129) |
| MR-M07 | Nhắc tới | Sửa một phần bởi DEC-135 | Không áp dụng: M07: danh sách sự kiện có chat | Nhóm B. M07: danh sách sự kiện có chat |
| MR-M09 | Nhắc tới | Hiện hành | Không áp dụng: M09: người bị ban vào màn hình khóa | Nhóm B. M09: người bị ban vào màn hình khóa |
| MR-M11 | Nhắc tới | Hiện hành | Không áp dụng: M11: Group Chat không thuộc Group | Nhóm B. M11: Group Chat không thuộc Group |
| ISS-137 | Nhắc tới | Hiện hành | Không áp dụng: M11: kế nhiệm Owner tự động — QA-222 nêu Group Chat không làm như vậy | Nhóm C. M11: kế nhiệm Owner tự động — QA-222 nêu Group Chat không làm như vậy |
| QA-124 | Phụ thuộc | Hiện hành | FR-M16-05.03, BR-M16-21 | Nhóm C. M07: email chỉ cho mật khẩu, vô hiệu hóa, ban, khiếu nại ban |
| QA-185 | Nhắc tới | Hiện hành | Không áp dụng: M11: kế nhiệm Owner tự động — QA-222 nêu Group Chat không làm như vậy | Nhóm C. M11: kế nhiệm Owner tự động — QA-222 nêu Group Chat không làm như vậy |
| DEC-127 | Phụ thuộc | Hiện hành | FR-M16-04.04 | Nhóm D. Dùng chung: lưu UTC, tính theo giờ Việt Nam |
| DEC-130 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: tải tệp — chat không gửi file | Nhóm D. Dùng chung: tải tệp — chat không gửi file |
| DEC-131 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: AI — chat không dùng AI | Nhóm D. Dùng chung: AI — chat không dùng AI |
| DEC-132 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: AI gợi ý Topic | Nhóm D. Dùng chung: AI gợi ý Topic |
| DEC-133 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: nhật ký AI — chat không gọi AI | Nhóm D. Dùng chung: nhật ký AI — chat không gọi AI |
| DEC-134 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: công nghệ | Nhóm D. Dùng chung: công nghệ |
| DEC-136 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: email — chat không gửi email | Nhóm D. Dùng chung: email — chat không gửi email |
| DEC-137 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: công nghệ | Nhóm D. Dùng chung: công nghệ |
| DEC-138 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: đồng ý chính sách khi đăng ký (M01) | Nhóm D. Dùng chung: đồng ý chính sách khi đăng ký (M01) |
| ISS-189 | Phụ thuộc | Trùng với DEC-127 | — | Nhóm D. Dùng chung: múi giờ (DEC-127) |
| ISS-190 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: ngôn ngữ giao diện | Nhóm D. Dùng chung: ngôn ngữ giao diện |
| ISS-192 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: tải tệp | Nhóm D. Dùng chung: tải tệp |
| ISS-193 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: AI | Nhóm D. Dùng chung: AI |
| ISS-194 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: AI | Nhóm D. Dùng chung: AI |
| ISS-195 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: AI | Nhóm D. Dùng chung: AI |
| ISS-196 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: theo dõi sự kiện | Nhóm D. Dùng chung: theo dõi sự kiện |
| ISS-197 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: công nghệ | Nhóm D. Dùng chung: công nghệ |
| ISS-199 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: email | Nhóm D. Dùng chung: email |
| ISS-200 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: cờ AI | Nhóm D. Dùng chung: cờ AI |
| ISS-201 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: triển khai | Nhóm D. Dùng chung: triển khai |
| ISS-202 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: công nghệ | Nhóm D. Dùng chung: công nghệ |
| ISS-203 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: công nghệ | Nhóm D. Dùng chung: công nghệ |
| ISS-204 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: đồng ý chính sách (M01) | Nhóm D. Dùng chung: đồng ý chính sách (M01) |
| QA-248 | Phụ thuộc | Trùng với DEC-127 | — | Nhóm D. Dùng chung: múi giờ (DEC-127) |
| QA-249 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: ngôn ngữ giao diện | Nhóm D. Dùng chung: ngôn ngữ giao diện |
| QA-251 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: tải tệp | Nhóm D. Dùng chung: tải tệp |
| QA-252 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: AI | Nhóm D. Dùng chung: AI |
| QA-253 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: AI | Nhóm D. Dùng chung: AI |
| QA-254 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: AI | Nhóm D. Dùng chung: AI |
| QA-255 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: theo dõi sự kiện | Nhóm D. Dùng chung: theo dõi sự kiện |
| QA-256 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: công nghệ | Nhóm D. Dùng chung: công nghệ |
| QA-258 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: email | Nhóm D. Dùng chung: email |
| QA-259 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: cờ AI | Nhóm D. Dùng chung: cờ AI |
| QA-260 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: triển khai | Nhóm D. Dùng chung: triển khai |
| QA-261 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: công nghệ | Nhóm D. Dùng chung: công nghệ |
| QA-262 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: cách làm mô hình dữ liệu | Nhóm D. Dùng chung: cách làm mô hình dữ liệu |
| QA-263 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: công nghệ | Nhóm D. Dùng chung: công nghệ |
| MR-A05 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: công nghệ | Nhóm D. Dùng chung: công nghệ |
| DEC-248 | Sở hữu | Hiện hành | FR-M16-06, FR-M16-06.07, BR-M16-12, BR-M16-18 | Nhóm A. Thu hồi là xóa mềm; đóng phần M16 của OPEN-011 |
| DEC-249 | Sở hữu | Hiện hành | FR-M16-02.04, FR-M16-03.06, FR-M16-04, FR-M16-04.03, FR-M16-04.08, FR-M16-04.10, FR-M16-05.06, FR-M16-07.10, FR-M16-08.06, FR-M16-08.08, FR-M16-11.01, FR-M16-11.03, FR-M16-14, FR-M16-14.01, FR-M16-14.04, FR-M16-14.05, FR-M16-16.08, BR-M16-03, BR-M16-04, BR-M16-07, BR-M16-27, BR-M16-28 | Nhóm A. Thành viên nhóm chat theo thời gian: 3 người chỉ khi tạo, thành viên cuối, thành viên cũ, vào lại, lịch sử |
| DEC-250 | Sở hữu | Sửa một phần bởi DEC-257 | FR-M16-13.03, FR-M16-17, FR-M16-17.01, FR-M16-17.02, FR-M16-17.03, BR-M16-30 | Nhóm A. Admin nhóm chat không thể khôi phục: tự tắt duyệt, người chờ vào ngay |
| DEC-251 | Sở hữu | Hiện hành | FR-M16-08, FR-M16-08.10, FR-M16-08.11, FR-M16-08.12, FR-M16-08.13, FR-M16-09.01, FR-M16-10, FR-M16-10.01, FR-M16-10.02, FR-M16-10.05, FR-M16-16, FR-M16-16.01, FR-M16-16.02, FR-M16-16.03, FR-M16-16.04, FR-M16-16.05, FR-M16-16.06, FR-M16-16.07, BR-M16-05, BR-M16-06, BR-M16-29 | Nhóm A. Link mời nhóm chat và xin gia nhập (mở rộng phạm vi) |
| DEC-252 | Sở hữu | Hiện hành | FR-M16-01, FR-M16-01.05, FR-M16-01.06, BR-M16-24 | Nhóm A. Một cuộc 1-1 mỗi cặp; không tự nhắn |
| DEC-253 | Sở hữu | Hiện hành | FR-M16-01.07, FR-M16-02.09, FR-M16-04.11, FR-M16-04.12, FR-M16-05.13, FR-M16-05.14, FR-M16-08.09, BR-M16-25, BR-M16-26 | Nhóm A. Tài khoản bị ban, vô hiệu hóa, đã xóa trong Chat |
| DEC-254 | Sở hữu | Hiện hành | FR-M16-03, FR-M16-03.01, FR-M16-03.04, FR-M16-03.05, FR-M16-03.06, FR-M16-03.07, FR-M16-03.08, BR-M16-31 | Nhóm A. Hộp thư Chat |
| DEC-255 | Sở hữu | Sửa một phần bởi DEC-257 | FR-M16-02, FR-M16-02.07, FR-M16-02.08, FR-M16-05, FR-M16-05.05, FR-M16-05.11, FR-M16-05.12, FR-M16-06.08, FR-M16-06.09, FR-M16-07, FR-M16-07.06, FR-M16-07.07, FR-M16-07.11, FR-M16-09.03, FR-M16-10.03, FR-M16-10.07, FR-M16-12.03, BR-M16-03, BR-M16-06, BR-M16-08, BR-M16-09, BR-M16-12, BR-M16-13, BR-M16-15, BR-M16-32 | Nhóm A. Danh sách xác nhận: duyệt, độ dài, 60 giây, đã xem, tên nhóm, thu hồi |
| DEC-256 | Sở hữu | Hiện hành | FR-M16-15, FR-M16-15.04, FR-M16-15.06, FR-M16-15.07, FR-M16-15.08, BR-M16-23 | Nhóm A. Khi cờ Chat tắt |
| ISS-383 | Sở hữu | Trùng với DEC-248 | — | Nhóm A. Câu hỏi ở bước 6 FR M16; xem DEC-248 |
| ISS-384 | Sở hữu | Trùng với DEC-249 | — | Nhóm A. Câu hỏi ở bước 6 FR M16; xem DEC-249 |
| ISS-385 | Sở hữu | Trùng với DEC-249 | — | Nhóm A. Câu hỏi ở bước 6 FR M16; xem DEC-249 |
| ISS-386 | Sở hữu | Trùng với DEC-250 | — | Nhóm A. Câu hỏi ở bước 6 FR M16; xem DEC-250 |
| ISS-387 | Sở hữu | Trùng với DEC-251 | — | Nhóm A. Câu hỏi ở bước 6 FR M16; xem DEC-251 |
| ISS-388 | Sở hữu | Trùng với DEC-252 | — | Nhóm A. Câu hỏi ở bước 6 FR M16; xem DEC-252 |
| ISS-389 | Sở hữu | Trùng với DEC-253 | — | Nhóm A. Câu hỏi ở bước 6 FR M16; xem DEC-253 |
| ISS-390 | Sở hữu | Trùng với DEC-254 | — | Nhóm A. Câu hỏi ở bước 6 FR M16; xem DEC-254 |
| ISS-391 | Sở hữu | Trùng với DEC-256 | — | Nhóm A. Câu hỏi ở bước 6 FR M16; xem DEC-256 |
| ISS-392 | Sở hữu | Trùng với DEC-255 | — | Nhóm A. Câu hỏi ở bước 6 FR M16; xem DEC-255 |
| QA-445 | Sở hữu | Trùng với DEC-248 | — | Nhóm A. Câu trả lời ở bước 6 FR M16; nội dung ghi ở DEC-248 |
| QA-446 | Sở hữu | Trùng với DEC-249 | — | Nhóm A. Câu trả lời ở bước 6 FR M16; nội dung ghi ở DEC-249 |
| QA-447 | Sở hữu | Trùng với DEC-249 | — | Nhóm A. Câu trả lời ở bước 6 FR M16; nội dung ghi ở DEC-249 |
| QA-448 | Sở hữu | Trùng với DEC-250 | — | Nhóm A. Câu trả lời ở bước 6 FR M16; nội dung ghi ở DEC-250 |
| QA-449 | Sở hữu | Trùng với DEC-251 | — | Nhóm A. Câu trả lời ở bước 6 FR M16; nội dung ghi ở DEC-251 |
| QA-450 | Sở hữu | Trùng với DEC-252 | — | Nhóm A. Câu trả lời ở bước 6 FR M16; nội dung ghi ở DEC-252 |
| QA-451 | Sở hữu | Trùng với DEC-253 | — | Nhóm A. Câu trả lời ở bước 6 FR M16; nội dung ghi ở DEC-253 |
| QA-452 | Sở hữu | Trùng với DEC-254 | — | Nhóm A. Câu trả lời ở bước 6 FR M16; nội dung ghi ở DEC-254 |
| QA-453 | Sở hữu | Trùng với DEC-256 | — | Nhóm A. Câu trả lời ở bước 6 FR M16; nội dung ghi ở DEC-256 |
| QA-454 | Sở hữu | Trùng với DEC-255 | — | Nhóm A. Câu trả lời ở bước 6 FR M16; nội dung ghi ở DEC-255 |
| DEC-257 | Sở hữu | Hiện hành | FR-M16-09.03, FR-M16-09.04, FR-M16-17.02, BR-M16-33 | Nhóm A. Người chờ duyệt khi tắt duyệt mà không đủ chỗ: chờ trước vào trước, còn lại bị từ chối |
| ISS-393 | Sở hữu | Trùng với DEC-257 | — | Nhóm A. Câu hỏi ở bước 6 FR M16; xem DEC-257 |
| QA-455 | Sở hữu | Trùng với DEC-257 | — | Nhóm A. Câu trả lời ở bước 6 FR M16; nội dung ghi ở DEC-257 |
| DEC-122 | Nhắc tới | Hiện hành | Không áp dụng: tiền lệ, DEC-253 dẫn lại: nội dung của tài khoản bị ban hiện bình thường | Nhóm C. DEC-253 dẫn lại: nội dung của tài khoản bị ban hiện bình thường |
| DEC-213 | Nhắc tới | Hiện hành | Không áp dụng: tiền lệ, DEC-255 dẫn lại: "mỗi phút" là 60 giây gần nhất | Nhóm C. DEC-255 dẫn lại: "mỗi phút" là 60 giây gần nhất |
| DEC-229 | Nhắc tới | Hiện hành | Không áp dụng: tiền lệ, DEC-251 dẫn lại: link mời của Group | Nhóm C. DEC-251 dẫn lại: link mời của Group |
| DEC-236 | Nhắc tới | Hiện hành | Không áp dụng: tiền lệ, DEC-256 dẫn lại: khuôn danh sách khi cờ Group tắt | Nhóm C. DEC-256 dẫn lại: khuôn danh sách khi cờ Group tắt |
| DEC-237 | Nhắc tới | Hiện hành | Không áp dụng: tiền lệ, DEC-251, DEC-255 dẫn lại: tên Group, công tắc của Group | Nhóm C. DEC-251, DEC-255 dẫn lại: tên Group, công tắc của Group |
| DEC-245 | Nhắc tới | Hiện hành | Không áp dụng: tiền lệ, DEC-256 dẫn lại: khuôn danh sách khi cờ Gamification tắt | Nhóm C. DEC-256 dẫn lại: khuôn danh sách khi cờ Gamification tắt |

### C.2 Chuỗi quyết định

| Chuỗi | Nội dung hiện hành |
|---|---|
| QA-023 → QA-221 → DEC-249 (ISS-163, MR-A01, MR-M11, F-GRP-05) | Còn hiệu lực: chat gồm cả 1-1 và Group Chat. Bị thay: "Group Chat trong Group" và phụ thuộc M16→M11; Group Chat là cuộc trò chuyện độc lập, ai cũng tạo được. "3+ người" chỉ kiểm khi tạo; nhóm còn dưới 3 vẫn hoạt động (DEC-249). QA-222 thêm giới hạn 100. |
| DM-6.4, DG-5, DG-7, DM-13, DM-x04 → QA-046 → DEC-135 (QA-257) | Bị thay: kênh WebSocket. Hiện hành: tin nhắn và trạng thái đã xem tới người nhận tức thời (đẩy từ máy chủ, SSE); gửi tin là yêu cầu thường. Không có trạng thái online/offline, không có "đang gõ". |
| DM-6.3, DG-5, DM-10.1 → QA-218 (ISS-160, OPEN-003) | Bị thay: báo cáo tin nhắn qua Report chung. Hiện hành ở MS1: không báo cáo, không chặn tin nhắn (TBD-M16-01). |
| DM-6.2 → QA-208 (QA-209, QA-210, QA-211, QA-212, ISS-155) → DEC-255 | Bị thay: trạng thái đã đọc/chưa đọc trên từng tin. Hiện hành: hai trạng thái Đã gửi, Đã xem, chỉ hiện ở tin mới nhất, suy ra từ mốc đã đọc của từng thành viên; gửi tin đưa mốc của người gửi tới tin đó; dưới tin mới nhất hiện avatar người đã đọc, trừ người gửi và người đang xem (DEC-255). |
| DEC-129 → DEC-156, DEC-248 (QA-312, ISS-252) | Hiện hành: nội dung tin nhắn giữ vĩnh viễn, kể cả tin đã thu hồi (DEC-248); tài khoản bị xóa thì tin nhắn giữ nội dung, người gửi hiện "[Người dùng đã xóa]". |
| QA-214 ↔ DEC-129, QA-343 → OPEN-011 → DEC-239, DEC-248 | Đã giải: thu hồi là xóa mềm — gắn cờ, nội dung gốc giữ, không ai xem được ở MS1; mọi thành viên thấy "Tin nhắn đã bị thu hồi" ở đúng vị trí (DEC-248). OPEN-011 đóng (phần M11 bởi DEC-239, phần M16 bởi DEC-248). Phần khác của QA-214, QA-215, QA-216 giữ nguyên. |
| DEC-067 → DEC-217, DEC-220, DEC-254 (QA-129, QA-411) | Hiện hành: biểu tượng Tin nhắn riêng, số trên biểu tượng là số cuộc trò chuyện có tin chưa đọc theo mốc đã đọc của M16; chuông thông báo không tính tin nhắn chat. Hộp thư Chat xếp theo tin mới nhất, mỗi dòng có tên, tin mới nhất, thời điểm, đánh dấu chưa đọc, tải 20 cuộc mỗi lần (DEC-254). |
| DEC-070 → DEC-219 (QA-132, QA-410) | Hiện hành: tắt thông báo từng cuộc và toàn bộ Chat; tắt toàn bộ không có ngoại lệ; tắt chỉ ẩn popup, số chưa đọc vẫn đúng; không popup khi đang xem đúng cuộc đó. |
| DEC-092 → DEC-225 → DEC-256 (QA-417; DEC-228 ngoài bảng nguồn) | Hiện hành: Chat có cờ tính năng; khi tắt, mọi thao tác của người dùng với Chat bị từ chối "Hệ thống đang bận, vui lòng thử lại sau" theo danh sách ở DEC-256; vẫn hiện biểu tượng Tin nhắn, số chưa đọc, nút "Nhắn tin"; vẫn chạy tự tắt duyệt (DEC-250) và hạn thu hồi; dữ liệu không đổi; ADMIN vẫn dùng được. Giá trị khởi tạo của cờ: bật (DEC-228). Các sửa đổi DEC-236, DEC-245 chỉ thuộc M11, M12. |
| ISS-114 → DEC-197 (DEC-152, MR-M09) | Hiện hành: tài khoản bị ban vẫn đăng nhập, vào màn hình khóa, chỉ khiếu nại được chính lệnh ban; mọi thao tác khác bị chặn. |
| OPEN-008 → DEC-154 (DEC-155–157 ngoài bảng nguồn) | Phần chat đã chốt: trang chính sách xếp tin nhắn vào "nội dung bạn tạo" và nêu việc giữ lại sau khi xóa tài khoản vì an toàn cộng đồng. Phần còn mở (email liên hệ, cách nhận bản sao dữ liệu) không thuộc M16. |
| DEC-065 → DEC-147, DEC-151, DEC-180, DEC-215, DEC-218, DEC-221, DEC-231, DEC-237, DEC-246 (ngoài bảng nguồn) | Các sửa đổi chỉ thêm sự kiện khác. Dòng "tin nhắn 1-1 / Group chat: trong ứng dụng có, email không" không đổi (QA-223 cùng ý). |
| DEC-092 → DEC-226 (ngoài bảng nguồn) | DEC-226 chỉ quy định banner toàn trang; mục cờ tính năng Chat không đổi. |
| DEC-156 → DEC-159 (ngoài bảng nguồn) | DEC-159 thêm việc xóa theo dõi và giữ phản hồi gợi ý Topic khi xóa tài khoản; phần tin nhắn ("[Người dùng đã xóa]", giữ nội dung) không đổi. |
| DEC-220 → DEC-222 (ngoài bảng nguồn) | DEC-222 chỉ sửa đề xuất làm Mod, Admin; mục biểu tượng Tin nhắn đếm số cuộc có tin chưa đọc không đổi. |
| QA-011 → DEC-171, DEC-206, DEC-208 (ngoài bảng nguồn) | Các sửa đổi về hồ sơ, tóm tắt AI, tìm kiếm của Guest; phần "MSG: Không" (Guest không nhắn tin) không đổi. |
| QA-222 → DEC-249, DEC-250, DEC-251 (ISS-164) | Hiện hành: vai trò Admin nhóm chat, Member; mọi thành viên thêm người, lấy link mời, đổi tên, rời; chỉ Admin duyệt, xóa thành viên, bật tắt duyệt, chuyển quyền; Admin là thành viên cuối cùng rời không cần chuyển quyền; người rời, bị xóa giữ lịch sử tới lúc rời, vào lại theo luồng thường (DEC-249); Admin không thể khôi phục thì duyệt tự tắt, không tự chuyển quyền (DEC-250); link mời và xin gia nhập (DEC-251, mở rộng phạm vi). |
| QA-220 → DEC-252, DEC-253 (ISS-162) | Hiện hành: nhắn 1-1 mở cho bất kỳ người dùng nào khác; mỗi cặp một cuộc 1-1 (DEC-252); không bắt đầu 1-1 mới, không thêm vào nhóm tài khoản bị ban, vô hiệu hóa, đã xóa; cuộc 1-1 đã có vẫn gửi được tới tài khoản bị ban, vô hiệu hóa, không gửi được tới tài khoản đã xóa (DEC-253). |
| QA-219 → DEC-255 (ISS-161) | Hiện hành: 30 tin trong 60 giây gần nhất, theo từng cặp (người gửi, cuộc trò chuyện); vượt thì bị từ chối và báo gửi quá nhanh. |
| MR-M16 → DEC-251 | Dòng module thêm link mời và xin gia nhập nhóm chat; phần còn lại không đổi. |
| DEC-250, DEC-255 → DEC-257 | Hiện hành: khi duyệt được tắt (Admin tắt hoặc tự tắt khi Admin không thể khôi phục), người chờ vào theo thứ tự bắt đầu chờ tới khi nhóm đủ 100; người không đủ chỗ chuyển Đã từ chối, vào lại theo luồng thường. |
