---
module: M12
ten_module: Gamification
ma_tai_lieu: FR-M12
phien_ban: 1.1
trang_thai: Đã chốt
ngay: 2026-10-24
tac_gia: Phạm Văn Đức
moc_nguon: DEC-271, QA-477, ISS-415, OPEN-012
steps_completed: [1, 2, 3, 4, 5, 6, 7]
---
# Tài liệu yêu cầu chức năng — M12 Gamification

| Mã tài liệu | FR-M12 |
|---|---|
| Dự án | iShare |
| Module | M12 — Gamification |
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

Gamification ghi nhận đóng góp của học sinh: người dùng upvote bài viết và bình luận hữu ích, tác giả nhận điểm đóng góp
theo trọng số (bài viết cao hơn bình luận), đạt huy hiệu khi điểm chạm các mốc, nhận danh hiệu "Ngôi sao tuần" khi lọt
top của tuần và được xếp hạng trên bảng xếp hạng chung. Module phục vụ mục tiêu thúc đẩy đóng góp tích cực bằng phần
thưởng rõ ràng, đồng thời hạn chế việc spam bình luận để "cày điểm".

### 1.2 Phạm vi

**Trong phạm vi:**

- Upvote bài viết (Post Star) và bình luận (Comment Star): upvote, rút lại upvote; chỉ có upvote, không có downvote;
  không tự upvote nội dung của chính mình; người chưa đăng nhập không upvote được.
- Điểm đóng góp: cộng khi nhận upvote theo trọng số bài viết và bình luận; trừ khi upvote bị rút; trừ hoặc giữ khi nội
  dung mất đi tùy nguyên nhân trực tiếp hay gián tiếp; hoàn điểm khi khiếu nại bài bị gỡ được chấp nhận; điểm không giảm
  theo thời gian.
- Huy hiệu theo mốc tổng điểm: trao tự động, vĩnh viễn, ghi ngày đạt, không hiện tiến độ trước khi đạt.
- Danh hiệu theo chu kỳ "Ngôi sao tuần" cho top người dùng của tuần, kèm lịch sử các lần đạt.
- Bảng xếp hạng người dùng: tuần qua, tháng qua (đã chốt) và toàn thời gian (tính định kỳ); lọc theo Lớp/Khối; đồng hạng;
  loại người ở mức cảnh cáo HEAVY, tài khoản bị ban, vô hiệu hóa; cách xử lý tài khoản đã xóa.
- Nhãn công khai "Tài khoản đã bị khóa" cho tài khoản bị ban, ở mọi nơi tên người đó xuất hiện.
- Các sự kiện của module làm phát sinh thông báo: upvote, bỏ upvote, đạt huy hiệu (cũng là "mốc điểm"), danh hiệu tuần.
- Hành vi của module khi cờ tính năng Gamification tắt: thao tác bị từ chối và việc vẫn chạy ngầm.

**Ngoài phạm vi:**

- Hiển thị điểm, huy hiệu trên trang hồ sơ — M02 User Profile (M12 cung cấp số liệu).
- Gửi, gộp, tắt thông báo (kể cả gộp thông báo upvote 5 phút) — M07 Notification.
- Xóa bài và mốc "Đã xóa hẳn" của bài; khóa bài chặn upvote — M03 Post & Content. Xóa, ẩn bình luận — M04 Comment.
- Gỡ nội dung vi phạm, cảnh cáo, ban và mức cảnh cáo — M08 Moderation. Xét khiếu nại bài bị gỡ — M09 Appeal (M12 chỉ
  hoàn điểm khi khiếu nại được chấp nhận).
- Quyền vote trong nhóm, gỡ nội dung khỏi nhóm, xóa nhóm — M11 Group.
- Bật, tắt cờ tính năng Gamification — M10 Admin Panel.
- Dùng số upvote làm tín hiệu Trending, xếp hạng và sắp xếp tìm kiếm, thứ tự Top của bình luận — M05, M06, M14, M04.
- Thống kê toàn hệ thống — M15 Analytics & Stats.
- Đã quyết không làm: Accepted Answer và điểm thưởng đi kèm (MS1); downvote; bảng xếp hạng, huy hiệu riêng cho giáo
  viên; bảng xếp hạng, điểm riêng theo nhóm; AI tự cộng, trừ điểm hoặc trao huy hiệu; xem lại bảng xếp hạng của các chu
  kỳ trước.

## 2. Thuật ngữ và viết tắt

### 2.1 Thuật ngữ

| Thuật ngữ | Định nghĩa |
|---|---|
| Upvote | Lượt đánh giá hữu ích của một người dùng đã đăng nhập cho một bài viết (Post Star) hoặc một bình luận (Comment Star) của người khác. Mỗi người có nhiều nhất một upvote đang có hiệu lực trên mỗi bài viết hoặc bình luận; upvote là bật/tắt, bấm lại thì rút lại. Không có downvote. |
| Post Star, Comment Star | Upvote trên bài viết, upvote trên bình luận. Hai loại được tính điểm với trọng số khác nhau. |
| Điểm | Điểm đóng góp của một người dùng: tổng điểm từ các upvote đang có hiệu lực trên bài viết và bình luận của người đó (Post Star 2 điểm, Comment Star 1 điểm), sau khi đã trừ phần của nội dung mất đi do trực tiếp. Điểm không giảm theo thời gian. |
| Điểm trong chu kỳ | Điểm từ các upvote có thời điểm upvote nằm trong chu kỳ, còn hiệu lực lúc tính và nằm trên nội dung chưa bị trừ điểm lúc tính, theo trọng số của điểm. Không bao giờ âm. |
| Huy hiệu | Cột mốc trao tự động khi tổng điểm của người dùng đạt một ngưỡng; có 5 huy hiệu. Đã đạt thì giữ vĩnh viễn. |
| Danh hiệu "Ngôi sao tuần" | Danh hiệu trao cho những người đứng đầu bảng xếp hạng của một tuần khi tuần đó kết thúc; có thể đạt nhiều lần ở các tuần khác nhau, nhưng chỉ hiện trên hồ sơ trong tuần ngay sau tuần đạt. |
| Bảng xếp hạng | Danh sách người dùng toàn hệ thống có điểm trong chu kỳ lớn hơn 0, xếp theo điểm đó, có ba tab: Tuần (tuần vừa kết thúc, đã chốt), Tháng (tháng vừa kết thúc, đã chốt), Toàn thời gian (tính lại định kỳ). |
| Chu kỳ tuần, chu kỳ tháng | Tuần lịch từ 00:00 thứ Hai đến trước 00:00 thứ Hai tuần sau; tháng lịch từ 00:00 ngày mùng 1 đến trước 00:00 ngày mùng 1 tháng sau; tính theo giờ Việt Nam (UTC+7). Chu kỳ toàn thời gian không có kết thúc. |
| Đồng hạng | Những người có cùng điểm trong chu kỳ hiện cùng một thứ hạng; người kế tiếp nhận thứ hạng bằng số người đứng trước cộng một. |
| Hạng cắt | Thứ hạng thấp nhất được nhận danh hiệu "Ngôi sao tuần" (hạng 3). |
| Gỡ vì vi phạm | Mod hoặc Admin hệ thống ẩn một bài viết (bài sang trạng thái kiểm duyệt Bị Mod ẩn của M03, FR-M08 gọi là Bị ẩn) hoặc ẩn một bình luận vì chính nội dung đó vi phạm (M08). Khác với gỡ khỏi nhóm của Owner, Group Mod (M11). |
| Đã xóa hẳn | Cờ của bài do tác giả tự xóa khi hết 7 ngày khôi phục (M03); bài không còn khôi phục được. |
| Thời điểm upvote | Lúc người dùng bấm upvote và upvote có hiệu lực; dùng để xếp upvote vào chu kỳ. |
| Chốt chu kỳ | Tính một lần bảng xếp hạng cuối cùng của một tuần hoặc tháng vừa kết thúc bằng số liệu đúng mốc đầu, cuối chu kỳ; bảng này hiện ở tab Tuần hoặc Tháng cho tới lần chốt sau. |
| Nhãn "Tài khoản đã bị khóa" | Nhãn công khai hiện cạnh tên của tài khoản đang ở trạng thái BANNED. |
| Cờ tính năng Gamification | Công tắc cấu hình bật, tắt module này (M10). |
| Có hiệu lực, Đã rút | Trạng thái của upvote của một người trên một nội dung: đang được tính, hoặc đã bị người đó bấm lại để rút. |
| Đang tính điểm, Đã trừ điểm | Trạng thái của một bài viết, bình luận đối với điểm của tác giả: upvote trên nội dung đang được cộng vào điểm, hoặc phần điểm đó đã bị trừ (BR-M12-08). |
| Chưa đạt, Đã đạt | Trạng thái của một huy hiệu với một người dùng; Đã đạt không đổi nữa. |
| Được xếp hạng, Bị loại, Hiện mờ | Trạng thái của một người dùng trên bảng xếp hạng: có thứ hạng; không hiện vì HEAVY, BANNED, DEACTIVATED, DELETED hoặc điểm chu kỳ bằng 0; hiện mờ kèm nhãn "[Người dùng đã xóa]" trên bảng đã chốt. |
| Đang diễn ra, Đã kết thúc chưa chốt, Đã chốt đang hiển thị, Không còn hiển thị | Trạng thái của một chu kỳ tuần hoặc tháng: chưa tới mốc cuối; đã qua mốc cuối nhưng chưa có lần tính định kỳ; đã chốt và đang hiện ở tab Tuần, Tháng; đã bị bảng của lần chốt sau thay thế. |

### 2.2 Viết tắt

| Viết tắt | Đầy đủ |
|---|---|
| FR | Functional Requirement — yêu cầu chức năng |
| BR | Business Rule — quy tắc nghiệp vụ |
| AI | Trí tuệ nhân tạo; ở module này chỉ là việc AI tự ẩn bình luận của M08, một sự kiện làm trừ điểm |
| UTC | Giờ phối hợp quốc tế; giờ Việt Nam là UTC+7 |

## 3. Thông tin đầu vào

### 3.1 Tài liệu đầu vào

| Tài liệu | Phiên bản / mốc |
|---|---|
| Draft: docs/_temp/iShare_modules.md, iShare_specs_general.md | Theo ngày sửa tệp |
| Register: decisions, qa-log, issue-queue, open-issues, glossary, module-registry | DEC-271, QA-477, ISS-415, OPEN-012 (khớp `moc_nguon`) |

### 3.2 Tài liệu liên quan

| Module | Liên quan ở điểm nào |
|---|---|
| M01 Authentication & Account | Trạng thái tài khoản DEACTIVATED, DELETED; upvote đã cho của tài khoản đã xóa vẫn tính. |
| M02 User Profile | Hiển thị điểm, huy hiệu trên hồ sơ; nhãn "Tài khoản đã bị khóa" trên hồ sơ. |
| M03 Post & Content | Bài viết là đối tượng upvote; mốc "Đã xóa hẳn" của bài tự xóa là lúc trừ điểm; Khóa toàn bộ chặn upvote. |
| M04 Comment | Bình luận là đối tượng upvote; thời điểm xóa, ẩn bình luận là mốc trừ điểm. |
| M05 Topic & Tag, M06 Search, M14 Feed & Discovery | Dùng số upvote cho Trending, xếp hạng và sắp xếp kết quả. |
| M07 Notification | Gửi thông báo upvote, huy hiệu, mốc điểm, danh hiệu tuần. |
| M08 Moderation | Gỡ nội dung vì vi phạm (trừ điểm ngay); mức HEAVY và tài khoản BANNED (loại khỏi bảng xếp hạng, nhãn). |
| M09 Appeal | Khiếu nại bài bị gỡ được chấp nhận thì hoàn điểm; ban được lật thì tài khoản ACTIVE lại. |
| M10 Admin Panel | Cờ tính năng Gamification. |
| M11 Group | Vote trong nhóm; xóa nhóm, gỡ khỏi nhóm, rời nhóm không trừ điểm; không có bảng xếp hạng theo nhóm. |
| M15 Analytics & Stats | Thống kê hệ thống tách khỏi thống kê người dùng của M12. |

## 4. Tổng quan chức năng

### 4.1 Luật, tiêu chuẩn liên quan

Không có.

### 4.2 Vai trò

| Vai trò | Mô tả trong module này |
|---|---|
| Guest | Người chưa đăng nhập. Xem bảng xếp hạng, điểm và huy hiệu của người dùng; không upvote. |
| User | Người dùng đã đăng nhập. Upvote, rút lại upvote bài viết và bình luận của người khác; nhận điểm, huy hiệu, danh hiệu từ nội dung của mình; xem bảng xếp hạng. |
| Tác giả | Vai trò theo ngữ cảnh: người đăng bài viết hoặc bình luận đang xét. Không upvote nội dung của chính mình; nhận điểm khi nội dung được upvote. |
| Mod | Có quyền của User. Gỡ nội dung vì vi phạm ở M08, việc này làm tác giả bị trừ điểm. Không chỉnh tay điểm, huy hiệu, danh hiệu. |
| Admin | Có quyền của Mod. Vẫn dùng được module khi cờ Gamification tắt. Không chỉnh tay điểm, huy hiệu, danh hiệu. |
| Hệ thống | Tính điểm, trao huy hiệu, tính bảng xếp hạng định kỳ, chốt chu kỳ và trao danh hiệu tuần, gắn nhãn "Tài khoản đã bị khóa", chặn thao tác khi cờ Gamification tắt. |

### 4.3 Ma trận quyền

| Hành động | Guest | User | Mod | Admin | Yêu cầu |
|---|---|---|---|---|---|
| Upvote, rút lại upvote bài viết hoặc bình luận của người khác | ✗ | ✓ | ✓ | ✓ | FR-M12-01.01, FR-M12-01.02, FR-M12-01.08 |
| Upvote nội dung của chính mình | — | ✗ | ✗ | ✗ | FR-M12-01.06, FR-M12-01.07 |
| Xem bảng xếp hạng | ✓ | ✓ | ✓ | ✓ | FR-M12-06.01 |
| Xem điểm, huy hiệu của một người dùng | ✓ | ✓ | ✓ | ✓ | FR-M12-03.06; M02 |
| Chỉnh tay điểm; trao, thu hồi huy hiệu hoặc danh hiệu | ✗ | ✗ | ✗ | ✗ | FR-M12-02.06, FR-M12-03.09 |
| Dùng module khi cờ Gamification tắt | ✗ | ✗ | ✗ | ✓ | FR-M12-08.01, FR-M12-08.06 |

<!-- Ô nói thẳng: hàng 1 cột Guest (DEC-126, QA-011: mọi tương tác cần đăng nhập), cột User (DEC-119); hàng 2
     (DEC-120); hàng 3, 4 cột Guest (QA-011); hàng 6 (DEC-225: Admin vẫn mở được module).
     Ô suy ra: hàng 1, 2 cột Mod, Admin (vai trò cao có mọi quyền của vai trò thấp, BR-M10-01; HEAVY vẫn vote, DEC-079);
     hàng 3, 4 cột User, Mod, Admin (Guest xem được thì người đã đăng nhập xem được); hàng 5 (DG-5, DM-11: điểm chỉ
     theo rule, không cơ chế cộng/trừ ngoài rule; DEC-090: hằng số không chỉnh qua giao diện; DEC-114: huy hiệu không
     thu hồi; quyền "Manage badges" của DM-1.3 đã hết hiệu lực); hàng 6 cột Guest, User, Mod (DEC-225 từ chối mọi yêu
     cầu của người dùng tới module).
     "—": hàng 2 cột Guest (Guest không có nội dung của mình).
     Quyền vote trong nhóm (thành viên, người ngoài nhóm Public, nhóm Private) và Khóa toàn bộ chặn upvote do M11, M03
     quy định; ghi ở mục Giao tiếp với module khác. -->

### 4.4 Danh sách chức năng

| ID | Chức năng | Tác nhân chính | Kích hoạt |
|---|---|---|---|
| FR-M12-01 | Upvote và rút lại upvote | User | Người dùng bấm nút upvote trên một bài viết hoặc bình luận của người khác |
| FR-M12-02 | Cập nhật điểm đóng góp | Hệ thống | Một upvote được thêm hoặc rút lại; nội dung mất đi do tác giả tự xóa hoặc bị gỡ vì vi phạm; khiếu nại bài bị gỡ được chấp nhận (M09) |
| FR-M12-03 | Trao huy hiệu theo mốc điểm | Hệ thống | Tổng điểm của người dùng chạm mốc của một huy hiệu người đó chưa có |
| FR-M12-04 | Tính bảng xếp hạng định kỳ | Hệ thống | Mỗi 60 phút |
| FR-M12-05 | Chốt chu kỳ và trao danh hiệu "Ngôi sao tuần" | Hệ thống | Lần tính định kỳ đầu tiên sau khi một tuần hoặc một tháng kết thúc |
| FR-M12-06 | Xem bảng xếp hạng | Guest, User | Người xem mở bảng xếp hạng, chọn chu kỳ hoặc Lớp/Khối |
| FR-M12-07 | Gắn nhãn "Tài khoản đã bị khóa" | Hệ thống | Tên của một tài khoản BANNED được hiển thị ở bất kỳ đâu |
| FR-M12-08 | Chặn thao tác Gamification khi cờ tắt | Hệ thống | Người dùng gửi yêu cầu tới module trong lúc cờ tính năng Gamification tắt |

### 4.5 Mốc và ưu tiên

Toàn bộ yêu cầu của module thuộc MS1, ưu tiên **Should** (dòng M12 của bảng Module List và bảng MoSCoW Summary của
module-registry khớp nhau: Should gồm M11, M12, M16). Không có yêu cầu ngoại lệ về ưu tiên.

## 5. Yêu cầu chức năng

### 5.1 FR-M12-01 Upvote và rút lại upvote

**Yêu cầu cấp trên:** Hệ thống phải cho phép người dùng đã đăng nhập upvote bài viết và bình luận của người khác và rút lại upvote của mình.

**Lý do:** Upvote là tín hiệu chính để đánh giá mức độ hữu ích của bài viết và bình luận. Chỉ có upvote; nội dung xấu được xử lý bằng báo cáo. Việc tự upvote bị chặn ngay từ nút bấm để chặn gian lận từ gốc.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M12-01.01 | Khi người dùng đã đăng nhập bấm upvote trên một bài viết hoặc bình luận của người khác mà người đó chưa có upvote đang có hiệu lực, hệ thống phải ghi nhận upvote kèm thời điểm upvote (BR-M12-02). |
| FR-M12-01.02 | Khi người dùng bấm lại vào upvote đang có hiệu lực của mình, hệ thống phải rút lại upvote đó (BR-M12-02). |
| FR-M12-01.03 | Nếu người dùng đã có upvote đang có hiệu lực trên một nội dung, hệ thống phải không ghi nhận thêm upvote thứ hai của người đó trên nội dung ấy (BR-M12-02). |
| FR-M12-01.04 | Hệ thống phải phân biệt upvote bài viết (Post Star) với upvote bình luận (Comment Star) (BR-M12-01). |
| FR-M12-01.05 | Hệ thống phải không có downvote hay phản ứng nào khác ngoài upvote trên bài viết và bình luận (BR-M12-01). |
| FR-M12-01.06 | Hệ thống phải ẩn hoặc tắt nút upvote trên bài viết và bình luận của chính người xem (BR-M12-03). |
| FR-M12-01.07 | Nếu người dùng gửi upvote cho bài viết hoặc bình luận của chính mình, hệ thống phải từ chối (BR-M12-03). |
| FR-M12-01.08 | Nếu người chưa đăng nhập upvote, hệ thống phải từ chối (BR-M12-04). |
| FR-M12-01.09 | Hệ thống phải cho người dùng ở mức cảnh cáo HEAVY upvote như người dùng khác (BR-M12-04). |
| FR-M12-01.10 | Nếu bài viết đang ở mức Khóa toàn bộ, hệ thống phải từ chối upvote mới và rút lại upvote trên bài viết đó và trên mọi bình luận của bài (BR-M12-04). |
| FR-M12-01.11 | Nếu người không là thành viên upvote bài của nhóm Private, kể cả bài của nhóm vừa chuyển sang Private, hệ thống phải từ chối (BR-M12-04). |
| FR-M12-01.12 | Nếu bài viết hoặc bình luận không còn hiển thị với người dùng (đã xóa, bị ẩn), hệ thống phải từ chối upvote trên nội dung đó. |
| FR-M12-01.13 | Khi một upvote được ghi nhận hoặc được rút lại, hệ thống phải gửi sự kiện tương ứng cho M07 để thông báo cho tác giả theo cách gộp của M07 (BR-M12-26). |

### 5.2 FR-M12-02 Cập nhật điểm đóng góp

**Yêu cầu cấp trên:** Hệ thống phải tính điểm đóng góp của mỗi người dùng từ upvote trên bài viết và bình luận của họ, trừ và hoàn điểm khi nội dung mất đi hoặc được khôi phục theo đúng nguyên nhân.

