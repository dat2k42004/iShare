# Issue Queue Register

> BA's working interview backlog — one row per question asked/to-ask.
> Built scope-by-scope, not front-loaded.
> Severity: **Blocker** / **Major** / **Minor**
> Status: Open / Asked / Closed / Deferred

| ID | Issue | Type | Severity | Scope | Status | Resulting QA-### |
|---|---|---|---|---|---|---|
| ISS-021 | Timeline & deadline cho MS1 | Business | Major | Phase 1 | Closed | QA-001 |
| ISS-022 | Definition of Done cho MS1 | Business | Blocker | Phase 1 | Closed | QA-002 |
| ISS-023 | Success metric & cách đo lường | Business | Major | Phase 1 | Closed | QA-003 |
| ISS-024 | Landscape cạnh tranh / thị trường hiện tại | Business | Major | Phase 1 | Closed | QA-004 |
| ISS-025 | Business goals của hệ thống | Business | Blocker | Phase 1 | Closed | QA-005, QA-006 |
| ISS-026 | AI cost & budget cho MS1 | Business | Major | Phase 1 | Open | QA-007 |
| ISS-027 | Production-readiness expectation | Business | Major | Phase 1 | Closed | QA-008 |
| ISS-028 | Ai giữ role ADMIN sau khi launch? | Business | Major | Phase 1 | Closed | QA-009 |
| ISS-029 | Ràng buộc học thuật / tech stack / hội đồng | Business | Minor | Phase 1 | Closed (Phase 7 prep) | QA-010, QA-261 |
| ISS-030 | Guest có quyền gì? | Permission | Blocker | Phase 2 | Closed | QA-011 |
| ISS-031 | USER → MODERATOR bằng cách nào? Ai phong? Điều kiện? | Business rule | Blocker | Phase 2 | Closed | QA-012 |
| ISS-032 | MODERATOR mất role bằng cách nào? | Business rule | Major | Phase 2 | Closed | QA-013 |
| ISS-033 | User có thể vừa là MODERATOR vừa là ADMIN không? | Permission | Major | Phase 2 | Closed | QA-014 |
| ISS-034 | Anonymous Post — danh tính ẩn với ai? | Permission | Blocker | Phase 2 | Closed | QA-015 |
| ISS-035 | GroupMember có role riêng trong Group không? | Permission | Major | Phase 2 | Closed | QA-016 |
| ISS-036 | Có system/background actor nào không? | Scope | Major | Phase 2 | Closed | QA-017 |
| ISS-037 | User tự xóa tài khoản — data xử lý thế nào? | Business rule | Major | Phase 2 | Closed | QA-018 |
| ISS-038 | Ban user — ai có quyền, phạm vi, appeal system? | Permission | Blocker | Phase 2 | Closed | QA-019, QA-020, QA-021 |
| ISS-039 | Group moderation toggle & quan hệ với system moderation | Business rule | Major | Phase 2 | Closed | QA-016 |
| ISS-GRP-01 | Public vs Private Group — deep dive | Business rule | Blocker | Phase 4 — GRP backlog | Open | — |
| ISS-GRP-02 | Chi tiết flow post trong group | Business rule | Blocker | Phase 4 — GRP backlog | Open | — |
| ISS-REWD-01 | Badge criteria & award conditions (full list) | Business rule | Blocker | Phase 5 — M12 | Closed | QA-194, QA-195 |
| ISS-REWD-02 | Warn level → trust/reputation display penalty | Business rule | Major | Phase 5 — M12 | Closed | QA-199 |
| ISS-ADMN-01 | Ngưỡng warn count để AI escalate | Business rule | Major | Phase 4 — ADMN backlog | Open | — |
| ISS-AI-01 | AI Moderation confidence threshold calibration | Business rule | Blocker | Phase 6 — AI backlog | Open | — |
| ISS-040 | Search: semantic hay full-text? entity nào được search? | Scope | Major | Phase 3 | Closed | QA-022 |
| ISS-041 | Chat: chỉ DM hay bao gồm Group Chat? | Scope | Major | Phase 3 | Closed | QA-023 (AMENDED Phase 5 — "within Group" scoping corrected, see ISS-163) |
| ISS-042 | AI Layer (M13): Should hay Must? | Priority | Blocker | Phase 3 | Closed | QA-024 |
| ISS-043 | OAuth provider? Account linking strategy? | Scope | Major | Phase 4 | Closed | QA-026 |
| ISS-044 | Post content types? Rich text format? Soft delete? Moderation states? Scan policy? | Scope | Blocker | Phase 4 | Closed | QA-025, QA-027, QA-028, QA-029, QA-030, QA-031 |
| ISS-045 | Comment nesting — bao nhiêu cấp? | Scope | Major | Phase 4 | Closed | QA-032 |
| ISS-046 | Classification depth — category/topic/tag? grade_level logic? | Scope | Major | Phase 4 | Closed | QA-033, QA-034 |
| ISS-047 | Search scope — entity nào support semantic/FTS/trigram? comment có search không? | Scope | Major | Phase 4 | Closed | QA-035, QA-036, QA-037 |
| ISS-048 | Leaderboard — chu kỳ, filter, scope? | Scope | Major | Phase 4 | Closed | QA-038, QA-039 |
| ISS-049 | Reward system — points tính theo gì? badge loại nào? | Scope | Major | Phase 4 | Closed | QA-040, QA-041 |
| ISS-050 | Report categories — loại nội dung vi phạm? | Scope | Minor | Phase 4 | Closed | QA-042 |
| ISS-051 | Follow scope — user/topic/post/group? | Scope | Major | Phase 4 | Closed | QA-043 |
| ISS-052 | Private group — visibility, join flow, custom question? | Business rule | Blocker | Phase 4 | Closed | QA-044, QA-045 |
| ISS-053 | Chat architecture — transport? pub/sub model? | Technical | Major | Phase 4 | Closed | QA-046 |

## Phase 5 — M01: Authentication & Account

| ID | Summary | Category | Priority | Phase | Status | QA Ref |
|----|---------|----------|----------|-------|--------|--------|
| ISS-054 | Registration flow + @mention system | Scope | Blocker | Phase 5 | Closed | QA-048–QA-056 |
| ISS-055 | Session management (JWT + refresh token + multi-device) | Technical | Major | Phase 5 | Closed | QA-057–QA-058 |
| ISS-056 | Password change + forgot password flow | Business rule | Major | Phase 5 | Closed | QA-059–QA-061 |
| ISS-057 | Account state machine (4 states + verify_level) | Business rule | Blocker | Phase 5 | Closed | QA-062–QA-066 |

---
## Phase 5 — M02: User Profile

| ID | Title | Status | Decision |
|----|-------|--------|----------|
| ISS-058 | Avatar: CDN, file types, size limit | Closed | Cloudinary; JPEG/PNG/WebP; max 10MB; no GIF |
| ISS-059 | Followers/Following visibility | Closed | Show count + full list to all users |
| ISS-060 | Username change history on profile | Closed | Not shown; no history table in v1 |
| ISS-061 | Bio char limit + profile URL | Closed | Bio 155 chars (DB 255); /u/{username} dual-context |

---
## Phase 5 — M03: Post & Content

| ID | Title | Status | Decision |
|----|-------|--------|----------|
| ISS-062 | Editor extensions (Tiptap) | Closed | Bold/italic/heading/list/code/LaTeX/table/blockquote/link+label; no inline image |
| ISS-063 | Post types | Closed | 1 type only (no post_type field); poll as separate table |
| ISS-064 | Post status flow | Closed | publish_state(6) + mod_state(3) + lock_level + locked_by |
| ISS-065 | Attachments | Closed | Images 5MB×10; Docs 20MB×3; JPEG/PNG/WebP + PDF/DOCX/XLSX/PPTX |
| ISS-066 | Edit history | Closed | Post: full history; Comment: edited_at only |
| ISS-067 | Poll details | Closed | min2/max10 options; 3 config flags; expires_at required; closed=permanent |
| ISS-068 | Pre-scan flow | Closed | Submit→PENDING→AI scan; flag=stay PENDING; mod approve/reject |
| ISS-069 | Soft delete | Closed | 7-day recovery window; author can restore; cron hard delete after |

---
## Phase 5 — M04: Comment

