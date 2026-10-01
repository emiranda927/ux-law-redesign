# Example: the request this skill came from

A real redesign of a multi-site clinic's weekly staff scheduling board (September 2026). Use it to calibrate depth and tone, not as a script: your screen, domain and user will differ.

## The request, cleaned up

> We need to redesign the scheduling board for better UX without losing any function.
>
> First, study the most recent changes to the operating model: how we've moved toward more efficient staffing guidelines that stay aligned with regulations. Pull the most recent merges.
>
> Then look at the board we have now. The UX is clunky, the information and layout are messy and hard to understand, and it isn't flexible or modern.
>
> Study these UX laws and how each applies to our scheduling board:
>
> 1. Hick's law
> 2. Fitts's law, including minimizing target distance
> 3. Jakob's law
> 4. Law of proximity
> 5. Miller's law
> 6. Doherty threshold
> 7. Von Restorff effect
> 8. Serial position effect
> 9. Peak-end rule
> 10. Zeigarnik effect
> 11. Law of Prägnanz
> 12. Law of similarity (keep patterns consistent)
> 13. Law of common region
> 14. Law of uniform connectedness (connect related elements visually)
> 15. Tesler's law
> 16. Postel's law
> 17. Parkinson's law
> 18. Occam's razor
> 19. Pareto principle
> 20. Aesthetic-usability effect
>
> Then write a plan and a structured prompt I can give Claude Design, so you have the right front end to implement. I want a premium feel, like Google or Apple design.

## What was corrected in the original

| Original | Correction |
|---|---|
| Numbered 1, 11, 20, 12, 3, 13… | Copied from a two-column layout; renumbered. "20. Fitts's law" was #2. |
| Zeigamnik effect | Zeigarnik effect |
| Law of Pregnanz | Law of Prägnanz |
| Uniform connec | Law of uniform connectedness |
| Tester's law | Tesler's law (Larry Tesler) |
| 16. Posters law and 17. Postel's law | Postel's law was listed twice. The user meant #16 as "maintain patterns consistently" and #17 as "connect related elements visually". Those are the law of similarity and uniform connectedness / common region, not Postel's law, which is "be liberal in what you accept and conservative in what you send". Postel's law stays once. |
| 8. Minimize target distance | The distance half of Fitts's law, not a separate law. Folded into #2. |
| (missing) | Added the law of common region and the aesthetic-usability effect at the user's request. That makes 20. |

## What each phase produced

1. **Ground truth.** Three parallel read-only agents covered the new staffing spec and recent merges (the rules: role ladder, state minimum, attendance bands, Duty and On-Call, hard versus soft rules), the board's full functional inventory, and prior briefs plus feedback from the program manager who uses it.
2. **Inventory.** About 60 functions across header, week status, grid, cells, person chips, the duties band, the add flow, drag, attendance, suggestions, time off, requests, notes and states. It became the brief's §8 parity checklist. Seven bugs were logged as "don't carry over".
3. **Baseline**, at 1440×900 on the live build: 2.84 screens tall; 40 of 62 chip labels truncated; smallest text 7.5px, with 63% of text under 12px; 95 of 113 controls under 44px; 4 typefaces; about 15 glyphs used as icons; dashed borders carrying 8 meanings. The finding a number didn't show: the Duty holder's name squeezed out by a backup picker on three days.
4. **Audit.** Twenty entries like: "*Hick's law.* Lead the add flow with the 1–3 people who close the gap; collapse the rest into Also free, Will be flagged, Can't add. Replace the five '+ duty / + assessor…' buttons with one add action per cell."
5. **Decisions** asked in one batch: visual direction (keep the brand, raise the craft), scope (the board and its overlays), and how to pull the latest code without losing local work.
6. **Brief.** Fifteen sections, saved as `docs/design-brief-scheduling-board-v4.md` in that repo, with acceptance targets such as "≤ 1.5 screens at 1440×900", "0 truncated names at 1280px", "add someone to a short cell in 2 interactions".
7. **Handoff and build.** Claude Design returned an HTML prototype (1.47 screens, 0 truncated names). The plan broke it into anatomy, visual system, components, interactions and easy-to-miss details, then listed where the build must differ: the prototype recomputed staffing rules in the browser and was wrong in more than ten places, so the build rendered the server's verdicts instead. It shipped as four PRs: pre-existing work, a rename, backend additions (edit hours, pin a draft, approve week, undo for time off and requests), then the new board. Real use then surfaced one gap: pop-up cards needed a visible × and click-outside to close.

## Tone that worked

- Directives name real elements ("the backup select", "the Duties band's five buttons"), never generic advice.
- Every number says where it was measured.
- Corrections to the user's list are stated plainly, once, with the reason.
- The user's own words are used for the feel ("premium, like Google or Apple"), then translated into specifics (one typeface, a 5-step type scale, one icon set, shadows only on floating layers).
