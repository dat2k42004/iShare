---
module: M10
ten_module: Admin Panel
ma_tai_lieu: FR-M10
phien_ban: 1.1
trang_thai: Đã chốt
ngay: 2026-10-24
tac_gia: Phạm Văn Đức
moc_nguon: DEC-228, QA-420, ISS-359, OPEN-012
steps_completed: [1, 2, 3, 4, 5, 6, 7]
---
# Tài liệu yêu cầu chức năng — M10 Admin Panel

| Mã tài liệu | FR-M10 |
|---|---|
| Dự án | iShare |
| Module | M10 — Admin Panel |
| Trạng thái | Đã chốt |
| Phiên bản | 1.1 |
| Ngày | 2026-10-24 |
| Tác giả | Phạm Văn Đức |

<!-- Quy ước chung cho mọi bảng dưới đây:
     - Thân tài liệu không ghi nguồn. Nguồn của mọi ID nằm ở Phụ lục A.
     - Ô không có nội dung ghi "—". Không xóa cột.
     - Mục chưa tới bước làm thì để dòng "(Chưa làm — bước N)". -->

## 1. Tổng quan

### 1.1 Mục đích

Admin Panel là nơi Admin vận hành hệ thống: quản lý vai trò (đề xuất người dùng làm Mod, giáng cấp Mod; tài khoản ADMIN
gốc đề xuất làm Admin và thu hồi vai trò Admin), bật tắt cấu hình hệ thống (công tắc AI tổng và theo module, chế độ bảo
trì, tạm dừng đăng ký, cờ tính năng cho Group, Chat, Gamification, banner thông báo toàn trang) và xem nhật ký thao tác
Admin. Mọi thao tác của Admin và mọi thay đổi vai trò đều được ghi vào nhật ký chỉ ghi thêm, để minh bạch kể cả với chính
Admin. Các hằng số chính sách (thời hạn, ngưỡng) không chỉnh qua giao diện.

### 1.2 Phạm vi

**Trong phạm vi:**

- Mô hình vai trò: ba vai trò USER, MODERATOR, ADMIN; mỗi tài khoản đúng một vai trò, theo thứ bậc
  USER < MODERATOR < ADMIN; Admin có mọi quyền của Mod. Một tài khoản ADMIN gốc tạo sẵn, không bị thu hồi, không từ chức.
- Phân định việc chỉ Admin làm (quản lý vai trò, cấu hình hệ thống, xem toàn bộ nhật ký, quản lý tài khoản Mod) và việc
  dùng chung với Mod.
- Xem người dùng: tìm theo username hoặc tên hiển thị, lọc theo vai trò; từ một Mod mở nhật ký kiểm duyệt lọc theo Mod đó
  (cách Admin theo dõi "hiệu suất" của Mod).
- Đề xuất làm Mod (Admin gửi) và đề xuất làm Admin (chỉ ADMIN gốc gửi): người nhận Chấp nhận hoặc Từ chối, một lần; đề
  xuất có hạn 7 ngày; mỗi người có tối đa một đề xuất còn hiệu lực cho mỗi loại; chỉ gửi cho tài khoản ACTIVE đã hoàn tất
  đăng ký.
- Giáng cấp Mod (Admin) và thu hồi vai trò Admin (chỉ ADMIN gốc): trực tiếp, ngay, không cần đồng ý, không khiếu nại;
  tài khoản về USER.
- Tự từ chức của Mod và của Admin không phải gốc, có bước xác nhận.
- Thu hồi vai trò Mod khi Mod bị ban (M08 kích hoạt).
- Cấu hình hệ thống, đổi lúc đang chạy, không cần triển khai lại, có giá trị khởi tạo: công tắc AI tổng và ba công tắc
  riêng (Search, Moderation, Topic suggestion); chế độ bảo trì; tạm dừng đăng ký; cờ tính năng cho Group, Chat,
  Gamification; banner thông báo toàn trang.
- Nguyên tắc chung khi một cờ tính năng tắt: chặn thao tác của người dùng với module và báo hệ thống đang bận; việc hệ
  thống tự làm vẫn chạy; dữ liệu giữ nguyên; Admin vẫn dùng được module.
- Banner: một banner, văn bản thuần, tối đa 200 ký tự; người xem đóng được, nội dung mới thì hiện lại.
- Nhật ký thao tác Admin: ghi mọi thao tác làm đổi dữ liệu của Admin và mọi thay đổi vai trò; chỉ ghi thêm; Admin xem
  được, mới nhất trước, lọc theo người làm và loại thao tác; không ai sửa, xóa; giữ vĩnh viễn.

**Ngoài phạm vi:**

- Hành vi của từng module khi công tắc AI tắt (cách dự phòng) — M03, M04, M05, M06, M08; gọi AI, lỗi tạm thời, nhật ký
  quyết định AI, tóm tắt AI theo công tắc tổng — M13 AI Layer.
- Tác động của tạm dừng đăng ký và chế độ bảo trì lên đăng ký, đăng nhập, phiên; gán vai trò USER khi tạo tài khoản —
  M01 Authentication & Account.
