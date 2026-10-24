---
module: M11
ten_module: Group
ma_tai_lieu: FR-M11
phien_ban: 1.3
trang_thai: Đã chốt
ngay: 2026-10-24
tac_gia: Phạm Văn Đức
moc_nguon: DEC-271, QA-477, ISS-415, OPEN-012
steps_completed: [1, 2, 3, 4, 5, 6, 7]
---
# Tài liệu yêu cầu chức năng — M11 Group

| Mã tài liệu | FR-M11 |
|---|---|
| Dự án | iShare |
| Module | M11 — Group |
| Trạng thái | Đã chốt |
| Phiên bản | 1.3 |
| Ngày | 2026-10-24 |
| Tác giả | Phạm Văn Đức |

<!-- Quy ước chung cho mọi bảng dưới đây:
     - Thân tài liệu không ghi nguồn. Nguồn của mọi ID nằm ở Phụ lục A.
     - Ô không có nội dung ghi "—". Không xóa cột.
     - Mục chưa tới bước làm thì để dòng "(Chưa làm — bước N)". -->

## 1. Tổng quan

### 1.1 Mục đích

Group là không gian nhóm dạng cộng đồng, tương tự group Facebook: người dùng tạo nhóm Public hoặc Private, mời và duyệt
thành viên, đăng bài và thảo luận trong nhóm. Nhóm tái dùng gần như toàn bộ cơ chế của Forum (bài viết, bình luận, star,
báo cáo, kiểm duyệt, AI, thông báo), chỉ thêm nhóm, thành viên nhóm và cổng duyệt đăng bài riêng của nhóm, có lọc thêm
theo quyền xem khi nhóm ở chế độ Private.

### 1.2 Phạm vi

**Trong phạm vi:**

- Tạo, sửa, xóa nhóm: tên, mô tả, chế độ Public hoặc Private, câu hỏi tham gia tùy chọn; mọi người dùng đã đăng nhập tạo
  được, có giới hạn số nhóm tạo mỗi ngày, không giới hạn số nhóm sở hữu hay tham gia. Xóa nhóm là xóa mềm.
- Vai trò trong nhóm: Owner, Group Mod, Member, theo thứ bậc; bổ nhiệm, giáng Group Mod; kick thành viên.
- Tham gia nhóm: vào ngay, gửi yêu cầu kèm câu trả lời, rút yêu cầu, Owner/Group Mod duyệt hoặc từ chối, chặn và bỏ
  chặn người gửi yêu cầu; mời và link mời chung của nhóm; danh sách thành viên; rời nhóm.
- Kế nhiệm Owner: Owner tự rời phải chỉ định người kế nhiệm; Owner mất quyền ngoài ý muốn thì hệ thống tự chuyển.
- Đăng bài trong nhóm: cổng duyệt của nhóm (công tắc duyệt trước, ngưỡng điểm quét AI), hàng chờ duyệt của nhóm; Group
  Mod/Owner gỡ bài và bình luận khỏi nhóm; quyết định cấp nhóm không có khiếu nại.
- Đăng ẩn danh trong nhóm: công tắc do Owner bật, tắt; thành viên chọn ẩn danh cho từng bài; Group Mod/Owner thấy danh tính
  thật.
- Danh sách nhóm và trang nhóm; quyền xem: nhóm Public và Private, Guest với nhóm; đổi chế độ Public↔Private; bài nhóm
  trong feed của thành viên và bài nhóm Public hiện ở feed chính.
- Hành vi của nhóm khi bị Ẩn hoặc Khóa (M08 quyết định), khi cờ tính năng Group tắt (M10 bật tắt), và với bài của ADMIN
  trong nhóm.
- Nội dung của thành viên khi rời nhóm, bị kick, và khi nhóm bị xóa.

**Ngoài phạm vi:**

- Group Chat — M16 Chat & Messaging (cuộc trò chuyện nhiều người độc lập, không gắn với nhóm).
- Tìm nhóm theo tên, gợi ý khi gõ, quy tắc nhóm Private không hiện với người ngoài nhóm khi tìm — M06 Search.
- Tab Group của feed (gom bài mọi nhóm đã tham gia), bài nhóm Public trong Trending (không vào Newest) và tab Following — M14 Feed & Discovery;
  Trending Topic/Tag tính bài nhóm Public — M05 Topic & Tag.
- Gửi thông báo các sự kiện nhóm (mời, tham gia, duyệt, bổ nhiệm, kick) — M07 Notification.
- Báo cáo nhóm, thao tác Ẩn/Khóa/Mở khóa nhóm, nhật ký kiểm duyệt, quét AI và kiểm duyệt hệ thống của bài, bình luận — M08
  Moderation, M13 AI Layer; khiếu nại — M09 Appeal.
- Cơ chế chung của bài viết, bình luận, star, bookmark — M03 Post & Content, M04 Comment, M02 User Profile; thứ tự gợi ý
  @mention theo nhóm — M01 Authentication & Account.
- Điểm, trừ điểm khi nội dung mất đi — M12 Gamification; bật, tắt cờ tính năng Group — M10 Admin Panel.
- Đã quyết không làm: leaderboard, reputation riêng theo nhóm; theo dõi (follow) nhóm; thực thể lời mời riêng có chấp
  nhận/từ chối; thời gian chờ khi gửi lại yêu cầu tham gia; khiếu nại quyết định kiểm duyệt cấp nhóm; giới hạn số nhóm
  tham gia hoặc sở hữu; thu hồi hoặc tạo lại link mời.

## 2. Thuật ngữ và viết tắt

### 2.1 Thuật ngữ

| Thuật ngữ | Định nghĩa |
|---|---|
| Nhóm | Không gian cộng đồng trong iShare, tái dùng cơ chế bài viết, bình luận, star, báo cáo của Forum; có tên, mô tả, chế độ Public hoặc Private và các thành viên. |
| Nhóm Public | Nhóm mọi người, kể cả Guest, thấy được trong danh sách và xem được thông tin, nội dung. |
| Nhóm Private | Nhóm chỉ thành viên thấy và xem được; người ngoài nhóm, kể cả Guest, không thấy nhóm ở danh sách, tìm kiếm, gợi ý; chỉ tới được qua lời mời hoặc link mời. |
| Thành viên nhóm | Người dùng đã vào một nhóm, mang đúng một vai trò nhóm trong nhóm đó. |
| Vai trò nhóm | Một trong ba giá trị Owner, Group Mod, Member, theo thứ bậc Member < Group Mod < Owner. Khác vai trò hệ thống USER, MODERATOR, ADMIN (M10). |
| Owner | Chủ nhóm; ban đầu là người tạo nhóm; mỗi nhóm có đúng một Owner. |
| Group Mod | Thành viên được Owner bổ nhiệm làm người kiểm duyệt của riêng nhóm đó. Khác Mod (vai trò hệ thống MODERATOR). |
| Member | Thành viên thường của nhóm. |
| Người ngoài nhóm | Người dùng đã đăng nhập nhưng không phải thành viên của nhóm đang xét. |
| Câu hỏi tham gia | Một câu hỏi tùy chọn do Owner đặt cho nhóm; người xin vào trả lời khi gửi yêu cầu tham gia. |
| Yêu cầu tham gia | Đề nghị vào nhóm của một người ngoài nhóm, chờ Owner hoặc Group Mod duyệt; kèm câu trả lời khi nhóm có câu hỏi tham gia. Trạng thái: Chờ duyệt, Đã chấp nhận, Đã từ chối, Đã rút. |
| Lời mời, link mời | Cách một thành viên đưa người khác tới nhóm. Mỗi nhóm có một link mời chung, không hết hạn, không thu hồi; mời một người cụ thể là gửi thông báo kèm link này. Không phải thực thể riêng có chấp nhận, từ chối; người được mời vào nhóm theo luồng tham gia. |
| Chặn tham gia | Owner hoặc Group Mod chặn một người dùng để người đó không vào được nhóm bằng bất kỳ cách nào; Owner, Group Mod xem được danh sách chặn và bỏ chặn. |
| Kick | Owner hoặc Group Mod đưa một thành viên ra khỏi nhóm; xử lý như thành viên tự rời. |
| Công tắc duyệt trước | Cài đặt của nhóm do Owner bật, tắt; khi bật, bài có điểm quét < 0.5 cũng phải chờ Owner hoặc Group Mod duyệt. |
| Công tắc ẩn danh | Cài đặt của nhóm do Owner bật, tắt; khi bật, thành viên chọn đăng ẩn danh cho từng bài mới. |
| Bài nhóm | Bài viết (M03) thuộc một nhóm. Một bài thuộc tối đa một nhóm. |
| Bài ẩn danh | Bài nhóm mà tác giả chọn ẩn danh; người xem thường thấy "Ẩn danh" thay cho tác giả, hệ thống vẫn giữ danh tính thật. |
| Điểm quét | Con số từ 0 đến 1 mà việc quét AI trả về cho một bài (M08, M13). |
| Cổng duyệt của nhóm | Bước quyết định bài gửi vào nhóm được đăng ngay, chờ nhóm duyệt hay bị từ chối, dựa vào điểm quét và công tắc duyệt trước. Chồng lên kiểm duyệt hệ thống, không thay nó. Bài của Owner không qua cổng này (BR-M11-40). |
| Hàng chờ duyệt của nhóm | Danh sách bài của một nhóm đang chờ Owner hoặc Group Mod duyệt; tách khỏi hàng chờ báo cáo (M08). |
| Nhận bài | Owner hoặc Group Mod giữ một bài trong hàng chờ duyệt của nhóm để xử lý; trong lúc đó người khác không xử lý được bài này. |
| Thời điểm thao tác cuối | Lần gần nhất người đang giữ bài làm một thao tác trên bài đó (mở xem, chấp nhận, từ chối); dùng để tính 30 phút tự nhả. |
| Kế nhiệm Owner | Việc chuyển vai trò Owner sang một thành viên khác: tự nguyện (Owner chỉ định trước khi rời) hoặc bắt buộc (hệ thống tự chọn khi Owner mất quyền ngoài ý muốn). |
| Owner mất quyền ngoài ý muốn | Tài khoản Owner bị ban (tạm thời hoặc vĩnh viễn), bị vô hiệu hóa (kể cả tự vô hiệu hóa) hoặc bị xóa (M01, M08); Owner không có cơ hội chỉ định người kế nhiệm. |
| Thời điểm tham gia | Lúc người dùng trở thành thành viên nhóm: lúc vào ngay, lúc yêu cầu tham gia được chấp nhận, hoặc lúc tạo nhóm với Owner đầu tiên. |
| Thâm niên Group Mod | Khoảng thời gian một thành viên đang giữ vai trò Group Mod, tính từ lần bổ nhiệm gần nhất. Người đã bị giáng về Member không được tính là Group Mod. |
| Xóa nhóm | Owner xóa nhóm: xóa mềm, nhóm và mọi nội dung không hiện với ai kể cả thành viên cũ, dữ liệu vẫn được giữ. |
| Trạng thái kiểm duyệt của nhóm | Bình thường, Bị khóa, Bị ẩn; do Mod, Admin quyết khi xử lý vụ báo cáo nhóm (M08); M11 áp lên cách nhóm hiển thị và thao tác được phép. |
| Quyết định kiểm duyệt cấp nhóm | Thao tác kiểm duyệt do Owner hoặc Group Mod làm trong nhóm: từ chối bài chờ duyệt, gỡ bài, bình luận khỏi nhóm. Không khiếu nại được. Bài bị AI tự từ chối không phải quyết định cấp nhóm. |
| Feed chính | Các luồng bài chung của iShare ngoài trang nhóm (M14): Trending, Newest, Following. |
| Cờ tính năng Group | Công tắc cấu hình (M10) bật hoặc tắt cả module Group. |
| Giờ Việt Nam | Múi giờ Asia/Ho_Chi_Minh (UTC+7); mọi ranh giới ngày và thời điểm hiển thị trong module tính theo múi giờ này. |
| Gỡ khỏi nhóm | Thao tác duy nhất để Owner, Group Mod bỏ một bài hoặc bình luận khỏi nhóm: xóa mềm; nội dung chỉ còn hiện với tác giả, Owner, Group Mod của nhóm, Mod và Admin; tác giả không tự hiện lại được. |
| Nhóm vào ngay | Nhóm Public không có câu hỏi tham gia: người ngoài nhóm chọn tham gia là thành viên ngay. |
| Trang danh sách nhóm | Trang liệt kê các nhóm Private mà người xem là thành viên và các nhóm Public, mới nhất trước; nơi nút "Khám phá Group" của M14 dẫn tới. |
| 24 giờ gần nhất | Khoảng 24 × 60 phút ngay trước thời điểm người dùng tạo nhóm; nhóm tạo đúng 24 giờ trước không còn nằm trong khoảng. |
| Ký tự (tên, mô tả nhóm) | Đơn vị đếm độ dài tên và mô tả nhóm: số ký tự của nội dung. |
| Trạng thái tồn tại của nhóm | Hoạt động hoặc Đã xóa (Owner xóa, hoặc nhóm bị xóa mềm khi Owner là thành viên cuối cùng). Khác trạng thái kiểm duyệt của nhóm. |
| Chờ duyệt (đang quét), Chờ duyệt (chờ nhóm duyệt) | Hai giai đoạn của trạng thái đăng Chờ duyệt (M03) với bài nhóm: đang được AI quét; đã vào hàng chờ duyệt của nhóm. Người khác tác giả không thấy bài trong cả hai giai đoạn. |
| Bị gỡ khỏi nhóm | Dấu đặt trên bài, bình luận khi Owner hoặc Group Mod gỡ khỏi nhóm (xóa mềm). Không phải trạng thái đăng: bài giữ trạng thái đăng của nó (M03). |
| Đã rút | Trạng thái của yêu cầu tham gia sau khi người gửi tự rút. |

### 2.2 Viết tắt

| Viết tắt | Đầy đủ |
|---|---|
| FR | Functional Requirement — yêu cầu chức năng |
| BR | Business Rule — quy tắc nghiệp vụ |
| TBD | To Be Determined — điểm chưa chốt |
| AI | Trí tuệ nhân tạo; ở module này là việc quét bài để chấm điểm vi phạm (M13) |

## 3. Thông tin đầu vào

### 3.1 Tài liệu đầu vào

| Tài liệu | Phiên bản / mốc |
|---|---|
| Draft: docs/_temp/iShare_modules.md, iShare_specs_general.md | Theo ngày sửa tệp |
| Register: decisions, qa-log, issue-queue, open-issues, glossary, module-registry | DEC-271, QA-477, ISS-415, OPEN-012 (khớp `moc_nguon`) |

### 3.2 Tài liệu liên quan

| Module | Liên quan ở điểm nào |
|---|---|
| M01 Authentication & Account | Thứ tự gợi ý @mention ưu tiên người cùng nhóm; trạng thái tài khoản (ban, vô hiệu hóa, xóa) kích hoạt kế nhiệm Owner. |
| M02 User Profile | Tab Bài viết và Bookmark chỉ hiện bài nhóm Private với thành viên. |
| M03 Post & Content, M04 Comment | Bài nhóm là bài viết chung có gắn nhóm; cơ chế bình luận, star, xóa mềm dùng chung. |
| M05 Topic & Tag | Trending tính bài nhóm Public, không tính bài nhóm Private. |
| M06 Search | Tìm nhóm theo tên; nhóm Private không hiện với người ngoài nhóm; nội dung nhóm Private chỉ hiện với thành viên. |
| M07 Notification | Gửi thông báo sự kiện nhóm (mời, yêu cầu tham gia mới, được duyệt, được bổ nhiệm, bị kick, trở thành Owner, bị gỡ khỏi nhóm); không theo dõi được nhóm. |
| M08 Moderation, M13 AI Layer | Quét AI trước khi đăng; báo cáo nhóm; Ẩn, Khóa nhóm; kiểm duyệt hệ thống vẫn áp dụng trong nhóm. |
| M09 Appeal | Quyết định cấp nhóm không có khiếu nại; nhóm bị Ẩn/Khóa không có link khiếu nại. |
| M10 Admin Panel | Cờ tính năng Group. |
| M12 Gamification | Xóa nhóm không trừ điểm; không có leaderboard theo nhóm. |
| M14 Feed & Discovery | Tab Group; bài nhóm Public ở Trending và tab Following; nút "Khám phá Group" dẫn sang trang danh sách/tìm nhóm. |
| M16 Chat & Messaging | Group Chat độc lập với nhóm. |

## 4. Tổng quan chức năng

### 4.1 Luật, tiêu chuẩn liên quan

Không có.

### 4.2 Vai trò

| Vai trò | Mô tả trong module này |
|---|---|
| Guest | Người chưa đăng nhập. Xem danh sách nhóm Public, thông tin và nội dung nhóm Public; không thấy nhóm Private; không tạo, tham gia nhóm hay thao tác gì khác. |
| User | Người dùng đã đăng nhập. Tạo nhóm; với nhóm mình chưa tham gia (người ngoài nhóm): xem nhóm Public, tham gia hoặc gửi yêu cầu tham gia. Trong một nhóm cụ thể, User mang một trong ba vai trò nhóm bên dưới. |
| Member | Vai trò theo ngữ cảnh: thành viên thường của một nhóm. Xem nội dung nhóm, đăng bài, bình luận, vote, mời người khác, chọn đăng ẩn danh khi nhóm bật, rời nhóm. |
| Group Mod | Vai trò theo ngữ cảnh: thành viên được Owner bổ nhiệm. Có quyền của Member, thêm: duyệt bài chờ đăng của nhóm, gỡ bài và bình luận khỏi nhóm, duyệt yêu cầu tham gia, chặn người gửi yêu cầu, kick Member; thấy danh tính thật của bài ẩn danh trong nhóm. Không tác động lên Group Mod khác hay Owner. |
| Owner | Vai trò theo ngữ cảnh: chủ nhóm, ban đầu là người tạo. Có quyền của Group Mod, thêm: bổ nhiệm, giáng Group Mod, kick Group Mod, đổi cài đặt nhóm, xóa nhóm. Mỗi nhóm có đúng một Owner; muốn rời phải chỉ định người kế nhiệm. Bài của Owner trong nhóm không qua duyệt của nhóm. |
| Mod | Vai trò hệ thống MODERATOR. Trong nhóm mình không tham gia, Mod không có vai trò nhóm: không thấy, không mở được nhóm Private, chỉ xem nội dung nhóm Private trong vụ báo cáo mình đang giữ; không duyệt bài chờ của nhóm; can thiệp nội dung nhóm qua kiểm duyệt hệ thống (M08); thấy danh tính thật của bài ẩn danh. |
| Admin | Có quyền của Mod. Vẫn dùng được module khi cờ Group tắt. Bài của Admin trong nhóm không bị AI quét, đi theo công tắc duyệt trước của nhóm; Admin là Owner thì đăng ngay. Bị giới hạn tạo nhóm như người dùng khác. |
| Hệ thống | Quyết định bài gửi vào nhóm được đăng, chờ nhóm duyệt hay bị từ chối; tự chuyển quyền Owner khi Owner mất quyền ngoài ý muốn; áp dụng trạng thái Ẩn, Khóa của nhóm; chặn thao tác khi cờ Group tắt. |

### 4.3 Ma trận quyền

Cột Member, Group Mod, Owner là vai trò của người dùng trong chính nhóm đang xét; cột User là người dùng đã đăng nhập
nhưng không phải thành viên nhóm đó; cột Mod, Admin là tài khoản có vai trò hệ thống đó nhưng không là thành viên nhóm.

| Hành động | Guest | User | Member | Group Mod | Owner | Mod | Admin | Yêu cầu |
|---|---|---|---|---|---|---|---|---|
| Tạo nhóm | ✗ | ✓ | — | — | — | ✓ | ✓ | FR-M11-01.01, FR-M11-01.04 |
| Xem danh sách nhóm, thông tin và nội dung nhóm Public | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | FR-M11-03.01, FR-M11-03.04 |
| Thấy nhóm Private, xem thông tin và nội dung nhóm Private | ✗ | ✗ | ✓ | ✓ | ✓ | ✗ (trừ trong vụ báo cáo) | ✗ (trừ trong vụ báo cáo) | FR-M11-03.02, FR-M11-03.05, FR-M11-03.06, FR-M11-03.11, FR-M11-03.12 |
| Sửa tên, mô tả nhóm | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ | FR-M11-02.01, FR-M11-02.10 |
| Đổi cài đặt nhóm (Public/Private, duyệt trước, ẩn danh, câu hỏi tham gia) | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ | FR-M11-02.02, FR-M11-02.09 |
| Tham gia nhóm hoặc gửi yêu cầu tham gia | ✗ | ✓ | — | — | — | ✓ | ✓ | FR-M11-04.01, FR-M11-04.03, FR-M11-04.05 |
| Mời người khác vào nhóm | ✗ | ✗ | ✓ | ✓ | ✓ | ✗ | ✗ | FR-M11-05.01, FR-M11-05.03 |
| Duyệt, từ chối yêu cầu tham gia | ✗ | ✗ | ✗ | ✓ | ✓ | ✗ | ✗ | FR-M11-06.02, FR-M11-06.03, FR-M11-06.05 |
| Chặn người gửi yêu cầu tham gia, xem danh sách chặn, bỏ chặn | ✗ | ✗ | ✗ | ✓ | ✓ | ✗ | ✗ | FR-M11-07.01, FR-M11-07.02, FR-M11-07.04, FR-M11-07.05 |
| Bổ nhiệm, giáng Group Mod | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ | FR-M11-08.01, FR-M11-08.02, FR-M11-08.04 |
| Kick Member | ✗ | ✗ | ✗ | ✓ | ✓ | ✗ | ✗ | FR-M11-09.01, FR-M11-09.02, FR-M11-09.04 |
| Kick Group Mod | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ | FR-M11-09.01, FR-M11-09.03, FR-M11-09.04 |
| Rời nhóm | — | — | ✓ | ✓ | ✓ (sau khi chỉ định người kế nhiệm) | — | — | FR-M11-10.01, FR-M11-10.04, FR-M11-10.05 |
| Đăng bài trong nhóm | ✗ | ✗ | ✓ | ✓ | ✓ | ✗ | ✗ | FR-M11-12.01, FR-M11-12.11 |
| Bình luận, vote, báo cáo, bookmark bài trong nhóm Public | ✗ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | FR-M11-03.08, FR-M11-03.13 |
| Bình luận, vote bài trong nhóm Private | ✗ | ✗ | ✓ | ✓ | ✓ | ✗ | ✗ | FR-M11-03.07, FR-M11-03.08 |
| Chọn đăng ẩn danh (khi nhóm bật ẩn danh) | ✗ | ✗ | ✓ | ✓ | ✓ | ✗ | ✗ | FR-M11-12.07, FR-M11-12.11 |
| Xem danh tính thật tác giả bài ẩn danh trong nhóm | ✗ | ✗ | ✗ | ✓ | ✓ | ✓ | ✓ | FR-M11-03.09, FR-M11-03.10 |
| Duyệt bài chờ đăng của nhóm | ✗ | ✗ | ✗ | ✓ | ✓ | ✗ | ✗ | FR-M11-13.01, FR-M11-13.08, FR-M11-13.09 |
| Gỡ bài, bình luận khỏi nhóm bằng quyền của nhóm | ✗ | ✗ | ✗ | ✓ | ✓ | — | — | FR-M11-14.01, FR-M11-14.02 |
| Tự duyệt bài chờ của chính mình | — | — | — | ✗ | — (bài của Owner không vào hàng chờ của nhóm) | — | — | FR-M11-13.13, FR-M11-12.16 |
| Xem danh sách thành viên | ✓ (nhóm Public) | ✓ (nhóm Public) | ✓ | ✓ | ✓ | ✓ (nhóm Public) | ✓ (nhóm Public) | FR-M11-03.14, FR-M11-03.15 |
| Rút yêu cầu tham gia | ✗ | ✓ (của mình) | — | — | — | ✓ (của mình) | ✓ (của mình) | FR-M11-04.10 |
| Gỡ bài, bình luận của Owner hoặc Group Mod khác | ✗ | ✗ | ✗ | ✗ | ✓ (của Group Mod) | — | — | FR-M11-14.08 |
| Thao tác quản trị trong nhóm Bị khóa | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | FR-M11-16.07, FR-M11-16.08 |
| Tự rời nhóm Bị khóa | — | — | ✓ | ✓ | ✗ | — | — | FR-M11-16.08, FR-M11-16.09 |
| Khiếu nại quyết định kiểm duyệt của nhóm | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | FR-M11-13.07, FR-M11-14.03 |
| Xóa nhóm | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ | FR-M11-15.01, FR-M11-15.04 |
| Đăng, bình luận, vote, bình chọn, tham gia, mời trong nhóm bị Khóa | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | FR-M11-16.04 |
| Thấy nhóm bị Ẩn và nội dung của nhóm | ✗ | ✗ | ✗ | ✗ | ✗ | — | — | FR-M11-16.01 |
| Dùng module khi cờ Group tắt | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | FR-M11-17.01, FR-M11-17.03 |

<!-- Ô nói thẳng: hàng 1 (DEC-101 mọi người đã đăng nhập; DEC-126 Guest cần đăng nhập); hàng 2 (QA-011 Guest xem
     danh sách, mô tả, nội dung nhóm công khai); hàng 3 cột Guest, User (QA-011, DEC-110, DEC-210); hàng 5, 8, 10–12,
     22 (DEC-102); hàng 7 (DEC-110 mọi thành viên mời được); hàng 9 (DEC-103 Owner/Mod chặn); hàng 13 (DEC-107);
     hàng 14 cột thành viên (DEC-102); hàng 16 cột User (DEC-108 nhóm Private không tương tác được với người ngoài);
     hàng 17 (DEC-112); hàng 18 (DEC-112 Group Mod, Owner; QA-015 MODERATOR, ADMIN); hàng 19, 20 (DEC-102, DEC-104);
     hàng 21 (DEC-109); hàng 23 (DEC-194 chặn với mọi người kể cả Owner, Group Mod); hàng 24 (DEC-194 không ai thấy,
     kể cả thành viên, Owner); hàng 25 (DEC-225 Admin vẫn dùng được).
     Ô suy ra: hàng 1, 6 cột Mod, Admin (Mod, Admin có quyền của User); hàng 4 cột Owner (F-GRP-01 "Edit group",
     DEC-102 cài đặt chỉ Owner); hàng 4, 5 các cột còn lại ✗ (DEC-102 chỉ Owner đổi cài đặt); hàng 6 cột Guest
     (DEC-126 tham gia cần đăng nhập); hàng 7 cột User, Mod, Admin (chỉ thành viên mời, DEC-110); hàng 14 cột User,
     Mod, Admin (DEC-102 liệt kê đăng bài là quyền của thành viên); hàng 15, 16 cột Guest (QA-011 tương tác cần đăng
     nhập); hàng 16 cột Mod, Admin (như cột User); hàng 17 cột không phải thành viên (chỉ thành viên đăng bài trong
     nhóm); hàng 18 cột Guest, User, Member (bài ẩn danh ẩn tác giả với người xem khác, QA-015, DEC-112); hàng 22 cột
     Mod, Admin (chỉ Owner xóa nhóm, DEC-102; Ẩn nhóm là thao tác M08).
     "—": hàng 1, 6 cột vai trò nhóm (tạo, tham gia không gắn với vai trò trong nhóm đó); hàng 13 người không thuộc
     nhóm; hàng 20, 24 cột Mod, Admin (can thiệp qua kiểm duyệt hệ thống M08, không qua quyền của nhóm).
     Sau bước 6: hàng 3 cột Mod, Admin, hàng "Duyệt bài chờ" cột Mod, Admin (DEC-233); hàng 4 cột Group Mod (DEC-237);
     hàng "Bình luận, vote, báo cáo, bookmark bài trong nhóm Public" (DEC-234); các hàng thêm: tự duyệt (DEC-237), danh
     sách thành viên, rút yêu cầu, danh sách chặn (DEC-238), gỡ nội dung của Owner, Group Mod (DEC-231), nhóm Bị khóa
     (DEC-235). -->

### 4.4 Danh sách chức năng