| ID | Title | Status | Decision |
|----|-------|--------|----------|
| ISS-070 | Comment editor | Closed | Bold/italic/inline-code/LaTeX/link/@mention/blockquote; no heavy extensions |
| ISS-071 | Threading depth | Closed | 2 levels (root + child); reply-to-child appends to same thread |
| ISS-072 | Reactions | Closed | Upvote only; no downvote |
| ISS-073 | Sort order | Closed | Top (default) / Mới nhất / Cũ nhất; child always chronological |
| ISS-074 | Edit/Delete | Closed | Edit unlimited; delete permanent; root tombstone if has replies |
| ISS-075 | Soft delete | Closed | No — delete is permanent |
| ISS-076 | Attachments | Closed | Not supported |
| ISS-077 | @Mention + notification | Closed | Uses M01 logic; always triggers notification |
| ISS-078 | Quote-reply | Closed | Auto-insert blockquote on Reply click |

---
## Phase 5 — M05: Topic & Tag

| ID | Title | Status | Decision |
|----|-------|--------|----------|
| ISS-079 | Topic vs Tag distinction | Closed | Topic = structured taxonomy; Tag = free hashtag |
| ISS-080 | Topic taxonomy | Closed | 11 topics, flat |
| ISS-081 | AI suggest topic flow | Closed | Button-triggered, max 3 suggested, is_stale handling |
| ISS-082 | Tag creation + limits + trending | Closed | Max 5 tags/post, 30 chars/tag, rolling trending window |
| ISS-083 | Topics per post limit | Closed | Min 1, max 3 |
| ISS-084 | Topic/tag edit/merge/delete | Closed | Topic: mod/admin edit+merge, no delete. Tag: free, soft-delete only for crisis |

---
## Phase 5 — M06: Search

| ID | Title | Status | Decision |
|----|-------|--------|----------|
| ISS-085 | Search scope (entities) | Closed | Post(semantic)+User+Tag+Topic+Group(pg_trgm); no Comment. Supersedes Phase 3 partial scope (Topic+Group added) |
| ISS-086 | Semantic search UX / trigger | Closed | Post=submit-only; User/Tag/Topic/Group=debounce+submit |
| ISS-087 | Ranking | Closed | final_score = relevance×0.8 + engagement×0.2 |
| ISS-088 | Filter kết quả | Closed | Topic, Tag, date range, Following-only, Sort |
| ISS-089 | Full-text fallback | Closed | Postgres FTS + unaccent + pg_trgm |
| ISS-090 | Autocomplete/suggestion | Closed | User/Tag/Topic/Group prefix match only |
| ISS-091 | Tìm không dấu | Closed | Solved via unaccent (merged with ISS-089) |
| ISS-092 | Search history | Closed | localStorage, max 10, clear button |
| ISS-093 | Kết quả hiển thị tabs vs mixed | Closed | Mixed 1 page; Post primary, User/Tag/Topic/Group supplementary |
| ISS-094 | Highlight/snippet | Closed | No highlight; plain ~150 char snippet |
| ISS-095 | Search permission | Closed | Guest normal search; private group content gated to members; private group entity visible-but-gated |
| ISS-096 | Rate limiting | Closed | Guest 30/10, User 45/20 (debounce/submit per min) |
| ISS-097 | Pagination | Closed | Infinite scroll, 15/load, max 120 total, cursor-based |

---
## Phase 5 — M07: Notification

| ID | Title | Status | Decision |
|----|-------|--------|----------|
| ISS-098 | Notification triggers + channel (in-app/email) | Closed | Full event list; email limited to security/ban; upvote batched 5min window |
| ISS-099 | In-app UI (bell/page, mark read) | Closed | Bell dropdown+page; separate Message icon for chat; click-to-read |
| ISS-100 | Email trigger timing | Closed | Real-time UX, but async via queue table + cron scan every 1min |
| ISS-101 | Notification preferences | Closed | No global category toggle; per-post mute + per-conversation chat mute + global chat toggle |
| ISS-102 | Real-time delivery mechanism | Closed | DB write = source of truth; WebSocket best-effort push; no cron retry needed for in-app [Amended: thông báo dùng SSE thay WebSocket — DEC-135/QA-257] |
| ISS-103 | Notification retention | Closed | No retention policy — kept indefinitely |

---
## Phase 5 — M08: Moderation

| ID | Title | Status | Decision |
|----|-------|--------|----------|
| ISS-104 | Report entities + reasons | Closed | Post(8)/Comment(7)/User(2)/Group(4); login required; evidence max3 images; desc required only for "Khác" |
| ISS-105 | Report flow (queue, priority, notify) | Closed | Priority=MAX severity+count×2; claim-based 30min timeout; reporter vague outcome, offender detailed reason |
| ISS-106 | Duplicate report handling | Closed | Grouped by target while OPEN into 1 case; individual data preserved; resolved→new case; mod sets resolution_reason independently |
| ISS-107 | AI auto-scan for Comment | Closed | Post-scan (not pre-scan), velocity-triggered (placeholder threshold), scans whole thread, re-scan on edit+next trigger |
| ISS-108 | Warning issuance trigger | Closed | AI auto-warn (high confidence); mod queue (low confidence); mod can also issue independently; ban always human |
| ISS-109 | Probation period restrictions | Closed | LIGHT 7d/none; MEDIUM 10d/no-post; HEAVY 15d/no-post-comment+downrank; status fully private |
| ISS-110 | Ban types | Closed | Temp (30d→90d→permanent escalation) + Permanent (manual); 2 separate mod buttons |
| ISS-111 | Moderation audit log | Closed | Admin full access; mod own-actions only; appeal-review exception for cross-mod visibility |
| ISS-112 | False/malicious report handling | Closed | target_concentration metric (90-day window), mod discretion only, no auto-punish |

---
## Phase 5 — M09: Appeal

| ID | Title | Status | Decision |
|----|-------|--------|----------|
| ISS-113 | Appeal submission content | Closed | Message required + evidence optional (max 3 images/5MB) |
| ISS-114 | Banned user access to appeal | Closed | Still login normally; locked screen + appeal button; all endpoints blocked except appeal submit |
| ISS-115 | Appeal deadline | Closed | Warning=probation duration; Temp ban=ban duration; Permanent ban=90 days |
| ISS-116 | Appeal review flow/queue | Closed | Separate queue from report; Ban>Warning priority; claim-based; own-actions auto-hidden; sole-mod escalates to admin |
| ISS-117 | Appeal outcome reversal | Closed | Ban→ACTIVE immediately (log kept, overturned flag); Warning→restriction lifted + warn count decremented |
| ISS-118 | Repeat appeal allowed? | Closed | No — one appeal per action, rejected appeals cannot be resubmitted |

---
## Phase 5 — M10: Admin Panel

| ID | Title | Status | Decision |
|----|-------|--------|----------|
| ISS-119 | Admin-exclusive vs shared-with-mod scope | Closed | Admin: role mgmt, config, full audit, mod account mgmt. Shared: report/warn/ban/appeal, topic/tag actions. Policy values hardcoded |
| ISS-120 | Role management flow | Closed | Promote=proposal+accept/decline; Demote=direct, no appeal |
| ISS-121 | System config options | Closed | AI toggle, maintenance mode, registration toggle, feature flags, announcement banner |
| ISS-122 | AI toggle granularity | Closed | Master toggle + per-module (Search/Moderation/Topic) |
| ISS-123 | Admin action audit | Closed | Logged, append-only, admin view-only (no edit/delete) |

---
## Phase 5 — M13: AI Layer

| ID | Title | Status | Decision |
|----|-------|--------|----------|
| ISS-124 | Embedding model | Closed | text-embedding-3-small, pgvector storage, HNSW index |
| ISS-125 | Topic suggestion model | Closed | GPT-4o-mini |
| ISS-126 | Moderation category mapping | Closed | AI covers harassment/hate/sexual/violence only; spam/plagiarism/misinfo manual-only |
| ISS-127 | Confidence threshold for auto-warn/auto-reject | Closed | Symmetric 2-branch (Content Gate + Warning), 0.9/0.5 shared thresholds, placeholder pending tuning |
| ISS-128 | AI failure/timeout handling | Closed | Distinguish admin-off (module fallbacks) vs transient failure (timeout 5s/10s, 1 retry w/2s delay, then per-module degradation) |
| ISS-129 | AI call rate limiting | Closed | Reuse existing limits (search); add 10/min/user for Topic Suggest button only |

