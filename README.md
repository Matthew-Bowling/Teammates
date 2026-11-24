# Teammates

**Find your team's people, and the place to watch the game together.**

Teammates is a web app for sports fans. It helps you find watch parties at local bars, join or start a fan group for your team in your city, and organize tailgates. I'm designing and building it on my own as a personal project.

> 🔒 **The source code is private.** I'm happy to walk through the code and design in an interview. Reach me on [LinkedIn](https://www.linkedin.com/in/matthewbowlingdev/).

## Features

- **Watch parties:** find upcoming watch parties by city, team or group, soonest first (games in progress still show)
- **Fan groups:** create a group for your team and city, follow groups, and manage members with admin and follower roles
- **Tailgates:** organize and discover tailgates by team, group or stadium
- **Map:** venues with upcoming watch parties on an interactive map, filtered by distance and your favorite teams
- **Calendar:** your favorite teams' games and your groups' watch parties in one view
- **Search:** one search bar across teams, groups, watch parties and tailgates
- **Group pages and photo galleries**
- **Accounts:** sign-up, login, favorite teams and followed groups
- Multiple pro and college leagues, including the NFL, MLS and NCAA football

## Architecture

One ASP.NET Core Blazor Web App (.NET 8, Interactive Server) serves the UI, hosts a REST API and talks to SQL Server.

```
Browser ───────► Blazor UI (MudBlazor) ──┐
                                         ├──► Repositories (Dapper) ──► SQL Server
Swagger / future mobile app ──► REST API ┘
```

- **Shared data layer:** Blazor pages call the repositories directly, with no HTTP hop. The REST API uses the same repositories, so it's ready for a mobile client.
- **Consistent structure:** each API area (teams, watch parties, groups, accounts, venues, tailgates, cities, photos) follows the same pattern: controller, Dapper repository, database entity, conversion, web entity.
- **Authentication:** JWT bearer tokens for API clients. The website signs in with a cookie set through a short-lived, single-use ticket, because Blazor's live connection can't set cookies itself.
- **Business rules in the API:** for example, a group always keeps at least one admin while anyone follows it.
- **Time zones:** every time is stored and served in UTC and shown in each user's local time.
- **Deployment:** containerized with Docker and set up to host on Render with Azure SQL.
- **API docs:** every endpoint is documented in Swagger / OpenAPI.

## Tech stack

C# · .NET 8 · ASP.NET Core · Blazor · MudBlazor · Dapper · SQL Server / Azure SQL · JWT authentication · Swagger · MapLibre GL · SkiaSharp · Docker · xUnit · bUnit

## Testing

- Test project using xUnit, bUnit (Blazor component tests) and the ASP.NET Core test host
- A test-data loader that fills the site with about 1,000 accounts, 400 groups, 2,000 watch parties and 350 tailgates across every league and region, plus a script that removes it cleanly

## Status

In active development. Designs are written up for Facebook integration and two-factor authentication.