| ID | Chức năng | Tác nhân chính | Kích hoạt |
|---|---|---|---|
| FR-M11-01 | Tạo nhóm | User | Người dùng chọn tạo nhóm |
| FR-M11-02 | Sửa thông tin và cài đặt nhóm | Owner | Owner mở phần cài đặt của nhóm và lưu thay đổi |
| FR-M11-03 | Xem danh sách nhóm và trang nhóm | Guest, User | Người xem mở danh sách nhóm hoặc trang một nhóm |
| FR-M11-04 | Tham gia nhóm | User (người ngoài nhóm) | Người dùng chọn tham gia một nhóm |
| FR-M11-05 | Mời người khác vào nhóm | Member, Group Mod, Owner | Thành viên chọn mời hoặc lấy link mời của nhóm |
| FR-M11-06 | Duyệt yêu cầu tham gia | Owner, Group Mod | Owner hoặc Group Mod mở danh sách yêu cầu tham gia và chọn chấp nhận hoặc từ chối |
| FR-M11-07 | Chặn người gửi yêu cầu tham gia | Owner, Group Mod | Owner hoặc Group Mod chọn chặn một người gửi yêu cầu |
| FR-M11-08 | Bổ nhiệm, giáng Group Mod | Owner | Owner chọn bổ nhiệm một Member hoặc giáng một Group Mod |
| FR-M11-09 | Kick thành viên khỏi nhóm | Owner, Group Mod | Owner hoặc Group Mod chọn kick một thành viên |
| FR-M11-10 | Rời nhóm | Member, Group Mod, Owner | Thành viên chọn rời nhóm |
| FR-M11-11 | Tự chuyển quyền Owner khi Owner mất quyền | Hệ thống | Tài khoản Owner bị ban, vô hiệu hóa hoặc xóa |
| FR-M11-12 | Đăng bài trong nhóm | Member, Group Mod, Owner | Thành viên gửi bài trong nhóm |
| FR-M11-13 | Duyệt bài chờ đăng của nhóm | Owner, Group Mod | Owner hoặc Group Mod mở hàng chờ duyệt của nhóm và nhận một bài |
| FR-M11-14 | Gỡ bài và bình luận khỏi nhóm | Owner, Group Mod | Owner hoặc Group Mod chọn gỡ một bài, bình luận khỏi nhóm |
| FR-M11-15 | Xóa nhóm | Owner | Owner chọn xóa nhóm, hoặc Owner là thành viên duy nhất rời nhóm |
| FR-M11-16 | Áp dụng trạng thái Ẩn, Khóa của nhóm | Hệ thống | MOD/ADMIN ẩn, khóa hoặc mở khóa nhóm (M08) |
| FR-M11-17 | Chặn thao tác nhóm khi cờ Group tắt | Hệ thống | Người dùng gửi yêu cầu tới module trong lúc cờ tính năng Group tắt |

### 4.5 Mốc và ưu tiên

Toàn bộ yêu cầu của module thuộc MS1 (MS1 gồm đủ chức năng của mọi module), ưu tiên **Should** (dòng M11 của bảng
Module List và bảng MoSCoW Summary của module-registry khớp nhau: Should gồm M11, M12, M16). Không có yêu cầu ngoại lệ về
ưu tiên.

## 5. Yêu cầu chức năng

### 5.1 FR-M11-01 Tạo nhóm

**Yêu cầu cấp trên:** Hệ thống phải cho phép người dùng đã đăng nhập tạo nhóm với tên, mô tả, chế độ Public hoặc Private, và trở thành Owner của nhóm.

**Lý do:** Mọi người dùng đã đăng nhập được tự do lập nhóm; giới hạn số nhóm tạo mỗi ngày để chống spam, không giới hạn tổng số nhóm sở hữu.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M11-01.01 | Khi người dùng đã đăng nhập tạo nhóm với tên, mô tả và chế độ Public hoặc Private, hệ thống phải tạo nhóm ở trạng thái Hoạt động và trạng thái kiểm duyệt Bình thường. |
| FR-M11-01.02 | Khi nhóm được tạo, hệ thống phải ghi người tạo là Owner, với thời điểm tham gia là thời điểm tạo nhóm (BR-M11-04). |
| FR-M11-01.03 | Nếu người dùng đã tạo 5 nhóm trong 24 giờ gần nhất tính tới lúc tạo, hệ thống phải từ chối tạo thêm nhóm (BR-M11-03). |
| FR-M11-01.04 | Nếu người chưa đăng nhập chọn tạo nhóm, hệ thống phải từ chối (BR-M11-03). |
| FR-M11-01.05 | Hệ thống phải không giới hạn tổng số nhóm một người dùng sở hữu (BR-M11-03). |
| FR-M11-01.06 | Hệ thống phải tính cả nhóm đã bị xóa vào giới hạn tạo nhóm (BR-M11-03). |
| FR-M11-01.07 | Hệ thống phải áp giới hạn tạo nhóm cho cả Admin (BR-M11-03). |
| FR-M11-01.08 | Nếu tên nhóm để trống hoặc dài hơn 100 ký tự, hệ thống phải từ chối lưu nhóm (BR-M11-31). |
| FR-M11-01.09 | Nếu mô tả nhóm dài hơn 500 ký tự, hệ thống phải từ chối lưu nhóm (BR-M11-31). |
| FR-M11-01.10 | Hệ thống phải cho tên nhóm trùng với tên của nhóm khác (BR-M11-31). |
| FR-M11-01.11 | Khi tạo nhóm, hệ thống phải cho người tạo đặt ngay công tắc duyệt trước, công tắc ẩn danh và câu hỏi tham gia (BR-M11-31). |
| FR-M11-01.12 | Nếu người tạo không đặt, hệ thống phải để công tắc duyệt trước và công tắc ẩn danh ở Tắt, câu hỏi tham gia trống (BR-M11-31). |

### 5.2 FR-M11-02 Sửa thông tin và cài đặt nhóm

**Yêu cầu cấp trên:** Hệ thống phải cho phép Owner sửa tên, mô tả và đổi cài đặt của nhóm: chế độ Public, Private, công tắc duyệt trước, công tắc ẩn danh, câu hỏi tham gia.

**Lý do:** Cài đặt đặt ở cấp Owner để kiểm soát cộng đồng rõ ràng; Owner đổi chế độ hiển thị bất kỳ lúc nào.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M11-02.01 | Khi Owner sửa tên hoặc mô tả nhóm, hệ thống phải lưu và hiển thị nội dung mới. |
| FR-M11-02.02 | Khi Owner đổi chế độ Public sang Private hoặc ngược lại, hệ thống phải áp chế độ mới cho mọi thao tác xảy ra sau thời điểm đổi (BR-M11-15). |
| FR-M11-02.03 | Khi nhóm chuyển sang Private, hệ thống phải từ chối bình luận, vote, báo cáo của người ngoài nhóm trên bài của nhóm (BR-M11-15). |
| FR-M11-02.04 | Khi nhóm chuyển sang Private, hệ thống phải không đưa bài của nhóm cho người ngoài nhóm ở các lần tải feed, tìm kiếm sau đó (BR-M11-15). |
| FR-M11-02.05 | Khi Owner bật hoặc tắt công tắc duyệt trước, hệ thống phải dùng giá trị mới cho các bài gửi vào nhóm sau thời điểm đổi (BR-M11-18). |
| FR-M11-02.06 | Khi Owner tắt công tắc ẩn danh, hệ thống phải giữ ẩn danh cho các bài đã đăng ẩn danh và chỉ chặn lựa chọn ẩn danh cho bài mới (BR-M11-16). |
| FR-M11-02.07 | Khi Owner đặt, sửa hoặc bỏ câu hỏi tham gia, hệ thống phải áp câu hỏi mới cho các yêu cầu tham gia gửi sau đó (BR-M11-08). |
| FR-M11-02.08 | Hệ thống phải cho mỗi nhóm tối đa một câu hỏi tham gia (BR-M11-08). |
| FR-M11-02.09 | Nếu Group Mod, Member hoặc người không là thành viên đổi chế độ, công tắc duyệt trước, công tắc ẩn danh hoặc câu hỏi tham gia, hệ thống phải từ chối (BR-M11-06). |
| FR-M11-02.10 | Nếu Group Mod, Member hoặc người không là thành viên sửa tên, mô tả nhóm, hệ thống phải từ chối (BR-M11-06). |
| FR-M11-02.11 | Nếu tên nhóm được sửa thành trống hoặc dài hơn 100 ký tự, hoặc mô tả dài hơn 500 ký tự, hệ thống phải từ chối lưu (BR-M11-31). |
| FR-M11-02.12 | Khi nhóm chuyển sang Private, hệ thống phải chỉ để người ngoài nhóm đọc những bài của nhóm đang hiện sẵn trên màn hình họ đã tải trước thời điểm đổi (BR-M11-15). |
| FR-M11-02.13 | Nếu người ngoài nhóm tải lại hoặc mở lại bài của nhóm đã chuyển Private bằng link, bookmark hay thông báo, hệ thống phải hiển thị "Nội dung không tồn tại" (BR-M11-15). |
| FR-M11-02.14 | Khi Owner đổi cài đặt làm nhóm thành vào ngay (Private sang Public không có câu hỏi tham gia, hoặc bỏ câu hỏi của nhóm Public), hệ thống phải chấp nhận ngay mọi yêu cầu tham gia đang Chờ duyệt của nhóm (BR-M11-32). |
| FR-M11-02.15 | Khi Owner tắt công tắc duyệt trước, hệ thống phải giữ các bài đang chờ nhóm duyệt trong hàng chờ duyệt của nhóm (BR-M11-18). |

### 5.3 FR-M11-03 Xem danh sách nhóm và trang nhóm

**Yêu cầu cấp trên:** Hệ thống phải cho phép người xem thấy danh sách nhóm và mở trang nhóm theo quyền xem của chế độ Public, Private.

**Lý do:** Nội dung công khai, kể cả nhóm Public, mở cho Guest để được tìm thấy; nhóm Private chỉ dành cho thành viên.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M11-03.01 | Hệ thống phải hiển thị các nhóm Public trong danh sách nhóm với mọi người, kể cả Guest (BR-M11-13). |
| FR-M11-03.02 | Nếu người xem không là thành viên của một nhóm Private, kể cả Guest, hệ thống phải không đưa nhóm đó vào danh sách nhóm (BR-M11-11). |
| FR-M11-03.03 | Khi thành viên của nhóm Private mở danh sách nhóm, hệ thống phải đưa nhóm Private đó vào danh sách (BR-M11-11). |
| FR-M11-03.04 | Khi người xem mở trang một nhóm Public, hệ thống phải hiển thị tên, mô tả và các bài hiển thị công khai của nhóm, kể cả với Guest (BR-M11-13). |
| FR-M11-03.05 | Khi thành viên mở trang nhóm của mình, dù nhóm Public hay Private, hệ thống phải hiển thị tên, mô tả và các bài của nhóm (BR-M11-14). |
| FR-M11-03.06 | Nếu người không là thành viên, kể cả Guest, mở trang hoặc một bài của nhóm Private, hệ thống phải không hiển thị thông tin và nội dung của nhóm, trừ tên, mô tả khi mở qua lời mời (FR-M11-03.18) (BR-M11-13). |
| FR-M11-03.07 | Nếu người không là thành viên bình luận hoặc vote bài của nhóm Private, hệ thống phải từ chối (BR-M11-13). |
| FR-M11-03.08 | Hệ thống phải cho thành viên bình luận và vote bài của nhóm mình (BR-M11-06). |
| FR-M11-03.09 | Khi bài ẩn danh hiển thị với người xem ngoài Owner, Group Mod của nhóm, Mod và Admin, hệ thống phải hiển thị "Ẩn danh" thay cho tác giả (BR-M11-17). |
| FR-M11-03.10 | Khi Owner, Group Mod của nhóm, Mod hoặc Admin xem bài ẩn danh trong nhóm, hệ thống phải hiển thị tác giả thật (BR-M11-17). |
| FR-M11-03.11 | Nếu Mod hoặc Admin không là thành viên tìm, mở danh sách nhóm hoặc mở trang của một nhóm Private, hệ thống phải không hiển thị nhóm đó (BR-M11-33). |
| FR-M11-03.12 | Khi Mod hoặc Admin mở nội dung của một nhóm Private từ vụ báo cáo mình đang giữ (M08), hệ thống phải hiển thị nội dung đó (BR-M11-33). |
| FR-M11-03.13 | Hệ thống phải cho người ngoài nhóm đã đăng nhập bình luận, vote, báo cáo và bookmark bài của nhóm Public như bài không thuộc nhóm (BR-M11-13). |
| FR-M11-03.14 | Khi người xem được trang nhóm mở danh sách thành viên, hệ thống phải hiển thị các thành viên kèm vai trò nhóm (BR-M11-34). |
| FR-M11-03.15 | Nếu người xem không xem được trang nhóm, hệ thống phải không hiển thị danh sách thành viên của nhóm (BR-M11-34). |
| FR-M11-03.16 | Khi người xem mở trang danh sách nhóm, hệ thống phải hiển thị các nhóm Private mà người đó là thành viên và các nhóm Public, mỗi nhóm kèm tên, mô tả, chế độ (BR-M11-35). |
| FR-M11-03.17 | Hệ thống phải xếp các nhóm trên trang danh sách nhóm theo thời điểm tạo, nhóm mới nhất trước (BR-M11-35). |
| FR-M11-03.18 | Khi người ngoài nhóm mở lời mời hoặc link mời của một nhóm Private, hệ thống phải hiển thị tên, mô tả nhóm để người đó tham gia theo luồng tham gia (BR-M11-12). |

### 5.4 FR-M11-04 Tham gia nhóm

**Yêu cầu cấp trên:** Hệ thống phải cho phép người ngoài nhóm vào nhóm ngay hoặc gửi yêu cầu tham gia, theo chế độ và câu hỏi tham gia của nhóm.

**Lý do:** Nhóm Private và nhóm có câu hỏi tham gia cần Owner hoặc Group Mod xem người xin vào; bị từ chối được gửi lại ngay như cách các nền tảng nhóm phổ biến làm, người gửi liên tục thì nhóm tự chặn.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M11-04.01 | Khi người ngoài nhóm chọn tham gia một nhóm Public không có câu hỏi tham gia, hệ thống phải thêm người đó làm Member ngay, với thời điểm tham gia là lúc chọn (BR-M11-07). |
| FR-M11-04.02 | Khi người ngoài nhóm chọn tham gia một nhóm có câu hỏi tham gia, hệ thống phải hiển thị câu hỏi để người đó trả lời trước khi gửi yêu cầu (BR-M11-08). |
| FR-M11-04.03 | Khi người ngoài nhóm gửi yêu cầu tham gia một nhóm Public có câu hỏi hoặc một nhóm Private, hệ thống phải tạo yêu cầu tham gia ở trạng thái Chờ duyệt, kèm câu trả lời khi nhóm có câu hỏi (BR-M11-07). |
| FR-M11-04.04 | Khi yêu cầu tham gia của một người bị từ chối, hệ thống phải cho người đó gửi yêu cầu mới ngay, không giới hạn số lần (BR-M11-09). |
| FR-M11-04.05 | Nếu Guest chọn tham gia nhóm, hệ thống phải từ chối và yêu cầu đăng nhập (BR-M11-07). |
| FR-M11-04.06 | Nếu người dùng đang bị nhóm chặn vào nhóm đó bằng bất kỳ cách nào (vào ngay, gửi yêu cầu, qua lời mời), hệ thống phải từ chối (BR-M11-10). |
| FR-M11-04.07 | Hệ thống phải không giới hạn số nhóm một người dùng tham gia (BR-M11-03). |
| FR-M11-04.08 | Nếu nhóm có câu hỏi tham gia mà người gửi để trống câu trả lời, hệ thống phải từ chối gửi yêu cầu (BR-M11-08). |
| FR-M11-04.09 | Nếu người dùng đang có một yêu cầu Chờ duyệt gửi thêm yêu cầu tới chính nhóm đó, hệ thống phải từ chối (BR-M11-09). |
| FR-M11-04.10 | Khi người gửi rút một yêu cầu đang Chờ duyệt của mình, hệ thống phải chuyển yêu cầu sang Đã rút (BR-M11-36). |

### 5.5 FR-M11-05 Mời người khác vào nhóm

**Yêu cầu cấp trên:** Hệ thống phải cho phép mọi thành viên của nhóm mời người khác vào nhóm bằng lời mời hoặc link mời.

**Lý do:** Nhóm Private không hiện trong tìm kiếm, chỉ tới được qua lời mời hoặc link mời; quyền mời không giới hạn cho Owner, Group Mod.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M11-05.01 | Khi một thành viên (Member, Group Mod hoặc Owner) chọn mời người khác hoặc lấy link mời, hệ thống phải cung cấp lời mời hoặc link mời tới nhóm (BR-M11-12). |
| FR-M11-05.02 | Khi thành viên mời một người dùng cụ thể, hệ thống phải gửi cho người đó thông báo mời trong ứng dụng kèm link mời của nhóm (M07) (BR-M11-12). |
| FR-M11-05.03 | Nếu người không là thành viên nhóm, kể cả Guest, chọn mời hoặc lấy link mời, hệ thống phải từ chối (BR-M11-12). |
| FR-M11-05.04 | Hệ thống phải không tạo lời mời riêng để người được mời chấp nhận hoặc từ chối (BR-M11-12). |
| FR-M11-05.05 | Khi người được mời mở lời mời hoặc link mời, hệ thống phải xử lý việc tham gia theo BR-M11-07: nhóm Public không có câu hỏi thì vào ngay, còn lại thì gửi yêu cầu Chờ duyệt (BR-M11-12). |
| FR-M11-05.06 | Hệ thống phải dùng một link mời chung, không hết hạn, cho mỗi nhóm (BR-M11-12). |
| FR-M11-05.07 | Hệ thống phải không cho thu hồi hay tạo lại link mời của nhóm (BR-M11-12). |

### 5.6 FR-M11-06 Duyệt yêu cầu tham gia

**Yêu cầu cấp trên:** Hệ thống phải cho phép Owner và Group Mod xem các yêu cầu tham gia Chờ duyệt kèm câu trả lời, rồi chấp nhận hoặc từ chối từng yêu cầu.

**Lý do:** Nhóm Private và nhóm có câu hỏi tham gia cần Owner hoặc Group Mod quyết định cho vào dựa trên câu trả lời.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M11-06.01 | Khi Owner hoặc Group Mod mở danh sách yêu cầu tham gia, hệ thống phải hiển thị các yêu cầu Chờ duyệt của nhóm, kèm câu trả lời khi nhóm có câu hỏi (BR-M11-08). |
| FR-M11-06.02 | Khi Owner hoặc Group Mod chấp nhận một yêu cầu, hệ thống phải chuyển yêu cầu sang Đã chấp nhận và thêm người gửi làm Member, với thời điểm tham gia là lúc chấp nhận (BR-M11-07). |
| FR-M11-06.03 | Khi Owner hoặc Group Mod từ chối một yêu cầu, hệ thống phải chuyển yêu cầu sang Đã từ chối (BR-M11-09). |
| FR-M11-06.04 | Khi một yêu cầu được chấp nhận, hệ thống phải gửi thông báo trong ứng dụng cho người gửi (M07). |
| FR-M11-06.05 | Nếu Member hoặc người không là thành viên chấp nhận, từ chối yêu cầu tham gia, hệ thống phải từ chối thao tác (BR-M11-06). |
| FR-M11-06.06 | Nếu yêu cầu không còn ở trạng thái Chờ duyệt, hệ thống phải từ chối chấp nhận hoặc từ chối yêu cầu đó. |
| FR-M11-06.07 | Khi có yêu cầu tham gia mới, hệ thống phải gửi thông báo trong ứng dụng cho Owner và các Group Mod của nhóm (M07) (BR-M11-37). |
| FR-M11-06.08 | Khi người ngoài nhóm vào ngay một nhóm Public, hệ thống phải không gửi thông báo (BR-M11-37). |
| FR-M11-06.09 | Khi một yêu cầu tham gia bị từ chối, hệ thống phải không gửi thông báo cho người gửi (BR-M11-37). |

### 5.7 FR-M11-07 Chặn người gửi yêu cầu tham gia

**Yêu cầu cấp trên:** Hệ thống phải cho phép Owner và Group Mod chặn một người dùng gửi yêu cầu tham gia nhóm.

**Lý do:** Nhóm xử lý người gửi yêu cầu liên tục bằng cách chặn từng người, thay cho thời gian chờ của hệ thống.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M11-07.01 | Khi Owner hoặc Group Mod chặn một người gửi yêu cầu, hệ thống phải ghi người đó vào danh sách chặn của nhóm (BR-M11-10). |
| FR-M11-07.02 | Nếu Member hoặc người không là thành viên chặn, xem danh sách chặn hoặc bỏ chặn, hệ thống phải từ chối (BR-M11-06). |
| FR-M11-07.03 | Khi Owner hoặc Group Mod chặn một người đang có yêu cầu Chờ duyệt, hệ thống phải chuyển yêu cầu đó sang Đã từ chối (BR-M11-10). |
| FR-M11-07.04 | Khi Owner hoặc Group Mod mở danh sách chặn, hệ thống phải hiển thị những người đang bị nhóm chặn (BR-M11-10). |
| FR-M11-07.05 | Khi Owner hoặc Group Mod bỏ chặn một người, hệ thống phải cho người đó vào nhóm lại theo luồng tham gia (BR-M11-10). |

### 5.8 FR-M11-08 Bổ nhiệm, giáng Group Mod

**Yêu cầu cấp trên:** Hệ thống phải cho phép Owner bổ nhiệm một Member làm Group Mod và giáng một Group Mod về Member.

**Lý do:** Group Mod giúp giữ chất lượng nội dung của nhóm; chỉ Owner bổ nhiệm, giáng theo thứ bậc chặt của nhóm.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M11-08.01 | Khi Owner bổ nhiệm một Member, hệ thống phải chuyển vai trò người đó sang Group Mod và ghi thời điểm bổ nhiệm (BR-M11-05, BR-M11-26). |
| FR-M11-08.02 | Khi Owner giáng một Group Mod, hệ thống phải chuyển vai trò người đó về Member (BR-M11-05). |
| FR-M11-08.03 | Khi một thành viên được bổ nhiệm làm Group Mod, hệ thống phải gửi thông báo trong ứng dụng cho người đó (M07). |
| FR-M11-08.04 | Nếu Group Mod, Member hoặc người không là thành viên bổ nhiệm hoặc giáng Group Mod, hệ thống phải từ chối (BR-M11-06). |
| FR-M11-08.05 | Khi Owner bổ nhiệm, giáng, kick hoặc chọn người kế nhiệm, hệ thống phải hiển thị cho Owner các thành viên của nhóm kèm vai trò. |
| FR-M11-08.06 | Khi Owner giáng một Group Mod, hệ thống phải không gửi thông báo cho người bị giáng (BR-M11-37). |

### 5.9 FR-M11-09 Kick thành viên khỏi nhóm

**Yêu cầu cấp trên:** Hệ thống phải cho phép Owner kick Member và Group Mod, Group Mod kick Member ra khỏi nhóm.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M11-09.01 | Khi Owner kick một Member hoặc Group Mod, hệ thống phải đưa người đó ra khỏi nhóm (BR-M11-05). |
| FR-M11-09.02 | Khi Group Mod kick một Member, hệ thống phải đưa người đó ra khỏi nhóm (BR-M11-05). |
| FR-M11-09.03 | Nếu Group Mod kick một Group Mod khác hoặc Owner, hệ thống phải từ chối (BR-M11-05). |
| FR-M11-09.04 | Nếu Member hoặc người không là thành viên kick một thành viên, hệ thống phải từ chối (BR-M11-06). |
| FR-M11-09.05 | Khi một thành viên bị kick, hệ thống phải giữ nguyên bài, bình luận của người đó trong nhóm, tác giả hiện như trước và không đổi điểm (BR-M11-24). |
| FR-M11-09.06 | Khi một thành viên bị kick, hệ thống phải gửi thông báo trong ứng dụng cho người đó (M07). |
| FR-M11-09.07 | Hệ thống phải cho người đã bị kick tham gia lại nhóm theo luồng tham gia như người đã tự rời (BR-M11-24). |

### 5.10 FR-M11-10 Rời nhóm

**Yêu cầu cấp trên:** Hệ thống phải cho phép thành viên rời nhóm; Owner chỉ rời được sau khi chỉ định người kế nhiệm.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M11-10.01 | Khi Member hoặc Group Mod chọn rời nhóm, hệ thống phải đưa người đó ra khỏi nhóm (BR-M11-24). |
| FR-M11-10.02 | Khi một thành viên rời nhóm, hệ thống phải giữ nguyên bài, bình luận của người đó trong nhóm, tác giả hiện như trước và không đổi điểm (BR-M11-24). |
| FR-M11-10.03 | Khi Owner chọn rời một nhóm còn thành viên khác, hệ thống phải yêu cầu Owner chọn một thành viên khác làm Owner trước (BR-M11-25). |
| FR-M11-10.04 | Khi Owner đã chọn người kế nhiệm và xác nhận rời, hệ thống phải chuyển vai trò Owner cho người được chọn rồi đưa Owner cũ ra khỏi nhóm (BR-M11-25). |
| FR-M11-10.05 | Nếu Owner rời nhóm còn thành viên khác mà chưa chỉ định người kế nhiệm, hệ thống phải từ chối (BR-M11-25). |
| FR-M11-10.06 | Khi Owner là thành viên duy nhất chọn rời, hệ thống phải cảnh báo nhóm sẽ bị xóa và chỉ xóa nhóm (FR-M11-15) khi Owner xác nhận (BR-M11-25). |
| FR-M11-10.07 | Khi một thành viên trở thành Owner do Owner cũ chỉ định, hệ thống phải gửi thông báo trong ứng dụng cho người đó (M07) (BR-M11-37). |
| FR-M11-10.08 | Khi người đã rời hoặc bị kick khỏi một nhóm Public sửa hoặc xóa bài, bình luận của chính mình trong nhóm, hệ thống phải cho làm như với bài, bình luận không thuộc nhóm (M03, M04) (BR-M11-24). |
| FR-M11-10.09 | Nếu người đã rời hoặc bị kick khỏi một nhóm Private sửa hoặc xóa bài, bình luận của mình trong nhóm, hệ thống phải từ chối (BR-M11-24). |

### 5.11 FR-M11-11 Tự chuyển quyền Owner khi Owner mất quyền

**Yêu cầu cấp trên:** Hệ thống phải tự chuyển vai trò Owner cho một thành viên khác khi Owner mất quyền ngoài ý muốn.

**Lý do:** Owner bị ban, bị vô hiệu hóa hoặc bị xóa tài khoản không có cơ hội chỉ định người kế nhiệm.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M11-11.01 | Khi tài khoản Owner bị ban (tạm thời hoặc vĩnh viễn), bị vô hiệu hóa (kể cả tự vô hiệu hóa) hoặc bị xóa, hệ thống phải chuyển ngay vai trò Owner cho Group Mod có thâm niên Group Mod dài nhất (BR-M11-26). |
| FR-M11-11.02 | Nếu nhóm không còn Group Mod, hệ thống phải chuyển vai trò Owner cho Member có thời điểm tham gia sớm nhất (BR-M11-26). |
| FR-M11-11.03 | Nếu Owner là thành viên duy nhất của nhóm, hệ thống phải xóa mềm nhóm (BR-M11-26, BR-M11-23). |
| FR-M11-11.04 | Trong khi cờ Group tắt, hệ thống phải vẫn tự chuyển vai trò Owner (BR-M11-29). |
| FR-M11-11.05 | Khi tự chuyển vai trò Owner, hệ thống phải giữ Owner cũ trong nhóm với vai trò Member, kể cả khi tài khoản đó hoạt động trở lại (BR-M11-26). |
| FR-M11-11.06 | Hệ thống phải tính thâm niên Group Mod từ lần bổ nhiệm gần nhất (BR-M11-26). |
| FR-M11-11.07 | Khi một thành viên trở thành Owner do hệ thống tự chuyển, hệ thống phải gửi thông báo trong ứng dụng cho người đó (M07) (BR-M11-37). |

### 5.12 FR-M11-12 Đăng bài trong nhóm

**Yêu cầu cấp trên:** Hệ thống phải cho phép thành viên đăng bài trong nhóm qua cổng duyệt của nhóm, kèm lựa chọn đăng ẩn danh khi nhóm bật.