---
## Phase 5 — M11: Group

| ID | Title | Status | Decision |
|----|-------|--------|----------|
| ISS-130 | Group creation — ai tạo được, giới hạn gì? | Closed | Mọi user login tạo tự do; rate limit 5 group/ngày/user; không giới hạn tổng sở hữu |
| ISS-131 | Role permissions — Owner/Group Mod/Member cụ thể? | Closed | Full matrix: Owner full quyền; Group Mod duyệt pre-mod/ẩn-xóa content/kick Member (không kick Mod khác); Member chỉ tương tác |
| ISS-132 | Join flow — public/private, join question | Closed | Public+no-question=join ngay; còn lại cần duyệt Owner/Mod theo câu trả lời; reject cho gửi lại ngay, không cooldown; block riêng cho spam |
| ISS-133 | Group content moderation quan hệ M08 system-wide | Closed | System Mod/Admin vẫn giám sát qua Report + can intervene anytime; publish gate riêng: ≥0.9 auto-reject, 0.5-0.9 bắt buộc Group Mod xử lý, <0.5 theo pre-mod toggle |
| ISS-134 | Group deletion (Owner xóa) / member rời group | Closed | Xóa group: soft-delete, reputation giữ trừ point content-tied bị mất; Member rời/kick: post giữ nguyên là tài sản group, point không đổi |
| ISS-135 | Anonymous posting trong group — cơ chế cụ thể | Closed | User tự chọn ẩn danh từng post (không bắt buộc toàn bộ); tắt toggle không de-anonymize post cũ; Group Mod/Owner thấy real identity (giống DEC-004/005) |
| ISS-136 | Group size limit — số group tối đa/user | Closed | Không giới hạn join lẫn sở hữu |
| ISS-137 | Owner rời/mất khả năng thao tác — ownership succession | Closed | Rời tự nguyện: bắt buộc chỉ định successor; involuntary: auto-promote Mod active senior nhất → Member senior nhất → xóa group nếu chỉ còn Owner |
| ISS-138 | Đổi visibility Public↔Private — post cũ trên feed | Closed | Post đã hiện thì giữ hiện (khóa tương tác nếu Private), query mới loại trừ non-member |
| ISS-139 | Group-level moderation có qua Appeal (M09) không | Closed | Không — quyết định Group Mod/Owner là cuối cùng |
| ISS-140 | Private group discovery & ai được invite | Closed | Ẩn khỏi search, chỉ qua invite/link; mọi member đều invite được, dùng lại join flow ISS-132 |
| ISS-141 | Group post cross-post ra main feed | Closed | Luôn hiện feed member group; Public group thêm hiện main feed; Private không bao giờ |

---
## Phase 5 — M09: Appeal (Amendment — Content Deletion Appeal)

| ID | Title | Status | Decision |
|----|-------|--------|----------|
| ISS-144 | Mở rộng Appeal scope: khiếu nại content bị xóa (chỉ Post) | Closed | Amend Phase 2 decision (trước đây chỉ Warning+Ban). Thêm loại appeal mới "Content Deletion Appeal", CHỈ áp dụng Post (không Comment). Deadline 30 ngày. Queue riêng, tái dùng claim-based 30 phút. Priority thấp nhất (Ban > Warning > Content Deletion). Thành công → khôi phục content + hoàn point + đảo ngược warn/ban đi kèm (nếu có) |

---
## Phase 5 — M12: Gamification | Status: CLOSED ✓

| ID | Title | Status | Decision |
|----|-------|--------|----------|
| ISS-142 | Content-tied point deduction — trường hợp nào trừ, thời điểm nào | Closed | Trừ nếu trực tiếp (tự xóa content của mình, hoặc bị Mod/Admin xóa do vi phạm của chính content đó); giữ nguyên nếu gián tiếp (group bị xóa, comment cascade theo post cha bị xóa). Thời điểm: tự xóa → trừ sau khi hết soft-delete (hard-delete xong); Mod/Admin xóa vi phạm → trừ ngay. Sửa lại ngoại lệ group trong DEC-105 (group deletion nay KHÔNG trừ điểm nữa) |
| ISS-143 | Badge: permanent hay revocable? Audit trail thế nào? | Closed | Badge vĩnh viễn, không thu hồi dù điểm sau giảm dưới ngưỡng (badge = cột mốc lịch sử, không phải chỉ số sống). Badge theo ngưỡng điểm: audit 1 lần (ngày đạt đầu tiên). Danh hiệu periodic top-N: audit nhiều lần (mỗi chu kỳ thắng 1 bản ghi) |
| ISS-REWD-01 | Danh sách badge đầy đủ + tiêu chí | Closed | Chỉ badge theo tổng điểm (không theo số bài/chủ đề). 5 mốc: Người mới nổi (25) / Cây bút triển vọng (100) / Cây bút tích cực (300) / Chuyên gia cộng đồng (600) / Huyền thoại iShare (1000). Chỉ hiện sau khi đạt, không hiện tiến độ |
| ISS-145 | Post Star vs Comment Star — trọng số cụ thể | Closed | Post Star = 2, Comment Star = 1 |
| ISS-146 | Periodic top-N title — chu kỳ nào, N bao nhiêu | Closed | Chỉ Weekly ("Ngôi sao tuần"), N=3. Nếu hòa ở hạng cắt thì tất cả cùng nhận (N là tối thiểu, không cắt cứng) — xem ISS-152 |
| ISS-152 | Tie-break ở hạng cắt N=3 cho top-N title | Closed | Cho tất cả user hòa ở hạng cắt đều nhận title, không cần tie-break riêng |
| ISS-REWD-02 | Warn level ảnh hưởng gì đến leaderboard/reputation display | Closed | HEAVY bị ẩn hoàn toàn khỏi leaderboard trong suốt probation (exception có chủ đích, amend DEC-079). Không áp dụng MEDIUM/LIGHT — xem DEC-118 |
| ISS-147 | Upvote rút lại được không, điểm xử lý ra sao | Closed | Vote là toggle, rút lại được, điểm trừ ngay lập tức khi rút |
| ISS-148 | Tự vote nội dung của chính mình có được phép không | Closed | Không cho phép — nút vote bị ẩn/disable trên chính content của tác giả |
| ISS-149 | Leaderboard ranking tính real-time hay batch | Closed | 1 cron job duy nhất, chạy mỗi 60 phút — vừa refresh hiển thị, vừa kiểm tra/finalize chu kỳ vừa đóng bằng query chính xác theo mốc thời gian (không phụ thuộc cache) |
| ISS-150 | Tie-break khi 2 user bằng điểm trên leaderboard | Closed | Đồng hạng (giống xếp hạng thể thao), người tiếp theo nhảy số hạng |
| ISS-151 | Badge chưa đạt có hiện tiến độ không | Closed | Không — chỉ hiện badge sau khi đã đạt |
| ISS-153 | Có cho xem lại leaderboard các chu kỳ trước không | Closed | Không — chỉ hiển thị trạng thái hiện tại của Weekly/Monthly/All-time. Lịch sử title/badge vẫn giữ qua audit trail riêng |
| ISS-154 | Banned account — hiển thị trên leaderboard/profile/post/comment ra sao | Closed | Ẩn khỏi leaderboard trong thời gian bị ban (nhất quán HEAVY, amend DEC-079 → DEC-122). Profile/post/comment vẫn hiển thị bình thường nhưng có nhãn "Tài khoản đã bị khóa" ở mọi nơi tên họ xuất hiện |

---

## Phase 5 — M16: Chat & Messaging | Status: Deep-dive substantially complete (OPEN-003 pending)

