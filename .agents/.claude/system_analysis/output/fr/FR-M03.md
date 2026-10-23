---
module: M03
ten_module: Post & Content
ma_tai_lieu: FR-M03
phien_ban: 1.7
trang_thai: Đã chốt
ngay: 2026-10-23
tac_gia: Phạm Văn Đức
moc_nguon: DEC-247, QA-444, ISS-382, OPEN-012
steps_completed: [1, 2, 3, 4, 5, 6, 7]
---
# Tài liệu yêu cầu chức năng — M03 Post & Content

| Mã tài liệu | FR-M03 |
|---|---|
| Dự án | iShare |
| Module | M03 — Post & Content |
| Trạng thái | Đã chốt |
| Phiên bản | 1.7 |
| Ngày | 2026-10-23 |
| Tác giả | Phạm Văn Đức |

<!-- Quy ước chung cho mọi bảng dưới đây:
     - Thân tài liệu không ghi nguồn. Nguồn của mọi ID nằm ở Phụ lục A.
     - Ô không có nội dung ghi "—". Không xóa cột.
     - Mục chưa tới bước làm thì để dòng "(Chưa làm — bước N)". -->

## 1. Tổng quan

### 1.1 Mục đích

Bài viết là đơn vị nội dung trung tâm của iShare: cùng một loại bài dùng cho chia sẻ kiến thức, hướng dẫn, kinh nghiệm,
thảo luận, đánh giá, tài liệu và tin tức. Module Post & Content giúp người dùng soạn bài với nội dung giàu định dạng
(kể cả công thức toán), đính kèm tệp, tạo bình chọn, đăng bài qua bước quét nội dung trước khi công khai, sửa bài kèm
lịch sử sửa, và xóa bài với thời hạn khôi phục.

### 1.2 Phạm vi

**Trong phạm vi:**

- Soạn bài trong trình soạn giàu định dạng (định dạng chữ, tiêu đề mục, danh sách, code, công thức LaTeX, bảng, trích dẫn,
  liên kết); không chèn ảnh trong nội dung.
- Một loại bài duy nhất: tiêu đề, nội dung, Lớp/Khối (tùy chọn), bình chọn (tùy chọn), tệp đính kèm (ảnh, tài liệu) dưới bài.
- Vòng đời đăng bài: lưu nháp, gửi bài, quét trước khi đăng, kết quả đăng / chờ Mod duyệt / bị từ chối, Mod hoặc Admin
  duyệt bài chờ đăng (đăng hoặc từ chối kèm lý do), sửa và gửi lại bài bị từ chối; hành vi khi AI tắt hoặc lỗi.
- Bình chọn (poll) đóng: tạo, cấu hình, bình chọn, đổi và bỏ phiếu, đổi hạn, kết thúc ngay, thêm lựa chọn, hiển thị kết quả.
- Sửa bài, lịch sử sửa công khai, quét lại khi sửa.
- Tác giả tự ẩn bài; tác giả hoặc Mod khóa bình luận, Mod khóa toàn bộ bài; mức khóa và người khóa; điều kiện để bài hiển thị.
- Xóa mềm, khôi phục trong 7 ngày (tab "Đã xóa"); hết hạn khôi phục thì bài chuyển sang Đã xóa hẳn — chỉ gắn cờ, không xóa
  dữ liệu; Mod, Admin và tác giả xem lại bài Đã xóa hẳn trong ngữ cảnh kiểm duyệt.
- Xem, đọc bài (gồm Guest).

**Ngoài phạm vi:**

- Bình luận, kể cả trình soạn, sửa, xóa, lịch sử sửa và đính kèm của bình luận — M04 Comment.
- Quy tắc Topic, Tag và gợi ý Topic bằng AI trong trình soạn — M05 Topic & Tag (M03 chỉ là nơi chọn khi soạn).
- Tìm kiếm bài — M06 Search. Feed, Trending Post — M14 Feed & Discovery.
- Thông báo về bài (đăng, bị từ chối, bị ẩn, poll kết thúc) và tắt thông báo theo bài — M07 Notification.
- Báo cáo bài, cách quét AI và ngưỡng điểm, cảnh cáo, ban, hạn chế đăng bài theo mức cảnh cáo, Mod ẩn/gỡ bài khi xử lý
  báo cáo — M08 Moderation.
- Khiếu nại bài bị Mod ẩn ("gỡ") — M09 Appeal. Công tắc AI — M10 Admin Panel.
- Bài trong nhóm (cổng duyệt riêng của nhóm), đăng ẩn danh — M11 Group.
- Upvote bài, điểm, trừ điểm khi xóa bài — M12 Gamification.
- Tóm tắt bài bằng AI, embedding — M13 AI Layer. Thống kê bài — M15 Analytics & Stats.
- Hiển thị bài khi tác giả vô hiệu hóa hoặc xóa tài khoản, nhắc tên (@mention) trong bài — M01 Authentication & Account.
- Đã quyết không làm: nhiều loại bài (một loại duy nhất); chèn ảnh trong nội dung; trình soạn LaTeX trực quan (để sau);
  mở lại bình chọn đã đóng; AI tự viết bài; đếm lượt xem bài ở MS1 (hoãn); Accepted Answer; ảnh bìa bài viết.

## 2. Thuật ngữ và viết tắt

### 2.1 Thuật ngữ

| Thuật ngữ | Định nghĩa |
|---|---|
| Bài viết | Đơn vị nội dung trung tâm của iShare. Chỉ có một loại bài viết, dùng cho mọi dạng nội dung (chia sẻ kiến thức, hướng dẫn, kinh nghiệm, thảo luận, đánh giá, tài liệu, tin tức). |
| Tác giả bài viết | Người dùng đã đăng nhập (User, Mod hoặc Admin) đã tạo bài viết. |
| Bài nháp | Bài viết tác giả đang soạn và chưa gửi (trạng thái đăng Nháp). |
| Gửi bài | Thao tác tác giả nộp bài nháp hoặc bài bị từ chối để đăng. Mốc thời gian "gửi" là lúc thao tác này được hệ thống ghi nhận. |
| Quét nội dung | Việc AI kiểm duyệt chấm điểm nội dung bài viết, chạy khi bài được gửi, khi bài đã đăng được sửa, và khi tác giả hiện lại bài Tự ẩn đã được sửa trong lúc ẩn. Cách gọi AI, thời gian chờ và cách tính điểm thuộc M08, M13. |
| Điểm quét | Con số từ 0 đến 1 mà bước quét nội dung trả về cho một bài viết; điểm càng cao càng có khả năng vi phạm. |
| Trạng thái đăng | Một trong sáu giá trị: Nháp, Chờ duyệt, Đã đăng, Tự ẩn, Bị từ chối, Đã xóa. Do tác giả và luồng đăng bài quyết định. Bài Đã xóa hết thời hạn khôi phục được gắn thêm cờ Đã xóa hẳn. |
| Chờ duyệt | Bài đã gửi, đang được quét hoặc đang chờ Mod duyệt; người khác không thấy. |
| Đã đăng | Bài đã qua bước quét, được Mod duyệt, hoặc được đăng thẳng khi AI tắt. Mốc "đăng" là lúc bài chuyển sang trạng thái này. |
| Bị từ chối | Bài bị Mod từ chối (kèm lý do) hoặc bị AI tự từ chối; tác giả sửa và gửi lại được. |
| Tự ẩn | Bài tác giả tự ẩn khỏi người khác; tác giả hiện lại được. |
| Đã xóa | Bài tác giả đã xóa nhưng còn trong thời hạn khôi phục (xóa mềm). |
| Đã xóa hẳn (xóa hẳn) | Cờ hệ thống gắn cho bài Đã xóa khi hết thời hạn khôi phục. **Chỉ là cờ, không xóa dữ liệu:** nội dung, tệp đính kèm, poll, phiếu bình chọn, lịch sử sửa, liên kết Topic/Tag và bình luận của bài vẫn được giữ. Với người dùng, bài coi như không còn: không hiện ở đâu, mở đường dẫn báo không tồn tại, không khôi phục được. Chỉ Mod, Admin (qua báo cáo, lịch sử báo cáo, khiếu nại) và tác giả (từ thông báo xử lý hoặc khiếu nại) xem lại được. Trong tài liệu này, "xóa hẳn" đều mang nghĩa này. |
| Thời hạn khôi phục | 7 × 24 giờ kể từ thời điểm tác giả xóa bài. |
| Trạng thái kiểm duyệt | Một trong ba giá trị: Bình thường, Bị gắn cờ (bước quét lại của AI gắn cờ, chờ Mod xét; báo cáo của người dùng không làm bài Bị gắn cờ), Bị Mod ẩn (tác giả không tự hiện lại được, phải khiếu nại; "Mod gỡ bài" chính là trạng thái này). Bài mới có giá trị Bình thường. Do AI và Mod quyết định. |
| Bài hiển thị công khai | Bài có trạng thái đăng Đã đăng và trạng thái kiểm duyệt Bình thường. Chỉ bài này hiện cho người không phải tác giả (trừ bài trong nhóm Private, M11). |
| Mức khóa | Một trong ba giá trị: Không khóa, Khóa bình luận (chặn bình luận mới), Khóa toàn bộ (chặn bình luận mới, upvote và bình chọn poll). Kèm người khóa: tác giả hoặc Mod. |
| Poll | Bình chọn tùy chọn trong bài viết, dạng đóng: chỉ tác giả đặt các lựa chọn, người xem chỉ chọn. Có hai kiểu: chọn một và chọn nhiều. |
| Lượt chọn | Một lựa chọn mà một người đã chọn trong poll. Ở poll chọn nhiều, người chọn A và C có 2 lượt chọn. |
| Hạn kết thúc poll | Thời điểm poll tự đóng, bắt buộc khi tạo poll, không được trước thời điểm hiện tại, tính theo giờ Việt Nam (UTC+7). |
| Poll đã đóng | Poll đã đến hạn hoặc bị tác giả kết thúc ngay; không nhận phiếu mới, không đổi hay bỏ phiếu, không mở lại được. |
| Tệp đính kèm | Ảnh hoặc tài liệu tác giả đính kèm ở phần dưới nội dung bài viết; không nằm trong nội dung. |
| Lịch sử sửa | Danh sách các phiên bản của bài viết đã gửi, mỗi lần tác giả lưu bản sửa là một phiên bản. |
| Lớp/Khối | Cấp học 10, 11 hoặc 12. Trên bài viết là trường tùy chọn do tác giả chọn, độc lập với Lớp/Khối trên hồ sơ (M02) và với Topic (M05). |
| MB | Đơn vị dung lượng tệp dùng trong giới hạn đính kèm (megabyte). |
| Từ (khi đếm độ dài nội dung) | Một cụm chữ ngăn cách bởi khoảng trắng, đếm trên phần chữ người đọc thấy (không tính định dạng). Ví dụ "Phương trình bậc hai" là 4 từ. |
| Bài trống | Bài không có tiêu đề, nội dung, poll và tệp đính kèm nào. |

> **Lưu ý về "Đã xóa hẳn" (bản 1.1, DEC-184):** "Đã xóa hẳn" không có nghĩa là xóa hết dữ liệu. Hệ thống chỉ gắn cờ;
> mọi dữ liệu của bài được giữ nguyên để phục vụ báo cáo, lịch sử báo cáo và khiếu nại. Bài viết và các nội dung báo
> cáo được khác chỉ được xóa mềm.

### 2.2 Viết tắt

| Viết tắt | Đầy đủ |
|---|---|
| FR | Functional Requirement — yêu cầu chức năng |

## 3. Thông tin đầu vào

### 3.1 Tài liệu đầu vào

| Tài liệu | Phiên bản / mốc |
|---|---|
| Draft: docs/_temp/iShare_modules.md, iShare_specs_general.md | Theo ngày sửa tệp |
| Register: decisions, qa-log, issue-queue, open-issues, glossary, module-registry | DEC-247, QA-444, ISS-382, OPEN-012 (khớp `moc_nguon`) |

### 3.2 Tài liệu liên quan

| Module | Liên quan ở điểm nào |
|---|---|
| M01 Authentication & Account | Bài của tác giả vô hiệu hóa hoặc xóa tài khoản bị ẩn; nhắc tên trong bài và thời điểm gửi thông báo nhắc tên. |
| M02 User Profile | Tab bài viết và tab "Đã xóa" trên hồ sơ; Lớp/Khối trên hồ sơ độc lập với Lớp/Khối trên bài. |
| M04 Comment | Bình luận gắn với bài; khóa bình luận chặn bình luận mới. |
| M05 Topic & Tag | Chọn Topic, gắn Tag, gợi ý Topic khi soạn và sửa bài; trạng thái bài dùng khi đếm và xóa Topic. |
| M06 Search | Tìm kiếm trên nội dung văn bản của bài. |
| M07 Notification | Thông báo bài được đăng, bị từ chối, bị ẩn, poll kết thúc; thông báo bài mới cho người theo dõi tác giả; tắt thông báo theo bài. |
| M08 Moderation | Quét AI trước khi đăng, hàng chờ Mod duyệt, Mod ẩn/khóa bài, hạn chế tạo bài theo mức cảnh cáo. |
| M09 Appeal | Khiếu nại bài bị Mod ẩn ("gỡ") hoặc bị AI tự từ chối; khiếu nại thành công thì bài trở lại hiển thị. |
| M10 Admin Panel | Công tắc AI tổng và công tắc Moderation quyết định có quét trước khi đăng hay không. |
| M11 Group | Bài trong nhóm dùng chung cơ chế bài, có cổng duyệt riêng và tùy chọn đăng ẩn danh. |
| M12 Gamification | Upvote bài; trừ điểm khi bài do tác giả xóa bị xóa hẳn hoặc bài bị Mod ẩn ("gỡ"). |
| M13 AI Layer | Ngưỡng quét nội dung, xử lý khi AI lỗi, tóm tắt bài, embedding. |
| M14 Feed & Discovery | Feed và Trending Post hiển thị bài đã đăng. |
| M15 Analytics & Stats | Thống kê bài theo trạng thái. |

## 4. Tổng quan chức năng

### 4.1 Luật, tiêu chuẩn liên quan

Không có.

### 4.2 Vai trò

| Vai trò | Mô tả trong module này |
|---|---|
| Guest | Người chưa đăng nhập. Xem, đọc bài viết đang hiển thị công khai (kể cả bài trong nhóm Public) và lịch sử sửa của bài. Không soạn, gửi, bình chọn hay thao tác gì khác trên bài. |
| User | Người dùng đã đăng nhập. Xem bài viết, bình chọn trong poll; khi là tác giả thì làm mọi thao tác trên bài của mình. |
| Mod | Có mọi quyền của User. Thêm quyền duyệt bài chờ đăng, khóa toàn bộ bài và mở khóa bài do Mod khóa. |
| Admin | Có các quyền của Mod trong module này. Bài của Admin được đăng ngay, không bị hệ thống quét hay duyệt; bài của Admin trong nhóm vẫn qua bước duyệt của nhóm (M11). |
| Tác giả bài viết | Vai trò theo ngữ cảnh: User, Mod hoặc Admin đang soạn, gửi, sửa, ẩn, khóa, xóa, khôi phục bài viết của chính mình, kể cả cấu hình poll trong bài. |
| Hệ thống | Tác nhân của việc quét nội dung bài trước khi đăng và sau khi sửa, kết thúc poll khi hết hạn, và chuyển bài hết hạn khôi phục sang Đã xóa hẳn. |

### 4.3 Ma trận quyền

| Hành động | Guest | User | Mod | Admin | Yêu cầu |
|---|---|---|---|---|---|
| Soạn, lưu nháp bài viết mới | ✗ | ✓ | ✓ | ✓ | FR-M03-01.01, FR-M03-01.10, FR-M03-07.06 |
| Đính kèm tệp, tạo poll trong bài | ✗ | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | FR-M03-02.01, FR-M03-02.11, FR-M03-03.01, FR-M03-03.08, FR-M03-07.06 |
| Gửi bài, gửi lại bài bị từ chối | ✗ | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | FR-M03-04.01, FR-M03-04.04, FR-M03-04.06, FR-M03-07.06 |
| Duyệt bài chờ đăng (đăng hoặc từ chối kèm lý do) | ✗ | ✗ | ✓ | ✓ | FR-M03-06.02, FR-M03-06.03, FR-M03-06.06 |
| Xem bài đang hiển thị công khai | ✓ | ✓ | ✓ | ✓ | FR-M03-07.01 |
| Xem bài chưa hiển thị công khai của mình (nháp, chờ duyệt, bị từ chối, tự ẩn, bị Mod ẩn, đã xóa) | ✗ | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | FR-M03-07.03, FR-M03-07.02, FR-M03-15.03 |
| Xem bài Nháp, Bị từ chối của người khác | ✗ | ✗ | ✗ | ✗ | FR-M03-07.02, FR-M03-07.07 |
| Xem bài Tự ẩn, Đã xóa của người khác trong báo cáo, lịch sử báo cáo, khiếu nại | ✗ | ✗ | ✓ | ✓ | FR-M03-07.11, FR-M03-17.04, FR-M03-07.02 |
| Xem lịch sử sửa bài | ✓ | ✓ | ✓ | ✓ | FR-M03-12.03 |
| Bình chọn trong poll của người khác | ✗ | ✓ | ✓ | ✓ | FR-M03-08.01, FR-M03-07.06 |
| Bình chọn trong poll của bài mình | ✗ | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | FR-M03-08.11, FR-M03-07.06 |
| Đổi hạn, kết thúc ngay, thêm lựa chọn cho poll | ✗ | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | FR-M03-09.01, FR-M03-09.02, FR-M03-09.06, FR-M03-09.04, FR-M03-07.06 |
| Sửa bài đã gửi | ✗ | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | FR-M03-11.01, FR-M03-11.04, FR-M03-07.06 |
| Tự ẩn, hiện lại bài | ✗ | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | FR-M03-13.01, FR-M03-13.02, FR-M03-13.03, FR-M03-07.06 |
| Khóa bình luận của bài | ✗ | ✓ (của mình) | ✓ | ✓ | FR-M03-14.01, FR-M03-14.02, FR-M03-14.11, FR-M03-07.06 |
| Mở khóa bình luận do tác giả khóa | ✗ | ✓ (của mình) | ✓ | ✓ | FR-M03-14.07, FR-M03-14.08, FR-M03-14.11, FR-M03-07.06 |
| Khóa toàn bộ bài (chặn bình luận và tương tác) | ✗ | ✗ | ✓ | ✓ | FR-M03-14.03, FR-M03-14.10, FR-M03-07.06 |
| Mở khóa bài do Mod khóa | ✗ | ✗ | ✓ | ✓ | FR-M03-14.08, FR-M03-14.09, FR-M03-14.11, FR-M03-07.06 |
| Xóa bài | ✗ | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | FR-M03-15.01, FR-M03-15.04, FR-M03-07.06 |
| Khôi phục bài đã xóa trong 7 ngày | ✗ | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | FR-M03-16.01, FR-M03-16.05, FR-M03-07.06 |
| Xem lại bài Đã xóa hẳn từ thông báo xử lý hoặc khiếu nại | ✗ | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | FR-M03-07.08, FR-M03-07.10 |

<!-- Ô nói thẳng: hàng 1, 3, 12, 18 cột User (DM-1.3); hàng 4 cột Mod (DEC-034); hàng 5 cột Guest (QA-011);
     hàng 8 (DEC-037 "public"); hàng 11 (DEC-036 "owner", DEC-165); hàng 13 (DEC-031); hàng 14–17 (DEC-033); hàng 19 (DEC-038).
     Ô suy ra: cột Guest ở mọi hàng ghi/tương tác (QA-011: Guest chỉ xem, "INTR: Không"); cột Mod/Admin ở các hàng "của mình"
     (Mod/Admin cũng là tác giả bài của mình); cột Admin ở hàng 4, 14–17 (DM-10.2 "Moderator/Admin có thể"); hàng 6 (tác giả
     thấy bài chờ duyệt của mình, QA-030 "pending state visible for author"); hàng 7 cột User và hàng 5 các cột còn lại
     (DEC-033: chỉ bài PUBLISHED + NORMAL hiển thị; Guest xem được thì vai trò cao hơn cũng xem được); hàng 9 (QA-081 "users vote"); hàng 7, 10 theo DEC-168, DEC-165;
     hàng 12, 18 cột Mod/Admin chỉ "của mình": nguồn chỉ cho Mod/Admin đổi Topic/Tag bài người khác (DEC-142, M05), không nói
     sửa nội dung; Mod/Admin ẩn, xóa bài người khác thuộc M08.
     Người ở mức cảnh cáo MEDIUM/HEAVY bị chặn theo BR-M03-38 (DEC-079, DEC-163); tài khoản BANNED do M08, M09 quy định. -->

### 4.4 Danh sách chức năng

| ID | Chức năng | Tác nhân chính | Kích hoạt |
|---|---|---|---|
| FR-M03-01 | Soạn và lưu nháp bài viết | Tác giả bài viết | Người dùng đã đăng nhập mở trình soạn bài mới, hoặc lưu bài đang soạn mà chưa gửi |
| FR-M03-02 | Đính kèm tệp vào bài viết | Tác giả bài viết | Tác giả thêm hoặc bỏ tệp ở phần đính kèm khi soạn hoặc sửa bài |
| FR-M03-03 | Tạo bình chọn trong bài viết | Tác giả bài viết | Tác giả thêm bình chọn (poll) vào bài khi soạn |
| FR-M03-04 | Gửi bài viết để đăng | Tác giả bài viết | Tác giả gửi bài nháp, hoặc gửi lại bài bị từ chối sau khi sửa |
| FR-M03-05 | Quét nội dung bài viết | Hệ thống | Bài vừa được gửi, hoặc bài đã đăng vừa được sửa |
| FR-M03-06 | Duyệt bài viết chờ đăng | Mod, Admin | Mod hoặc Admin xử lý một bài đang chờ duyệt sau bước quét |
| FR-M03-07 | Xem bài viết | Guest, User, Mod, Admin | Người dùng mở một bài viết |
| FR-M03-08 | Bình chọn trong poll | User, Mod, Admin | Người xem chọn lựa chọn trong poll của một bài |
| FR-M03-09 | Đổi hạn, kết thúc và thêm lựa chọn cho poll | Tác giả bài viết | Tác giả đổi hạn, kết thúc ngay hoặc thêm lựa chọn cho poll đang mở |
| FR-M03-10 | Kết thúc poll khi hết hạn | Hệ thống | Đến hạn kết thúc của poll |
| FR-M03-11 | Sửa bài viết đã gửi | Tác giả bài viết | Tác giả chọn sửa một bài của mình đã gửi |
| FR-M03-12 | Xem lịch sử sửa bài viết | Guest, User, Mod, Admin | Người xem chọn "Xem lịch sử" trên bài có nhãn "(đã chỉnh sửa)" |
| FR-M03-13 | Tự ẩn và hiện lại bài viết | Tác giả bài viết | Tác giả chọn ẩn bài của mình, hoặc hiện lại bài đã tự ẩn |
| FR-M03-14 | Khóa và mở khóa bài viết | Tác giả bài viết, Mod, Admin | Tác giả khóa hoặc mở khóa bình luận bài của mình; Mod hoặc Admin khóa, mở khóa một bài |
| FR-M03-15 | Xóa bài viết | Tác giả bài viết | Tác giả chọn xóa một bài của mình |
| FR-M03-16 | Khôi phục bài viết đã xóa | Tác giả bài viết | Tác giả chọn khôi phục bài trong tab "Đã xóa" trên hồ sơ |
| FR-M03-17 | Chuyển bài hết hạn khôi phục sang Đã xóa hẳn | Hệ thống | Bài đã xóa đủ 7 ngày |

### 4.5 Mốc và ưu tiên

Toàn bộ yêu cầu của module thuộc MS1, ưu tiên **Must** (bảng MoSCoW Summary của module-registry: Must gồm M01–M10, M13;
cột MoSCoW ở dòng M03 của bảng Module List bị lệch nên không dùng). Không có yêu cầu ngoại lệ về ưu tiên.

## 5. Yêu cầu chức năng

### 5.1 FR-M03-01 Soạn và lưu nháp bài viết

**Yêu cầu cấp trên:** Hệ thống phải cho phép người dùng đã đăng nhập soạn bài viết mới trong trình soạn giàu định dạng và lưu bài chưa gửi dưới dạng bài nháp.