**Lý do:** AI lọc vi phạm nghiêm trọng, Group Mod giữ chất lượng nội dung của nhóm; cổng của nhóm là bước thêm, không thay kiểm duyệt hệ thống. Đăng ẩn danh gắn với ngữ cảnh nhóm nên do nhóm bật, tắt.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M11-12.01 | Khi thành viên khác Owner gửi bài trong nhóm, hệ thống phải gắn bài với nhóm đó và đưa bài qua cổng duyệt của nhóm thay cho luồng duyệt của bài không thuộc nhóm (BR-M11-01, BR-M11-18). |
| FR-M11-12.02 | Khi bài nhóm có điểm quét ≥ 0.9, hệ thống phải chuyển bài sang Bị từ chối (BR-M11-18). |
| FR-M11-12.03 | Khi bài nhóm của thành viên khác Owner có điểm quét từ 0.5 tới dưới 0.9, hệ thống phải đưa bài vào hàng chờ duyệt của nhóm, kể cả khi công tắc duyệt trước tắt (BR-M11-18). |
| FR-M11-12.04 | Khi bài nhóm của thành viên khác Owner có điểm quét < 0.5 và công tắc duyệt trước bật, hệ thống phải đưa bài vào hàng chờ duyệt của nhóm (BR-M11-18). |
| FR-M11-12.05 | Khi bài nhóm của thành viên khác Owner có điểm quét < 0.5 và công tắc duyệt trước tắt, hệ thống phải chuyển bài sang Đã đăng (BR-M11-18). |
| FR-M11-12.06 | Khi tác giả là Admin và không là Owner của nhóm, hệ thống phải không quét bài và đưa bài theo công tắc duyệt trước của nhóm: bật thì vào hàng chờ duyệt của nhóm, tắt thì Đã đăng (BR-M11-19). |
| FR-M11-12.07 | Ở nơi công tắc ẩn danh của nhóm bật, hệ thống phải cho tác giả chọn đăng ẩn danh hay không cho từng bài (BR-M11-16). |
| FR-M11-12.08 | Nếu công tắc ẩn danh của nhóm tắt, hệ thống phải không cho chọn đăng ẩn danh (BR-M11-16). |
| FR-M11-12.09 | Nếu bài không thuộc nhóm, hệ thống phải không cho chọn đăng ẩn danh (BR-M11-16). |
| FR-M11-12.10 | Khi bài ẩn danh được lưu, hệ thống phải giữ danh tính thật của tác giả (BR-M11-17). |
| FR-M11-12.11 | Nếu người không là thành viên gửi bài vào nhóm, hệ thống phải từ chối (BR-M11-06). |
| FR-M11-12.12 | Khi bài của nhóm Public được đăng, hệ thống phải cho bài hiện với người ngoài nhóm như bài thường ở feed chính (M14) (BR-M11-14). |
| FR-M11-12.13 | Nếu bài thuộc nhóm Private, hệ thống phải không đưa bài ra feed chính, kể cả với thành viên nhóm (BR-M11-14). |
| FR-M11-12.14 | Trong khi công tắc AI tổng hoặc công tắc Moderation tắt, hệ thống phải đưa bài của thành viên khác Owner gửi vào nhóm theo công tắc duyệt trước: bật thì vào hàng chờ duyệt của nhóm, tắt thì Đã đăng (BR-M11-18). |
| FR-M11-12.15 | Nếu quét bài nhóm của thành viên khác Owner thất bại sau một lần thử lại, hệ thống phải đưa bài vào hàng chờ duyệt của nhóm, dù công tắc duyệt trước tắt (BR-M11-18). |
| FR-M11-12.16 | Khi Owner gửi bài trong nhóm của mình, hệ thống phải gắn bài với nhóm và không đưa bài vào hàng chờ duyệt của nhóm, bất kể công tắc duyệt trước (BR-M11-40). |
| FR-M11-12.17 | Khi bài của Owner có điểm quét ≥ 0.9, hệ thống phải chuyển bài sang Bị từ chối (BR-M11-40). |
| FR-M11-12.18 | Khi bài của Owner có điểm quét từ 0.5 tới dưới 0.9, hoặc quét thất bại sau một lần thử lại, hệ thống phải đưa bài vào hàng chờ duyệt của Mod hệ thống như bài không thuộc nhóm (M03) (BR-M11-40). |
| FR-M11-12.19 | Khi bài của Owner có điểm quét < 0.5, hoặc công tắc AI tổng hay Moderation tắt, hệ thống phải chuyển bài sang Đã đăng (BR-M11-40). |
| FR-M11-12.20 | Khi Owner là Admin, hệ thống phải không quét bài của Owner trong nhóm và chuyển bài sang Đã đăng (BR-M11-40). |

### 5.13 FR-M11-13 Duyệt bài chờ đăng của nhóm

**Yêu cầu cấp trên:** Hệ thống phải cho phép Owner và Group Mod nhận bài trong hàng chờ duyệt của nhóm rồi chấp nhận hoặc từ chối bài.

**Lý do:** Group Mod tập trung giữ chất lượng nội dung của nhóm; hàng chờ của nhóm tách khỏi hàng chờ báo cáo và dùng cùng cơ chế nhận việc 30 phút.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M11-13.01 | Khi Owner hoặc Group Mod mở hàng chờ duyệt của nhóm, hệ thống phải hiển thị các bài đang chờ nhóm duyệt của riêng nhóm đó, tách khỏi hàng chờ báo cáo (BR-M11-20). |
| FR-M11-13.02 | Khi Owner hoặc Group Mod nhận một bài, hệ thống phải ghi người đó là người đang giữ bài (BR-M11-20). |
| FR-M11-13.03 | Nếu một người khác người đang giữ bài chấp nhận hoặc từ chối bài, hệ thống phải từ chối thao tác (BR-M11-20). |
| FR-M11-13.04 | Nếu người đang giữ không thao tác trên bài trong 30 phút tính từ thời điểm thao tác cuối, hệ thống phải nhả bài về hàng chờ duyệt của nhóm (BR-M11-20). |
| FR-M11-13.05 | Khi người đang giữ chấp nhận bài, hệ thống phải chuyển bài sang Đã đăng (BR-M11-18). |
| FR-M11-13.06 | Khi người đang giữ từ chối bài kèm lý do, hệ thống phải chuyển bài sang Bị từ chối kèm lý do đó (BR-M11-38). |
| FR-M11-13.07 | Nếu tác giả khiếu nại việc nhóm từ chối bài, hệ thống phải từ chối khiếu nại (BR-M11-21). |
| FR-M11-13.08 | Nếu Member hoặc người không là thành viên mở hàng chờ duyệt, nhận, chấp nhận hoặc từ chối bài của nhóm, hệ thống phải từ chối (BR-M11-06). |
| FR-M11-13.09 | Nếu Mod hoặc Admin không là thành viên nhóm mở hàng chờ duyệt, nhận, chấp nhận hoặc từ chối bài của nhóm, hệ thống phải từ chối (BR-M11-33). |
| FR-M11-13.10 | Nếu người đang giữ từ chối bài mà không nhập lý do, hệ thống phải từ chối thao tác (BR-M11-38). |
| FR-M11-13.11 | Khi tác giả sửa và gửi lại bài bị nhóm từ chối, hệ thống phải đưa bài vào cổng duyệt của nhóm thêm một lần (BR-M11-38). |
| FR-M11-13.12 | Nếu tác giả khiếu nại một bài nhóm bị AI tự từ chối, hệ thống phải nhận khiếu nại qua M09 như với bài không thuộc nhóm (BR-M11-38). |
| FR-M11-13.13 | Nếu Group Mod nhận, chấp nhận hoặc từ chối bài chờ duyệt của chính mình, hệ thống phải từ chối (BR-M11-39). |
| FR-M11-13.14 | Khi khiếu nại về một bài nhóm bị AI tự từ chối được chấp nhận (M09), hệ thống phải đưa bài qua cổng duyệt của nhóm như bài có điểm quét dưới 0.5 mà không quét lại: công tắc duyệt trước bật thì bài chờ nhóm duyệt, tắt hoặc bài của Owner thì bài sang Đã đăng (BR-M11-38). |

### 5.14 FR-M11-14 Gỡ bài và bình luận khỏi nhóm

**Yêu cầu cấp trên:** Hệ thống phải cho phép Owner và Group Mod gỡ bài và bình luận khỏi nhóm bằng xóa mềm; quyết định này không khiếu nại được.

**Lý do:** Group Mod giữ chất lượng nội dung của nhóm; như việc gỡ bài của người kiểm duyệt cộng đồng con trên các nền tảng tham khảo, quyết định cấp nhóm không có khiếu nại lên hệ thống.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M11-14.01 | Khi Owner hoặc Group Mod gỡ một bài hoặc bình luận khỏi nhóm, hệ thống phải xóa mềm và chỉ hiển thị nội dung đó cho tác giả, Owner, Group Mod của nhóm, Mod và Admin (BR-M11-30). |
| FR-M11-14.02 | Nếu Member hoặc người không là thành viên gỡ bài hoặc bình luận của người khác khỏi nhóm bằng quyền của nhóm, hệ thống phải từ chối (BR-M11-06). |
| FR-M11-14.03 | Nếu tác giả khiếu nại việc Owner, Group Mod gỡ bài hoặc bình luận khỏi nhóm, hệ thống phải từ chối khiếu nại (BR-M11-21). |
| FR-M11-14.04 | Hệ thống phải giữ việc báo cáo và quyền can thiệp của Mod, Admin hệ thống với bài, bình luận trong nhóm (BR-M11-22). |
| FR-M11-14.05 | Nếu tác giả hiện lại bài, bình luận đã bị gỡ khỏi nhóm, hệ thống phải từ chối (BR-M11-30). |
| FR-M11-14.06 | Khi một bài hoặc bình luận bị gỡ khỏi nhóm, hệ thống phải gửi thông báo trong ứng dụng cho tác giả (M07) (BR-M11-30). |
| FR-M11-14.07 | Khi một bài hoặc bình luận bị gỡ khỏi nhóm, hệ thống phải không trừ điểm của tác giả (M12) (BR-M11-30). |
| FR-M11-14.08 | Nếu Group Mod gỡ bài hoặc bình luận của Owner hoặc của một Group Mod khác, hệ thống phải từ chối (BR-M11-05). |

### 5.15 FR-M11-15 Xóa nhóm

**Yêu cầu cấp trên:** Hệ thống phải cho phép Owner xóa nhóm bằng xóa mềm.

**Lý do:** Xóa mềm giữ lại dữ liệu; với thành viên, nhóm bị xóa là việc gián tiếp, họ không chọn và không vi phạm gì nên điểm được giữ nguyên.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M11-15.01 | Khi Owner xóa nhóm, hệ thống phải chuyển nhóm sang Đã xóa và không hiển thị nhóm cùng mọi nội dung với bất kỳ ai, kể cả thành viên cũ (BR-M11-23). |
| FR-M11-15.02 | Khi nhóm bị xóa, hệ thống phải giữ dữ liệu của nhóm và nội dung của nhóm (BR-M11-23). |
| FR-M11-15.03 | Khi nhóm bị xóa, hệ thống phải không trừ điểm của các thành viên vì nội dung mất theo nhóm (BR-M11-23). |
| FR-M11-15.04 | Nếu Group Mod, Member hoặc người không là thành viên xóa nhóm, hệ thống phải từ chối (BR-M11-06). |
| FR-M11-15.05 | Nếu người dùng mở, tham gia hoặc đăng bài vào một nhóm Đã xóa, hệ thống phải từ chối (BR-M11-23). |

### 5.16 FR-M11-16 Áp dụng trạng thái Ẩn, Khóa của nhóm

**Yêu cầu cấp trên:** Hệ thống phải áp trạng thái kiểm duyệt Bị ẩn, Bị khóa do Mod, Admin quyết (M08) lên cách nhóm hiển thị và các thao tác được phép trong nhóm.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M11-16.01 | Trong khi nhóm Bị ẩn, hệ thống phải không hiển thị nhóm và mọi nội dung của nhóm với bất kỳ ai, kể cả thành viên và Owner (BR-M11-27). |
| FR-M11-16.02 | Trong khi nhóm Bị ẩn, hệ thống phải giữ dữ liệu của nhóm (BR-M11-27). |
| FR-M11-16.03 | Trong khi nhóm Bị khóa, hệ thống phải hiển thị nhóm theo chế độ Public, Private như trước và cho đọc nội dung đã có (BR-M11-28). |
| FR-M11-16.04 | Trong khi nhóm Bị khóa, hệ thống phải từ chối đăng bài, bình luận, vote, bình chọn poll, tham gia và mời trong nhóm với mọi người, kể cả Owner và Group Mod (BR-M11-28). |
| FR-M11-16.05 | Trong khi nhóm Bị khóa, hệ thống phải cho bookmark và báo cáo nội dung của nhóm (BR-M11-28). |
| FR-M11-16.06 | Khi Mod, Admin mở khóa nhóm, hệ thống phải cho lại các thao tác đã bị chặn lúc nhóm Bị khóa (BR-M11-28). |
| FR-M11-16.07 | Trong khi nhóm Bị khóa, hệ thống phải từ chối với mọi người, kể cả Owner và Group Mod, các thao tác: duyệt yêu cầu tham gia, duyệt bài chờ, gỡ nội dung, kick, chặn, bỏ chặn, bổ nhiệm, giáng Group Mod, đổi thông tin và cài đặt, xóa nhóm (BR-M11-28). |
| FR-M11-16.08 | Nếu Owner rời nhóm trong khi nhóm Bị khóa, hệ thống phải từ chối (BR-M11-28). |
| FR-M11-16.09 | Trong khi nhóm Bị khóa, hệ thống phải cho Member và Group Mod tự rời nhóm (BR-M11-28). |
| FR-M11-16.10 | Trong khi nhóm Bị khóa, hệ thống phải vẫn tự chuyển vai trò Owner khi Owner mất quyền ngoài ý muốn (BR-M11-28). |

### 5.17 FR-M11-17 Chặn thao tác nhóm khi cờ Group tắt

**Yêu cầu cấp trên:** Hệ thống phải chặn thao tác của người dùng khác Admin với module Group trong khi cờ tính năng Group tắt, đồng thời giữ nguyên dữ liệu và việc hệ thống tự làm.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M11-17.01 | Trong khi cờ Group tắt, nếu người dùng khác Admin gửi một thao tác tới module Group, hệ thống phải từ chối với thông báo "Hệ thống đang bận, vui lòng thử lại sau" (BR-M11-29). |
| FR-M11-17.02 | Trong khi cờ Group tắt, hệ thống phải vẫn hiển thị lối vào module Group (BR-M11-29). |
| FR-M11-17.03 | Trong khi cờ Group tắt, hệ thống phải cho Admin dùng module Group như khi cờ bật (BR-M11-29). |
| FR-M11-17.04 | Trong khi cờ Group tắt, hệ thống phải không xóa hay đổi dữ liệu của nhóm (BR-M11-29). |
| FR-M11-17.05 | Trong khi cờ Group tắt, hệ thống phải vẫn cho kiểm duyệt M08 chạy với nhóm và nội dung nhóm (BR-M11-29). |
| FR-M11-17.06 | Khi cờ Group được bật lại, hệ thống phải không làm bù các thao tác đã bị từ chối trong lúc cờ tắt (BR-M11-29). |
| FR-M11-17.07 | Trong khi cờ Group tắt, hệ thống phải vẫn hiển thị nhóm và bài nhóm ở các lối vào: danh sách nhóm, Trending, tab Group và tab Following của feed, tab Bài viết trên hồ sơ, tìm kiếm, bookmark, thông báo (BR-M11-29). |
| FR-M11-17.08 | Trong khi cờ Group tắt, nếu người dùng khác Admin mở một nhóm, mở một bài nhóm hoặc tương tác với bài nhóm, hệ thống phải từ chối với thông báo "Hệ thống đang bận, vui lòng thử lại sau" (BR-M11-29). |

### 5.18 Quy tắc nghiệp vụ