| ID | Title | Status | Decision |
|----|-------|--------|----------|
| ISS-155 | Trạng thái tin nhắn ("Đã gửi"/"Đã xem") — lưu trữ và cơ chế cập nhật thế nào? | Closed | Không lưu enum trạng thái trên message — "đã xem" là quan hệ tin nhắn↔người đọc, suy ra từ `last_read_message_id` (FK tới message, không dùng timestamp để tránh clock-skew) lưu trên bảng thành viên conversation (`conversation_members`), update qua `GREATEST()` để chống race condition. UI chỉ hiện 2 trạng thái tính toán (không lưu DB): "Đã gửi" (default) / "Đã xem" (chỉ ở tin nhắn MỚI NHẤT, không rải theo lịch sử). Mark-as-read trigger: mở conversation, hoặc tin mới tới khi đang mở + tab đang focus (Page Visibility API) + đang ở đáy danh sách (IntersectionObserver trên sentinel cuối) — nếu đang cuộn đọc tin cũ thì không tự cuộn, hiện badge "tin nhắn mới" thay vì auto mark-as-read. Debounce ~500ms–1s trước khi gọi API để tránh spam khi tin dồn dập. Group chat: hiện avatar từng thành viên đã đọc kịp tin mới nhất ngay dưới tin đó (Messenger-style); thành viên chưa đọc kịp thì không hiện gì. Read-receipt cập nhật realtime cho các thành viên khác qua SSE broadcast (`event: read_receipt`), tái dùng pub/sub `Map<chatId, Set<SSEConnection>>` đã có (QA-046) — không mở kết nối riêng. |
| ISS-158 | Tin nhắn có cho sửa/xóa sau khi gửi không? | Closed | Sửa: KHÔNG cho phép sửa nội dung tin nhắn sau khi gửi. Xóa: cho phép, soft-delete kiểu tombstone — nội dung gốc bị xóa hẳn (không giữ lại kể cả cho mod xem, khác Post/Comment vì chat là kênh riêng tư), thay bằng placeholder "Tin nhắn đã bị thu hồi" tại đúng vị trí trong luồng chat. Giới hạn thời gian thu hồi: 5 phút kể từ lúc gửi (`now() - created_at <= 5 minutes`). Chỉ có đúng 1 kiểu xóa — thu hồi cho CẢ 2 phía cùng lúc, không có tùy chọn "xóa chỉ ở phía tôi". Sau 5 phút, tin nhắn không còn cách nào xóa/ẩn được nữa — vĩnh viễn, nhất quán với nguyên tắc "không cho sửa". |
| ISS-159 | Tin nhắn hỗ trợ nội dung gì — chỉ text, hay thêm emoji/đính kèm ảnh-file? | Closed | Text + emoji cho MS1. Đính kèm ảnh/file: ngoài phạm vi MS1, để mở rộng ở phase sau. Không có AI Moderation quét nội dung chat (khác Post/Comment) — chat là kênh riêng tư 1-1/nhóm nhỏ, không thuộc phạm vi kiểm duyệt như nội dung công khai. |
| ISS-160 | Không có AI Moderation, chat cũng chưa nằm trong Report system (M08) — vậy harassment/quấy rối qua DM xử lý bằng cách nào? | **Open** → OPEN-003 | Đã cân nhắc 2 hướng: (A) Report tin nhắn — tái dùng M08, nhưng chỉ xử lý được sau (delay chờ mod), không ngăn được tin nhắn tiếp tục trong lúc chờ xử lý; (B) Block — kiểm soát tức thời nhưng phát sinh câu hỏi scope (level nào, có ảnh hưởng content/leaderboard/group chat không). Quyết định cuối: KHÔNG làm Block, KHÔNG làm Report cho tin nhắn ở MS1 — chấp nhận đánh đổi, để dành xử lý ở phase sau. Không phải Blocker cho việc viết spec M16 vì đây là quyết định defer có chủ đích của stakeholder, không phải unknown. |
| ISS-161 | Rate limiting cho chat — có cần giới hạn số tin/phút không, mức nào? | Closed | Có — 30 tin nhắn/phút, tính theo từng cặp (người gửi, conversation). Mục đích: chặn spam script/bot (không phải giới hạn chi phí AI như Search, vì chat không gọi AI), bảo vệ tài nguyên server, và là lớp chặn kỹ thuật tối thiểu cho vấn đề chưa có Block/Report (OPEN-003). 30 tin/phút = nhanh hơn tốc độ gõ tự nhiên của người thật, không cản trở use case hợp lệ. |
| ISS-162 | Ai nhắn tin (DM) được cho ai — mở hoàn toàn, cần mutual follow, hay message request như Messenger? | Closed | Mở hoàn toàn — bất kỳ user nào (đã login) cũng nhắn DM được cho bất kỳ user nào khác, không cần điều kiện gì trước (không cần follow, không có "message request" riêng). Làm rộng thêm phạm vi rủi ro ở OPEN-003 (người lạ hoàn toàn cũng nhắn được) nhưng đã có rate limit ISS-161 làm lớp chặn tối thiểu. |
| ISS-163 | Group Chat có phải là kênh gắn liền với Group (M11) không? | Closed | KHÔNG — correction so với scoping ban đầu ở QA-023 (Phase 3 ghi nhầm "Group Chat within Group"). Group Chat là 1 loại conversation multi-party (3+ người) hoàn toàn độc lập, không liên quan gì tới Group/cộng đồng ở M11 — bất kỳ user nào cũng tạo được, không phụ thuộc việc có chung Group nào không. Đã sửa lại module-registry.md: bỏ dependency M16→M11, sửa Notes của cả M11 và M16. |
| ISS-164 | Group Chat — cơ chế quản trị: role, add/remove member, đổi tên, kiểm duyệt, rời nhóm, kế nhiệm Admin, giới hạn size? | Closed | Follow: mở, không cần follow trước (giống DM, ISS-162). Role: Admin (người tạo) + Member thường. Add/remove: Member chỉ add được người khác, KHÔNG xóa được ai; chỉ Admin xóa được thành viên. Toggle kiểm duyệt do Admin bật/tắt — bật thì add thành viên mới cần Admin duyệt (chỉ Admin duyệt, Member không duyệt được). Đổi tên nhóm: mọi thành viên đều đổi được. Rời nhóm: tự do, tách biệt hoàn toàn với việc bị Admin xóa. Admin rời: bắt buộc chủ động chuyển quyền quản trị cho người khác trước khi rời (không có auto-promote tự động như Owner ở Group M11/ISS-137 — là hành động chủ động của Admin, không phải hệ thống tự làm). Giới hạn: 100 thành viên/Group Chat. |
| ISS-165 | Notification cho tin nhắn mới (email?) và pagination lịch sử chat? | Closed | Email: KHÔNG gửi email cho tin nhắn mới — chỉ in-app (khớp mặc định đã chốt ở QA-124, không thêm ngoại lệ cho chat). Pagination: infinite scroll lên trên, 20 tin/lần load, cursor-based theo `message_id` (nhất quán pattern Search QA-097). Khác Search: KHÔNG giới hạn tổng số tin tối đa tải được — user phải cuộn được tới tận tin nhắn đầu tiên của conversation, không có khái niệm "hết liên quan" như search result. |

## Phase 5 — M14: Feed & Discovery | Status: CLOSED ✓