**Lý do:** Bài viết là đơn vị nội dung trung tâm của hệ thống; mọi dạng nội dung dùng cùng một loại bài, vì nếu các loại chỉ khác nhau về cách hiển thị thì Topic/Tag là đủ.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M03-01.01 | Hệ thống phải cho phép người dùng đã đăng nhập tạo bài viết mới và lưu bài chưa gửi ở trạng thái Nháp. |
| FR-M03-01.02 | Hệ thống phải cung cấp trình soạn bài có các định dạng nêu ở BR-M03-03. |
| FR-M03-01.03 | Hệ thống phải cho tác giả nhập công thức LaTeX dạng mã thô và hiển thị công thức đó trong bài. |
| FR-M03-01.04 | Hệ thống phải giữ mọi ảnh của bài ở phần tệp đính kèm, không đặt ảnh trong nội dung bài. |
| FR-M03-01.05 | Hệ thống phải cho tác giả chọn Lớp/Khối của bài là 10, 11, 12 hoặc để trống. |
| FR-M03-01.06 | Nếu Lớp/Khối của bài là giá trị khác 10, 11 và 12, hệ thống phải từ chối lưu bài. |
| FR-M03-01.07 | Hệ thống phải lưu Lớp/Khối của bài độc lập với Lớp/Khối trên hồ sơ của tác giả. |
| FR-M03-01.08 | Hệ thống phải lưu tác giả, thời điểm tạo và thời điểm cập nhật của bài viết. |
| FR-M03-01.09 | Hệ thống phải tạo bài viết mới với mức khóa Không khóa. |
| FR-M03-01.10 | Nếu tác giả đang ở mức cảnh cáo MEDIUM hoặc HEAVY, hệ thống phải từ chối lưu bài nháp mới. |
| FR-M03-01.11 | Hệ thống phải dùng một loại bài viết cho mọi dạng nội dung, không yêu cầu tác giả chọn loại bài. |
| FR-M03-01.12 | Hệ thống phải tạo bài viết mới với trạng thái kiểm duyệt Bình thường. |
| FR-M03-01.13 | Nếu tác giả lưu nháp khi bài không có tiêu đề, nội dung, poll và tệp đính kèm nào, hệ thống phải từ chối lưu. |
| FR-M03-01.14 | Nếu tiêu đề dài hơn 150 ký tự, hệ thống phải từ chối lưu và gửi bài. |
| FR-M03-01.15 | Nếu nội dung dài hơn 6.000 từ, hệ thống phải từ chối lưu và gửi bài. |
| FR-M03-01.16 | Khi tiêu đề vượt 150 ký tự hoặc nội dung vượt 6.000 từ trong lúc tác giả soạn hoặc sửa bài, hệ thống phải hiển thị cảnh báo ngay, kèm số hiện tại so với giới hạn. |
| FR-M03-01.17 | Nếu việc lưu hoặc gửi bị từ chối vì vượt giới hạn độ dài, hệ thống phải giữ nguyên nội dung tác giả đang soạn. |

### 5.2 FR-M03-02 Đính kèm tệp vào bài viết

**Yêu cầu cấp trên:** Hệ thống phải cho phép tác giả đính kèm ảnh và tài liệu vào bài của mình trong giới hạn về định dạng, dung lượng và số lượng.

**Lý do:** Không hỗ trợ chèn ảnh trong nội dung vì việc này làm phức tạp lưu trữ và quét nội dung; mọi media là tệp đính kèm.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M03-02.01 | Hệ thống phải cho phép tác giả thêm và bỏ tệp đính kèm khi soạn bài của mình. |
| FR-M03-02.02 | Hệ thống phải cho phép tác giả thêm và bỏ tệp đính kèm khi sửa bài đã gửi của mình. |
| FR-M03-02.03 | Hệ thống phải hiển thị các tệp đính kèm ở phần dưới nội dung bài. |
| FR-M03-02.04 | Nếu ảnh đính kèm không có định dạng JPEG, PNG hoặc WebP, hệ thống phải từ chối ảnh đó. |
| FR-M03-02.05 | Nếu ảnh đính kèm lớn hơn 5 MB, hệ thống phải từ chối ảnh đó. |
| FR-M03-02.06 | Nếu bài đã có 10 ảnh đính kèm và tác giả thêm ảnh, hệ thống phải từ chối ảnh thêm. |
| FR-M03-02.07 | Nếu tài liệu đính kèm không có định dạng PDF, DOCX, XLSX hoặc PPTX, hệ thống phải từ chối tài liệu đó. |
| FR-M03-02.08 | Nếu tài liệu đính kèm lớn hơn 20 MB, hệ thống phải từ chối tài liệu đó. |
| FR-M03-02.09 | Nếu bài đã có 3 tài liệu đính kèm và tác giả thêm tài liệu, hệ thống phải từ chối tài liệu thêm. |
| FR-M03-02.10 | Hệ thống phải tính giới hạn số ảnh và giới hạn số tài liệu riêng với nhau. |
| FR-M03-02.11 | Nếu người thêm hoặc bỏ tệp khác tác giả của bài, hệ thống phải từ chối. |

### 5.3 FR-M03-03 Tạo bình chọn trong bài viết

**Yêu cầu cấp trên:** Hệ thống phải cho phép tác giả thêm vào bài chưa gửi của mình một poll đóng có từ 2 đến 10 lựa chọn, hai tùy chọn cấu hình và hạn kết thúc bắt buộc.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M03-03.01 | Hệ thống phải cho phép tác giả thêm một poll vào bài khi bài chưa được gửi. |
| FR-M03-03.02 | Hệ thống phải để tác giả đặt các lựa chọn của poll; người bình chọn chỉ chọn trong các lựa chọn có sẵn. |
| FR-M03-03.03 | Nếu poll có ít hơn 2 hoặc nhiều hơn 10 lựa chọn, hệ thống phải từ chối tạo poll. |
| FR-M03-03.04 | Nếu bài đã có poll và tác giả thêm poll khác, hệ thống phải từ chối poll thêm. |
| FR-M03-03.05 | Hệ thống phải cho phép tác giả chọn poll chọn một hoặc chọn nhiều, và bật hoặc tắt tùy chọn hiện kết quả trước khi bình chọn. |
| FR-M03-03.06 | Hệ thống phải đặt mặc định cho poll mới là chọn nhiều và tắt hiện kết quả trước khi bình chọn. |
| FR-M03-03.07 | Nếu tác giả không đặt hạn kết thúc cho poll, hệ thống phải từ chối tạo poll. |
| FR-M03-03.08 | Nếu người tạo poll khác tác giả của bài, hệ thống phải từ chối. |
| FR-M03-03.09 | Nếu hạn kết thúc của poll trước thời điểm hiện tại, hệ thống phải từ chối. |
| FR-M03-03.10 | Trong khi bài còn là bài nháp, hệ thống phải cho phép tác giả bỏ poll và đổi lựa chọn, cấu hình, hạn kết thúc của poll. |
| FR-M03-03.11 | Nếu bài đã được gửi, hệ thống phải từ chối thêm poll, bỏ poll, sửa hoặc xóa lựa chọn đã có và đổi cấu hình của poll. |

### 5.4 FR-M03-04 Gửi bài viết để đăng

**Yêu cầu cấp trên:** Hệ thống phải cho phép tác giả gửi bài nháp, hoặc gửi lại bài bị từ chối sau khi sửa, để bài được quét và đăng.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M03-04.01 | Khi tác giả khác Admin gửi bài nháp trong lúc công tắc AI tổng và công tắc Moderation đều bật, hệ thống phải chuyển bài sang Chờ duyệt và quét nội dung bài theo FR-M03-05. |
| FR-M03-04.02 | Trong khi bài ở trạng thái Chờ duyệt, hệ thống phải ẩn bài với mọi người trừ tác giả và người duyệt bài theo FR-M03-06. |
| FR-M03-04.03 | Ở nơi công tắc AI tổng hoặc công tắc Moderation đang tắt, khi tác giả gửi bài, hệ thống phải chuyển bài sang Đã đăng ngay mà không quét. |
| FR-M03-04.04 | Khi tác giả gửi lại bài Bị từ chối sau khi sửa, hệ thống phải xử lý bài như bài nháp vừa được gửi theo FR-M03-04.01 và FR-M03-04.03. |
| FR-M03-04.05 | Hệ thống phải áp dụng luồng gửi bài của FR-M03-04 cho bài không thuộc nhóm; bài thuộc nhóm theo luồng duyệt của M11, trong đó bài của Owner nhóm có điểm quét từ 0.5 đến nhỏ hơn 0.9 hoặc quét thất bại được đưa vào hàng chờ duyệt của Mod như bài không thuộc nhóm (BR-M03-25). |
| FR-M03-04.06 | Nếu người gửi khác tác giả của bài, hệ thống phải từ chối. |
| FR-M03-04.07 | Nếu bài không ở trạng thái Nháp hoặc Bị từ chối, hệ thống phải từ chối thao tác gửi bài. |
| FR-M03-04.08 | Nếu bài được gửi không có tiêu đề, hệ thống phải từ chối gửi. |
| FR-M03-04.09 | Nếu bài được gửi không có nội dung và cũng không có poll, hệ thống phải từ chối gửi, kể cả khi bài có tệp đính kèm. |
| FR-M03-04.10 | Nếu tác giả đang ở mức cảnh cáo MEDIUM hoặc HEAVY, hệ thống phải từ chối gửi bài nháp và gửi lại bài Bị từ chối. |
| FR-M03-04.11 | Khi tác giả là Admin gửi bài nháp hoặc gửi lại bài Bị từ chối không thuộc nhóm, hệ thống phải chuyển bài sang Đã đăng ngay mà không quét và không đưa vào hàng chờ duyệt (BR-M03-51). |

### 5.5 FR-M03-05 Quét nội dung bài viết

**Yêu cầu cấp trên:** Hệ thống phải quét nội dung bài vừa gửi và bài đã đăng vừa được sửa, và quyết định trạng thái bài theo điểm quét khi AI đang bật.

**Lý do:** Nền tảng phục vụ học sinh nên cần quét trước để kiểm soát nội dung; quét chặn khi sửa bài đã được duyệt gây trải nghiệm xấu nên bài sửa được quét lại ngầm; quét lại toàn bộ khi bật lại AI gây tải dồn không kiểm soát được. Khi quét lỗi, giữ bài chờ Mod an toàn hơn tự đăng.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M03-05.01 | Khi quét xong bài vừa gửi với điểm quét nhỏ hơn 0.5, hệ thống phải chuyển bài sang Đã đăng. |
| FR-M03-05.02 | Khi quét xong bài vừa gửi với điểm quét từ 0.5 đến nhỏ hơn 0.9, hệ thống phải giữ bài ở Chờ duyệt và đưa bài vào hàng chờ duyệt của Mod. |
| FR-M03-05.03 | Khi quét xong bài vừa gửi với điểm quét từ 0.9 trở lên, hệ thống phải chuyển bài sang Bị từ chối mà không qua Mod. |
| FR-M03-05.04 | Nếu bước quét bài vừa gửi thất bại sau một lần thử lại, hệ thống phải giữ bài ở Chờ duyệt và đưa bài vào hàng chờ duyệt của Mod. |
| FR-M03-05.05 | Khi tác giả khác Admin lưu bản sửa của bài Đã đăng, hoặc hiện lại bài Tự ẩn có bản sửa được lưu trong lúc ẩn, trong lúc công tắc AI tổng và công tắc Moderation đều bật, hệ thống phải quét lại nội dung bài. |
| FR-M03-05.06 | Trong khi quét lại bài theo FR-M03-05.05, hệ thống phải giữ bài ở trạng thái đang hiển thị, với nội dung đã sửa, cho tới khi có kết quả quét. |
| FR-M03-05.07 | Khi quét lại bài vừa sửa cho điểm quét từ 0.5 trở lên, hệ thống phải chuyển trạng thái kiểm duyệt của bài sang Bị gắn cờ, ẩn bài với người khác tác giả và đưa bài cho Mod xét. |
| FR-M03-05.08 | Ở nơi công tắc AI tổng hoặc công tắc Moderation đang tắt, hệ thống phải không quét bài khi gửi và khi sửa. |
| FR-M03-05.09 | Khi công tắc AI tổng hoặc công tắc Moderation được bật lại, hệ thống phải không quét lại các bài đã đăng trong thời gian tắt. |
| FR-M03-05.10 | Khi quét lại bài vừa sửa cho điểm quét nhỏ hơn 0.5, hệ thống phải giữ nguyên trạng thái của bài. |
| FR-M03-05.11 | Nếu bước quét lại bài vừa sửa thất bại, hệ thống phải giữ nguyên trạng thái và tiếp tục hiển thị bài. |
| FR-M03-05.12 | Khi bài vừa gửi bị tự từ chối theo FR-M03-05.03, hệ thống phải hiển thị cho tác giả nhóm vi phạm mà AI phát hiện. |
| FR-M03-05.13 | Hệ thống phải cho phép tác giả sửa và gửi lại bài bị AI tự từ chối không giới hạn số lần, mỗi lần đều được quét lại. |
| FR-M03-05.14 | Khi tác giả lưu bản sửa của bài Tự ẩn, hệ thống phải không quét bài tại lúc lưu; việc quét diễn ra khi tác giả hiện lại bài (FR-M03-05.05). |
| FR-M03-05.15 | Nếu tác giả bài là Admin, hệ thống phải không quét lại bài khi Admin lưu bản sửa của bài Đã đăng hoặc hiện lại bài Tự ẩn đã sửa (BR-M03-51). |

### 5.6 FR-M03-06 Duyệt bài viết chờ đăng

**Yêu cầu cấp trên:** Hệ thống phải cho phép Mod và Admin duyệt bài đang chờ duyệt: chấp nhận để đăng, hoặc từ chối kèm lý do.

**Lý do:** AI chỉ đưa ra dự đoán; với trường hợp nhạy cảm con người quyết định cuối cùng.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M03-06.01 | Hệ thống phải hiển thị cho Mod và Admin các bài Chờ duyệt đang nằm trong hàng chờ duyệt. |
| FR-M03-06.02 | Khi Mod hoặc Admin chấp nhận một bài Chờ duyệt, hệ thống phải chuyển bài sang Đã đăng. |
| FR-M03-06.03 | Khi Mod hoặc Admin từ chối một bài Chờ duyệt, hệ thống phải chuyển bài sang Bị từ chối và lưu lý do từ chối. |
| FR-M03-06.04 | Nếu Mod hoặc Admin từ chối bài mà không nhập lý do, hệ thống phải từ chối thao tác. |
| FR-M03-06.05 | Hệ thống phải hiển thị lý do từ chối cho tác giả của bài Bị từ chối. |
| FR-M03-06.06 | Nếu người duyệt khác Mod và Admin, hệ thống phải từ chối. |
| FR-M03-06.07 | Nếu bài không còn ở trạng thái Chờ duyệt khi Mod hoặc Admin duyệt, hệ thống phải từ chối thao tác duyệt. |

### 5.7 FR-M03-07 Xem bài viết

**Yêu cầu cấp trên:** Hệ thống phải cho phép mọi người, kể cả Guest, xem bài viết đang hiển thị công khai, và cho tác giả xem bài của mình ở mọi trạng thái.

**Lý do:** Cho Guest xem bài là quyết định quan trọng về khả năng được tìm thấy: nội dung iShare được công cụ tìm kiếm index, mang lại lượt truy cập tự nhiên.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M03-07.01 | Hệ thống phải hiển thị bài cho mọi người, kể cả Guest, khi bài có trạng thái đăng Đã đăng và trạng thái kiểm duyệt Bình thường, bất kể mức khóa, trừ bài trong nhóm Private chỉ hiển thị cho thành viên nhóm (M11). |
| FR-M03-07.02 | Nếu bài không ở trạng thái hiển thị công khai, hệ thống phải không hiển thị bài cho người khác tác giả, trừ bài Chờ duyệt trong hàng chờ ở FR-M03-06.01, bài Bị gắn cờ, Bị Mod ẩn mà Mod, Admin xem khi xử lý ở M08, M09, và bài Tự ẩn, Đã xóa, Đã xóa hẳn mà Mod, Admin xem trong báo cáo, lịch sử báo cáo, khiếu nại (FR-M03-07.11, FR-M03-17.04). |
| FR-M03-07.03 | Hệ thống phải cho tác giả xem bài của mình ở mọi trạng thái đăng, cho tới khi bài bị xóa hẳn. |
| FR-M03-07.04 | Hệ thống phải hiển thị trên bài: tiêu đề, nội dung, tác giả, Lớp/Khối (nếu có), tệp đính kèm và poll (nếu có). |
| FR-M03-07.05 | Nếu người dùng mở một bài Đã xóa hẳn qua đường dẫn của bài, hệ thống phải báo bài không tồn tại. |
| FR-M03-07.06 | Nếu người chưa đăng nhập thực hiện thao tác khác ngoài xem bài viết và xem lịch sử sửa, hệ thống phải từ chối. |
| FR-M03-07.07 | Nếu Mod hoặc Admin mở bài Nháp hoặc Bị từ chối của người khác, hoặc mở bài Tự ẩn của người khác ngoài báo cáo, lịch sử báo cáo, khiếu nại liên quan tới bài đó, hệ thống phải từ chối. |
| FR-M03-07.08 | Khi tác giả mở thông báo kết quả xử lý báo cáo về bài của mình hoặc mở khiếu nại của mình liên quan tới bài, hệ thống phải hiển thị bài ở chế độ chỉ đọc, kể cả khi bài Đã xóa hẳn. |
| FR-M03-07.09 | Hệ thống phải không hiển thị cho tác giả danh tính, lý do đã chọn, mô tả hay bằng chứng của người báo cáo khi tác giả xem lại bài. |
| FR-M03-07.10 | Nếu người mở khác tác giả bài, hệ thống phải từ chối hiển thị bài Đã xóa hẳn qua đường xem lại này. |
| FR-M03-07.11 | Hệ thống phải cho Mod, Admin xem bài Tự ẩn của người khác chỉ trong báo cáo, lịch sử báo cáo hoặc khiếu nại liên quan tới chính bài đó. |

### 5.8 FR-M03-08 Bình chọn trong poll

**Yêu cầu cấp trên:** Hệ thống phải cho phép người dùng đã đăng nhập bình chọn trong poll đang mở theo cấu hình của poll, và hiển thị kết quả theo tùy chọn hiển thị.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M03-08.01 | Khi người dùng đã đăng nhập chọn lựa chọn trong một poll đang mở, hệ thống phải ghi phiếu của người đó. |
| FR-M03-08.02 | Ở nơi poll không cho chọn nhiều, hệ thống phải nhận đúng một lựa chọn trong mỗi phiếu. |
| FR-M03-08.03 | Ở nơi poll cho chọn nhiều, hệ thống phải cho người bình chọn chọn từ 1 tới tất cả lựa chọn. |
| FR-M03-08.04 | Khi người đã bình chọn chọn lại trong lúc poll còn mở, hệ thống phải thay phiếu cũ bằng phiếu mới. |
| FR-M03-08.05 | Khi người đã bình chọn bỏ chọn trong lúc poll còn mở, hệ thống phải xóa phiếu của người đó. |
| FR-M03-08.06 | Nếu poll đã đóng, hệ thống phải từ chối phiếu mới, việc đổi phiếu và bỏ chọn. |
| FR-M03-08.07 | Trong khi poll còn mở và tùy chọn hiện kết quả trước khi bình chọn đang tắt, hệ thống phải không hiển thị kết quả cho người chưa bình chọn. |
| FR-M03-08.08 | Ở nơi tùy chọn hiện kết quả trước khi bình chọn đang bật, hệ thống phải hiển thị kết quả cho mọi người xem bài trong lúc poll còn mở. |
| FR-M03-08.09 | Trong khi poll còn mở, hệ thống phải hiển thị kết quả cho người đã bình chọn. |
| FR-M03-08.10 | Khi poll đã đóng, hệ thống phải hiển thị kết quả theo phần trăm cho mọi người xem bài, bất kể tùy chọn hiện kết quả trước khi bình chọn. |
| FR-M03-08.11 | Hệ thống phải cho phép tác giả bình chọn trong poll của chính bài mình. |
| FR-M03-08.12 | Hệ thống phải tính phần trăm của mỗi lựa chọn bằng số lượt chọn lựa chọn đó chia cho tổng lượt chọn của poll, làm tròn tới số nguyên. |
| FR-M03-08.13 | Trong khi bài ở mức Khóa toàn bộ, hệ thống phải từ chối bình chọn, đổi phiếu và bỏ chọn trong poll của bài. |

### 5.9 FR-M03-09 Đổi hạn, kết thúc và thêm lựa chọn cho poll

**Yêu cầu cấp trên:** Hệ thống phải cho phép tác giả đổi hạn kết thúc, kết thúc ngay và thêm lựa chọn cho poll đang mở của bài mình.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M03-09.01 | Khi tác giả đổi hạn kết thúc của poll đang mở sang thời điểm không trước thời điểm hiện tại, hệ thống phải lưu hạn kết thúc mới. |
| FR-M03-09.02 | Khi tác giả chọn kết thúc ngay một poll đang mở, hệ thống phải đặt hạn kết thúc bằng thời điểm hiện tại và chuyển poll sang Đã đóng. |
| FR-M03-09.03 | Nếu poll đã đóng, hệ thống phải từ chối mọi thao tác mở lại poll, kể cả dời hạn kết thúc. |
| FR-M03-09.04 | Nếu người đổi hạn, kết thúc poll hoặc thêm lựa chọn khác tác giả của bài, hệ thống phải từ chối. |
| FR-M03-09.05 | Nếu hạn kết thúc mới trước thời điểm hiện tại, hệ thống phải từ chối. |
| FR-M03-09.06 | Khi tác giả thêm lựa chọn vào poll đang mở của bài đã gửi, hệ thống phải lưu lựa chọn mới. |
| FR-M03-09.07 | Nếu việc thêm lựa chọn làm poll có hơn 10 lựa chọn, hệ thống phải từ chối. |
| FR-M03-09.08 | Nếu poll đã đóng, hệ thống phải từ chối thêm lựa chọn. |

### 5.10 FR-M03-10 Kết thúc poll khi hết hạn

**Yêu cầu cấp trên:** Hệ thống phải tự đóng poll khi đến hạn kết thúc.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M03-10.01 | Khi đến hạn kết thúc của một poll đang mở, hệ thống phải chuyển poll sang Đã đóng. |
| FR-M03-10.02 | Khi một poll chuyển sang Đã đóng, hệ thống phải gửi sự kiện poll kết thúc cho M07. |

### 5.11 FR-M03-11 Sửa bài viết đã gửi

**Yêu cầu cấp trên:** Hệ thống phải cho phép tác giả sửa bài đã gửi của mình và ghi mỗi lần sửa vào lịch sử sửa của bài.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M03-11.01 | Hệ thống phải cho phép tác giả sửa tiêu đề, nội dung, Lớp/Khối và tệp đính kèm của bài mình ở trạng thái Bị từ chối, Đã đăng hoặc Tự ẩn, kể cả khi bài đang bị khóa; bài nháp được sửa theo FR-M03-01. |
| FR-M03-11.02 | Khi tác giả lưu bản sửa của bài đã gửi, hệ thống phải ghi vào lịch sử sửa một phiên bản gồm nội dung trước lần sửa, người sửa và thời điểm sửa. |
| FR-M03-11.03 | Khi tác giả lưu bản sửa của bài Đã đăng, hệ thống phải quét lại bài theo FR-M03-05.05. |
| FR-M03-11.04 | Nếu người sửa khác tác giả của bài, hệ thống phải từ chối sửa tiêu đề, nội dung, Lớp/Khối và tệp đính kèm. |
| FR-M03-11.05 | Khi Mod hoặc Admin đổi Topic, Tag trên bài của người khác, hệ thống phải không ghi việc đổi này vào lịch sử sửa. |
| FR-M03-11.06 | Khi Mod hoặc Admin đổi Topic, Tag trên bài của người khác, hệ thống phải không báo cho tác giả. |
| FR-M03-11.07 | Nếu bài ở trạng thái Chờ duyệt hoặc Đã xóa, hoặc có trạng thái kiểm duyệt Bị Mod ẩn, hệ thống phải từ chối sửa bài. |

### 5.12 FR-M03-12 Xem lịch sử sửa bài viết

**Yêu cầu cấp trên:** Hệ thống phải cho phép người xem được bài xem lịch sử sửa của bài đã được sửa.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M03-12.01 | Khi bài có ít nhất một phiên bản trong lịch sử sửa, hệ thống phải hiển thị nhãn "(đã chỉnh sửa)" và nút "Xem lịch sử" trên bài. |
| FR-M03-12.02 | Khi người xem chọn "Xem lịch sử", hệ thống phải hiển thị các phiên bản của bài kèm người sửa và thời điểm sửa. |
| FR-M03-12.03 | Hệ thống phải cho mọi người xem được bài, kể cả Guest, xem lịch sử sửa của bài đó. |
| FR-M03-12.04 | Nếu người xem không xem được bài theo FR-M03-07.02, hệ thống phải không hiển thị lịch sử sửa của bài. |

### 5.13 FR-M03-13 Tự ẩn và hiện lại bài viết

**Yêu cầu cấp trên:** Hệ thống phải cho phép tác giả tự ẩn bài đã đăng của mình và hiện lại bài đã tự ẩn.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M03-13.01 | Khi tác giả ẩn bài Đã đăng của mình, hệ thống phải chuyển bài sang Tự ẩn. |
| FR-M03-13.02 | Khi tác giả hiện lại bài Tự ẩn của mình, hệ thống phải chuyển bài về Đã đăng. |
| FR-M03-13.03 | Nếu người ẩn hoặc hiện lại bài khác tác giả, hệ thống phải từ chối. |
| FR-M03-13.04 | Nếu bài không ở trạng thái Đã đăng, hệ thống phải từ chối thao tác tự ẩn. |
| FR-M03-13.05 | Nếu bài có trạng thái kiểm duyệt Bị Mod ẩn, hệ thống phải không cho tác giả tự đưa bài về hiển thị công khai. |
| FR-M03-13.06 | Khi tác giả hiện lại bài Tự ẩn có bản sửa được lưu trong lúc ẩn, hệ thống phải quét lại bài theo FR-M03-05.05. |

### 5.14 FR-M03-14 Khóa và mở khóa bài viết