| ID | Loại | Quy tắc | Ví dụ |
|---|---|---|---|
| BR-M11-01 | Sự kiện | Nhóm tái dùng cơ chế bài viết, bình luận, star, báo cáo, kiểm duyệt, AI, thông báo của Forum. Bài nhóm là bài viết chung có gắn nhóm, không phải loại bài riêng; một bài thuộc tối đa một nhóm. | — |
| BR-M11-02 | Sự kiện | Không có leaderboard hay reputation riêng theo nhóm. | — |
| BR-M11-03 | Ràng buộc | Mọi người dùng đã đăng nhập tạo được nhóm, tối đa 5 nhóm trong 24 giờ gần nhất tính tới lúc tạo; nhóm đã bị xóa vẫn được tính; Admin cũng bị giới hạn. Không giới hạn số nhóm một người sở hữu hay tham gia. | A tạo 5 nhóm lúc 20:00, 20:05, 20:10, 20:15, 20:20 ngày 01/11 → tạo nhóm thứ 6 lúc 19:59 ngày 02/11 bị từ chối; lúc 20:00 ngày 02/11 được (nhóm 20:00 ngày 01/11 đã ra khỏi 24 giờ). A xóa một trong 5 nhóm lúc 21:00 ngày 01/11 → vẫn tính đủ 5. A đang là Owner 40 nhóm, thành viên 100 nhóm → vẫn tạo, vẫn tham gia thêm được. |
| BR-M11-04 | Sự kiện | Người tạo nhóm là Owner đầu tiên của nhóm. Mỗi nhóm luôn có đúng một Owner. | A tạo nhóm "Ôn thi HSG Toán 12" → A là Owner, nhóm có 1 thành viên. |
| BR-M11-05 | Ràng buộc | Vai trò nhóm theo thứ bậc Member < Group Mod < Owner; không vai trò nào tác động lên người ngang hoặc cao hơn mình, kể cả với nội dung: Group Mod không gỡ bài, bình luận của Owner hay Group Mod khác. | Group Mod B kick Member C → được. Group Mod B kick Group Mod D → bị từ chối. Group Mod B kick Owner A → bị từ chối. Owner A kick Group Mod D → được. Group Mod B gỡ bài của Group Mod D → bị từ chối; Owner A gỡ bài của D → được. |
| BR-M11-06 | Ràng buộc | Chỉ Owner được: đổi cài đặt nhóm (Public/Private, công tắc duyệt trước, công tắc ẩn danh, câu hỏi tham gia), bổ nhiệm và giáng Group Mod, kick Group Mod, xóa nhóm. Owner và Group Mod được: duyệt bài chờ đăng, gỡ bài và bình luận khỏi nhóm, duyệt yêu cầu tham gia, chặn người gửi yêu cầu, kick Member. Mọi thành viên được: đăng bài, bình luận, vote, mời người khác. | Group Mod B bật công tắc ẩn danh → bị từ chối. Member C duyệt yêu cầu tham gia → bị từ chối. |
| BR-M11-07 | Suy diễn | Người ngoài nhóm chọn tham gia: nhóm Public không có câu hỏi tham gia → thành viên ngay; nhóm Public có câu hỏi → gửi yêu cầu kèm câu trả lời, chờ duyệt; nhóm Private không có câu hỏi → gửi yêu cầu, chờ duyệt; nhóm Private có câu hỏi → gửi yêu cầu kèm câu trả lời, chờ duyệt. Người duyệt là Owner hoặc Group Mod. | Public, không câu hỏi: C bấm "Tham gia" lúc 09:00 → thành viên lúc 09:00. Public có câu hỏi "Bạn học lớp mấy?": C trả lời "11" → yêu cầu Chờ duyệt. Private không câu hỏi: C → yêu cầu Chờ duyệt. Private có câu hỏi: C trả lời → yêu cầu Chờ duyệt, Owner thấy câu trả lời. |
| BR-M11-08 | Ràng buộc | Mỗi nhóm có tối đa một câu hỏi tham gia, không bắt buộc, do Owner đặt hoặc bỏ; câu hỏi áp cho cả nhóm Public và Private. Nhóm có câu hỏi thì người gửi yêu cầu bắt buộc trả lời. Owner, Group Mod xem câu trả lời khi duyệt yêu cầu. | Owner đặt câu hỏi thứ hai → không có chỗ đặt, chỉ sửa được câu hỏi duy nhất. Nhóm có câu hỏi, C để trống câu trả lời → không gửi được yêu cầu. |
| BR-M11-09 | Kích hoạt | Yêu cầu tham gia bị từ chối thì người đó gửi lại yêu cầu mới ngay được, không có thời gian chờ, không giới hạn số lần. Người đang có một yêu cầu Chờ duyệt không gửi thêm yêu cầu tới cùng nhóm. | Yêu cầu của C bị từ chối lúc 10:00 → C gửi lại lúc 10:01 được; bị từ chối lần 2 lúc 10:30 → gửi lại lần 3 lúc 10:31 được. C đang có yêu cầu chờ từ 11:00, gửi thêm lúc 11:05 → bị từ chối. |
| BR-M11-10 | Ràng buộc | Owner hoặc Group Mod chặn một người dùng thì người đó không vào được nhóm bằng bất kỳ cách nào (vào ngay, gửi yêu cầu, qua lời mời); yêu cầu đang Chờ duyệt của người đó chuyển sang Đã từ chối. Owner, Group Mod xem được danh sách chặn và bỏ chặn; bỏ chặn thì người đó vào lại theo luồng tham gia. Hệ thống không có thời gian chờ. | C có yêu cầu chờ; nhóm chặn C lúc 11:00 → yêu cầu thành Đã từ chối; C mở link mời lúc 11:05 → bị từ chối. Bỏ chặn lúc 12:00 → C gửi yêu cầu lúc 12:01 được. C vẫn vào nhóm khác bình thường. |
| BR-M11-11 | Sự kiện | Nhóm Private không hiện với người ngoài nhóm, kể cả Guest, ở danh sách nhóm, tìm kiếm, gợi ý khi gõ, khám phá; người ngoài tới nhóm Private chỉ qua lời mời hoặc link mời. Thành viên vẫn thấy và tìm thấy nhóm Private của mình. | Nhóm Private "CLB Hóa": D không là thành viên tìm "Hóa" → không thấy nhóm. E là thành viên tìm "Hóa" → thấy nhóm. |
| BR-M11-12 | Ràng buộc | Mọi thành viên (Member, Group Mod, Owner) mời được người khác. Mỗi nhóm có một link mời chung, không hết hạn, không thu hồi hay tạo lại được; mời một người cụ thể là gửi cho người đó thông báo kèm link này. Không có lời mời riêng để chấp nhận hay từ chối; người được mời vào nhóm theo luồng tham gia (BR-M11-07). | Member Bình gửi link mời nhóm Private N (có câu hỏi) cho Chi → Chi thấy tên, mô tả N, trả lời câu hỏi, yêu cầu Chờ duyệt; Owner An chấp nhận → Chi là Member. Link mời nhóm Public không câu hỏi → Chi vào ngay. |
| BR-M11-13 | Suy diễn | Nhóm Public: mọi người kể cả Guest xem được thông tin và nội dung nhóm; người ngoài nhóm đã đăng nhập bình luận, vote, báo cáo, bookmark bài như bài không thuộc nhóm. Nhóm Private: chỉ thành viên xem được thông tin và nội dung (bài, bình luận) của nhóm. | Bài P thuộc nhóm Public: người ngoài D upvote, bình luận P → được; Guest đọc P → được, upvote → bị từ chối. Bài Q thuộc nhóm Private: thành viên E mở Q → thấy; người ngoài D, Guest mở link Q → không thấy. |
| BR-M11-14 | Suy diễn | Bài nhóm luôn hiện với thành viên của nhóm (trang nhóm; tab Group, M14), dù nhóm Public hay Private. Bài nhóm Public còn hiện với người ngoài nhóm như bài thường ở feed chính, cụ thể là Trending và tab Following, không vào Newest (M14). Bài nhóm Private không bao giờ ra feed chính, kể cả với thành viên nhóm. | Bài P nhóm Public đã đăng: Guest thấy P ở Trending nếu P đủ điểm; P không có ở Newest; người theo dõi tác giả của P thấy P ở tab Following. Bài Q nhóm Private: không có ở Trending, Newest, tab Following với ai, kể cả thành viên; thành viên thấy Q ở trang nhóm và tab Group. |
| BR-M11-15 | Kích hoạt | Owner đổi chế độ Public↔Private bất kỳ lúc nào. Khi nhóm chuyển sang Private: người ngoài nhóm chỉ còn đọc những bài của nhóm đang hiện sẵn trên màn hình họ đã tải trước thời điểm đổi, không bình luận, vote, báo cáo được; tải lại hoặc mở lại bằng link, bookmark, thông báo thì thấy "Nội dung không tồn tại"; các lần tải feed, tìm kiếm sau đó không còn trả bài của nhóm cho người ngoài nhóm. | Nhóm chuyển Private lúc 10:00; người ngoài D đang xem P từ 09:55 → D vẫn đọc P, bấm upvote lúc 10:05 bị từ chối. D tải lại trang P lúc 10:10 → "Nội dung không tồn tại"; tải lại Trending → không còn P. |
| BR-M11-16 | Ràng buộc | Ẩn danh chỉ có trong nhóm. Khi công tắc ẩn danh của nhóm bật, thành viên tự chọn đăng ẩn danh hay không cho từng bài. Owner tắt công tắc thì chỉ chặn chọn ẩn danh cho bài mới; bài đã đăng ẩn danh vẫn ẩn danh. | Công tắc bật ngày 01/11; A đăng P1 ẩn danh, P2 không ẩn danh. Owner tắt công tắc ngày 05/11 → P1 vẫn ẩn danh; ngày 06/11 A đăng P3 → không có lựa chọn ẩn danh. |
| BR-M11-17 | Suy diễn | Hệ thống luôn giữ danh tính thật của tác giả bài ẩn danh. Người thấy danh tính thật: Owner, Group Mod của nhóm đó và Mod, Admin hệ thống; mọi người khác (Member, người ngoài nhóm, Guest) thấy "Ẩn danh". | Bài ẩn danh P của A trong nhóm N: Group Mod của N thấy "A"; Member khác của N thấy "Ẩn danh"; Mod hệ thống mở P từ một vụ báo cáo thấy "A". |
| BR-M11-18 | Kích hoạt | Bài gửi vào nhóm qua cổng duyệt của nhóm theo điểm quét: điểm ≥ 0.9 → bị tự từ chối; 0.5 ≤ điểm < 0.9 → chờ Owner hoặc Group Mod duyệt, dù công tắc duyệt trước tắt; điểm < 0.5 → công tắc duyệt trước bật thì chờ duyệt, tắt thì đăng ngay. Không có điểm quét: công tắc AI tổng hoặc Moderation tắt → theo công tắc duyệt trước; quét thất bại sau một lần thử lại → chờ nhóm duyệt dù công tắc tắt. Tắt công tắc duyệt trước không nhả các bài đang chờ. Bài không thuộc nhóm theo luồng của M03; bài của Owner theo BR-M11-40. | 0.95 → Bị từ chối. 0.90 → Bị từ chối. 0.89, công tắc tắt → chờ nhóm duyệt. 0.50, công tắc tắt → chờ nhóm duyệt. 0.49, công tắc tắt → Đã đăng. 0.49, công tắc bật → chờ nhóm duyệt. AI tắt, công tắc tắt → Đã đăng; AI tắt, công tắc bật → chờ nhóm duyệt. Quét lỗi, công tắc tắt → chờ nhóm duyệt. |
| BR-M11-19 | Sự kiện | Bài của Admin trong nhóm không bị AI quét, không qua duyệt của hệ thống, và đi theo công tắc duyệt trước của nhóm: bật thì chờ Owner, Group Mod duyệt, tắt thì đăng ngay. Admin là Owner của nhóm thì bài đăng ngay (BR-M11-40). | Admin gửi bài vào nhóm có công tắc duyệt trước bật → chờ nhóm duyệt; nhóm có công tắc tắt → Đã đăng ngay. |
| BR-M11-20 | Ràng buộc | Mỗi nhóm có một hàng chờ duyệt riêng, tách khỏi hàng chờ báo cáo (M08). Owner hoặc Group Mod nhận một bài để xử lý; trong lúc bài đang được giữ, người khác không xử lý được bài đó. Người giữ không thao tác trên bài trong 30 phút, tính từ thời điểm thao tác cuối, thì bài tự được nhả về hàng chờ. | Group Mod B nhận P lúc 10:00, mở xem lúc 10:10 → P tự nhả lúc 10:40 nếu B không thao tác thêm; Owner A mở P lúc 10:20 → không chấp nhận, từ chối được vì B đang giữ. |
| BR-M11-21 | Sự kiện | Quyết định kiểm duyệt cấp nhóm (từ chối bài chờ duyệt, gỡ bài, bình luận khỏi nhóm) là cuối cùng, không khiếu nại được; khác thao tác của Mod, Admin hệ thống, vẫn khiếu nại qua M09. Bài nhóm bị AI tự từ chối không phải quyết định cấp nhóm, khiếu nại qua M09 như bài thường. | — |
| BR-M11-22 | Sự kiện | Kiểm duyệt cấp nhóm chồng lên, không thay kiểm duyệt hệ thống: báo cáo (M08) và việc Mod, Admin hệ thống can thiệp vẫn áp dụng với nhóm và nội dung nhóm. | Bài P đã được Group Mod duyệt và đăng; người dùng báo cáo P → vụ vào hàng chờ báo cáo của Mod hệ thống như bài thường. |
| BR-M11-23 | Kích hoạt | Owner xóa nhóm là xóa mềm: nhóm và mọi nội dung của nhóm không hiện với ai, kể cả thành viên cũ; dữ liệu được giữ. Điểm của các thành viên không bị trừ vì nhóm bị xóa. | Member C có 20 điểm từ upvote trên bài trong nhóm N; Owner xóa N → bài của C không còn hiện; điểm của C giữ nguyên 20. |
| BR-M11-24 | Suy diễn | Thành viên rời nhóm hoặc bị kick (nhóm còn tồn tại): bài, bình luận của họ trong nhóm giữ nguyên, tác giả hiện như trước, điểm không đổi. Kick được xử lý giống tự rời. Sau khi rời, người đó vẫn sửa, xóa được bài, bình luận của mình ở nhóm Public; ở nhóm Private thì không. | C rời nhóm Public N có 3 bài → 3 bài vẫn ở N, hiện tên C; bài C đăng ẩn danh vẫn ẩn danh; C vẫn xóa được một bài của mình. C rời nhóm Private M → C không sửa, xóa được bài của mình trong M. |
| BR-M11-25 | Ràng buộc | Owner muốn rời nhóm phải chỉ định trước một thành viên khác làm Owner; chưa chỉ định thì không rời được. Owner là thành viên duy nhất thì rời nhóm là xóa nhóm, sau khi được cảnh báo. | Nhóm có A (Owner), B, C: A bấm rời → phải chọn B hoặc C làm Owner rồi mới rời được. Nhóm chỉ có A: A bấm rời → cảnh báo nhóm sẽ bị xóa; A xác nhận → nhóm bị xóa. |
| BR-M11-26 | Kích hoạt | Owner mất quyền ngoài ý muốn (bị ban tạm thời hoặc vĩnh viễn, bị vô hiệu hóa kể cả tự vô hiệu hóa, bị xóa tài khoản) thì hệ thống chuyển ngay vai trò Owner theo thứ tự: (1) Group Mod có thâm niên Group Mod dài nhất, tính từ lần bổ nhiệm gần nhất; (2) không có Group Mod thì Member có thời điểm tham gia sớm nhất; (3) Owner là thành viên duy nhất thì nhóm bị xóa mềm. Owner cũ ở lại nhóm với vai trò Member, kể cả khi tài khoản hoạt động trở lại. Việc này vẫn chạy khi cờ Group tắt hoặc nhóm Bị khóa. | Owner A bị ban 7 ngày từ 01/11. Group Mod B bổ nhiệm 01/09, Group Mod D bổ nhiệm 15/10 → B thành Owner ngày 01/11; ngày 08/11 A hết ban, vẫn là Member. D từng làm Group Mod từ 01/06, bị giáng 01/09, bổ nhiệm lại 20/10 → thâm niên của D tính từ 20/10. Không có Group Mod; Member C tham gia 01/08, E tham gia 01/07 → E thành Owner. Nhóm chỉ có A → nhóm bị xóa mềm. |
| BR-M11-27 | Kích hoạt | Nhóm Bị ẩn (M08): nhóm và mọi nội dung không hiện với ai, kể cả thành viên và Owner; dữ liệu được giữ; không có bỏ ẩn. | — |
| BR-M11-28 | Kích hoạt | Nhóm Bị khóa (M08): nhóm vẫn hiện như trước theo chế độ Public, Private và nội dung cũ vẫn đọc được. Bị chặn với mọi người, kể cả Owner và Group Mod: đăng bài, bình luận, vote, bình chọn poll, tham gia, mời; duyệt yêu cầu tham gia, duyệt bài chờ, gỡ nội dung, kick, chặn, bỏ chặn, bổ nhiệm, giáng Group Mod, đổi thông tin và cài đặt, xóa nhóm, Owner rời nhóm. Vẫn được: Member, Group Mod tự rời nhóm; bookmark, báo cáo; hệ thống tự chuyển quyền Owner. Mod, Admin mở khóa trực tiếp; nhóm đang Bị khóa vẫn có thể bị ẩn ở một vụ sau. | Nhóm N bị khóa lúc 09:00: Owner A đăng bài lúc 09:10 → bị từ chối; A kick C lúc 09:15 → bị từ chối; A xóa nhóm → bị từ chối; C tự rời lúc 09:20 → được; Guest đọc bài cũ (N Public) → được; A bị ban lúc 09:30 → Group Mod B thành Owner. Mod mở khóa lúc 10:00 → B làm lại mọi thao tác. |
| BR-M11-29 | Kích hoạt | Trong khi cờ Group tắt: mọi thao tác người dùng gửi tới module bị từ chối với thông báo "Hệ thống đang bận, vui lòng thử lại sau", kể cả mở nhóm, mở bài nhóm và tương tác với bài nhóm; nhóm và bài nhóm vẫn hiện ở các lối vào (danh sách nhóm, Trending, tab Group và tab Following của feed, tab Bài viết trên hồ sơ, tìm kiếm, bookmark, thông báo); việc hệ thống tự làm vẫn chạy (kế nhiệm Owner); dữ liệu không bị xóa hay đổi; bật lại cờ thì không làm bù; Admin vẫn dùng được module; kiểm duyệt M08 vẫn chạy. | Cờ tắt lúc 08:00; User C thấy bài nhóm P ở Trending lúc 08:06, bấm mở → "Hệ thống đang bận, vui lòng thử lại sau"; Admin mở P → đọc được. Owner bị ban lúc 09:00 → vẫn chuyển Owner lúc 09:00. |
| BR-M11-30 | Kích hoạt | Owner, Group Mod gỡ bài hoặc bình luận khỏi nhóm bằng một thao tác: xóa mềm; nội dung chỉ còn hiện với tác giả, Owner, Group Mod của nhóm, Mod và Admin; tác giả không tự hiện lại được; tác giả nhận thông báo trong ứng dụng; không trừ điểm; không khiếu nại. | Bài P của C (10 upvote, C có 20 điểm từ P) bị Group Mod B gỡ → Member khác, Guest không thấy P; C vẫn thấy P, nhận thông báo, giữ 20 điểm; C khiếu nại → bị từ chối. |
| BR-M11-31 | Ràng buộc | Tên nhóm bắt buộc, tối đa 100 ký tự; mô tả không bắt buộc, tối đa 500 ký tự; tên được trùng với nhóm khác. Khi tạo, người tạo chọn chế độ Public hoặc Private và đặt được ngay công tắc duyệt trước, công tắc ẩn danh, câu hỏi tham gia; mặc định hai công tắc Tắt, câu hỏi trống. | Tên 100 ký tự → được; 101 ký tự → bị từ chối; tên trống → bị từ chối. Mô tả 500 ký tự → được; 501 → bị từ chối. Hai nhóm cùng tên "Ôn thi Toán" → được. |
| BR-M11-32 | Kích hoạt | Owner đổi cài đặt làm nhóm thành vào ngay (Private sang Public không có câu hỏi tham gia, hoặc bỏ câu hỏi của nhóm Public) thì mọi yêu cầu tham gia đang Chờ duyệt của nhóm được chấp nhận ngay. | Nhóm Private N có 3 yêu cầu chờ; lúc 10:00 Owner đổi N sang Public, không câu hỏi → 3 người thành Member lúc 10:00. Nhóm Public M có câu hỏi và 2 yêu cầu chờ; Owner chỉ sửa câu hỏi → 2 yêu cầu vẫn chờ. |
| BR-M11-33 | Ràng buộc | Mod, Admin không là thành viên chỉ xem nội dung nhóm Private trong vụ báo cáo mình đang giữ (M08); không tìm, không thấy trong danh sách, không mở được trang nhóm Private. Hàng chờ duyệt của nhóm chỉ Owner, Group Mod của nhóm xử lý; Mod, Admin can thiệp nội dung nhóm qua báo cáo và vụ (M08). Ngoại lệ: bài của Owner có điểm 0.5–< 0.9 hoặc quét lỗi vào hàng chờ duyệt của Mod hệ thống (BR-M11-40). | Mod M không là thành viên nhóm Private N: tìm "N" → không thấy; mở link trang N → không hiển thị; nhận vụ báo cáo bài P của N → xem được P trong vụ. Bài Q của N đang chờ duyệt → M không duyệt được. |
| BR-M11-34 | Suy diễn | Ai xem được trang nhóm thì xem được danh sách thành viên kèm vai trò nhóm: nhóm Public — mọi người kể cả Guest; nhóm Private — thành viên. | Guest mở danh sách thành viên nhóm Public N → thấy; người ngoài D mở danh sách thành viên nhóm Private M → không thấy. |
| BR-M11-35 | Sự kiện | Trang danh sách nhóm (nơi nút "Khám phá Group" của M14 dẫn tới) gồm các nhóm Private mà người xem là thành viên và các nhóm Public; mỗi nhóm hiện tên, mô tả, chế độ; xếp theo thời điểm tạo, mới nhất trước. Tìm nhóm theo tên thuộc M06. | Nhóm Public N1 tạo 01/11, N2 tạo 05/11, nhóm Private P (C là thành viên) tạo 03/11 → C thấy N2, P, N1 theo thứ tự đó; Guest thấy N2, N1. |
| BR-M11-36 | Kích hoạt | Người gửi rút được yêu cầu tham gia đang Chờ duyệt của mình; yêu cầu chuyển sang Đã rút. | — |
| BR-M11-37 | Sự kiện | Thông báo trong ứng dụng của nhóm (M07): được mời → người được mời (kèm link mời); có yêu cầu tham gia mới → Owner và các Group Mod; yêu cầu được chấp nhận → người gửi; được bổ nhiệm Group Mod → người đó; bị kick → người đó; trở thành Owner (do chỉ định hoặc tự chuyển) → người đó; bài, bình luận bị gỡ khỏi nhóm → tác giả. Không có thông báo khi: vào ngay nhóm Public, yêu cầu bị từ chối, bị giáng Group Mod. | — |
| BR-M11-38 | Ràng buộc | Nhóm từ chối bài chờ duyệt phải kèm lý do; tác giả sửa và gửi lại được, bài gửi lại đi qua cổng duyệt của nhóm thêm một lần. Bài nhóm bị AI tự từ chối khiếu nại qua M09 như bài thường; khiếu nại được chấp nhận thì bài đi tiếp qua cổng duyệt của nhóm như bài có điểm quét dưới 0.5, không quét lại: công tắc duyệt trước bật → chờ nhóm duyệt; tắt, hoặc bài của Owner → Đã đăng. | Group Mod B từ chối bài P không nhập lý do → bị từ chối thao tác; nhập "Lạc đề" → P Bị từ chối. Tác giả sửa P, gửi lại → P được quét lại và qua cổng của nhóm. |
| BR-M11-39 | Ràng buộc | Group Mod không tự nhận, chấp nhận hay từ chối bài chờ duyệt của chính mình; bài của Group Mod do Owner hoặc Group Mod khác duyệt. Bài của Owner không vào hàng chờ của nhóm (BR-M11-40). | Group Mod B gửi bài, điểm 0.6 → Owner A hoặc Group Mod D duyệt; B nhận bài của mình → bị từ chối. |
| BR-M11-40 | Kích hoạt | Bài của Owner trong nhóm của mình không qua duyệt của nhóm (bỏ qua công tắc duyệt trước và bước nhóm bắt buộc duyệt với điểm 0.5–< 0.9). Quét AI vẫn áp dụng: điểm ≥ 0.9 → bị tự từ chối; 0.5 ≤ điểm < 0.9, hoặc quét thất bại sau một lần thử lại → vào hàng chờ duyệt của Mod hệ thống như bài không thuộc nhóm (M03); điểm < 0.5, hoặc công tắc AI tổng hay Moderation tắt → đăng ngay. Owner là Admin thì không quét, đăng ngay. | Owner An, nhóm bật công tắc duyệt trước: bài điểm 0.30 → Đã đăng; 0.95 → Bị từ chối; 0.60 → hàng chờ Mod hệ thống; quét lỗi → hàng chờ Mod hệ thống; AI tắt → Đã đăng. An là Admin → Đã đăng, không quét. |

### 5.19 Dữ liệu nghiệp vụ

| Thực thể | Thuộc tính nguồn đã nêu | Quan hệ |
|---|---|---|
| Nhóm | Tên (bắt buộc, tối đa 100 ký tự); mô tả (tối đa 500 ký tự); chế độ (Public, Private); câu hỏi tham gia (tùy chọn, tối đa một); công tắc duyệt trước (Bật, Tắt; mặc định Tắt); công tắc ẩn danh (Bật, Tắt; mặc định Tắt); người tạo; Owner; đã xóa (khi Owner xóa); trạng thái kiểm duyệt (Bình thường, Bị khóa, Bị ẩn — M08 quyết); thời điểm tạo (đếm số nhóm tạo trong 24 giờ, xếp danh sách nhóm); link mời (một link chung, không hết hạn) | Có nhiều thành viên nhóm, nhiều yêu cầu tham gia, nhiều người bị chặn, nhiều bài nhóm; một Owner |
| Thành viên nhóm | Người dùng; nhóm; vai trò nhóm (Owner, Group Mod, Member); thời điểm tham gia; thời điểm được bổ nhiệm Group Mod (khi là Group Mod) | Một người dùng là thành viên của nhiều nhóm, mỗi nhóm một vai trò |
| Yêu cầu tham gia | Người gửi; nhóm; câu trả lời (bắt buộc khi nhóm có câu hỏi); trạng thái (Chờ duyệt, Đã chấp nhận, Đã từ chối, Đã rút) | Một người có thể có nhiều yêu cầu theo thời gian tới cùng một nhóm, tối đa một yêu cầu Chờ duyệt |
| Chặn tham gia | Nhóm; người bị chặn | Một nhóm chặn nhiều người dùng |
| Bài viết (M03) — phần M11 | Nhóm (tùy chọn); ẩn danh (Có, Không); điểm quét; người đang giữ và thời điểm thao tác cuối (khi bài trong hàng chờ duyệt của nhóm); lý do khi nhóm từ chối; dấu bị gỡ khỏi nhóm (xóa mềm; bài giữ trạng thái đăng) | Thuộc tối đa một nhóm; tác giả là thành viên nhóm |

**Ma trận CRUD:**

| Thực thể | Tạo | Đọc | Sửa | Xóa |
|---|---|---|---|---|
| Nhóm | FR-M11-01.01 | FR-M11-03.01, FR-M11-03.04, FR-M11-03.05 | Thông tin, cài đặt: FR-M11-02.01, FR-M11-02.02, FR-M11-02.05, FR-M11-02.06, FR-M11-02.07; Owner: FR-M11-10.04, FR-M11-11.01, FR-M11-11.02; trạng thái kiểm duyệt: M08, áp dụng ở FR-M11-16.01, FR-M11-16.04, FR-M11-16.06 | Xóa mềm: FR-M11-15.01, FR-M11-10.06, FR-M11-11.03 (BR-M11-23) |
| Thành viên nhóm | FR-M11-01.02, FR-M11-04.01, FR-M11-06.02, FR-M11-02.14 | FR-M11-03.14, FR-M11-08.05 | FR-M11-08.01, FR-M11-08.02, FR-M11-10.04, FR-M11-11.01, FR-M11-11.02, FR-M11-11.05 | FR-M11-09.01, FR-M11-09.02, FR-M11-10.01, FR-M11-10.04 |
| Yêu cầu tham gia | FR-M11-04.03 | FR-M11-06.01 | FR-M11-06.02, FR-M11-06.03, FR-M11-02.14, FR-M11-07.03, FR-M11-04.10 | Không có (BR-M11-36: rút thì chuyển sang Đã rút) |
| Chặn tham gia | FR-M11-07.01 | FR-M11-07.04 | Không có (BR-M11-10: chỉ có chặn, bỏ chặn) | FR-M11-07.05 |
| Bài viết (M03) — phần M11 | FR-M11-12.01 (M03 soạn bài) | FR-M11-03.04, FR-M11-03.05, FR-M11-03.06, FR-M11-03.12 | FR-M11-12.02, FR-M11-12.03, FR-M11-12.04, FR-M11-12.05, FR-M11-12.06, FR-M11-12.14, FR-M11-12.15, FR-M11-12.16, FR-M11-12.17, FR-M11-12.18, FR-M11-12.19, FR-M11-12.20, FR-M11-13.05, FR-M11-13.06, FR-M11-13.11, FR-M11-14.01; M03 (tác giả sửa) | FR-M11-14.01; M03 (tác giả xóa) |

### 5.20 Chuyển trạng thái

#### Nhóm — tồn tại

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Người dùng tạo nhóm | Chưa quá giới hạn tạo nhóm trong ngày (BR-M11-03) | Hoạt động | FR-M11-01.01, FR-M11-01.03 |
| Hoạt động | Owner xóa nhóm | — | Đã xóa | FR-M11-15.01 |
| Hoạt động | Owner là thành viên duy nhất rời nhóm | Đã xác nhận cảnh báo (BR-M11-25) | Đã xóa | FR-M11-10.06 |
| Hoạt động | Owner mất quyền ngoài ý muốn | Owner là thành viên duy nhất (BR-M11-26) | Đã xóa | FR-M11-11.03 |

#### Nhóm — trạng thái kiểm duyệt (M08 quyết, M11 áp dụng)

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Nhóm được tạo | — | Bình thường | FR-M11-01.01 |
| Bình thường | Mod, Admin khóa nhóm trong vụ báo cáo | — | Bị khóa | M08; FR-M11-16.04 |
| Bị khóa | Mod, Admin mở khóa nhóm | — | Bình thường | M08; FR-M11-16.06 |
| Bình thường | Mod, Admin ẩn nhóm trong vụ báo cáo | — | Bị ẩn | M08; FR-M11-16.01 |
| Bị khóa | Mod, Admin ẩn nhóm trong một vụ sau | — | Bị ẩn | M08; FR-M11-16.01 |

#### Nhóm — chế độ

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Người dùng tạo nhóm | Người tạo chọn chế độ | Public hoặc Private | FR-M11-01.01 |
| Public | Owner đổi chế độ | — | Private | FR-M11-02.02, FR-M11-02.03, FR-M11-02.04 |
| Private | Owner đổi chế độ | — | Public | FR-M11-02.02 |

#### Vai trò của thành viên nhóm

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Người dùng tạo nhóm | — | Owner | FR-M11-01.02 |
| (bắt đầu) | Người ngoài nhóm tham gia nhóm Public không có câu hỏi | Không bị chặn | Member | FR-M11-04.01 |
| (bắt đầu) | Owner hoặc Group Mod chấp nhận yêu cầu tham gia | — | Member | FR-M11-06.02 |
| (bắt đầu) | Owner đổi cài đặt làm nhóm thành vào ngay | Có yêu cầu đang Chờ duyệt (BR-M11-32) | Member | FR-M11-02.14 |
| Member | Owner bổ nhiệm | — | Group Mod | FR-M11-08.01 |
| Group Mod | Owner giáng | — | Member | FR-M11-08.02 |
| Member | Owner chỉ định làm người kế nhiệm rồi rời | — | Owner | FR-M11-10.04 |
| Group Mod | Owner chỉ định làm người kế nhiệm rồi rời | — | Owner | FR-M11-10.04 |
| Member | Hệ thống chọn khi Owner mất quyền ngoài ý muốn | Không còn Group Mod nào; tham gia sớm nhất (BR-M11-26) | Owner | FR-M11-11.02 |
| Group Mod | Hệ thống chọn khi Owner mất quyền ngoài ý muốn | Thâm niên Group Mod dài nhất (BR-M11-26) | Owner | FR-M11-11.01 |
| Member | Rời nhóm, hoặc bị Owner, Group Mod kick | — | (kết thúc) | FR-M11-10.01, FR-M11-09.01, FR-M11-09.02 |
| Group Mod | Rời nhóm, hoặc bị Owner kick | — | (kết thúc) | FR-M11-10.01, FR-M11-09.01 |
| Owner | Rời nhóm | Đã chỉ định người kế nhiệm (BR-M11-25); nhóm không Bị khóa (BR-M11-28) | (kết thúc) | FR-M11-10.04, FR-M11-16.08 |
| Owner | Hệ thống tự chuyển quyền khi Owner mất quyền ngoài ý muốn | Còn thành viên khác (BR-M11-26) | Member | FR-M11-11.05 |

#### Yêu cầu tham gia

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Người ngoài nhóm gửi yêu cầu (kể cả qua lời mời) | Nhóm cần duyệt (BR-M11-07); người gửi không bị chặn, chưa có yêu cầu Chờ duyệt; đã trả lời câu hỏi nếu có | Chờ duyệt | FR-M11-04.03, FR-M11-04.06, FR-M11-04.08, FR-M11-04.09, FR-M11-05.05 |
| Chờ duyệt | Owner hoặc Group Mod chấp nhận | — | Đã chấp nhận | FR-M11-06.02 |
| Chờ duyệt | Owner hoặc Group Mod từ chối | — | Đã từ chối | FR-M11-06.03 |
| Chờ duyệt | Owner hoặc Group Mod chặn người gửi | — | Đã từ chối | FR-M11-07.03 |
| Chờ duyệt | Owner đổi cài đặt làm nhóm thành vào ngay | BR-M11-32 | Đã chấp nhận | FR-M11-02.14 |
| Chờ duyệt | Người gửi rút yêu cầu | — | Đã rút | FR-M11-04.10 |

#### Bài nhóm — phần cổng duyệt của nhóm (các trạng thái khác theo M03)

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Thành viên soạn bài trong nhóm (M03) | — | Nháp | M03 |
| Nháp | Thành viên gửi bài vào nhóm | Tác giả khác Owner; có quét AI (công tắc AI tổng và Moderation bật; tác giả khác Admin) | Chờ duyệt (đang quét) | FR-M11-12.01 |
| Nháp | Thành viên khác Owner gửi bài vào nhóm khi không quét (AI tắt hoặc tác giả là Admin) | Công tắc duyệt trước bật | Chờ duyệt (chờ nhóm duyệt) | FR-M11-12.06, FR-M11-12.14 |
| Nháp | Thành viên khác Owner gửi bài vào nhóm khi không quét (AI tắt hoặc tác giả là Admin) | Công tắc duyệt trước tắt | Đã đăng | FR-M11-12.06, FR-M11-12.14 |
| Chờ duyệt (đang quét) | Quét thất bại sau một lần thử lại | — | Chờ duyệt (chờ nhóm duyệt) | FR-M11-12.15 |
| Nháp | Owner gửi bài vào nhóm của mình | Điểm < 0.5; hoặc AI tắt; hoặc Owner là Admin (BR-M11-40) | Đã đăng | FR-M11-12.19, FR-M11-12.20 |
| Nháp | Owner gửi bài vào nhóm của mình | Điểm ≥ 0.9 | Bị từ chối | FR-M11-12.17 |
| Nháp | Owner gửi bài vào nhóm của mình | 0.5 ≤ điểm < 0.9, hoặc quét thất bại | Chờ duyệt (hàng chờ Mod hệ thống, M03) | FR-M11-12.18 |
| Chờ duyệt (đang quét) | Quét xong | Điểm ≥ 0.9 | Bị từ chối | FR-M11-12.02 |
| Chờ duyệt (đang quét) | Quét xong | 0.5 ≤ điểm < 0.9; hoặc điểm < 0.5 và công tắc duyệt trước bật | Chờ duyệt (chờ nhóm duyệt) | FR-M11-12.03, FR-M11-12.04 |
| Chờ duyệt (đang quét) | Quét xong | Điểm < 0.5 và công tắc duyệt trước tắt | Đã đăng | FR-M11-12.05 |
| Chờ duyệt (chờ nhóm duyệt) | Owner hoặc Group Mod chấp nhận | Đang giữ bài; không phải bài của chính mình (BR-M11-20, BR-M11-39) | Đã đăng | FR-M11-13.05 |
| Chờ duyệt (chờ nhóm duyệt) | Owner hoặc Group Mod từ chối | Đang giữ bài; có lý do; không phải bài của chính mình (BR-M11-20, BR-M11-38, BR-M11-39) | Bị từ chối | FR-M11-13.06 |
| Bị từ chối | Tác giả sửa và gửi lại | — | Chờ duyệt (đang quét) | FR-M11-13.11 |
| Bị từ chối | Khiếu nại bài bị AI tự từ chối được chấp nhận (M09) | Tác giả chưa gửi lại; tác giả khác Owner; công tắc duyệt trước bật | Chờ duyệt (chờ nhóm duyệt) | FR-M11-13.14 |
| Bị từ chối | Khiếu nại bài bị AI tự từ chối được chấp nhận (M09) | Tác giả chưa gửi lại; công tắc duyệt trước tắt, hoặc tác giả là Owner | Đã đăng | FR-M11-13.14 |
| Đã đăng | Owner hoặc Group Mod gỡ khỏi nhóm | Người gỡ là Group Mod thì bài không phải của Owner, Group Mod khác (BR-M11-05) | Đã đăng, mang dấu bị gỡ khỏi nhóm | FR-M11-14.01 |

### 5.21 Giao tiếp với module khác

