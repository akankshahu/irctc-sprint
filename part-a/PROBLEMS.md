# IRCTC Problem Discovery — Part A

## Summary
- Total problems documented: 6
- Given problems: 3
- Self-discovered problems: 3
- Platform explored: IRCTC live website at irctc.co.in
- Devices used: Desktop Chrome on Linux; homepage service pages and linked utility pages reviewed in-browser
- Date of exploration: June 8, 2026

---

## Problem 1: Tatkal Booking Crashes at 10:00 AM [Given]

**What is broken:**
Tatkal booking becomes unreliable exactly when demand spikes at 10:00 AM. The booking flow freezes, throws server errors, or drops the session before payment completes, so users lose their place despite arriving on time and completing earlier steps.

**Affected users:**
Anyone trying to book Tatkal tickets during the 9:58–10:05 AM window, especially urgent travellers, commuters, and users in Tier 2/3 cities who depend on train travel and cannot switch to alternate transport easily.

**Frequency:**
Daily, every morning at Tatkal opening time. The issue is condition-based but recurring, and the failure rate rises sharply during the highest-traffic seconds around 10:00 AM.

**Current flow — step by step:**
1. User opens IRCTC at 9:50 AM and logs in.
2. User searches for a route and selects a train.
3. User switches to Tatkal quota.
4. User fills passenger details and prepares to book.
5. User clicks “Book Now” at 9:59:45.
6. At 10:00:00 the page freezes and the spinner shows no useful progress.
7. After a delay, the system returns an error, times out, or resets the CAPTCHA/session.
8. User refreshes and finds Tatkal availability gone or waitlisted.

**Where exactly it breaks:**
Steps 5–7. The system cannot absorb the peak request surge cleanly, and the user gets no queue position, no progress indicator, and no reliable confirmation of whether the booking request was accepted.

---

## Problem 2: Search Filters Do Not Work Reliably [Given]

**What is broken:**
The train search filters do not consistently match the results shown. A user can select class, quota, or availability filters and still see trains that do not obey those settings, or the filters reset after navigation.

**Affected users:**
Every user who searches trains on IRCTC, with higher impact for senior citizens, first-time users, and travellers who rely on filters to narrow down usable options quickly.

**Frequency:**
Intermittent but frequent under real usage. The issue shows up more during high-traffic periods and when users move back and forth between results and train details.

**Current flow — step by step:**
1. User enters source, destination, and journey date.
2. User clicks Search Trains and gets a long result list.
3. User applies filters such as Sleeper Class and Available seats only.
4. Results refresh, but some trains still violate the selected filter.
5. User opens a train and sees a different availability state than expected.
6. User goes back and notices the filter state has reset or partially cleared.
7. User stops trusting the filters and manually scans the full list.

**Where exactly it breaks:**
Steps 3–6. Filter state and live availability are not consistently synchronized, so the interface looks authoritative while showing stale or mismatched results.

---

## Problem 3: Seat Selection Resets Randomly [Given]

**What is broken:**
The chosen berth or seat is not preserved reliably between the seat map and the next booking step. Users select a berth, proceed, and then find that the seat preference has changed or reverted to Auto.

**Affected users:**
Families booking lower berths, elderly passengers, users with mobility needs, and anyone who cares about a specific berth assignment. The issue is more painful on mobile because state resets happen more often there.

**Frequency:**
Intermittent, but significant. It typically appears in seat-map sessions and is reported more often on mobile than desktop.

**Current flow — step by step:**
1. User selects a train, class, and quota.
2. The seat map loads and displays available and booked berths.
3. User clicks a preferred berth, such as a lower berth for an elderly passenger.
4. The berth shows as selected in the map.
5. User clicks Proceed to reach passenger details.
6. The passenger form shows Auto or a different berth number.
7. User goes back to reselect the berth, but the original seat may now be unavailable.
8. User continues with the wrong seat or gives up and accepts Auto.

**Where exactly it breaks:**
Steps 4–6. The selected seat is not passed cleanly between components or survives a re-render poorly, so the user’s explicit preference is lost at the transition point.

---

## Problem 4: PNR Status and Reservation Chart Break the Main Flow

**How I found it:**
From the IRCTC homepage header, where the PNR Status and Reservation Chart links are placed near the main booking controls.