**Lý do:** Gamification thúc đẩy đóng góp tích cực bằng phần thưởng rõ ràng. Upvote bài viết có trọng số gấp đôi bình luận để việc spam bình luận "cày điểm" kém hiệu quả hơn hẳn đăng bài, nhất quán với chủ trương đề cao nội dung có chiều sâu. Điểm chỉ bị trừ khi nội dung mất đi do chính hành động hay vi phạm của người giữ điểm; người dùng không bị phạt vì việc ngoài tầm kiểm soát của họ.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M12-02.01 | Khi một upvote bài viết được ghi nhận, hệ thống phải cộng ngay 2 điểm cho tác giả bài viết (BR-M12-05, BR-M12-07). |
| FR-M12-02.02 | Khi một upvote bình luận được ghi nhận, hệ thống phải cộng ngay 1 điểm cho tác giả bình luận (BR-M12-05, BR-M12-07). |
| FR-M12-02.03 | Khi một upvote được rút lại, hệ thống phải trừ ngay khỏi điểm của tác giả đúng số điểm upvote đó đã cộng (BR-M12-07). |
| FR-M12-02.04 | Hệ thống phải giữ trong điểm của người nhận các upvote do tài khoản nay đã xóa trao (BR-M12-05). |
| FR-M12-02.05 | Hệ thống phải không giảm điểm theo thời gian (BR-M12-06). |
| FR-M12-02.06 | Hệ thống phải không cho AI, Mod hay Admin cộng, trừ tay điểm của người dùng (BR-M12-06). |
| FR-M12-02.07 | Hệ thống phải không cộng điểm từ nguồn nào khác ngoài upvote bài viết và upvote bình luận (BR-M12-06). |
| FR-M12-02.08 | Khi bài viết do tác giả tự xóa chuyển sang Đã xóa hẳn (M03), hệ thống phải trừ khỏi điểm của tác giả phần điểm từ các upvote đang có hiệu lực trên bài và ghi số điểm đã trừ (BR-M12-08, BR-M12-09). |
| FR-M12-02.09 | Nếu bài viết do tác giả tự xóa được khôi phục trước khi chuyển sang Đã xóa hẳn, hệ thống phải không trừ điểm của bài (BR-M12-09). |
| FR-M12-02.10 | Khi Mod hoặc Admin hệ thống gỡ một bài viết vì vi phạm (bài sang Bị ẩn), hệ thống phải trừ ngay khỏi điểm của tác giả phần điểm từ các upvote đang có hiệu lực trên bài và ghi số điểm đã trừ (BR-M12-08, BR-M12-09). |
| FR-M12-02.11 | Khi Mod hoặc Admin hệ thống ẩn một bình luận vì vi phạm, hệ thống phải trừ ngay khỏi điểm của tác giả phần điểm từ các upvote đang có hiệu lực trên bình luận (BR-M12-08, BR-M12-09). |
| FR-M12-02.12 | Khi khiếu nại bài bị gỡ được chấp nhận (M09), hệ thống phải cộng lại cho tác giả số điểm đã trừ vì lần gỡ đó (BR-M12-10). |
| FR-M12-02.13 | Hệ thống phải không hoàn điểm đã trừ của bình luận bị gỡ (BR-M12-10). |
| FR-M12-02.14 | Khi nhóm bị Owner xóa, hệ thống phải giữ nguyên điểm của thành viên từ bài viết, bình luận trong nhóm (BR-M12-08). |
| FR-M12-02.15 | Khi một người rời hoặc bị kick khỏi nhóm, hệ thống phải giữ nguyên điểm của người đó từ bài viết, bình luận trong nhóm (BR-M12-08). |
| FR-M12-02.16 | Khi Owner hoặc Group Mod gỡ một bài viết hoặc bình luận khỏi nhóm, hệ thống phải không trừ điểm của tác giả (BR-M12-08). |
| FR-M12-02.17 | Khi một bình luận bị ẩn theo bài cha bị gỡ hoặc bị xóa, hệ thống phải không trừ điểm của tác giả bình luận (BR-M12-08). |
| FR-M12-02.18 | Nếu điểm của một nội dung đã bị trừ, hệ thống phải không cộng vào điểm các upvote trên nội dung đó và không trừ lại lần nữa khi nội dung tiếp tục bị xóa hoặc gỡ (BR-M12-05). |
| FR-M12-02.19 | Khi tác giả tự xóa một bình luận, hệ thống phải trừ ngay khỏi điểm của tác giả phần điểm từ các upvote đang có hiệu lực trên bình luận (BR-M12-08, BR-M12-09). |
| FR-M12-02.20 | Khi AI tự ẩn một bình luận với điểm quét từ 0,9 trở lên, hệ thống phải trừ ngay khỏi điểm của tác giả phần điểm từ các upvote đang có hiệu lực trên bình luận (BR-M12-08, BR-M12-09). |
| FR-M12-02.21 | Khi Mod hoặc Admin kết luận một bình luận bị AI ẩn với điểm quét từ 0,5 đến dưới 0,9 là vi phạm, hệ thống phải trừ khỏi điểm của tác giả phần điểm từ các upvote đang có hiệu lực trên bình luận tại lúc kết luận (BR-M12-09). |
| FR-M12-02.22 | Nếu Mod hoặc Admin kết luận một bình luận bị AI ẩn với điểm quét từ 0,5 đến dưới 0,9 là không vi phạm, hệ thống phải không trừ điểm của bình luận đó (BR-M12-09). |

### 5.3 FR-M12-03 Trao huy hiệu theo mốc điểm

**Yêu cầu cấp trên:** Hệ thống phải tự động trao huy hiệu khi tổng điểm của người dùng chạm mốc và giữ huy hiệu đó vĩnh viễn.

**Lý do:** Huy hiệu là cột mốc đã đạt được, không phải chỉ số theo dõi liên tục. Giữ vĩnh viễn để không phạt người dùng vì những thay đổi điểm ngoài tầm kiểm soát và tránh phải kiểm tra, thu hồi lại. Ghi ngày đạt thay vì ngưỡng để không gây hiểu lầm khi điểm hiện tại thấp hơn ngưỡng.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M12-03.01 | Hệ thống phải có đúng 5 huy hiệu với ngưỡng tổng điểm: Người mới nổi 25, Cây bút triển vọng 100, Cây bút tích cực 300, Chuyên gia cộng đồng 600, Huyền thoại iShare 1000 (BR-M12-11). |
| FR-M12-03.02 | Khi tổng điểm của người dùng lớn hơn hoặc bằng ngưỡng của một huy hiệu người đó chưa có, hệ thống phải trao huy hiệu đó và ghi ngày đạt (BR-M12-11, BR-M12-12). |
| FR-M12-03.03 | Khi tổng điểm vượt nhiều ngưỡng cùng lúc, hệ thống phải trao mọi huy hiệu có ngưỡng đã vượt mà người dùng chưa có (BR-M12-11). |
| FR-M12-03.04 | Hệ thống phải không thu hồi huy hiệu đã trao, kể cả khi điểm sau đó giảm dưới ngưỡng (BR-M12-12). |
| FR-M12-03.05 | Nếu người dùng đã có một huy hiệu, hệ thống phải không trao lại huy hiệu đó khi điểm chạm ngưỡng lần nữa và giữ ngày đạt đầu tiên (BR-M12-12). |
| FR-M12-03.06 | Hệ thống phải cung cấp cho nơi hiển thị (M02) các huy hiệu người dùng đã đạt kèm ngày đạt, không kèm ngưỡng điểm (BR-M12-12). |
| FR-M12-03.07 | Hệ thống phải không cung cấp huy hiệu chưa đạt hay tiến độ tới huy hiệu chưa đạt (BR-M12-13). |
| FR-M12-03.08 | Hệ thống phải không có huy hiệu theo số bài đăng hay theo chủ đề (BR-M12-11). |
| FR-M12-03.09 | Hệ thống phải không cho Mod hay Admin trao, thu hồi tay huy hiệu hoặc danh hiệu (BR-M12-06). |
| FR-M12-03.10 | Khi trao một huy hiệu, hệ thống phải gửi sự kiện đạt huy hiệu cho M07 để thông báo trong ứng dụng; đây cũng là sự kiện "mốc điểm" (BR-M12-26). |
| FR-M12-03.11 | Nếu tài khoản đã bị xóa (DELETED), hệ thống phải không hiển thị huy hiệu của tài khoản đó (BR-M12-21). |
| FR-M12-03.12 | Hệ thống phải không gửi thông báo mốc điểm riêng ngoài thông báo đạt huy hiệu (BR-M12-26). |

### 5.4 FR-M12-04 Tính bảng xếp hạng định kỳ

**Yêu cầu cấp trên:** Hệ thống phải tính lại thứ hạng người dùng của ba chu kỳ tuần, tháng, toàn thời gian mỗi 60 phút.

**Lý do:** Gom việc tính bảng xếp hạng và chốt chu kỳ vào một lần chạy định kỳ thay vì tính theo từng upvote, để chỉ có một cơ chế; xếp hạng có đồng hạng phức tạp hơn thống kê thông thường nên được tính theo lô. Bảng theo tuần, tháng giữ cho bảng xếp hạng luôn mới mà không cần giảm điểm theo thời gian.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M12-04.01 | Hệ thống phải tính lại bảng toàn thời gian mỗi 60 phút (BR-M12-19). |
| FR-M12-04.02 | Hệ thống phải xếp người dùng theo điểm trong chu kỳ, từ cao xuống thấp, chỉ xét người có điểm trong chu kỳ lớn hơn 0 (BR-M12-15, BR-M12-18). |
| FR-M12-04.03 | Hệ thống phải xác định chu kỳ tuần từ 00:00 thứ Hai đến trước 00:00 thứ Hai tuần sau và chu kỳ tháng từ 00:00 ngày mùng 1 đến trước 00:00 ngày mùng 1 tháng sau, theo giờ Việt Nam (UTC+7) (BR-M12-14). |
| FR-M12-04.04 | Hệ thống phải dùng tổng điểm làm điểm của chu kỳ toàn thời gian (BR-M12-15). |
| FR-M12-04.05 | Hệ thống phải không có chu kỳ năm (BR-M12-14). |
| FR-M12-04.06 | Hệ thống phải cho những người cùng điểm trong chu kỳ cùng một thứ hạng, và cho người kế tiếp thứ hạng bằng số người đứng trên cộng một (BR-M12-18). |
| FR-M12-04.07 | Trong khi người dùng ở mức cảnh cáo HEAVY, hệ thống phải loại người đó khỏi bảng xếp hạng (BR-M12-20). |
| FR-M12-04.08 | Trong khi tài khoản ở trạng thái BANNED, hệ thống phải loại tài khoản đó khỏi bảng xếp hạng (BR-M12-20). |
| FR-M12-04.09 | Hệ thống phải không loại người dùng ở mức cảnh cáo LIGHT hoặc MEDIUM khỏi bảng xếp hạng (BR-M12-20). |
| FR-M12-04.10 | Khi người dùng không còn ở mức HEAVY, tài khoản không còn BANNED hoặc DEACTIVATED, hệ thống phải đưa người đó trở lại bảng toàn thời gian từ lần tính kế tiếp và hiện lại dòng của người đó trên bảng tuần, tháng đã chốt (BR-M12-20). |
| FR-M12-04.11 | Khi một tài khoản chuyển sang DELETED, hệ thống phải tiếp tục hiện tài khoản đó trên bảng tuần, tháng đã chốt đang hiển thị ở dạng hiện mờ kèm nhãn "[Người dùng đã xóa]" (BR-M12-21). |
| FR-M12-04.12 | Hệ thống phải không đưa tài khoản DELETED vào bảng của các lần chốt sau và loại tài khoản đó khỏi bảng toàn thời gian từ lần tính kế tiếp (BR-M12-21). |
| FR-M12-04.13 | Hệ thống phải chỉ có một bảng xếp hạng toàn hệ thống cho mỗi chu kỳ, không có bảng theo nhóm hay bảng riêng cho giáo viên (BR-M12-17). |
| FR-M12-04.14 | Hệ thống phải chỉ giữ bảng đã chốt của tuần vừa kết thúc, bảng đã chốt của tháng vừa kết thúc và kết quả lần tính gần nhất của bảng toàn thời gian; không lưu bảng của các chu kỳ cũ hơn (BR-M12-22). |
| FR-M12-04.15 | Hệ thống phải tính điểm trong chu kỳ chỉ từ các upvote có thời điểm upvote trong chu kỳ, còn hiệu lực lúc tính và nằm trên nội dung chưa bị trừ điểm lúc tính (BR-M12-15). |
| FR-M12-04.16 | Khi một upvote bị rút hoặc một nội dung bị trừ điểm, hệ thống phải không trừ vào điểm trong chu kỳ của chu kỳ khác với chu kỳ của upvote đó và không đổi bảng đã chốt (BR-M12-15). |
| FR-M12-04.17 | Trong khi tài khoản ở trạng thái DEACTIVATED, hệ thống phải loại tài khoản đó khỏi bảng xếp hạng (BR-M12-20). |
| FR-M12-04.18 | Nếu một người trên bảng tuần, tháng đã chốt trở thành HEAVY, BANNED hoặc DEACTIVATED sau lúc chốt, hệ thống phải ẩn dòng của người đó khi hiển thị và giữ nguyên thứ hạng đã chốt của những người khác (BR-M12-20). |
| FR-M12-04.19 | Hệ thống phải tiếp tục tính điểm cho người đang bị loại khỏi bảng xếp hạng, để khi trở lại người đó có đủ điểm trong chu kỳ (BR-M12-20). |

### 5.5 FR-M12-05 Chốt chu kỳ và trao danh hiệu "Ngôi sao tuần"

**Yêu cầu cấp trên:** Hệ thống phải chốt bảng xếp hạng của mỗi tuần, tháng vừa kết thúc bằng số liệu đúng mốc và trao danh hiệu "Ngôi sao tuần" cho những người đứng đầu tuần.

**Lý do:** Danh hiệu dành cho một nhóm người đứng đầu, không chỉ một người. Số người nhận là số tối thiểu: người đồng hạng ở hạng cắt đều nhận, không cần luật phân xử thêm. Chốt bằng số liệu đúng mốc để người thắng luôn đúng, chấp nhận thông báo trễ tối đa 60 phút.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M12-05.01 | Khi lần tính định kỳ thấy một tuần hoặc một tháng đã kết thúc từ lần tính trước, hệ thống phải tính bảng cuối cùng của chu kỳ đó bằng số liệu đúng mốc đầu, cuối chu kỳ, không dùng kết quả đang hiển thị (BR-M12-23, BR-M12-25). |
| FR-M12-05.02 | Khi chốt một tuần, hệ thống phải trao danh hiệu "Ngôi sao tuần" cho mọi người có điểm tuần lớn hơn 0 và thứ hạng từ 1 đến 3 trong bảng cuối cùng của tuần, kể cả mọi người đồng hạng ở hạng 3 (BR-M12-23). |
| FR-M12-05.03 | Hệ thống phải ghi mỗi lần trao danh hiệu thành một bản ghi riêng gồm người nhận và tuần đạt (BR-M12-24). |
| FR-M12-05.04 | Nếu người dùng đã đạt danh hiệu ở tuần trước, hệ thống phải vẫn trao danh hiệu ở tuần mới mà người đó đạt (BR-M12-24). |
| FR-M12-05.05 | Hệ thống phải không trao danh hiệu cho chu kỳ tháng và chu kỳ toàn thời gian (BR-M12-24). |
| FR-M12-05.06 | Hệ thống phải chốt tuần và trao danh hiệu không muộn hơn 60 phút sau khi tuần kết thúc (BR-M12-25). |
| FR-M12-05.07 | Khi trao danh hiệu, hệ thống phải gửi sự kiện đạt danh hiệu tuần cho M07 để thông báo trong ứng dụng (BR-M12-26). |
| FR-M12-05.08 | Khi chốt một tuần hoặc một tháng, hệ thống phải hiển thị bảng cuối cùng đó ở tab Tuần hoặc Tháng cho tới lần chốt sau của cùng loại chu kỳ (BR-M12-22). |
| FR-M12-05.09 | Nếu số người có điểm tuần lớn hơn 0 ít hơn 3, hệ thống phải chỉ trao danh hiệu cho những người đó, và không trao cho ai khi tuần không có người nào có điểm (BR-M12-23). |
| FR-M12-05.10 | Nếu người dùng đang ở mức HEAVY hoặc tài khoản đang BANNED tại lúc chốt tuần, hệ thống phải không xếp hạng và không trao danh hiệu cho người đó, và không để người đó chiếm suất trong 3 hạng đầu (BR-M12-23). |
| FR-M12-05.11 | Khi chốt một tháng, hệ thống phải chỉ chốt bảng tháng, không trao gì và không gửi thông báo (BR-M12-24). |
| FR-M12-05.12 | Hệ thống phải cung cấp cho hồ sơ (M02) danh hiệu "Ngôi sao tuần" chỉ khi người dùng đạt danh hiệu ở tuần vừa chốt, từ lúc chốt tới lần chốt tuần sau, không kèm số lần đạt hay danh sách tuần đạt (BR-M12-24). |
| FR-M12-05.13 | Hệ thống phải không hiển thị lịch sử các lần đạt "Ngôi sao tuần" ở bất kỳ đâu, dù vẫn lưu bản ghi của mỗi lần đạt (BR-M12-24). |

### 5.6 FR-M12-06 Xem bảng xếp hạng

**Yêu cầu cấp trên:** Hệ thống phải cho mọi người, kể cả người chưa đăng nhập, xem bảng xếp hạng của từng chu kỳ và lọc theo Lớp/Khối.

**Lý do:** Bảng xếp hạng là chức năng chính của module; tôn vinh rõ ràng người đóng góp để thúc đẩy tinh thần học hỏi từ bạn bè. Người chưa đăng nhập cũng xem được bảng xếp hạng, huy hiệu và điểm của người dùng.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M12-06.01 | Hệ thống phải cho Guest và người dùng đã đăng nhập xem bảng xếp hạng. |
| FR-M12-06.02 | Hệ thống phải cho người xem chọn một trong ba tab: Tuần (tuần vừa kết thúc), Tháng (tháng vừa kết thúc), Toàn thời gian (BR-M12-14, BR-M12-22). |
| FR-M12-06.03 | Hệ thống phải cho người xem lọc bảng xếp hạng theo Lớp/Khối 10, 11, 12 hoặc Tất cả, trong đó Tất cả gồm cả người chưa đặt Lớp/Khối (BR-M12-16). |
| FR-M12-06.04 | Hệ thống phải hiển thị ở tab Tuần, Tháng bảng đã chốt của chu kỳ vừa kết thúc, không hiển thị bảng của tuần, tháng đang diễn ra (BR-M12-22). |
| FR-M12-06.05 | Hệ thống phải hiển thị cùng một thứ hạng cho những người đồng hạng (BR-M12-18). |
| FR-M12-06.06 | Hệ thống phải không cho xem bảng xếp hạng của các chu kỳ cũ hơn chu kỳ vừa chốt (BR-M12-22). |
| FR-M12-06.07 | Hệ thống phải hiển thị ở tab Toàn thời gian kết quả của lần tính định kỳ gần nhất (BR-M12-19). |
| FR-M12-06.08 | Khi lọc theo Lớp/Khối, hệ thống phải đánh lại thứ hạng trong nhóm lọc theo cùng quy tắc đồng hạng (BR-M12-16). |
| FR-M12-06.09 | Hệ thống phải xét Lớp/Khối của mỗi người tại lúc chốt bảng, với tab Toàn thời gian tại lần tính gần nhất (BR-M12-16). |
| FR-M12-06.10 | Hệ thống phải hiển thị những người đồng hạng theo username từ A đến Z (BR-M12-18). |
| FR-M12-06.11 | Hệ thống phải hiển thị ở mỗi dòng: thứ hạng, avatar, tên hiển thị kèm username, điểm trong chu kỳ, dấu "Ngôi sao tuần" ở tab Tuần với người nhận danh hiệu, và nhãn "[Người dùng đã xóa]" với tài khoản đã xóa (BR-M12-29). |
| FR-M12-06.12 | Khi người xem bấm vào tên hoặc avatar trên một dòng, hệ thống phải mở hồ sơ của người đó (BR-M12-29). |
| FR-M12-06.13 | Hệ thống phải hiển thị mọi người có điểm trong chu kỳ lớn hơn 0, tải 20 dòng mỗi lần cuộn (BR-M12-29). |

### 5.7 FR-M12-07 Gắn nhãn "Tài khoản đã bị khóa"

**Yêu cầu cấp trên:** Hệ thống phải gắn nhãn công khai "Tài khoản đã bị khóa" cạnh tên của tài khoản đang bị ban ở mọi nơi tên đó xuất hiện.

**Lý do:** Ban là mức phạt nặng hơn cảnh cáo và mang tính công khai, minh bạch, khác với trạng thái cảnh cáo được giữ riêng tư. Ban có thể được gỡ qua khiếu nại và khác với xóa tài khoản, nên hồ sơ, bài viết, bình luận vẫn hiển thị bình thường; nội dung vi phạm cụ thể được xử lý riêng ở kiểm duyệt.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M12-07.01 | Trong khi tài khoản ở trạng thái BANNED, hệ thống phải hiển thị nhãn "Tài khoản đã bị khóa" cạnh tên tài khoản ở mọi nơi tên đó xuất hiện, gồm trang hồ sơ, tên tác giả trên bài viết, bình luận, kể cả trong Trending (BR-M12-27). |
| FR-M12-07.02 | Trong khi tài khoản ở trạng thái BANNED, hệ thống phải tiếp tục hiển thị hồ sơ, bài viết, bình luận của tài khoản như bình thường (BR-M12-27). |
| FR-M12-07.03 | Khi tài khoản không còn BANNED, hệ thống phải bỏ nhãn "Tài khoản đã bị khóa" (BR-M12-27). |
| FR-M12-07.04 | Hệ thống phải dùng nhãn "Tài khoản đã bị khóa" riêng, khác nhãn "Tài khoản tạm thời vô hiệu hoá" của tài khoản DEACTIVATED (BR-M12-27). |