| Hướng | Module | Nội dung ở mức nghiệp vụ | Yêu cầu |
|---|---|---|---|
| Dùng | M01 | Trạng thái tài khoản (bị ban, vô hiệu hóa, đã xóa) để tự chuyển quyền Owner; yêu cầu đăng nhập khi Guest tham gia | FR-M11-11.01, FR-M11-04.05 |
| Cung cấp | M01 | Thành viên nhóm, để xếp danh sách gợi ý nhắc tên trong bài nhóm | FR-M11-04.01, FR-M11-06.02 |
| Cung cấp | M02 | Thành viên nhóm Private và bài ẩn danh, để chọn bài hiện ở tab Bài viết và bài đã lưu xem được | FR-M11-03.06, FR-M11-03.09 |
| Dùng | M03 | Soạn bài, trạng thái đăng, sửa, xóa của tác giả (kể cả người đã rời nhóm Public); bài thuộc nhóm theo cổng duyệt của M11; hàng chờ duyệt của Mod hệ thống cho bài của Owner có điểm 0.5–< 0.9 hoặc quét lỗi | FR-M11-12.01, FR-M11-10.08, FR-M11-12.18 |
| Cung cấp | M03 | Cổng duyệt của nhóm thay cho luồng duyệt của bài không thuộc nhóm; lựa chọn ẩn danh | FR-M11-12.01, FR-M11-12.02, FR-M11-12.03, FR-M11-12.04, FR-M11-12.05, FR-M11-12.07 |
| Cung cấp | M04 | Quyền bình luận theo thành viên nhóm; nhóm Private chặn bình luận của người ngoài; nhóm chuyển Private chặn tương tác | FR-M11-03.07, FR-M11-03.08, FR-M11-02.03 |
| Cung cấp | M05 | Bài nhóm Public tính vào Trending, bài nhóm Private không tính | FR-M11-12.12, FR-M11-12.13 |
| Cung cấp | M06 | Nhóm, chế độ Public, Private, thành viên nhóm, việc nhóm đổi sang Private, để tìm Group và lọc bài | FR-M11-02.02, FR-M11-02.04, FR-M11-03.02 |
| Cung cấp | M07 | Sự kiện thông báo trong ứng dụng: mời (kèm link mời), yêu cầu tham gia mới (tới Owner, Group Mod), yêu cầu được chấp nhận, bổ nhiệm Group Mod, kick, trở thành Owner, bài, bình luận bị gỡ khỏi nhóm; quyền xem nội dung nhóm Private; bài nhóm được đăng hoặc bị nhóm từ chối qua cổng duyệt (dùng chung sự kiện bài được đăng, bị từ chối của M03) | FR-M11-12.05, FR-M11-12.06, FR-M11-13.05, FR-M11-13.06, FR-M11-05.02, FR-M11-06.04, FR-M11-06.07, FR-M11-08.03, FR-M11-09.06, FR-M11-10.07, FR-M11-11.07, FR-M11-14.06 |
| Dùng | M08 | Trạng thái kiểm duyệt của nhóm (Bình thường, Bị khóa, Bị ẩn); báo cáo và can thiệp của Mod, Admin với nhóm và nội dung nhóm; vụ báo cáo là nơi Mod, Admin xem nội dung nhóm Private | FR-M11-16.01, FR-M11-16.04, FR-M11-16.06, FR-M11-16.07, FR-M11-14.04, FR-M11-03.12 |
| Cung cấp | M08 | Danh tính thật của bài ẩn danh; nhóm Private chặn báo cáo của người ngoài | FR-M11-03.10, FR-M11-02.03 |
| Cung cấp | M09 | Quyết định kiểm duyệt cấp nhóm không khiếu nại được; bài nhóm bị AI tự từ chối khiếu nại được như bài thường, được chấp nhận thì đi tiếp qua cổng duyệt của nhóm | FR-M11-13.07, FR-M11-14.03, FR-M11-13.12, FR-M11-13.14 |
| Cung cấp | M13 | Bài nhóm chuyển sang Đã đăng qua cổng duyệt của nhóm, để tạo embedding như mọi bài Đã đăng | FR-M11-12.05, FR-M11-12.06, FR-M11-13.05, FR-M11-13.14 |
| Cung cấp | M15 | Bài bị gỡ khỏi nhóm giữ trạng thái đăng (dấu bị gỡ khỏi nhóm), để thống kê nội dung đếm theo trạng thái đăng của bài | FR-M11-14.01 |
| Dùng | M10 | Cờ tính năng Group | FR-M11-17.01, FR-M11-17.03 |
| Cung cấp | M12 | Nhóm bị xóa, thành viên rời hoặc bị kick, nội dung bị gỡ khỏi nhóm, để M12 không trừ điểm | FR-M11-15.03, FR-M11-09.05, FR-M11-10.02, FR-M11-14.07 |
| Cung cấp | M12 | Quyền vote bài nhóm: thành viên vote bài nhóm mình; người ngoài nhóm đã đăng nhập vote bài nhóm Public; nhóm Private (kể cả vừa chuyển Private) và nhóm Bị khóa chặn vote | FR-M11-03.07, FR-M11-03.08, FR-M11-03.13, FR-M11-02.03, FR-M11-16.04 |
| Dùng | M13 | Điểm quét của bài trong nhóm, cùng ngưỡng 0.9, 0.5 | FR-M11-12.02, FR-M11-12.03, FR-M11-12.04, FR-M11-12.05 |
| Cung cấp | M14 | Bài nhóm cho tab Group của thành viên; bài nhóm Public cho Trending, không cho Newest; bài nhóm Public cho tab Following, không có bài nhóm Private; bài nhóm đăng ẩn danh; trang danh sách nhóm cho nút "Khám phá Group"; lối vào (Trending, tab Group, tab Following) vẫn hiện khi cờ Group tắt | FR-M11-03.05, FR-M11-12.07, FR-M11-12.12, FR-M11-12.13, FR-M11-03.16, FR-M11-17.07 |

### 5.22 AI hỗ trợ và hành vi khi tắt AI

Module dùng điểm quét AI của M13 ở cổng duyệt của nhóm: FR-M11-12.02, FR-M11-12.03, FR-M11-12.04, FR-M11-12.05.
Khi công tắc AI tổng hoặc Moderation tắt (có chủ đích), bài nhóm đi theo công tắc duyệt trước: FR-M11-12.14. Khi quét thất
bại sau một lần thử lại, bài bắt buộc chờ nhóm duyệt: FR-M11-12.15. Bài của Admin không bị quét, đi theo công tắc duyệt
trước: FR-M11-12.06. Bài của Owner không qua duyệt của nhóm, chỉ chịu quét AI; điểm 0.5–< 0.9 hoặc quét lỗi thì vào hàng
chờ Mod hệ thống: FR-M11-12.16 đến FR-M11-12.20.

### 5.23 Yêu cầu HMI

Chưa có — chờ giai đoạn thiết kế.

### 5.24 Chuyển màn hình

Chưa có — chờ giai đoạn thiết kế.

## 6. Lịch sử sửa đổi

| Phiên bản | Ngày | Nội dung | Người sửa |
|---|---|---|---|
| 0.1 | 2026-10-21 | Tạo mới | Phạm Văn Đức |
| 1.0 | 2026-10-21 | Chốt sau 7 bước; câu trả lời bước 6 và sửa ở bước 7 (bài của Owner không qua duyệt của nhóm) ghi ở DEC-229–240 | Phạm Văn Đức |
| 1.1 | 2026-10-23 | Rà lại với register tới DEC-247: thêm dòng Cung cấp M12 về quyền vote bài nhóm, khớp FR-M12. Không đổi yêu cầu. Chốt bản 1.1 | Phạm Văn Đức |
| 1.2 | 2026-10-24 | Đối chiếu với FR-M14 (DEC-258, DEC-261, DEC-262): bài nhóm Public vào tab Following, bài nhóm Private vẫn không ra feed chính kể cả tab Following (BR-M11-14); tab Group, tab Following là lối vào khi cờ Group tắt (FR-M11-17.07, BR-M11-29); dòng Cung cấp M14 thêm bài nhóm cho tab Following và bài đăng ẩn danh. Chốt bản 1.2 | Phạm Văn Đức |
| 1.3 | 2026-10-24 | Rà soát chéo toàn bộ FR (review-cross-module.md): gỡ khỏi nhóm là dấu, bài giữ trạng thái đăng (DEC-270: thuật ngữ, dữ liệu, bảng trạng thái, thêm dòng Cung cấp M15); bài nhóm bị AI từ chối được chấp nhận khiếu nại đi qua cổng duyệt của nhóm (DEC-271: thêm FR-M11-13.14, BR-M11-38, bảng trạng thái, giao tiếp M09); dòng Cung cấp M07 và dòng mới Cung cấp M13 gồm bài nhóm được đăng, bị từ chối qua cổng duyệt; C.1, C.2. Chốt bản 1.3 | Phạm Văn Đức |

## Phụ lục A. Truy vết

| ID | Nguồn | Căn cứ | Ghi chú |
|---|---|---|---|
| FR-M11-01 | DEC-101, DEC-106, DM-5.1, F-GRP-01, MR-M11 | Nói thẳng | — |
| FR-M11-01.01 | DM-5.1, DEC-101, DEC-194 | Suy ra | DM-5.1 nêu tên, mô tả, public/private; nhóm mới chưa bị Mod, Admin xử lý nên ở Bình thường (DEC-194 có ba trạng thái kiểm duyệt) |
| FR-M11-01.02 | DM-5.1, DEC-107 | Suy ra | Draft "Người tạo / owner"; thời điểm tham gia cần cho thứ tự kế nhiệm DEC-107 |
| FR-M11-01.03 | DEC-101, DEC-237 | Nói thẳng | — |
| FR-M11-01.04 | DEC-101, QA-011 | Suy ra | "Any logged-in user can create" ⇒ Guest bị từ chối |
| FR-M11-01.05 | DEC-101, DEC-106 | Nói thẳng | — |
| FR-M11-01.06 | DEC-237 | Nói thẳng | — |
| FR-M11-01.07 | DEC-237 | Nói thẳng | — |
| FR-M11-01.08 | DEC-237 | Nói thẳng | — |
| FR-M11-01.09 | DEC-237 | Nói thẳng | — |
| FR-M11-01.10 | DEC-237 | Nói thẳng | — |
| FR-M11-01.11 | DEC-237 | Nói thẳng | — |
| FR-M11-01.12 | DEC-237 | Nói thẳng | — |
| FR-M11-02 | DEC-102, DEC-108, DEC-009, DEC-112, QA-016, QA-045, F-GRP-01, F-GRP-04, F-GRP-06, F-GRP-09, F-GRP-10, DM-5.1 | Nói thẳng | — |
| FR-M11-02.01 | F-GRP-01, DEC-102 | Suy ra | F-GRP-01 "Edit group"; DEC-102 cho Owner đổi cài đặt nhóm ⇒ Owner sửa được thông tin nhóm |
| FR-M11-02.02 | DEC-108 | Nói thẳng | — |
| FR-M11-02.03 | DEC-108 | Nói thẳng | — |
| FR-M11-02.04 | DEC-108 | Nói thẳng | — |
| FR-M11-02.05 | DEC-102, DEC-104, QA-016 | Suy ra | Công tắc quyết nhánh của bài lúc gửi (DEC-104) ⇒ đổi công tắc áp cho bài gửi sau đó |
| FR-M11-02.06 | DEC-009, DEC-112 | Nói thẳng | — |
| FR-M11-02.07 | QA-045, DEC-103 | Suy ra | Câu hỏi được trả lời lúc gửi yêu cầu ⇒ câu hỏi mới chỉ áp cho yêu cầu gửi sau |
| FR-M11-02.08 | QA-045 | Nói thẳng | — |
| FR-M11-02.09 | DEC-102 | Nói thẳng | — |
| FR-M11-02.10 | DEC-102, DEC-237 | Nói thẳng | — |
| FR-M11-02.11 | DEC-237 | Nói thẳng | — |
| FR-M11-02.12 | DEC-108, DEC-234 | Nói thẳng | — |
| FR-M11-02.13 | DEC-234 | Nói thẳng | — |
| FR-M11-02.14 | DEC-237 | Nói thẳng | — |
| FR-M11-02.15 | DEC-237 | Nói thẳng | — |
| FR-M11-03 | QA-011, DEC-110, DEC-111, DEC-108, DEC-112, QA-015, DM-5.3, QA-230, GL:Group | Nói thẳng | — |
| FR-M11-03.01 | QA-011 | Nói thẳng | — |
| FR-M11-03.02 | QA-011, DEC-110 | Nói thẳng | — |
| FR-M11-03.03 | DEC-210 | Suy ra | DEC-210 "A member of the Private group still finds it" (ở tìm kiếm) ⇒ thành viên cũng thấy nhóm của mình ở danh sách |
| FR-M11-03.04 | QA-011, DM-5.1 | Nói thẳng | — |
| FR-M11-03.05 | DEC-111, QA-011 | Nói thẳng | — |
| FR-M11-03.06 | QA-011, DM-5.3, DEC-062 | Nói thẳng | — |
| FR-M11-03.07 | DEC-108, DM-5.3 | Suy ra | Người ngoài không xem được nội dung nhóm Private ⇒ không tương tác được; DEC-108 chặn tương tác khi nhóm thành Private |
| FR-M11-03.08 | DEC-102 | Nói thẳng | — |
| FR-M11-03.09 | QA-015, DEC-112 | Nói thẳng | — |
| FR-M11-03.10 | QA-015, DEC-112 | Nói thẳng | — |
| FR-M11-03.11 | DEC-233, DEC-210 | Nói thẳng | — |
| FR-M11-03.12 | DEC-233 | Nói thẳng | — |
| FR-M11-03.13 | DEC-234 | Nói thẳng | — |
| FR-M11-03.14 | DEC-238 | Nói thẳng | — |
| FR-M11-03.15 | DEC-238 | Nói thẳng | — |
| FR-M11-03.16 | DEC-237, QA-230 | Nói thẳng | — |
| FR-M11-03.17 | DEC-237 | Nói thẳng | — |
| FR-M11-03.18 | DEC-229 | Suy ra | Người được mời theo luồng tham gia (DEC-229) phải biết nhóm và trả lời câu hỏi để gửi yêu cầu ⇒ thấy tên, mô tả nhóm |
| FR-M11-04 | DEC-103, QA-044, QA-045, DM-5.2, F-GRP-03, F-GRP-08, F-GRP-09, DEC-126 | Nói thẳng | — |
| FR-M11-04.01 | DEC-103, F-GRP-03 | Nói thẳng | — |
| FR-M11-04.02 | QA-045, DEC-103 | Nói thẳng | — |
| FR-M11-04.03 | DEC-103, QA-044, QA-045, F-GRP-08 | Nói thẳng | — |
| FR-M11-04.04 | DEC-103 | Nói thẳng | — |
| FR-M11-04.05 | DEC-126 | Nói thẳng | — |
| FR-M11-04.06 | DEC-103, DEC-238 | Nói thẳng | — |
| FR-M11-04.07 | DEC-106 | Nói thẳng | — |
| FR-M11-04.08 | DEC-237 | Nói thẳng | — |
| FR-M11-04.09 | DEC-237 | Nói thẳng | — |
| FR-M11-04.10 | DEC-238 | Nói thẳng | — |
| FR-M11-05 | DEC-110, QA-044, F-GRP-07 | Nói thẳng | Cách người được mời vào nhóm chờ Q-01 |
| FR-M11-05.01 | DEC-110, QA-044, F-GRP-07 | Nói thẳng | — |
| FR-M11-05.02 | DEC-065, DEC-238 | Nói thẳng | — |
| FR-M11-05.03 | DEC-110 | Suy ra | "Any group member ... can invite" ⇒ người ngoài nhóm không mời được |
| FR-M11-05.04 | DEC-110 | Nói thẳng | — |
| FR-M11-05.05 | DEC-229 | Nói thẳng | — |
| FR-M11-05.06 | DEC-238 | Nói thẳng | — |
| FR-M11-05.07 | DEC-238 | Nói thẳng | — |
| FR-M11-06 | DEC-102, DEC-103, QA-044, QA-045, F-GRP-08 | Nói thẳng | — |
| FR-M11-06.01 | QA-045, DEC-103 | Nói thẳng | — |
| FR-M11-06.02 | DEC-103, DEC-102, F-GRP-08 | Nói thẳng | — |
| FR-M11-06.03 | DEC-103 | Nói thẳng | — |
| FR-M11-06.04 | DEC-065, DEC-237 | Nói thẳng | — |
| FR-M11-06.05 | DEC-102 | Nói thẳng | — |
| FR-M11-06.06 | DEC-103 | Suy ra | Chỉ yêu cầu Chờ duyệt mới được duyệt (bảng trạng thái) ⇒ yêu cầu đã xử lý không duyệt lại được |
| FR-M11-06.07 | DEC-237, DEC-065 | Nói thẳng | — |
| FR-M11-06.08 | DEC-237 | Nói thẳng | — |
| FR-M11-06.09 | DEC-237 | Nói thẳng | — |
| FR-M11-07 | DEC-103 | Nói thẳng | — |
| FR-M11-07.01 | DEC-103 | Nói thẳng | — |
| FR-M11-07.02 | DEC-103, DEC-238 | Suy ra | Chặn do Owner/Mod làm (DEC-103); DEC-238 cho Owner, Group Mod xem danh sách và bỏ chặn ⇒ vai trò khác không làm được |
| FR-M11-07.03 | DEC-238 | Nói thẳng | — |
| FR-M11-07.04 | DEC-238 | Nói thẳng | — |
| FR-M11-07.05 | DEC-238 | Nói thẳng | — |
| FR-M11-08 | DEC-102, QA-016 | Nói thẳng | — |
| FR-M11-08.01 | DEC-102, QA-016, DEC-107 | Suy ra | Thời điểm bổ nhiệm cần cho thâm niên Group Mod ở DEC-107 |
| FR-M11-08.02 | DEC-102 | Nói thẳng | — |
| FR-M11-08.03 | DEC-065 | Suy ra | DEC-065 có sự kiện "promote" của nhóm ⇒ người được bổ nhiệm nhận thông báo |
| FR-M11-08.04 | DEC-102 | Nói thẳng | — |
| FR-M11-08.05 | DEC-102, DEC-107 | Suy ra | Owner chỉ làm được các thao tác này trên một thành viên cụ thể ⇒ phải thấy thành viên; ai khác xem danh sách chờ Q-16 |
| FR-M11-08.06 | DEC-237 | Nói thẳng | — |
| FR-M11-09 | DEC-102, DEC-105, DEC-113 | Nói thẳng | — |
| FR-M11-09.01 | DEC-102 | Nói thẳng | — |
| FR-M11-09.02 | DEC-102 | Nói thẳng | — |
| FR-M11-09.03 | DEC-102 | Nói thẳng | — |
| FR-M11-09.04 | DEC-102 | Nói thẳng | — |
| FR-M11-09.05 | DEC-105, DEC-113 | Nói thẳng | — |
| FR-M11-09.06 | DEC-065 | Suy ra | DEC-065 có sự kiện "kick" của nhóm ⇒ người bị kick nhận thông báo |
| FR-M11-09.07 | DEC-105, DEC-113 | Suy ra | "Kicked is treated identically to voluntary leave" ⇒ người bị kick như người đã rời, tham gia lại theo BR-M11-07; muốn ngăn thì nhóm chặn (BR-M11-10) |
| FR-M11-10 | DEC-107, DEC-105, DEC-113 | Nói thẳng | — |
| FR-M11-10.01 | DEC-105, DEC-113, DEC-107 | Nói thẳng | — |
| FR-M11-10.02 | DEC-105, DEC-113 | Nói thẳng | — |
| FR-M11-10.03 | DEC-107 | Nói thẳng | — |
| FR-M11-10.04 | DEC-107 | Nói thẳng | — |
| FR-M11-10.05 | DEC-107 | Nói thẳng | — |
| FR-M11-10.06 | DEC-107 | Nói thẳng | — |
| FR-M11-10.07 | DEC-237 | Nói thẳng | — |
| FR-M11-10.08 | DEC-237 | Nói thẳng | — |
| FR-M11-10.09 | DEC-237 | Nói thẳng | — |
| FR-M11-11 | DEC-107, DEC-225 | Nói thẳng | — |
| FR-M11-11.01 | DEC-107, DEC-232 | Nói thẳng | — |
| FR-M11-11.02 | DEC-107 | Nói thẳng | — |
| FR-M11-11.03 | DEC-107, DEC-105, DEC-113 | Nói thẳng | — |
| FR-M11-11.04 | DEC-225 | Nói thẳng | — |
| FR-M11-11.05 | DEC-232 | Nói thẳng | — |
| FR-M11-11.06 | DEC-237 | Nói thẳng | — |
| FR-M11-11.07 | DEC-237 | Nói thẳng | — |
| FR-M11-12 | DM-5.3, DEC-003, DEC-104, DEC-111, DEC-112, DEC-009, DEC-195, QA-016, DM-2.1, DG-5 | Nói thẳng | — |
| FR-M11-12.01 | DM-5.3, DEC-003, DEC-104, DEC-240 | Nói thẳng | — |
| FR-M11-12.02 | DEC-104 | Nói thẳng | — |
| FR-M11-12.03 | DEC-104, DEC-240 | Nói thẳng | — |
| FR-M11-12.04 | DEC-104, QA-016, DEC-240 | Nói thẳng | — |
| FR-M11-12.05 | DEC-104, DEC-240 | Nói thẳng | — |
| FR-M11-12.06 | DEC-195, DEC-230, DEC-240 | Nói thẳng | — |
| FR-M11-12.07 | DEC-112, DEC-009, F-GRP-10 | Nói thẳng | — |
| FR-M11-12.08 | DEC-009, DEC-112 | Nói thẳng | — |
| FR-M11-12.09 | DEC-009, DG-5 | Nói thẳng | — |
| FR-M11-12.10 | QA-015, DM-2.1, GL:Anonymous Post | Nói thẳng | — |
| FR-M11-12.11 | DEC-102 | Suy ra | DEC-102 chỉ liệt kê đăng bài là quyền của thành viên ⇒ người ngoài nhóm không đăng được |
| FR-M11-12.12 | DEC-111, DEC-125 | Nói thẳng | — |
| FR-M11-12.13 | DEC-111, DEC-262 | Nói thẳng | — |
| FR-M11-12.14 | DEC-230, DEC-240 | Nói thẳng | — |
| FR-M11-12.15 | DEC-230, DEC-240 | Nói thẳng | — |
| FR-M11-12.16 | DEC-240 | Nói thẳng | — |
| FR-M11-12.17 | DEC-240 | Nói thẳng | — |
| FR-M11-12.18 | DEC-240 | Nói thẳng | — |
| FR-M11-12.19 | DEC-240 | Nói thẳng | — |
| FR-M11-12.20 | DEC-240 | Nói thẳng | — |
| FR-M11-13 | DEC-104, DEC-102, QA-016, DEC-109, F-GRP-04 | Nói thẳng | — |
| FR-M11-13.01 | DEC-104 | Nói thẳng | — |
| FR-M11-13.02 | DEC-104 | Nói thẳng | — |
| FR-M11-13.03 | DEC-104 | Suy ra | Cơ chế nhận việc (claim-based) ⇒ chỉ người đang giữ xử lý được |
| FR-M11-13.04 | DEC-104, DEC-190 | Suy ra | "30-min timeout" cùng cơ chế hàng chờ báo cáo ⇒ 30 phút tính từ thao tác cuối như DEC-190 |
| FR-M11-13.05 | DEC-104, QA-016 | Nói thẳng | — |
| FR-M11-13.06 | DEC-104, DEC-237 | Nói thẳng | — |
| FR-M11-13.07 | DEC-109 | Nói thẳng | — |
| FR-M11-13.08 | DEC-102 | Nói thẳng | — |
| FR-M11-13.09 | DEC-233 | Nói thẳng | — |
| FR-M11-13.10 | DEC-237 | Nói thẳng | — |
| FR-M11-13.11 | DEC-237 | Nói thẳng | — |
| FR-M11-13.12 | DEC-237 | Nói thẳng | — |
| FR-M11-13.13 | DEC-237, DEC-240 | Nói thẳng | — |
| FR-M11-13.14 | DEC-271, DEC-237, DEC-104, DEC-240 | Nói thẳng | — |
| FR-M11-14 | DEC-102, DEC-109 | Nói thẳng | — |
| FR-M11-14.01 | DEC-102, DEC-231, DEC-270 | Nói thẳng | — |
| FR-M11-14.02 | DEC-102 | Nói thẳng | — |
| FR-M11-14.03 | DEC-109, DEC-115 | Nói thẳng | — |
| FR-M11-14.04 | DEC-104, QA-016 | Nói thẳng | — |
| FR-M11-14.05 | DEC-231 | Nói thẳng | — |
| FR-M11-14.06 | DEC-231 | Nói thẳng | — |
| FR-M11-14.07 | DEC-231 | Nói thẳng | — |
| FR-M11-14.08 | DEC-231 | Nói thẳng | — |
| FR-M11-15 | DEC-102, DEC-105, DEC-113, DEC-107, F-GRP-01 | Nói thẳng | — |
| FR-M11-15.01 | DEC-105, DEC-113, DEC-102 | Nói thẳng | — |
| FR-M11-15.02 | DEC-105, DEC-113, DEC-239 | Nói thẳng | — |
| FR-M11-15.03 | DEC-113 | Nói thẳng | — |
| FR-M11-15.04 | DEC-102 | Nói thẳng | — |
| FR-M11-15.05 | DEC-105, DEC-113 | Suy ra | Nhóm Đã xóa không hiện với ai ⇒ không thao tác được trên nhóm |
| FR-M11-16 | DEC-194 | Nói thẳng | Thao tác Ẩn, Khóa thuộc M08; M11 áp dụng cách hiển thị và chặn thao tác |
| FR-M11-16.01 | DEC-194 | Nói thẳng | — |
| FR-M11-16.02 | DEC-194 | Nói thẳng | — |
| FR-M11-16.03 | DEC-194 | Nói thẳng | — |
| FR-M11-16.04 | DEC-194 | Nói thẳng | — |
| FR-M11-16.05 | DEC-194 | Nói thẳng | — |
| FR-M11-16.06 | DEC-194 | Nói thẳng | — |
| FR-M11-16.07 | DEC-235 | Nói thẳng | — |
| FR-M11-16.08 | DEC-235 | Nói thẳng | — |
| FR-M11-16.09 | DEC-235 | Nói thẳng | — |
| FR-M11-16.10 | DEC-235 | Nói thẳng | — |
| FR-M11-17 | DEC-225 | Nói thẳng | DEC-225 giao danh sách chặn và việc vẫn chạy cho FR-M11 |
| FR-M11-17.01 | DEC-225 | Nói thẳng | — |
| FR-M11-17.02 | DEC-225 | Nói thẳng | — |
| FR-M11-17.03 | DEC-225 | Nói thẳng | — |
| FR-M11-17.04 | DEC-225 | Nói thẳng | — |
| FR-M11-17.05 | DEC-225 | Nói thẳng | — |
| FR-M11-17.06 | DEC-225 | Nói thẳng | — |
| FR-M11-17.07 | DEC-236, DEC-261 | Nói thẳng | — |
| FR-M11-17.08 | DEC-236 | Nói thẳng | — |
| BR-M11-01 | DEC-003, DM-5, DM-5.3, DM-5.4, DG-5 | Nói thẳng | — |
| BR-M11-02 | DM-5.4, DG-5, QA-038, DM-9.4 | Nói thẳng | — |
| BR-M11-03 | DEC-101, DEC-106, DEC-237 | Nói thẳng | — |
| BR-M11-04 | DM-5.1, DEC-107 | Suy ra | Draft "Người tạo / owner" ⇒ người tạo là Owner; DEC-107 luôn chọn đúng một người kế nhiệm ⇒ mỗi nhóm đúng một Owner |
| BR-M11-05 | DEC-102, QA-016, GL:GroupMember, DEC-231 | Nói thẳng | — |
| BR-M11-06 | DEC-102, DEC-103, DEC-110 | Nói thẳng | — |
| BR-M11-07 | DEC-103, QA-044, QA-045 | Nói thẳng | — |
| BR-M11-08 | QA-045, DEC-103, F-GRP-09, DEC-237 | Nói thẳng | — |
| BR-M11-09 | DEC-103, DEC-237 | Nói thẳng | — |
| BR-M11-10 | DEC-103, DEC-238 | Nói thẳng | — |
| BR-M11-11 | DEC-110, DEC-210, QA-011 | Nói thẳng | — |
| BR-M11-12 | DEC-110, DEC-229, DEC-238 | Nói thẳng | — |
| BR-M11-13 | QA-011, DM-5.3, DEC-062, DEC-175, DEC-234 | Nói thẳng | — |
| BR-M11-14 | DEC-111, DEC-125, DEC-258, DEC-262 | Nói thẳng | — |
| BR-M11-15 | DEC-108, DEC-234 | Nói thẳng | — |
| BR-M11-16 | DEC-009, DEC-112, F-GRP-10, DG-5 | Nói thẳng | — |
| BR-M11-17 | QA-015, DEC-112, GL:Anonymous Post, DM-2.1 | Nói thẳng | — |
| BR-M11-18 | DEC-104, QA-016, DEC-230, DEC-237, DEC-240 | Nói thẳng | — |
| BR-M11-19 | DEC-195, DEC-230, DEC-240 | Nói thẳng | — |
| BR-M11-20 | DEC-104, DEC-190 | Suy ra | DEC-104 "claim-based 30-min timeout" cùng cơ chế hàng chờ báo cáo ⇒ 30 phút tính từ thao tác cuối như DEC-190 |
| BR-M11-21 | DEC-109, DEC-115, DEC-237 | Nói thẳng | — |
| BR-M11-22 | DEC-104, QA-016 | Nói thẳng | — |
| BR-M11-23 | DEC-105, DEC-113, DEC-239 | Nói thẳng | — |
| BR-M11-24 | DEC-105, DEC-113, DEC-112, DEC-237 | Suy ra | DEC-105 "author shown with real name"; bài ẩn danh vẫn ẩn danh vì DEC-112 không cho lộ tác giả bài ẩn danh cũ |
| BR-M11-25 | DEC-107 | Nói thẳng | — |
| BR-M11-26 | DEC-107, DEC-225, DEC-232, DEC-235, DEC-237 | Nói thẳng | — |
| BR-M11-27 | DEC-194 | Nói thẳng | — |
| BR-M11-28 | DEC-194, DEC-235 | Nói thẳng | — |
| BR-M11-29 | DEC-225, DEC-236, DEC-261 | Nói thẳng | — |
| BR-M11-30 | DEC-102, DEC-231 | Nói thẳng | — |
| BR-M11-31 | DEC-237 | Nói thẳng | — |
| BR-M11-32 | DEC-237 | Nói thẳng | — |
| BR-M11-33 | DEC-233, DEC-210, DEC-240 | Nói thẳng | — |
| BR-M11-34 | DEC-238 | Nói thẳng | — |
| BR-M11-35 | DEC-237, QA-230 | Nói thẳng | — |
| BR-M11-36 | DEC-238 | Nói thẳng | — |
| BR-M11-37 | DEC-065, DEC-231, DEC-237, DEC-238 | Nói thẳng | — |
| BR-M11-38 | DEC-237, DEC-271 | Nói thẳng | — |
| BR-M11-39 | DEC-237, DEC-240 | Nói thẳng | — |
| BR-M11-40 | DEC-240 | Nói thẳng | — |

