---
module: M02
ten_module: User Profile
ma_tai_lieu: FR-M02
phien_ban: 1.0
trang_thai: Đã chốt
ngay: 2026-10-13
tac_gia: Phạm Văn Đức
moc_nguon: DEC-177, QA-341, ISS-281, OPEN-009
steps_completed: [1, 2, 3, 4, 5, 6, 7]
---
# Tài liệu yêu cầu chức năng — M02 User Profile

| Mã tài liệu | FR-M02 |
|---|---|
| Dự án | iShare |
| Module | M02 — User Profile |
| Trạng thái | Đã chốt |
| Phiên bản | 1.0 |
| Ngày | 2026-10-13 |
| Tác giả | Phạm Văn Đức |

<!-- Quy ước chung cho mọi bảng dưới đây:
     - Thân tài liệu không ghi nguồn. Nguồn của mọi ID nằm ở Phụ lục A.
     - Ô không có nội dung ghi "—". Không xóa cột.
     - Mục chưa tới bước làm thì để dòng "(Chưa làm — bước N)". -->

## 1. Tổng quan

### 1.1 Mục đích

Module User Profile cho mỗi người dùng một trang hồ sơ công khai tại một địa chỉ theo username, nơi mọi người, kể cả
người chưa đăng nhập, xem avatar, tên, bio, Lớp/Khối, ngày tham gia, điểm và badge, số người theo dõi và bài viết của
người đó. Chủ hồ sơ sửa thông tin hồ sơ, đổi avatar, lưu bài viết để đọc lại và xem các bài đã lưu, bài đã xóa ngay
trên trang hồ sơ của mình.

### 1.2 Phạm vi

**Trong phạm vi:**

- Trang hồ sơ tại một địa chỉ theo username, hiển thị khác nhau cho chủ hồ sơ và người xem (kể cả Guest, chỉ đọc):
  avatar, display_name, username, bio, Lớp/Khối, ngày tham gia, điểm và badge (chỉ hiển thị), số và danh sách người
  theo dõi, đang theo dõi (danh sách cần đăng nhập).
- Các tab nội dung trên hồ sơ: chủ hồ sơ thấy Bài viết, Bookmark và tab "Đã xóa"; người xem chỉ thấy Bài viết. Bài nào
  hiện ở tab Bài viết tùy người xem; thứ tự các danh sách trên hồ sơ.
- Sửa hồ sơ: thay avatar (loại tệp, kích thước, xóa ảnh cũ), avatar mặc định, sửa bio (cách đếm ký tự), tự cập nhật
  hoặc bỏ chọn Lớp/Khối; trang sửa hồ sơ là nơi đổi username, display_name.
- Bookmark: lưu bài, bỏ lưu, danh sách Bookmark của chủ tài khoản, cách hiện bài đã lưu khi bài không còn xem được.
- Hiển thị hồ sơ theo trạng thái tài khoản: tài khoản vô hiệu hóa hoặc đã xóa hiện "người dùng không tồn tại";
  tài khoản bị khóa vẫn hiện hồ sơ kèm nhãn "Tài khoản đã bị khóa"; tài khoản vô hiệu hóa, bị khóa không có trong
  danh sách theo dõi của người khác.

**Ngoài phạm vi:**

- Quy tắc username, display_name; bước 3 đăng ký (nhập bio, Lớp/Khối, avatar lần đầu); dữ liệu bị xóa khi tài khoản
  chuyển DELETED; trạng thái tài khoản — M01 Authentication & Account.
- Tính điểm, trao badge, thống kê người dùng (stars nhận, stars cho, reputation) — M12 Gamification; M02 chỉ hiển thị.
- Hành động theo dõi (Follow) người dùng và thông báo "người theo dõi mới" — M07 Notification.
- Nội dung bài viết và việc khôi phục bài đã xóa — M03 Post & Content; M02 chỉ đặt tab "Đã xóa" trên hồ sơ.
- Tính bookmark vào Trending Topic/Tag — M05 Topic & Tag; Trending Post — M14 Feed & Discovery.
- Mức cảnh báo của người dùng (không bao giờ hiện trên hồ sơ) — M08 Moderation.
- Bài nháp, chờ duyệt, bị từ chối, tự ẩn và trạng thái của bài — M03; bài ẩn danh, nhóm Private — M11 Group. M02
  chỉ quyết bài nào hiện ở tab Bài viết.
- Đã quyết không làm: lịch sử đổi username trên hồ sơ; liên kết mạng xã hội; avatar ảnh GIF động; tự tăng Lớp/Khối
  theo năm học; Bookmark kèm nhận thông báo về bài đã lưu; nhắc cập nhật Lớp/Khối đầu năm học; số stars nhận, stars cho
  trên hồ sơ; Mod, Admin gỡ avatar hoặc bio của người khác.

## 2. Thuật ngữ và viết tắt

### 2.1 Thuật ngữ

| Thuật ngữ | Định nghĩa |
|---|---|
| Hồ sơ | Thông tin công khai của một người dùng: avatar, bio, Lớp/Khối, cùng username, display_name lấy từ tài khoản (M01). Mỗi tài khoản có một hồ sơ. |
| Trang hồ sơ | Trang hiển thị hồ sơ của một người dùng tại địa chỉ /u/{username}. |
| Chủ hồ sơ | Người đang đăng nhập và đang xem trang hồ sơ của chính mình. |
| Người xem | Người đang xem trang hồ sơ không phải của mình. |
| Tab nội dung | Các danh sách trên trang hồ sơ: Bài viết (bài của chủ hồ sơ), Bookmark (bài chủ hồ sơ đã lưu), Đã xóa (bài chủ hồ sơ đã xóa còn trong thời hạn khôi phục của M03). |
| Avatar | Ảnh đại diện của người dùng, hiển thị cắt tròn. |
| Bio | Đoạn giới thiệu ngắn, không bắt buộc, do người dùng tự viết. |
| Ngày tham gia | Ngày tài khoản của người dùng được tạo (M01), hiện trên trang hồ sơ. |
| Thời điểm tạo bài | Lúc bài viết được tạo (M03); dùng để xếp tab Bài viết. |
| Bài đăng ẩn danh | Bài trong nhóm được đăng không hiện tên tác giả với người dùng thường (M11). |
| Lớp/Khối (trên hồ sơ) | Cấp học 10, 11 hoặc 12 người dùng tự khai trên hồ sơ, không bắt buộc. Độc lập với Lớp/Khối trên bài viết (M03). |
| Bookmark, lưu bài | Việc người dùng lưu một bài viết để đọc lại. Bỏ lưu là thao tác ngược lại. |
| Bài đã lưu | Bài viết một người dùng đang lưu (chưa bỏ lưu). |
| Thời điểm lưu | Lúc người dùng lưu bài; dùng để xếp tab Bookmark. |
| Bị xóa hẳn | Bài tác giả đã xóa mà không khôi phục trong thời hạn khôi phục của M03 (7 × 24 giờ từ lúc xóa). |
| Nội dung không tồn tại | Dòng thay thế ở tab Bookmark cho bài đã lưu tạm thời không xem được; cũng là câu hiện khi mở bài bị ẩn. |
| Người theo dõi | Người dùng đang theo dõi chủ hồ sơ. Việc theo dõi do M07 thực hiện. |
| Đang theo dõi | Những người dùng chủ hồ sơ đang theo dõi. Không gồm Topic, bài viết chủ hồ sơ theo dõi. |
| Thời điểm bắt đầu theo dõi | Lúc người theo dõi bắt đầu theo dõi người kia (M07); dùng để xếp danh sách theo dõi. |
| Điểm, badge | Điểm đóng góp và huy hiệu của người dùng do M12 tính và trao; M02 chỉ hiển thị. |
| Trạng thái tài khoản | ACTIVE, DEACTIVATED (vô hiệu hóa, còn trong thời hạn kích hoạt lại), DELETED (đã xóa), BANNED (bị khóa). Do M01 quản lý. |
| Trạng thái bài | Nháp, Chờ duyệt, Đã đăng, Tự ẩn, Bị từ chối, Đã xóa, và trạng thái kiểm duyệt Bị Mod ẩn. Do M03 quản lý. |
| Khóa toàn bộ | Mức khóa bài của M03: chặn bình luận mới, upvote, bình chọn poll; vẫn lưu và báo cáo được. |
| Nhãn "Tài khoản đã bị khóa" | Nhãn công khai hiện ở mọi nơi tên người dùng xuất hiện khi tài khoản ở trạng thái BANNED (M12). |
| Mức cảnh báo | LIGHT, MEDIUM, HEAVY của M08; riêng tư, không hiện trên hồ sơ. |
| Ký tự | Đơn vị đếm độ dài bio, sau khi cắt khoảng trắng đầu và cuối: mỗi chữ cái (kể cả chữ có dấu), chữ số, khoảng trắng, dấu, emoji hoặc lần xuống dòng là một ký tự. |
| Avatar mặc định | Avatar hệ thống hiện khi người dùng chưa đặt avatar. Hình thức (ảnh chung hoặc chữ cái đầu của display_name) chốt ở giai đoạn thiết kế; tài khoản đã xóa luôn dùng ảnh chung. |
| Bài xem được | Bài người đang xem có quyền mở theo quy tắc của M03, M11 (ví dụ bài đã đăng, không bị ẩn; bài nhóm Private với thành viên nhóm). |
| MB | Đơn vị dung lượng tệp dùng trong giới hạn avatar (megabyte), cùng đơn vị với giới hạn ảnh đính kèm của M03. |

### 2.2 Viết tắt

| Viết tắt | Đầy đủ |
|---|---|
| FR | Functional Requirement — yêu cầu chức năng |
| BR | Business Rule — quy tắc nghiệp vụ |
| MS1 | Milestone 1 — mốc phát hành đầu tiên |
| CRUD | Tạo, Đọc, Sửa, Xóa |
| Mod | Moderator — người kiểm duyệt |

## 3. Thông tin đầu vào

### 3.1 Tài liệu đầu vào

| Tài liệu | Phiên bản / mốc |
|---|---|
| Draft: docs/_temp/iShare_modules.md, iShare_specs_general.md | Theo ngày sửa tệp |
| Register: decisions, qa-log, issue-queue, open-issues, glossary, module-registry | DEC-177, QA-341, ISS-281, OPEN-009 (khớp `moc_nguon`) |

### 3.2 Tài liệu liên quan

| Module | Liên quan ở điểm nào |
|---|---|
| M01 Authentication & Account | Cấp username, display_name và quy tắc đổi tên; nhận bio, Lớp/Khối, avatar ở bước 3 đăng ký; trạng thái tài khoản quyết định hồ sơ có hiện hay không; xóa dữ liệu hồ sơ, bookmark, theo dõi khi DELETED. |
| M03 Post & Content | Bài viết và trạng thái bài cho tab Bài viết, tab Bookmark; tab "Đã xóa" trên hồ sơ để tác giả khôi phục bài; bài Khóa toàn bộ vẫn bookmark được. |
| M04 Comment | Avatar giữ chỗ, avatar mặc định ở bình luận của tài khoản vô hiệu hóa, đã xóa. |
| M05 Topic & Tag | Bookmark là một tương tác tính vào Trending Topic/Tag. |
| M07 Notification | Hành động theo dõi người dùng và thông báo người theo dõi mới; số người theo dõi hiện trên hồ sơ. |
| M08 Moderation | Mức cảnh báo không hiện trên hồ sơ; báo cáo người dùng xử lý bằng cảnh cáo, khóa, không gỡ avatar, bio. |
| M12 Gamification | Điểm, badge, thống kê hiển thị trên hồ sơ; nhãn tài khoản bị khóa. |
| M11 Group | Bài đăng ẩn danh và bài trong nhóm Private quyết định bài nào hiện ở tab Bài viết và bài đã lưu nào xem được. |
| M14 Feed & Discovery | Guest phải đăng nhập để bookmark, theo dõi; Trending Post có thể tính bookmark (OPEN-009). |
| M16 Chat & Messaging | Avatar, display_name hiện ở người gửi tin nhắn. |

## 4. Tổng quan chức năng

### 4.1 Luật, tiêu chuẩn liên quan

Không có.

### 4.2 Vai trò

| Vai trò | Mô tả trong module này |
|---|---|
| Guest | Người chưa đăng nhập. Xem trang hồ sơ ở ngữ cảnh người xem, chỉ đọc; không mở danh sách theo dõi, không lưu bài, không sửa hồ sơ. |
| User | Người dùng đã đăng nhập. Xem hồ sơ và danh sách theo dõi của mọi người dùng; sửa hồ sơ, đổi avatar, lưu bài và xem bài đã lưu của chính mình. |
| Mod | Có mọi quyền của User trong module này. Không có quyền nào trên hồ sơ của người khác, kể cả gỡ avatar hoặc bio. |
| Admin | Có mọi quyền của User trong module này. Không có quyền nào trên hồ sơ của người khác, kể cả gỡ avatar hoặc bio. |
| Chủ hồ sơ | Vai trò theo ngữ cảnh: User, Mod hoặc Admin đang xem trang hồ sơ của chính mình. Thấy nút sửa hồ sơ và các tab Bài viết, Bookmark, Đã xóa. |
| Người xem | Vai trò theo ngữ cảnh: người đang xem trang hồ sơ không phải của mình. Chỉ đọc, chỉ thấy tab Bài viết. |