### 5.8 FR-M12-08 Chặn thao tác Gamification khi cờ tắt

**Yêu cầu cấp trên:** Hệ thống phải từ chối thao tác của người dùng không phải Admin với module trong lúc cờ tính năng Gamification tắt, trong khi việc hệ thống tự chạy vẫn tiếp tục.

**Lý do:** Khi tắt, một số việc vẫn nên chạy ngầm; chỉ từ chối yêu cầu của người dùng và hiện thông báo hệ thống đang bận khi truy cập module.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M12-08.01 | Trong khi cờ Gamification tắt, nếu người dùng không phải Admin gửi yêu cầu tới module, hệ thống phải từ chối và hiển thị "Hệ thống đang bận, vui lòng thử lại sau" (BR-M12-28). |
| FR-M12-08.02 | Trong khi cờ Gamification tắt, hệ thống phải vẫn hiển thị lối vào của module (BR-M12-28). |
| FR-M12-08.03 | Trong khi cờ Gamification tắt, hệ thống phải tiếp tục tính điểm và bảng xếp hạng (BR-M12-28). |
| FR-M12-08.04 | Trong khi cờ Gamification tắt, hệ thống phải giữ nguyên dữ liệu của module (BR-M12-28). |
| FR-M12-08.05 | Khi cờ Gamification được bật lại, hệ thống phải không bù lại những yêu cầu đã bị từ chối trong lúc tắt (BR-M12-28). |
| FR-M12-08.06 | Trong khi cờ Gamification tắt, hệ thống phải cho Admin dùng module như khi cờ bật (BR-M12-28). |
| FR-M12-08.07 | Hệ thống phải khởi tạo cờ Gamification ở trạng thái Bật (BR-M12-28). |
| FR-M12-08.08 | Trong khi cờ Gamification tắt, nếu người dùng không phải Admin upvote, rút upvote hoặc mở bảng xếp hạng, hệ thống phải từ chối, và vẫn hiển thị nút upvote và lối vào bảng xếp hạng (BR-M12-28). |
| FR-M12-08.09 | Trong khi cờ Gamification tắt, hệ thống phải tiếp tục trừ, hoàn điểm theo nội dung, trao huy hiệu, tính bảng toàn thời gian, chốt tuần, tháng, trao danh hiệu tuần và gửi thông báo huy hiệu, danh hiệu (BR-M12-28). |
| FR-M12-08.10 | Trong khi cờ Gamification tắt, hệ thống phải tiếp tục hiển thị số upvote trên bài viết, bình luận, điểm, huy hiệu, danh hiệu trên hồ sơ và nhãn "Tài khoản đã bị khóa" (BR-M12-28). |

### 5.9 Quy tắc nghiệp vụ

| ID | Loại | Quy tắc | Ví dụ |
|---|---|---|---|
| BR-M12-01 | Sự kiện | Phản ứng duy nhất trên bài viết và bình luận là upvote: upvote bài viết là Post Star, upvote bình luận là Comment Star. Không có downvote; nội dung không phù hợp được xử lý bằng báo cáo (M08). | — |
| BR-M12-02 | Ràng buộc | Upvote là bật/tắt: mỗi người dùng có nhiều nhất một upvote đang có hiệu lực trên mỗi bài viết hoặc bình luận; bấm lại thì rút lại, bấm tiếp thì upvote lại. | Cường bấm upvote bài X → 1 upvote của Cường trên X. Bấm lại → 0. Bấm tiếp → 1. |
| BR-M12-03 | Ràng buộc | Không ai upvote được bài viết hoặc bình luận của chính mình; nút upvote bị ẩn hoặc tắt trên nội dung của chính người xem. | An xem bài của chính An → không upvote được. Cường xem bài đó → upvote được. |
| BR-M12-04 | Ràng buộc | Chỉ người dùng đã đăng nhập upvote được. Người ở mức cảnh cáo HEAVY vẫn upvote được. Upvote bị từ chối nơi module khác chặn tương tác: bài nhóm Private với người ngoài nhóm (M11). Bài ở mức Khóa toàn bộ (M03) chặn mọi thao tác upvote: upvote mới và rút lại upvote, trên bài và trên mọi bình luận của bài. | Guest bấm upvote → bị từ chối. Cường đang ở HEAVY upvote bài X → được. Bài X bị Mod đặt Khóa toàn bộ → upvote X, upvote bình luận trong X, rút upvote cũ trên X đều bị từ chối. |
| BR-M12-05 | Tính toán | Điểm của một người = 2 × số upvote đang có hiệu lực trên các bài viết của người đó + 1 × số upvote đang có hiệu lực trên các bình luận của người đó, chỉ tính trên nội dung chưa bị trừ điểm (BR-M12-08). Upvote của tài khoản đã xóa vẫn được tính. | An có bài X 3 upvote, bài Y 1 upvote, bình luận Z 4 upvote → 2 × (3 + 1) + 1 × 4 = 12 điểm. Một trong 3 upvote của X là của tài khoản đã xóa → vẫn 12. |
| BR-M12-06 | Sự kiện | Upvote là nguồn điểm duy nhất; không có Accepted Answer. Điểm không giảm theo thời gian. Điểm chỉ thay đổi theo các quy tắc của module: AI, Mod, Admin không cộng, trừ tay điểm, không trao hay thu hồi tay huy hiệu, danh hiệu; trọng số, mốc huy hiệu là hằng số, chỉ đổi bằng triển khai. | — |
| BR-M12-07 | Kích hoạt | Khi một upvote được thêm, điểm của tác giả nội dung tăng ngay (2 với bài viết, 1 với bình luận); khi upvote bị rút lại, điểm giảm ngay đúng phần đó. Điểm của từng người cập nhật tức thời, không chờ lần tính bảng xếp hạng. | An 12 điểm. 10:00 Cường upvote bình luận Z → 13. 10:01 Cường rút lại → 12. 10:02 Dũng upvote bài X → 14. |
| BR-M12-08 | Suy diễn | Điểm từ upvote của một nội dung bị trừ khi nội dung mất đi do trực tiếp: tác giả tự xóa; Mod hoặc Admin hệ thống gỡ vì vi phạm của chính nội dung đó (bài sang Bị ẩn, bình luận bị Ẩn); AI tự ẩn bình luận với điểm quét từ 0,9; bình luận bị AI ẩn với điểm quét 0,5–< 0,9 được Mod, Admin kết luận vi phạm. Điểm được giữ khi nội dung mất đi gián tiếp: nhóm bị Owner xóa; tác giả rời hoặc bị kick khỏi nhóm; Owner, Group Mod gỡ khỏi nhóm; bình luận bị ẩn theo bài cha bị gỡ hoặc bị xóa vì bất kỳ lý do gì. | Bài X của An (3 upvote, 6 điểm) bị Mod ẩn vì vi phạm → An 14 → 8. Bình luận của An trong bài W của Bình (2 upvote) → W bị Mod ẩn → An giữ 2 điểm đó. Nhóm có bài của An (5 upvote) bị Owner xóa → An giữ 10 điểm đó. |
| BR-M12-09 | Kích hoạt | Thời điểm trừ: bài do tác giả tự xóa bị trừ lúc bài chuyển sang Đã xóa hẳn (M03); bài được khôi phục trước đó thì không bao giờ bị trừ. Bình luận do tác giả tự xóa bị trừ ngay lúc xóa. Nội dung bị Mod, Admin gỡ vì vi phạm, bình luận bị AI ẩn với điểm từ 0,9 bị trừ ngay; bình luận bị AI ẩn với điểm 0,5–< 0,9 bị trừ lúc Mod, Admin kết luận vi phạm, không bị trừ nếu kết luận không vi phạm. Phần trừ là điểm từ các upvote đang có hiệu lực trên nội dung ở thời điểm trừ. | An xóa bài Y (1 upvote) lúc 10:00 01/10 → 2 điểm vẫn tính tới khi Y chuyển Đã xóa hẳn (10:00 08/10) thì bị trừ; An khôi phục Y lúc 05/10 → không trừ. An xóa bình luận Z (4 upvote) lúc 10:00 → trừ 4 lúc 10:00. Bình luận V (3 upvote) bị AI chấm 0,93 lúc 10:00 → trừ 3 lúc 10:00; chấm 0,7, Mod kết luận vi phạm lúc 15:00 → trừ 3 lúc 15:00; Mod kết luận không vi phạm → không trừ. |
| BR-M12-10 | Kích hoạt | Khi khiếu nại bài bị gỡ được chấp nhận (M09), điểm đã trừ vì lần gỡ đó được hoàn lại. Bình luận bị gỡ không có khiếu nại; điểm đã trừ của bình luận không được hoàn. | Bài X bị gỡ, An bị trừ 6 điểm; khiếu nại X được chấp nhận → An được cộng lại 6. Bình luận Z bị Mod ẩn, An bị trừ 4 → giữ nguyên mức trừ. |
| BR-M12-11 | Ràng buộc | Có 5 huy hiệu, chỉ dựa trên tổng điểm: Người mới nổi (25), Cây bút triển vọng (100), Cây bút tích cực (300), Chuyên gia cộng đồng (600), Huyền thoại iShare (1000). Khi tổng điểm lớn hơn hoặc bằng ngưỡng của một huy hiệu người đó chưa có, người đó đạt huy hiệu ấy; vượt nhiều ngưỡng cùng lúc thì đạt tất cả. Không có huy hiệu theo số bài hay theo chủ đề. | 24 → nhận 1 Comment Star → 25: đạt Người mới nổi. 99 → nhận 1 Post Star → 101: đạt Cây bút triển vọng. 90 → được hoàn 220 → 310: đạt cả Cây bút triển vọng và Cây bút tích cực. 299 → 299: chưa đạt Cây bút tích cực. |
| BR-M12-12 | Sự kiện | Huy hiệu đã đạt là vĩnh viễn, không bị thu hồi kể cả khi điểm giảm dưới ngưỡng; mỗi huy hiệu chỉ đạt một lần, lưu ngày đạt đầu tiên. Nơi hiển thị huy hiệu ghi ngày đạt, không ghi lại ngưỡng điểm. | An đạt Người mới nổi ngày 01/10 (25 điểm). 05/10 bị trừ còn 20 → vẫn giữ. 10/10 lên lại 25 → không đạt lại, ngày đạt vẫn 01/10. |
| BR-M12-13 | Ràng buộc | Chỉ huy hiệu đã đạt được hiển thị; không hiển thị huy hiệu chưa đạt hay tiến độ tới nó. | An 150 điểm → hiện Người mới nổi, Cây bút triển vọng; không hiện "150/300". |
| BR-M12-14 | Ràng buộc | Bảng xếp hạng có ba chu kỳ: tuần, tháng, toàn thời gian. Tuần từ 00:00 thứ Hai đến trước 00:00 thứ Hai tuần sau; tháng từ 00:00 ngày mùng 1 đến trước 00:00 ngày mùng 1 tháng sau; tính theo giờ Việt Nam (UTC+7). | Upvote lúc 23:58 Chủ nhật 19/10 thuộc tuần 13/10–19/10; lúc 00:05 thứ Hai 20/10 thuộc tuần 20/10–26/10. Upvote lúc 23:59 31/10 giờ Việt Nam (16:59 UTC) thuộc tháng 10. |
| BR-M12-15 | Tính toán | Điểm trong chu kỳ = điểm theo trọng số của BR-M12-05 từ các upvote có thời điểm upvote trong chu kỳ, còn hiệu lực lúc tính và nằm trên nội dung chưa bị trừ điểm lúc tính. Rút upvote hay trừ điểm nội dung chỉ làm giảm tổng điểm, không trừ vào chu kỳ đang tính khi upvote thuộc chu kỳ khác; bảng đã chốt không đổi. Điểm trong chu kỳ không bao giờ âm. Chu kỳ toàn thời gian dùng tổng điểm. | Tuần 13/10–19/10 bài X của An nhận 5 upvote → điểm tuần 10, chốt 20/10. Thứ Ba 21/10 Mod gỡ X (tổng −10); tuần 20/10–26/10 bình luận của An nhận 3 upvote, Bình rút một upvote đã cho bài Y từ tuần trước (tổng −2) → điểm tuần 20/10–26/10 của An = 3; bảng tuần 13/10–19/10 vẫn ghi An 10. |
| BR-M12-16 | Ràng buộc | Bảng xếp hạng lọc được theo Lớp/Khối: 10, 11, 12 hoặc Tất cả; Tất cả gồm cả người chưa đặt Lớp/Khối. Khi lọc, thứ hạng được đánh lại trong nhóm lọc theo cùng quy tắc đồng hạng. Lớp/Khối của mỗi người lấy tại lúc chốt (Toàn thời gian: tại lần tính gần nhất). | Bảng tuần qua: An 1 (Khối 12), Bình 2 (Khối 11), Cường 3 (Khối 11), Dũng 4 (Khối 10). Lọc Khối 11 → Bình 1, Cường 2. Thứ Tư Cường đổi hồ sơ sang Khối 12 → bảng tuần qua lọc Khối 11 vẫn có Cường. Lọc Tất cả → đủ 4 người với hạng 1–4. |
| BR-M12-17 | Sự kiện | Chỉ có một bảng xếp hạng toàn hệ thống cho mỗi chu kỳ; không có bảng xếp hạng theo nhóm, không có bảng riêng cho giáo viên. | — |
| BR-M12-18 | Tính toán | Chỉ người có điểm trong chu kỳ lớn hơn 0 được xếp hạng. Người có cùng điểm đồng hạng; người kế tiếp nhận thứ hạng bằng số người đứng trên cộng một. Những người đồng hạng hiện theo username từ A đến Z; thứ tự này không đổi thứ hạng. | Điểm 50, 40 (bao_tran), 40 (an_nguyen), 30, 0 → hạng 1, 2 (an_nguyen), 2 (bao_tran), 4; người 0 điểm không có trên bảng. |
| BR-M12-19 | Kích hoạt | Bảng toàn thời gian được tính lại mỗi 60 phút và tab Toàn thời gian hiện kết quả của lần tính gần nhất. Bảng tuần, tháng được tính một lần khi chốt (BR-M12-23, BR-M12-25). Điểm của từng người cập nhật tức thời. | An nhận upvote lúc 10:05; lần tính lúc 10:00 và 11:00 → tab Toàn thời gian phản ánh từ 11:00, hồ sơ của An đổi điểm ngay 10:05; tab Tuần vẫn là tuần đã chốt. |
| BR-M12-20 | Suy diễn | Người ở mức cảnh cáo HEAVY bị loại khỏi bảng xếp hạng trong thời gian ở mức đó; tài khoản BANNED trong thời gian bị ban; tài khoản DEACTIVATED trong thời gian vô hiệu hóa. Mức LIGHT, MEDIUM không ảnh hưởng. Trạng thái xét tại lúc tính bảng; người trở thành bị loại sau lúc chốt thì dòng của họ bị ẩn khi xem bảng đã chốt, người khác giữ thứ hạng đã chốt. Người bị loại vẫn tích điểm bình thường, khi trở lại hiện đủ điểm. Đây là ngoại lệ công khai duy nhất của trạng thái cảnh cáo, chỉ áp cho bảng xếp hạng; Trending và các nơi khác không loại. | Bảng tuần chốt 00:00 thứ Hai: An 1, Cường 2, Dũng 3. Thứ Tư Cường bị ban → bảng hiện An 1, Dũng 3. Cường được gỡ ban thứ Sáu → dòng Cường hiện lại hạng 2. |
| BR-M12-21 | Suy diễn | Tài khoản đã xóa (DELETED): trên bảng tuần, tháng đã chốt đang hiển thị, tài khoản bị xóa sau lúc chốt vẫn hiện mờ kèm nhãn "[Người dùng đã xóa]" cho tới khi bảng của lần chốt sau thay thế; bảng của các lần chốt sau không có tài khoản đó. Bảng toàn thời gian loại tài khoản đã xóa từ lần tính kế tiếp. Huy hiệu của tài khoản đã xóa không hiển thị. | Bình bị xóa tài khoản thứ Tư 22/10 → tab Tuần (tuần 13/10–19/10) vẫn có Bình mờ, nhãn "[Người dùng đã xóa]"; tab Toàn thời gian không còn Bình từ lần tính kế tiếp; bảng tuần 20/10–26/10 chốt 27/10 không có Bình. |
| BR-M12-22 | Sự kiện | Tab Tuần, Tháng hiện bảng đã chốt của tuần, tháng vừa kết thúc, không hiện tuần, tháng đang diễn ra. Không xem được bảng của các chu kỳ cũ hơn. Lịch sử chỉ còn qua huy hiệu và danh hiệu đã đạt. | Thứ Tư 22/10 mở tab Tuần → bảng tuần 13/10–19/10; không có bảng tuần 20/10–26/10 đang chạy, không có bảng tuần 06/10–12/10. |
| BR-M12-23 | Tính toán | Khi một tuần kết thúc, bảng của tuần đó được chốt bằng số liệu đúng mốc đầu, cuối tuần. Người có thứ hạng từ 1 đến 3 nhận danh hiệu "Ngôi sao tuần"; người đồng hạng ở hạng cắt đều nhận, nên số người nhận có thể nhiều hơn 3. Chỉ người có điểm tuần lớn hơn 0 được xét, nên tuần ít người có điểm có thể có ít hơn 3 người nhận, kể cả không ai. Người đang ở HEAVY hoặc BANNED lúc chốt không được xếp hạng, không nhận danh hiệu, không chiếm suất. | Điểm tuần A 30, B 25, C 20, D 20, E 18 → A, B, C, D nhận. A 30, B 25, C 25, D 25 → cả 4 nhận. Chỉ An 8, Bình 3 có điểm → 2 người nhận. Cường 45 (HEAVY lúc chốt), An 40, Dũng 30, Bình 20 → An, Dũng, Bình nhận. |
| BR-M12-24 | Ràng buộc | Chỉ chu kỳ tuần có danh hiệu. Chốt tháng chỉ chốt bảng tháng: không trao gì, không gửi thông báo. Một người có thể đạt "Ngôi sao tuần" ở nhiều tuần; mỗi lần đạt là một bản ghi riêng, nhưng lịch sử các lần đạt không hiển thị ở đâu. Hồ sơ chỉ hiện "Ngôi sao tuần" khi người dùng đạt ở tuần vừa chốt, từ lúc chốt tới lần chốt tuần sau, không kèm số lần đạt hay danh sách tuần; tab Tuần hiện dấu cạnh tên người nhận. Chỉ huy hiệu theo mốc điểm hiện vĩnh viễn. | An đạt ở tuần 13/10–19/10 → hồ sơ An hiện "Ngôi sao tuần" từ lúc chốt 20/10 tới lần chốt 27/10. Tuần 20/10–26/10 An không đạt → từ lần chốt 27/10 hồ sơ An không còn danh hiệu; 2 bản ghi cũ của An vẫn được lưu. |
| BR-M12-25 | Ràng buộc | Việc chốt tuần và trao danh hiệu chạy ở lần tính định kỳ đầu tiên sau khi tuần kết thúc, nên trễ tối đa 60 phút so với lúc tuần kết thúc; người nhận luôn đúng vì số liệu chốt theo mốc. | Tuần kết thúc lúc 00:00; lần tính lúc 00:40 chốt tuần và trao danh hiệu. Upvote lúc 00:10 thuộc tuần mới, không tính vào tuần vừa kết thúc. |
| BR-M12-26 | Sự kiện | Đạt huy hiệu và đạt danh hiệu tuần được thông báo trong ứng dụng (M07), không gửi email. "Mốc điểm" là đạt huy hiệu: mỗi huy hiệu một thông báo, không có thông báo mốc điểm riêng. Upvote được thông báo theo cách gộp của M07; rút upvote không đổi thông báo đã gửi. | An lên 101 điểm → một thông báo "đạt Cây bút triển vọng". |
| BR-M12-27 | Suy diễn | Trong khi tài khoản ở trạng thái BANNED, mọi nơi hiển thị tên người đó (trang hồ sơ, cạnh tên tác giả trên bài viết và bình luận, kể cả trong Trending) có nhãn công khai "Tài khoản đã bị khóa"; hồ sơ, bài viết, bình luận của người đó vẫn hiển thị bình thường. Nhãn này khác nhãn "Tài khoản tạm thời vô hiệu hoá" của tài khoản DEACTIVATED. | Bình bị ban → bình luận cũ của Bình hiện "Bình · Tài khoản đã bị khóa". Bình được gỡ ban → nhãn không còn. |
| BR-M12-28 | Suy diễn | Trong khi cờ tính năng Gamification tắt: upvote, rút upvote và mở bảng xếp hạng của người dùng không phải Admin bị từ chối với thông báo "Hệ thống đang bận, vui lòng thử lại sau"; nút upvote và lối vào bảng xếp hạng vẫn hiện. Vẫn chạy: trừ, hoàn điểm theo nội dung, trao huy hiệu, tính bảng toàn thời gian, chốt tuần, tháng, trao danh hiệu tuần, thông báo huy hiệu, danh hiệu. Vẫn hiển thị: số upvote trên bài viết, bình luận; điểm, huy hiệu, danh hiệu trên hồ sơ; nhãn "Tài khoản đã bị khóa". Dữ liệu giữ nguyên; bật lại không bù gì; Admin dùng module như bình thường. Cờ khởi tạo ở trạng thái Bật. | Cờ tắt: An bấm upvote → báo bận; Mod gỡ bài của Bình → Bình vẫn bị trừ điểm ngay; 00:00 thứ Hai tuần vẫn được chốt, danh hiệu vẫn trao. |
| BR-M12-29 | Ràng buộc | Mỗi dòng của bảng xếp hạng hiện: thứ hạng, avatar, tên hiển thị kèm username (bấm vào mở hồ sơ), điểm trong chu kỳ, dấu "Ngôi sao tuần" (chỉ tab Tuần), nhãn "[Người dùng đã xóa]" khi có. Bảng hiện mọi người có điểm trong chu kỳ lớn hơn 0, tải 20 dòng mỗi lần cuộn. | Dòng ở tab Tuần: "2 · [avatar] Nguyễn An (@an_nguyen) · ★ Ngôi sao tuần · 18 điểm". Bảng có 45 người → lần đầu hiện 20, cuộn hiện thêm 20, rồi 5. |