| ID | Title | Status | Decision |
|----|-------|--------|----------|
| ISS-166 | Guest (chưa đăng nhập) xem feed gì? | Closed | Guest xem đầy đủ Newest + Trending (3 sub); tab Following/Group vẫn hiện nhưng cần login mới xem nội dung; mọi tương tác (upvote/report...) cần login (nhất quán QA-011). Mặc định guest vào tab Trending |
| ISS-167 | Personalized Home Feed ranking dựa trên tín hiệu nào? | Closed — N/A | Không còn tab thuật toán cá nhân hóa riêng (xem ISS-168) nên không cần định nghĩa ranking signal |
| ISS-168 | M14 cần những tab/view nào cho Feed? | Closed | 4 tab: Trending (sub Post/Topic/Tag) + Following + Group + Newest. Không có tab "For You" thuật toán riêng |
| ISS-169 | Tab Following rỗng (chưa follow ai/gì) hiện gì? | Closed | Empty state + CTA dẫn sang trang Search (tìm User/Topic/Post) — đúng phạm vi 3 loại follow target, khác Trending có cả Tag (không follow được) |
| ISS-170 | AI-off fallback cho Personalized Home Feed? | Closed — N/A | Không còn tab cá nhân hóa cần AI (xem ISS-168, ISS-186) |
| ISS-171 | Trending Section có tái dùng công thức QA-106/DEC-052 không? | Closed — superseded by ISS-185 | Trending Topic/Tag giữ nguyên DEC-052; Trending Post là khái niệm mới, xem ISS-185 |
| ISS-172 | Trending Post có filter theo Topic không? | Closed | Không — chỉ 1 danh sách global duy nhất (đã có Trending Topic/Tag riêng để lọc theo chủ đề) |
| ISS-173 | Bài Group Public cross-post có tính vào Newest/Trending Post không? | Closed | Tính vào Trending Post và tab Group; KHÔNG tính vào Newest (Newest giữ thuần nội dung không-thuộc-group) |
| ISS-174 | Cơ chế phân trang cho 4 tab? | Closed | Infinite scroll, cursor-based, 20 bài/lần load, áp dụng cả 4 tab. Cần SSR cho batch đầu (SEO cho Guest, nhắc lại Phase 7) — **[Amended: SSR hoãn ở MS1 theo DEC-134/QA-256, ghi OPEN-006]** |
| ISS-175 | Có ngưỡng tối thiểu để vào Trending không? | Closed | Không đặt ngưỡng cho MS1 (dataset nhỏ). Có thể bổ sung sau — provisional |
| ISS-176 | Trending có loại bài BANNED/HEAVY-warn không? | Closed | Không loại, không chỉnh score — dựa vào label công khai sẵn có (BANNED, QA-205) và nguyên tắc private mặc định (HEAVY warn, DEC-079). Nhất quán DEC-118/122 (ngoại lệ ẩn chỉ áp dụng Leaderboard) |
| ISS-177 | Feed có tự cập nhật real-time khi có bài mới không? | Closed | Không auto-insert. Newest/Following/Group dùng banner "có bài mới" (polling), bấm vào chỉ prepend (giữ vị trí cuộn). Trending không cần banner — tự refresh theo chu kỳ decay recalculation (15-30 phút). Giữ polling, không chuyển real-time (tránh phức tạp filter cá nhân hóa theo follow/membership per-connection) |
| ISS-185 | Trending Post dùng công thức/decay nào? | Closed | DEC-124 — exponential half-life decay 7 ngày: `weight=0.5^(age_days/7)`, cắt hẳn sau 28 ngày (4 tuần). Trending Topic/Tag không đổi (DEC-052) |
| ISS-186 | M14 có còn phụ thuộc M13 (AI Layer) không? | Closed | Bỏ dependency M13 cho scope hiện tại (chỉ còn M03, M05). Có thể tái thêm nếu mở rộng AI personalization sau MS1 |
| ISS-187 | Có nên thêm tab Group (feed tổng hợp từ group đã join) không? | Closed | Có — thêm tab thứ 4 "Group", tổng hợp bài từ mọi group (Public+Private) user đã join, chronological |
| ISS-188 | Tab Group hiện/ẩn thế nào? | Closed | Luôn hiện cho user đã login (Guest thấy tab nhưng gate). Chưa join group nào → empty state + CTA "Khám phá Group" |

## Phase 5 — M15: Analytics & Stats | Status: CLOSED ✓

| ID | Title | Status | Decision |
|----|-------|--------|----------|
| ISS-178 | M15 Analytics & Stats — ai truy cập được, ADMIN-only hay mở thêm cho MOD? | Closed | Chỉ ADMIN truy cập cả 3 dashboard. Cân nhắc mở Moderation Stats cho MOD (kèm ý tưởng bảng Top-N MOD xử lý nhiều report nhất) nhưng lọc số liệu cá nhân hóa theo MOD làm tăng độ phức tạp, trong khi module là Could-priority — bỏ hẳn, giữ ADMIN-only |
| ISS-179 | User Stats dashboard gồm những chỉ số nào? | Closed | Tổng theo trạng thái tài khoản (ACTIVE/DEACTIVATED/BANNED) · trend đăng ký mới theo thời gian · theo vai trò (USER/MOD/ADMIN) · theo Lớp/Khối (grade_level) · theo mức warn (Clean/LIGHT/MEDIUM/HEAVY/BANNED). Không thêm DAU/WAU/MAU (cần activity-log infra mới, không tận dụng dữ liệu sẵn có) |
| ISS-180 | Content Stats dashboard gồm những chỉ số nào? | Closed | Tổng Post theo publish_state · breakdown mod_state (pending/active/under_review/removed) · trend bài đăng mới theo thời gian · phân bố theo Topic · trend Comment theo thời gian. Bỏ tỉ lệ Group-post/độc lập và tỉ lệ ẩn danh (không cần thiết, thêm nhiễu) |
| ISS-181 | Moderation Stats dashboard gồm những chỉ số nào? | Closed | Tổng Report theo trạng thái + category (5 category + Khác, ISS-050) · Warn issued theo level theo thời gian · Ban/Unban theo thời gian · Appeal theo loại + outcome |
| ISS-182 | Filter thời gian cho cả 3 dashboard — custom range hay preset? | Closed | Preset: Hôm nay / 7 ngày / 30 ngày / Toàn thời gian. Không có custom date range picker cho MS1 |
| ISS-183 | Cách tính toán — real-time query hay batch/cache? | Closed | Real-time query mỗi lần load (COUNT/GROUP BY đơn giản), không cache/batch — khác Leaderboard (M12) vốn cần batch vì ranking/tie-break phức tạp; lượng truy cập admin thấp hơn nhiều so với user thường nên không tạo áp lực hệ thống |
| ISS-184 | Có export dữ liệu (CSV) không? | Closed | Không làm cho MS1 — **OPEN-004**, để ngỏ xem xét lại sau khi các module core hoàn thiện |

## Phase 6 — Cross-cutting Concerns | Status: CLOSED ✓

| ID | Title | Status | Decision |
|----|-------|--------|----------|
| ISS-189 | Timezone & date handling — lưu trữ/tính toán theo múi giờ nào? | Closed | Lưu UTC trong DB; mọi ranh giới ngày/tuần (leaderboard reset, appeal deadline, warn probation, preset M15, soft-delete window...) và hiển thị UI quy về Asia/Ho_Chi_Minh (UTC+7, cố định, không DST) |
| ISS-190 | i18n/localisation — site có cần hỗ trợ ngôn ngữ nào ngoài tiếng Việt không? | Closed | Vietnamese-only ở MS1, nhưng kiến trúc i18n-ready (string qua i18n key, locale `vi` duy nhất, không có language switcher). Content đa ngôn ngữ (dịch/tag nội dung theo ngôn ngữ) là ý tưởng mở, không thuộc scope MS1 |
| ISS-191 | Data retention tổng quát — audit log và chat message có cần policy xóa/lưu trữ gì không? | Closed | Giữ vĩnh viễn, không hard-delete/archive — nhất quán Notification (DEC-071). Nguyên tắc chung: chỉ hard-delete khi thật sự an toàn (có lý do rõ ràng — privacy/PII hoặc dọn rác content do user chủ động xóa có UX hợp lý — VÀ không phá referential integrity với bảng khác tham chiếu). Post/Comment/Account hard-delete đã chốt trước đó không đổi |
| ISS-192 | File/media upload — có cần cơ chế scan virus/malware không? | Closed | Không scan riêng — chỉ giữ whitelist type/size đã có (ảnh JPEG/PNG/WebP). Dựa vào CDN (Cloudinary) tự transcode ảnh khi upload, đủ an toàn cho MS1 |
| ISS-193 | AI — nội dung user gửi ra OpenAI (3rd party) có cần xử lý gì về privacy không? | Closed | Thêm trang Privacy Policy/ToS công khai, nêu rõ nội dung đăng công khai (post/comment) được xử lý bởi dịch vụ AI bên thứ 3 (OpenAI) cho mục đích kiểm duyệt (Moderation API) và tìm kiếm ngữ nghĩa (Embedding). Link ở footer/registration flow |
| ISS-194 | AI — Topic Suggestion (GPT-4o-mini) trả về ngoài danh sách 11 topic hợp lệ thì xử lý sao? | Closed | Validate output theo whitelist 11 topic; không khớp → coi như suggestion fail, hiển thị non-blocking error ("Không thể gợi ý chủ đề, vui lòng chọn thủ công") + user tự chọn — dùng chung đúng UX pattern với AI transient-failure (DEC-099) |
| ISS-195 | AI — có cần lưu log raw output (score Moderation, Topic suggestion) để audit/debug không? | Closed | Có — lưu raw response mỗi lần gọi AI (Moderation/Embedding/Topic Suggestion) vào bảng `ai_decision_log` riêng, gắn với post/comment liên quan. Phục vụ debug/tinh chỉnh threshold 0.9/0.5 (placeholder, DEC-098) và làm cơ sở xử lý Content Deletion Appeal (M09) |
| ISS-196 | Analytics events — có cần hạ tầng event-tracking chung (ngoài 3 dashboard M15) không? | Closed | Không xây cho MS1 — **OPEN-005**, formalize lại quyết định đã ngầm chọn ở M15 (QA-242, từ chối DAU/WAU/MAU) áp dụng chung cho toàn hệ thống. Để ngỏ xem xét sau khi core xong |

