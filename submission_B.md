# Day 16 Submission — Phiên bản B (BTVN — After critique & research)

**Student:** Nguyễn Đức Mạnh
**Role:** Product Lead / Backend Engineer
**Submitted:** Day 16 — Phiên bản B (BTVN)

> **Reflection so với phiên bản A:** Bản A có skeleton đúng nhưng mắt xích Customer và Market Size đều yếu — customer segment còn mơ hồ (chưa rõ ai thật sự là buyer), TAM/SAM hoàn toàn là guess không có số nào thật. Bản B đã: (1) tách rõ buyer vs. user, pivot sang "host organization" thay vì sinh viên organizer, (2) bổ sung market data thật từ research, (3) làm rõ cơ chế moat cụ thể hơn, (4) cập nhật strategy statement phản ánh sự thay đổi customer. Đây là những thay đổi có lý do, không phải cosmetic edit.

---

## 1. Idea reframed

**Original idea:**
> HackFlow — platform matching mentor với mentee cho hackathon, bootcamp, PBL event. Dùng AI để tăng chất lượng matching thay vì matching tay.

**Reframed as a product opportunity:**
> Observed gap: Các tổ chức (trường đại học, công ty tech, cộng đồng dev) host hackathon và bootcamp tại Việt Nam đang dùng Google Sheet thủ công để matching mentor-mentee, dẫn đến no-show rate cao (~30%), feedback satisfaction thấp, và tốn 20+ giờ nhân lực của ban tổ chức chuyên nghiệp. Founding belief: Matching quality không chỉ là skill overlap mà còn là personality fit và communication style — những signal này có thể extract từ structured profile + narrative text bằng AI embedding, và một khi system đã học từ dữ liệu VN tech event thì quality cải thiện theo thời gian theo cơ chế flywheel mà global platform không có động lực đầu tư.

> **Thay đổi so với bản A:** Bản A assume buyer là sinh viên organizer. Sau khi suy nghĩ kỹ hơn, tôi nhận ra actual buyer nhiều khả năng là *host organization* (HUST, FPT, Viettel, các công ty tech organize bootcamp) — những người có budget và pain thật. Sinh viên organizer chỉ là *user/operator*, không phải buyer. Đây là pivot quan trọng ảnh hưởng đến toàn bộ strategy.

---

## 2. Customer / Segment Card

- **Segment name:** Tech program manager tại tổ chức host hackathon/bootcamp ở Việt Nam
- **Operational context:** Nhân viên phụ trách chương trình tại university (HUST, NEU, UET), tech company (FPT, Viettel, VNG, Techcombank), hoặc startup community (Topcoder VN, Junction VN) — người có budget và chịu trách nhiệm về program quality, không phải sinh viên tình nguyện
- **Recurring workflow:** Mỗi event (hackathon 2-3 ngày, bootcamp 4-8 tuần), họ phải thu thập profile 50-200 participants + 10-30 mentors, sau đó matching thủ công bằng Google Sheet trong 2-3 ngày trước event
- **Pain moment:** Khi họ nhận feedback sau event: mentor satisfaction thấp ("nhận quá nhiều request không phù hợp"), mentee satisfaction thấp ("mentor không relevant với project"), và no-show rate cao — những số liệu này ảnh hưởng trực tiếp đến KPI program của họ và khả năng mời mentor chất lượng cho event sau
- **Why now:** LLM API (OpenAI, Claude) đã đủ rẻ và accessible để build AI matching engine với chi phí deploy hợp lý; Vietnam tech event ecosystem đang scale (Junction VN 2023: 15,000 thí sinh; NASA Hackathon lần đầu tổ chức tại VN năm 2024) — đủ critical mass để có data flywheel
- **Access path:** Alumni network HUST/UET/FPT, cộng đồng Junction Vietnam, Topcoder Vietnam, các nhóm FB "Tech Event Organizer Vietnam"

**One-sentence description:**
> Program manager tại tổ chức tech (university, company, community) tại Hà Nội/HCM, chịu trách nhiệm về chất lượng hackathon/bootcamp 50-200 người, đang matching mentor-mentee thủ công và bị đánh giá bởi satisfaction score mà họ không có tool để improve.