**Yêu cầu cấp trên:** Hệ thống phải cho phép tác giả khóa bình luận bài của mình, cho phép Mod và Admin khóa bình luận hoặc khóa toàn bộ một bài, và ghi lại người khóa.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M03-14.01 | Khi tác giả khóa bình luận bài của mình, hệ thống phải đặt mức Khóa bình luận và ghi người khóa là tác giả. |
| FR-M03-14.02 | Khi Mod hoặc Admin khóa bình luận một bài, hệ thống phải đặt mức Khóa bình luận và ghi người khóa là Mod. |
| FR-M03-14.03 | Khi Mod hoặc Admin khóa toàn bộ một bài, hệ thống phải đặt mức Khóa toàn bộ và ghi người khóa là Mod. |
| FR-M03-14.04 | Trong khi bài ở mức Khóa bình luận hoặc Khóa toàn bộ, hệ thống phải từ chối bình luận mới trên bài. |
| FR-M03-14.05 | Trong khi bài ở mức Khóa bình luận hoặc Khóa toàn bộ, hệ thống phải tiếp tục hiển thị các bình luận đã có. |
| FR-M03-14.06 | Trong khi bài ở mức Khóa toàn bộ, hệ thống phải từ chối upvote mới và rút lại upvote trên bài và trên mọi bình luận của bài (M12). |
| FR-M03-14.07 | Khi tác giả mở khóa bình luận do chính tác giả khóa, hệ thống phải đặt mức Không khóa. |
| FR-M03-14.08 | Khi Mod hoặc Admin mở khóa hoặc hạ mức khóa của một bài, hệ thống phải đặt mức khóa mới. |
| FR-M03-14.09 | Nếu người khóa là Mod và tác giả mở khóa hoặc đổi mức khóa, hệ thống phải từ chối. |
| FR-M03-14.10 | Nếu người khác Mod và Admin đặt mức Khóa toàn bộ, hệ thống phải từ chối. |
| FR-M03-14.11 | Nếu người khác tác giả, Mod và Admin khóa hoặc mở khóa bình luận của bài, hệ thống phải từ chối. |
| FR-M03-14.12 | Trong khi bài ở mức Khóa toàn bộ, hệ thống phải tiếp tục cho phép bookmark và báo cáo bài. |

### 5.15 FR-M03-15 Xóa bài viết

**Yêu cầu cấp trên:** Hệ thống phải cho phép tác giả xóa bài của mình ở mọi trạng thái theo cách xóa mềm, giữ bài trong thời hạn khôi phục.

**Lý do:** 7 ngày đủ để người dùng nhận ra lỡ tay xóa.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M03-15.01 | Khi tác giả xóa bài của mình ở bất kỳ trạng thái nào trừ Đã xóa, hệ thống phải chuyển bài sang Đã xóa, ghi thời điểm xóa và trạng thái trước khi xóa. |
| FR-M03-15.02 | Trong khi bài ở trạng thái Đã xóa, hệ thống phải không hiển thị bài ở feed và mọi nơi công khai. |
| FR-M03-15.03 | Trong khi bài ở trạng thái Đã xóa, hệ thống phải hiển thị bài trong tab "Đã xóa" trên hồ sơ của tác giả. |
| FR-M03-15.04 | Nếu người xóa bài khác tác giả, hệ thống phải từ chối thao tác xóa mềm. |
| FR-M03-15.05 | Nếu bài đã ở trạng thái Đã xóa, hệ thống phải từ chối xóa lại. |
| FR-M03-15.06 | Khi tác giả xóa một bài Chờ duyệt, hệ thống phải đưa bài ra khỏi hàng chờ duyệt của Mod. |

### 5.16 FR-M03-16 Khôi phục bài viết đã xóa

**Yêu cầu cấp trên:** Hệ thống phải cho phép tác giả khôi phục bài đã xóa trong thời hạn khôi phục.

**Lý do:** 7 ngày đủ để người dùng nhận ra lỡ tay xóa.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M03-16.01 | Khi tác giả khôi phục bài Đã xóa của mình trong thời hạn khôi phục, hệ thống phải đưa bài về trạng thái trước khi xóa. |
| FR-M03-16.02 | Hệ thống phải tính thời hạn khôi phục là 7 × 24 giờ kể từ thời điểm tác giả xóa bài. |
| FR-M03-16.03 | Nếu thời hạn khôi phục đã hết, hệ thống phải từ chối khôi phục. |
| FR-M03-16.04 | Nếu bài có trạng thái kiểm duyệt Bị Mod ẩn, hệ thống phải từ chối khôi phục. |
| FR-M03-16.05 | Nếu người khôi phục khác tác giả, hệ thống phải từ chối. |
| FR-M03-16.06 | Khi tác giả khôi phục một bài vốn ở trạng thái Chờ duyệt trước khi xóa, hệ thống phải đưa bài về Nháp. |

### 5.17 FR-M03-17 Chuyển bài hết hạn khôi phục sang Đã xóa hẳn

**Yêu cầu cấp trên:** Hệ thống phải tự gắn cờ Đã xóa hẳn cho bài đã xóa khi hết thời hạn khôi phục, giữ nguyên mọi dữ liệu của bài.

**Lý do:** Stakeholder chốt: "post, comment và những thứ có thể report ta chỉ cho xoá mềm thôi, gắn cờ vào là được"; vẫn giữ 7 ngày để khôi phục vì 7 ngày đủ để người dùng nhận ra lỡ tay xóa.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M03-17.01 | Khi bài Đã xóa hết thời hạn khôi phục, hệ thống phải gắn cờ Đã xóa hẳn cho bài. |
| FR-M03-17.02 | Khi gắn cờ Đã xóa hẳn, hệ thống phải giữ nguyên nội dung bài, tệp đính kèm, poll, phiếu bình chọn, lịch sử sửa, liên kết với Topic, Tag và bình luận của bài. |
| FR-M03-17.03 | Trong khi bài ở trạng thái Đã xóa hẳn, hệ thống phải không hiển thị bài cho người dùng ở bất kỳ đâu, kể cả tab "Đã xóa" của tác giả, trừ đường xem lại ở FR-M03-07.08. |
| FR-M03-17.04 | Hệ thống phải cho Mod, Admin xem bài Đã xóa, kể cả bài Đã xóa hẳn, chỉ trong báo cáo, lịch sử báo cáo hoặc khiếu nại liên quan tới chính bài đó, không có chỗ duyệt hay tìm kiếm bài đã xóa. |

### 5.18 Quy tắc nghiệp vụ

| ID | Loại | Quy tắc | Ví dụ |
|---|---|---|---|
| BR-M03-01 | Sự kiện | Hệ thống chỉ có một loại bài viết; mọi dạng nội dung dùng chung loại bài này, không có trường loại bài. | — |
| BR-M03-02 | Sự kiện | Bài viết gồm tiêu đề và nội dung giàu định dạng; Lớp/Khối, poll và tệp đính kèm là phần tùy chọn. Topic và Tag của bài theo quy tắc của M05. | — |
| BR-M03-03 | Ràng buộc | Trình soạn bài hỗ trợ: đậm, nghiêng, gạch chân, gạch ngang, tô sáng; tiêu đề mục H1–H3; danh sách chấm, danh sách số, danh sách việc cần làm; code trong dòng và khối code có tô màu cú pháp; công thức LaTeX; bảng; trích dẫn; đường kẻ ngang; liên kết có nhãn tùy chỉnh. | — |
| BR-M03-04 | Ràng buộc | Không chèn ảnh vào trong nội dung bài; mọi ảnh và tài liệu là tệp đính kèm hiện ở phần dưới nội dung. | — |
| BR-M03-05 | Ràng buộc | Công thức LaTeX được nhập dạng mã thô; không có trình soạn công thức trực quan. | Tác giả gõ \frac{1}{2} trong khối công thức: bài hiển thị phân số một phần hai. Không có bảng chọn ký hiệu. |
| BR-M03-06 | Ràng buộc | Lớp/Khối trên bài là tùy chọn, nhận một trong ba giá trị 10, 11, 12, do tác giả chọn; không phụ thuộc Lớp/Khối trên hồ sơ tác giả. | Không chọn: hợp lệ. Chọn 11: hợp lệ. Hồ sơ tác giả ghi 12, bài chọn 10: hợp lệ. |
| BR-M03-07 | Ràng buộc | Ảnh đính kèm có định dạng JPEG, PNG hoặc WebP, mỗi ảnh tối đa 5 MB, mỗi bài tối đa 10 ảnh. | Ảnh PNG 5 MB: nhận. Ảnh 5,1 MB: từ chối. Ảnh GIF: từ chối. Bài đã có 10 ảnh, thêm ảnh thứ 11: từ chối. |
| BR-M03-08 | Ràng buộc | Tài liệu đính kèm có định dạng PDF, DOCX, XLSX hoặc PPTX, mỗi tệp tối đa 20 MB, mỗi bài tối đa 3 tài liệu; giới hạn ảnh và giới hạn tài liệu tính riêng. Tài liệu không được quét mã độc ở MS1. | PDF 20 MB: nhận. PDF 21 MB: từ chối. Tệp ZIP: từ chối. Bài có 10 ảnh và 3 tài liệu: hợp lệ. Thêm tài liệu thứ 4: từ chối. |
| BR-M03-09 | Ràng buộc | Mỗi bài có tối đa 1 poll; mỗi poll có từ 2 đến 10 lựa chọn. | Poll 1 lựa chọn: từ chối. 2 lựa chọn: nhận. 10 lựa chọn: nhận. 11 lựa chọn: từ chối. Thêm poll thứ hai vào bài: từ chối. |
| BR-M03-10 | Sự kiện | Poll là poll đóng: chỉ tác giả đặt các lựa chọn; người bình chọn chỉ chọn trong các lựa chọn có sẵn. | — |
| BR-M03-11 | Ràng buộc | Poll có hai tùy chọn: chọn một hoặc chọn nhiều (mặc định chọn nhiều), và hiện kết quả trước khi bình chọn (mặc định tắt). Khi chọn nhiều, mỗi người chọn từ 1 đến tất cả lựa chọn; khi chọn một, mỗi người chọn đúng 1 lựa chọn. Cấu hình đổi được khi bài còn là nháp và bị khóa khi bài đã gửi. | Poll 4 lựa chọn, chọn nhiều: chọn 1, 2, 3 hoặc cả 4 đều được. Chọn một: chọn 2 lựa chọn bị từ chối. Bài đã gửi, tác giả đổi sang chọn một: từ chối. |
| BR-M03-12 | Ràng buộc | Poll bắt buộc có hạn kết thúc, và hạn kết thúc không được trước thời điểm hiện tại khi đặt hoặc đổi. | Tạo poll không đặt hạn: từ chối. Hôm nay 15/10 10:00, đặt hạn 15/10 09:00: từ chối. |
| BR-M03-13 | Kích hoạt | Poll đóng khi đến hạn kết thúc hoặc khi tác giả kết thúc ngay; poll đã đóng không nhận phiếu mới, không cho đổi phiếu hay bỏ chọn. | Hạn 20/10 10:00. Phiếu lúc 20/10 09:59: nhận. Phiếu lúc 20/10 10:00: từ chối. Tác giả kết thúc ngay lúc 19/10 08:00: phiếu lúc 19/10 08:01 bị từ chối. |
| BR-M03-14 | Ràng buộc | Trong lúc poll còn mở, tác giả đổi được hạn kết thúc sớm hơn hoặc muộn hơn, miễn không trước thời điểm hiện tại; "kết thúc ngay" là đặt hạn bằng thời điểm hiện tại. Poll đã đóng không mở lại được và không đổi hạn được. | Hạn 20/10 10:00. Ngày 15/10 đổi thành 18/10 10:00: nhận. Đổi thành 25/10: nhận. Ngày 15/10 09:00 bấm kết thúc ngay: hạn thành 15/10 09:00, poll đóng. Poll đã đóng, dời hạn tới 30/10: từ chối. |
| BR-M03-15 | Tính toán | Khi poll còn mở, kết quả hiện cho người chưa bình chọn chỉ khi tùy chọn hiện kết quả trước khi bình chọn bật; người đã bình chọn thấy kết quả. Khi poll đã đóng, mọi người xem bài thấy kết quả. Phần trăm của một lựa chọn = số lượt chọn lựa chọn đó ÷ tổng lượt chọn của poll, làm tròn tới số nguyên; tổng hiển thị có thể là 99% hoặc 101%. | 4 người, An chọn A và C, ba người còn lại chọn A, A và B, B: A 3 lượt, B 2, C 1 → tổng 6 → A 50%, B 33%, C 17%. 3 lượt chia đều A, B, C → 33%, 33%, 33% (tổng 99%). 6 lượt A 1, B 1, C 4 → 17%, 17%, 67% (tổng 101%). |
| BR-M03-16 | Ràng buộc | Trong lúc poll còn mở, người đã bình chọn luôn được đổi phiếu và bỏ chọn; khi poll đã đóng thì không. | Bình chọn A, đổi sang B khi poll còn mở: nhận. Bỏ chọn B: nhận, Bình không còn phiếu. Sau khi poll đóng, đổi phiếu: từ chối. |
| BR-M03-17 | Sự kiện | Trạng thái của bài viết gồm ba phần độc lập: trạng thái đăng, trạng thái kiểm duyệt và mức khóa (kèm người khóa). | — |
| BR-M03-18 | Suy diễn | Bài hiển thị công khai khi và chỉ khi trạng thái đăng là Đã đăng và trạng thái kiểm duyệt là Bình thường. Mức khóa không ảnh hưởng việc hiển thị. Bài trong nhóm Private chỉ hiện cho thành viên nhóm (M11). | Đã đăng + Bình thường + Khóa toàn bộ: hiển thị. Đã đăng + Bị gắn cờ: không hiển thị. Tự ẩn + Bình thường: không hiển thị. |
| BR-M03-19 | Kích hoạt | Khi tác giả khác Admin gửi bài không thuộc nhóm trong lúc công tắc AI tổng và công tắc Moderation đều bật, bài chuyển sang Chờ duyệt, không hiện với người khác, và được quét nội dung. | — |
| BR-M03-20 | Suy diễn | Kết quả quét bài vừa gửi: điểm quét dưới 0.5 → Đã đăng; từ 0.5 đến dưới 0.9 → giữ Chờ duyệt và chờ Mod duyệt; từ 0.9 trở lên → AI tự từ chối, không qua Mod. Hai ngưỡng 0.9 và 0.5 là giá trị tạm, có thể chỉnh sau. | 0.49 → Đã đăng. 0.5 → chờ Mod. 0.89 → chờ Mod. 0.9 → Bị từ chối. |
| BR-M03-21 | Suy diễn | Nếu AI đang bật mà bước quét thất bại sau một lần thử lại, bài giữ Chờ duyệt và chờ Mod duyệt; hệ thống không tự đăng bài. | Quét lần đầu quá thời gian chờ, lần thử lại cũng lỗi: bài vào hàng chờ Mod, vẫn Chờ duyệt. |
| BR-M03-22 | Suy diễn | Khi công tắc AI tổng hoặc công tắc Moderation đang tắt, bài gửi được đăng ngay, không quét; người dùng dựa vào báo cáo để xử lý vi phạm. Khi bật lại, hệ thống không quét lại các bài đã đăng trong lúc tắt. | AI tắt từ 09:00 đến 10:00. Bài gửi 09:30: Đã đăng ngay. 10:00 bật lại: bài 09:30 không bị quét. Bài gửi 10:05: Chờ duyệt và được quét. |
| BR-M03-23 | Kích hoạt | Khi Mod hoặc Admin duyệt một bài Chờ duyệt: chấp nhận → Đã đăng; từ chối → Bị từ chối, kèm lý do bắt buộc. | Mod từ chối mà không nhập lý do: từ chối thao tác. |
| BR-M03-24 | Suy diễn | Bài Bị từ chối được tác giả sửa và gửi lại; khi gửi lại, bài đi lại luồng như bài mới gửi (BR-M03-19 đến BR-M03-22). | — |
| BR-M03-25 | Ràng buộc | Luồng gửi, quét và duyệt của BR-M03-19 đến BR-M03-24 áp dụng cho bài không thuộc nhóm; bài thuộc nhóm theo cổng duyệt của M11. Ngoại lệ: bài của Owner nhóm trong nhóm của mình có điểm quét từ 0.5 đến nhỏ hơn 0.9, hoặc quét thất bại, vào hàng chờ duyệt của Mod như bài không thuộc nhóm (M11). | Owner An gửi bài vào nhóm của mình, điểm 0.6 → hàng chờ duyệt của Mod. Member C gửi bài vào nhóm đó, điểm 0.6 → hàng chờ duyệt của nhóm (M11). |
| BR-M03-26 | Kích hoạt | Khi tác giả sửa bài Đã đăng, hoặc hiện lại bài Tự ẩn có bản sửa được lưu trong lúc ẩn, trong lúc công tắc AI tổng và công tắc Moderation đều bật, bài được quét lại; bài vẫn ở trạng thái hiển thị (với nội dung đã sửa) trong lúc quét. Điểm quét dưới 0.5: giữ nguyên. Điểm từ 0.5 trở lên, kể cả từ 0.9: bài sang Bị gắn cờ, bị ẩn, chờ Mod xét. Quét lỗi: giữ nguyên, bài vẫn hiển thị. Sửa bài Tự ẩn không quét lúc lưu. Việc tự từ chối ở điểm từ 0.9 chỉ áp dụng cho bài vừa gửi. | Quét lại 0.3: bài vẫn hiện. 0.6: Bị gắn cờ. 0.95: Bị gắn cờ (không tự từ chối). Lỗi: bài vẫn hiện. X ẩn bài P, sửa hai lần (không quét), rồi hiện lại → P hiện ngay và được quét một lần; 0.7 → Bị gắn cờ, ẩn. X ẩn P rồi hiện lại mà không sửa → không quét. |
| BR-M03-27 | Ràng buộc | Mỗi lần tác giả lưu bản sửa của bài đã gửi, hệ thống ghi một phiên bản vào lịch sử sửa (nội dung trước lần sửa, người sửa, thời điểm sửa). Bài có ít nhất một lần sửa hiện nhãn "(đã chỉnh sửa)" và nút "Xem lịch sử"; ai xem được bài thì xem được lịch sử sửa. | Bài đăng 10:00, sửa lúc 10:30 và 11:00: lịch sử có 2 lần sửa, bài có nhãn. Bài chưa sửa lần nào: không có nhãn. |
| BR-M03-28 | Ràng buộc | Việc Mod hoặc Admin đổi Topic, Tag trên bài của người khác không ghi vào lịch sử sửa, không làm hiện nhãn "(đã chỉnh sửa)" và không báo cho tác giả. | Bài chưa sửa lần nào, Mod đổi Topic: bài vẫn không có nhãn. |
| BR-M03-29 | Ràng buộc | Tác giả tự ẩn bài Đã đăng của mình (sang Tự ẩn) và hiện lại bài đã tự ẩn (về Đã đăng) bất kỳ lúc nào; bài được sửa trong lúc ẩn thì quét lại khi hiện lại (BR-M03-26). | — |
| BR-M03-30 | Ràng buộc | Khóa bình luận chặn bình luận mới trên bài; các bình luận đã có vẫn hiển thị. Tác giả (với bài của mình), Mod và Admin đặt được mức này. | — |
| BR-M03-31 | Ràng buộc | Chỉ Mod và Admin đặt được Khóa toàn bộ; mức này chặn bình luận mới, mọi thao tác upvote (upvote mới, rút lại upvote, trên bài và trên bình luận của bài) và bình chọn poll (kể cả đổi phiếu, bỏ chọn); bookmark và báo cáo vẫn dùng được. | Bài bị khóa toàn bộ: Bình bình luận, upvote bài, upvote một bình luận của bài, rút upvote cũ, bình chọn → từ chối; bookmark, báo cáo → được. |
| BR-M03-32 | Ràng buộc | Hệ thống ghi người khóa. Khi người khóa là Mod hoặc Admin, tác giả không mở khóa hay đổi mức khóa được. Khi tác giả khóa bình luận, tác giả và Mod, Admin đều mở được. | Tác giả khóa bình luận rồi mở lại: được. Mod khóa bình luận, tác giả mở: từ chối. Tác giả khóa bình luận, Mod nâng lên Khóa toàn bộ: người khóa thành Mod. |
| BR-M03-33 | Suy diễn | Bài có trạng thái kiểm duyệt Bị Mod ẩn thì tác giả không tự hiện lại được; tác giả phải khiếu nại (M09). | — |
| BR-M03-34 | Kích hoạt | Khi tác giả xóa bài ở bất kỳ trạng thái nào trừ Đã xóa, bài chuyển sang Đã xóa; hệ thống ghi thời điểm xóa và trạng thái trước khi xóa; bài không còn hiện ở feed và mọi nơi công khai, và hiện trong tab "Đã xóa" trên hồ sơ tác giả. | — |
| BR-M03-35 | Ràng buộc | Tác giả khôi phục được bài Đã xóa trong thời hạn khôi phục là 7 × 24 giờ kể từ lúc xóa. Bài khôi phục về trạng thái trước khi xóa; riêng bài trước đó ở Chờ duyệt thì về Nháp. | Xóa bài Đã đăng lúc 01/10 21:00: khôi phục lúc 08/10 20:59 → Đã đăng. Lúc 08/10 21:00: đã xóa hẳn. Xóa bài Tự ẩn rồi khôi phục → Tự ẩn. Xóa bài Chờ duyệt rồi khôi phục → Nháp. |
| BR-M03-36 | Ràng buộc | Bài có trạng thái kiểm duyệt Bị Mod ẩn ("Mod gỡ bài") thì tác giả không khôi phục được sau khi xóa. | — |
| BR-M03-37 | Kích hoạt | Khi bài Đã xóa hết thời hạn khôi phục, hệ thống gắn cờ Đã xóa hẳn; mọi dữ liệu của bài được giữ (chỉ là cờ, không xóa dữ liệu). Với người dùng bài không còn và không khôi phục được. Mod, Admin xem bài qua báo cáo, lịch sử báo cáo, khiếu nại; tác giả xem lại chỉ đọc từ thông báo xử lý hoặc khiếu nại, không thấy thông tin người báo cáo. | Tác giả xóa bài P lúc 01/10 21:00 → khôi phục được tới trước 08/10 21:00; lúc 08/10 21:00 P được gắn cờ Đã xóa hẳn, dữ liệu còn nguyên. Y đã báo cáo P trước đó → Mod mở báo cáo vẫn xem được P. Guest mở đường dẫn P → "không tồn tại". |
| BR-M03-38 | Ràng buộc | Tác giả đang ở mức cảnh cáo MEDIUM hoặc HEAVY không được lưu bài nháp mới, gửi bài nháp và gửi lại bài Bị từ chối; vẫn được sửa bài đã đăng, khôi phục bài đã xóa và bình chọn poll. | An đang MEDIUM: lưu nháp mới → từ chối. Gửi nháp cũ → từ chối. Sửa bài đã đăng → được. Bình chọn poll → được. |
| BR-M03-39 | Sự kiện | Guest xem được bài hiển thị công khai, kể cả bài trong nhóm Public. | — |
| BR-M03-40 | Ràng buộc | Khi gửi, bài phải có tiêu đề, và phải có nội dung hoặc poll; poll thay được cho nội dung, tệp đính kèm thì không. | Tiêu đề + nội dung: nhận. Tiêu đề + poll, nội dung trống: nhận. Tiêu đề + chỉ tệp PDF: từ chối. Không tiêu đề: từ chối. |
| BR-M03-41 | Ràng buộc | Bài nháp phải có ít nhất một trong bốn phần: tiêu đề, nội dung, poll, tệp đính kèm. | Chỉ có tiêu đề: lưu được. Chỉ chọn Lớp/Khối: từ chối. |
| BR-M03-42 | Ràng buộc | Tiêu đề tối đa 150 ký tự; nội dung tối đa 6.000 từ, một từ là một cụm chữ ngăn cách bởi khoảng trắng, đếm trên phần chữ người đọc thấy. Giới hạn áp dụng khi lưu nháp và khi gửi. | Tiêu đề 150 ký tự: nhận; 151: từ chối. Nội dung 6.000 từ: nhận; 6.001: từ chối. "x^2 + 2x + 1 = 0" là 7 từ. |
| BR-M03-43 | Kích hoạt | Khi tiêu đề hoặc nội dung vượt giới hạn trong lúc soạn hoặc sửa, hệ thống cảnh báo ngay kèm số hiện tại so với giới hạn; lưu hoặc gửi khi đang vượt thì bị từ chối và nội dung được giữ nguyên. | Tiêu đề 162 ký tự: cảnh báo "162/150" hiện ngay; bấm gửi → từ chối, tiêu đề vẫn còn để sửa. |
| BR-M03-44 | Ràng buộc | Poll chỉ được thêm hoặc bỏ khi bài chưa gửi. Sau khi gửi, tác giả chỉ được thêm lựa chọn (tổng vẫn tối đa 10) và đổi hạn trong lúc poll còn mở; không sửa hay xóa lựa chọn đã có. Chỉ tác giả thêm được lựa chọn. | Bài đã đăng có poll 9 lựa chọn: thêm lựa chọn thứ 10 → nhận; thứ 11 → từ chối. Sửa chữ của lựa chọn cũ → từ chối. Bỏ poll → từ chối. |
| BR-M03-45 | Sự kiện | Tác giả được bình chọn trong poll của chính bài mình. | — |
| BR-M03-46 | Suy diễn | Bài vừa gửi bị AI tự từ chối thì tác giả thấy nhóm vi phạm AI phát hiện; tác giả sửa và gửi lại không giới hạn số lần, mỗi lần đều được quét lại; phản đối thì khiếu nại qua M09. Khiếu nại được chấp nhận thì bài chuyển Đã đăng ngay, không quét lại; nếu tác giả đã sửa và gửi lại bài trước khi có kết luận thì trạng thái bài không đổi (M09). | Bài bị từ chối lúc 09:00, khiếu nại được chấp nhận lúc 15:00 → Đã đăng lúc 15:00. Tác giả đã gửi lại bản sửa lúc 10:00 và bài đã được đăng → khiếu nại được chấp nhận lúc 15:00 không đổi trạng thái bài. |
| BR-M03-47 | Ràng buộc | Tác giả sửa được bài ở trạng thái Nháp, Bị từ chối, Đã đăng, Tự ẩn, kể cả khi bài đang bị khóa; không sửa được bài Chờ duyệt, Đã xóa hoặc Bị Mod ẩn. | Bài Chờ duyệt: sửa → từ chối. Bài Đã đăng bị Mod khóa bình luận: sửa → được. |
| BR-M03-48 | Sự kiện | Bài viết mới có trạng thái kiểm duyệt Bình thường. "Mod gỡ bài" chính là trạng thái kiểm duyệt Bị Mod ẩn. | — |
| BR-M03-49 | Ràng buộc | Mod và Admin không xem bài Nháp, Bị từ chối của người khác; Mod, Admin xem bài Chờ duyệt qua hàng chờ duyệt, bài Bị gắn cờ, Bị Mod ẩn qua M08, M09, và bài Tự ẩn, Đã xóa, Đã xóa hẳn chỉ trong báo cáo, lịch sử báo cáo, khiếu nại liên quan tới bài đó. | Y báo cáo bài P của X; X tự ẩn P → Mod mở báo cáo vẫn xem được P. Mod mở thẳng bài nháp của X → từ chối. |
| BR-M03-50 | Sự kiện | MS1 không có Accepted Answer và bài viết không có ảnh bìa; ảnh dùng qua phần đính kèm. | — |
| BR-M03-51 | Sự kiện | Bài của Admin không bị hệ thống quét hay duyệt: gửi (hoặc gửi lại) là Đã đăng ngay, sửa hay hiện lại sau khi sửa không bị quét lại, kể cả khi công tắc AI tổng và Moderation đang bật. Bài của Admin trong nhóm vẫn qua bước duyệt của nhóm (M11). | AI đang bật. Admin gửi bài lúc 10:00 → Đã đăng lúc 10:00, không vào hàng chờ. User gửi bài lúc 10:00 → Chờ duyệt và được quét. Admin sửa bài đã đăng → không quét lại. |

