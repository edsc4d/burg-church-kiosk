# Staff Guide · Life Groups Kiosk

You never need to open or edit the kiosk file. Everything you'll change lives in the Google Sheet.

## Update a group

1. Open the Life Groups Google Sheet.
2. Find the group's row and change what you need.
3. That's it. The kiosk checks the sheet every 15 minutes.

Want it to update right now? Tap the **top-right corner of the screen 5 times** to open the admin panel, then tap **Reload data now**.

## Add a group

Add a new row to the sheet. Only `category` and `name` are required; everything else is optional. Leave a cell blank and that section just won't show on the kiosk.

## Hide a group without deleting it

Type `no` in the `show` column. Clear it to bring the group back.

## What each column does

| Column | What to put in it | Example |
| --- | --- | --- |
| `category` | `study`, `support`, or `social` (picks the tab) | `study` |
| `name` | Group name | `Aged to Perfection` |
| `subtitle` | Short line under the name | `55+ Life Group` |
| `schedule` | When it meets | `Thursdays · 11am–1pm` |
| `leaders` | Leader first names | `Bill & Mike` |
| `location` | Where it meets | `Home group · Concord, NC` |
| `about` | A few sentences about the group | |
| `contact` | Email for questions | `mike@theburg.church` |
| `signup_url` | Church Center sign-up link (becomes the QR code) | |
| `photo` | A photo link, or `none` for no photo. Leave blank to use the built-in photo. | |
| `emoji` | Icon shown when there's no photo | `📖` |
| `color` | Accent color as a hex code. Leave blank for automatic. | `#CD5B30` |
| `show` | `no` hides the group | |

A new category (for example `serve`) automatically gets its own tab at the end.

## Admin panel

Tap the top-right corner 5 times. From there you can:

- **Reload data now.** Pulls the latest from the sheet. It also shows whether the kiosk is using the live sheet, a saved copy, or the built-in backup list.
- **Starting tab.** Which tab the kiosk opens to.
- **Auto-reset timer.** How long before it returns to the start screen: 30 seconds, 1 minute, or 2 minutes.

Tap outside the panel or **Close panel** to go back.

## If something looks wrong

- **Changes aren't showing.** Wait 15 minutes or use **Reload data now**. Check that the row's `category` is spelled `study`, `support`, or `social`.
- **The admin panel says "saved copy."** The kiosk couldn't reach the internet. It keeps showing the last data it loaded, so nothing breaks. Check the Wi-Fi.
- **The admin panel says "built-in backup list."** The sheet link isn't set up, or the kiosk has never reached it. Contact Elijah.
- **A QR code goes to the wrong page.** Fix the `signup_url` in that group's row.