**Thay đổi so với bản A:** Bản A target "sinh viên năm cuối/fresher tổ chức event" — đây là user thật nhưng không phải buyer. Segment mới focus vào *professional program manager* có budget và accountability. Đây là sự thay đổi quan trọng vì nó resolve luôn câu hỏi "ai trả tiền?" ở bản A.

---

## 3. Need Map

### Need #1 (priority — buyer need)
- **Statement (JTBD):** When tôi là program manager chuẩn bị hackathon 100 participants với 20 mentors, tôi want matching system tự động pair dựa trên skill + project fit + availability, so I can giảm 20+ giờ matching manual và cải thiện satisfaction score — KPI trực tiếp ảnh hưởng đến budget renewal của chương trình.
- **Current workaround:** Google Sheet + đọc CV thủ công, đôi khi kết hợp Google Form structured nhưng vẫn cần human review
- **Pain signal:** No-show rate ~30% (estimate từ kinh nghiệm trực tiếp organize 2 hackathon tại HUST); post-event feedback "mentor không relevant" xuất hiện trong top 3 complaints nhất quán
- **Evidence / proxy evidence:** Kinh nghiệm trực tiếp tổ chức 2 hackathon tại HUST (first-hand). Proxy: Junction VN tổ chức chuỗi sự kiện với 15,000 thí sinh năm 2023 — ở quy mô đó, matching manual là bottleneck rõ ràng. Chưa có formal survey nhưng pain pattern nhất quán với những gì tôi biết từ 3-4 organizer khác (informal).
- **Why underserved:** MentorCruise và ADPList là browse-directory model, không có event-context matching, không support tiếng Việt, không có API để organizer integrate vào workflow của họ. Google Sheet là default vì không có alternative nào tốt hơn đủ nhiều để justify effort chuyển đổi — cho đến khi AI làm gap này đủ lớn.

### Need #2 (mentee need — ảnh hưởng đến platform adoption)
- **Statement (JTBD):** When tôi là mentee vừa được assign mentor, tôi want hiểu được tại sao tôi được match với mentor này và mentor có experience với problem của tôi không, so I can trust hệ thống và chuẩn bị tốt hơn cho buổi mentor đầu tiên.
- **Current workaround:** Accept match không có context, gặp mentor mới biết có phù hợp không — nhiều trường hợp "phá băng" chiếm hết buổi đầu
- **Pain signal:** Feedback "mentor không biết gì về domain của em" (anecdotal từ participant hackathon tôi organize)
- **Why underserved:** Không platform nào trong context VN tech event cung cấp match explanation. Explainability là differentiator vì nó tăng trust và engagement — người ta không reject match khi họ hiểu lý do.

### Need #3 (mentor need — supply-side retention)
- **Statement (JTBD):** When tôi là mentor volunteer tham gia hackathon, tôi want nhận mentee request đã pre-filter theo domain và seniority, so I can dành thời gian cho mentoring thực sự thay vì screening
- **Current workaround:** Nhận tất cả request rồi tự filter hoặc politely decline — tốn thời gian và gây friction
- **Pain signal:** "Nhận request từ team làm AI nhưng tôi chỉ biết mobile" — feedback từ 3-4 mentor tại HUST event (informal)
- **Why underserved:** Không event platform nào có filter logic. Mentor satisfaction là critical vì mentor là supply-side của platform — nếu mentor churn, cả hệ sinh thái sụp.

---

## 4. Strategy Statement

For tech program managers tại tổ chức host hackathon và bootcamp tại Việt Nam (universities, tech companies, dev communities)
who struggle với việc matching mentor-mentee thủ công tốn 20+ giờ và dẫn đến satisfaction score thấp — KPI ảnh hưởng trực tiếp đến program renewal,
our product helps them automate matching với explainable AI scoring và event management dashboard,
through 3-tier profile (technical skill + project context + communication preference) + composite AI scorer trained trên VN tech event data,
unlike MentorCruise/ADPList (global browse-directory, không có event context, không hỗ trợ tiếng Việt, không có organizer API) và Google Sheet (hoàn toàn thủ công),
because chúng tôi có thể build VN-specific matching logic từ event data local mà global platform không có động lực đầu tư, và có thể integrate trực tiếp vào event workflow của organizer thay vì là standalone mentoring marketplace.