### 5.19 Dữ liệu nghiệp vụ

| Thực thể | Thuộc tính nguồn đã nêu | Quan hệ |
|---|---|---|
| Bài viết | Tiêu đề (tối đa 150 ký tự); nội dung giàu định dạng (tối đa 6.000 từ); nội dung dạng chữ thuần (dùng cho tìm kiếm); tác giả; Lớp/Khối (tùy chọn); trạng thái đăng; trạng thái kiểm duyệt; mức khóa và người khóa; lý do từ chối (khi bị Mod từ chối); thời điểm tạo; thời điểm cập nhật; thời điểm xóa và trạng thái trước khi xóa (khi Đã xóa); cờ Đã xóa hẳn (khi hết thời hạn khôi phục); có bản sửa được lưu trong lúc Tự ẩn chưa được quét | Thuộc một tác giả (M01); có 0–1 Poll, 0–10 ảnh và 0–3 tài liệu đính kèm, nhiều Phiên bản sửa; có Topic, Tag (M05); có thể thuộc một nhóm (M11); có bình luận (M04) |
| Tệp đính kèm | Loại (ảnh hoặc tài liệu), định dạng tệp, dung lượng | Thuộc một Bài viết |
| Poll | Các lựa chọn (2–10); chọn một hoặc chọn nhiều; hiện kết quả trước khi bình chọn; hạn kết thúc; đã đóng | Thuộc một Bài viết; có nhiều Phiếu bình chọn |
| Phiếu bình chọn | Người bình chọn; các lựa chọn đã chọn | Thuộc một Poll và một người dùng |
| Phiên bản sửa | Nội dung bài trước lần sửa; người sửa; thời điểm sửa | Thuộc một Bài viết |

<!-- Draft DM-2.1 còn nêu ảnh bìa, số lượt xem, số sao, số bình luận, is_anonymous, accepted_comment_id. Không đưa vào bảng:
     lượt xem hoãn (TBD-M03-01); số sao thuộc M12; số bình luận thuộc M04; ẩn danh thuộc M11 (DEC-009);
     ảnh bìa và Accepted Answer không có ở MS1 (DEC-169). -->

**Ma trận CRUD:**

| Thực thể | Tạo | Đọc | Sửa | Xóa |
|---|---|---|---|---|
| Bài viết | FR-M03-01.01 | FR-M03-07.01, FR-M03-07.03 | FR-M03-11.01, FR-M03-04.01, FR-M03-05.01, FR-M03-06.02, FR-M03-13.01, FR-M03-14.01; trạng thái kiểm duyệt: M08, M09 | FR-M03-15.01 (xóa mềm), FR-M03-17.01 (gắn cờ Đã xóa hẳn); xóa dữ liệu: Không có (BR-M03-37) |
| Tệp đính kèm | FR-M03-02.01 | FR-M03-02.03 | FR-M03-02.02 (bỏ tệp cũ, thêm tệp mới) | FR-M03-02.01; theo bài: giữ, không xóa (FR-M03-17.02) |
| Poll | FR-M03-03.01 | FR-M03-07.04 | FR-M03-09.01, FR-M03-09.02, FR-M03-09.06, FR-M03-10.01; khi bài còn là nháp: FR-M03-03.10; sau khi gửi, sửa lựa chọn cũ và cấu hình: Không có (BR-M03-44) | Khi bài còn là nháp: FR-M03-03.10; sau khi gửi: Không có (BR-M03-44); theo bài: giữ, không xóa (FR-M03-17.02) |
| Phiếu bình chọn | FR-M03-08.01 | FR-M03-08.10 (kết quả theo BR-M03-15) | FR-M03-08.04 | FR-M03-08.05 (bỏ chọn); theo bài: giữ, không xóa (FR-M03-17.02) |
| Phiên bản sửa | FR-M03-11.02 | FR-M03-12.02 | — | Theo bài: giữ, không xóa (FR-M03-17.02) |

<!-- Ô "—" ở cột Sửa của Phiên bản sửa: không chức năng nào sửa lịch sử, không ảnh hưởng hành vi người dùng thấy, nên không tạo GAP.
     Bản 1.1 (DEC-184): bài Đã xóa hẳn giữ nguyên tệp, poll, phiếu, lịch sử sửa (FR-M03-17.02); chúng chỉ không còn chỗ hiển thị với người dùng. -->

### 5.20 Chuyển trạng thái

#### Bài viết — trạng thái đăng

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Tác giả tạo bài mới và lưu chưa gửi | Bài không trống; không bị chặn bởi BR-M03-38 | Nháp | FR-M03-01.01, FR-M03-01.13 |
| Nháp | Tác giả gửi bài | AI tổng và công tắc Moderation bật; bài không thuộc nhóm; tác giả khác Admin | Chờ duyệt | FR-M03-04.01 |
| Nháp | Admin gửi bài của mình | Bài không thuộc nhóm | Đã đăng | FR-M03-04.11 |
| Nháp | Tác giả gửi bài | AI tổng hoặc công tắc Moderation tắt; bài không thuộc nhóm | Đã đăng | FR-M03-04.03 |
| Chờ duyệt | Quét xong | Điểm quét < 0.5 | Đã đăng | FR-M03-05.01 |
| Chờ duyệt | Quét xong, hoặc quét thất bại sau một lần thử lại; bài vào hàng chờ Mod | 0.5 ≤ điểm quét < 0.9, hoặc quét thất bại | Chờ duyệt | FR-M03-05.02, FR-M03-05.04 |
| Chờ duyệt | Quét xong | Điểm quét ≥ 0.9 | Bị từ chối | FR-M03-05.03 |
| Chờ duyệt | Mod hoặc Admin chấp nhận | — | Đã đăng | FR-M03-06.02 |
| Chờ duyệt | Mod hoặc Admin từ chối | Có lý do | Bị từ chối | FR-M03-06.03 |
| Bị từ chối | Tác giả sửa và gửi lại | AI tổng và công tắc Moderation bật; tác giả khác Admin | Chờ duyệt | FR-M03-04.04, FR-M03-04.01 |
| Bị từ chối | Admin sửa và gửi lại bài của mình | Bài không thuộc nhóm | Đã đăng | FR-M03-04.11 |
| Bị từ chối | Khiếu nại về bài bị AI tự từ chối được chấp nhận (M09) | Tác giả chưa gửi lại bài trước khi có kết luận | Đã đăng | FR-M09-08.12 |
| Bị từ chối | Tác giả sửa và gửi lại | AI tổng hoặc công tắc Moderation tắt | Đã đăng | FR-M03-04.04, FR-M03-04.03 |
| Đã đăng | Tác giả tự ẩn | — | Tự ẩn | FR-M03-13.01 |
| Tự ẩn | Tác giả hiện lại | — | Đã đăng | FR-M03-13.02 |
| Nháp | Tác giả xóa | — | Đã xóa | FR-M03-15.01 |
| Chờ duyệt | Tác giả xóa | — | Đã xóa | FR-M03-15.01, FR-M03-15.06 |
| Bị từ chối | Tác giả xóa | — | Đã xóa | FR-M03-15.01 |
| Đã đăng | Tác giả xóa | — | Đã xóa | FR-M03-15.01 |
| Tự ẩn | Tác giả xóa | — | Đã xóa | FR-M03-15.01 |
| Đã xóa | Tác giả khôi phục | Trong thời hạn khôi phục; không Bị Mod ẩn; trước khi xóa là Nháp hoặc Chờ duyệt | Nháp | FR-M03-16.01, FR-M03-16.06 |
| Đã xóa | Tác giả khôi phục | Trong thời hạn khôi phục; không Bị Mod ẩn; trước khi xóa là Bị từ chối | Bị từ chối | FR-M03-16.01 |
| Đã xóa | Tác giả khôi phục | Trong thời hạn khôi phục; không Bị Mod ẩn; trước khi xóa là Đã đăng | Đã đăng | FR-M03-16.01 |
| Đã xóa | Tác giả khôi phục | Trong thời hạn khôi phục; không Bị Mod ẩn; trước khi xóa là Tự ẩn | Tự ẩn | FR-M03-16.01 |
| Đã xóa | Hết thời hạn khôi phục | — | Đã xóa hẳn (trạng thái cuối, dữ liệu giữ nguyên) | FR-M03-17.01, FR-M03-17.02 |

Bài Bị từ chối mà tác giả không gửi lại hay xóa thì ở mãi trạng thái này.

#### Bài viết — trạng thái kiểm duyệt

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Bài được tạo | — | Bình thường | FR-M03-01.12 |
| Bình thường | Quét lại sau khi sửa bài Đã đăng, hoặc sau khi hiện lại bài Tự ẩn đã sửa trong lúc ẩn, cho điểm từ 0.5 trở lên | Công tắc AI tổng và công tắc Moderation đều bật | Bị gắn cờ | FR-M03-05.07, FR-M03-13.06 |
| Bị gắn cờ | Mod xét và giữ bài | — | Bình thường | FR-M08-07.01 |
| Bị gắn cờ | Mod xét và ẩn bài | — | Bị Mod ẩn | FR-M08-07.02 |
| Bị Mod ẩn | Khiếu nại của tác giả được chấp nhận | — | Bình thường | FR-M09-08.08 |

<!-- Hai dòng "Mod xét…" suy ra từ DEC-032 "FLAGGED: awaiting mod" và "HIDDEN: mod-hidden". -->

#### Bài viết — mức khóa

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Bài được tạo | — | Không khóa | FR-M03-01.09 |
| Không khóa | Tác giả, Mod hoặc Admin khóa bình luận | Người khóa ghi là người thực hiện | Khóa bình luận | FR-M03-14.01, FR-M03-14.02 |
| Không khóa | Mod hoặc Admin khóa toàn bộ | Người khóa ghi là Mod | Khóa toàn bộ | FR-M03-14.03 |
| Khóa bình luận | Mod hoặc Admin khóa toàn bộ | Người khóa ghi là Mod | Khóa toàn bộ | FR-M03-14.03 |
| Khóa bình luận | Mở khóa | Người khóa là tác giả: tác giả, Mod hoặc Admin mở; người khóa là Mod: chỉ Mod hoặc Admin mở | Không khóa | FR-M03-14.07, FR-M03-14.08 |
| Khóa toàn bộ | Mod hoặc Admin mở khóa | — | Không khóa | FR-M03-14.08 |
| Khóa toàn bộ | Mod hoặc Admin hạ mức | Người khóa giữ là Mod | Khóa bình luận | FR-M03-14.08 |

#### Poll

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Tác giả thêm poll vào bài | 2–10 lựa chọn, có hạn kết thúc | Đang mở | FR-M03-03.01 |
| Đang mở | Tác giả đổi hạn kết thúc | Hạn mới không trước thời điểm hiện tại | Đang mở | FR-M03-09.01 |
| Đang mở | Tác giả thêm lựa chọn | Tổng không quá 10 | Đang mở | FR-M03-09.06 |
| Đang mở | Đến hạn kết thúc | — | Đã đóng | FR-M03-10.01 |
| Đang mở | Tác giả kết thúc ngay | Hạn đặt bằng thời điểm hiện tại | Đã đóng | FR-M03-09.02 |

Đã đóng là trạng thái cuối: poll không mở lại được (BR-M03-14).

### 5.21 Giao tiếp với module khác

| Hướng | Module | Nội dung ở mức nghiệp vụ | Yêu cầu |
|---|---|---|---|
| Cung cấp | M04 | Bài viết là nơi chứa bình luận; mức khóa của bài chặn bình luận mới | FR-M03-14.04, FR-M03-14.05 |
| Cung cấp | M01 | Lưu, sửa nội dung bài chứa lượt nhắc tên (lượt nhắc đi theo bài, giữ cùng bài khi Đã xóa hẳn); thời điểm bài trở thành công khai (sau bước quét) để gửi thông báo nhắc tên | FR-M03-01.01, FR-M03-11.01, FR-M03-17.02, FR-M03-05.01 |
| Cung cấp | M05 | Thao tác soạn, gửi, sửa bài và trạng thái nháp, đã gửi, là nơi áp quy tắc Topic, Tag và gợi ý Topic; khi bài chuyển Đã xóa hẳn, liên kết bài–Topic, bài–Tag được giữ cùng bài (bài không còn hiển thị) | FR-M03-01.01, FR-M03-04.01, FR-M03-11.01, FR-M03-17.02 |
| Cung cấp | M06, M14 | Bài viết đang hiển thị công khai và nội dung chữ của bài | FR-M03-07.01 |
| Cung cấp | M07 | Sự kiện bài được đăng, bài bị từ chối, poll kết thúc. Sự kiện bài được đăng kèm tác giả, bài có đăng ẩn danh không và có phải lần đầu hiển thị công khai không, để M07 báo bài mới cho người theo dõi tác giả (DEC-215) | FR-M03-05.01, FR-M03-05.03, FR-M03-06.02, FR-M03-06.03, FR-M03-10.02 |
| Dùng | M07 | Công tắc "Tắt thông báo cho bài này" hiện trên mỗi bài (FR-M07-08) | — |
| Cung cấp | M08 | Bài vào hàng chờ duyệt sau bước quét; bài đã sửa (hoặc tự ẩn đã sửa rồi hiện lại) bị bước quét lại gắn cờ; bài Tự ẩn xem được trong báo cáo | FR-M03-05.02, FR-M03-05.04, FR-M03-05.07 |
| Cung cấp | M12 | Thời điểm bài do tác giả xóa chuyển sang Đã xóa hẳn (mốc trừ điểm) | FR-M03-17.01 |
| Cung cấp | M02 | Thời điểm bài chuyển sang Đã xóa hẳn (mốc bỏ bookmark, DEC-174) | FR-M03-17.01 |
| Cung cấp | M08, M09 | Bài Đã xóa hẳn giữ nguyên dữ liệu để Mod, Admin xem trong báo cáo, lịch sử báo cáo, khiếu nại; tác giả xem lại từ thông báo xử lý, khiếu nại | FR-M03-17.02, FR-M03-17.04, FR-M03-07.08 |
| Cung cấp | M15 | Trạng thái của bài để thống kê | — |
| Dùng | M01 | Cách hiển thị bài theo trạng thái tài khoản tác giả (ẩn khi vô hiệu hóa hoặc xóa tài khoản, nhãn tài khoản bị khóa); nhắc tên trong bài | — |
| Dùng | M02 | Tab "Đã xóa" trên hồ sơ tác giả | FR-M03-15.03 |
| Dùng | M05 | Quy tắc Topic, Tag khi gửi và sửa bài; Mod, Admin đổi Topic, Tag trên bài người khác | FR-M03-11.05, FR-M03-11.06 |
| Dùng | M08 | Điểm quét; hàng chờ duyệt của Mod; gắn cờ, ẩn, gỡ bài; hạn chế tạo bài theo mức cảnh cáo | FR-M03-01.10, FR-M03-05.01, FR-M03-06.01 |
| Dùng | M09 | Khiếu nại bài bị Mod ẩn ("gỡ") hoặc bị AI tự từ chối; bài trở lại hiển thị khi khiếu nại thành công; bài bị AI tự từ chối được chấp nhận khiếu nại thì Đã đăng ngay, không quét lại | FR-M03-13.05, BR-M03-46 |
| Dùng | M10 | Công tắc AI tổng và công tắc Moderation | FR-M03-04.03, FR-M03-05.08 |
| Dùng | M11 | Luồng duyệt bài trong nhóm (kể cả bài nhóm quét thất bại chờ nhóm duyệt); đăng ẩn danh; bài trong nhóm Private; bài bị Owner, Group Mod gỡ khỏi nhóm (xóa mềm, M11 làm) | FR-M03-04.05 |
| Cung cấp | M11 | Soạn bài, trạng thái đăng, sửa, xóa của tác giả cho bài nhóm; hàng chờ duyệt của Mod cho bài của Owner nhóm có điểm quét từ 0.5 đến nhỏ hơn 0.9 hoặc quét thất bại | FR-M03-04.05, FR-M03-05.02, FR-M03-05.04 |
| Dùng | M12 | Trừ điểm khi tác giả xóa bài hoặc bài bị Mod gỡ; thao tác upvote, rút upvote (bị chặn khi bài ở mức Khóa toàn bộ, DEC-246) | FR-M03-14.06 |
| Dùng | M13 | Gọi AI kiểm duyệt (thời gian chờ, một lần thử lại), tóm tắt bài (chỉ người đã đăng nhập), embedding | FR-M03-05.04 |
| Cung cấp | M13 | Thời điểm bài chuyển sang Đã đăng theo mọi đường (quét sạch, Mod chấp nhận, AI tắt, bài của Admin) để tạo embedding; thay đổi tiêu đề, nội dung chữ để tạo lại embedding | FR-M03-04.03, FR-M03-04.11, FR-M03-05.01, FR-M03-06.02, FR-M03-11.01 |

### 5.22 AI hỗ trợ và hành vi khi tắt AI

Module dùng AI kiểm duyệt (M08, M13) để quét bài.

- Khi AI tổng và công tắc Moderation bật: bài gửi được quét trước khi đăng và kết quả theo điểm quét (FR-M03-04.01, FR-M03-05.01, FR-M03-05.02, FR-M03-05.03); bài đã đăng được quét lại sau khi sửa (FR-M03-05.05, FR-M03-05.06, FR-M03-05.07).
- Nếu AI không khả dụng (quét thất bại sau một lần thử lại): bài giữ Chờ duyệt và vào hàng chờ Mod, không tự đăng (FR-M03-05.04).
- Khi AI tổng hoặc công tắc Moderation tắt: bài gửi được đăng ngay, không quét; bật lại không quét bài cũ (FR-M03-04.03, FR-M03-05.08, FR-M03-05.09).
- Bài của Admin không bị quét dù AI bật hay tắt (FR-M03-04.11, FR-M03-05.15).

### 5.23 Yêu cầu HMI

Chưa có — chờ giai đoạn thiết kế.

### 5.24 Chuyển màn hình

Chưa có — chờ giai đoạn thiết kế.

## 6. Lịch sử sửa đổi

| Phiên bản | Ngày | Nội dung | Người sửa |
|---|---|---|---|
| 0.1 | 2026-10-11 | Tạo mới | Phạm Văn Đức |
| 1.0 | 2026-10-11 | Chốt sau 7 bước: 17 chức năng, 141 yêu cầu cấp dưới, 50 quy tắc; câu trả lời bước 6 ghi ở DEC-160–169 | Phạm Văn Đức |
| 1.1 | 2026-10-14 | Chốt 1.1. Theo OPEN-010 / DEC-184: bài hết hạn khôi phục chỉ gắn cờ Đã xóa hẳn, giữ dữ liệu (FR-M03-17 viết lại, thêm 17.03, 17.04); tác giả xem lại bài từ thông báo, khiếu nại (thêm FR-M03-07.08–07.10); ghi chú định nghĩa "Đã xóa hẳn". Theo DEC-185: Mod xem bài Tự ẩn trong báo cáo (FR-M03-07.11), quét lại khi hiện lại bài Tự ẩn đã sửa (FR-M03-05.14, 13.06). Rà soát: ngoại lệ nhóm Private ở FR-M03-07.01, BR-M03-18; thống nhất điều kiện công tắc AI; làm rõ FR-M03-05.06 | Phạm Văn Đức |
| 1.2 | 2026-10-15 | Đối chiếu với FR-M08 (DEC-190): báo cáo của người dùng không làm bài Bị gắn cờ — sửa định nghĩa "Trạng thái kiểm duyệt" ở 2.1, bỏ dòng "AI hoặc báo cáo gắn cờ bài" ở bảng chuyển trạng thái; cập nhật C.1, C.2, mốc nguồn. Chốt bản 1.2 | Phạm Văn Đức |
| 1.3 | 2026-10-20 | Đối chiếu với FR-M06: ghi chuỗi DEC-208, DEC-211 ở C.2; không đổi yêu cầu. Chốt bản 1.3 | Phạm Văn Đức |
| 1.4 | 2026-10-21 | Đối chiếu với FR-M07 (DEC-215): sự kiện bài được đăng cung cấp thêm tác giả, cờ ẩn danh, lần đầu công khai cho thông báo bài mới; thêm dòng "Dùng M07" (công tắc tắt thông báo bài). Không đổi yêu cầu. Chốt bản 1.4 | Phạm Văn Đức |
| 1.5 | 2026-10-21 | Đối chiếu với FR-M09, FR-M13: bài của Admin đăng ngay, không quét, không duyệt (FR-M03-04.11, FR-M03-05.15, BR-M03-51); khiếu nại bài bị AI từ chối được chấp nhận thì Đã đăng ngay (BR-M03-46, trạng thái); giao tiếp với M13 về embedding, tóm tắt; trạng thái kiểm duyệt trỏ tới FR-M08, FR-M09. Chốt bản 1.5 | Phạm Văn Đức |
| 1.6 | 2026-10-21 | Đối chiếu với FR-M11 (DEC-230, DEC-231, DEC-240): bài của Owner nhóm có điểm quét từ 0.5 đến nhỏ hơn 0.9 hoặc quét thất bại vào hàng chờ duyệt của Mod (FR-M03-04.05, BR-M03-25); thêm "Cung cấp M11"; "Dùng M11" ghi thêm bài nhóm quét lỗi chờ nhóm duyệt, bài bị gỡ khỏi nhóm. Chốt bản 1.6 | Phạm Văn Đức |
| 1.7 | 2026-10-23 | Rà lại với register tới DEC-247: Khóa toàn bộ chặn cả rút upvote và upvote bình luận của bài (DEC-246: FR-M03-14.06, BR-M03-31); dòng Dùng M12. Chốt bản 1.7 | Phạm Văn Đức |

## Phụ lục A. Truy vết

