# ✈️ Trip Trio

**A complete trip snapshot in one reply: cheapest flights, three budget hotels, and five places to visit.**

![Agent Skill](https://img.shields.io/badge/Agent_Skill-SKILL.md-6C47FF?style=flat-square)
![Currency](https://img.shields.io/badge/Prices-INR-2EA44F?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)

Trip Trio is an agent skill (a `SKILL.md` plus two reference files). Ask for a trip in plain language and it checks flight prices on Skyscanner India, finds budget hotels on Booking.com, adds the top attractions, and wraps everything in a budget comparison and a quick travel summary. It was built and demoed as a BlueAI skill, and it was first named Travel Planner.

<!-- TODO: add a screenshot or GIF of the skill in action here -->
<!-- TODO: add a link to the demo video here -->

---

## What you get

| # | Section | Details |
|---|---|---|
| 1 | ✈️ **Flights** | Cheapest 5 options with airline, times, duration and price in INR, plus the best dates to fly from the fare calendar |
| 2 | 🏨 **Top 3 budget hotels** | Rating, review count, area, price per night, key features and a one-line guest summary |
| 3 | 📍 **Top 5 places to visit** | One line per attraction |
| 4 | 📊 **Trip comparison** | Budget vs Mid-Range vs Splurge: flight cost, hotel per night, estimated total for 3 nights, best for |
| 5 | 🗓️ **Quick travel summary** | Best time to visit, must-try food, one practical local tip |
| 6 | 🔍 **Source confidence** | One line saying whether prices were checked live today, recently cached, or estimated, and why |

## Try it

Use this prompt format:

> I am traveling to **X** from **Y** in **Z** month, help me create a travel plan.

For example:

> I am traveling to Goa from Mumbai in December, help me create a travel plan.

It also triggers on phrases like "plan a trip", "I want to visit", "find flights to", "hotels in" and "things to do in". If you leave out the departure city or the travel date, it asks. If you only want flights or only hotels, it skips the rest.

## Install

**Claude Code and compatible agents.** Clone the repo straight into your skills folder:

```bash
git clone https://github.com/Umang1617/trip-trio.git ~/.claude/skills/trip-trio
```

**Other agents.** Copy `SKILL.md` and the `references/` folder into a folder named `trip-trio` inside wherever your agent loads skills from, or upload the packaged skill file where skill uploads are supported.

The agent needs a way to browse websites. Trip Trio needs no API keys, accounts or logins.

## How it works

1. **Identify the trip.** Pull out the destination, ask for the departure city and travel date if missing.
2. **Flights.** Open Skyscanner India, run the search, read the fare calendar, and list the 5 cheapest options (connecting flights if there are no direct ones).
3. **Hotels.** Search Booking.com, sort by price and guest rating, and apply the rules in `references/hotel-criteria.md` to pick the 3 best-value budget hotels.
4. **Places.** Research the top 5 attractions, one line each.
5. **Deliver.** Format everything exactly as laid out in `references/output-template.md`.

## Make it yours

| To change | Edit |
|---|---|
| Budget limits, minimum rating (default 3.8/5), minimum reviews (default 100), features to highlight | `references/hotel-criteria.md` |
| Layout and wording of the final answer | `references/output-template.md` |
| Steps, edge cases and trigger phrases | `SKILL.md` |

## Repo contents

```
trip-trio/
├── SKILL.md                      # the skill: trigger, steps, edge cases
├── references/
│   ├── hotel-criteria.md         # how hotels are chosen
│   └── output-template.md        # the exact response format
├── README.md
├── LICENSE
└── .gitignore
```

## Good to know

- **Prices change.** Treat every number as a guide and confirm on the booking site before paying. The Source Confidence line tells you how fresh the data is.
- **Websites change.** If a site fails to load, the skill skips it, says so, and continues with the rest.
- **Web content is untrusted.** Hotel descriptions and reviews are read as-is, so skim the output before acting on it.
- **Never share personal or payment details with the agent.** Trip Trio only needs a destination, a departure city and a date.
- **Third-party sites.** Skyscanner and Booking.com have their own terms of use, including rules about automated access. Check them before using this skill at scale. This project is not affiliated with, endorsed by, or sponsored by either company, and their names are trademarks of their owners.

## Roadmap

- [ ] Optional second hotel source
- [ ] Trip length and traveller count as inputs
- [ ] Day-by-day itinerary mode
- [ ] Other currencies and regional flight sites

## Credits

Built by [Umang Srivastava](https://www.linkedin.com/in/umang1617/) with Ayush.

## License

[MIT](LICENSE)