**Thay đổi so với bản A:** Bản A strategy nhắm vào "organizer hackathon/bootcamp" chung chung. Bản B target rõ hơn là professional program manager với KPI cụ thể (satisfaction score, program renewal) — điều này làm cho value proposition rõ hơn và dễ pitch hơn.

---

## 5. Moat Hypothesis

**Moat mechanism:** VN Event Data Flywheel + Organizer Lock-in

**Cụ thể hóa cơ chế (bản A chỉ nói "data flywheel" chung chung):**

Nếu HackFlow deploy tại 10 hackathon/bootcamp tại VN trong 12 tháng đầu, những thứ sau improve theo vòng lặp:

1. **Training data chất lượng cao với VN context:** Mỗi event tạo ra labeled data — accept/reject decision, attendance rate, post-event satisfaction score (1-5). Sau 10 events (ước tính ~500-1,000 matched pairs), đủ signal để fine-tune LightGBM ranker với VN tech skill taxonomy
2. **Vietnamese tech skill taxonomy:** Skill mapping có local context — ví dụ "Flutter" ở VN market có nuance khác với global (nhiều outsourcing shop), "AI" ở VN bootcamp thường nghĩa là Python + basic ML chứ không phải LLM research. Global model không capture được nuance này.
3. **Organizer workflow lock-in:** Khi organizer đã integrate HackFlow vào event workflow (Google Form → HackFlow → match notification), switching cost cao. Data lịch sử của event (mentor pool, past matches) là asset của organizer nếu ở lại, mất đi nếu chuyển.
4. **Mentor network effect:** Mentor quality trên platform tăng khi organizer tốt hơn join — mentor muốn tham gia event chất lượng cao, tạo supply flywheel.

**Why competitors cannot easily replicate this:**
> MentorCruise và ADPList target global market, không có incentive để invest vào VN-specific data. Local competitors (nếu có) không có AI infrastructure và labeled data. Data flywheel này cần ~6-12 tháng và 5-10 events để bắt đầu có meaningful signal — đây là time-based moat, không phải technical moat. Barrier thật sự là ai build relationship với VN organizer community trước, vì data chỉ có khi organizer trust platform đủ để dùng trong event thật.

**Thay đổi so với bản A:** Bản A chỉ nói "data flywheel là moat" mà không giải thích cơ chế. Bản B làm rõ 4 cơ chế cụ thể và thành thật hơn: moat thật sự là relationship + data, không phải technology.

---

## 6. Initial TAM / SAM / SOM view

*(Note về methodology: Bản A hoàn toàn dùng guess. Bản B dùng real data làm anchor, sau đó estimate từ bottom-up.)*

### Anchor data từ research:
- **Vietnam EdTech market:** $364.7M revenue năm 2024, CAGR 13.5% (GlobalData / Austrade report 2024–2025)
- **Global Mentoring Software market:** $369M năm 2024, projected $615.5M năm 2030 (Valuates Reports). APAC là fastest-growing region.
- **VN tech events scale:** Junction VN 2023: 15,000 thí sinh trong 1 chuỗi sự kiện; NASA Hackathon lần đầu tổ chức tại VN năm 2024; AngelHack HCM vẫn active 2024. Ước tính conservative: 30-60 hackathon/bootcamp quy mô đáng kể/năm tại VN (HUST, UET, FPT, các tech company).

| Layer | Estimate | Key assumptions | Confidence |
|---|---|---|---|
| TAM | $3–8M/year (VN + SEA event-based mentoring tool market) | APAC mentoring software market là ~22% của global $369M = ~$81M. VN + SEA event-specific subset ước tính 4-10% của APAC. Assumption yếu vì không có SEA-specific breakdown. | low |
| SAM | $300K–$1M/year (VN organizations có budget cho event management tool) | 30–60 events/năm × $5K–$15K average contract value. Contract value estimate dựa trên: organizer pro thường có event budget $10K–$50K, matching tool chiếm 10–30%. Chưa validate WTP thật. | low |
| SOM | $30K–$80K/year (12-month target) | 5–10 paying organizations × $3K–$8K/contract (annual license per event organizer). Realistic nếu bắt đầu từ HUST/UET network và 1-2 tech company partner. | medium — vì dựa trên known relationships |