| ID | Nguồn | Căn cứ | Ghi chú |
|---|---|---|---|
| FR-M03-01 | DEC-029, DEC-030, DEC-031, DEC-140, QA-033, QA-034, DM-1.3, DM-2.1, DM-2.2, DM-3.3, F-POST-01, F-POST-03, F-POST-09, DM-2.4 | Nói thẳng | Lý do lấy từ DM-2.1, DM-2.4 |
| FR-M03-01.01 | DEC-031, DM-1.3 | Nói thẳng | — |
| FR-M03-01.02 | DEC-029 | Nói thẳng | — |
| FR-M03-01.03 | DEC-029 | Nói thẳng | — |
| FR-M03-01.04 | DEC-029, DEC-030 | Nói thẳng | — |
| FR-M03-01.05 | QA-034, DEC-140, DM-3.3, F-POST-09, GL:Lớp/Khối | Nói thẳng | — |
| FR-M03-01.06 | F-POST-09, DM-3.3 | Suy ra | Lớp/Khối chỉ nhận ba giá trị ⇒ giá trị khác bị từ chối |
| FR-M03-01.07 | QA-034, DEC-140 | Nói thẳng | — |
| FR-M03-01.08 | DM-2.1 | Nói thẳng | — |
| FR-M03-01.09 | DEC-033 | Suy ra | Mức khóa chỉ được đặt bởi thao tác khóa của tác giả hoặc Mod ⇒ bài mới chưa bị khóa |
| FR-M03-01.10 | DEC-079, DEC-163 | Nói thẳng | — |
| FR-M03-01.11 | DEC-030, DM-2.4 | Nói thẳng | — |
| FR-M03-01.12 | DEC-161 | Nói thẳng | — |
| FR-M03-01.13 | DEC-164 | Nói thẳng | — |
| FR-M03-01.14 | DEC-164 | Nói thẳng | — |
| FR-M03-01.15 | DEC-164 | Nói thẳng | — |
| FR-M03-01.16 | DEC-164 | Nói thẳng | — |
| FR-M03-01.17 | DEC-164 | Nói thẳng | — |
| FR-M03-02 | DEC-030, DEC-035, DM-2.2, F-POST-02, QA-025 | Nói thẳng | Phần tài liệu chờ Q-01. Lý do lấy từ QA-025 |
| FR-M03-02.01 | DEC-030, F-POST-02 | Nói thẳng | — |
| FR-M03-02.02 | DEC-030, DEC-037 | Suy ra | Phần đính kèm là một phần của bài ⇒ sửa bài gồm sửa phần đính kèm |
| FR-M03-02.03 | DEC-030 | Nói thẳng | — |
| FR-M03-02.04 | DEC-035 | Suy ra | Chỉ ba định dạng được nêu ⇒ định dạng khác bị từ chối |
| FR-M03-02.05 | DEC-035 | Suy ra | Tối đa 5 MB/ảnh ⇒ vượt thì từ chối |
| FR-M03-02.06 | DEC-035 | Suy ra | Tối đa 10 ảnh ⇒ ảnh thứ 11 bị từ chối |
| FR-M03-02.07 | DEC-035, DEC-160 | Suy ra | Chỉ bốn định dạng được nêu ⇒ định dạng khác bị từ chối |
| FR-M03-02.08 | DEC-035, DEC-160 | Suy ra | Tối đa 20 MB/tệp ⇒ vượt thì từ chối |
| FR-M03-02.09 | DEC-035, DEC-160 | Suy ra | Tối đa 3 tài liệu ⇒ tài liệu thứ 4 bị từ chối |
| FR-M03-02.10 | DEC-035 | Nói thẳng | DEC-035 nêu hai giới hạn trên hai dòng riêng |
| FR-M03-02.11 | DEC-035, DM-1.3 | Suy ra | Đính kèm là thao tác soạn bài của tác giả ⇒ người khác bị từ chối |
| FR-M03-03 | DEC-030, DEC-036, QA-081 | Nói thẳng | Nguồn chưa nêu lý do |
| FR-M03-03.01 | DEC-036, DEC-165 | Nói thẳng | — |
| FR-M03-03.02 | QA-081 | Nói thẳng | — |
| FR-M03-03.03 | DEC-036 | Suy ra | Tối thiểu 2, tối đa 10 ⇒ ngoài khoảng thì từ chối |
| FR-M03-03.04 | DEC-036 | Suy ra | Tối đa 1 poll/bài ⇒ poll thứ hai bị từ chối |
| FR-M03-03.05 | DEC-036, DEC-165 | Nói thẳng | — |
| FR-M03-03.06 | DEC-036, DEC-165 | Nói thẳng | — |
| FR-M03-03.07 | DEC-036 | Suy ra | Hạn kết thúc bắt buộc ⇒ thiếu thì từ chối |
| FR-M03-03.08 | DEC-036 | Suy ra | Poll do chủ bài cấu hình ⇒ người khác bị từ chối |
| FR-M03-03.09 | DEC-165 | Nói thẳng | — |
| FR-M03-03.10 | DEC-165 | Nói thẳng | — |
| FR-M03-03.11 | DEC-165 | Nói thẳng | — |
| FR-M03-04 | DEC-031, DEC-034, DM-1.3 | Nói thẳng | Nguồn chưa nêu lý do |
| FR-M03-04.01 | DEC-034, DEC-013, DEC-195 | Nói thẳng | — |
| FR-M03-04.02 | DEC-013, DEC-034 | Nói thẳng | DEC-013: "ẩn với public cho đến khi AI scan xong" |
| FR-M03-04.03 | DEC-099, DEC-013, MR-FB-M08 | Nói thẳng | — |
| FR-M03-04.04 | DEC-031, DEC-034 | Nói thẳng | — |
| FR-M03-04.05 | DEC-104, DEC-240  | Nói thẳng | — |
| FR-M03-04.06 | DM-1.3, DEC-031 | Suy ra | Gửi bài là thao tác của tác giả ⇒ người khác bị từ chối |
| FR-M03-04.07 | DEC-031, DEC-034 | Suy ra | Theo bảng trạng thái, gửi bài chỉ đi từ Nháp hoặc Bị từ chối |
| FR-M03-04.08 | DEC-164 | Nói thẳng | — |
| FR-M03-04.09 | DEC-164 | Nói thẳng | — |
| FR-M03-04.10 | DEC-163 | Nói thẳng | — |
| FR-M03-04.11 | DEC-195 | Nói thẳng | — |
| FR-M03-05 | DEC-013, DEC-034, DEC-098, DEC-099, F-POST-08 | Nói thẳng | Lý do lấy từ DEC-013, DEC-099 |
| FR-M03-05.01 | DEC-098, DEC-034 | Nói thẳng | — |
| FR-M03-05.02 | DEC-098, DEC-034 | Nói thẳng | — |
| FR-M03-05.03 | DEC-098 | Nói thẳng | — |
| FR-M03-05.04 | DEC-099 | Nói thẳng | — |
| FR-M03-05.05 | DEC-013, DEC-185, DEC-093, DEC-195 | Nói thẳng | Điều kiện công tắc theo DEC-093; phần bài Tự ẩn theo DEC-185 |
| FR-M03-05.06 | DEC-013, DEC-161, DEC-185 | Nói thẳng | "không ẩn" (DEC-013); "stays visible during the scan" (DEC-185) |
| FR-M03-05.07 | DEC-161, DEC-013 | Nói thẳng | — |
| FR-M03-05.08 | DEC-013, DEC-099 | Nói thẳng | — |
| FR-M03-05.09 | DEC-013, DEC-093 | Nói thẳng | — |
| FR-M03-05.10 | DEC-161 | Nói thẳng | — |
| FR-M03-05.11 | DEC-161 | Nói thẳng | — |
| FR-M03-05.12 | DEC-166, DEC-097 | Nói thẳng | — |
| FR-M03-05.13 | DEC-166 | Nói thẳng | — |
| FR-M03-05.14 | DEC-185 | Nói thẳng | — |
| FR-M03-05.15 | DEC-195 | Nói thẳng | — |
| FR-M03-06 | DEC-034, DEC-098, DM-10.2, DG-5 | Nói thẳng | DEC-034 ghi "mod review"; Admin suy ra từ DM-10.2 ("Moderator/Admin có thể"). Lý do lấy từ DG-5 |
| FR-M03-06.01 | DEC-034, DM-10.2 | Nói thẳng | Admin theo DM-10.2 ("Moderator/Admin có thể") |
| FR-M03-06.02 | DEC-034 | Nói thẳng | — |
| FR-M03-06.03 | DEC-034 | Nói thẳng | — |
| FR-M03-06.04 | DEC-034 | Suy ra | "reject: REJECTED + reason" ⇒ lý do bắt buộc |
| FR-M03-06.05 | DEC-034, DEC-031 | Suy ra | Tác giả sửa và gửi lại sau khi bị từ chối kèm lý do ⇒ lý do phải đến được tác giả |
| FR-M03-06.06 | DEC-034 | Suy ra | Chỉ Mod (và Admin) duyệt ⇒ người khác bị từ chối |
| FR-M03-06.07 | DEC-034 | Suy ra | Theo bảng trạng thái, duyệt chỉ đi từ Chờ duyệt |
| FR-M03-07 | QA-011, DEC-033, DM-2.1 | Nói thẳng | Lý do lấy từ QA-011 |
| FR-M03-07.01 | DEC-033, QA-011, DEC-175 | Nói thẳng | "Bất kể mức khóa" suy ra từ quy tắc hiển thị chỉ xét hai trường; ngoại lệ nhóm Private theo DEC-175, M11 |
| FR-M03-07.02 | DEC-033, DEC-168, DEC-184, DEC-185 | Suy ra | Quy tắc hiển thị là điều kiện cần ⇒ bài không thỏa thì người khác không thấy; ngoại lệ theo DEC-168, DEC-184, DEC-185 |
| FR-M03-07.03 | DEC-031, DEC-038 | Suy ra | Tác giả sửa bài nháp, sửa bài bị từ chối, hiện lại bài tự ẩn, khôi phục bài từ tab "Đã xóa" ⇒ tác giả phải thấy bài ở các trạng thái đó |
| FR-M03-07.04 | DEC-030, DM-2.1 | Nói thẳng | — |
| FR-M03-07.05 | DEC-038, DEC-184 | Nói thẳng | — |
| FR-M03-07.06 | QA-011 | Suy ra | Guest chỉ được xem/đọc post; "INTR: Không" |
| FR-M03-07.07 | DEC-168, DEC-185 | Nói thẳng | — |
| FR-M03-07.08 | DEC-184, DEC-179 | Nói thẳng | — |
| FR-M03-07.09 | DEC-184, DEC-179 | Nói thẳng | — |
| FR-M03-07.10 | DEC-184 | Suy ra | "The author can view it" ⇒ người khác bị từ chối qua đường này; Mod, Admin xem qua báo cáo (FR-M03-17.04) |
| FR-M03-07.11 | DEC-185 | Nói thẳng | — |
| FR-M03-08 | DEC-036, QA-081 | Nói thẳng | Nguồn chưa nêu lý do |
| FR-M03-08.01 | DEC-036, QA-081 | Nói thẳng | — |
| FR-M03-08.02 | DEC-036 | Suy ra | "allow_multiple" tắt ⇒ mỗi người một lựa chọn |
| FR-M03-08.03 | DEC-036 | Nói thẳng | — |
| FR-M03-08.04 | DEC-165 | Nói thẳng | — |
| FR-M03-08.05 | DEC-165 | Nói thẳng | — |
| FR-M03-08.06 | DEC-036, DEC-165 | Suy ra | Poll đã đóng là poll kết thúc ⇒ không nhận thay đổi phiếu |
| FR-M03-08.07 | DEC-036 | Nói thẳng | — |
| FR-M03-08.08 | DEC-036 | Nói thẳng | — |
| FR-M03-08.09 | DEC-036 | Suy ra | Tên tùy chọn "hiện kết quả trước khi bình chọn" ⇒ sau khi bình chọn thì thấy kết quả |
| FR-M03-08.10 | DEC-036 | Nói thẳng | — |
| FR-M03-08.11 | DEC-165 | Nói thẳng | — |
| FR-M03-08.12 | DEC-165 | Nói thẳng | — |
| FR-M03-08.13 | DEC-167 | Nói thẳng | — |
| FR-M03-09 | DEC-036 | Nói thẳng | Nguồn chưa nêu lý do |
| FR-M03-09.01 | DEC-036, DEC-165 | Nói thẳng | — |
| FR-M03-09.02 | DEC-036, DEC-165 | Nói thẳng | — |
| FR-M03-09.03 | DEC-036 | Nói thẳng | — |
| FR-M03-09.04 | DEC-036, DEC-165 | Suy ra | Chỉ chủ bài cấu hình và thêm lựa chọn ⇒ người khác bị từ chối |
| FR-M03-09.05 | DEC-165 | Nói thẳng | — |
| FR-M03-09.06 | DEC-165 | Nói thẳng | — |
| FR-M03-09.07 | DEC-165, DEC-036 | Suy ra | Tối đa 10 lựa chọn ⇒ lựa chọn thứ 11 bị từ chối |
| FR-M03-09.08 | DEC-165, DEC-036 | Suy ra | Poll đã đóng không nhận thay đổi (không mở lại) |
| FR-M03-10 | DEC-036 | Suy ra | Poll bắt buộc có hạn (expires_at) và "sau khi đóng luôn hiện kết quả" ⇒ đến hạn thì poll kết thúc. Nguồn chưa nêu lý do |
| FR-M03-10.01 | DEC-036 | Suy ra | Hạn kết thúc bắt buộc và "sau khi đóng luôn hiện kết quả" ⇒ đến hạn thì poll đóng |
| FR-M03-10.02 | DEC-065 | Nói thẳng | DEC-065: sự kiện "poll ended" có thông báo trong ứng dụng |
| FR-M03-11 | DEC-013, DEC-037, DM-1.3, F-POST-01 | Nói thẳng | Nguồn chưa nêu lý do |
| FR-M03-11.01 | DM-1.3, F-POST-01, DEC-037, DEC-162 | Nói thẳng | — |
| FR-M03-11.02 | DEC-037, DM-2.3 | Nói thẳng | — |
| FR-M03-11.03 | DEC-013 | Nói thẳng | — |
| FR-M03-11.04 | DM-1.3, DEC-142 | Suy ra | Nguồn chỉ cho Mod/Admin đổi Topic, Tag trên bài người khác (M05) ⇒ phần khác chỉ tác giả sửa |
| FR-M03-11.05 | DEC-142 | Nói thẳng | — |
| FR-M03-11.06 | DEC-142 | Nói thẳng | — |
| FR-M03-11.07 | DEC-162 | Nói thẳng | — |
| FR-M03-12 | DEC-037, DM-2.3, F-POST-04 | Nói thẳng | Nguồn chưa nêu lý do |
| FR-M03-12.01 | DEC-037 | Nói thẳng | — |
| FR-M03-12.02 | DEC-037, DM-2.3, F-POST-04 | Nói thẳng | — |
| FR-M03-12.03 | DEC-037 | Nói thẳng | DEC-037: "public badge" |
| FR-M03-12.04 | DEC-037, DEC-033 | Suy ra | Lịch sử sửa là một phần của bài ⇒ không xem được bài thì không xem được lịch sử |
| FR-M03-13 | DEC-031 | Nói thẳng | Nguồn chưa nêu lý do |
| FR-M03-13.01 | DEC-031 | Nói thẳng | — |
| FR-M03-13.02 | DEC-031 | Suy ra | "author self-hide (reversible)" ⇒ hiện lại về trạng thái trước khi ẩn |
| FR-M03-13.03 | DEC-031 | Suy ra | Tự ẩn là thao tác của tác giả ⇒ người khác bị từ chối |
| FR-M03-13.04 | DEC-031 | Suy ra | Theo bảng trạng thái, Tự ẩn chỉ đi từ Đã đăng |
| FR-M03-13.05 | DEC-032 | Nói thẳng | Tác giả phải khiếu nại qua M09 |
| FR-M03-13.06 | DEC-185 | Nói thẳng | — |
| FR-M03-14 | DEC-033, DM-10.2 | Nói thẳng | Nguồn chưa nêu lý do |
| FR-M03-14.01 | DEC-033 | Nói thẳng | — |
| FR-M03-14.02 | DEC-033, DM-10.2 | Nói thẳng | Admin theo DM-10.2 |
| FR-M03-14.03 | DEC-033, DM-10.2 | Nói thẳng | Admin theo DM-10.2 |
| FR-M03-14.04 | DEC-033 | Nói thẳng | — |
| FR-M03-14.05 | DEC-033 | Suy ra | "blocks new comments" ⇒ chỉ chặn bình luận mới |
| FR-M03-14.06 | DEC-033, DEC-167, DEC-246 | Nói thẳng | — |
| FR-M03-14.07 | DEC-033 | Suy ra | "if MOD, author cannot override" ⇒ khóa do tác giả thì tác giả mở được |
| FR-M03-14.08 | DEC-033, DM-10.2 | Suy ra | Mod đặt được mọi mức ⇒ Mod đổi được về mức thấp hơn |
| FR-M03-14.09 | DEC-033 | Nói thẳng | — |
| FR-M03-14.10 | DEC-033 | Suy ra | "FULLY_LOCKED: mod only" |
| FR-M03-14.11 | DEC-033 | Suy ra | Chỉ tác giả hoặc Mod khóa bình luận ⇒ người khác bị từ chối |
| FR-M03-14.12 | DEC-167 | Nói thẳng | — |
| FR-M03-15 | DEC-011, DEC-038, DM-1.3, F-POST-06 | Nói thẳng | Lý do lấy từ DEC-011; vế "không tích lũy dữ liệu rác" bị DEC-184 thay (bản 1.1) |
| FR-M03-15.01 | DEC-038, DEC-011, DEC-162, F-POST-06 | Nói thẳng | — |
| FR-M03-15.02 | DEC-038 | Nói thẳng | — |
| FR-M03-15.03 | DEC-038 | Nói thẳng | — |
| FR-M03-15.04 | DEC-038, DM-1.3 | Suy ra | Xóa mềm là thao tác của tác giả; Mod gỡ bài thuộc M08 |
| FR-M03-15.05 | DEC-162 | Suy ra | Theo bảng trạng thái, xóa đi từ mọi trạng thái trừ Đã xóa |
| FR-M03-15.06 | DEC-162, DEC-034 | Suy ra | Bài Đã xóa không còn ở Chờ duyệt ⇒ không còn gì để duyệt |
| FR-M03-16 | DEC-011, DEC-038 | Nói thẳng | Lý do lấy từ DEC-011; vế "không tích lũy dữ liệu rác" bị DEC-184 thay (bản 1.1) |
| FR-M03-16.01 | DEC-162, DEC-038 | Nói thẳng | — |
| FR-M03-16.02 | DEC-162 | Nói thẳng | — |
| FR-M03-16.03 | DEC-038, DEC-011 | Nói thẳng | — |
| FR-M03-16.04 | DEC-011, DEC-161 | Nói thẳng | — |
| FR-M03-16.05 | DEC-038 | Suy ra | Khôi phục là thao tác của tác giả ⇒ người khác bị từ chối |
| FR-M03-16.06 | DEC-162 | Nói thẳng | — |
| FR-M03-17 | DEC-011, DEC-038, DEC-184 | Nói thẳng | Lý do lấy từ QA-343 (qua DEC-184) và DEC-011 |
| FR-M03-17.01 | DEC-184, DEC-038 | Nói thẳng | — |
| FR-M03-17.02 | DEC-184 | Nói thẳng | — |
| FR-M03-17.03 | DEC-184 | Nói thẳng | — |
| FR-M03-17.04 | DEC-184 | Suy ra | Phần bài Đã xóa hẳn nói thẳng; phần bài Đã xóa còn trong hạn khôi phục suy ra: bài đã xóa hẳn còn xem được trong báo cáo thì bài vừa xóa cũng xem được |
| BR-M03-01 | DEC-030, DM-2.1, DM-2.4 | Nói thẳng | — |
| BR-M03-02 | DEC-030, DM-2.1, F-POST-01 | Nói thẳng | — |
| BR-M03-03 | DEC-029, DM-2.2, F-POST-03 | Nói thẳng | — |
| BR-M03-04 | DEC-029, DEC-030, F-POST-02 | Nói thẳng | — |
| BR-M03-05 | DEC-029 | Nói thẳng | — |
| BR-M03-06 | QA-033, QA-034, DEC-140, DM-3.3, F-POST-09, GL:Lớp/Khối | Nói thẳng | — |
| BR-M03-07 | DEC-035 | Nói thẳng | — |
| BR-M03-08 | DEC-035, DEC-160 | Nói thẳng | — |
| BR-M03-09 | DEC-036 | Nói thẳng | — |
| BR-M03-10 | QA-081 | Nói thẳng | — |
| BR-M03-11 | DEC-036, DEC-165 | Nói thẳng | "Từ 1" và "đúng 1" suy ra từ ý bình chọn là chọn lựa chọn |
| BR-M03-12 | DEC-036, DEC-165 | Nói thẳng | — |
| BR-M03-13 | DEC-036 | Nói thẳng | Đóng đúng tại thời điểm hạn suy ra từ "hạn kết thúc" |
| BR-M03-14 | DEC-036, DEC-165 | Nói thẳng | — |
| BR-M03-15 | DEC-036, DEC-165 | Nói thẳng | "Người đã bình chọn thấy kết quả" suy ra từ tên tùy chọn "hiện kết quả trước khi bình chọn" |
| BR-M03-16 | DEC-165 | Nói thẳng | — |
| BR-M03-17 | DEC-012, DEC-031, DEC-032, DEC-033, F-POST-07, MR-M03 | Nói thẳng | — |
| BR-M03-18 | DEC-033, DEC-175 | Nói thẳng | "Mức khóa không ảnh hưởng" suy ra từ quy tắc hiển thị chỉ xét hai trường; câu nhóm Private theo DEC-175, M11 |
| BR-M03-19 | DEC-034, DEC-013, F-POST-08, DEC-195 | Nói thẳng | — |
| BR-M03-20 | DEC-098, DEC-034 | Nói thẳng | — |
| BR-M03-21 | DEC-099 | Nói thẳng | — |
| BR-M03-22 | DEC-013, DEC-099, MR-FB-M08 | Nói thẳng | Công tắc Moderation lấy từ DEC-093 (M10) |
| BR-M03-23 | DEC-034 | Nói thẳng | "Lý do bắt buộc" suy ra từ "reject: REJECTED + reason" |
| BR-M03-24 | DEC-031, DEC-034 | Nói thẳng | — |
| BR-M03-25 | DEC-104, DEC-240  | Nói thẳng | — |
| BR-M03-26 | DEC-013, DEC-161, DEC-185, DEC-093 | Nói thẳng | — |
| BR-M03-27 | DEC-037, DM-2.3, F-POST-04 | Nói thẳng | — |
| BR-M03-28 | DEC-142 | Nói thẳng | "Không làm hiện nhãn" suy ra từ việc không ghi lịch sử |
| BR-M03-29 | DEC-031, DEC-185 | Nói thẳng | Trạng thái đích khi hiện lại suy ra từ "reversible" |
| BR-M03-30 | DEC-033 | Nói thẳng | "Bình luận cũ vẫn hiển thị" suy ra từ "blocks new comments" |
| BR-M03-31 | DEC-033, DEC-167, DM-10.2, DEC-246 | Nói thẳng | Admin theo DM-10.2 |
| BR-M03-32 | DEC-033 | Nói thẳng | Tác giả mở được khóa của chính mình suy ra từ "if MOD, author cannot override" |
| BR-M03-33 | DEC-032 | Nói thẳng | — |
| BR-M03-34 | DEC-038, DEC-011, DEC-162, F-POST-06 | Nói thẳng | — |
| BR-M03-35 | DEC-038, DEC-162 | Nói thẳng | — |
| BR-M03-36 | DEC-011, DEC-161 | Nói thẳng | — |
| BR-M03-37 | DEC-184, DEC-038, DEC-011 | Nói thẳng | — |
| BR-M03-38 | DEC-079, DEC-163 | Nói thẳng | — |
| BR-M03-39 | QA-011 | Nói thẳng | — |
| BR-M03-40 | DEC-164 | Nói thẳng | — |
| BR-M03-41 | DEC-164 | Nói thẳng | — |
| BR-M03-42 | DEC-164, DEC-144 | Nói thẳng | Định nghĩa "từ" dùng lại của DEC-144 |
| BR-M03-43 | DEC-164 | Nói thẳng | — |
| BR-M03-44 | DEC-165 | Nói thẳng | — |
| BR-M03-45 | DEC-165 | Nói thẳng | — |
| BR-M03-46 | DEC-166, DEC-097, DEC-198 | Nói thẳng | — |
| BR-M03-47 | DEC-162 | Nói thẳng | — |
| BR-M03-48 | DEC-161 | Nói thẳng | — |
| BR-M03-49 | DEC-168, DEC-184, DEC-185 | Suy ra | Phần bài Tự ẩn nói thẳng (DEC-185); phần bài Đã xóa (trong hạn khôi phục) suy từ DEC-184: bài Đã xóa hẳn còn xem được trong báo cáo thì bài vừa xóa cũng xem được |
| BR-M03-50 | DEC-169 | Nói thẳng | — |
| BR-M03-51 | DEC-195 | Nói thẳng | — |

## Phụ lục B. Câu hỏi, giả định và TBD

### B.1 Câu hỏi đã hỏi

