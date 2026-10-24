---
module: M04
ten_module: Comment
ma_tai_lieu: FR-M04
phien_ban: 1.4
trang_thai: Đã chốt
ngay: 2026-10-24
tac_gia: Phạm Văn Đức
moc_nguon: DEC-271, QA-477, ISS-415, OPEN-012
steps_completed: [1, 2, 3, 4, 5, 6, 7]
---
# Tài liệu yêu cầu chức năng — M04 Comment

| Mã tài liệu | FR-M04 |
|---|---|
| Dự án | iShare |
| Module | M04 — Comment |
| Trạng thái | Đã chốt |
| Phiên bản | 1.4 |
| Ngày | 2026-10-24 |
| Tác giả | Phạm Văn Đức |

<!-- Quy ước chung cho mọi bảng dưới đây:
     - Thân tài liệu không ghi nguồn. Nguồn của mọi ID nằm ở Phụ lục A.
     - Ô không có nội dung ghi "—". Không xóa cột.
     - Mục chưa tới bước làm thì để dòng "(Chưa làm — bước N)". -->

## 1. Tổng quan

### 1.1 Mục đích

Bình luận cho phép người dùng phản hồi một bài viết và trả lời nhau ngay dưới bài: viết bình luận, trả lời, sửa, xóa,
nhắc tên và báo cáo. Bình luận được tổ chức thành luồng hai cấp, soạn bằng trình soạn tối giản (có công thức toán và
trích dẫn), chỉ nhận upvote để đánh giá mức độ hữu ích của một phản hồi.

### 1.2 Phạm vi

**Trong phạm vi:**

- Viết bình luận gốc dưới bài và trả lời bình luận theo luồng hai cấp (bình luận gốc và trả lời); trả lời một trả lời
  được đưa vào cùng luồng.
- Trình soạn bình luận tối giản: in đậm, in nghiêng, code trong dòng, công thức LaTeX, liên kết, nhắc tên, trích dẫn.
  Nội dung tối đa 1.000 từ, không được trống.
- Trích dẫn khi trả lời: phía trên mỗi trả lời hiển thị một dòng trích bình luận được trả lời; dòng này chỉ để hiển thị,
  không thuộc nội dung trả lời.
- Xem danh sách bình luận của bài, sắp xếp Top (mặc định), Mới nhất, Cũ nhất; trả lời luôn theo thứ tự thời gian
  từ cũ đến mới. Số bình luận của bài.
- Sửa bình luận không giới hạn thời gian, nhãn "(đã chỉnh sửa)", không lưu lịch sử sửa; các trường hợp không được sửa.
- Xóa bình luận: với người dùng là vĩnh viễn, không khôi phục; hệ thống chỉ gắn cờ đã xóa và giữ nội dung. Bình luận
  gốc còn trả lời để lại dấu "[Bình luận đã bị xóa]".
- Quy định phản ứng trên bình luận chỉ có upvote, không có downvote; sắp xếp Top dựa trên số upvote.
- Trạng thái kiểm duyệt của bình luận (Bình thường, Bị ẩn) và cách luồng hiển thị bình luận bị ẩn.
- Chủ bình luận xem lại, chỉ đọc, bình luận của mình đã bị ẩn hoặc đã bị xử lý khi mở từ thông báo hoặc khiếu nại
  (mở rộng phạm vi đã được chấp nhận).

**Ngoài phạm vi:**

- Danh sách gợi ý nhắc tên, thời điểm gửi thông báo nhắc tên; cách hiển thị tác giả bình luận khi tài khoản vô hiệu hóa
  hoặc đã xóa — M01 Authentication & Account. Avatar, tên hiển thị của tác giả — M02 User Profile.
- Khóa bình luận và khóa toàn bộ bài (chặn bình luận mới) — M03 Post & Content; M04 chỉ tuân theo mức khóa. Xóa bài,
  thời hạn khôi phục bài — M03.
- Thông báo bình luận mới, trả lời, nhắc tên, upvote bình luận, "Bình luận của bạn đã bị ẩn"; tắt thông báo theo bài —
  M07 Notification.
- Báo cáo bình luận (kể cả nút báo cáo trên bình luận), quét AI bình luận theo tốc độ trả lời, Mod, Admin ẩn bình luận,
  Mod, Admin xem nội dung bình luận đã xóa trong báo cáo và lịch sử báo cáo, chặn bình luận ở mức cảnh cáo nặng —
  M08 Moderation. Công tắc AI Moderation — M10 Admin Panel.
- Khiếu nại cảnh cáo, ban; bình luận không có khiếu nại riêng — M09 Appeal.
- Bình luận trong nhóm (quyền theo thành viên nhóm, Owner, Group Mod gỡ bình luận khỏi nhóm, nhóm chuyển Private, nhóm Bị khóa) — M11 Group.
- Thao tác upvote bình luận (upvote, rút lại, chặn tự vote), điểm Comment Star, trừ điểm khi bình luận bị xóa —
  M12 Gamification.
- Ngưỡng AI và xử lý khi AI lỗi — M13 AI Layer.
- Tìm kiếm (bình luận không được tìm kiếm) — M06 Search. Trending và xếp hạng dùng số bình luận — M05, M06, M14.
  Thống kê bình luận — M15 Analytics & Stats.
- Đã quyết không làm: đính kèm trong bình luận; downvote; lồng sâu hơn hai cấp; lịch sử sửa bình luận; khôi phục bình
  luận đã xóa; xóa hẳn bình luận; khiếu nại bình luận; Mod, Admin xóa bình luận (chỉ có ẩn); Accepted Answer ở MS1;
  Tag cho bình luận; tóm tắt luồng bình luận bằng AI; AI tự viết bình luận.

## 2. Thuật ngữ và viết tắt

### 2.1 Thuật ngữ

| Thuật ngữ | Định nghĩa |
|---|---|
| Bình luận | Phản hồi do người dùng đã đăng nhập viết dưới một bài viết. Gồm hai loại: bình luận gốc và trả lời. |
| Bình luận gốc | Bình luận gắn trực tiếp vào bài viết, mở đầu một luồng bình luận. |
| Trả lời | Bình luận viết để đáp một bình luận gốc hoặc một trả lời khác; luôn thuộc luồng của một bình luận gốc. |
| Luồng bình luận | Một bình luận gốc cùng mọi trả lời thuộc nó. Luồng chỉ có hai cấp. |
| Bình luận được trả lời | Bình luận (gốc hoặc trả lời) mà người dùng bấm "Trả lời" trên đó khi viết một trả lời. |
| Trích dẫn khi trả lời | Một dòng hệ thống hiển thị phía trên trả lời, gồm tên tác giả và phần đầu nội dung hiện tại của bình luận được trả lời. Chỉ để hiển thị, không thuộc nội dung trả lời. |
| Tác giả bình luận | Người dùng đã đăng nhập (User, Mod hoặc Admin) đã viết bình luận. Cũng gọi là chủ bình luận. |
| Nội dung bình luận | Phần chữ tác giả bình luận tự viết trong trình soạn, kể cả khối trích dẫn tác giả tự gõ; không gồm trích dẫn khi trả lời. |
| Từ | Đơn vị đếm độ dài nội dung bình luận: một cụm chữ ngăn cách bởi khoảng trắng, đếm trên phần chữ người đọc thấy của nội dung bình luận (cùng cách đếm với bài viết). |
| Thời điểm đăng | Lúc hệ thống ghi nhận bình luận được gửi. Bình luận hiển thị ngay từ lúc này (không quét trước). Sửa bình luận không đổi thời điểm đăng. |
| Thời điểm sửa | Lúc hệ thống ghi nhận lần sửa gần nhất của bình luận. |
| Nhãn "(đã chỉnh sửa)" | Nhãn hiện trên bình luận đã được tác giả sửa ít nhất một lần. |
| Bình luận đã xóa | Bình luận đã được tác giả xóa: hệ thống gắn cờ đã xóa, không hiển thị nội dung trong luồng, nhưng vẫn giữ nội dung. Không khôi phục được. |
| Dấu "[Bình luận đã bị xóa]" | Nội dung thay thế hiện ở vị trí của bình luận gốc đã xóa hoặc đang bị ẩn khi bình luận đó còn ít nhất một trả lời đang hiển thị. |
| Số upvote của bình luận | Số người dùng đang upvote bình luận tại thời điểm xem (upvote đã rút lại không tính). Thao tác upvote thuộc M12. |
| Trạng thái kiểm duyệt của bình luận | Một trong hai giá trị: Bình thường, Bị ẩn. Do việc quét AI và Mod, Admin quyết định (M08). |
| Bình luận bị ẩn | Bình luận ở trạng thái kiểm duyệt Bị ẩn. Trong luồng không ai thấy nội dung của nó, kể cả tác giả. |
| Bình luận hiển thị bình thường | Bình luận chưa bị xóa và ở trạng thái kiểm duyệt Bình thường. |
| Số bình luận của bài | Số bình luận gốc và trả lời đang hiển thị bình thường của bài; không tính dấu "[Bình luận đã bị xóa]" và bình luận bị ẩn. |
| Thông báo xử lý | Thông báo kết quả xử lý báo cáo gửi cho người vi phạm (M08) và thông báo "Bình luận của bạn đã bị ẩn" khi AI ẩn bình luận (M07). |
| Khóa bình luận, Khóa toàn bộ | Mức khóa của bài viết (M03). Cả hai mức chặn bình luận mới trên bài; Khóa toàn bộ còn chặn upvote và rút upvote trên bài và trên mọi bình luận của bài (M03, M12). |
| Mức cảnh cáo HEAVY | Mức cảnh cáo nặng nhất (5–6 lần cảnh cáo, M08); trong thời gian thử thách, người dùng không tạo được bình luận mới. |

### 2.2 Viết tắt

| Viết tắt | Đầy đủ |
|---|---|
| FR | Functional Requirement — yêu cầu chức năng |

## 3. Thông tin đầu vào

### 3.1 Tài liệu đầu vào

| Tài liệu | Phiên bản / mốc |
|---|---|
| Draft: docs/_temp/iShare_modules.md, iShare_specs_general.md | Theo ngày sửa tệp |
| Register: decisions, qa-log, issue-queue, open-issues, glossary, module-registry | DEC-271, QA-477, ISS-415, OPEN-012 (khớp `moc_nguon`) |

### 3.2 Tài liệu liên quan

| Module | Liên quan ở điểm nào |
|---|---|
| M01 Authentication & Account | Nhắc tên trong bình luận; hiển thị bình luận của tài khoản vô hiệu hóa, đã xóa. |
| M02 User Profile | Avatar, tên hiển thị của tác giả bình luận. |
| M03 Post & Content | Bình luận gắn với bài; mức khóa của bài chặn bình luận mới; bình luận giữ cùng bài khi bài bị xóa. |
| M05 Topic & Tag | Trending Topic/Tag đếm bình luận (gồm trả lời). |
| M06 Search | Bình luận không được tìm kiếm; xếp hạng bài dùng số bình luận. |
| M07 Notification | Thông báo bình luận mới, trả lời, nhắc tên, upvote bình luận, bình luận bị ẩn; tắt thông báo theo bài. |
| M08 Moderation | Báo cáo bình luận, quét AI sau khi đăng, Mod, Admin ẩn bình luận, xem nội dung đã xóa trong báo cáo, hạn chế bình luận theo mức cảnh cáo. |
| M09 Appeal | Không có khiếu nại cho bình luận; chủ bình luận xem lại bình luận từ khiếu nại cảnh cáo, ban liên quan. |
| M10 Admin Panel | Công tắc AI tổng và công tắc Moderation (gồm quét bình luận). |
| M11 Group | Bình luận trong nhóm dùng chung cơ chế, thêm quyền theo vai trò nhóm. |
| M12 Gamification | Upvote bình luận, điểm Comment Star, trừ điểm khi bình luận bị xóa hoặc bị ẩn, nhãn tài khoản bị khóa. |
| M13 AI Layer | Ngưỡng tự ẩn bình luận, xử lý khi AI lỗi. |
| M14 Feed & Discovery | Trending Post dùng số bình luận. |
| M15 Analytics & Stats | Xu hướng bình luận theo thời gian. |

## 4. Tổng quan chức năng

### 4.1 Luật, tiêu chuẩn liên quan

Không có.

### 4.2 Vai trò

| Vai trò | Mô tả trong module này |
|---|---|
| Guest | Người chưa đăng nhập. Xem bình luận của bài đang hiển thị công khai. Không viết, trả lời, sửa, xóa hay tương tác gì khác với bình luận. |
| User | Người dùng đã đăng nhập. Xem, viết bình luận, trả lời bình luận; khi là tác giả bình luận thì sửa, xóa, xem lại bình luận của mình theo các điều kiện ở mục 5. |
| Mod | Có mọi quyền của User trong module này. Ẩn bình luận của người khác và xem nội dung bình luận đã xóa trong báo cáo thuộc M08. |
| Admin | Có các quyền của Mod trong module này. |
| Tác giả bình luận | Vai trò theo ngữ cảnh: User, Mod hoặc Admin đang sửa, xóa bình luận (bình luận gốc hoặc trả lời) của chính mình, hoặc xem lại bình luận của mình đã bị ẩn, đã bị xử lý. |

### 4.3 Ma trận quyền

| Hành động | Guest | User | Mod | Admin | Yêu cầu |
|---|---|---|---|---|---|
| Xem bình luận của bài đang hiển thị công khai | ✓ | ✓ | ✓ | ✓ | FR-M04-01.01, FR-M04-01.02 |
| Viết bình luận gốc vào bài | ✗ | ✓ | ✓ | ✓ | FR-M04-02.01, FR-M04-02.05 |
| Trả lời bình luận (gốc hoặc trả lời) | ✗ | ✓ | ✓ | ✓ | FR-M04-03.02, FR-M04-03.03, FR-M04-03.06 |
| Sửa bình luận | ✗ | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | FR-M04-04.01, FR-M04-04.07 |
| Xóa bình luận | ✗ | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | FR-M04-05.01, FR-M04-05.02, FR-M04-05.03, FR-M04-05.05 |
| Xem bình luận đang bị ẩn trong luồng | ✗ | ✗ | ✗ | ✗ | FR-M04-01.09 |
| Xem lại bình luận bị ẩn, bị xử lý từ thông báo hoặc khiếu nại | ✗ | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | FR-M04-06.01, FR-M04-06.02, FR-M04-06.03, FR-M04-06.05 |
| Sửa, xóa bình luận của mình khi đang ở mức cảnh cáo HEAVY | ✗ | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | FR-M04-04.11, FR-M04-05.09 |
| Sửa bình luận của mình khi bài đang bị Khóa bình luận hoặc Khóa toàn bộ | ✗ | ✗ | ✗ | ✗ | FR-M04-04.09 |
| Xóa bình luận của mình khi bài đang bị Khóa bình luận hoặc Khóa toàn bộ | ✗ | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | FR-M04-05.08 |
| Sửa, xóa bình luận của mình đang bị ẩn | ✗ | ✗ | ✗ | ✗ | FR-M04-04.10, FR-M04-05.10 |

<!-- Ô nói thẳng: hàng 1 cột Guest (QA-011 "COMT: Xem comment"); hàng 2–5 cột User (DM-1.3 "Create / edit / delete comment",
     DM-4.2); hàng 4–5 "của mình" (DEC-043 "author can edit"); hàng 6 (DEC-180: không ai thấy trong luồng, kể cả tác giả);
     hàng 7 (DEC-179, DEC-180); hàng 8–11 (DEC-178).
     Ô suy ra: hàng 1 các cột còn lại (Guest xem được thì vai trò cao hơn cũng xem được); cột Guest ở hàng 2–11 (QA-011 "INTR: Không",
     QA-227 mọi tương tác cần đăng nhập); cột Mod/Admin ở hàng 2–3 (Mod, Admin có quyền của User, DM-1.3); cột Mod/Admin ở hàng 4–5, 7–11
     chỉ "của mình": với bình luận người khác, Mod, Admin chỉ có thao tác Ẩn (DEC-180, M08) và xem nội dung đã xóa qua báo cáo,
     lịch sử báo cáo, khiếu nại (DEC-179, M08, M09).
     Điều kiện chặn không theo vai trò: bài bị khóa chặn bình luận mới và trả lời (DEC-033, DEC-167); mức cảnh cáo HEAVY
     không được tạo bình luận mới (DEC-079, DEC-178); bài trong nhóm theo quyền nhóm (M11). -->

