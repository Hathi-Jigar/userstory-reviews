# Mobile App Shortcuts Long Press

**Module / Area:** Mobile App â Global / Cross-Module

**Type:** Feature

**Interactive Prototype:**
- View Live Screen â *Not Available*
- View Source Code â *Not Available*

---

## ð Brief Description

When a user long-presses the digiQC app icon on their Android or iOS device, a quick-action menu appears with five shortcuts. Each shortcut takes the user directly into a specific screen or action inside the app â skipping the home screen and any intermediate navigation. This saves time for field engineers and site teams who need to start an inspection, raise an instruction, or check their to-do items quickly while on-site.

---

## ð¯ Jobs to Be Done (JTD)

| Role | Whenâ¦ | They want toâ¦ | So they canâ¦ |
|------|--------|---------------|--------------|
| Site Engineer / QC Inspector | On-site, about to start a new inspection | Jump straight to the new inspection form without navigating through the app | Save time and start capturing data faster |
| Site Engineer / QC Inspector | On-site, spotting a quality issue | Open the raise instruction flow immediately | Record and assign the issue before moving to the next location |
| Site Engineer / QC Inspector | Arriving at site, checking what's pending for the day | Open their inspection or instruction to-do list in one tap | Know exactly what to do without searching or scrolling |
| Project Manager / QC Head | On the go, needing to check pending field activity | Open to-do lists directly | Review pending items without launching and navigating the app manually |

---

## ð¡ How Might We (HMW)

- How might we reduce the number of taps required for the most frequent field actions?
- How might we make the app feel faster and more suited for on-site use, where time and attention are limited?
- How might we support users who already know what they need to do, so the app gets out of their way?
- How might we ensure shortcuts always land the user in the right state â not a broken or empty screen â even if they are not logged in or lack permission?
- How might we make the shortcut list feel like it was designed for field engineers, not just added as a technical feature?

---

## ð¤ User Persona

| Role | Context of Use | Goal | Frustration | Success |
|------|----------------|------|-------------|---------|
| Site Engineer / QC Inspector | On-site, mobile, often in bright sunlight, limited time | Start or check work instantly without navigating menus | Wastes time tapping through home screens and menus before reaching the right screen | Long-presses, taps a shortcut, and lands on the right screen in under 3 seconds |
| Project Manager / QC Head | On the move, checking pending items between meetings | See what is open and pending without logging into the app step by step | Has to navigate through multiple tabs to reach the to-do lists | Long-presses, taps Inspection To Do or Instruction To Do, and sees open items immediately |

---

## ð User Story

> As a **Site Engineer / QC Inspector**, I want to long-press the digiQC app icon and see quick shortcuts, so that I can jump directly to my most-used actions without navigating through the app every time.

> As a **Project Manager / QC Head**, I want to reach my inspection and instruction to-do lists from the home screen in one step, so that I can check what is pending quickly while on the move.

---

## â Acceptance Criteria

### Shortcut Availability

- [ ] When any user long-presses the digiQC app icon on Android or iOS, a shortcut menu appears with exactly 5 options â regardless of whether they are logged in or not
- [ ] The shortcuts are displayed in this order:
  1. Start New Inspection
  2. Raise New Instruction
  3. Fill New Register
  4. Inspection To Do
  5. Instruction To Do
- [ ] Each shortcut shows a label and a recognisable icon
- [ ] The shortcut menu follows the native OS behaviour â it does not open the full app first
- [ ] Shortcuts are always visible on the OS home screen â the app does not hide or remove them based on login state

---

### Shortcut 1 â Start New Inspection

- [ ] Tapping "Start New Inspection" opens the digiQC app and takes the user directly to the Inspection screen with the **Add / New Inspection form already open** â same state as tapping the "+" button on the Inspection list screen
- [ ] The user can immediately begin filling in the inspection form without any extra tap
- [ ] If the user is not logged in, they are taken to the login screen immediately upon tapping the shortcut; after successful login, the app redirects them directly to the new inspection form â not the home screen

---

### Shortcut 2 â Raise New Instruction