| Mã | Loại | Câu hỏi | Trả lời | Ghi vào register |
|---|---|---|---|---|
| Q-01 | Mâu thuẫn | Bài viết có được đính kèm tài liệu (PDF, DOCX, XLSX, PPTX) không? DEC-035 cho mỗi bài tối đa 3 tài liệu, 20MB/tệp; DEC-130 (sau đó, khi quyết định không quét virus) lập luận rằng hệ thống "chỉ cho tải ảnh lên" và dựa vào việc nén lại ảnh để loại mã độc, lý do này không áp dụng được cho tệp tài liệu. A) Giữ tài liệu theo DEC-035, ghi rõ tài liệu không được quét virus. B) Bỏ tài liệu, bài chỉ đính kèm ảnh. Đề xuất A. | A — giữ tài liệu theo DEC-035, không quét mã độc; bảo mật xử lý sau. | QA-321, DEC-160 |
| Q-02 | Cần cân nhắc | Ngoài bài đang chờ duyệt, Mod và Admin có xem được bài chưa hiển thị công khai của người khác (bài nháp, bài tác giả tự ẩn, bài bị từ chối, bài bị Mod ẩn) không? Nguồn chỉ nêu Mod duyệt bài chờ đăng (DEC-034) và Mod/Admin xem bài bị ẩn của tác giả đã vô hiệu hóa tài khoản (DEC-150). | Mở rộng phạm vi, không chấp nhận: Mod, Admin không xem bài Nháp, Tự ẩn, Bị từ chối của người khác. | QA-331, DEC-168 |
| Q-03 | Thiếu chi tiết | Tác giả có được bình chọn trong poll của chính bài mình không? DEC-036 chỉ nêu chủ bài cấu hình poll và QA-081 "users vote only". | Có, tác giả được bình chọn. | QA-327, DEC-165 |
| Q-04 | Thiếu chi tiết | Khi gửi bài, những phần nào bắt buộc (tiêu đề, nội dung) và có giới hạn độ dài không? Bài nháp có cần tiêu đề không? DEC-030 chỉ liệt kê các phần của bài. | Gửi: bắt buộc tiêu đề và nội dung hoặc poll (tệp không thay nội dung). Nháp: không trống. Tiêu đề ≤ 150 ký tự, nội dung ≤ 6.000 từ, áp dụng cả nháp, cảnh báo ngay khi soạn. | QA-326, DEC-164 |
| Q-05 | Thiếu chi tiết | Chi tiết poll (danh sách xác nhận): (a) mặc định của "cho đổi phiếu" và "cho chọn nhiều"; (b) sửa lựa chọn, cấu hình sau khi đã có phiếu; (c) hạn kết thúc tối thiểu, tối đa, rút ngắn hạn; (d) rút phiếu; (e) bỏ poll khỏi bài. DEC-036 chỉ nêu mặc định của "hiện kết quả trước" và việc gia hạn, đóng sớm. | Bỏ tùy chọn đổi phiếu (luôn đổi, bỏ chọn được khi còn mở); chọn nhiều mặc định; khóa cấu hình sau khi gửi; thêm, bỏ poll chỉ khi chưa gửi; sau khi gửi chỉ thêm lựa chọn (≤ 10) và đổi hạn; hạn ≥ hiện tại, đổi được khi còn mở. | QA-327, DEC-165 |
| Q-06 | Mơ hồ | Poll cho chọn nhiều: phần trăm tính trên tổng lượt chọn hay tổng số người bình chọn, làm tròn thế nào? Ví dụ 4 người, A được 3 người chọn, B 2, C 1: theo lượt chọn là 50%, 33%, 17%; theo người là 75%, 50%, 25%. | Tính trên tổng lượt chọn, làm tròn số nguyên. | QA-327, DEC-165 |
| Q-07 | Mơ hồ | Quét lại khi sửa bài đã đăng (DEC-013: không ẩn, bị gắn cờ thì "under_review"): với điểm dưới 0.5, từ 0.5 đến dưới 0.9, từ 0.9, khi AI lỗi và khi AI tắt, bài chuyển sang trạng thái nào trong bộ trạng thái hiện hành? | Bài sửa: điểm từ 0.5 (kể cả từ 0.9) → Bị gắn cờ, chờ Mod; dưới 0.5 → giữ nguyên; lỗi → giữ nguyên. | QA-323, DEC-161 |
| Q-08 | Thiếu chi tiết | Bài bị AI tự từ chối (điểm ≥ 0.9, DEC-098): tác giả thấy lý do gì; gửi lại có giới hạn số lần không? | Thấy nhóm vi phạm; gửi lại không giới hạn; khiếu nại qua M09. | QA-328, DEC-166 |
| Q-09 | Mơ hồ | Khóa toàn bộ "chặn bình luận và tương tác" (DEC-033): tương tác gồm upvote, bình chọn poll, bookmark, báo cáo hay chỉ một phần? Tác giả còn sửa, xóa bài đang bị khóa không? | Chặn bình luận, upvote và bình chọn poll; tác giả vẫn sửa, xóa bài bị khóa. | QA-329, QA-324, DEC-167, DEC-162 |
| Q-10 | Mơ hồ | Thời hạn khôi phục 7 ngày (DEC-038, DEC-127 giờ UTC+7) đếm theo 7 × 24 giờ hay theo ngày lịch? Ví dụ xóa lúc 01/10 21:00: theo 7 × 24 giờ thì khôi phục được tới trước 08/10 21:00; theo ngày lịch thì tới hết ngày 08/10. | 7 × 24 giờ từ lúc xóa. | QA-330, DEC-162 |
| Q-11 | Thiếu chi tiết | Bài ở trạng thái nào thì xóa được (Nháp, Chờ duyệt, Bị từ chối, Tự ẩn)? Khôi phục bài xóa từ các trạng thái đó thì về trạng thái nào (DEC-038 chỉ nói khôi phục về Đã đăng)? Bài nháp xóa có qua thời hạn khôi phục không? | Theo đề xuất: xóa được mọi trạng thái trừ Đã xóa; khôi phục về trạng thái trước khi xóa, Chờ duyệt về Nháp. | QA-324, DEC-162 |
| Q-12 | Thiếu chi tiết | Mức cảnh cáo MEDIUM, HEAVY "không tạo bài mới" (DEC-079) có chặn lưu nháp, gửi bài nháp đã có, gửi lại bài bị từ chối, sửa bài đã đăng, khôi phục bài đã xóa không? | A — chặn lưu nháp mới, gửi nháp, gửi lại bài bị từ chối; vẫn sửa, khôi phục, bình chọn. | QA-325, DEC-163 |
| Q-13 | Thiếu chi tiết | Bài ở trạng thái nào thì tác giả sửa được (Chờ duyệt, Tự ẩn, Bị Mod ẩn, Đã xóa, đang bị khóa)? Nguồn chỉ nói sửa bài và sửa bài bị từ chối để gửi lại. | Sửa được Nháp, Bị từ chối, Đã đăng, Tự ẩn, kể cả khi bị khóa; không sửa Chờ duyệt, Đã xóa, Bị Mod ẩn. | QA-324, DEC-162 |
| Q-14 | Mơ hồ | Bài mới tạo và bài đang Chờ duyệt mang trạng thái kiểm duyệt gì? "Mod gỡ bài" (DEC-011, DEC-113, DEC-115) có phải là trạng thái Bị Mod ẩn (DEC-032) không, hay là một hành động khác? | Bài mới Bình thường; "gỡ" chính là Bị Mod ẩn. | QA-322, DEC-161 |
| Q-15 | Cần cân nhắc | Mở rộng phạm vi: Accepted Answer (draft DM-4.2.1, DG-5) có làm ở MS1 không? Register chưa có DEC nào. | Không — MS1 không hỗ trợ Accepted Answer. | QA-332, DEC-169 |
| Q-16 | Cần cân nhắc | Mở rộng phạm vi: bài viết có ảnh bìa (draft DM-2.1) không? DEC-030 không có ảnh bìa. | Không — ảnh dùng qua phần đính kèm. | QA-333, DEC-169 |
| Q-17 | Cần cân nhắc | Mở rộng phạm vi (bản 1.1, OPEN-010): áp xóa mềm cho bài viết — hết 7 ngày khôi phục giữ gì; ai xem lại bài đã xóa hẳn; bookmark, trừ điểm tính ở mốc nào? | Hết hạn chỉ gắn cờ Đã xóa hẳn, giữ toàn bộ dữ liệu; Mod, Admin xem qua báo cáo, lịch sử báo cáo, khiếu nại; tác giả xem lại từ thông báo xử lý, khiếu nại; bookmark và trừ điểm tính tại lúc gắn cờ; "Đã xóa hẳn" không phải xóa hết dữ liệu. | QA-350, DEC-184 |
| Q-18 | Cần cân nhắc | Bài Tự ẩn có thể né kiểm duyệt: Mod không xem được bài Tự ẩn bị báo cáo (DEC-168); sửa bài trong lúc ẩn rồi hiện lại thì không bị quét (DEC-161 chỉ quét khi sửa bài Đã đăng). | Mod, Admin xem bài Tự ẩn trong báo cáo, lịch sử báo cáo, khiếu nại; quét lại khi tác giả hiện lại bài Tự ẩn đã sửa trong lúc ẩn (không quét lúc lưu). | QA-351, DEC-185 |

### B.2 TBD

| ID | Nội dung | Ảnh hưởng | Lý do chưa chốt |
|---|---|---|---|
| TBD-M03-01 | Lượt xem bài (draft liệt kê "View count" trong thông tin bài) chưa được đếm ở MS1. | Thấp | DEC-145 hoãn: cần hạ tầng ghi sự kiện, đang hoãn có chủ đích ở OPEN-005 |
| TBD-M03-02 | Trang bài viết công khai (Guest đọc được) chưa được tối ưu để công cụ tìm kiếm index và hiển thị xem trước khi chia sẻ link. | Thấp | OPEN-006 hoãn có chủ đích (không làm SSR/SEO ở MS1) |

### B.3 Cần cân nhắc (ngoài dữ liệu hiện có)

| Mã | Điểm cần cân nhắc | Vì sao cần | Quyết định |
|---|---|---|---|
| CC-01 | Tài liệu đính kèm (PDF, DOCX, XLSX, PPTX) không được quét mã độc. | An toàn dữ liệu: DEC-130 chỉ dựa vào việc nén lại ảnh để loại mã độc, không áp dụng cho tài liệu. | Hoãn: MS1 chỉ cần cho tải lên, xử lý bảo mật sau (QA-321, DEC-160). |

## Phụ lục C. Sổ nguồn

**Owner keywords:** M03, F-POST, publish_state, mod_state, lock_level, locked_by, COMMENT_LOCKED, FULLY_LOCKED, PENDING, PUBLISHED, REJECTED, under_review, mod_state=removed, pre-scan, prescan, retroactive scan, Content Gate, auto-reject, Manual moderation queue, Tiptap, ProseMirror, editor, trình soạn, LaTeX, KaTeX, poll, polls, bình chọn, khảo sát, attachment, attachments, đính kèm, tệp đính kèm, edit history, lịch sử chỉnh sửa, lịch sử sửa, post_edits, post_revisions, đã chỉnh sửa, soft delete, soft-delete, xóa mềm, khôi phục, recover, recovery, restore, Đã xóa, hard delete, đăng bài, viết bài, sửa bài, xóa bài, ẩn bài, create post, edit post, delete post, Cannot create new posts, no-post, bài nháp, content_json, content_text, cover image, ảnh bìa, view count, Post views, lượt xem, khóa bài, khóa bình luận, grade_level, Lớp/Khối, post type, post_type, Xem/đọc post, Nội dung không tồn tại, hidden posts, Content Deletion Appeal, Anonymous Post, anonymous posting, Accepted Answer, accepted_comment_id, group_id, per-post mute, Post Summarization, event-tracking, Guest xem được post
**Dependency keywords:** comment, bình luận, topic, tag, moderation, kiểm duyệt, report, appeal, khiếu nại, notification, thông báo, search, feed, trending, group, nhóm, anonymous, ẩn danh, star, upvote, bookmark, mention, AI_ENABLED, AI off, timezone, Cloudinary, summarization, tóm tắt, warning, ban, BANNED, profile, audit log, guest, points
**Mục draft của module:** DM-2 (gồm DM-2.1–2.4)
**Loại khỏi bảng nguồn (khớp nhầm):** DEC-039, DEC-043, DEC-044, DEC-046, ISS-070, ISS-075, ISS-076, QA-092, QA-098, MR-M04 (trình soạn, xóa, đính kèm của bình luận — M04); DEC-051, DEC-090, ISS-084, QA-107, QA-270 ("soft-delete"/"xóa mềm" của Tag); ISS-159, QA-217, ISS-158, QA-214 (đính kèm, xóa tin nhắn chat); DEC-087, ISS-118, QA-155 ("rejected" của khiếu nại); DEC-103 ("rejected" của yêu cầu vào nhóm); DM-10.1, QA-244 (trạng thái báo cáo); QA-005 ("pending confirm"); DEC-149, QA-066, QA-293 ("đã xóa" — bình luận của tài khoản đã xóa); ISS-252, QA-312 (tin nhắn, nhật ký của tài khoản đã xóa); ISS-260, QA-320 (phản hồi gợi ý Topic của tài khoản đã xóa); DEC-014, DM-1.2, ISS-179, QA-242 (Lớp/Khối trên hồ sơ); DM-3.2 ("lớp12" trong ví dụ Tag); DEC-173, DEC-176, ISS-277, ISS-280, QA-067, QA-337, QA-340 (Lớp/Khối, ngày tham gia trên hồ sơ — M02; bản 1.1); DEC-183, ISS-286 ("editor", "đã xóa" của bình luận — M04; bản 1.1)

### C.1 Bảng nguồn