### 4.4 Danh sách chức năng

| ID | Chức năng | Tác nhân chính | Kích hoạt |
|---|---|---|---|
| FR-M04-01 | Xem bình luận của bài viết | Guest, User, Mod, Admin | Người xem mở bài viết, hoặc đổi cách sắp xếp bình luận |
| FR-M04-02 | Viết bình luận vào bài viết | User, Mod, Admin | Người dùng nhập nội dung vào ô bình luận dưới bài và gửi |
| FR-M04-03 | Trả lời bình luận | User, Mod, Admin | Người dùng bấm "Trả lời" trên một bình luận gốc hoặc một trả lời |
| FR-M04-04 | Sửa bình luận | Tác giả bình luận | Tác giả chọn sửa trên bình luận của mình |
| FR-M04-05 | Xóa bình luận | Tác giả bình luận | Tác giả chọn xóa trên bình luận của mình |
| FR-M04-06 | Xem lại bình luận đã bị xử lý của mình | Tác giả bình luận | Tác giả mở thông báo xử lý về bình luận của mình, hoặc mở khiếu nại của mình liên quan tới bình luận đó |

### 4.5 Mốc và ưu tiên

Toàn bộ yêu cầu của module thuộc MS1, ưu tiên **Must** (bảng MoSCoW Summary của module-registry: Must gồm M01–M10, M13;
cột MoSCoW ở dòng M04 của bảng Module List bị lệch nên không dùng). Không có yêu cầu ngoại lệ về ưu tiên.

## 5. Yêu cầu chức năng

### 5.1 FR-M04-01 Xem bình luận của bài viết

**Yêu cầu cấp trên:** Hệ thống phải cho phép mọi người xem được một bài viết đang hiển thị công khai xem các luồng bình luận của bài, sắp xếp theo cách người xem chọn.

**Lý do:** Cho Guest xem bài viết và bình luận là quyết định quan trọng về SEO và khả năng được tìm thấy: nội dung iShare được công cụ tìm kiếm lập chỉ mục, tạo lượt truy cập tự nhiên.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M04-01.01 | Khi người xem mở một bài đang hiển thị công khai, hệ thống phải hiển thị các bình luận gốc của bài, mỗi bình luận gốc kèm các trả lời thuộc luồng của nó. |
| FR-M04-01.02 | Hệ thống phải cho Guest xem bình luận của bài đang hiển thị công khai mà không cần đăng nhập. |
| FR-M04-01.03 | Khi người xem mở bình luận của bài, hệ thống phải sắp xếp bình luận gốc theo cách Top. |
| FR-M04-01.04 | Khi người xem chọn cách sắp xếp Top, Mới nhất hoặc Cũ nhất, hệ thống phải sắp xếp lại bình luận gốc theo cách đó (BR-M04-05). |
| FR-M04-01.05 | Hệ thống phải xếp trả lời trong mỗi luồng theo thời điểm đăng từ cũ đến mới với cả ba cách sắp xếp (BR-M04-06). |
| FR-M04-01.06 | Hệ thống phải hiển thị nhãn "(đã chỉnh sửa)" trên bình luận đã được tác giả sửa ít nhất một lần. |
| FR-M04-01.07 | Hệ thống phải hiển thị dấu "[Bình luận đã bị xóa]" ở vị trí của bình luận gốc đã xóa hoặc đang bị ẩn khi bình luận đó còn ít nhất một trả lời đang hiển thị bình thường. |
| FR-M04-01.08 | Nếu bình luận được trả lời của một trả lời đã xóa hoặc đang bị ẩn, hệ thống phải hiển thị "trả lời [bình luận đã bị xóa]" ở chỗ dòng trích dẫn của trả lời đó. |
| FR-M04-01.09 | Trong khi bình luận ở trạng thái Bị ẩn, hệ thống phải không hiển thị nội dung bình luận đó trong luồng cho bất kỳ ai, kể cả tác giả bình luận. |
| FR-M04-01.10 | Hệ thống phải hiển thị trên bài viết số bình luận của bài tính theo BR-M04-18, như nhau với mọi người xem. |
| FR-M04-01.11 | Nếu người xem không xem được bài viết, hệ thống phải không hiển thị bình luận của bài cho người đó. |
| FR-M04-01.12 | Khi một bài không hiển thị trở lại hiển thị, hệ thống phải hiển thị lại các bình luận chưa bị xóa của bài như trước. |
| FR-M04-01.13 | Trong khi bài ở mức Khóa bình luận hoặc Khóa toàn bộ, hệ thống phải tiếp tục hiển thị các bình luận đã có của bài. |
| FR-M04-01.14 | Khi sắp xếp theo cách Top, hệ thống phải xếp các bình luận gốc cùng số upvote theo thời điểm đăng, bình luận đăng trước đứng trước. |
| FR-M04-01.15 | Khi một bình luận gốc đang hiện dấu "[Bình luận đã bị xóa]" không còn trả lời nào hiển thị bình thường, hệ thống phải bỏ dấu đó khỏi luồng. |
| FR-M04-01.16 | Hệ thống phải hiển thị phía trên mỗi trả lời một dòng trích dẫn gồm tên tác giả và nội dung hiện tại của bình luận được trả lời. |
| FR-M04-01.17 | Nếu nội dung bình luận được trả lời dài hơn một dòng, hệ thống phải chỉ hiển thị phần đầu vừa một dòng trong dòng trích dẫn. |

### 5.2 FR-M04-02 Viết bình luận vào bài viết

**Yêu cầu cấp trên:** Hệ thống phải cho phép người dùng đã đăng nhập viết bình luận gốc vào bài viết đang hiển thị bằng trình soạn tối giản và hiển thị bình luận ngay khi gửi.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M04-02.01 | Khi người dùng đã đăng nhập gửi bình luận gốc trên một bài đang hiển thị với họ, hệ thống phải lưu bình luận vào bài với tác giả là người gửi và thời điểm đăng là lúc gửi. |
| FR-M04-02.02 | Khi bình luận gốc được gửi, hệ thống phải hiển thị bình luận ngay ở trạng thái kiểm duyệt Bình thường, không quét trước khi hiển thị. |
| FR-M04-02.03 | Hệ thống phải cung cấp trong trình soạn bình luận đúng các định dạng: in đậm, in nghiêng, code trong dòng, công thức LaTeX, liên kết, nhắc tên, trích dẫn. |
| FR-M04-02.04 | Hệ thống phải không cung cấp đính kèm tệp trong trình soạn bình luận. |
| FR-M04-02.05 | Nếu người gửi chưa đăng nhập, hệ thống phải từ chối bình luận. |
| FR-M04-02.06 | Nếu bài đang ở mức Khóa bình luận hoặc Khóa toàn bộ, hệ thống phải từ chối bình luận gốc mới trên bài. |
| FR-M04-02.07 | Nếu người gửi đang ở mức cảnh cáo HEAVY, hệ thống phải từ chối bình luận gốc mới. |
| FR-M04-02.08 | Nếu bài không tồn tại hoặc không hiển thị với người gửi, hệ thống phải từ chối bình luận. |
| FR-M04-02.09 | Khi nội dung đang soạn vượt 1.000 từ, hệ thống phải hiển thị cảnh báo ngay, kèm số từ hiện tại so với giới hạn. |
| FR-M04-02.10 | Nếu nội dung dài hơn 1.000 từ, hệ thống phải từ chối gửi bình luận và giữ nguyên nội dung trong trình soạn. |
| FR-M04-02.11 | Nếu nội dung trống hoặc chỉ có khoảng trắng, hệ thống phải từ chối gửi bình luận. |

### 5.3 FR-M04-03 Trả lời bình luận

**Yêu cầu cấp trên:** Hệ thống phải cho phép người dùng đã đăng nhập trả lời một bình luận gốc hoặc một trả lời đang hiển thị, giữ luồng ở hai cấp và ghi nhận bình luận được trả lời để hiển thị trích dẫn.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M04-03.01 | Khi người dùng bấm "Trả lời" trên một bình luận gốc hoặc một trả lời đang hiển thị bình thường, hệ thống phải mở trình soạn trả lời và ghi nhận bình luận đó là bình luận được trả lời. |
| FR-M04-03.02 | Khi người dùng gửi trả lời cho một bình luận gốc, hệ thống phải lưu trả lời vào luồng của bình luận gốc đó, với bình luận được trả lời là bình luận gốc. |
| FR-M04-03.03 | Khi người dùng gửi trả lời cho một trả lời, hệ thống phải lưu trả lời mới vào luồng của bình luận gốc chứa trả lời đó, cùng cấp với các trả lời khác, với bình luận được trả lời là trả lời đó. |
| FR-M04-03.04 | Khi trả lời được gửi, hệ thống phải hiển thị trả lời ngay ở trạng thái kiểm duyệt Bình thường, không quét trước khi hiển thị. |
| FR-M04-03.05 | Hệ thống phải cung cấp trong trình soạn trả lời cùng các định dạng của trình soạn bình luận ở BR-M04-01, không có đính kèm tệp. |
| FR-M04-03.06 | Nếu người gửi chưa đăng nhập, hệ thống phải từ chối trả lời. |
| FR-M04-03.07 | Nếu bài đang ở mức Khóa bình luận hoặc Khóa toàn bộ, hệ thống phải từ chối trả lời mới trên bài. |
| FR-M04-03.08 | Nếu người gửi đang ở mức cảnh cáo HEAVY, hệ thống phải từ chối trả lời mới. |
| FR-M04-03.09 | Nếu bài không tồn tại hoặc không hiển thị với người gửi, hệ thống phải từ chối trả lời. |
| FR-M04-03.10 | Nếu bình luận được trả lời đã xóa hoặc đang bị ẩn, kể cả bình luận gốc đang hiện dấu "[Bình luận đã bị xóa]", hệ thống phải từ chối trả lời. |
| FR-M04-03.11 | Trong khi bình luận gốc của một luồng đang hiện dấu "[Bình luận đã bị xóa]", hệ thống phải cho người dùng trả lời các trả lời đang hiển thị bình thường của luồng. |
| FR-M04-03.12 | Hệ thống phải áp cho nội dung trả lời cùng giới hạn, cảnh báo và từ chối về độ dài, nội dung trống như bình luận gốc (BR-M04-19). |
| FR-M04-03.13 | Hệ thống phải không tính dòng trích dẫn của bình luận được trả lời vào nội dung và độ dài của trả lời. |

### 5.4 FR-M04-04 Sửa bình luận

**Yêu cầu cấp trên:** Hệ thống phải cho phép tác giả sửa nội dung bình luận của mình không giới hạn thời gian và đánh dấu bình luận đã được sửa, trừ các trường hợp bị chặn.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M04-04.01 | Khi tác giả lưu nội dung sửa của bình luận của mình, hệ thống phải thay nội dung bình luận bằng nội dung mới. |
| FR-M04-04.02 | Khi tác giả lưu nội dung sửa, hệ thống phải ghi thời điểm sửa là lúc lưu, thay cho thời điểm sửa trước đó. |
| FR-M04-04.03 | Khi tác giả lưu nội dung sửa, hệ thống phải giữ nguyên thời điểm đăng, vị trí trong luồng và trạng thái kiểm duyệt của bình luận. |
| FR-M04-04.04 | Hệ thống phải không lưu nội dung trước khi sửa của bình luận và không cung cấp chức năng xem lịch sử sửa bình luận. |
| FR-M04-04.05 | Hệ thống phải cho tác giả sửa bình luận của mình không giới hạn thời gian kể từ thời điểm đăng và không giới hạn số lần. |
| FR-M04-04.06 | Khi tác giả sửa bình luận, hệ thống phải dùng trình soạn có cùng các định dạng ở BR-M04-01, không có đính kèm tệp. |
| FR-M04-04.07 | Nếu người sửa khác tác giả bình luận, hệ thống phải từ chối thao tác sửa. |
| FR-M04-04.08 | Nếu bình luận đã xóa, hệ thống phải từ chối thao tác sửa. |
| FR-M04-04.09 | Nếu bài chứa bình luận đang ở mức Khóa bình luận hoặc Khóa toàn bộ, hệ thống phải từ chối thao tác sửa. |
| FR-M04-04.10 | Nếu bình luận đang ở trạng thái Bị ẩn, hệ thống phải từ chối thao tác sửa. |
| FR-M04-04.11 | Trong khi tác giả ở mức cảnh cáo HEAVY, hệ thống phải cho tác giả sửa bình luận đã có của mình. |
| FR-M04-04.12 | Khi nội dung đang sửa vượt 1.000 từ, hệ thống phải hiển thị cảnh báo ngay, kèm số từ hiện tại so với giới hạn. |
| FR-M04-04.13 | Nếu nội dung sửa dài hơn 1.000 từ, trống hoặc chỉ có khoảng trắng, hệ thống phải từ chối lưu bản sửa và giữ nguyên nội dung trong trình soạn. |

### 5.5 FR-M04-05 Xóa bình luận

**Yêu cầu cấp trên:** Hệ thống phải cho phép tác giả xóa bình luận của mình; với người dùng việc xóa là vĩnh viễn, còn hệ thống chỉ gắn cờ đã xóa và giữ nội dung.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M04-05.01 | Khi tác giả xóa bình luận gốc của mình còn ít nhất một trả lời đang hiển thị bình thường, hệ thống phải gắn cờ đã xóa và hiển thị dấu "[Bình luận đã bị xóa]" ở vị trí bình luận, giữ nguyên các trả lời. |
| FR-M04-05.02 | Khi tác giả xóa bình luận gốc của mình không còn trả lời nào hiển thị bình thường, hệ thống phải gắn cờ đã xóa và bỏ bình luận khỏi luồng. |
| FR-M04-05.03 | Khi tác giả xóa một trả lời của mình, hệ thống phải gắn cờ đã xóa và bỏ trả lời khỏi luồng. |
| FR-M04-05.04 | Hệ thống phải không cung cấp khôi phục bình luận đã xóa. |
| FR-M04-05.05 | Nếu người xóa khác tác giả bình luận, hệ thống phải từ chối thao tác xóa của tác giả. |
| FR-M04-05.06 | Nếu bình luận đã xóa, hệ thống phải từ chối xóa lại. |
| FR-M04-05.07 | Hệ thống phải giữ nội dung của bình luận đã xóa và không xóa hẳn bình luận. |
| FR-M04-05.08 | Trong khi bài chứa bình luận ở mức Khóa bình luận hoặc Khóa toàn bộ, hệ thống phải cho tác giả xóa bình luận của mình trên bài. |
| FR-M04-05.09 | Trong khi tác giả ở mức cảnh cáo HEAVY, hệ thống phải cho tác giả xóa bình luận đã có của mình. |
| FR-M04-05.10 | Nếu bình luận đang ở trạng thái Bị ẩn, hệ thống phải từ chối thao tác xóa của tác giả. |
| FR-M04-05.11 | Khi bài chứa bình luận bị xóa, kể cả khi hết thời hạn khôi phục của bài, hệ thống phải giữ các bình luận của bài cùng bài và không xóa riêng bình luận. |

### 5.6 FR-M04-06 Xem lại bình luận đã bị xử lý của mình

**Yêu cầu cấp trên:** Hệ thống phải cho phép tác giả bình luận xem lại, chỉ đọc, bình luận của mình đã bị ẩn hoặc đã bị xử lý sau báo cáo, khi mở từ thông báo xử lý hoặc từ khiếu nại của mình.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M04-06.01 | Khi tác giả mở thông báo "Bình luận của bạn đã bị ẩn", hệ thống phải hiển thị nội dung bình luận đó ở chế độ chỉ đọc kèm nhãn cho biết bình luận đang bị ẩn. |
| FR-M04-06.02 | Khi tác giả mở thông báo kết quả xử lý báo cáo về bình luận của mình, hệ thống phải hiển thị nội dung bình luận đó ở chế độ chỉ đọc, kể cả khi bình luận đang bị ẩn hoặc đã bị tác giả xóa. |
| FR-M04-06.03 | Khi tác giả mở khiếu nại của mình liên quan tới một bình luận của mình, hệ thống phải hiển thị nội dung bình luận đó ở chế độ chỉ đọc. |
| FR-M04-06.04 | Hệ thống phải không hiển thị cho tác giả danh tính, lý do đã chọn, mô tả hay bằng chứng của người báo cáo. |
| FR-M04-06.05 | Nếu người mở khác tác giả bình luận, hệ thống phải từ chối hiển thị nội dung bình luận bị ẩn hoặc đã xóa qua các đường xem lại này. |