### 5.10 Dữ liệu nghiệp vụ

| Thực thể | Thuộc tính nguồn đã nêu | Quan hệ |
|---|---|---|
| Upvote | Người upvote (không còn ghi nhận khi tài khoản người upvote đã xóa); nội dung được upvote (bài viết hoặc bình luận); thời điểm upvote | Một người dùng có nhiều nhất một upvote đang có hiệu lực trên một bài viết hoặc bình luận |
| Điểm của người dùng | Tổng điểm | Mỗi người dùng một tổng điểm; tính từ upvote trên nội dung của người đó |
| Điểm đã trừ của nội dung | Nội dung (bài viết hoặc bình luận); số điểm đã trừ | Gắn với một nội dung; dùng để hoàn điểm khi khiếu nại bài được chấp nhận |
| Huy hiệu | Tên; ngưỡng điểm | Danh mục cố định 5 huy hiệu |
| Huy hiệu đã đạt | Người dùng; huy hiệu; ngày đạt | Một người dùng đạt mỗi huy hiệu nhiều nhất một lần |
| Danh hiệu đã đạt | Người dùng; danh hiệu "Ngôi sao tuần"; tuần đạt | Một người dùng có nhiều bản ghi, mỗi tuần đạt một bản ghi |
| Kết quả bảng xếp hạng | Chu kỳ (tuần vừa chốt, tháng vừa chốt, toàn thời gian); thời điểm tính; mỗi người: điểm trong chu kỳ, thứ hạng, Lớp/Khối tại lúc tính, nhận danh hiệu (tab Tuần) | Mỗi loại chu kỳ một kết quả hiện hành: tuần, tháng thay ở lần chốt sau; toàn thời gian thay ở mỗi lần tính |
| Người dùng (M01, M02, M08) — phần M12 dùng | Lớp/Khối (M02); trạng thái tài khoản ACTIVE, DEACTIVATED, BANNED, DELETED (M01, M08); mức cảnh cáo (M08) | Lọc và loại khỏi bảng xếp hạng; nhãn "Tài khoản đã bị khóa" |

**Ma trận CRUD:**

| Thực thể | Tạo | Đọc | Sửa | Xóa |
|---|---|---|---|---|
| Upvote | FR-M12-01.01 | FR-M12-02.01, FR-M12-02.02, FR-M12-04.02, FR-M12-05.01; M04, M05, M06, M07, M14 | Không có (BR-M12-02: chỉ có upvote và rút lại) | FR-M12-01.02 (rút lại) |
| Điểm của người dùng | FR-M12-02.01, FR-M12-02.02 | FR-M12-03.02, FR-M12-04.04; M02 | FR-M12-02.03, FR-M12-02.08, FR-M12-02.10, FR-M12-02.11, FR-M12-02.12, FR-M12-02.19, FR-M12-02.20, FR-M12-02.21 | Không có (BR-M12-06: không giảm theo thời gian; tài khoản đã xóa vẫn còn bản ghi, M01) |
| Điểm đã trừ của nội dung | FR-M12-02.08, FR-M12-02.10 | FR-M12-02.12 | FR-M12-02.12 (hoàn điểm) | Không có (BR-M12-10) |
| Huy hiệu | Không có (BR-M12-06, BR-M12-11: danh mục cố định, đổi bằng triển khai) | FR-M12-03.01, FR-M12-03.02 | Không có (BR-M12-06) | Không có (BR-M12-06) |
| Huy hiệu đã đạt | FR-M12-03.02, FR-M12-03.03 | FR-M12-03.06; M02 | Không có (BR-M12-12) | Không có (BR-M12-12: không thu hồi) |
| Danh hiệu đã đạt | FR-M12-05.02, FR-M12-05.03 | FR-M12-05.12 (chỉ tuần vừa chốt), FR-M12-06.11; M02 | Không có (BR-M12-24) | Không có (BR-M12-24: lưu mỗi lần đạt, không hiển thị lịch sử) |
| Kết quả bảng xếp hạng | FR-M12-04.01, FR-M12-05.01 | FR-M12-06.04, FR-M12-06.07 | FR-M12-04.01, FR-M12-05.08 | Không có (FR-M12-04.14: lần chốt, lần tính sau thay kết quả cũ, không lưu lịch sử) |

### 5.11 Chuyển trạng thái

#### Upvote của một người trên một nội dung

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Người dùng bấm upvote | Đã đăng nhập; không phải nội dung của mình; nội dung cho phép tương tác (BR-M12-03, BR-M12-04) | Có hiệu lực | FR-M12-01.01 |
| Có hiệu lực | Người dùng bấm lại | — | Đã rút | FR-M12-01.02 |
| Đã rút | Người dùng bấm upvote | Như dòng đầu | Có hiệu lực | FR-M12-01.01 |

#### Nội dung — tính điểm

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Bài viết được đăng hoặc bình luận được tạo (M03, M04) | — | Đang tính điểm | M03, M04 |
| Đang tính điểm | Bài do tác giả tự xóa chuyển sang Đã xóa hẳn (M03) | — | Đã trừ điểm | FR-M12-02.08 |
| Đang tính điểm | Mod, Admin gỡ vì vi phạm (M08) | — | Đã trừ điểm | FR-M12-02.10, FR-M12-02.11 |
| Đang tính điểm | Tác giả tự xóa bình luận (M04) | — | Đã trừ điểm | FR-M12-02.19 |
| Đang tính điểm | AI tự ẩn bình luận với điểm quét ≥ 0,9 (M08) | — | Đã trừ điểm | FR-M12-02.20 |
| Đang tính điểm | Mod, Admin kết luận vi phạm với bình luận bị AI ẩn (0,5–< 0,9) | — | Đã trừ điểm | FR-M12-02.21 |
| Đã trừ điểm | Khiếu nại bài bị gỡ được chấp nhận (M09) | Nội dung là bài viết, bị trừ vì bị gỡ | Đang tính điểm | FR-M12-02.12 |

Nội dung mất đi gián tiếp (BR-M12-08) ở lại Đang tính điểm. Đã trừ điểm của bình luận và của bài tự xóa là trạng thái
cuối.

#### Huy hiệu của một người dùng

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Tài khoản được tạo | — | Chưa đạt | M01 |
| Chưa đạt | Tổng điểm thay đổi | Tổng điểm ≥ ngưỡng của huy hiệu (BR-M12-11) | Đã đạt | FR-M12-03.02, FR-M12-03.03 |

Đã đạt là trạng thái cuối (BR-M12-12).

#### Người dùng trên bảng xếp hạng của một chu kỳ

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Lần tính định kỳ hoặc lần chốt | Điểm trong chu kỳ > 0; không ở HEAVY, không BANNED, không DEACTIVATED, không DELETED | Được xếp hạng | FR-M12-04.01, FR-M12-04.02 |
| Được xếp hạng | Lần tính định kỳ, lần chốt, hoặc lúc xem bảng đã chốt | Người dùng đang ở HEAVY, BANNED hoặc DEACTIVATED (BR-M12-20) | Bị loại | FR-M12-04.07, FR-M12-04.08, FR-M12-04.17, FR-M12-04.18 |
| Bị loại | Lần tính định kỳ hoặc lúc xem bảng đã chốt | Người dùng không còn ở HEAVY, BANNED, DEACTIVATED | Được xếp hạng | FR-M12-04.10 |
| Được xếp hạng | Tài khoản chuyển DELETED | Bảng tuần, tháng đã chốt đang hiển thị (BR-M12-21) | Hiện mờ | FR-M12-04.11 |
| Hiện mờ | Lần chốt sau thay bảng đang hiển thị | — | Bị loại | FR-M12-04.12 |
| Được xếp hạng | Tài khoản chuyển DELETED | Bảng toàn thời gian, lần tính kế tiếp | Bị loại | FR-M12-04.12 |

Với tài khoản DELETED, Bị loại là trạng thái cuối.

#### Chu kỳ tuần, tháng

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Tới mốc đầu chu kỳ (BR-M12-14) | — | Đang diễn ra | FR-M12-04.03 |
| Đang diễn ra | Tới mốc cuối chu kỳ | — | Đã kết thúc, chưa chốt | FR-M12-04.03 |
| Đã kết thúc, chưa chốt | Lần tính định kỳ đầu tiên sau mốc cuối (BR-M12-25) | — | Đã chốt, đang hiển thị | FR-M12-05.01, FR-M12-05.08 |
| Đã chốt, đang hiển thị | Chu kỳ kế tiếp cùng loại được chốt | — | Không còn hiển thị | FR-M12-05.08, FR-M12-04.14 |

Không còn hiển thị là trạng thái cuối (không lưu, không xem lại); chu kỳ toàn thời gian luôn Đang diễn ra.

### 5.12 Giao tiếp với module khác

| Hướng | Module | Nội dung ở mức nghiệp vụ | Yêu cầu |
|---|---|---|---|
| Dùng | M01 | Trạng thái tài khoản DELETED (upvote đã trao vẫn tính, hiện mờ trên bảng đã chốt, ẩn huy hiệu), DEACTIVATED (loại khỏi bảng xếp hạng, nhãn riêng) | FR-M12-02.04, FR-M12-04.11, FR-M12-04.12, FR-M12-04.17, FR-M12-03.11, FR-M12-07.04 |
| Cung cấp | M02 | Tổng điểm cập nhật tức thời; huy hiệu đã đạt kèm ngày đạt, không có tiến độ; danh hiệu "Ngôi sao tuần" khi đạt ở tuần vừa chốt; nhãn "Tài khoản đã bị khóa" trên hồ sơ | FR-M12-02.01, FR-M12-02.02, FR-M12-03.06, FR-M12-03.07, FR-M12-05.12, FR-M12-07.01 |
| Dùng | M02 | Lớp/Khối của người dùng để lọc bảng xếp hạng, lấy tại lúc chốt | FR-M12-06.03, FR-M12-06.09 |
| Dùng | M03 | Bài viết là đối tượng upvote; mốc Đã xóa hẳn và khôi phục bài tự xóa; Khóa toàn bộ chặn upvote, rút upvote trên bài và bình luận của bài; bài bị ẩn không hiện | FR-M12-01.10, FR-M12-01.12, FR-M12-02.08, FR-M12-02.09 |
| Cung cấp | M03, M04 | Số upvote đang có hiệu lực của bài viết, bình luận; nút upvote ẩn hoặc tắt trên nội dung của chính mình | FR-M12-01.01, FR-M12-01.06 |
| Cung cấp | M02, M03, M04, M06, M14 | Nhãn "Tài khoản đã bị khóa" cạnh tên của tài khoản BANNED ở mọi nơi tên xuất hiện (hồ sơ, tác giả bài, bình luận, kết quả tìm kiếm, Trending) | FR-M12-07.01, FR-M12-07.03 |
| Dùng | M04 | Bình luận là đối tượng upvote; tác giả xóa bình luận (trừ điểm ngay); bình luận ẩn theo bài cha | FR-M12-01.12, FR-M12-02.17, FR-M12-02.19 |
| Cung cấp | M05, M06, M14 | Upvote của bài viết kèm thời điểm, upvote đã rút không còn tính, để tính Trending, xếp hạng, sắp xếp | FR-M12-01.01, FR-M12-01.02 |
| Cung cấp | M07 | Sự kiện upvote, rút upvote, đạt huy hiệu, đạt danh hiệu tuần để gửi thông báo trong ứng dụng | FR-M12-01.13, FR-M12-03.10, FR-M12-05.07 |
| Dùng | M08 | Bài bị gỡ (Bị ẩn), bình luận bị ẩn vì vi phạm; bình luận bị AI tự ẩn (điểm quét ≥ 0,9) và kết luận của Mod với bình luận bị AI ẩn 0,5–< 0,9; mức cảnh cáo HEAVY; trạng thái BANNED | FR-M12-02.10, FR-M12-02.11, FR-M12-02.20, FR-M12-02.21, FR-M12-02.22, FR-M12-04.07, FR-M12-04.08, FR-M12-07.01 |
| Dùng | M09 | Khiếu nại bài bị gỡ được chấp nhận (hoàn điểm); ban được lật (tài khoản trở lại bảng xếp hạng, bỏ nhãn) | FR-M12-02.12, FR-M12-04.10, FR-M12-07.03 |
| Dùng | M10 | Cờ tính năng Gamification và giá trị khởi tạo; thứ bậc vai trò | FR-M12-08.01, FR-M12-08.07 |
| Dùng | M11 | Quyền vote bài nhóm của thành viên và người ngoài nhóm; xóa nhóm, rời, kick, gỡ khỏi nhóm (không trừ điểm) | FR-M12-01.11, FR-M12-02.14, FR-M12-02.15, FR-M12-02.16 |

### 5.13 AI hỗ trợ và hành vi khi tắt AI

Không áp dụng. Module không dùng AI; AI không cộng, trừ điểm hay trao huy hiệu (FR-M12-02.06). Kết quả AI tự ẩn bình luận của M08 là một sự kiện làm trừ điểm (FR-M12-02.20); khi AI tắt, không có sự kiện này và các quy tắc khác không đổi.

### 5.14 Yêu cầu HMI

Chưa có — chờ giai đoạn thiết kế.

### 5.15 Chuyển màn hình

Chưa có — chờ giai đoạn thiết kế.

## 6. Lịch sử sửa đổi

| Phiên bản | Ngày | Nội dung | Người sửa |
|---|---|---|---|
| 0.1 | 2026-10-21 | Tạo mới | Phạm Văn Đức |
| 0.2 | 2026-10-23 | Cập nhật theo câu trả lời Q-01–Q-15 (DEC-241–DEC-247): bảng Tuần, Tháng hiện chu kỳ vừa chốt; điểm chu kỳ; trừ điểm bình luận; cờ Gamification | Phạm Văn Đức |
| 1.0 | 2026-10-23 | Chốt sau 7 bước; câu trả lời ghi ở DEC-241–DEC-247; đối chiếu chéo và sửa các module liên quan | Phạm Văn Đức |
| 1.1 | 2026-10-24 | Rà soát chéo toàn bộ FR (review-cross-module.md): thuật ngữ "Gỡ vì vi phạm" dùng tên trạng thái Bị Mod ẩn (M03) thay mã HIDDEN; C.2 thêm MR-M12 → DEC-079 và DEC-256; không đổi yêu cầu. Chốt bản 1.1 | Phạm Văn Đức |

## Phụ lục A. Truy vết

