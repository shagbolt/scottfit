# scottfit

My fitness tracker for Carilion Workouts.

**Scott.Fit** is a single-file web app (`scott_workout_tracker.html`) for logging Tuesday/Thursday strength sessions at the Carilion Wellness Center on an iPhone. It pre-fills each workout from my 12-month strength roadmap, stores everything on the device, and runs from GitHub Pages:

**https://shagbolt.github.io/scottfit/scott_workout_tracker.html**

---

## How to use it

1. Open the link in Safari on the iPhone (or use the Home Screen shortcut).
2. Check the plan card at the top. It shows the current roadmap week, phase, and that week's note.
3. Each strength machine is already filled in with two sets at this week's planned weights. Adjust the weight or reps to what you actually did.
4. Tap the round set number when you finish a set; it turns into a ✓. Only completed sets count in your history.
   To change the order of the machines, tap **↕ Change order** in the Strength heading.
5. Tap **+ Add Set** for an extra set; it copies the set above it.
6. Tap **💾 Save Workout** in the bar at the bottom of the screen.

Watch for a green **Ready to move up** box on a machine. It appears when you've earned an increase under the roadmap's two-session rule, with a button to set the new weight.

When the roadmap spreadsheet is revised, load the new file from **⇅ Data → Load roadmap (.xlsx)**. No code changes are needed.

## Backing up

All data lives in local storage on the device that recorded it. On iPhone, open Scott.Fit from its **Home Screen icon**, not a Safari tab: Safari can clear a website's data after about a week without a visit, while Home Screen apps keep theirs. The two also keep separate storage, so move data between them with a backup. The app reminds you to back up every two weeks. You can also use **⇅ Data → Export JSON backup** anytime; on iPhone, choose **Save to Files** in the share sheet. A JSON backup restores everything: workouts, custom machines, machine settings, exercise order, and any loaded roadmap. CSV export is for spreadsheets.

## Files

| File | Purpose |
|---|---|
| `scott_workout_tracker.html` | The entire app (HTML, CSS, and JavaScript in one file) |
| `README.md` | This file |

---

## Changelog

### Version 5.1 — October 22, 2026: Easier machine reordering

- The Strength heading now has a visible **↕ Change order** button (it was a small text link before). The Machines panel has the same option.
- New **⤒** button sends a machine straight to the top, alongside ▲ and ▼ for one place at a time.
- Each machine shows its position number, and the one just moved stays highlighted and on screen.
- **Cancel** now discards changes; before, every tap was saved immediately. **Done** saves the new order.
- "Reset to roadmap order" previews the roadmap's order and is kept only if you tap Done.
- Instructions match the device: arrows on iPhone, drag handles plus arrows with a mouse or trackpad.

### Version 5 — October 22, 2026: Done tracking, move-up guidance, data safety

**Mark sets done**
- The set number on each row is now a large tap target. Tap it when the set is finished and it becomes a ✓; tap again to undo.
- Each card header shows its progress (for example "1/2"), and a ✓ appears after the machine name when every set is done.
- The bottom bar shows the whole workout's progress, for example "9 of 15 sets done."
- History, progress charts, CSV exports, the "↑" last-weight hints, and weight pre-fills count only completed sets. Workouts saved before this version have no done marks and still count in full.
- Saving with nothing marked done asks whether to mark every set done first.
- **⎘ Copy Last** brings in the previous workout's weights with every set unmarked.