### 4.3 Ma trận quyền

| Hành động | Guest | User | Mod | Admin | Yêu cầu |
|---|---|---|---|---|---|
| Xem trang hồ sơ của một người dùng (thông tin hồ sơ, tab Bài viết) | ✓ | ✓ | ✓ | ✓ | FR-M02-01.01, FR-M02-01.16 |
| Xem danh sách người theo dõi, đang theo dõi của một người dùng | ✗ | ✓ | ✓ | ✓ | FR-M02-02.01, FR-M02-02.03, FR-M02-02.05 |
| Sửa thông tin hồ sơ (bio, Lớp/Khối) | ✗ | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | FR-M02-03.02, FR-M02-03.10 |
| Đổi avatar | ✗ | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | FR-M02-04.01, FR-M02-04.07 |
| Sửa, gỡ thông tin hồ sơ, avatar của người khác | ✗ | ✗ | ✗ | ✗ | FR-M02-03.10, FR-M02-04.07, FR-M02-01.06 |
| Lưu bài viết (Bookmark), bỏ lưu | ✗ | ✓ | ✓ | ✓ | FR-M02-05.01, FR-M02-06.01, FR-M02-05.02 |
| Xem danh sách bài đã lưu, tab Đã xóa | ✗ | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | FR-M02-07.01, FR-M02-01.05 |
| Xem danh sách bài đã lưu, tab Đã xóa của người khác | ✗ | ✗ | ✗ | ✗ | FR-M02-07.02, FR-M02-01.06 |

<!-- Ô suy ra:
     - Hàng 1–2 cột User/Mod/Admin: DEC-025 "Full list public", ISS-059 "to all users"; DEC-023 người xem có trang chỉ đọc.
       Cột Guest hàng 1–2 nói thẳng ở DEC-171.
     - Hàng 3–5: DEC-023 nút sửa hồ sơ chỉ hiện khi người xem là chủ hồ sơ ⇒ không ai sửa được hồ sơ người khác, Guest không có hồ sơ.
     - Hàng 6 cột Guest: DEC-126 mọi tương tác, kể cả bookmark, cần đăng nhập.
     - Hàng 7–8: DEC-023, DEC-024 người xem chỉ thấy tab Bài viết ⇒ Bookmark và Đã xóa chỉ chủ hồ sơ thấy; Guest không có hồ sơ.
     - Mod/Admin không có quyền riêng: DEC-177 (không gỡ avatar, bio). -->

### 4.4 Danh sách chức năng

| ID | Chức năng | Tác nhân chính | Kích hoạt |
|---|---|---|---|
| FR-M02-01 | Xem trang hồ sơ | Người xem, Chủ hồ sơ | Người dùng mở địa chỉ hồ sơ /u/{username} của một người dùng |
| FR-M02-02 | Xem danh sách người theo dõi và đang theo dõi | Người xem, Chủ hồ sơ | Người dùng chọn số người theo dõi hoặc đang theo dõi trên trang hồ sơ |
| FR-M02-03 | Sửa thông tin hồ sơ | Chủ hồ sơ | Chủ hồ sơ bấm nút sửa hồ sơ trên trang hồ sơ của mình |
| FR-M02-04 | Đổi avatar | Chủ hồ sơ | Chủ hồ sơ tải lên ảnh mới làm avatar |
| FR-M02-05 | Lưu bài viết (Bookmark) | User, Mod, Admin | Người dùng chọn lưu một bài viết |
| FR-M02-06 | Bỏ lưu bài viết | User, Mod, Admin | Người dùng chọn bỏ lưu một bài viết đã lưu |
| FR-M02-07 | Xem danh sách bài đã lưu | Chủ hồ sơ | Chủ hồ sơ mở tab Bookmark trên trang hồ sơ của mình |

### 4.5 Mốc và ưu tiên

Toàn bộ yêu cầu của module thuộc MS1, ưu tiên **Must** (bảng MoSCoW Summary của module-registry: Must gồm M01–M10, M13;
cột MoSCoW ở dòng M02 của bảng Module List bị lệch nên không dùng). Không có yêu cầu ngoại lệ về ưu tiên.

## 5. Yêu cầu chức năng

### 5.1 FR-M02-01 Xem trang hồ sơ

**Yêu cầu cấp trên:** Hệ thống phải hiển thị trang hồ sơ của một người dùng tại địa chỉ /u/{username}, theo ngữ cảnh chủ hồ sơ hoặc người xem.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M02-01.01 | Khi người dùng mở địa chỉ /u/{username} của một tài khoản ACTIVE hoặc BANNED, hệ thống phải hiển thị trang hồ sơ của người dùng đó. |
| FR-M02-01.02 | Hệ thống phải hiển thị trên trang hồ sơ avatar, display_name, username, bio, Lớp/Khối khi đã đặt, ngày tham gia, điểm, badge, số người theo dõi, số đang theo dõi và các tab nội dung. |
| FR-M02-01.03 | Hệ thống phải hiển thị avatar dạng cắt tròn. |
| FR-M02-01.04 | Nếu bio trống, hệ thống phải không hiển thị gì ở vị trí bio. |
| FR-M02-01.05 | Khi chủ hồ sơ mở trang hồ sơ của mình, hệ thống phải hiển thị nút sửa hồ sơ và ba tab Bài viết, Bookmark, Đã xóa, mở sẵn tab Bài viết. |
| FR-M02-01.06 | Khi người xem mở trang hồ sơ của người khác, hệ thống phải chỉ hiển thị tab Bài viết, không hiển thị nút sửa hồ sơ. |
| FR-M02-01.07 | Khi người xem mở tab Bài viết, hệ thống phải chỉ hiển thị các bài đã đăng, không bị ẩn, không đăng ẩn danh của chủ hồ sơ, trong đó bài thuộc nhóm Private chỉ hiển thị khi người xem là thành viên nhóm đó. |
| FR-M02-01.08 | Khi chủ hồ sơ mở tab Đã xóa, hệ thống phải hiển thị các bài đã xóa của chủ hồ sơ theo FR-M03-15.03. |
| FR-M02-01.09 | Hệ thống phải hiển thị tổng điểm của người dùng phản ánh ngay mỗi thay đổi điểm, không chờ chu kỳ tính bảng xếp hạng. |
| FR-M02-01.10 | Hệ thống phải chỉ hiển thị badge người dùng đã đạt, không hiển thị tiến độ tới badge chưa đạt. |
| FR-M02-01.11 | Nếu tài khoản của hồ sơ ở trạng thái DEACTIVATED hoặc DELETED, hệ thống phải hiển thị "người dùng không tồn tại" thay cho nội dung hồ sơ. |
| FR-M02-01.12 | Nếu tài khoản của hồ sơ ở trạng thái BANNED, hệ thống phải hiển thị nhãn "Tài khoản đã bị khóa" trên trang hồ sơ. |
| FR-M02-01.13 | Hệ thống phải không hiển thị mức cảnh báo của người dùng trên trang hồ sơ. |
| FR-M02-01.14 | Hệ thống phải không hiển thị lịch sử đổi username trên trang hồ sơ. |
| FR-M02-01.15 | Hệ thống phải không hiển thị liên kết mạng xã hội trên hồ sơ. |
| FR-M02-01.16 | Hệ thống phải cho phép Guest xem trang hồ sơ ở ngữ cảnh người xem, chỉ đọc. |
| FR-M02-01.17 | Khi chủ hồ sơ mở tab Bài viết, hệ thống phải hiển thị thêm các bài nháp, chờ duyệt, bị từ chối, tự ẩn và bài đăng ẩn danh của chủ hồ sơ, bài ẩn danh kèm dấu "ẩn danh". |
| FR-M02-01.18 | Nếu người dùng chưa đặt avatar, hệ thống phải hiển thị avatar mặc định. |
| FR-M02-01.19 | Hệ thống phải sắp xếp tab Bài viết theo thời điểm tạo bài, mới nhất trước. |
| FR-M02-01.20 | Khi địa chỉ /u/{username} khác username của một tài khoản chỉ ở chữ hoa, chữ thường, hệ thống phải mở trang hồ sơ của tài khoản đó. |
| FR-M02-01.21 | Nếu không có tài khoản nào mang username trong địa chỉ /u/{username}, hệ thống phải hiển thị "người dùng không tồn tại". |
| FR-M02-01.22 | Khi người dùng đã đổi username, hệ thống phải không chuyển hướng địa chỉ theo username cũ sang địa chỉ theo username mới. |
| FR-M02-01.23 | Hệ thống phải không hiển thị số stars nhận, số stars cho trên trang hồ sơ. |

### 5.2 FR-M02-02 Xem danh sách người theo dõi và đang theo dõi

**Yêu cầu cấp trên:** Hệ thống phải cho phép xem danh sách người theo dõi và danh sách đang theo dõi của một người dùng.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M02-02.01 | Khi người dùng đã đăng nhập chọn số người theo dõi trên trang hồ sơ, hệ thống phải hiển thị danh sách người dùng đang theo dõi chủ hồ sơ. |
| FR-M02-02.02 | Khi người dùng đã đăng nhập chọn số đang theo dõi trên trang hồ sơ, hệ thống phải hiển thị danh sách người dùng chủ hồ sơ đang theo dõi. |
| FR-M02-02.03 | Hệ thống phải cho mọi người dùng đã đăng nhập xem danh sách người theo dõi, đang theo dõi của mọi người dùng, không có tùy chọn ẩn danh sách. |
| FR-M02-02.04 | Nếu tài khoản của hồ sơ ở trạng thái DEACTIVATED hoặc DELETED, hệ thống phải không hiển thị danh sách theo dõi của tài khoản đó. |
| FR-M02-02.05 | Nếu Guest chọn mở danh sách người theo dõi hoặc đang theo dõi, hệ thống phải yêu cầu đăng nhập. |
| FR-M02-02.06 | Hệ thống phải chỉ đưa người dùng vào danh sách đang theo dõi, không đưa Topic, bài viết chủ hồ sơ theo dõi. |
| FR-M02-02.07 | Trong khi một tài khoản ở trạng thái DEACTIVATED hoặc BANNED, hệ thống phải không hiển thị và không đếm tài khoản đó trong danh sách người theo dõi, đang theo dõi của người khác. |
| FR-M02-02.08 | Khi tài khoản đó trở lại trạng thái ACTIVE, hệ thống phải hiển thị và đếm lại tài khoản đó trong các danh sách theo dõi. |
| FR-M02-02.09 | Hệ thống phải sắp xếp danh sách người theo dõi, đang theo dõi theo thời điểm bắt đầu theo dõi, mới nhất trước. |

### 5.3 FR-M02-03 Sửa thông tin hồ sơ

**Yêu cầu cấp trên:** Hệ thống phải cho phép chủ hồ sơ sửa bio và Lớp/Khối trên hồ sơ của mình.

**Lý do:** Giới hạn bio 155 ký tự là quyết định về trải nghiệm sản phẩm: 155 ký tự gần bằng độ dài mô tả ngắn hiển thị tốt. Nguồn chưa nêu lý do cho các phần khác.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M02-03.01 | Khi chủ hồ sơ bấm nút sửa hồ sơ, hệ thống phải hiển thị trang sửa hồ sơ gồm bio, Lớp/Khối, avatar, username và display_name. |
| FR-M02-03.02 | Khi chủ hồ sơ lưu thay đổi hợp lệ, hệ thống phải cập nhật bio, Lớp/Khối trên hồ sơ theo giá trị mới. |
| FR-M02-03.03 | Khi chủ hồ sơ nhập bio, hệ thống phải hiển thị số ký tự đã dùng. |
| FR-M02-03.04 | Nếu bio dài hơn 155 ký tự, hệ thống phải từ chối lưu bio. |
| FR-M02-03.05 | Hệ thống phải cho phép lưu hồ sơ với bio trống. |
| FR-M02-03.06 | Nếu Lớp/Khối nằm ngoài ba giá trị 10, 11, 12, hệ thống phải từ chối lưu Lớp/Khối. |
| FR-M02-03.07 | Hệ thống phải cho phép hồ sơ không có Lớp/Khối. |
| FR-M02-03.08 | Hệ thống phải giữ nguyên Lớp/Khối trên hồ sơ cho tới khi chủ hồ sơ tự sửa, không tự tăng theo năm học. |
| FR-M02-03.09 | Nếu tài khoản của chủ hồ sơ không ở trạng thái ACTIVE, hệ thống phải từ chối sửa thông tin hồ sơ. |
| FR-M02-03.10 | Nếu người thực hiện khác chủ hồ sơ, hệ thống phải từ chối sửa thông tin hồ sơ. |
| FR-M02-03.11 | Khi chủ hồ sơ lưu bio, hệ thống phải cắt khoảng trắng ở đầu và cuối bio trước khi đếm ký tự. |
| FR-M02-03.12 | Nếu bio chỉ gồm khoảng trắng, hệ thống phải lưu bio là trống. |
| FR-M02-03.13 | Hệ thống phải tính mỗi emoji và mỗi lần xuống dòng trong bio là một ký tự. |
| FR-M02-03.14 | Hệ thống phải cho phép chủ hồ sơ bỏ chọn Lớp/Khối đã đặt để hồ sơ không có Lớp/Khối. |
| FR-M02-03.15 | Hệ thống phải không gửi thông báo nhắc cập nhật Lớp/Khối theo năm học. |

