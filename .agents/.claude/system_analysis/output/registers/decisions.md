# Decision Log

> Decisions taken during the interview, with options considered and rationale.
> Format: DEC-### | Decision | Options considered | Rationale | Who decided

| ID | Decision | Options considered | Rationale | Decided by |
|---|---|---|---|---|
| DEC-001 | No Teacher account type | A: Teacher role / B: No distinction | Too few teachers for meaningful leaderboard; doubles Reward system cost for a 2-person team | Stakeholder (in draft) |
| DEC-002 | Messaging: text-only, no file/voice/video | A: Full media / B: Text-only | WebRTC/media server out of scope for 2-person team | Stakeholder (in draft) |
| DEC-003 | Group reuses Forum mechanism (no rebuild) | A: Separate Post table / B: Shared + group_id | Avoids duplication, consistent behavior | Stakeholder (in draft) |
| DEC-004 | Post Star ≠ Comment Star (separate weights) | A: Unified star / B: Separate | Prevents spam-comment-to-farm-reputation | Stakeholder (in draft) |
| DEC-005 | AI as support layer only — no autonomous decisions on sensitive cases | A: Full auto / B: Human-in-the-loop | AI quality unpredictable; trust requires human oversight | Stakeholder (in draft) |
| DEC-006 | All 5 AI features are mandatory (not optional) | A: Only AI Moderation / B: All 5 | Product differentiator; thesis requirement | Stakeholder (updated draft) |


---

### DEC-007
- **ID:** DEC-007
- **Title:** Super Admin Pattern — ADMIN có thể promote user khác lên ADMIN
- **Decision:** Hệ thống áp dụng super admin pattern: 1 root ADMIN được seed từ DB (không qua UI đăng ký); ADMIN có thể promote/demote user thành ADMIN khác qua giao diện quản trị. Dev team giữ root credential, bàn giao operational admin cho client sau MS1 qua flow trong UI.
- **Source:** QA-009 / ISS-028
- **Rationale:** Cho phép bàn giao vận hành linh hoạt mà không cần dev team can thiệp DB. Production-ready từ đầu.

**[Amended 2026-10-21 — DEC-221: chỉ ADMIN gốc cấp, thu hồi Admin; cấp qua đề xuất; gốc không bị thu hồi]**

---

### DEC-008
- **ID:** DEC-008
- **Title:** AI Layer Feature Flag — global toggle on/off
- **Decision:** Hệ thống có global toggle `AI_ENABLED` (Admin config UI hoặc env var ở deploy level). Mỗi module có fallback rõ ràng khi AI tắt: M06 Search → full-text keyword; M08 Moderation → manual queue only; M05 Topic → user tự chọn topic, không có gợi ý. Tech stack lưu flag defer sang Phase 8 (OPEN-002). **[Clarified: nơi lưu/đổi flag đã được giải quyết bởi DEC-092/093 — Admin Panel (M10) có System config gồm AI master + per-module toggle; flag lưu bền (DB) để đổi lúc đang chạy, không cần redeploy. Không có quyết định mới — ISS-200/QA-259]**
- **Source:** QA-024 / ISS-042
- **Rationale:** Hệ thống phải hoạt động độc lập khi AI off (per DEC-005). Feature flag cho phép toggle linh hoạt mà không cần redeploy.

---

### DEC-009
- **ID:** DEC-009
- **Title:** Anonymous Post — Group-level toggle, not system-level
- **Decision:** Anonymous posting được bật/tắt ở cấp Group bởi Group Owner (không phải per-post toggle cho mọi user). Khi toggle bị tắt, chỉ áp dụng cho post mới (existing anonymous posts giữ nguyên). Feature này thuộc M11 (Group), không phải M03 (Post). Removed F-POST-05 from M03; added F-GRP-10 in M11.
- **Source:** QA-025 / ISS-043 (partial) / ISS-GRP-01
- **Rationale:** Anonymous post gắn liền với context Group; không phải feature của Post độc lập. Toggle ở Group Owner level đảm bảo kiểm soát cộng đồng rõ ràng.

---

### DEC-010
- **ID:** DEC-010
- **Title:** Account Linking — Auto-link by verified Google email
- **Decision:** Khi user đăng nhập bằng Google OAuth, hệ thống tự động link account nếu email Google khớp với email đã đăng ký (verified). Notification được gửi sau khi link thành công. Không cần manual confirmation.
- **Source:** QA-026 / ISS-043
- **Rationale:** Đảm bảo đồng nhất account, tránh duplicate. Auto-link là practice phổ biến (Google, GitHub, Facebook đều làm vậy với verified email).

**[Amended 2026-10-11 — DEC-147: liên kết cả khi email chưa xác minh; thông báo trong ứng dụng và email]**

---

### DEC-011
- **ID:** DEC-011
- **Title:** Post Soft Delete — 7-day recovery window
- **Decision:** Post bị xóa sử dụng soft delete: set `deleted_at` timestamp, `publish_state = 'deleted'`. Cron job hard-delete sau 7 ngày. User có thể khôi phục trong 7 ngày nếu mod chưa removed. Sau 7 ngày không thể khôi phục.
- **Source:** QA-027 / ISS-044
- **Rationale:** 7 ngày đủ để user nhận ra lỡ tay xóa mà không tích lũy data rác lâu dài.

**[Amended 2026-10-11 — DEC-162: xóa ở mọi trạng thái, khôi phục về trạng thái trước khi xóa, hạn 7 × 24 giờ]**

**[Amended 2026-10-14 — DEC-184: hết 7 ngày chỉ gắn cờ "đã xóa hẳn", không xóa dữ liệu]**

---

### DEC-012
- **ID:** DEC-012
- **Title:** Post Status Model — 3 independent fields
- **Decision:** Post status được tách thành 3 trường độc lập: `publish_state` (draft/published/deleted — user controls), `mod_state` (pending/active/under_review/removed — system/mod controls), `lock_level` (none/author/mod — author locks comments; mod can also lock). Author có thể lock comments của bài mình; Mod có quyền lock thêm. User không tự xóa bài — chỉ set `publish_state=deleted`; Mod set `mod_state=removed` để kiểm soát nội dung.
- **Source:** QA-028, QA-029 / ISS-044
- **Rationale:** Separation of concerns rõ ràng. Tránh trạng thái xung đột. Pattern theo Discourse/Reddit.

---

### DEC-013
- **ID:** DEC-013
- **Title:** Content Scan Policy — Pre-scan new posts, background re-scan edits
- **Decision:** Post mới → pre-scan (ẩn với public cho đến khi AI scan xong, `mod_state=pending`). Edit post → background re-scan (không ẩn, nếu flagged thì chuyển `under_review`). AI off → bypass scan, post active ngay. Không retroactive scan khi AI re-enable (Option C: chỉ scan post mới từ đó trở đi).
- **Source:** QA-030, QA-031 / ISS-044
- **Rationale:** Platform phục vụ học sinh — pre-scan cần thiết để kiểm soát nội dung. Edit pre-scan gây UX tệ cho đã-vetted content. Retroactive scan khi re-enable gây burst load không kiểm soát được.

**[Amended 2026-10-11 — DEC-161: quét lại khi sửa — điểm ≥ 0.5 thì FLAGGED, lỗi thì giữ nguyên]**

**[Amended 2026-10-18 — DEC-195: bài của Admin không quét trước khi đăng]**

---

### DEC-014
- **ID:** DEC-014
- **Title:** Registration Flow — 3-step progressive onboarding
- **Decision:** Step 1: email + password. Step 2: verify email (magic link, 1h, mandatory). Step 3: setup username (required) + display_name (required) + bio/grade_level/avatar (optional, skippable). Google OAuth: skip Step 1+2, display_name auto-fill, must set username at Step 3. Login gate: redirect to last incomplete step.
- **Source:** QA-048, QA-049, QA-053 / ISS-054
- **Rationale:** Minimal friction at registration (2 fields), defer identity setup post-verify. Google OAuth already verified email so steps collapse.

---

### DEC-015
- **ID:** DEC-015
- **Title:** Identity Fields — display_name (free, not unique) + username (unique, for @mention)
- **Decision:** `display_name`: free-form, any style (nickname/full name/creative), NOT unique. `username`: unique, alphanumeric + underscore, min 3 / max 20 chars — used ONLY for @mention trigger and search, never displayed as primary identity. Display_name shown everywhere; username shown muted in mention dropdown.
- **Source:** QA-050, QA-051, QA-052 / ISS-054
- **Rationale:** Forum community norm (free display name) + mention usability (unique handle without spaces).

**[Amended 2026-10-11 — DEC-148: so trùng username không phân biệt hoa thường; giới hạn display_name; đổi tên]**

---

### DEC-016
- **ID:** DEC-016
- **Title:** Email flows — verify (1h) + forgot password (15min) + change password (in-app)
- **Decision:** Verify email: magic link 1h, manual resend (banner), 60s cooldown. Forgot password: magic link 15min → revoke all other sessions → auto-login new session. Change password (Settings, logged in): old+new+confirm, no session revoke. Google OAuth accounts: no password flow — show redirect message.
- **Source:** QA-049, QA-059, QA-060, QA-061 / ISS-054, ISS-056
- **Rationale:** Reset = security event (revoke); change = normal update (no revoke). 15min for reset = tighter security window.

**[Amended 2026-10-11 — DEC-151: magic link dùng một lần; đặt lại mật khẩu gửi thông báo]**

---

### DEC-017
- **ID:** DEC-017
- **Title:** Session Management — JWT + rotating refresh token, multi-device allowed
- **Decision:** JWT (stateless). Access token 1 hour. Refresh token 30 days, rotating (new token each use, old invalidated). `refresh_tokens` table in PostgreSQL. Multi-device: allowed — each device independent JWT + SSE connection. SSE pub/sub naturally handles multi-device (multiple SSEConnections per user in Set).
- **Source:** QA-057, QA-058 / ISS-055
- **Rationale:** JWT simple for thesis scale. Rotating refresh token adds security without Redis overhead. Multi-device doesn't complicate SSE architecture.

**[Amended 2026-10-11 — DEC-151: hạn 30 ngày tính lại sau mỗi lần làm mới]**

---

### DEC-018
- **ID:** DEC-018
- **Title:** Account State Machine — account_state (4) + verify_level (3)
- **Decision:** Two separate fields: `account_state` ENUM('ACTIVE','DEACTIVATED','DELETED','BANNED') DEFAULT 'ACTIVE'; `verify_level` ENUM('NONE','EMAIL_VERIFIED','SETUP_COMPLETED') DEFAULT 'NONE'. Login gate checks account_state first (BANNED/DELETED → block), then verify_level (redirect to appropriate step). Google OAuth starts at EMAIL_VERIFIED.
- **Source:** QA-062 / ISS-057
- **Rationale:** Separation of concerns: lifecycle state vs onboarding progress. Cleaner than single expanded ENUM.

---

### DEC-019
- **ID:** DEC-019
- **Title:** Deactivation — 14-day window, post hidden, comment tombstone, auto-delete
- **Decision:** No direct delete — user must deactivate first. Window: 14 days → auto-DELETED. Posts: hidden (URL → "Nội dung không tồn tại"). Comments: content visible, author → "Tài khoản tạm thời vô hiệu hoá", avatar → placeholder. After auto-DELETED: comments → "[Người dùng đã xóa]", PII wiped. BANNED screen: reason + appeal time + appeal button (if within window) + OK.
- **Source:** QA-063, QA-064, QA-065, QA-066 / ISS-057
- **Rationale:** Posts are standalone → safe to hide. Comments are part of others' threads → tombstone preserves thread integrity. 14 days sufficient for accidental deactivation recovery.

**[Amended 2026-10-11 — DEC-148, DEC-149: 14 × 24 giờ; username giữ vĩnh viễn, email giải phóng khi DELETED]**

**[Amended 2026-10-11 — DEC-156: danh mục dữ liệu xóa và giữ khi DELETED]**

---

### DEC-020
- **ID:** DEC-020
- **Title:** @Mention System — search both fields, priority tiers, atomic node
- **Decision:** Trigger: @ + min 1 char, debounce 300ms, spaces allowed in query. Search: pg_trgm on display_name AND username. Priority (Group): following > same group > global. Priority (Post, no group): following > common group > global. Dropdown: top 5. Each item: avatar + display_name + @username (muted). Render: display_name + brand highlight (no @ shown). Stored: user_id (auto-updates on name change). Node atomic: no trim/edit label.
- **Source:** QA-054, QA-055, QA-056 / ISS-054
- **Rationale:** pg_trgm handles Vietnamese names + spaces naturally. Priority tiers surface relevant people first. Atomic node prevents misrepresentation via label editing.

**[Amended 2026-10-11 — DEC-153: thứ tự trong tầng, loại tài khoản không ACTIVE khỏi danh sách gợi ý]**

**[Amended 2026-10-20 — DEC-214: khớp tên như tìm người dùng M06 (DEC-209): bất kỳ vị trí, bỏ dấu, gần đúng]**

---
## Phase 5 — M02: User Profile

### DEC-021: Avatar upload
- CDN: Cloudinary (backed by AWS S3)
- Allowed types: JPEG, PNG, WebP only (no animated GIF)
- Max size: 5 MB
- On upload: old avatar deleted from CDN
- Display: circular crop rendered by UI; original stored

### DEC-022: Bio field
- DB: VARCHAR(255)
- UI character limit: 155 chars (live counter)
- Optional; empty bio renders nothing

### DEC-023: Profile URL
- Route: `/u/{username}`, dual-context
- Owner: Edit Profile button, tabs = Posts + Bookmarks
- Visitor: read-only, tabs = Posts only
- Conditional on `request.user === profile.user`

**[Amended 2026-10-13 — DEC-170: chủ hồ sơ thêm tab "Đã xóa"]**

### DEC-024: Profile content tabs
- Owner: Posts | Bookmarks (default: Posts)
- Visitor: Posts only

**[Amended 2026-10-13 — DEC-170: chủ hồ sơ thêm tab "Đã xóa"]**

### DEC-025: Followers / Following display
- Count shown on profile
- Full list public (no privacy restriction)

**[Amended 2026-10-13 — DEC-171, DEC-172: Guest phải đăng nhập mới xem danh sách; danh sách chỉ người dùng, không hiện DEACTIVATED, BANNED]**

### DEC-026: Username change history
- NOT displayed on profile — no history table in v1

### DEC-027: Social links
- DROPPED for v1 — future extension
- Concerns: malicious links, off-platform traffic

### DEC-028: Points + badges on profile
- Display only; M12 handles logic/calculation

---
## Phase 5 — M03: Post & Content

### DEC-029: Tiptap editor extensions
Bold, italic, underline, strikethrough, highlight; Heading H1–H3; Bullet/numbered/task list; Inline code + code block (syntax highlight); LaTeX/KaTeX (raw input, no visual editor v1); Table; Blockquote; Horizontal rule; Link with custom label. No inline image.

### DEC-030: Post structure
- 1 post type (no post_type field)
- Fields: title, content_json (ProseMirror JSON), content_text (plain text for search)
- Optional poll (separate table), attachment section below body

**[Amended 2026-10-11 — DEC-164, DEC-169: phần bắt buộc, giới hạn độ dài; không có ảnh bìa]**

### DEC-031: publish_state machine
DRAFT | PENDING | PUBLISHED | HIDDEN | REJECTED | DELETED
- DRAFT: composing, not submitted
- PENDING: submitted, under AI scan or mod review
- PUBLISHED: public
- HIDDEN: author self-hide (reversible)
- REJECTED: mod rejected, author can fix and resubmit
- DELETED: soft delete, 7-day recovery window

### DEC-032: mod_state
NORMAL | FLAGGED | HIDDEN
- FLAGGED: AI/report flagged, awaiting mod
- HIDDEN: mod-hidden, author cannot self-unhide, must appeal (M09)

**[Amended 2026-10-11 — DEC-161: bài mới NORMAL; "gỡ" = HIDDEN]**

**[Amended 2026-10-15 — DEC-190: báo cáo không đổi trạng thái kiểm duyệt; chỉ AI quét lại làm bài Bị gắn cờ]**

### DEC-033: lock_level + locked_by
- lock_level: NONE | COMMENT_LOCKED | FULLY_LOCKED
- COMMENT_LOCKED: author OR mod can set (blocks new comments)
- FULLY_LOCKED: mod only (blocks comments + reactions)
- locked_by: NULL | AUTHOR | MOD — if MOD, author cannot override
- Visibility rule: publish_state=PUBLISHED AND mod_state=NORMAL

**[Amended 2026-10-11 — DEC-167: FULLY_LOCKED chặn bình luận, upvote, bình chọn poll]**

### DEC-034: Pre-scan flow
Submit → PENDING → AI scan → clean: PUBLISHED; flagged: stay PENDING → mod review → approve: PUBLISHED | reject: REJECTED + reason → author resubmit → PENDING

### DEC-035: Attachments
- Images (JPEG/PNG/WebP): 5MB/file, max 10 files
- Documents (PDF/DOCX/XLSX/PPTX): 20MB/file, max 3 files
- CDN: Cloudinary (same as avatar)
- Avatar size updated to 5MB (see DEC-021)

### DEC-036: Poll (table: polls, FK → posts)
- Optional, max 1 per post; options min 2 max 10
- Owner config: allow_change_vote, allow_multiple (if true: select up to all options), show_result_before_vote (default false)
- expires_at: NOT NULL (required)
- is_closed: boolean — force-close early; extend by updating expires_at
- Once closed: cannot reopen
- After close: always show result % regardless of show_result_before_vote

**[Amended 2026-10-11 — DEC-165: bỏ allow_change_vote, mặc định chọn nhiều, khóa cấu hình sau khi gửi, thêm lựa chọn, hạn, rút phiếu, %]**

### DEC-037: Edit history
- Post: full history in post_edits table; public badge "(đã chỉnh sửa)" + "Xem lịch sử"
- Comment: edited_at timestamp only; badge "(đã chỉnh sửa)"; no history UI

### DEC-038: Soft delete
- DELETED: hidden from feed
- 7-day window: author can recover → PUBLISHED (tab "Đã xóa" on profile)
- After 7 days: cron job hard deletes

**[Amended 2026-10-11 — DEC-162: khôi phục về trạng thái trước khi xóa; 7 × 24 giờ]**

**[Amended 2026-10-14 — DEC-184: hết 7 ngày chỉ gắn cờ "đã xóa hẳn", không xóa dữ liệu]**

---
## Phase 5 — M04: Comment

### DEC-039: Comment editor extensions
Bold, italic, inline code, LaTeX/KaTeX, link, @mention, blockquote (for quote-reply). No heading, table, task list, attachments.

### DEC-040: Threading model
2 levels only — root comment + child replies. Reply to child → appended to same thread (no deeper nesting). @mention used for context when replying to a specific child.

### DEC-041: Reactions
Upvote only — no downvote/dislike. Bad content → report (M08).

### DEC-042: Comment sort
- Top (default): by upvotes
- Mới nhất: newest first
- Cũ nhất: oldest first
Child replies always sort chronological (oldest first) regardless of filter.

### DEC-043: Edit/Delete
- Edit: author can edit anytime, no time limit; badge "(đã chỉnh sửa)" shown
- Delete: permanent (no soft delete, no recovery window)
- Root with replies → tombstone "[Bình luận đã bị xóa]"; replies remain
- Root without replies → hard delete
- Child → hard delete; replies of child show "reply to [bình luận đã bị xóa]"

**[Amended 2026-10-14 — DEC-179: xóa mềm, nội dung giữ vĩnh viễn]**

### DEC-044: Attachments
Not supported in comments. Share files via post instead.

### DEC-045: @Mention + Notification
@mention uses shared M01 logic. Always triggers notification regardless of mention location (post or comment).

**[Amended 2026-10-11 — DEC-153: thông báo nhắc tên gửi khi nội dung công khai]**

### DEC-046: Quote-reply
Click Reply → editor auto-inserts blockquote with original content + author name. Uses Tiptap blockquote extension.

