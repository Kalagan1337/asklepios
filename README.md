# Asklepios (Асклепій): an offline AI medic for a crew on its way to Mars

**NASA Space Apps Challenge 2026** · Local event: Dnipro, Ukraine · Challenge: **Create Health Monitoring Software for Astronauts on Space Missions**
**Team vod0laz1:** Maksym, Matvii, Dmytro, Stanislav, Denys

**Live app:** {{APP_LINK}} · **30-second demo:** {{DEMO_LINK}}

[English](#english) · [Українська](#українська)

![The start guide of Asklepios](screenshots/01-start-guide.png)

---

## English

### What it is

On the way to Mars, a doctor’s answer takes up to 44 minutes round trip, and for about two weeks around solar conjunction there is no contact at all. There is no doctor on board, only a crew medical officer with short training, no evacuation, and no resupply of medicines.

Asklepios is health-monitoring and decision-support software that lives on board. It:

- watches each astronaut’s vital signs against **their own baseline** and raises an alarm when a value needs attention;
- asks every crew member for a **daily check-in** (sleep, mood, blood sugar) and shows **7-day color-coded trends**;
- turns a complaint typed **in plain English or Ukrainian** into an **explained decision**: urgency, the evidence behind it, treatment steps, medicines from the onboard kit and an automatic re-check;
- covers what a long mission needs: a pharmacy forecast to the end of the mission, a mode for when the medical officer is the patient, training alarms, and a crew guardian that acts when nobody can.

Everything is **one HTML file (1.44 MB)** that runs in any modern browser with **no internet, no server and no installation**. The interface is in English and Ukrainian.

### Files

| File | What it is |
|---|---|
| `index.html` | **The app.** Double-click to open it in Chrome, Edge or Firefox. Works offline. Language: UA / EN at the top. |
| `presentation.html` | Full deck, 14 slides, English and Ukrainian. → or a click: next; the left edge: back; L: language; F: full screen. |
| `pitch-7-slides.html` | 7-slide English deck (title included), the alternative project demo. |
| `defense.html` | 5-slide deck for the live defense; opens in Ukrainian, `?lang=en` or L switches to English. |
| `Asklepios-demo-30s-EN.mp4` | The 30-second demo (29.6 s), English subtitles, silent. |
| `Asklepios-video-EN.mp4` | The full film (1:48), English subtitles, silent. |
| `screenshots/` | Five 1920×1080 screenshots of the English app. |
| `LICENSE` | MIT license. |

### Start here

On first open the app shows a **“Start here”** window with five choices; each one starts at once:

1. **CO₂ build-up**: CO₂ rises in the lab, the monitor raises the alarm, the AI medic asks questions and explains its decision.
2. **Describe a complaint**: examine anyone in the crew; type what is wrong in your own words.
3. **Training alarm**: someone suddenly gets worse; you have 2 minutes to help.
4. **Problem catalog**: 2,792 health problems, search in your own words.
5. **Depressurization**: the crew is unconscious, so the ship acts on its own.

“Just look around” closes the window; the **Start here** button in the header opens it again. The footer says: *“Prototype. Vital signs are simulated. Not medical advice.”*

**A three-minute tour:** Start here → **CO₂ build-up** → when the red alarm appears, **Examine** → type `I feel dizzy, it is hard to breathe, no nausea` → Enter → **Next →** → “Do others in this module feel the same?” **Yes** → **Show decision →** → read **Why** and open **How the system decided** → tick the four steps (start with “Move to a module with normal air”) → the re-check says the vitals are back to normal. Then click **Illia’s** line “Check-in: not yet · sleep ↓ · mood ↓” in the crew column to see his 7-day trends, and search the **Problem catalog** for `blocked ear` or `chest pain`.

### How Asklepios answers the challenge

The challenge suggests tracking *“blood pressure, heart rate, blood sugar, body temperature, daily sleep hours, and mood.”* Asklepios tracks all six:

| Indicator | How Asklepios measures it | What it does with it |
|---|---|---|
| **Heart rate** | Every second for each person (simulated wearable stream), with a 90-second chart and a dashed line at the person’s baseline | Caution above max(105, baseline + 45) bpm; alarm above max(140, baseline + 75) or below 40; an “irregular rhythm” flag; evidence for the heart-rhythm and other protocols |
| **Blood pressure** | Systolic/diastolic for each person, shown on the crew card (simulated; in flight a cuff from the medical kit) | Alarm below 90 systolic, caution above 150; high pressure counts as evidence in kidney colic; below 85 makes the decision life-threatening |
| **Blood sugar** | Optional field of the daily check-in, 40–400 mg/dL | Caution below 70 or above 180, alarm below 54 or above 250; an out-of-range value raises the exam’s urgency and shows three simple steps (re-check; 15 g of fast sugar if low or water and no sweets if high; call the medical officer) |
| **Body temperature** | Every second for each person | Caution at max(37.8, baseline + 1.1) °C, alarm at max(39, baseline + 2.0) °C; a baseline up to 38.2 °C is accepted because resting temperature rises in flight (“space fever”) |
| **Daily sleep hours** | Daily check-in slider, 0–14 h | Caution below 6 h, alarm below 4.5 h; two short nights out of the last three count as evidence for the *Sleep disorder* protocol |
| **Mood** | Daily check-in, five drawn faces from “Very bad” to “Great” | Caution at 2 or lower, alarm at 1; a low mood raises any decision to at least “Needs medical officer” and suggests talking to the medical officer or psychological support |

It also follows SpO₂, breathing rate, CO₂ in each module and each person’s radiation dose.

The challenge’s other questions:

- **Which measurements can be done in space?** Wearable signals (heart rate, SpO₂, breathing, skin temperature, as on CSA’s Astroskin), a cuff, a thermometer and a glucometer from the medical kit, and a one-minute check-in.
- **Why is an exam needed?** Numbers alone do not tell a headache from a CO₂ problem. The 4-step exam (Patient → Complaints → Questions → Decision) combines complaints, sensors, mission context and answers.
- **How do spaceflight hazards change the indicators?** Each demo scenario and the check-in carry a tag naming the NASA HRP hazard it illustrates (table below), and the protocols use the context: CO₂ in the module, the flight day, a recent spacewalk, a solar proton event.
- **When does a result need the crew or the flight surgeon?** Status colors (Normal, Caution, Alarm) on every reading, and four urgency levels on every decision: *Self-care*, *Needs medical officer*, *Urgent*, *Life-threatening*.
- **What actions prevent a critical condition?** Step-by-step treatment checklists, medicines checked against allergies and stock, an automatic re-check, and training alarms that rehearse the response.
- **Interface:** animated live charts, color coding, a daily reminder (“Daily check-in: 4 of 4 haven’t checked in yet”), a graded 2-minute training game, and a simple mode with short steps and large text.

### Features

| Part | What it does |
|---|---|
| Crew monitor | Four crew members on the ship “Argo”, day 214 of an 860-day mission. Pulse, SpO₂ and temperature every second; blood pressure, breathing and the daily radiation dose under each card. Limits come from each person’s baseline. An alarm appears at once and clears only after 6 calm seconds, so it does not flicker. |
| Daily check-in | Sleep, mood, optional blood sugar and a note, once per mission day. A reminder at the top of the crew column, a line on each crew card, an overview with the last 7 days as colored squares, and for each person three 7-day charts (sleep bars with a 6 h line, mood faces over an amber band, sugar dots over the 70–180 band). Six earlier days of example data are included and labeled. |
| Exam in 4 steps | Complaints in plain English or Ukrainian. The parser handles word stems, negations (“no nausea”, “I don’t have a headache but…”), clauses split by commas and “but”, and matching against the catalog. |
| Explained decision | Urgency level, a **Why** line, and **How the system decided**: every piece of evidence with its weight and source (complaint, sensor, context, answer, daily check-in), plus what was ruled out. Then a checklist of steps, medicines and an automatic before-and-after re-check. |
| Knowledge base | 12 onboard protocols, 3 red-flag rules (possible head injury, anaphylaxis, heart attack) and a general algorithm for everything else. A protocol is named only with enough evidence (35% or more, with objective support where needed); otherwise the screen says “The cause is not clear yet” and lists up to three possibilities. |
| Problem catalog | 2,792 health problems in 15 body sections, 14,240 search phrasings in Ukrainian and 15,444 in English, best matches first, A–Z index, one-typo tolerance. 363 entries are marked life-threatening and 841 urgent; they raise the urgency automatically. The crew can add their own problems. |
| Medical card | Records per person: problem, severity 1–10, onset, note; filters by person; the daily check-in block. |
| People | Add, edit or remove crew members: role, module, allergies (penicillins, NSAIDs) and personal baselines. A new person appears everywhere at once. |
| Pharmacy for the whole mission | 17 items. Courses on board against courses needed until the end of the mission, allergy substitutes (for example levofloxacin instead of amoxicillin/clavulanate for a penicillin allergy), expiry dates and an approximate radiation-potency model. |
| “The medic is ill” | When the patient is the crew medical officer, a simple mode for a helper with no training: short steps, large text, dose lines, and “The commander decides after consulting Earth”, or “at once” in an emergency. |
| Test mode | A training alarm: who, what (suffocation from CO₂ build-up, arrhythmia, kidney colic, decompression) and when. Without help the patient gets worse. The test passes only when the right protocol is running, all its steps are ticked and the vitals are back to normal. Grades: Excellent, Good, Just in time, Too late, with a breakdown. |
| Crew guardian | If at least 3 people (or the whole crew, if smaller) fall below their SpO₂ limit and nobody responds, a 6-second countdown with an “I am conscious” button; then the ship sounds the siren, closes the hatches, isolates the leak in the airlock and supplies oxygen from reserve. |
| Readiness | A 5-try reaction test before docking, a spacewalk or robotic-arm work, compared with the person’s baseline and sensors. |
| Log | Alarms, decisions, steps and check-ins of the current session. |

### NASA Human Research Program: five hazards, five answers

| Hazard (NASA HRP) | What Asklepios does about it | Where to see it |
|---|---|---|
| Space radiation | Radiation background and each person’s daily dose; the *Solar flare* scenario (proton event, shelter, acute radiation reaction protocol); radiation-potency model for medicines | Air and radiation panel, crew cards, Pharmacy |
| Isolation and confinement | Daily check-in: sleep and mood with 7-day trends and a daily reminder; a low mood raises the exam’s urgency | Crew column, Medical card |
| Distance from Earth | All decisions are made on board, offline; a pharmacy for the whole mission; *The medic is ill* mode; training alarms | Everywhere; Demo scenarios; Test tab |
| Gravity fields | Protocols for vision change (SANS), back pain, kidney stones (*Kidney colic* scenario) and heart rhythm (*Arrhythmia* scenario) | Exam, Demo scenarios |
| Hostile closed environments | *CO₂ build-up*, the *Depressurization* guardian, *Decompression after a spacewalk* | Start here, Demo scenarios |

In the app each scenario, the test mode and the daily check-in carry a small tag such as “NASA HRP: hostile closed environments”.

### Architecture

```mermaid
flowchart LR
  subgraph inputs["Inputs"]
    V["Vital signs every second<br/>pulse, SpO₂, temperature,<br/>blood pressure, breathing<br/>(simulated in the prototype)"]
    ENV["Module CO₂<br/>and radiation dose"]
    CI["Daily check-in<br/>sleep, mood, blood sugar"]
    TXT["Complaint in plain words<br/>English or Ukrainian"]
  end
  V --> FL["Flags against each<br/>person's own baseline<br/>alarm at once, all-clear<br/>after 6 calm seconds"]
  ENV --> FL
  FL --> AL["Alarm bar"]
  FL --> GD["Crew guardian<br/>3 or more crew below<br/>their SpO₂ limit"]
  TXT --> NLP["Parser<br/>stems, negations, clauses"]
  NLP --> CAT["Catalog match<br/>2,792 problems<br/>363 red flags"]
  NLP --> EV["Evidence with weights<br/>complaints, sensors,<br/>context, answers, check-in"]
  CAT --> EV
  CI --> EV
  FL --> EV
  EV --> KB["12 protocols<br/>3 red-flag rules<br/>general algorithm"]
  KB --> DEC["Decision<br/>urgency, Why, steps"]
  DEC --> MED["Medicines<br/>allergies, stock to mission end,<br/>expiry, potency"]
  DEC --> RE["Automatic re-check<br/>before and after"]
  DEC --> LOG["Log and medical card<br/>stored only in this browser"]
```

- **Classic, explainable AI:** a rule-based expert system with a weighted-evidence inference engine. The confidence shown is the protocol’s share of the evidence points, damped when there is little evidence; it is not a calibrated probability. When two options are close, the more dangerous one sets the urgency.
- **One file:** HTML, CSS and plain JavaScript with no libraries, no external fonts and no network calls. Data (records, people, check-ins, custom problems, test history, language) stays in the browser’s localStorage on that computer; “Clear all data” in the Demo scenarios menu removes it.
- **Simulation:** a 1-second tick drives a physiology model per person; speed ×1, ×10 or ×60.

### Validation (measured by the team on the final build)

Measured on 14 November 2026 on the final `index.html` (1,441,067 bytes, SHA-256 `8db72f08…94c0290`) in headless Chrome, with a scripted test that drives the real app:

| Check | Result |
|---|---|
| Scenario complaints → the expected protocol (6 demo scenarios + 4 training alarms) | **10 / 10** |
| Free complaints, normal sensors, 18 Ukrainian + 12 English phrases → a safe decision* | **30 / 30** |
| CO₂ build-up demo path | alarm after 10 simulation ticks (about 9 s in real time); “Excess CO₂ and low oxygen”, Urgent, confidence 75–83% depending on when the exam starts; re-check “better: readings are back to normal” about 5 s after the first step |
| Network requests while running | **0** (only the file itself is opened) |
| Console errors and exceptions | **0** |
| Size | **1.44 MB**, one file, no dependencies |

\* Safe means: the right protocol, a red-flag decision, or the general algorithm at a fitting urgency; “no complaint recognized” only for phrases where nothing is wrong. The criteria were written per phrase before scoring.

<details>
<summary>Confidence per scenario and the 30 free complaints</summary>

Scenarios: CO₂ build-up 82%, The medic is ill 71%, Arrhythmia 40%, Decompression after a spacewalk 79%, Kidney colic 53%, Solar flare 71%. Training alarms: suffocation 80%, arrhythmia 55%, kidney colic 53%, decompression 79%.

| Phrase (Ukrainian phrases with an English gloss) | Decision | Urgency |
|---|---|---|
| «голова паморочиться, важко дихати, нудоти немає» (dizzy, hard to breathe, no nausea) | The cause is not clear yet | Urgent |
| «болить голова» (headache) | The cause is not clear yet | Needs medical officer |
| «не болить голова, але нудить» (no headache, but nauseous) | A symptom without an onboard protocol | Needs medical officer |
| «болить у грудях, віддає в ліву руку» (chest pain going to the left arm) | Possible heart attack | Life-threatening |
| «тисне в грудях, холодний піт» (chest pressure, cold sweat) | Possible heart attack | Life-threatening |
| «вдарився головою, тепер хочеться спати» (hit my head, now sleepy) | Possible head injury | Life-threatening |
| «болить живіт справа внизу і температура» (lower right belly pain and fever) | Infection with fever | Urgent |
| «опік руки окропом» (scalded hand) | A symptom without an onboard protocol | Needs medical officer |
| «набрякли губи, висип і важко дихати після таблетки» (swollen lips, rash, hard to breathe after a pill) | Possible anaphylaxis | Life-threatening |
| «не можу помочитися» (cannot pass urine) | A symptom without an onboard protocol | Urgent |
| «болить зуб» (toothache) | A symptom without an onboard protocol | Needs medical officer |
| «поганий настрій, нічого не хочеться, не бачу сенсу» (low mood, see no point) | A symptom without an onboard protocol | Needs medical officer |
| «порізав палець, кров не зупиняється» (cut finger, bleeding will not stop) | A symptom without an onboard protocol | Life-threatening |
| «немає сил і морозить» (no strength, chills) | Infection with fever | Needs medical officer |
| «не можу дихати» (cannot breathe) | The cause is not clear yet | Urgent |
| «кашель з кров’ю» (coughing blood) | The cause is not clear yet | Life-threatening |
| «все добре, нічого не болить» (all good, nothing hurts) | No complaint recognized | none |
| «закладає вухо» (blocked ear) | A symptom without an onboard protocol | Needs medical officer |
| I feel dizzy, it is hard to breathe, no nausea | The cause is not clear yet | Urgent |
| crushing chest pain going to my left arm | Possible heart attack | Life-threatening |
| I hit my head and now I feel sleepy | Possible head injury | Life-threatening |
| pain in my lower right belly and a fever | Infection with fever | Urgent |
| my lips are swollen, rash and hard to breathe after a pill | Possible anaphylaxis | Life-threatening |
| I can’t pee | A symptom without an onboard protocol | Urgent |
| I don’t have a headache but I feel sick | A symptom without an onboard protocol | Needs medical officer |
| no fever, no cough, just tired | The cause is not clear yet | Needs medical officer |
| I feel hopeless and can’t stop crying | A symptom without an onboard protocol | Urgent |
| burned my hand on a hot plate | A symptom without an onboard protocol | Urgent |
| toothache | A symptom without an onboard protocol | Needs medical officer |
| my ear feels blocked | A symptom without an onboard protocol | Needs medical officer |

With normal sensors and normal module air, “dizzy, hard to breathe” is not named as a CO₂ problem: that protocol needs objective support (high module CO₂, low SpO₂, fast breathing, or others in the module feeling the same).

</details>

This is engineering validation, not clinical validation. The next step is a set of standardized clinical cases reviewed by physicians.

### NASA data and resources

| Data or resource | Where it comes from | How Asklepios uses it |
|---|---|---|
| The five hazards of human spaceflight | NASA Human Research Program, [5 Hazards of Human Spaceflight](https://www.nasa.gov/hrp/hazards/) | The feature map of the whole product (table above); every scenario, the test mode and the daily check-in carry a “NASA HRP: …” tag |
| Human spaceflight risks | NASA HRP, [Risks of Human Spaceflight](https://www.nasa.gov/hrp/risks/) | Which conditions get an onboard protocol: vision change (SANS), kidney stones, decompression sickness, heart rhythm problems, sleep and behavioral health, radiation, in-flight medical conditions |
| Research done in flight | NASA HRP, [Ongoing HRP Research in Space](https://www.nasa.gov/hrp/ongoing-hrp-research/) | Background for what can be measured on board and why repeated, routine measurements matter |
| CO₂ limit: no more than 3 mmHg as a 1-hour average | NASA-STD-3001 and the NASA OCHMO [CO₂ technical brief](https://www.nasa.gov/wp-content/uploads/2023/03/co2-technical-brief-ochmo.pdf) | Module CO₂ above 3 mmHg is a caution flag and above 5 an alarm; in the decision it is +4 evidence, shown as “… mmHg vs NASA limit 3”; the *CO₂ build-up* scenario |
| CO₂ and headache: the odds roughly double with every extra 1 mmHg | Law et al., NASA JSC, 2014 ([summary](https://www.sciencedaily.com/releases/2014/05/140501100922.htm)) | Why module CO₂ is weighed as its own evidence |
| Radiation dose in cruise to Mars, about 1.8 mSv per day | Curiosity RAD measurements (Zeitlin et al., *Science*, 2013; [SwRI release](https://www.swri.org/press-release/swri-led-team-calculates-radiation-exposure-associated-trip-mars)) | Background of 75 µSv/h, which is 1.8 mSv per day; each person’s daily dose on the crew card; the approximate radiation-potency model of the pharmacy |
| Signal delay 3–22 minutes one way; a blackout of about 13 days at solar conjunction | NASA: [Mars 2020 communications](https://science.nasa.gov/missions/mars-2020-perseverance/speaking-percys-language-how-to-talk-so-perseverance-will-listen/), [Mars communications disruption and delay](https://www.nasa.gov/wp-content/uploads/2024/01/mars-communications-disruption-and-delay.pdf) | The reason everything runs on board; in an emergency the simple mode says the commander decides at once, because an answer from Earth takes up to 44 minutes |
| Health checks on the ISS are periodic, not continuous | NASA Glenn, [Exploration medical technologies](https://www.nasa.gov/glenn/glenn-expertise-space-exploration/human-health-performance/exploration-medical-technologies/multifunctional-integrated-medical-devices) | Why Asklepios watches continuously and adds a daily check-in |
| ISS medical kit contents | NASA [medical kit checklist](https://www.nasa.gov/wp-content/uploads/2015/03/medical_kit_checklist_-_full_release.pdf) | The pharmacy is modeled on drugs carried on the ISS (paracetamol, ibuprofen, ketorolac, tamsulosin, promethazine, ondansetron, levofloxacin, metoprolol, melatonin, adrenaline, diphenhydramine, aspirin); the kit’s blood pressure cuff and thermometer are the in-flight sources of those readings |
| Personal dosimetry | NASA SRAG, [Crew Active Dosimeter](https://srag.jsc.nasa.gov/spaceradiation/how/how.cfm) | The planned real source of each person’s dose |

### Space agency partner data

| Data or resource | Agency | How Asklepios uses it |
|---|---|---|
| [Monitoring Radiation for Astronaut Health](https://www.asc-csa.gc.ca/eng/news/articles/2026/2026-02-26-monitoring-radiation-astronaut-health.asp) (2026): neutrons are about 30% of the radiation on the ISS; the CANS instrument will measure them continuously and autonomously | CSA | Supports continuous, autonomous radiation monitoring instead of sessions; cited on the science slides |
| [Bio-Monitor](https://www.asc-csa.gc.ca/eng/sciences/bio-monitor.asp) / [Astroskin](https://www.asc-csa.gc.ca/eng/sciences/astroskin.asp) smart shirt, on the ISS since December 2018: ECG, breathing, skin temperature, pulse and SpO₂ from a headband sensor, about 48 h of battery | CSA | The simulated sensor stream is modeled on what Astroskin measures; it is the first real data source we would connect |
| [Why Do We Conduct Science Experiments in Space?](https://www.asc-csa.gc.ca/eng/iss/science/why-do-we-conduct-science-experiments-in-space.asp) | CSA | Background on how spaceflight changes the body |
| [Circadian Rhythms](https://www.esa.int/Science_Exploration/Human_and_Robotic_Exploration/Research/Keeping_the_rhythm_in_space) experiment and the Double Sensor for core body temperature; [Thermolab](https://www.dlr.de/en/latest/news/2009/20091015_from-charit-into-space-thermolab-experiment-starts-on-the-iss_20458/@@download/file) | ESA, DLR | The in-flight source for body temperature |
| “Space fever”: resting core temperature about 1 °C higher after months in orbit, above 40 °C during exercise (Stahn et al., *Scientific Reports*, 2017, [PMC5701078](https://pmc.ncbi.nlm.nih.gov/articles/PMC5701078)) | ESA / DLR / Charité study | Temperature limits are set from each person’s baseline, and a baseline up to 38.2 °C is accepted |

**Other references:** International Consensus on Time in Range (Battelino et al., *Diabetes Care*, 2019) for the 70–180, 54 and 250 mg/dL glucose limits; Barger et al., *Lancet Neurology*, 2014, on short sleep in flight (about 6 hours a night) as context for daily sleep tracking; Wotring, *AAPS Journal*, 2016, on medicines stored 550 days on the ISS.

### Limitations

- Vital signs and crew data are **simulated**; no real person’s data is used.
- The radiation-potency model for medicines is **approximate**. A NASA study of medicines kept 550 days on the ISS found no unusual degradation, so expiry dates (also tracked) matter more.
- The protocols are simplified and are **not medical advice**; this is not a medical device. Check-in limits are typical clinical ranges, not mission-certified ones.
- The problem catalog describes real symptoms, but it is **not an official medical reference**.
- Drug use rates and stock are our assumptions; a real system would take them from NASA’s Integrated Medical Model.
- The log lasts for the current session only.

### What’s next

1. Real sensors over Web Bluetooth (standard heart-rate chest straps), then an Astroskin-class wearable.
2. Pulse from the tablet camera (rPPG).
3. A small language model on the onboard computer for conversation, also offline; red flags and limits stay as rules.
4. Clinical review of the protocols with physicians, and a field test at a polar station or on a ship.
5. On Earth: polar stations, ships at sea and remote clinics have the same problem, help is far away.

### License, credits and tools

- Code and content: **MIT License**, © 2026 vod0laz1 (see `LICENSE`).
- No third-party code, libraries, fonts, images or music. Icons and graphics are inline SVG made for this project; the videos are screen recordings of the app with subtitles.
- NASA, CSA, ESA and other sources are cited above and are not redistributed. No NASA logos or other agency branding are used.
- Tools used: HTML, CSS and JavaScript, no libraries; headless Chrome and ffmpeg for the videos; an AI assistant (Claude by Anthropic) for code, catalog translation and media under the team’s direction.

---

## Українська

### Що це

На шляху до Марса відповідь лікаря з Землі йде до 44 хвилин туди й назад, а приблизно два тижні під час сонячного з’єднання зв’язку немає взагалі. Лікаря на борту немає, лише медофіцер екіпажу з короткою підготовкою; евакуації немає, аптечку не поповнити.

Асклепій — програма для моніторингу здоров’я й підтримки рішень, яка живе на борту. Вона:

- стежить за показниками кожного астронавта щодо **його власної норми** й вмикає тривогу, коли показник потребує уваги;
- щодня просить кожного пройти **щоденну перевірку** (сон, настрій, цукор крові) і показує **тренди за 7 днів** із кольоровим кодуванням;
- перетворює скаргу, написану **звичайними словами українською чи англійською**, на **пояснене рішення**: терміновість, докази, кроки лікування, ліки з бортової аптечки й автоматичну повторну перевірку;
- покриває те, що потрібно в довгій місії: прогноз аптечки до кінця місії, режим, коли хворіє сам медофіцер, навчальні тривоги й вартового екіпажу, який діє, коли ніхто не може.

Усе це **один HTML-файл (1,44 МБ)**, що працює в будь-якому сучасному браузері **без інтернету, сервера й встановлення**. Інтерфейс українською та англійською.

### Файли

| Файл | Що це |
|---|---|
| `index.html` | **Застосунок.** Двічі клацніть: відкриється в Chrome, Edge або Firefox. Працює без інтернету. Мова: UA / EN угорі. |
| `presentation.html` | Повна презентація, 14 слайдів, українською й англійською. → або клацання: далі; лівий край: назад; L: мова; F: повний екран. |
| `pitch-7-slides.html` | 7 слайдів англійською (разом із титульним) — альтернативне демо проєкту. |
| `defense.html` | 5 слайдів для захисту; відкривається українською, `?lang=en` або L — англійська. |
| `Asklepios-demo-30s-EN.mp4` | 30-секундне демо (29,6 с), англійські субтитри, без звуку. |
| `Asklepios-video-EN.mp4` | Повний фільм (1:48), англійські субтитри, без звуку. |
| `screenshots/` | П’ять знімків англійського інтерфейсу 1920×1080. |
| `LICENSE` | Ліцензія MIT. |

### З чого почати

Під час першого запуску застосунок показує вікно **«З чого почати»** з п’ятьма варіантами; кожен запускається одразу:

1. **Накопичення CO₂**: у лабораторії росте CO₂, монітор вмикає тривогу, ШІ-медик розпитує й пояснює рішення.
2. **Опишіть свою скаргу**: огляд будь-кого з екіпажу; напишіть своїми словами, що турбує.
3. **Навчальна тривога**: комусь раптово погано, на допомогу 2 хвилини.
4. **Каталог проблем**: 2 792 проблеми зі здоров’ям, пошук своїми словами.
5. **Розгерметизація**: екіпаж непритомний, корабель діє сам.

«Просто подивитися» закриває вікно; кнопка **«З чого почати»** вгорі відкриває його знову. Унизу вікна: *«Прототип. Показники симульовані. Не є медичною порадою.»*

**Маршрут на три хвилини:** «З чого почати» → **«Накопичення CO₂»** → коли з’явиться червона тривога, **«Оглянути»** → напишіть `голова паморочиться, важко дихати, нудоти немає` → Enter → **«Далі →»** → «Інші в цьому модулі відчувають те саме?» **«Так»** → **«Показати рішення →»** → прочитайте **«Чому»** й відкрийте **«Як система ухвалила рішення»** → відмітьте чотири кроки (першим «Перейти в модуль із нормальним повітрям») → повторна перевірка скаже, що показники повернулися до норми. Потім клацніть у колонці екіпажу рядок **Іллі** «Перевірка: ще ні · сон ↓ · настрій ↓», щоб побачити тренди за 7 днів, і пошукайте в **«Каталозі проблем»** `закладає вухо` або `біль у грудях`.

### Як Асклепій відповідає на завдання

Завдання радить стежити за такими показниками: *артеріальний тиск, пульс, цукор крові, температура тіла, години сну за добу й настрій.* Асклепій відстежує всі шість:

| Показник | Як вимірюється | Що з ним робить система |
|---|---|---|
| **Пульс** | Щосекунди для кожного (симульований потік із натільного датчика), графік за 90 секунд і пунктир на рівні особистої норми | Увага вище max(105, норма + 45), тривога вище max(140, норма + 75) або нижче 40; ознака «нерегулярний ритм»; доказ для протоколу порушення ритму та інших |
| **Артеріальний тиск** | Верхній і нижній для кожного, на картці екіпажу (симульовано; у польоті — манжета з аптечки) | Тривога, якщо верхній нижче 90, увага — вище 150; високий тиск — доказ при нирковій коліці; нижче 85 робить рішення «Загроза життю» |
| **Цукор крові** | Необов’язкове поле щоденної перевірки, 40–400 мг/дл | Увага нижче 70 або вище 180, тривога нижче 54 або вище 250; значення поза нормою підвищує терміновість огляду й показує три прості кроки |
| **Температура тіла** | Щосекунди для кожного | Увага від max(37,8, норма + 1,1) °C, тривога від max(39, норма + 2,0) °C; норму до 38,2 °C можна задати, бо в польоті температура в спокої зростає («космічна лихоманка») |
| **Години сну** | Повзунок щоденної перевірки, 0–14 год | Увага менше 6 год, тривога менше 4,5 год; дві короткі ночі з останніх трьох — доказ для протоколу «Порушення сну» |
| **Настрій** | Щоденна перевірка, п’ять намальованих облич від «Дуже погано» до «Чудово» | Увага при 2 і нижче, тривога при 1; низький настрій підвищує будь-яке рішення щонайменше до «Потрібен медофіцер» і радить поговорити з медофіцером або психологічною підтримкою |

Додатково система стежить за SpO₂, частотою дихання, CO₂ у кожному модулі й дозою радіації кожного.

Інші питання завдання:

- **Що можна виміряти в космосі?** Сигнали натільного датчика (пульс, SpO₂, дихання, температура шкіри, як в Astroskin Канадського космічного агентства), манжета, термометр і глюкометр з аптечки та хвилинна щоденна перевірка.
- **Навіщо огляд?** Самі числа не відрізнять звичайний головний біль від надлишку CO₂. Огляд у 4 кроки (Пацієнт → Скарги → Питання → Рішення) поєднує скарги, датчики, обставини місії та відповіді.
- **Як небезпеки польоту змінюють показники?** Кожен сценарій і щоденна перевірка мають позначку небезпеки NASA HRP (таблиця нижче), а протоколи враховують обставини: CO₂ у модулі, день польоту, нещодавній вихід у відкритий космос, сонячну протонну подію.
- **Коли результат потребує уваги екіпажу чи лікаря з Землі?** Кольори стану (Норма, Увага, Тривога) на кожному показнику й чотири рівні терміновості рішення: *Самодопомога*, *Потрібен медофіцер*, *Терміново*, *Загроза життю*.
- **Які дії запобігають критичному стану?** Покрокові плани лікування, ліки з перевіркою алергій і запасу, автоматична повторна перевірка й навчальні тривоги, що тренують реакцію.
- **Інтерфейс:** живі анімовані графіки, кольорове кодування, щоденне нагадування («Щоденна перевірка: 4 з 4 ще не відмітилися»), гра на 2 хвилини з оцінкою та простий режим із короткими кроками й великим текстом.

### Можливості

| Розділ | Що робить |
|---|---|
| Монітор екіпажу | Четверо на кораблі «Арго», день 214 із 860. Пульс, SpO₂ і температура щосекунди; тиск, дихання й доза за добу під кожною карткою. Межі рахуються від особистої норми. Тривога вмикається одразу, а знімається лише після 6 спокійних секунд, тож не мигає. |
| Щоденна перевірка | Сон, настрій, за бажанням цукор крові й нотатка, раз на день місії. Нагадування вгорі колонки екіпажу, рядок на картці кожного, огляд усіх із 7 останніми днями кольоровими квадратами, а для кожного — три графіки за 7 днів. Шість попередніх днів прикладу даних позначено. |
| Огляд у 4 кроки | Скарги звичайними словами українською чи англійською: основи слів, заперечення («нудоти немає»), поділ фрази на частини («але», “but”), пошук у каталозі. |
| Пояснене рішення | Рівень терміновості, рядок **«Чому»** і **«Як система ухвалила рішення»**: кожен доказ із вагою та джерелом (скарга, датчик, обставини, відповідь, щоденна перевірка) і що виключено. Далі кроки, ліки й автоматична повторна перевірка «до і після». |
| База знань | 12 бортових протоколів, 3 правила червоних прапорців (можлива черепно-мозкова травма, анафілаксія, інфаркт) і загальний алгоритм для решти. Протокол називається лише за достатніх доказів (від 35%, де потрібно — з об’єктивним підтвердженням); інакше система пише «Причина поки неясна» й показує до трьох можливих варіантів. |
| Каталог проблем | 2 792 проблеми в 15 розділах тіла, 14 240 формулювань для пошуку українською і 15 444 англійською, спершу найточніші, абетка, допуск однієї помилки. 363 записи позначено як загрозу життю, 841 — як термінові; вони автоматично підвищують терміновість. Екіпаж може додати свою проблему. |
| Медкартка | Записи кожного: проблема, сила 1–10, коли почалося, нотатка; фільтр за людиною; блок щоденної перевірки. |
| Люди | Додати, змінити, видалити: роль, модуль, алергії (пеніциліни, НПЗП) і особиста норма. Нова людина одразу з’являється всюди. |
| Аптечка на всю місію | 17 позицій. Курси на борту проти потрібних до кінця місії, заміна при алергії (наприклад, левофлоксацин замість амоксициліну/клавуланату), строки придатності й умовна модель втрати активності від радіації. |
| «Медик захворів» | Коли пацієнт — сам медофіцер, простий режим для помічника без підготовки: короткі кроки, великий текст, дози й «Рішення командира після консультації з Землею», а в екстреному випадку — «одразу». |
| Тестовий режим | Навчальна тривога: кому, що (задуха через накопичення CO₂, аритмія, ниркова коліка, декомпресія) і коли. Без допомоги стан погіршується. Тест пройдено, лише коли розпочато правильний протокол, відмічено всі кроки й показники повернулися до норми. Оцінки: Відмінно, Добре, Встигли в останню мить, Не встигли — і розбір. |
| Вартовий екіпажу | Якщо щонайменше троє (або весь менший екіпаж) опускаються нижче своєї межі SpO₂ і ніхто не відповідає — відлік 6 секунд із кнопкою «Я при тямі»; далі корабель вмикає сирену, зачиняє люки, ізолює витік у шлюзі й подає кисень із резерву. |
| Допуск | Тест реакції з 5 спроб перед стикуванням, виходом у відкритий космос або роботою маніпулятором, порівняно з особистою нормою й датчиками. |
| Журнал | Тривоги, рішення, кроки й перевірки поточного сеансу. |

### П’ять небезпек NASA HRP — п’ять відповідей

| Небезпека (NASA HRP) | Що робить Асклепій | Де побачити |
|---|---|---|
| Космічна радіація | Радіаційний фон і доза кожного за добу; сценарій «Сонячний спалах» (протонна подія, укриття, протокол гострої променевої реакції); модель активності ліків | Панель «Повітря і радіація», картки екіпажу, «Аптечка» |
| Ізоляція та замкнутий простір | Щоденна перевірка: сон і настрій із трендом за 7 днів і нагадуванням; низький настрій підвищує терміновість огляду | Колонка екіпажу, «Медкартка» |
| Віддаленість від Землі | Усі рішення на борту, без зв’язку; аптечка на всю місію; режим «Медик захворів»; навчальні тривоги | Усюди; «Сценарії демо»; вкладка «Тест» |
| Гравітаційні поля | Протоколи зміни зору (SANS), болю в спині, каменів у нирках (сценарій «Ниркова коліка») і ритму серця (сценарій «Аритмія») | «Огляд», «Сценарії демо» |
| Ворожі замкнені середовища | «Накопичення CO₂», вартовий «Розгерметизації», «Декомпресія після виходу» | «З чого почати», «Сценарії демо» |

### Архітектура

Схема — в англійській частині вище (розділ Architecture). Коротко: показники щосекунди → прапорці щодо особистої норми → тривога й вартовий; скарга звичайними словами → розбір мови → каталог → докази з вагами (скарги, датчики, обставини, відповіді, щоденна перевірка) → 12 протоколів, 3 червоні прапорці, загальний алгоритм → рішення, ліки, повторна перевірка → журнал і медкартка в браузері.

- **Класичний пояснюваний ШІ:** експертна система на правилах із механізмом зважування доказів. Відсоток «впевненості» — частка балів протоколу серед усіх варіантів, зменшена, коли доказів мало; це не калібрована ймовірність. Якщо два варіанти близькі, терміновість визначає небезпечніший.
- **Один файл:** HTML, CSS і JavaScript без бібліотек, без зовнішніх шрифтів і мережевих запитів. Дані зберігаються лише в localStorage браузера цього комп’ютера; «Очистити всі дані» в меню «Сценарії демо» їх видаляє.

### Перевірка (виміряно командою на фінальній збірці)

14 листопада 2026 року, фінальний `index.html` (1 441 067 байтів), headless Chrome, скрипт керує справжнім застосунком:

- скарги зі сценаріїв → правильний протокол: **10 з 10** (6 сценаріїв + 4 навчальні тривоги);
- вільні скарги за нормальних датчиків, 18 українською й 12 англійською → безпечне рішення: **30 з 30** (повний список — в англійській частині);
- «Накопичення CO₂»: тривога через 10 тактів симуляції (близько 9 с); «Надлишок CO₂ і нестача кисню», «Терміново», впевненість 75–83% залежно від того, коли почати огляд; повторна перевірка «стало краще» приблизно через 5 с після першого кроку;
- мережевих запитів: **0**; помилок у консолі й винятків: **0**; розмір: **1,44 МБ**.

Це інженерна, а не клінічна перевірка. Наступний крок — стандартизовані клінічні випадки з лікарями.

### Дані NASA та партнерів

- **NASA HRP «5 Hazards of Human Spaceflight»** — карта функцій продукту й позначки «NASA HRP: …» у застосунку.
- **NASA HRP «Risks of Human Spaceflight»** — вибір бортових протоколів (SANS, камені в нирках, декомпресійна хвороба, ритм серця, сон і поведінкове здоров’я, радіація).
- **NASA HRP «Ongoing HRP Research in Space»** — контекст: що вимірюють у польоті.
- **NASA-STD-3001 / OCHMO**: CO₂ не більше 3 мм рт. ст. у середньому за годину — прапорець «Увага» понад 3, «Тривога» понад 5, доказ +4 у рішенні; кожен зайвий 1 мм рт. ст. приблизно подвоює шанси головного болю (Law et al., 2014).
- **Curiosity RAD**: близько 1,8 мЗв на добу в польоті до Марса — фон 75 мкЗв/год, доза кожного, модель активності ліків.
- **NASA**: затримка сигналу 3–22 хв в один бік і близько 13 днів без зв’язку під час сонячного з’єднання — тому все працює на борту.
- **NASA Glenn**: на МКС показники знімають періодично — тому безперервний моніторинг і щоденна перевірка.
- **Чек-лист аптечки МКС (NASA)** — основа списку ліків; **Crew Active Dosimeter (NASA SRAG)** — майбутнє джерело дози.
- **CSA «Monitoring Radiation for Astronaut Health» (2026)**: нейтрони — близько 30% радіації на МКС, прилад CANS вимірюватиме їх безперервно й автономно.
- **CSA Bio-Monitor / Astroskin** — на нього змодельовано потік датчиків; **CSA «Why Do We Conduct Science Experiments in Space?»** — контекст.
- **ESA / DLR**: Double Sensor, експерименти Circadian Rhythms і Thermolab; «космічна лихоманка» (Stahn et al., 2017) — межі температури від особистої норми.

Посилання на всі джерела — в англійській частині.

### Чесно про обмеження

- Показники й дані екіпажу **симульовані**; даних реальних людей немає.
- Модель втрати активності ліків від радіації **умовна**; дослідження NASA ліків, що 550 днів зберігалися на МКС, незвичної деградації не виявило, тож строки придатності (за ними система теж стежить) важливіші.
- Протоколи спрощені й **не є медичною порадою**; це не медичний виріб. Межі щоденної перевірки — типові клінічні діапазони, а не сертифіковані для місії.
- Каталог проблем описує реальні симптоми, але це **не офіційний медичний довідник**.
- Частота використання ліків і запаси — наші припущення; справжня система брала б їх із моделі NASA Integrated Medical Model.
- Журнал зберігається лише впродовж сеансу.

### Що далі

1. Справжні датчики через Web Bluetooth (нагрудні пульсометри), потім натільний датчик класу Astroskin.
2. Пульс із камери планшета (rPPG).
3. Невелика мовна модель на бортовому комп’ютері для розмови, теж офлайн; червоні прапорці й межі лишаються правилами.
4. Клінічна перевірка протоколів із лікарями й польові випробування на полярній станції чи судні.
5. На Землі: полярні станції, судна в морі й віддалені амбулаторії мають ту саму проблему — допомога далеко.

### Ліцензія та інструменти

- Код і вміст: **MIT**, © 2026 vod0laz1 (файл `LICENSE`).
- Сторонніх бібліотек, шрифтів, зображень і музики немає; іконки й графіка — вбудований SVG, зроблений для проєкту; відео — запис екрана застосунку із субтитрами.
- Джерела NASA, CSA, ESA та інші процитовано й не поширюються; логотипів NASA чи інших агенцій немає.
- Інструменти: HTML, CSS і JavaScript без бібліотек; headless Chrome і ffmpeg для відео; ШІ-асистент (Claude від Anthropic) для коду, перекладу каталогу й медіа під керівництвом команди.

**Команда vod0laz1:** Максим, Матвій, Дмитро, Станіслав, Денис.