**Top 3 unknowns requiring further research:**
1. **WTP của host organization thật sự là bao nhiêu?** Cần interview 5-10 program manager tại university + tech company để validate $3K–$8K/contract có reasonable không hay quá cao
2. **Ai trong tổ chức host là decision maker cho budget?** University: Dean/Rector hay student affairs office? Tech company: HR hay Marketing? Buyer journey khác nhau hoàn toàn.
3. **Existing event management tool nào đang được dùng?** Nếu họ đã dùng Eventbrite/Hopin, HackFlow phải integrate hay compete?

**Judgment:**
- [x] Worth pursuing but not now — cần validate WTP và identify exact buyer trong tổ chức trước. Nếu WTP validate dương, move to "worth pursuing now" ngay.
- [ ] Worth pursuing now
- [ ] Not worth pursuing as currently framed

---

## 7. Positioning Note

**What we are:**
> HackFlow là AI-powered mentor matching engine cho professional tech event organizer tại Việt Nam, giúp automate và improve quality matching mentor-mentee với explainable scoring — integrate trực tiếp vào event workflow, không phải mentoring marketplace standalone.

**What we are not / not yet:**
> Chưa phải là general mentoring platform (như MentorCruise/ADPList), chưa target individual mentee/mentor B2C, và chưa phải event management platform đầy đủ (không replace Eventbrite) — HackFlow là matching engine layer nằm giữa event registration và mentor coordination.

---

## 8. Self-assessment before Day 17

**Mắt xích nào đã cải thiện rõ nhất từ A → B?**

> **Customer** cải thiện nhiều nhất: bản A target sinh viên organizer (user), bản B pivot sang professional program manager (buyer) — sự thay đổi này resolve được câu hỏi "ai trả tiền?" và làm cho toàn bộ strategy coherent hơn.
>
> **Market Size** cũng cải thiện: bản A hoàn toàn là guess, bản B anchor vào số thật (Vietnam EdTech $364.7M, Global Mentoring Software $369M) rồi bottom-up estimate từ đó. Confidence vẫn low nhưng số không còn là fabricated.

**Mắt xích nào vẫn còn yếu nhất?**

> **Moat** vẫn chưa đủ mạnh. Tôi đã làm rõ cơ chế hơn nhưng "relationship + data flywheel" là moat mà rất nhiều B2B startup claim — chưa chứng minh được tại sao HackFlow có thể build relationship network nhanh hơn competitor tiềm năng nào đó cũng nhắm vào VN university market.
>
> **Strategy** vẫn cần refine: pivot sang host organization là đúng hướng nhưng chưa clear về go-to-market motion — bán trực tiếp vào university thì sales cycle dài, bán qua tech company thì có thể nhanh hơn nhưng different use case. Chưa chọn entry point cụ thể.

**Open questions cho Day 17:**
1. **Entry point nào nhanh nhất để validate WTP?** University (budget chậm, procurement phức tạp) vs. tech company (budget nhanh hơn, nhưng do HR hay Marketing quyết định?)
2. **Pricing model nào fit nhất?** Per-event (one-time fee mỗi hackathon) vs. annual subscription (organizer dùng nhiều lần/năm) — model nào align incentive tốt hơn với buyer?
3. **Khi nào thì nên thêm B2C layer (individual mentee/mentor)?** Hay giữ B2B thuần để focus?

---

## Appendix: Reflection về AI usage trong bản B

Tôi đã dùng Claude để:
- Research số liệu market (Vietnam EdTech, Global Mentoring Software market size)
- Critique logic của từng mắt xích trong bản A
- Brainstorm buyer vs. user distinction

Tôi không copy-paste output của AI. Tất cả số liệu được verify cross-reference từ ít nhất 2 nguồn (Austrade 2024 report, GlobalData, Valuates Reports). Judgment call về pivot customer segment là của tôi sau khi Claude đặt câu hỏi "ai thực sự chịu trách nhiệm về program quality?" — câu hỏi đó trigger insight, không phải AI đưa ra câu trả lời sẵn.