| ID | Nguồn | Căn cứ | Ghi chú |
|---|---|---|---|
| FR-M12-01 | DM-4.1, DM-4.3, DEC-041, DEC-119, DEC-120, DEC-126, QA-011, GL:Post Star, GL:Comment Star, MR-M12 | Nói thẳng | — |
| FR-M12-01.01 | DEC-119, QA-038 | Suy ra | DEC-119 upvote là bật/tắt; QA-038 xếp upvote vào chu kỳ theo thời điểm ⇒ phải ghi thời điểm upvote |
| FR-M12-01.02 | DEC-119 | Nói thẳng | — |
| FR-M12-01.03 | DEC-119 | Suy ra | Upvote là bật/tắt ⇒ mỗi người nhiều nhất một upvote đang có hiệu lực trên một nội dung |
| FR-M12-01.04 | DEC-004, DM-4.1, DM-4.3, GL:Post Star, GL:Comment Star | Nói thẳng | — |
| FR-M12-01.05 | DEC-041 | Nói thẳng | — |
| FR-M12-01.06 | DEC-120 | Nói thẳng | — |
| FR-M12-01.07 | DEC-120 | Suy ra | Tự upvote không được phép ⇒ yêu cầu tự upvote gửi tới bị từ chối, không chỉ ẩn nút |
| FR-M12-01.08 | DEC-126, QA-011 | Nói thẳng | — |
| FR-M12-01.09 | DEC-079 | Nói thẳng | — |
| FR-M12-01.10 | DEC-167, DEC-033, DEC-246 | Nói thẳng | — |
| FR-M12-01.11 | DEC-108, DEC-234 | Nói thẳng | — |
| FR-M12-01.12 | DEC-184, DEC-180, DEC-161 | Suy ra | Bài đã xóa hiện "không tồn tại", bài bị ẩn và bình luận bị ẩn không hiện với ai ⇒ không có nội dung để upvote |
| FR-M12-01.13 | DEC-065, DEC-216 | Nói thẳng | — |
| FR-M12-02 | DEC-116, DEC-004, QA-040, QA-047, DEC-119, DEC-113, DEC-184, DEC-231, DEC-105, DEC-156, DEC-115, DEC-169, QA-017, DG-5, DM-11, DM-9.1, GL:Reputation, MR-M12, DEC-241  | Nói thẳng | — |
| FR-M12-02.01 | DEC-116, DEC-121, QA-040, DM-9.1, GL:Reputation | Nói thẳng | — |
| FR-M12-02.02 | DEC-116, DEC-121, QA-040 | Nói thẳng | — |
| FR-M12-02.03 | DEC-119 | Nói thẳng | — |
| FR-M12-02.04 | DEC-156 | Nói thẳng | — |
| FR-M12-02.05 | QA-047 | Nói thẳng | — |
| FR-M12-02.06 | DG-5, DM-11, DM-x03, DG-8, DEC-090 | Suy ra | DG-5, DM-11: không có cơ chế cộng, trừ ngoài rule, AI không tự cộng, trừ; DEC-090 hằng số không chỉnh qua giao diện ⇒ không có thao tác chỉnh tay |
| FR-M12-02.07 | DEC-169, QA-040, DM-x02 | Nói thẳng | — |
| FR-M12-02.08 | DEC-113, DEC-184 | Suy ra | DEC-113, DEC-184 nói thời điểm trừ; ghi số điểm đã trừ là điều kiện để hoàn đúng phần đã trừ (DEC-115) |
| FR-M12-02.09 | DEC-113 | Nói thẳng | — |
| FR-M12-02.10 | DEC-113, DEC-161, DEC-115 | Suy ra | DEC-113 trừ ngay khi bị gỡ; DEC-161 "gỡ" là Bị ẩn; ghi số điểm đã trừ để hoàn (DEC-115) |
| FR-M12-02.11 | DEC-113, DEC-180 | Nói thẳng | — |
| FR-M12-02.12 | DEC-115 | Nói thẳng | — |
| FR-M12-02.13 | DEC-115 | Nói thẳng | — |
| FR-M12-02.14 | DEC-113, DEC-105, ISS-134, QA-183 | Nói thẳng | — |
| FR-M12-02.15 | DEC-105, DEC-113, ISS-134, QA-183 | Nói thẳng | — |
| FR-M12-02.16 | DEC-231 | Nói thẳng | — |
| FR-M12-02.17 | DEC-113 | Nói thẳng | — |
| FR-M12-02.18 | DEC-113 | Suy ra | Trừ phần điểm của nội dung khi nó mất đi ⇒ mỗi nội dung chỉ bị trừ một lần và không còn đóng góp điểm cho tới khi được hoàn |
| FR-M12-02.19 | DEC-241 | Nói thẳng | — |
| FR-M12-02.20 | DEC-241 | Nói thẳng | — |
| FR-M12-02.21 | DEC-241 | Nói thẳng | — |
| FR-M12-02.22 | DEC-241 | Nói thẳng | — |
| FR-M12-03 | QA-194, QA-195, DEC-114, QA-207, QA-040, QA-017, GL:Badge, DEC-065, MR-M12, DEC-246  | Nói thẳng | — |
| FR-M12-03.01 | QA-195, QA-194, GL:Badge | Nói thẳng | — |
| FR-M12-03.02 | QA-040, QA-017, DEC-114 | Suy ra | Huy hiệu theo ngưỡng (QA-040, QA-195) ⇒ đạt khi tổng điểm ≥ ngưỡng; DEC-114 lưu ngày đạt |
| FR-M12-03.03 | QA-195 | Suy ra | Mỗi huy hiệu đạt khi tổng điểm ≥ ngưỡng của nó ⇒ vượt nhiều ngưỡng thì đạt tất cả |
| FR-M12-03.04 | DEC-114 | Nói thẳng | — |
| FR-M12-03.05 | DEC-114 | Nói thẳng | — |
| FR-M12-03.06 | DEC-114, DEC-028 | Nói thẳng | — |
| FR-M12-03.07 | QA-207 | Nói thẳng | — |
| FR-M12-03.08 | QA-194 | Nói thẳng | — |
| FR-M12-03.09 | DEC-114, DEC-090, DM-1.3, DG-5 | Suy ra | Huy hiệu chỉ theo tổng điểm, không thu hồi (DEC-114); danh mục là hằng số không chỉnh qua giao diện (DEC-090) ⇒ quyền "Manage badges" của draft hết hiệu lực |
| FR-M12-03.10 | DEC-065, QA-017, DEC-246 | Nói thẳng | — |
| FR-M12-03.11 | QA-018 | Nói thẳng | — |
| FR-M12-03.12 | DEC-246 | Nói thẳng | — |
| FR-M12-04 | DEC-121, QA-038, QA-047, DEC-123, DEC-052, DEC-145, DEC-127, MR-M12, DEC-242, DEC-243, DEC-246  | Nói thẳng | DEC-145 chỉ thay công thức Trending của DEC-052; câu "tuần của leaderboard là tuần lịch cố định" còn hiệu lực |
| FR-M12-04.01 | DEC-121, DEC-242, QA-038 | Nói thẳng | — |
| FR-M12-04.02 | QA-038, QA-047, DEC-116, DEC-243 | Suy ra | QA-047 xếp hạng theo tổng trong chu kỳ, DEC-116 trọng số ⇒ người nhiều điểm hơn đứng trên; DEC-243 chỉ xét điểm > 0 |
| FR-M12-04.03 | DEC-242, DEC-127, DEC-052, DEC-145, QA-038, DM-9.4, GL:Leaderboard | Nói thẳng | DEC-145 chỉ thay công thức Trending của DEC-052 |
| FR-M12-04.04 | QA-047 | Nói thẳng | — |
| FR-M12-04.05 | QA-038 | Suy ra | QA-038 chốt đúng ba chu kỳ tuần, tháng, toàn thời gian ⇒ chu kỳ năm của draft không còn |
| FR-M12-04.06 | DEC-123 | Nói thẳng | — |
| FR-M12-04.07 | DEC-118, DEC-079 | Nói thẳng | — |
| FR-M12-04.08 | DEC-122 | Nói thẳng | — |
| FR-M12-04.09 | DEC-118 | Nói thẳng | — |
| FR-M12-04.10 | DEC-118, DEC-122, DEC-089, DEC-242, DEC-246 | Suy ra | Bị loại "trong thời gian" ở HEAVY, bị ban, vô hiệu hóa ⇒ hết thời gian đó thì có lại; DEC-242 hiện lại dòng trên bảng đã chốt |
| FR-M12-04.11 | QA-018, DEC-246, DEC-242 | Nói thẳng | — |
| FR-M12-04.12 | QA-018, DEC-246 | Nói thẳng | — |
| FR-M12-04.13 | QA-039, DG-5, DEC-001 | Nói thẳng | — |
| FR-M12-04.14 | DEC-121, DEC-242 | Nói thẳng | — |
| FR-M12-04.15 | DEC-243 | Nói thẳng | — |
| FR-M12-04.16 | DEC-243 | Nói thẳng | — |
| FR-M12-04.17 | DEC-246 | Nói thẳng | — |
| FR-M12-04.18 | DEC-242 | Nói thẳng | — |
| FR-M12-04.19 | DEC-246 | Nói thẳng | — |
| FR-M12-05 | DEC-117, DEC-121, DEC-123, DEC-114, QA-040, QA-041, DEC-065, MR-M12, DEC-242, DEC-243, DEC-244, DEC-246, DEC-247  | Nói thẳng | — |
| FR-M12-05.01 | DEC-121 | Nói thẳng | — |
| FR-M12-05.02 | DEC-117, DEC-123, QA-040, QA-041, DEC-243 | Nói thẳng | — |
| FR-M12-05.03 | DEC-114 | Nói thẳng | — |
| FR-M12-05.04 | DEC-114 | Nói thẳng | — |
| FR-M12-05.05 | DEC-117 | Nói thẳng | — |
| FR-M12-05.06 | DEC-121 | Nói thẳng | — |
| FR-M12-05.07 | DEC-065, DEC-121 | Nói thẳng | — |
| FR-M12-05.08 | DEC-242 | Nói thẳng | — |
| FR-M12-05.09 | DEC-243 | Nói thẳng | — |
| FR-M12-05.10 | DEC-246 | Nói thẳng | — |
| FR-M12-05.11 | DEC-246 | Nói thẳng | — |
| FR-M12-05.12 | DEC-247, DEC-244 | Nói thẳng | — |
| FR-M12-05.13 | DEC-247, DEC-114 | Nói thẳng | — |
| FR-M12-06 | DM-9.4, QA-038, QA-039, DEC-118, DEC-122, DEC-123, DEC-121, QA-011, QA-018, QA-236, GL:Leaderboard, DG-5, MR-M12, DEC-242, DEC-243, DEC-246  | Nói thẳng | — |
| FR-M12-06.01 | QA-011, DM-9.4 | Nói thẳng | — |
| FR-M12-06.02 | QA-038, DEC-242 | Nói thẳng | — |
| FR-M12-06.03 | QA-038 | Nói thẳng | — |
| FR-M12-06.04 | DEC-242 | Nói thẳng | — |
| FR-M12-06.05 | DEC-123 | Nói thẳng | — |
| FR-M12-06.06 | DEC-121, DEC-242 | Nói thẳng | — |
| FR-M12-06.07 | DEC-242 | Nói thẳng | — |
| FR-M12-06.08 | DEC-243 | Nói thẳng | — |
| FR-M12-06.09 | DEC-243 | Nói thẳng | — |
| FR-M12-06.10 | DEC-246 | Nói thẳng | — |
| FR-M12-06.11 | DEC-243, DEC-244 | Nói thẳng | — |
| FR-M12-06.12 | DEC-243 | Nói thẳng | — |
| FR-M12-06.13 | DEC-243 | Nói thẳng | — |
| FR-M12-07 | DEC-122, QA-236, MR-M12 | Nói thẳng | — |
| FR-M12-07.01 | DEC-122, QA-236 | Nói thẳng | — |
| FR-M12-07.02 | DEC-122 | Nói thẳng | — |
| FR-M12-07.03 | DEC-122, DEC-089 | Suy ra | Nhãn hiện trong thời gian bị ban ⇒ gỡ ban thì nhãn không còn |
| FR-M12-07.04 | QA-205, DEC-019 | Nói thẳng | — |
| FR-M12-08 | DEC-225, DEC-092, DEC-228, DEC-245  | Nói thẳng | — |
| FR-M12-08.01 | DEC-225, DEC-092 | Nói thẳng | — |
| FR-M12-08.02 | DEC-225 | Nói thẳng | — |
| FR-M12-08.03 | DEC-225 | Nói thẳng | — |
| FR-M12-08.04 | DEC-225 | Nói thẳng | — |
| FR-M12-08.05 | DEC-225 | Nói thẳng | — |
| FR-M12-08.06 | DEC-225 | Nói thẳng | — |
| FR-M12-08.07 | DEC-228 | Nói thẳng | — |
| FR-M12-08.08 | DEC-245 | Nói thẳng | — |
| FR-M12-08.09 | DEC-245 | Nói thẳng | — |
| FR-M12-08.10 | DEC-245 | Nói thẳng | — |
| BR-M12-01 | DEC-041, DEC-004, DM-4.1, DM-4.3, GL:Post Star, GL:Comment Star | Nói thẳng | — |
| BR-M12-02 | DEC-119 | Suy ra | Upvote là bật/tắt ⇒ mỗi người nhiều nhất một upvote đang có hiệu lực trên một nội dung |
| BR-M12-03 | DEC-120 | Nói thẳng | — |
| BR-M12-04 | DEC-126, QA-011, DEC-079, DEC-167, DEC-033, DEC-108, DEC-234, DEC-246 | Nói thẳng | — |
| BR-M12-05 | DEC-116, QA-040, DEC-113, DEC-156, DM-9.1, GL:Reputation | Nói thẳng | — |
| BR-M12-06 | DEC-169, QA-040, QA-047, DG-5, DM-11, DM-x02, DM-x03, DG-8, DEC-090, DM-1.3 | Suy ra | DEC-090 hằng số chính sách không chỉnh qua giao diện ⇒ trọng số, mốc huy hiệu đổi bằng triển khai; DG-5, DM-11 không cộng/trừ ngoài rule ⇒ không chỉnh tay |
| BR-M12-07 | DEC-119, DEC-116, DEC-121 | Nói thẳng | — |
| BR-M12-08 | DEC-113, DEC-231, DEC-105, ISS-134, QA-183, DEC-161, DEC-180, DEC-241 | Nói thẳng | — |
| BR-M12-09 | DEC-113, DEC-184, DEC-241 | Nói thẳng | — |
| BR-M12-10 | DEC-115 | Nói thẳng | — |
| BR-M12-11 | QA-194, QA-195, QA-040, QA-017, GL:Badge | Suy ra | QA-195 nêu ngưỡng ⇒ đạt khi tổng điểm ≥ ngưỡng; vượt nhiều ngưỡng cùng lúc (ví dụ hoàn điểm) thì đạt tất cả |
| BR-M12-12 | DEC-114 | Nói thẳng | — |
| BR-M12-13 | QA-207 | Nói thẳng | — |
| BR-M12-14 | QA-038, DEC-052, DEC-145, DEC-127, DM-9.4, GL:Leaderboard, DEC-242 | Nói thẳng | DEC-145 chỉ thay công thức Trending của DEC-052 |
| BR-M12-15 | QA-038, QA-047, DEC-116, DEC-243 | Nói thẳng | — |
| BR-M12-16 | QA-038, DEC-243 | Nói thẳng | — |
| BR-M12-17 | QA-039, DG-5, DEC-001, DG-8, DM-x03 | Nói thẳng | — |
| BR-M12-18 | DEC-123, DEC-243, DEC-246 | Nói thẳng | — |
| BR-M12-19 | DEC-121, DEC-242 | Nói thẳng | — |
| BR-M12-20 | DEC-118, DEC-122, DEC-079, QA-236, DEC-242, DEC-246 | Nói thẳng | — |
| BR-M12-21 | QA-018, DEC-246, DEC-242 | Nói thẳng | — |
| BR-M12-22 | DEC-121, DEC-242 | Nói thẳng | — |
| BR-M12-23 | DEC-117, DEC-123, DEC-121, QA-041, DEC-243, DEC-246 | Nói thẳng | — |
| BR-M12-24 | DEC-117, DEC-114, DEC-244, DEC-247, DEC-246 | Nói thẳng | — |
| BR-M12-25 | DEC-121 | Nói thẳng | — |
| BR-M12-26 | DEC-065, DEC-216, DEC-246 | Nói thẳng | — |
| BR-M12-27 | DEC-122, QA-236 | Suy ra | Nhãn hiện trong thời gian bị ban ⇒ gỡ ban thì nhãn không còn |
| BR-M12-28 | DEC-225, DEC-228, DEC-245 | Nói thẳng | — |
| BR-M12-29 | DEC-243, DEC-244 | Nói thẳng | — |

## Phụ lục B. Câu hỏi, giả định và TBD

### B.1 Câu hỏi đã hỏi

| Mã | Loại | Câu hỏi | Trả lời | Ghi vào register |
|---|---|---|---|---|
| Q-01 | Mâu thuẫn | Tác giả tự xóa bình luận thì trừ điểm từ upvote của bình luận đó vào lúc nào? DEC-113 nói tự xóa (bài hoặc bình luận) thì trừ sau khi hết cửa sổ xóa mềm 7 ngày, nhưng bình luận không có cửa sổ khôi phục (DEC-043, DEC-179). Đề xuất: trừ ngay khi tác giả xóa bình luận, vì bình luận đã xóa không khôi phục được nên không cần chờ. | A — trừ ngay khi tác giả xóa bình luận. | QA-434, DEC-241 |
| Q-02 | Mơ hồ | Bình luận bị AI tự ẩn có trừ điểm không? DEC-113 chỉ nói Mod/Admin gỡ vì vi phạm thì trừ ngay; M08 cho AI tự ẩn bình luận có điểm quét ≥ 0,9 (không qua Mod) và ẩn bình luận 0,5–< 0,9 chờ Mod xét. Đề xuất: ≥ 0,9 trừ ngay lúc AI ẩn; 0,5–< 0,9 chỉ trừ khi Mod kết luận vi phạm và giữ ẩn. | A — điểm quét ≥ 0,9: trừ ngay lúc AI ẩn; 0,5–< 0,9: chỉ trừ khi Mod kết luận vi phạm, tại lúc kết luận. | QA-435, DEC-241 |
| Q-03 | Mơ hồ | Bài ở mức Khóa toàn bộ có chặn upvote bình luận trong bài, và có chặn rút lại upvote đã có không? DEC-033 "blocks comments + reactions", DEC-167 "blocks new comments, upvotes"; FR-M03 chỉ chặn upvote trên bài. Đề xuất: chặn upvote mới trên cả bài và bình luận của bài; vẫn cho rút lại upvote đã có. | Theo đề xuất, chặn cả rút lại: "khoá toàn bộ là khoá mọi thao tác". | QA-443, DEC-246 |
| Q-04 | Mơ hồ | Điểm trong chu kỳ tính theo thời điểm nào? QA-038 "sum upvotes trong window". Đề xuất: theo thời điểm upvote, chỉ đếm upvote còn hiệu lực trên nội dung chưa bị trừ điểm; upvote tuần trước bị rút tuần này làm giảm điểm tuần trước (đã chốt thì không đổi kết quả chốt) và điểm toàn thời gian, không trừ vào tuần này. | A — theo thời điểm upvote; không bao giờ âm; bảng đã chốt không đổi. | QA-437, DEC-243 |
| Q-05 | Thiếu chi tiết | Tuần của bảng xếp hạng bắt đầu từ thứ mấy (và bảng Tuần hiện tuần đang chạy hay tuần đã chốt)? Đề xuất: 00:00 thứ Hai giờ Việt Nam, như tuần lịch của bộ lọc tìm kiếm (DEC-212). | Đổi mô hình: tab Tuần, Tháng hiện bảng đã chốt của tuần qua, tháng qua (sửa DEC-121, QA-202). Tuần từ 00:00 thứ Hai, tháng từ 00:00 ngày mùng 1; Toàn thời gian giữ tính lại mỗi 60 phút; người bị loại sau lúc chốt bị ẩn dòng. | QA-436, DEC-242 |
| Q-06 | Mơ hồ | Người có 0 điểm trong chu kỳ có hiện trên bảng xếp hạng và có nhận danh hiệu tuần không? Nếu có, tuần chỉ 2 người có điểm thì mọi người 0 điểm đồng hạng 3 và đều nhận danh hiệu. Đề xuất: chỉ người có điểm trong chu kỳ > 0 được xếp hạng và nhận danh hiệu. | A — chỉ người có điểm chu kỳ > 0 được xếp hạng, nhận danh hiệu. | QA-438, DEC-243 |
| Q-07 | Thiếu chi tiết | Những người đồng hạng hiện theo thứ tự nào? Đề xuất: theo tên hiển thị A–Z, chỉ để hiển thị, không đổi thứ hạng. | Theo đề xuất — username A–Z. | QA-443, DEC-246 |
| Q-08 | Mơ hồ | Người đang ở HEAVY hoặc BANNED lúc chốt tuần có nhận danh hiệu không, và điểm có được trong thời gian bị loại có tính khi trở lại không? Đề xuất: xét trạng thái lúc chốt, người bị loại không nhận và không chiếm hạng; điểm vẫn tích lũy bình thường, chỉ ẩn khỏi bảng. | Theo đề xuất — xét lúc chốt; không nhận, không chiếm suất; điểm vẫn tích. | QA-443, DEC-246 |
| Q-09 | Thiếu chi tiết | Tài khoản đã xóa: ở chu kỳ toàn thời gian (không có "chu kỳ sau") xử lý thế nào; nhãn "[Tài khoản đã xóa]" (QA-018) có đổi thành "[Người dùng đã xóa]" như nơi khác (DEC-149, DEC-156) không; tài khoản DEACTIVATED có trên bảng xếp hạng không? Đề xuất: toàn thời gian loại ngay; dùng "[Người dùng đã xóa]"; DEACTIVATED bị loại trong thời gian vô hiệu hóa. | Theo đề xuất — Toàn thời gian loại ngay; nhãn "[Người dùng đã xóa]"; DEACTIVATED bị loại khi vô hiệu hóa. | QA-443, DEC-246 |
| Q-10 | Mơ hồ | "Point milestone" trong DEC-065 là sự kiện gì? Huy hiệu đã là mốc điểm. Đề xuất: mốc điểm chính là đạt huy hiệu, chỉ có một thông báo cho mỗi lần đạt huy hiệu. | Theo đề xuất — mốc điểm là đạt huy hiệu. | QA-443, DEC-246 |
| Q-11 | Thiếu chi tiết | Danh hiệu "Ngôi sao tuần" đã đạt hiện ở đâu? DEC-121 nói lịch sử danh hiệu "remain permanently visible" nhưng FR-M02 chỉ hiện điểm, huy hiệu. Đề xuất: trên hồ sơ (M02) cạnh huy hiệu, hiện số lần đạt và các tuần đạt. | B — trên hồ sơ và dấu cạnh tên trên tab Tuần; sửa ở bước 7: hồ sơ chỉ hiện khi đạt ở tuần vừa chốt, không đếm số lần, không danh sách tuần. | QA-439, DEC-244; QA-444, DEC-247 |
| Q-12 | Thiếu chi tiết | Khi chốt chu kỳ tháng có làm gì ngoài chốt bảng (thông báo thứ hạng tháng)? DEC-121 nói chốt cả tuần và tháng nhưng danh hiệu chỉ có ở tuần. Đề xuất: không làm gì thêm; chu kỳ tháng mới bắt đầu. | Theo đề xuất — chốt tháng không trao, không thông báo. | QA-443, DEC-246 |
| Q-13 | Thiếu chi tiết | Bảng xếp hạng hiện những thông tin gì cho mỗi người và bao nhiêu người? DM-9.4 gợi ý Rank, User, Score, Reputation, Stars received, Contribution statistics. Đề xuất: hạng, tên hiển thị, avatar, điểm trong chu kỳ; hiện 100 người đầu và dòng của chính người xem nếu ngoài 100. | A — thứ hạng, avatar, tên kèm username, điểm chu kỳ, dấu danh hiệu, nhãn đã xóa; mọi người điểm > 0, 20 dòng mỗi lần cuộn. | QA-440, DEC-243 |
| Q-14 | Thiếu chi tiết | Khi cờ Gamification tắt, những gì bị từ chối và những gì vẫn chạy (DEC-225 giao danh sách cho FR M12)? Đề xuất: từ chối upvote, rút upvote, mở bảng xếp hạng; vẫn chạy tính điểm, trao huy hiệu, tính và chốt bảng, trao danh hiệu, thông báo; số upvote, điểm, huy hiệu vẫn hiện ở bài, bình luận, hồ sơ; nhãn "Tài khoản đã bị khóa" vẫn hiện. | A — xem BR-M12-28. | QA-442, DEC-245 |
| Q-15 | Mơ hồ | Khi lọc bảng xếp hạng theo Lớp/Khối, thứ hạng được đánh lại trong nhóm lọc (1, 2, 3…) hay giữ thứ hạng toàn hệ thống? Lớp/Khối lấy theo giá trị hiện tại trên hồ sơ? Đề xuất: đánh lại thứ hạng trong nhóm lọc theo cùng quy tắc đồng hạng; dùng Lớp/Khối hiện tại trên hồ sơ. | A — đánh lại thứ hạng trong nhóm lọc; Lớp/Khối lấy lúc chốt. | QA-441, DEC-243 |

### B.2 TBD

| ID | Nội dung | Ảnh hưởng | Lý do chưa chốt |
|---|---|---|---|

Không có mục OPEN nào hoãn hành vi của M12.

### B.3 Cần cân nhắc (ngoài dữ liệu hiện có)

| Mã | Điểm cần cân nhắc | Vì sao cần | Quyết định |
|---|---|---|---|

## Phụ lục C. Sổ nguồn