### 5.4 FR-M02-04 Đổi avatar

**Yêu cầu cấp trên:** Hệ thống phải cho phép chủ hồ sơ tải lên một ảnh làm avatar thay cho avatar hiện tại.

**Lý do:** Giới hạn 5 MB để cùng mức với ảnh đính kèm bài viết. Không nhận ảnh GIF động vì cấu hình nơi lưu ảnh phức tạp, không đáng làm.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M02-04.01 | Khi chủ hồ sơ tải lên một ảnh JPEG, PNG hoặc WebP không quá 5 MB, hệ thống phải đặt ảnh đó làm avatar của chủ hồ sơ. |
| FR-M02-04.02 | Hệ thống phải lưu ảnh gốc của avatar. |
| FR-M02-04.03 | Nếu ảnh thuộc loại khác JPEG, PNG, WebP, kể cả ảnh GIF động, hệ thống phải từ chối ảnh. |
| FR-M02-04.04 | Nếu ảnh lớn hơn 5 MB, hệ thống phải từ chối ảnh. |
| FR-M02-04.05 | Khi avatar mới được đặt thành công, hệ thống phải xóa avatar cũ khỏi nơi lưu ảnh. |
| FR-M02-04.06 | Nếu tài khoản của chủ hồ sơ không ở trạng thái ACTIVE, hệ thống phải từ chối đổi avatar. |
| FR-M02-04.07 | Nếu người thực hiện khác chủ hồ sơ, hệ thống phải từ chối đổi avatar. |

### 5.5 FR-M02-05 Lưu bài viết (Bookmark)

**Yêu cầu cấp trên:** Hệ thống phải cho phép người dùng đã đăng nhập lưu một bài viết để đọc lại.

**Lý do:** Lưu bài để đọc hoặc tham khảo lại.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M02-05.01 | Khi người dùng đã đăng nhập chọn lưu một bài viết chưa lưu, hệ thống phải thêm bài đó vào danh sách bài đã lưu của người dùng. |
| FR-M02-05.02 | Nếu người dùng chưa đăng nhập chọn lưu hoặc bỏ lưu bài viết, hệ thống phải yêu cầu đăng nhập. |
| FR-M02-05.03 | Nếu bài viết đã có trong danh sách bài đã lưu, hệ thống phải không thêm bài đó lần nữa. |
| FR-M02-05.04 | Trong khi bài viết ở mức Khóa toàn bộ, hệ thống phải tiếp tục cho phép lưu bài. |
| FR-M02-05.05 | Hệ thống phải không gửi thông báo về một bài viết cho người dùng chỉ vì người dùng đã lưu bài đó. |

### 5.6 FR-M02-06 Bỏ lưu bài viết

**Yêu cầu cấp trên:** Hệ thống phải cho phép người dùng bỏ lưu một bài viết đang lưu.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M02-06.01 | Khi người dùng chọn bỏ lưu một bài viết đang lưu, hệ thống phải xóa bài đó khỏi danh sách bài đã lưu của người dùng. |
| FR-M02-06.02 | Trong khi bài viết ở mức Khóa toàn bộ, hệ thống phải tiếp tục cho phép bỏ lưu bài. |

### 5.7 FR-M02-07 Xem danh sách bài đã lưu

**Yêu cầu cấp trên:** Hệ thống phải hiển thị cho chủ hồ sơ danh sách bài viết mình đang lưu trong tab Bookmark.

**Lý do:** Lưu bài để đọc hoặc tham khảo lại.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M02-07.01 | Khi chủ hồ sơ mở tab Bookmark, hệ thống phải hiển thị các bài viết chủ hồ sơ đang lưu. |
| FR-M02-07.02 | Nếu người yêu cầu xem khác chủ của danh sách bài đã lưu, hệ thống phải từ chối hiển thị danh sách đó. |
| FR-M02-07.03 | Trong khi một bài đã lưu không xem được với chủ danh sách, hệ thống phải hiển thị dòng "Nội dung không tồn tại" ở vị trí của bài đó trong tab Bookmark, không nêu lý do. |
| FR-M02-07.04 | Khi bài đó xem được trở lại, hệ thống phải hiển thị lại bài ở vị trí cũ trong tab Bookmark. |
| FR-M02-07.05 | Hệ thống phải cho phép chủ danh sách bỏ lưu dòng "Nội dung không tồn tại". |
| FR-M02-07.06 | Khi bài đã lưu bị xóa hẳn hoặc tác giả của bài chuyển sang DELETED, hệ thống phải xóa bookmark của bài đó. |
| FR-M02-07.07 | Hệ thống phải sắp xếp tab Bookmark theo thời điểm lưu, mới nhất trước. |

### 5.8 Quy tắc nghiệp vụ

| ID | Loại | Quy tắc | Ví dụ |
|---|---|---|---|
| BR-M02-01 | Sự kiện | Mỗi người dùng có một trang hồ sơ tại /u/{username}. Cùng một địa chỉ hiển thị theo hai ngữ cảnh: chủ hồ sơ khi người đang đăng nhập là chính người dùng đó, người xem trong mọi trường hợp còn lại. | Lan (username lan_12) mở /u/lan_12: ngữ cảnh chủ hồ sơ. Minh mở /u/lan_12: ngữ cảnh người xem. |
| BR-M02-02 | Ràng buộc | Trang hồ sơ hiện avatar, display_name, username, bio, Lớp/Khối (khi đã đặt), ngày tham gia, điểm, badge, số người theo dõi, số đang theo dõi và các tab nội dung; không hiện số stars nhận, stars cho. | — |
| BR-M02-03 | Ràng buộc | Chủ hồ sơ thấy nút sửa hồ sơ và ba tab Bài viết, Bookmark, Đã xóa, mặc định mở tab Bài viết. Người xem không thấy nút sửa hồ sơ và chỉ thấy tab Bài viết. | Lan mở hồ sơ của mình: thấy 3 tab, đang ở Bài viết. Minh mở hồ sơ Lan: chỉ có tab Bài viết. |
| BR-M02-04 | Ràng buộc | Bio không bắt buộc, dài tối đa 155 ký tự; khi nhập bio, hệ thống hiện số ký tự đã dùng. | Bio 155 ký tự: nhận. Bio 156 ký tự: từ chối. Bio trống: nhận. |
| BR-M02-05 | Suy diễn | Bio trống thì trang hồ sơ không hiện gì ở vị trí bio. | — |
| BR-M02-06 | Ràng buộc | Avatar chỉ nhận ảnh JPEG, PNG hoặc WebP, dung lượng tối đa 5 MB; không nhận ảnh GIF động. | Ảnh PNG 5 MB: nhận. Ảnh JPEG 5,2 MB: từ chối. Ảnh GIF động 1 MB: từ chối. |
| BR-M02-07 | Kích hoạt | Khi chủ hồ sơ thay avatar mới thành công, avatar cũ bị xóa khỏi nơi lưu ảnh. | — |
| BR-M02-08 | Sự kiện | Avatar hiển thị dạng cắt tròn; ảnh gốc được lưu nguyên. | — |
| BR-M02-09 | Ràng buộc | Lớp/Khối trên hồ sơ không bắt buộc, nhận một trong ba giá trị 10, 11, 12, có thể bỏ chọn để về trống, và độc lập với Lớp/Khối trên bài viết. | Hồ sơ đặt Lớp 11: nhận. Bỏ chọn Lớp 11: hồ sơ không có Lớp/Khối. Hồ sơ Lớp 12, đăng bài chọn Lớp 10: hợp lệ. |
| BR-M02-10 | Sự kiện | Lớp/Khối trên hồ sơ chỉ đổi khi người dùng tự sửa; hệ thống không tự tăng theo năm học. | Đặt Lớp 10 tháng 9/2026; tháng 9/2027 hồ sơ vẫn hiện Lớp 10 cho tới khi người dùng sửa. |
| BR-M02-11 | Sự kiện | Điểm và badge trên hồ sơ chỉ để hiển thị; việc tính điểm, trao badge thuộc M12. | — |
| BR-M02-12 | Ràng buộc | Tổng điểm trên hồ sơ phản ánh ngay mỗi thay đổi điểm, không chờ chu kỳ tính bảng xếp hạng. | Bài của Lan được upvote lúc 10:05: tổng điểm trên hồ sơ đổi ngay, dù bảng xếp hạng chỉ cập nhật ở lần tính kế tiếp. |
| BR-M02-13 | Ràng buộc | Hồ sơ chỉ hiện badge người dùng đã đạt; không hiện tiến độ tới badge chưa đạt. | Lan đang có 150 điểm, mốc badge kế tiếp là 300: không hiện "150/300 điểm". |
| BR-M02-14 | Ràng buộc | Danh sách người theo dõi và đang theo dõi của mọi người dùng xem được bởi mọi người dùng đã đăng nhập; người dùng không ẩn được danh sách của mình. Guest thấy hai con số nhưng phải đăng nhập mới mở được danh sách. | — |
| BR-M02-15 | Suy diễn | Trang hồ sơ của tài khoản DEACTIVATED hoặc DELETED hiện "người dùng không tồn tại" thay cho nội dung hồ sơ. | Lan vô hiệu hóa lúc 01/10 21:00: từ lúc đó /u/lan_12 hiện "người dùng không tồn tại". Lan kích hoạt lại ngày 05/10: hồ sơ hiện lại bình thường. |
| BR-M02-16 | Suy diễn | Trang hồ sơ của tài khoản BANNED vẫn hiện bình thường cho người khác, kèm nhãn "Tài khoản đã bị khóa". | — |
| BR-M02-17 | Ràng buộc | Trang hồ sơ không bao giờ hiện mức cảnh báo của người dùng. | — |
| BR-M02-18 | Ràng buộc | Chỉ tài khoản ACTIVE được sửa thông tin hồ sơ và đổi avatar. | — |
| BR-M02-19 | Sự kiện | Trang hồ sơ không hiện lịch sử đổi username. | — |
| BR-M02-20 | Sự kiện | Hồ sơ không có liên kết mạng xã hội. | — |
| BR-M02-21 | Sự kiện | Bookmark chỉ dùng để lưu bài đọc lại; lưu bài không kèm nhận thông báo về bài đó. | — |
| BR-M02-22 | Ràng buộc | Mỗi người dùng lưu một bài viết nhiều nhất một lần; bài đang lưu chỉ có thể bỏ lưu. | Lan lưu bài A: A vào danh sách bài đã lưu. Lan chọn lưu A lần nữa: danh sách vẫn chỉ có một A. |
| BR-M02-23 | Ràng buộc | Danh sách bài đã lưu chỉ chủ tài khoản xem được. | — |
| BR-M02-24 | Ràng buộc | Phải đăng nhập mới lưu hoặc bỏ lưu bài viết. | — |
| BR-M02-25 | Suy diễn | Bài ở mức Khóa toàn bộ vẫn lưu và bỏ lưu được. | — |
| BR-M02-26 | Ràng buộc | Guest xem được trang hồ sơ ở ngữ cảnh người xem, chỉ đọc. | — |
| BR-M02-27 | Ràng buộc | Danh sách đang theo dõi chỉ gồm người dùng. Tài khoản DEACTIVATED hoặc BANNED không hiện và không được đếm trong danh sách người theo dõi, đang theo dõi; tài khoản trở lại ACTIVE thì hiện và được đếm lại. | Lan theo dõi Minh, Hà, Tú và Topic Toán: hồ sơ Lan ghi "Đang theo dõi: 3". Hà bị khóa: ghi 2, danh sách Minh, Tú. Hà được gỡ khóa: ghi 3. |
| BR-M02-28 | Ràng buộc | Tab Bài viết: người xem chỉ thấy bài đã đăng, không bị ẩn, không đăng ẩn danh của chủ hồ sơ, bài nhóm Private chỉ khi người xem là thành viên nhóm đó; chủ hồ sơ thấy thêm bài nháp, chờ duyệt, bị từ chối, tự ẩn và bài ẩn danh của mình, bài ẩn danh kèm dấu "ẩn danh". | Lan có bài A đã đăng, bài B nháp, bài C đăng ẩn danh trong nhóm, bài D trong nhóm Private "Đội tuyển Toán". Minh (không trong nhóm D) xem hồ sơ Lan: thấy A. Hà (thành viên nhóm D): thấy A, D. Lan: thấy A, B, C (dấu "ẩn danh"), D. |
| BR-M02-29 | Suy diễn | Trong khi một bài đã lưu không xem được với người lưu, tab Bookmark hiện dòng "Nội dung không tồn tại" ở vị trí của bài, không nêu lý do; người lưu bỏ lưu được dòng này. Bài xem được trở lại thì dòng đó hiện lại bài. | 01/10 Lan lưu bài của Minh. 03/10 Minh xóa bài: 04/10 tab Bookmark của Lan có dòng "Nội dung không tồn tại" ở chỗ cũ. 05/10 Minh khôi phục: 06/10 dòng đó lại là bài. |
| BR-M02-30 | Kích hoạt | Khi bài đã lưu bị xóa hẳn hoặc tác giả của bài chuyển sang DELETED, bookmark của bài đó bị xóa. | Minh xóa bài lúc 01/10 21:00 và không khôi phục: từ 08/10 21:00 bài bị xóa hẳn, dòng của bài biến khỏi tab Bookmark của Lan. |
| BR-M02-31 | Ràng buộc | Mọi danh sách trên hồ sơ xếp mới nhất trước: tab Bài viết theo thời điểm tạo bài, tab Bookmark theo thời điểm lưu, danh sách theo dõi theo thời điểm bắt đầu theo dõi. | Lan lưu bài A ngày 01/10, bài B ngày 03/10: tab Bookmark hiện B rồi A. |
| BR-M02-32 | Sự kiện | Người dùng chưa đặt avatar thì hiện avatar mặc định. | — |
| BR-M02-33 | Tính toán | Độ dài bio được đếm sau khi cắt khoảng trắng đầu và cuối; mỗi emoji, mỗi lần xuống dòng là một ký tự; bio chỉ gồm khoảng trắng là bio trống. | "  Thích Toán 📐  " được lưu thành "Thích Toán 📐", dài 12 ký tự. "     ": lưu là bio trống. |
| BR-M02-34 | Ràng buộc | Địa chỉ /u/{username} không phân biệt chữ hoa, chữ thường. Địa chỉ theo username cũ không chuyển hướng sang username mới; địa chỉ không ứng với tài khoản nào hiện "người dùng không tồn tại". | /u/LAN_12 mở hồ sơ lan_12. Lan đổi sang lan_nguyen: /u/lan_12 hiện "người dùng không tồn tại" nếu chưa ai lấy lan_12; Tú lấy lan_12 thì /u/lan_12 mở hồ sơ của Tú. |
| BR-M02-35 | Sự kiện | Không có thông báo nhắc cập nhật Lớp/Khối theo năm học ở MS1. | — |
| BR-M02-36 | Sự kiện | Mod và Admin không gỡ, không sửa avatar hoặc bio của người khác; xử lý báo cáo người dùng giữ như M08 (cảnh cáo hoặc khóa). | — |