## Phụ lục B. Câu hỏi, giả định và TBD

### B.1 Câu hỏi đã hỏi

| Mã | Loại | Câu hỏi | Trả lời | Ghi vào register |
|---|---|---|---|---|
| Q-01 | Mâu thuẫn | Người dùng mở link mời (hoặc được thành viên mời) vào nhóm thì vào thẳng, hay vẫn đi theo ma trận tham gia (nhóm Private, nhóm có câu hỏi → chờ Owner/Group Mod duyệt)? QA-044, F-GRP-07 nói link mời vào thẳng; DEC-110 (QA-188) nói mời "dùng lại luồng tham gia DEC-103". | B: lời mời chỉ đưa tới nhóm, người được mời theo ma trận tham gia; Private hoặc có câu hỏi thì chờ duyệt. | QA-421, DEC-229 |
| Q-02 | Thiếu chi tiết | Group Mod có sửa được tên, mô tả nhóm không? DEC-102 chỉ nói "đổi setting group (public/private, pre-mod, anonymous, join question)" là quyền riêng của Owner, không nhắc tên, mô tả. | Không, chỉ Owner sửa (L3). | QA-430, DEC-237 |
| Q-03 | Thiếu chi tiết | Mod, Admin hệ thống không là thành viên có thấy và xem được nhóm Private không? QA-016 "System MODERATOR và ADMIN vẫn có quyền can thiệp vào content trong group bất kỳ lúc nào"; DEC-110 nhóm Private chỉ vào qua lời mời. | A: chỉ xem nội dung nhóm Private trong vụ báo cáo mình đang giữ. | QA-425, DEC-233 |
| Q-04 | Thiếu chi tiết | Người ngoài nhóm có bình luận, vote bài của nhóm Public không? DEC-111 bài nhóm Public hiện ở feed chính "like an ordinary post"; DEC-108 chỉ nói bài thành không tương tác được khi nhóm chuyển Private. | A: có, như bài thường (bình luận, vote, báo cáo, bookmark). | QA-426, DEC-234 |
| Q-05 | Thiếu chi tiết | Hàng chờ "chờ duyệt đăng" của System Mod (DEC-104) có gồm bài của nhóm không, tức Mod, Admin hệ thống có duyệt bài chờ đăng của nhóm không? | A: không; hàng chờ của nhóm chỉ Owner, Group Mod duyệt. | QA-425, DEC-233 |
| Q-06 | Mơ hồ | "5 nhóm mỗi ngày mỗi người" (DEC-101) tính theo ngày lịch giờ Việt Nam hay 24 giờ trượt; nhóm đã xóa có được tính; Admin có bị giới hạn không? | 24 giờ gần nhất; nhóm đã xóa vẫn tính; Admin cũng bị giới hạn (L1). | QA-430, DEC-237 |
| Q-07 | Thiếu chi tiết | Nhóm có câu hỏi tham gia thì người gửi yêu cầu có bắt buộc trả lời không (QA-045 ghi câu trả lời có thể để trống)? | Bắt buộc trả lời (L7). | QA-430, DEC-237 |
| Q-08 | Thiếu chi tiết | Link mời (QA-044, DEC-110) là một link chung của nhóm hay mỗi thành viên một link; có hết hạn, thu hồi được không? | Không mở rộng: một link chung, không hết hạn, không thu hồi (S3). | QA-431, DEC-238 |
| Q-09 | Mơ hồ | DEC-108 "Posts already delivered to a given user's feed remain visible": "đã hiện" là bài đang mở trên màn hình lúc đổi chế độ, hay mọi bài từng xuất hiện với người đó? | A: chỉ bài đang hiện sẵn trên màn hình đã tải; tải lại, mở lại thì "Nội dung không tồn tại". | QA-426, DEC-234 |
| Q-10 | Thiếu chi tiết | Yêu cầu tham gia đang Chờ duyệt xử lý sao khi Owner đổi cài đặt làm nhóm thành "vào ngay" (Private → Public không câu hỏi, hoặc bỏ câu hỏi của nhóm Public)? | Duyệt luôn các yêu cầu đang chờ (L4, sửa so với đề xuất). | QA-430, DEC-237 |
| Q-11 | Thiếu chi tiết | Bài gửi vào nhóm không có điểm quét (công tắc AI tổng hoặc Moderation tắt; quét thất bại; tác giả là Admin — DEC-195) đi theo nhánh nào của cổng duyệt DEC-104? | C: AI tắt hoặc tác giả Admin theo công tắc duyệt trước; quét thất bại thì bắt buộc chờ nhóm duyệt. | QA-422, DEC-230 |
| Q-12 | Thiếu chi tiết | Kế nhiệm bắt buộc (DEC-107 "ban/deactivate/delete"): ban tạm thời và tự vô hiệu hóa (kích hoạt lại được) có kích hoạt chuyển Owner không; Owner cũ quay lại mang vai trò gì? | A: mọi ban, vô hiệu hóa, xóa đều chuyển ngay; Owner cũ ở lại làm Member. | QA-424, DEC-232 |
| Q-13 | Thiếu chi tiết | Trong nhóm Bị khóa (DEC-194 chỉ liệt kê đăng, bình luận, vote, bình chọn, tham gia, mời), các thao tác quản trị (duyệt bài chờ, duyệt yêu cầu, kick, bổ nhiệm, đổi cài đặt, rời, xóa nhóm) còn làm được không? | Chặn hết thao tác quản trị, kể cả xóa nhóm, Owner rời; Member, Group Mod tự rời được; hệ thống vẫn chuyển Owner. | QA-427, QA-428, DEC-235 |
| Q-14 | Thiếu chi tiết | Khi cờ Group tắt (DEC-225 giao danh sách cho FR-M11), bài nhóm ở feed chính, tab Group, hồ sơ, tìm kiếm, bookmark và nhóm trong tìm kiếm còn hiện không? | A: lối vào vẫn hiện, mở ra hoặc tương tác thì "Hệ thống đang bận". | QA-429, DEC-236 |
| Q-15 | Mơ hồ | "Ẩn/xóa post-comment trong group" (DEC-102) là một hay hai thao tác; bài, bình luận chuyển sang trạng thái nào; tác giả có được báo, có bị trừ điểm (DEC-113) không? | A: một thao tác gỡ khỏi nhóm, xóa mềm, có thông báo, không trừ điểm, theo thứ bậc. | QA-423, DEC-231 |
| Q-16 | Cần cân nhắc | Mở rộng phạm vi: Ai xem được danh sách thành viên của nhóm? | Có: ai xem được trang nhóm thì xem được danh sách thành viên (S1). | QA-431, DEC-238 |
| Q-17 | Cần cân nhắc | Mở rộng phạm vi: Người gửi có rút được yêu cầu tham gia đang chờ không; Owner, Group Mod có xem danh sách và bỏ chặn được không; người bị chặn có vào được bằng link mời không? | Không gửi thêm khi đang có yêu cầu chờ (L8); có rút yêu cầu, xem danh sách chặn, bỏ chặn; chặn áp mọi cách vào (S2). | QA-430, QA-431, DEC-237, DEC-238 |
| Q-18 | Thiếu chi tiết | Bài bị Owner, Group Mod từ chối có kèm lý do, tác giả có sửa và gửi lại được không; bài nhóm bị AI tự từ chối có khiếu nại qua M09 như bài thường không? | Từ chối bắt buộc lý do; tác giả sửa, gửi lại được; bài bị AI từ chối khiếu nại qua M09 (L11). | QA-430, DEC-237 |
| Q-19 | Thiếu chi tiết | Thâm niên Group Mod (DEC-107) của người từng bị giáng rồi được bổ nhiệm lại tính từ lần bổ nhiệm nào? | Từ lần bổ nhiệm gần nhất (L10). | QA-430, DEC-237 |
| Q-20 | Thiếu chi tiết | Người đã rời hoặc bị kick còn sửa, xóa được bài, bình luận của mình trong nhóm không, nhất là nhóm Private họ không còn xem được? | Nhóm Public: được; nhóm Private: không (L13). | QA-430, DEC-237 |
| Q-21 | Thiếu chi tiết | Tên, mô tả nhóm có bắt buộc, giới hạn độ dài, tên có được trùng không; công tắc duyệt trước, công tắc ẩn danh, câu hỏi tham gia đặt được ngay khi tạo không, mặc định là gì? | Tên bắt buộc ≤ 100 ký tự, mô tả ≤ 500, tên được trùng, chọn chế độ khi tạo, hai công tắc mặc định Tắt, câu hỏi trống, đặt được ngay khi tạo (L2). | QA-430, DEC-237 |
| Q-22 | Thiếu chi tiết | Bài đang chờ nhóm duyệt chỉ vì công tắc duyệt trước (điểm < 0.5) xử lý sao khi Owner tắt công tắc: tự đăng hay vẫn chờ duyệt? | Bài đang chờ vẫn chờ (L5). | QA-430, DEC-237 |
| Q-23 | Thiếu chi tiết | Danh sách nhóm (QA-011 Guest "xem danh sách"; QA-230 "trang danh sách/tìm Group") là trang riêng hay chính là tìm Group của M06; sắp xếp theo gì; mỗi nhóm hiện gì? | Trang riêng: nhóm Private của mình và nhóm Public, mới nhất trước (L6). | QA-430, DEC-237 |
| Q-24 | Thiếu chi tiết | Sự kiện "join" của nhóm (DEC-065) gửi cho ai; từ chối yêu cầu, giáng Group Mod, chuyển Owner có sinh thông báo không? | Yêu cầu mới → Owner, Group Mod; không thông báo khi vào ngay, bị từ chối, bị giáng; trở thành Owner có thông báo (L9). | QA-430, DEC-237 |
| Q-25 | Thiếu chi tiết | Owner, Group Mod có tự chấp nhận bài chờ duyệt của chính mình không? | Group Mod không tự duyệt (L12); bài của Owner không qua duyệt của nhóm, điểm 0.5–< 0.9 hoặc quét lỗi vào hàng chờ Mod hệ thống (sửa ở bước 7). | QA-430, QA-433, DEC-237, DEC-240 |

### B.2 TBD

| ID | Nội dung | Ảnh hưởng | Lý do chưa chốt |
|---|---|---|---|
| TBD-M11-01 | (Đã đóng ở phiên bản 0.1 — DEC-239: mọi cách nội dung nhóm mất đi trong M11 đều là xóa mềm) | Thấp | Đã chốt; phần M16 của OPEN-011 vẫn mở |

### B.3 Cần cân nhắc (ngoài dữ liệu hiện có)

| Mã | Điểm cần cân nhắc | Vì sao cần | Quyết định |
|---|---|---|---|
| Q-16 | Mở rộng phạm vi: cho người xem trang nhóm xem danh sách thành viên | Nguồn chỉ cần Owner thấy thành viên để bổ nhiệm, kick, chỉ định người kế nhiệm | Có (DEC-238) |
| Q-17 | Mở rộng phạm vi: rút yêu cầu tham gia; xem danh sách chặn, bỏ chặn | Không có thì người bị chặn bị chặn vĩnh viễn, yêu cầu gửi nhầm không rút được | Có (DEC-238) |
| Q-08 | Mở rộng phạm vi: thu hồi, tạo lại link mời | Lộ link chỉ lộ tên, mô tả nhóm vì người được mời vẫn phải được duyệt (DEC-229) | Không làm (DEC-238) |

## Phụ lục C. Sổ nguồn

**Owner keywords:** M11, F-GRP, Group, Groups, group, groups, nhóm, GroupMember, group member, group members, thành viên nhóm, Group Mod, Group Moderator, Group Owner, Owner, chủ nhóm, quản trị nhóm, join question, câu hỏi tham gia, invite link, link mời, lời mời, invite, join request, yêu cầu tham gia, join, tham gia nhóm, rời nhóm, kick, pre-mod, pre-moderation, duyệt trước, visible-but-gated, Public group, Private group, nhóm Public, nhóm Private, successor, kế nhiệm, group_id, anonymous posting, đăng ẩn danh, anonymous post, is_anonymous, ẩn danh
**Dependency keywords:** post, bài viết, comment, bình luận, star, upvote, report, báo cáo, moderation, kiểm duyệt, AI scan, appeal, khiếu nại, notification, thông báo, feed, search, tìm kiếm, anonymous, ẩn danh, points, điểm, reputation, ban, BANNED, deactivate, feature flag, AI_ENABLED, AI off, audit log, timezone, Group Chat, chat, ADMIN, MOD, rate limit
**Mục draft của module:** DM-5 (gồm DM-5.1–5.4)
**Loại khỏi bảng nguồn (khớp nhầm):** DEC-023, DEC-024, DEC-170, QA-068, MR-M02 ("owner" là chủ hồ sơ, M02); DEC-036, QA-081 ("owner" của bình chọn, M03); DEC-139 ("owner module" của tài liệu); DEC-147, QA-018, DEC-220 ("owner" là chủ tài khoản, chủ nội dung); DEC-154 ("groups" là nhóm dữ liệu cá nhân); DEC-076, ISS-183, QA-246 ("group by" của vụ báo cáo và truy vấn thống kê); DEC-098, DEC-186, ISS-332, QA-392, QA-361, QA-366, QA-328 ("nhóm vi phạm" của AI); QA-292, QA-298, QA-299, QA-302, QA-303, QA-304, QA-306, QA-307, QA-309, QA-364, QA-365, QA-367, QA-411 ("ok cả nhóm", nhóm bảo mật, nhóm dữ liệu); ISS-203, QA-263 ("nhóm công nghệ"); DM-9.2 (nhóm huy hiệu); QA-004 (group Facebook là bối cảnh cạnh tranh); DEC-067, DEC-070, DEC-219, ISS-155, QA-209, QA-211, ISS-159, ISS-160, QA-218, DM-6, DM-6.1 (Group chat, M16)

### C.1 Bảng nguồn