**[Amended 2026-10-14 — DEC-183: trích dẫn chỉ hiển thị, một dòng, không thuộc nội dung]**

---
## Phase 5 — M05: Topic & Tag

### DEC-047: Topic vs Tag
- Topic: structured taxonomy, AI suggest + user confirm, used for filter/browse. Flat structure (nested deferred).
- Tag: free-form #hashtag, user-typed, no fixed list, no spaces.

### DEC-048: Topic list (11, final)
Toán học, Ngữ văn, Ngoại ngữ, Khoa học tự nhiên (Lý/Hóa/Sinh), Khoa học xã hội (Sử/Địa/KT&PL), Tin học, Kỹ năng mềm, Hướng nghiệp, Nghệ thuật & Sáng tạo, Góc Chill, Khác

**[Amended 2026-10-07 — DEC-141: 11 Topic là danh mục ban đầu; Admin thêm, gộp, xóa Topic]**

### DEC-049: Topic rules
- Min 1, max 3 topics/post (mandatory)
- Mod/admin: edit (rename) + merge. No delete.
- Merge auto re-points post_topics from source to target

**[Amended 2026-10-07 — DEC-141, DEC-142: thêm/gộp/xóa Topic chỉ Admin, bỏ đổi tên, xóa khi chưa có bài; nháp được 0 Topic; đổi Topic khi sửa bài]**

### DEC-050: AI suggest topic flow
- "Gợi ý topic" button (not automatic) → AI analyzes text only (title + content_text, no attachment processing) → suggest max 3 topics, pre-ticked
- Content <20 words → no suggestion, shown "content too short"
- User adjusts freely → publish
- Content changed after suggest → flag is_stale, soft warning + re-suggest button, does not block publish
- Feedback (AI suggest vs final selection) only recorded when not stale
- User manually picks topic from start → skips AI flow entirely
- AI off → user picks from dropdown, no suggest

**[Amended 2026-10-07 — DEC-142, DEC-144: gợi ý cả khi tác giả sửa bài; 20 từ đếm trên tiêu đề + nội dung]**

### DEC-051: Tag data model + rules
- Tables: tags (id, name unique lowercase-normalized, created_at — no created_by) + post_tags junction
- Auto-created, no approval
- Max 5 tags/post, max 30 chars/tag
- Fully free — mod/admin do NOT edit/merge/delete under normal conditions
- Crisis case: mod/admin soft-delete (is_active=false) → hidden from autocomplete/trending/browse; old posts keep post_tags record but tag chip hidden from display; if user retypes a disabled tag name, it's NOT tagified — rendered as plain text

**[Amended 2026-10-07 — DEC-143, DEC-146: tập ký tự Tag, "#" không tính, hiển thị chữ thường, kích hoạt lại Tag, ghi nhật ký]**