- [ ] Tapping "Raise New Instruction" opens the digiQC app and takes the user directly to the Instruction screen with the **Add / New Instruction form already open** â same state as tapping the "+" button on the Instruction list screen
- [ ] The user can immediately begin filling in the instruction form without any extra tap
- [ ] If the user is not logged in, they are taken to the login screen immediately upon tapping the shortcut; after successful login, the app redirects them directly to the new instruction form â not the home screen

---

### Shortcut 3 â Fill New Register

- [ ] Tapping "Fill New Register" opens **app.digiqc.com** in the device's default web browser
- [ ] The browser navigates to the user's first project and lands on the **Register tab**
- [ ] "First project" is defined as the first project in the user's project list, ordered the same way as shown in the app
- [ ] If the user is not logged in to the web app, they are taken to the web login screen; after successful login, the browser redirects them to the Register tab of their first project â not the default dashboard
- [ ] If the user has no projects assigned, the browser opens app.digiqc.com and shows the default empty project state with a message guiding the user

---

### Shortcut 4 â Inspection To Do

- [ ] Tapping "Inspection To Do" opens the digiQC app and takes the user directly to the **Inspection module**, with the **To Do tab pre-selected and active**
- [ ] The list loads and shows all inspections assigned to or pending for the logged-in user
- [ ] If the user is not logged in, they are taken to the login screen immediately upon tapping the shortcut; after successful login, the app redirects them directly to the Inspection To Do tab â not the home screen

---

### Shortcut 5 â Instruction To Do

- [ ] Tapping "Instruction To Do" opens the digiQC app and takes the user directly to the **Instruction module**, with the **To Do tab pre-selected and active**
- [ ] The list loads and shows all instructions assigned to or pending for the logged-in user
- [ ] If the user is not logged in, they are taken to the login screen immediately upon tapping the shortcut; after successful login, the app redirects them directly to the Instruction To Do tab â not the home screen

---

### Role & Permission Behaviour

- [ ] Shortcuts are visible and accessible to all users â both logged in and logged out â from the OS home screen
- [ ] A logged-out user who taps any shortcut is taken to the login screen; the intended shortcut destination is remembered and the user is redirected there immediately after successful login
- [ ] The app must not drop the shortcut intent after login â the user must always land on the shortcut target, not the home screen
- [ ] Once logged in, shortcuts work for all roles without restriction
- [ ] If a user's role does not have permission to raise an instruction or start an inspection, they land on the respective screen and see the same restricted state they would normally see inside the app â no special shortcut error
- [ ] Shortcuts do not bypass any existing role or permission restrictions in the app

---

### States & Validations

- [ ] If the app is already open in the background, tapping a shortcut navigates within the running app â it does not open a second instance
- [ ] If the app is force-closed or not running, the shortcut launches the app and navigates to the correct destination
- [ ] If the app is updating or unavailable, the OS handles this gracefully â the shortcut behaves the same as tapping the app icon directly
- [ ] No shortcut should open to a blank or crashed screen â if navigation fails, the user lands on the home screen with no error loop

---

### Platform Behaviour

- [ ] On **Android**, shortcuts are implemented using the Android App Shortcuts API (static shortcuts)
- [ ] On **iOS**, shortcuts are implemented using UIApplicationShortcutItem (Home Screen Quick Actions)
- [ ] Shortcut labels must not exceed the character limits set by each OS (Android: ~25 chars, iOS: ~20 chars per line)
- [ ] Shortcut icons must use simple, clear glyphs that are visible at small sizes and match the digiQC icon style

---

### Flow Continuity â What Happens Next

- [ ] After completing the action launched by the shortcut (e.g., submitting a new inspection), the user is returned to the normal in-app flow â no forced app restart or loop back to the shortcut menu
- [ ] The back button / navigation behaves exactly as it would if the user had navigated to the screen normally from inside the app

---

## â ï¸ Edge Cases & Constraints

**Positive Cases**
- [ ] A logged-in user with full permissions taps any shortcut â they land on the exact target screen within 2â3 seconds
- [ ] A user who has the app open in the background taps a shortcut â they are taken to the target screen without restarting the app