| Nguồn | Nhãn | Trạng thái | Dùng ở | Ghi chú |
|---|---|---|---|---|
| DEC-101 | Sở hữu | Sửa một phần bởi DEC-237 | FR-M11-01, FR-M11-01.01, FR-M11-01.03, FR-M11-01.04, FR-M11-01.05, BR-M11-03 | Nhóm A. Tạo nhóm: mọi người đã đăng nhập, tối đa 5 nhóm/ngày/người, không giới hạn tổng|
| DEC-102 | Sở hữu | Sửa một phần bởi DEC-231, DEC-237 | FR-M11-02, FR-M11-02.01, FR-M11-02.05, FR-M11-02.09, FR-M11-02.10, FR-M11-03.08, FR-M11-06, FR-M11-06.02, FR-M11-06.05, FR-M11-08, FR-M11-08.01, FR-M11-08.02, FR-M11-08.04, FR-M11-08.05, FR-M11-09, FR-M11-09.01, FR-M11-09.02, FR-M11-09.03, FR-M11-09.04, FR-M11-12.11, FR-M11-13, FR-M11-13.08, FR-M11-14, FR-M11-14.01, FR-M11-14.02, FR-M11-15, FR-M11-15.01, FR-M11-15.04, BR-M11-05, BR-M11-06, BR-M11-30 | Nhóm A. Ma trận quyền Owner / Group Mod / Member; không vai trò nào tác động lên người ngang hoặc cao hơn|
| DEC-103 | Sở hữu | Sửa một phần bởi DEC-237, DEC-238 | FR-M11-02.07, FR-M11-04, FR-M11-04.01, FR-M11-04.02, FR-M11-04.03, FR-M11-04.04, FR-M11-04.06, FR-M11-06, FR-M11-06.01, FR-M11-06.02, FR-M11-06.03, FR-M11-06.06, FR-M11-07, FR-M11-07.01, FR-M11-07.02, BR-M11-06, BR-M11-07, BR-M11-08, BR-M11-09, BR-M11-10 | Nhóm A. Ma trận tham gia Public/Private × có/không câu hỏi; bị từ chối gửi lại ngay; Owner/Mod chặn người gửi yêu cầu|
| DEC-104 | Sở hữu | Sửa một phần bởi DEC-195, DEC-230, DEC-233, DEC-240 | FR-M11-02.05, FR-M11-12, FR-M11-12.01, FR-M11-12.02, FR-M11-12.03, FR-M11-12.04, FR-M11-12.05, FR-M11-13, FR-M11-13.01, FR-M11-13.02, FR-M11-13.03, FR-M11-13.04, FR-M11-13.05, FR-M11-13.06, FR-M11-14.04, BR-M11-18, BR-M11-20, BR-M11-22 | Nhóm A. Cổng đăng bài của nhóm chồng lên kiểm duyệt hệ thống (M08); ngưỡng 0.9/0.5; hàng chờ duyệt của nhóm và của System Mod, giữ 30 phút. DEC-195: bài của ADMIN trong nhóm không bị AI quét nhưng vẫn qua cổng duyệt của nhóm|
| DEC-105 | Sở hữu | Sửa một phần bởi DEC-113 | FR-M11-09, FR-M11-09.05, FR-M11-09.07, FR-M11-10, FR-M11-10.01, FR-M11-10.02, FR-M11-11.03, FR-M11-15, FR-M11-15.01, FR-M11-15.02, FR-M11-15.05, BR-M11-23, BR-M11-24 | Nhóm A. Xóa nhóm là xóa mềm; rời hoặc bị kick thì bài giữ nguyên, hiện tên thật. Phần trừ điểm khi xóa nhóm đã bị DEC-113 bỏ. DEC-113 bỏ ngoại lệ trừ điểm khi nhóm bị xóa|
| DEC-106 | Sở hữu | Hiện hành | FR-M11-01, FR-M11-01.05, FR-M11-04.07, BR-M11-03 | Nhóm A. Không giới hạn số nhóm tham gia, sở hữu|
| DEC-107 | Sở hữu | Sửa một phần bởi DEC-232, DEC-237 | FR-M11-01.02, FR-M11-08.01, FR-M11-08.05, FR-M11-10, FR-M11-10.01, FR-M11-10.03, FR-M11-10.04, FR-M11-10.05, FR-M11-10.06, FR-M11-11, FR-M11-11.01, FR-M11-11.02, FR-M11-11.03, FR-M11-15, BR-M11-04, BR-M11-25, BR-M11-26 | Nhóm A. Kế nhiệm Owner: tự rời phải chỉ định; mất quyền bắt buộc thì tự chuyển theo thâm niên; còn một mình thì xóa nhóm|
| DEC-108 | Sở hữu | Sửa một phần bởi DEC-234 | FR-M11-02, FR-M11-02.02, FR-M11-02.03, FR-M11-02.04, FR-M11-02.12, FR-M11-03, FR-M11-03.07, BR-M11-15 | Nhóm A. Đổi Public↔Private bất kỳ lúc nào; bài đã hiện giữ hiện nhưng khóa tương tác khi sang Private|
| DEC-109 | Sở hữu | Sửa một phần bởi DEC-237 | FR-M11-13, FR-M11-13.07, FR-M11-14, FR-M11-14.03, BR-M11-21 | Nhóm A. Quyết định kiểm duyệt cấp nhóm không có khiếu nại|
| DEC-110 | Sở hữu | Sửa một phần bởi DEC-210, DEC-229, DEC-238 | FR-M11-03, FR-M11-03.02, FR-M11-05, FR-M11-05.01, FR-M11-05.03, FR-M11-05.04, BR-M11-06, BR-M11-11, BR-M11-12 | Nhóm A. Nhóm Private ẩn khỏi tìm kiếm, khám phá; vào qua lời mời/link; mọi thành viên mời được; không có thực thể lời mời riêng. DEC-210 làm rõ: thành viên vẫn tìm thấy. DEC-210 làm rõ: thành viên vẫn tìm thấy nhóm Private của mình. Câu "dùng lại luồng DEC-103" mâu thuẫn với link mời vào thẳng (QA-044, F-GRP-07) — Q-01|
| DEC-111 | Sở hữu | Sửa một phần bởi DEC-125, DEC-234, DEC-258, DEC-262 | FR-M11-03, FR-M11-03.05, FR-M11-12, FR-M11-12.12, FR-M11-12.13, BR-M11-14 | Nhóm A. Bài nhóm luôn hiện ở feed của thành viên; nhóm Public thêm hiện ở feed chính; nhóm Private không bao giờ. Không dấu sửa: DEC-125 (nguồn QA-233) cho bài nhóm Public vào Trending và tab Group, không vào Newest |
| DEC-112 | Sở hữu | Hiện hành | FR-M11-02, FR-M11-02.06, FR-M11-03, FR-M11-03.09, FR-M11-03.10, FR-M11-12, FR-M11-12.07, FR-M11-12.08, BR-M11-16, BR-M11-17, BR-M11-24 | Nhóm A. Ẩn danh trong nhóm: chọn từng bài khi công tắc bật; tắt không lộ bài cũ; Group Mod/Owner thấy danh tính thật. Ghi "giống DEC-004/005" nhưng mẫu MOD/ADMIN thấy danh tính thật là QA-015|
| DM-5 | Sở hữu | Hiện hành | BR-M11-01 | Nhóm A. Draft: nhóm dạng cộng đồng, tái dùng cơ chế Forum|
| DM-5.1 | Sở hữu | Sửa một phần bởi DEC-103, DEC-110 | FR-M11-01, FR-M11-01.01, FR-M11-01.02, FR-M11-02, FR-M11-03.04, BR-M11-04 | Nhóm A. Draft: tên, mô tả, public/private, người tạo/owner. Không dấu sửa: nhóm Public có câu hỏi cũng cần duyệt; nhóm Private vào qua lời mời/link|
| DM-5.2 | Sở hữu | Sửa một phần bởi QA-016, DEC-103 | FR-M11-04 | Nhóm A. Draft: thành viên và vai trò (owner/member); tham gia tự do hoặc duyệt/mời. Vai trò đã thành ba cấp (QA-016). Không dấu sửa: ba vai trò thay cho owner/member; nhóm Public có câu hỏi cũng cần duyệt|
| DM-5.3 | Sở hữu | Sửa một phần bởi DEC-104 | FR-M11-03, FR-M11-03.06, FR-M11-03.07, FR-M11-12, FR-M11-12.01, BR-M11-01, BR-M11-13 | Nhóm A. Draft: bài trong nhóm dùng chung bài viết; bình luận, star, báo cáo, kiểm duyệt, AI, thông báo dùng chung, lọc thêm theo quyền xem. Không dấu sửa: thêm cổng duyệt đăng bài riêng của nhóm, chồng lên kiểm duyệt chung|
| DM-5.4 | Sở hữu | Hiện hành | BR-M11-01, BR-M11-02 | Nhóm A. Draft: quan hệ Group–GroupMember–Post; không có leaderboard, reputation riêng theo nhóm|
| ISS-130 | Sở hữu | Trùng với DEC-101 | — | Nhóm A. Tạo nhóm|
| ISS-131 | Sở hữu | Trùng với DEC-102 | — | Nhóm A. Ma trận quyền|
| ISS-132 | Sở hữu | Trùng với DEC-103 | — | Nhóm A. Luồng tham gia|
| ISS-133 | Sở hữu | Trùng với DEC-104 | — | Nhóm A. Kiểm duyệt nhóm và M08|
| ISS-134 | Sở hữu | Trùng với DEC-105 | — | Nhóm A. Xóa nhóm, rời nhóm. Phần trừ điểm khi xóa nhóm đã bị DEC-113 bỏ|
| ISS-135 | Sở hữu | Trùng với DEC-112 | — | Nhóm A. Ẩn danh trong nhóm|
| ISS-136 | Sở hữu | Trùng với DEC-106 | — | Nhóm A. Không giới hạn số nhóm|
| ISS-137 | Sở hữu | Trùng với DEC-107 | — | Nhóm A. Kế nhiệm Owner|
| ISS-138 | Sở hữu | Trùng với DEC-108 | — | Nhóm A. Đổi Public↔Private|
| ISS-139 | Sở hữu | Trùng với DEC-109 | — | Nhóm A. Không khiếu nại cấp nhóm|
| ISS-140 | Sở hữu | Trùng với DEC-110 | — | Nhóm A. Nhóm Private, ai được mời|
| ISS-141 | Sở hữu | Trùng với DEC-111 | — | Nhóm A. Bài nhóm ra feed chính|
| QA-179 | Sở hữu | Trùng với DEC-101 | — | Nhóm A. Tạo nhóm|
| QA-180 | Sở hữu | Trùng với DEC-102 | — | Nhóm A. Ma trận quyền|
| QA-181 | Sở hữu | Trùng với DEC-103 | — | Nhóm A. Luồng tham gia|
| QA-182 | Sở hữu | Trùng với DEC-104 | — | Nhóm A. Kiểm duyệt nhóm và M08|
| QA-183 | Sở hữu | Trùng với DEC-105 | — | Nhóm A. Xóa nhóm, rời nhóm (phần trừ điểm đã bị thay). Phần trừ điểm khi xóa nhóm đã bị DEC-113 bỏ|
| QA-184 | Sở hữu | Trùng với DEC-106 | — | Nhóm A. Không giới hạn số nhóm|
| QA-185 | Sở hữu | Trùng với DEC-107 | — | Nhóm A. Kế nhiệm Owner|
| QA-186 | Sở hữu | Trùng với DEC-108 | — | Nhóm A. Đổi Public↔Private|
| QA-187 | Sở hữu | Trùng với DEC-109 | — | Nhóm A. Không khiếu nại cấp nhóm|
| QA-188 | Sở hữu | Trùng với DEC-110 | — | Nhóm A. Nhóm Private, ai được mời|
| QA-189 | Sở hữu | Trùng với DEC-111 | — | Nhóm A. Bài nhóm ra feed chính|
| QA-190 | Sở hữu | Trùng với DEC-112 | — | Nhóm A. Ẩn danh trong nhóm|
| MR-M11 | Sở hữu | Sửa một phần bởi DEC-110, DEC-210, DEC-229, DEC-238 | FR-M11-01 | Nhóm A. Dòng module M11: Should; Public/Private, vai trò, duyệt trước, ẩn danh, câu hỏi tham gia; Group Chat không thuộc M11. Visible-but-gated của nhóm Private không còn áp dụng|
| DEC-003 | Sở hữu | Hiện hành | FR-M11-12, FR-M11-12.01, BR-M11-01 | Nhóm B. Ngoài section. Nhóm tái dùng cơ chế Forum, bài nhóm dùng chung bài viết|
| DEC-009 | Sở hữu | Sửa một phần bởi DEC-112 | FR-M11-02, FR-M11-02.06, FR-M11-12, FR-M11-12.07, FR-M11-12.08, FR-M11-12.09, BR-M11-16 | Nhóm B. Ngoài section. Công tắc ẩn danh ở cấp nhóm do Owner bật/tắt, chỉ áp cho bài mới; F-GRP-10. DEC-112 làm rõ: khi công tắc bật, thành viên chọn ẩn danh cho từng bài|
| DEC-020 | Phụ thuộc | Sửa một phần bởi DEC-153 | Chuyển M01 | Nhóm B. M01: thứ tự gợi ý @mention ưu tiên cùng nhóm. Tầng ưu tiên cùng nhóm giữ nguyên. DEC-214 (ngoài bảng nguồn) đổi cách khớp tên. Dấu "DEC-209" thực ra là của DEC-214 dẫn lại DEC-209 — DEC-209 không sửa trực tiếp DEC-020|
| DEC-053 | Phụ thuộc | Sửa một phần bởi DEC-209, DEC-210 | Chuyển M06 | Nhóm B. M06: phạm vi tìm Group. Phần nhóm Private visible-but-gated đã bị DEC-210 bỏ|
| DEC-054 | Nhắc tới | Hiện hành | Không áp dụng: chỉ nhắc tới, không quy định hành vi M11 | Nhóm B. M06: cách kích hoạt tìm Group|
| DEC-057 | Nhắc tới | Sửa một phần bởi DEC-209 | Không áp dụng: chỉ nhắc tới, không quy định hành vi M11 | Nhóm B. M06: khớp gần đúng cho Group. DEC-211 (ngoài bảng nguồn) chỉ chạm full-text của bài|
| DEC-058 | Nhắc tới | Sửa một phần bởi DEC-209 | Không áp dụng: chỉ nhắc tới, không quy định hành vi M11 | Nhóm B. M06: gợi ý có Group|
| DEC-060 | Nhắc tới | Hiện hành | Không áp dụng: chỉ nhắc tới, không quy định hành vi M11 | Nhóm B. M06: hiển thị kết quả Group|
| DEC-062 | Phụ thuộc | Sửa một phần bởi DEC-208, DEC-210 | FR-M11-03.06, BR-M11-13 | Nhóm B. M06: nội dung nhóm Private chỉ hiện với thành viên khi tìm kiếm|
| DEC-065 | Phụ thuộc | Sửa một phần bởi DEC-215, DEC-231, DEC-237 | FR-M11-05.02, FR-M11-06.04, FR-M11-06.07, FR-M11-08.03, FR-M11-09.06, BR-M11-37 | Nhóm B. M07: sự kiện thông báo của nhóm: mời, tham gia, duyệt, bổ nhiệm, kick — chỉ trong ứng dụng. Dòng sự kiện nhóm giữ nguyên. DEC-147 (loại), DEC-151, DEC-180, DEC-218, DEC-221 (ngoài bảng nguồn) không chạm sự kiện nhóm|
| DEC-072 | Phụ thuộc | Sửa một phần bởi DEC-194 | Chuyển M08 | Nhóm B. M08: báo cáo nhóm với 4 lý do; chỉ người đã đăng nhập. DEC-191 (ngoài bảng nguồn) không chạm nhóm|
| DEC-081 | Nhắc tới | Sửa một phần bởi DEC-193 | Không áp dụng: chỉ nhắc tới, không quy định hành vi M11 | Nhóm B. M08: nhật ký kiểm duyệt; phần nhóm ở DEC-193. DEC-146, DEC-224 (ngoài bảng nguồn) không chạm nhóm|
| DEC-092 | Phụ thuộc | Sửa một phần bởi DEC-225 | Chuyển M10 | Nhóm B. M10: cờ tính năng cho Group. DEC-152, DEC-226, DEC-228 (ngoài bảng nguồn) không chạm cờ Group|
| DEC-113 | Phụ thuộc | Sửa một phần bởi DEC-231 | FR-M11-09, FR-M11-09.05, FR-M11-09.07, FR-M11-10, FR-M11-10.01, FR-M11-10.02, FR-M11-11.03, FR-M11-15, FR-M11-15.01, FR-M11-15.02, FR-M11-15.03, FR-M11-15.05, BR-M11-23, BR-M11-24 | Nhóm B. M12: xóa nhóm không trừ điểm của thành viên (thay ngoại lệ của DEC-105)|
| DEC-115 | Phụ thuộc | Hiện hành | FR-M11-14.03, BR-M11-21 | Nhóm B. M09: khiếu nại xóa nội dung chỉ cho bài bị MOD/ADMIN gỡ; xác nhận DEC-109 giữ nguyên. DEC-198, DEC-200, DEC-202 (ngoài bảng nguồn) sửa phần khác, không chạm DEC-109|
| DEC-125 | Phụ thuộc | Sửa một phần bởi DEC-215 | FR-M11-12.12, BR-M11-14 | Nhóm B. M14: tab Group gom bài mọi nhóm đã tham gia; bài nhóm Public vào Trending, không vào Newest. Phần tab Group giữ nguyên|
| DEC-126 | Phụ thuộc | Hiện hành | FR-M11-04, FR-M11-04.05 | Nhóm B. M14: Guest thấy tab Group nhưng phải đăng nhập; tham gia nhóm cần đăng nhập|
| DEC-145 | Phụ thuộc | Hiện hành | Chuyển M05 | Nhóm B. M05: Trending tính bài nhóm Public, không tính bài nhóm Private|
| DEC-153 | Phụ thuộc | Hiện hành | Chuyển M01 | Nhóm B. M01: mention trong bình luận của bài nhóm dùng thứ tự theo nhóm|
| DEC-174 | Phụ thuộc | Hiện hành | Chuyển M02 | Nhóm B. M02: bookmark bài nhóm Private khi không còn là thành viên|
| DEC-175 | Phụ thuộc | Hiện hành | BR-M11-13 | Nhóm B. M02: tab Bài viết chỉ hiện bài nhóm Private với thành viên|
| DEC-179 | Phụ thuộc | Hiện hành | TBD-M11-01 | Nhóm B. M04: nội dung báo cáo được chỉ xóa mềm; phần nhóm chuyển OPEN-011|
| DEC-190 | Phụ thuộc | Hiện hành | FR-M11-13.04, BR-M11-20 | Nhóm B. M08: mức nặng lý do báo cáo nhóm; mở khóa nhóm không cần vụ|
| DEC-192 | Phụ thuộc | Sửa một phần bởi DEC-197 | Chuyển M08 | Nhóm B. M08: thông báo kết quả khi nhóm bị Ẩn/Khóa không kèm link khiếu nại. Phần nhóm giữ nguyên|
| DEC-193 | Phụ thuộc | Hiện hành | Chuyển M08 | Nhóm B. M08: nhật ký kiểm duyệt ghi ẩn, khóa, mở khóa nhóm|
| DEC-194 | Sở hữu | Sửa một phần bởi DEC-235 | FR-M11-01.01, FR-M11-16, FR-M11-16.01, FR-M11-16.02, FR-M11-16.03, FR-M11-16.04, FR-M11-16.05, FR-M11-16.06, BR-M11-27, BR-M11-28 | Nhóm B. Ngoài section (M08). Phần M11 áp dụng: nhóm bị Ẩn không ai thấy; nhóm bị Khóa chặn đăng, bình luận, vote, tham gia, mời. Thao tác Ẩn/Khóa là của M08|
| DEC-195 | Sở hữu | Sửa một phần bởi DEC-240 | FR-M11-12, FR-M11-12.06, BR-M11-19 | Nhóm B. Ngoài section (M09). Phần M11: bài của ADMIN trong nhóm vẫn qua cổng duyệt của nhóm; nhóm do ADMIN làm Owner không báo cáo được|
| DEC-197 | Phụ thuộc | Hiện hành | Chuyển M09 | Nhóm B. M09: không có link khiếu nại cho nhóm bị Ẩn/Khóa|
| DEC-208 | Nhắc tới | Hiện hành | Không áp dụng: chỉ nhắc tới, không quy định hành vi M11 | Nhóm B. M06: Guest tìm Group như USER|
| DEC-209 | Phụ thuộc | Hiện hành | Chuyển M06 | Nhóm B. M06: Group khớp theo tên, không theo mô tả|
| DEC-210 | Phụ thuộc | Hiện hành | FR-M11-03.03, FR-M11-03.11, BR-M11-11, BR-M11-33 | Nhóm B. M06: nhóm Private không hiện khi người ngoài nhóm tìm; thành viên vẫn tìm thấy|
| DEC-212 | Nhắc tới | Sửa một phần bởi DEC-215 | Không áp dụng: chỉ nhắc tới, không quy định hành vi M11 | Nhóm B. M06: bộ lọc không áp cho kết quả Group|
| DEC-215 | Phụ thuộc | Hiện hành | Chuyển M07 | Nhóm B. M07: không theo dõi được nhóm; thông báo bài mới không gửi cho người không xem được bài nhóm Private|
| DEC-225 | Sở hữu | Sửa một phần bởi DEC-236 | FR-M11-11, FR-M11-11.04, FR-M11-17, FR-M11-17.01, FR-M11-17.02, FR-M11-17.03, FR-M11-17.04, FR-M11-17.05, FR-M11-17.06, BR-M11-26, BR-M11-29 | Nhóm B. Ngoài section (M10). Phần M11: khi cờ Group tắt, yêu cầu bị từ chối, việc hệ thống (kế nhiệm Owner) vẫn chạy; danh sách chặn/chạy thuộc FR-M11|
| DEC-227 | Phụ thuộc | Hiện hành | Chuyển M10 | Nhóm B. M10: nhật ký thao tác Admin ghi ẩn/khóa/mở khóa nhóm|
| DG-1 | Nhắc tới | Hiện hành | Không áp dụng: chỉ nhắc tới, không quy định hành vi M11 | Nhóm B. Tổng quan: có không gian nhóm|
| DG-4 | Nhắc tới | Hiện hành | Không áp dụng: chỉ nhắc tới, không quy định hành vi M11 | Nhóm B. Bản đồ module: Group|
| DG-5 | Sở hữu | Sửa một phần bởi DEC-009, DEC-104 | FR-M11-12, FR-M11-12.09, BR-M11-01, BR-M11-02, BR-M11-16 | Nhóm B. Ngoài section. Nguyên tắc: nhóm tái dùng cơ chế Forum, không leaderboard/reputation riêng; bài ẩn danh vẫn lưu danh tính thật. Ẩn danh chỉ có trong nhóm; nhóm có cổng duyệt riêng|
| DG-7 | Nhắc tới | Hiện hành | Không áp dụng: chỉ nhắc tới, không quy định hành vi M11 | Nhóm B. Kiến trúc: API cho Group|
| DM-13 | Nhắc tới | Hiện hành | Không áp dụng: chỉ nhắc tới, không quy định hành vi M11 | Nhóm B. Sơ đồ kiến trúc có Group|
| DM-2.1 | Sở hữu | Sửa một phần bởi DEC-009 | FR-M11-12, FR-M11-12.10, BR-M11-17 | Nhóm B. Ngoài section (draft M03). Chỉ phần is_anonymous: ẩn tác giả với người xem khác, vẫn lưu danh tính thật; ẩn danh đã chuyển về M11 (DEC-009). Ẩn danh chỉ có trong nhóm, theo công tắc của nhóm|
| DM-4.5 | Nhắc tới | Sửa một phần bởi QA-043, DEC-215 | Không áp dụng: chỉ nhắc tới, không quy định hành vi M11 | Nhóm B. Draft: Follow Group — đã bị QA-043, DEC-215 bỏ. Không theo dõi được nhóm|
| DM-7.1 | Nhắc tới | Sửa một phần bởi DEC-125 | Không áp dụng: chỉ nhắc tới, không quy định hành vi M11 | Nhóm B. Draft: feed Personalized theo Group đang theo dõi — đã bị DEC-125 thay|
| DM-8.1 | Nhắc tới | Sửa một phần bởi DEC-215 | Không áp dụng: chỉ nhắc tới, không quy định hành vi M11 | Nhóm B. Draft: thông báo nội dung mới trong group đang follow — đã bị DEC-215 thay|
| DM-9.4 | Phụ thuộc | Hiện hành | BR-M11-02 | Nhóm B. Draft M12: không có leaderboard riêng theo Group|
| DM-x02 | Nhắc tới | Hiện hành | Không áp dụng: chỉ nhắc tới, không quy định hành vi M11 | Nhóm B. Phạm vi: Group trong phạm vi|
| DM-x04 | Phụ thuộc | Hiện hành | Không áp dụng: nguyên tắc chung; hành vi của cổng duyệt khi AI tắt chờ Q-11 | Nhóm B. Draft: lõi Forum/Group không phụ thuộc cứng vào AI|
| GL:Anonymous Post | Sở hữu | Hiện hành | FR-M11-12.10, BR-M11-17 | Nhóm B. Ngoài section. Thuật ngữ bài ẩn danh: hệ thống vẫn giữ danh tính thật để kiểm duyệt|
| GL:Group | Sở hữu | Hiện hành | FR-M11-03 | Nhóm B. Ngoài section. Thuật ngữ Group|
| GL:GroupMember | Sở hữu | Sửa một phần bởi QA-016 | BR-M11-05 | Nhóm B. Ngoài section. Thuật ngữ GroupMember (ghi owner/member; nay ba cấp). Ba vai trò thay cho owner/member|
| ISS-034 | Sở hữu | Trùng với QA-015 | — | Nhóm B. Ngoài section. Danh tính bài ẩn danh (QA-015)|
| ISS-035 | Sở hữu | Trùng với QA-016 | — | Nhóm B. Ngoài section. Vai trò riêng trong nhóm (QA-016)|
| ISS-039 | Sở hữu | Trùng với QA-016 | — | Nhóm B. Ngoài section. Công tắc kiểm duyệt nhóm và kiểm duyệt hệ thống (QA-016)|
| ISS-041 | Nhắc tới | Sửa một phần bởi QA-221 | Không áp dụng: chỉ nhắc tới, không quy định hành vi M11 | Nhóm B. Group Chat thuộc M16 (sửa ở ISS-163)|
| ISS-051 | Phụ thuộc | Trùng với QA-043 | — | Nhóm B. M07: phạm vi theo dõi (QA-043)|
| ISS-052 | Sở hữu | Trùng với QA-044, QA-045 | — | Nhóm B. Ngoài section. Nhóm Private: hiển thị, tham gia, câu hỏi (QA-044, QA-045)|
| ISS-085 | Nhắc tới | Trùng với DEC-053 | — | Nhóm B. M06: phạm vi tìm có Group|
| ISS-086 | Nhắc tới | Trùng với DEC-054 | — | Nhóm B. M06: cách kích hoạt tìm Group|
| ISS-090 | Nhắc tới | Trùng với DEC-058 | — | Nhóm B. M06: gợi ý có Group|
| ISS-093 | Nhắc tới | Trùng với DEC-060 | — | Nhóm B. M06: hiển thị kết quả Group|
| ISS-095 | Phụ thuộc | Sửa một phần bởi DEC-208, DEC-210 | Chuyển M06 | Nhóm B. M06: quyền tìm kiếm với nhóm Private|
| ISS-104 | Phụ thuộc | Trùng với DEC-072 | — | Nhóm B. M08: đối tượng báo cáo có Group|
| ISS-142 | Phụ thuộc | Trùng với DEC-113 | — | Nhóm B. M12: nguồn của DEC-113|
| ISS-163 | Nhắc tới | Trùng với QA-221 | — | Nhóm B. Group Chat không thuộc M11|
| ISS-164 | Nhắc tới | Trùng với QA-222 | — | Nhóm B. M16: quản trị Group Chat; chỉ so sánh với kế nhiệm Owner của M11|
| ISS-166 | Phụ thuộc | Trùng với DEC-126 | — | Nhóm B. M14: Guest với tab Group|
| ISS-168 | Phụ thuộc | Trùng với DEC-125 | — | Nhóm B. M14: bốn tab có Group|
| ISS-173 | Phụ thuộc | Trùng với QA-233 | — | Nhóm B. M14: bài nhóm Public vào Trending, không vào Newest|
| ISS-177 | Nhắc tới | Trùng với QA-237 | — | Nhóm B. M14: banner bài mới ở tab Group|
| ISS-180 | Nhắc tới | Trùng với QA-243 | — | Nhóm B. M15: đã bỏ tỉ lệ bài nhóm|
| ISS-187 | Phụ thuộc | Trùng với QA-229 | — | Nhóm B. M14: tab Group (QA-229)|
| ISS-188 | Phụ thuộc | Trùng với QA-230 | — | Nhóm B. M14: hiện/ẩn tab Group (QA-230)|
| ISS-302 | Nhắc tới | Trùng với DEC-192 | — | Nhóm B. M08: kết quả chung khi đối tượng là nhóm (DEC-192)|
| ISS-309 | Phụ thuộc | Trùng với DEC-194 | — | Nhóm B. M08: báo cáo nhóm (DEC-194)|
| ISS-334 | Nhắc tới | Trùng với DEC-209 | — | Nhóm B. M06: khớp tên Group (DEC-209)|
| ISS-335 | Phụ thuộc | Trùng với DEC-210 | — | Nhóm B. M06: câu hỏi dẫn tới DEC-210|
| ISS-GRP-01 | Nhắc tới | Bị thay bởi DEC-110 | — | Nhóm B. Backlog Phase 4 còn ghi Open; nội dung đã được trả lời ở Phase 5 M11 (QA-188, DEC-110)|
| ISS-GRP-02 | Nhắc tới | Bị thay bởi DEC-104 | — | Nhóm B. Backlog Phase 4 còn ghi Open; nội dung đã được trả lời ở Phase 5 M11 (QA-182, DEC-104)|
| OPEN-011 | Sở hữu | Bị thay bởi DEC-239 | — | Nhóm B. Ngoài section. Xét áp "nội dung báo cáo được chỉ xóa mềm" cho M11; hẹn bàn khi làm FR M11. Phần M11 đã chốt ở DEC-239; phần M16 vẫn mở |
| QA-011 | Sở hữu | Sửa một phần bởi DEC-208 | FR-M11-01.04, FR-M11-03, FR-M11-03.01, FR-M11-03.02, FR-M11-03.04, FR-M11-03.05, FR-M11-03.06, BR-M11-11, BR-M11-13 | Nhóm B. Ngoài section. Phần GRP của Guest: xem danh sách, mô tả, nội dung nhóm công khai; nhóm Private ẩn hoàn toàn; tham gia cần đăng nhập. Phần GRP giữ nguyên. DEC-171, DEC-206 (ngoài bảng nguồn) sửa phần hồ sơ, tóm tắt AI, không chạm nhóm|
| QA-015 | Sở hữu | Sửa một phần bởi DEC-112 | FR-M11-03, FR-M11-03.09, FR-M11-03.10, FR-M11-12.10, BR-M11-17 | Nhóm B. Ngoài section. Bài ẩn danh: ẩn với USER; MODERATOR và ADMIN thấy danh tính thật. DEC-112 thêm Group Mod/Owner thấy danh tính thật|
| QA-016 | Sở hữu | Sửa một phần bởi DEC-104, DEC-233 | FR-M11-02, FR-M11-02.05, FR-M11-08, FR-M11-08.01, FR-M11-12, FR-M11-12.04, FR-M11-13, FR-M11-13.05, FR-M11-14.04, BR-M11-05, BR-M11-18, BR-M11-22 | Nhóm B. Ngoài section. Ba cấp Owner/Group Mod/Member; công tắc duyệt trước do Owner; System MOD/ADMIN can thiệp bất kỳ lúc nào. Không dấu sửa: điểm ≥ 0.9 tự từ chối; 0.5–<0.9 bắt buộc nhóm duyệt dù công tắc tắt; < 0.5 theo công tắc|
| QA-023 | Nhắc tới | Sửa một phần bởi QA-221 | Không áp dụng: chỉ nhắc tới, không quy định hành vi M11 | Nhóm B. Group Chat "trong Group" — đã sửa: độc lập với M11|
| QA-035 | Phụ thuộc | Sửa một phần bởi DEC-209 | Chuyển M06 | Nhóm B. M06: Group tìm theo tên + mô tả (đã sửa bởi DEC-209). Không dấu sửa: Group khớp theo tên, không theo mô tả|
| QA-036 | Nhắc tới | Sửa một phần bởi DEC-209 | Không áp dụng: chỉ nhắc tới, không quy định hành vi M11 | Nhóm B. M06: lý do dùng khớp chuỗi|
| QA-038 | Phụ thuộc | Hiện hành | BR-M11-02 | Nhóm B. M12: leaderboard chỉ toàn hệ thống, không theo nhóm|
| QA-039 | Phụ thuộc | Trùng với QA-038 | — | Nhóm B. M12: không có leaderboard theo nhóm|
| QA-043 | Phụ thuộc | Sửa một phần bởi DEC-215 | Chuyển M07 | Nhóm B. M07: không theo dõi nhóm, tham gia/rời đã đủ nghĩa. Phần không theo dõi nhóm giữ nguyên|
| QA-044 | Sở hữu | Sửa một phần bởi DEC-210, DEC-229 | FR-M11-04, FR-M11-04.03, FR-M11-05, FR-M11-05.01, FR-M11-06, BR-M11-07 | Nhóm B. Ngoài section. Vào nhóm Private qua link mời (vào thẳng) hoặc gửi yêu cầu (Owner/Mod duyệt). Phần visible-but-gated đã bị DEC-210 bỏ. Link mời vào thẳng vs dùng lại luồng DEC-103 (Q-01); phần visible-but-gated bị DEC-210 bỏ. Mâu thuẫn với DEC-110 đã giải ở DEC-229 (Q-01) |
| QA-045 | Sở hữu | Sửa một phần bởi DEC-237 | FR-M11-02, FR-M11-02.07, FR-M11-02.08, FR-M11-04, FR-M11-04.02, FR-M11-04.03, FR-M11-06, FR-M11-06.01, BR-M11-07, BR-M11-08 | Nhóm B. Ngoài section. Một câu hỏi tham gia tùy chọn do Owner đặt; người xin vào điền câu trả lời|
| QA-054 | Phụ thuộc | Trùng với DEC-020 | — | Nhóm B. M01: thứ tự gợi ý @mention theo nhóm. Dấu sửa ghi DEC-214 (ngoài bảng nguồn) dẫn lại DEC-209; chỉ đổi cách khớp tên|
| QA-109 | Nhắc tới | Trùng với DEC-053 | — | Nhóm B. M06: phạm vi tìm có Group|
| QA-115 | Nhắc tới | Trùng với DEC-058 | — | Nhóm B. M06: gợi ý có Group|
| QA-120 | Phụ thuộc | Sửa một phần bởi DEC-210 | Chuyển M06 | Nhóm B. M06: nhóm Private trong tìm kiếm (đã sửa bởi DEC-210). Phần nội dung chỉ thành viên thấy giữ nguyên|
| QA-123 | Phụ thuộc | Trùng với DEC-065 | — | Nhóm B. M07: danh sách sự kiện có nhóm|
| QA-134 | Phụ thuộc | Trùng với DEC-072 | — | Nhóm B. M08: lý do báo cáo theo đối tượng, Group 4|
| QA-191 | Phụ thuộc | Trùng với DEC-113 | — | Nhóm B. M12: nguồn của DEC-113|
| QA-193 | Phụ thuộc | Trùng với DEC-115 | — | Nhóm B. M09: nguồn của DEC-115|
| QA-221 | Nhắc tới | Hiện hành | Không áp dụng: chỉ nhắc tới, không quy định hành vi M11 | Nhóm B. Group Chat không thuộc M11|
| QA-222 | Nhắc tới | Hiện hành | Không áp dụng: chỉ nhắc tới, không quy định hành vi M11 | Nhóm B. M16: quản trị Group Chat; chỉ so sánh với QA-185|
| QA-227 | Phụ thuộc | Trùng với DEC-126 | — | Nhóm B. M14: Guest với tab Group|
| QA-229 | Phụ thuộc | Trùng với DEC-125 | — | Nhóm B. M14: tab Group, khác với vào từng nhóm ở M11|
| QA-230 | Phụ thuộc | Hiện hành | FR-M11-03, FR-M11-03.16, BR-M11-35 | Nhóm B. M14: chưa tham gia nhóm nào → nút "Khám phá Group" dẫn sang trang danh sách/tìm Group|
| QA-232 | Phụ thuộc | Bị thay bởi QA-233 | — | Nhóm B. M14: bị sửa ngay bởi QA-233|
| QA-233 | Phụ thuộc | Trùng với DEC-125 | — | Nhóm B. M14: bài nhóm Public loại khỏi Newest, giữ trong Trending|
| QA-237 | Nhắc tới | Hiện hành | Không áp dụng: chỉ nhắc tới, không quy định hành vi M11 | Nhóm B. M14: banner bài mới ở tab Group|
| QA-239 | Nhắc tới | Hiện hành | Không áp dụng: chỉ nhắc tới, không quy định hành vi M11 | Nhóm B. M14: banner polling cho tab Group|
| QA-243 | Nhắc tới | Hiện hành | Không áp dụng: chỉ nhắc tới, không quy định hành vi M11 | Nhóm B. M15: đã bỏ tỉ lệ bài nhóm. DEC-203 (ngoài bảng nguồn) thêm chỉ số khác|
| QA-285 | Phụ thuộc | Trùng với DEC-145 | — | Nhóm B. M05: nguồn của DEC-145|
| QA-339 | Phụ thuộc | Trùng với DEC-175 | — | Nhóm B. M02: nguồn của DEC-175|
| QA-343 | Phụ thuộc | Trùng với DEC-179 | — | Nhóm B. M04: nguồn của DEC-179 và OPEN-011|
| QA-357 | Phụ thuộc | Trùng với DEC-190 | — | Nhóm B. M08: mức nặng của lý do "Group giả mạo"|
| QA-369 | Sở hữu | Trùng với DEC-194 | — | Nhóm B. Ngoài section (M08). Nguồn của DEC-194|
| QA-371 | Sở hữu | Trùng với DEC-195 | — | Nhóm B. Ngoài section (M09). Nguồn của DEC-195 (E1, E2)|
| QA-394 | Nhắc tới | Trùng với DEC-209 | — | Nhóm B. M06: Group không khớp mô tả (DEC-209)|
| QA-395 | Phụ thuộc | Trùng với DEC-210 | — | Nhóm B. M06: nguồn của DEC-210|
| QA-405 | Phụ thuộc | Trùng với DEC-215 | — | Nhóm B. M07: nguồn của DEC-215|
| QA-417 | Phụ thuộc | Trùng với DEC-225 | — | Nhóm B. M10: chỉ Group, Chat, Gamification có cờ|
| F-GRP-01 | Sở hữu | Hiện hành | FR-M11-01, FR-M11-02, FR-M11-02.01, FR-M11-15 | Nhóm B. Ngoài section. Tạo/sửa/xóa nhóm|
| F-GRP-02 | Sở hữu | Trùng với DEC-102 | — | Nhóm B. Ngoài section. Vai trò nhóm|
| F-GRP-03 | Sở hữu | Sửa một phần bởi DEC-103 | FR-M11-04, FR-M11-04.01 | Nhóm B. Ngoài section. Tham gia nhóm Public. Nhóm Public có câu hỏi thì cần duyệt|
| F-GRP-04 | Sở hữu | Hiện hành | FR-M11-02, FR-M11-13 | Nhóm B. Ngoài section. Công tắc duyệt trước|
| F-GRP-05 | Nhắc tới | Hiện hành | Không áp dụng: chỉ nhắc tới, không quy định hành vi M11 | Nhóm B. Group Chat đã bỏ khỏi M11|
| F-GRP-06 | Sở hữu | Sửa một phần bởi DEC-110, DEC-210 | FR-M11-02 | Nhóm B. Ngoài section. Nhóm Private (làm rõ bởi DEC-210). Không còn visible-but-gated trong tìm kiếm|
| F-GRP-07 | Sở hữu | Sửa một phần bởi DEC-229 | FR-M11-05, FR-M11-05.01 | Nhóm B. Ngoài section. Link mời vào thẳng. Link mời vào thẳng vs dùng lại luồng DEC-103 (Q-01). Mâu thuẫn với DEC-110 đã giải ở DEC-229 (Q-01): không còn vào thẳng |
| F-GRP-08 | Sở hữu | Hiện hành | FR-M11-04, FR-M11-04.03, FR-M11-06, FR-M11-06.02 | Nhóm B. Ngoài section. Gửi yêu cầu, Owner/Mod duyệt|
| F-GRP-09 | Sở hữu | Sửa một phần bởi DEC-103 | FR-M11-02, FR-M11-04, BR-M11-08 | Nhóm B. Ngoài section. Câu hỏi tham gia tùy chọn. Câu hỏi tham gia áp cho cả nhóm Public|
| F-GRP-10 | Sở hữu | Sửa một phần bởi DEC-112 | FR-M11-02, FR-M11-12.07, BR-M11-16 | Nhóm B. Ngoài section. Công tắc ẩn danh, chỉ Owner, chỉ bài mới. Thành viên chọn ẩn danh cho từng bài|
| MR-A01 | Nhắc tới | Trùng với QA-221 | — | Nhóm B. Đợt sửa M16: Group Chat độc lập với M11|
| MR-A02 | Phụ thuộc | Trùng với DEC-125 | — | Nhóm B. M14: tóm tắt đợt sửa, có tab Group|
| MR-A03 | Nhắc tới | Hiện hành | Không áp dụng: chỉ nhắc tới, không quy định hành vi M11 | Nhóm B. Trạng thái Phase 5: M11 đã phỏng vấn xong|
| MR-M06 | Phụ thuộc | Sửa một phần bởi DEC-208, DEC-209, DEC-210, DEC-212 | Chuyển M06 | Nhóm B. M06: phạm vi tìm có Group|
| MR-M07 | Phụ thuộc | Sửa một phần bởi DEC-135 | Chuyển M07 | Nhóm B. M07: danh sách sự kiện có nhóm. Phần nhóm giữ nguyên. QA-257 trùng với DEC-135|
| MR-M14 | Phụ thuộc | Hiện hành | Chuyển M14 | Nhóm B. M14: dòng module, có tab Group|
| MR-M16 | Nhắc tới | Hiện hành | Không áp dụng: chỉ nhắc tới, không quy định hành vi M11 | Nhóm B. M16 không phụ thuộc M11|
| DEC-004 | Nhắc tới | Hiện hành | Không áp dụng: chỉ nhắc tới, không quy định hành vi M11 | Nhóm C. DEC-112 trích làm mẫu danh tính ẩn danh nhưng DEC-004 nói về Post Star ≠ Comment Star; mẫu đúng là QA-015|
| DEC-005 | Nhắc tới | Hiện hành | Không áp dụng: chỉ nhắc tới, không quy định hành vi M11 | Nhóm C. DEC-112 trích làm mẫu danh tính ẩn danh nhưng DEC-005 nói về AI chỉ hỗ trợ; mẫu đúng là QA-015|
| DEC-127 | Phụ thuộc | Hiện hành | Không áp dụng: giới hạn tạo nhóm tính theo 24 giờ gần nhất, không theo ranh giới ngày | Nhóm D. Dùng chung: múi giờ cho "5 nhóm/ngày", thâm niên, 30 phút giữ bài chờ duyệt|
| DEC-128 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M11 | Nhóm D. Dùng chung; không quy định hành vi M11|
| DEC-129 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M11 | Nhóm D. Dùng chung; không quy định hành vi M11. DEC-156 (ngoài bảng nguồn) không chạm M11|
| DEC-130 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M11 | Nhóm D. Dùng chung; không quy định hành vi M11. DEC-160 (ngoài bảng nguồn) không chạm M11|
| DEC-131 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M11 | Nhóm D. Dùng chung; không quy định hành vi M11. DEC-146 (ngoài bảng nguồn), DEC-154 (loại) không chạm M11|
| DEC-132 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M11 | Nhóm D. Dùng chung; không quy định hành vi M11. DEC-141, DEC-144 (ngoài bảng nguồn) không chạm M11|
| DEC-133 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M11 | Nhóm D. Dùng chung; không quy định hành vi M11. DEC-207 (ngoài bảng nguồn) không chạm M11|
| DEC-134 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M11 | Nhóm D. Dùng chung; không quy định hành vi M11|
| DEC-135 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M11 | Nhóm D. Dùng chung; không quy định hành vi M11|
| DEC-136 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M11 | Nhóm D. Dùng chung; không quy định hành vi M11|
| DEC-137 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M11 | Nhóm D. Dùng chung; không quy định hành vi M11|
| DEC-138 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M11 | Nhóm D. Dùng chung; không quy định hành vi M11. DEC-155, DEC-157 (ngoài bảng nguồn) không chạm M11|
| ISS-189 | Phụ thuộc | Trùng với DEC-127 | — | Nhóm D. Dùng chung: múi giờ (như DEC-127)|
| ISS-190 | Nhắc tới | Trùng với DEC-128 | — | Nhóm D. Dùng chung; không quy định hành vi M11|
| ISS-191 | Nhắc tới | Trùng với DEC-129 | — | Nhóm D. Dùng chung; không quy định hành vi M11|
| ISS-192 | Nhắc tới | Trùng với DEC-130 | — | Nhóm D. Dùng chung; không quy định hành vi M11|
| ISS-193 | Nhắc tới | Trùng với DEC-131 | — | Nhóm D. Dùng chung; không quy định hành vi M11|
| ISS-194 | Nhắc tới | Trùng với DEC-132 | — | Nhóm D. Dùng chung; không quy định hành vi M11|
| ISS-195 | Nhắc tới | Trùng với DEC-133 | — | Nhóm D. Dùng chung; không quy định hành vi M11|
| ISS-196 | Nhắc tới | Trùng với QA-255 | — | Nhóm D. Dùng chung; không quy định hành vi M11|
| ISS-197 | Nhắc tới | Trùng với DEC-134 | — | Nhóm D. Dùng chung; không quy định hành vi M11|
| ISS-198 | Nhắc tới | Trùng với DEC-135 | — | Nhóm D. Dùng chung; không quy định hành vi M11|
| ISS-199 | Nhắc tới | Trùng với DEC-136 | — | Nhóm D. Dùng chung; không quy định hành vi M11|
| ISS-200 | Nhắc tới | Trùng với QA-259 | — | Nhóm D. Dùng chung; không quy định hành vi M11|
| ISS-201 | Nhắc tới | Trùng với QA-260 | — | Nhóm D. Dùng chung; không quy định hành vi M11|
| ISS-202 | Nhắc tới | Trùng với QA-261 | — | Nhóm D. Dùng chung; không quy định hành vi M11|
| ISS-204 | Nhắc tới | Trùng với DEC-138 | — | Nhóm D. Dùng chung; không quy định hành vi M11|
| QA-248 | Phụ thuộc | Trùng với DEC-127 | — | Nhóm D. Dùng chung: múi giờ (như DEC-127)|
| QA-249 | Nhắc tới | Trùng với DEC-128 | — | Nhóm D. Dùng chung; không quy định hành vi M11|
| QA-250 | Nhắc tới | Trùng với DEC-129 | — | Nhóm D. Dùng chung; không quy định hành vi M11|
| QA-251 | Nhắc tới | Trùng với DEC-130 | — | Nhóm D. Dùng chung; không quy định hành vi M11|
| QA-252 | Nhắc tới | Trùng với DEC-131 | — | Nhóm D. Dùng chung; không quy định hành vi M11|
| QA-253 | Nhắc tới | Trùng với DEC-132 | — | Nhóm D. Dùng chung; không quy định hành vi M11|
| QA-254 | Nhắc tới | Trùng với DEC-133 | — | Nhóm D. Dùng chung; không quy định hành vi M11|
| QA-255 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M11 | Nhóm D. Dùng chung; không quy định hành vi M11|
| QA-256 | Nhắc tới | Trùng với DEC-134 | — | Nhóm D. Dùng chung; không quy định hành vi M11|
| QA-257 | Nhắc tới | Trùng với DEC-135 | — | Nhóm D. Dùng chung; không quy định hành vi M11|
| QA-258 | Nhắc tới | Trùng với DEC-136 | — | Nhóm D. Dùng chung; không quy định hành vi M11|
| QA-259 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M11 | Nhóm D. Dùng chung; không quy định hành vi M11|
| QA-260 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M11 | Nhóm D. Dùng chung; không quy định hành vi M11|
| QA-261 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M11 | Nhóm D. Dùng chung; không quy định hành vi M11|
| QA-262 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M11 | Nhóm D. Dùng chung; không quy định hành vi M11|
| QA-264 | Nhắc tới | Trùng với DEC-138 | — | Nhóm D. Dùng chung; không quy định hành vi M11|
| MR-A04 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M11 | Nhóm D. Dùng chung; không quy định hành vi M11|
| MR-A05 | Nhắc tới | Trùng với DEC-137 | — | Nhóm D. Dùng chung; không quy định hành vi M11|
| DEC-229 | Sở hữu | Hiện hành | FR-M11-03.18, FR-M11-05.05, BR-M11-12 | Nhóm A. Người được mời theo luồng tham gia; giải mâu thuẫn QA-044, F-GRP-07 với DEC-110 |
| DEC-230 | Sở hữu | Sửa một phần bởi DEC-240 | FR-M11-12.06, FR-M11-12.14, FR-M11-12.15, BR-M11-18, BR-M11-19 | Nhóm A. Bài nhóm không có điểm quét: AI tắt, tác giả Admin theo công tắc; quét lỗi chờ nhóm duyệt |
| DEC-231 | Sở hữu | Sửa một phần bởi DEC-270 | FR-M11-14.01, FR-M11-14.05, FR-M11-14.06, FR-M11-14.07, FR-M11-14.08, BR-M11-05, BR-M11-30, BR-M11-37 | Nhóm A. Gỡ khỏi nhóm: một thao tác, xóa mềm, thông báo, không trừ điểm, theo thứ bậc |
| DEC-232 | Sở hữu | Hiện hành | FR-M11-11.01, FR-M11-11.05, BR-M11-26 | Nhóm A. Mọi ban, vô hiệu hóa, xóa đều chuyển Owner ngay; Owner cũ là Member |
| DEC-233 | Sở hữu | Sửa một phần bởi DEC-240 | FR-M11-03.11, FR-M11-03.12, FR-M11-13.09, BR-M11-33 | Nhóm A. Mod, Admin ngoài nhóm chỉ xem nhóm Private trong vụ báo cáo; hàng chờ nhóm chỉ Owner, Group Mod |
| DEC-234 | Sở hữu | Hiện hành | FR-M11-02.12, FR-M11-02.13, FR-M11-03.13, BR-M11-13, BR-M11-15 | Nhóm A. Người ngoài tương tác bài nhóm Public; "đã hiện" khi chuyển Private |
| DEC-235 | Sở hữu | Hiện hành | FR-M11-16.07, FR-M11-16.08, FR-M11-16.09, FR-M11-16.10, BR-M11-26, BR-M11-28 | Nhóm A. Nhóm Bị khóa chặn mọi thao tác quản trị; thành viên vẫn tự rời |
| DEC-236 | Sở hữu | Sửa một phần bởi DEC-261 | FR-M11-17.07, FR-M11-17.08, BR-M11-29 | Nhóm A. Cờ Group tắt: lối vào vẫn hiện, mở ra thì hệ thống đang bận |
| DEC-258 | Phụ thuộc | Sửa một phần bởi DEC-262 | BR-M11-14 | Nhóm B (đối chiếu FR-M14). Bài nhóm Public vào tab Following; bài ẩn danh không vào nhờ theo dõi tác giả; phần bài nhóm Private bị DEC-262 rút |
| DEC-261 | Phụ thuộc | Hiện hành | FR-M11-17.07, BR-M11-29 | Nhóm B (đối chiếu FR-M14). Cờ Group tắt: tab Group vẫn liệt kê bài nhóm như lối vào |
| DEC-262 | Phụ thuộc | Hiện hành | FR-M11-12.13, BR-M11-14 | Nhóm B (đối chiếu FR-M14). Bài nhóm Private không vào tab Following; DEC-111 giữ nguyên |
| DEC-237 | Sở hữu | Sửa một phần bởi DEC-240 | FR-M11-01.03, FR-M11-01.06, FR-M11-01.07, FR-M11-01.08, FR-M11-01.09, FR-M11-01.10, FR-M11-01.11, FR-M11-01.12, FR-M11-02.10, FR-M11-02.11, FR-M11-02.14, FR-M11-02.15, FR-M11-03.16, FR-M11-03.17, FR-M11-04.08, FR-M11-04.09, FR-M11-06.04, FR-M11-06.07, FR-M11-06.08, FR-M11-06.09, FR-M11-08.06, FR-M11-10.07, FR-M11-10.08, FR-M11-10.09, FR-M11-11.06, FR-M11-11.07, FR-M11-13.06, FR-M11-13.10, FR-M11-13.11, FR-M11-13.12, FR-M11-13.13, BR-M11-03, BR-M11-08, BR-M11-09, BR-M11-18, BR-M11-21, BR-M11-24, BR-M11-26, BR-M11-31, BR-M11-32, BR-M11-35, BR-M11-37, BR-M11-38, BR-M11-39 | Nhóm A. Danh sách xác nhận L1–L13 (L4 duyệt luôn) |
| DEC-238 | Sở hữu | Hiện hành | FR-M11-03.14, FR-M11-03.15, FR-M11-04.06, FR-M11-04.10, FR-M11-05.02, FR-M11-05.06, FR-M11-05.07, FR-M11-07.02, FR-M11-07.03, FR-M11-07.04, FR-M11-07.05, BR-M11-10, BR-M11-12, BR-M11-34, BR-M11-36, BR-M11-37 | Nhóm A. Mở rộng phạm vi: danh sách thành viên, rút yêu cầu, bỏ chặn; link mời chung không thu hồi |
| DEC-239 | Sở hữu | Hiện hành | FR-M11-15.02, BR-M11-23 | Nhóm A. Đóng phần M11 của OPEN-011: nội dung nhóm chỉ xóa mềm |
| ISS-360 | Sở hữu | Trùng với DEC-229 | — | Nhóm A. Vấn đề dẫn tới DEC-229 |
| ISS-361 | Sở hữu | Trùng với DEC-230 | — | Nhóm A. Vấn đề dẫn tới DEC-230 |
| ISS-362 | Sở hữu | Trùng với DEC-231 | — | Nhóm A. Vấn đề dẫn tới DEC-231 |
| ISS-363 | Sở hữu | Trùng với DEC-232 | — | Nhóm A. Vấn đề dẫn tới DEC-232 |
| ISS-364 | Sở hữu | Trùng với DEC-233 | — | Nhóm A. Vấn đề dẫn tới DEC-233 |
| ISS-365 | Sở hữu | Trùng với DEC-234 | — | Nhóm A. Vấn đề dẫn tới DEC-234 |
| ISS-366 | Sở hữu | Trùng với DEC-235 | — | Nhóm A. Vấn đề dẫn tới DEC-235 |
| ISS-367 | Sở hữu | Trùng với DEC-236 | — | Nhóm A. Vấn đề dẫn tới DEC-236 |
| ISS-368 | Sở hữu | Trùng với DEC-237 | — | Nhóm A. Vấn đề dẫn tới DEC-237 |
| ISS-369 | Sở hữu | Trùng với DEC-238 | — | Nhóm A. Vấn đề dẫn tới DEC-238 |
| ISS-370 | Sở hữu | Trùng với DEC-239 | — | Nhóm A. Vấn đề dẫn tới DEC-239 |
| QA-421 | Sở hữu | Trùng với DEC-229 | — | Nhóm A. Câu trả lời của stakeholder cho DEC-229 |
| QA-422 | Sở hữu | Trùng với DEC-230 | — | Nhóm A. Câu trả lời của stakeholder cho DEC-230 |
| QA-423 | Sở hữu | Trùng với DEC-231 | — | Nhóm A. Câu trả lời của stakeholder cho DEC-231 |
| QA-424 | Sở hữu | Trùng với DEC-232 | — | Nhóm A. Câu trả lời của stakeholder cho DEC-232 |
| QA-425 | Sở hữu | Trùng với DEC-233 | — | Nhóm A. Câu trả lời của stakeholder cho DEC-233 |
| QA-426 | Sở hữu | Trùng với DEC-234 | — | Nhóm A. Câu trả lời của stakeholder cho DEC-234 |
| QA-427 | Sở hữu | Trùng với DEC-235 | — | Nhóm A. Câu trả lời của stakeholder cho DEC-235 |
| QA-428 | Sở hữu | Trùng với DEC-235 | — | Nhóm A. Câu trả lời của stakeholder cho DEC-235 |
| QA-429 | Sở hữu | Trùng với DEC-236 | — | Nhóm A. Câu trả lời của stakeholder cho DEC-236 |
| QA-430 | Sở hữu | Trùng với DEC-237 | — | Nhóm A. Câu trả lời của stakeholder cho DEC-237 |
| QA-431 | Sở hữu | Trùng với DEC-238 | — | Nhóm A. Câu trả lời của stakeholder cho DEC-238 |
| QA-432 | Sở hữu | Trùng với DEC-239 | — | Nhóm A. Câu trả lời của stakeholder cho DEC-239 |
| DEC-144 | Nhắc tới | Hiện hành | Không áp dụng: tiền lệ "60 giây gần nhất" mà DEC-237 dẫn cho cách tính 24 giờ | Nhóm C. M05, M06: cách tính giới hạn theo khoảng gần nhất |
| DEC-240 | Sở hữu | Hiện hành | FR-M11-12.01, FR-M11-12.03, FR-M11-12.04, FR-M11-12.05, FR-M11-12.06, FR-M11-12.14, FR-M11-12.15, FR-M11-12.16, FR-M11-12.17, FR-M11-12.18, FR-M11-12.19, FR-M11-12.20, FR-M11-13.13, BR-M11-18, BR-M11-19, BR-M11-33, BR-M11-39, BR-M11-40 | Nhóm A. Bài của Owner không qua duyệt của nhóm; điểm 0.5–< 0.9 hoặc quét lỗi vào hàng chờ Mod hệ thống |
| ISS-371 | Sở hữu | Trùng với DEC-240 | — | Nhóm A. Vấn đề dẫn tới DEC-240 |
| QA-433 | Sở hữu | Trùng với DEC-240 | — | Nhóm A. Câu trả lời của stakeholder cho DEC-240 |
| DEC-270 | Sở hữu | Hiện hành | FR-M11-14.01 | Rà soát chéo 2026-10-24. Gỡ khỏi nhóm là dấu, bài giữ trạng thái đăng; M15 đếm theo trạng thái đó |
| DEC-271 | Sở hữu | Hiện hành | FR-M11-13.14, BR-M11-38 | Rà soát chéo 2026-10-24. Bài nhóm bị AI từ chối, được chấp nhận khiếu nại thì đi qua cổng duyệt của nhóm |
| QA-476 | Sở hữu | Trùng với DEC-270 | — | Rà soát chéo 2026-10-24. Câu trả lời của stakeholder |
| QA-477 | Sở hữu | Trùng với DEC-271 | — | Rà soát chéo 2026-10-24. Câu trả lời của stakeholder |
| ISS-414 | Sở hữu | Trùng với DEC-270 | — | Rà soát chéo 2026-10-24. Câu hỏi rà soát chéo, đã có DEC-270 |
| ISS-415 | Sở hữu | Trùng với DEC-271 | — | Rà soát chéo 2026-10-24. Câu hỏi rà soát chéo, đã có DEC-271 |