**Screenshot or description:**
The homepage shows a PNR Status link that opens a separate window and a Reservation Chart link that opens a different tab/site. This is visible alongside the primary BOOK TICKET area and the home page booking form.

**What is broken:**
Core post-booking tasks are not integrated into one flow. PNR lookup and reservation chart access jump to separate legacy pages on other domains, which creates a context switch at the exact moment a user needs fast, trusted information.

**Affected users:**
Booked passengers checking journey status, family members monitoring travel, station-side users confirming chart details, and support staff helping others find train status.

**Frequency:**
Every time a user checks PNR status or opens the reservation chart. This is a common post-booking activity, so the friction repeats for a large share of booked travellers.

**Current flow — step by step:**
1. User lands on the IRCTC homepage.
2. User clicks PNR Status from the header.
3. The system opens a separate legacy PNR enquiry page on a different domain.
4. The user sees a different layout and must re-enter the PNR.
5. The user checks the result and then returns to IRCTC.
6. User clicks Reservation Chart from the homepage.
7. A new tab opens with another separate service.
8. The user now has to manage multiple windows and different site styles to complete one journey-related task.

**Where exactly it breaks:**
Steps 2–4 and 6–8. The break is the handoff to separate services, which destroys continuity, introduces extra navigation work, and makes the experience feel fragmented instead of unified.

---

## Problem 5: The Homepage Buries the Primary Booking Task

**How I found it:**
By reviewing the live IRCTC homepage booking area and the surrounding service modules, promotions, and floating help entry points.

**Screenshot or description:**
The top of the homepage mixes the BOOK TICKET controls with service links, promotional holiday content, social links, AskDISHA chat, and multiple secondary destinations. The booking form itself is compact and visually crowded.

**What is broken:**
The homepage does not create a clear visual hierarchy for the core task. The primary booking flow competes with many other modules, so users have to work harder to locate the relevant fields and understand what to do first.

**Affected users:**
First-time users, older users, low-literacy users, and mobile users who need a simpler, more obvious route into ticket booking.

**Frequency:**
Every homepage visit. This is a persistent structural issue, not a rare edge case, so it affects a very large share of traffic.

**Current flow — step by step:**
1. User opens irctc.co.in.
2. The homepage shows multiple competing service categories and promotional blocks before the booking task becomes obvious.
3. User locates the booking form and starts identifying From, To, date, class, and quota.
4. The form combines several controls in a tight layout, making it easy to misread or skip fields.
5. The user must also ignore chat, social, holiday, and service-entry distractions.
6. The user finally clicks Search Trains after visually parsing the clutter.

**Where exactly it breaks:**
Steps 1–4. The problem is not a single broken control; it is the lack of clear hierarchy. The user spends cognitive effort just finding the actual booking path.

---

## Problem 6: The Site Signals Narrow Browser Compatibility

**How I found it:**
By opening the “Compatible Browsers” page linked from the IRCTC footer.

**Screenshot or description:**
The compatibility page lists specific minimum versions: Firefox 46+, Chrome 45+, Edge 13+, and Safari 10+. That page is presented as a support boundary for the IRCTC site rather than a soft recommendation.

**What is broken:**
IRCTC exposes a legacy compatibility model that pushes browser risk onto the user. Instead of behaving like a modern web app that gracefully adapts, it tells users that only a narrow set of browsers is supported, which can create access failures or inconsistent rendering on older devices and managed environments.

**Affected users:**
People on older laptops, cybercafe systems, enterprise-managed browsers, low-end devices, and users who do not know which browser version they are on.

**Frequency:**
Whenever someone lands on IRCTC from an unsupported or partially supported browser. The issue is conditional, but the condition is common enough to matter because the platform serves a mass public audience.

**Current flow — step by step:**
1. User opens IRCTC from a browser outside the listed support range or on a constrained device.
2. The user reaches the site without any strong compatibility guardrail in the main flow.
3. The user starts booking, searching, or logging in.
4. Some layout or behavior inconsistency appears, or the user is forced to check compatibility separately.
5. The user opens the compatibility information page.
6. The user must troubleshoot browser choice instead of completing the intended task.

**Where exactly it breaks:**
Steps 1–3. The failure begins at entry, because the platform communicates support constraints too late and relies on the user to self-diagnose environment issues.