**Owner keywords:** M12, F-REWD, REWD, Gamification, gamification, points, point, user_points, cộng điểm, trừ điểm, tổng điểm, hoàn điểm, điểm đóng góp, cày điểm, reputation, uy tín, Post Star, PostStar, Comment Star, CommentStar, upvote, upvotes, upvoted, downvote, star, stars, unstar, bỏ upvote, self-vote, self-voting, tự vote, vote retraction, rút lại, badge, badges, huy hiệu, achievement, milestone, mốc điểm, top-N title, periodic title, danh hiệu, Ngôi sao tuần, weekly top, top-N, top N, leaderboard, bảng xếp hạng, xếp hạng, đồng hạng, ranking, rank, Weekly, Monthly, All-time, All Time, Yearly, Người mới nổi, Cây bút triển vọng, Cây bút tích cực, Chuyên gia cộng đồng, Huyền thoại iShare, Tài khoản đã bị khóa, User Statistics, Stars received, Stars given, vote, votes, feature flag, feature flags, cờ tính năng, DEC-113, DEC-114, DEC-115, DEC-116, DEC-117, DEC-118, DEC-119, DEC-120, DEC-121, DEC-122, DEC-123, DEC-043, Policy constants, QA-018
**Dependency keywords:** post, bài viết, comment, bình luận, soft-delete, hard-delete, xóa mềm, xóa hẳn, appeal, khiếu nại, warning, cảnh cáo, HEAVY, probation, ban, BANNED, unban, profile, hồ sơ, notification, thông báo, group, nhóm, feature flag, cờ tính năng, timezone, Asia/Ho_Chi_Minh, anonymous, ẩn danh, Accepted Answer, DEACTIVATED, DELETED, audit log, cron, AI_ENABLED, ADMIN, MOD, Guest, poll, trending, feed
**Mục draft của module:** DM-4.1, DM-4.3, DM-9.1, DM-9.2, DM-9.3, DM-9.4
**Loại khỏi bảng nguồn (khớp nhầm):** DEC-008, QA-022, QA-024, QA-259 (cờ AI_ENABLED, không phải cờ Gamification); DEC-165, QA-081 ("vote" là bình chọn poll, M03); DEC-037 ("badge (đã chỉnh sửa)", M03); QA-210, ISS-155 (badge "tin nhắn mới", M16); DEC-067 (badge số chưa đọc, M07); DEC-049 ("re-points" khi gộp Topic, M05); DEC-140, DEC-198 ("point" là từ thường); DEC-236 ("entry points" của nhóm, M11); DEC-139, QA-265 ("milestone" của tài liệu); DM-11.4 ("Key Points" của tóm tắt, M13); DEC-203, QA-245, MR-M15 (mốc lọc "All-time" của M15); ISS-255, QA-315 ("rút lại" sự đồng ý, M01); QA-186 ("rút lại" bài khỏi feed, M11); QA-241, ISS-178 (bảng xếp hạng Mod của M15, đã bỏ); QA-037 (tìm kiếm bình luận, M06); ISS-087, ISS-336, QA-396, ISS-337, QA-397, MR-M06, DEC-125, QA-233, ISS-167 ("ranking/xếp hạng" của tìm kiếm, feed, Trending); DEC-133, QA-254, DEC-192, DEC-194, DEC-200, DEC-201, DEC-202 (trích DEC-115 về khiếu nại, nhật ký AI, không nói tới điểm); DEC-158, DEC-190 (khớp nhầm từ khóa bổ sung ở bước 2)

### C.1 Bảng nguồn