## Phase 7 prep — Tech Stack (OPEN-002) | Status: CLOSED ✓

| ID | Title | Status | Decision |
|----|-------|--------|----------|
| ISS-197 | Tech stack — Backend/Frontend framework, và có cần SSR/SEO ở MS1 không? | Closed | Backend: Java + Spring Boot. Frontend: ReactJS (Vite, client-side SPA). MS1 chỉ đảm bảo core — chưa làm SSR/SEO; ghi **OPEN-006**. Next.js đã được cân nhắc (SSR sẵn) nhưng chưa chọn vì team chưa dùng và rủi ro tiến độ. UI Kit dùng chung toàn app (làm sau khi có design): chỉ dùng nội bộ trong application, không phải phần nộp riêng, không thêm scope. Yêu cầu cốt lõi: bộ common UI thống nhất; được phép xây trên thư viện nền có sẵn. Thư viện nền chọn sau khi có design, hiện nghiêng về MUI (chưa chốt) → **OPEN-007** |
| ISS-198 | Kênh realtime — thống nhất SSE hay giữ WebSocket cho thông báo? | Closed | Thống nhất dùng SSE cho cả chat và thông báo; không dùng WebSocket trong app. Đã rà: không có tính năng hai chiều thật sự nào (chat = POST gửi + SSE nhận; feed banner = polling QA-239; AI = request/response). Online/offline (heartbeat ping) được nêu rồi bỏ — không phải yêu cầu |
| ISS-199 | Email — thư viện và nguồn SMTP gửi magic-link / OTP / thông báo bảo mật? | Closed | Spring Mail (`spring-boot-starter-mail`, `JavaMailSender`) + SMTP chuẩn cấu hình bằng biến môi trường; dùng gói miễn phí của một nhà cung cấp email cho MS1, nhà cụ thể chọn lúc triển khai (Gmail SMTP chỉ ở dev). Phạm vi email không đổi (chỉ security/ban + magic-link/OTP theo M07) |
| ISS-200 | Cờ `AI_ENABLED` (DEC-008) — lưu ở đâu: env var hay Admin config? | Closed (đã giải quyết bởi quyết định cũ) | Không cần quyết định mới: DEC-092/093 (M10 Admin Panel) đã chốt System config có AI toggle master + per-module, đổi từ giao diện admin, ghi audit log (DEC-094). Cờ lưu bền để đổi lúc chạy không cần redeploy. Câu hỏi lưu trữ ở DEC-008/OPEN-002 vì thế được đóng |
| ISS-201 | Hosting / deployment cho MS1 | Closed | N/A ở MS1 — không deploy (nhất quán QA-002). Không tạo OPEN vì không có việc nào bị chặn; chọn nhà cung cấp và cách đóng gói (ví dụ Docker) khi thật sự cần deploy. Không có quyết định mới |
| ISS-202 | Ràng buộc học thuật về công nghệ (đóng ISS-029) | Closed | Không có yêu cầu hay hạn chế nào về công nghệ — tự do khi implement. Kỳ vọng chất lượng: đồ án rất nặng về thiết kế hệ thống/nghiệp vụ (thiết kế DB, models, luồng qua từng class, phản hồi...) nên phải làm cực kỳ kỹ — ghi nhận là kỳ vọng chất lượng, cách đáp ứng ở Phase 8/spec đang hỏi tiếp |
| ISS-203 | Xác nhận nhóm công nghệ ngầm định (PostgreSQL+pgvector, Cloudinary, OpenAI, Tiptap, JWT) | Closed | Xác nhận tất cả; công nghệ bổ sung về sau sẽ bàn khi cần. Đóng OPEN-002 (DEC-137) |

## System Requirement prep — Privacy & Consent | Status: IN PROGRESS

| ID | Title | Status | Decision |
|----|-------|--------|----------|
| ISS-204 | Đăng ký tài khoản có bắt buộc đồng ý Privacy Policy/ToS không, và privacy xây dựng thế nào? | Closed (một phần) | Bắt buộc đồng ý mới đăng ký được (DEC-138). Privacy chắc chắn phải có nhưng xây dựng chi tiết sau → **OPEN-008** |

## System Requirement prep — Documentation approach | Status: CLOSED ✓

| ID | Title | Status | Decision |
|----|-------|--------|----------|
| ISS-205 | Cách viết tài liệu System Requirement (SR) theo module: cấu trúc, ngôn ngữ, thời điểm, quy trình Author–Auditor | Closed | Xem DEC-139. Quy ước ID để bàn sau (chốt trước khi chạy thử M05) |
| ISS-206 | Quy ước ID cho tài liệu SR | Closed | Xem DEC-139 (amended): tiền tố `ISH`, `ISH-SR-Mxx`, `ISH-Mxx-nnn[.k]`, `OP-Mxx-nn`, `AUD-Mxx-nn`; ID vĩnh viễn **[Sẽ bị thay thế 2026-10-07 — quy ước ID và quy trình theo skill FR mới, xem DEC-139]** |

---

## Functional Requirement — M05: Topic & Tag | Status: CLOSED ✓

| ID | Title | Status | Decision |
|----|-------|--------|----------|
| ISS-207 | AI Classification có gợi ý Tag không? (draft nói có, QA-017 nói không) | Closed | Xem DEC-140 |
| ISS-208 | Có bước Mod duyệt kết quả gợi ý Topic không? | Closed | Xem DEC-140 |
| ISS-209 | Topic phẳng hay 2 tầng Category → Topic? (QA-033 vs DEC-047) | Closed | Xem DEC-140 |
| ISS-210 | Cho Admin thêm Topic mới vào danh mục và các quy tắc đi kèm | Closed | Xem DEC-141 |
| ISS-211 | Đổi công thức Trending Topic/Tag | Closed | Xem DEC-145, OPEN-009 |
| ISS-212 | Có giữ quyền đổi tên Topic không? | Closed | Xem DEC-141 |
| ISS-213 | Tác giả có đổi Topic, Tag khi sửa bài đã gửi không? | Closed | Xem DEC-142 |
| ISS-214 | Mod/Admin có đổi Topic, Tag trên bài người khác không? | Closed | Xem DEC-142 |
| ISS-215 | "Browse" Topic/Tag có gồm trang liệt kê bài theo Topic/Tag không? | Closed | Xem DEC-142 |
| ISS-216 | Mod/Admin có kích hoạt lại Tag đã vô hiệu hóa được không? | Closed | Xem DEC-143 |
| ISS-217 | Bài nháp có bắt buộc đủ 1–3 Topic không? | Closed | Xem DEC-142 |
| ISS-218 | So trùng tên Topic thế nào? | Closed | Xem DEC-141 |
| ISS-219 | "Topic chưa có bài viết" đếm những bài nào? | Closed | Xem DEC-141 |
| ISS-220 | Sau khi gộp Topic: Topic nguồn và người follow ra sao? | Closed | Xem DEC-141 |
| ISS-221 | Ngưỡng 20 từ của gợi ý Topic đếm thế nào? | Closed | Xem DEC-144 |
| ISS-222 | AI trả về một phần Topic ngoài danh mục thì xử lý sao? | Closed | Xem DEC-144 |
| ISS-223 | Giới hạn 10 lần/phút tính theo cửa sổ nào? | Closed | Xem DEC-144 |
| ISS-224 | Tag: tập ký tự, cách hiển thị, "#" có tính vào 30 ký tự không? | Closed | Xem DEC-143 |
| ISS-225 | Trending tính trên những bài và tương tác nào? | Closed | Xem DEC-145 |
| ISS-226 | Chu kỳ tính lại Trending 15–30 phút: mốc kiểm chứng | Closed | Xem DEC-145 |
| ISS-227 | Trending: mục điểm 0, thứ tự khi bằng điểm | Closed | Xem DEC-145 |
| ISS-228 | Có dùng gợi ý Topic khi sửa bài không? | Closed | Xem DEC-142 |
| ISS-229 | Mod/Admin đổi Topic, Tag bài người khác: có thông báo, có ghi lịch sử sửa bài không? | Closed | Xem DEC-142 |
| ISS-230 | Có ghi nhật ký thao tác Tag/Topic của Mod không? | Closed | Xem DEC-146 |
| ISS-231 | Trang Chính sách quyền riêng tư có nêu việc gửi nội dung bài cho AI gợi ý Topic không? | Closed | Xem DEC-146 |