**Ready to move up** (the roadmap's two-session rule)
- When the top of the rep range is reached on every planned set in the last two workouts at the same weight, the machine shows a green **Ready to move up** box and a ▲ beside its name. Its button sets each set 5 lb higher (never above the roadmap's target ceiling).
- When the roadmap raises the weight this week but the rule hasn't been met yet, an amber box suggests staying at the current weight, with a button to do that.
- When the top of the range was reached once, it notes that one more workout at that weight qualifies.
- At the target ceiling (the highest weight the roadmap reaches for that machine), it says to hold the weight.
- No advice is shown during Rebuild, Deload, Return, or Recovery weeks, when the roadmap sets the weights on purpose.

**Data safety**
- On iPhone in a Safari tab, a notice explains how to move to a Home Screen app safely: export a backup, add to Home Screen, then import the backup there. It can be postponed for a week.
- A backup reminder appears when there has never been a backup, or when the last one is over two weeks old and newer workouts exist. It can be postponed three days.
- On iPhone, exports open the share sheet (Save to Files, Mail, AirDrop). This works in Home Screen apps, where ordinary downloads are unreliable.
- The app asks the browser to keep its storage permanently where that is supported.
- Fixed: downloads could fail in Safari because the file link was released too quickly.

### Version 4 — October 21, 2026: Roadmap-driven workouts

**Training plan**
- Built in the 52-week *Scott-Strength-Roadmap-12mo-Revised.xlsx* plan (June 1, 2026 to May 30, 2027).
- New plan card at the top shows the week number, phase (Rebuild, Build, Deload, Recovery, Return, Maintain), dates, and the week's note. The card's accent color reflects the phase.
- Each strength card shows the week's targets, for example "This week: 50 lb × 10, then 45 lb × 12–15."
- Set rows pre-fill with the planned weight for each set; reps start at the low end of the target, with the full range shown beside the reps box (`/12–15`).
- "Fill weights from" menu: this week's plan (default), last session, or any past workout.
- Changing the session date switches to that week's plan. The app asks before replacing weights already typed in, and offers to open a workout already saved for that date.
- Recovery weeks and dates outside the roadmap fall back to the last workout's weights, and the plan card says so.
- Load an updated roadmap spreadsheet from the Data panel, or revert to the built-in one.
- The "Day Streak" stat (always 1 on a Tue/Thu schedule) is replaced by "Week _n_ of 52."

**Workout changes**
- Default is now **2 sets per machine**; more can be added.
- Shoulder Press and Hip Abduction are now built-in machines.
- Default exercise order follows the roadmap: Chest Press, Leg Press, Leg Curl, Leg Extension, Hip Abduction, Row, Shoulder Press. The ↕ reorder button still overrides it.
- **+ Add Set** now copies the previous set's weight and reps instead of a generic default.
- Removed the Balance section (SLB, Tandem, Side Stepper, Grapevine).
- Stretches trimmed to three: Cross Arm, Figure 4, and Hamstring (Touch Toes removed). The cool-down lap remains.

**Data migration (automatic, one time)**
- Custom machines named "Shoulder Press" or "Hip Abduction" are merged into the new built-ins, keeping their history, notes, settings, and position in the exercise order.
- A backup of the pre-migration data is saved in local storage (`scottfit_v3_backup_before_v4`).

**Fixes**
- The date rolled over to "tomorrow" after 8 pm because it was calculated in UTC; it now uses local time.
- Editing a custom machine or its settings no longer erases sets already entered for it.
- Custom machine cards could be duplicated after editing; fixed.
- A leftover unsaved draft from an earlier day now asks whether to finish it or start fresh, instead of reloading silently.
- The "saved" badge now reflects the selected date, not just today.
- Reopening the app after saving today's workout now shows that workout, instead of a fresh form that could overwrite it on the next save.
- The full CSV export was missing its "Notes" column header; exercise names are now quoted.
- The "↑" last-weight hint now compares against the most recent workout *before* the selected date.
- Exercise cards and chart tabs are now generated from one configuration list instead of several hard-coded copies.
- JSON backups now include the exercise order and any loaded roadmap.

### Version 3 — April 2026: Polish, export, and reordering

**Features**
- **↕ Reorder** for strength exercises (up/down arrows on iPhone, drag and drop on desktop), saved between sessions; chart tabs follow the same order.
- Export a single past workout as CSV or JSON from the ↓ button in Past Sessions.
- CSV import with a preview, plus a choice to merge with or replace existing data.
- **⎘ Copy Last** button to start from the most recent workout.
- Amber "unsaved changes" badge and a warning before leaving the page with unsaved work.
- Keyboard shortcuts: ⌘/Ctrl+S to save, ⌘/Ctrl+Shift+C to clear.
- Print layout for a clean paper copy of a workout.
- Sticky Save bar at the bottom of the screen on iPhone.
- "✓ saved" badge next to the session date.
- Expand all / collapse all for strength cards; Progress Charts collapsed by default.
- "Last Workout" date in the stats strip; Past Sessions show the top weight for each exercise.

**iPhone usability**
- Number pad keyboards for weight and reps, text selected on tap so a new value can be typed straight over it, and larger tap targets.
- 16 px input text to stop Safari from zooming in on focus.

**Fixes**
- Removed a duplicated copy of the page (second `<style>`, `<head>`, and `<body>`) that broke the theme toggle and script loading.
- Fixed broken JavaScript (a split regular expression and an unterminated string) that stopped the whole app from loading.
- Added `type="button"` to every button so Safari doesn't treat taps as form submissions.
- New custom machines could not be saved, and edits to existing machines didn't stick; both fixed.
- Clearer messages when phone storage is full.

### Version 2 — April 2026: iPhone and GitHub Pages

- Per-set logging with weight and reps for each set, plus automatic volume.
- Machine Manager: add custom machines and edit seat, arm, and chest settings, including tap-to-edit setting pills on each card.
- Pre-fill weights from the last session (or a chosen past session).
- JSON backup and restore; CSV export.
- Progress charts (max weight, total volume, total reps) for each exercise.
- Light and dark themes that follow the phone's setting.
- Add to Home Screen support and safe-area spacing for iPhone.
- Published on GitHub Pages.

### Version 1 — March 2026: First version

- Built from the Carilion fitness card: recumbent bike warm-up, sit-to-stand, five strength machines (Chest Press, Row, Seated Leg Curl, Seated Leg Press, Leg Extension), balance checklist, cool-down lap, and stretches.
- Workouts saved in the browser; history list and basic progress charts.
- Companion Excel workbook for logging and tracking personal bests.

---

## Technical notes

- Plain HTML, CSS, and JavaScript in one file. Chart.js 4.4.1 is loaded from cdnjs; SheetJS 0.18.5 is loaded only when a roadmap spreadsheet is imported.
- Local storage keys: `scottfit_v3_sessions`, `scottfit_v3_draft`, `scottfit_v3_machines`, `scottfit_v3_builtin_settings`, `scottfit_v3_strength_order`, `scottfit_v3_roadmap`, `scottfit_v3_last_backup`, `scottfit_v3_notice_snooze`, `scottfit_theme`.
- Each saved set is `{weight, reps, done}`. Sets without a `done` field (saved before Version 5) count as completed.
- Move-up rule: the last two workouts at the same weight must reach the top of every planned set's rep range. Increases are 5 lb, capped at the highest weight the roadmap reaches for that lift.
- The roadmap importer reads the "Weekly Roadmap" sheet. It expects a header row starting with "Week" that includes "Phase", lift names above "Set 1 / Set 2" columns, month rows such as "June 2026", and numbered week rows.
- Safari reminders: every `<button>` needs `type="button"`; avoid raw line breaks inside JavaScript strings; keep input text at 16 px or larger.