### 5.7 Quy tắc nghiệp vụ

| ID | Loại | Quy tắc | Ví dụ |
|---|---|---|---|
| BR-M04-01 | Ràng buộc | Trình soạn bình luận chỉ có các định dạng: in đậm, in nghiêng, code trong dòng, công thức LaTeX, liên kết, nhắc tên, trích dẫn. Không có tiêu đề mục, bảng, danh sách việc cần làm. | — |
| BR-M04-02 | Sự kiện | Bình luận không có tệp đính kèm; muốn chia sẻ tệp thì đăng bài viết. | — |
| BR-M04-03 | Ràng buộc | Luồng bình luận có hai cấp: bình luận gốc gắn trực tiếp vào bài; trả lời thuộc một bình luận gốc. Trả lời viết trên một trả lời được đưa vào luồng của bình luận gốc chứa trả lời đó, cùng cấp với các trả lời khác, không tạo cấp thứ ba. | A là bình luận gốc; B trả lời A; C bấm "Trả lời" trên B → C thuộc luồng A, cùng cấp với B, xếp sau B (BR-M04-06), bình luận được trả lời của C là B. |
| BR-M04-04 | Ràng buộc | Trích dẫn khi trả lời chỉ để hiển thị: phía trên mỗi trả lời, hệ thống hiển thị một dòng gồm tên tác giả và phần đầu nội dung hiện tại của bình luận được trả lời (không gồm các dòng trích dẫn mà bình luận đó hiển thị). Dòng trích dẫn không thuộc nội dung trả lời. Bình luận được trả lời đã xóa hoặc đang bị ẩn thì thay bằng "trả lời [bình luận đã bị xóa]". | B của X: "Dùng định lý Pytago là ra. Cạnh huyền bằng 5 vì 3² + 4² = 25 …". Y trả lời B → phía trên trả lời của Y hiện một dòng "X: Dùng định lý Pytago là ra. Cạnh huyền bằng 5…". X sửa B → dòng trích dẫn hiện nội dung mới. Z trả lời Y → dòng trích dẫn chỉ có phần Y viết, không có dòng trích B. X xóa B → trả lời của Y hiện "trả lời [bình luận đã bị xóa]". |
| BR-M04-05 | Ràng buộc | Bình luận gốc của một bài được sắp xếp theo một trong ba cách do người xem chọn: Top (mặc định) — số upvote giảm dần, cùng số upvote thì bình luận đăng trước đứng trước; Mới nhất — thời điểm đăng giảm dần; Cũ nhất — thời điểm đăng tăng dần. | Ba bình luận gốc: A (đăng 09:00, 5 upvote), B (09:10, 2 upvote), C (09:20, 5 upvote). Top: A, C, B (A và C cùng 5 upvote, A đăng trước). Mới nhất: C, B, A. Cũ nhất: A, B, C. |
| BR-M04-06 | Ràng buộc | Trả lời trong một luồng luôn xếp theo thời điểm đăng từ cũ đến mới, với cả ba cách sắp xếp bình luận gốc. | Luồng A có trả lời B (10:00, 7 upvote) và D (10:05, 0 upvote). Ở Top, Mới nhất và Cũ nhất đều hiện B rồi D. |
| BR-M04-07 | Ràng buộc | Tác giả sửa bình luận của mình không giới hạn thời gian và số lần. Bình luận đã được sửa ít nhất một lần hiện nhãn "(đã chỉnh sửa)". Hệ thống chỉ ghi thời điểm sửa gần nhất; không lưu nội dung trước khi sửa và không có chức năng xem lịch sử sửa. | Bình luận đăng 01/10 09:00, sửa lúc 01/10 09:05 và 20/10 21:00: cả hai lần sửa được chấp nhận; nhãn hiện từ 01/10 09:05; thời điểm sửa ghi 20/10 21:00; thời điểm đăng vẫn là 01/10 09:00. |
| BR-M04-08 | Suy diễn | Tác giả xóa bình luận: với người dùng là vĩnh viễn, không khôi phục; hệ thống gắn cờ đã xóa và giữ nội dung. Hiển thị trong luồng: (a) bình luận gốc còn ít nhất một trả lời hiển thị bình thường → dấu "[Bình luận đã bị xóa]", các trả lời giữ nguyên; (b) bình luận gốc không còn trả lời hiển thị bình thường → bỏ khỏi luồng; (c) trả lời → bỏ khỏi luồng, các trả lời có bình luận được trả lời là nó hiện "trả lời [bình luận đã bị xóa]". Dấu của bình luận gốc mất khỏi luồng khi luồng không còn trả lời hiển thị bình thường. | Luồng A có B, C (C trả lời B). Xóa A → A hiện "[Bình luận đã bị xóa]", B và C còn nguyên. Xóa B → B mất khỏi luồng, C hiện "trả lời [bình luận đã bị xóa]". Xóa tiếp C → luồng không còn trả lời hiển thị, dấu của A mất khỏi luồng. Bình luận gốc E không có trả lời: xóa E → E mất khỏi luồng. Nội dung A, B, C, E vẫn được giữ. |
| BR-M04-09 | Sự kiện | Phản ứng duy nhất trên bình luận là upvote; không có downvote hay phản ứng khác. Nội dung không phù hợp được xử lý bằng báo cáo (M08). | — |
| BR-M04-10 | Sự kiện | Bình luận không có Topic hay Tag riêng; bình luận thuộc ngữ cảnh Topic, Tag của bài chứa nó. | — |
| BR-M04-11 | Sự kiện | MS1 không có Accepted Answer: không có thao tác đánh dấu một bình luận là câu trả lời tốt nhất. | — |
| BR-M04-12 | Ràng buộc | Bình luận hiển thị ngay khi được gửi, không qua bước quét trước khi đăng. Việc quét bình luận sau khi đăng thuộc M08; bình luận của Admin không bị quét và không báo cáo được (M08). | — |
| BR-M04-13 | Ràng buộc | Bình luận đang Bị ẩn không hiển thị nội dung trong luồng cho ai, kể cả tác giả. Bình luận gốc Bị ẩn còn ít nhất một trả lời hiển thị bình thường hiện dấu "[Bình luận đã bị xóa]" như bình luận đã xóa; trả lời Bị ẩn không hiện, các trả lời có bình luận được trả lời là nó hiện "trả lời [bình luận đã bị xóa]". | Bình luận gốc A của X bị ẩn, có trả lời B, C của người khác: X, Y và Guest đều thấy dấu ở chỗ A và thấy B, C. Trả lời D của X bị ẩn: không ai thấy D; trả lời E trả lời D hiện "trả lời [bình luận đã bị xóa]". |
| BR-M04-14 | Ràng buộc | Trong khi bài ở mức Khóa bình luận hoặc Khóa toàn bộ, không ai tạo được bình luận gốc hay trả lời mới trên bài; bình luận đã có vẫn hiển thị. | — |
| BR-M04-15 | Ràng buộc | Người đang ở mức cảnh cáo HEAVY không tạo được bình luận gốc hay trả lời; mức LIGHT và MEDIUM vẫn bình luận được. | X ở mức MEDIUM (3 lần cảnh cáo): viết bình luận → được. Y ở mức HEAVY (5 lần cảnh cáo): viết bình luận hoặc trả lời → bị từ chối. |
| BR-M04-16 | Ràng buộc | Guest chỉ xem bình luận; viết, trả lời, sửa, xóa bình luận đều cần đăng nhập. | — |
| BR-M04-17 | Suy diễn | Bình luận chỉ được xem cùng bài chứa nó: người xem không xem được bài thì cũng không xem được bình luận của bài; khi bài hiển thị lại, các bình luận chưa bị xóa hiển thị lại như trước. | Bài P có 4 bình luận, tác giả tự ẩn P: Guest mở đường dẫn P → không thấy P, không thấy bình luận. Tác giả hiện lại P → 4 bình luận hiện lại. |
| BR-M04-18 | Tính toán | Số bình luận của bài = số bình luận gốc + số trả lời đang hiển thị bình thường. Không tính dấu "[Bình luận đã bị xóa]" và bình luận bị ẩn. Mọi người xem thấy cùng một số. | Bài có: bình luận gốc A đang hiện dấu, với trả lời B, C; bình luận gốc D với trả lời E đang bị ẩn; bình luận gốc F. Số bình luận = B, C, D, F = 4. |
| BR-M04-19 | Ràng buộc | Nội dung bình luận gốc và trả lời tối đa 1.000 từ và không được trống hoặc chỉ có khoảng trắng; áp khi gửi và khi lưu bản sửa. Vượt giới hạn trong lúc soạn thì cảnh báo ngay, kèm số từ hiện tại so với giới hạn; gửi hoặc lưu khi đang vượt thì bị từ chối, nội dung trong trình soạn được giữ. Dòng trích dẫn khi trả lời không tính; khối trích dẫn tác giả tự gõ có tính. | Bình luận 1.000 từ → gửi được. 1.001 từ → hiện cảnh báo "1.001/1.000", gửi bị từ chối, chữ còn nguyên. Trả lời 950 từ cho một bình luận 900 từ → gửi được (dòng trích dẫn không tính). Bình luận chỉ có ba dấu cách → từ chối. |
| BR-M04-20 | Ràng buộc | Tác giả sửa, xóa bình luận của mình theo điều kiện: bài đang Khóa bình luận hoặc Khóa toàn bộ → không sửa, được xóa; tác giả ở mức cảnh cáo HEAVY → được sửa và xóa (chỉ chặn tạo bình luận mới); bình luận đang Bị ẩn → không sửa, không xóa. | Bài P bị Mod khóa bình luận: X sửa bình luận của mình trên P → từ chối; X xóa → được. X ở mức HEAVY: sửa lỗi chính tả bình luận cũ → được. Bình luận B của X bị AI ẩn: X không thấy B trong luồng, không sửa, không xóa được. |
| BR-M04-21 | Sự kiện | Bình luận không bao giờ bị xóa hẳn. Khi bài bị xóa, kể cả khi hết thời hạn khôi phục của bài, bình luận của bài được giữ cùng bài. Mod, Admin chỉ xem nội dung bình luận đã xóa trong ngữ cảnh kiểm duyệt của chính bình luận đó: báo cáo đang mở, lịch sử báo cáo của bình luận, khiếu nại (M08, M09); không có chỗ duyệt hay tìm kiếm bình luận đã xóa. | X xóa bình luận B sau khi Y báo cáo B → Mod mở báo cáo vẫn xem được nội dung B. |
| BR-M04-22 | Ràng buộc | Tác giả bình luận chỉ xem lại bình luận của mình đang bị ẩn hoặc đã bị xử lý sau báo cáo khi mở từ thông báo xử lý hoặc từ khiếu nại của mình, ở chế độ chỉ đọc; không thấy danh tính, lý do đã chọn, mô tả hay bằng chứng của người báo cáo. | Y báo cáo bình luận B của X; X xóa B; Mod kết luận vi phạm và cảnh cáo X. X mở thông báo kết quả xử lý → xem được nội dung B và lý do xử lý của Mod, không biết Y báo cáo. |
| BR-M04-23 | Sự kiện | Với bình luận của người khác, Mod, Admin chỉ có thao tác Ẩn (chuyển sang Bị ẩn, M08); không có thao tác xóa. Bình luận không có khiếu nại riêng (M09). | — |

### 5.8 Dữ liệu nghiệp vụ

| Thực thể | Thuộc tính nguồn đã nêu | Quan hệ |
|---|---|---|
| Bình luận | Nội dung (định dạng theo BR-M04-01, tối đa 1.000 từ); tác giả; bài chứa bình luận; bình luận gốc của luồng (với trả lời); bình luận được trả lời (với trả lời); thời điểm đăng; thời điểm sửa gần nhất; trạng thái kiểm duyệt (Bình thường, Bị ẩn); cờ đã xóa (nội dung vẫn giữ) | Thuộc một Bài viết (M03); có một tác giả là Tài khoản (M01); trả lời thuộc một bình luận gốc và trỏ tới một bình luận được trả lời; nhận nhiều upvote (M12); chứa lượt nhắc tên (M01); có thể bị báo cáo (M08) |

<!-- Số bình luận của bài (draft DM-2.1 "Comment count") là giá trị đếm theo BR-M04-18, hiện trên Bài viết (M03).
     Số upvote của bình luận lấy từ M12. "Bình luận được trả lời" suy ra từ DEC-043 và dùng cho dòng trích dẫn (DEC-183).
     Dòng trích dẫn khi trả lời không phải thuộc tính lưu của trả lời: được dựng từ bình luận được trả lời lúc hiển thị (DEC-183). -->

**Ma trận CRUD:**

| Thực thể | Tạo | Đọc | Sửa | Xóa |
|---|---|---|---|---|
| Bình luận | FR-M04-02.01, FR-M04-03.02, FR-M04-03.03 | FR-M04-01.01, FR-M04-06.01, FR-M04-06.02, FR-M04-06.03; Mod, Admin xem bình luận đã xóa: M08 (BR-M04-21) | FR-M04-04.01 (nội dung); trạng thái kiểm duyệt: M08 | Gắn cờ đã xóa: FR-M04-05.01, FR-M04-05.02, FR-M04-05.03; xóa hẳn: Không có (BR-M04-21, FR-M04-05.07); Mod, Admin: Không có, chỉ Ẩn (BR-M04-23); theo bài: giữ cùng bài (FR-M04-05.11) |

### 5.9 Chuyển trạng thái

#### Bình luận

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Người dùng gửi bình luận gốc hoặc trả lời | Đã đăng nhập; bài đang hiển thị và không bị khóa; người gửi không ở mức HEAVY; nội dung hợp lệ (BR-M04-19) | Bình thường | FR-M04-02.02, FR-M04-03.04 |
| Bình thường | Quét AI (M08) cho điểm ≥ 0,9 | — | Bị ẩn | M08; FR-M04-01.09 |
| Bình thường | Quét AI (M08) cho điểm từ 0,5 đến dưới 0,9; bình luận vào hàng chờ Mod | — | Bị ẩn | M08; FR-M04-01.09 |
| Bị ẩn | Mod, Admin xem xét bình luận đang chờ và kết luận không vi phạm (M08) | Bình luận vào hàng chờ với điểm từ 0,5 đến dưới 0,9 | Bình thường | M08; FR-M04-01.01 |
| Bình thường | Mod, Admin ẩn bình luận khi xử lý báo cáo (M08) | — | Bị ẩn | M08; FR-M04-01.09 |
| Bình thường | Tác giả xóa | Người xóa là tác giả | Đã xóa | FR-M04-05.01, FR-M04-05.02, FR-M04-05.03 |

<!-- Đã xóa là trạng thái cuối: không khôi phục (FR-M04-05.04), không xóa hẳn (FR-M04-05.07).
     Bị ẩn do điểm ≥ 0,9 hoặc do Mod ẩn khi xử lý báo cáo là trạng thái cuối: bình luận không có khiếu nại (DEC-115, DEC-180);
     bình luận không hiện lại khi cảnh cáo, ban liên quan bị lật trên khiếu nại (DEC-201, M09).
     Bị ẩn → Đã xóa không có: tác giả không xóa được bình luận đang bị ẩn (FR-M04-05.10).
     Bị ẩn → Bình thường suy ra từ DEC-098 "hold for mod review".
     Sửa nội dung không đổi trạng thái kiểm duyệt (DEC-077: sửa không tự kích hoạt quét lại).
     Dấu "[Bình luận đã bị xóa]" là cách hiển thị (BR-M04-08, BR-M04-13), không phải trạng thái. -->

### 5.10 Giao tiếp với module khác