### 5.9 Dữ liệu nghiệp vụ

| Thực thể | Thuộc tính nguồn đã nêu | Quan hệ |
|---|---|---|
| Hồ sơ | Avatar (ảnh gốc), bio, Lớp/Khối. Draft nêu thêm ngày tham gia (Q-04). | Thuộc một tài khoản (M01); lấy từ tài khoản username, display_name, trạng thái tài khoản |
| Bookmark | Người lưu, bài viết được lưu, thời điểm lưu | Thuộc một người dùng và một bài viết (M03); M05 dùng để tính Trending |
| Quan hệ theo dõi | Người theo dõi, đối tượng được theo dõi (người dùng, Topic, bài viết) | Do M07 tạo; M02 đọc để hiện số và danh sách người theo dõi, đang theo dõi |

<!-- Thời điểm lưu: DEC-145 chỉ tính bookmark xảy ra trong cửa sổ 7 ngày ⇒ phải biết lúc lưu.
     Quan hệ theo dõi không thuộc M02; ghi ở đây vì trang hồ sơ đọc nó. -->

**Ma trận CRUD:**

| Thực thể | Tạo | Đọc | Sửa | Xóa |
|---|---|---|---|---|
| Hồ sơ | M01 (tạo tài khoản; bước 3 đăng ký nhập bio, Lớp/Khối, avatar) | FR-M02-01.02 | FR-M02-03.02, FR-M02-04.01, FR-M02-04.05 | M01 (khi DELETED xóa avatar, bio, Lớp/Khối) |
| Bookmark | FR-M02-05.01 | FR-M02-07.01; M05 | Không có (chỉ lưu hoặc bỏ lưu, BR-M02-22) | FR-M02-06.01, FR-M02-07.06; M01 (khi DELETED) |
| Quan hệ theo dõi | M07 | FR-M02-01.02, FR-M02-02.01, FR-M02-02.02 | M07 | M07; M01 (khi DELETED); M05 (khi gộp, xóa Topic) |

### 5.10 Chuyển trạng thái

Không có thực thể nào của module có trạng thái theo nguồn. Bookmark chỉ có hai khả năng: có hoặc không có.
Cách trang hồ sơ hiện theo trạng thái tài khoản (M01) được ghi bằng quy tắc BR-M02-15, BR-M02-16.

### 5.11 Giao tiếp với module khác

| Hướng | Module | Nội dung ở mức nghiệp vụ | Yêu cầu |
|---|---|---|---|
| Cung cấp | M01 | Quy tắc bio, Lớp/Khối, avatar cho bước 3 đăng ký (FR-M01-03.03); trang sửa hồ sơ là nơi đổi username, display_name | FR-M02-03.01, FR-M02-03.04, FR-M02-03.06, FR-M02-04.03, FR-M02-04.04 |
| Dùng | M01 | username, display_name và quy tắc đổi tên (FR-M01-03.15, FR-M01-03.16); trạng thái tài khoản (hồ sơ, danh sách theo dõi, bookmark khi tác giả DELETED); khi DELETED xóa avatar, bio, Lớp/Khối, bookmark và mọi lượt theo dõi | FR-M02-01.01, FR-M02-01.11, FR-M02-02.07, FR-M02-03.09, FR-M02-07.06 |
| Cung cấp | M03 | Tab Đã xóa trên hồ sơ tác giả, nơi tác giả khôi phục bài (FR-M03-15.03, FR-M03-16) | FR-M02-01.05, FR-M02-01.08 |
| Dùng | M03 | Bài viết của chủ hồ sơ cho tab Bài viết; mức Khóa toàn bộ của bài (vẫn lưu, bỏ lưu được) | FR-M02-01.07, FR-M02-05.04, FR-M02-06.02 |
| Cung cấp | M05 | Bookmark kèm thời điểm lưu và việc bỏ lưu, dùng tính Trending Topic/Tag | FR-M02-05.01, FR-M02-06.01 |
| Cung cấp | M14 | Bookmark cho Trending Post nếu OPEN-009 chốt thêm bookmark | FR-M02-05.01 |
| Dùng | M07 | Quan hệ theo dõi để hiện số và danh sách người theo dõi, đang theo dõi; hành động theo dõi và thông báo người theo dõi mới thuộc M07 | FR-M02-02.01, FR-M02-02.02 |
| Dùng | M12 | Tổng điểm, badge đã đạt; nhãn "Tài khoản đã bị khóa" cho tài khoản BANNED | FR-M02-01.09, FR-M02-01.10, FR-M02-01.12 |
| Dùng | M08 | Mức cảnh báo của người dùng, không được hiện trên hồ sơ | FR-M02-01.13 |
| Cung cấp | M03, M04, M16, M01 | Avatar, display_name hiện ở nơi hiển thị tác giả, người gửi tin nhắn và danh sách gợi ý nhắc tên; avatar mặc định khi chưa đặt | FR-M02-04.01, FR-M02-01.18 |
| Dùng | M03 | Trạng thái của bài (đã đăng, nháp, chờ duyệt, bị từ chối, tự ẩn, đã xóa, bị Mod ẩn) để chọn bài hiện ở tab Bài viết và dòng "Nội dung không tồn tại" ở tab Bookmark; thời điểm bài bị xóa hẳn | FR-M02-01.07, FR-M02-01.17, FR-M02-07.03, FR-M02-07.06 |
| Dùng | M11 | Bài đăng ẩn danh; thành viên nhóm Private, để chọn bài hiện ở tab Bài viết và bài đã lưu xem được | FR-M02-01.07, FR-M02-01.17, FR-M02-07.03 |
| Dùng | M08 | Việc xử lý báo cáo người dùng không gồm gỡ avatar, bio (cảnh cáo hoặc khóa như M08) | FR-M02-03.10, FR-M02-04.07 |

### 5.12 AI hỗ trợ và hành vi khi tắt AI

Không áp dụng. Nguồn không giao việc AI nào cho module này.

### 5.13 Yêu cầu HMI

Chưa có — chờ giai đoạn thiết kế.

### 5.14 Chuyển màn hình

Chưa có — chờ giai đoạn thiết kế.

## 6. Lịch sử sửa đổi

| Phiên bản | Ngày | Nội dung | Người sửa |
|---|---|---|---|
| 0.1 | 2026-10-12 | Tạo mới | Phạm Văn Đức |
| 1.0 | 2026-10-13 | Chốt sau 7 bước; câu trả lời bước 6 ghi ở DEC-170–177 | Phạm Văn Đức |

## Phụ lục A. Truy vết