| Nguồn | Nhãn | Trạng thái | Dùng ở | Ghi chú |
|---|---|---|---|---|
| DEC-029 | Sở hữu | Hiện hành | FR-M03-01, FR-M03-01.02, FR-M03-01.03, FR-M03-01.04, BR-M03-03, BR-M03-04, BR-M03-05 | Nhóm A. Trình soạn bài: các định dạng, LaTeX, không chèn ảnh |
| DEC-030 | Sở hữu | Sửa một phần bởi DEC-164, DEC-169 | FR-M03-01, FR-M03-01.04, FR-M03-01.11, FR-M03-02, FR-M03-02.01, FR-M03-02.02, FR-M03-02.03, FR-M03-03, FR-M03-07.04, BR-M03-01, BR-M03-02, BR-M03-04 | Nhóm A. Cấu trúc bài: một loại bài, tiêu đề, nội dung, poll tùy chọn, phần đính kèm |
| DEC-031 | Sở hữu | Hiện hành | FR-M03-01, FR-M03-01.01, FR-M03-04, FR-M03-04.04, FR-M03-04.06, FR-M03-04.07, FR-M03-06.05, FR-M03-07.03, FR-M03-13, FR-M03-13.01, FR-M03-13.02, FR-M03-13.03, FR-M03-13.04, BR-M03-17, BR-M03-24, BR-M03-29 | Nhóm A. Trạng thái đăng bài (6 giá trị) |
| DEC-032 | Sở hữu | Sửa một phần bởi DEC-161, DEC-190 | FR-M03-13.05, BR-M03-17, BR-M03-33 | Nhóm A. Trạng thái kiểm duyệt (3 giá trị); bài bị Mod ẩn phải khiếu nại (M09) |
| DEC-033 | Sở hữu | Sửa một phần bởi DEC-167 | FR-M03-01.09, FR-M03-07, FR-M03-07.01, FR-M03-07.02, FR-M03-12.04, FR-M03-14, FR-M03-14.01, FR-M03-14.02, FR-M03-14.03, FR-M03-14.04, FR-M03-14.05, FR-M03-14.06, FR-M03-14.07, FR-M03-14.08, FR-M03-14.09, FR-M03-14.10, FR-M03-14.11, BR-M03-17, BR-M03-18, BR-M03-30, BR-M03-31, BR-M03-32 | Nhóm A. Mức khóa bài và người khóa; điều kiện bài hiển thị |
| DEC-034 | Sở hữu | Sửa một phần bởi DEC-098 | FR-M03-04, FR-M03-04.01, FR-M03-04.02, FR-M03-04.04, FR-M03-04.07, FR-M03-05, FR-M03-05.01, FR-M03-05.02, FR-M03-06, FR-M03-06.01, FR-M03-06.02, FR-M03-06.03, FR-M03-06.04, FR-M03-06.05, FR-M03-06.06, FR-M03-06.07, FR-M03-15.06, BR-M03-19, BR-M03-20, BR-M03-23, BR-M03-24 | Nhóm A. Luồng quét trước khi đăng |
| DEC-035 | Sở hữu | Hiện hành | FR-M03-02, FR-M03-02.04, FR-M03-02.05, FR-M03-02.06, FR-M03-02.07, FR-M03-02.08, FR-M03-02.09, FR-M03-02.10, FR-M03-02.11, BR-M03-07, BR-M03-08 | Nhóm A. Tệp đính kèm: loại, dung lượng, số lượng. Mâu thuẫn với DEC-130 đã giải quyết bởi DEC-160 |
| DEC-036 | Sở hữu | Sửa một phần bởi DEC-165 | FR-M03-03, FR-M03-03.01, FR-M03-03.03, FR-M03-03.04, FR-M03-03.05, FR-M03-03.06, FR-M03-03.07, FR-M03-03.08, FR-M03-08, FR-M03-08.01, FR-M03-08.02, FR-M03-08.03, FR-M03-08.06, FR-M03-08.07, FR-M03-08.08, FR-M03-08.09, FR-M03-08.10, FR-M03-09, FR-M03-09.01, FR-M03-09.02, FR-M03-09.03, FR-M03-09.04, FR-M03-09.07, FR-M03-09.08, FR-M03-10, FR-M03-10.01, BR-M03-09, BR-M03-11, BR-M03-12, BR-M03-13, BR-M03-14, BR-M03-15 | Nhóm A. Poll: số lựa chọn, cấu hình, hạn, đóng sớm |
| DEC-037 | Sở hữu | Sửa một phần bởi DEC-142 | FR-M03-02.02, FR-M03-11, FR-M03-11.01, FR-M03-11.02, FR-M03-12, FR-M03-12.01, FR-M03-12.02, FR-M03-12.03, FR-M03-12.04, BR-M03-27 | Nhóm A. Lịch sử sửa bài (phần bình luận thuộc M04) |
| DEC-038 | Sở hữu | Sửa một phần bởi DEC-162, DEC-184 | FR-M03-07.03, FR-M03-07.05, FR-M03-15, FR-M03-15.01, FR-M03-15.02, FR-M03-15.03, FR-M03-15.04, FR-M03-16, FR-M03-16.01, FR-M03-16.03, FR-M03-16.05, FR-M03-17, FR-M03-17.01, FR-M03-17.02, BR-M03-34, BR-M03-35, BR-M03-37 | Nhóm A. Xóa mềm, khôi phục trong 7 ngày, xóa hẳn |
| DM-2 | Nhắc tới | Hiện hành | Không áp dụng: Chỉ là tiêu đề mục draft | Nhóm A. Chỉ là tiêu đề mục draft |
| DM-2.1 | Sở hữu | Sửa một phần bởi DEC-009, DEC-031, DEC-032, DEC-033, DEC-049, DEC-145, DEC-169 | FR-M03-01, FR-M03-01.08, FR-M03-07, FR-M03-07.04, BR-M03-01, BR-M03-02 | Nhóm A. Draft: thông tin bài, trạng thái bài; có is_anonymous, accepted_comment_id, view count, cover image |
| DM-2.2 | Sở hữu | Sửa một phần bởi DEC-029 | FR-M03-01, FR-M03-02, BR-M03-03 | Nhóm A. Draft: nội dung giàu định dạng |
| DM-2.3 | Sở hữu | Hiện hành | FR-M03-11.02, FR-M03-12, FR-M03-12.02, BR-M03-27 | Nhóm A. Draft: lịch sử sửa bài |
| DM-2.4 | Sở hữu | Hiện hành | FR-M03-01, FR-M03-01.11, BR-M03-01 | Nhóm A. Draft: không cần loại bài |
| ISS-062 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-029 | Nhóm A. Đã có DEC-029 |
| ISS-063 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-030 | Nhóm A. Đã có DEC-030 |
| ISS-064 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-031, DEC-032, DEC-033 | Nhóm A. Đã có DEC-031, DEC-032, DEC-033 |
| ISS-065 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-035 | Nhóm A. Đã có DEC-035 |
| ISS-066 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-037 | Nhóm A. Đã có DEC-037 |
| ISS-067 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-036 | Nhóm A. Đã có DEC-036 |
| ISS-068 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-034 | Nhóm A. Đã có DEC-034 |
| ISS-069 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-038 | Nhóm A. Đã có DEC-038 |
| QA-078 | Sở hữu | Trùng với DEC-029 | — | Nhóm A. LaTeX nhập thô, chưa có trình soạn trực quan |
| QA-079 | Sở hữu | Trùng với DEC-029 | — | Nhóm A. Không chèn ảnh trong nội dung; ảnh là tệp đính kèm dưới bài |
| QA-080 | Sở hữu | Trùng với DEC-030 | — | Nhóm A. Một loại bài; poll là phần tùy chọn |
| QA-081 | Sở hữu | Sửa một phần bởi DEC-165 | FR-M03-03, FR-M03-03.02, FR-M03-08, FR-M03-08.01, BR-M03-10 | Nhóm A. Poll đóng: chủ bài định lựa chọn, người khác chỉ bình chọn |
| QA-082 | Sở hữu | Trùng với DEC-031 | — | Nhóm A. Giá trị trạng thái đăng bài |
| QA-083 | Sở hữu | Trùng với DEC-032 | — | Nhóm A. Giá trị trạng thái kiểm duyệt |
| QA-084 | Sở hữu | Trùng với DEC-033 | — | Nhóm A. Ai được khóa bài ở mức nào |
| QA-085 | Sở hữu | Trùng với DEC-034 | — | Nhóm A. Quét trước: chặn đăng, giữ chờ Mod duyệt |
| QA-086 | Sở hữu | Trùng với DEC-035 | — | Nhóm A. Giới hạn tệp đính kèm |
| QA-087 | Nhắc tới | Hiện hành | Không áp dụng: Kích thước avatar (M02) | Nhóm A. Kích thước avatar (M02); chỉ nêu lý do đồng bộ với ảnh đính kèm |
| QA-088 | Sở hữu | Trùng với DEC-036 | — | Nhóm A. Poll bắt buộc có hạn; gia hạn hoặc đóng sớm |
| QA-089 | Sở hữu | Trùng với DEC-036 | — | Nhóm A. Poll đã đóng không mở lại |
| QA-090 | Nhắc tới | Hiện hành | Không áp dụng: Lịch sử sửa bình luận — thuộc M04 | Nhóm A. Lịch sử sửa bình luận — thuộc M04 |
| QA-091 | Sở hữu | Trùng với DEC-038 | — | Nhóm A. Khôi phục bài trong 7 ngày, tab "Đã xóa" trên hồ sơ |
| MR-M03 | Sở hữu | Sửa một phần bởi DEC-160, DEC-184 | BR-M03-17 | Nhóm A. Dòng module M03; cột MoSCoW lệch, ưu tiên lấy từ bảng MoSCoW Summary. Dấu [Amended … FR M03: DEC-160–169] |
| DEC-003 | Phụ thuộc | Hiện hành | Chuyển M11 | Nhóm B. M11: bài trong nhóm dùng chung cơ chế bài viết |
| DEC-009 | Phụ thuộc | Hiện hành | Chuyển M11 | Nhóm B. Bài ẩn danh thuộc M11, không thuộc M03 (bỏ F-POST-05) |
| DEC-011 | Sở hữu | Sửa một phần bởi DEC-162, DEC-184 | FR-M03-15, FR-M03-15.01, FR-M03-16, FR-M03-16.03, FR-M03-16.04, FR-M03-17, FR-M03-17.01, BR-M03-34, BR-M03-36, BR-M03-37 | Nhóm B. Xóa mềm 7 ngày; khôi phục nếu Mod chưa gỡ (cũ hơn DEC-038). Điều kiện "Mod chưa removed" dùng tên trạng thái Phase 4 |
| DEC-012 | Sở hữu | Sửa một phần bởi DEC-031, DEC-032, DEC-033 | BR-M03-17 | Nhóm B. Mô hình 3 trường trạng thái (bản Phase 4, giá trị khác DEC-031/032/033) |
| DEC-013 | Sở hữu | Sửa một phần bởi DEC-032, DEC-034, DEC-161, DEC-195 | FR-M03-04.01, FR-M03-04.02, FR-M03-04.03, FR-M03-05, FR-M03-05.05, FR-M03-05.06, FR-M03-05.07, FR-M03-05.08, FR-M03-05.09, FR-M03-11, FR-M03-11.03, BR-M03-19, BR-M03-22, BR-M03-26 | Nhóm B. Quét trước bài mới, quét lại ngầm khi sửa, AI tắt thì đăng ngay, không quét lại khi bật AI |
| DEC-019 | Phụ thuộc | Sửa một phần bởi DEC-156 | Chuyển M01 | Nhóm B. M01: bài của tài khoản vô hiệu hóa bị ẩn ("Nội dung không tồn tại"). DEC-148, DEC-149 (ngoài bảng nguồn) chỉ sửa phần thời hạn, username, bình luận; phần bài bị ẩn giữ nguyên |
| DEC-049 | Phụ thuộc | Sửa một phần bởi DEC-141, DEC-142 | Chuyển M05 | Nhóm B. M05: 1–3 Topic mỗi bài khi gửi |
| DEC-050 | Phụ thuộc | Sửa một phần bởi DEC-142, DEC-144 | Chuyển M05 | Nhóm B. M05: nút gợi ý Topic trong trình soạn bài |
| DEC-057 | Nhắc tới | Hiện hành | Không áp dụng: M06: dùng nội dung văn bản của bài để tìm kiếm | Nhóm B. M06: dùng nội dung văn bản của bài để tìm kiếm |
| DEC-061 | Nhắc tới | Hiện hành | Không áp dụng: M06: đoạn trích từ nội dung bài | Nhóm B. M06: đoạn trích từ nội dung bài |
| DEC-065 | Phụ thuộc | Hiện hành | FR-M03-10.02 | Nhóm B. M07: thông báo bài được đăng, bị từ chối, bị ẩn, poll kết thúc. Sửa bởi DEC-147, DEC-151 (ngoài bảng nguồn) chỉ ở sự kiện tài khoản, phần bài viết không đổi |
| DEC-070 | Phụ thuộc | Hiện hành | Chuyển M07 | Nhóm B. M07: tắt thông báo cho từng bài |
| DEC-077 | Nhắc tới | Hiện hành | Không áp dụng: M08: bình luận quét sau, khác bài | Nhóm B. M08: bình luận quét sau, khác bài |
| DEC-079 | Phụ thuộc | Sửa một phần bởi MR-M12, DEC-163 | FR-M03-01.10, BR-M03-38 | Nhóm B. M08: mức cảnh cáo MEDIUM, HEAVY không được tạo bài. MR-M12 tóm DEC-118, DEC-122 (ngoài bảng nguồn): chỉ thêm ngoại lệ bảng xếp hạng; hạn chế tạo bài giữ nguyên |
| DEC-083 | Nhắc tới | Hiện hành | Không áp dụng: M04: trạng thái kiểm duyệt của bình luận | Nhóm B. M04: trạng thái kiểm duyệt của bình luận |
| DEC-093 | Phụ thuộc | Sửa một phần bởi DEC-205 | Chuyển M10 | Nhóm B. M10: công tắc AI Moderation bao gồm quét trước bài |
| DEC-095 | Phụ thuộc | Hiện hành | Chuyển M13 | Nhóm B. M13: embedding tính khi đăng bài, tính lại khi sửa nhiều |
| DEC-098 | Sở hữu | Sửa một phần bởi DEC-166, DEC-186 | FR-M03-05, FR-M03-05.01, FR-M03-05.02, FR-M03-05.03, FR-M03-06, BR-M03-20 | Nhóm B. Nhánh A cho bài viết: ≥0.9 tự từ chối, 0.5–0.9 giữ chờ Mod; nhánh B (cảnh cáo) thuộc M08 |
| DEC-099 | Sở hữu | Sửa một phần bởi DEC-205, DEC-206, DEC-207 | FR-M03-04.03, FR-M03-05, FR-M03-05.04, FR-M03-05.08, BR-M03-21, BR-M03-22 | Nhóm B. AI tắt: bài đăng thẳng (M03/M08); AI lỗi khi quét trước: chuyển hàng chờ Mod |
| DEC-100 | Nhắc tới | Sửa một phần bởi DEC-144 | Không áp dụng: Quét trước không cần giới hạn tần suất | Nhóm B. Quét trước không cần giới hạn tần suất |
| DEC-102 | Phụ thuộc | Hiện hành | Chuyển M11 | Nhóm B. M11: vai trò nhóm được đăng bài; Group Mod ẩn/xóa bài trong nhóm |
| DEC-104 | Phụ thuộc | Hiện hành | FR-M03-04.05, BR-M03-25 | Nhóm B. M11: bài trong nhóm có cổng duyệt riêng; bài ngoài nhóm giữ luồng M03 |
| DEC-105 | Phụ thuộc | Sửa một phần bởi DEC-113 | Chuyển M11 | Nhóm B. M11: xóa nhóm thì bài trong nhóm bị ẩn (xóa mềm); thành viên rời nhóm, bài giữ nguyên |
| DEC-112 | Phụ thuộc | Hiện hành | Chuyển M11 | Nhóm B. M11: đăng ẩn danh trong nhóm, chọn theo từng bài |
| DEC-113 | Phụ thuộc | Hiện hành | Chuyển M12 | Nhóm B. M12: trừ điểm khi tự xóa bài (sau 7 ngày) hoặc bị Mod xóa |
| DEC-115 | Phụ thuộc | Hiện hành | Chuyển M09 | Nhóm B. M09: khiếu nại bài bị xóa; thành công thì khôi phục bài |
| DEC-125 | Nhắc tới | Hiện hành | Không áp dụng: M14 phụ thuộc M03 | Nhóm B. M14 phụ thuộc M03 |
| DEC-127 | Phụ thuộc | Hiện hành | Chuyển M03 | Nhóm B. Dùng chung: múi giờ cho mọi mốc "N ngày" (gồm M03) |
| DEC-129 | Phụ thuộc | Sửa một phần bởi DEC-156, DEC-184 | FR-M03-17, BR-M03-37 | Nhóm B. Dùng chung: chỉ xóa hẳn khi an toàn |
| DEC-133 | Nhắc tới | Hiện hành | Không áp dụng: M13: log đầu ra AI gắn với bài | Nhóm B. M13: log đầu ra AI gắn với bài |
| DEC-137 | Nhắc tới | Hiện hành | Không áp dụng: Công nghệ (Tiptap) — không phải nghiệp vụ | Nhóm B. Công nghệ (Tiptap) — không phải nghiệp vụ |
| DEC-140 | Sở hữu | Hiện hành | FR-M03-01, FR-M03-01.05, FR-M03-01.07, BR-M03-06 | Nhóm B. Chỉ ý cuối: Lớp/Khối là trường tùy chọn độc lập trên bài (M03); phần còn lại thuộc M05 |
| DEC-141 | Nhắc tới | Hiện hành | Không áp dụng: M05: xóa Topic xét trạng thái bài | Nhóm B. M05: xóa Topic xét trạng thái bài |
| DEC-142 | Phụ thuộc | Hiện hành | FR-M03-11.04, FR-M03-11.05, FR-M03-11.06, FR-M03-17.02, BR-M03-28 | Nhóm B. M05: đổi Topic/Tag khi sửa bài; Mod đổi không ghi lịch sử sửa |
| DEC-144 | Nhắc tới | Hiện hành | BR-M03-42 | Nhóm B. M05: đếm từ trên tiêu đề + nội dung |
| DEC-145 | Phụ thuộc | Hiện hành | Chuyển M05 | Nhóm B. M05: lượt xem bài chưa đếm ở MS1 (OPEN-005) |
| DEC-150 | Phụ thuộc | Hiện hành | Chuyển M01 | Nhóm B. M01: Mod/Admin xem bài bị ẩn của tác giả đã vô hiệu hóa |
| DEC-153 | Phụ thuộc | Hiện hành | Chuyển M01 | Nhóm B. M01: thông báo nhắc tên gửi khi bài công khai (sau quét); sửa bài chỉ báo nhắc tên mới |
| DEC-154 | Nhắc tới | Hiện hành | Không áp dụng: M01: trang chính sách nhắc tệp đính kèm | Nhóm B. M01: trang chính sách nhắc tệp đính kèm |
| DEC-156 | Phụ thuộc | Hiện hành | Chuyển M01 | Nhóm B. M01: bài của tài khoản DELETED vẫn ẩn. DEC-159 (ngoài bảng nguồn) thêm xóa lượt theo dõi bài; phần bài vẫn ẩn giữ nguyên |
| DG-3 | Nhắc tới | Hiện hành | Không áp dụng: Ba trục phân loại | Nhóm B. Ba trục phân loại |
| DG-4 | Nhắc tới | Hiện hành | Không áp dụng: Bản đồ module | Nhóm B. Bản đồ module |
| DG-5 | Phụ thuộc | Sửa một phần bởi DEC-009 | FR-M03-06 | Nhóm B. Nguyên tắc: Lớp/Khối gắn bài; bài ẩn danh; nhóm dùng lại cơ chế bài |
| DG-6 | Phụ thuộc | Hiện hành | Không áp dụng: Phạm vi AI: kiểm duyệt nội dung, gợi ý khi đăng bài, tóm tắt | Nhóm B. Phạm vi AI: kiểm duyệt nội dung, gợi ý khi đăng bài, tóm tắt |
| DG-8 | Phụ thuộc | Hiện hành | Không áp dụng: Không làm: AI tự viết bài | Nhóm B. Không làm: AI tự viết bài |
| DM-1.3 | Sở hữu | Hiện hành | FR-M03-01, FR-M03-01.01, FR-M03-02.11, FR-M03-04, FR-M03-04.06, FR-M03-11, FR-M03-11.01, FR-M03-11.04, FR-M03-15, FR-M03-15.04 | Nhóm B. Draft: quyền tạo, sửa, xóa bài |
| DM-10.2 | Phụ thuộc | Hiện hành | FR-M03-06, FR-M03-06.01, FR-M03-14, FR-M03-14.02, FR-M03-14.03, FR-M03-14.08, BR-M03-31 | Nhóm B. Draft M08: Mod/Admin ẩn, khóa, xóa bài; gỡ Accepted Answer |
| DM-11 | Nhắc tới | Hiện hành | Không áp dụng: Nguyên tắc AI chung | Nhóm B. Nguyên tắc AI chung |
| DM-11.4 | Phụ thuộc | Hiện hành | Chuyển M13 | Nhóm B. M13: tóm tắt bài dài |
| DM-3.3 | Sở hữu | Hiện hành | FR-M03-01, FR-M03-01.05, FR-M03-01.06, BR-M03-06 | Nhóm B. Lớp/Khối trên bài (draft đặt ở mục Topic/Tag; FR-M05 đã chuyển M03) |
| DM-4.2.1 | Phụ thuộc | Bị thay bởi DEC-169 | — | Nhóm B. Draft: Accepted Answer ghi trên bài (accepted_comment_id); chưa có DEC |
| DM-5.3 | Phụ thuộc | Hiện hành | Chuyển M11 | Nhóm B. M11: bài trong nhóm qua group_id |
| DM-5.4 | Nhắc tới | Hiện hành | Không áp dụng: Quan hệ nhóm–bài | Nhóm B. Quan hệ nhóm–bài |
| DM-7.1 | Nhắc tới | Hiện hành | Không áp dụng: M14: feed | Nhóm B. M14: feed |
| DM-7.3 | Nhắc tới | Hiện hành | Không áp dụng: M06: tìm theo Lớp/Khối | Nhóm B. M06: tìm theo Lớp/Khối |
| DM-7.4 | Nhắc tới | Hiện hành | Không áp dụng: M06: lọc, sắp xếp (có "most viewed") | Nhóm B. M06: lọc, sắp xếp (có "most viewed") |
| DM-8.1 | Nhắc tới | Hiện hành | Không áp dụng: M07: sự kiện thông báo | Nhóm B. M07: sự kiện thông báo |
| DM-9.1 | Nhắc tới | Hiện hành | Không áp dụng: M12: nguồn uy tín | Nhóm B. M12: nguồn uy tín |
| DM-x02 | Nhắc tới | Sửa một phần bởi DEC-009, DEC-169 | Không áp dụng: Danh sách trong phạm vi: Post (Accepted Answer, Anonymous Post) | Nhóm B. Danh sách trong phạm vi: Post (Accepted Answer, Anonymous Post) |
| DM-x03 | Phụ thuộc | Hiện hành | Không áp dụng: Ngoài phạm vi: AI tự viết bài, Related Posts | Nhóm B. Ngoài phạm vi: AI tự viết bài, Related Posts |
| GL:Accepted Answer | Nhắc tới | Sửa một phần bởi DEC-169 | Không áp dụng: Thuật ngữ | Nhóm B. Thuật ngữ; chưa có DEC |
| GL:Anonymous Post | Phụ thuộc | Sửa một phần bởi DEC-009 | Chuyển M11 | Nhóm B. Thuật ngữ; tính năng thuộc M11 (DEC-009) |
| GL:Lớp/Khối | Sở hữu | Hiện hành | FR-M03-01.05, BR-M03-06 | Nhóm B. Thuật ngữ; phần trên bài thuộc M03, phần hồ sơ thuộc M02 |
| ISS-034 | Nhắc tới | Hiện hành | Không áp dụng: Đã có QA-015 | Nhóm B. Đã có QA-015 |
| ISS-044 | Nhắc tới | Hiện hành | Không áp dụng: Đã có QA-025–QA-031 | Nhóm B. Đã có QA-025–QA-031 |
| ISS-046 | Nhắc tới | Hiện hành | Không áp dụng: Đã có QA-033, QA-034 | Nhóm B. Đã có QA-033, QA-034 |
| ISS-101 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-070 | Nhóm B. Đã có DEC-070 |
| ISS-107 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-077 | Nhóm B. Đã có DEC-077 |
| ISS-109 | Phụ thuộc | Trùng với DEC-079 | — | Nhóm B. Đã có DEC-079; MEDIUM/HEAVY không được tạo bài |
| ISS-127 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-098 | Nhóm B. Đã có DEC-098 |
| ISS-133 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-104 | Nhóm B. Đã có DEC-104 |
| ISS-134 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-105 | Nhóm B. Đã có DEC-105 |
| ISS-135 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-112 | Nhóm B. Đã có DEC-112 |
| ISS-142 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-113 | Nhóm B. Đã có DEC-113 |
| ISS-144 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-115 | Nhóm B. Đã có DEC-115 |
| ISS-180 | Nhắc tới | Hiện hành | Không áp dụng: Đã có QA-243 | Nhóm B. Đã có QA-243 |
| ISS-186 | Nhắc tới | Hiện hành | Không áp dụng: Đã có QA-240 | Nhóm B. Đã có QA-240 |
| ISS-189 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-127 | Nhóm B. Đã có DEC-127 |
| ISS-195 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-133 | Nhóm B. Đã có DEC-133 |
| ISS-196 | Nhắc tới | Hiện hành | Không áp dụng: Đã có QA-255 | Nhóm B. Đã có QA-255 |
| ISS-203 | Nhắc tới | Hiện hành | Không áp dụng: Đã có QA-263 | Nhóm B. Đã có QA-263 |
| ISS-213 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-142 | Nhóm B. Đã có DEC-142 |
| ISS-217 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-142 | Nhóm B. Đã có DEC-142 |
| ISS-228 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-142 | Nhóm B. Đã có DEC-142 |
| ISS-229 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-142 | Nhóm B. Đã có DEC-142 |
| OPEN-005 | Phụ thuộc | Hiện hành | TBD-M03-01 | Nhóm B. Hạ tầng ghi sự kiện hoãn; lượt xem bài (draft) phụ thuộc vào đây |
| OPEN-006 | Phụ thuộc | Hiện hành | TBD-M03-02 | Nhóm B. SSR/SEO hoãn; trang bài cho Guest chưa tối ưu index, xem trước link |
| QA-011 | Sở hữu | Sửa một phần bởi DEC-206 | FR-M03-07, FR-M03-07.01, FR-M03-07.06, BR-M03-39 | Nhóm B. Guest xem/đọc bài (công khai và nhóm Public), xem tóm tắt AI trên bài. Phần lý do SEO hoãn thực thi theo OPEN-006 DEC-206: tóm tắt AI chỉ cho người đã đăng nhập (M13); quyền xem bài của Guest không đổi. |
| QA-015 | Phụ thuộc | Sửa một phần bởi DEC-009, DEC-112 | Chuyển M11 | Nhóm B. Bài ẩn danh: Mod/Admin thấy danh tính (M11) |
| QA-018 | Phụ thuộc | Sửa một phần bởi DEC-019, DEC-156 | Chuyển M01 | Nhóm B. M01: bài của tài khoản đã xóa (bản Phase 2) |
| QA-020 | Phụ thuộc | Sửa một phần bởi DEC-079, DEC-115 | Chuyển M08 | Nhóm B. M08: "bài bị xóa không có khiếu nại" (bản Phase 2) |
| QA-025 | Sở hữu | Hiện hành | FR-M03-02 | Nhóm B. Không chèn ảnh trong nội dung, mọi media là tệp đính kèm. Cùng nội dung với DEC-029 nhưng có thêm lý do, nên giữ hiện hành |
| QA-027 | Sở hữu | Trùng với DEC-011 | — | Nhóm B. Cửa sổ xóa mềm 7 ngày |
| QA-028 | Sở hữu | Trùng với DEC-012 | — | Nhóm B. Ai quyết trạng thái nào (bản Phase 4) |
| QA-029 | Sở hữu | Bị thay bởi DEC-032 | — | Nhóm B. Giá trị mod_state bản Phase 4 (pending/active/under_review/removed) |
| QA-030 | Sở hữu | Trùng với DEC-013 | — | Nhóm B. Quét trước bài mới, quét lại khi sửa |
| QA-031 | Sở hữu | Trùng với DEC-013 | — | Nhóm B. Không quét lại bài cũ khi bật lại AI |
| QA-033 | Sở hữu | Sửa một phần bởi DEC-140 | FR-M03-01, BR-M03-06 | Nhóm B. Ý còn hiệu lực: Lớp/Khối là trường độc lập, tùy chọn trên bài |
| QA-034 | Sở hữu | Hiện hành | FR-M03-01, FR-M03-01.05, FR-M03-01.07, BR-M03-06 | Nhóm B. Lớp/Khối trên bài và trên hồ sơ là hai trường độc lập |
| QA-037 | Nhắc tới | Hiện hành | Không áp dụng: M06: không embed Accepted Answer | Nhóm B. M06: không embed Accepted Answer |
| QA-065 | Phụ thuộc | Trùng với DEC-019 | — | Nhóm B. M01: bài của tài khoản vô hiệu hóa bị ẩn |
| QA-132 | Phụ thuộc | Trùng với DEC-070 | — | Nhóm B. M07: chỉ có tắt thông báo theo bài |
| QA-141 | Nhắc tới | Hiện hành | Không áp dụng: M08: bình luận quét sau | Nhóm B. M08: bình luận quét sau |
| QA-171 | Sở hữu | Trùng với DEC-098 | — | Nhóm B. AI tự từ chối bài khi điểm ≥0.9 |
| QA-172 | Phụ thuộc | Trùng với DEC-098 | — | Nhóm B. M13: cùng ngưỡng 0.9/0.5 cho cổng nội dung và cảnh cáo |
| QA-177 | Sở hữu | Trùng với DEC-099 | — | Nhóm B. Quét trước lỗi: giữ chờ Mod, không tự đăng |
| QA-180 | Phụ thuộc | Trùng với DEC-102 | — | Nhóm B. M11: Member đăng bài; Group Mod ẩn/xóa bài |
| QA-182 | Phụ thuộc | Trùng với DEC-104 | — | Nhóm B. M11: cổng duyệt bài trong nhóm |
| QA-183 | Phụ thuộc | Sửa một phần bởi DEC-113 | Chuyển M11 | Nhóm B. M11: xóa nhóm, thành viên rời nhóm — bài xử lý thế nào |
| QA-190 | Phụ thuộc | Trùng với DEC-112 | — | Nhóm B. M11: ẩn danh theo từng bài trong nhóm |
| QA-191 | Phụ thuộc | Trùng với DEC-113 | — | Nhóm B. M12: trừ điểm theo xóa bài |
| QA-193 | Phụ thuộc | Trùng với DEC-115 | — | Nhóm B. M09: khiếu nại bài bị xóa |
| QA-240 | Nhắc tới | Hiện hành | Không áp dụng: M14 phụ thuộc M03 | Nhóm B. M14 phụ thuộc M03 |
| QA-243 | Nhắc tới | Hiện hành | Không áp dụng: M15: thống kê bài theo trạng thái | Nhóm B. M15: thống kê bài theo trạng thái |
| QA-248 | Phụ thuộc | Trùng với DEC-127 | — | Nhóm B. Dùng chung: múi giờ |
| QA-254 | Nhắc tới | Hiện hành | Không áp dụng: M13: log AI | Nhóm B. M13: log AI |
| QA-255 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: không xây hạ tầng ghi sự kiện ở MS1 (OPEN-005) | Nhóm B. Dùng chung: không xây hạ tầng ghi sự kiện ở MS1 (OPEN-005) |
| QA-263 | Nhắc tới | Hiện hành | Không áp dụng: Công nghệ | Nhóm B. Công nghệ |
| QA-271 | Phụ thuộc | Trùng với DEC-145 | — | Nhóm B. M05: chưa đếm lượt xem ở MS1 |
| QA-273 | Phụ thuộc | Trùng với DEC-142 | — | Nhóm B. M05: tác giả, Mod, Admin đổi Topic/Tag khi sửa bài |
| QA-277 | Phụ thuộc | Trùng với DEC-142 | — | Nhóm B. M05: bài nháp được 0 Topic |
| QA-279 | Nhắc tới | Hiện hành | Không áp dụng: M05: đếm bài khi xóa Topic | Nhóm B. M05: đếm bài khi xóa Topic |
| QA-288 | Phụ thuộc | Trùng với DEC-142 | — | Nhóm B. M05: gợi ý Topic khi sửa bài |
| QA-289 | Phụ thuộc | Trùng với DEC-142 | — | Nhóm B. M05: Mod đổi Topic/Tag không ghi lịch sử sửa |
| QA-311 | Phụ thuộc | Trùng với DEC-156 | — | Nhóm B. M01: dữ liệu khi xóa tài khoản |
| QA-319 | Nhắc tới | Hiện hành | Không áp dụng: M01: xóa lượt theo dõi bài khi xóa tài khoản | Nhóm B. M01: xóa lượt theo dõi bài khi xóa tài khoản |
| F-GRP-10 | Phụ thuộc | Hiện hành | Chuyển M11 | Nhóm B. M11: công tắc đăng ẩn danh (thay F-POST-05) |
| F-POST-01 | Sở hữu | Hiện hành | FR-M03-01, FR-M03-11, FR-M03-11.01, BR-M03-02 | Nhóm B. Tạo, đọc, sửa, xóa bài |
| F-POST-02 | Sở hữu | Hiện hành | FR-M03-02, FR-M03-02.01, BR-M03-04 | Nhóm B. Tải tệp đính kèm |
| F-POST-03 | Sở hữu | Hiện hành | FR-M03-01, BR-M03-03 | Nhóm B. Trình soạn bài |
| F-POST-04 | Sở hữu | Hiện hành | FR-M03-12, FR-M03-12.02, BR-M03-27 | Nhóm B. Lịch sử sửa |
| F-POST-06 | Sở hữu | Hiện hành | FR-M03-15, FR-M03-15.01, BR-M03-34 | Nhóm B. Xóa mềm |
| F-POST-07 | Sở hữu | Hiện hành | BR-M03-17 | Nhóm B. Mô hình 3 trường trạng thái |
| F-POST-08 | Sở hữu | Sửa một phần bởi DEC-034, DEC-098 | FR-M03-05, BR-M03-19 | Nhóm B. Quét trước (giá trị trạng thái kiểu Phase 4) |
| F-POST-09 | Sở hữu | Hiện hành | FR-M03-01, FR-M03-01.05, FR-M03-01.06, BR-M03-06 | Nhóm B. Lớp/Khối trên bài |
| MR-A02 | Nhắc tới | Hiện hành | Không áp dụng: M14 | Nhóm B. M14 |
| MR-A03 | Nhắc tới | Hiện hành | Không áp dụng: M15 | Nhóm B. M15 |
| MR-A04 | Phụ thuộc | Hiện hành | Không áp dụng: Phase 6: múi giờ áp dụng cho M03 | Nhóm B. Phase 6: múi giờ áp dụng cho M03 |
| MR-A05 | Nhắc tới | Hiện hành | Không áp dụng: Công nghệ | Nhóm B. Công nghệ |
| MR-FB-M08 | Phụ thuộc | Sửa một phần bởi DEC-099 | FR-M03-04.03, BR-M03-22 | Nhóm B. AI tắt: Moderation chỉ còn hàng chờ thủ công |
| MR-M08 | Phụ thuộc | Hiện hành | Chuyển M08 | Nhóm B. M08 sở hữu việc quét AI (gồm quét trước bài) |
| MR-M11 | Phụ thuộc | Hiện hành | Chuyển M11 | Nhóm B. M11 phụ thuộc M03; công tắc ẩn danh |
| MR-M12 | Nhắc tới | Hiện hành | Không áp dụng: M12 phụ thuộc M03 | Nhóm B. M12 phụ thuộc M03 |
| MR-M14 | Nhắc tới | Hiện hành | Không áp dụng: M14 phụ thuộc M03 | Nhóm B. M14 phụ thuộc M03 |
| MR-M15 | Nhắc tới | Hiện hành | Không áp dụng: M15 phụ thuộc M03 | Nhóm B. M15 phụ thuộc M03 |
| DEC-021 | Nhắc tới | Hiện hành | Không áp dụng: M02: avatar 5MB | Nhóm C. M02: avatar 5MB |
| QA-250 | Nhắc tới | Hiện hành | Không áp dụng: Lưu giữ dữ liệu chung | Nhóm C. Lưu giữ dữ liệu chung |
| DEC-128 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| DEC-130 | Phụ thuộc | Sửa một phần bởi DEC-160 | CC-01 (B.3) | Nhóm D. Dùng chung: tải tệp không quét virus; nêu "chỉ ảnh" trong khi DEC-035 cho tài liệu. Phần tài liệu của bài viết theo DEC-160 |
| DEC-131 | Nhắc tới | Sửa một phần bởi DEC-154 | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| DEC-132 | Nhắc tới | Sửa một phần bởi DEC-141, DEC-144 | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| DEC-134 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| DEC-135 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| DEC-136 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| DEC-138 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03. DEC-155, DEC-157 (ngoài bảng nguồn) sửa phần đồng ý chính sách |
| ISS-190 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| ISS-191 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| ISS-192 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| ISS-193 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| ISS-194 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| ISS-197 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| ISS-198 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| ISS-199 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| ISS-200 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| ISS-201 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| ISS-202 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| ISS-204 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| QA-249 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| QA-251 | Phụ thuộc | Trùng với DEC-130 | — | Nhóm D. Dùng chung: tải tệp không quét virus |
| QA-252 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| QA-253 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| QA-256 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| QA-257 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| QA-258 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| QA-259 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| QA-260 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| QA-261 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| QA-262 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| QA-264 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M03 |
| DEC-160 | Sở hữu | Hiện hành | FR-M03-02.07, FR-M03-02.08, FR-M03-02.09, BR-M03-08 | Nhóm A. Tài liệu đính kèm giữ, không quét mã độc |
| DEC-161 | Sở hữu | Sửa một phần bởi DEC-185 | FR-M03-01.12, FR-M03-05.07, FR-M03-05.10, FR-M03-05.11, FR-M03-16.04, BR-M03-26, BR-M03-36, BR-M03-48 | Nhóm A. Trạng thái kiểm duyệt: bài mới, "gỡ" = ẩn, quét lại khi sửa |
| DEC-162 | Sở hữu | Sửa một phần bởi DEC-184 | FR-M03-11.01, FR-M03-11.07, FR-M03-15.01, FR-M03-15.05, FR-M03-15.06, FR-M03-16.01, FR-M03-16.02, FR-M03-16.06, BR-M03-34, BR-M03-35, BR-M03-47 | Nhóm A. Sửa, xóa, khôi phục theo trạng thái; 7 × 24 giờ |
| DEC-163 | Sở hữu | Hiện hành | FR-M03-01.10, FR-M03-04.10, BR-M03-38 | Nhóm A. Phạm vi chặn của MEDIUM, HEAVY |
| DEC-164 | Sở hữu | Hiện hành | FR-M03-01.13, FR-M03-01.14, FR-M03-01.15, FR-M03-01.16, FR-M03-01.17, FR-M03-04.08, FR-M03-04.09, BR-M03-40, BR-M03-41, BR-M03-42, BR-M03-43 | Nhóm A. Phần bắt buộc, giới hạn độ dài, cảnh báo khi soạn |
| DEC-165 | Sở hữu | Hiện hành | FR-M03-03.01, FR-M03-03.05, FR-M03-03.06, FR-M03-03.09, FR-M03-03.10, FR-M03-03.11, FR-M03-08.04, FR-M03-08.05, FR-M03-08.06, FR-M03-08.11, FR-M03-08.12, FR-M03-09.01, FR-M03-09.02, FR-M03-09.04, FR-M03-09.05, FR-M03-09.06, FR-M03-09.07, FR-M03-09.08, BR-M03-11, BR-M03-12, BR-M03-14, BR-M03-15, BR-M03-16, BR-M03-44, BR-M03-45 | Nhóm A. Chi tiết poll |
| DEC-166 | Sở hữu | Sửa một phần bởi DEC-198 | FR-M03-05.12, FR-M03-05.13, BR-M03-46 | Nhóm A. Bài bị AI tự từ chối |
| DEC-167 | Sở hữu | Sửa một phần bởi DEC-246 | FR-M03-08.13, FR-M03-14.06, FR-M03-14.12, BR-M03-31 | Nhóm A. Phạm vi Khóa toàn bộ |
| DEC-168 | Sở hữu | Sửa một phần bởi DEC-185 | FR-M03-07.02, FR-M03-07.07, BR-M03-49 | Nhóm A. Mod không xem bài chưa công khai của người khác |
| DEC-169 | Sở hữu | Hiện hành | BR-M03-50 | Nhóm A. MS1 không có Accepted Answer, ảnh bìa |
| ISS-261 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-160 | Nhóm A. Đã có DEC-160 |
| ISS-262 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-161 | Nhóm A. Đã có DEC-161 |
| ISS-263 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-161 | Nhóm A. Đã có DEC-161 |
| ISS-264 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-162 | Nhóm A. Đã có DEC-162 |
| ISS-265 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-163 | Nhóm A. Đã có DEC-163 |
| ISS-266 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-164 | Nhóm A. Đã có DEC-164 |
| ISS-267 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-165 | Nhóm A. Đã có DEC-165 |
| ISS-268 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-166 | Nhóm A. Đã có DEC-166 |
| ISS-269 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-167 | Nhóm A. Đã có DEC-167 |
| ISS-270 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-162 | Nhóm A. Đã có DEC-162 |
| ISS-271 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-168 | Nhóm A. Đã có DEC-168 |
| ISS-272 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-169 | Nhóm A. Đã có DEC-169 |
| ISS-273 | Nhắc tới | Hiện hành | Không áp dụng: Đã có DEC-169 | Nhóm A. Đã có DEC-169 |
| QA-321 | Sở hữu | Trùng với DEC-160 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| QA-322 | Sở hữu | Trùng với DEC-161 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| QA-323 | Sở hữu | Trùng với DEC-161 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| QA-324 | Sở hữu | Trùng với DEC-162 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| QA-325 | Sở hữu | Trùng với DEC-163 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| QA-326 | Sở hữu | Trùng với DEC-164 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| QA-327 | Sở hữu | Trùng với DEC-165 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| QA-328 | Sở hữu | Trùng với DEC-166 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| QA-329 | Sở hữu | Trùng với DEC-167 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| QA-330 | Sở hữu | Trùng với DEC-162 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| QA-331 | Sở hữu | Trùng với DEC-168 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| QA-332 | Sở hữu | Trùng với DEC-169 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| QA-333 | Sở hữu | Trùng với DEC-169 | — | Nhóm A. Lời trả lời của stakeholder, bước 6 |
| DEC-097 | Phụ thuộc | Hiện hành | FR-M03-05.12, BR-M03-46 | Nhóm C. M13: các nhóm vi phạm AI kiểm duyệt phát hiện được |
| DEC-023 | Phụ thuộc | Hiện hành | Chuyển M02 | Nhóm B (bản 1.1). M02: tab trên hồ sơ; DEC-170 thêm tab "Đã xóa" |
| DEC-024 | Phụ thuộc | Hiện hành | Chuyển M02 | Nhóm B (bản 1.1). M02: tab trên hồ sơ; DEC-170 thêm tab "Đã xóa" |
| DEC-170 | Phụ thuộc | Hiện hành | FR-M03-15.03 | Nhóm B (bản 1.1). M02: tab "Đã xóa" liệt kê bài đã xóa còn trong hạn khôi phục; liệt kê và khôi phục thuộc M03 |
| DEC-174 | Phụ thuộc | Hiện hành | Chuyển M02 | Nhóm B (bản 1.1). M02: bookmark của bài không xem được; ý "bài bị xóa hẳn thì bỏ bookmark" chạm OPEN-010 |
| DEC-175 | Phụ thuộc | Hiện hành | FR-M03-07.01, BR-M03-18 | Nhóm B (bản 1.1). M02: bài hiện ở tab Bài viết theo trạng thái bài |
| DEC-178 | Nhắc tới | Hiện hành | Không áp dụng: M04: sửa, xóa bình luận khi bài bị khóa | Nhóm B (bản 1.1). M04: sửa, xóa bình luận khi bài bị khóa |
| DEC-179 | Phụ thuộc | Hiện hành | FR-M03-07.08, FR-M03-07.09 | Nhóm B (bản 1.1). M04: nội dung báo cáo được chỉ xóa mềm; Mod, Admin và chủ nội dung xem nội dung đã xóa; "Posts: see OPEN-010" |
| ISS-274 | Phụ thuộc | Trùng với DEC-170 | — | Nhóm B (bản 1.1). Câu hỏi M02 về tab "Đã xóa" |
| ISS-283 | Nhắc tới | Hiện hành | Không áp dụng: Câu hỏi M04, đã có DEC-179 | Nhóm B (bản 1.1). Câu hỏi M04 về xóa mềm |
| ISS-289 | Nhắc tới | Hiện hành | Không áp dụng: Câu hỏi M04, đã có DEC-179 | Nhóm B (bản 1.1). Câu hỏi M04 về xem lại nội dung đã xóa |
| OPEN-010 | Sở hữu | Bị thay bởi DEC-184 | — | Nhóm B (bản 1.1). M03: giữ 7 ngày khôi phục, hết hạn chuyển cờ thay vì xóa hẳn; Mod, Admin và chủ bài xem nội dung đã xóa theo DEC-179 |
| OPEN-011 | Nhắc tới | Hiện hành | Không áp dụng: M11, M16 | Nhóm B (bản 1.1). M11, M16: xét nguyên tắc xóa mềm |
| QA-334 | Phụ thuộc | Trùng với DEC-170 | — | Nhóm B (bản 1.1). M02: tab "Đã xóa" |
| QA-338 | Phụ thuộc | Trùng với DEC-174 | — | Nhóm B (bản 1.1). M02: bookmark bài không xem được |
| QA-342 | Nhắc tới | Hiện hành | Không áp dụng: M04: bình luận khi bài bị khóa | Nhóm B (bản 1.1). M04: bình luận khi bài bị khóa |
| QA-343 | Sở hữu | Trùng với DEC-184 | — | Nhóm B (bản 1.1). Phần bài viết: "vẫn giữ tính năng 7 ngày để khôi phục, sau đó thay vì xoá hẳn ta có thể chuyển cờ" |
| QA-349 | Sở hữu | Trùng với DEC-184 | — | Nhóm B (bản 1.1). Chủ nội dung xem lại nội dung đã xóa khi bị xử lý hoặc khiếu nại; áp cho bài theo OPEN-010 |
| DEC-184 | Sở hữu | Hiện hành | FR-M03-07.02, FR-M03-07.05, FR-M03-07.08, FR-M03-07.09, FR-M03-07.10, FR-M03-17, FR-M03-17.01, FR-M03-17.02, FR-M03-17.03, FR-M03-17.04, BR-M03-37, BR-M03-49 | Nhóm A (bản 1.1). Bài viết chỉ xóa mềm; Đã xóa hẳn là cờ, giữ dữ liệu; Mod, Admin, tác giả xem lại |
| ISS-290 | Sở hữu | Trùng với DEC-184 | — | Nhóm A (bản 1.1). Câu hỏi OPEN-010 |
| QA-350 | Sở hữu | Trùng với DEC-184 | — | Nhóm A (bản 1.1). Câu trả lời OPEN-010 |
| DEC-185 | Sở hữu | Hiện hành | FR-M03-05.05, FR-M03-05.06, FR-M03-05.14, FR-M03-07.02, FR-M03-07.07, FR-M03-07.11, FR-M03-13.06, BR-M03-26, BR-M03-29, BR-M03-49 | Nhóm A (bản 1.1). Mod xem bài Tự ẩn trong báo cáo; quét lại khi hiện lại bài Tự ẩn đã sửa |
| ISS-291 | Sở hữu | Trùng với DEC-185 | — | Nhóm A (bản 1.1). Câu hỏi bài Tự ẩn né kiểm duyệt |
| QA-351 | Sở hữu | Trùng với DEC-185 | — | Nhóm A (bản 1.1). Câu trả lời bài Tự ẩn né kiểm duyệt |
| DEC-186 | Phụ thuộc | Hiện hành | Chuyển M08 | Nhóm B. M08: điểm quét là điểm cao nhất trong bốn nhóm; AI không tự cảnh cáo Mod, Admin |
| DEC-190 | Phụ thuộc | Hiện hành | Chuyển M08 | Nhóm B. M08: báo cáo của người dùng không đổi trạng thái kiểm duyệt của bài; chỉ bước quét lại làm bài Bị gắn cờ; bài Bị gắn cờ thành mục trong vụ ở hàng chờ báo cáo |
| DEC-194 | Phụ thuộc | Hiện hành | Chuyển M08, M11 | Nhóm B. M08, M11: nhóm Bị khóa chặn đăng bài, bình chọn poll trong nhóm; nhóm Bị ẩn ẩn mọi bài của nhóm |
| ISS-300 | Phụ thuộc | Trùng với DEC-190 | — | Nhóm C. Báo cáo có làm bài Bị gắn cờ không |
| DEC-215 | Phụ thuộc | Hiện hành | Chuyển M07 | Nhóm B (đối chiếu FR-M07). M07: thông báo bài mới cho người theo dõi tác giả; không gửi khi bài ẩn danh, bị từ chối, sửa, khôi phục |
| DEC-195 | Sở hữu | Hiện hành | FR-M03-04.01, FR-M03-04.11, FR-M03-05.05, FR-M03-05.15, BR-M03-19, BR-M03-51 | Nhóm B (đối chiếu FR-M09). Bài của Admin đăng ngay, không quét, không duyệt; trong nhóm vẫn qua duyệt của nhóm |
| DEC-198 | Phụ thuộc | Hiện hành | BR-M03-46 | Nhóm B (đối chiếu FR-M09). M09: khiếu nại bài bị AI tự từ chối, chấp nhận thì Đã đăng ngay không quét lại |
| DEC-205 | Phụ thuộc | Hiện hành | Chuyển M13 | Nhóm B (đối chiếu FR-M13). M13: embedding bài tạo khi bài Đã đăng theo mọi đường, tạo lại khi đổi tiêu đề, nội dung chữ |
| DEC-206 | Phụ thuộc | Hiện hành | Chuyển M13 | Nhóm B (đối chiếu FR-M13). M13: tóm tắt bài theo yêu cầu, chỉ người đã đăng nhập |
| DEC-207 | Phụ thuộc | Hiện hành | Chuyển M13 | Nhóm B (đối chiếu FR-M13). M13: phạm vi nhật ký AI |
| DEC-240 | Phụ thuộc | Hiện hành | FR-M03-04.05, BR-M03-25 | Nhóm B (đối chiếu FR-M11). M11: bài của Owner không qua duyệt của nhóm; điểm 0.5–< 0.9 hoặc quét lỗi vào hàng chờ duyệt của Mod |
| DEC-230 | Phụ thuộc | Hiện hành | Chuyển M11 | Nhóm B (đối chiếu FR-M11). M11: bài nhóm không có điểm quét; quét lỗi thì chờ nhóm duyệt |
| DEC-231 | Phụ thuộc | Hiện hành | Chuyển M11 | Nhóm B (đối chiếu FR-M11). M11: Owner, Group Mod gỡ bài khỏi nhóm (xóa mềm, không trừ điểm) |
| DEC-246 | Phụ thuộc | Hiện hành | FR-M03-14.06, BR-M03-31 | Nhóm B (rà lại 1.7). M12: Khóa toàn bộ chặn cả rút upvote và upvote bình luận của bài |