| Nguồn | Nhãn | Trạng thái | Dùng ở | Ghi chú |
|---|---|---|---|---|
| DEC-116 | Sở hữu | Hiện hành | FR-M12-02, FR-M12-02.01, FR-M12-02.02, FR-M12-04.02, BR-M12-05, BR-M12-07, BR-M12-15 | Nhóm A. Trọng số điểm: Post Star 2, Comment Star 1 |
| DEC-117 | Sở hữu | Sửa một phần bởi DEC-243 | FR-M12-05, FR-M12-05.02, FR-M12-05.05, BR-M12-23, BR-M12-24 | Nhóm A. Danh hiệu "Ngôi sao tuần": chỉ chu kỳ tuần, N=3, hòa ở hạng cắt cùng nhận |
| DEC-118 | Sở hữu | Sửa một phần bởi DEC-242, DEC-246 | FR-M12-04.07, FR-M12-04.09, FR-M12-04.10, FR-M12-06, BR-M12-20 | Nhóm A. HEAVY bị loại khỏi bảng xếp hạng trong thời gian thử thách (sửa DEC-079) |
| DEC-119 | Sở hữu | Hiện hành | FR-M12-01, FR-M12-01.01, FR-M12-01.02, FR-M12-01.03, FR-M12-02, FR-M12-02.03, BR-M12-02, BR-M12-07 | Nhóm A. Upvote rút lại được; điểm người nhận trừ ngay |
| DEC-120 | Sở hữu | Hiện hành | FR-M12-01, FR-M12-01.06, FR-M12-01.07, BR-M12-03 | Nhóm A. Không tự vote; nút vote ẩn/tắt trên nội dung của chính mình |
| DEC-121 | Sở hữu | Sửa một phần bởi DEC-242, DEC-247 | FR-M12-02.01, FR-M12-02.02, FR-M12-04, FR-M12-04.01, FR-M12-04.14, FR-M12-05, FR-M12-05.01, FR-M12-05.06, FR-M12-05.07, FR-M12-06, FR-M12-06.06, BR-M12-07 và 4 yêu cầu khác | Nhóm A. Bảng xếp hạng tính bằng một việc định kỳ 60 phút; chốt chu kỳ, trao danh hiệu; điểm cá nhân tức thời; không xem chu kỳ trước |
| DEC-122 | Sở hữu | Sửa một phần bởi DEC-242, DEC-246 | FR-M12-04.08, FR-M12-04.10, FR-M12-06, FR-M12-07, FR-M12-07.01, FR-M12-07.02, FR-M12-07.03, BR-M12-20, BR-M12-27 | Nhóm A. BANNED bị loại khỏi bảng xếp hạng; nhãn "Tài khoản đã bị khóa" ở mọi nơi tên xuất hiện |
| DEC-123 | Sở hữu | Sửa một phần bởi DEC-243, DEC-246 | FR-M12-04, FR-M12-04.06, FR-M12-05, FR-M12-05.02, FR-M12-06, FR-M12-06.05, BR-M12-18, BR-M12-23 | Nhóm A. Đồng hạng trên bảng xếp hạng; hòa ở hạng cắt danh hiệu tuần |
| DM-4.1 | Sở hữu | Sửa một phần bởi DEC-119, DEC-173 | FR-M12-01, FR-M12-01.04, BR-M12-01 | Nhóm A. Draft: Post Star (star, unstar; stars nhận, stars cho) |
| DM-4.3 | Sở hữu | Hiện hành | FR-M12-01, FR-M12-01.04, BR-M12-01 | Nhóm A. Draft: Comment Star tách khỏi Post Star, trọng số khác nhau |
| DM-9.1 | Sở hữu | Sửa một phần bởi QA-040, DEC-116, DEC-169, DEC-090 | FR-M12-02, FR-M12-02.01, BR-M12-05 | Nhóm A. Draft: nguồn reputation |
| DM-9.2 | Sở hữu | Bị thay bởi QA-194, QA-195 | — | Nhóm A. Draft: nhóm và ví dụ badge |
| DM-9.3 | Sở hữu | Sửa một phần bởi DEC-169, DEC-173 | Chuyển M02 | Nhóm A. Draft: thống kê người dùng; phần còn hiệu lực (điểm, huy hiệu, người theo dõi) do hồ sơ M02 hiển thị (QA-067, DEC-173) |
| DM-9.4 | Sở hữu | Sửa một phần bởi QA-038, QA-047, DEC-116, DEC-242, DEC-243 | FR-M12-04.03, FR-M12-06, FR-M12-06.01, BR-M12-14 | Nhóm A. Draft: bảng xếp hạng Weekly/Monthly/Yearly/All Time |
| ISS-142 | Sở hữu | Trùng với DEC-113 | — | Nhóm A. Trừ điểm theo nội dung |
| ISS-143 | Sở hữu | Trùng với DEC-114 | — | Nhóm A. Badge vĩnh viễn, lịch sử đạt |
| ISS-145 | Sở hữu | Trùng với DEC-116 | — | Nhóm A. Trọng số Post Star, Comment Star |
| ISS-146 | Sở hữu | Trùng với DEC-117 | — | Nhóm A. Chu kỳ và N của danh hiệu tuần |
| ISS-147 | Sở hữu | Trùng với DEC-119 | — | Nhóm A. Rút lại upvote |
| ISS-148 | Sở hữu | Trùng với DEC-120 | — | Nhóm A. Tự vote |
| ISS-149 | Sở hữu | Trùng với DEC-121 | — | Nhóm A. Tính bảng xếp hạng định kỳ |
| ISS-150 | Sở hữu | Trùng với DEC-123 | — | Nhóm A. Đồng hạng |
| ISS-151 | Sở hữu | Trùng với QA-207 | — | Nhóm A. Không hiện tiến độ badge |
| ISS-152 | Sở hữu | Trùng với DEC-123 | — | Nhóm A. Hòa ở hạng cắt N=3 |
| ISS-153 | Sở hữu | Trùng với DEC-121 | — | Nhóm A. Không xem bảng xếp hạng chu kỳ trước |
| ISS-154 | Sở hữu | Trùng với DEC-122 | — | Nhóm A. Tài khoản BANNED: bảng xếp hạng, nhãn |
| ISS-REWD-01 | Sở hữu | Trùng với QA-195 | — | Nhóm A. Danh sách badge, tiêu chí |
| ISS-REWD-02 | Sở hữu | Trùng với DEC-118 | — | Nhóm A. Mức cảnh cáo và bảng xếp hạng |
| QA-194 | Sở hữu | Hiện hành | FR-M12-03, FR-M12-03.01, FR-M12-03.08, BR-M12-11 | Nhóm A. Badge chỉ theo tổng điểm |
| QA-195 | Sở hữu | Hiện hành | FR-M12-03, FR-M12-03.01, FR-M12-03.03, BR-M12-11 | Nhóm A. 5 mốc badge: 25/100/300/600/1000 và tên |
| QA-196 | Sở hữu | Trùng với DEC-116 | — | Nhóm A. Post Star 2, Comment Star 1 |
| QA-197 | Sở hữu | Trùng với DEC-117 | — | Nhóm A. Danh hiệu tuần, N=3 |
| QA-198 | Sở hữu | Trùng với DEC-123 | — | Nhóm A. Hòa ở hạng cắt cùng nhận danh hiệu |
| QA-199 | Sở hữu | Trùng với DEC-118 | — | Nhóm A. Chỉ HEAVY bị ẩn khỏi bảng xếp hạng |
| QA-200 | Sở hữu | Trùng với DEC-119 | — | Nhóm A. Upvote là bật/tắt; trừ điểm ngay khi rút |
| QA-201 | Sở hữu | Trùng với DEC-120 | — | Nhóm A. Ẩn/tắt nút vote trên nội dung của chính mình |
| QA-202 | Sở hữu | Trùng với DEC-121 | — | Nhóm A. Không xem lại chu kỳ trước |
| QA-203 | Sở hữu | Trùng với DEC-121 | — | Nhóm A. Một việc định kỳ 60 phút; trễ tối đa 60 phút khi chốt chu kỳ |
| QA-204 | Sở hữu | Trùng với DEC-122 | — | Nhóm A. BANNED ẩn khỏi bảng xếp hạng; hồ sơ, bài, bình luận vẫn hiện |
| QA-205 | Sở hữu | Hiện hành | FR-M12-07.04 | Nhóm A. Nhãn "Tài khoản đã bị khóa" ở mọi nơi tên tác giả xuất hiện |
| QA-206 | Sở hữu | Trùng với DEC-123 | — | Nhóm A. Đồng hạng kiểu thể thao |
| QA-207 | Sở hữu | Hiện hành | FR-M12-03, FR-M12-03.07, BR-M12-13 | Nhóm A. Không hiện tiến độ badge |
| MR-M12 | Sở hữu | Sửa một phần bởi DEC-241, DEC-242, DEC-243, DEC-244, DEC-245, DEC-246, DEC-247 | FR-M12-01, FR-M12-02, FR-M12-03, FR-M12-04, FR-M12-05, FR-M12-06, FR-M12-07 | Nhóm A. Dòng module M12: Should; tóm tắt phạm vi |
| DEC-001 | Sở hữu | Hiện hành | FR-M12-04.13, BR-M12-17 | Nhóm B. Không có loại tài khoản Giáo viên, không leaderboard riêng cho giáo viên |
| DEC-004 | Sở hữu | Hiện hành | FR-M12-01.04, FR-M12-02, BR-M12-01 | Nhóm B. Post Star tách Comment Star, trọng số riêng |
| DEC-028 | Phụ thuộc | Hiện hành | FR-M12-03.06 | Nhóm B. M02: điểm, badge trên hồ sơ chỉ hiển thị; M12 tính |
| DEC-033 | Phụ thuộc | Sửa một phần bởi DEC-167 | FR-M12-01.10, BR-M12-04 | Nhóm B. M03: Khóa toàn bộ chặn reactions |
| DEC-041 | Sở hữu | Hiện hành | FR-M12-01, FR-M12-01.05, BR-M12-01 | Nhóm B. Chỉ upvote, không downvote (section M04) |
| DEC-042 | Nhắc tới | Sửa một phần bởi DEC-182 | Không áp dụng: M04: sắp Top theo số upvote | Nhóm B. M04: sắp Top theo số upvote |
| DEC-043 | Phụ thuộc | Sửa một phần bởi DEC-179 | Chuyển M04 | Nhóm B. M04: xóa bình luận không có cửa sổ khôi phục (mốc trừ điểm) |
| DEC-052 | Sở hữu | Sửa một phần bởi DEC-145 | FR-M12-04, FR-M12-04.03, BR-M12-14 | Nhóm B. Câu so sánh: tuần của leaderboard là tuần lịch cố định (phần còn lại là Trending M05) |
| DEC-055 | Nhắc tới | Sửa một phần bởi DEC-211 | Không áp dụng: M06: xếp hạng tìm kiếm dùng số upvote | Nhóm B. M06: xếp hạng tìm kiếm dùng số upvote |
| DEC-056 | Nhắc tới | Sửa một phần bởi DEC-211, DEC-212 | Không áp dụng: M06: sắp xếp Nhiều upvote nhất | Nhóm B. M06: sắp xếp Nhiều upvote nhất |
| DEC-065 | Phụ thuộc | Sửa một phần bởi DEC-180, DEC-231, DEC-246 | FR-M12-01.13, FR-M12-03, FR-M12-03.10, FR-M12-05, FR-M12-05.07, BR-M12-26 | Nhóm B. M07: thông báo in-app cho upvote, badge, mốc điểm, danh hiệu tuần; DEC-147, DEC-151, DEC-215, DEC-218, DEC-221, DEC-237 (ngoài bảng nguồn) thêm sự kiện khác, không chạm sự kiện M12 |
| DEC-066 | Phụ thuộc | Sửa một phần bởi DEC-216 | Chuyển M07 | Nhóm B. M07: gộp thông báo upvote 5 phút |
| DEC-070 | Nhắc tới | Sửa một phần bởi DEC-220 | Không áp dụng: M07: tắt thông báo upvote theo bài | Nhóm B. M07: tắt thông báo upvote theo bài |
| DEC-079 | Phụ thuộc | Sửa một phần bởi DEC-118, DEC-122, DEC-211 | FR-M12-01.09, FR-M12-04.07, BR-M12-04, BR-M12-20 | Nhóm B. M08: mức HEAVY, thời gian thử thách; HEAVY vẫn vote; sửa bởi DEC-118, DEC-122; DEC-163, DEC-188 (ngoài bảng nguồn) sửa hạn chế đăng bài, thử thách nối tiếp; HEAVY vẫn upvote được |
| DEC-090 | Phụ thuộc | Hiện hành | FR-M12-02.06, FR-M12-03.09, BR-M12-06 | Nhóm B. M10: hằng số chính sách (ngưỡng, thời hạn) không chỉnh qua giao diện, đổi bằng triển khai; DEC-141, DEC-224 (ngoài bảng nguồn) chỉ nói Topic và nhật ký Mod |
| DEC-092 | Phụ thuộc | Sửa một phần bởi DEC-225, DEC-228 | FR-M12-08, FR-M12-08.01 | Nhóm B. M10: cờ tính năng Gamification |
| DEC-102 | Phụ thuộc | Sửa một phần bởi DEC-231 | Chuyển M11 | Nhóm B. M11: Owner, Group Mod, Member đều vote trong nhóm |
| DEC-105 | Sở hữu | Sửa một phần bởi DEC-113 | FR-M12-02, FR-M12-02.14, FR-M12-02.15, BR-M12-08 | Nhóm B. Điểm khi xóa nhóm, rời hoặc bị kick (ngoại lệ trừ điểm đã bị DEC-113 bỏ) |
| DEC-108 | Phụ thuộc | Sửa một phần bởi DEC-234 | FR-M12-01.11, BR-M12-04 | Nhóm B. M11: nhóm chuyển Private thì bài đã hiện không vote được |
| DEC-113 | Sở hữu | Sửa một phần bởi DEC-184, DEC-231, DEC-241 | FR-M12-02, FR-M12-02.08, FR-M12-02.09, FR-M12-02.10, FR-M12-02.11, FR-M12-02.14, FR-M12-02.15, FR-M12-02.17, FR-M12-02.18, BR-M12-05, BR-M12-08, BR-M12-09 | Nhóm B. Trừ điểm khi nội dung mất đi do trực tiếp; giữ khi gián tiếp; thời điểm trừ (section M09 + M12). Mâu thuẫn về thời điểm trừ khi tự xóa bình luận đã giải quyết ở DEC-241 (Q-01) |
| DEC-114 | Sở hữu | Sửa một phần bởi DEC-244 | FR-M12-03, FR-M12-03.02, FR-M12-03.04, FR-M12-03.05, FR-M12-03.06, FR-M12-03.09, FR-M12-05, FR-M12-05.03, FR-M12-05.04, FR-M12-05.13, BR-M12-12, BR-M12-24 | Nhóm B. Badge vĩnh viễn, hiện ngày đạt; lịch sử badge và danh hiệu (section M09 + M12) |
| DEC-115 | Phụ thuộc | Hiện hành | FR-M12-02, FR-M12-02.10, FR-M12-02.12, FR-M12-02.13, BR-M12-10 | Nhóm B. M09: khiếu nại bài bị gỡ thành công thì hoàn điểm đã trừ; bình luận không khiếu nại; DEC-198, DEC-200, DEC-202 (loại) đổi phạm vi khiếu nại, danh sách khiếu nại, không chạm phần hoàn điểm |
| DEC-124 | Nhắc tới | Hiện hành | Không áp dụng: M14: Trending Post dùng số upvote | Nhóm B. M14: Trending Post dùng số upvote |
| DEC-126 | Sở hữu | Hiện hành | FR-M12-01, FR-M12-01.08, BR-M12-04 | Nhóm B. Guest phải đăng nhập để upvote |
| DEC-127 | Phụ thuộc | Hiện hành | FR-M12-04, FR-M12-04.03, BR-M12-14 | Nhóm B. Dùng chung: UTC+7, ranh giới tuần của leaderboard |
| DEC-145 | Nhắc tới | Hiện hành | FR-M12-04, FR-M12-04.03, BR-M12-14 | Nhóm B. M05: Trending Topic/Tag dùng upvote bài, upvote đã rút không tính |
| DEC-149 | Phụ thuộc | Hiện hành | Chuyển M01 | Nhóm B. M01: hiển thị tài khoản đã xóa; sửa phần bình luận của QA-018 |
| DEC-156 | Sở hữu | Hiện hành | FR-M12-02, FR-M12-02.04, BR-M12-05 | Nhóm B. Upvote đã cho của tài khoản đã xóa vẫn tính cho người nhận (section M01); DEC-159 (ngoài bảng nguồn) thêm dữ liệu bị xóa, không chạm upvote |
| DEC-161 | Phụ thuộc | Hiện hành | FR-M12-01.12, FR-M12-02.10, BR-M12-08 | Nhóm B. M03: "bị Mod/Admin gỡ" là trạng thái kiểm duyệt HIDDEN của bài; DEC-185 (ngoài bảng nguồn) chỉ nói quét lại |
| DEC-167 | Phụ thuộc | Sửa một phần bởi DEC-246 | FR-M12-01.10, BR-M12-04 | Nhóm B. M03: Khóa toàn bộ chặn upvote |
| DEC-169 | Sở hữu | Hiện hành | FR-M12-02, FR-M12-02.07, BR-M12-06 | Nhóm B. MS1 không có Accepted Answer, ảnh hưởng M12 |
| DEC-172 | Nhắc tới | Hiện hành | Không áp dụng: M02: hồ sơ BANNED vẫn hiện kèm nhãn (DEC-122) | Nhóm B. M02: hồ sơ BANNED vẫn hiện kèm nhãn (DEC-122) |
| DEC-173 | Phụ thuộc | Hiện hành | Chuyển M02 | Nhóm B. M02: hồ sơ không hiện stars nhận, stars cho |
| DEC-179 | Phụ thuộc | Hiện hành | Chuyển M04 | Nhóm B. M04: bình luận chỉ xóa mềm, không khôi phục |
| DEC-180 | Phụ thuộc | Hiện hành | FR-M12-01.12, FR-M12-02.11, BR-M12-08 | Nhóm B. M04: Mod/Admin chỉ có thao tác Ẩn bình luận; DEC-201 (loại) chỉ nói bình luận bị ẩn không hiện lại |
| DEC-182 | Nhắc tới | Hiện hành | Không áp dụng: M04: thứ tự Top khi cùng số upvote | Nhóm B. M04: thứ tự Top khi cùng số upvote |
| DEC-184 | Sở hữu | Hiện hành | FR-M12-01.12, FR-M12-02, FR-M12-02.08, BR-M12-09 | Nhóm B. Trừ điểm bài tự xóa khi bài chuyển cờ Đã xóa hẳn (section M03) |
| DEC-211 | Nhắc tới | Hiện hành | Không áp dụng: M06: sắp xếp Nhiều upvote nhất | Nhóm B. M06: sắp xếp Nhiều upvote nhất |
| DEC-212 | Nhắc tới | Hiện hành | Không áp dụng: M06: duyệt theo Topic/Tag, sắp Nhiều upvote nhất | Nhóm B. M06: duyệt theo Topic/Tag, sắp Nhiều upvote nhất; DEC-215 (ngoài bảng nguồn) chỉ đổi bộ lọc đang theo dõi |
| DEC-216 | Phụ thuộc | Hiện hành | FR-M12-01.13, BR-M12-26 | Nhóm B. M07: chi tiết gộp upvote; bỏ upvote không đổi thông báo |
| DEC-217 | Nhắc tới | Hiện hành | Không áp dụng: M07: thông báo upvote gộp được đưa lên đầu chuông | Nhóm B. M07: thông báo upvote gộp được đưa lên đầu chuông |
| DEC-220 | Nhắc tới | Hiện hành | Không áp dụng: M07: công tắc bài tắt cả upvote bình luận của mình trong bài | Nhóm B. M07: công tắc bài tắt cả upvote bình luận của mình trong bài; DEC-222 (ngoài bảng nguồn) chỉ nói đề xuất vai trò |
| DEC-225 | Sở hữu | Sửa một phần bởi DEC-245 | FR-M12-08, FR-M12-08.01, FR-M12-08.02, FR-M12-08.03, FR-M12-08.04, FR-M12-08.05, FR-M12-08.06, BR-M12-28 | Nhóm B. Danh sách thao tác bị chặn khi cờ Gamification tắt thuộc FR M12; điểm, bảng xếp hạng vẫn chạy (section M10); DEC-236 (loại) chỉ áp cho cờ Group |
| DEC-228 | Phụ thuộc | Hiện hành | FR-M12-08, FR-M12-08.07, BR-M12-28 | Nhóm B. M10: ba cờ tính năng khởi tạo Bật |
| DEC-231 | Sở hữu | Hiện hành | FR-M12-02, FR-M12-02.16, BR-M12-08 | Nhóm B. Gỡ khỏi nhóm không trừ điểm (section M11) |
| DEC-234 | Phụ thuộc | Hiện hành | FR-M12-01.11, BR-M12-04 | Nhóm B. M11: người ngoài nhóm đã đăng nhập vote bài nhóm Public |
| DG-1 | Nhắc tới | Hiện hành | Không áp dụng: Mô tả chung: uy tín, xếp hạng | Nhóm B. Mô tả chung: uy tín, xếp hạng |
| DG-4 | Nhắc tới | Sửa một phần bởi DEC-169 | Không áp dụng: Bản đồ module: Reward / Reputation / Statistics / Leaderboard | Nhóm B. Bản đồ module: Reward / Reputation / Statistics / Leaderboard |
| DG-5 | Sở hữu | Sửa một phần bởi DEC-169 | FR-M12-02, FR-M12-02.06, FR-M12-03.09, FR-M12-04.13, FR-M12-06, BR-M12-06, BR-M12-17 | Nhóm B. Nguyên tắc: điểm chỉ theo rule; Post Star tách Comment Star; không leaderboard giáo viên, không leaderboard theo nhóm |
| DG-8 | Sở hữu | Hiện hành | FR-M12-02.06, BR-M12-06, BR-M12-17 | Nhóm B. Không làm: leaderboard/badge riêng cho giáo viên; AI tự quyết reputation/badge |
| DM-1.2 | Phụ thuộc | Sửa một phần bởi DEC-173 | Chuyển M02 | Nhóm B. M02: hồ sơ có stars, reputation, badges (draft) |
| DM-1.3 | Sở hữu | Sửa một phần bởi DEC-090 | FR-M12-03.09, BR-M12-06 | Nhóm B. Draft: quyền "Manage badges"; "Manage badges" hết hiệu lực: mốc huy hiệu là hằng số, đổi bằng triển khai |
| DM-11 | Sở hữu | Hiện hành | FR-M12-02, FR-M12-02.06, BR-M12-06 | Nhóm B. Draft: AI không tự cộng/trừ reputation |
| DM-13 | Nhắc tới | Hiện hành | Không áp dụng: Draft: khối Reward trong kiến trúc | Nhóm B. Draft: khối Reward trong kiến trúc |
| DM-2.1 | Nhắc tới | Sửa một phần bởi DEC-169 | Không áp dụng: Draft: Star count của bài | Nhóm B. Draft: Star count của bài |
| DM-4.2.1 | Nhắc tới | Bị thay bởi DEC-169 | — | Nhóm B. Draft: Accepted Answer cộng reputation (MS1 không làm, DEC-169) |
| DM-5.3 | Phụ thuộc | Hiện hành | Chuyển M11 | Nhóm B. Draft M11: Star trong nhóm dùng chung cơ chế Forum |
| DM-5.4 | Sở hữu | Trùng với QA-039 | — | Nhóm B. Draft: không leaderboard, reputation riêng theo nhóm |
| DM-7.2 | Nhắc tới | Sửa một phần bởi DEC-145 | Không áp dụng: Draft M05/M14: Trending dựa trên Stars | Nhóm B. Draft M05/M14: Trending dựa trên Stars |
| DM-8.1 | Phụ thuộc | Sửa một phần bởi DEC-065, DEC-169 | Chuyển M07 | Nhóm B. Draft M07: thông báo bài nhận star, nhận badge |
| DM-9 | Nhắc tới | Hiện hành | Không áp dụng: Draft: tiêu đề mục 9 | Nhóm B. Draft: tiêu đề mục 9 |
| DM-9.5 | Nhắc tới | Hiện hành | Không áp dụng: Draft: thống kê hệ thống (M15) | Nhóm B. Draft: thống kê hệ thống (M15) |
| DM-x02 | Sở hữu | Sửa một phần bởi DEC-169 | FR-M12-02.07, BR-M12-06 | Nhóm B. Draft: trong phạm vi có Star, Reputation, Badge, Statistics, Leaderboard |
| DM-x03 | Sở hữu | Hiện hành | FR-M12-02.06, BR-M12-06, BR-M12-17 | Nhóm B. Draft: ngoài phạm vi có AI tự quyết reputation/badge, phân biệt Giáo viên |
| GL:Badge | Sở hữu | Sửa một phần bởi QA-194 | FR-M12-03, FR-M12-03.01, BR-M12-11 | Nhóm B. Thuật ngữ Badge |
| GL:Comment Star | Sở hữu | Hiện hành | FR-M12-01, FR-M12-01.04, BR-M12-01 | Nhóm B. Thuật ngữ Comment Star |
| GL:Group | Nhắc tới | Hiện hành | Không áp dụng: Group dùng chung Star | Nhóm B. Group dùng chung Star |
| GL:Leaderboard | Sở hữu | Sửa một phần bởi QA-038, DEC-242 | FR-M12-04.03, FR-M12-06, BR-M12-14 | Nhóm B. Thuật ngữ Leaderboard (4 chu kỳ) |
| GL:Post Star | Sở hữu | Hiện hành | FR-M12-01, FR-M12-01.04, BR-M12-01 | Nhóm B. Thuật ngữ Post Star |
| GL:Reputation | Sở hữu | Sửa một phần bởi DEC-116, DEC-169 | FR-M12-02, FR-M12-02.01, BR-M12-05 | Nhóm B. Thuật ngữ Reputation |
| ISS-037 | Nhắc tới | Trùng với QA-018 | — | Nhóm B. Câu hỏi xóa tài khoản, trả lời ở QA-018 |
| ISS-048 | Sở hữu | Trùng với QA-038 | — | Nhóm B. Leaderboard: chu kỳ, bộ lọc, phạm vi |
| ISS-049 | Sở hữu | Trùng với QA-040 | — | Nhóm B. Điểm tính theo gì, loại badge |
| ISS-072 | Sở hữu | Trùng với DEC-041 | — | Nhóm B. Chỉ upvote, không downvote |
| ISS-098 | Phụ thuộc | Trùng với DEC-065 | — | Nhóm B. M07: danh sách sự kiện thông báo |
| ISS-121 | Phụ thuộc | Trùng với DEC-092 | — | Nhóm B. M10: danh sách cấu hình có cờ tính năng |
| ISS-134 | Sở hữu | Sửa một phần bởi DEC-113 | FR-M12-02.14, FR-M12-02.15, BR-M12-08 | Nhóm B. Điểm khi xóa nhóm, rời nhóm |
| ISS-144 | Phụ thuộc | Trùng với DEC-115 | — | Nhóm B. M09: khiếu nại bài bị gỡ, hoàn điểm |
| ISS-160 | Nhắc tới | Trùng với QA-218 | — | Nhóm B. M16: Block có thể ảnh hưởng leaderboard, đã hoãn (OPEN-003) |
| ISS-166 | Sở hữu | Trùng với DEC-126 | — | Nhóm B. Mọi tương tác (upvote) cần đăng nhập |
| ISS-176 | Sở hữu | Trùng với QA-236 | — | Nhóm B. Ngoại lệ ẩn chỉ áp cho bảng xếp hạng; Trending không loại |
| ISS-183 | Nhắc tới | Trùng với QA-246 | — | Nhóm B. M15 so sánh: leaderboard tính theo lô |
| ISS-189 | Phụ thuộc | Trùng với DEC-127 | — | Nhóm B. Dùng chung: múi giờ |
| ISS-233 | Nhắc tới | Trùng với DEC-149 | — | Nhóm B. Bình luận của tài khoản DELETED, xem DEC-149 |
| ISS-277 | Phụ thuộc | Trùng với DEC-173 | — | Nhóm B. M02: không hiện stars nhận/cho trên hồ sơ |
| ISS-287 | Nhắc tới | Trùng với DEC-182 | — | Nhóm B. M04: thứ tự Top khi cùng upvote |
| ISS-338 | Nhắc tới | Trùng với DEC-211 | — | Nhóm B. M06: sắp xếp Nhiều upvote nhất |
| ISS-347 | Phụ thuộc | Trùng với DEC-216 | — | Nhóm B. M07: gộp thông báo upvote, bỏ upvote |
| ISS-356 | Phụ thuộc | Trùng với DEC-225 | — | Nhóm B. M10: cờ tính năng, hành vi khi tắt |
| QA-003 | Nhắc tới | Hiện hành | Không áp dụng: Dữ liệu demo gồm badge | Nhóm B. Dữ liệu demo gồm badge |
| QA-004 | Nhắc tới | Hiện hành | Không áp dụng: Gamification tạo động lực ban đầu | Nhóm B. Gamification tạo động lực ban đầu |
| QA-005 | Nhắc tới | Bị thay bởi QA-006 | — | Nhóm B. Đề xuất mục tiêu Gamification |
| QA-006 | Nhắc tới | Hiện hành | Không áp dụng: Mục tiêu BG-03 (Expectancy Theory) — lý do của module | Nhóm B. Mục tiêu BG-03 (Expectancy Theory) — lý do của module |
| QA-011 | Sở hữu | Hiện hành | FR-M12-01, FR-M12-01.08, FR-M12-06, FR-M12-06.01, BR-M12-04 | Nhóm B. Guest xem Leaderboard, Badges, Reputation; DEC-171, DEC-206, DEC-208 (ngoài bảng nguồn) không chạm quyền xem bảng xếp hạng, huy hiệu, điểm |
| QA-012 | Nhắc tới | Hiện hành | Không áp dụng: Lên Mod không cần reputation | Nhóm B. Lên Mod không cần reputation |
| QA-017 | Sở hữu | Hiện hành | FR-M12-02, FR-M12-03, FR-M12-03.02, FR-M12-03.10, BR-M12-11 | Nhóm B. Badge/Reputation Engine tính điểm, trao badge tự động; DEC-203 (loại) chỉ nói vòng phản hồi AI |
| QA-018 | Sở hữu | Sửa một phần bởi DEC-019, DEC-149, DEC-156, DEC-246 | FR-M12-03.11, FR-M12-04.11, FR-M12-04.12, FR-M12-06, BR-M12-21 | Nhóm B. Leaderboard, badge của tài khoản đã xóa; phần bảng xếp hạng, huy hiệu của tài khoản đã xóa chưa bị sửa |
| QA-020 | Nhắc tới | Sửa một phần bởi DEC-079 | Không áp dụng: Phát sinh ISS-REWD-02 | Nhóm B. Phát sinh ISS-REWD-02; ngưỡng AI, giảm mức còn được sửa bởi DEC-186, DEC-188 (ngoài bảng nguồn) |
| QA-038 | Sở hữu | Sửa một phần bởi DEC-243 | FR-M12-01.01, FR-M12-04, FR-M12-04.01, FR-M12-04.02, FR-M12-04.03, FR-M12-04.05, FR-M12-06, FR-M12-06.02, FR-M12-06.03, BR-M12-14, BR-M12-15, BR-M12-16 | Nhóm B. Chu kỳ Weekly/Monthly/All-time; bộ lọc Lớp/Khối; chỉ toàn hệ thống |
| QA-039 | Sở hữu | Hiện hành | FR-M12-04.13, FR-M12-06, BR-M12-17 | Nhóm B. Không có leaderboard theo nhóm |
| QA-040 | Sở hữu | Sửa một phần bởi DEC-116, QA-195 | FR-M12-02, FR-M12-02.01, FR-M12-02.02, FR-M12-02.07, FR-M12-03, FR-M12-03.02, FR-M12-05, FR-M12-05.02, BR-M12-05, BR-M12-06, BR-M12-11 | Nhóm B. Điểm = tổng upvote nhận; badge theo ngưỡng; danh hiệu top-N theo chu kỳ |
| QA-041 | Sở hữu | Sửa một phần bởi DEC-117 | FR-M12-05, FR-M12-05.02, BR-M12-23 | Nhóm B. Danh hiệu cho top N, không chỉ top 1 |
| QA-047 | Sở hữu | Hiện hành | FR-M12-02, FR-M12-02.05, FR-M12-04, FR-M12-04.02, FR-M12-04.04, BR-M12-06, BR-M12-15 | Nhóm B. Điểm không giảm theo thời gian; xếp hạng theo tổng trong chu kỳ |
| QA-067 | Phụ thuộc | Sửa một phần bởi DEC-173 | Chuyển M02 | Nhóm B. M02: hồ sơ hiện points, badges |
| QA-077 | Phụ thuộc | Trùng với DEC-028 | — | Nhóm B. M02: điểm, badge chỉ hiển thị |
| QA-094 | Sở hữu | Trùng với DEC-041 | — | Nhóm B. Không downvote bình luận |
| QA-106 | Nhắc tới | Bị thay bởi DEC-145 | — | Nhóm B. M05: Trending dùng upvote |
| QA-112 | Nhắc tới | Trùng với DEC-055 | — | Nhóm B. M06: trọng số upvote trong xếp hạng tìm kiếm |
| QA-123 | Phụ thuộc | Trùng với DEC-065 | — | Nhóm B. M07: danh sách sự kiện có gamification |
| QA-126 | Phụ thuộc | Trùng với DEC-066 | — | Nhóm B. M07: báo upvote từng lượt, gộp 5 phút |
| QA-161 | Phụ thuộc | Trùng với DEC-090 | — | Nhóm B. M10: hằng số chính sách không chỉnh qua giao diện |
| QA-164 | Phụ thuộc | Trùng với DEC-092 | — | Nhóm B. M10: cấu hình có cờ tính năng |
| QA-180 | Phụ thuộc | Trùng với DEC-102 | — | Nhóm B. M11: quyền vote của vai trò trong nhóm |
| QA-183 | Sở hữu | Sửa một phần bởi DEC-113 | FR-M12-02.14, FR-M12-02.15, BR-M12-08 | Nhóm B. Điểm khi xóa nhóm, rời nhóm |
| QA-191 | Sở hữu | Trùng với DEC-113 | — | Nhóm B. Nguyên tắc trừ điểm trực tiếp/gián tiếp; thời điểm trừ |
| QA-192 | Sở hữu | Trùng với DEC-114 | — | Nhóm B. Badge vĩnh viễn, lịch sử đạt |
| QA-193 | Phụ thuộc | Trùng với DEC-115 | — | Nhóm B. M09: khiếu nại bài bị gỡ, hoàn điểm |
| QA-218 | Nhắc tới | Hiện hành | Không áp dụng: M16: Block có thể ảnh hưởng leaderboard, đã hoãn | Nhóm B. M16: Block có thể ảnh hưởng leaderboard, đã hoãn |
| QA-227 | Sở hữu | Trùng với DEC-126 | — | Nhóm B. Guest: mọi tương tác (upvote) cần đăng nhập |
| QA-235 | Nhắc tới | Hiện hành | Không áp dụng: M14: ngưỡng upvote cho Trending | Nhóm B. M14: ngưỡng upvote cho Trending |
| QA-236 | Sở hữu | Hiện hành | FR-M12-06, FR-M12-07, FR-M12-07.01, BR-M12-20, BR-M12-27 | Nhóm B. Ngoại lệ ẩn chỉ áp cho bảng xếp hạng; nhãn BANNED hiện cả trên Trending |
| QA-246 | Nhắc tới | Hiện hành | Không áp dụng: M15 so sánh: leaderboard tính theo lô | Nhóm B. M15 so sánh: leaderboard tính theo lô |
| QA-248 | Phụ thuộc | Trùng với DEC-127 | — | Nhóm B. Dùng chung: múi giờ, ranh giới tuần leaderboard |
| QA-257 | Nhắc tới | Trùng với DEC-135 | — | Nhóm B. Leaderboard tính định kỳ, không cần kênh thời gian thực |
| QA-271 | Nhắc tới | Trùng với DEC-145 | — | Nhóm B. M05: Trending dùng upvote, upvote rút lại |
| QA-285 | Nhắc tới | Trùng với DEC-145 | — | Nhóm B. M05: Trending dùng upvote |
| QA-311 | Sở hữu | Trùng với DEC-156 | — | Nhóm B. Upvote đã cho của tài khoản đã xóa vẫn giữ |
| QA-329 | Phụ thuộc | Trùng với DEC-167 | — | Nhóm B. M03: Khóa toàn bộ chặn upvote |
| QA-337 | Phụ thuộc | Trùng với DEC-173 | — | Nhóm B. M02: không hiện stars nhận/cho |
| QA-347 | Nhắc tới | Trùng với DEC-182 | — | Nhóm B. M04: thứ tự Top khi cùng upvote |
| QA-350 | Sở hữu | Trùng với DEC-184 | — | Nhóm B. Trừ điểm bài tự xóa tại lúc chuyển cờ |
| QA-398 | Nhắc tới | Trùng với DEC-211 | — | Nhóm B. M06: sắp xếp Nhiều upvote nhất |
| QA-399 | Nhắc tới | Trùng với DEC-212 | — | Nhóm B. M06: sắp xếp Nhiều upvote nhất khi duyệt |
| QA-407 | Phụ thuộc | Trùng với DEC-216 | — | Nhóm B. M07: gộp upvote, bỏ upvote |
| QA-411 | Nhắc tới | Trùng với DEC-220 | — | Nhóm B. M07: tắt thông báo upvote theo bài |
| QA-416 | Phụ thuộc | Trùng với DEC-225 | — | Nhóm B. M10: cờ tắt thì việc ngầm vẫn chạy, từ chối request |
| QA-417 | Phụ thuộc | Trùng với DEC-225 | — | Nhóm B. M10: chỉ Group, Chat, Gamification có cờ |
| QA-423 | Sở hữu | Trùng với DEC-231 | — | Nhóm B. Gỡ khỏi nhóm không trừ điểm |
| QA-426 | Phụ thuộc | Trùng với DEC-234 | — | Nhóm B. M11: người ngoài vote bài nhóm Public |
| MR-A03 | Nhắc tới | Trùng với QA-246 | — | Nhóm B. M15 so sánh với leaderboard |
| MR-A04 | Nhắc tới | Hiện hành | Không áp dụng: DEC-127 áp cho M12 | Nhóm B. DEC-127 áp cho M12 |
| MR-M02 | Phụ thuộc | Hiện hành | Chuyển M02 | Nhóm B. M02: hồ sơ hiện points, badges; DEC-170–177 (FR M02) không đổi việc hồ sơ hiện điểm, huy hiệu |
| MR-M04 | Nhắc tới | Hiện hành | Không áp dụng: M04: upvote-only | Nhóm B. M04: upvote-only; DEC-178–183 (FR M04) không đổi upvote-only |
| MR-M07 | Phụ thuộc | Hiện hành | Chuyển M07 | Nhóm B. M07: sự kiện gamification; DEC-135 chỉ đổi kênh SSE |
| MR-M10 | Phụ thuộc | Hiện hành | Chuyển M10 | Nhóm B. M10: cờ tính năng; DEC-221–228 không đổi cờ Gamification ngoài DEC-225, DEC-228 |
| DEC-019 | Phụ thuộc | Sửa một phần bởi DEC-149, DEC-156 | FR-M12-07.04 | Nhóm C. M01: DEACTIVATED, DELETED (hiển thị tài khoản); DEC-148 (ngoài bảng nguồn) chỉ đổi quy tắc định danh |
| DEC-089 | Phụ thuộc | Hiện hành | FR-M12-04.10, FR-M12-07.03 | Nhóm C. M09: ban được lật thì tài khoản ACTIVE lại ngay; DEC-199, DEC-201 (ngoài bảng nguồn, loại) không đổi việc ban được lật thì ACTIVE ngay |
| DEC-128 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M12 |
| DEC-129 | Nhắc tới | Sửa một phần bởi DEC-156 | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M12 |
| DEC-130 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M12 |
| DEC-131 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M12 |
| DEC-132 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M12 |
| DEC-134 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M12 |
| DEC-135 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M12 |
| DEC-136 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M12 |
| DEC-137 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M12 |
| DEC-138 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M12 |
| ISS-190 | Nhắc tới | Trùng với DEC-128 | — | Nhóm D. Dùng chung; không quy định hành vi M12 |
| ISS-191 | Nhắc tới | Trùng với DEC-129 | — | Nhóm D. Dùng chung; không quy định hành vi M12 |
| ISS-192 | Nhắc tới | Trùng với DEC-130 | — | Nhóm D. Dùng chung; không quy định hành vi M12 |
| ISS-193 | Nhắc tới | Trùng với DEC-131 | — | Nhóm D. Dùng chung; không quy định hành vi M12 |
| ISS-194 | Nhắc tới | Trùng với DEC-132 | — | Nhóm D. Dùng chung; không quy định hành vi M12 |
| ISS-195 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M12 |
| ISS-196 | Nhắc tới | Trùng với QA-255 | — | Nhóm D. Dùng chung; không quy định hành vi M12 |
| ISS-197 | Nhắc tới | Trùng với DEC-134 | — | Nhóm D. Dùng chung; không quy định hành vi M12 |
| ISS-198 | Nhắc tới | Trùng với DEC-135 | — | Nhóm D. Dùng chung; không quy định hành vi M12 |
| ISS-199 | Nhắc tới | Trùng với DEC-136 | — | Nhóm D. Dùng chung; không quy định hành vi M12 |
| ISS-200 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M12 |
| ISS-201 | Nhắc tới | Trùng với QA-260 | — | Nhóm D. Dùng chung; không quy định hành vi M12 |
| ISS-202 | Nhắc tới | Trùng với QA-261 | — | Nhóm D. Dùng chung; không quy định hành vi M12 |
| ISS-203 | Nhắc tới | Trùng với QA-263 | — | Nhóm D. Dùng chung; không quy định hành vi M12 |
| ISS-204 | Nhắc tới | Trùng với DEC-138 | — | Nhóm D. Dùng chung; không quy định hành vi M12 |
| QA-249 | Nhắc tới | Trùng với DEC-128 | — | Nhóm D. Dùng chung; không quy định hành vi M12 |
| QA-250 | Nhắc tới | Trùng với DEC-129 | — | Nhóm D. Dùng chung; không quy định hành vi M12 |
| QA-251 | Nhắc tới | Trùng với DEC-130 | — | Nhóm D. Dùng chung; không quy định hành vi M12 |
| QA-252 | Nhắc tới | Trùng với DEC-131 | — | Nhóm D. Dùng chung; không quy định hành vi M12 |
| QA-253 | Nhắc tới | Trùng với DEC-132 | — | Nhóm D. Dùng chung; không quy định hành vi M12 |
| QA-255 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M12 |
| QA-256 | Nhắc tới | Trùng với DEC-134 | — | Nhóm D. Dùng chung; không quy định hành vi M12 |
| QA-258 | Nhắc tới | Trùng với DEC-136 | — | Nhóm D. Dùng chung; không quy định hành vi M12 |
| QA-260 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M12 |
| QA-261 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M12 |
| QA-262 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M12 |
| QA-263 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M12 |
| QA-264 | Nhắc tới | Trùng với DEC-138 | — | Nhóm D. Dùng chung; không quy định hành vi M12 |
| MR-A05 | Nhắc tới | Trùng với DEC-137 | — | Nhóm D. Dùng chung; không quy định hành vi M12 |
| DEC-241 | Sở hữu | Hiện hành | FR-M12-02, FR-M12-02.19, FR-M12-02.20, FR-M12-02.21, FR-M12-02.22, BR-M12-08, BR-M12-09 | Nhóm A. Trừ điểm bình luận: tự xóa trừ ngay; AI ẩn ≥ 0,9 trừ ngay; 0,5–< 0,9 trừ khi Mod kết luận vi phạm |
| DEC-242 | Sở hữu | Hiện hành | FR-M12-04, FR-M12-04.01, FR-M12-04.03, FR-M12-04.10, FR-M12-04.11, FR-M12-04.14, FR-M12-04.18, FR-M12-05, FR-M12-05.08, FR-M12-06, FR-M12-06.02, FR-M12-06.04 và 7 yêu cầu khác | Nhóm A. Tab Tuần, Tháng hiện bảng đã chốt của chu kỳ vừa qua; mốc tuần, tháng; Toàn thời gian 60 phút; ẩn người bị loại sau chốt |
| DEC-243 | Sở hữu | Hiện hành | FR-M12-04, FR-M12-04.02, FR-M12-04.15, FR-M12-04.16, FR-M12-05, FR-M12-05.02, FR-M12-05.09, FR-M12-06, FR-M12-06.08, FR-M12-06.09, FR-M12-06.11, FR-M12-06.12 và 6 yêu cầu khác | Nhóm A. Điểm chu kỳ theo thời điểm upvote; chỉ điểm > 0; lọc Lớp/Khối đánh lại hạng; nội dung dòng |
| DEC-244 | Sở hữu | Sửa một phần bởi DEC-247 | FR-M12-05, FR-M12-05.12, FR-M12-06.11, BR-M12-24, BR-M12-29 | Nhóm A. Danh hiệu hiện trên hồ sơ (M02) và dấu trên tab Tuần |
| DEC-245 | Sở hữu | Hiện hành | FR-M12-08, FR-M12-08.08, FR-M12-08.09, FR-M12-08.10, BR-M12-28 | Nhóm A. Danh sách bị từ chối, vẫn chạy, vẫn hiển thị khi cờ Gamification tắt |
| DEC-246 | Sở hữu | Hiện hành | FR-M12-01.10, FR-M12-03, FR-M12-03.10, FR-M12-03.12, FR-M12-04, FR-M12-04.10, FR-M12-04.11, FR-M12-04.12, FR-M12-04.17, FR-M12-04.19, FR-M12-05, FR-M12-05.10 và 10 yêu cầu khác | Nhóm A. Danh sách xác nhận: Khóa toàn bộ, thứ tự đồng hạng, HEAVY/BANNED lúc chốt, tài khoản đã xóa, vô hiệu hóa, mốc điểm, chốt tháng |
| QA-434 | Sở hữu | Trùng với DEC-241 | — | Nhóm A. Câu trả lời ở bước 6 FR M12; nội dung ghi ở DEC-241 |
| QA-435 | Sở hữu | Trùng với DEC-241 | — | Nhóm A. Câu trả lời ở bước 6 FR M12; nội dung ghi ở DEC-241 |
| QA-436 | Sở hữu | Trùng với DEC-242 | — | Nhóm A. Câu trả lời ở bước 6 FR M12; nội dung ghi ở DEC-242 |
| QA-437 | Sở hữu | Trùng với DEC-243 | — | Nhóm A. Câu trả lời ở bước 6 FR M12; nội dung ghi ở DEC-243 |
| QA-438 | Sở hữu | Trùng với DEC-243 | — | Nhóm A. Câu trả lời ở bước 6 FR M12; nội dung ghi ở DEC-243 |
| QA-439 | Sở hữu | Trùng với DEC-244 | — | Nhóm A. Câu trả lời ở bước 6 FR M12; nội dung ghi ở DEC-244 |
| QA-440 | Sở hữu | Trùng với DEC-243 | — | Nhóm A. Câu trả lời ở bước 6 FR M12; nội dung ghi ở DEC-243 |
| QA-441 | Sở hữu | Trùng với DEC-243 | — | Nhóm A. Câu trả lời ở bước 6 FR M12; nội dung ghi ở DEC-243 |
| QA-442 | Sở hữu | Trùng với DEC-245 | — | Nhóm A. Câu trả lời ở bước 6 FR M12; nội dung ghi ở DEC-245 |
| QA-443 | Sở hữu | Trùng với DEC-246 | — | Nhóm A. Câu trả lời ở bước 6 FR M12; nội dung ghi ở DEC-246 |
| ISS-372 | Sở hữu | Trùng với DEC-241 | — | Nhóm A. Câu hỏi ở bước 6 FR M12; xem DEC-241 |
| ISS-373 | Sở hữu | Trùng với DEC-241 | — | Nhóm A. Câu hỏi ở bước 6 FR M12; xem DEC-241 |
| ISS-374 | Sở hữu | Trùng với DEC-242 | — | Nhóm A. Câu hỏi ở bước 6 FR M12; xem DEC-242 |
| ISS-375 | Sở hữu | Trùng với DEC-243 | — | Nhóm A. Câu hỏi ở bước 6 FR M12; xem DEC-243 |
| ISS-376 | Sở hữu | Trùng với DEC-243 | — | Nhóm A. Câu hỏi ở bước 6 FR M12; xem DEC-243 |
| ISS-377 | Sở hữu | Trùng với DEC-244 | — | Nhóm A. Câu hỏi ở bước 6 FR M12; xem DEC-244 |
| ISS-378 | Sở hữu | Trùng với DEC-243 | — | Nhóm A. Câu hỏi ở bước 6 FR M12; xem DEC-243 |
| ISS-379 | Sở hữu | Trùng với DEC-243 | — | Nhóm A. Câu hỏi ở bước 6 FR M12; xem DEC-243 |
| ISS-380 | Sở hữu | Trùng với DEC-245 | — | Nhóm A. Câu hỏi ở bước 6 FR M12; xem DEC-245 |
| ISS-381 | Sở hữu | Trùng với DEC-246 | — | Nhóm A. Câu hỏi ở bước 6 FR M12; xem DEC-246 |
| DEC-247 | Sở hữu | Hiện hành | FR-M12-05, FR-M12-05.12, FR-M12-05.13, BR-M12-24 | Nhóm A. Hồ sơ chỉ hiện danh hiệu tuần vừa chốt; lịch sử chỉ lưu; chỉ huy hiệu hiện vĩnh viễn |
| QA-444 | Sở hữu | Trùng với DEC-247 | — | Nhóm A. Câu trả lời ở bước 7 FR M12; nội dung ghi ở DEC-247 |
| ISS-382 | Sở hữu | Trùng với DEC-247 | — | Nhóm A. Câu hỏi ở bước 7 FR M12; xem DEC-247 |