| ID | Nguồn | Căn cứ | Ghi chú |
|---|---|---|---|
| FR-M02-01 | DEC-023, DEC-024, DEC-038, DEC-170, DEC-171, DEC-173, DEC-175, DEC-176, DEC-025, DEC-028, DEC-022, DEC-021, DEC-122, QA-018, QA-067, QA-034, DM-1.2, DM-3.3 | Nói thẳng | — |
| FR-M02-01.01 | DEC-023, QA-018, DEC-122 | Suy ra | Hồ sơ của DEACTIVATED, DELETED bị thay (BR-M02-15), BANNED vẫn hiện (BR-M02-16) ⇒ hồ sơ hiện với ACTIVE và BANNED |
| FR-M02-01.02 | QA-067, DEC-025, DEC-028, DEC-173 | Nói thẳng | — |
| FR-M02-01.03 | DEC-021 | Nói thẳng | — |
| FR-M02-01.04 | DEC-022 | Nói thẳng | — |
| FR-M02-01.05 | DEC-023, DEC-024, DEC-170 | Nói thẳng | — |
| FR-M02-01.06 | DEC-023, DEC-024 | Nói thẳng | — |
| FR-M02-01.07 | DEC-175 | Nói thẳng | — |
| FR-M02-01.08 | DEC-038 | Nói thẳng | Nội dung và việc khôi phục thuộc M03 |
| FR-M02-01.09 | DEC-121 | Nói thẳng | — |
| FR-M02-01.10 | QA-207 | Nói thẳng | — |
| FR-M02-01.11 | QA-018 | Nói thẳng | — |
| FR-M02-01.12 | DEC-122 | Nói thẳng | — |
| FR-M02-01.13 | DEC-079 | Nói thẳng | — |
| FR-M02-01.14 | DEC-026 | Nói thẳng | — |
| FR-M02-01.15 | DEC-027 | Nói thẳng | — |
| FR-M02-01.16 | DEC-171 | Nói thẳng | — |
| FR-M02-01.17 | DEC-175 | Nói thẳng | — |
| FR-M02-01.18 | DEC-176 | Nói thẳng | Hình thức chốt ở giai đoạn thiết kế |
| FR-M02-01.19 | DEC-176 | Nói thẳng | — |
| FR-M02-01.20 | DEC-176 | Nói thẳng | — |
| FR-M02-01.21 | DEC-176 | Nói thẳng | Gồm username cũ đã đổi mà chưa ai lấy |
| FR-M02-01.22 | DEC-176 | Nói thẳng | — |
| FR-M02-01.23 | DEC-173 | Nói thẳng | — |
| FR-M02-02 | DEC-025, DEC-171, DEC-172, DEC-176, QA-067, DM-1.2 | Nói thẳng | — |
| FR-M02-02.01 | DEC-025, DEC-171, QA-067 | Nói thẳng | — |
| FR-M02-02.02 | DEC-025, DEC-172, QA-067 | Nói thẳng | — |
| FR-M02-02.03 | DEC-025, DEC-171 | Nói thẳng | — |
| FR-M02-02.04 | QA-018 | Suy ra | Nội dung hồ sơ bị thay bằng "người dùng không tồn tại" ⇒ không có danh sách |
| FR-M02-02.05 | DEC-171 | Nói thẳng | Số người theo dõi, đang theo dõi vẫn hiện cho Guest |
| FR-M02-02.06 | DEC-172 | Nói thẳng | — |
| FR-M02-02.07 | DEC-172 | Nói thẳng | — |
| FR-M02-02.08 | DEC-172 | Nói thẳng | — |
| FR-M02-02.09 | DEC-176 | Nói thẳng | — |
| FR-M02-03 | DEC-022, DEC-023, DEC-148, DEC-176, DEC-177, QA-034, QA-074, DM-1.2, DM-3.3, GL:Lớp/Khối | Nói thẳng | Đổi username, display_name ở trang này theo quy tắc M01 (DEC-148) |
| FR-M02-03.01 | DEC-023, DEC-148, DEC-022, QA-034 | Nói thẳng | Đổi username, display_name theo FR-M01-03.15, FR-M01-03.16 |
| FR-M02-03.02 | DEC-022, QA-034 | Nói thẳng | — |
| FR-M02-03.03 | DEC-022 | Nói thẳng | — |
| FR-M02-03.04 | DEC-022 | Suy ra | "UI character limit: 155" ⇒ 156 ký tự trở lên bị từ chối |
| FR-M02-03.05 | DEC-022 | Nói thẳng | "Optional" |
| FR-M02-03.06 | QA-034, DM-1.2 | Suy ra | Lớp/Khối chỉ có ba giá trị 10, 11, 12 ⇒ giá trị khác bị từ chối |
| FR-M02-03.07 | QA-034, DM-1.2 | Nói thẳng | Tùy chọn |
| FR-M02-03.08 | QA-034 | Nói thẳng | — |
| FR-M02-03.09 | DEC-151 | Nói thẳng | — |
| FR-M02-03.10 | DEC-023, DEC-177 | Suy ra | Nút sửa hồ sơ chỉ hiện cho chủ hồ sơ; DEC-177: Mod, Admin không gỡ, không sửa |
| FR-M02-03.11 | DEC-176 | Nói thẳng | — |
| FR-M02-03.12 | DEC-176 | Nói thẳng | — |
| FR-M02-03.13 | DEC-176 | Nói thẳng | — |
| FR-M02-03.14 | DEC-176 | Nói thẳng | — |
| FR-M02-03.15 | DEC-176 | Nói thẳng | — |
| FR-M02-04 | DEC-021, DEC-035, DEC-177, QA-087, QA-071, QA-072 | Nói thẳng | — |
| FR-M02-04.01 | DEC-021, QA-087 | Nói thẳng | — |
| FR-M02-04.02 | DEC-021 | Nói thẳng | — |
| FR-M02-04.03 | DEC-021, QA-072 | Suy ra | "Allowed types: JPEG, PNG, WebP only" ⇒ loại khác bị từ chối |
| FR-M02-04.04 | DEC-021, QA-087 | Suy ra | "Max size: 5 MB" ⇒ lớn hơn bị từ chối |
| FR-M02-04.05 | DEC-021, QA-071 | Nói thẳng | — |
| FR-M02-04.06 | DEC-151 | Nói thẳng | Avatar là thông tin hồ sơ |
| FR-M02-04.07 | DEC-023, DEC-177 | Suy ra | Nút sửa hồ sơ chỉ hiện cho chủ hồ sơ; DEC-177: Mod, Admin không gỡ avatar |
| FR-M02-05 | DM-4.4, QA-127 | Nói thẳng | — |
| FR-M02-05.01 | DM-4.4 | Nói thẳng | — |
| FR-M02-05.02 | DEC-126 | Nói thẳng | — |
| FR-M02-05.03 | DM-4.4 | Suy ra | Chỉ có Bookmark và Unbookmark ⇒ một bài hoặc đang được lưu hoặc không |
| FR-M02-05.04 | DEC-167 | Nói thẳng | Cùng hành vi với FR-M03-14.12 |
| FR-M02-05.05 | QA-127 | Nói thẳng | — |
| FR-M02-06 | DM-4.4 | Nói thẳng | — |
| FR-M02-06.01 | DM-4.4 | Nói thẳng | — |
| FR-M02-06.02 | DEC-167 | Nói thẳng | — |
| FR-M02-07 | DM-4.4, DEC-023, DEC-024, DEC-170, DEC-174, DEC-176 | Nói thẳng | — |
| FR-M02-07.01 | DM-4.4, DEC-023, DEC-024, DEC-170 | Nói thẳng | — |
| FR-M02-07.02 | DEC-023, DEC-024 | Suy ra | Người xem chỉ thấy tab Bài viết ⇒ danh sách bài đã lưu chỉ chủ hồ sơ xem được |
| FR-M02-07.03 | DEC-174 | Nói thẳng | — |
| FR-M02-07.04 | DEC-174 | Nói thẳng | — |
| FR-M02-07.05 | DEC-174 | Nói thẳng | — |
| FR-M02-07.06 | DEC-174 | Nói thẳng | — |
| FR-M02-07.07 | DEC-176 | Nói thẳng | — |
| BR-M02-01 | DEC-023 | Nói thẳng | — |
| BR-M02-02 | QA-067, DEC-025, DEC-028, DEC-173 | Nói thẳng | — |
| BR-M02-03 | DEC-023, DEC-024, DEC-170 | Nói thẳng | — |
| BR-M02-04 | DEC-022 | Nói thẳng | — |
| BR-M02-05 | DEC-022 | Nói thẳng | — |
| BR-M02-06 | DEC-021, QA-087, DEC-035, QA-072 | Nói thẳng | — |
| BR-M02-07 | DEC-021, QA-071 | Nói thẳng | — |
| BR-M02-08 | DEC-021 | Nói thẳng | — |
| BR-M02-09 | QA-034, DM-1.2, DM-3.3, GL:Lớp/Khối, DEC-176 | Nói thẳng | — |
| BR-M02-10 | QA-034 | Nói thẳng | — |
| BR-M02-11 | DEC-028 | Nói thẳng | — |
| BR-M02-12 | DEC-121 | Nói thẳng | — |
| BR-M02-13 | QA-207 | Nói thẳng | — |
| BR-M02-14 | DEC-025, DEC-171 | Suy ra | "Full list public (no privacy restriction)" ⇒ không có tùy chọn ẩn danh sách |
| BR-M02-15 | QA-018 | Nói thẳng | Ví dụ kích hoạt lại thì hồ sơ hiện lại: quy tắc chỉ áp cho DEACTIVATED, DELETED |
| BR-M02-16 | DEC-122 | Nói thẳng | — |
| BR-M02-17 | DEC-079 | Nói thẳng | — |
| BR-M02-18 | DEC-151 | Nói thẳng | — |
| BR-M02-19 | DEC-026 | Nói thẳng | — |
| BR-M02-20 | DEC-027 | Nói thẳng | — |
| BR-M02-21 | DM-4.4, QA-127 | Nói thẳng | — |
| BR-M02-22 | DM-4.4 | Suy ra | Draft chỉ có Bookmark và Unbookmark ⇒ một bài hoặc đang được lưu hoặc không |
| BR-M02-23 | DEC-023, DEC-024 | Suy ra | Người xem chỉ thấy tab Bài viết ⇒ tab Bookmark chỉ chủ hồ sơ thấy |
| BR-M02-24 | DEC-126 | Nói thẳng | — |
| BR-M02-25 | DEC-167 | Nói thẳng | — |
| BR-M02-26 | DEC-171 | Nói thẳng | — |
| BR-M02-27 | DEC-172 | Nói thẳng | — |
| BR-M02-28 | DEC-175 | Nói thẳng | — |
| BR-M02-29 | DEC-174 | Nói thẳng | — |
| BR-M02-30 | DEC-174 | Nói thẳng | Mốc 7 × 24 giờ theo DEC-162 (M03) |
| BR-M02-31 | DEC-176 | Nói thẳng | — |
| BR-M02-32 | DEC-176 | Nói thẳng | — |
| BR-M02-33 | DEC-176 | Nói thẳng | — |
| BR-M02-34 | DEC-176 | Nói thẳng | — |
| BR-M02-35 | DEC-176 | Nói thẳng | — |
| BR-M02-36 | DEC-177 | Nói thẳng | — |

## Phụ lục B. Câu hỏi, giả định và TBD

### B.1 Câu hỏi đã hỏi

| Mã | Loại | Câu hỏi | Trả lời | Ghi vào register |
|---|---|---|---|---|
| Q-01 | Mâu thuẫn | DEC-023, DEC-024 nêu tab của chủ hồ sơ chỉ gồm Bài viết + Bookmark; DEC-038 (M03) đặt thêm tab "Đã xóa" trên hồ sơ để tác giả khôi phục bài trong 7 ngày. Chủ hồ sơ có ba tab (Bài viết, Bookmark, Đã xóa) hay "Đã xóa" nằm ở chỗ khác? Đề xuất: ba tab, mặc định Bài viết. | A — bổ sung tab "Đã xóa": chủ hồ sơ có ba tab Bài viết, Bookmark, Đã xóa (mặc định Bài viết); người xem chỉ thấy Bài viết. | ISS-274, QA-334, DEC-170 |
| Q-02 | Thiếu chi tiết | Guest (chưa đăng nhập) có xem được trang hồ sơ (thông tin hồ sơ, tab Bài viết) và danh sách người theo dõi, đang theo dõi của một người dùng không? Đề xuất: được xem, chỉ đọc. | Guest xem được trang hồ sơ, chỉ đọc; mở danh sách theo dõi phải đăng nhập (con số vẫn hiện). | ISS-275, QA-335, DEC-171 |
| Q-03 | Mơ hồ | Danh sách "đang theo dõi" trên hồ sơ gồm những gì: chỉ người dùng, hay cả Topic và bài viết đang theo dõi? Tài khoản DEACTIVATED, BANNED có hiện và có được đếm trong danh sách người theo dõi, đang theo dõi không? Đề xuất: chỉ người dùng; DEACTIVATED không hiện, không đếm; BANNED hiện kèm nhãn và được đếm. | Chỉ tính người dùng; tài khoản DEACTIVATED, BANNED không hiện, không đếm, trở lại ACTIVE thì hiện lại. | ISS-276, QA-336, DEC-172 |
| Q-04 | Mơ hồ | QA-067 liệt kê thông tin trên hồ sơ, không có Lớp/Khối, ngày tham gia, stars nhận, stars cho; draft DM-1.2 có. Hồ sơ có hiện các mục này không? Đề xuất: hiện Lớp/Khối (khi đã đặt) và ngày tham gia; không hiện stars nhận, stars cho ở MS1. | A — hiện Lớp/Khối (khi đã đặt) và ngày tham gia; không hiện stars nhận, stars cho. | ISS-277, QA-337, DEC-173 |
| Q-05 | Mơ hồ | QA-034 nói hệ thống "có thể" gửi thông báo nhắc cập nhật Lớp/Khối đầu năm học. Có làm không? Đề xuất: không làm ở MS1, vì danh sách sự kiện thông báo DEC-065 không có sự kiện này. | Không làm ở MS1. | ISS-280, QA-340, DEC-176 |
| Q-06 | Thiếu chi tiết | Bài đã lưu sau đó không còn xem được (tác giả xóa rồi khôi phục, Mod ẩn, tác giả vô hiệu hóa tài khoản) thì tab Bookmark hiện thế nào? Đề xuất: bookmark được giữ; bài không hiện trong tab khi không xem được và hiện lại khi xem được trở lại. | B — giữ bookmark, hiện "Nội dung không tồn tại" ở vị trí cũ, bỏ lưu được; bài xóa hẳn hoặc tác giả DELETED thì bookmark bị xóa. | ISS-278, QA-338, DEC-174 |
| Q-07 | Thiếu chi tiết | Thứ tự sắp xếp của tab Bài viết, tab Bookmark và danh sách người theo dõi, đang theo dõi. Đề xuất: mới nhất trước (theo thời điểm đăng, thời điểm lưu, thời điểm bắt đầu theo dõi). | Mới nhất trước cho mọi danh sách. | ISS-280, QA-340, DEC-176 |
| Q-08 | Thiếu chi tiết | Người dùng chưa đặt avatar thì hồ sơ hiện gì? Đề xuất: avatar mặc định, cùng loại avatar mặc định đã dùng cho tài khoản đã xóa (DEC-149). | Avatar mặc định; hình thức (ảnh chung hoặc chữ cái đầu display_name) chốt ở thiết kế; tài khoản đã xóa dùng ảnh chung. | ISS-280, QA-340, DEC-176 |
| Q-09 | Thiếu chi tiết | Bio: được xuống dòng, emoji không và đếm thế nào; khoảng trắng đầu cuối có bị cắt không? Lớp/Khối đã đặt có bỏ chọn về trống được không? Đề xuất: cắt khoảng trắng đầu cuối như display_name (DEC-148), bio chỉ có khoảng trắng coi như trống; mỗi emoji, mỗi lần xuống dòng tính một ký tự; Lớp/Khối bỏ chọn được vì không bắt buộc. | Cắt khoảng trắng đầu cuối; emoji, xuống dòng tính một ký tự; Lớp/Khối bỏ chọn được. | ISS-280, QA-340, DEC-176 |
| Q-10 | Thiếu chi tiết | Mở /u/{username} gõ khác hoa thường; mở địa chỉ theo username cũ sau khi người dùng đổi username; mở username không tồn tại: hiện gì? Đề xuất: không phân biệt hoa thường (DEC-148); địa chỉ cũ không chuyển hướng, hiện "người dùng không tồn tại" nếu chưa ai lấy username đó; username không tồn tại cũng hiện "người dùng không tồn tại". | Theo đề xuất. | ISS-280, QA-340, DEC-176 |
| Q-11 | Thiếu chi tiết | Tab Bài viết hiện những bài nào? Với chủ hồ sơ: có hiện bài nháp, chờ duyệt, bị từ chối, tự ẩn của mình không? Với người xem: bài đăng ẩn danh trong nhóm, bài trong nhóm Private có hiện không? Đề xuất: người xem chỉ thấy bài đã đăng, không bị ẩn, không đăng ẩn danh, bài nhóm Private chỉ hiện với thành viên nhóm đó; chủ hồ sơ thấy thêm bài nháp, chờ duyệt, bị từ chối, tự ẩn của mình (M03 cho tác giả xem các bài này nhưng chưa nêu xem ở đâu). | A — người xem thấy bài công khai không ẩn danh, bài nhóm Private chỉ với thành viên; chủ hồ sơ thấy thêm nháp, chờ duyệt, bị từ chối, tự ẩn, bài ẩn danh của mình (có dấu). | ISS-279, QA-339, DEC-175 |

