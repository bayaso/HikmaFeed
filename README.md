[README.md](https://github.com/user-attachments/files/34931081/README.md)
# Hikmah: your iPhone app

A swipe feed of ideas from psychology, self-growth and Islamic books. It works offline, sends a daily notification with one idea, has a page for every book, and downloads new books automatically.

**What's in this folder**

| Item | What it is |
|---|---|
| `Hikmah.swiftpm` | The app. You open this in Xcode on your Mac. |
| `content.json` | All the books and ideas. You upload this to GitHub so the app can update itself. |
| `README.md` | This guide. |

---

## Part 1: Install the app on your iPhone (about 30 minutes the first time)

### 1. Get Xcode on your Mac
1. Open the **App Store** on your Mac, search for **Xcode**, and install it. It's free but large (around 10 GB).
2. Open Xcode once. Accept the license, and when it asks which platforms to install, tick **iOS**.
3. Go to **Xcode → Settings → Accounts**. Click **+**, choose **Apple ID**, and sign in with your normal Apple ID.

### 2. Prepare your iPhone
1. Connect your iPhone to the Mac with a cable. On the iPhone, tap **Trust** and enter your passcode.
2. On the iPhone, open **Settings → Privacy & Security → Developer Mode**, turn it **on**, and restart when asked. After the restart, confirm by tapping **Turn On**.
   - If you don't see Developer Mode, do step 3 first (open the project in Xcode with the phone plugged in). Then the option will show up.

### 3. Open the app in Xcode
1. In Xcode, choose **File → Open…** and select the **`Hikmah.swiftpm`** folder. Select the whole folder, not a file inside it.
2. Wait until the loading bar at the top finishes.
3. In the left sidebar, click **Hikmah** at the top. Then click the **Hikmah** target and open the **Signing & Capabilities** tab.
4. Under **Team**, choose **Your Name (Personal Team)**.
   - If you see an error about the bundle identifier, change `com.hikmahfeed.personal` to something unique, such as `com.yourname.hikmah`.

### 4. Run it on your phone
1. At the top of the Xcode window, click the device menu and choose **your iPhone**.
2. Press the **▶ Run** button (or ⌘R). The first build takes a minute or two.
3. On the iPhone, the first time you open the app you may see **"Untrusted Developer"**. To fix it, go to **Settings → General → VPN & Device Management**, tap your Apple ID, and tap **Trust**.

The app is now on your home screen. ✅

### ⚠️ The 7-day rule (important)
With a **free** Apple ID, Apple makes self-installed apps stop opening after **7 days**. To renew it, plug the phone in and press **▶ Run** again. Your saved cards and settings stay.

Ways to make this easier:
- **Run over Wi-Fi:** in Xcode, open **Window → Devices and Simulators**, select your iPhone, and tick **Connect via network**. After that you can press Run without a cable while both devices are on the same Wi-Fi.
- **Apple Developer Program ($99/year):** with this, the app lasts a full year. You can also send it to friends through TestFlight. It's only worth it if you get serious about the app.

---

## Part 2: Turn on automatic updates (one-time, about 10 minutes)

The app already contains 49 ideas from 20 books. To get new books without reinstalling, the app reads `content.json` from GitHub.

1. Create a free account at **github.com**.
2. Click **+ → New repository**. Name it `hikmah-content`, set it to **Public**, and click **Create repository**.
3. Click **uploading an existing file**, drag in **`content.json`**, then click **Commit changes**.
4. Click `content.json` in your repository, then click the **Raw** button. Copy the address from the browser. It looks like this:
   `https://raw.githubusercontent.com/YOURNAME/hikmah-content/main/content.json`
5. In the app, tap **⚙︎ Settings**, paste the link into **New books & ideas**, and tap **Check for new ideas**.

From then on, the app checks for updates every time you open it. It also keeps everything on the phone, so it still works without internet.

### Adding new books later
1. Ask Claude something like: *"Add 8 cards from Ibn al-Qayyim's al-Fawa'id and 5 from The Power of Habit to my Hikmah content.json."* Attach your current `content.json`.
2. Claude gives you a new `content.json` with a **higher `version` number**. This matters, because the app only updates when the version goes up.
3. On GitHub, open `content.json`, click the ✏️ / **Upload** button, replace the file, and commit.
4. The next time you open the app, it shows a message like **"8 new ideas added"**.

---

## How the content file works

```json
{
  "version": 2,
  "categories": [
    { "id": "biz", "label": "Business", "light": "#6A3D9A", "dark": "#B89AE6" }
  ],
  "books": [
    { "id": "atomic", "title": "Atomic Habits", "author": "James Clear", "c": "grow", "about": "Short description…" }
  ],
  "cards": [
    { "id": "g1", "c": "grow", "book": "atomic",
      "t": "Title", "a": "Arabic text (optional)", "b": "The idea / meaning",
      "steps": ["Step one", "Step two"],
      "x": "Try this action", "s": "Source line shown on the card" }
  ]
}
```
- `c` is the category id. Categories are defined in `categories`, so you can add a new one (with its own colour) without touching Xcode.
- `steps` is optional. When present, the card shows a numbered list.
- Every card `id` must be unique. Don't reuse old ids, or saved cards will get mixed up.
- `book` must match a book's `id`. You can leave it out for a card that isn't from a specific book.

---

## Using the app
- **Swipe up** to see the next idea. The first card is always **Today's idea**.
- **Double-tap** a card, or tap the bookmark, to save it. Saved cards appear under **Saved**.
- **Tap the source line** on a card to open that book's page and see all its ideas.
- **📚 button** (top right): the library of all books.
- **⚙︎ button**: daily reminder time and content updates.

## If something goes wrong
- **"No such module 'AppleProductTypes'"**: you opened `Package.swift` instead of the `Hikmah.swiftpm` folder, or your Xcode is older than version 15. Update Xcode and reopen the folder.
- **Error on the line `.placeholder(icon: .moon)`**: change `.moon` to `.leaf` in `Package.swift`.
- **Any red error in a Swift file**: take a screenshot or copy the error text and send it to Claude. It's usually a one-line fix.
- **Plan B:** in Xcode, choose **File → New → Project → iOS App**. Name it Hikmah, set Interface to SwiftUI, and set the minimum iOS version to 17. Delete the `ContentView.swift` and `HikmahApp.swift` files it creates. Then drag every `.swift` file from `Hikmah.swiftpm` into the project, except `Package.swift`.

> Hadith references come from Bukhari, Muslim, Tirmidhi, an-Nawawi and al-Hakim, with gradings noted. Before you share any of them publicly, double-check them on sunnah.com.
