# Flight Search Playbook

## Source Mix

Use a mix of sources because travel sites often disagree:

- Fare calendar or metasearch: Google Flights, Skyscanner, Kayak, Momondo, or similar.
- Online travel agencies: Booking.com, Expedia, Priceline, Trip.com, or similar.
- Airline direct sites for the cheapest or most plausible top candidates.
- Regional low-cost carriers when they commonly serve the route.

If the user names specific sites, include those sites unless they are inaccessible.

## Query Method

Use IATA airport codes when known. If only a city is given, identify the likely airports and ask before including far-away alternates that materially change ground travel.

For each source:

1. Set trip type, passengers, cabin, origin, destination, and date window.
2. Use flexible-date, monthly calendar, or price graph views whenever available.
3. Sort or filter by lowest total price, then inspect the cheapest realistic choices.
4. Open the fare details far enough to see taxes, fees, baggage, layovers, and whether the ticket is sold as separate bookings.
5. Record the result with a source URL and timestamp.

## Site Notes

- Booking.com: Use the Flights search, check whether the listed fare is operated by an OTA partner, and verify baggage and fare rules before ranking.
- Expedia: Use Flights, flexible dates when available, and continue to the fare detail page because package prompts and member pricing can obscure the actual ticket price.
- Google Flights: Good for date grids, price graphs, airline direct links, and sanity checks, but often not the final seller.
- Skyscanner/Kayak/Momondo: Good for broad discovery. Treat unusually low OTA fares as leads until verified on the seller page.
- Airline direct: Use to confirm whether the fare exists, whether baggage differs, and whether booking direct is close enough in price to be better value.

## Ranking Heuristics

Rank by verified total price first, then by practical quality:

- Nonstop or shorter total duration beats a slightly cheaper itinerary with severe layovers.
- Avoid self-transfer, separate tickets, airport changes, or overnight layovers unless the price difference is large and the user accepts the risk.
- Basic economy can be cheapest but must be labeled if seat selection, changes, carry-on, or checked bags are restricted.
- For international flights, note long transits and visa-sensitive self-transfers without giving legal advice.

## Result Template

Record candidates in this shape before summarizing:

```text
checked_at:
source:
source_url:
price_total:
currency:
trip_type:
origin:
destination:
depart_date:
return_date:
airline:
flight_numbers:
depart_time:
arrival_time:
stops:
duration:
baggage_included:
fare_type:
seller:
verification_status:
notes:
```