### B.2 TBD

| ID | Nội dung | Ảnh hưởng | Lý do chưa chốt |
|---|---|---|---|

<!-- Bước 2: không OPEN nào sinh TBD cho M02. OPEN-008: phần còn mở (email liên hệ, cách nhận bản sao dữ liệu) thuộc M01 và triển khai. OPEN-009: công thức Trending Post thuộc M14; M02 cung cấp bookmark dù kết quả ra sao. -->

### B.3 Cần cân nhắc (ngoài dữ liệu hiện có)

| Mã | Điểm cần cân nhắc | Vì sao cần | Quyết định |
|---|---|---|---|
| CC-01 | Mở rộng phạm vi: khi xử lý báo cáo một người dùng, Mod/Admin có được gỡ avatar hoặc bio vi phạm (đưa về avatar mặc định, bio trống) không? | Chạm an toàn nội dung: avatar, bio hiện công khai trên hồ sơ; DEC-072 cho báo cáo User (Quấy rối, Khác) nhưng hình phạt chỉ là cảnh cáo hoặc khóa, không có cách gỡ ảnh hay chữ vi phạm, và chỉ chủ hồ sơ sửa được (DEC-023). | Không làm ở MS1 (ISS-281, QA-341, DEC-177). |

## Phụ lục C. Sổ nguồn

**Owner keywords:** M02, User Profile, profile, profiles, hồ sơ, trang cá nhân, avatar, ảnh đại diện, bio, /u/, dual-context, Edit Profile, sửa hồ sơ, bookmark, bookmarks, lưu bài, followers, follower, người theo dõi, follow scope, social links, username change history, lịch sử đổi username, Identity Fields, Reputation score của user, thanh tiến độ, personalization tab, Lớp/Khối của user
**Dependency keywords:** username, display_name, follow, theo dõi, points, điểm, badge, huy hiệu, Lớp/Khối, grade_level, Cloudinary, post, bài viết, DEACTIVATED, DELETED, BANNED, guest, stats, thống kê, Đã xóa
**Mục draft của module:** DM-1.2, DM-4.4
**Loại khỏi bảng nguồn (khớp nhầm):** ISS-155, QA-211, QA-212 (avatar "đã xem" trong chat — M16); DEC-141 (người theo dõi Topic — M05)

### C.1 Bảng nguồn