### C.2 Chuỗi quyết định

| Chuỗi | Nội dung hiện hành |
|---|---|
| DM-4.3, DEC-004 → QA-040 → DEC-116 | Điểm = 2 × số upvote bài nhận được + 1 × số upvote bình luận nhận được. Phần "điểm = tổng upvote thuần túy" của QA-040 bị thay. Điểm không giảm theo thời gian (QA-047). |
| DM-9.1, GL:Reputation → QA-040, DEC-116, DEC-169, DEC-090 | Nguồn điểm chỉ còn upvote bài và upvote bình luận. Accepted Answer, "contribution milestones", "community contribution" của draft hết hiệu lực. "Rule/configuration" chỉ còn nghĩa: hằng số đổi bằng triển khai, không chỉnh qua giao diện. |
| DM-9.2, GL:Badge → QA-040 → QA-194, QA-195 → DEC-114 (QA-207) | Huy hiệu chỉ theo tổng điểm, 5 mốc: Người mới nổi 25, Cây bút triển vọng 100, Cây bút tích cực 300, Chuyên gia cộng đồng 600, Huyền thoại iShare 1000. Vĩnh viễn, không thu hồi, hiện ngày đạt, mỗi huy hiệu một bản ghi lịch sử; không hiện tiến độ trước khi đạt. Nhóm và ví dụ huy hiệu của draft, ví dụ "10 upvotes" của QA-040 hết hiệu lực. |
| DM-1.3 → DEC-090 | Quyền "Manage badges" của draft hết hiệu lực: danh sách và mốc huy hiệu là hằng số, đổi bằng triển khai. |
| QA-040 → QA-041 → DEC-117, DEC-123 → DEC-243, DEC-244, DEC-246 → DEC-247 (DEC-114, DEC-121) | Danh hiệu "Ngôi sao tuần" chỉ cho chu kỳ tuần; trao lúc chốt tuần cho người có điểm tuần > 0 và hạng 1–3, hòa ở hạng 3 đều nhận, có thể ít hơn 3 người hoặc không ai; mỗi lần đạt một bản ghi, lịch sử chỉ lưu, không hiển thị ("remain permanently visible" của DEC-121 hiểu là lưu, theo QA-202 "vẫn giữ"). Hồ sơ chỉ hiện danh hiệu khi đạt ở tuần vừa chốt, tới lần chốt sau; tab Tuần hiện dấu cạnh tên người nhận. Chỉ huy hiệu theo mốc điểm hiện vĩnh viễn. Chốt tháng không trao gì, không thông báo. |
| DM-9.4, GL:Leaderboard → QA-038, QA-039 → QA-047 → DEC-116, DEC-121, DEC-123 → DEC-242, DEC-243, DEC-246 (DEC-052, DEC-127) | Ba tab: Tuần, Tháng hiện bảng đã chốt của tuần, tháng vừa kết thúc (tính một lần khi chốt, không hiện chu kỳ đang chạy, không xem chu kỳ cũ hơn); Toàn thời gian tính lại mỗi 60 phút. Tuần từ 00:00 thứ Hai, tháng từ 00:00 ngày mùng 1, giờ Việt Nam. Điểm chu kỳ theo thời điểm upvote, chỉ upvote còn hiệu lực trên nội dung chưa bị trừ điểm lúc tính, không âm; bảng đã chốt không đổi. Chỉ người có điểm > 0 được xếp hạng. Đồng hạng chung thứ hạng, hiện theo username A–Z. Lọc Lớp/Khối 10, 11, 12, Tất cả: đánh lại thứ hạng trong nhóm lọc, Lớp/Khối lấy lúc chốt. Mỗi dòng: thứ hạng, avatar, tên kèm username, điểm chu kỳ, dấu danh hiệu (tab Tuần), nhãn đã xóa; tải 20 dòng mỗi lần cuộn. Chu kỳ năm của draft đã bỏ. |
| DEC-079 → DEC-118, DEC-122, MR-M12 → DEC-242, DEC-246 (QA-236) | Người ở mức HEAVY, tài khoản BANNED, tài khoản DEACTIVATED bị loại khỏi bảng xếp hạng trong thời gian đó; xét tại lúc tính, lúc chốt; ai trở thành bị loại sau lúc chốt bị ẩn dòng trên bảng đã chốt, người khác giữ hạng; điểm vẫn tích, trở lại hiện đủ. Người HEAVY/BANNED lúc chốt tuần không nhận danh hiệu, không chiếm suất. Mức cảnh cáo vẫn riêng tư ở mọi nơi khác; LIGHT, MEDIUM không bị ảnh hưởng. BANNED: hồ sơ, bài, bình luận vẫn hiện, có nhãn "Tài khoản đã bị khóa" ở mọi nơi tên xuất hiện (cả Trending). |
| QA-020 → DEC-079 | Chỉ báo cảnh cáo công khai của QA-020 bị bỏ: cảnh cáo riêng tư. |
| DEC-105 → DEC-113 → DEC-184, DEC-231, DEC-241 (DEC-161, DEC-180, DEC-115) | Trừ điểm khi nội dung mất do trực tiếp: tác giả tự xóa bài (trừ lúc bài chuyển "Đã xóa hẳn" sau 7 ngày, khôi phục trước đó thì không trừ); tác giả tự xóa bình luận (trừ ngay); Mod/Admin hệ thống gỡ vì vi phạm (bài Bị ẩn, bình luận Ẩn: trừ ngay); AI tự ẩn bình luận ≥ 0,9 (trừ ngay); bình luận bị AI ẩn 0,5–< 0,9 (trừ lúc Mod kết luận vi phạm, không trừ nếu không vi phạm). Không trừ khi gián tiếp: nhóm bị Owner xóa, rời hoặc bị kick, gỡ khỏi nhóm, bình luận bị ẩn theo bài cha. Khiếu nại bài bị gỡ được chấp nhận thì hoàn điểm; bình luận không có khiếu nại. |
| DEC-043 → DEC-179 | Bình luận chỉ xóa mềm, không có khôi phục; nội dung giữ vĩnh viễn. |
| DEC-041 (ISS-072, QA-094), DEC-119, DEC-120 | Chỉ có upvote; upvote là bật/tắt, rút lại thì trừ điểm ngay; không tự upvote nội dung của mình. |
| DM-4.1, DM-1.2, DM-9.3, QA-067 → DEC-169, DEC-173 | Hồ sơ hiện điểm, huy hiệu (M02 hiển thị). Stars nhận, stars cho không hiện trên hồ sơ; "Accepted answers received" hết hiệu lực. |
| QA-011, DEC-126 | Guest xem được bảng xếp hạng, huy hiệu, điểm; mọi tương tác (upvote) cần đăng nhập. |
| QA-018 → DEC-019 → DEC-149, DEC-156 → DEC-246 | Upvote đã cho của tài khoản đã xóa vẫn tính cho người nhận. Tài khoản bị xóa sau lúc chốt vẫn hiện mờ trên bảng tuần, tháng đang hiển thị với nhãn "[Người dùng đã xóa]" (thay "[Tài khoản đã xóa]" của QA-018) cho tới lần chốt sau; Toàn thời gian loại từ lần tính kế tiếp; huy hiệu không hiển thị. Phần bình luận của QA-018 thay bởi DEC-149. |
| DEC-033 → DEC-167 → DEC-246 | Khóa toàn bộ chặn mọi thao tác upvote: upvote mới và rút lại upvote, trên bài và trên mọi bình luận của bài. |
| DEC-102, DEC-108 → DEC-231, DEC-234 | Owner, Group Mod, Member vote trong nhóm; người ngoài đã đăng nhập vote bài nhóm Public; nhóm chuyển Private thì người ngoài không vote được bài đang hiện. |
| DEC-066 → DEC-216; DEC-065 → DEC-180, DEC-231, DEC-246 | Thông báo upvote gộp theo từng bài, từng bình luận, cửa sổ 5 phút; bỏ upvote không đổi thông báo đã gửi. Huy hiệu và danh hiệu tuần chỉ thông báo trong ứng dụng; "mốc điểm" là đạt huy hiệu, không có thông báo mốc điểm riêng. |
| DEC-092 → DEC-225, DEC-228 → DEC-245 | Cờ tính năng Gamification, khởi tạo Bật. Khi tắt: upvote, rút upvote, mở bảng xếp hạng của người không phải Admin bị từ chối ("Hệ thống đang bận, vui lòng thử lại sau"), nút và lối vào vẫn hiện; vẫn chạy trừ, hoàn điểm, trao huy hiệu, tính Toàn thời gian, chốt tuần, tháng, trao danh hiệu, thông báo; vẫn hiển thị số upvote, điểm, huy hiệu, danh hiệu, nhãn bị khóa; dữ liệu giữ nguyên, bật lại không bù; Admin dùng bình thường. |
| DEC-052 → DEC-145; QA-106 → DEC-145 | Câu "tuần của leaderboard là tuần lịch cố định" của DEC-052 dùng cho M12, với mốc 00:00 thứ Hai của DEC-242; công thức Trending thuộc M05. |
| DEC-019, DEC-065, DEC-079, DEC-089, DEC-090, DEC-092, DEC-115, DEC-122, DEC-156, DEC-161, DEC-180, DEC-225, QA-011, QA-017 → DEC-148, DEC-147, DEC-151, DEC-215, DEC-218, DEC-221, DEC-237, DEC-163, DEC-188, DEC-211, DEC-199, DEC-201, DEC-141, DEC-224, DEC-152, DEC-226, DEC-198, DEC-200, DEC-202, ISS-154, DEC-159, DEC-185, DEC-236, DEC-171, DEC-206, DEC-208, DEC-203 | Các sửa đổi này không chạm phần M12 dùng: thêm sự kiện thông báo khác; hạn chế đăng bài, thử thách nối tiếp, giảm hạng tìm kiếm của HEAVY; chi tiết lật ban, nhật ký Mod, Topic; tạm dừng đăng ký, banner; phạm vi và danh sách khiếu nại; dữ liệu bị xóa khác; quét lại bài; bình luận bị ẩn không hiện lại; cờ Group; quyền Guest xem hồ sơ, tóm tắt AI, tìm kiếm; vòng phản hồi AI. ISS-154 → DEC-122 là cạnh tool đọc nhầm (bác bỏ ở bước 2). |
| DEC-079 → MR-M12 | Dòng module M12 của registry ghi lại phần bảng xếp hạng của DEC-079 (người ở mức HEAVY bị loại khỏi bảng xếp hạng), đã có ở BR-M12-20; không đổi hành vi (rà soát chéo 2026-10-24). |
| DEC-225 → DEC-256 | Danh sách khi cờ Chat tắt thuộc M16; không chạm M12. Danh sách khi cờ Gamification tắt của M12 theo DEC-245 (BR-M12-28). |
| DEC-231 → DEC-270 | Không đổi hành vi M12: bài bị gỡ khỏi nhóm giữ trạng thái đăng, gỡ khỏi nhóm vẫn không trừ điểm. |