### C.2 Chuỗi quyết định

| Chuỗi | Nội dung hiện hành |
|---|---|
| DEC-105 → DEC-113 → DEC-239 (QA-183, ISS-134 trùng DEC-105) | Xóa nhóm là xóa mềm, nhóm và nội dung không hiện với ai; rời hoặc bị kick thì bài giữ nguyên, tác giả hiện như trước. Xóa nhóm không trừ điểm của ai (DEC-113 bỏ ngoại lệ cũ). Mọi cách nội dung nhóm mất đi trong M11 đều là xóa mềm (DEC-239). |
| QA-016 → DEC-104 → DEC-195 → DEC-230, DEC-233, DEC-240 | Ba cấp Owner / Group Mod / Member; công tắc duyệt trước do Owner. Cổng duyệt theo điểm quét: ≥ 0.9 tự từ chối; 0.5–< 0.9 nhóm bắt buộc duyệt; < 0.5 theo công tắc. Không có điểm: AI tắt có chủ đích hoặc tác giả Admin thì theo công tắc, quét thất bại thì bắt buộc chờ nhóm duyệt (DEC-230). Hàng chờ của nhóm chỉ Owner, Group Mod duyệt; "hàng chờ của System Mod" là bài không thuộc nhóm; Mod, Admin can thiệp nội dung nhóm qua vụ báo cáo (DEC-233). Bài của Owner không qua duyệt của nhóm: ≥ 0.9 tự từ chối, 0.5–< 0.9 hoặc quét lỗi vào hàng chờ Mod hệ thống, còn lại đăng ngay; Owner là Admin thì đăng ngay (DEC-240). Group Mod không tự duyệt bài của mình (DEC-237). |
| DM-5.2, GL:GroupMember → QA-016 | Vai trò owner/member của draft thay bằng ba cấp Owner / Group Mod / Member. |
| DM-5.1, DM-5.2, F-GRP-03, F-GRP-09 → DEC-103 → DEC-237, DEC-238 | Ma trận tham gia: Public không câu hỏi vào ngay; Public có câu hỏi và mọi nhóm Private cần Owner/Group Mod duyệt; có câu hỏi thì bắt buộc trả lời. Bị từ chối gửi lại ngay; đang có yêu cầu chờ thì không gửi thêm; người gửi rút được yêu cầu. Nhóm thành vào ngay thì yêu cầu đang chờ được duyệt luôn. Chặn áp cho mọi cách vào nhóm; Owner, Group Mod xem danh sách chặn và bỏ chặn. |
| QA-044, F-GRP-07, MR-M11 → DEC-110 → DEC-210, DEC-229, DEC-238 | Nhóm Private không hiện với người ngoài nhóm (kể cả Guest, Mod, Admin), thành viên vẫn tìm thấy. Mọi thành viên mời được; một link mời chung của nhóm, không hết hạn, không thu hồi; người được mời theo luồng tham gia, không vào thẳng (mâu thuẫn Q-01 đã giải). |
| DEC-053, DEC-062, QA-120, ISS-095, F-GRP-06 → DEC-210 | "Visible-but-gated" không còn áp dụng: nhóm Private ẩn khỏi tìm kiếm với người ngoài nhóm; nội dung chỉ thành viên thấy. |
| DG-5, DM-2.1 → DEC-009 → DEC-112; QA-015 → DEC-112 | Ẩn danh chỉ có trong nhóm, công tắc do Owner, chỉ áp cho bài mới; khi bật, thành viên chọn ẩn danh cho từng bài; tắt không lộ bài cũ. Người thấy danh tính thật: MODERATOR, ADMIN và Group Mod, Owner của nhóm. |
| DEC-111, DEC-108 → DEC-125, DEC-234, DEC-258 → DEC-262 (QA-232 → QA-233) | Bài nhóm luôn hiện với thành viên; bài nhóm Public hiện với người ngoài nhóm ở Trending (không vào Newest) và người ngoài đã đăng nhập tương tác như bài thường. Bài nhóm Public vào tab Following của người theo dõi; bài ẩn danh không vào nhờ theo dõi tác giả (DEC-258). Bài nhóm Private không bao giờ ra feed chính, kể cả tab Following của thành viên (DEC-262 rút ngoại lệ của DEC-258). Nhóm chuyển Private: người ngoài chỉ còn đọc bài đang hiện sẵn trên màn hình đã tải, tải lại hoặc mở lại thì "Nội dung không tồn tại"; feed, tìm kiếm sau đó không trả bài. |
| DEC-102 → DEC-231, DEC-237 | Quyền theo ma trận DEC-102, thứ bậc chặt áp cả cho nội dung. "Ẩn/xóa" là một thao tác gỡ khỏi nhóm: xóa mềm, thông báo tác giả, không trừ điểm, không khiếu nại. Chỉ Owner sửa tên, mô tả. |
| DEC-107 → DEC-232, DEC-237 | Owner tự rời phải chỉ định người kế nhiệm; một mình thì rời là xóa nhóm. Mọi ban, vô hiệu hóa, xóa tài khoản Owner chuyển quyền ngay: Group Mod thâm niên dài nhất (tính từ lần bổ nhiệm gần nhất) → Member tham gia sớm nhất → xóa nhóm; Owner cũ ở lại làm Member. |
| DEC-109 → DEC-237 | Quyết định cấp nhóm không khiếu nại; bài nhóm bị AI tự từ chối vẫn khiếu nại qua M09. Nhóm từ chối bài phải kèm lý do; tác giả sửa, gửi lại được. |
| DEC-101 → DEC-237 | Tối đa 5 nhóm trong 24 giờ gần nhất, kể cả nhóm đã xóa, áp cả Admin; không giới hạn tổng số nhóm sở hữu, tham gia. |
| QA-045 → DEC-237 | Tối đa một câu hỏi tham gia, tùy chọn; có câu hỏi thì bắt buộc trả lời. |
| DM-4.5, DM-8.1, QA-043 → DEC-215 | Không theo dõi được nhóm; không có thông báo "nội dung mới trong nhóm đang theo dõi". |
| DM-7.1 → DEC-125 | Không có feed Personalized theo nhóm đang theo dõi; thay bằng tab Group. |
| DEC-072 → DEC-194 → DEC-235; DEC-192 → DEC-197 | Nhóm bị báo cáo (Owner là người bị báo cáo); Mod, Admin Ẩn (không bỏ ẩn) hoặc Khóa (mở khóa trực tiếp). Nhóm Bị khóa chặn đăng, bình luận, vote, bình chọn, tham gia, mời và mọi thao tác quản trị kể cả xóa nhóm, Owner rời; Member, Group Mod tự rời được; bookmark, báo cáo vẫn được; hệ thống vẫn chuyển Owner. Không có link khiếu nại. |
| DEC-092 → DEC-225 → DEC-236 → DEC-261 | Cờ Group tắt: mọi yêu cầu của người dùng khác Admin bị từ chối với "Hệ thống đang bận, vui lòng thử lại sau", kể cả mở nhóm, mở bài nhóm; lối vào (danh sách nhóm, Trending, tab Group và tab Following của feed, hồ sơ, tìm kiếm, bookmark, thông báo) vẫn hiện; kế nhiệm Owner và kiểm duyệt M08 vẫn chạy; dữ liệu giữ nguyên; không làm bù. |
| DEC-065 → DEC-246; DEC-113 → DEC-241; DEC-125 → DEC-260; DEC-225 → DEC-245, DEC-256; QA-038 → DEC-243 | Các sửa đổi này chỉ chạm phần M11 không dùng: thông báo danh hiệu tuần, trừ điểm bình luận, bảng xếp hạng (M12); tab mặc định của feed (M14); cờ Gamification, cờ Chat (M12, M16). Phần M11 dùng giữ nguyên. |
| DEC-065 → DEC-215, DEC-231, DEC-237 (DEC-147, DEC-151, DEC-180, DEC-218, DEC-221 ngoài bảng nguồn hoặc đã loại) | Thông báo nhóm chỉ trong ứng dụng: mời (kèm link), yêu cầu tham gia mới (tới Owner, Group Mod), được chấp nhận, được bổ nhiệm, bị kick, trở thành Owner, bị gỡ khỏi nhóm. Không thông báo khi vào ngay nhóm Public, bị từ chối, bị giáng. |
| QA-023, ISS-041 → QA-221 | Group Chat độc lập, không thuộc M11. |
| DEC-020 → DEC-153 (→ DEC-214, ngoài bảng nguồn) | Gợi ý @mention trong bài nhóm ưu tiên: đang theo dõi > cùng nhóm > toàn hệ thống; DEC-153, DEC-214 chỉ đổi thứ tự trong tầng và cách khớp tên. |
| QA-035 → DEC-053 → DEC-209 | Tìm Group khớp theo tên (bất kỳ vị trí, bỏ dấu, gần đúng), không khớp mô tả. |
| QA-011 → DEC-171, DEC-206, DEC-208 (DEC-171, DEC-206 ngoài bảng nguồn) | Phần GRP của Guest còn hiệu lực: xem danh sách, mô tả, nội dung nhóm Public; nhóm Private ẩn hoàn toàn. Các DEC sau chỉ sửa phần hồ sơ, tóm tắt AI, tìm bài của Guest. |
| DEC-115 → DEC-198, DEC-200, DEC-202 (ngoài bảng nguồn) | Khiếu nại xóa nội dung chỉ cho thao tác của Mod, Admin hệ thống; quyết định cấp nhóm không khiếu nại (DEC-109). |
| DEC-231 → DEC-270 | Gỡ khỏi nhóm không tạo trạng thái đăng mới: bài giữ trạng thái đăng (thường là Đã đăng), mang dấu "bị gỡ khỏi nhóm"; hiển thị, không khôi phục, không trừ điểm, không khiếu nại như DEC-231; M15 đếm theo trạng thái đăng (rà soát chéo 2026-10-24). |
| DEC-237 (L11), DEC-198 → DEC-271 | Bài nhóm bị AI tự từ chối, khiếu nại qua M09 được chấp nhận: đi tiếp qua cổng duyệt của nhóm như bài có điểm quét dưới 0.5, không quét lại (công tắc duyệt trước bật → chờ nhóm duyệt; tắt, hoặc bài của Owner → Đã đăng). |
