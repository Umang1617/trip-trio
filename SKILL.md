---
name: trip-trio
description: A quick travel planner that directly checks flight prices on Skyscanner India, finds top 3 budget hotels on Booking.com, and lists top 5 places to visit. Use this skill whenever the user asks about travel, trip planning, visiting a city or country, finding flights, hotels, or tourist spots. Trigger on phrases like "plan a trip", "I want to visit", "find flights to", "hotels in", "things to do in", or any travel-related request.
argument-hint: "[destination city or country]"
author: "Umang Srivastava & Ayush"
version: 5
---

# Trip Trio

A compact travel planner that checks live websites directly:
- ✈️ Cheapest flights checked on Skyscanner India
- 🏨 Top 3 budget hotels checked on Booking.com
- 📍 Top 5 places to visit

## Steps

### Step 1 — Identify the Destination
- Extract the destination from the user's request: **$ARGUMENTS**
- If no destination is provided, ask the user: "Where would you like to travel?"
- Ask for departure city if not mentioned.
- Ask for travel date or month if not provided.

### Step 2 — Find Cheapest Flights (Check Skyscanner India directly)
- Open **Skyscanner India** at https://www.skyscanner.co.in/
- Enter the departure city, destination, and travel date → fetch results.
- Check the fare calendar for the **best/cheapest dates to fly**.
- Show the cheapest 5 flight options sorted by price.
- If no direct flights found, show the cheapest connecting options.

### Step 3 — Top 3 Budget Hotels (Check websites directly)
- Open and search for hotels at the destination on Booking.com:
  1. **Booking.com** — Go to https://www.booking.com/ → enter destination and dates → filter by price (low to high) and guest rating
- Load `references/hotel-criteria.md` for selection and rating guidelines.
- Pick the **top 3 best value budget hotels** from the Booking.com results.

### Step 4 — Top 5 Places to Visit
- Research the top 5 must-visit attractions at the destination.
- Keep each entry to one line.

### Step 5 — Format and Deliver the Response
Load `references/output-template.md` now.
Follow the template exactly. The response must contain:

1. **Flights Table** — Cheapest flights from Skyscanner India with airline, times, duration, and price in INR. Include the best dates to fly based on the fare calendar.
2. **Top 3 Budget Hotels** — Each hotel with rating, number of reviews, location, price per night, key highlights, a one-line guest summary, and the site it was found on (Booking.com).
3. **Top 5 Places to Visit** — One line per attraction.
4. **Trip Comparison Table** — A markdown table comparing Budget, Mid-Range, and Splurge trip options across Flight Cost, Hotel per Night, Estimated Total (3 nights), and Best For.
5. **Quick Travel Summary** — Best time to visit, must-try local food, and one practical local tip.
6. **Source Confidence** — One line stating whether prices are from live site data (checked today), recently cached (within 7 days), or estimated — with a note explaining why if data was unavailable.

## Edge Cases
- If a website fails to load, skip it, note the issue, and continue with the remaining site.
- If destination is ambiguous (e.g. "Paris" — France or Texas?), ask the user to clarify.
- If the user has no travel date, suggest the cheapest season to visit and use that for searching.
- If the destination is remote, suggest the nearest major airport and onward travel options.
- If the user only wants one section (flights only, hotels only, etc.), focus on that and skip the rest.