**Negative Cases**
- [ ] A logged-out user taps any shortcut â they see the login screen and after successful login are redirected to the exact shortcut destination, not the home screen
- [ ] A user with read-only permissions taps "Start New Inspection" or "Raise New Instruction" â they land on the respective screen but the "+" button is hidden or disabled, matching normal app behaviour

**Edge Cases**
- [ ] User has no projects assigned â "Fill New Register" shortcut opens app.digiqc.com and shows the empty project state gracefully â no crash or broken redirect
- [ ] User taps a shortcut while the app is mid-update or loading â shortcut behaves like a normal app open, takes the user to the home screen if the deep link cannot resolve
- [ ] User's session has expired â treated the same as logged-out; they see the login screen, and after re-authentication are redirected to the shortcut destination â not the home screen
- [ ] User switches to a different account after using shortcuts â shortcuts still work and navigate based on the currently logged-in account
- [ ] Device OS does not support app shortcuts (very old Android/iOS versions) â shortcut menu simply does not appear; the app continues to function normally with no impact

**How to Test**
- Test each shortcut on both Android and iOS â confirm the landing screen and state is exactly correct (e.g., new form open, correct tab selected)
- Test while logged out â confirm each shortcut takes the user to the login screen, and after login they land on the correct shortcut destination (not the home screen)
- Test with a user who has no projects â confirm "Fill New Register" does not crash
- Test with a restricted role â confirm shortcuts land correctly but permissions are respected within the screen
- Test with the app running in the background â confirm navigation happens within the existing app instance
- Test on both older and latest OS versions to confirm shortcut menu appears and functions correctly

---

## ð¨ Design Prompt

```
Screen: App Shortcuts â Long Press Quick Action Menu (OS-native)
Platform: Mobile â Android and iOS
Audience: Site Engineer, QC Inspector, Project Manager â field use
Style: Native OS shortcut menu. No custom UI needed â follows OS visual style.
       Icons must be simple, single-colour glyphs, matching digiQC icon language.

Shortcuts to show (in this order):
1. Start New Inspection â icon: clipboard with a "+" mark
2. Raise New Instruction â icon: alert or exclamation with a "+" mark
3. Fill New Register â icon: table grid or form sheet
4. Inspection To Do â icon: clipboard with a checkmark or clock
5. Instruction To Do â icon: list with a clock or pending indicator

States to show in prototype:
- Android: Long-press popup appearing above the app icon with 5 shortcut rows â native Material You style, dark overlay background
- iOS: Long-press context menu appearing above the app icon with 5 shortcut rows â native iOS style with rounded card and blur background

Icons:
- Each shortcut row shows: [icon] [label]
- Icons must be simple and recognisable at ~20px size
- Use digiQC brand colour (#FC5027) as icon tint where the OS allows custom icon colours

No modals or additional screens needed for the shortcut menu itself.
All landing screens (inspection form, instruction form, to-do tabs, web browser) are existing screens â no new screen design needed for those.

Notes:
- The prototype should demonstrate the long-press gesture and the shortcut menu appearance on both platforms
- Show the Android version and iOS version side by side for design review
```

---

## ð£ Release Note Details

**Overview**
digiQC now supports App Shortcuts on Android and iOS. Long-pressing the digiQC app icon gives you five quick actions â so you can jump straight to your most-used screens without opening the app and navigating manually.

**Who Benefits & How**
- **Site Engineers / QC Inspectors:** Start inspections and raise instructions from the home screen in one tap â saves time on-site
- **Project Managers / QC Heads:** Check pending inspections and instructions directly without navigating through the app

**What's New**
Five shortcuts available on long press:
1. **Start New Inspection** â Opens the new inspection form directly
2. **Raise New Instruction** â Opens the new instruction form directly
3. **Fill New Register** â Opens the Register tab in your first project on the digiQC web app
4. **Inspection To Do** â Takes you straight to your inspection pending list
5. **Instruction To Do** â Takes you straight to your instruction pending list

**How It Works**
Long-press the digiQC app icon on your Android or iOS home screen. A quick-action menu appears with five shortcuts. Tap any shortcut and you land directly on that screen â no extra navigation needed. If you are not logged in, you will be taken to the login screen first and redirected to the right place after sign-in.