| Hướng | Module | Nội dung ở mức nghiệp vụ | Yêu cầu |
|---|---|---|---|
| Cung cấp | M01 | Lưu, sửa, xóa bình luận chứa lượt nhắc tên (lượt nhắc đi theo bình luận); bình luận hiển thị công khai ngay khi gửi, là mốc gửi thông báo nhắc tên | FR-M04-02.01, FR-M04-02.02, FR-M04-03.04, FR-M04-04.01, FR-M04-05.02, FR-M04-05.03 |
| Cung cấp | M07 | Sự kiện có bình luận gốc mới trên bài, có trả lời vào một bình luận; nơi mở bình luận bị ẩn từ thông báo "Bình luận của bạn đã bị ẩn" và thông báo xử lý | FR-M04-02.01, FR-M04-03.02, FR-M04-03.03, FR-M04-06.01, FR-M04-06.02 |
| Cung cấp | M08 | Bình luận và luồng bình luận để báo cáo và quét AI sau khi đăng (bình luận của Admin không bị quét, không báo cáo được, DEC-195); trạng thái kiểm duyệt Bình thường, Bị ẩn; nội dung bình luận đã xóa được giữ để Mod, Admin xem trong báo cáo, lịch sử báo cáo | FR-M04-02.02, FR-M04-03.04, FR-M04-01.09, FR-M04-05.07 |
| Cung cấp | M09 | Nơi chủ bình luận xem lại bình luận từ khiếu nại cảnh cáo, ban liên quan; nội dung bình luận đã xóa được giữ để xét khiếu nại | FR-M04-06.03, FR-M04-05.07 |
| Cung cấp | M12 | Bình luận là đối tượng của upvote bình luận; thời điểm tác giả xóa bình luận (mốc trừ điểm) | FR-M04-05.01, FR-M04-05.02, FR-M04-05.03 |
| Cung cấp | M05, M06, M14 | Bình luận (gồm trả lời) với thời điểm đăng và việc bị xóa, dùng cho Trending và xếp hạng; bình luận không được tìm kiếm | FR-M04-02.01, FR-M04-03.02, FR-M04-05.02 |
| Cung cấp | M15 | Bình luận mới theo thời gian để thống kê | FR-M04-02.01 |
| Dùng | M01 | Cách hiển thị tác giả bình luận theo trạng thái tài khoản (vô hiệu hóa, đã xóa); danh sách gợi ý và thông báo nhắc tên | — |
| Dùng | M02 | Avatar, tên hiển thị của tác giả bình luận | — |
| Dùng | M03 | Bài đang hiển thị với người xem; mức khóa của bài (Khóa toàn bộ chặn cả upvote bình luận, M12); bài bị xóa (bình luận giữ cùng bài) | FR-M04-01.11, FR-M04-01.13, FR-M04-02.06, FR-M04-03.07, FR-M04-04.09, FR-M04-05.08, FR-M04-05.11 |
| Dùng | M07 | Gửi thông báo bình luận mới, trả lời, nhắc tên, upvote bình luận, "Bình luận của bạn đã bị ẩn" (chỉ trong ứng dụng); tắt thông báo theo bài | FR-M04-06.01 |
| Dùng | M08 | Quét AI theo tốc độ trả lời và ẩn bình luận; báo cáo bình luận; Mod, Admin ẩn bình luận; thông báo kết quả xử lý; mức cảnh cáo HEAVY | FR-M04-01.09, FR-M04-02.07, FR-M04-03.08, FR-M04-06.02 |
| Dùng | M09 | Khiếu nại cảnh cáo, ban; bình luận không có khiếu nại riêng | FR-M04-06.03 |
| Dùng | M10 | Công tắc AI tổng và công tắc Moderation (gồm quét bình luận) | — |
| Dùng | M11 | Quyền bình luận trong nhóm: thành viên bình luận bài nhóm; người ngoài nhóm đã đăng nhập bình luận bài nhóm Public như bài thường; nhóm Private, kể cả nhóm vừa chuyển Private, chặn bình luận của người ngoài; nhóm Bị khóa chặn bình luận; Owner, Group Mod gỡ bình luận khỏi nhóm (xóa mềm, không trừ điểm, không khiếu nại); người đã rời nhóm Private không sửa, xóa được bình luận của mình trong nhóm | — |
| Dùng | M12 | Số upvote của bình luận (sắp xếp Top); thao tác upvote; nhãn "Tài khoản đã bị khóa" cạnh tên tác giả | FR-M04-01.03, FR-M04-01.04, FR-M04-01.14 |
| Dùng | M13 | Ngưỡng điểm quét, xử lý khi AI lỗi | — |

### 5.11 AI hỗ trợ và hành vi khi tắt AI

Module không gọi AI trực tiếp. Bình luận và trả lời hiển thị ngay khi gửi, không chờ AI (FR-M04-02.02, FR-M04-03.04),
nên việc AI bật, tắt hay lỗi không đổi luồng viết bình luận. Quét bình luận sau khi đăng (chỉ khi luồng vượt ngưỡng tốc độ
trả lời), hành vi khi công tắc Moderation tắt và khi AI lỗi thuộc M08, M13. M04 hiển thị bình luận theo trạng thái kiểm
duyệt (FR-M04-01.09) và cho tác giả xem lại bình luận bị AI ẩn từ thông báo (FR-M04-06.01).

### 5.12 Yêu cầu HMI

Chưa có — chờ giai đoạn thiết kế. Câu chữ của nhãn "bình luận đang bị ẩn" (FR-M04-06.01) chốt ở giai đoạn thiết kế.

### 5.13 Chuyển màn hình

Chưa có — chờ giai đoạn thiết kế.

## 6. Lịch sử sửa đổi

| Phiên bản | Ngày | Nội dung | Người sửa |
|---|---|---|---|
| 0.1 | 2026-10-14 | Tạo mới | Phạm Văn Đức |
| 1.0 | 2026-10-14 | Chốt sau 7 bước; bổ sung DEC-178–183 (xóa mềm, bình luận bị ẩn, giới hạn 1.000 từ, trích dẫn khi trả lời) | Phạm Văn Đức |
| 1.1 | 2026-10-20 | Đối chiếu với FR-M06: ghi chuỗi DEC-208, DEC-211 ở C.2; không đổi yêu cầu. Chốt bản 1.1 | Phạm Văn Đức |
| 1.2 | 2026-10-21 | Đối chiếu với FR-M11 (DEC-231, DEC-234, DEC-235, DEC-237): "Dùng M11" ghi rõ người ngoài bình luận bài nhóm Public, gỡ bình luận khỏi nhóm, nhóm Bị khóa, người đã rời nhóm Private; không đổi yêu cầu. Chốt bản 1.2 | Phạm Văn Đức |
| 1.3 | 2026-10-23 | Rà lại với register tới DEC-247: bình luận của Admin không bị quét, không báo cáo được (DEC-195, BR-M04-12, dòng Cung cấp M08); đóng TBD-M04-01 (DEC-201); ghi chú thời điểm trừ điểm bình luận theo DEC-241, DEC-231. Chốt bản 1.3 | Phạm Văn Đức |
| 1.4 | 2026-10-24 | Rà soát chéo toàn bộ FR (review-cross-module.md): thuật ngữ Khóa toàn bộ và dòng "Dùng M03" ghi thêm việc chặn upvote bình luận (DEC-246); sửa ghi chú C.1 về theo dõi bài; C.2; không đổi yêu cầu. Chốt bản 1.4 | Phạm Văn Đức |

## Phụ lục A. Truy vết

| ID | Nguồn | Căn cứ | Ghi chú |
|---|---|---|---|
| FR-M04-01 | DEC-042, DEC-043, DEC-037, DEC-083, DEC-077, DEC-180, DEC-181, DEC-182, DEC-183, DM-2.1, DM-4.2, QA-011, MR-M04 | Nói thẳng | Lý do lấy từ QA-011 (Traceability note). Số bình luận của bài: DM-2.1 (FR-M03 chuyển sang M04) |
| FR-M04-02 | DM-4.2, DM-1.3, DEC-039, DEC-040, DEC-044, DEC-183, GL:Comment, QA-011, MR-M04 | Nói thẳng | — |
| FR-M04-03 | DM-4.2, DEC-040, DEC-046, DEC-039, DEC-181, DEC-183, QA-032, MR-M04 | Nói thẳng | — |
| FR-M04-04 | DM-4.2, DM-1.3, DEC-043, DEC-037, DEC-178, DEC-183, MR-M04 | Nói thẳng | — |
| FR-M04-05 | DM-4.2, DM-1.3, DEC-043, DEC-178, DEC-179, MR-M04 | Nói thẳng | — |
| FR-M04-06 | DEC-179, DEC-180, DEC-074 | Nói thẳng | Mở rộng phạm vi đã được chấp nhận (Q-13) |
| FR-M04-01.01 | DEC-040, QA-011 | Nói thẳng | — |
| FR-M04-01.02 | QA-011 | Nói thẳng | — |
| FR-M04-01.03 | DEC-042 | Nói thẳng | — |
| FR-M04-01.04 | DEC-042 | Nói thẳng | — |
| FR-M04-01.05 | DEC-042 | Nói thẳng | — |
| FR-M04-01.06 | DEC-043, DEC-037 | Nói thẳng | — |
| FR-M04-01.07 | DEC-043, DEC-181 | Nói thẳng | — |
| FR-M04-01.08 | DEC-043, DEC-181, DEC-183 | Nói thẳng | — |
| FR-M04-01.09 | DEC-180, DEC-083 | Nói thẳng | — |
| FR-M04-01.10 | DM-2.1, DEC-182 | Nói thẳng | — |
| FR-M04-01.11 | DEC-113, QA-011 | Suy ra | DEC-113 "comment cascade-hidden because its parent post was removed" ⇒ bình luận ẩn theo bài; QA-011 cho xem bình luận cùng bài |
| FR-M04-01.12 | DEC-113 | Suy ra | Bình luận chỉ ẩn theo bài, không bị xóa ⇒ hiện lại khi bài hiện lại |
| FR-M04-01.13 | DEC-033, DEC-167 | Suy ra | "blocks new comments" ⇒ chỉ chặn bình luận mới, bình luận đã có vẫn hiện |
| FR-M04-01.14 | DEC-182 | Nói thẳng | — |
| FR-M04-01.15 | DEC-181 | Nói thẳng | — |
| FR-M04-01.16 | DEC-183 | Nói thẳng | — |
| FR-M04-01.17 | DEC-183 | Nói thẳng | — |
| FR-M04-02.01 | DM-1.3, DM-4.2, GL:Comment | Nói thẳng | — |
| FR-M04-02.02 | DEC-077 | Nói thẳng | — |
| FR-M04-02.03 | DEC-039 | Nói thẳng | — |
| FR-M04-02.04 | DEC-044 | Nói thẳng | — |
| FR-M04-02.05 | QA-011, QA-227 | Nói thẳng | — |
| FR-M04-02.06 | DEC-033, DEC-167 | Nói thẳng | — |
| FR-M04-02.07 | DEC-079 | Nói thẳng | — |
| FR-M04-02.08 | DEC-113, QA-011 | Suy ra | Không xem được bài thì không xem được bình luận của bài (BR-M04-17) ⇒ không viết được bình luận vào bài đó |
| FR-M04-02.09 | DEC-183, DEC-164 | Nói thẳng | — |
| FR-M04-02.10 | DEC-183 | Nói thẳng | — |
| FR-M04-02.11 | DEC-183 | Nói thẳng | — |
| FR-M04-03.01 | DEC-046, DEC-183 | Nói thẳng | — |
| FR-M04-03.02 | DEC-040 | Nói thẳng | — |
| FR-M04-03.03 | DEC-040, QA-032, DEC-043 | Suy ra | DEC-040 "appended to same thread" là nói thẳng; "bình luận được trả lời" suy từ DEC-043 (trả lời hiện "trả lời [bình luận đã bị xóa]") |
| FR-M04-03.04 | DEC-077 | Nói thẳng | — |
| FR-M04-03.05 | DEC-039, DEC-044 | Suy ra | Trả lời là bình luận ⇒ dùng chung trình soạn bình luận |
| FR-M04-03.06 | QA-011, QA-227 | Nói thẳng | — |
| FR-M04-03.07 | DEC-033, DEC-167 | Suy ra | Trả lời là bình luận mới ⇒ bị chặn như bình luận mới |
| FR-M04-03.08 | DEC-079 | Suy ra | "Cannot create ... comments" ⇒ trả lời cũng là bình luận nên bị chặn |
| FR-M04-03.09 | DEC-113, QA-011 | Suy ra | Không xem được bài thì không xem được bình luận (BR-M04-17) ⇒ không trả lời được |
| FR-M04-03.10 | DEC-181, DEC-180, DEC-043 | Suy ra | DEC-181 "not to the placeholder" là nói thẳng; bình luận đã xóa, bị ẩn không hiện với ai (DEC-043, DEC-180) ⇒ không còn để trả lời |
| FR-M04-03.11 | DEC-181 | Nói thẳng | — |
| FR-M04-03.12 | DEC-183 | Nói thẳng | — |
| FR-M04-03.13 | DEC-183 | Nói thẳng | — |
| FR-M04-04.01 | DEC-043, DM-1.3 | Nói thẳng | — |
| FR-M04-04.02 | DEC-037 | Suy ra | "edited_at timestamp only" ⇒ một mốc thời gian, là lần sửa gần nhất |
| FR-M04-04.03 | DEC-037, DEC-077 | Suy ra | Thời điểm sửa ghi riêng (DEC-037) ⇒ thời điểm đăng không đổi; "edit alone does not trigger" quét (DEC-077) ⇒ trạng thái kiểm duyệt không đổi |
| FR-M04-04.04 | DEC-037 | Nói thẳng | — |
| FR-M04-04.05 | DEC-043 | Nói thẳng | — |
| FR-M04-04.06 | DEC-039, DEC-044 | Suy ra | Nội dung bình luận theo cùng trình soạn khi viết và khi sửa |
| FR-M04-04.07 | DEC-043 | Suy ra | "author can edit" ⇒ người khác, kể cả Guest, Mod, Admin, bị từ chối |
| FR-M04-04.08 | DEC-043, DEC-179 | Suy ra | Bình luận đã xóa không còn hiển thị và không khôi phục (DEC-179) ⇒ sửa sẽ làm mất tác dụng của việc xóa |
| FR-M04-04.09 | DEC-178 | Nói thẳng | — |
| FR-M04-04.10 | DEC-178 | Nói thẳng | — |
| FR-M04-04.11 | DEC-178 | Nói thẳng | — |
| FR-M04-04.12 | DEC-183, DEC-164 | Nói thẳng | — |
| FR-M04-04.13 | DEC-183 | Nói thẳng | — |
| FR-M04-05.01 | DEC-043, DEC-179, DEC-181 | Nói thẳng | — |
| FR-M04-05.02 | DEC-043, DEC-179, DEC-181 | Nói thẳng | — |
| FR-M04-05.03 | DEC-043, DEC-179 | Nói thẳng | — |
| FR-M04-05.04 | DEC-043, DEC-179 | Nói thẳng | — |
| FR-M04-05.05 | DM-1.3, DM-10.2, DEC-180 | Suy ra | DM-1.3 cho người dùng xóa bình luận (của mình); với bình luận người khác Mod, Admin chỉ có thao tác Ẩn (DEC-180, M08) |
| FR-M04-05.06 | DEC-043 | Suy ra | Bình luận đã xóa đã gắn cờ, không còn hiển thị ⇒ xóa lại không có nghĩa |
| FR-M04-05.07 | DEC-179 | Nói thẳng | — |
| FR-M04-05.08 | DEC-178 | Nói thẳng | — |
| FR-M04-05.09 | DEC-178 | Nói thẳng | — |
| FR-M04-05.10 | DEC-178 | Nói thẳng | — |
| FR-M04-05.11 | DEC-179 | Nói thẳng | — |
| FR-M04-06.01 | DEC-180 | Nói thẳng | — |
| FR-M04-06.02 | DEC-179, DEC-074 | Nói thẳng | — |
| FR-M04-06.03 | DEC-179 | Nói thẳng | — |
| FR-M04-06.04 | DEC-179 | Nói thẳng | — |
| FR-M04-06.05 | DEC-179 | Suy ra | "The content owner can view their own" ⇒ người khác bị từ chối qua đường này; Mod, Admin xem qua M08 |
| BR-M04-01 | DEC-039 | Nói thẳng | — |
| BR-M04-02 | DEC-044 | Nói thẳng | — |
| BR-M04-03 | DEC-040, QA-032 | Nói thẳng | — |
| BR-M04-04 | DEC-183, DEC-181 | Nói thẳng | — |
| BR-M04-05 | DEC-042, DEC-182 | Nói thẳng | — |
| BR-M04-06 | DEC-042 | Nói thẳng | — |
| BR-M04-07 | DEC-043, DEC-037 | Suy ra | "edited_at timestamp only" ⇒ chỉ một mốc thời gian, là lần sửa gần nhất; "anytime, no time limit" ⇒ không giới hạn số lần |
| BR-M04-08 | DEC-043, DEC-179, DEC-181 | Nói thẳng | — |
| BR-M04-09 | DEC-041 | Nói thẳng | — |
| BR-M04-10 | QA-108 | Nói thẳng | — |
| BR-M04-11 | DEC-169 | Nói thẳng | — |
| BR-M04-12 | DEC-077, DEC-195 | Nói thẳng | — |
| BR-M04-13 | DEC-180, DEC-181, DEC-083 | Nói thẳng | — |
| BR-M04-14 | DEC-033, DEC-167 | Suy ra | "blocks new comments" ⇒ trả lời cũng là bình luận mới nên bị chặn; bình luận đã có vẫn hiển thị |
| BR-M04-15 | DEC-079 | Nói thẳng | — |
| BR-M04-16 | QA-011, QA-227 | Nói thẳng | — |
| BR-M04-17 | DEC-113, QA-011 | Suy ra | DEC-113 "comment cascade-hidden because its parent post was removed" ⇒ bình luận ẩn theo bài; bình luận không bị xóa nên hiện lại khi bài hiện lại |
| BR-M04-18 | DEC-182 | Nói thẳng | — |
| BR-M04-19 | DEC-183, DEC-164 | Nói thẳng | — |
| BR-M04-20 | DEC-178 | Nói thẳng | — |
| BR-M04-21 | DEC-179, DEC-076 | Nói thẳng | — |
| BR-M04-22 | DEC-179, DEC-074 | Nói thẳng | — |
| BR-M04-23 | DEC-180, DEC-115 | Nói thẳng | — |