| Nguồn | Nhãn | Trạng thái | Dùng ở | Ghi chú |
|---|---|---|---|---|
| DEC-021 | Sở hữu | Hiện hành | FR-M02-01, FR-M02-01.03, FR-M02-04, FR-M02-04.01, FR-M02-04.02, FR-M02-04.03, FR-M02-04.04, FR-M02-04.05, BR-M02-06, BR-M02-07, BR-M02-08 | Nhóm A. Avatar: nơi lưu ảnh, loại tệp, kích thước 5 MB, xóa ảnh cũ khi thay, cắt tròn khi hiển thị. |
| DEC-022 | Sở hữu | Hiện hành | FR-M02-01, FR-M02-01.04, FR-M02-03, FR-M02-03.01, FR-M02-03.02, FR-M02-03.03, FR-M02-03.04, FR-M02-03.05, BR-M02-04, BR-M02-05 | Nhóm A. Bio: giới hạn 155 ký tự, có bộ đếm, tùy chọn, bio trống không hiện gì. |
| DEC-023 | Sở hữu | Sửa một phần bởi DEC-170 | FR-M02-01, FR-M02-01.01, FR-M02-01.05, FR-M02-01.06, FR-M02-03, FR-M02-03.01, FR-M02-03.10, FR-M02-04.07, FR-M02-07, FR-M02-07.01, FR-M02-07.02, BR-M02-01, BR-M02-03, BR-M02-23 | Nhóm A. Một địa chỉ /u/{username}, hai ngữ cảnh chủ hồ sơ và người xem. Chỉ phần tab của chủ hồ sơ; địa chỉ, hai ngữ cảnh còn hiệu lực |
| DEC-024 | Sở hữu | Sửa một phần bởi DEC-170 | FR-M02-01, FR-M02-01.05, FR-M02-01.06, FR-M02-07, FR-M02-07.01, FR-M02-07.02, BR-M02-03, BR-M02-23 | Nhóm A. Tab nội dung: chủ hồ sơ Bài viết + Bookmark (mặc định Bài viết); người xem chỉ Bài viết. |
| DEC-025 | Sở hữu | Sửa một phần bởi DEC-171, DEC-172 | FR-M02-01, FR-M02-01.02, FR-M02-02, FR-M02-02.01, FR-M02-02.02, FR-M02-02.03, BR-M02-02, BR-M02-14 | Nhóm A. Số followers/following hiện trên hồ sơ; danh sách công khai. |
| DEC-026 | Sở hữu | Hiện hành | FR-M02-01.14, BR-M02-19 | Nhóm A. Không hiện lịch sử đổi username (ngoài phạm vi). |
| DEC-027 | Sở hữu | Hiện hành | FR-M02-01.15, BR-M02-20 | Nhóm A. Liên kết mạng xã hội bị bỏ ở v1 (ngoài phạm vi). |
| DEC-028 | Sở hữu | Hiện hành | FR-M02-01, FR-M02-01.02, BR-M02-02, BR-M02-11 | Nhóm A. Điểm và badge chỉ hiển thị trên hồ sơ; M12 tính. |
| DEC-170 | Sở hữu | Hiện hành | FR-M02-01, FR-M02-01.05, FR-M02-07, FR-M02-07.01, BR-M02-03 | Nhóm A. Tab của chủ hồ sơ: Bài viết, Bookmark, Đã xóa. |
| DEC-171 | Sở hữu | Hiện hành | FR-M02-01, FR-M02-01.16, FR-M02-02, FR-M02-02.01, FR-M02-02.03, FR-M02-02.05, BR-M02-14, BR-M02-26 | Nhóm A. Guest xem hồ sơ chỉ đọc; danh sách theo dõi cần đăng nhập. |
| DEC-172 | Sở hữu | Hiện hành | FR-M02-02, FR-M02-02.02, FR-M02-02.06, FR-M02-02.07, FR-M02-02.08, BR-M02-27 | Nhóm A. Danh sách theo dõi chỉ người dùng; ẩn DEACTIVATED, BANNED. |
| DEC-173 | Sở hữu | Hiện hành | FR-M02-01, FR-M02-01.02, FR-M02-01.23, BR-M02-02 | Nhóm A. Thêm Lớp/Khối, ngày tham gia; không hiện stars. |
| DEC-174 | Sở hữu | Hiện hành | FR-M02-07, FR-M02-07.03, FR-M02-07.04, FR-M02-07.05, FR-M02-07.06, BR-M02-29, BR-M02-30 | Nhóm A. Bookmark của bài không còn xem được. |
| DEC-175 | Sở hữu | Hiện hành | FR-M02-01, FR-M02-01.07, FR-M02-01.17, BR-M02-28 | Nhóm A. Bài hiện ở tab Bài viết theo người xem. |
| DEC-176 | Sở hữu | Hiện hành | FR-M02-01, FR-M02-01.18, FR-M02-01.19, FR-M02-01.20, FR-M02-01.21, FR-M02-01.22, FR-M02-02, FR-M02-02.09, FR-M02-03, FR-M02-03.11, FR-M02-03.12, FR-M02-03.13, FR-M02-03.14, FR-M02-03.15, FR-M02-07, FR-M02-07.07, BR-M02-09, BR-M02-31, BR-M02-32, BR-M02-33, BR-M02-34, BR-M02-35 | Nhóm A. Chi tiết hồ sơ: nhắc Lớp/Khối, thứ tự, avatar mặc định, bio, địa chỉ /u/. |
| DEC-177 | Sở hữu | Hiện hành | FR-M02-03, FR-M02-03.10, FR-M02-04, FR-M02-04.07, BR-M02-36 | Nhóm A. Mod, Admin không gỡ avatar, bio. |
| DM-1.2 | Sở hữu | Sửa một phần bởi DEC-125 | FR-M02-01, FR-M02-02, FR-M02-03, FR-M02-03.06, FR-M02-03.07, BR-M02-09 | Nhóm A. Draft trường hồ sơ. Username thuộc M01; stars, reputation, badge do M12 tính; Lớp/Khối, joined date chỉ draft nêu. Phần "cá nhân hóa feed" của Lớp/Khối |
| DM-4.4 | Sở hữu | Hiện hành | FR-M02-05, FR-M02-05.01, FR-M02-05.03, FR-M02-06, FR-M02-06.01, FR-M02-07, FR-M02-07.01, BR-M02-21, BR-M02-22 | Nhóm A. Bookmark: lưu, bỏ lưu, danh sách Bookmark của tôi. Draft xếp ở Interaction, register đặt tab Bookmark ở hồ sơ. |
| ISS-058 | Nhắc tới | Sửa một phần bởi QA-087 | Không áp dụng: Câu hỏi avatar; ghi 10 MB, đã có DEC-021 | Nhóm A. Câu hỏi avatar; ghi 10 MB, đã có DEC-021. 10 MB → 5 MB |
| ISS-059 | Nhắc tới | Trùng với DEC-025 | — | Nhóm A. Câu hỏi hiển thị followers/following; đã có DEC-025. |
| ISS-060 | Nhắc tới | Trùng với DEC-026 | — | Nhóm A. Câu hỏi lịch sử đổi username; đã có DEC-026. |
| ISS-061 | Nhắc tới | Trùng với DEC-022, DEC-023 | — | Nhóm A. Câu hỏi bio và địa chỉ hồ sơ; đã có DEC-022, DEC-023. |
| ISS-274 | Nhắc tới | Trùng với DEC-170 | — | Nhóm A. Câu hỏi bước 6 FR M02; đã có DEC-170. |
| ISS-275 | Nhắc tới | Trùng với DEC-171 | — | Nhóm A. Câu hỏi bước 6 FR M02; đã có DEC-171. |
| ISS-276 | Nhắc tới | Trùng với DEC-172 | — | Nhóm A. Câu hỏi bước 6 FR M02; đã có DEC-172. |
| ISS-277 | Nhắc tới | Trùng với DEC-173 | — | Nhóm A. Câu hỏi bước 6 FR M02; đã có DEC-173. |
| ISS-278 | Nhắc tới | Trùng với DEC-174 | — | Nhóm A. Câu hỏi bước 6 FR M02; đã có DEC-174. |
| ISS-279 | Nhắc tới | Trùng với DEC-175 | — | Nhóm A. Câu hỏi bước 6 FR M02; đã có DEC-175. |
| ISS-280 | Nhắc tới | Trùng với DEC-176 | — | Nhóm A. Câu hỏi bước 6 FR M02; đã có DEC-176. |
| ISS-281 | Nhắc tới | Trùng với DEC-177 | — | Nhóm A. Câu hỏi bước 6 FR M02; đã có DEC-177. |
| QA-067 | Sở hữu | Sửa một phần bởi DEC-173 | FR-M02-01, FR-M02-01.02, FR-M02-02, FR-M02-02.01, FR-M02-02.02, BR-M02-02 | Nhóm A. Các thông tin trên trang hồ sơ. |
| QA-068 | Sở hữu | Trùng với DEC-024 | — | Nhóm A. Tab chủ hồ sơ và người xem. |
| QA-069 | Sở hữu | Trùng với DEC-025 | — | Nhóm A. Danh sách followers/following công khai. |
| QA-070 | Sở hữu | Trùng với DEC-026 | — | Nhóm A. Không có lịch sử đổi username. |
| QA-071 | Sở hữu | Sửa một phần bởi QA-087 | FR-M02-04, FR-M02-04.05, BR-M02-07 | Nhóm A. Avatar: loại tệp, 10 MB, xóa ảnh cũ khi thay. 10 MB → 5 MB; loại tệp, xóa ảnh cũ còn hiệu lực |
| QA-072 | Sở hữu | Hiện hành | FR-M02-04, FR-M02-04.03, BR-M02-06 | Nhóm A. Không nhận ảnh GIF động. |
| QA-073 | Sở hữu | Trùng với DEC-022 | — | Nhóm A. Bio 155 ký tự. |
| QA-074 | Sở hữu | Hiện hành | FR-M02-03 | Nhóm A. Lý do chọn 155 ký tự. |
| QA-075 | Sở hữu | Trùng với DEC-023 | — | Nhóm A. Một địa chỉ, hai ngữ cảnh. |
| QA-076 | Sở hữu | Trùng với DEC-027 | — | Nhóm A. Bỏ liên kết mạng xã hội, kèm lý do. |
| QA-077 | Sở hữu | Trùng với DEC-028 | — | Nhóm A. Điểm, badge chỉ hiển thị; M12 tính. |
| QA-334 | Sở hữu | Trùng với DEC-170 | — | Nhóm A. Câu trả lời của stakeholder cho ISS-274. |
| QA-335 | Sở hữu | Trùng với DEC-171 | — | Nhóm A. Câu trả lời của stakeholder cho ISS-275. |
| QA-336 | Sở hữu | Trùng với DEC-172 | — | Nhóm A. Câu trả lời của stakeholder cho ISS-276. |
| QA-337 | Sở hữu | Trùng với DEC-173 | — | Nhóm A. Câu trả lời của stakeholder cho ISS-277. |
| QA-338 | Sở hữu | Trùng với DEC-174 | — | Nhóm A. Câu trả lời của stakeholder cho ISS-278. |
| QA-339 | Sở hữu | Trùng với DEC-175 | — | Nhóm A. Câu trả lời của stakeholder cho ISS-279. |
| QA-340 | Sở hữu | Trùng với DEC-176 | — | Nhóm A. Câu trả lời của stakeholder cho ISS-280. |
| QA-341 | Sở hữu | Trùng với DEC-177 | — | Nhóm A. Câu trả lời của stakeholder cho ISS-281. |
| MR-M02 | Sở hữu | Sửa một phần bởi DEC-021, DEC-170 | Không áp dụng: dòng tóm tắt module; nội dung đã có ở DEC-021–028, DEC-170–177 | Nhóm A. Dòng module; ghi avatar 10 MB; cột MoSCoW lệch. 10 MB → 5 MB; FR M02 DEC-170–177 |
| DEC-014 | Phụ thuộc | Hiện hành | Chuyển M01 | Nhóm B. M01: bước 3 đăng ký cho nhập bio, Lớp/Khối, avatar (bỏ qua được); quy tắc trường thuộc M02. |
| DEC-015 | Phụ thuộc | Sửa một phần bởi DEC-148 | Chuyển M01 | Nhóm B. M01: display_name hiện ở mọi nơi, username không là danh tính chính. |
| DEC-019 | Phụ thuộc | Sửa một phần bởi DEC-148, DEC-149, DEC-156 | Chuyển M01 | Nhóm B. M01: vô hiệu hóa; avatar thay bằng ảnh giữ chỗ ở bình luận. |
| DEC-020 | Nhắc tới | Sửa một phần bởi DEC-153 | Không áp dụng: M01: avatar trong danh sách gợi ý nhắc tên | Nhóm B. M01: avatar trong danh sách gợi ý nhắc tên. |
| DEC-035 | Sở hữu | Hiện hành | FR-M02-04, BR-M02-06 | Nhóm B. M03 section nhưng sửa kích thước avatar thành 5 MB (cùng ảnh đính kèm). |
| DEC-038 | Sở hữu | Hiện hành | FR-M02-01, FR-M02-01.08 | Nhóm B. M03 section; tab "Đã xóa" trên hồ sơ để tác giả khôi phục bài. Hành vi khôi phục thuộc M03. DEC-162 sửa phần khôi phục, thuộc M03 |
| DEC-052 | Nhắc tới | Sửa một phần bởi DEC-145 | Không áp dụng: M05: công thức cũ; bookmark chỉ có trong ghi chú sửa đổi DEC-145 | Nhóm B. M05: công thức cũ; bookmark chỉ có trong ghi chú sửa đổi DEC-145. Công thức bị thay |
| DEC-065 | Phụ thuộc | Sửa một phần bởi DEC-151 | Chuyển M07 | Nhóm B. M07: thông báo "người theo dõi mới". DEC-147 (ngoài bảng nguồn) cũng sửa; dòng "New follower" không đổi |
| DEC-079 | Phụ thuộc | Sửa một phần bởi DEC-122, QA-199 | FR-M02-01.13, BR-M02-17 | Nhóm B. M08: mức cảnh báo không bao giờ hiện trên hồ sơ. DEC-118, DEC-163 (ngoài bảng nguồn) cũng sửa; phần không hiện cảnh báo trên hồ sơ còn hiệu lực |
| DEC-121 | Phụ thuộc | Hiện hành | FR-M02-01.09, BR-M02-12 | Nhóm B. M12: tổng điểm trên hồ sơ của chính người dùng cập nhật tức thì. |
| DEC-122 | Sở hữu | Hiện hành | FR-M02-01, FR-M02-01.01, FR-M02-01.12, BR-M02-16 | Nhóm B. M12 section; hồ sơ tài khoản BANNED vẫn hiện bình thường, kèm nhãn "Tài khoản đã bị khóa". |
| DEC-125 | Phụ thuộc | Hiện hành | Không áp dụng: M14 bỏ feed cá nhân hóa; ghi ở C.2 | Nhóm B. M14: không có feed cá nhân hóa; Lớp/Khối trên hồ sơ không còn dùng xếp feed. |
| DEC-126 | Phụ thuộc | Hiện hành | FR-M02-05.02, BR-M02-24 | Nhóm B. M14: Guest phải đăng nhập để bookmark, follow. |
| DEC-145 | Phụ thuộc | Hiện hành | Chuyển M05 | Nhóm B. M05: bookmark là tương tác tính Trending; bookmark đã bỏ không tính. |
| DEC-148 | Phụ thuộc | Hiện hành | FR-M02-03, FR-M02-03.01 | Nhóm B. M01: đổi username, display_name ở trang sửa hồ sơ (M02), quy tắc thuộc M01. |
| DEC-149 | Phụ thuộc | Hiện hành | Chuyển M01 | Nhóm B. M01: avatar mặc định cho bình luận của tài khoản DELETED. |
| DEC-151 | Phụ thuộc | Hiện hành | FR-M02-03.09, FR-M02-04.06, BR-M02-18 | Nhóm B. M01: chỉ đổi thông tin hồ sơ khi tài khoản ACTIVE. |
| DEC-153 | Phụ thuộc | Hiện hành | Chuyển M01 | Nhóm B. M01: lượt nhắc tới tài khoản DEACTIVATED, DELETED không dẫn tới hồ sơ. |
| DEC-154 | Nhắc tới | Hiện hành | Không áp dụng: M01: trang chính sách nêu nhóm dữ liệu hồ sơ, bookmark | Nhóm B. M01: trang chính sách nêu nhóm dữ liệu hồ sơ, bookmark. |
| DEC-156 | Phụ thuộc | Sửa một phần bởi DEC-159 | Chuyển M01 | Nhóm B. M01: khi DELETED xóa display_name, avatar, bio, Lớp/Khối, bookmark, quan hệ theo dõi. |
| DEC-159 | Phụ thuộc | Hiện hành | Chuyển M01 | Nhóm B. M01/M05: khi DELETED xóa mọi lượt theo dõi; số người theo dõi giảm theo. |
| DEC-167 | Phụ thuộc | Hiện hành | FR-M02-05.04, FR-M02-06.02, BR-M02-25 | Nhóm B. M03: bài Khóa toàn bộ vẫn bookmark được. |
| DG-4 | Nhắc tới | Hiện hành | Không áp dụng: Bản đồ module: hồ sơ ở nhóm User; Bookmark, Follow ở nhóm Interaction | Nhóm B. Bản đồ module: hồ sơ ở nhóm User; Bookmark, Follow ở nhóm Interaction. |
| DG-5 | Nhắc tới | Sửa một phần bởi DEC-125 | Không áp dụng: Lớp/Khối gắn Profile để cá nhân hóa feed (M14) | Nhóm B. Lớp/Khối gắn Profile để cá nhân hóa feed (M14). Phần feed cá nhân hóa theo Lớp/Khối |
| DM-3.3 | Sở hữu | Sửa một phần bởi DEC-125 | FR-M02-01, FR-M02-03, BR-M02-09 | Nhóm B. Lớp/Khối tùy chọn trên hồ sơ; phần trên bài thuộc M03. Phần Personalized Feed |
| DM-7.1 | Nhắc tới | Bị thay bởi DEC-125 | — | Nhóm B. Draft feed Personalized theo Lớp/Khối của user (M14). |
| DM-7.2 | Nhắc tới | Hiện hành | Không áp dụng: M14/M05: Trending dựa trên Bookmarks | Nhóm B. M14/M05: Trending dựa trên Bookmarks. |
| DM-9.3 | Phụ thuộc | Hiện hành | Chuyển M12 | Nhóm B. M12: thống kê người dùng (followers, following, stars, reputation, badges). |
| DM-x02 | Nhắc tới | Sửa một phần bởi DEC-125 | Không áp dụng: Danh sách phạm vi: Bookmark, Follow | Nhóm B. Danh sách phạm vi: Bookmark, Follow. Feed Personalized |
| GL:Lớp/Khối | Sở hữu | Sửa một phần bởi DEC-125 | FR-M02-03, BR-M02-09 | Nhóm B. Thuật ngữ; phần hồ sơ thuộc M02, phần bài thuộc M03. "Used to personalize feed" |
| ISS-051 | Nhắc tới | Trùng với QA-043 | — | Nhóm B. Câu hỏi phạm vi follow; đã có QA-043. |
| ISS-154 | Nhắc tới | Trùng với DEC-122 | — | Nhóm B. Câu hỏi hiển thị tài khoản BANNED; đã có QA-204, QA-205, DEC-122. |
| OPEN-008 | Nhắc tới | Sửa một phần bởi DEC-154 | Không áp dụng: Privacy; nêu M02 là module chịu ảnh hưởng; phần còn mở (email liên hệ, bản sao dữ liệu) không thuộc M02 | Nhóm B. Privacy; nêu M02 là module chịu ảnh hưởng; phần còn mở (email liên hệ, bản sao dữ liệu) không thuộc M02. DEC-155–157 cũng chốt; phần còn mở không thuộc M02 |
| OPEN-009 | Nhắc tới | Hiện hành | Không áp dụng: M14: Trending Post có tính bookmark không | Nhóm B. M14: Trending Post có tính bookmark không. |
| QA-011 | Phụ thuộc | Sửa một phần bởi DEC-171 | Không áp dụng: quyền Guest với hồ sơ lấy từ DEC-171 | Nhóm B. Quyền Guest: xem Leaderboard, Badges, Reputation của user; INTR không. |
| QA-015 | Nhắc tới | Hiện hành | Không áp dụng: M03/M11: bài ẩn danh; Mod/Admin thấy link hồ sơ tác giả thật | Nhóm B. M03/M11: bài ẩn danh; Mod/Admin thấy link hồ sơ tác giả thật. |
| QA-018 | Sở hữu | Sửa một phần bởi DEC-149, DEC-156 | FR-M02-01, FR-M02-01.01, FR-M02-01.11, FR-M02-02.04, BR-M02-15 | Nhóm B. Hồ sơ của tài khoản DEACTIVATED/DELETED hiện "người dùng không tồn tại"; phần còn lại thuộc M01. Phần hồ sơ "người dùng không tồn tại" còn hiệu lực |
| QA-027 | Sở hữu | Trùng với DEC-038 | — | Nhóm B. M03 section; mục "Bài viết đã xóa" trong hồ sơ. |
| QA-034 | Sở hữu | Sửa một phần bởi DEC-176 | FR-M02-01, FR-M02-03, FR-M02-03.01, FR-M02-03.02, FR-M02-03.06, FR-M02-03.07, FR-M02-03.08, BR-M02-09, BR-M02-10 | Nhóm B. Lớp/Khối trên hồ sơ không tự tăng theo năm, người dùng tự cập nhật; độc lập với Lớp/Khối trên bài. Phần "có thể gửi notification" bị bỏ |
| QA-043 | Phụ thuộc | Hiện hành | Chuyển M07 | Nhóm B. Follow User, Topic, Post; không follow Group. |
| QA-065 | Phụ thuộc | Trùng với DEC-019 | — | Nhóm B. M01/M04: avatar giữ chỗ ở bình luận của tài khoản vô hiệu hóa. |
| QA-087 | Sở hữu | Hiện hành | FR-M02-04, FR-M02-04.01, FR-M02-04.04, BR-M02-06 | Nhóm B. M03 section; avatar giảm còn 5 MB. |
| QA-091 | Sở hữu | Trùng với DEC-038 | — | Nhóm B. M03 section; tác giả thấy tab "Đã xóa" trên hồ sơ. |
| QA-127 | Sở hữu | Hiện hành | FR-M02-05, FR-M02-05.05, BR-M02-21 | Nhóm B. Bookmark chỉ để lưu, không kèm nhận thông báo. |
| QA-199 | Nhắc tới | Hiện hành | Không áp dụng: M12: cảnh báo HEAVY chỉ ảnh hưởng leaderboard | Nhóm B. M12: cảnh báo HEAVY chỉ ảnh hưởng leaderboard. |
| QA-204 | Sở hữu | Trùng với DEC-122 | — | Nhóm B. M12 section; hồ sơ tài khoản BANNED vẫn hiện bình thường cho người khác. |
| QA-205 | Sở hữu | Trùng với DEC-122 | — | Nhóm B. M12 section; nhãn "Tài khoản đã bị khóa" trên trang hồ sơ. |
| QA-207 | Phụ thuộc | Hiện hành | FR-M02-01.10, BR-M02-13 | Nhóm B. M12: chỉ hiện badge đã đạt, không có thanh tiến độ. |
| QA-227 | Phụ thuộc | Trùng với DEC-126 | — | Nhóm B. M14: mọi tương tác (bookmark, follow) cần đăng nhập. |
| QA-236 | Nhắc tới | Hiện hành | Không áp dụng: M14: Trending không loại bài của BANNED | Nhóm B. M14: Trending không loại bài của BANNED. |
| QA-251 | Phụ thuộc | Hiện hành | Không áp dụng: giới hạn avatar đã lấy từ DEC-021 | Nhóm B. Dùng chung: tải tệp không quét virus, chỉ whitelist loại/kích thước; nêu avatar 5 MB. |
| QA-271 | Phụ thuộc | Trùng với DEC-145 | — | Nhóm B. M05: bookmark trọng số 1 trong Trending Topic/Tag. |
| QA-293 | Phụ thuộc | Trùng với DEC-149 | — | Nhóm B. M01/M04: avatar mặc định cho bình luận của tài khoản DELETED. |
| QA-301 | Phụ thuộc | Trùng với DEC-153 | — | Nhóm B. M01: lượt nhắc tới tài khoản DEACTIVATED/DELETED không dẫn sang trang cá nhân. |
| QA-305 | Phụ thuộc | Trùng với DEC-148 | — | Nhóm B. M01: đổi username, display_name ở trang sửa hồ sơ, không giới hạn số lần. |
| QA-309 | Nhắc tới | Trùng với DEC-154 | — | Nhóm B. M01: nhóm dữ liệu "tài khoản và hồ sơ" trên trang chính sách. |
| QA-311 | Phụ thuộc | Trùng với DEC-156 | — | Nhóm B. M01: dữ liệu hồ sơ, bookmark, theo dõi bị xóa khi DELETED. |
| QA-329 | Phụ thuộc | Trùng với DEC-167 | — | Nhóm B. M03: Khóa toàn bộ vẫn cho bookmark. |
| MR-M14 | Nhắc tới | Trùng với DEC-125 | — | Nhóm B. M14: không có tab cá nhân hóa. |
| DEC-162 | Phụ thuộc | Hiện hành | Chuyển M03 | Nhóm C. M03: khôi phục bài, hạn 7 × 24 giờ; bài quá hạn bị xóa hẳn. |
| DEC-127 | Phụ thuộc | Hiện hành | Không áp dụng: ngày tham gia hiển thị theo quy định múi giờ chung, không tạo hành vi riêng của M02 | Nhóm D. Dùng chung: múi giờ cho mọi mốc thời gian (ngày tham gia). |
| DEC-128 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| DEC-129 | Nhắc tới | Sửa một phần bởi DEC-156 | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| DEC-130 | Phụ thuộc | Hiện hành | Không áp dụng: không quét virus là dùng chung, không đổi hành vi M02 | Nhóm D. Dùng chung: tải tệp không quét virus, giữ whitelist loại/kích thước. DEC-160 (ngoài bảng nguồn) sửa phần tài liệu đính kèm bài, không chạm avatar |
| DEC-131 | Nhắc tới | Sửa một phần bởi DEC-154 | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. DEC-146 (ngoài bảng nguồn) cũng sửa |
| DEC-132 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. DEC-141 (loại), DEC-144 (ngoài bảng nguồn) sửa; không chạm M02 |
| DEC-133 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| DEC-134 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| DEC-135 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| DEC-136 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| DEC-137 | Nhắc tới | Hiện hành | Không áp dụng: Công nghệ (Cloudinary) — không phải nghiệp vụ | Nhóm D. Công nghệ (Cloudinary) — không phải nghiệp vụ. |
| DEC-138 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. DEC-155, DEC-157 (ngoài bảng nguồn) sửa phần đồng ý chính sách |
| ISS-189 | Nhắc tới | Trùng với DEC-127 | — | Nhóm D. Dùng chung; không quy định hành vi M02. |
| ISS-190 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| ISS-191 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| ISS-192 | Nhắc tới | Trùng với DEC-130 | — | Nhóm D. Đã có DEC-130, QA-251. |
| ISS-193 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| ISS-194 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| ISS-195 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| ISS-196 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| ISS-197 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| ISS-198 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| ISS-199 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| ISS-200 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| ISS-201 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| ISS-202 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| ISS-203 | Nhắc tới | Trùng với QA-263 | — | Nhóm D. Đã có QA-263. |
| ISS-204 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| QA-248 | Nhắc tới | Trùng với DEC-127 | — | Nhóm D. Dùng chung; không quy định hành vi M02. |
| QA-249 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| QA-250 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| QA-252 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| QA-253 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| QA-254 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| QA-255 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| QA-256 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| QA-257 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| QA-258 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| QA-259 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| QA-260 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| QA-261 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| QA-262 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| QA-263 | Nhắc tới | Hiện hành | Không áp dụng: Công nghệ (Cloudinary) — không phải nghiệp vụ | Nhóm D. Công nghệ (Cloudinary) — không phải nghiệp vụ. |
| QA-264 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| MR-A04 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M02 | Nhóm D. Dùng chung; không quy định hành vi M02. |
| MR-A05 | Nhắc tới | Hiện hành | Không áp dụng: Công nghệ | Nhóm D. Công nghệ. |

