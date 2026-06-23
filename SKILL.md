---
name: find-cheap-flights
description: Find and compare the cheapest live flight options across travel booking sites and airline sites. Use when the user asks to search for cheap airfare, flexible-date flights, flight deals, or the lowest ticket price from a given start date across about the next month, including sites such as Booking.com, Expedia, Google Flights, Skyscanner, Kayak, and airline direct booking pages.
---

# Find Cheap Flights

## Overview

Find low airfare across a flexible date window, normalize the results into comparable total prices, and verify the best options before presenting them.

This skill depends on current live data. Use browser or web tools when available, and be explicit when a source cannot be accessed.

## Intake

Collect the minimum trip details before searching:

- Origin and destination, preferably city plus airport or IATA code.
- One-way or round-trip.
- Departure start date. Default search window is the start date through the next 29 days unless the user asks for a different range.
- For round trips, return date, trip length, or acceptable return-date window.
- Number of travelers, cabin, and any required baggage.
- Preferences that affect price: nonstop only, maximum stops, departure time, nearby airports, specific airlines, visa/self-transfer tolerance, refundability.

If details are missing, make conservative assumptions only when low-risk. Default to 1 adult, economy, USD for US-based users, flexible nearby airports only after asking, and prices including taxes and unavoidable fees.

## Search Workflow

1. Read `references/search-playbook.md` before doing a live search.
2. Build the date set:
   - One-way: search every departure date in the window, using flexible-date calendars when possible.
   - Round-trip with a fixed trip length: search each departure date with return date equal to departure plus the trip length.
   - Round-trip with flexible returns: ask for a trip length or return window unless the user already gave one.
3. Search at least three independent current sources when possible:
   - Broad fare calendar or metasearch source.
   - Online travel agency such as Booking.com or Expedia.
   - Airline direct site for the best candidates.
4. Normalize each candidate into the same fields: total price, currency, source, airline, route, dates, times, stops, duration, baggage included, fare restrictions, booking link, and timestamp checked.
5. Verify the top options by clicking through to the final fare summary or airline direct booking page. Replace stale teaser prices with the verified price.
6. Present a ranked shortlist with the cheapest verified option first, then summarize tradeoffs such as long layovers, self-transfer, basic economy restrictions, baggage fees, and refundability.

## Accuracy Rules

- Do not bypass captchas, logins, paywalls, bot checks, or site access controls.
- Do not scrape at scale or repeatedly hammer travel sites. Prefer normal browser interactions, official APIs, or publicly accessible search pages.
- Treat prices as volatile. Always include the date and time checked.
- Compare total trip cost, not only the headline fare. Include taxes, mandatory fees, and baggage assumptions.
- Be clear when a price is unverified, unavailable, region-locked, shown in another currency, or requires separate tickets.
- Do not ask the user for passport, payment, loyalty-account, or sensitive personal details. Stop before purchase.

## Output Format

Lead with the best few options and the exact assumptions used. Use a compact table for comparison:

| Rank | Price | Dates | Airline | Route | Stops | Duration | Source | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |

After the table, include:

- Cheapest verified fare and why it wins.
- Best value alternative if the cheapest has meaningful drawbacks.
- Sources checked and any blocked or unavailable sources.
- Next step for the user to book or refine the search.