## Phụ lục B. Câu hỏi, giả định và TBD

### B.1 Câu hỏi đã hỏi

| Mã | Loại | Câu hỏi | Trả lời | Ghi vào register |
|---|---|---|---|---|
| Q-01 | Mơ hồ | Người ở mức cảnh cáo HEAVY có sửa, xóa bình luận đã có của mình không? DEC-079 ghi HEAVY "Cannot create posts or comments (read/vote only)": "create" chỉ chặn tạo mới, còn "read/vote only" như chặn cả sửa, xóa. Với bài, DEC-163 cho sửa bài đã đăng ở mức cảnh cáo; với bình luận, nguồn chưa nói. | Có: HEAVY chỉ chặn tạo bình luận mới; vẫn sửa, xóa bình luận đã có. | QA-342, DEC-178 |
| Q-02 | Thiếu chi tiết | Tác giả có sửa, xóa bình luận của mình khi bài đang bị Khóa bình luận hoặc Khóa toàn bộ không? DEC-033, DEC-167 chỉ nói chặn bình luận mới. | Không sửa; được xóa. | QA-342, DEC-178 |
| Q-03 | Thiếu chi tiết | Tác giả có sửa, xóa bình luận đang bị ẩn do kiểm duyệt (chỉ tác giả thấy, DEC-077) không? Nguồn chỉ nói sửa không tự kích hoạt quét lại. | Không sửa, không xóa. Chủ bình luận cũng không thấy bình luận bị ẩn trong luồng; chỉ xem lại khi mở từ thông báo ("làm giống bài"). | QA-342, QA-345, DEC-178, DEC-180 |
| Q-04 | Mơ hồ | Khi sắp xếp Top, hai bình luận gốc cùng số upvote xếp thế nào? DEC-042 chỉ nói "by upvotes". | Bình luận đăng trước đứng trước. | QA-347, DEC-182 |
| Q-05 | Thiếu chi tiết | Bình luận gốc đã xóa và để lại dấu "[Bình luận đã bị xóa]": khi mọi trả lời của luồng cũng bị xóa thì dấu còn giữ hay bình luận gốc bị xóa hẳn? DEC-043 chỉ nói trường hợp còn trả lời. | Dấu mất khỏi luồng khi không còn trả lời hiển thị bình thường; dữ liệu vẫn giữ. | QA-346, DEC-181 |
| Q-06 | Mơ hồ | Số bình luận của bài (DM-2.1 "Comment count") đếm những gì: có tính trả lời, bình luận gốc đã xóa để lại dấu, bình luận bị ẩn không? Người xem khác nhau có thấy số khác nhau không? | Đếm bình luận gốc và trả lời đang hiển thị bình thường; không tính dấu và bình luận bị ẩn; mọi người thấy cùng số. | QA-347, DEC-182 |
| Q-07 | Thiếu chi tiết | Bình luận gốc bị ẩn do kiểm duyệt mà có trả lời: người khác có thấy các trả lời không, và ở chỗ bình luận gốc hiện gì? DEC-077 chỉ nói bình luận bị ẩn chỉ tác giả thấy. | Hiện dấu "[Bình luận đã bị xóa]" ở chỗ bình luận gốc, các trả lời vẫn hiện. | QA-346, DEC-181 |
| Q-08 | Thiếu chi tiết | Khi bài bị xóa hẳn (hết 7 ngày khôi phục, M03), các bình luận của bài bị xóa hẳn theo không? Nguồn chỉ nói bình luận ẩn theo bài (DEC-113). | Giữ bình luận cùng bài, không xóa riêng. Việc bài không còn bị xóa hẳn: OPEN-010 (M03). | QA-344, DEC-179 |
| Q-09 | Mơ hồ | "Mod, Admin xóa bình luận" (DM-10.2, glossary Moderator) là chuyển bình luận sang Bị ẩn (như bài: "gỡ" là Bị ẩn, DEC-161) hay xóa vĩnh viễn như khi tác giả xóa (DEC-043)? DEC-083 chỉ cho bình luận hai trạng thái Bình thường, Bị ẩn. | Mod, Admin chỉ có thao tác Ẩn. Giữ quét AI theo DEC-077. Không có khiếu nại cho bình luận. | QA-345, DEC-180 |
| Q-10 | Thiếu chi tiết | Bình luận, trả lời có yêu cầu nội dung tối thiểu (không được trống) và giới hạn độ dài tối đa không? Nguồn chỉ nêu trình soạn (DEC-039), không nêu giới hạn. | Tối đa 1.000 từ, đếm như bài; không được trống; trích dẫn khi trả lời không tính. | QA-348, DEC-183 |
| Q-11 | Thiếu chi tiết | Người dùng có trả lời được vào luồng có bình luận gốc đã bị xóa và để lại dấu "[Bình luận đã bị xóa]" không? DEC-043 chỉ nói các trả lời cũ giữ nguyên. | Được trả lời các trả lời đang hiển thị; không trả lời trên chính dấu. | QA-346, DEC-181 |
| Q-12 | Cần cân nhắc | Mở rộng phạm vi: xóa bình luận vĩnh viễn (DEC-043) làm báo cáo mất đối tượng (báo cáo chỉ trỏ tới bình luận, DEC-076), người vi phạm thoát kiểm duyệt bằng cách tự xóa. Có đổi sang xóa mềm không? | Có: nội dung báo cáo được chỉ xóa mềm, gắn cờ; Mod, Admin xem qua báo cáo, lịch sử báo cáo, khiếu nại. Bài viết: OPEN-010; nhóm, chat: OPEN-011. | QA-343, DEC-179 |
| Q-13 | Cần cân nhắc | Mở rộng phạm vi: người bị xử lý có xem lại nội dung đã xóa của mình khi khiếu nại hoặc khi nhận kết quả xử lý không? | Có: chỉ chủ nội dung, chỉ đọc, từ thông báo xử lý hoặc khiếu nại; không thấy thông tin người báo cáo. | QA-349, DEC-179 |
| Q-14 | Thiếu chi tiết | Trích dẫn tự chèn khi trả lời (DEC-046) chứa toàn bộ nội dung kể cả trích dẫn lồng bên trong, và có tính vào độ dài không? | Trích dẫn chỉ là phần hiển thị, một dòng, không tính vào độ dài. | QA-348, DEC-183 |

<!-- Bước 2: không có cặp mâu thuẫn nào cần hỏi; các cặp nói khác nhau đều giải được bằng thứ tự ưu tiên (xem C.2). -->

### B.2 TBD

| ID | Nội dung | Ảnh hưởng | Lý do chưa chốt |
|---|---|---|---|
| TBD-M04-01 | (Đã đóng ở phiên bản 1.3 — DEC-201: bình luận bị ẩn vẫn Bị ẩn khi cảnh cáo, ban gắn với nó bị lật) | Thấp | Đã chốt |

### B.3 Cần cân nhắc (ngoài dữ liệu hiện có)

| Mã | Điểm cần cân nhắc | Vì sao cần | Quyết định |
|---|---|---|---|
| CC-01 | Xóa mềm bình luận thay cho xóa vĩnh viễn (Q-12) | Chạm an toàn dữ liệu kiểm duyệt: tự xóa làm báo cáo mất đối tượng | Chấp nhận — DEC-179 |
| CC-02 | Chủ nội dung xem lại nội dung bị xử lý từ thông báo hoặc khiếu nại (Q-13) | Chạm quyền: người bị phạt cần thấy nội dung bị phạt để khiếu nại có căn cứ | Chấp nhận — DEC-179 |

## Phụ lục C. Sổ nguồn

**Owner keywords:** M04, comment, comments, bình luận, reply, replies, child reply, root comment, thread, threading, nesting, quote-reply, quote reply, blockquote, tombstone, Bình luận đã bị xóa, Comment Star, CommentStar, comment sort, Mới nhất, Cũ nhất, comment-thread, comment thread, Người dùng đã xóa, Accepted Answer, Vote retraction, Self-vote, Self-voting, rút lại, Tự vote, Tài khoản tạm thời vô hiệu hoá, mọi tương tác, edited_at
**Dependency keywords:** post, bài viết, notification, thông báo, mention, @mention, upvote, star, report, báo cáo, moderation, kiểm duyệt, velocity, post-scan, warning, cảnh cáo, ban, BANNED, DEACTIVATED, DELETED, lock_level, COMMENT_LOCKED, FULLY_LOCKED, khóa bình luận, search, FTS, trending, summarization, tóm tắt, group, nhóm, anonymous, ẩn danh, points, điểm, appeal, khiếu nại, guest, timezone, AI_ENABLED, AI off, audit log, mute, LaTeX, KaTeX, Tiptap
**Mục draft của module:** DM-4.2 (gồm DM-4.2.1), DM-4.3
**Loại khỏi bảng nguồn (khớp nhầm):** ISS-155, QA-211 ("mới nhất" — tin nhắn chat, M16); QA-340 ("mới nhất" — thứ tự hồ sơ, M02); ISS-158, QA-214 (tombstone tin nhắn chat); ISS-159, QA-217 (nội dung, đính kèm tin nhắn chat); ISS-165, QA-224 (phân trang chat; "QA-097" trích nhầm số); DEC-029, ISS-062 (blockquote của trình soạn bài, M03); QA-003 (dữ liệu demo); DG-1 ("trôi đi như bình luận" theo nghĩa chung); QA-312 (tin nhắn, nhật ký của tài khoản đã xóa); ISS-255, QA-315 ("rút lại" sự đồng ý chính sách); QA-286 (độ trễ Trending)

### C.1 Bảng nguồn

