# Day 16 Submission — Phiên bản A (End-of-session draft)

**Student:** Nguyễn Đức Mạnh
**Role:** Product Lead / Backend Engineer
**Submitted at:** Day 16 — 12:50 (before 13:00 deadline)

> Đây là snapshot tư duy tại thời điểm kết thúc buổi học. Bản này được viết ra trong ~60 phút cuối buổi. Phiên bản B sẽ có iterations đáng kể dựa trên critique từ AI và thời gian suy nghĩ thêm.

---

## 1. Idea reframed

**Original idea:**
> HackFlow — platform matching mentor với mentee cho hackathon, bootcamp, PBL event. Dùng AI để tăng chất lượng matching thay vì matching tay.

**Reframed as a product opportunity:**
> Observed gap: organizer hackathon/bootcamp đang matching mentor-mentee bằng Google Sheet thủ công, dẫn đến no-show cao và feedback chất lượng thấp. Founding belief: matching quality không phải chỉ về skill overlap mà còn về personality fit và communication style — những signal này có thể extract từ profile structured + narrative text bằng AI.

---

## 2. Customer / Segment Card

- **Segment name:** Tech event organizer tại Việt Nam (hackathon, bootcamp, PBL)
- **Operational context:** Sinh viên năm cuối/fresher tổ chức event kéo dài 2-8 tuần, 30-200 participants, 10-30 mentors volunteer
- **Recurring workflow:** Matching mentor-mentee thủ công qua Google Sheet/Form
- **Pain moment:** Khi organizer phải đọc 100+ CV và pair với 20+ mentors trong 2-3 ngày trước event
- **Why now:** AI tools (LLM, embedding) đã đủ rẻ và dễ deploy để automate việc này lần đầu tiên
- **Access path:** HUST alumni network, VN tech community Facebook groups

One-sentence description:
> Student organizers của tech event tại HUST và các trường top VN, 2-4 người, đang matching mentor-mentee thủ công và gặp vấn đề với quality & scale.

---

## 3. Need Map

### Need #1 (priority)
- **Statement (JTBD):** When tôi organize hackathon 100 participants với 20 mentors, tôi want matching system tự động pair dựa trên skill + personality fit, so I can save 20+ giờ công và tăng satisfaction rate.
- **Current workaround:** Google Sheet + manual review CV
- **Pain signal:** No-show rate ~30%, satisfaction feedback score thấp
- **Evidence / proxy evidence:** Tôi đã từng organize 2 hackathon tại HUST, biết pain này trực tiếp. Chưa có data formal survey.
- **Why underserved:** Tools hiện tại (MentorCruise, ADPList) không support VN, không có matching logic, chỉ là browse directory.

### Need #2
- **Statement (JTBD):** When tôi là mentee tham gia hackathon, tôi want hiểu được tại sao tôi được match với mentor này, so I can trust hệ thống và engage thật sự.
- **Current workaround:** Accept match không biết lý do, gặp mentor rồi mới thấy không phù hợp
- **Pain signal:** Reported "mentor không relevant với project của em"
- **Evidence / proxy evidence:** Feedback từ participants của hackathon tôi từng organize (anecdotal)
- **Why underserved:** Không platform nào provide match explanation

### Need #3
- **Statement (JTBD):** When tôi là mentor volunteer, tôi want nhận request đã pre-filter, so I can save thời gian screening và focus vào mentoring thực sự.
- **Current workaround:** Nhận tất cả request, tự filter
- **Pain signal:** Mentor feedback "nhận quá nhiều request không phù hợp"
- **Evidence / proxy evidence:** Conversation với 3-4 mentor tại HUST (informal)
- **Why underserved:** Platform hiện tại không có filter logic

---

## 4. Strategy Statement

For tech event organizers tại VN
who struggle with matching mentor-mentee thủ công tốn 20+ giờ và kết quả không consistent,
our product helps them automate matching với explainable AI scoring,
through 3-tier profile (skill + preference + narrative) + composite scorer,
unlike MentorCruise/ADPList (browse-based, không VN support) và Google Sheet (thủ công),
because we can leverage domain-specific data từ VN tech events để fine-tune model qua thời gian.

---

## 5. Moat Hypothesis

**Moat mechanism:** Domain-learning flywheel từ VN tech event data

If we deploy HackFlow tại 10 hackathon/bootcamp tại VN, the following improve:
1. Labeled matching data (accept/reject, satisfaction score) để train LightGBM ranker
2. Vietnamese tech skill taxonomy (skills mapping có local context)
3. Network effect với mentor pool — mentor quay lại vì quality match

Why competitors cannot easily replicate this:
> MentorCruise/ADPList focus global, không invest vào VN. Local competitors không có AI infrastructure. Data flywheel càng chạy càng có moat.

---

## 6. Initial TAM / SAM / SOM view

| Layer | Estimate | Key assumptions | Confidence |
|---|---|---|---|
| TAM | $5-15M/year (SEA tech mentoring market) | Giả định mentoring platform market SEA ~$50M, HackFlow address 10-30% | low |
| SAM | $500K-2M/year (VN tech events) | ~50 hackathon/bootcamp/năm tại VN, mỗi event budget $5-10K cho matching tool | low |
| SOM | $20-50K/year (12mo target) | 5-10 events × $2-5K contract | low |

**Top 3 unknowns requiring further research:**
1. Organizer có willingness to pay thật sự không? Hay expect free?
2. VN tech event market size — bao nhiêu hackathon/năm thật sự?
3. Mentor supply-side — có đủ mentor volunteer không?

**Judgment:**
- [x] Worth pursuing but not now (need to validate organizer WTP first)
- [ ] Worth pursuing now
- [ ] Not worth pursuing as currently framed

---

## 7. Positioning Note

**What we are:**
> HackFlow là AI matching engine cho tech event organizer tại VN, automate việc pair mentor-mentee với explainable scoring.

**What we are not / not yet:**
> Chưa phải là mentoring platform general (như MentorCruise) — chỉ focus vào event context. Chưa có marketplace/monetization trực tiếp với individual mentee.

---

## 8. Self-assessment before Day 17

Trong 6 mắt xích (Idea → Customer → Need → Strategy → Moat → Market Size), mắt xích nào yếu nhất?

> Mắt xích **Customer** và **Market Size** yếu nhất. Tôi đang assume organizer là buyer, nhưng chưa validate — có thể actual buyer là university/company tổ chức event, organizer chỉ là executor. TAM/SAM hoàn toàn dựa trên guess, không có số thật nào.
>
> Mắt xích **Moat** cũng chỉ "sounds good" — data flywheel là cliché, chưa chứng minh cơ chế cụ thể.

Open questions chúng tôi muốn khám phá thêm ở Day 17:
1. Ai thực sự pay cho matching tool — organizer (sinh viên), hay host organization (HUST, FPT...)?
2. Event-based (one-off) vs recurring (platform subscription) — model nào sustainable hơn?
3. Có nên pivot sang individual mentee/mentor B2C thay vì B2B event organizer không?