### DEC-052: Trending (Topic + Tag)
- Rolling 7-day window (sliding from now, unlike leaderboard's fixed calendar week)
- Recalculated every 15-30 min (cached, not live query)
- Score: Σ(1 + upvotes×2 + comments×1) across all posts in window
- To be integrated as a dedicated Feed section (note for M14)

**[Amended 2026-10-07 — DEC-145: công thức theo tương tác trong cửa sổ, thêm bookmark, phạm vi bài, mốc 30 phút, thứ tự]**

---
## Phase 5 — M06: Search

### DEC-053: Search scope (final, supersedes Phase 3 ISS-040 partial scope)
- Post: semantic search via embedding (pgvector)
- User: exact/prefix match on display_name + username (pg_trgm, shared with M01 @mention)
- Tag: exact/prefix match (pg_trgm)
- Topic: exact/prefix match (pg_trgm)
- Group: exact/prefix match (pg_trgm); visible-but-gated for private groups (name+description shown, content gated per M11)
- Comment: NOT searchable (too many, low value)
- Fallback: full-text (Postgres FTS) when AI off

**[Amended 2026-10-20 — DEC-209, DEC-210: khớp ở bất kỳ vị trí, bỏ dấu, gần đúng; nhóm Private ẩn khỏi tìm kiếm với người ngoài nhóm]**

### DEC-054: Search trigger
- Post (semantic): submit-only (Enter/click), no debounce — expensive compute
- User/Tag/Topic/Group: debounce (300ms live suggestion) + also works on submit

### DEC-055: Ranking (Post search)
```
relevance_score = cosine similarity from embedding, normalized 0-1
engagement_raw = log(1+upvotes)×2 + log(1+comments)×1
engagement_score = normalize(engagement_raw) to 0-1 within candidate set
final_score = relevance_score × 0.8 + engagement_score × 0.2
```
Top N candidates by relevance first (vector search), then re-rank by final_score.

**[Clarified 2026-10-20 — DEC-211: tập ứng viên 120 bài; cách chuẩn hóa; bằng điểm; full-text dùng tỷ lệ từ khớp]**

### DEC-056: Filters (Post search)
Topic, Tag, date range (Today/This week/This month/All), Following-only toggle, Sort (Relevance default / Newest / Most upvoted)

**[Clarified 2026-10-20 — DEC-211, DEC-212: sắp xếp trên tập ứng viên; mỗi loại bộ lọc một giá trị; tuần, tháng theo lịch; "đang theo dõi" gồm User/Topic/Post]**

### DEC-057: Full-text fallback + Vietnamese diacritics
- Postgres FTS: tsvector/tsquery
- unaccent extension strips Vietnamese diacritics before indexing (solves "tìm không dấu")
- pg_trgm for prefix/fuzzy match on Tag/User/Topic/Group
- Generated column: content_search = to_tsvector('simple', unaccent(title || ' ' || content_text))

**[Clarified 2026-10-20 — DEC-209, DEC-211: khớp tên ở bất kỳ vị trí, gần đúng; full-text khớp ít nhất một từ]**

### DEC-058: Autocomplete (debounce dropdown)
Shows User/Tag/Topic/Group prefix matches only (pg_trgm). No Post title suggestions (Post is submit-only).

**[Clarified 2026-10-20 — DEC-209: gợi ý từ ký tự đầu, mỗi loại tối đa 3, chỉ tài khoản ACTIVE]**

### DEC-059: Search history
localStorage only (no DB). Max 10 recent searches. Shown on search box focus. "Clear history" button.

**[Amended 2026-10-20 — DEC-213: khi nào thêm mục, không trùng, chọn mục thì gửi luôn; xóa khi đăng xuất]**

### DEC-060: Results display
Mixed, single scrollable page (no tabs). Post results are primary (by final_score). User/Tag/Topic/Group shown as supplementary (max 3 each, sidebar/bottom).

### DEC-061: Snippet
No keyword highlighting. Plain snippet, first ~150 chars of content_text. Same approach for both semantic and full-text modes.

**[Clarified 2026-10-20 — DEC-213: cắt 150 ký tự trước từ bị chia đôi, thêm "…"]**

### DEC-062: Search permission
- Guest: search normally (same as public browse)
- Private group content (posts): only shown if searcher is a member of that group
- Private group entity (name/description): visible-but-gated — shows in Group search results regardless of membership (per M11), but content inside stays gated

**[Amended 2026-10-20 — DEC-208, DEC-210: Guest chỉ tìm bài bằng full-text; nhóm Private ẩn khỏi tìm kiếm với người ngoài nhóm]**

### DEC-063: Rate limiting
| | Debounce | Submit search |
|---|----------|----------------|
| Guest (by IP) | 30/min | 10/min |
| User (by user_id) | 45/min | 20/min |
429 Too Many Requests when exceeded, no captcha/long-term block.

**[Clarified 2026-10-20 — DEC-213: 60 giây gần nhất; tải thêm không tính lượt]**

### DEC-064: Pagination
Infinite scroll, 15 results/load, max 120 total results (8 loads), cursor-based (not offset). Beyond max: "Thu hẹp tìm kiếm để có kết quả chính xác hơn"

**[Clarified 2026-10-20 — DEC-211, DEC-212: thông báo khi đã tải 120; không giới hạn 120 khi không có truy vấn]**

---
## Phase 5 — M07: Notification

### DEC-065: Notification event list + channel
| Event | In-app | Email |
|-------|--------|-------|
| Password changed | Yes | Yes |
| DEACTIVATED auto-delete warning | No (can't login) | Yes |
| New follower | Yes | No |
| Post published/rejected/hidden/poll ended | Yes | No |
| Upvote (post + comment), batched | Yes | No |
| New comment / reply / @mention | Yes | No |
| Report result / warning received | Yes | No |
| Ban/unban | Yes | Yes |
| Appeal — ban-related | Yes | Yes |
| Appeal — post/comment/warn-related | Yes | No |
| Group: invite/join/approve/promote/kick | Yes | No |
| Badge / point milestone / weekly top | Yes | No |
| DM / Group chat message | Yes | No |
Email limited to: security (password change), account-deletion warning, ban/unban, ban-related appeals only. No digest email.

**[Amended 2026-10-11 — DEC-147, DEC-151: thêm sự kiện liên kết Google (in-app + email); đặt lại mật khẩu cũng là "password changed"]**

**[Amended 2026-10-14 — DEC-180: thêm sự kiện "Bình luận của bạn đã bị ẩn" (in-app)]**

**[Amended 2026-10-20 — DEC-215, DEC-218: thêm sự kiện bài mới của người đang theo dõi; quy tắc người nhận, tên người gây sự kiện]**

**[Amended 2026-10-21 — DEC-221: thêm sự kiện "Đề xuất làm Admin" (in-app)]**

**[Amended 2026-10-21 — DEC-231, DEC-237: thêm thông báo gỡ khỏi nhóm, yêu cầu tham gia mới, trở thành Owner]**

**[Clarified 2026-10-23 — DEC-246: "mốc điểm" là đạt huy hiệu]**

### DEC-066: Upvote notification batching
Batch upvotes (post + comment) within a 5-minute rolling window into one notification ("A và N người khác đã upvote..."). Single upvote shows the voter's name directly.

**[Clarified 2026-10-20 — DEC-216: báo ngay lượt đầu, cửa sổ từ lượt đầu, gộp theo từng bài/bình luận]**

### DEC-067: In-app notification UI
- Bell icon: dropdown (5-10 most recent) + dedicated page /notifications (full list)
- Separate Message icon (navbar): DM + Group chat, own unread badge, links to Chat inbox — NOT mixed with bell
- Mark read: click item → auto mark read + navigate; "Mark all as read" button

**[Clarified 2026-10-20 — DEC-217, DEC-220: chuông 10 thông báo, số chưa đọc; trang tải 20; biểu tượng Tin nhắn đếm cuộc trò chuyện]**

### DEC-068: Email delivery architecture
Event → write to email_queue table → cron scans every 1 minute → sends. Async, no blocking, no message broker needed for v1 scope.

**[Clarified 2026-10-20 — DEC-220: email lỗi gửi lại tối đa 3 lần]**

### DEC-069: In-app delivery architecture
Event → write to notifications table (source of truth) → best-effort WebSocket push to online clients. No cron/retry needed for in-app — client fetches unread from DB on page load/bell click regardless of WebSocket push success. [Amended: thông báo dùng SSE thay WebSocket — DEC-135/QA-257]

### DEC-070: Notification preferences — no global category toggle
No granular global preference settings page for v1. Instead:
- Per-post mute: toggle on each post ("Tắt thông báo cho bài này") mutes comment/reply/upvote notifications from that post specifically. @Mention still fires even when post is muted (deliberate address to user).
- Per-conversation mute (Chat): mute individual DM/Group chat threads.
- Global chat toggle: "Tắt thông báo cho toàn bộ Chat" setting, mutes all DM+Group chat notifications; coexists with per-conversation mute for finer override.

**[Clarified 2026-10-20 — DEC-219, DEC-220: tắt Chat chỉ ẩn popup tin nhắn, tắt toàn bộ không có ngoại lệ; công tắc bài trên mọi bài]**

### DEC-071: Notification retention
No auto-deletion / no retention policy — notifications kept indefinitely, consistent with Facebook/Twitter/Discord/GitHub approach. No cron cleanup.

---
## Phase 5 — M08: Moderation

### DEC-072: Report entities + reasons
- Post (8): Spam/Quảng cáo, Nội dung sai/hiểu nhầm, Đạo văn/Vi phạm bản quyền, Quấy rối/Bắt nạt, Ngôn từ thù ghét/Phân biệt, Nội dung người lớn/Không phù hợp, Bạo lực/Đe dọa, Khác
- Comment (7): same minus Đạo văn
- User (2): Quấy rối/Bắt nạt có hệ thống, Khác
- Group (4): Nội dung người lớn/Không phù hợp, Group giả mạo, Quấy rối/Bắt nạt có hệ thống, Khác
- Only logged-in users can report (no guest reporting)

**[Amended 2026-10-15 — DEC-191, DEC-194: không báo cáo chính mình, không báo cáo trùng khi vụ còn mở; nhóm bị báo cáo: Ẩn hoặc Khóa]**

### DEC-073: Report submission
- Evidence: max 3 images, 5MB/file (shared with platform image limit)
- Description text: optional, REQUIRED only when reason = "Khác"

### DEC-074: Report outcome notification (split by recipient)
- Reporter: vague outcome only ("đã xử lý — nội dung vi phạm đã gỡ/ẩn" or "không phát hiện vi phạm"), never sees punishment details of reported user
- Reported/offending user: detailed — resolution_reason, punishment level (warning level or ban), link to Appeal (M09)

**[Amended 2026-10-15 — DEC-192: không thông báo người bị báo cáo khi Bác bỏ; kết quả chung dùng cho mọi loại đối tượng]**

### DEC-075: Report queue mechanics
- Priority score = MAX(severity_weight across reasons in case) + report_count × 2
- Claim-based assignment: mod clicks "Nhận xử lý" to lock a case; auto-unlock after 30 min inactivity
- No SLA deadline, processed by priority order

**[Amended 2026-10-15 — DEC-190: mức nặng 10/5/2, bằng điểm thì vụ mở trước, 30 phút tính từ thao tác cuối]**

### DEC-076: Report grouping (case model)
- Group by (target_type, target_id) while status=OPEN into one "case"; each individual report row keeps its own data (reporter_id, reason, evidence, description)
- Case resolved → all open reports under it move to RESOLVED together; reporter notifications sent to all reporters in case (same generic outcome)
- New report on an already-RESOLVED target → opens a NEW case (no reopening), but mod sees full report history (past cases + outcomes) for that target as context
- Mod sets `resolution_reason` independently when resolving — mod's own determination, not necessarily matching reporters' stated reasons
- report status: OPEN → RESOLVED (action_taken | dismissed)

### DEC-077: Comment AI scan (post-scan, velocity-triggered)
- Unlike Post's pre-scan (blocks publish), Comment publishes immediately, no default scan
- Trigger: reply velocity crosses threshold within a sliding time window (exact numbers TBD, needs real usage data to tune) — e.g. placeholder "10 replies in 5 min"
- On trigger: scan entire thread (root + all replies) not yet scanned with current content version
- Re-trigger: velocity threshold crossed again AND content not yet scanned with current version (edit alone does not trigger — waits for next velocity trigger)
- If AI flags → comment auto-hidden (author only sees it) + pushed into report queue for mod review
- Report system works independently of velocity/scan status at all times

**[Amended 2026-10-14 — DEC-180: chủ bình luận cũng không thấy bình luận bị ẩn trong luồng]**

**[Amended 2026-10-15 — DEC-186, DEC-190: kích hoạt khi đạt ngưỡng; bình luận chờ xét là một vụ trong hàng chờ báo cáo]**

**[Amended 2026-10-18 — DEC-195: bình luận của Admin không bị AI quét]**

### DEC-078: Warning issuance mechanism
- AI high confidence → auto-issues warning directly, no mod involved (user can appeal via M09 if wrong)
- AI low confidence/borderline → escalates to mod queue, mod manually decides
- Mod can also independently issue warning when resolving a report case
- Ban always requires human (MOD/ADMIN) — AI never auto-bans, regardless of confidence

### DEC-079: Warning levels + probation (updated durations + restrictions)
| Level | Warns | Probation | Restriction |
|-------|-------|-----------|-------------|
| LIGHT | 1-2 | 7 days (was 5) | None — tracking window only |
| MEDIUM | 3-4 | 10 days | Cannot create new posts; comments OK |
| HEAVY | 5-6 | 15 days (was 14) | Cannot create posts or comments (read/vote only); existing content search-downranked ×0.5 |
Warning status is fully PRIVATE — visible only to the user themselves and to mods; never shown publicly on posts/comments/profile (prevents bullying of warned students).

> **AMENDED by DEC-118 and DEC-122 (Phase 5, M12):** the private scope above is narrowed by one deliberate, explicit public exception — a user at HEAVY warning level, or a BANNED user, is excluded from the public leaderboard for the duration of that state. This is the only public-facing consequence carved out of DEC-079's privacy guarantee; LIGHT/MEDIUM warn levels remain unaffected, and for BANNED users specifically, their profile/post/comment content stays visible as normal (see DEC-122) — only leaderboard eligibility is affected.

**[Amended 2026-10-11 — DEC-163: phạm vi "tạo bài mới" ở M03]**

**[Amended 2026-10-15 — DEC-188: giảm mức và thời gian thử thách nối tiếp, N × 24 giờ]**

**[Clarified 2026-10-20 — DEC-211: giảm hạng ×0,5 trên điểm cuối, chỉ khi xếp theo Liên quan]**

### DEC-080: Ban types + escalation
- Temporary ban (auto-escalating): 1st ban = 30 days, 2nd ban = 90 days, 3rd+ ban = permanent
- Permanent ban (manual): mod/admin can directly issue for severe first-offense violations, bypassing escalation
- Auto-ban trigger: user violates again while already at HEAVY warning level (warn #7+) → escalates to ban instead of another warning cycle
- 2 separate mod UI actions: "Ban" (auto-escalating duration) vs "Ban vĩnh viễn" (manual permanent override)
- Both always require MOD/ADMIN — never AI-triggered

**[Amended 2026-10-11 — DEC-152: ban tạm thời hết hạn thì tự về ACTIVE]**

**[Amended 2026-10-15 — DEC-187: không có suspend; lần thứ 7 thành yêu cầu ban; cách đếm số lần ban; không ban chồng]**

### DEC-081: Moderation audit log
- Log fields: actor_id (mod/AI), action_type (warn/ban/hide/resolve), target_id, reason, timestamp
- Admin: full audit log access, all mods, all actions
- Mod (default): sees only their own resolved case list
- Mod (appeal review exception): can see another mod's action details specifically when reviewing an appeal referencing that action (per QA-021 policy)

**[Amended 2026-10-07 — DEC-146: thêm loại thao tác vô hiệu hóa/kích hoạt lại Tag, đổi Topic/Tag bài người khác]**

**[Amended 2026-10-15 — DEC-193: ghi thêm gỡ ban, bỏ cảnh cáo AI, ẩn/khóa/mở khóa nhóm; không sửa, không xóa]**

**[Amended 2026-10-21 — DEC-224: Admin lọc nhật ký kiểm duyệt theo người làm]**

### DEC-082: False/malicious report handling
- No automated punishment — false positives risk discouraging legitimate reporting
- Metric shown to mod as reference: target_concentration = (dismissed reports targeting the same single target) / (total resolved reports by that reporter), calculated over reports resolved in the last 90 days
- High concentration = signal of targeted harassment via report system (not honest mistake, which shows spread-out low-concentration pattern)
- Mod uses judgment to manually issue warning to abusive reporter via existing warning mechanism — no separate automated system

**[Amended 2026-10-15 — DEC-192: tính cho đối tượng của vụ đang xem, 90 × 24 giờ]**

### DEC-083: Comment schema update (M04 cross-reference, added during M08 deep dive)
Comment needs a `mod_state` field similar to Post's (NORMAL | HIDDEN) to support AI auto-scan flagging (DEC-077) and mod report resolution. Not present in original M04 decisions (DEC-039-046) — added here as a retroactive schema requirement for M04.

---
## Phase 5 — M09: Appeal

### DEC-084: Appeal submission
Message (required, explanation text) + evidence (optional, max 3 images, 5MB/file — shared limits with report system).

### DEC-085: Banned user access
Banned users can still log in normally. Post-login they see only a "account banned" screen with reason + "Gửi khiếu nại" button (if within appeal window). All other API endpoints blocked (403) except appeal submission endpoint. Ban notification email includes direct "Appeal" link to protected /appeal route (redirects through login if needed).

**[Amended 2026-10-18 — DEC-197: trong lúc bị ban chỉ khiếu nại được chính lệnh ban]**

### DEC-086: Appeal deadline
- Warning: appeal window = entire probation duration (7/10/15 days matching DEC-079)
- Temporary ban: appeal window = entire ban duration (30/90 days matching DEC-080)
- Permanent ban: appeal window = 90 days from ban date, then appeal right permanently expires

**[Amended 2026-10-18 — DEC-199: hạn khiếu nại cảnh cáo cố định 7/10/15 ngày từ lúc ra, theo mức của chính cảnh cáo đó]**

### DEC-087: One appeal per action
Each resolved report action, warning, or ban may be appealed exactly once. A rejected appeal cannot be resubmitted for the same underlying action.

**[Clarified 2026-10-18 — DEC-202: áp cho xử lý đi kèm bài bị gỡ]**

### DEC-088: Appeal queue (separate from report queue)
- Separate queue from M08's report queue — different assignment rule needed (mod cannot review appeals of their own actions, per QA-021)
- Priority: Ban appeals > Warning appeals; FIFO within same tier
- Claim-based (30-min inactivity timeout, same mechanic as report queue)
- Mod's own actions are automatically excluded from their queue view (not just skipped — hidden entirely)
- Sole-mod edge case: if the only available mod is the action's author, auto-escalate to ADMIN

**[Amended 2026-10-18 — DEC-196, DEC-200: chuyển lên Admin là quy tắc lọc; một danh sách chung ban > cảnh cáo > bài]**

### DEC-089: Appeal outcome (reversal)
- Ban approved: account_state reverts to ACTIVE immediately; ban record kept in log marked overturned=true for audit, no longer in effect
- Warning approved: restriction lifted immediately; warn count decremented (treated as if warning never happened) to keep LIGHT/MEDIUM/HEAVY escalation math accurate

**[Amended 2026-10-18 — DEC-199, DEC-201: vẫn lật khi xử lý đã kết thúc; lật ban của Mod không trả lại vai trò]**

---
## Phase 5 — M10: Admin Panel

### DEC-090: Admin panel scope split
- Admin-only: Role management (promote/demote USER↔MOD), System config (AI toggle etc.), full audit log view, MOD account management (performance, revoke)
- Shared with Mod: report/warning/ban/appeal handling, Topic edit/merge (M05), Tag crisis soft-delete (M05)
- Policy constants (warning durations, ban durations, thresholds) are NOT admin-configurable via UI — hardcoded in code, changed via deployment + notify if needed

**[Amended 2026-10-07 — DEC-141: Topic thêm/gộp/xóa chỉ Admin; xóa mềm Tag vẫn dùng chung Mod]**

**[Clarified 2026-10-21 — DEC-224: "performance" = xem nhật ký kiểm duyệt theo Mod]**

### DEC-091: Role management flow
- Promote: Admin sends a proposal ("Đề xuất làm Mod") to a user (no eligibility conditions — admin free choice) → user receives notification with Accept/Decline → Accept sets role=MOD immediately; Decline does nothing (admin can re-propose later)
- Demote: Admin executes directly and immediately, no consent needed, no appeal right (role management, not punishment — different from M09 appeal scope)

**[Clarified 2026-10-20 — DEC-220: thông báo đề xuất trả lời một lần, không hết hạn]**

**[Amended 2026-10-21 — DEC-221, DEC-222, DEC-223: đề xuất làm Admin; đề xuất hạn 7 ngày; tự từ chức]**

### DEC-092: System config list (Admin Panel)
1. AI toggle (master + per-module, see DEC-093)
2. Maintenance mode (locks site to admin-only access)
3. Registration toggle (pause new signups)
4. Feature flags for Should/Could modules (Group, Chat, Gamification)
5. Site-wide announcement banner
(Email service toggle explicitly excluded — not needed for v1)

**[Amended 2026-10-11 — DEC-152: phạm vi của tạm dừng đăng ký và chế độ bảo trì]**

**[Clarified 2026-10-21 — DEC-225, DEC-226, DEC-228: cờ tính năng, banner, giá trị khởi tạo]**

### DEC-093: AI toggle granularity
Two-tier hierarchy:
- Master "AI Layer" toggle: overrides everything OFF when disabled
- Per-module toggles (only apply when master is ON): Search (semantic embedding, M06), Moderation (pre-scan+comment auto-scan+auto-warn, M08), Topic suggestion (M05)

**[Clarified 2026-10-19 — DEC-205: công tắc Search điều khiển cả embedding bài và embedding truy vấn; tóm tắt không có công tắc riêng]**

### DEC-094: Admin action audit log
All admin actions (promote/demote, config toggles, ban/warn actions) logged. Append-only — admin can view but cannot edit or delete entries. Ensures transparency even over admin's own actions.

**[Clarified 2026-10-21 — DEC-227, DEC-228: phạm vi, lý do, thứ tự và lọc của nhật ký]**

---
## Phase 5 — M13: AI Layer

### DEC-095: Embedding model + storage
- Model: OpenAI `text-embedding-3-small` (same vendor as Moderation API, cheap ~$0.02/1M tokens, multilingual incl. Vietnamese)
- Storage: pgvector extension, `posts.embedding vector(1536)` column, HNSW index
- Computed once at publish time (or alongside pre-scan); recomputed if content edited significantly (mirrors is_stale pattern from M05)

**[Clarified 2026-10-19 — DEC-205: tạo khi bài Đã đăng; tạo lại mỗi lần tiêu đề, nội dung chữ thay đổi; hàng chờ tạo bù]**

### DEC-096: Topic suggestion model
GPT-4o-mini — sufficient for simple 11-topic classification task, low cost.

### DEC-097: Moderation category mapping + coverage limits
- OpenAI Moderation API covers: Quấy rối (harassment), Ngôn từ thù ghét (hate), Người lớn (sexual), Bạo lực (violence) — maps directly to report reason categories
- NOT covered by AI: Spam, Đạo văn/Vi phạm bản quyền, Nội dung sai/gây hiểu nhầm — these rely entirely on manual report, no AI detection exists for them

### DEC-098: Confidence threshold — symmetric 2-branch design
One Moderation API call drives two independent decision branches from the same category scores:
- **Branch A (Content Gate)**: score≥0.9 → AI auto-reject (Post) / auto-hide (Comment), skip mod; 0.5≤score<0.9 → hold for mod review (Post stays PENDING, Comment stays hidden+queued); <0.5 → publish/show normally
- **Branch B (Warning)**: score≥0.9 → AI auto-issues warning; 0.5≤score<0.9 → mod decides during their review; <0.5 → no warning
Same 0.9/0.5 thresholds shared across Post and Comment. Values are placeholder/tunable pending real usage data.

**[Amended 2026-10-11 — DEC-166: bài bị AI từ chối — lý do, gửi lại]**

**[Amended 2026-10-15 — DEC-186: điểm quét = điểm cao nhất trong 4 nhóm; không đổi theo mức cảnh cáo]**

### DEC-099: AI failure handling (distinct from admin AI-off toggle)
Two distinct scenarios:
1. **AI deliberately OFF** (M10 admin toggle): uses each module's defined fallback — Search→full-text (M06), Topic→manual dropdown (M05), Moderation→no scan, content publishes directly, relies on report only (M03/M08)
2. **AI transient failure** (timeout/error while AI is ON): per-request degradation, not a state change
   - Timeout thresholds: Fast APIs (Moderation, Embedding) = 5s; LLM generation (Topic suggestion) = 10s
   - Retry: exactly 1 retry, sequential (wait for first attempt to fail/timeout, then 2s delay, then retry once)
   - If retry also fails: Search→fallback full-text for that query only; Topic suggest→show non-blocking error, no action taken; Moderation (Post pre-scan)→route to mod review queue (treat as safety-net, do NOT auto-publish); Moderation (Comment)→leave as-is, log error for admin

**[Clarified 2026-10-19 — DEC-205, DEC-206, DEC-207: embedding bài lỗi → hàng chờ tạo bù; tóm tắt 10 giây, lỗi báo bận; "log error for admin" = bản ghi thất bại trong nhật ký AI]**

### DEC-100: AI rate limiting
No dedicated AI-specific rate limit system. Relies on existing limits: Search (M06 DEC-063). New limit added: Topic Suggest button — 10 requests/min/user (only AI-triggered action lacking a natural rate limiter). Pre-scan/auto-scan are system-triggered, not user-invoked repeatedly, so no separate limit needed.

**[Amended 2026-10-07 — DEC-144: 10 lần tính theo 60 giây gần nhất]**

---
## Phase 5 — M11: Group

### DEC-101: Group creation — open access, rate-limited
Any logged-in user can create a group freely. Rate limit: 5 groups/day/user (anti-spam). No cap on total groups a user can own.

**[Clarified 2026-10-21 — DEC-237: 5 nhóm trong 24 giờ gần nhất; nhóm đã xóa vẫn tính; Admin cũng bị giới hạn]**

### DEC-102: Group role permission matrix
| Quyền | Owner | Group Mod | Member |
|-------|-------|-----------|--------|
| Đăng bài/comment/vote | ✓ | ✓ | ✓ |
| Duyệt pre-mod queue (nếu toggle bật) | ✓ | ✓ | ✗ |
| Ẩn/xóa post-comment trong group | ✓ | ✓ | ✗ |
| Duyệt/kick Member | ✓ | ✓ | ✗ |
| Promote/demote Group Mod | ✓ | ✗ | ✗ |
| Kick Group Mod khác | ✓ | ✗ | ✗ |
| Đổi setting group (public/private, pre-mod, anonymous, join question) | ✓ | ✗ | ✗ |
| Xóa group | ✓ | ✗ | ✗ |
Strict hierarchy: no role acts on a peer or superior (Group Mod cannot kick another Group Mod — Owner only).

**[Clarified 2026-10-21 — DEC-231, DEC-237: "ẩn/xóa" là một thao tác gỡ khỏi nhóm; chỉ Owner sửa tên, mô tả]**

### DEC-103: Group join flow matrix
|  | Không có join question | Có join question |
|---|---|---|
| Public | Join ngay lập tức | Cần duyệt (Owner/Mod xem câu trả lời) |
| Private | Cần duyệt | Cần duyệt (kèm câu trả lời) |
Rejected join requests can be resubmitted immediately, no cooldown (matches Facebook/LinkedIn/Discord group behavior). Owner/Mod use per-user block for persistent spam requesters instead of a system cooldown.

**[Amended 2026-10-21 — DEC-237, DEC-238: nhóm thành "vào ngay" thì duyệt luôn yêu cầu đang chờ; rút yêu cầu; bỏ chặn; chặn áp cho mọi cách vào]**

### DEC-104: Group content moderation layers on top of system-wide M08, does not replace it
Report (M08) and "System Mod/Admin can intervene anytime" (Phase 2, QA-016) remain fully in effect for group content. The group's AI-scan → Group Mod queue → Live flow is an additional publishing gate, not a substitute for system oversight. For posts belonging to a group: score≥0.9 → auto-reject (skips everyone); 0.5≤score<0.9 → mandatory Group Mod/Owner review regardless of pre-mod toggle state; score<0.5 → follows the group's pre-mod toggle (ON=review, OFF=publish direct). Group and System Mod each get their own claim-based "pending publish" queue (30-min timeout), separate from the Report queue. Posts not in any group keep the original M03/M13 flow unchanged.

**[Clarified 2026-10-21 — DEC-230, DEC-233: bài không có điểm quét; hàng chờ của nhóm chỉ Owner, Group Mod duyệt]**

**[Amended 2026-10-21 — DEC-240: bài của Owner không qua duyệt của nhóm]**

### DEC-105: Group deletion & member departure — content and point handling
Group deleted by Owner: soft-delete (content hidden from everyone including ex-members, not hard-deleted in DB). User's overall reputation is fully preserved — **AMENDED by DEC-113: the original exception deducting points tied to content lost with the group has been removed.** Group deletion is an indirect cause from the member's perspective (they didn't choose it, didn't violate anything), so no point deduction applies, consistent with DEC-113's direct-vs-indirect principle.
Member leaves or is kicked (group NOT deleted): their posts/comments remain exactly as-is, treated as the group's asset; author shown with real name; no point deduction. Kicked is treated identically to voluntary leave.

### DEC-106: Group size — no membership or ownership cap
A user may join unlimited groups and be Owner of unlimited groups simultaneously.

### DEC-107: Group ownership succession
Voluntary leave: Owner MUST designate a successor before leaving is allowed (blocking UI action). If the Owner is the group's only member, leaving deletes the group instead (with a warning shown).
Involuntary loss (ban/deactivate/delete — no chance to designate): auto-promote in order — (1) currently-active Group Moderator with longest tenure as Mod (a demoted ex-Mod doesn't count); (2) if none, longest-tenured Member; (3) if Owner was the sole member, the group is soft-deleted.

**[Clarified 2026-10-21 — DEC-232, DEC-237: mọi ban, vô hiệu hóa đều kích hoạt; Owner cũ quay lại là Member; thâm niên tính từ lần bổ nhiệm gần nhất]**

### DEC-108: Group visibility change (Public↔Private) — feed/post retention
Owner can change visibility anytime. Posts already delivered to a given user's feed remain visible to that user (not retroactively pulled) but become non-interactive once the group goes Private (comment/vote/report → error). New feed/search queries by non-members exclude these posts going forward.

**[Clarified 2026-10-21 — DEC-234: "đã hiện" là bài đang hiện trên màn hình đã tải]**

### DEC-109: No appeal path for group-level moderation
Actions taken by Group Mod/Owner within a group (e.g. pre-mod rejection, content removal) are final — no appeal mechanism, unlike system-level MOD/ADMIN actions which go through the Appeal module (M09).

**[Clarified 2026-10-21 — DEC-237: bài nhóm bị AI tự từ chối vẫn khiếu nại qua M09]**

### DEC-110: Private group discovery & invite permissions
Private groups are fully hidden from search/discovery; reachable only via invite/link. Any group member (Member, Group Mod, or Owner alike) can invite others — not restricted to Mod/Owner. Join flow reuses the mechanism established in DEC-103 (no separate targeted Invitation entity with accept/decline).

**[Clarified 2026-10-20 — DEC-210: thành viên vẫn tìm thấy nhóm Private của mình]**

**[Clarified 2026-10-21 — DEC-229, DEC-238: người được mời theo luồng tham gia; một link mời chung, không hết hạn; chặn áp cho mọi cách vào nhóm]**

### DEC-111: Group post cross-posting to main feed
A group post always appears in the feed of that group's own members, whether the group is Public or Private. For Public groups specifically, the post additionally appears on the main feed like an ordinary post (visible to non-members). Private group posts never surface on the main feed.

**[Clarified 2026-10-21 — DEC-234: người ngoài nhóm tương tác bài nhóm Public như bài thường]**

### DEC-112: Anonymous posting in group — opt-in, sticky, visible to Group staff
When a group's anonymous-posting toggle is ON, each member chooses per-post whether to post anonymously (not forced group-wide). If the Owner later turns the toggle OFF, previously-anonymous posts stay anonymous (the toggle only gates new posts, it does not retroactively reveal authors). Group Mod and Owner can see the real identity of an anonymous post's author, consistent with the system-wide MOD/ADMIN pattern (DEC-004, DEC-005).

## Phase 5 — M09 Amendment + M12: Gamification

### DEC-113: Content-tied point deduction — direct vs indirect principle, supersedes DEC-105's group exception
Points earned from upvotes on a piece of content are deducted ONLY when the content's disappearance is a DIRECT consequence of the point-holder's own action or own violation:
- Self-delete (post or comment, by its own author) → deducted
- Removed by Mod/Admin for that specific content's own violation → deducted
Points are PRESERVED when the disappearance is INDIRECT — caused by someone else's action, not the point-holder's own choice or fault:
- Group deleted by its Owner (a Member's content vanishes as a side effect, not their own action) — supersedes and removes DEC-105's original exception
- A comment cascade-hidden because its parent post was removed (for any reason) — the comment author didn't delete it themselves nor did their comment violate anything
Timing: self-delete → deduction applied only after the 7-day soft-delete window ends (hard-delete); if restored within the window, no deduction ever occurs (no separate refund mechanic needed). Mod/Admin removal for violation → deducted immediately, no waiting period.

**[Clarified 2026-10-21 — DEC-231: gỡ cấp nhóm không trừ điểm]**

**[Clarified 2026-10-23 — DEC-241: bình luận tự xóa trừ ngay; bình luận bị AI ẩn]**

### DEC-114: Badge permanence and audit trail
Badges are permanent once earned and are never revoked, even if the user's points later drop below the badge's threshold (including via a legitimate DEC-113 deduction). Rationale: a badge represents an achieved milestone (a historical fact), not a live status — consistent with common platform convention (Stack Overflow, Duolingo); avoids penalizing users for point changes outside their control; avoids the added complexity of live threshold recheck-and-revoke logic. Badge UI displays the date earned rather than re-displaying the threshold value, to avoid the appearance of inconsistency when current points sit below it.
Audit trail: threshold-based permanent badges get a single audit entry (the date first achieved — they cannot be "re-earned"). Periodic top-N titles (e.g. "Ngôi sao tuần", reset each cycle) get multiple audit entries — one per cycle win, since the same title can be won again in a later cycle.

**[Clarified 2026-10-23 — DEC-244: danh hiệu hiện trên hồ sơ, bảng Tuần]**

### DEC-115: Content Deletion Appeal — new appeal type, Post only (amends Phase 2 Appeal scope)
Amends the original Phase 2 decision that Appeal (M09) covers only Warning and Ban. A third appeal type, "Content Deletion Appeal," is added for content removed by Mod/Admin due to violation — **scoped to Post only, explicitly excluding Comment** (posts are higher-value assets; comment volume is too high for a sustainable appeal queue; consistent with DEC-004 treating posts as higher-value than comments).
Precedent reviewed: Reddit distinguishes admin-level content removal (formal appeal, ~6-month window) from subreddit-moderator removal (no platform-wide appeal — this maps to and confirms DEC-109's "no appeal for group-level moderation" staying unchanged); YouTube allows content-removal appeals within 1 year, strikes within 6 months. Given iShare's much smaller scale, a shorter fixed window of 30 days from removal is used instead.
Mechanism: a separate "Content Deletion Appeal" queue (distinct from Report and from Warning/Ban Appeal), reusing the existing claim-based 30-minute-timeout mechanism. Priority ranks lowest among the three appeal types: Ban > Warning > Content Deletion Appeal.
Outcome on success: (1) the content is restored, (2) any points deducted under DEC-113 are refunded, (3) any warning or ban issued together with that specific removal is also reversed, reusing the existing appeal-outcome mechanism from ISS-117 (warning: restriction lifted + warn count decremented; ban: immediate unban, log kept with an overturned flag).
Comments have no equivalent appeal path — points deducted for a Mod/Admin-removed comment remain permanently deducted.

**[Amended 2026-10-18 — DEC-198, DEC-200: thêm khiếu nại bài bị AI từ chối (gộp với cảnh cáo AI); một danh sách khiếu nại chung]**

**[Clarified 2026-10-18 — DEC-202: xử lý đi kèm chỉ bị lật một lần; đã bị từ chối riêng thì khiếu nại bài không lật]**


## Phase 5 — M12: Gamification Deep Dive

### DEC-116: Point weight — Post Star vs Comment Star
Post Star = 2, Comment Star = 1. A stronger 2:1 ratio (rather than a softer 3:2) was chosen specifically because it better serves DEC-004's original anti-farming rationale ("prevents spam-comment-to-farm-reputation") — a bigger gap makes comment-spamming clearly less rewarding than posting, and stays consistent with DEC-001 (content depth over breadth). The formula: `points = 2 × post_upvotes_received + 1 × comment_upvotes_received`.

### DEC-117: Periodic top-N title — cadence and N
The periodic top-N title ("Ngôi sao tuần") applies to the **Weekly** window only (not Monthly/All-time), with **N = 3** (top 3 users each week receive the title). N is a floor, not a hard cap: if multiple users tie exactly at the cutoff rank, all tied users receive the title that week (see DEC-123 for the tie mechanism) rather than applying a secondary tie-break rule.

**[Clarified 2026-10-23 — DEC-243: chỉ người có điểm chu kỳ > 0]**

### DEC-118: HEAVY warn — leaderboard exclusion (amends DEC-079)
A user at **HEAVY** warning level is excluded from the public leaderboard for the duration of their probation period. This is a deliberate, explicit exception carved into DEC-079's "fully private" warning-status guarantee — the only public-facing consequence of a warning. Does not apply to LIGHT or MEDIUM levels. Rationale: losing leaderboard visibility functions as an additional privilege loss at the most severe warning tier (consistent with HEAVY already losing posting/commenting rights per DEC-079), and the stakeholder accepted the trade-off that this may let observant peers infer a HEAVY warning is in effect, despite DEC-079's original bullying-prevention intent — deemed an acceptable, bounded exception rather than a full reversal of that principle.

**[Clarified 2026-10-23 — DEC-242, DEC-246: ẩn sau lúc chốt; xét lúc chốt khi trao danh hiệu]**

### DEC-119: Vote retraction
Upvotes are toggleable — a user can retract their own upvote by clicking again. The recipient's point total is deducted immediately upon retraction, symmetric with how it was added.

### DEC-120: Self-vote prohibition
Self-voting is not permitted. The vote button is hidden/disabled on a user's own post or comment, blocking the fraud vector at the source rather than allowing the click and silently discounting it.

### DEC-121: Leaderboard computation — single periodic job
Leaderboard ranking (across all three windows — Weekly/Monthly/All-time) is computed by a single cron job running every 60 minutes, not real-time per vote. Each run does two things: (1) refreshes the cached ranking used for live in-progress display, and (2) checks whether a cycle boundary (week/month) has closed since the last run — if so, it computes that cycle's final ranking using an exact date-range query (not the display cache) and triggers title award + notification for it. This keeps the architecture to one mechanism instead of two separate jobs, at the cost of up to 60 minutes of delay between a cycle's true close and its title-award notification — the winner computed is always correct because the finalization query is boundary-exact regardless of when the job happens to run.
Individual point totals (on a user's own profile) remain real-time, unaffected by this batching — only the aggregate ranked list is batched.
No historical full-leaderboard view is provided for past cycles (only the current state of each window is shown); past periodic-title wins remain permanently visible through the title/badge audit trail (DEC-114), which is a much narrower record than a full historical ranking snapshot.

**[Amended 2026-10-23 — DEC-242: bảng Tuần, Tháng hiện chu kỳ vừa chốt]**

**[Clarified 2026-10-23 — DEC-247: lịch sử danh hiệu tuần chỉ lưu, không hiển thị]**

### DEC-122: Banned account — display treatment (extends DEC-118's exception to DEC-079)
A **BANNED** account is also excluded from the public leaderboard for the duration of the ban, consistent with the HEAVY-warn treatment in DEC-118 (a ban is a more severe sanction than a HEAVY warning). Unlike a HEAVY warning, however, a banned user's profile, posts and comments remain visible to other users as normal — not hidden or tombstoned — because a ban is reversible (via appeal, DEC-089) and distinct from account deletion (DEC-019); any specific violating content is handled separately through the existing M08 report/moderation flow, independent of the account-level ban action. A **"Tài khoản đã bị khóa"** ("Account has been locked") label is shown everywhere the banned user's name appears — on their profile page and next to their author name on every post/comment they've made — a deliberately public label, unlike the strict privacy DEC-079 applies to warning status, since a ban is treated as a more transparent, public-facing sanction.

**[Clarified 2026-10-23 — DEC-242, DEC-246: ẩn sau lúc chốt; xét lúc chốt khi trao danh hiệu]**

### DEC-123: Leaderboard/title tie handling
Two mechanisms, kept consistent with each other:
- **Leaderboard display ranking**: users with equal points share the same displayed rank (standard competition ranking, e.g. two users tied at rank 3 both show "3", the next user shows rank 5) — no secondary tie-break criterion needed.
- **Weekly top-N title cutoff**: if multiple users tie exactly at the N=3 cutoff, all of them receive the title for that week (N acts as a floor, not a hard cap) — same "no arbitrary tie-break" philosophy as the display ranking.

---
## Phase 5 — M14: Feed & Discovery

### DEC-124: Trending Post — decay formula (new, distinct from DEC-052)
DEC-052 (Trending Topic/Tag, M05) stays unchanged — rolling 7-day hard window, no decay. Trending Post (new sub-view under M14's Trending tab) uses a separate, smoother formula: exponential half-life decay, `weight = 0.5^(age_days / 7)` (weight halves every 7 days), hard cutoff at 28 days (4 weeks) — posts older than that are excluded entirely regardless of residual weight. Base engagement score unchanged: `Σ(weight × (1 + upvotes×2 + comments×1))`, recalculated every 15-30 min (same cadence as DEC-052). 28-day cutoff chosen as a clean multiple of the 7-day half-life (residual weight ≈6.25% at cutoff — negligible, avoids an abrupt "cliff" effect vs. shorter windows like 21 days which would cut off content still at 12.5% weight).

### DEC-125: M14 Feed structure — 4 tabs, no AI-driven personalization tab
M14 Feed consists of 4 tabs: **Trending** (3 sub-views: Post/Topic/Tag), **Following** (chronological, from Follow targets established in M07 — User/Topic/Post), **Group** (chronological, aggregated from all groups — Public+Private — the user has joined), **Newest** (chronological, site-wide, excluding Group-sourced posts). There is no separate algorithmic "For You" personalized-ranking tab — this simplifies scope and removes M14's dependency on M13 (AI Layer); M14 now depends only on M03 (Post) and M05 (Topic & Tag). Group Public posts cross-posted to the main feed (per DEC-111) are included in Trending Post and the Group tab, but excluded from Newest (Newest is kept as a pure non-group content stream).

**[Amended 2026-10-20 — DEC-215: tab Following không còn bài đang theo dõi]**

### DEC-126: Guest access to Feed tabs
Guest (unauthenticated) can view Newest and the full Trending tab (all 3 sub-views) without restriction — consistent with the existing Guest browse permissions (QA-011) and the SEO/discoverability rationale behind them. The Following and Group tabs remain visible to Guest but are gated behind login. All interactions (upvote, report, bookmark, follow, join) require login regardless of tab, per the existing Guest permission matrix (QA-011).

### Issues Closed
ISS-166 through ISS-177, ISS-185 through ISS-188 (see issue-queue.md / qa-log.md Phase 5 — M14 section for full detail)

---
## Phase 6 — Cross-cutting Concerns

### DEC-127: Timezone & date handling
All timestamps stored as UTC in the database (standard practice). All date/week boundary calculations (Weekly leaderboard reset — M12, 30-day appeal deadline — M09, warn probation 5/10/15 days — M08, Today/7d/30d presets — M15, 7-day post soft-delete window — M03, etc.) and all UI display are computed against **Asia/Ho_Chi_Minh (UTC+7)**, fixed, no DST (Vietnam does not observe daylight saving). Chosen because the entire target user base is Vietnamese students with no multi-timezone need, and a fixed +7 offset introduces no technical edge cases year-round.

### DEC-128: i18n/localisation scope
Vietnamese-only at MS1 (no language switcher), but the UI is built with an i18n-ready architecture — UI strings externalized via an i18n key library (e.g. i18next-style), with a single active locale `vi`. This avoids a full UI-string refactor if another language is added later. Important distinction clarified during interview: UI i18n only localizes the "chrome" (labels, buttons, system messages) — it does NOT translate user-generated content (posts/comments remain in whichever language the author wrote them). Multilingual CONTENT support (translation, content-language tagging/filtering) is a materially different feature, outside the original draft's scope — noted as an open future idea, not built at MS1.

### DEC-129: Data retention — audit log & chat messages (general hard-delete principle)
Audit/mod action log and chat message content are both kept indefinitely — no hard-delete, no archival/cleanup cron — consistent with the existing Notification retention decision (DEC-071: "no retention policy"). Rationale: log/audit-type data is conventionally never deleted in production systems (compliance/transparency/trace value), unlike user content which users may legitimately want removed. Additional technical reason: many other tables reference audit log/chat message rows via FK (reports reference message_id, warn actions reference report rows, etc.) — hard-deleting them risks breaking referential integrity or losing investigative context.
**General principle established for all future hard-delete decisions in this project:** hard-delete only when it is genuinely safe — i.e. there is a clear justification (privacy/PII that must be erased, or cleaning up content a user deliberately deleted with a sensible UX reason) AND it does not break referential integrity with other tables that reference it. Existing hard-delete decisions (Post 7-day soft-delete then hard-delete — DEC-011; Comment permanent delete — DEC-038; Account PII wipe on DELETED — DEC-019) all satisfy this principle and remain unchanged.

**[Amended 2026-10-11 — DEC-156: tin nhắn, nhật ký của tài khoản đã xóa hiện "[Người dùng đã xóa]", vẫn tra cứu qua username]**

### DEC-130: File/media upload — no virus/malware scanning
No dedicated malware scan layer is added. The existing per-feature type/size whitelist (image formats only — JPEG/PNG/WebP, size caps per feature) combined with CDN-side (Cloudinary) image re-encoding/transcoding on upload (which naturally strips malicious payloads hidden in image files) is considered sufficient for MS1, given upload scope is image-only (no executable file types accepted).

**[Amended 2026-10-11 — DEC-160: tài liệu đính kèm bài vẫn được, không quét virus]**

### DEC-131: AI — third-party data privacy disclosure
A public Privacy Policy / Terms of Service page is added, explicitly disclosing that publicly posted content (posts/comments) is processed by a third-party AI service (OpenAI — Moderation API for content scanning, Embedding API for semantic search). Linked from the footer and/or the registration flow. Low-cost (a single static content page) but materially increases transparency — judged especially important given the user base includes minors (THPT students).

**[Amended 2026-10-07 — DEC-146: công bố thêm Topic Suggestion, kể cả nội dung chưa đăng]**

**[Amended 2026-10-11 — DEC-154: ghi "nhà cung cấp dịch vụ AI", không nêu tên; trang thuộc M01]**

### DEC-132: AI — Topic Suggestion hallucination handling
Topic Suggestion (GPT-4o-mini) output is validated against the system's fixed 11-topic whitelist. If the returned topic does not match, it is treated as a suggestion failure: a non-blocking error is shown ("Không thể gợi ý chủ đề lúc này, vui lòng chọn thủ công") and the user selects manually. This deliberately reuses the exact same UX pattern already established for AI transient failure (DEC-099: timeout/retry exhausted) — even though the underlying technical cause differs (hallucination vs. timeout), the user-facing experience is identical, requiring no new UI pattern.

**[Amended 2026-10-07 — DEC-141, DEC-144: đối chiếu danh mục Topic hiện tại; bỏ Topic sai, giữ Topic đúng]**

### DEC-133: AI — raw output logging
Every AI call (Moderation API, Embedding, Topic Suggestion) has its raw response logged to a dedicated `ai_decision_log` table, linked to the relevant post/comment. Distinct from the existing admin/mod action audit log (DEC-081/094), which logs human actions — this logs AI-made decisions specifically. Serves two purposes: (1) provides real usage data to tune the currently-placeholder 0.9/0.5 confidence thresholds (DEC-098), (2) gives Moderators/Admins an evidence trail when handling a Content Deletion Appeal (M09/DEC-115) where a user disputes an AI-driven rejection.

**[Clarified 2026-10-19 — DEC-207: mỗi lời gọi một bản ghi, kể cả thất bại; không ghi tóm tắt, embedding truy vấn; không sửa, không xóa; chỉ xem khi xét khiếu nại]**

### Issues Closed
ISS-189 through ISS-196 (see issue-queue.md / qa-log.md Phase 6 section for full detail). One item deferred: **OPEN-005** — no general event-tracking infrastructure for MS1 (formalizes the implicit decision already made at M15/QA-242).

## Phase 7 prep — Tech Stack (OPEN-002, partial)

### DEC-134: Backend/Frontend stack and SSR deferral
Backend is Java + Spring Boot. Frontend is ReactJS built with Vite as a client-side SPA (no server-side rendering) for MS1. SEO/SSR is deliberately deferred and tracked as **OPEN-006**; it does not change Guest read access (QA-011), which stays as decided. QA-234/ISS-174 SSR note is amended accordingly. Rationale: MS1 is demo-only and prioritises core features (QA-002/QA-008); the team has not used Next.js and a self-built or learned SSR layer is a schedule risk across 16 modules. Known consequences: weaker search-engine indexing and no link-preview metadata when sharing URLs (e.g. Zalo/Facebook) until OPEN-006 is resolved. Mitigation (approach, not a requirement): keep API calls in a separate layer and components presentational so a later move to Next.js or another SSR framework is cheaper. UI Kit: a shared in-app UI Kit (component library) will be built for the whole application after the design phase; it is an internal implementation approach inside the frontend codebase, not a separately submitted deliverable and not a new module or scope item (it must respect i18n keys, DEC-128, and the display timezone, DEC-127). The Kit's core requirement is a unified set of common UI components used across the app; building it on top of an existing base library is acceptable (stakeholder: either is fine, the common UI set is what matters). The base library will be chosen after the design is available (**OPEN-007**); the stakeholder currently leans towards MUI (a preference, not a decision). Not decided here: the final base library, and the remaining OPEN-002 items (email provider, AI_ENABLED storage, realtime channel, hosting, confirmation of implied technologies, academic constraints).

### DEC-135: Realtime channel — SSE only
Server-to-client realtime uses Server-Sent Events (SSE) for both chat (M16) and in-app notifications (M07); WebSocket is not used. Chat sending remains a normal POST; read receipts remain POST + SSE (QA-212). Notifications keep DB write as source of truth with best-effort push, now over SSE (QA-131 amended). Feed new-post banner stays on polling (QA-239). Rationale: no feature requires true two-way low-latency communication, and a single mechanism is simpler in a 3-month schedule. Online/offline presence was raised (client heartbeat ping) and explicitly dropped; it is not a requirement. Known limit: in-memory pub/sub supports a single server instance, accepted at demo scale (to be recorded in Phase 7 NFRs).

### DEC-136: Email delivery — Spring Mail over standard SMTP
Outgoing email (magic-link, reactivation OTP, security/ban notices; scope unchanged from M07) is sent with Spring Mail (`spring-boot-starter-mail` / `JavaMailSender`) over standard SMTP, with host/port/credentials supplied via environment configuration. For MS1 the SMTP source is the free tier of an email provider; the specific provider is chosen at implementation time and does not affect the spec. Gmail SMTP may be used in local development only. Sender-domain authentication (SPF/DKIM) is required before real production use, not for the MS1 demo. Switching provider is a configuration change, not a code change.

### DEC-137: Confirmed technology stack (closes OPEN-002)
Technology stack for iShare, confirmed by the stakeholder: Backend Java + Spring Boot (DEC-134); Frontend ReactJS with Vite as a client-side SPA, no SSR at MS1 (DEC-134, OPEN-006), with an in-app shared UI Kit whose base library is chosen after design (OPEN-007); Database PostgreSQL with pgvector (plus the already-decided pg_trgm and `to_tsvector('simple', unaccent())` full-text search); Cloudinary for avatars/attachments; OpenAI for Moderation API, text-embedding-3-small and GPT-4o-mini (Topic Suggestion); Tiptap/ProseMirror editor storing JSON content; JWT authentication with rotating refresh tokens (existing Session decision); Spring Mail over standard SMTP (DEC-136); SSE for all server-to-client realtime (DEC-135); AI toggle lives in the Admin Panel system config (DEC-092/093); no hosting/deployment at MS1 (QA-002, ISS-201). No academic technology constraints (ISS-202). Additions to the stack will be discussed when needed.

### Issues Closed
ISS-197 through ISS-203 and ISS-029 (see issue-queue.md / qa-log.md QA-256–QA-263). OPEN-002 closed. Deferred: **OPEN-006** (SEO/SSR), **OPEN-007** (UI Kit base library). OPEN-001 (AI budget) is now unblocked. Deferred: **OPEN-006** (SEO/SSR), **OPEN-007** (UI Kit base library).

## System Requirement prep — Privacy & Consent

### DEC-138: Consent to Privacy Policy/ToS is mandatory at registration
A user cannot register unless they explicitly consent to the Privacy Policy/ToS (the public page decided in DEC-131). Privacy is a mandatory part of the product; its detailed scope (personal-data inventory, user rights, handling of users under 18, legal basis, and how permanent retention in DEC-129 relates to PII erasure on account deletion) is deliberately deferred and tracked as **OPEN-008**. Source: QA-264.

**[Amended 2026-10-11 — DEC-155, DEC-157: lưu phiên bản đã đồng ý, đồng ý lại khi chính sách đổi; ô đồng ý kèm cam kết dưới 16 tuổi]**

### Issues Closed
ISS-204 (partial; see OPEN-008).

## System Requirement prep — Documentation approach

### DEC-139: System Requirement (SR) documentation approach
SR documents are written per module, in Vietnamese (English kept for necessary technical terms), following the structure of the stakeholder's reference sample: 1 Overview, 2 Terms and Abbreviations (terms used in that document), 3 Input Information, 4 Functional Overview (4.1 laws/standards only if the stakeholder names them, otherwise 'Không có'), 5 Functional Requirements (per feature: upper-level requirement, rationale, lower-level requirements; State Transitions where the module has statuses; HMI Requirements and Screen Transitions are placeholders until design), 6 Revision History. Each document is self-contained for terms and role-based permissions. A behaviour is written in exactly one owner module; other modules reference it by ID. Source and Basis (Stated/Derived) are kept in a traceability appendix, not in the body. Milestone and priority are stated once in section 5.1, with labels only on exceptional requirements. Header: document ID, project, module, status, version, date, author (Phạm Văn Đức); no reviewer/approver field. Files are saved under `.agents/.claude/system_analysis/output/specs/` (audit reports under `specs/audit/`). Process: an Author agent drafts; an independent Auditor agent only audits (source-to-requirement coverage matrix plus a rule checklist, partly machine-checked) and never edits; the Author fixes per the report; at most 2 rounds, then the stakeholder decides. Every GAP, ambiguity or suggestion is raised to the stakeholder one at a time; answers are recorded in the registers (QA/DEC) and the Author updates the SR accordingly. SR is written now; Phase 7 and 8 follow. First run is a pilot on one module (proposed: M05). Requirement ID convention: see the amendment below. This decision deliberately departs from two rules in BA-INTERVIEW-RULES (English-only output; no spec before Phase 9). Source: QA-265.

**[Amended 2026-10-04 — QA-266]** Details fixed for the pilot: (1) ID convention — project prefix `ISH`; document `ISH-SR-Mxx` (routing file `ISH-RT-Mxx`); upper-level requirement `ISH-Mxx-nnn`, lower-level `ISH-Mxx-nnn.k`; open point `OP-Mxx-nn` (temporary, Appendix B only); audit finding `AUD-Mxx-nn`; source items keep their ISS/QA/DEC/OPEN IDs; IDs are permanent (never renumbered or reused, gaps allowed); section numbers 5.x are not IDs. (2) Requirement sentences use Vietnamese EARS templates with 'hệ thống' as the only subject of 'phải', plus INCOSE-style rules (atomic, measurable, no escape clauses, no pronouns, no solution or data-model terms). (3) Content that is not a functional requirement (data model → Phase 8, NFR → Phase 7, HMI, process notes, other-module behaviour, superseded items, omissions) goes to a per-module routing file `specs/routing/ISH-RT-Mxx.md`, not into the SR; every source item of the module must appear either in SR Appendix A or in the routing file. (4) Appendix A = traceability (ID | Source | Basis Stated/Derived | Note); Appendix B = temporary open points. (5) Normative rules live in `.agent-instructions/system_analysis/shared/SR-DOCUMENT-RULES.md`; Author role `.agent-instructions/system_analysis/roles/sr-author/AGENT.md` (Auditor role `roles/sr-auditor/` later); helper scripts `inventory.py` and `check_sr.py` live in `.agent-instructions/system_analysis/shared/sr-tools/`. [Layout updated 2026-10-04 when the instruction set was restructured into roles/ and shared/.] Source: QA-266.

**[To be superseded 2026-10-07 — stakeholder]** The process and convention parts of DEC-139 and its QA-266 amendment are marked to be superseded by the new Functional Requirement skill and will be replaced by a new DEC when that skill is confirmed: the Author/Auditor process and audit rounds, raising every GAP one at a time, the `ISH-*`, `OP-*` and `AUD-*` ID convention, the Vietnamese EARS sentence rules, the routing file and Appendices A/B, the `specs/` file locations, and the references to SR-DOCUMENT-RULES, the sr-author/sr-auditor roles and the sr-tools scripts. The M05 pilot run was discarded. Still in force until then: one document per module, self-contained terms and permissions; Vietnamese with English kept for necessary technical terms; requirements written now, before Phase 7/8; the reference-sample section structure; one owner module per behaviour, other modules reference it; sources kept out of the body; milestone/priority stated once; header fields.

### Issues Closed
ISS-205.

---

## Functional Requirement — M05: Topic & Tag

### DEC-140: M05 — AI Classification scope and Topic structure (confirmations)
- AI suggests Topics only; it never suggests or assigns Tags (Tags stay fully user-decided, per QA-017). The draft and glossary wording "AI suggests Topic and Tags" is superseded.
- No Moderator review step for suggestion results: the author adjusts the pre-ticked suggestions and submits (DEC-050 flow unchanged).
- The Topic taxonomy is flat (DEC-047); the "2 tiers Category → Topic" of QA-033 is superseded. QA-033's point that grade_level is an independent optional Post field stays (M03).
Source: QA-267, QA-268, QA-269

### DEC-141: M05 — Topic catalog management (Admin only)
- The 11 Topics of DEC-048 are the initial catalog. Only ADMIN can add a Topic; the catalog has no size limit; a new Topic is not assigned to existing posts.
- Topic names are unique. Comparison ignores letter case and extra whitespace (leading, trailing, repeated inner spaces) but keeps diacritics: "Tin học" = "tin học" = " Tin  học "; "Tin hoc" ≠ "Tin học".
- Topic rename is not supported. To fix a name, Admin adds the correct Topic and merges the old one into it.
- Merge is ADMIN only. All posts of the source Topic move to the target (a post holding both keeps the target once). The source Topic is then deleted automatically. Users following the source Topic are moved to follow the target (already-followers unchanged).
- Delete is ADMIN only, and only when the Topic has no non-draft post (pending, published, self-hidden, rejected, and deleted posts still inside the 7-day recovery window all count). Drafts holding that Topic lose it (drafts may have 0 Topics, DEC-142). Follows of a deleted Topic are removed.
- Topic Suggestion validates against the current catalog, not a fixed 11-topic list.
- MOD no longer edits or merges Topics (amends DEC-090 "Shared with Mod: Topic edit/merge"). Tag crisis soft-delete stays shared MOD/ADMIN.
Source: QA-270, QA-272, QA-278, QA-279, QA-280

### DEC-142: M05 — Topics and Tags on posts (drafts, edits, browse)
- The 1–3 Topic rule is enforced on submit only; a draft may hold 0 Topics (still max 3 Topics, max 5 Tags).
- When editing a submitted post, the author may change its Topics and Tags within the same limits.
- MOD and ADMIN may change Topics and Tags on any user's post within the same limits. The author is not notified and the change is not recorded in the public post edit history (DEC-037).
- The author may use Topic Suggestion while editing a submitted post, under the same rules (including feedback recording). MOD/ADMIN changing someone else's post do not use suggestion.
- "Browse" in M05 means viewing the Topic and Tag lists. Viewing the posts of a Topic or Tag is done through M06 Search filters; M05 has no per-Topic/Tag post page.
Source: QA-273, QA-274, QA-275, QA-277, QA-288, QA-289

### DEC-143: M05 — Tag characters, display, re-activation
- A Tag name contains only letters (including Vietnamese diacritics), digits and underscore, with at least one letter. Valid: #XácSuất, #đạo_hàm, #lớp12, #covid19. Invalid: #covid-19, #node.js, #c++, #12, #___.
- The "#" prefix is display-only and is not counted in the 30-character limit.
- Tags are displayed everywhere in their normalized lowercase name (e.g. #xácsuất); no original casing is stored.
- MOD and ADMIN may re-activate a disabled Tag: it reappears in autocomplete, Trending Tag, the Tag list and on posts still linked to it. Text typed as "#name" while the Tag was disabled stays plain text.
Source: QA-276, QA-284

### DEC-144: M05 — Topic Suggestion details
- The 20-word minimum is counted over title + content_text; a word is a whitespace-separated token (each Vietnamese syllable counts as one word).
- If the AI returns some Topics outside the catalog, those are dropped and the valid ones kept; the suggestion fails only when no valid Topic remains.
- The 10 requests per user limit (DEC-100) uses a sliding 60-second window.
Source: QA-281, QA-282, QA-283

### DEC-145: M05 — Trending Topic/Tag formula (supersedes the formula of DEC-052)
- Score of a Topic or Tag = sum of interactions that happened inside the sliding 7-day window on its posts, regardless of when the post was published: post published in the window = 1, post upvote = 2, comment (replies included) = 1, bookmark = 1. Retracted interactions (removed upvote, deleted comment, removed bookmark) do not count. A post with several Topics/Tags counts for each. No decay.
- Only posts visible on the main feed count: published and not hidden by moderation, including Public-group posts, excluding Private-group posts. Comment upvotes do not count. Disabled Tags have no score.
- Post views are not counted at MS1 (deferred; requires event tracking, see OPEN-005).
- Freshness: every interaction is reflected in the score at most 30 minutes after it happens; the recalculation cycle stays within 15–30 minutes.
- Only Topics/Tags with score > 0 are listed. Order: score descending; ties broken by the number of posts published in the window (descending), then by name A–Z. Each item has its own rank.
Example (computed 07/10 10:00, window from 30/09 10:00): post A published 05/10 with 3 upvotes, 2 comments, 1 bookmark in window → 1 + 6 + 2 + 1 = 10; post B published 20/09 with 2 upvotes in window → 4; post C published 30/09 09:00 with 1 comment on 01/10 → 1; Topic total 15.
Source: QA-271, QA-285, QA-286, QA-287

### DEC-146: M05 — Moderator action logging and AI disclosure
- Disabling a Tag, re-activating a Tag, and changing Topics/Tags on another user's post are recorded in the moderation audit log (DEC-081 fields: actor, action type, target, reason optional, timestamp), for MOD and ADMIN alike. ADMIN actions also remain in the admin action log (DEC-094).
- The Privacy Policy / ToS page (DEC-131) additionally discloses that when a user clicks "Gợi ý topic", the title and content of the post being composed or edited, including unpublished content, are sent to a third-party AI service to suggest Topics.
Source: QA-290, QA-291

### Issues Closed
ISS-207 – ISS-231.

---

## Functional Requirement — M01: Authentication & Account

### DEC-147: M01 — Google sign-in linking (amends DEC-010, DEC-065)
- Signing in with Google whose email matches an existing email account links Google to that account automatically, without confirmation, whether or not the account's email was verified. If it was not verified (verify_level NONE), it becomes EMAIL_VERIFIED and the user continues at Step 3. Accepted risk: someone who registered first with another person's email keeps their password.
- After linking, the owner is notified in-app and by email (security group, like password change). DEC-065 gains the event "Google account linked — In-app: Yes, Email: Yes".
- Source: QA-292, QA-297

### DEC-148: M01 — Credential and identity rules (amends DEC-015, DEC-019)
- Password: 8–64 characters; no required character classes; any character allowed, including spaces and Vietnamese diacritics; no trimming. A new password (change or reset) must differ from the current one. No common-password blocklist, no comparison with email/username.
- username: letters a–z, A–Z, digits, "_" only, 3–20 characters (DEC-015). Uniqueness and @mention search are case-insensitive; displayed with the case the user typed ("Duc_PV" and "duc_pv" are the same username).
- display_name: 1–50 characters after trimming leading/trailing spaces; letters (with diacritics), digits, spaces and . , - _ ' ( ) only; no emoji or other symbols; not unique (DEC-015).
- Both names can be changed any number of times on the Edit Profile page (M02) under the same rules; a username given up by a rename becomes available immediately.
- When an account becomes DELETED: its email is released and can register a new account; its username is retired permanently and can never be taken again.
- Source: QA-295, QA-296, QA-305

### DEC-149: M01 — Deactivation window, reactivation and deleted-account display (clarifies DEC-019, amends QA-018)
- The 14-day window is exactly 14 × 24 hours from the moment of deactivation (e.g. deactivated 01/10 21:00 → reactivation possible until before 15/10 21:00, DELETED at 15/10 21:00).
- One warning email is sent 24 hours before automatic deletion.
- Reactivation page: the user enters only the account email and receives a 6-digit code by email. The code is valid 15 minutes; a code becomes invalid after 5 wrong entries; a new code can be requested at least 60 seconds after the previous one. Correct code → ACTIVE and the device is signed in automatically.
- Comments of a DELETED account keep their content; author shown as "[Người dùng đã xóa]" with the default avatar. This replaces QA-018's "[Bình luận từ tài khoản đã xóa]" tombstone.
- Source: QA-293, QA-299, QA-300, QA-302

### DEC-150: M01 — Moderator view of deactivated authors (scope extension)
- While an account is DEACTIVATED, MOD and ADMIN can see its hidden posts and the real identity behind the "Tài khoản tạm thời vô hiệu hoá" author label, so that deactivation cannot be used to escape moderation (same reasoning as QA-015). Regular users see the replacement display. After DELETED, personal data is erased, so there is no identity left to show.
- Source: QA-294

### DEC-151: M01 — Sessions, magic links, password reset (amends DEC-016, DEC-017, DEC-065)
- Each refresh issues a new refresh session valid 30 days from that refresh (e.g. sign-in 01/10, refresh 25/10 → expires 24/11).
- Every magic link (verification, password reset) is single-use; sending a new link invalidates the previous one.
- A successful password reset also sends the "password changed" notification in-app and by email.
- "Forgot password": every request, including an email with no account, shows the same message "Liên kết đã được gửi, vui lòng kiểm tra email của bạn". A DEACTIVATED account gets no link and is pointed to the reactivation page. A BANNED account may reset its password, only so it can sign in to the locked screen and submit an appeal (DEC-085); after the reset it still sees only the locked screen.
- Changing password (in Settings) or profile information is available only while the account is ACTIVE.
- Source: QA-298, QA-302, QA-306, QA-308

### DEC-152: M01 — Registration pause, maintenance mode, ban expiry, locked screen (amends DEC-092, DEC-080)
- While the registration pause (DEC-092) is on, new accounts cannot be created by email or by first-time Google sign-in; linking Google to an existing account still works; accounts that finished Step 1 can still complete Steps 2 and 3.
- While maintenance mode is on, only ADMIN can sign in; other users are refused and their existing sessions cannot be used.
- A temporary ban returns the account to ACTIVE automatically at the moment it expires.
- The OK button on the locked (banned) screen signs the user out.
- Source: QA-303, QA-304, QA-307

### DEC-153: M01 — @mention list and notification (amends DEC-020, DEC-045)
- Within the same priority tier, users who match the typed text more closely come first.
- A mention inside a comment uses the context of the post containing the comment (post in a Group → Group ordering).
- The suggestion list never shows DEACTIVATED, DELETED or BANNED accounts, nor accounts that have not completed Step 3.
- Existing mentions of a DEACTIVATED or DELETED account show the replacement name ("Tài khoản tạm thời vô hiệu hoá" / "[Người dùng đã xóa]") and do not link to a profile.
- The mention notification is sent when the content becomes publicly visible (after the pre-publish scan); editing content notifies only newly added mentions.
- Source: QA-301

### DEC-154: M01 — Privacy Policy/ToS page: data categories, AI wording, legal basis, sections (amends DEC-131; narrows OPEN-008)
- The page groups data into four categories, without field-level detail: (1) account and profile information, including the email and name received from Google when signing in with Google; (2) content you create (posts, comments, messages, attachments, likes, bookmarks); (3) data kept for community safety (reports, warnings, bans, appeals); (4) data processed by an AI service provider. Login sessions are not mentioned. The field-level inventory is kept in the FR documents for design.
- AI wording: "processed by an AI service provider" — the provider is not named (amends DEC-131's naming of OpenAI; the disclosure that content leaves iShare is kept). Other external services (sign-in, image storage, email) are covered by one general section; no provider names; the page states that iShare does not sell user data.
- Legal basis: consent at registration and at each new policy version; data retained after account deletion is kept for community safety.
- Sections: data collected; purposes; external services; retention; your rights; users under 16; policy changes; contact. Terms of Service part: community rules and prohibited content; moderation and warnings; account locking and appeals; rights over posted content. Exact wording is written later; the contact address is decided at deployment.
- The page belongs to M01 (shown and consented to in the registration flow).
- Source: QA-309, QA-313, QA-314

### DEC-155: M01 — Consent record and re-consent (amends DEC-138)
- The system records the time and the policy version each user consented to.
- Users are asked to consent again only when the policy changes to a new version, at their next sign-in. A user who declines cannot use the system and may only sign out or deactivate the account; they are asked again at the next sign-in.
- Withdrawing consent is done by deactivating the account (existing flow, DEC-019).
- Source: QA-310, QA-315

**[Amended 2026-10-11 — DEC-158: hỏi lại ở lần mở ứng dụng kế tiếp; phiên bản do đội phát triển phát hành khi triển khai]**

### DEC-156: M01 — Data on account deletion (amends DEC-019, DEC-129)
- On DELETED, erased: email (released, DEC-148), password, Google link, display_name, avatar, bio, Lớp/Khối, all login sessions, bookmarks, follow relations (both directions), consent records.
- Kept: username (retired, DEC-148), account state, role; posts stay hidden (DEC-019); comments show "[Người dùng đã xóa]" (DEC-149); upvotes already given still count for their recipients without identifying the giver.
- Chat messages, moderation logs and AI decision logs are kept (DEC-129): message content stays, sender shown as "[Người dùng đã xóa]"; logs stay linked to the deleted account through its retained username so MOD/ADMIN can investigate. The policy page states that some data is kept after deletion for community safety.
- Source: QA-311, QA-312

**[Amended 2026-10-11 — DEC-159: xóa cả theo dõi Topic, bài viết; giữ phản hồi gợi ý Topic]**

### DEC-157: M01 — Data copy right and users under 16 (amends DEC-138; narrows OPEN-008)
- No "download my data" feature in MS1. The policy page states the right to obtain a copy; how to request it is announced at deployment.
- No age question. The Step 1 consent checkbox reads: "Tôi đồng ý với Điều khoản và Chính sách quyền riêng tư. Nếu dưới 16 tuổi, tôi đã được cha mẹ hoặc người giám hộ đồng ý." The policy page has a section for users under 16. A parent-confirmation flow can be added later if real deployment requires it.
- Source: QA-315, QA-316

### DEC-158: M01 — Re-consent timing and policy versioning (amends DEC-155)
- "Next sign-in" in DEC-155 means the next time the user opens the app, including while an existing login session is still valid; the user must consent to the new version before continuing.
- New policy versions are released by the development team as part of a deployment: the page content and its version number live in the codebase (same approach as policy constants, DEC-090). There is no Admin screen for editing or publishing the policy.
- Source: QA-317, QA-318

### DEC-159: M01/M05 — Follows and Topic-suggestion feedback on account deletion (amends DEC-156)
- On DELETED, all follows held by the account are erased: users, Topics and posts it followed, plus users following it. Follower counts of those Topics and users decrease accordingly.
- Topic-suggestion feedback records (M05: suggested Topics vs. chosen Topics) are kept, like AI decision logs (DEC-156), for AI quality evaluation (M13); they contain no post content and no longer identify the user.
- Source: QA-319, QA-320

**[Amended 2026-10-20 — DEC-215: không còn theo dõi bài viết]**

### Issues Closed
ISS-232 → ISS-260

---
## Functional Requirement — M03: Post & Content

### DEC-160: M03 — Document attachments kept without malware scanning (amends DEC-130)
- Posts keep document attachments as in DEC-035 (PDF/DOCX/XLSX/PPTX, 20 MB/file, max 3), alongside images (JPEG/PNG/WebP, 5 MB/file, max 10).
- Documents are not scanned for malware. DEC-130's "image-only" premise does not cover them; the stakeholder accepts this risk for MS1 and will revisit it as a security item later.
- Source: QA-321

### DEC-161: M03 — Moderation state of posts (clarifies DEC-032, amends DEC-013)
- A new post starts with moderation state NORMAL; while it is PENDING, it is hidden by its publish state.
- "Removed by Mod/Admin" (DEC-011, DEC-113, DEC-115) is the moderation state HIDDEN; no separate "removed" state.
- Re-scan after editing a PUBLISHED post: score < 0.5 → unchanged; score ≥ 0.5 (including ≥ 0.9) → FLAGGED (hidden, awaiting Mod); scan failure → unchanged, the post stays visible. The 0.9 auto-reject applies only to newly submitted posts.
- Source: QA-322, QA-323

**[Amended 2026-10-14 — DEC-185: quét lại cả khi hiện lại bài tự ẩn đã sửa trong lúc ẩn]**

### DEC-162: M03 — Edit, delete and restore by post state; restore window (amends DEC-011, DEC-038)
- Author may edit: DRAFT, REJECTED, PUBLISHED, self-HIDDEN, and posts under any lock level. Not editable: PENDING, moderation-HIDDEN (must appeal), DELETED (restore first).
- Author may delete a post in any state except DELETED; every deletion goes through the DELETED window.
- Restore returns the post to the state it had before deletion (PUBLISHED → PUBLISHED as in DEC-038); a PENDING post is restored as DRAFT. A post removed by Mod (moderation-HIDDEN) cannot be restored.
- The restore window is 7 × 24 hours from the moment of deletion (e.g. deleted 01/10 21:00 → restorable until before 08/10 21:00).
- Source: QA-324, QA-330

**[Amended 2026-10-14 — DEC-184: hết hạn khôi phục chuyển "đã xóa hẳn" (cờ); Mod/Admin, tác giả xem lại theo DEC-179]**

### DEC-163: M03 — Posting restrictions under MEDIUM/HEAVY warning (clarifies DEC-079)
- "Cannot create new posts" covers every action that makes a never-public post public or starts one: saving a new draft, submitting an existing draft, resubmitting a REJECTED post.
- Still allowed: editing an already published post, restoring a deleted post, voting in polls.
- Source: QA-325

### DEC-164: M03 — Required content and length limits (amends DEC-030)
- Submit requires a title and either content or a poll (a poll substitutes for content; attachments do not).
- A draft must not be empty: at least one of title, content, poll, attachment.
- Title max 150 characters; content max 6,000 words, a word being a whitespace-separated token (as DEC-144), counted over the text readers see. Limits apply to drafts and submissions.
- The editor warns immediately when a limit is exceeded, showing the current count against the limit; saving or submitting over the limit is rejected and the text is kept.
- Source: QA-326

### DEC-165: M03 — Poll details (amends DEC-036)
- The allow_change_vote option is removed: while a poll is open, voters can always change or withdraw their vote.
- Options: single/multiple choice (default multiple), show results before voting (default off). Both are locked once the post is submitted.
- A poll can be added or removed only before the post is submitted. After submission the author can only add options (total still ≤ 10) and change the end time; existing options cannot be edited or deleted. Only the author adds options.
- End time is required and must be ≥ now; while the poll is open it can be moved earlier or later (≥ now); "close now" sets it to now. A closed poll cannot be reopened.
- Result % = selections of an option ÷ total selections, rounded to whole numbers (the displayed sum may be 99% or 101%). The author may vote in their own poll.
- Source: QA-327

### DEC-166: M03 — Posts auto-rejected by AI (details DEC-098 for posts)
- The author sees the violation category detected by AI (DEC-097 categories).
- The author can edit and resubmit without limit; each resubmission is scanned again. Disputes go through M09 (DEC-133).
- Source: QA-328

**[Clarified 2026-10-18 — DEC-198: khiếu nại gộp bài và cảnh cáo AI; hạn theo cảnh cáo, không có cảnh cáo thì 3 ngày]**

### DEC-167: M03 — Scope of FULLY_LOCKED (clarifies DEC-033)
- FULLY_LOCKED blocks new comments, upvotes and poll voting (including changing or withdrawing a vote). Bookmark and report remain available.
- Source: QA-329

**[Clarified 2026-10-23 — DEC-246: chặn cả upvote, rút upvote trên bình luận của bài]**

### DEC-168: M03 — Moderator visibility of non-public posts
- MOD and ADMIN do not see other users' DRAFT, self-HIDDEN or REJECTED posts. They see PENDING posts through the review queue, and FLAGGED or moderation-HIDDEN posts through M08/M09.
- Rationale (stakeholder): review applies to content that others will read.
- Source: QA-331

**[Amended 2026-10-14 — DEC-185: Mod/Admin xem bài tự ẩn của người khác trong báo cáo, lịch sử báo cáo, khiếu nại]**

### DEC-169: MS1 scope — no Accepted Answer, no post cover image
- Accepted Answer (draft DM-4.2.1) is not supported in MS1, system-wide (affects M03, M04, M12).
- Posts have no cover image; images are used through attachments.
- Source: QA-332, QA-333

### DEC-184: M03 — Posts are soft-deleted only (amends DEC-011, DEC-038, DEC-162; closes OPEN-010)
- When the 7-day restore window ends, the post is flagged "permanently deleted" ("Đã xóa hẳn") instead of being removed. "Permanently deleted" is only a flag: no data is erased — content, attachments, poll, votes, edit history, Topic/Tag links and comments are all kept.
- Users see no change: the post leaves the Deleted tab, its link shows "not found", and it cannot be restored, edited or deleted again.
- MOD/ADMIN see a permanently deleted post only in its moderation context (open report, report history, appeal); there is no browsing or searching of deleted posts. The author can view it read-only from a report outcome notification or their own appeal, never seeing reporter information (same as DEC-179 for comments).
- Bookmark removal (DEC-174) and point deduction for a self-deleted post (DEC-113) happen when the post is flagged, as they did at permanent deletion.
- Source: QA-350

### DEC-185: M03 — Self-hidden posts in moderation (amends DEC-161, DEC-168)
- MOD/ADMIN can see another user's self-HIDDEN post only in its moderation context (open report, report history, appeal), as for deleted posts (DEC-184). DRAFT and REJECTED posts of others stay invisible to them (DEC-168).
- Edits saved while a post is self-HIDDEN are not scanned at save time. When the author unhides a post that has at least one edit saved while it was self-HIDDEN, the post returns to PUBLISHED and is re-scanned exactly as after editing a PUBLISHED post (DEC-161): it stays visible during the scan; score < 0.5 → unchanged; score ≥ 0.5 → FLAGGED (hidden, awaiting Mod); scan failure → unchanged, stays visible. No scan while the master AI or Moderation switch is off.
- Source: QA-351

### Issues Closed
ISS-261 → ISS-273, ISS-290 → ISS-291

## Functional Requirement — M02: User Profile

### DEC-170: M02 — Profile tabs of the owner (amends DEC-023, DEC-024)
- Owner sees three tabs: Posts | Bookmarks | Deleted (default: Posts). Visitors see Posts only.
- The Deleted tab lists the owner's deleted posts still inside the restore window; listing and restore are M03 (DEC-038, DEC-162).
- Source: QA-334

### DEC-171: M02 — Guest access to profiles (extends QA-011)
- Guest can view any profile page read-only (profile info, follower/following counts, Posts tab).
- Opening the follower or following list requires login; the counts stay visible.
- Source: QA-335

### DEC-172: M02 — Follower/following lists (amends DEC-025)
- "Following" on the profile counts and lists users only; followed Topics and posts are not shown.
- DEACTIVATED and BANNED accounts do not appear in either list and are not counted; they reappear when the account is ACTIVE again. DELETED accounts are removed by DEC-159.
- A BANNED account's own profile page remains visible with its label (DEC-122); this decision covers the lists only.
- Source: QA-336

### DEC-173: M02 — Additional profile fields (clarifies QA-067)
- Besides QA-067, the profile shows Lớp/Khối (only when set) and the joined date.
- Stars received and stars given are not shown on the profile.
- Source: QA-337

### DEC-174: M02 — Bookmarks of posts that become unavailable
- When a saved post becomes unviewable to the saver (deleted by author within the restore window, hidden by moderation, author DEACTIVATED, saver no longer a member of the Private group), the bookmark is kept and the Bookmarks tab shows "Nội dung không tồn tại" at the same position, with no reason; the user can remove it.
- When the post becomes viewable again, the entry shows the post again.
- When the post is permanently deleted or its author becomes DELETED, the bookmark is removed.
- Source: QA-338

### DEC-175: M02 — Posts tab content
- Visitors (including Guest) see the user's published posts that are not hidden and not posted anonymously; posts in a Private group are shown only to members of that group.
- The owner additionally sees own DRAFT, PENDING, REJECTED and self-HIDDEN posts, and own anonymous posts marked as anonymous.
- Source: QA-339

### DEC-176: M02 — Profile details
- No start-of-school-year reminder to update Lớp/Khối in MS1 (resolves QA-034's "có thể").
- All profile lists are newest first: Posts by creation time, Bookmarks by save time, follower/following lists by follow time.
- A user without an avatar shows a default avatar; its form (generic image or the first letter of display_name) is decided at design. DELETED accounts use the generic image.
- Bio: leading/trailing spaces are trimmed before counting; a bio of only spaces is empty; each emoji and each line break counts as one character. Lớp/Khối can be cleared back to empty.
- /u/{username} is case-insensitive. After a rename the old address does not redirect: it shows "người dùng không tồn tại" unless another user has taken that username. An unknown username also shows "người dùng không tồn tại".
- Source: QA-340

### DEC-177: M02 — No moderator removal of avatar or bio in MS1
- MOD and ADMIN cannot remove or reset another user's avatar or bio. Handling a user report stays as in M08 (warning or ban).
- Source: QA-341

### Issues Closed
ISS-274 → ISS-281

---

## Functional Requirement — M04: Comment

### DEC-178: M04 — Editing and deleting own comments under restrictions
- On a post at COMMENT_LOCKED or FULLY_LOCKED, the author cannot edit own comments on that post but can delete them.
- At HEAVY warning level only creating new comments and replies is blocked; editing and deleting existing own comments stay allowed (same principle as DEC-163 for posts).
- A comment whose moderation state is HIDDEN can be neither edited nor deleted by its author.
- Source: QA-342

### DEC-179: M04 — Comments are soft-deleted only; viewing deleted content (amends DEC-043; scope extension)
- Deleting a comment sets a deleted flag. What users see is unchanged from DEC-043 (placeholder or removal) and there is no restore. The content is kept permanently; comments are never hard-deleted.
- Comments stay with their post when the post is deleted; there is no separate removal of comments.
- MOD/ADMIN see deleted content only in the moderation context of that content: an open report, the report history of the target (DEC-076), or an appeal (M09). There is no browsing or searching of deleted content.
- The content owner can view their own handled content (deleted or hidden), read-only, when opening it from a report outcome notification (DEC-074) or from their own appeal; they never see reporters' identity, chosen reasons, descriptions or evidence.
- Posts: see OPEN-010. Groups and chat: see OPEN-011. Account deletion (DEC-156) is unchanged.
- Source: QA-343, QA-344, QA-349

### DEC-180: M04 — Hidden comments: visibility and moderator action (amends DEC-077, DEC-065)
- A HIDDEN comment is shown in the thread to no one, its author included. The author can view it read-only, with a "hidden" label, only when opening it from a notification: the report outcome (DEC-074) or a new in-app event "Bình luận của bạn đã bị ẩn" sent when AI hides the comment (added to DEC-065; in-app only). Label wording is decided at design.
- MOD/ADMIN have a single action on comments: Hide (state HIDDEN). "Delete comment" in draft DM-10.2 means Hide.
- Comment AI scanning stays as DEC-077 (velocity-triggered thread scan).
- Comments have no appeal (DEC-115 unchanged). Whether a comment is shown again when a related warning or ban is overturned on appeal: see OPEN-012.
- Source: QA-345

**[Amended 2026-10-18 — DEC-201: bình luận bị ẩn không hiện lại khi cảnh cáo, ban liên quan bị lật (đóng OPEN-012)]**

### DEC-181: M04 — Thread display with deleted or hidden comments
- A HIDDEN root comment with at least one visible reply shows "[Bình luận đã bị xóa]" in its place, like an author-deleted root; replies stay. A HIDDEN reply is not shown; replies pointing to it show "trả lời [bình luận đã bị xóa]".
- When a root showing the placeholder no longer has any visible reply, the placeholder disappears from the thread (data kept, DEC-179).
- In a thread whose root shows the placeholder, users can reply to visible replies but not to the placeholder.
- Source: QA-346

### DEC-182: M04 — Comment count and Top ordering
- A post's comment count = root comments and replies shown normally; placeholders and HIDDEN comments are not counted; all viewers see the same number. Example: root A (placeholder) with replies B, C; root D with HIDDEN reply E; root F → count 4 (B, C, D, F).
- Top ordering: comments with equal upvotes are ordered by posting time, earlier first.
- Source: QA-347

### DEC-183: M04 — Comment length and reply quote (amends DEC-046)
- Comment and reply content: max 1,000 words, a word counted as in DEC-164. The editor warns immediately, showing the count against the limit; sending or saving an edit over the limit is rejected and the text is kept. Empty or whitespace-only content is rejected.
- The reply quote is display only: shown above the reply, built from the replied comment's current own content (not the quotes it displays) plus its author's name, on one line. It is not part of the reply's content and not counted. If the replied comment is deleted or hidden, "trả lời [bình luận đã bị xóa]" is shown instead.
- Users can still type their own blockquote (DEC-039); it is content and is counted.
- Source: QA-348

### Issues Closed
ISS-282 → ISS-289

---

## Functional Requirement — M08: Moderation

### DEC-186: M08 — AI scan score, thresholds, velocity trigger and auto-warnings (amends QA-020, clarifies DEC-077, DEC-078, DEC-098)
- One pair of thresholds 0.9 / 0.5 (DEC-098) applies to everyone. The warning level of the author does not change the thresholds; the per-level thresholds sketched in QA-020 are dropped.
- The scan score of a post or comment is the highest of the four category scores (DEC-097); that category is the reason recorded on the case the AI creates. Example: harassment 0.92, violence 0.10 → score 0.92, reason "Quấy rối/Bắt nạt".
- The comment-thread scan is triggered when the number of replies in the thread within the sliding window reaches the threshold or more (placeholder "10 replies in 5 min": the 10th reply within 5 minutes triggers). Only replies are counted.
- Each post or comment scoring ≥ 0.9 gives its author one AI warning; one scan that catches several items of the same author gives one warning per item.
- AI never auto-warns a MOD or ADMIN: a MOD's content scoring ≥ 0.9 is hidden or rejected as usual, and the warning decision goes to ADMIN; ADMIN content gets no warning.
- Source: QA-352, QA-355, QA-366

**[Amended 2026-10-18 — DEC-195: nội dung của Admin không bị AI quét]**

**[Clarified 2026-10-19 — DEC-204: hai nhóm cùng điểm cao nhất → lấy theo thứ tự DEC-097]**

### DEC-187: M08 — Account sanctions: ban only, 7th violation, ban count, no stacked bans (clarifies DEC-080, QA-019)
- MOD/ADMIN sanctions on an account are warning and ban only. "Suspend" in drafts DM-10.2, DM-10.3 means a temporary ban; there is no "Disable account" action (consistent with FR-M01).
- A user at HEAVY who violates again (7th violation) gets no 7th warning. The violating content is handled as usual, and the system creates a ban request as a case in the report queue; MOD/ADMIN decide and press "Ban" (escalating duration). A MOD who finds the violation while resolving a case chooses Ban instead of a warning. AI never bans (DEC-078).
- "Number of previous bans" counts every ban that took effect, including bans lifted early by MOD/ADMIN and manual permanent bans; a ban overturned on appeal (DEC-089) is not counted.
- A new ban cannot be issued while the account has a ban in effect; to make it permanent, lift the ban then use "Ban vĩnh viễn".
- Source: QA-353, QA-354, QA-359, QA-367

### DEC-188: M08 — Warning step-down, probation timing, removed or overturned warnings (clarifies QA-020, DEC-079, DEC-089)
- When the probation of the current level ends, the level goes down one step and the warning count becomes the highest count of the lower level: HEAVY → MEDIUM with 4, MEDIUM → LIGHT with 2, LIGHT → clean with 0. The new level starts its own probation at that moment (HEAVY 15 days, then MEDIUM 10, then LIGHT 7).
- "N days" means N × 24 hours from the warning or from the step-down. Example: 6th warning 01/10 09:00 → MEDIUM 16/10 09:00 (4 warnings) → LIGHT 26/10 09:00 (2) → clean 02/11 09:00; a warning on 20/10 makes 5 → HEAVY again.
- A warning removed by MOD/ADMIN ("Override AI warn", QA-019) or overturned on appeal: the warning count goes down by 1 and the level is recomputed from the remaining count; the warning record is kept, marked removed or overturned; the end of the current probation does not change.
- Source: QA-358, QA-366

### DEC-189: M08 — Moderating MOD and ADMIN accounts; cases about oneself
- Only ADMIN can warn or ban a MOD account. A MOD handling a case about another MOD's content can hide the content and conclude the case, but cannot warn or ban that MOD.
- ADMIN accounts cannot be warned or banned by anyone.
- A MOD or ADMIN does not see, and cannot claim, a case about their own posts, comments or account; another MOD or ADMIN handles it.
- Banning a MOD revokes the MOD role (QA-013, unchanged).
- Source: QA-355, QA-365

**[Amended 2026-10-18 — DEC-195: Admin không bị báo cáo; vụ về Mod chỉ Admin xử lý]**

### DEC-190: M08 — Report queue: everything goes through cases; AI-created cases; priority; reports do not hide posts (clarifies DEC-032, DEC-075, DEC-077)
- Hiding content, warning and banning are done only inside a case. A MOD who finds a violation without a report reports it first, then claims the case. (Exceptions: lifting a ban, unlocking a group — DEC-194.)
- Content flagged by AI that needs MOD review — a comment hidden with score 0.5–<0.9, a post FLAGGED after re-scan — and the ban request of DEC-187 each become a case in the report queue, with reporter "System (AI)". If the target already has an open case, they join it. The case's reason is the AI category (DEC-186); the AI entry counts as one report. A ban-request case is marked as such.
- Severity weights: 10 — Bạo lực/Đe dọa; Nội dung người lớn/Không phù hợp; Ngôn từ thù ghét/Phân biệt; Quấy rối/Bắt nạt (incl. "có hệ thống"); Group giả mạo. 5 — Nội dung sai/hiểu nhầm; Đạo văn/Vi phạm bản quyền. 2 — Spam/Quảng cáo; Khác. Each report has exactly one reason. Equal priority → the case opened earlier comes first. These are policy constants (DEC-090).
- Example: 1 "Bạo lực" report → 10 + 2 = 12; 5 "Spam" → 2 + 10 = 12 (the earlier one first); 3 "Spam" → 8.
- "30 min inactivity" counts from the holder's last action on the case: opening it, hiding, warning, banning, concluding.
- A user report never changes the moderation state of a post; only the AI re-scan (M03) sets FLAGGED. "AI/report flagged" in DEC-032 is read as AI only.
- Source: QA-356, QA-357, QA-360, QA-361, QA-365

### DEC-191: M08 — Submitting reports
- A user cannot report their own post, comment or account.
- While the target has an open case, the same reporter cannot report the same target again.
- Users at HEAVY can still report (DEC-178: HEAVY only blocks creating posts and comments).
- A report on a target that is no longer visible to the reporter (deleted or hidden while the report was being written) is refused.
- Reports cannot be withdrawn or edited after sending.
- Source: QA-363, QA-364, QA-368

**[Amended 2026-10-18 — DEC-195: không báo cáo được Admin]**

### DEC-192: M08 — Concluding a case: reason and notifications; target concentration (clarifies DEC-074, DEC-082)
- The resolution reason is required for both outcomes (action taken, dismissed).
- The reported user is notified only when action is taken; nothing is sent when the case is dismissed.
- Reporters receive one of two meanings, the same for every target type: "action has been taken" or "no violation found"; wording is decided at design. A case created by AI has no reporter notification.
- The appeal link is included only when the action can be appealed: warning, ban, hidden post (DEC-115); not for a hidden comment or a hidden or locked group.
- Target concentration of a reporter is computed for the target of the case being viewed: (that reporter's dismissed reports on this target) ÷ (that reporter's resolved reports), over reports resolved in the last 90 × 24 hours. Example: 10 resolved, 6 dismissed on user X → 0.6 when viewing a case about X.
- Source: QA-362, QA-365

**[Amended 2026-10-18 — DEC-197: mọi thông báo về xử lý khiếu nại được đều kèm đường dẫn khiếu nại]**

### DEC-193: M08 — Moderation log additions (amends DEC-081)
- The moderation log also records lifting a ban, removing an AI warning, hiding, locking and unlocking a group. Claiming and auto-release of a case are not logged.
- Log entries cannot be edited or deleted (same as the admin action log, DEC-094).
- Source: QA-367, QA-369

### DEC-194: M08 — Hiding and locking a reported group (scope extension)
- When a group is reported, the reported user is its Owner. In the case, MOD/ADMIN can hide or lock the group, and can also warn or ban the Owner (DEC-189 rules apply).
- Hide: the group and all its content are shown to no one, members and Owner included; data is kept (as for a group deleted by its Owner, DEC-105). There is no unhide. A locked group can be hidden in a later case.
- Lock: the group stays visible as before (Public/Private) and existing content stays readable. Posting, commenting, upvoting, poll voting, joining and inviting are blocked for everyone, Owner and Group Mods included; bookmark and report stay available (as FULLY_LOCKED, DEC-167). MOD/ADMIN can unlock directly on the group, without a case; unlocking is logged.
- The Owner gets the outcome notification (DEC-192) without an appeal link: content-removal appeal covers posts only (DEC-115).
- How a hidden or locked group is displayed and which group actions are blocked is applied by M11; to be cross-checked when FR-M11 is written.
- Source: QA-369

**[Clarified 2026-10-21 — DEC-235: nhóm Bị khóa chặn mọi thao tác quản trị; thành viên vẫn tự rời được]**

### Issues Closed
ISS-292 → ISS-309

---

## Functional Requirement — M09: Appeal

### DEC-195: M09 — ADMIN cannot be reported; cases and appeals about a MOD are handled by ADMIN only; ADMIN content is not reviewed or scanned (amends DEC-189, DEC-191, DEC-186, DEC-013, DEC-077)
- No one can report an ADMIN's post, comment or account. Since ADMIN accounts are never warned or banned (DEC-189), an ADMIN has no appeals.
- A case about a MOD's post, comment or account is seen, claimed and handled by ADMIN only; other MODs do not see it (replaces "A MOD handling a case about another MOD's content can hide the content" in DEC-189).
- An appeal sent by a MOD (warned by ADMIN, post removed, or AI warning) is seen and reviewed by ADMIN only. The role counted is the role at the time of the action: a MOD banned by ADMIN loses the MOD role (DEC-189) but the ban appeal still goes to ADMIN only.
- Other appeals keep the source rule: MODs review them, including appeals about actions taken by ADMIN, except appeals about their own actions (QA-020, DEC-088).
- ADMIN posts are published without pre-scan or review, and ADMIN comments are not AI-scanned. Applied by M03, M04, M08; to be revised in FR-M03, FR-M04, FR-M08.
- A group whose Owner is an ADMIN cannot be reported (a group report targets its Owner, DEC-194).
- An ADMIN post inside a group still goes through that group's own approval gate (M11); only the system AI scan and system review are skipped.
- Consequence accepted: ADMIN content has no system moderation at all (no scan, no review, no report).
- Source: QA-370, QA-371

**[Amended 2026-10-21 — DEC-240: bài của Owner không qua duyệt của nhóm]**

### DEC-196: M09 — Who sees an appeal; "escalate to ADMIN" is the visibility rule (clarifies DEC-088, QA-021)
- An appeal about MOD X's action is shown to every MOD other than X and to ADMIN; an appeal sent by a MOD is shown to ADMIN only (DEC-195); ADMIN sees every appeal.
- There is no separate escalation step, flag or notification: when no MOD other than the action's author exists, only ADMIN sees the appeal, which is what DEC-088's "auto-escalate to ADMIN" means.
- Source: QA-372

### DEC-197: M09 — Appeals while banned; appeal link on every appealable notice (amends DEC-085, DEC-192)
- While an account is BANNED it can appeal only that ban (locked-screen button or ban email link). Warnings and removed posts can be appealed only while the account is ACTIVE and within their appeal window.
- Every notification about an appealable action carries the appeal link, whoever issued it (AI, MOD or ADMIN): warning (including AI auto-warnings), ban, post removed by MOD/ADMIN. Also for a post auto-rejected by AI (DEC-198). Not for a hidden comment or a hidden or locked group. Applied to M08 notifications (FR-M08-09.05, FR-M08-10.03 to be revised).
- Source: QA-373, QA-374

### DEC-198: M09 — Appeal of a post auto-rejected by AI, combined with its AI warning; no content snapshot (clarifies DEC-115, DEC-133, DEC-166)
- A post auto-rejected by AI (score ≥ 0.9) can be appealed. The author may also edit and resubmit without limit (DEC-166).
- When the rejection comes with an AI warning (DEC-186), the post and that warning are appealed together in one appeal, and one notification tells the author both facts — the post was rejected (not published) and a warning was issued — with one appeal link. The appeal window is that warning's window (DEC-199: 7, 10 or 15 × 24 hours by level).
- When the rejection comes without a warning (author at HEAVY, where a ban request is created instead; author is a MOD, where ADMIN decides on a warning), the appeal window is 3 × 24 hours from the rejection.
- The appeal is of type "post" in the appeal list (DEC-200). The reviewer sees the AI decision log of the post (DEC-133).
- Accepted: the post is published at once without a new scan, and the AI warning issued with that rejection is overturned. If the author has already edited and resubmitted the post before the conclusion, accepting overturns only the warning. Rejected: both stay as they are.
- No snapshot of content is kept at the time of an action for MS1. Reviewers rely on the resolution reason (required, DEC-192), report evidence, post edit history and the AI decision log. Remaining gap (a comment or profile warned without being hidden, then edited before the appeal) is recorded as a point to reconsider after MS1.
- Source: QA-375, QA-376

### DEC-199: M09 — Warning appeal window; appeals reviewed after the action ended (clarifies DEC-086, DEC-089)
- Each warning has a fixed appeal window counted from the moment it is issued: 7, 10 or 15 × 24 hours according to the level that warning brings the user to (LIGHT, MEDIUM, HEAVY). Later warnings and step-downs do not change it. Example: warning 1 at 01/10 09:00 (LIGHT) → until before 08/10 09:00; warning 2 at 05/10 09:00 → until before 12/10 09:00.
- A warning issued together with an AI rejection of a post is appealed only through the combined post appeal (DEC-198), within this same window.
- An appeal sent within the window is reviewed and overturned as usual even if the action has ended meanwhile (temporary ban expired or lifted, warning level stepped down): the ban becomes overturned and is not counted in the number of previous bans; the warning becomes overturned and the current warning count goes down by 1, never below 0, and the level is recomputed.
- Source: QA-377, QA-378

### DEC-200: M09 — One appeal queue view (clarifies DEC-088, DEC-115)
- Appeals are shown in one list, separate from the report queue: ban appeals, then warning appeals, then post appeals (removed by MOD/ADMIN or auto-rejected by AI); within a type, earlier submitted first. Moderators can filter by type, which is how the "separate queue" of DEC-115 is kept.
- Source: QA-379

### DEC-201: M09 — Overturned ban of a MOD, hidden comments, conclusion reason, no withdrawal (amends DEC-089, DEC-180; closes OPEN-012)
- When the ban of a former MOD is overturned, the account returns to ACTIVE with role USER; the MOD role is not restored. ADMIN may send a new "Đề xuất làm Mod" (DEC-091).
- When a warning or ban issued together with hiding a comment is overturned, the comment stays HIDDEN (comments have no appeal, DEC-115, QA-345).
- The reviewer must give a conclusion reason for both Accepted and Rejected; the appellant sees the conclusion with its reason.
- An appellant cannot withdraw or edit an appeal once sent.
- Source: QA-380, QA-381, QA-382

### DEC-202: M09 — Removed-post appeal vs separate appeals of the warning or ban issued with it (clarifies DEC-115, DEC-087)
- A warning or ban issued together with a post removal is overturned at most once, by whichever appeal is accepted first: its own appeal or the appeal of the removed post.
- If that warning or ban already had its own appeal rejected, accepting the post appeal does not overturn it (the rejection is final, DEC-087).
- Once it is overturned, a new appeal of it is refused; an appeal of it already pending is reviewed as usual, and accepting it changes nothing more.
- Source: QA-383

### Issues Closed
ISS-310 → ISS-323

---

## Functional Requirement — M13: AI Layer

### DEC-203: M13 — AI quality evaluation covers Topic Suggestion only; one metric shown to ADMIN in M15 (clarifies DM-11.5, QA-017, DEC-133)
- The Feedback / Evaluation Loop (5th mandatory AI capability, DEC-006 unchanged) evaluates Topic Suggestion only. It sends nothing back to the AI provider and retrains nothing (DM-11.5 unchanged).
- AI Moderation is not evaluated automatically: no MOD / "Trusted User" correct–incorrect marking (the DM-11.5 draft flow is dropped), no moderation metrics. Threshold tuning (DEC-098) is done by the development team reading the AI decision log, and changed by deployment (DEC-090).
- Data: the Topic-suggestion feedback records of M05 (suggested Topics vs. Topics the author finally chose; recorded only when the suggestion is not stale), including those of deleted accounts (DEC-159).
- Metric (single): share of suggested Topics kept = suggested Topics the author kept ÷ all suggested Topics, over the feedback records in the selected period. Example: {Toán, Vật lý, Hóa}→{Toán, Hóa}; {Ngữ văn}→{Ngữ văn, Lịch sử}; {Tin học, Toán}→{Tin học, Toán} → 5 kept of 6 suggested ≈ 83%. Precision/Recall/F1/Accuracy listed in DM-11.5 are not computed.
- Shown to ADMIN in the M15 Content Stats dashboard with the existing M15 presets (Today / 7 days / 30 days / All-time); a record belongs to a period by the time it was recorded, Asia/Ho_Chi_Minh (DEC-127). Adds one item to M15 (QA-243).
- Source: QA-384, QA-385, QA-392

### DEC-204: M13 — Moderation scan input; tie between violation categories (clarifies DEC-097, DEC-186)
- A post is sent to AI Moderation with its title, text content, poll (question and options) and image attachments. Document attachments (PDF/DOCX/XLSX/PPTX) are not sent (consistent with DEC-160). A comment is sent with its text.
- When two or more categories share the highest score, the reason is the first of them in the order Harassment (Quấy rối), Hate (Ngôn từ thù ghét), Sexual (Nội dung người lớn), Violence (Bạo lực) — the order of DEC-097. All four have the same severity (BR-M08-06), so case priority is unaffected. Example: Harassment 0.92, Violence 0.92 → reason Harassment.
- Source: QA-386, QA-392

### DEC-205: M13 — Post embedding: when it is created, when recomputed, switches and backfill (clarifies DEC-095, DEC-093, DEC-099)
- A post's embedding is created when the post becomes PUBLISHED, whatever the path: clean scan, MOD approval, published directly while AI Moderation is off, ADMIN post (no pre-scan, DEC-195). Rejected and pending posts have none.
- It is recomputed every time the title or text content changes ("edited significantly" in DEC-095 means this, the same as the M05 stale rule). Changing only Tags, Topics, images or documents does not recompute it.
- Post embedding and query embedding both follow the master AI switch and the Search switch (DEC-093).
- A published post left without a current embedding — because the master or Search switch was off, or both attempts failed (DEC-099) — is put in a backfill queue and its embedding is created once the switches are on and the AI responds. This differs on purpose from DEC-013 (no retroactive moderation scan): creating an embedding changes nothing users see.
- Source: QA-387, QA-388

### DEC-206: M13 — Post summary on request, kept temporarily and shared; logged-in users only (amends DM-11.4, QA-011, QA-007, QA-388)
- No summary is created automatically and none is stored permanently. A logged-in user (USER, MOD, ADMIN) who can see a post presses "Tóm tắt" to get one. A Guest sees the button; pressing it shows a message asking to log in to use the feature (amends QA-011 "Guest: Xem AI Summary").
- The button exists only on posts whose title + text content has at least 300 words, counted as in DEC-144 (whitespace-separated tokens; each Vietnamese syllable is one word). Example: 250 words → no button; 300 → button.
- Sent to the AI: title and text content only; no attachments, no poll. Below the summary the note "Tóm tắt chưa bao gồm nội dung tệp đính kèm" is shown.
- The first request calls the AI; the result is kept and shared system-wide for 24 hours from its creation (24 × 60 minutes). Within that time every request for the post gets that result without calling the AI. The kept result is dropped when the title or text content changes, or when the post falls below 300 words. There is no separate rate limit (no change to DEC-100).
- Timeout 10 s per attempt, one retry after 2 s (as DEC-099 for LLM generation); this is a constant changed by deployment. After both attempts fail, a non-blocking message ("Hệ thống đang bận, vui lòng thử lại sau", wording at design) is shown and the post stays readable; a failure is not kept. While the master AI switch is off, the button stays visible and pressing it shows the same message at once, without calling the AI. Summary has no own switch (DEC-093 unchanged).
- Summary calls are not written to the AI decision log (DEC-207). Since nothing is stored, the backfill of QA-388 does not apply to summaries.
- Source: QA-389, QA-390

### DEC-207: M13 — AI decision log: what is logged, unit, immutability, who views it (clarifies DEC-133, DEC-099, DEC-156)
- Logged: AI Moderation scoring, post embedding, Topic Suggestion (as DEC-133). Not logged: summary (DEC-206) and query embedding (not linked to any post or comment).
- One record per AI call (not per attempt), including failed calls, with whether the call succeeded. A failed comment scan recorded here is the "log error for admin" of DEC-099.
- A comment-thread scan writes one record per comment, so every record is linked to a post or comment.
- Records are never edited or deleted (kept indefinitely, DEC-129; kept for deleted accounts, DEC-156).
- Only MOD/ADMIN reviewing an appeal of a post auto-rejected by AI see the log (DEC-198). No other lookup screen in MS1; the development team reads the data when tuning thresholds.
- Source: QA-391, QA-392

### Issues Closed
ISS-324 → ISS-332

---

## Functional Requirement — M06: Search

### DEC-208: M06 — Guest searches posts by full-text only; "Tìm kiếm thông minh" prompts login (resolves DEC-062 vs QA-011)
- A Guest can search (DEC-062) but posts are always searched by full-text (QA-011 "Semantic Search: Không" holds; FR-M13-04.04 unchanged). Typeahead suggestions, user/Tag/Topic/Group search, filters and history work for Guest as for USER.
- Semantic search is shown to users as "Tìm kiếm thông minh". Only a Guest sees this option; pressing it shows a message asking to log in, and the results stay full-text. The same happens while the master or Search switch is off (as the summary button, DEC-206).
- A logged-in user (USER, MOD, ADMIN) always gets semantic search while both switches are on; there is no switch to turn it off.
- A Guest also sees the Following-only filter; pressing it shows the same login message.
- Source: QA-393, QA-402

### DEC-209: M06 — Matching users, Tags, Topics, Groups; which accounts appear; typeahead (amends DEC-053, clarifies DEC-057, DEC-058, QA-110)
- Users, Tags, Topics and Groups match the typed text anywhere in the name (not only at the start), case-insensitive, ignoring Vietnamese diacritics, with approximate (typo-tolerant) matching. Only names are matched: users by display_name and username, Groups by name only (not description). Examples: "Nam" → "Nguyễn Văn Nam"; "toan" → Topic "Toán học"; "tóan" → "Toán học"; "hàm" → #đạo_hàm; "HSG" does not match a Group whose name lacks it.
- Within each type, the closer match to the typed text comes first (as @mention, DEC-153).
- User search (typeahead and results) shows ACTIVE accounts that have completed Step 3 only; BANNED, DEACTIVATED, DELETED and unfinished-Step-3 accounts are not shown (as @mention, DEC-153).
- Typeahead starts from the first character typed and shows at most 3 items per type (users, Tags, Topics, Groups).
- Source: QA-394, QA-401, QA-402

### DEC-210: M06 — Private groups hidden from search for non-members (resolves DEC-053, DEC-062, QA-044, QA-120 vs DEC-110)
- A Private group does not appear in Group search results or typeahead for anyone who is not its member, Guest included (DEC-110 holds; "visible-but-gated in search" of DEC-053, DEC-062, QA-044, QA-120 no longer applies).
- A member of the Private group still finds it in search.
- Posts of a Private group remain visible in search only to its members (DEC-062, DEC-108 unchanged).
- Source: QA-395

### DEC-211: M06 — Post ranking details, full-text matching, sort modes (clarifies DEC-055, DEC-057, DEC-064, DEC-079)
- Full-text: a post matches when it contains at least one word of the query (title or text content, diacritics ignored). Relevance in full-text mode = query words found in the post ÷ query words. Example: "phương trình bậc hai" (4 words): post with all 4 → 1.0; post with "phương trình" only → 0.5.
- Candidate set = the 120 posts with the highest relevance (the DEC-064 maximum). In semantic mode, relevance = cosine similarity mapped to 0–1 on a fixed scale (−1 → 0, 0 → 0.5, 1 → 1), independent of other posts.
- Engagement = (raw − min raw) ÷ (max raw − min raw) within the candidate set; when all candidates have the same raw value, engagement = 0 for all.
- Final score = relevance × 0.8 + engagement × 0.2 in both modes. Ties: higher relevance first, then the more recently published post.
- A post whose author is at HEAVY: final score × 0.5, in both modes, only when sorting by Relevance.
- Sort Newest and Most upvoted reorder the same candidate set; ties → more recently published first; no HEAVY downranking in these two sorts.
- The message "Thu hẹp tìm kiếm để có kết quả chính xác hơn" is shown when 120 results have been loaded and the user scrolls further.
- Example: raw A 3, B 1, C 5; relevance A 0.9, B 0.9, C 0.7 → engagement A 0.5, B 0, C 1 → final A 0.82, C 0.76, B 0.72. If A's author is at HEAVY: A 0.41, last.
- Source: QA-396, QA-397, QA-398

### DEC-212: M06 — Filters and browsing without a query (clarifies DEC-056, DEC-064, DEC-142)
- One value per filter type (one Topic, one Tag, one time range); several filters together → a post must satisfy all. Filters apply to post results only, not to user/Tag/Topic/Group results.
- Following-only = posts by followed users, posts in followed Topics, and followed posts (the three follow targets, as the M14 Following tab, DEC-125).
- Today / This week / This month are calendar periods in Asia/Ho_Chi_Minh (DEC-127) by the post's publish time: from 00:00 today; from 00:00 Monday this week; from 00:00 on the 1st of this month. Example: Wednesday 15/10 10:00 → This week = posts published from Monday 13/10 00:00.
- Without a query (opening a Topic/Tag from M05, or sending an empty query with at least one filter): list every visible post matching the filters; default sort Newest, Most upvoted available, no Relevance; no 120-result limit; no AI call. An empty query with no filter does nothing.
- Source: QA-399, QA-400, QA-402

**[Amended 2026-10-20 — DEC-215: "đang theo dõi" gồm người dùng, Topic; không còn bài đang theo dõi]**

### DEC-213: M06 — Snippet, search history, rate-limit counting (clarifies DEC-059, DEC-061, DEC-063)
- Snippet: the first 150 characters of the text content; if character 150 falls inside a word, cut before that word and add "…"; text content of 150 characters or fewer is shown whole without "…"; a post without text content (poll only) has no snippet.
- History: an entry is added only when a query with text is sent (not when picking a typeahead item, not when opening a Topic/Tag page); sending a query already in history moves it to the top (no duplicate); shown newest first; picking an entry sends that query at once; no per-entry delete, only "clear history".
- On logout, the whole search history in that browser is cleared (scope extension; Guest history on shared devices is not covered).
- Rate limit "per minute" = the last 60 seconds (as DEC-144). Loading more results while scrolling is not counted. Changing a filter or the sort, opening a Topic/Tag page, and picking a history entry each count as one submit.
- Source: QA-402, QA-403

### DEC-214: M01 — @mention suggestions match names as DEC-209 (amends DEC-020)
- The @mention suggestion list matches the typed text against display_name and username the same way as M06 user search (DEC-209): anywhere in the name, case-insensitive, ignoring Vietnamese diacritics, approximate (typo-tolerant). Examples: "@Nam" → "Nguyễn Văn Nam"; "@nguyen" and "@Nguyên" → "Nguyễn".
- Ordering by context tiers (DEC-020, DEC-153) is unchanged; within a tier the closer match comes first (DEC-153). Accounts shown are unchanged (DEC-153).
- Source: QA-404

### Issues Closed
ISS-333 → ISS-344

---

## Functional Requirement — M07: Notification

### DEC-215: M07 — Follow targets, new-post notification, unfollow (resolves QA-043 vs DEC-065, QA-127; amends DM-4.5, QA-043, DEC-125, DEC-159, DEC-212; scope extension)
- Follow targets are users and Topics only. Following a post is removed; Tag and Group stay non-followable. A followed post is no longer part of the M14 Following tab (DEC-125) or the M06 Following-only filter (DEC-212); DEC-159 has no post follows to erase.
- Following a user adds the in-app event "a user you follow published a new post" (no email). It is sent when the post first becomes publicly visible (after the pre-publish scan), not for anonymous posts, not to followers who cannot view the post (Private group, DM-5.3), not for rejected posts, and not again on edit or restore.
- Following a Topic sends no notification; it is used only by the M14 Following tab and the M06 Following-only filter.
- Unfollow (scope extension): a user can unfollow a user or a Topic; the follow relation is removed, the follower count decreases by 1, nobody is notified. The "new follower" notification is sent at most once per (follower, followed user) pair, so re-following does not notify again.
- Source: QA-405, QA-406

### DEC-216: M07 — Upvote notification batching details (clarifies DEC-066)
- The first upvote is notified immediately and opens a 5-minute window (5 × 60 s) for that post or comment. Upvotes on the same post or comment inside the window update that same notification: text "A và N người khác đã upvote…", back to unread, moved to the top. The first upvote after the window opens a new notification and window.
- Batching is per post and per comment. A = the most recent upvoter; N = the number of other distinct users who upvoted inside the window.
- Withdrawing an upvote does not change a notification already sent; the same user upvoting again inside the window is not counted twice.
- Example: 10:00 B upvotes X → "B đã upvote…"; 10:02 C → "C và 1 người khác…"; 10:04 D upvotes comment Y → separate notification; 10:05:00 E upvotes X → new notification.
- Source: QA-407

### DEC-217: M07 — Bell and Notifications page (clarifies DEC-067)
- The bell shows the 10 most recent notifications, newest first by last update (a batched upvote notification moves up when updated), and its own unread count (chat messages not included).
- Opening the bell does not mark anything as read; only clicking a notification or "Đánh dấu tất cả đã đọc" does.
- The Notifications page lists all notifications newest first, loading 20 per scroll, down to the oldest.
- Source: QA-408

### DEC-218: M07 — Recipients and actor display (clarifies DEC-065)
- No notification is created for the user who caused the event (comment on own post, reply to own comment, self-mention).
- Notifications are still created for recipients who are BANNED or DEACTIVATED and are seen when the account is ACTIVE again; email events follow DEC-065 unchanged. No notification is created for a DELETED recipient.
- The actor's name is shown as "Tài khoản tạm thời vô hiệu hoá" when the actor is DEACTIVATED and "[Người dùng đã xóa]" when DELETED (as DEC-149, DEC-156).
- Source: QA-409

### DEC-219: M07 — New-message popup and chat mute settings (clarifies DEC-070, DEC-067)
- Each new chat message (DM or Group chat) shows a small popup to a member who has the app open, except while that member is viewing that same conversation.
- "Tắt thông báo cho toàn bộ Chat" mutes every conversation with no per-conversation exception. Per-conversation mute applies while the global mute is off; turning the global mute off keeps conversations muted individually.
- Muting only hides the popup. The Message icon count still counts muted conversations, so it always matches the unread state (counting rule: DEC-220).
- Source: QA-410

### DEC-220: M07 — Confirmation list (clarifies DEC-067, DEC-068, DEC-070, DEC-091)
- A user cannot follow themselves and cannot start following a BANNED account; existing follows of BANNED or DEACTIVATED accounts are kept (as DEC-172).
- The "Đề xuất làm Mod" notification can be answered once; afterwards it shows the choice made. A proposal does not expire; a new proposal from ADMIN is a new notification.
- An email that fails to send stays in the queue and is retried at the next scan, at most 3 retries, then stops.
- Clicking a notification whose content was deleted, hidden or is no longer viewable marks it read and shows "Nội dung không tồn tại" (as DEC-174); the notification itself is kept (DEC-071). Owner read-only views (DEC-179, DEC-180, DEC-184) are unchanged.
- The Message icon count is the number of conversations with unread messages, by the M16 read marker (QA-209).
- The "Tắt thông báo cho bài này" toggle is shown on every post to logged-in users and mutes upvotes on the post and on the user's own comments in it, besides comments and replies.
- Source: QA-411

**[Amended 2026-10-21 — DEC-222: đề xuất có hạn 7 ngày, mỗi người một đề xuất cùng loại]**

### Issues Closed
ISS-345 → ISS-351

---
## Functional Requirement — M10: Admin Panel

### DEC-221: M10 — ADMIN root; granting and revoking ADMIN (amends DEC-007, DEC-065)
- The seeded root ADMIN account is marked "root" (ADMIN gốc). Its role is ADMIN; root is not a separate role. No one can revoke its ADMIN role, and it has no resign option.
- Only the root ADMIN can grant or revoke the ADMIN role; other ADMINs cannot.
- Grant follows the Mod flow: the root sends an "Đề xuất làm Admin" to a USER or MOD account; Accept sets the role to ADMIN immediately; Decline changes nothing.
- Revoke is direct, immediate, needs no consent and has no appeal; the account returns to USER.
- The root account always stays ADMIN, so the system always has at least one ADMIN.
- M07 adds the in-app notification event "Đề xuất làm Admin" with Accept/Decline, the same as "Đề xuất làm Mod".
- Source: QA-412

### DEC-222: M10 — Proposal validity (amends DEC-220, DEC-091)
- A "Đề xuất làm Mod" or "Đề xuất làm Admin" is valid for 7 days, counted as 7 × 24 hours from sending (policy constant, DEC-090). An expired proposal shows "Đã hết hạn" and can no longer be answered; the role does not change.
- A person has at most one valid proposal of each kind; sending a new one ends the previous one.
- Accept takes effect only if, at that moment, the account still has an eligible role: USER for Mod; USER or MOD for Admin.
- Example: sent 09:00 on 01/11 → can be accepted until 08:59:59 on 08/11; at 09:00 on 08/11 it is expired.
- Source: QA-413

### DEC-223: M10 — Self-resignation (confirms QA-013)
- A MOD may resign and return to USER; a non-root ADMIN may resign and return to USER. The system asks for confirmation once before changing the role. Regaining the role requires a new proposal.
- Source: QA-414

### DEC-224: M10 — MOD account management (clarifies DEC-090; amends DEC-081)
- There is no separate "Mod performance" screen and no new metric. "Performance" means the ADMIN reviews a Mod's actions in the moderation log (M08) filtered by actor; "revoke" means demotion.
- M08 adds the ability for ADMIN to filter the moderation log by actor.
- Source: QA-415

### DEC-225: M10 — Feature flags (clarifies DEC-092)
- Exactly three flags: Group (M11), Chat (M16), Gamification (M12). No other module has a flag: Must modules are core or already have a switch (maintenance, registration pause, AI); Feed (M14) is the home page; Analytics (M15) is ADMIN-only. Registration pause is a separate config item, not a feature flag.
- While a flag is off: every user request to that module is refused with "Hệ thống đang bận, vui lòng thử lại sau"; entry points stay visible; system-run work continues (e.g. points and leaderboard, group ownership succession); data is not deleted or changed; nothing is back-filled when the flag is turned on again; ADMIN can still open the module; M08 moderation continues.
- The detailed lists of what is blocked and what keeps running belong to the FR of M11, M12, M16.
- Source: QA-416, QA-417

**[Clarified 2026-10-21 — DEC-236: nhóm, bài nhóm vẫn hiện ở lối vào, mở ra thì báo hệ thống đang bận]**

**[Clarified 2026-10-23 — DEC-245: danh sách khi cờ Gamification tắt]**

### DEC-226: M10 — Site-wide banner (clarifies DEC-092)
- One banner at a time, plain text, 1–200 characters after trimming leading and trailing spaces. ADMIN sets, edits and removes it. It is shown on every page to everyone, including Guests.
- A viewer can close it; a closed banner reappears when the ADMIN edits it or sets a new one.
- Source: QA-418, QA-420

### DEC-227: M10 — Admin action log scope (clarifies DEC-094)
- Recorded: every data-changing action done in an ADMIN capacity — role (proposals sent, demotion, ADMIN revocation); config (every switch change; banner set, edit, remove); moderation, in parallel with the M08 log (warn, remove AI warning, ban, lift ban, hide content, hide/lock/unlock group, conclude case, conclude appeal); catalog (Topic add/merge/delete; Tag disable/reactivate; Topic/Tag change on others' posts).
- Also recorded: every role change not done by an ADMIN — proposal accepted (actor: that person), resignation (actor: that person), MOD role lost on ban (actor: "Hệ thống").
- Not recorded: viewing; claiming or releasing cases and appeals; actions an ADMIN does as an ordinary user (posting, commenting, starring).
- Source: QA-419

### DEC-228: M10 — Confirmation list (clarifies DEC-092, DEC-094, DEC-091)
- User list: ADMIN searches users by username or display name (matched as M06 user search) and filters by role; each row shows username, display name, role and account state; the root is labelled; a Mod row links to the moderation log filtered by that Mod.
- Proposals go only to ACTIVE accounts that completed Step 3; accepting while the account is not ACTIVE is refused.
- Log reason is optional; when the source module requires a reason, the log entry uses it. The log is shown newest first and can be filtered by actor and by action type.
- Initial config: master AI and the three per-module AI switches ON; maintenance and registration pause OFF; the three feature flags ON; no banner.
- Source: QA-420

### Issues Closed
ISS-352 → ISS-359

## Functional Requirement — M11: Group

### DEC-229: M11 — Invites lead into the normal join flow (resolves QA-044, F-GRP-07 vs DEC-110)
- An invite or invite link only brings the invitee to the group; the invitee then follows the DEC-103 join matrix: Public without a join question → member at once; Public with a question, or any Private group → join request waiting for Owner/Group Mod approval (with the answer when there is a question).
- "Invite link (direct join)" of F-GRP-07 and "direct approve" of QA-044 no longer apply.
- Source: QA-421

### DEC-230: M11 — Group posts without a scan score (clarifies DEC-104, DEC-195)
- AI master switch or Moderation switch off, or author is ADMIN (not scanned, DEC-195): the post follows the group's pre-moderation toggle (ON → waits for group approval, OFF → published).
- Scan failed (after the one retry): the post must wait for group approval, whatever the toggle.
- Source: QA-422

**[Amended 2026-10-21 — DEC-240: bài của Owner không qua duyệt của nhóm]**

### DEC-231: M11 — Group-level removal of posts and comments (clarifies DEC-102; scope of DEC-113)
- "Ẩn/xóa" by Owner/Group Mod is one action, "gỡ khỏi nhóm": soft delete. The content is no longer shown in the group to anyone except its author, the group's Owner and Group Mods, and system Mod/Admin. The author cannot restore it.
- The author gets an in-app notification. No points are deducted (DEC-113 deduction applies only to system Mod/Admin removal for a violation).
- Strict hierarchy applies to content: a Group Mod cannot remove content of the Owner or of another Group Mod.
- No appeal (DEC-109 unchanged).
- Source: QA-423

### DEC-232: M11 — Triggers of forced ownership succession (clarifies DEC-107)
- Any ban (temporary or permanent), deactivation (including self-deactivation that can still be reactivated) or deletion of the Owner account triggers the DEC-107 succession immediately.
- When the former Owner's account becomes active again, they stay in the group as Member; the role is not given back automatically.
- Source: QA-424

### DEC-233: M11 — System Mod/Admin and groups they are not members of (clarifies QA-016, DEC-104)
- A Mod/Admin who is not a member sees a Private group's content only inside a report case they hold (M08); they cannot find, list or open the Private group otherwise (DEC-210 holds).
- Only the group's Owner and Group Mods approve posts in the group's approval queue. The "System Mod pending-publish queue" in DEC-104 is the queue of posts not in any group (M03).
- System intervention "at any time" is exercised through reports and cases (M08).
- Source: QA-425

**[Amended 2026-10-21 — DEC-240: bài của Owner không qua duyệt của nhóm]**

### DEC-234: M11 — Non-members and group posts (clarifies DEC-108, DEC-111)
- Public group: logged-in non-members comment, vote, report and bookmark the group's posts like ordinary posts.
- When a group becomes Private: a non-member can still read a post only as already loaded on their screen at the moment of the change, without interacting. Reloading, or opening it again by link, bookmark or notification, shows "Nội dung không tồn tại".
- Source: QA-426

### DEC-235: M11 — Locked group freezes management actions (clarifies DEC-194)
- While a group is Bị khóa, in addition to DEC-194's list, these are refused for everyone including Owner and Group Mods: approving join requests and queued posts, removing content, kicking, blocking, appointing/demoting Group Mods, changing settings, deleting the group, Owner leaving.
- Still allowed: Member/Group Mod leaving the group; bookmark and report; system-run ownership succession.
- Source: QA-427, QA-428

### DEC-236: M11 — Group content elsewhere while the Group flag is off (clarifies DEC-225)
- Groups and group posts keep showing at entry points (group list, Trending, profile tab, search, bookmarks, old notifications); opening them gives "Hệ thống đang bận, vui lòng thử lại sau". Every interaction with group posts is refused. ADMIN is not affected.
- Source: QA-429

### DEC-237: M11 — Confirmation list L1–L13
- L1 (DEC-101): 5 groups per 24 hours (last 24 hours, like DEC-144); deleted groups count; ADMIN is limited too. Example: groups at 20:00–20:20 on 01/11 → the 6th is refused at 19:59 on 02/11, allowed at 20:00 on 02/11.
- L2: name required (≤ 100 characters), description optional (≤ 500 characters); names may repeat; mode (Public/Private) chosen at creation; pre-moderation and anonymous toggles default OFF; join question empty by default; all three can be set at creation.
- L3: only the Owner edits name and description.
- L4: when the Owner changes settings so the group becomes "join at once" (Private → Public without question, or the question removed from a Public group), pending join requests are approved immediately.
- L5: turning the pre-moderation toggle off does not release posts already waiting; the new value applies to posts sent afterwards.
- L6: the group list is its own page (target of M14 "Khám phá Group"): the viewer's Private groups and all Public groups; each shows name, description, mode; newest first. Search by name stays in M06.
- L7: when the group has a join question, an answer is required.
- L8: a person with a pending request cannot send another to the same group.
- L9 (DEC-065): new join request → in-app notification to Owner and Group Mods; joining a Public group at once → no notification; rejection and demotion → no notification; becoming Owner (designated or automatic) → notification.
- L10 (DEC-107): Group Mod tenure counts from the latest appointment.
- L11 (DEC-109): group rejection of a queued post requires a reason; the author can edit and resubmit (back through the group gate); a group post auto-rejected by AI is appealable via M09 like any post (not a group-level decision).
- L12: Owner/Group Mod cannot approve their own queued post; if no other approver exists, the post waits.
- L13: after leaving, a former member can still edit and delete their own posts and comments in a Public group; not in a Private group they can no longer see.
- Source: QA-430

**[Amended 2026-10-21 — DEC-240: bài của Owner không qua duyệt của nhóm]**

### DEC-238: M11 — Member list, withdrawing requests, unblocking (scope extension; invite link unchanged)
- Whoever can view the group page can view its member list with roles (Public: everyone including Guest; Private: members).
- The sender can withdraw a pending join request. Owner and Group Mods can view the block list and unblock.
- A block applies to every way into the group (direct join, join request, invite). Blocking someone with a pending request turns it into Đã từ chối.
- Invite link: one shared link per group, no expiry, no revocation; inviting a specific user sends a notification with that link.
- Source: QA-431

### DEC-239: M11 — Soft deletion of group content (closes the M11 part of OPEN-011)
- Every way group content disappears in M11 is soft delete: Owner deletes the group (DEC-105), Mod/Admin hide the group (DEC-194), group-level removal (DEC-231); posts and comments follow M03, M04. The M16 part of OPEN-011 stays open.
- Source: QA-432

### DEC-240: M11 — The Owner's posts skip group approval (amends DEC-237 L12, DEC-104, DEC-195, DEC-230, DEC-233)
- A post by a group's Owner in that group does not go through the group's approval: the pre-moderation toggle and the 0.5–<0.9 group review do not apply.
- The AI scan still applies: score ≥ 0.9 → auto-rejected; 0.5 ≤ score < 0.9, or scan failed → system Mod pending-publish queue, as for a post not in any group (M03); score < 0.5, or AI master/Moderation switch off → published.
- An Owner who is ADMIN: not scanned (DEC-195), published at once.
- Group Mods still cannot approve their own posts (DEC-237 L12 unchanged for them); a Group Mod's post is approved by the Owner or another Group Mod.
- Source: QA-433

### Issues Closed
ISS-360 → ISS-371

## Functional Requirement — M12: Gamification

### DEC-241: M12 — Point deduction for comments (clarifies DEC-113)
- A comment deleted by its author: points from its upvotes are deducted at once (comments have no restore window, DEC-179). The 7-day wait of DEC-113 applies to posts only.
- A comment hidden by AI with score ≥ 0.9: deducted at once when hidden. A comment hidden by AI with 0.5–< 0.9: deducted only when a Mod/Admin concludes it violates and keeps it hidden, at that moment; if the Mod concludes no violation, nothing is deducted.
- Source: QA-434, QA-435

### DEC-242: M12 — Weekly and monthly boards show the last closed cycle (amends DEC-121, QA-202)
- The Week and Month tabs show the final ranking of the last closed week / month, computed once when the cycle closes and unchanged until the next close. The in-progress week or month is not shown.
- Week: 00:00 Monday to before 00:00 the next Monday; month: 00:00 on the 1st; Asia/Ho_Chi_Minh (DEC-127). Closing and the weekly title stay as DEC-121 (at most 60 minutes after the boundary).
- The All-time tab is unchanged: recomputed every 60 minutes.
- A user who becomes excluded after the close (HEAVY, BANNED, DEACTIVATED) is hidden from the shown board while excluded; the others keep their closed ranks; titles already awarded are unchanged.
- Source: QA-436

### DEC-243: M12 — Cycle score, eligibility, Lớp/Khối filter and row content (clarifies QA-038, DEC-117, DEC-123, DM-9.4)
- The cycle score counts upvotes by the time they were given: upvotes given inside the cycle, still in effect at the close, on content not deducted at the close. It is never negative. Later retractions or deductions change total points only, not a closed board.
- Only users with cycle score > 0 are ranked or receive the weekly title (all three tabs). A week with fewer scorers awards fewer than 3 titles, possibly none.
- Lớp/Khối filter: ranks are recomputed within the filtered group with the same tie rule; Lớp/Khối is taken at the close (All-time: at the latest computation).
- Each row: rank, avatar, display name and username (opens the profile), cycle score, "Ngôi sao tuần" mark (Week tab), deleted-account label when applicable. All users with score > 0 are listed, 20 rows per scroll.
- Source: QA-437, QA-438, QA-440, QA-441

### DEC-244: M12 — Where weekly titles are shown (clarifies DEC-114, DEC-121)
- On the profile, next to badges: "Ngôi sao tuần" with the number of wins and the list of weeks won, newest first (displayed by M02).
- On the Week tab, a "Ngôi sao tuần" mark next to each recipient.
- Source: QA-439

**[Amended 2026-10-23 — DEC-247: hồ sơ chỉ hiện danh hiệu của tuần vừa chốt]**

### DEC-245: M12 — Behaviour while the Gamification flag is off (clarifies DEC-225)
- Refused with "Hệ thống đang bận, vui lòng thử lại sau": upvote and retracting an upvote (the button stays visible); opening the leaderboard (its entry stays visible). ADMIN is not affected.
- Keeps running: point deduction and refund by content, badge award, All-time recomputation, week/month close, weekly title award, badge and title notifications.
- Keeps showing: upvote counts on posts and comments (Top sort, Trending, search ranking unchanged), points, badges and titles on profiles, the "Tài khoản đã bị khóa" label.
- Source: QA-442

### DEC-246: M12 — Confirmation list (clarifies DEC-167, DEC-065; amends QA-018)
- FULLY_LOCKED blocks new upvotes and retracting upvotes on the post and on every comment of the post.
- Tied users are listed by username A–Z (display only).
- Weekly title: HEAVY/BANNED is checked at the close; an excluded user gets no title and takes no top-3 place; their points keep accruing and show fully when they return.
- Deleted account: All-time drops it from the next computation; the label is "[Người dùng đã xóa]" (replaces QA-018's "[Tài khoản đã xóa]"). DEACTIVATED accounts are excluded while deactivated and return when reactivated.
- "Point milestone" in DEC-065 means earning a badge; one notification per badge, no separate milestone notification.
- Closing a month only closes the monthly board; no award, no notification.
- Source: QA-443

### DEC-247: M12 — The profile shows the weekly title only for the last closed week (amends DEC-244; clarifies DEC-121)
- The profile shows "Ngôi sao tuần" only if the user won it in the last closed week, from that close until the next weekly close; no win count, no list of weeks won.
- Each win is still recorded (DEC-114). "Remain permanently visible" in DEC-121 means the records are kept (QA-202 "vẫn giữ"), not displayed; past weekly wins are not displayed anywhere.
- Only threshold badges are shown permanently on the profile (DEC-114 unchanged).
- The "Ngôi sao tuần" mark on the Week tab (DEC-244) is unchanged.
- Source: QA-444

### Issues Closed
ISS-372 → ISS-382
