# Delta Airlines GraphQL Schema

## Overview

This GraphQL schema represents the conceptual data model for Delta Air Lines' flight and travel APIs, covering the full passenger journey from flight search and booking through check-in, boarding, and loyalty program management. Access to Delta's partner APIs requires approval through the Delta developer portal at [apiportal.delta.com](https://apiportal.delta.com).

## Schema Source

This schema is conceptual, derived from publicly known Delta Air Lines product and service offerings, NDC (New Distribution Capability) industry standards, and the Delta developer portal documentation. It is not an officially published GraphQL endpoint.

## Domain Coverage

### Flight Operations
Types covering the core flight lifecycle: `Flight`, `FlightNumber`, `FlightSchedule`, `FlightStatus`, `FlightDetails`, `AircraftInfo`, `Departure`, `Arrival`, `Gate`, `Terminal`, `Delay`, `Cancellation`, and `Diversion`. These represent the operational state of any Delta-operated or codeshare flight.

### Seats and Cabins
The seat model covers `Seat`, `SeatMap`, `SeatAvailability`, and cabin classes including `BasicEconomy`, `MainCabin`, `ComfortPlus`, `FirstClass`, `DeltaOne`, and `DeltaOneSuite`. Seat selection and upgrade eligibility are represented through `Upgrade` and `UpgradeCertificate`.

### Passengers and Identity
The `Passenger` type captures traveler information. The `KnownTraveler` type represents TSA PreCheck and trusted traveler data. Special service requests are modeled through `SpecialServiceRequest`.

### SkyMiles Loyalty Program
Delta's loyalty program is represented by `SkyMiles`, `SkyMilesAccount`, `MedallionStatus`, and tier types `SilverMedallion`, `GoldMedallion`, `PlatinumMedallion`, and `DiamondMedallion`. Miles activity is captured through `MilesEarning` and `MilesRedemption`. The `ChoiceCard` type models Medallion Choice Benefits.

### Booking and Reservations
The booking domain includes `Booking`, `Reservation`, `Confirmation`, `PNR`, `Itinerary`, `Ticket`, `Fare`, `FareRules`, and `FareBrand`. Companion travel is modeled through the `Companion` type.

### Check-in and Boarding
The passenger flow through the airport is represented by `Checkin`, `BoardingPass`, `BagTag`, `BaggageAllowance`, and `ExcessBag`.

### In-Flight Services
Onboard services are captured through `MealService`, `WiFi`, and `InFlightEntertainment`.

### Airport and Network
Airport infrastructure is represented by `Airport`, `Hub`, `Codeshare`, `Partner`, and `SkyTeam`. The SkyTeam alliance relationship is modeled explicitly to support partner redemption and earning scenarios.

### Access and Authentication
API access types include `APIKey` and `Token` for representing partner authentication state.

## Key Queries

- `flight(flightNumber, date)` — retrieve current status and details for a specific flight
- `flightSearch(origin, destination, date, passengers)` — search available flights and fares
- `itinerary(pnr, lastName)` — retrieve a reservation by PNR
- `seatMap(flightNumber, date, cabinClass)` — retrieve the seat map for a flight
- `skyMilesAccount(memberId)` — retrieve loyalty account details and balance
- `airport(code)` — retrieve airport information by IATA code

## Key Mutations

- `createBooking(input)` — create a new flight booking
- `cancelBooking(pnr)` — cancel an existing reservation
- `selectSeat(pnr, passengerId, seatNumber)` — assign a seat to a passenger
- `checkin(pnr, passengerId)` — initiate check-in for a passenger
- `redeemMiles(memberId, bookingInput)` — apply miles toward a booking
- `addSpecialServiceRequest(pnr, passengerId, ssrCode)` — add an SSR to a booking

## References

- Delta Developer Portal: https://apiportal.delta.com
- Delta Air Lines: https://www.delta.com
- NDC Standard: https://www.iata.org/en/programs/airline-distribution/ndc/
- SkyMiles Program: https://www.delta.com/us/en/skymiles/overview
- SkyTeam Alliance: https://www.skyteam.com