### C.2 Chuỗi quyết định

| Chuỗi | Nội dung hiện hành |
|---|---|
| DM-2.1, QA-028, QA-029, DEC-012, F-POST-07 → DEC-031, DEC-032, DEC-033 → DEC-161; DEC-032 → DEC-190 | Ba trường trạng thái độc lập: trạng thái đăng (tác giả và luồng đăng), trạng thái kiểm duyệt (AI, Mod), mức khóa. Trạng thái đăng: Nháp, Chờ duyệt, Đã đăng, Tự ẩn, Bị từ chối, Đã xóa. Trạng thái kiểm duyệt: Bình thường, Bị gắn cờ, Bị Mod ẩn; bài mới mang Bình thường; "Mod gỡ bài" chính là Bị Mod ẩn (DEC-161). Mức khóa: Không khóa, Khóa bình luận (tác giả hoặc Mod), Khóa toàn bộ (chỉ Mod) kèm người khóa. Bài hiển thị khi Đã đăng và Bình thường. Bị thay: PENDING_REVIEW, LOCKED của draft; pending/active/under_review/removed và none/author/mod của Phase 4. Báo cáo của người dùng không đổi trạng thái kiểm duyệt; chỉ bước quét lại của AI làm bài Bị gắn cờ (DEC-190, M08). |
| QA-030, QA-031, DEC-013, F-POST-08 → DEC-034 → DEC-098, DEC-099 (MR-FB-M08) → DEC-161, DEC-166 | Bài vừa gửi → Chờ duyệt → quét. Điểm < 0.5: Đã đăng. 0.5 ≤ điểm < 0.9: giữ Chờ duyệt, chờ Mod duyệt (chấp nhận → Đã đăng; từ chối kèm lý do → Bị từ chối). Điểm ≥ 0.9: AI tự từ chối; tác giả thấy nhóm vi phạm, sửa và gửi lại không giới hạn, khiếu nại qua M09 (DEC-166). Ngưỡng 0.9/0.5 là giá trị tạm. Quét lỗi sau một lần thử lại: vào hàng chờ Mod. AI hoặc Moderation tắt: đăng ngay, không quét; bật lại không quét bài cũ. Sửa bài đã đăng: quét lại, bài vẫn hiện; điểm < 0.5 giữ nguyên, từ 0.5 trở lên (kể cả ≥ 0.9) Bị gắn cờ chờ Mod, lỗi giữ nguyên (DEC-161). |
| QA-027 → DEC-011 → DEC-038 → DEC-162 → DEC-184 (F-POST-06, DEC-113, DEC-129, DEC-179) | Tác giả xóa bài ở mọi trạng thái trừ Đã xóa → Đã xóa (xóa mềm), ghi thời điểm và trạng thái trước khi xóa, bài hiện ở tab "Đã xóa". Trong 7 × 24 giờ khôi phục được về trạng thái trước khi xóa (Chờ duyệt về Nháp); bài Bị Mod ẩn không khôi phục được. Hết hạn thì bài được gắn cờ Đã xóa hẳn: chỉ là cờ, mọi dữ liệu giữ nguyên (DEC-184); ý "cron job hard-delete" của DEC-011, DEC-038 bị thay. Mod, Admin xem bài Đã xóa hẳn qua báo cáo, lịch sử báo cáo, khiếu nại; tác giả xem lại từ thông báo xử lý, khiếu nại. Trừ điểm upvote và bỏ bookmark tính tại lúc gắn cờ (M12, M02). Tác giả sửa được bài Nháp, Bị từ chối, Đã đăng, Tự ẩn, kể cả khi bị khóa; không sửa Chờ duyệt, Đã xóa, Bị Mod ẩn. |
| DEC-065 → DEC-180; QA-011 → DEC-171; QA-034 → DEC-176 (bản 1.1) | Các sửa đổi này thuộc phần ngoài bài viết: DEC-180 thêm sự kiện "Bình luận của bạn đã bị ẩn" (M04, M07); DEC-171 cho Guest xem trang hồ sơ (M02); DEC-176 bỏ nhắc cập nhật Lớp/Khối trên hồ sơ (M02). Yêu cầu của M03 không đổi. |
| DM-2.3, F-POST-04 → DEC-037 → DEC-142 | Bài giữ lịch sử sửa đầy đủ, công khai nhãn "(đã chỉnh sửa)" và "Xem lịch sử". Mod, Admin đổi Topic/Tag trên bài người khác không ghi vào lịch sử, không báo tác giả. Phần bình luận của DEC-037 thuộc M04. |
| DM-2.2, QA-025, QA-078, QA-079 → DEC-029, DEC-030 | Trình soạn: đậm, nghiêng, gạch chân, gạch ngang, tô sáng; tiêu đề H1–H3; danh sách chấm, số, việc cần làm; code dòng và khối code; LaTeX nhập thô (chưa có trình soạn trực quan); bảng; trích dẫn; đường kẻ ngang; liên kết có nhãn. Không chèn ảnh trong nội dung: mọi media là tệp đính kèm ở phần dưới bài ("Image" của draft bị thay). |
| DEC-035, QA-086, DEC-130, QA-251 → DEC-160 | Bài đính kèm ảnh JPEG/PNG/WebP (5 MB × 10) và tài liệu PDF/DOCX/XLSX/PPTX (20 MB × 3), tính riêng. Tài liệu không được quét mã độc ở MS1; tiền đề "chỉ tải ảnh" của DEC-130 không áp cho tài liệu bài viết; rủi ro ghi ở CC-01. |
| DM-2.4, QA-080, QA-081, QA-088, QA-089 → DEC-030, DEC-036 → DEC-165 | Một loại bài. Poll tùy chọn, tối đa 1 poll/bài, 2–10 lựa chọn, poll đóng (chỉ tác giả đặt và thêm lựa chọn). Hai tùy chọn: chọn một/chọn nhiều (mặc định chọn nhiều), hiện kết quả trước khi bình chọn (mặc định tắt); khóa khi bài đã gửi. Thêm, bỏ poll chỉ khi chưa gửi; sau khi gửi chỉ thêm lựa chọn (≤ 10) và đổi hạn. Hạn bắt buộc, không trước hiện tại, đổi sớm hoặc muộn được khi poll còn mở; kết thúc ngay = hạn bằng hiện tại; đã đóng không mở lại. Khi poll mở, luôn đổi phiếu và bỏ chọn được (tùy chọn "cho đổi phiếu" bị bỏ). % = lượt chọn ÷ tổng lượt chọn, làm tròn số nguyên. Tác giả được bình chọn poll của mình. |
| DM-2.1, DG-5, DM-x02, GL:Anonymous Post, QA-015 → DEC-009 → DEC-112 | Bài ẩn danh chỉ có trong nhóm bật tùy chọn ẩn danh, thuộc M11. Không có ẩn danh ở cấp hệ thống cho bài ngoài nhóm. |
| QA-033, QA-034 → DEC-140 (DM-3.3, F-POST-09) | Lớp/Khối là trường tùy chọn trên bài (10, 11, 12), do tác giả chọn, độc lập với Lớp/Khối trên hồ sơ và với Topic. Phần "2 tầng Category → Topic" của QA-033 bị thay (M05). |
| QA-018 → DEC-019 → DEC-156 | Bài của tài khoản DEACTIVATED và DELETED bị ẩn (mở link thấy "Nội dung không tồn tại"). Phần "bài của tài khoản đã xóa vẫn hiển thị" của QA-018 bị thay. |
| QA-020 → DEC-079, DEC-115 | Bài bị Mod/Admin xóa do vi phạm được khiếu nại (M09, 30 ngày); phần "bài bị xóa không có khiếu nại" của QA-020 bị thay. Mức MEDIUM không được tạo bài mới; HEAVY không được tạo bài và bình luận (M08). |
| DM-2.1 → DEC-049 → DEC-141, DEC-142 | Topic bắt buộc 1–3 khi gửi bài, bài nháp được 0 Topic ("nếu sử dụng" của draft bị thay); quy tắc thuộc M05. |
| DM-2.1 → DEC-145 (OPEN-005) | Lượt xem bài chưa được đếm ở MS1; xem TBD-M03-01. |
| QA-183 → DEC-105 → DEC-113 | Nhóm bị xóa: bài trong nhóm bị ẩn (xóa mềm), không trừ điểm; thành viên rời hoặc bị kick: bài giữ nguyên. |
| DEC-065 → DEC-147, DEC-151 | Danh sách sự kiện thông báo của DEC-065 còn hiệu lực cho bài viết (đăng, bị từ chối, bị ẩn, poll kết thúc); DEC-147, DEC-151 chỉ thêm sự kiện liên kết Google và đặt lại mật khẩu (M01). |
| DEC-079 → DEC-118, DEC-122, DEC-163 | Mức MEDIUM, HEAVY không được lưu nháp mới, gửi nháp, gửi lại bài bị từ chối; vẫn sửa bài đã đăng, khôi phục bài và bình chọn poll (DEC-163). HEAVY cũng không bình luận. DEC-118, DEC-122 chỉ thêm ngoại lệ ẩn khỏi bảng xếp hạng (M12). |
| DEC-030 → DEC-164 | Gửi bài cần tiêu đề và nội dung hoặc poll (tệp không thay nội dung); nháp phải có ít nhất tiêu đề, nội dung, poll hoặc tệp. Tiêu đề ≤ 150 ký tự, nội dung ≤ 6.000 từ (cụm chữ ngăn cách bởi khoảng trắng), áp dụng cả nháp; cảnh báo ngay khi soạn, vượt thì từ chối lưu và gửi, giữ nội dung. |
| DEC-033 → DEC-167 → DEC-246 | Khóa toàn bộ chặn bình luận mới, mọi thao tác upvote (upvote mới, rút lại, trên bài và bình luận của bài) và bình chọn poll (kể cả đổi, bỏ phiếu); bookmark và báo cáo vẫn được. |
| DM-2.1, DM-4.2.1, GL:Accepted Answer, DM-x02 → DEC-169 | MS1 không có Accepted Answer (toàn hệ thống) và bài không có ảnh bìa; ảnh dùng qua phần đính kèm. |
| DEC-168 → DEC-184, DEC-185 | Mod, Admin không xem bài Nháp, Bị từ chối của người khác; xem bài Chờ duyệt qua hàng chờ, bài Bị gắn cờ và Bị Mod ẩn qua M08, M09; bài Tự ẩn, Đã xóa, Đã xóa hẳn chỉ trong báo cáo, lịch sử báo cáo, khiếu nại liên quan tới bài đó. Ý "không xem bài Tự ẩn" của DEC-168 bị DEC-185 thay. |
| DEC-013 → DEC-161 → DEC-185 | Sửa bài Đã đăng thì quét lại ngầm, bài vẫn hiển thị trong lúc quét; điểm < 0.5 giữ nguyên, ≥ 0.5 sang Bị gắn cờ, quét lỗi giữ nguyên. DEC-185 thêm: sửa bài Tự ẩn không quét lúc lưu; khi tác giả hiện lại bài Tự ẩn đã sửa trong lúc ẩn thì quét lại y như vậy. Chỉ quét khi công tắc AI tổng và Moderation đều bật. |
| DEC-050 → DEC-142, DEC-144 | Định nghĩa "từ" của DEC-144 (cụm chữ ngăn cách bởi khoảng trắng) được M03 dùng lại để đếm giới hạn 6.000 từ của nội dung bài (BR-M03-42). Các phần khác của DEC-050, DEC-142, DEC-144 thuộc M05. |
| DEC-079 → DEC-188; DEC-098 → DEC-186 | Chỉ sửa phần thuộc M08: cách giảm mức cảnh cáo, thời gian thử thách N × 24 giờ (DEC-188); điểm quét là điểm cao nhất trong bốn nhóm, ngưỡng không đổi theo mức cảnh cáo, AI không tự cảnh cáo Mod, Admin (DEC-186). Ngưỡng 0,9/0,5 và hạn chế tạo bài ở MEDIUM, HEAVY của M03 không đổi. |
| DEC-079 → DEC-211; QA-011 → DEC-208 (M06) | Chỉ sửa phần thuộc M06: giảm hạng ×0,5 của người ở mức HEAVY nhân vào Điểm cuối, chỉ khi xếp theo Liên quan (DEC-211); Guest tìm bài bằng full-text (DEC-208). Quyền Guest xem bài của M03 không đổi. |
| DEC-065 → DEC-215, DEC-218; DEC-070 → DEC-219, DEC-220 (đối chiếu FR-M07) | Phần thuộc M07: thêm sự kiện "người bạn theo dõi có bài mới", quy tắc người nhận; tắt thông báo Chat chỉ ẩn popup, công tắc tắt thông báo bài có trên mọi bài. Không đổi yêu cầu của module này. |
| DEC-013 → DEC-195 | Bài của Admin được đăng ngay, không quét trước, không quét lại khi sửa, không qua duyệt (BR-M03-51); bài của Admin trong nhóm vẫn qua bước duyệt của nhóm (M11). Phần còn lại của DEC-013 giữ như chuỗi DEC-013 → DEC-161 → DEC-185. |
| DEC-166 → DEC-198 | Bài bị AI tự từ chối khiếu nại được (M09); chấp nhận thì Đã đăng ngay, không quét lại; tác giả đã sửa và gửi lại trước khi có kết luận thì trạng thái bài không đổi (BR-M03-46). |
| DEC-093, DEC-099 → DEC-205, DEC-206, DEC-207; QA-011 → DEC-206 | Phần thuộc M13: embedding bài tạo khi bài Đã đăng, tạo lại khi đổi tiêu đề, nội dung chữ; tóm tắt theo yêu cầu, chỉ người đã đăng nhập (Guest bấm thì được nhắc đăng nhập); phạm vi nhật ký AI. Yêu cầu của M03 không đổi, chỉ thêm dòng Giao tiếp với M13. |
| DEC-186 → DEC-204 (ngoài bảng nguồn; dấu sửa trích DEC-097) | DEC-204 chỉ quy định khi hai nhóm vi phạm cùng điểm cao nhất thì lấy theo thứ tự nhóm của DEC-097; phần thuộc M08, M13, không chạm M03. Cạnh DEC-097 → DEC-186 của tool là trích dẫn, không phải sửa đổi. |
| DEC-104 → DEC-240 | Bài của Owner nhóm không qua duyệt của nhóm; điểm 0.5–< 0.9 hoặc quét thất bại vào hàng chờ duyệt của Mod như bài không thuộc nhóm (BR-M03-25). |