- Gửi và hiển thị thông báo "Đề xuất làm Mod", "Đề xuất làm Admin" (nút Chấp nhận, Từ chối; trả lời một lần; hiện "Đã
  hết hạn") — M07 Notification.
- Cảnh cáo, ban (kể cả việc chỉ Admin cảnh cáo, ban Mod; Admin không bị cảnh cáo, ban, báo cáo), gỡ ban, hàng chờ báo
  cáo, nhật ký kiểm duyệt, quyền xem và việc lọc nhật ký kiểm duyệt theo người làm — M08 Moderation.
- Khiếu nại; lật ban của Mod cũ không trả lại vai trò Mod — M09 Appeal.
- Thêm, gộp, xóa Topic (chỉ Admin), vô hiệu hóa Tag — M05 Topic & Tag.
- Danh sách chi tiết thao tác bị chặn và việc chạy ngầm khi cờ tính năng tắt — M11 Group, M12 Gamification, M16 Chat &
  Messaging.
- Bảng thống kê chỉ Admin xem — M15 Analytics & Stats.
- Đã quyết không làm: chỉnh hằng số chính sách (thời hạn cảnh cáo, ban, ngưỡng AI, trọng số mức nghiêm trọng, hạn của
  đề xuất) qua giao diện; công tắc dịch vụ email; màn hình Admin sửa hoặc đăng trang chính sách; điều kiện về điểm, uy
  tín để được làm Mod; khiếu nại việc giáng cấp, thu hồi vai trò Admin; một tài khoản giữ cùng lúc hai vai trò; công tắc
  AI riêng cho tóm tắt; màn hình hay chỉ số hiệu suất riêng của Mod; cờ tính năng cho module khác ngoài Group, Chat,
  Gamification; Admin không phải gốc cấp, thu hồi vai trò Admin; thu hồi vai trò của tài khoản ADMIN gốc; nhiều banner
  cùng lúc, hẹn giờ banner.

## 2. Thuật ngữ và viết tắt

### 2.1 Thuật ngữ

| Thuật ngữ | Định nghĩa |
|---|---|
| Vai trò | Một trong ba giá trị USER, MODERATOR (Mod), ADMIN gắn với mỗi tài khoản. Mỗi tài khoản có đúng một vai trò, theo thứ bậc USER < MODERATOR < ADMIN; vai trò cao hơn có mọi quyền của vai trò thấp hơn. |
| Admin Panel | Khu vực quản trị chỉ tài khoản ADMIN vào được, gồm quản lý người dùng và vai trò, cấu hình hệ thống, nhật ký thao tác Admin. |
| Tài khoản ADMIN gốc | Tài khoản ADMIN đầu tiên do đội phát triển tạo sẵn khi khởi tạo hệ thống, không qua đăng ký. Mang vai trò ADMIN và được đánh dấu "gốc"; "gốc" không phải vai trò thứ tư. Là tài khoản duy nhất cấp, thu hồi vai trò Admin; không bị thu hồi, không từ chức. |
| Đề xuất | Lời mời gửi tới một người dùng để người đó nhận một vai trò. Có hai loại: đề xuất làm Mod (Admin gửi, cho tài khoản USER) và đề xuất làm Admin (ADMIN gốc gửi, cho tài khoản USER hoặc MODERATOR). Người nhận trả lời Chấp nhận hoặc Từ chối trên thông báo (M07). |
| Người được đề xuất | Vai trò theo ngữ cảnh: người dùng nhận một đề xuất. |
| Thời điểm gửi đề xuất | Lúc hệ thống lưu đề xuất; dùng để tính hạn của đề xuất. |
| Hạn của đề xuất | 7 ngày, tính bằng 7 × 24 giờ từ thời điểm gửi đề xuất. Là hằng số chính sách. |
| Đề xuất còn hiệu lực | Đề xuất ở trạng thái Chưa trả lời: chưa được trả lời, chưa quá hạn, chưa bị một đề xuất mới cùng loại cho cùng người thay. |
| Trạng thái của đề xuất | Chưa trả lời, Đã chấp nhận, Đã từ chối, Hết hiệu lực (quá hạn hoặc bị đề xuất mới cùng loại thay). |
| Giáng cấp | Admin đưa một Mod về vai trò USER; không cần Mod đồng ý, không phải hình phạt nên không khiếu nại được. |
| Thu hồi vai trò Admin | ADMIN gốc đưa một tài khoản ADMIN khác về vai trò USER; không cần đồng ý, không khiếu nại được. |
| Tự từ chức | Mod hoặc Admin không phải gốc tự bỏ vai trò của mình để về vai trò USER, sau một bước xác nhận. |
| Cấu hình hệ thống | Các công tắc và nội dung Admin đổi được từ Admin Panel lúc hệ thống đang chạy, không cần triển khai lại: công tắc AI, chế độ bảo trì, tạm dừng đăng ký, cờ tính năng, banner thông báo toàn trang. |
| Công tắc AI tổng | Công tắc cấu hình bật hoặc tắt toàn bộ lớp AI; khi tắt, mọi tính năng AI tắt bất kể công tắc riêng. |
| Công tắc AI riêng | Ba công tắc cấu hình Search, Moderation, Topic suggestion; mỗi công tắc chỉ có tác dụng khi công tắc AI tổng bật. |
| Chế độ bảo trì | Cấu hình khi bật thì chỉ tài khoản ADMIN đăng nhập và dùng hệ thống được (thi hành ở M01). |
| Tạm dừng đăng ký | Cấu hình khi bật thì hệ thống ngừng nhận tài khoản mới (thi hành ở M01). Không phải cờ tính năng. |
| Cờ tính năng | Công tắc cấu hình bật hoặc tắt một trong ba module Group (M11), Chat (M16), Gamification (M12). |
| Thao tác của người dùng với một module | Mọi yêu cầu người dùng gửi tới module: mở trang, xem nội dung, tạo, sửa, xóa, tham gia, gửi tin nhắn… |
| Việc hệ thống tự làm | Việc module chạy mà không do người dùng gửi yêu cầu, ví dụ cộng điểm khi có Star, tính bảng xếp hạng định kỳ, tự chuyển quyền chủ nhóm. |
| Banner thông báo toàn trang | Một thông báo văn bản do Admin đặt, hiện trên mọi trang cho mọi người, kể cả Guest. |
| Ký tự của banner | Số ký tự của nội dung banner sau khi bỏ khoảng trắng ở đầu và cuối. |
| Nhật ký thao tác Admin | Danh sách các thao tác làm đổi dữ liệu do Admin làm và các thay đổi vai trò; chỉ ghi thêm, không ai sửa hoặc xóa được. Khác nhật ký kiểm duyệt (M08) và nhật ký quyết định AI (M13). |
| Người làm (của mục nhật ký) | Tài khoản đã làm thao tác, hoặc "Hệ thống" với thay đổi do hệ thống tự làm (Mod mất vai trò do bị ban). |
| Thời điểm (của mục nhật ký) | Lúc thao tác hoàn tất và được hệ thống ghi nhận. |
| Hằng số chính sách | Giá trị nghiệp vụ cố định như thời hạn cảnh cáo, ban, ngưỡng AI, trọng số mức nghiêm trọng, hạn của đề xuất; không chỉnh qua Admin Panel, chỉ đổi qua triển khai. |
| Giờ Việt Nam | Múi giờ Asia/Ho_Chi_Minh (UTC+7); mọi thời điểm hiển thị trong module tính theo múi giờ này. |
| Trạng thái của công tắc cấu hình | Bật hoặc Tắt. Banner: Đang hiện hoặc Không hiện. |

### 2.2 Viết tắt

| Viết tắt | Đầy đủ |
|---|---|
| FR | Functional Requirement — yêu cầu chức năng |
| BR | Business Rule — quy tắc nghiệp vụ |
| TBD | To Be Determined — điểm chưa chốt |
| AI | Artificial Intelligence — trí tuệ nhân tạo |
| MS1 | Milestone 1 — mốc phát hành đầu tiên của dự án |
| UTC | Coordinated Universal Time — giờ phối hợp quốc tế |

## 3. Thông tin đầu vào

### 3.1 Tài liệu đầu vào

| Tài liệu | Phiên bản / mốc |
|---|---|
| Draft: docs/_temp/iShare_modules.md, iShare_specs_general.md | Theo ngày sửa tệp |
| Register: decisions, qa-log, issue-queue, open-issues, glossary, module-registry | DEC-228, QA-420, ISS-359, OPEN-012 (khớp `moc_nguon`) |

### 3.2 Tài liệu liên quan

| Module | Liên quan ở điểm nào |
|---|---|
| M01 Authentication & Account | Thi hành tạm dừng đăng ký và chế độ bảo trì; tài khoản mới mang vai trò USER. |
| M03 Post & Content, M04 Comment | Theo công tắc AI tổng và công tắc Moderation để quét bài, bình luận. |
| M05 Topic & Tag | Theo công tắc gợi ý Topic; quản lý danh mục Topic chỉ Admin làm. |
| M06 Search | Theo công tắc AI tổng và công tắc Search (tìm ngữ nghĩa hay full-text); cách khớp tên khi tìm người dùng được dùng lại ở Admin Panel. |
| M07 Notification | Gửi thông báo "Đề xuất làm Mod", "Đề xuất làm Admin", hiện "Đã hết hạn" khi đề xuất hết hiệu lực; chuyển lựa chọn Chấp nhận, Từ chối về M10. |
| M08 Moderation | Ban Mod thì thu hồi vai trò Mod; quyền theo vai trò khi xử lý; nhật ký kiểm duyệt riêng với nhật ký thao tác Admin, lọc được theo người làm để Admin theo dõi Mod. |
| M09 Appeal | Giáng cấp, thu hồi vai trò Admin không khiếu nại; lật ban Mod cũ không trả vai trò. |
| M11 Group, M12 Gamification, M16 Chat & Messaging | Bị bật, tắt bằng cờ tính năng; FR của từng module ghi chi tiết thao tác bị chặn và việc chạy ngầm khi cờ tắt. |
| M13 AI Layer | Áp dụng trạng thái công tắc AI cho các lời gọi AI. |
| M15 Analytics & Stats | Bảng thống kê chỉ Admin xem. |

## 4. Tổng quan chức năng

### 4.1 Luật, tiêu chuẩn liên quan

Không có.

### 4.2 Vai trò

| Vai trò | Mô tả trong module này |
|---|---|
| Guest | Người chưa đăng nhập. Không vào được Admin Panel; thấy và đóng được banner; bị từ chối khi dùng module có cờ tính năng đang tắt. |
| User | Người dùng đã đăng nhập. Không vào được Admin Panel; trả lời đề xuất làm Mod, làm Admin gửi cho mình; thấy, đóng banner; bị từ chối khi dùng module có cờ đang tắt. |
| Mod | Có quyền của User. Không vào được Admin Panel; trả lời đề xuất làm Admin gửi cho mình; tự từ chức vai trò Mod. |
| Admin | Có mọi quyền của Mod. Vào Admin Panel: xem người dùng, đề xuất làm Mod, giáng cấp Mod, đổi cấu hình hệ thống, đặt banner, xem nhật ký thao tác Admin; tự từ chức nếu không phải ADMIN gốc; vẫn dùng module có cờ đang tắt. Không cấp, thu hồi vai trò Admin; không sửa, xóa nhật ký; không chỉnh hằng số chính sách. |
| Tài khoản ADMIN gốc | Vai trò theo ngữ cảnh: tài khoản ADMIN tạo sẵn. Có mọi quyền của Admin, thêm: gửi đề xuất làm Admin, thu hồi vai trò Admin của tài khoản khác. Không bị thu hồi, không từ chức. |
| Người được đề xuất | Vai trò theo ngữ cảnh: người dùng nhận một đề xuất; chỉ người này trả lời được đề xuất đó. |
| Hệ thống | Cho đề xuất hết hiệu lực khi quá hạn; thu hồi vai trò Mod khi Mod bị ban; ghi nhật ký thao tác Admin. |

### 4.3 Ma trận quyền

| Hành động | Guest | User | Mod | Admin | Yêu cầu |
|---|---|---|---|---|---|
| Vào Admin Panel, xem người dùng | ✗ | ✗ | ✗ | ✓ | FR-M10-01.01, FR-M10-01.02 |
| Gửi đề xuất làm Mod | ✗ | ✗ | ✗ | ✓ | FR-M10-02.01, FR-M10-02.06 |
| Gửi đề xuất làm Admin | ✗ | ✗ | ✗ | ✓ (chỉ ADMIN gốc) | FR-M10-07.05, FR-M10-07.01, FR-M10-07.07 |
| Trả lời đề xuất làm Mod | ✗ | ✓ (của mình) | — | — | FR-M10-03.01, FR-M10-03.03, FR-M10-03.07 |
| Trả lời đề xuất làm Admin | ✗ | ✓ (của mình) | ✓ (của mình) | — | FR-M10-03.09, FR-M10-03.03, FR-M10-03.07 |
| Giáng cấp Mod | ✗ | ✗ | ✗ | ✓ | FR-M10-04.01, FR-M10-04.04 |
| Thu hồi vai trò Admin của tài khoản Admin khác | ✗ | ✗ | ✗ | ✓ (chỉ ADMIN gốc) | FR-M10-08.03, FR-M10-08.01, FR-M10-08.05 |
| Thu hồi vai trò của tài khoản ADMIN gốc | ✗ | ✗ | ✗ | ✗ | FR-M10-08.04 |
| Tự từ chức | ✗ | — | ✓ (của mình) | ✓ (của mình, trừ ADMIN gốc) | FR-M10-05.01, FR-M10-05.02, FR-M10-05.04, FR-M10-05.05 |
| Bật, tắt công tắc AI tổng và công tắc AI riêng | ✗ | ✗ | ✗ | ✓ | FR-M10-09.02, FR-M10-09.08 |
| Bật, tắt chế độ bảo trì | ✗ | ✗ | ✗ | ✓ | FR-M10-10.01, FR-M10-10.03 |
| Bật, tắt tạm dừng đăng ký | ✗ | ✗ | ✗ | ✓ | FR-M10-11.01, FR-M10-11.03 |
| Bật, tắt cờ tính năng | ✗ | ✗ | ✗ | ✓ | FR-M10-12.01, FR-M10-12.02 |
| Đặt, sửa, gỡ banner thông báo toàn trang | ✗ | ✗ | ✗ | ✓ | FR-M10-13.01, FR-M10-13.09, FR-M10-13.02, FR-M10-13.03 |
| Xem, đóng banner thông báo toàn trang | ✓ | ✓ | ✓ | ✓ | FR-M10-13.01, FR-M10-13.07 |
| Dùng Group, Chat, Gamification khi cờ tính năng của module đó tắt | ✗ | ✗ | ✗ | ✓ | FR-M10-12.04, FR-M10-12.08 |
| Xem nhật ký thao tác Admin | ✗ | ✗ | ✗ | ✓ | FR-M10-15.01, FR-M10-15.02 |
| Sửa, xóa mục trong nhật ký thao tác Admin | ✗ | ✗ | ✗ | ✗ | FR-M10-14.04, FR-M10-15.03 |
| Chỉnh hằng số chính sách qua giao diện | ✗ | ✗ | ✗ | ✗ | FR-M10-09.09 |

<!-- Ô nói thẳng: cột Admin các hàng việc Admin (DEC-090 "Admin-only: Role management, System config, full audit log
     view, MOD account management"; DEC-091; DEC-092; DM-10.3); hàng 3, 7, 8 (DEC-221: chỉ ADMIN gốc cấp, thu hồi
     Admin; gốc không bị thu hồi); hàng 4, 5 (DEC-091, DEC-221: người nhận Chấp nhận/Từ chối); hàng 9 (QA-013, DEC-223);
     hàng 15 (DEC-226: hiện cho mọi người kể cả Guest, người xem đóng được); hàng 16 (DEC-225: chặn thao tác người dùng,
     Admin vẫn dùng); hàng 18 (DEC-094); hàng 19 (DEC-090, QA-161). Cột Guest hàng 1 (QA-011 "ADMN: Không").
     Ô suy ra: cột Guest, User, Mod các hàng việc Admin (DEC-090 "Admin-only" ⇒ vai trò khác bị từ chối); cột Guest
     hàng 4, 5, 9 (không có tài khoản ⇒ không có đề xuất, vai trò để từ bỏ).
     "—": đề xuất làm Mod chỉ cho USER, đề xuất làm Admin chỉ cho USER, MODERATOR (DEC-091, DEC-221); User không có vai
     trò để từ chức. -->

### 4.4 Danh sách chức năng

| ID | Chức năng | Tác nhân chính | Kích hoạt |
|---|---|---|---|
| FR-M10-01 | Xem người dùng trong Admin Panel | Admin | Admin mở phần quản lý người dùng của Admin Panel |
| FR-M10-02 | Đề xuất người dùng làm Mod | Admin | Admin chọn "Đề xuất làm Mod" cho một người dùng |
| FR-M10-03 | Trả lời đề xuất làm Mod hoặc làm Admin | User, Mod (người được đề xuất) | Người được đề xuất chọn Chấp nhận hoặc Từ chối trên thông báo đề xuất |
| FR-M10-04 | Giáng cấp Mod | Admin | Admin chọn giáng cấp một Mod |
| FR-M10-05 | Tự từ chức vai trò Mod hoặc Admin | Mod; Admin không phải gốc | Mod hoặc Admin chọn từ chức |
| FR-M10-06 | Thu hồi vai trò Mod khi Mod bị ban | Hệ thống | Một tài khoản có vai trò Mod bị ban (M08) |
| FR-M10-07 | Đề xuất làm Admin | Admin (tài khoản ADMIN gốc) | ADMIN gốc chọn "Đề xuất làm Admin" cho một tài khoản |
| FR-M10-08 | Thu hồi vai trò Admin | Admin (tài khoản ADMIN gốc) | ADMIN gốc chọn thu hồi vai trò Admin của một tài khoản |
| FR-M10-09 | Bật, tắt công tắc AI | Admin | Admin đổi công tắc AI tổng hoặc một công tắc AI riêng |
| FR-M10-10 | Bật, tắt chế độ bảo trì | Admin | Admin đổi công tắc chế độ bảo trì |
| FR-M10-11 | Bật, tắt tạm dừng đăng ký | Admin | Admin đổi công tắc tạm dừng đăng ký |
| FR-M10-12 | Bật, tắt cờ tính năng | Admin | Admin đổi cờ tính năng của Group, Chat hoặc Gamification |
| FR-M10-13 | Đặt, sửa, gỡ banner thông báo toàn trang | Admin | Admin đặt, sửa nội dung banner hoặc gỡ banner đang hiện |
| FR-M10-14 | Ghi nhật ký thao tác Admin | Hệ thống | Admin vừa hoàn tất một thao tác làm đổi dữ liệu, hoặc vai trò của một tài khoản vừa đổi |
| FR-M10-15 | Xem nhật ký thao tác Admin | Admin | Admin mở nhật ký thao tác Admin |

### 4.5 Mốc và ưu tiên

Toàn bộ yêu cầu của module thuộc MS1, ưu tiên **Must** (bảng MoSCoW Summary của module-registry: Must gồm M01–M10, M13;
cột MoSCoW ở dòng M10 của bảng Module List bị lệch nên không dùng). Không có yêu cầu ngoại lệ về ưu tiên.

## 5. Yêu cầu chức năng

### 5.1 FR-M10-01 Xem người dùng trong Admin Panel

**Yêu cầu cấp trên:** Hệ thống phải cho phép Admin tìm, lọc và xem người dùng trong Admin Panel để chọn người cần đổi vai trò và theo dõi thao tác của Mod.

**Lý do:** Admin cần thấy các Mod hiện có và thao tác của họ để quyết định giữ hay giáng cấp; quản lý vai trò và tài khoản Mod chỉ Admin làm.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M10-01.01 | Khi Admin chọn một người dùng trong phần quản lý người dùng, hệ thống phải cho Admin thực hiện các thao tác vai trò áp được cho người đó: đề xuất làm Mod, giáng cấp; với tài khoản ADMIN gốc thêm đề xuất làm Admin, thu hồi vai trò Admin. |
| FR-M10-01.02 | Nếu người chưa đăng nhập hoặc tài khoản không có vai trò ADMIN mở Admin Panel, hệ thống phải từ chối (BR-M10-02). |
| FR-M10-01.03 | Khi Admin tìm người dùng, hệ thống phải tìm theo username hoặc tên hiển thị, khớp như tìm người dùng ở M06 (BR-M10-29). |
| FR-M10-01.04 | Khi Admin lọc theo vai trò USER, MODERATOR hoặc ADMIN, hệ thống phải chỉ hiện người dùng có vai trò đó (BR-M10-29). |
| FR-M10-01.05 | Hệ thống phải hiện ở mỗi người dùng: username, tên hiển thị, vai trò, trạng thái tài khoản; tài khoản ADMIN gốc có nhãn "gốc" (BR-M10-29). |
| FR-M10-01.06 | Khi Admin chọn "Xem thao tác" ở một Mod, hệ thống phải mở nhật ký kiểm duyệt (M08) lọc theo người làm là Mod đó (BR-M10-30). |

### 5.2 FR-M10-02 Đề xuất người dùng làm Mod

**Yêu cầu cấp trên:** Hệ thống phải cho phép Admin gửi đề xuất làm Mod cho một người dùng có vai trò USER mà không cần điều kiện về điểm hay uy tín.

**Lý do:** Admin toàn quyền chọn người làm Mod, không có điều kiện về uy tín hay thâm niên; người được chọn vẫn có quyền từ chối.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M10-02.01 | Khi Admin gửi đề xuất làm Mod cho một người dùng có vai trò USER, hệ thống phải lưu đề xuất ở trạng thái Chưa trả lời kèm thời điểm gửi. |
| FR-M10-02.02 | Khi lưu một đề xuất làm Mod, hệ thống phải gửi cho người được đề xuất thông báo "Đề xuất làm Mod" có hai lựa chọn Chấp nhận và Từ chối (M07). |
| FR-M10-02.03 | Khi Admin gửi đề xuất, hệ thống phải giữ nguyên vai trò của người được đề xuất cho tới khi người đó chọn Chấp nhận (BR-M10-06). |
| FR-M10-02.04 | Hệ thống phải không kiểm điểm, uy tín hay thời gian sử dụng của người được đề xuất (BR-M10-05). |
| FR-M10-02.05 | Khi Admin đề xuất lại cho một người đã từ chối hoặc có đề xuất đã hết hiệu lực, hệ thống phải tạo một đề xuất mới kèm thông báo mới (BR-M10-06). |
| FR-M10-02.06 | Nếu người gửi đề xuất không có vai trò ADMIN, hệ thống phải từ chối đề xuất (BR-M10-02). |
| FR-M10-02.07 | Nếu người nhận đang có vai trò MODERATOR hoặc ADMIN, hệ thống phải từ chối đề xuất làm Mod. |
| FR-M10-02.08 | Khi Admin gửi đề xuất làm Mod cho người đang có một đề xuất làm Mod còn hiệu lực, hệ thống phải chuyển đề xuất cũ sang Hết hiệu lực trước khi lưu đề xuất mới (BR-M10-27). |
| FR-M10-02.09 | Nếu người nhận không ở trạng thái ACTIVE hoặc chưa hoàn tất bước 3 đăng ký, hệ thống phải từ chối đề xuất (BR-M10-05). |
| FR-M10-02.10 | Khi đủ 7 × 24 giờ kể từ thời điểm gửi mà đề xuất làm Mod vẫn Chưa trả lời, hệ thống phải chuyển đề xuất sang Hết hiệu lực để thông báo hiện "Đã hết hạn" (BR-M10-07). |

### 5.3 FR-M10-03 Trả lời đề xuất làm Mod hoặc làm Admin

**Yêu cầu cấp trên:** Hệ thống phải cho phép người được đề xuất chấp nhận hoặc từ chối một đề xuất làm Mod hoặc làm Admin còn hiệu lực, một lần.

**Lý do:** Người được chọn có quyền từ chối; chấp nhận thì có vai trò mới ngay. Đề xuất làm Admin đi theo cùng luồng với đề xuất làm Mod cho đồng nhất.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M10-03.01 | Khi người được đề xuất chọn Chấp nhận trên một đề xuất làm Mod còn hiệu lực, hệ thống phải đổi vai trò của người đó thành MODERATOR ngay (BR-M10-06). |
| FR-M10-03.02 | Khi người được đề xuất chọn Chấp nhận, hệ thống phải chuyển đề xuất sang trạng thái Đã chấp nhận. |
| FR-M10-03.03 | Khi người được đề xuất chọn Từ chối, hệ thống phải giữ nguyên vai trò của người đó và chuyển đề xuất sang trạng thái Đã từ chối (BR-M10-06). |
| FR-M10-03.04 | Khi một đề xuất đã được trả lời, hệ thống phải hiện lựa chọn đã chọn trên đề xuất đó (BR-M10-07). |
| FR-M10-03.05 | (Đã bỏ ở phiên bản 0.1 — đề xuất có hạn 7 ngày, xem FR-M10-03.08) |
| FR-M10-03.06 | Nếu người được đề xuất trả lời một đề xuất đã được trả lời, hệ thống phải từ chối lần trả lời đó (BR-M10-07). |
| FR-M10-03.07 | Nếu một người khác người được đề xuất trả lời đề xuất, hệ thống phải từ chối. |
| FR-M10-03.08 | Nếu người được đề xuất trả lời một đề xuất đã Hết hiệu lực, hệ thống phải từ chối và giữ nguyên vai trò (BR-M10-07, BR-M10-27). |
| FR-M10-03.09 | Khi người được đề xuất chọn Chấp nhận trên một đề xuất làm Admin còn hiệu lực, hệ thống phải đổi vai trò của người đó thành ADMIN ngay (BR-M10-06, BR-M10-11). |
| FR-M10-03.10 | Nếu lúc chọn Chấp nhận vai trò của người đó không còn hợp lệ cho loại đề xuất (đề xuất làm Mod: không còn USER; đề xuất làm Admin: không còn USER hoặc MODERATOR), hệ thống phải từ chối và giữ nguyên vai trò (BR-M10-27). |
| FR-M10-03.11 | Nếu lúc chọn Chấp nhận tài khoản không ở trạng thái ACTIVE, hệ thống phải từ chối (BR-M10-05). |

### 5.4 FR-M10-04 Giáng cấp Mod

**Yêu cầu cấp trên:** Hệ thống phải cho phép Admin đưa một Mod về vai trò USER ngay mà không cần Mod đồng ý.

**Lý do:** Giáng cấp là quản lý vai trò, không phải hình phạt, nên Admin làm trực tiếp và Mod không khiếu nại được.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M10-04.01 | Khi Admin giáng cấp một Mod, hệ thống phải đổi vai trò của người đó thành USER ngay (BR-M10-08). |
| FR-M10-04.02 | Khi Admin giáng cấp một Mod, hệ thống phải không yêu cầu sự đồng ý của Mod đó (BR-M10-08). |
| FR-M10-04.03 | Hệ thống phải không cho khiếu nại việc giáng cấp (BR-M10-08). |
| FR-M10-04.04 | Nếu người thao tác không có vai trò ADMIN, hệ thống phải từ chối giáng cấp (BR-M10-02). |
| FR-M10-04.05 | Nếu tài khoản bị chọn không có vai trò MODERATOR, hệ thống phải từ chối giáng cấp. |

### 5.5 FR-M10-05 Tự từ chức vai trò Mod hoặc Admin

**Yêu cầu cấp trên:** Hệ thống phải cho phép Mod và Admin không phải gốc tự bỏ vai trò của mình để về vai trò USER, sau một bước xác nhận.

**Lý do:** Mod, Admin làm tình nguyện có thể muốn thôi mà không phải nhờ người khác giáng cấp; tự từ chức là một trong ba cách Mod mất vai trò.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M10-05.01 | Khi Mod chọn từ chức và xác nhận, hệ thống phải đổi vai trò của người đó thành USER (BR-M10-25). |
| FR-M10-05.02 | Nếu tài khoản chọn từ chức không có vai trò MODERATOR hoặc ADMIN, hệ thống phải từ chối. |
| FR-M10-05.03 | Khi người dùng chọn từ chức, hệ thống phải hỏi xác nhận một lần trước khi đổi vai trò; người dùng hủy thì giữ nguyên vai trò (BR-M10-25). |
| FR-M10-05.04 | Khi một Admin khác tài khoản ADMIN gốc chọn từ chức và xác nhận, hệ thống phải đổi vai trò của người đó thành USER (BR-M10-25). |
| FR-M10-05.05 | Nếu tài khoản ADMIN gốc chọn từ chức, hệ thống phải từ chối (BR-M10-10). |
| FR-M10-05.06 | Hệ thống phải chỉ trả lại vai trò đã từ chức khi người đó chấp nhận một đề xuất mới (BR-M10-25). |

### 5.6 FR-M10-06 Thu hồi vai trò Mod khi Mod bị ban

**Yêu cầu cấp trên:** Hệ thống phải tự đưa tài khoản Mod bị ban về vai trò USER.

**Lý do:** Tránh lỗi logic giữa vai trò và trạng thái tài khoản: tài khoản bị ban không được giữ vai trò Mod.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M10-06.01 | Khi một tài khoản có vai trò MODERATOR bị ban (M08), hệ thống phải đổi vai trò của tài khoản đó thành USER ngay (BR-M10-09). |
| FR-M10-06.02 | Khi ban của một tài khoản từng là Mod hết hạn hoặc được gỡ (M08), hệ thống phải giữ vai trò USER của tài khoản đó; trường hợp ban bị lật do khiếu nại theo quy định của M09 (BR-M10-09). |

### 5.7 FR-M10-07 Đề xuất làm Admin

**Yêu cầu cấp trên:** Hệ thống phải cho phép tài khoản ADMIN gốc gửi đề xuất làm Admin cho một tài khoản USER hoặc MODERATOR.

**Lý do:** Cho phép bàn giao quyền vận hành linh hoạt mà không cần đội phát triển can thiệp vào dữ liệu; chỉ ADMIN gốc cấp vai trò Admin, theo cùng luồng với đề xuất làm Mod cho đồng nhất.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M10-07.01 | Nếu người thao tác không có vai trò ADMIN, hệ thống phải từ chối đề xuất làm Admin (BR-M10-02). |
| FR-M10-07.02 | Nếu tài khoản được chọn đã có vai trò ADMIN, hệ thống phải từ chối đề xuất làm Admin. |
| FR-M10-07.03 | Trong khi một tài khoản có vai trò ADMIN, hệ thống phải cho tài khoản đó mọi quyền của Mod mà không cần vai trò MODERATOR, và là vai trò duy nhất làm được các việc chỉ Admin làm ở module khác (BR-M10-01, BR-M10-03). |
| FR-M10-07.04 | Hệ thống phải có sẵn một tài khoản ADMIN gốc khi khởi tạo, không tạo qua đăng ký (BR-M10-10). |
| FR-M10-07.05 | Khi tài khoản ADMIN gốc gửi đề xuất làm Admin cho một tài khoản USER hoặc MODERATOR, hệ thống phải lưu đề xuất ở trạng thái Chưa trả lời kèm thời điểm gửi (BR-M10-11). |
| FR-M10-07.06 | Khi lưu một đề xuất làm Admin, hệ thống phải gửi cho người được đề xuất thông báo "Đề xuất làm Admin" có hai lựa chọn Chấp nhận và Từ chối (M07). |
| FR-M10-07.07 | Nếu người gửi có vai trò ADMIN nhưng khác tài khoản ADMIN gốc, hệ thống phải từ chối đề xuất làm Admin (BR-M10-11). |
| FR-M10-07.08 | Nếu người nhận không ở trạng thái ACTIVE hoặc chưa hoàn tất bước 3 đăng ký, hệ thống phải từ chối đề xuất làm Admin (BR-M10-05). |
| FR-M10-07.09 | Khi ADMIN gốc gửi đề xuất làm Admin cho người đang có một đề xuất làm Admin còn hiệu lực, hệ thống phải chuyển đề xuất cũ sang Hết hiệu lực trước khi lưu đề xuất mới (BR-M10-27). |
| FR-M10-07.10 | Khi đủ 7 × 24 giờ kể từ thời điểm gửi mà đề xuất làm Admin vẫn Chưa trả lời, hệ thống phải chuyển đề xuất sang Hết hiệu lực để thông báo hiện "Đã hết hạn" (BR-M10-07). |
| FR-M10-07.11 | Khi ADMIN gốc gửi đề xuất làm Admin, hệ thống phải giữ nguyên vai trò của người được đề xuất cho tới khi người đó chọn Chấp nhận (BR-M10-06). |

### 5.8 FR-M10-08 Thu hồi vai trò Admin

**Yêu cầu cấp trên:** Hệ thống phải cho phép tài khoản ADMIN gốc thu hồi vai trò ADMIN của một tài khoản Admin khác, đưa tài khoản đó về USER ngay.

**Lý do:** Cho phép bàn giao và thu lại quyền vận hành mà không cần đội phát triển can thiệp vào dữ liệu; chỉ ADMIN gốc làm, theo cùng cách với giáng cấp Mod.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M10-08.01 | Nếu người thao tác không có vai trò ADMIN, hệ thống phải từ chối thu hồi vai trò Admin (BR-M10-02). |
| FR-M10-08.02 | Nếu tài khoản được chọn không có vai trò ADMIN, hệ thống phải từ chối thu hồi. |
| FR-M10-08.03 | Khi ADMIN gốc thu hồi vai trò Admin của một tài khoản, hệ thống phải đổi vai trò của tài khoản đó thành USER ngay, không cần tài khoản đó đồng ý (BR-M10-11). |
| FR-M10-08.04 | Nếu tài khoản bị chọn là tài khoản ADMIN gốc, hệ thống phải từ chối thu hồi (BR-M10-10). |
| FR-M10-08.05 | Nếu người thao tác có vai trò ADMIN nhưng khác tài khoản ADMIN gốc, hệ thống phải từ chối thu hồi (BR-M10-11). |
| FR-M10-08.06 | Hệ thống phải không cho khiếu nại việc thu hồi vai trò Admin (BR-M10-11). |

### 5.9 FR-M10-09 Bật, tắt công tắc AI

**Yêu cầu cấp trên:** Hệ thống phải cho phép Admin bật, tắt công tắc AI tổng và ba công tắc AI riêng (Search, Moderation, Topic suggestion) lúc hệ thống đang chạy.

**Lý do:** Tắt AI có kiểm soát mà hệ thống vẫn chạy nhờ cách dự phòng của từng module; công tắc lưu bền để đổi lúc đang chạy, không cần triển khai lại.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M10-09.01 | Hệ thống phải có công tắc AI tổng và ba công tắc AI riêng Search, Moderation, Topic suggestion, mỗi công tắc ở trạng thái Bật hoặc Tắt (BR-M10-12, BR-M10-15). |
| FR-M10-09.02 | Khi Admin đổi một công tắc AI, hệ thống phải lưu trạng thái mới và áp dụng cho mọi thao tác sau thời điểm đổi mà không cần triển khai lại (BR-M10-13). |
| FR-M10-09.03 | Trong khi công tắc AI tổng tắt, hệ thống phải coi mọi tính năng AI là tắt, bất kể trạng thái của công tắc riêng (BR-M10-14). |
| FR-M10-09.04 | Trong khi công tắc AI tổng bật, hệ thống phải coi một tính năng AI có công tắc riêng là bật khi và chỉ khi công tắc riêng của nó bật (BR-M10-14, BR-M10-15). |
| FR-M10-09.05 | Hệ thống phải không có công tắc riêng cho tóm tắt AI; tóm tắt chỉ theo công tắc AI tổng (BR-M10-15). |
| FR-M10-09.06 | Khi Admin đổi công tắc AI riêng trong lúc công tắc AI tổng tắt, hệ thống phải lưu trạng thái công tắc riêng và áp dụng nó khi công tắc tổng được bật lại. |
| FR-M10-09.07 | Trong khi một công tắc AI tắt, hệ thống phải để các module dùng cách dự phòng của mình như một trạng thái có chủ đích, không coi là AI lỗi (BR-M10-16). |
| FR-M10-09.08 | Nếu người thao tác không có vai trò ADMIN, hệ thống phải từ chối đổi công tắc AI (BR-M10-02). |
| FR-M10-09.09 | Hệ thống phải không có mục nào trong Admin Panel để đổi hằng số chính sách: thời hạn cảnh cáo, ban, ngưỡng AI, trọng số mức nghiêm trọng, thời gian chờ của AI, hạn của đề xuất, nội dung và phiên bản trang chính sách (BR-M10-04). |
| FR-M10-09.10 | Khi khởi tạo hệ thống, hệ thống phải đặt công tắc AI tổng và ba công tắc AI riêng ở trạng thái Bật (BR-M10-26). |

### 5.10 FR-M10-10 Bật, tắt chế độ bảo trì

**Yêu cầu cấp trên:** Hệ thống phải cho phép Admin bật, tắt chế độ bảo trì; trong khi bật, chỉ tài khoản ADMIN dùng được hệ thống.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M10-10.01 | Khi Admin bật hoặc tắt chế độ bảo trì, hệ thống phải lưu trạng thái mới và áp dụng cho mọi thao tác sau thời điểm đổi (BR-M10-13). |
| FR-M10-10.02 | Trong khi chế độ bảo trì bật, hệ thống phải cung cấp trạng thái này cho M01 để chỉ tài khoản ADMIN đăng nhập và thao tác được, tài khoản khác bị từ chối kể cả phiên đang có (BR-M10-17). |
| FR-M10-10.03 | Nếu người thao tác không có vai trò ADMIN, hệ thống phải từ chối đổi chế độ bảo trì (BR-M10-02). |
| FR-M10-10.04 | Khi khởi tạo hệ thống, hệ thống phải đặt chế độ bảo trì ở trạng thái Tắt (BR-M10-26). |

### 5.11 FR-M10-11 Bật, tắt tạm dừng đăng ký

**Yêu cầu cấp trên:** Hệ thống phải cho phép Admin bật, tắt tạm dừng đăng ký; trong khi bật, hệ thống không nhận tài khoản mới.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M10-11.01 | Khi Admin bật hoặc tắt tạm dừng đăng ký, hệ thống phải lưu trạng thái mới và áp dụng cho mọi thao tác sau thời điểm đổi (BR-M10-13). |
| FR-M10-11.02 | Trong khi tạm dừng đăng ký bật, hệ thống phải cung cấp trạng thái này cho M01 để từ chối tạo tài khoản mới bằng email hoặc đăng nhập Google lần đầu, vẫn cho liên kết Google vào tài khoản có sẵn và cho tài khoản đã xong bước 1 làm tiếp (BR-M10-18). |
| FR-M10-11.03 | Nếu người thao tác không có vai trò ADMIN, hệ thống phải từ chối đổi tạm dừng đăng ký (BR-M10-02). |
| FR-M10-11.04 | Khi khởi tạo hệ thống, hệ thống phải đặt tạm dừng đăng ký ở trạng thái Tắt (BR-M10-26). |

### 5.12 FR-M10-12 Bật, tắt cờ tính năng

**Yêu cầu cấp trên:** Hệ thống phải cho phép Admin bật, tắt cờ tính năng của Group, Chat, Gamification; khi một cờ tắt, hệ thống chặn thao tác của người dùng với module đó mà vẫn chạy các việc tự làm của module.

**Lý do:** Cho Admin tạm dừng một module không thuộc lõi (ví dụ tắt Chat khi bị lạm dụng, vì MS1 chưa có chặn, báo cáo tin nhắn) mà không làm mất dữ liệu hay dừng phần hệ thống tự chạy.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M10-12.01 | Khi Admin bật hoặc tắt cờ tính năng của Group, Chat hoặc Gamification, hệ thống phải lưu trạng thái mới và áp dụng cho mọi thao tác sau thời điểm đổi (BR-M10-13, BR-M10-19). |
| FR-M10-12.02 | Nếu người thao tác không có vai trò ADMIN, hệ thống phải từ chối đổi cờ tính năng (BR-M10-02). |
| FR-M10-12.03 | Hệ thống phải có cờ tính năng cho đúng ba module Group (M11), Chat (M16), Gamification (M12), không có cờ cho module khác (BR-M10-19). |
| FR-M10-12.04 | Trong khi cờ tính năng của một module tắt, nếu người dùng không có vai trò ADMIN gửi một thao tác tới module đó, hệ thống phải từ chối và hiện "Hệ thống đang bận, vui lòng thử lại sau" (BR-M10-28). |
| FR-M10-12.05 | Trong khi cờ tính năng của một module tắt, hệ thống phải vẫn hiện lối vào module đó (BR-M10-28). |
| FR-M10-12.06 | Trong khi cờ tính năng của một module tắt, hệ thống phải vẫn chạy các việc hệ thống tự làm của module đó và kiểm duyệt (M08) liên quan tới module đó (BR-M10-28). |
| FR-M10-12.07 | Khi cờ tính năng của một module tắt rồi bật lại, hệ thống phải giữ nguyên dữ liệu của module, không xóa, không sửa do việc tắt, và không tính bù cho khoảng thời gian đã tắt (BR-M10-28). |
| FR-M10-12.08 | Trong khi cờ tính năng của một module tắt, hệ thống phải cho tài khoản ADMIN dùng module đó như khi cờ bật (BR-M10-28). |
| FR-M10-12.09 | Khi khởi tạo hệ thống, hệ thống phải đặt ba cờ tính năng ở trạng thái Bật (BR-M10-26). |

Danh sách chi tiết thao tác bị chặn và việc chạy ngầm của từng module: xem TBD-M10-01.

### 5.13 FR-M10-13 Đặt, sửa, gỡ banner thông báo toàn trang

**Yêu cầu cấp trên:** Hệ thống phải cho phép Admin đặt, sửa và gỡ một banner thông báo văn bản hiện trên mọi trang, và cho người xem đóng banner.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M10-13.01 | Khi Admin đặt banner thông báo, hệ thống phải hiện banner trên mọi trang cho mọi người xem, kể cả người chưa đăng nhập (BR-M10-20). |
| FR-M10-13.02 | Khi Admin gỡ banner thông báo, hệ thống phải thôi hiện banner trên mọi trang. |
| FR-M10-13.03 | Nếu người thao tác không có vai trò ADMIN, hệ thống phải từ chối đặt, sửa hoặc gỡ banner (BR-M10-02). |
| FR-M10-13.04 | Khi Admin đặt banner mới trong lúc đang có banner hiện, hệ thống phải thay banner đang hiện bằng banner mới (BR-M10-20). |
| FR-M10-13.05 | Nếu nội dung banner trống hoặc dài hơn 200 ký tự (tính sau khi bỏ khoảng trắng ở đầu và cuối), hệ thống phải từ chối (BR-M10-20). |
| FR-M10-13.06 | Hệ thống phải hiện nội dung banner dưới dạng văn bản thuần (BR-M10-20). |
| FR-M10-13.07 | Khi người xem đóng banner, hệ thống phải không hiện banner đó với người xem ấy nữa (BR-M10-20). |
| FR-M10-13.08 | Khi Admin sửa nội dung banner hoặc đặt banner mới, hệ thống phải hiện banner lại với mọi người, kể cả người đã đóng (BR-M10-20). |
| FR-M10-13.09 | Khi Admin sửa nội dung banner đang hiện, hệ thống phải thay nội dung banner trên mọi trang (BR-M10-20). |
| FR-M10-13.10 | Khi khởi tạo hệ thống, hệ thống phải không có banner nào (BR-M10-26). |

### 5.14 FR-M10-14 Ghi nhật ký thao tác Admin

**Yêu cầu cấp trên:** Hệ thống phải ghi mọi thao tác làm đổi dữ liệu của Admin và mọi thay đổi vai trò vào nhật ký thao tác Admin chỉ ghi thêm.

**Lý do:** Bảo đảm minh bạch, kể cả với chính thao tác của Admin; mọi lần một tài khoản đổi vai trò đều truy được ở một chỗ.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M10-14.01 | Khi Admin hoàn tất một thao tác làm đổi dữ liệu với vai trò Admin, hệ thống phải ghi một mục vào nhật ký thao tác Admin gồm người làm, thao tác, đối tượng, lý do và thời điểm (BR-M10-21, BR-M10-23). |
| FR-M10-14.02 | Hệ thống phải ghi vào nhật ký thao tác Admin: gửi đề xuất làm Mod, làm Admin; giáng cấp Mod; thu hồi vai trò Admin; đổi mỗi công tắc cấu hình; đặt, sửa, gỡ banner; cảnh cáo, bỏ cảnh cáo AI, ban, gỡ ban, ẩn nội dung, ẩn, khóa, mở khóa nhóm, kết luận vụ báo cáo, kết luận khiếu nại; thêm, gộp, xóa Topic; vô hiệu hóa, kích hoạt lại Tag; đổi Topic, Tag trên bài người khác (BR-M10-21). |
| FR-M10-14.03 | Khi Admin làm một thao tác kiểm duyệt hoặc thao tác Tag, Topic, hệ thống phải ghi mục ở nhật ký thao tác Admin dù thao tác đó cũng được ghi ở nhật ký kiểm duyệt (M08) (BR-M10-24). |
| FR-M10-14.04 | Hệ thống phải không cho sửa hoặc xóa một mục nhật ký thao tác Admin đã ghi, và giữ các mục vĩnh viễn (BR-M10-22). |
| FR-M10-14.05 | Hệ thống phải không ghi quyết định của AI vào nhật ký thao tác Admin; quyết định AI thuộc nhật ký quyết định AI (M13) (BR-M10-24). |
| FR-M10-14.06 | Khi người được đề xuất chấp nhận một đề xuất, hoặc Mod, Admin tự từ chức, hệ thống phải ghi một mục với người làm là chính người đó (BR-M10-21). |
| FR-M10-14.07 | Khi một Mod mất vai trò do bị ban, hệ thống phải ghi một mục với người làm là "Hệ thống" (BR-M10-21). |
| FR-M10-14.08 | Hệ thống phải không ghi vào nhật ký thao tác Admin: việc xem trang; việc nhận, nhả vụ báo cáo hay khiếu nại; thao tác Admin làm như người dùng thường (đăng bài, bình luận, Star) (BR-M10-21). |
| FR-M10-14.09 | Hệ thống phải để lý do của mục nhật ký là tùy chọn; với thao tác mà module gốc bắt buộc lý do, mục nhật ký lấy đúng lý do đó (BR-M10-23). |

### 5.15 FR-M10-15 Xem nhật ký thao tác Admin

**Yêu cầu cấp trên:** Hệ thống phải cho phép Admin xem, lọc nhật ký thao tác Admin nhưng không sửa, không xóa.

**Lý do:** Bảo đảm minh bạch, kể cả với chính thao tác của Admin.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M10-15.01 | Khi Admin mở nhật ký thao tác Admin, hệ thống phải hiện các mục với người làm, thao tác, đối tượng, lý do và thời điểm theo giờ Việt Nam (BR-M10-23). |
| FR-M10-15.02 | Nếu người mở nhật ký không có vai trò ADMIN, hệ thống phải từ chối (BR-M10-02). |
| FR-M10-15.03 | Nếu bất kỳ ai, kể cả Admin, sửa hoặc xóa một mục nhật ký thao tác Admin, hệ thống phải từ chối (BR-M10-22). |
| FR-M10-15.04 | Khi Admin mở nhật ký thao tác Admin, hệ thống phải hiện mục mới nhất trước (BR-M10-23). |
| FR-M10-15.05 | Khi Admin lọc nhật ký theo người làm hoặc theo loại thao tác, hệ thống phải chỉ hiện các mục khớp (BR-M10-23). |

### 5.16 Quy tắc nghiệp vụ

| ID | Loại | Quy tắc | Ví dụ |
|---|---|---|---|
| BR-M10-01 | Sự kiện | Hệ thống có ba vai trò USER, MODERATOR, ADMIN. Mỗi tài khoản có đúng một vai trò, theo thứ bậc USER < MODERATOR < ADMIN; vai trò cao hơn có mọi quyền của vai trò thấp hơn. | Một tài khoản ADMIN mở được hàng chờ báo cáo như Mod mà không cần thêm vai trò MODERATOR. |
| BR-M10-02 | Ràng buộc | Chỉ tài khoản ADMIN vào được Admin Panel và làm các việc: quản lý vai trò, cấu hình hệ thống, xem toàn bộ nhật ký, quản lý tài khoản Mod. | — |
| BR-M10-03 | Sự kiện | Việc dùng chung giữa Mod và Admin (xử lý báo cáo, cảnh cáo, ban, khiếu nại; xóa mềm Tag) thuộc module khác, với các ngoại lệ chỉ Admin làm: thêm, gộp, xóa Topic (M05); cảnh cáo, ban Mod và xử lý vụ, khiếu nại về Mod (M08, M09). | — |
| BR-M10-04 | Ràng buộc | Hằng số chính sách không chỉnh được qua Admin Panel; chỉ đổi qua triển khai. Gồm: thời hạn cảnh cáo, ban; ngưỡng AI; trọng số mức nghiêm trọng của báo cáo; thời gian chờ của AI; hạn của đề xuất; nội dung và phiên bản trang chính sách. | Admin Panel không có ô nào để đổi ngưỡng 0,9 của quét AI hay hạn 7 ngày của đề xuất; muốn đổi thì đội phát triển sửa và triển khai lại. |
| BR-M10-05 | Ràng buộc | Đề xuất làm Mod, làm Admin không có điều kiện về điểm, uy tín hay thời gian dùng. Đề xuất chỉ gửi được cho tài khoản ACTIVE đã hoàn tất bước 3 đăng ký; người nhận chấp nhận cũng phải đang ACTIVE. | Tài khoản USER vừa hoàn tất bước 3, 0 điểm → được đề xuất. Tài khoản DEACTIVATED, BANNED, hoặc mới xong bước 1 → bị từ chối. |
| BR-M10-06 | Kích hoạt | Người được đề xuất chọn Chấp nhận trên một đề xuất còn hiệu lực thì vai trò chuyển ngay sang MODERATOR (đề xuất làm Mod) hoặc ADMIN (đề xuất làm Admin); chọn Từ chối thì vai trò không đổi. Người gửi có thể gửi đề xuất mới cho người đã từ chối. | B từ chối đề xuất làm Mod lúc 09:00 ngày 02/11 → B vẫn là USER; 03/11 Admin gửi đề xuất mới, B chấp nhận → MODERATOR ngay. |
| BR-M10-07 | Ràng buộc | Mỗi đề xuất chỉ trả lời được một lần; sau khi trả lời, đề xuất hiện lựa chọn đã chọn. Đề xuất có hạn 7 ngày, tính bằng 7 × 24 giờ từ thời điểm gửi; quá hạn mà chưa trả lời thì đề xuất Hết hiệu lực, hiện "Đã hết hạn", không trả lời được nữa, vai trò không đổi. | Gửi 09:00:00 ngày 01/11 → chấp nhận lúc 08:59:59 ngày 08/11 thì được; lúc 09:00:00 ngày 08/11 thì đã hết hạn, bị từ chối. Đã bấm Từ chối thì không bấm Chấp nhận trên chính đề xuất đó được nữa. |
| BR-M10-08 | Ràng buộc | Giáng cấp do Admin làm trực tiếp, có hiệu lực ngay, đưa Mod về vai trò USER; không cần Mod đồng ý; Mod không khiếu nại được vì đây không phải hình phạt. | — |
| BR-M10-09 | Kích hoạt | Khi một tài khoản MODERATOR bị ban, vai trò chuyển về USER ngay. Ban đó sau này bị gỡ, hết hạn hay bị lật do khiếu nại thì vai trò Mod cũng không được trả lại; Admin muốn thì gửi đề xuất mới. | Mod A bị Admin ban 30 ngày lúc 10:00 ngày 01/11 → A là USER từ 10:00 ngày 01/11. Ngày 05/11 khiếu nại ban của A được chấp nhận → A về hoạt động với vai trò USER. |
| BR-M10-10 | Sự kiện | Tài khoản ADMIN gốc do đội phát triển tạo sẵn khi khởi tạo hệ thống, không qua đăng ký; đội phát triển giữ thông tin đăng nhập. Tài khoản này mang vai trò ADMIN, được đánh dấu "gốc" (không phải vai trò thứ tư), không bị ai thu hồi vai trò và không tự từ chức; vì vậy hệ thống luôn có ít nhất một Admin. | Admin T thu hồi vai trò của ADMIN gốc R → bị từ chối. R bấm từ chức → bị từ chối. |
| BR-M10-11 | Ràng buộc | Chỉ tài khoản ADMIN gốc cấp và thu hồi vai trò ADMIN. Cấp qua đề xuất làm Admin gửi cho tài khoản USER hoặc MODERATOR, người nhận chấp nhận; thu hồi làm trực tiếp, ngay, không cần đồng ý, không khiếu nại, tài khoản về USER. | R (gốc) gửi đề xuất làm Admin cho giáo viên T (USER), T chấp nhận → ADMIN. T gửi đề xuất làm Admin cho U → bị từ chối. R thu hồi T → T về USER, kể cả khi trước đó T từng là Mod. |
| BR-M10-12 | Sự kiện | Cấu hình hệ thống gồm đúng năm mục: công tắc AI (tổng và riêng), chế độ bảo trì, tạm dừng đăng ký, cờ tính năng, banner thông báo toàn trang. Không có công tắc dịch vụ email. | — |
| BR-M10-13 | Ràng buộc | Thay đổi cấu hình được lưu lại và áp dụng cho mọi thao tác xảy ra sau thời điểm đổi, không cần triển khai lại. | Admin tắt công tắc Search lúc 08:00:00; một tìm kiếm gửi lúc 08:00:05 dùng full-text; tìm kiếm gửi lúc 07:59:55 vẫn là tìm ngữ nghĩa. |
| BR-M10-14 | Suy diễn | Một tính năng AI có công tắc riêng chỉ chạy khi cả công tắc AI tổng và công tắc riêng của nó đều bật. Công tắc tổng tắt thì mọi tính năng AI tắt, bất kể công tắc riêng. | Tổng bật, Search bật → tìm ngữ nghĩa. Tổng bật, Search tắt → full-text. Tổng tắt, Search bật → full-text. Tổng tắt, Search tắt → full-text. |
| BR-M10-15 | Sự kiện | Phạm vi của ba công tắc AI riêng: Search — tạo embedding bài và embedding truy vấn (M06, M13); Moderation — quét bài trước khi đăng, quét bình luận tự động, tự cảnh cáo (M03, M04, M08); Topic suggestion — gợi ý Topic (M05). Tóm tắt AI không có công tắc riêng, chỉ theo công tắc tổng. | Tổng bật, Moderation tắt, Topic suggestion bật → bài đăng không qua quét AI nhưng nút gợi ý Topic vẫn dùng được. |
| BR-M10-16 | Suy diễn | Tắt công tắc AI là trạng thái có chủ đích: mỗi module dùng cách dự phòng của mình (M05 chọn Topic thủ công, M06 full-text, M03/M04/M08 không quét, chỉ dựa vào báo cáo), khác với xử lý AI lỗi tạm thời. Bài đăng khi Search tắt được tạo embedding bù sau khi công tắc bật lại. | Admin tắt Search lúc 08:00; bài P đăng lúc 08:30 không có embedding; Admin bật lại lúc 10:00 → P vào hàng tạo bù. |
| BR-M10-17 | Kích hoạt | Trong khi chế độ bảo trì bật, chỉ tài khoản ADMIN đăng nhập được; người khác bị từ chối và phiên đang có của họ không dùng được (M01 thi hành). | Bảo trì bật lúc 22:00; User C đang đăng nhập từ 21:00 → từ 22:00 thao tác của C bị từ chối; Admin D đăng nhập lúc 22:10 được. |
| BR-M10-18 | Kích hoạt | Trong khi tạm dừng đăng ký bật, không tạo được tài khoản mới bằng email hay bằng đăng nhập Google lần đầu; liên kết Google vào tài khoản có sẵn vẫn được; tài khoản đã xong bước 1 vẫn làm tiếp bước 2, 3 (M01 thi hành). | E xong bước 1 lúc 09:00, tạm dừng bật lúc 09:05 → E vẫn hoàn tất bước 2, 3 lúc 09:10. F bắt đầu đăng ký lúc 09:06 → bị từ chối. |
| BR-M10-19 | Sự kiện | Có cờ tính năng cho đúng ba module: Group (M11), Chat (M16), Gamification (M12). Module khác không có cờ: module Must là lõi hoặc đã có công tắc riêng (bảo trì, tạm dừng đăng ký, AI); Feed & Discovery (M14) là trang chủ; Analytics & Stats (M15) chỉ Admin xem. Tạm dừng đăng ký là mục cấu hình riêng, không phải cờ tính năng. | — |
| BR-M10-20 | Ràng buộc | Có tối đa một banner tại một thời điểm, nội dung văn bản thuần dài 1–200 ký tự (đếm sau khi bỏ khoảng trắng ở đầu và cuối). Banner hiện trên mọi trang cho mọi người, kể cả Guest. Người xem đóng được banner; banner đã đóng hiện lại khi Admin sửa nội dung hoặc đặt banner mới. Với Guest, việc đã đóng banner chỉ có tác dụng trên trình duyệt đã đóng. | Nội dung 200 ký tự → nhận; 201 ký tự → từ chối; chỉ gồm khoảng trắng → từ chối. G đóng banner lúc 10:00; Admin sửa nội dung lúc 11:00 → G thấy banner lại. |
| BR-M10-21 | Sự kiện | Nhật ký thao tác Admin ghi mọi thao tác làm đổi dữ liệu do Admin làm với vai trò Admin (vai trò, cấu hình, banner, kiểm duyệt, khiếu nại, danh mục Topic, Tag) và mọi thay đổi vai trò không do Admin làm (chấp nhận đề xuất, tự từ chức: người làm là chính người đó; mất vai trò Mod do bị ban: người làm là "Hệ thống"). Không ghi việc xem, việc nhận hoặc nhả vụ, khiếu nại, và việc Admin làm như người dùng thường. | Admin R gửi đề xuất làm Mod cho K → mục "R — gửi đề xuất làm Mod — K"; K chấp nhận → mục "K — chấp nhận đề xuất làm Mod". Admin T ban Mod M → mục ban của T và mục "Hệ thống — thu hồi vai trò Mod — M". T nhận một vụ, T đăng một bài → không ghi. |
| BR-M10-22 | Ràng buộc | Nhật ký thao tác Admin chỉ ghi thêm: không ai, kể cả Admin, sửa hoặc xóa được một mục; nhật ký giữ vĩnh viễn. | — |
| BR-M10-23 | Sự kiện | Mỗi mục nhật ký thao tác Admin gồm: người làm, thao tác, đối tượng, lý do (tùy chọn; lấy lý do bắt buộc của module gốc nếu có), thời điểm. Thời điểm hiển thị theo giờ Việt Nam. Nhật ký hiện mục mới nhất trước, lọc được theo người làm và theo loại thao tác. | Thao tác lúc 17:30:00 UTC ngày 01/11 hiển thị 00:30:00 ngày 02/11, nằm trên thao tác lúc 17:29:00 UTC cùng ngày. |
| BR-M10-24 | Sự kiện | Thao tác kiểm duyệt của Admin được ghi ở cả nhật ký thao tác Admin và nhật ký kiểm duyệt (M08). Nhật ký quyết định AI (M13) là nhật ký riêng, không thuộc nhật ký thao tác Admin. | Admin ban user G → một mục ở nhật ký thao tác Admin và một mục ở nhật ký kiểm duyệt. |
| BR-M10-25 | Ràng buộc | Mod và Admin không phải gốc tự từ chức được và về USER; hệ thống hỏi xác nhận một lần trước khi đổi vai trò. Muốn có lại vai trò thì phải chấp nhận một đề xuất mới. | Mod M bấm Từ chức rồi hủy ở bước xác nhận → vẫn là Mod. M xác nhận → USER ngay; muốn làm Mod lại phải chờ Admin gửi đề xuất mới. |
| BR-M10-26 | Sự kiện | Giá trị cấu hình lúc khởi tạo hệ thống: công tắc AI tổng và ba công tắc AI riêng Bật; chế độ bảo trì và tạm dừng đăng ký Tắt; ba cờ tính năng Bật; không có banner. | — |
| BR-M10-27 | Ràng buộc | Mỗi người có tối đa một đề xuất còn hiệu lực cho mỗi loại; gửi đề xuất mới cùng loại thì đề xuất cũ Hết hiệu lực. Chấp nhận chỉ có tác dụng khi vai trò lúc bấm còn hợp lệ: USER với đề xuất làm Mod; USER hoặc MODERATOR với đề xuất làm Admin. | Admin gửi đề xuất làm Mod lúc 09:00 ngày 01/11 rồi gửi lại lúc 09:00 ngày 03/11 → đề xuất ngày 01/11 Hết hiệu lực; đề xuất ngày 03/11 chấp nhận được tới trước 09:00 ngày 10/11. MOD nhận đề xuất làm Admin, bị giáng về USER rồi chấp nhận → thành ADMIN. |
| BR-M10-28 | Suy diễn | Trong khi cờ tính năng của một module tắt: mọi thao tác của người dùng không phải Admin với module đó bị từ chối và hiện "Hệ thống đang bận, vui lòng thử lại sau"; lối vào vẫn hiện; việc hệ thống tự làm của module và kiểm duyệt (M08) vẫn chạy; dữ liệu không bị xóa, sửa do việc tắt; bật lại không tính bù; Admin vẫn dùng module. Danh sách chi tiết thuộc FR của M11, M12, M16. | Admin tắt Gamification lúc 08:00 thứ Hai; A được 3 Star lúc 09:00 → điểm của A vẫn tăng 6; A mở bảng xếp hạng → thông báo bận; bật lại lúc 17:00 → A thấy điểm đã có 6 điểm đó. |
| BR-M10-29 | Sự kiện | Admin tìm người dùng theo username hoặc tên hiển thị (khớp như tìm người dùng ở M06), lọc theo vai trò; mỗi người dùng hiện username, tên hiển thị, vai trò, trạng thái tài khoản; tài khoản ADMIN gốc có nhãn "gốc". | — |
| BR-M10-30 | Sự kiện | Admin theo dõi "hiệu suất" của Mod bằng nhật ký kiểm duyệt (M08) lọc theo Mod đó; không có màn hình hay chỉ số hiệu suất riêng. Thu hồi vai trò Mod là giáng cấp. | Admin lọc vai trò Mod, chọn Mod M, bấm "Xem thao tác" → nhật ký kiểm duyệt chỉ hiện thao tác của M. |

### 5.17 Dữ liệu nghiệp vụ

| Thực thể | Thuộc tính nguồn đã nêu | Quan hệ |
|---|---|---|
| Tài khoản (M01) | Vai trò (USER, MODERATOR, ADMIN); dấu "gốc" (chỉ tài khoản ADMIN gốc) — phần M10 quản lý | Nhận đề xuất; là người làm hoặc đối tượng trong nhật ký thao tác Admin |
| Đề xuất | Loại (làm Mod, làm Admin); người được đề xuất; người gửi; thời điểm gửi; trạng thái (Chưa trả lời, Đã chấp nhận, Đã từ chối, Hết hiệu lực) | Một tài khoản có nhiều đề xuất theo thời gian, tối đa một đề xuất còn hiệu lực cho mỗi loại; mỗi đề xuất có một thông báo (M07) |
| Cấu hình hệ thống | Công tắc AI tổng; công tắc AI riêng Search, Moderation, Topic suggestion; chế độ bảo trì; tạm dừng đăng ký; cờ tính năng Group, Chat, Gamification (mỗi công tắc Bật hoặc Tắt); banner thông báo toàn trang (nội dung 1–200 ký tự, Đang hiện hoặc Không hiện, những người xem đã đóng banner hiện tại) | Được M01, M03, M04, M05, M06, M08, M11, M12, M13, M16 đọc |
| Mục nhật ký thao tác Admin | Người làm (tài khoản hoặc "Hệ thống"); thao tác; đối tượng; lý do (tùy chọn); thời điểm | Người làm là một tài khoản hoặc "Hệ thống" |

**Ma trận CRUD:**

| Thực thể | Tạo | Đọc | Sửa | Xóa |
|---|---|---|---|---|
| Tài khoản (M01) | M01 (vai trò USER); tài khoản ADMIN gốc: FR-M10-07.04 | FR-M10-01.03, FR-M10-01.04, FR-M10-01.05 | Vai trò: FR-M10-03.01, FR-M10-03.09, FR-M10-04.01, FR-M10-05.01, FR-M10-05.04, FR-M10-06.01, FR-M10-08.03 | M01 |
| Đề xuất | FR-M10-02.01, FR-M10-07.05 | M07 (thông báo); FR-M10-03.04 | Trả lời: FR-M10-03.02, FR-M10-03.03; hết hiệu lực: FR-M10-02.08, FR-M10-02.10, FR-M10-07.09, FR-M10-07.10 | Không có (BR-M10-07: hết hạn thì chuyển trạng thái, không xóa) |
| Cấu hình hệ thống | Khởi tạo: FR-M10-09.10, FR-M10-10.04, FR-M10-11.04, FR-M10-12.09, FR-M10-13.10 | FR-M10-09.03, FR-M10-09.04, FR-M10-10.02, FR-M10-11.02, FR-M10-12.04, FR-M10-13.01; M01, M03, M04, M05, M06, M08, M11, M12, M13, M16 | FR-M10-09.02, FR-M10-10.01, FR-M10-11.01, FR-M10-12.01, FR-M10-13.01, FR-M10-13.02, FR-M10-13.07, FR-M10-13.09 | Không có (BR-M10-12) |
| Mục nhật ký thao tác Admin | FR-M10-14.01, FR-M10-14.06, FR-M10-14.07 | FR-M10-15.01 | Không có (FR-M10-14.04) | Không có (FR-M10-14.04) |

### 5.18 Chuyển trạng thái

#### Vai trò của tài khoản

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Người dùng tạo tài khoản (M01) | — | USER | M01 |
| (bắt đầu) | Đội phát triển khởi tạo hệ thống | Tài khoản ADMIN gốc (BR-M10-10) | ADMIN | FR-M10-07.04 |
| USER | Người được đề xuất chấp nhận đề xuất làm Mod | Đề xuất còn hiệu lực; tài khoản ACTIVE (BR-M10-05, BR-M10-27) | MODERATOR | FR-M10-03.01 |
| USER | Người được đề xuất chấp nhận đề xuất làm Admin | Đề xuất còn hiệu lực; tài khoản ACTIVE | ADMIN | FR-M10-03.09 |
| MODERATOR | Người được đề xuất chấp nhận đề xuất làm Admin | Đề xuất còn hiệu lực; tài khoản ACTIVE | ADMIN | FR-M10-03.09 |
| MODERATOR | Admin giáng cấp | — | USER | FR-M10-04.01 |
| MODERATOR | Mod tự từ chức | Đã xác nhận (BR-M10-25) | USER | FR-M10-05.01 |
| MODERATOR | Tài khoản bị ban (M08) | — | USER | FR-M10-06.01 |
| ADMIN | ADMIN gốc thu hồi vai trò Admin | Không phải tài khoản ADMIN gốc (BR-M10-10, BR-M10-11) | USER | FR-M10-08.03 |
| ADMIN | Admin tự từ chức | Không phải tài khoản ADMIN gốc; đã xác nhận | USER | FR-M10-05.04 |

#### Đề xuất

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Admin gửi đề xuất làm Mod, hoặc ADMIN gốc gửi đề xuất làm Admin | Người nhận ACTIVE, đã xong bước 3, có vai trò hợp lệ cho loại đề xuất (BR-M10-05, BR-M10-27) | Chưa trả lời | FR-M10-02.01, FR-M10-07.05 |
| Chưa trả lời | Người được đề xuất chọn Chấp nhận | Vai trò còn hợp lệ, tài khoản ACTIVE | Đã chấp nhận | FR-M10-03.02 |
| Chưa trả lời | Người được đề xuất chọn Từ chối | — | Đã từ chối | FR-M10-03.03 |
| Chưa trả lời | Đủ 7 × 24 giờ từ thời điểm gửi (BR-M10-07) | — | Hết hiệu lực | FR-M10-02.10, FR-M10-07.10 |
| Chưa trả lời | Gửi đề xuất mới cùng loại cho cùng người (BR-M10-27) | — | Hết hiệu lực | FR-M10-02.08, FR-M10-07.09 |

#### Công tắc cấu hình (mỗi công tắc AI, chế độ bảo trì, tạm dừng đăng ký, mỗi cờ tính năng)

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Khởi tạo hệ thống | Công tắc AI, cờ tính năng (BR-M10-26) | Bật | FR-M10-09.10, FR-M10-12.09 |
| (bắt đầu) | Khởi tạo hệ thống | Chế độ bảo trì, tạm dừng đăng ký (BR-M10-26) | Tắt | FR-M10-10.04, FR-M10-11.04 |
| Tắt | Admin bật | — | Bật | FR-M10-09.02, FR-M10-10.01, FR-M10-11.01, FR-M10-12.01 |
| Bật | Admin tắt | — | Tắt | FR-M10-09.02, FR-M10-10.01, FR-M10-11.01, FR-M10-12.01 |

#### Banner thông báo toàn trang

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Khởi tạo hệ thống | BR-M10-26 | Không hiện | FR-M10-13.10 |
| Không hiện | Admin đặt banner | Nội dung 1–200 ký tự (BR-M10-20) | Đang hiện | FR-M10-13.01 |
| Đang hiện | Admin sửa nội dung hoặc đặt banner mới | Nội dung 1–200 ký tự | Đang hiện | FR-M10-13.09, FR-M10-13.04 |
| Đang hiện | Admin gỡ banner | — | Không hiện | FR-M10-13.02 |

### 5.19 Giao tiếp với module khác

| Hướng | Module | Nội dung ở mức nghiệp vụ | Yêu cầu |
|---|---|---|---|
| Cung cấp | M01 | Trạng thái chế độ bảo trì (chỉ ADMIN đăng nhập, phiên của người khác không dùng được) và tạm dừng đăng ký (không tạo tài khoản mới); vai trò của tài khoản (ADMIN để M01 cho đăng nhập khi bảo trì); tài khoản ADMIN gốc tạo sẵn, không qua đăng ký | FR-M10-10.02, FR-M10-11.02, FR-M10-07.04 |
| Dùng | M01 | Tài khoản mới mang vai trò USER; trạng thái tài khoản và việc hoàn tất bước 3 để xét đối tượng đề xuất | FR-M10-02.09, FR-M10-07.08, FR-M10-03.11 |
| Cung cấp | M03, M04, M08 | Công tắc AI tổng và công tắc Moderation quyết định có quét bài trước khi đăng, quét bình luận, tự cảnh cáo hay không | FR-M10-09.03, FR-M10-09.04, FR-M10-09.07 |
| Cung cấp | M05 | Công tắc AI tổng và công tắc Topic suggestion | FR-M10-09.03, FR-M10-09.04, FR-M10-09.07 |
| Cung cấp | M06 | Công tắc AI tổng và công tắc Search (tìm ngữ nghĩa hay full-text) | FR-M10-09.03, FR-M10-09.04, FR-M10-09.07 |
| Dùng | M06 | Cách khớp tên khi tìm người dùng, dùng lại cho tìm người dùng trong Admin Panel | FR-M10-01.03 |
| Cung cấp | M13 | Trạng thái mọi công tắc AI, áp dụng cho các lời gọi sau thời điểm đổi; tóm tắt chỉ theo công tắc tổng; bật lại Search thì M13 tạo embedding bù; ngưỡng, thời gian chờ là hằng số, không chỉnh qua Admin Panel; nhật ký quyết định AI tách khỏi nhật ký thao tác Admin | FR-M10-09.02, FR-M10-09.05, FR-M10-09.09, FR-M10-14.05 |
| Cung cấp | M05, M08, M09 | Vai trò MODERATOR, ADMIN quyết định quyền xử lý; các việc chỉ Admin làm (danh mục Topic, cảnh cáo, ban Mod, vụ và khiếu nại về Mod) | FR-M10-07.03 |
| Cung cấp | M05 | Nhật ký thao tác Admin ghi việc Admin thêm, gộp, xóa Topic và thao tác Tag | FR-M10-14.02, FR-M10-14.03 |
| Cung cấp | M08 | Thu hồi vai trò Mod khi M08 ban một Mod | FR-M10-06.01 |
| Cung cấp | M09 | Giáng cấp, thu hồi vai trò Admin là quản lý vai trò, không phải xử lý kiểm duyệt, nên không có khiếu nại; vai trò Mod đã thu hồi lúc bị ban không trả lại | FR-M10-04.03, FR-M10-08.06, FR-M10-06.02 |
| Cung cấp | M07 | Sự kiện đề xuất làm Mod, đề xuất làm Admin (sự kiện mới) và đề xuất lại, để gửi thông báo có Chấp nhận, Từ chối; trạng thái Hết hiệu lực để thông báo hiện "Đã hết hạn" | FR-M10-02.02, FR-M10-07.06, FR-M10-02.10, FR-M10-07.10 |
| Dùng | M07 | Lựa chọn Chấp nhận, Từ chối của người được đề xuất trên thông báo | FR-M10-03.01, FR-M10-03.03, FR-M10-03.09 |
| Dùng | M08 | Sự kiện ban một tài khoản Mod để thu hồi vai trò Mod; nhật ký kiểm duyệt ghi song song thao tác kiểm duyệt của Admin; nhật ký kiểm duyệt lọc được theo người làm | FR-M10-06.01, FR-M10-14.03, FR-M10-01.06 |
| Cung cấp | M11, M12, M16 | Cờ tính năng của Group, Gamification, Chat; khi tắt: chặn thao tác của người dùng không phải Admin, hiện "Hệ thống đang bận…", việc tự làm và kiểm duyệt vẫn chạy, dữ liệu giữ nguyên; danh sách chi tiết ở FR của từng module | FR-M10-12.03, FR-M10-12.04, FR-M10-12.05, FR-M10-12.06, FR-M10-12.07, FR-M10-12.08 |

### 5.20 AI hỗ trợ và hành vi khi tắt AI

- M10 không gọi AI. M10 là nơi đặt công tắc AI tổng và ba công tắc riêng (FR-M10-09.01–FR-M10-09.06), mặc định Bật
  khi khởi tạo (FR-M10-09.10); thay đổi áp dụng cho các thao tác sau thời điểm đổi (FR-M10-09.02). Khi công tắc tắt,
  các module dùng cách dự phòng như trạng thái có chủ đích (FR-M10-09.07); cách dự phòng cụ thể thuộc M03, M04, M05,
  M06, M08, M13.
- Công tắc AI tắt không làm đổi hành vi của M10. Ngưỡng và thời gian chờ của AI là hằng số chính sách, không chỉnh qua
  Admin Panel (FR-M10-09.09).

### 5.21 Yêu cầu HMI

Chưa có — chờ giai đoạn thiết kế.

### 5.22 Chuyển màn hình

Chưa có — chờ giai đoạn thiết kế.

## 6. Lịch sử sửa đổi

| Phiên bản | Ngày | Nội dung | Người sửa |
|---|---|---|---|
| 0.1 | 2026-10-21 | Tạo mới | Phạm Văn Đức |
| 1.0 | 2026-10-21 | Chốt sau 7 bước; ghi register DEC-221–228, QA-412–420, ISS-352–359; còn TBD-M10-01 (Trung bình) | Phạm Văn Đức |
| 1.1 | 2026-10-24 | Đối chiếu với FR-M11, FR-M12, FR-M16: đóng TBD-M10-01 (DEC-236, DEC-245, DEC-256). Không đổi yêu cầu. Chốt bản 1.1 | Phạm Văn Đức |

## Phụ lục A. Truy vết

| ID | Nguồn | Căn cứ | Ghi chú |
|---|---|---|---|
| FR-M10-01 | DM-10.3, DEC-090, DEC-224, DEC-228 | Nói thẳng | Draft "Admin có thể: View user"; DEC-090 "MOD account management" thuộc Admin; DEC-224, DEC-228 làm rõ |
| FR-M10-01.01 | DM-10.3, DEC-090, DEC-221 | Suy ra | Draft "Admin có thể: View user, Change role" ⇒ Admin xem người dùng để chọn người đổi vai trò; các thao tác theo DEC-091, DEC-221 |
| FR-M10-01.02 | DEC-090, QA-011 | Nói thẳng | — |
| FR-M10-01.03 | DEC-228 | Nói thẳng | — |
| FR-M10-01.04 | DEC-228 | Nói thẳng | — |
| FR-M10-01.05 | DEC-228 | Nói thẳng | — |
| FR-M10-01.06 | DEC-224, DEC-228 | Nói thẳng | — |
| FR-M10-02 | DEC-091, DEC-090, QA-012, DEC-220, DEC-222, DEC-228, MR-M10 | Nói thẳng | — |
| FR-M10-02.01 | DEC-091, DEC-222 | Nói thẳng | — |
| FR-M10-02.02 | DEC-091, DEC-220 | Nói thẳng | — |
| FR-M10-02.03 | DEC-091 | Nói thẳng | — |
| FR-M10-02.04 | DEC-091, QA-012 | Nói thẳng | — |
| FR-M10-02.05 | DEC-091, DEC-220, DEC-222 | Nói thẳng | — |
| FR-M10-02.06 | DEC-090, DEC-091 | Nói thẳng | — |
| FR-M10-02.07 | DEC-091, DEC-090 | Suy ra | Đề xuất làm Mod đưa USER lên MOD (DEC-090 "promote USER↔MOD") ⇒ người đã là Mod hoặc Admin không phải đối tượng |
| FR-M10-02.08 | DEC-222 | Nói thẳng | — |
| FR-M10-02.09 | DEC-228 | Nói thẳng | — |
| FR-M10-02.10 | DEC-222 | Nói thẳng | — |
| FR-M10-03 | DEC-091, DEC-220, DEC-221, DEC-222, DEC-228 | Nói thẳng | — |
| FR-M10-03.01 | DEC-091, DEC-222 | Nói thẳng | — |
| FR-M10-03.02 | DEC-091, DEC-220 | Nói thẳng | — |
| FR-M10-03.03 | DEC-091, DEC-220, DEC-221 | Nói thẳng | — |
| FR-M10-03.04 | DEC-220 | Nói thẳng | — |
| FR-M10-03.05 | DEC-220, DEC-222 | Nói thẳng | Bị thay bởi DEC-222 |
| FR-M10-03.06 | DEC-220 | Nói thẳng | — |
| FR-M10-03.07 | DEC-091 | Suy ra | Đề xuất gửi cho một người dùng, người đó chọn Chấp nhận hoặc Từ chối ⇒ người khác không trả lời được |
| FR-M10-03.08 | DEC-222 | Nói thẳng | — |
| FR-M10-03.09 | DEC-221, DEC-222 | Nói thẳng | — |
| FR-M10-03.10 | DEC-222 | Nói thẳng | — |
| FR-M10-03.11 | DEC-228 | Nói thẳng | — |
| FR-M10-04 | DEC-091, DEC-090, QA-013, MR-M10 | Nói thẳng | — |
| FR-M10-04.01 | DEC-091, QA-013 | Nói thẳng | — |
| FR-M10-04.02 | DEC-091 | Nói thẳng | — |
| FR-M10-04.03 | DEC-091 | Nói thẳng | — |
| FR-M10-04.04 | DEC-090 | Nói thẳng | — |
| FR-M10-04.05 | DEC-091, DEC-090 | Suy ra | Giáng cấp đưa MOD về USER (DEC-090 "demote USER↔MOD") ⇒ chỉ áp cho tài khoản MODERATOR |
| FR-M10-05 | QA-013, DEC-223 | Nói thẳng | — |
| FR-M10-05.01 | QA-013, DEC-223 | Nói thẳng | — |
| FR-M10-05.02 | QA-013, DEC-223 | Suy ra | Tự từ chức là cách Mod, Admin bỏ vai trò ⇒ tài khoản USER không có gì để từ chức |
| FR-M10-05.03 | DEC-223 | Nói thẳng | — |
| FR-M10-05.04 | DEC-223 | Nói thẳng | — |
| FR-M10-05.05 | DEC-221, DEC-223 | Nói thẳng | — |
| FR-M10-05.06 | DEC-223 | Nói thẳng | — |
| FR-M10-06 | QA-013, DEC-189, DEC-201 | Nói thẳng | — |
| FR-M10-06.01 | QA-013, DEC-189 | Nói thẳng | — |
| FR-M10-06.02 | DEC-201, QA-013 | Suy ra | DEC-201: lật ban (M09) không trả lại vai trò Mod ⇒ ban hết hạn hay được gỡ cũng không trả lại; vai trò đã về USER lúc bị ban |
| FR-M10-07 | DEC-007, DEC-221, DEC-222, DEC-228 | Nói thẳng | — |
| FR-M10-07.01 | DEC-090, DEC-007 | Nói thẳng | — |
| FR-M10-07.02 | QA-014, DEC-221 | Suy ra | Mỗi tài khoản đúng một vai trò (BR-M10-01), đề xuất làm Admin cho USER, MODERATOR (DEC-221) ⇒ tài khoản ADMIN không phải đối tượng |
| FR-M10-07.03 | QA-014, DM-1.3, DEC-090, DEC-141, DEC-189, DEC-195 | Nói thẳng | — |
| FR-M10-07.04 | DEC-007, DEC-221 | Nói thẳng | — |
| FR-M10-07.05 | DEC-221, DEC-222 | Nói thẳng | — |
| FR-M10-07.06 | DEC-221 | Nói thẳng | — |
| FR-M10-07.07 | DEC-221 | Nói thẳng | — |
| FR-M10-07.08 | DEC-228 | Nói thẳng | — |
| FR-M10-07.09 | DEC-222 | Nói thẳng | — |
| FR-M10-07.10 | DEC-222 | Nói thẳng | — |
| FR-M10-07.11 | DEC-221 | Nói thẳng | — |
| FR-M10-08 | DEC-007, DEC-221 | Nói thẳng | — |
| FR-M10-08.01 | DEC-090, DEC-007 | Nói thẳng | — |
| FR-M10-08.02 | DEC-007, DEC-221 | Suy ra | Thu hồi vai trò Admin chỉ áp cho tài khoản ADMIN |
| FR-M10-08.03 | DEC-221 | Nói thẳng | — |
| FR-M10-08.04 | DEC-221 | Nói thẳng | — |
| FR-M10-08.05 | DEC-221 | Nói thẳng | — |
| FR-M10-08.06 | DEC-221 | Nói thẳng | — |
| FR-M10-09 | DEC-092, DEC-093, DEC-008, QA-259, DEC-205, DEC-206, DEC-228, MR-M10 | Nói thẳng | — |
| FR-M10-09.01 | DEC-092, DEC-093 | Nói thẳng | — |
| FR-M10-09.02 | DEC-008, QA-259 | Nói thẳng | — |
| FR-M10-09.03 | DEC-093 | Nói thẳng | — |
| FR-M10-09.04 | DEC-093, DEC-205 | Nói thẳng | — |
| FR-M10-09.05 | DEC-206, DEC-093 | Nói thẳng | — |
| FR-M10-09.06 | DEC-093 | Suy ra | DEC-093: công tắc riêng "only apply when master is ON" ⇒ trạng thái công tắc riêng được giữ và có tác dụng trở lại khi tổng bật |
| FR-M10-09.07 | DEC-099, DEC-008 | Nói thẳng | — |
| FR-M10-09.08 | DEC-090 | Nói thẳng | — |
| FR-M10-09.09 | DEC-090, DEC-158, DEC-190, DEC-203, DEC-206, DEC-222 | Nói thẳng | — |
| FR-M10-09.10 | DEC-228 | Nói thẳng | — |
| FR-M10-10 | DEC-092, DEC-152, DEC-228, MR-M10 | Nói thẳng | — |
| FR-M10-10.01 | DEC-092, DEC-008 | Nói thẳng | — |
| FR-M10-10.02 | DEC-092, DEC-152 | Nói thẳng | — |
| FR-M10-10.03 | DEC-090 | Nói thẳng | — |
| FR-M10-10.04 | DEC-228 | Nói thẳng | — |
| FR-M10-11 | DEC-092, DEC-152, DEC-228, MR-M10 | Nói thẳng | — |
| FR-M10-11.01 | DEC-092, DEC-008 | Nói thẳng | — |
| FR-M10-11.02 | DEC-092, DEC-152 | Nói thẳng | — |
| FR-M10-11.03 | DEC-090 | Nói thẳng | — |
| FR-M10-11.04 | DEC-228 | Nói thẳng | — |
| FR-M10-12 | DEC-092, DEC-225, DEC-228, MR-M10 | Nói thẳng | — |
| FR-M10-12.01 | DEC-092, DEC-008, DEC-225 | Nói thẳng | — |
| FR-M10-12.02 | DEC-090 | Nói thẳng | — |
| FR-M10-12.03 | DEC-225 | Nói thẳng | — |
| FR-M10-12.04 | DEC-225 | Nói thẳng | — |
| FR-M10-12.05 | DEC-225 | Nói thẳng | — |
| FR-M10-12.06 | DEC-225 | Nói thẳng | — |
| FR-M10-12.07 | DEC-225 | Nói thẳng | — |
| FR-M10-12.08 | DEC-225 | Nói thẳng | — |
| FR-M10-12.09 | DEC-228 | Nói thẳng | — |
| FR-M10-13 | DEC-092, DEC-226, DEC-228, MR-M10 | Nói thẳng | — |
| FR-M10-13.01 | DEC-092, DEC-226 | Nói thẳng | — |
| FR-M10-13.02 | DEC-226 | Nói thẳng | — |
| FR-M10-13.03 | DEC-090 | Nói thẳng | — |
| FR-M10-13.04 | DEC-226 | Suy ra | DEC-226 "one banner at a time" ⇒ đặt banner mới thì banner cũ không còn |
| FR-M10-13.05 | DEC-226, DEC-228 | Nói thẳng | — |
| FR-M10-13.06 | DEC-226 | Nói thẳng | — |
| FR-M10-13.07 | DEC-226 | Nói thẳng | — |
| FR-M10-13.08 | DEC-226 | Nói thẳng | — |
| FR-M10-13.09 | DEC-226 | Nói thẳng | — |
| FR-M10-13.10 | DEC-228 | Nói thẳng | — |
| FR-M10-14 | DEC-094, DEC-146, DM-10.4, DEC-129, DEC-227, DEC-228, MR-M10 | Nói thẳng | — |
| FR-M10-14.01 | DEC-094, DM-10.4, DEC-227 | Nói thẳng | — |
| FR-M10-14.02 | DEC-094, DEC-146, DEC-227 | Nói thẳng | — |
| FR-M10-14.03 | DEC-146, DEC-081, DEC-227 | Nói thẳng | — |
| FR-M10-14.04 | DEC-094, DEC-129 | Nói thẳng | — |
| FR-M10-14.05 | DEC-133 | Nói thẳng | — |
| FR-M10-14.06 | DEC-227 | Nói thẳng | — |
| FR-M10-14.07 | DEC-227 | Nói thẳng | — |
| FR-M10-14.08 | DEC-227 | Nói thẳng | — |
| FR-M10-14.09 | DEC-228 | Nói thẳng | — |
| FR-M10-15 | DEC-094, DEC-090, DEC-228 | Nói thẳng | — |
| FR-M10-15.01 | DEC-094, DM-10.4, DEC-127 | Nói thẳng | — |
| FR-M10-15.02 | DEC-090, DEC-094 | Nói thẳng | — |
| FR-M10-15.03 | DEC-094 | Nói thẳng | — |
| FR-M10-15.04 | DEC-228 | Nói thẳng | — |
| FR-M10-15.05 | DEC-228 | Nói thẳng | — |
| BR-M10-01 | DM-1.3, QA-014 | Nói thẳng | — |
| BR-M10-02 | DEC-090, QA-011, DM-10.3 | Nói thẳng | QA-011 "ADMN: Không" với Guest |
| BR-M10-03 | DEC-090, DEC-141, DEC-189, DEC-195 | Nói thẳng | — |
| BR-M10-04 | DEC-090, QA-259, DEC-158, DEC-190, DEC-203, DEC-206, DEC-222 | Nói thẳng | — |
| BR-M10-05 | DEC-091, QA-012, DEC-228 | Nói thẳng | — |
| BR-M10-06 | DEC-091, DEC-221 | Nói thẳng | — |
| BR-M10-07 | DEC-220, DEC-222 | Nói thẳng | — |
| BR-M10-08 | DEC-091, QA-013 | Nói thẳng | — |
| BR-M10-09 | QA-013, DEC-189, DEC-201 | Suy ra | DEC-201 nói lật ban không trả vai trò ⇒ gỡ ban, hết hạn ban càng không trả (vai trò đã về USER lúc bị ban) |
| BR-M10-10 | DEC-007, DEC-221 | Nói thẳng | — |
| BR-M10-11 | DEC-007, DEC-221 | Nói thẳng | — |
| BR-M10-12 | DEC-092, MR-M10 | Nói thẳng | — |
| BR-M10-13 | DEC-008, QA-259 | Suy ra | Nguồn nói cờ "lưu bền để đổi lúc đang chạy, không cần redeploy" ⇒ thay đổi áp dụng cho thao tác sau thời điểm đổi |
| BR-M10-14 | DEC-093, DEC-008 | Nói thẳng | — |
| BR-M10-15 | DEC-093, DEC-205, DEC-206 | Nói thẳng | — |
| BR-M10-16 | DEC-099, DEC-008, DEC-205 | Nói thẳng | — |
| BR-M10-17 | DEC-092, DEC-152 | Nói thẳng | — |
| BR-M10-18 | DEC-092, DEC-152 | Nói thẳng | — |
| BR-M10-19 | DEC-092, DEC-225 | Nói thẳng | — |
| BR-M10-20 | DEC-092, DEC-226, DEC-228 | Suy ra | Phần Guest: Guest không có tài khoản ⇒ việc đã đóng banner chỉ gắn được với trình duyệt đã đóng; phần còn lại nói thẳng (DEC-226, DEC-228) |
| BR-M10-21 | DEC-094, DEC-146, DEC-227 | Nói thẳng | — |
| BR-M10-22 | DEC-094, DEC-129 | Nói thẳng | — |
| BR-M10-23 | DM-10.4, DEC-127, DEC-228 | Nói thẳng | — |
| BR-M10-24 | DEC-146, DEC-081, DEC-133 | Nói thẳng | — |
| BR-M10-25 | QA-013, DEC-223 | Nói thẳng | — |
| BR-M10-26 | DEC-228 | Nói thẳng | — |
| BR-M10-27 | DEC-222 | Nói thẳng | — |
| BR-M10-28 | DEC-225 | Nói thẳng | — |
| BR-M10-29 | DEC-228 | Nói thẳng | — |
| BR-M10-30 | DEC-224 | Nói thẳng | — |

## Phụ lục B. Câu hỏi, giả định và TBD

### B.1 Câu hỏi đã hỏi

| Mã | Loại | Câu hỏi | Trả lời | Ghi vào register |
|---|---|---|---|---|
| Q-01 | Thiếu chi tiết | Cấp và thu hồi vai trò Admin: làm trực tiếp hay qua đề xuất; cấp cho USER hay chỉ cho Mod; thu hồi được tài khoản ADMIN gốc không; Admin tự thu hồi mình được không; có chặn việc hệ thống không còn Admin nào không? | Chỉ ADMIN gốc cấp, thu hồi vai trò Admin; cấp qua đề xuất làm Admin cho USER hoặc MOD như luồng Mod; thu hồi trực tiếp về USER; ADMIN gốc không bị thu hồi nên luôn còn ít nhất một Admin. Kèm: mọi đề xuất (Mod, Admin) có hạn 7 ngày. | ISS-352, QA-412, DEC-221; ISS-353, QA-413, DEC-222 |
| Q-02 | Mơ hồ | Mod tự từ chức (QA-013) còn hiệu lực không, khi DEC-091 chỉ nêu đề xuất và giáng cấp; nếu còn thì có cần xác nhận không? | A — giữ, áp cả Admin không phải gốc; xác nhận một lần trước khi đổi vai trò. | ISS-354, QA-414, DEC-223 |
| Q-03 | Mơ hồ | "MOD account management (performance, revoke)" (DEC-090): phần "performance" là gì — xem nhật ký kiểm duyệt theo từng Mod (đã có ở M08), hay một màn hình riêng? | A — không có màn hình riêng; xem nhật ký kiểm duyệt (M08) lọc theo Mod; "revoke" là giáng cấp. | ISS-355, QA-415, DEC-224 |
| Q-04 | Thiếu chi tiết | "View user" (DM-10.3): Admin tìm người dùng theo gì và thấy những thông tin gì để đổi vai trò? | Tìm theo username, tên hiển thị (khớp như M06); lọc theo vai trò; hiện username, tên hiển thị, vai trò, trạng thái tài khoản, nhãn "gốc". | ISS-359, QA-420, DEC-228 |
| Q-05 | Thiếu chi tiết | Đề xuất làm Mod gửi được cho tài khoản USER ở trạng thái nào: DEACTIVATED, BANNED, chưa hoàn tất bước 3 đăng ký? | Chỉ tài khoản ACTIVE đã hoàn tất bước 3; chấp nhận khi không còn ACTIVE thì bị từ chối. | ISS-359, QA-420, DEC-228 |
| Q-06 | Mơ hồ | Nhiều đề xuất cho cùng một người: đề xuất cũ chưa trả lời còn Chấp nhận được sau khi người đó đã thành Mod rồi bị giáng cấp, hoặc sau khi đã trả lời một đề xuất khác không? | A — hạn 7 × 24 giờ từ lúc gửi; mỗi người một đề xuất cùng loại còn hiệu lực, đề xuất mới làm đề xuất cũ hết hiệu lực; chấp nhận chỉ có tác dụng khi vai trò còn hợp lệ. | ISS-353, QA-413, DEC-222 |
| Q-07 | Mơ hồ | Cờ tính năng gồm đúng ba module Group, Chat, Gamification, hay mọi module Should/Could (thêm M14 Feed & Discovery, M15 Analytics & Stats)? | Đúng ba module Group, Chat, Gamification, sau khi xét cả 16 module; tạm dừng đăng ký là mục riêng. | ISS-356, QA-416, QA-417, DEC-225 |
| Q-08 | Thiếu chi tiết | Khi một cờ tính năng tắt: người dùng thấy gì (ẩn lối vào, báo tạm ngưng), dữ liệu của module đó được giữ không? | Chặn thao tác của người dùng, hiện "Hệ thống đang bận, vui lòng thử lại sau"; lối vào vẫn hiện; việc tự làm và kiểm duyệt vẫn chạy; dữ liệu giữ nguyên; Admin vẫn dùng được. | ISS-356, QA-416, QA-417, DEC-225 |
| Q-09 | Thiếu chi tiết | Banner: nội dung gồm gì, giới hạn độ dài; một hay nhiều banner cùng lúc; người xem đóng được không; Admin sửa nội dung khi banner đang hiện được không? | B — một banner, văn bản thuần, tối đa 200 ký tự; người xem đóng được; sửa hoặc đặt mới thì hiện lại. | ISS-357, QA-418, DEC-226 |
| Q-10 | Mơ hồ | "Mọi thao tác của Admin" ghi vào nhật ký thao tác Admin gồm những thao tác nào; có ghi việc người được đề xuất chấp nhận không? | A — mọi thao tác làm đổi dữ liệu với vai trò Admin, và mọi thay đổi vai trò kể cả khi người làm không phải Admin; không ghi việc xem, nhận/nhả vụ, việc làm như người dùng thường. | ISS-358, QA-419, DEC-227 |
| Q-11 | Thiếu chi tiết | Lý do trong mục nhật ký thao tác Admin bắt buộc hay tùy chọn, với từng loại thao tác? | Tùy chọn; nếu module gốc bắt buộc lý do thì mục lấy lý do đó. | ISS-359, QA-420, DEC-228 |
| Q-12 | Thiếu chi tiết | Giá trị của từng mục cấu hình lúc khởi tạo hệ thống? | Công tắc AI Bật; bảo trì, tạm dừng đăng ký Tắt; ba cờ tính năng Bật; không có banner. | ISS-359, QA-420, DEC-228 |
| Q-13 | Thiếu chi tiết | Nhật ký thao tác Admin hiện theo thứ tự nào, lọc được theo gì? | Mới nhất trước; lọc theo người làm và loại thao tác. | ISS-359, QA-420, DEC-228 |

### B.2 TBD

| ID | Nội dung | Ảnh hưởng | Lý do chưa chốt |
|---|---|---|---|
| TBD-M10-01 | (Đã đóng ở phiên bản 1.1 — danh sách thao tác bị chặn, vẫn chạy, vẫn hiển thị khi cờ tắt ghi ở FR của từng module: Group DEC-236, Gamification DEC-245, Chat DEC-256) | Thấp | — |

<!-- Bước 2: không OPEN nào sinh TBD cho M10. OPEN-001 (ngân sách AI) chỉ gắn nhãn ADMN, đã loại ở bước 1. OPEN-008: phần còn mở (email liên hệ, bản sao dữ liệu) thuộc M01. -->

### B.3 Cần cân nhắc (ngoài dữ liệu hiện có)

| Mã | Điểm cần cân nhắc | Vì sao cần | Quyết định |
|---|---|---|---|

## Phụ lục C. Sổ nguồn

**Owner keywords:** M10, Admin Panel, admin panel, Admin-only, admin-exclusive, ADMN, role management, role mgmt, quản lý vai trò, Change role, đổi vai trò, promote, promoted, demote, demoted, giáng cấp, Đề xuất làm Mod, proposal, revoke, Auto-revoke, self-resign, từ chức, MOD account management, super admin, root ADMIN, root admin, ADMIN gốc, ADMIN accounts, hierarchy, System config, cấu hình hệ thống, Maintenance mode, maintenance, bảo trì, Registration toggle, registration pause, tạm dừng đăng ký, feature flag, feature flags, announcement banner, banner, AI toggle, master toggle, per-module toggle, công tắc AI, Policy constants, hằng số chính sách, hardcoded, admin action, nhật ký thao tác Admin, append-only, full audit
**Dependency keywords:** MODERATOR, MOD, ADMIN, role, vai trò, notification, thông báo, ban, BANNED, warning, cảnh cáo, appeal, khiếu nại, audit log, nhật ký, AI_ENABLED, AI off, search, moderation, topic, tag, group, nhóm, chat, gamification, registration, đăng ký, login, đăng nhập, session, report, timezone, deployment
**Mục draft của module:** Không có mục riêng cho Admin Panel. Dùng DM-1.3 (vai trò), DM-10.3 (phần xem người dùng, đổi vai trò), DM-10.4 (trường nhật ký, dùng chung với M08)
**Loại khỏi bảng nguồn (khớp nhầm):** DEC-016, QA-059, QA-060 ("revoke" phiên đăng nhập khi đặt lại mật khẩu, M01); DEC-114, QA-192 ("revoke" huy hiệu, M12); DEC-135, ISS-198, QA-257, ISS-177, QA-237, QA-238, QA-239, MR-A02 ("banner" có bài mới trong feed, M14); DEC-102, QA-180, DEC-107, ISS-137, QA-185 (promote, demote Group Mod, M11); ISS-164, QA-222 (vai trò trong Group Chat, M16); DEC-065 ("promote" là sự kiện nhóm, M07); OPEN-001 (ngân sách AI, chỉ gắn nhãn ADMN)

### C.1 Bảng nguồn

| Nguồn | Nhãn | Trạng thái | Dùng ở | Ghi chú |
|---|---|---|---|---|
| DEC-090 | Sở hữu | Sửa một phần bởi DEC-141, DEC-189, DEC-195, DEC-224 | FR-M10-01, FR-M10-01.01, FR-M10-01.02, FR-M10-02, FR-M10-02.06, FR-M10-02.07, FR-M10-04, FR-M10-04.04, FR-M10-04.05, FR-M10-07.01, FR-M10-07.03, FR-M10-08.01, FR-M10-09.08, FR-M10-09.09, FR-M10-10.03, FR-M10-11.03, FR-M10-12.02, FR-M10-13.03, FR-M10-15, FR-M10-15.02, BR-M10-02, BR-M10-03, BR-M10-04 | Nhóm A. Phạm vi Admin riêng (quản lý vai trò, cấu hình, xem toàn bộ nhật ký, quản lý tài khoản Mod) và phần dùng chung với Mod; hằng số chính sách không chỉnh qua giao diện. Phần dùng chung đổi: Topic chỉ Admin (DEC-141); vụ, khiếu nại về Mod và cảnh cáo, ban Mod chỉ Admin (DEC-189, DEC-195) |
| DEC-091 | Sở hữu | Sửa một phần bởi DEC-220, DEC-221, DEC-222, DEC-223 | FR-M10-02, FR-M10-02.01, FR-M10-02.02, FR-M10-02.03, FR-M10-02.04, FR-M10-02.05, FR-M10-02.06, FR-M10-02.07, FR-M10-03, FR-M10-03.01, FR-M10-03.02, FR-M10-03.03, FR-M10-03.07, FR-M10-04, FR-M10-04.01, FR-M10-04.02, FR-M10-04.03, FR-M10-04.05, BR-M10-05, BR-M10-06, BR-M10-08 | Nhóm A. Đề xuất làm Mod (Chấp nhận/Từ chối), giáng cấp trực tiếp, không khiếu nại. DEC-220: đề xuất trả lời một lần, không hết hạn, đề xuất lại là thông báo mới |
| DEC-092 | Sở hữu | Sửa một phần bởi DEC-152, DEC-225, DEC-226, DEC-228 | FR-M10-09, FR-M10-09.01, FR-M10-10, FR-M10-10.01, FR-M10-10.02, FR-M10-11, FR-M10-11.01, FR-M10-11.02, FR-M10-12, FR-M10-12.01, FR-M10-13, FR-M10-13.01, BR-M10-12, BR-M10-17, BR-M10-18, BR-M10-19, BR-M10-20 | Nhóm A. Danh sách cấu hình hệ thống: công tắc AI, bảo trì, tạm dừng đăng ký, cờ tính năng, banner; không có công tắc email. DEC-152: phạm vi tạm dừng đăng ký và bảo trì |
| DEC-093 | Sở hữu | Sửa một phần bởi DEC-205 | FR-M10-09, FR-M10-09.01, FR-M10-09.03, FR-M10-09.04, FR-M10-09.05, FR-M10-09.06, BR-M10-14, BR-M10-15 | Nhóm A. Công tắc AI tổng và ba công tắc riêng Search, Moderation, Topic suggestion. DEC-205: Search điều khiển embedding bài và truy vấn, bật lại thì tạo bù |
| DEC-094 | Sở hữu | Sửa một phần bởi DEC-227, DEC-228 | FR-M10-14, FR-M10-14.01, FR-M10-14.02, FR-M10-14.04, FR-M10-15, FR-M10-15.01, FR-M10-15.02, FR-M10-15.03, BR-M10-21, BR-M10-22 | Nhóm A. Nhật ký thao tác Admin: ghi mọi thao tác Admin, chỉ ghi thêm, Admin xem nhưng không sửa, xóa |
| DM-1.3 | Sở hữu | Hiện hành | FR-M10-07.03, BR-M10-01 | Nhóm A. Ba vai trò USER, MODERATOR, ADMIN. Danh sách quyền thuộc từng module; "Manage users" là phần đổi vai trò |
| DM-10.3 | Sở hữu | Sửa một phần bởi DEC-090, DEC-091 | FR-M10-01, FR-M10-01.01, BR-M10-02 | Nhóm A. Phần "View user", "Change role". Disable, suspend, ban thuộc M08 (DEC-187). "Change role" là đề xuất, giáng cấp. DEC-187 (ngoài bảng nguồn, M08): không có disable, suspend là ban tạm thời |
| DM-10.4 | Sở hữu | Hiện hành | FR-M10-14, FR-M10-14.01, FR-M10-15.01, BR-M10-23 | Nhóm A. Trường của nhật ký (người làm, thao tác, đối tượng, lý do, thời điểm); dùng chung với nhật ký kiểm duyệt M08 |
| ISS-119 | Sở hữu | Trùng với DEC-090 | — | Nhóm A. Phạm vi Admin riêng và dùng chung |
| ISS-120 | Sở hữu | Trùng với DEC-091 | — | Nhóm A. Luồng đề xuất, giáng cấp |
| ISS-121 | Sở hữu | Trùng với DEC-092 | — | Nhóm A. Danh sách cấu hình hệ thống |
| ISS-122 | Sở hữu | Trùng với DEC-093 | — | Nhóm A. Công tắc AI tổng và theo module |
| ISS-123 | Sở hữu | Trùng với DEC-094 | — | Nhóm A. Nhật ký thao tác Admin chỉ ghi thêm |
| QA-160 | Sở hữu | Trùng với DEC-090 | — | Nhóm A. Phạm vi Admin riêng và dùng chung (đã có ghi chú sửa theo DEC-141) |
| QA-161 | Sở hữu | Trùng với DEC-090 | — | Nhóm A. Hằng số chính sách không chỉnh qua giao diện, đổi qua triển khai |
| QA-162 | Sở hữu | Trùng với DEC-091 | — | Nhóm A. Đề xuất làm Mod không điều kiện, người nhận có thể từ chối |
| QA-163 | Sở hữu | Trùng với DEC-091 | — | Nhóm A. Giáng cấp không cần đồng ý, ngay, không khiếu nại |
| QA-164 | Sở hữu | Trùng với DEC-092 | — | Nhóm A. Danh sách cấu hình hệ thống |
| QA-165 | Sở hữu | Trùng với DEC-093 | — | Nhóm A. Công tắc AI tổng và theo module |
| QA-166 | Sở hữu | Trùng với DEC-094 | — | Nhóm A. Thao tác của Admin được ghi, không sửa được |
| MR-M10 | Sở hữu | Sửa một phần bởi DEC-221 | FR-M10-02, FR-M10-04, FR-M10-09, FR-M10-10, FR-M10-11, FR-M10-12, FR-M10-13, FR-M10-14, BR-M10-12 | Nhóm A. Dòng module M10 |
| DEC-007 | Sở hữu | Sửa một phần bởi DEC-221 | FR-M10-07, FR-M10-07.01, FR-M10-07.04, FR-M10-08, FR-M10-08.01, FR-M10-08.02, BR-M10-10, BR-M10-11 | Nhóm B. Ngoài section. Tài khoản ADMIN gốc tạo sẵn, không qua đăng ký; ADMIN cấp, thu hồi vai trò ADMIN qua giao diện quản trị |
| DEC-008 | Sở hữu | Sửa một phần bởi DEC-092, DEC-093 | FR-M10-09, FR-M10-09.02, FR-M10-09.07, FR-M10-10.01, FR-M10-11.01, FR-M10-12.01, BR-M10-13, BR-M10-14, BR-M10-16 | Nhóm B. Ngoài section. Phần nơi đổi cờ AI (ghi chú làm rõ: ở cấu hình hệ thống M10, lưu bền, đổi lúc chạy). Cách dự phòng từng module thuộc M05, M06, M08. Bỏ phương án env var: công tắc ở cấu hình hệ thống, lưu bền, hai tầng |
| DEC-081 | Phụ thuộc | Sửa một phần bởi DEC-146, DEC-193, DEC-224 | FR-M10-14.03, BR-M10-24 | Nhóm B. M08: nhật ký kiểm duyệt, Admin xem toàn bộ |
| DEC-099 | Phụ thuộc | Sửa một phần bởi DEC-205, DEC-206 | FR-M10-09.07, BR-M10-16 | Nhóm B. M13: AI tắt có chủ đích (công tắc M10) khác AI lỗi tạm thời. DEC-207 (ngoài bảng nguồn) chỉ sửa phần nhật ký AI |
| DEC-137 | Nhắc tới | Hiện hành | Không áp dụng: công nghệ | Nhóm B. Công nghệ; nhắc công tắc AI nằm ở cấu hình hệ thống |
| DEC-146 | Phụ thuộc | Hiện hành | FR-M10-14, FR-M10-14.02, FR-M10-14.03, BR-M10-21, BR-M10-24 | Nhóm B. M05/M08: thao tác Tag, Topic của Admin vẫn ghi ở nhật ký thao tác Admin |
| DEC-152 | Phụ thuộc | Hiện hành | FR-M10-10, FR-M10-10.02, FR-M10-11, FR-M10-11.02, BR-M10-17, BR-M10-18 | Nhóm B. M01: tác động của tạm dừng đăng ký và chế độ bảo trì lên đăng ký, đăng nhập, phiên |
| DEC-158 | Phụ thuộc | Hiện hành | FR-M10-09.09, BR-M10-04 | Nhóm B. M01: không có màn hình Admin sửa, đăng trang chính sách; đổi qua triển khai như hằng số chính sách |
| DEC-189 | Phụ thuộc | Sửa một phần bởi DEC-195 | FR-M10-06, FR-M10-06.01, FR-M10-07.03, BR-M10-03, BR-M10-09 | Nhóm B. M08: chỉ Admin cảnh cáo, ban Mod; Admin không bị cảnh cáo, ban; ban Mod thu hồi vai trò Mod |
| DEC-190 | Phụ thuộc | Hiện hành | FR-M10-09.09, BR-M10-04 | Nhóm B. M08: trọng số mức nghiêm trọng là hằng số chính sách (DEC-090) |
| DEC-193 | Nhắc tới | Hiện hành | Không áp dụng: nhật ký kiểm duyệt thuộc M08 | Nhóm B. M08: nhật ký kiểm duyệt không sửa, xóa như nhật ký thao tác Admin |
| DEC-195 | Phụ thuộc | Hiện hành | FR-M10-07.03, BR-M10-03 | Nhóm B. M08/M09: Admin không bị báo cáo; vụ, khiếu nại về Mod chỉ Admin xử lý; nội dung Admin không quét |
| DEC-201 | Phụ thuộc | Hiện hành | FR-M10-06, FR-M10-06.02, BR-M10-09 | Nhóm B. M09: lật ban của Mod cũ không trả vai trò Mod; Admin có thể gửi đề xuất mới |
| DEC-220 | Sở hữu | Sửa một phần bởi DEC-222 | FR-M10-02, FR-M10-02.02, FR-M10-02.05, FR-M10-03, FR-M10-03.02, FR-M10-03.03, FR-M10-03.04, FR-M10-03.05, FR-M10-03.06, BR-M10-07 | Nhóm B. Ngoài section. Đề xuất làm Mod trả lời một lần, không hết hạn; đề xuất lại là thông báo mới. Phần còn lại thuộc M07 |
| ISS-178 | Nhắc tới | Trùng với QA-241 | — | Nhóm B. M15: bảng thống kê chỉ Admin |
| ISS-200 | Nhắc tới | Trùng với QA-259 | — | Nhóm B. Nơi lưu cờ AI; đã có DEC-092/093 |
| ISS-243 | Nhắc tới | Trùng với DEC-152 | — | Nhóm B. Câu hỏi về tạm dừng đăng ký, bảo trì; đã có DEC-152 |
| ISS-351 | Nhắc tới | Trùng với DEC-220 | — | Nhóm B. Danh sách xác nhận M07; đã có DEC-220 |
| ISS-ADMN-01 | Nhắc tới | Hiện hành | Không áp dụng: M08 đã giải quyết | Nhóm B. Backlog cũ gắn ADMN: ngưỡng cảnh cáo để AI chuyển lên; M08 đã giải quyết |
| QA-009 | Sở hữu | Trùng với DEC-007 | — | Nhóm B. Ngoài section. Dev giữ ADMIN gốc; ADMIN cấp ADMIN cho người khác để bàn giao vận hành |
| QA-011 | Phụ thuộc | Sửa một phần bởi DEC-206 | FR-M10-01.02, BR-M10-02 | Nhóm B. Dùng chung: Guest không có quyền ADMN. DEC-171, DEC-208 (ngoài bảng nguồn) sửa phần khác; phần ADMN không đổi |
| QA-012 | Sở hữu | Sửa một phần bởi DEC-091 | FR-M10-02, FR-M10-02.04, BR-M10-05 | Nhóm B. Ngoài section. Admin chỉ định Mod thủ công, không điều kiện. Không sửa dấu: Admin không phong trực tiếp mà gửi đề xuất, người nhận chấp nhận; phần "không điều kiện" còn hiệu lực |
| QA-013 | Sở hữu | Sửa một phần bởi DEC-223 | FR-M10-04, FR-M10-04.01, FR-M10-05, FR-M10-05.01, FR-M10-05.02, FR-M10-06, FR-M10-06.01, FR-M10-06.02, BR-M10-08, BR-M10-09, BR-M10-25 | Nhóm B. Ngoài section. Ba cách Mod mất vai trò: Admin thu hồi, tự động khi bị ban, Mod tự từ chức |
| QA-014 | Sở hữu | Hiện hành | FR-M10-07.02, FR-M10-07.03, BR-M10-01 | Nhóm B. Ngoài section. Mỗi tài khoản một vai trò, thứ bậc USER < MODERATOR < ADMIN; Admin có mọi quyền Mod |
| QA-019 | Nhắc tới | Sửa một phần bởi DEC-189 | Không áp dụng: quyền ban, cảnh cáo, khiếu nại thuộc M08, M09 | Nhóm B. M08/M09: quyền ban, cảnh cáo, khiếu nại; nhắc backlog ADMN. DEC-187 (ngoài bảng nguồn) cũng sửa |
| QA-022 | Nhắc tới | Hiện hành | Không áp dụng: đã có DEC-008 | Nhóm B. M06: nguồn gốc DEC-008 |
| QA-024 | Nhắc tới | Hiện hành | Không áp dụng: đã có DEC-008 | Nhóm B. M13: nguồn gốc DEC-008 |
| QA-241 | Nhắc tới | Hiện hành | Không áp dụng: thống kê chỉ Admin thuộc M15 | Nhóm B. M15: bảng thống kê chỉ Admin |
| QA-259 | Sở hữu | Hiện hành | FR-M10-09, FR-M10-09.02, BR-M10-04, BR-M10-13 | Nhóm B. Ngoài section. Cờ AI ở cấu hình hệ thống, lưu bền; phân biệt công tắc cấu hình với hằng số chính sách |
| QA-303 | Phụ thuộc | Trùng với DEC-152 | — | Nhóm B. M01: tác động của tạm dừng đăng ký và chế độ bảo trì |
| QA-380 | Phụ thuộc | Trùng với DEC-201 | — | Nhóm B. M09: lật ban Mod không trả vai trò, Admin gửi đề xuất mới |
| QA-411 | Sở hữu | Trùng với DEC-220 | — | Nhóm B. Ngoài section. Mục X2: đề xuất làm Mod trả lời một lần, không hết hạn. Các mục khác thuộc M07 |
| MR-A03 | Nhắc tới | Hiện hành | Không áp dụng: thống kê chỉ Admin thuộc M15 | Nhóm B. M15: bảng thống kê chỉ Admin |
| MR-A04 | Nhắc tới | Hiện hành | Không áp dụng: tóm tắt Phase 6, đã có DEC-092 | Nhóm B. Phase 6: cấu hình, cờ tính năng đã có ở M10 |
| MR-A05 | Nhắc tới | Trùng với DEC-137 | — | Nhóm B. Công nghệ; công tắc AI ở Admin Panel |
| MR-M15 | Nhắc tới | Sửa một phần bởi DEC-203 | Không áp dụng: thống kê chỉ Admin thuộc M15 | Nhóm B. M15: bảng thống kê chỉ Admin |
| DEC-133 | Phụ thuộc | Hiện hành | FR-M10-14.05, BR-M10-24 | Nhóm C. M13: nhật ký quyết định AI tách khỏi nhật ký thao tác Admin (ghi thao tác của người). DEC-207 (ngoài bảng nguồn) làm rõ phần nhật ký AI |
| DEC-141 | Phụ thuộc | Hiện hành | FR-M10-07.03, BR-M10-03 | Nhóm C. M05: thêm, gộp, xóa Topic chỉ Admin; sửa phần dùng chung của DEC-090 |
| DEC-203 | Phụ thuộc | Hiện hành | FR-M10-09.09, BR-M10-04 | Nhóm C. M13: ngưỡng chỉnh bằng triển khai |
| DEC-205 | Phụ thuộc | Hiện hành | FR-M10-09, FR-M10-09.04, BR-M10-15, BR-M10-16 | Nhóm C. M13: công tắc Search điều khiển embedding bài và truy vấn; tạo bù khi bật lại |
| DEC-206 | Phụ thuộc | Hiện hành | FR-M10-09, FR-M10-09.05, FR-M10-09.09, BR-M10-04, BR-M10-15 | Nhóm C. M13: tóm tắt theo công tắc AI tổng, không có công tắc riêng |
| QA-254 | Phụ thuộc | Trùng với DEC-133 | — | Nhóm C. M13: nhật ký AI khác nhật ký thao tác Admin |
| DEC-127 | Phụ thuộc | Hiện hành | FR-M10-15.01, BR-M10-23 | Nhóm D. Dùng chung: múi giờ cho thời điểm hiển thị |
| DEC-128 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M10 | Nhóm D. Dùng chung; không quy định hành vi M10 |
| DEC-129 | Phụ thuộc | Hiện hành | FR-M10-14, FR-M10-14.04, BR-M10-22 | Nhóm D. Dùng chung: nhật ký giữ vĩnh viễn, không xóa cứng. DEC-156 (ngoài bảng nguồn) chỉ sửa phần tài khoản đã xóa: nhật ký giữ, gắn qua username |
| DEC-130 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M10 | Nhóm D. Dùng chung; không quy định hành vi M10. DEC-160 (ngoài bảng nguồn) không chạm M10 |
| DEC-131 | Nhắc tới | Sửa một phần bởi DEC-146 | Không áp dụng: dùng chung, không quy định hành vi M10 | Nhóm D. Dùng chung; không quy định hành vi M10. DEC-154 (ngoài bảng nguồn) cũng sửa; không chạm M10 |
| DEC-132 | Nhắc tới | Sửa một phần bởi DEC-141 | Không áp dụng: dùng chung, không quy định hành vi M10 | Nhóm D. Dùng chung; không quy định hành vi M10. DEC-144 (ngoài bảng nguồn) cũng sửa; không chạm M10 |
| DEC-134 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M10 | Nhóm D. Dùng chung; không quy định hành vi M10 |
| DEC-136 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M10 | Nhóm D. Dùng chung; không quy định hành vi M10 |
| DEC-138 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M10 | Nhóm D. Dùng chung; không quy định hành vi M10. DEC-155, DEC-157 (ngoài bảng nguồn) không chạm M10 |
| ISS-189 | Phụ thuộc | Trùng với DEC-127 | — | Nhóm D. Dùng chung: múi giờ (như DEC-127) |
| ISS-190 | Nhắc tới | Trùng với DEC-128 | — | Nhóm D. Dùng chung; không quy định hành vi M10 |
| ISS-191 | Phụ thuộc | Trùng với DEC-129 | — | Nhóm D. Dùng chung: giữ nhật ký (như DEC-129) |
| ISS-192 | Nhắc tới | Trùng với DEC-130 | — | Nhóm D. Dùng chung; không quy định hành vi M10 |
| ISS-193 | Nhắc tới | Trùng với DEC-131 | — | Nhóm D. Dùng chung; không quy định hành vi M10 |
| ISS-194 | Nhắc tới | Trùng với DEC-132 | — | Nhóm D. Dùng chung; không quy định hành vi M10 |
| ISS-195 | Nhắc tới | Trùng với DEC-133 | — | Nhóm D. Dùng chung; không quy định hành vi M10 |
| ISS-196 | Nhắc tới | Trùng với QA-255 | — | Nhóm D. Dùng chung; không quy định hành vi M10 |
| ISS-197 | Nhắc tới | Trùng với DEC-134 | — | Nhóm D. Dùng chung; không quy định hành vi M10 |
| ISS-199 | Nhắc tới | Trùng với DEC-136 | — | Nhóm D. Dùng chung; không quy định hành vi M10 |
| ISS-201 | Nhắc tới | Trùng với QA-260 | — | Nhóm D. Dùng chung; không quy định hành vi M10 |
| ISS-202 | Nhắc tới | Trùng với QA-261 | — | Nhóm D. Dùng chung; không quy định hành vi M10 |
| ISS-203 | Nhắc tới | Trùng với QA-263 | — | Nhóm D. Dùng chung; không quy định hành vi M10 |
| ISS-204 | Nhắc tới | Trùng với DEC-138 | — | Nhóm D. Dùng chung; không quy định hành vi M10 |
| QA-248 | Phụ thuộc | Trùng với DEC-127 | — | Nhóm D. Dùng chung: múi giờ (như DEC-127) |
| QA-249 | Nhắc tới | Trùng với DEC-128 | — | Nhóm D. Dùng chung; không quy định hành vi M10 |
| QA-250 | Phụ thuộc | Trùng với DEC-129 | — | Nhóm D. Dùng chung: giữ nhật ký (như DEC-129) |
| QA-251 | Nhắc tới | Trùng với DEC-130 | — | Nhóm D. Dùng chung; không quy định hành vi M10 |
| QA-252 | Nhắc tới | Trùng với DEC-131 | — | Nhóm D. Dùng chung; không quy định hành vi M10 |
| QA-253 | Nhắc tới | Trùng với DEC-132 | — | Nhóm D. Dùng chung; không quy định hành vi M10 |
| QA-255 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M10 | Nhóm D. Dùng chung; không quy định hành vi M10 |
| QA-256 | Nhắc tới | Trùng với DEC-134 | — | Nhóm D. Dùng chung; không quy định hành vi M10 |
| QA-258 | Nhắc tới | Trùng với DEC-136 | — | Nhóm D. Dùng chung; không quy định hành vi M10 |
| QA-260 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M10 | Nhóm D. Dùng chung; không quy định hành vi M10 |
| QA-261 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M10 | Nhóm D. Dùng chung; không quy định hành vi M10 |
| QA-262 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M10 | Nhóm D. Dùng chung; không quy định hành vi M10 |
| QA-263 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M10 | Nhóm D. Dùng chung; không quy định hành vi M10 |
| QA-264 | Nhắc tới | Trùng với DEC-138 | — | Nhóm D. Dùng chung; không quy định hành vi M10 |
| DEC-221 | Sở hữu | Hiện hành | FR-M10-01.01, FR-M10-03, FR-M10-03.03, FR-M10-03.09, FR-M10-05.05, FR-M10-07, FR-M10-07.02, FR-M10-07.04, FR-M10-07.05, FR-M10-07.06, FR-M10-07.07, FR-M10-07.11, FR-M10-08, FR-M10-08.02, FR-M10-08.03, FR-M10-08.04, FR-M10-08.05, FR-M10-08.06, BR-M10-06, BR-M10-10, BR-M10-11 | Nhóm A. ADMIN gốc; chỉ gốc cấp (qua đề xuất), thu hồi Admin; sự kiện thông báo mới ở M07 |
| DEC-222 | Sở hữu | Hiện hành | FR-M10-02, FR-M10-02.01, FR-M10-02.05, FR-M10-02.08, FR-M10-02.10, FR-M10-03, FR-M10-03.01, FR-M10-03.05, FR-M10-03.08, FR-M10-03.09, FR-M10-03.10, FR-M10-07, FR-M10-07.05, FR-M10-07.09, FR-M10-07.10, FR-M10-09.09, BR-M10-04, BR-M10-07, BR-M10-27 | Nhóm A. Đề xuất có hạn 7 ngày; một đề xuất cùng loại còn hiệu lực; vai trò hợp lệ khi chấp nhận |
| DEC-223 | Sở hữu | Hiện hành | FR-M10-05, FR-M10-05.01, FR-M10-05.02, FR-M10-05.03, FR-M10-05.04, FR-M10-05.05, FR-M10-05.06, BR-M10-25 | Nhóm A. Tự từ chức của Mod, Admin không phải gốc, có xác nhận |
| DEC-224 | Sở hữu | Hiện hành | FR-M10-01, FR-M10-01.06, BR-M10-30 | Nhóm A. Hiệu suất Mod = nhật ký kiểm duyệt lọc theo Mod; M08 thêm lọc theo người làm |
| DEC-225 | Sở hữu | Hiện hành | FR-M10-12, FR-M10-12.01, FR-M10-12.03, FR-M10-12.04, FR-M10-12.05, FR-M10-12.06, FR-M10-12.07, FR-M10-12.08, BR-M10-19, BR-M10-28 | Nhóm A. Cờ tính năng cho Group, Chat, Gamification; hành vi khi tắt |
| DEC-226 | Sở hữu | Hiện hành | FR-M10-13, FR-M10-13.01, FR-M10-13.02, FR-M10-13.04, FR-M10-13.05, FR-M10-13.06, FR-M10-13.07, FR-M10-13.08, FR-M10-13.09, BR-M10-20 | Nhóm A. Banner: một, văn bản thuần, 200 ký tự, người xem đóng được |
| DEC-227 | Sở hữu | Hiện hành | FR-M10-14, FR-M10-14.01, FR-M10-14.02, FR-M10-14.03, FR-M10-14.06, FR-M10-14.07, FR-M10-14.08, BR-M10-21 | Nhóm A. Phạm vi nhật ký thao tác Admin |
| DEC-228 | Sở hữu | Hiện hành | FR-M10-01, FR-M10-01.03, FR-M10-01.04, FR-M10-01.05, FR-M10-01.06, FR-M10-02, FR-M10-02.09, FR-M10-03, FR-M10-03.11, FR-M10-07, FR-M10-07.08, FR-M10-09, FR-M10-09.10, FR-M10-10, FR-M10-10.04, FR-M10-11, FR-M10-11.04, FR-M10-12, FR-M10-12.09, FR-M10-13, FR-M10-13.05, FR-M10-13.10, FR-M10-14, FR-M10-14.09, FR-M10-15, FR-M10-15.04, FR-M10-15.05, BR-M10-05, BR-M10-20, BR-M10-23, BR-M10-26, BR-M10-29 | Nhóm A. Danh sách xác nhận: xem người dùng, đối tượng đề xuất, độ dài banner, nhật ký, giá trị khởi tạo |
| ISS-352 | Sở hữu | Trùng với DEC-221 | — | Nhóm A. Câu hỏi đã có DEC-221 |
| ISS-353 | Sở hữu | Trùng với DEC-222 | — | Nhóm A. Câu hỏi đã có DEC-222 |
| ISS-354 | Sở hữu | Trùng với DEC-223 | — | Nhóm A. Câu hỏi đã có DEC-223 |
| ISS-355 | Sở hữu | Trùng với DEC-224 | — | Nhóm A. Câu hỏi đã có DEC-224 |
| ISS-356 | Sở hữu | Trùng với DEC-225 | — | Nhóm A. Câu hỏi đã có DEC-225 |
| ISS-357 | Sở hữu | Trùng với DEC-226 | — | Nhóm A. Câu hỏi đã có DEC-226 |
| ISS-358 | Sở hữu | Trùng với DEC-227 | — | Nhóm A. Câu hỏi đã có DEC-227 |
| ISS-359 | Sở hữu | Trùng với DEC-228 | — | Nhóm A. Câu hỏi đã có DEC-228 |
| QA-412 | Sở hữu | Trùng với DEC-221 | — | Nhóm A. Lời stakeholder cho DEC-221 |
| QA-413 | Sở hữu | Trùng với DEC-222 | — | Nhóm A. Lời stakeholder cho DEC-222 |
| QA-414 | Sở hữu | Trùng với DEC-223 | — | Nhóm A. Lời stakeholder cho DEC-223 |
| QA-415 | Sở hữu | Trùng với DEC-224 | — | Nhóm A. Lời stakeholder cho DEC-224 |
| QA-416 | Sở hữu | Trùng với DEC-225 | — | Nhóm A. Lời stakeholder cho DEC-225 (hành vi khi tắt) |
| QA-417 | Sở hữu | Trùng với DEC-225 | — | Nhóm A. Lời stakeholder cho DEC-225 (module có cờ) |
| QA-418 | Sở hữu | Trùng với DEC-226 | — | Nhóm A. Lời stakeholder cho DEC-226 |
| QA-419 | Sở hữu | Trùng với DEC-227 | — | Nhóm A. Lời stakeholder cho DEC-227 |
| QA-420 | Sở hữu | Trùng với DEC-228 | — | Nhóm A. Lời stakeholder cho DEC-228 |
| DEC-236 | Nhắc tới | Hiện hành | Không áp dụng: đóng TBD-M10-01 (phần Group) | Đối chiếu FR-M11, FR-M16 (bản 1.1) |
| DEC-245 | Nhắc tới | Hiện hành | Không áp dụng: đóng TBD-M10-01 (phần Gamification) | Đối chiếu FR-M12, FR-M16 (bản 1.1) |
| DEC-256 | Nhắc tới | Hiện hành | Không áp dụng: đóng TBD-M10-01 (phần Chat) | Đối chiếu FR-M16 (bản 1.1) |

### C.2 Chuỗi quyết định

| Chuỗi | Nội dung hiện hành |
|---|---|
| DEC-090 → DEC-141; DEC-189 → DEC-195; DEC-090 → DEC-224 (ISS-119, QA-160, QA-161, QA-415, ISS-355) | Việc chỉ Admin làm: quản lý vai trò, cấu hình hệ thống, xem toàn bộ nhật ký, quản lý tài khoản Mod; hằng số chính sách không chỉnh qua giao diện. Quản lý tài khoản Mod là xem nhật ký kiểm duyệt lọc theo Mod và giáng cấp; không có màn hình, chỉ số hiệu suất riêng (DEC-224). Phần dùng chung với Mod bị thu hẹp: thêm, gộp, xóa Topic chỉ Admin (DEC-141), xóa mềm Tag vẫn dùng chung; chỉ Admin cảnh cáo, ban Mod; vụ và khiếu nại về Mod chỉ Admin xử lý; Admin không bị báo cáo, cảnh cáo, ban (DEC-189, DEC-195; thi hành ở M08, M09). |
| QA-012 → DEC-091 → DEC-220 → DEC-222; DEC-228 (QA-162, QA-163, ISS-120, QA-411, ISS-351, QA-413, ISS-353) | Làm Mod: Admin gửi đề xuất, không cần điều kiện về điểm, uy tín; chỉ cho tài khoản USER ACTIVE đã xong bước 3 (DEC-228). Chấp nhận thì thành Mod ngay, Từ chối thì không đổi gì; trả lời một lần. Đề xuất có hạn 7 × 24 giờ từ lúc gửi, quá hạn thì Hết hiệu lực, hiện "Đã hết hạn" (DEC-222 thay phần "không hết hạn" của DEC-220); mỗi người một đề xuất cùng loại còn hiệu lực; chấp nhận chỉ có tác dụng khi vai trò còn hợp lệ. Phần "Admin chọn người rồi phong thẳng" của QA-012 bị thay bằng đề xuất + chấp nhận. Giáng cấp: Admin làm trực tiếp, ngay, không cần đồng ý, không khiếu nại. |
| QA-013 → DEC-189 → DEC-201; QA-013 → DEC-223 (QA-380, QA-414, ISS-354) | Mod mất vai trò theo ba cách: Admin giáng cấp (DEC-091); tự động khi bị ban (DEC-189); tự từ chức có xác nhận (DEC-223, áp cả Admin không phải gốc). Lật ban của Mod cũ không trả lại vai trò; muốn có lại vai trò thì chấp nhận một đề xuất mới. |
| DEC-007 (QA-009) → DEC-221 (QA-412, ISS-352); QA-014; DEC-065 → DEC-221 (M07, đã loại khỏi bảng nguồn) | Một tài khoản ADMIN gốc tạo sẵn, không qua đăng ký, mang vai trò ADMIN và dấu "gốc"; không bị thu hồi, không từ chức, nên hệ thống luôn có ít nhất một Admin. Chỉ ADMIN gốc cấp vai trò Admin (qua đề xuất làm Admin cho USER hoặc MOD, hạn 7 ngày như đề xuất làm Mod) và thu hồi vai trò Admin (trực tiếp, về USER). M07 thêm sự kiện thông báo "Đề xuất làm Admin". Mỗi tài khoản đúng một vai trò, thứ bậc USER < MODERATOR < ADMIN, Admin có mọi quyền Mod. |
| DEC-008 → DEC-092, DEC-093 (ISS-200, QA-259) → DEC-205; DEC-206, DEC-099; DEC-228 | Công tắc AI nằm ở cấu hình hệ thống, lưu bền, đổi lúc đang chạy (bỏ phương án env var của DEC-008), mặc định Bật khi khởi tạo (DEC-228). Hai tầng: công tắc tổng tắt thì mọi AI tắt; ba công tắc riêng Search, Moderation, Topic suggestion chỉ có tác dụng khi công tắc tổng bật. Search điều khiển cả embedding bài và embedding truy vấn, bật lại thì tạo bù (DEC-205); tóm tắt theo công tắc tổng, không có công tắc riêng (DEC-206). Công tắc cấu hình khác hằng số chính sách (QA-259). Cách dự phòng khi tắt thuộc từng module (DEC-099; DEC-099 → DEC-207 ngoài bảng nguồn chỉ làm rõ nhật ký AI). |
| DEC-092 → DEC-152, DEC-225, DEC-226, DEC-228 (QA-164, ISS-121, QA-303, ISS-243, QA-416, QA-417, QA-418, QA-420, ISS-356, ISS-357, ISS-359) | Năm mục cấu hình: công tắc AI, chế độ bảo trì, tạm dừng đăng ký, cờ tính năng, banner; không có công tắc email. Tạm dừng đăng ký: không tạo tài khoản mới bằng email hay Google lần đầu; liên kết Google vẫn được; người đã qua bước 1 làm tiếp. Bảo trì: chỉ ADMIN đăng nhập; phiên của người khác không dùng được (thi hành ở M01). Cờ tính năng chỉ cho Group, Chat, Gamification; khi tắt: chặn thao tác của người dùng không phải Admin, hiện "Hệ thống đang bận, vui lòng thử lại sau", lối vào vẫn hiện, việc tự làm và kiểm duyệt vẫn chạy, dữ liệu giữ nguyên, bật lại không tính bù (DEC-225). Banner: một, văn bản thuần, 1–200 ký tự, mọi người thấy, người xem đóng được, nội dung mới thì hiện lại (DEC-226). Khởi tạo: công tắc AI và cờ tính năng Bật, bảo trì và tạm dừng đăng ký Tắt, không có banner (DEC-228). |
| DEC-094 → DEC-227, DEC-228 (ISS-123, QA-166, QA-419, ISS-358); DEC-146; DEC-081 → DEC-193, DEC-224; DEC-133 (QA-254); DEC-129; DM-10.4 | Nhật ký thao tác Admin ghi mọi thao tác làm đổi dữ liệu với vai trò Admin (vai trò, cấu hình, banner, kiểm duyệt, khiếu nại, Topic, Tag) và mọi thay đổi vai trò không do Admin làm (chấp nhận đề xuất, tự từ chức, mất vai trò Mod do ban với người làm "Hệ thống"); không ghi việc xem, nhận/nhả vụ, việc làm như người dùng thường (DEC-227). Chỉ ghi thêm, không sửa, không xóa, giữ vĩnh viễn (DEC-094, DEC-129). Trường: người làm, thao tác, đối tượng, lý do (tùy chọn, lấy lý do bắt buộc của module gốc nếu có), thời điểm; hiện mới nhất trước, lọc theo người làm và loại thao tác (DEC-228). Thao tác kiểm duyệt của Admin đồng thời nằm ở nhật ký kiểm duyệt M08, nhật ký này lọc được theo người làm (DEC-224). Nhật ký quyết định AI là nhật ký riêng (DEC-133; DEC-133 → DEC-207 ngoài bảng nguồn chỉ làm rõ nhật ký AI). DEC-129 → DEC-156 (ngoài bảng nguồn): nhật ký của tài khoản đã xóa vẫn giữ, gắn qua username. |
| DEC-090 (QA-161) → DEC-158, DEC-190, DEC-203, DEC-206, DEC-222 | Hằng số chính sách đổi qua triển khai, không có màn hình Admin: thời hạn cảnh cáo, ban, ngưỡng AI (DEC-203), trọng số mức nghiêm trọng (DEC-190), thời gian chờ tóm tắt (DEC-206), hạn 7 ngày của đề xuất (DEC-222), nội dung và phiên bản trang chính sách (DEC-158). |
| DM-10.3 → DEC-090, DEC-091, DEC-228 | "View user" là tìm theo username, tên hiển thị, lọc theo vai trò, hiện username, tên hiển thị, vai trò, trạng thái tài khoản, nhãn "gốc" (DEC-228). "Change role" là đề xuất làm Mod, Admin, giáng cấp, thu hồi Admin. "Disable, Suspend, Ban" thuộc M08 (DEC-187, ngoài bảng nguồn: không có disable, suspend là ban tạm thời). |
| MR-M10 → DEC-221 (DEC-221–228) | Dòng module M10 có dấu sửa đổi FR M10; nội dung hiện hành theo các chuỗi trên. |
| QA-011 → DEC-206; DEC-171, DEC-208 (ngoài bảng nguồn) | Guest không có quyền ở Admin Panel ("ADMN: Không") giữ nguyên; các sửa đổi chỉ chạm hồ sơ, tóm tắt AI, tìm kiếm. |
| MR-M15 → DEC-203; ISS-178 (QA-241) | Bảng thống kê chỉ Admin xem thuộc M15; không chạm M10. |