### C.2 Chuỗi quyết định

| Chuỗi | Nội dung hiện hành |
|---|---|
| QA-071, ISS-058, MR-M02 → QA-087 → DEC-021, DEC-035 | Avatar tối đa 5 MB (10 MB cũ bị thay, để cùng mức với ảnh đính kèm bài). Loại tệp JPEG, PNG, WebP, không GIF động, xóa ảnh cũ khi thay, hiển thị cắt tròn và lưu ảnh gốc. |
| DEC-023, DEC-024 → DEC-038 → DEC-170 (QA-027, QA-091, QA-334) | Chủ hồ sơ có ba tab Bài viết, Bookmark, Đã xóa, mặc định Bài viết, và nút sửa hồ sơ; người xem chỉ có tab Bài viết. Địa chỉ /u/{username} và hai ngữ cảnh của DEC-023 còn hiệu lực. Nội dung tab Đã xóa và việc khôi phục thuộc M03 (DEC-162). |
| QA-011 → DEC-171; DEC-025 → DEC-171, DEC-172 | Guest xem được trang hồ sơ, chỉ đọc, thấy số người theo dõi, đang theo dõi nhưng phải đăng nhập mới mở danh sách. Người dùng đã đăng nhập xem được danh sách của mọi người, không ẩn được. Danh sách đang theo dõi chỉ gồm người dùng; tài khoản DEACTIVATED, BANNED không hiện, không được đếm, trở lại ACTIVE thì hiện lại. |
| QA-067, DM-1.2 → DEC-173 | Hồ sơ hiện avatar, display_name, username, bio, Lớp/Khối (khi đã đặt), ngày tham gia, điểm, badge, số người theo dõi, số đang theo dõi, các tab; không hiện stars nhận, stars cho. |
| DM-1.2, DM-3.3, DM-7.1, DG-5, GL:Lớp/Khối → DEC-125; QA-034 → DEC-173, DEC-176 | Không có feed cá nhân hóa; Lớp/Khối trên hồ sơ là trường tùy chọn, hiện trên hồ sơ khi đã đặt, người dùng tự sửa hoặc bỏ chọn, không tự tăng theo năm, không có thông báo nhắc cập nhật ở MS1; độc lập với Lớp/Khối trên bài. |
| DEC-022 → DEC-176 | Bio không bắt buộc, tối đa 155 ký tự, có bộ đếm; cắt khoảng trắng đầu cuối trước khi đếm, mỗi emoji, mỗi lần xuống dòng là một ký tự, bio chỉ gồm khoảng trắng là bio trống. |
| DM-4.4 → DEC-174, DEC-176 (QA-127) | Bookmark chỉ để lưu, không kèm thông báo, riêng tư. Bài đã lưu tạm không xem được thì tab Bookmark hiện "Nội dung không tồn tại" ở vị trí cũ, bỏ lưu được, và hiện lại bài khi xem được; bài xóa hẳn hoặc tác giả DELETED thì bookmark bị xóa. Tab xếp theo thời điểm lưu, mới nhất trước. |
| DEC-023, DEC-024 → DEC-175 | Tab Bài viết: người xem thấy bài đã đăng, không bị ẩn, không ẩn danh, bài nhóm Private chỉ với thành viên; chủ hồ sơ thấy thêm nháp, chờ duyệt, bị từ chối, tự ẩn và bài ẩn danh của mình (kèm dấu). Xếp theo thời điểm tạo bài, mới nhất trước. |
| DEC-148 → DEC-176 | /u/{username} không phân biệt hoa thường; địa chỉ theo username cũ không chuyển hướng; địa chỉ không ứng với tài khoản nào hiện "người dùng không tồn tại". Chưa đặt avatar thì hiện avatar mặc định. |
| QA-018 → DEC-019 → DEC-149, DEC-156 → DEC-159 | Hồ sơ tài khoản DEACTIVATED, DELETED hiện "người dùng không tồn tại". Khi DELETED: xóa display_name, avatar, bio, Lớp/Khối, bookmark, mọi lượt theo dõi hai chiều; số người theo dõi giảm theo. |
| DEC-079 → DEC-118, DEC-122, QA-199, DEC-163 (ISS-154, QA-204, QA-205) | Mức cảnh báo không bao giờ hiện trên hồ sơ. Tài khoản BANNED: trang hồ sơ vẫn hiện bình thường kèm nhãn "Tài khoản đã bị khóa", nhưng không có trong danh sách theo dõi của người khác (DEC-172). DEC-118, DEC-163 sửa phần không chạm hồ sơ. |
| DEC-072 → DEC-177 | Báo cáo người dùng được xử lý bằng cảnh cáo hoặc khóa (M08); Mod, Admin không gỡ, không sửa avatar hoặc bio của người khác. |
| DEC-015 → DEC-148 (QA-305) | display_name hiện ở mọi nơi, username không là danh tính chính. Đổi username, display_name ở trang sửa hồ sơ, không giới hạn số lần, theo quy tắc của M01. |
| DEC-052 → DEC-145 (QA-271) | Bookmark là tương tác trọng số 1 trong Trending Topic/Tag; bookmark đã bỏ không tính. |
| DEC-020 → DEC-153 (QA-301) | Lượt nhắc tới tài khoản DEACTIVATED, DELETED không dẫn tới trang hồ sơ. |
| DEC-065 → DEC-151 | Dòng "người theo dõi mới" (in-app, không email) không đổi; DEC-151 chỉ thêm việc đặt lại mật khẩu cũng gửi thông báo "đổi mật khẩu", không chạm M02. |