---

## Functional Requirement — M01: Authentication & Account | Status: CLOSED ✓

| ID | Title | Status | Decision |
|----|-------|--------|----------|
| ISS-232 | Có thông báo sau khi tự liên kết Google không? (DEC-010 có, danh sách sự kiện DEC-065 không có) | Closed | Xem DEC-147 |
| ISS-233 | Bình luận của tài khoản DELETED hiển thị thế nào? (QA-018 vs DEC-019) | Closed | Xem DEC-149 |
| ISS-234 | Mod/Admin có xem được bài bị ẩn và danh tính tác giả đã vô hiệu hóa tài khoản không? | Closed | Xem DEC-150 |
| ISS-235 | Quy tắc mật khẩu | Closed | Xem DEC-148 |
| ISS-236 | Chi tiết quy tắc username, display_name | Closed | Xem DEC-148 |
| ISS-237 | Đăng nhập Google khi email trùng tài khoản email chưa xác minh | Closed | Xem DEC-147 |
| ISS-238 | Hạn 30 ngày của phiên làm mới tính thế nào? | Closed | Xem DEC-151 |
| ISS-239 | Thời hạn vô hiệu hóa 14 ngày tính thế nào? | Closed | Xem DEC-149 |
| ISS-240 | Chi tiết mã kích hoạt lại (OTP) và trang kích hoạt | Closed | Xem DEC-149 |
| ISS-241 | Danh sách gợi ý nhắc tên và thời điểm gửi thông báo nhắc tên | Closed | Xem DEC-153 |
| ISS-242 | Email cảnh báo trước khi tự xóa gửi lúc nào; đặt lại mật khẩu có gửi thông báo "mật khẩu đã đổi" không? | Closed | Xem DEC-149, DEC-151 |
| ISS-243 | Công tắc tạm dừng đăng ký và chế độ bảo trì tác động tới đăng ký, đăng nhập thế nào? | Closed | Xem DEC-152 |
| ISS-244 | Ban tạm thời hết hạn thì tài khoản có tự về ACTIVE không? | Closed | Xem DEC-152 |
| ISS-245 | Đổi username, display_name; dùng lại email, username của tài khoản DELETED | Closed | Xem DEC-148 |
| ISS-246 | Magic link dùng được mấy lần? | Closed | Xem DEC-151 |
| ISS-247 | Nút OK trên màn hình tài khoản bị khóa làm gì? | Closed | Xem DEC-152 |
| ISS-248 | "Quên mật khẩu" với email lạ và với tài khoản không ACTIVE | Closed | Xem DEC-151 |
| ISS-249 | Privacy: danh mục dữ liệu cá nhân và cách trình bày trên trang Privacy Policy | Closed | Xem DEC-154 |
| ISS-250 | Privacy: lưu việc đồng ý và đồng ý lại khi chính sách đổi phiên bản | Closed | Xem DEC-155 |
| ISS-251 | Privacy: khi tài khoản DELETED thì xóa gì, giữ gì | Closed | Xem DEC-156 |
| ISS-252 | Privacy: tin nhắn và nhật ký giữ vĩnh viễn khi người liên quan đã xóa tài khoản | Closed | Xem DEC-156 |
| ISS-253 | Privacy: trang chính sách nêu việc xử lý bởi AI và dịch vụ bên ngoài thế nào | Closed | Xem DEC-154 |
| ISS-254 | Privacy: cơ sở xử lý dữ liệu và các mục của trang Privacy Policy/ToS | Closed | Xem DEC-154 |
| ISS-255 | Privacy: quyền nhận bản sao dữ liệu và rút lại sự đồng ý | Closed | Xem DEC-155, DEC-157 |
| ISS-256 | Privacy: người dùng dưới 16 tuổi | Closed | Xem DEC-157 |
| ISS-257 | Privacy: "đồng ý lại ở lần đăng nhập kế tiếp" áp dụng thế nào khi người dùng đang giữ phiên đăng nhập | Closed | Xem DEC-158 |
| ISS-258 | Privacy: ai phát hành phiên bản chính sách mới | Closed | Xem DEC-158 |
| ISS-259 | Privacy: khi tài khoản DELETED, lượt theo dõi Topic và bài viết của tài khoản đó xử lý thế nào | Closed | Xem DEC-159 |
| ISS-260 | Privacy: phản hồi gợi ý Topic (M05) của tài khoản đã xóa có giữ không | Closed | Xem DEC-159 |

---
## Functional Requirement — M03: Post & Content | Status: CLOSED ✓

| ID | Title | Status | Decision |
|----|-------|--------|----------|
| ISS-261 | Bài viết có được đính kèm tài liệu không? (DEC-035 cho PDF/DOCX/XLSX/PPTX, DEC-130 coi phạm vi tải lên chỉ là ảnh) | Closed | Xem DEC-160 |
| ISS-262 | Trạng thái kiểm duyệt của bài mới tạo; "Mod gỡ bài" là trạng thái nào? | Closed | Xem DEC-161 |
| ISS-263 | Quét lại khi sửa bài đã đăng: xử lý theo điểm quét và khi AI lỗi | Closed | Xem DEC-161 |
| ISS-264 | Bài ở trạng thái nào thì tác giả sửa, xóa được; khôi phục về trạng thái nào | Closed | Xem DEC-162 |
| ISS-265 | Mức cảnh cáo MEDIUM, HEAVY chặn những thao tác nào trên bài viết | Closed | Xem DEC-163 |
| ISS-266 | Phần bắt buộc khi gửi bài, khi lưu nháp; giới hạn độ dài tiêu đề, nội dung | Closed | Xem DEC-164 |
| ISS-267 | Chi tiết poll: cấu hình, đổi và bỏ phiếu, hạn kết thúc, thêm lựa chọn, cách tính % | Closed | Xem DEC-165 |
| ISS-268 | Bài bị AI tự từ chối: tác giả thấy gì, gửi lại thế nào | Closed | Xem DEC-166 |
| ISS-269 | "Khóa toàn bộ" chặn những tương tác nào | Closed | Xem DEC-167 |
| ISS-270 | Thời hạn khôi phục 7 ngày đếm thế nào | Closed | Xem DEC-162 |
| ISS-271 | Mod/Admin có xem được bài nháp, bài tự ẩn, bài bị từ chối của người khác không | Closed | Xem DEC-168 |
| ISS-272 | Accepted Answer (draft DM-4.2.1) có trong MS1 không | Closed | Xem DEC-169 |
| ISS-273 | Ảnh bìa bài viết (draft DM-2.1) có làm không | Closed | Xem DEC-169 |
| ISS-290 | Áp xóa mềm cho bài viết (OPEN-010): hết hạn khôi phục giữ gì, ai xem lại bài đã xóa hẳn | Closed | Xem DEC-184 |
| ISS-291 | Bài tự ẩn né kiểm duyệt: Mod không xem được bài Tự ẩn bị báo cáo; sửa trong lúc ẩn rồi hiện lại không bị quét | Closed | Xem DEC-185 |

---

## Functional Requirement — M02: User Profile | Status: CLOSED ✓

| ID | Title | Status | Decision |
|----|-------|--------|----------|
| ISS-274 | Tab nội dung của chủ hồ sơ: DEC-023, DEC-024 chỉ có Bài viết + Bookmark, DEC-038 đặt thêm tab "Đã xóa" | Closed | Xem DEC-170 |
| ISS-275 | Guest có xem được trang hồ sơ và danh sách người theo dõi, đang theo dõi không | Closed | Xem DEC-171 |
| ISS-276 | Danh sách "đang theo dõi" gồm những gì; tài khoản DEACTIVATED, BANNED trong danh sách theo dõi | Closed | Xem DEC-172 |
| ISS-277 | Hồ sơ có hiện Lớp/Khối, ngày tham gia, stars nhận, stars cho (draft DM-1.2) ngoài danh sách QA-067 không | Closed | Xem DEC-173 |
| ISS-278 | Bài đã lưu sau đó không còn xem được thì tab Bookmark hiện thế nào | Closed | Xem DEC-174 |
| ISS-279 | Tab Bài viết hiện những bài nào với chủ hồ sơ và với người xem | Closed | Xem DEC-175 |
| ISS-280 | Chi tiết hồ sơ: nhắc cập nhật Lớp/Khối, thứ tự danh sách, avatar mặc định, đếm ký tự bio, bỏ chọn Lớp/Khối, địa chỉ /u/{username} | Closed | Xem DEC-176 |
| ISS-281 | Mod/Admin có được gỡ avatar, bio vi phạm khi xử lý báo cáo người dùng không (mở rộng phạm vi) | Closed | Xem DEC-177 |