| Nguồn | Nhãn | Trạng thái | Dùng ở | Ghi chú |
|---|---|---|---|---|
| DEC-039 | Sở hữu | Sửa một phần bởi DEC-183 | FR-M04-02, FR-M04-03, BR-M04-01 | Nhóm A. Trình soạn bình luận tối giản |
| DEC-040 | Sở hữu | Hiện hành | FR-M04-02, FR-M04-03, BR-M04-03 | Nhóm A. Luồng 2 cấp; trả lời một trả lời nối vào cùng luồng |
| DEC-041 | Sở hữu | Hiện hành | BR-M04-09 | Nhóm A. Chỉ upvote, không downvote; nội dung xấu → báo cáo (M08) |
| DEC-042 | Sở hữu | Sửa một phần bởi DEC-182 | FR-M04-01, BR-M04-05, BR-M04-06 | Nhóm A. Sắp xếp Top/Mới nhất/Cũ nhất; trả lời luôn theo thời gian |
| DEC-043 | Sở hữu | Sửa một phần bởi DEC-179, DEC-181 | FR-M04-01, FR-M04-04, FR-M04-05, BR-M04-07, BR-M04-08 | Nhóm A. Sửa không giới hạn, nhãn "(đã chỉnh sửa)"; xóa vĩnh viễn, tombstone gốc có trả lời |
| DEC-044 | Sở hữu | Hiện hành | FR-M04-02, BR-M04-02 | Nhóm A. Không đính kèm trong bình luận |
| DEC-045 | Phụ thuộc | Sửa một phần bởi DEC-153 | Chuyển M01, M07 | Nhóm A. M01/M07: @mention dùng logic chung M01, luôn sinh thông báo |
| DEC-046 | Sở hữu | Sửa một phần bởi DEC-183 | FR-M04-03, FR-M04-03.01 | Nhóm A. Trả lời kèm trích dẫn tự chèn |
| DM-4.2 | Sở hữu | Hiện hành | FR-M04-01, FR-M04-02, FR-M04-03, FR-M04-04, FR-M04-05 | Nhóm A. Draft: Comment, Reply, Edit, Delete, Mention, Report |
| DM-4.2.1 | Sở hữu | Bị thay bởi DEC-169 | — | Nhóm A. Draft: Accepted Answer chọn một bình luận; MS1 không làm (DEC-169) |
| DM-4.3 | Phụ thuộc | Hiện hành | Chuyển M12 | Nhóm A. M12: Comment Star tách khỏi Post Star (ranh giới cần xác nhận) |
| ISS-070 | Sở hữu | Trùng với DEC-039 | — | Nhóm A. Trình soạn bình luận |
| ISS-071 | Sở hữu | Trùng với DEC-040 | — | Nhóm A. Độ sâu luồng |
| ISS-072 | Sở hữu | Trùng với DEC-041 | — | Nhóm A. Chỉ upvote |
| ISS-073 | Sở hữu | Trùng với DEC-042 | — | Nhóm A. Thứ tự sắp xếp |
| ISS-074 | Sở hữu | Trùng với DEC-043 | — | Nhóm A. Sửa, xóa |
| ISS-075 | Sở hữu | Bị thay bởi DEC-179 | — | Nhóm A. Không xóa mềm |
| ISS-076 | Sở hữu | Trùng với DEC-044 | — | Nhóm A. Không đính kèm |
| ISS-077 | Phụ thuộc | Trùng với DEC-045 | — | Nhóm A. M01/M07: @mention và thông báo |
| ISS-078 | Sở hữu | Trùng với DEC-046 | — | Nhóm A. Trả lời kèm trích dẫn |
| QA-092 | Sở hữu | Trùng với DEC-039 | — | Nhóm A. Trình soạn bình luận |
| QA-093 | Sở hữu | Trùng với DEC-040 | — | Nhóm A. Độ sâu luồng 2 cấp |
| QA-094 | Sở hữu | Trùng với DEC-041 | — | Nhóm A. Không downvote |
| QA-095 | Sở hữu | Trùng với DEC-042 | — | Nhóm A. Sắp xếp |
| QA-096 | Sở hữu | Trùng với DEC-043 | — | Nhóm A. Sửa không giới hạn thời gian |
| QA-097 | Sở hữu | Trùng với DEC-043 | — | Nhóm A. Hành vi xóa |
| QA-098 | Sở hữu | Trùng với DEC-044 | — | Nhóm A. Không đính kèm |
| QA-099 | Phụ thuộc | Trùng với DEC-045 | — | Nhóm A. M01/M07: nhắc tên trong bình luận luôn sinh thông báo |
| QA-100 | Sở hữu | Trùng với DEC-046 | — | Nhóm A. Trả lời kèm trích dẫn |
| MR-M04 | Sở hữu | Sửa một phần bởi DEC-178, DEC-179, DEC-183 | FR-M04-01, FR-M04-02, FR-M04-03, FR-M04-04, FR-M04-05 | Nhóm A. Dòng module-registry của M04; cột MoSCoW lệch (xem 4.5) |
| DEC-004 | Phụ thuộc | Hiện hành | Chuyển M12 | Nhóm B. M12: Post Star và Comment Star tách riêng, trọng số khác |
| DEC-012 | Phụ thuộc | Sửa một phần bởi DEC-033 | Chuyển M03 | Nhóm B. M03: tác giả, Mod khóa bình luận của bài |
| DEC-019 | Phụ thuộc | Sửa một phần bởi DEC-149, DEC-150, DEC-156 | Chuyển M01 | Nhóm B. M01: bình luận của tài khoản vô hiệu hóa, đã xóa. DEC-148 (ngoài bảng nguồn) chỉ sửa thời hạn, username |
| DEC-033 | Phụ thuộc | Sửa một phần bởi DEC-167 | FR-M04-01.13, FR-M04-02.06, FR-M04-03.07, BR-M04-14 | Nhóm B. M03: Khóa bình luận / Khóa toàn bộ chặn bình luận mới |
| DEC-037 | Sở hữu | Hiện hành | FR-M04-01, FR-M04-04, BR-M04-07 | Nhóm B. Phần bình luận: chỉ ghi thời điểm sửa, nhãn "(đã chỉnh sửa)", không có lịch sử (phần bài thuộc M03) |
| DEC-052 | Nhắc tới | Sửa một phần bởi DEC-145 | Không áp dụng: M05: Trending dùng số bình luận | Nhóm B. M05: Trending dùng số bình luận |
| DEC-053 | Nhắc tới | Hiện hành | Không áp dụng: M06: bình luận không được tìm kiếm | Nhóm B. M06: bình luận không được tìm kiếm |
| DEC-055 | Nhắc tới | Hiện hành | Không áp dụng: M06: xếp hạng dùng số bình luận | Nhóm B. M06: xếp hạng dùng số bình luận |
| DEC-065 | Phụ thuộc | Sửa một phần bởi DEC-180 | Chuyển M07 | Nhóm B. M07: thông báo bình luận mới, trả lời, nhắc tên, upvote bình luận. DEC-147, DEC-151 (ngoài bảng nguồn) chỉ thêm sự kiện liên kết Google, đặt lại mật khẩu |
| DEC-066 | Nhắc tới | Hiện hành | Không áp dụng: M07: gộp thông báo upvote | Nhóm B. M07: gộp thông báo upvote |
| DEC-070 | Phụ thuộc | Hiện hành | Chuyển M07 | Nhóm B. M07: tắt thông báo theo bài gồm bình luận, trả lời, upvote |
| DEC-072 | Phụ thuộc | Hiện hành | Chuyển M08 | Nhóm B. M08: lý do báo cáo bình luận (7) |
| DEC-077 | Phụ thuộc | Sửa một phần bởi DEC-098, DEC-180 | FR-M04-01, FR-M04-02.02, FR-M04-03.04, FR-M04-04.03, BR-M04-12 | Nhóm B. M08: bình luận đăng ngay, quét AI theo tốc độ trả lời; bị gắn cờ → ẩn, chỉ tác giả thấy |
| DEC-079 | Phụ thuộc | Sửa một phần bởi DEC-122 | FR-M04-02.07, FR-M04-03.08, BR-M04-15 | Nhóm B. M08: mức HEAVY không được bình luận. DEC-118, DEC-163 (ngoài bảng nguồn) chỉ sửa phần bảng xếp hạng và phạm vi "tạo bài mới"; hạn chế bình luận ở HEAVY giữ nguyên |
| DEC-083 | Sở hữu | Hiện hành | FR-M04-01, FR-M04-01.09, BR-M04-13 | Nhóm B. Bình luận có trạng thái kiểm duyệt Bình thường/Bị ẩn — yêu cầu bổ sung cho M04 từ M08 |
| DEC-093 | Phụ thuộc | Hiện hành | Chuyển M10 | Nhóm B. M10: công tắc Moderation gồm quét bình luận |
| DEC-098 | Phụ thuộc | Hiện hành | Chuyển M13 | Nhóm B. M13: ngưỡng 0.9/0.5 — tự ẩn bình luận. DEC-166 (ngoài bảng nguồn) chỉ sửa phần bài bị AI từ chối |
| DEC-099 | Phụ thuộc | Hiện hành | Chuyển M13 | Nhóm B. M13: AI lỗi khi quét bình luận → giữ nguyên, ghi lỗi |
| DEC-102 | Phụ thuộc | Hiện hành | Chuyển M11 | Nhóm B. M11: vai trò nhóm bình luận, ẩn/xóa bình luận trong nhóm |
| DEC-105 | Phụ thuộc | Sửa một phần bởi DEC-113 | Chuyển M11 | Nhóm B. M11: rời nhóm, bình luận giữ nguyên; nhóm bị xóa thì nội dung ẩn |
| DEC-108 | Phụ thuộc | Hiện hành | Chuyển M11 | Nhóm B. M11: nhóm chuyển Private → bình luận báo lỗi |
| DEC-113 | Phụ thuộc | Sửa một phần bởi DEC-231, DEC-241 | FR-M04-01.11, FR-M04-01.12, FR-M04-02.08, FR-M04-03.09, BR-M04-17 | Nhóm B. M12: trừ điểm khi tự xóa hoặc bị Mod xóa; bình luận ẩn theo bài cha không trừ. Bình luận do tác giả tự xóa bị trừ điểm ngay lúc xóa; bình luận bị AI ẩn ≥ 0,9 trừ ngay, 0,5–< 0,9 trừ khi Mod kết luận vi phạm (DEC-241, M12); gỡ khỏi nhóm không trừ (DEC-231) |
| DEC-115 | Phụ thuộc | Hiện hành | BR-M04-23 | Nhóm B. M09: khiếu nại xóa nội dung chỉ cho bài, không cho bình luận |
| DEC-116 | Nhắc tới | Hiện hành | Không áp dụng: M12: Comment Star = 1 điểm | Nhóm B. M12: Comment Star = 1 điểm |
| DEC-119 | Phụ thuộc | Hiện hành | Chuyển M12 | Nhóm B. M12: rút lại upvote |
| DEC-120 | Phụ thuộc | Hiện hành | Chuyển M12 | Nhóm B. M12: ẩn nút vote trên bình luận của chính mình |
| DEC-122 | Phụ thuộc | Hiện hành | Chuyển M12 | Nhóm B. M12: nhãn "Tài khoản đã bị khóa" cạnh tên tác giả bình luận. Cạnh "ISS-154 sửa DEC-122" bị bác: ISS-154 là câu hỏi sinh ra DEC-122 |
| DEC-124 | Nhắc tới | Hiện hành | Không áp dụng: M14: Trending Post | Nhóm B. M14: Trending Post |
| DEC-128 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: không dịch nội dung người dùng | Nhóm B. Dùng chung: không dịch nội dung người dùng |
| DEC-129 | Phụ thuộc | Sửa một phần bởi DEC-156, DEC-179 | Không áp dụng: Dùng chung: chỉ xóa hẳn khi an toàn; xóa hẳn bình luận đã chốt không đổi | Nhóm B. Dùng chung: chỉ xóa hẳn khi an toàn; xóa hẳn bình luận đã chốt không đổi |
| DEC-131 | Nhắc tới | Sửa một phần bởi DEC-154 | Không áp dụng: Dùng chung: trang chính sách nêu bình luận được AI xử lý | Nhóm B. Dùng chung: trang chính sách nêu bình luận được AI xử lý. DEC-146 (ngoài bảng nguồn) thêm công bố gợi ý Topic |
| DEC-133 | Nhắc tới | Hiện hành | Không áp dụng: M13: log đầu ra AI gắn với bình luận | Nhóm B. M13: log đầu ra AI gắn với bình luận |
| DEC-145 | Nhắc tới | Hiện hành | Không áp dụng: M05: Trending tính bình luận gồm trả lời, không tính upvote bình luận | Nhóm B. M05: Trending tính bình luận gồm trả lời, không tính upvote bình luận |
| DEC-149 | Phụ thuộc | Hiện hành | Chuyển M01 | Nhóm B. M01: bình luận của tài khoản DELETED giữ nội dung, tên "[Người dùng đã xóa]" |
| DEC-150 | Phụ thuộc | Hiện hành | Chuyển M01 | Nhóm B. M01: Mod, Admin thấy danh tính thật sau nhãn tài khoản vô hiệu hóa |
| DEC-153 | Phụ thuộc | Hiện hành | Chuyển M01 | Nhóm B. M01: nhắc tên trong bình luận dùng ngữ cảnh bài; thời điểm gửi thông báo |
| DEC-154 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: trang chính sách | Nhóm B. Dùng chung: trang chính sách |
| DEC-156 | Phụ thuộc | Hiện hành | Chuyển M01 | Nhóm B. M01: dữ liệu giữ khi DELETED — bình luận giữ, upvote đã cho vẫn tính. DEC-159 (ngoài bảng nguồn) chỉ sửa phần theo dõi, gợi ý Topic |
| DEC-167 | Phụ thuộc | Hiện hành | FR-M04-01.13, FR-M04-02.06, FR-M04-03.07, BR-M04-14 | Nhóm B. M03: Khóa toàn bộ chặn bình luận mới và upvote |
| DEC-169 | Sở hữu | Hiện hành | BR-M04-11 | Nhóm B. MS1 không có Accepted Answer, ảnh hưởng M03, M04, M12 |
| DG-4 | Nhắc tới | Sửa một phần bởi DEC-169 | Không áp dụng: Bản đồ module: Comment, Comment Star | Nhóm B. Bản đồ module: Comment, Comment Star |
| DG-5 | Nhắc tới | Sửa một phần bởi DEC-169 | Không áp dụng: Nguyên tắc: Comment Star tách Post Star; Accepted Answer | Nhóm B. Nguyên tắc: Comment Star tách Post Star; Accepted Answer |
| DG-6 | Phụ thuộc | Sửa một phần bởi QA-007 | Chuyển M13 | Nhóm B. M13: tóm tắt bài hoặc luồng bình luận dài |
| DG-8 | Phụ thuộc | Hiện hành | Không áp dụng: Không làm: AI tự viết bình luận | Nhóm B. Không làm: AI tự viết bình luận |
| DM-1.3 | Sở hữu | Hiện hành | FR-M04-02, FR-M04-04, FR-M04-05 | Nhóm B. Draft: quyền tạo, sửa, xóa bình luận theo vai trò |
| DM-10.1 | Phụ thuộc | Sửa một phần bởi DEC-072 | Chuyển M08 | Nhóm B. M08: báo cáo bình luận |
| DM-10.2 | Phụ thuộc | Sửa một phần bởi DEC-169, DEC-180 | FR-M04-05.05 | Nhóm B. M08: Mod, Admin ẩn, xóa bình luận |
| DM-11 | Nhắc tới | Hiện hành | Không áp dụng: AI không tự chọn Accepted Answer | Nhóm B. AI không tự chọn Accepted Answer |
| DM-11.1 | Phụ thuộc | Sửa một phần bởi DEC-077 | Chuyển M08, M13 | Nhóm B. M08/M13: AI kiểm duyệt Post/Comment |
| DM-11.4 | Phụ thuộc | Sửa một phần bởi QA-007 | Chuyển M13 | Nhóm B. M13: tóm tắt luồng bình luận dài (đối chiếu QA-007 ở bước 2) |
| DM-13 | Nhắc tới | Hiện hành | Không áp dụng: Kiến trúc: Comment thuộc Forum | Nhóm B. Kiến trúc: Comment thuộc Forum |
| DM-2.1 | Sở hữu | Sửa một phần bởi DEC-169 | FR-M04-01 | Nhóm B. Chỉ phần "Comment count" của bài (FR-M03 đã chuyển sang M04); phần còn lại thuộc M03 |
| DM-5.3 | Phụ thuộc | Hiện hành | Chuyển M11 | Nhóm B. M11: nhóm dùng chung cơ chế bình luận, lọc theo quyền xem |
| DM-7.2 | Nhắc tới | Sửa một phần bởi DEC-145 | Không áp dụng: M14: Trending dùng số bình luận | Nhóm B. M14: Trending dùng số bình luận |
| DM-8.1 | Phụ thuộc | Sửa một phần bởi DEC-065, DEC-169 | Chuyển M07 | Nhóm B. M07: sự kiện comment mới, reply, mention, Accepted Answer |
| DM-9.1 | Nhắc tới | Sửa một phần bởi DEC-169 | Không áp dụng: M12: nguồn uy tín | Nhóm B. M12: nguồn uy tín |
| DM-9.3 | Nhắc tới | Sửa một phần bởi DEC-169 | Không áp dụng: M12/M02: thống kê người dùng | Nhóm B. M12/M02: thống kê người dùng |
| DM-9.5 | Nhắc tới | Hiện hành | Không áp dụng: M15: thống kê hệ thống | Nhóm B. M15: thống kê hệ thống |
| DM-x02 | Nhắc tới | Sửa một phần bởi DEC-169, QA-007 | Không áp dụng: Danh sách phạm vi: Comment, Comment Star, tóm tắt luồng bình luận | Nhóm B. Danh sách phạm vi: Comment, Comment Star, tóm tắt luồng bình luận |
| DM-x03 | Phụ thuộc | Hiện hành | Không áp dụng: Ngoài phạm vi: AI tự viết comment | Nhóm B. Ngoài phạm vi: AI tự viết comment |
| GL:Accepted Answer | Nhắc tới | Bị thay bởi DEC-169 | — | Nhóm B. Accepted Answer; đã có DEC-169 |
| GL:Comment | Sở hữu | Sửa một phần bởi DEC-169 | FR-M04-02 | Nhóm B. Thuật ngữ Comment; "accepted as an answer" bị DEC-169 thay |
| GL:Comment Star | Nhắc tới | Hiện hành | Không áp dụng: M12: định nghĩa Comment Star | Nhóm B. M12: định nghĩa Comment Star |
| GL:Group | Phụ thuộc | Hiện hành | Chuyển M11 | Nhóm B. M11: nhóm dùng lại cơ chế bình luận |
| GL:Moderator (MOD) | Phụ thuộc | Sửa một phần bởi DEC-180 | Chuyển M08 | Nhóm B. M08: Mod ẩn, khóa, xóa bình luận |
| GL:Post Star | Nhắc tới | Hiện hành | Không áp dụng: M12: phân biệt với Comment Star | Nhóm B. M12: phân biệt với Comment Star |
| GL:Reputation | Nhắc tới | Sửa một phần bởi DEC-169 | Không áp dụng: M12: uy tín | Nhóm B. M12: uy tín |
| GL:Summarization | Phụ thuộc | Sửa một phần bởi QA-007 | Chuyển M13 | Nhóm B. M13: tóm tắt luồng bình luận |
| ISS-045 | Sở hữu | Trùng với QA-032 | — | Nhóm B. Câu hỏi độ sâu bình luận (Phase 4) |
| ISS-047 | Nhắc tới | Hiện hành | Không áp dụng: M06: phạm vi tìm kiếm | Nhóm B. M06: phạm vi tìm kiếm |
| ISS-066 | Sở hữu | Trùng với DEC-037 | — | Nhóm B. Phần bình luận: chỉ thời điểm sửa |
| ISS-085 | Nhắc tới | Trùng với DEC-053 | — | Nhóm B. M06: phạm vi tìm kiếm |
| ISS-104 | Phụ thuộc | Trùng với DEC-072 | — | Nhóm B. M08: đối tượng và lý do báo cáo |
| ISS-107 | Phụ thuộc | Trùng với DEC-077 | — | Nhóm B. M08: quét AI bình luận |
| ISS-109 | Phụ thuộc | Trùng với DEC-079 | — | Nhóm B. M08: hạn chế theo mức cảnh cáo |
| ISS-142 | Phụ thuộc | Trùng với DEC-113 | — | Nhóm B. M12: trừ điểm theo nội dung |
| ISS-144 | Phụ thuộc | Trùng với DEC-115 | — | Nhóm B. M09: khiếu nại xóa nội dung chỉ cho bài |
| ISS-145 | Nhắc tới | Trùng với DEC-116 | — | Nhóm B. M12: trọng số sao |
| ISS-147 | Phụ thuộc | Trùng với DEC-119 | — | Nhóm B. M12: rút lại upvote |
| ISS-148 | Phụ thuộc | Trùng với DEC-120 | — | Nhóm B. M12: không tự vote |
| ISS-154 | Phụ thuộc | Trùng với DEC-122 | — | Nhóm B. M12: hiển thị tài khoản BANNED |
| ISS-166 | Phụ thuộc | Trùng với QA-227 | — | Nhóm B. Dùng chung: mọi tương tác cần đăng nhập |
| ISS-180 | Nhắc tới | Hiện hành | Không áp dụng: M15: xu hướng bình luận | Nhóm B. M15: xu hướng bình luận |
| ISS-191 | Phụ thuộc | Trùng với DEC-129 | — | Nhóm B. Dùng chung: lưu giữ dữ liệu |
| ISS-193 | Nhắc tới | Trùng với DEC-131 | — | Nhóm B. Dùng chung: trang chính sách |
| ISS-195 | Nhắc tới | Trùng với DEC-133 | — | Nhóm B. M13: log AI |
| ISS-233 | Phụ thuộc | Trùng với DEC-149 | — | Nhóm B. M01: hiển thị bình luận của tài khoản DELETED |
| ISS-272 | Sở hữu | Trùng với DEC-169 | — | Nhóm B. Accepted Answer có trong MS1 không |
| QA-007 | Phụ thuộc | Hiện hành | Chuyển M13 | Nhóm B. M13: tóm tắt chỉ cho bài, không cho luồng bình luận. Thắng draft về tóm tắt luồng bình luận (QA > draft) |
| QA-011 | Phụ thuộc | Hiện hành | FR-M04-01, FR-M04-01.01, FR-M04-01.02, FR-M04-02, FR-M04-02.05, FR-M04-03.06, BR-M04-16, BR-M04-17 | Nhóm B. Dùng chung: Guest xem bình luận, không báo cáo, không tương tác. DEC-171 (ngoài bảng nguồn) chỉ thêm quyền xem hồ sơ của Guest |
| QA-017 | Phụ thuộc | Sửa một phần bởi DEC-077 | Chuyển M08, M13 | Nhóm B. M08/M13: AI kiểm duyệt quét cả bình luận |
| QA-018 | Phụ thuộc | Sửa một phần bởi DEC-149 | Chuyển M01 | Nhóm B. M01: tombstone bình luận của tài khoản đã xóa (bị DEC-149 thay) |
| QA-019 | Phụ thuộc | Sửa một phần bởi DEC-115 | Chuyển M09 | Nhóm B. M09: bài, bình luận bị xóa không có khiếu nại |
| QA-020 | Phụ thuộc | Sửa một phần bởi DEC-079, DEC-115 | Chuyển M08, M09 | Nhóm B. M08/M09: mức cảnh cáo; "post/comment bị xóa không có appeal" |
| QA-022 | Nhắc tới | Sửa một phần bởi DEC-053 | Không áp dụng: M06: bình luận không đưa vào tìm kiếm | Nhóm B. M06: bình luận không đưa vào tìm kiếm |
| QA-028 | Phụ thuộc | Sửa một phần bởi DEC-033 | Chuyển M03 | Nhóm B. M03: tác giả khóa bình luận bài của mình |
| QA-032 | Sở hữu | Sửa một phần bởi DEC-040 | FR-M04-03, BR-M04-03 | Nhóm B. Độ sâu bình luận "1 cấp, không reply to reply" (Phase 4); đối chiếu DEC-040 ở bước 2 |
| QA-035 | Nhắc tới | Sửa một phần bởi DEC-053 | Không áp dụng: M06: bình luận không được tìm kiếm | Nhóm B. M06: bình luận không được tìm kiếm |
| QA-037 | Nhắc tới | Bị thay bởi DEC-053 | — | Nhóm B. M06: bình luận chỉ FTS (khác DEC-053) |
| QA-043 | Phụ thuộc | Hiện hành | Chuyển M07 | Nhóm B. M07: theo dõi người dùng, Topic (theo dõi bài viết đã bỏ, DEC-215) |
| QA-065 | Phụ thuộc | Trùng với DEC-019 | — | Nhóm B. M01: bình luận của tài khoản vô hiệu hóa |
| QA-066 | Phụ thuộc | Sửa một phần bởi DEC-149 | Chuyển M01 | Nhóm B. M01: bình luận sau khi tài khoản bị xóa |
| QA-090 | Sở hữu | Trùng với DEC-037 | — | Nhóm B. Lịch sử sửa bình luận: chỉ thời điểm sửa, không có giao diện lịch sử |
| QA-106 | Nhắc tới | Sửa một phần bởi DEC-145 | Không áp dụng: M05: Trending | Nhóm B. M05: Trending |
| QA-108 | Sở hữu | Hiện hành | BR-M04-10 | Nhóm B. Bình luận không có Tag, theo ngữ cảnh bài |
| QA-112 | Nhắc tới | Trùng với DEC-055 | — | Nhóm B. M06: xếp hạng |
| QA-123 | Phụ thuộc | Trùng với DEC-065 | — | Nhóm B. M07: danh sách sự kiện thông báo |
| QA-134 | Phụ thuộc | Trùng với DEC-072 | — | Nhóm B. M08: lý do báo cáo theo loại |
| QA-141 | Phụ thuộc | Trùng với DEC-077 | — | Nhóm B. M08: bình luận quét sau khi đăng |
| QA-142 | Phụ thuộc | Trùng với DEC-077 | — | Nhóm B. M08: phạm vi quét cả luồng |
| QA-143 | Phụ thuộc | Trùng với DEC-077 | — | Nhóm B. M08: sửa không tự kích hoạt quét lại |
| QA-171 | Phụ thuộc | Trùng với DEC-098 | — | Nhóm B. M13: AI tự ẩn bình luận khi điểm ≥ 0.9 |
| QA-180 | Phụ thuộc | Trùng với DEC-102 | — | Nhóm B. M11: quyền vai trò nhóm |
| QA-186 | Phụ thuộc | Trùng với DEC-108 | — | Nhóm B. M11: chuyển Private khóa tương tác |
| QA-191 | Phụ thuộc | Trùng với DEC-113 | — | Nhóm B. M12: trừ điểm theo nội dung |
| QA-193 | Phụ thuộc | Trùng với DEC-115 | — | Nhóm B. M09: khiếu nại xóa nội dung chỉ cho bài |
| QA-196 | Nhắc tới | Trùng với DEC-116 | — | Nhóm B. M12: trọng số sao |
| QA-199 | Nhắc tới | Hiện hành | Không áp dụng: M12: bảng xếp hạng | Nhóm B. M12: bảng xếp hạng |
| QA-200 | Phụ thuộc | Trùng với DEC-119 | — | Nhóm B. M12: rút lại upvote |
| QA-201 | Phụ thuộc | Trùng với DEC-120 | — | Nhóm B. M12: không tự vote |
| QA-204 | Phụ thuộc | Trùng với DEC-122 | — | Nhóm B. M12: bình luận của tài khoản BANNED vẫn hiện |
| QA-205 | Phụ thuộc | Trùng với DEC-122 | — | Nhóm B. M12: nhãn tài khoản bị khóa trên bình luận |
| QA-227 | Phụ thuộc | Hiện hành | FR-M04-02.05, FR-M04-03.06, BR-M04-16 | Nhóm B. Dùng chung: mọi tương tác cần đăng nhập |
| QA-234 | Nhắc tới | Sửa một phần bởi DEC-134 | Không áp dụng: M14: phân trang feed; Guest xem bài, bình luận | Nhóm B. M14: phân trang feed; Guest xem bài, bình luận |
| QA-235 | Nhắc tới | Hiện hành | Không áp dụng: M14: ngưỡng Trending | Nhóm B. M14: ngưỡng Trending |
| QA-236 | Nhắc tới | Hiện hành | Không áp dụng: M14: Trending | Nhóm B. M14: Trending |
| QA-243 | Nhắc tới | Hiện hành | Không áp dụng: M15: xu hướng bình luận | Nhóm B. M15: xu hướng bình luận |
| QA-249 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: i18n | Nhóm B. Dùng chung: i18n |
| QA-250 | Phụ thuộc | Trùng với DEC-129 | — | Nhóm B. Dùng chung: lưu giữ dữ liệu |
| QA-252 | Nhắc tới | Trùng với DEC-131 | — | Nhóm B. Dùng chung: trang chính sách |
| QA-254 | Nhắc tới | Trùng với DEC-133 | — | Nhóm B. M13: log AI |
| QA-271 | Nhắc tới | Trùng với DEC-145 | — | Nhóm B. M05: Trending |
| QA-285 | Nhắc tới | Trùng với DEC-145 | — | Nhóm B. M05: Trending |
| QA-293 | Phụ thuộc | Trùng với DEC-149 | — | Nhóm B. M01: hiển thị bình luận của tài khoản DELETED |
| QA-301 | Phụ thuộc | Trùng với DEC-153 | — | Nhóm B. M01: danh sách gợi ý và thông báo nhắc tên |
| QA-311 | Phụ thuộc | Trùng với DEC-156 | — | Nhóm B. M01: dữ liệu giữ khi DELETED |
| QA-329 | Phụ thuộc | Trùng với DEC-167 | — | Nhóm B. M03: Khóa toàn bộ chặn bình luận, upvote |
| QA-332 | Sở hữu | Trùng với DEC-169 | — | Nhóm B. MS1 không hỗ trợ Accepted Answer |
| MR-A03 | Nhắc tới | Hiện hành | Không áp dụng: M15: xu hướng bình luận | Nhóm B. M15: xu hướng bình luận |
| MR-M06 | Nhắc tới | Trùng với DEC-053 | — | Nhóm B. M06: không tìm bình luận |
| MR-M07 | Nhắc tới | Sửa một phần bởi DEC-135 | Không áp dụng: M07: sự kiện bình luận | Nhóm B. M07: sự kiện bình luận |
| MR-M08 | Nhắc tới | Trùng với DEC-077 | — | Nhóm B. M08: quét bình luận; đã có DEC-077 |
| MR-M12 | Nhắc tới | Hiện hành | Không áp dụng: M12 phụ thuộc M04 | Nhóm B. M12 phụ thuộc M04 |
| DEC-127 | Phụ thuộc | Hiện hành | Không áp dụng: Dùng chung: múi giờ hiển thị thời điểm bình luận | Nhóm D. Dùng chung: múi giờ hiển thị thời điểm bình luận |
| DEC-130 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: tải tệp; bình luận không có đính kèm | Nhóm D. Dùng chung: tải tệp; bình luận không có đính kèm. DEC-160 (ngoài bảng nguồn) chỉ sửa phần tài liệu đính kèm bài |
| DEC-132 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M04 | Nhóm D. Dùng chung; không quy định hành vi M04. DEC-141, DEC-144 (ngoài bảng nguồn) sửa phần Topic |
| DEC-134 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M04 | Nhóm D. Dùng chung; không quy định hành vi M04 |
| DEC-135 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M04 | Nhóm D. Dùng chung; không quy định hành vi M04 |
| DEC-136 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M04 | Nhóm D. Dùng chung; không quy định hành vi M04 |
| DEC-137 | Nhắc tới | Hiện hành | Không áp dụng: Công nghệ (Tiptap) | Nhóm D. Công nghệ (Tiptap) |
| DEC-138 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M04 | Nhóm D. Dùng chung; không quy định hành vi M04. DEC-155, DEC-157 (ngoài bảng nguồn) sửa phần đồng ý chính sách |
| ISS-189 | Nhắc tới | Trùng với DEC-127 | — | Nhóm D. Đã có DEC-127 |
| ISS-190 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M04 | Nhóm D. Dùng chung; không quy định hành vi M04 |
| ISS-192 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: tải tệp | Nhóm D. Dùng chung: tải tệp |
| ISS-194 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M04 | Nhóm D. Dùng chung; không quy định hành vi M04 |
| ISS-196 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M04 | Nhóm D. Dùng chung; không quy định hành vi M04 |
| ISS-197 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M04 | Nhóm D. Dùng chung; không quy định hành vi M04 |
| ISS-198 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M04 | Nhóm D. Dùng chung; không quy định hành vi M04 |
| ISS-199 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M04 | Nhóm D. Dùng chung; không quy định hành vi M04 |
| ISS-200 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M04 | Nhóm D. Dùng chung; không quy định hành vi M04 |
| ISS-201 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M04 | Nhóm D. Dùng chung; không quy định hành vi M04 |
| ISS-202 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M04 | Nhóm D. Dùng chung; không quy định hành vi M04 |
| ISS-203 | Nhắc tới | Hiện hành | Không áp dụng: Công nghệ | Nhóm D. Công nghệ |
| ISS-204 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M04 | Nhóm D. Dùng chung; không quy định hành vi M04 |
| QA-248 | Phụ thuộc | Trùng với DEC-127 | — | Nhóm D. Dùng chung: múi giờ |
| QA-251 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: tải tệp | Nhóm D. Dùng chung: tải tệp |
| QA-253 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M04 | Nhóm D. Dùng chung; không quy định hành vi M04 |
| QA-255 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M04 | Nhóm D. Dùng chung; không quy định hành vi M04 |
| QA-256 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M04 | Nhóm D. Dùng chung; không quy định hành vi M04 |
| QA-257 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M04 | Nhóm D. Dùng chung; không quy định hành vi M04 |
| QA-258 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M04 | Nhóm D. Dùng chung; không quy định hành vi M04 |
| QA-259 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M04 | Nhóm D. Dùng chung; không quy định hành vi M04 |
| QA-260 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M04 | Nhóm D. Dùng chung; không quy định hành vi M04 |
| QA-261 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M04 | Nhóm D. Dùng chung; không quy định hành vi M04 |
| QA-262 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M04 | Nhóm D. Dùng chung; không quy định hành vi M04 |
| QA-263 | Nhắc tới | Hiện hành | Không áp dụng: Công nghệ | Nhóm D. Công nghệ |
| QA-264 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M04 | Nhóm D. Dùng chung; không quy định hành vi M04 |
| MR-A04 | Phụ thuộc | Hiện hành | Không áp dụng: Phase 6: múi giờ | Nhóm D. Phase 6: múi giờ |
| MR-A05 | Nhắc tới | Hiện hành | Không áp dụng: Công nghệ | Nhóm D. Công nghệ |
| DEC-178 | Sở hữu | Hiện hành | FR-M04-04, FR-M04-04.09, FR-M04-04.10, FR-M04-04.11, FR-M04-05, FR-M04-05.08, FR-M04-05.09, FR-M04-05.10, BR-M04-20 | Nhóm A. Sửa, xóa bình luận khi bài khóa, ở mức HEAVY, khi bị ẩn |
| DEC-179 | Sở hữu | Hiện hành | FR-M04-04.08, FR-M04-05, FR-M04-05.01, FR-M04-05.02, FR-M04-05.03, FR-M04-05.04, FR-M04-05.07, FR-M04-05.11, FR-M04-06, FR-M04-06.02, FR-M04-06.03, FR-M04-06.04, FR-M04-06.05, BR-M04-08, BR-M04-21, BR-M04-22 | Nhóm A. Xóa mềm; Mod, Admin và chủ nội dung xem lại nội dung đã xóa (mở rộng phạm vi) |
| DEC-180 | Sở hữu | Hiện hành | FR-M04-01, FR-M04-01.09, FR-M04-03.10, FR-M04-05.05, FR-M04-06, FR-M04-06.01, BR-M04-13, BR-M04-23 | Nhóm A. Bình luận bị ẩn không hiện với ai trong luồng; thông báo bị ẩn; Mod chỉ có thao tác Ẩn |
| DEC-181 | Sở hữu | Hiện hành | FR-M04-01, FR-M04-01.07, FR-M04-01.08, FR-M04-01.15, FR-M04-03, FR-M04-03.10, FR-M04-03.11, FR-M04-05.01, FR-M04-05.02, BR-M04-04, BR-M04-08, BR-M04-13 | Nhóm A. Hiển thị luồng có bình luận đã xóa, bị ẩn |
| DEC-182 | Sở hữu | Hiện hành | FR-M04-01, FR-M04-01.10, FR-M04-01.14, BR-M04-05, BR-M04-18 | Nhóm A. Số bình luận của bài; thứ tự Top khi cùng upvote |
| DEC-183 | Sở hữu | Hiện hành | FR-M04-01, FR-M04-01.08, FR-M04-01.16, FR-M04-01.17, FR-M04-02, FR-M04-02.09, FR-M04-02.10, FR-M04-02.11, FR-M04-03, FR-M04-03.01, FR-M04-03.12, FR-M04-03.13, FR-M04-04, FR-M04-04.12, FR-M04-04.13, BR-M04-04, BR-M04-19 | Nhóm A. Giới hạn 1.000 từ; trích dẫn khi trả lời chỉ hiển thị, một dòng |
| ISS-282 | Sở hữu | Trùng với DEC-178 | — | Nhóm A. Câu hỏi FR M04 |
| ISS-283 | Sở hữu | Trùng với DEC-179 | — | Nhóm A. Câu hỏi FR M04 |
| ISS-284 | Sở hữu | Trùng với DEC-179 | — | Nhóm A. Câu hỏi FR M04 |
| ISS-285 | Sở hữu | Trùng với DEC-180 | — | Nhóm A. Câu hỏi FR M04 |
| ISS-286 | Sở hữu | Trùng với DEC-181 | — | Nhóm A. Câu hỏi FR M04 |
| ISS-287 | Sở hữu | Trùng với DEC-182 | — | Nhóm A. Câu hỏi FR M04 |
| ISS-288 | Sở hữu | Trùng với DEC-183 | — | Nhóm A. Câu hỏi FR M04 |
| ISS-289 | Sở hữu | Trùng với DEC-179 | — | Nhóm A. Câu hỏi FR M04 |
| QA-342 | Sở hữu | Trùng với DEC-178 | — | Nhóm A. Câu trả lời FR M04, chốt ở DEC-178 |
| QA-343 | Sở hữu | Trùng với DEC-179 | — | Nhóm A. Câu trả lời FR M04, chốt ở DEC-179 |
| QA-344 | Sở hữu | Trùng với DEC-179 | — | Nhóm A. Câu trả lời FR M04, chốt ở DEC-179 |
| QA-345 | Sở hữu | Trùng với DEC-180 | — | Nhóm A. Câu trả lời FR M04, chốt ở DEC-180 |
| QA-346 | Sở hữu | Trùng với DEC-181 | — | Nhóm A. Câu trả lời FR M04, chốt ở DEC-181 |
| QA-347 | Sở hữu | Trùng với DEC-182 | — | Nhóm A. Câu trả lời FR M04, chốt ở DEC-182 |
| QA-348 | Sở hữu | Trùng với DEC-183 | — | Nhóm A. Câu trả lời FR M04, chốt ở DEC-183 |
| QA-349 | Sở hữu | Trùng với DEC-179 | — | Nhóm A. Câu trả lời FR M04, chốt ở DEC-179 |
| OPEN-010 | Nhắc tới | Hiện hành | Không áp dụng: M03: áp xóa mềm cho bài viết sau 7 ngày khôi phục | Nhóm B. M03: áp xóa mềm cho bài viết sau 7 ngày khôi phục |
| OPEN-011 | Nhắc tới | Hiện hành | Không áp dụng: M11, M16: xét nguyên tắc xóa mềm khi viết FR | Nhóm B. M11, M16: xét nguyên tắc xóa mềm khi viết FR |
| OPEN-012 | Phụ thuộc | Bị thay bởi DEC-201 | — | Nhóm B. M09: bình luận bị ẩn có hiện lại khi khiếu nại cảnh cáo, ban thành công |
| DEC-074 | Phụ thuộc | Hiện hành | FR-M04-06, FR-M04-06.02, BR-M04-22 | Nhóm C. M08: thông báo kết quả xử lý gửi người vi phạm |
| DEC-076 | Phụ thuộc | Hiện hành | BR-M04-21 | Nhóm C. M08: báo cáo gom theo đối tượng; lịch sử báo cáo |
| DEC-163 | Phụ thuộc | Hiện hành | Chuyển M03 | Nhóm C. M03: mức cảnh cáo chỉ chặn tạo bài mới, vẫn cho sửa bài cũ; DEC-178 áp cùng nguyên tắc |
| DEC-164 | Phụ thuộc | Hiện hành | FR-M04-02.09, FR-M04-04.12, BR-M04-19 | Nhóm C. M03: cách đếm từ, cảnh báo khi vượt giới hạn |
| DEC-231 | Phụ thuộc | Hiện hành | Chuyển M11 | Nhóm B (đối chiếu FR-M11). M11: gỡ bình luận khỏi nhóm |
| DEC-234 | Phụ thuộc | Hiện hành | Chuyển M11 | Nhóm B (đối chiếu FR-M11). M11: người ngoài bình luận bài nhóm Public |
| DEC-235 | Phụ thuộc | Hiện hành | Chuyển M11 | Nhóm B (đối chiếu FR-M11). M11: nhóm Bị khóa chặn bình luận và thao tác quản trị |
| DEC-237 | Phụ thuộc | Hiện hành | Chuyển M11 | Nhóm B (đối chiếu FR-M11). M11: người đã rời nhóm Private không sửa, xóa bình luận của mình |
| DEC-195 | Phụ thuộc | Hiện hành | BR-M04-12 | Nhóm B (rà lại 1.3). M09: bình luận của Admin không bị AI quét, không báo cáo được; áp ở M08 |
| DEC-201 | Phụ thuộc | Hiện hành | Chuyển M09 | Nhóm B (rà lại 1.3). M09: bình luận bị ẩn không hiện lại khi cảnh cáo, ban liên quan bị lật; đóng OPEN-012 |
| DEC-231 | Phụ thuộc | Hiện hành | Chuyển M11 | Nhóm B (rà lại 1.3). M11: gỡ bình luận khỏi nhóm không trừ điểm |
| DEC-241 | Phụ thuộc | Hiện hành | Chuyển M12 | Nhóm B (rà lại 1.3). M12: thời điểm trừ điểm của bình luận |