---

## Functional Requirement — M04: Comment | Status: CLOSED ✓

| ID | Title | Status | Decision |
|----|-------|--------|----------|
| ISS-282 | Tác giả có sửa, xóa bình luận của mình khi bài bị khóa, khi ở mức HEAVY, khi bình luận đang bị ẩn không | Closed | Xem DEC-178 |
| ISS-283 | Xóa bình luận là vĩnh viễn hay xóa mềm; ai được xem lại nội dung đã xóa (liên quan báo cáo) | Closed | Xem DEC-179 |
| ISS-284 | Bài bị xóa hẳn thì bình luận của bài xử lý thế nào | Closed | Xem DEC-179 |
| ISS-285 | Chủ bình luận thấy bình luận bị ẩn ở đâu; "Mod xóa bình luận" là ẩn hay xóa; quét AI bình luận; khiếu nại bình luận | Closed | Xem DEC-180 |
| ISS-286 | Bình luận gốc bị ẩn còn trả lời; dấu đã xóa khi hết trả lời; trả lời vào luồng có dấu | Closed | Xem DEC-181 |
| ISS-287 | Số bình luận của bài đếm gì; thứ tự Top khi cùng số upvote | Closed | Xem DEC-182 |
| ISS-288 | Giới hạn độ dài bình luận; trích dẫn khi trả lời có tính vào độ dài không | Closed | Xem DEC-183 |
| ISS-289 | Xem lại nội dung đã xóa khi bị xử lý hoặc khiếu nại (mở rộng phạm vi) | Closed | Xem DEC-179 |

---

## Functional Requirement — M08: Moderation | Status: CLOSED ✓

| ID | Title | Status | Decision |
|----|-------|--------|----------|
| ISS-292 | Ngưỡng AI có phụ thuộc mức cảnh cáo của tác giả không (QA-020 nói có, DEC-098 một cặp 0,9/0,5) | Closed | Xem DEC-186 |
| ISS-293 | "Suspend", "Disable account" trong draft có là thao tác riêng không (DEC-080 chỉ có ban) | Closed | Xem DEC-187 |
| ISS-294 | Vi phạm lần thứ 7 (đang HEAVY) chuyển sang ban thế nào ("auto-ban" của DEC-080 so với "AI never auto-bans" của DEC-078) | Closed | Xem DEC-187 |
| ISS-295 | Ai được cảnh cáo, ban tài khoản Mod, Admin; Mod có xử lý vụ nhắm vào chính mình không | Closed | Xem DEC-189 |
| ISS-296 | Mod, Admin có ẩn, cảnh cáo, ban ngoài một vụ báo cáo không | Closed | Xem DEC-190 |
| ISS-297 | Mức nặng của từng lý do báo cáo; một hay nhiều lý do mỗi báo cáo; thứ tự khi bằng điểm ưu tiên | Closed | Xem DEC-190 |
| ISS-298 | Hết thời gian thử thách thì số lần, mức, thời gian thử thách mới ra sao; "N ngày" tính thế nào | Closed | Xem DEC-188 |
| ISS-299 | Ban nào được tính vào "số lần đã bị ban" | Closed | Xem DEC-187 |
| ISS-300 | Báo cáo có làm bài chuyển Bị gắn cờ (tạm ẩn) không (DEC-032 "AI/report flagged") | Closed | Xem DEC-190 |
| ISS-301 | Nội dung do AI gắn cờ và yêu cầu ban nằm ở hàng chờ nào | Closed | Xem DEC-190 |
| ISS-302 | Kết luận vụ: lý do bắt buộc khi Bác bỏ; thông báo cho người bị báo cáo khi Bác bỏ; kết quả chung khi đối tượng là người dùng, nhóm | Closed | Xem DEC-192 |
| ISS-303 | Báo cáo một đối tượng không còn hiển thị với người báo cáo | Closed | Xem DEC-191 |
| ISS-304 | Gửi báo cáo: báo cáo chính mình, báo cáo trùng khi vụ còn mở, người ở mức HEAVY | Closed | Xem DEC-191 |
| ISS-305 | Hàng chờ: "30 phút không thao tác", chỉ số tập trung, Admin xử lý vụ nhắm vào chính mình | Closed | Xem DEC-189, DEC-190, DEC-192 |
| ISS-306 | Quét AI và cảnh cáo: ngưỡng tốc độ, điểm quét, nhiều nội dung trong một lần quét, bỏ hoặc lật cảnh cáo | Closed | Xem DEC-186, DEC-188 |
| ISS-307 | Ban chồng lên ban đang hiệu lực; nhật ký ghi thêm thao tác nào, có sửa được không | Closed | Xem DEC-187, DEC-193 |
| ISS-308 | Người báo cáo có rút, sửa báo cáo không (mở rộng phạm vi) | Closed | Xem DEC-191 |
| ISS-309 | Báo cáo nhóm: người bị báo cáo, Mod xử lý nhóm vi phạm bằng thao tác gì (mở rộng phạm vi) | Closed | Xem DEC-194 |

---

## Functional Requirement — M09: Appeal | Status: CLOSED ✓

| ID | Title | Status | Decision |
|----|-------|--------|----------|
| ISS-310 | Ai xét khiếu nại khi người khiếu nại hoặc người ra xử lý là Mod, Admin; Mod tự duyệt khiếu nại của mình | Closed | Xem DEC-195, DEC-196 |
| ISS-311 | Bài, bình luận của Admin có qua duyệt, quét AI không (phát sinh từ ISS-310) | Closed | Xem DEC-195 |
| ISS-312 | "Mod duy nhất có thể xét" và việc chuyển khiếu nại lên Admin khi Admin vốn thấy mọi khiếu nại | Closed | Xem DEC-196 |
| ISS-313 | Tài khoản đang bị ban có khiếu nại cảnh cáo, bài bị gỡ được không | Closed | Xem DEC-197 |
| ISS-314 | Người bị AI tự cảnh cáo vào trang khiếu nại từ đâu (thông báo cảnh cáo AI không kèm đường dẫn) | Closed | Xem DEC-197 |
| ISS-315 | Khiếu nại bài bị AI tự từ chối: có cho khiếu nại không, hạn, kết quả; cảnh cáo AI đi kèm | Closed | Xem DEC-198 |
| ISS-316 | Bản chụp nội dung lúc xử lý để xét khiếu nại (mở rộng phạm vi, stakeholder nêu) | Closed | Xem DEC-198 |
| ISS-317 | Hạn khiếu nại cảnh cáo khi thời gian thử thách bị đặt lại hoặc nối tiếp khi giảm mức | Closed | Xem DEC-199 |
| ISS-318 | Khiếu nại được xét sau khi xử lý đã kết thúc (ban hết hạn, được gỡ; cảnh cáo đã giảm mức) | Closed | Xem DEC-199 |
| ISS-319 | Ưu tiên giữa hàng chờ khiếu nại bài viết (riêng) và khiếu nại cảnh cáo, ban | Closed | Xem DEC-200 |
| ISS-320 | Khiếu nại ban của một Mod được chấp nhận thì vai trò Mod có được trả lại không | Closed | Xem DEC-201 |
| ISS-321 | OPEN-012: bình luận bị ẩn có hiện lại khi cảnh cáo, ban liên quan bị lật không | Closed | Xem DEC-201 |
| ISS-322 | Lý do kết luận khiếu nại; rút, sửa khiếu nại đã gửi | Closed | Xem DEC-201 |
| ISS-323 | Khiếu nại bài bị Mod gỡ chồng với khiếu nại riêng cảnh cáo, ban đi kèm | Closed | Xem DEC-202 |