### C.2 Chuỗi quyết định

| Chuỗi | Nội dung hiện hành |
|---|---|
| QA-032 → DEC-040 | Luồng hai cấp: bình luận gốc và trả lời. Trả lời vào một trả lời được nối vào cùng luồng, không lồng sâu hơn; dùng nhắc tên để chỉ người được trả lời. Ý "không có reply to reply" của QA-032 được DEC-040 thay bằng cách nối vào cùng luồng. |
| DEC-045 → DEC-153 | Nhắc tên trong bình luận dùng logic chung của M01 và luôn sinh thông báo, kể cả khi bài bị tắt thông báo (DEC-070). DEC-153 thêm: thông báo gửi khi nội dung hiển thị công khai; sửa nội dung chỉ báo người mới được nhắc; nhắc tên trong bình luận dùng ngữ cảnh của bài chứa nó. |
| DM-4.2.1 → DEC-169 | MS1 không có Accepted Answer. Phần Accepted Answer trong GL:Accepted Answer, GL:Comment, DM-2.1, DM-8.1, DM-9.1, DM-9.3, DM-10.2, DG-4, DG-5, DM-x02 hết hiệu lực; phần còn lại của các mục đó giữ nguyên. |
| DEC-037 (phần bình luận), DEC-043 → DEC-179, DEC-181 | Bình luận chỉ ghi thời điểm sửa, hiện nhãn "(đã chỉnh sửa)", không có lịch sử sửa. Tác giả xóa bình luận: với người dùng là vĩnh viễn, không khôi phục; hệ thống gắn cờ đã xóa và giữ nội dung, không bao giờ xóa hẳn (DEC-179). Bình luận gốc còn trả lời hiển thị bình thường hiện dấu "[Bình luận đã bị xóa]"; dấu mất khi luồng không còn trả lời hiển thị bình thường (DEC-181). Ý "permanent, no soft delete" của DEC-043 và ISS-075 bị thay. Bình luận giữ cùng bài khi bài bị xóa. |
| QA-018 → DEC-019 → DEC-149, DEC-150, DEC-156 | Bình luận của tài khoản vô hiệu hóa: giữ nội dung, tác giả "Tài khoản tạm thời vô hiệu hoá", avatar giữ chỗ; Mod, Admin thấy danh tính thật (DEC-150). Tài khoản đã xóa: giữ nội dung, tác giả "[Người dùng đã xóa]", avatar mặc định (DEC-149); upvote đã cho vẫn tính cho người nhận (DEC-156). Tombstone "[Bình luận từ tài khoản đã xóa]" của QA-018 bị thay. |
| QA-017 → DEC-077 → DEC-098 → DEC-180 | Bình luận đăng ngay, không quét trước. Khi tốc độ trả lời vượt ngưỡng (số cụ thể chưa chốt), quét cả luồng chưa được quét với nội dung hiện tại; sửa một mình không kích hoạt quét lại. Điểm ≥ 0,9 → tự ẩn, bỏ qua Mod; 0,5–< 0,9 → ẩn và vào hàng chờ Mod; < 0,5 → hiện bình thường. Báo cáo luôn hoạt động độc lập. DEC-083 thêm trạng thái kiểm duyệt Bình thường/Bị ẩn; DEC-099: AI lỗi khi quét bình luận thì giữ nguyên, ghi lỗi. Bình luận bị ẩn không hiện trong luồng cho ai, kể cả tác giả; tác giả nhận thông báo "Bình luận của bạn đã bị ẩn" khi AI ẩn và xem lại bình luận từ thông báo (DEC-180). Ý "author only sees it" của DEC-077 và "quét mọi bình luận mới, thời gian thực" của QA-017 bị thay. |
| QA-020 → DEC-079 → DEC-122 | Mức HEAVY không được tạo bình luận (chỉ đọc, vote); MEDIUM vẫn bình luận được. Trạng thái cảnh cáo không hiện trên bình luận. Tài khoản BANNED: bình luận vẫn hiện, cạnh tên tác giả có nhãn "Tài khoản đã bị khóa". DEC-118, DEC-163 (ngoài bảng nguồn) không đổi phần bình luận. |
| QA-019, QA-020 → DEC-115, DEC-180 | Khiếu nại xóa nội dung chỉ áp dụng cho bài; bình luận không có khiếu nại riêng (DEC-180 giữ nguyên), điểm đã trừ giữ nguyên. Khiếu nại cảnh cáo, ban gắn với bình luận vẫn có; bình luận có hiện lại khi khiếu nại đó thành công không là TBD-M04-01 (OPEN-012). |
| DEC-012, QA-028 → DEC-033 → DEC-167 | Khóa bình luận (tác giả hoặc Mod đặt) chặn bình luận mới; Khóa toàn bộ (chỉ Mod) chặn bình luận mới và upvote; bookmark, báo cáo vẫn dùng được. Bình luận đã có vẫn hiển thị. |
| DEC-105 → DEC-113 | Thành viên rời hoặc bị đuổi khỏi nhóm: bình luận giữ nguyên. Điểm từ upvote bình luận chỉ bị trừ khi tác giả tự xóa hoặc Mod, Admin ẩn vì vi phạm; bình luận bị ẩn theo bài cha không bị trừ. Câu "trừ sau cửa sổ xóa mềm 7 ngày" không khớp với bình luận (bình luận không có thời hạn khôi phục, DEC-043, DEC-179) — thuộc M12, ghi lại để đối chiếu khi viết FR-M12. |
| DM-11.4, DG-6, GL:Summarization, DM-x02 → QA-007 | Tóm tắt bằng AI chỉ áp dụng cho bài, không tóm tắt luồng bình luận (câu trả lời QA thắng draft theo thứ tự ưu tiên). |
| DM-10.1 → DEC-072 | Báo cáo bình luận có 7 lý do (như bài, bỏ "Đạo văn/Vi phạm bản quyền"); chỉ người đã đăng nhập được báo cáo. |
| QA-022, QA-035, QA-037 → DEC-053 | Bình luận không được tìm kiếm. Ý "bình luận tìm bằng FTS" của QA-037 bị thay. |
| DEC-052, QA-106, DM-7.2 → DEC-145 | Trending Topic/Tag tính mỗi bình luận (gồm trả lời) là 1; bình luận đã xóa không tính; upvote bình luận không tính. |
| DEC-129 → DEC-156, DEC-179 | Nguyên tắc chỉ xóa hẳn khi an toàn. Với bình luận, DEC-179 chốt không bao giờ xóa hẳn: xóa chỉ gắn cờ, nội dung giữ vĩnh viễn. DEC-156 chỉ sửa phần tin nhắn, nhật ký. |
| QA-011 → DEC-171 | Guest xem bình luận, không báo cáo, không tương tác (QA-011) giữ nguyên. DEC-171 (ngoài bảng nguồn) chỉ thêm quyền Guest xem trang hồ sơ (M02). |
| DM-8.1 → DEC-065 → DEC-180 | Sự kiện thông báo về bình luận: bình luận mới, trả lời, nhắc tên, upvote bình luận (gộp trong 5 phút, DEC-066), và "Bình luận của bạn đã bị ẩn" khi AI ẩn bình luận (chỉ trong ứng dụng, DEC-180). Sự kiện "Comment được đánh dấu Accepted Answer" bỏ (DEC-169). |
| DEC-039, DEC-046 → DEC-183 | Trích dẫn khi trả lời chỉ là một dòng hiển thị phía trên trả lời, dựng từ tên tác giả và nội dung hiện tại của bình luận được trả lời; không chèn vào nội dung trả lời, không tính vào độ dài. Ý "editor auto-inserts blockquote with original content" của DEC-046 và "blockquote (for quote-reply)" của DEC-039 bị thay; định dạng trích dẫn tác giả tự gõ vẫn có và được tính. Nội dung bình luận tối đa 1.000 từ, đếm như DEC-164, không được trống. |
| DEC-042 → DEC-182 | Sắp xếp Top, Mới nhất, Cũ nhất giữ như DEC-042; Top cùng số upvote thì bình luận đăng trước đứng trước. Số bình luận của bài = bình luận gốc và trả lời hiển thị bình thường, không tính dấu và bình luận bị ẩn. |
| DEC-163 → DEC-178 | Mức cảnh cáo HEAVY chỉ chặn tạo bình luận mới; tác giả vẫn sửa, xóa bình luận đã có (cùng nguyên tắc DEC-163 cho bài). Bài bị khóa: không sửa, được xóa. Bình luận bị ẩn: không sửa, không xóa. |
| DM-10.2, GL:Moderator (MOD) → DEC-180 | Với bình luận của người khác, Mod, Admin chỉ có thao tác Ẩn; "Delete comment" của draft là Ẩn. Mod, Admin xem nội dung bình luận đã xóa qua báo cáo, lịch sử báo cáo, khiếu nại (DEC-179). |
| DEC-077, DEC-115 → DEC-179 | Chủ bình luận xem lại, chỉ đọc, bình luận của mình bị ẩn hoặc bị xử lý khi mở từ thông báo xử lý (DEC-074) hoặc khiếu nại; không thấy thông tin người báo cáo. |
| DEC-079 → DEC-211; QA-011 → DEC-208 (M06) | Chỉ sửa phần thuộc M06: cách áp giảm hạng ×0,5 khi tìm bài (DEC-211); Guest tìm bài bằng full-text (DEC-208). Bình luận vẫn không được tìm; quyền Guest xem bình luận không đổi. |
| OPEN-012 → DEC-201 | Bình luận bị ẩn không hiện lại khi cảnh cáo, ban gắn với nó bị lật. |
| DEC-077 → DEC-195 | Bình luận của Admin không bị AI quét và không báo cáo được; phần còn lại của việc quét sau khi đăng giữ nguyên (M08). |
| DEC-113 → DEC-231, DEC-241 | Bình luận do tác giả tự xóa bị trừ điểm ngay lúc xóa (không chờ 7 ngày như bài); bình luận bị AI ẩn ≥ 0,9 trừ ngay, 0,5–< 0,9 trừ khi Mod kết luận vi phạm; gỡ khỏi nhóm không trừ. Việc trừ điểm thuộc M12. |
| DEC-167 → DEC-246 | Khóa toàn bộ chặn upvote và rút upvote trên bài và trên mọi bình luận của bài (M03 FR-M03-14.06, M12); yêu cầu bình luận của M04 không đổi (rà soát chéo 2026-10-24). |
| DEC-195 → DEC-240; QA-227 → DEC-260 | Không đổi hành vi M04: bài của Owner nhóm không qua duyệt của nhóm (M11); tab mặc định của trang chủ (M14). |
