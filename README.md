# ProveIT

A fully-functional Industrial Intelligence application built on the [FUUZ](https://fuuz.app) platform — demonstrating real-time telemetry, OEE, production tracking, alarm management, predictive analytics, and enterprise UNS integration across 4 manufacturing sites and 500+ assets.

ProveIT was built in **2–3 weeks part-time** to showcase the speed and breadth of what's possible on FUUZ.

## What Problems Does ProveIT Solve?

### Strategic (C-Suite)

| Problem | How ProveIT Solves It |
|---------|----------------------|
| No unified view of operational costs | Real-time production, OEE, and downtime data published to a single enterprise namespace — giving finance and operations a shared source of truth |
| Limited supply chain visibility | Work orders, production logs, and inventory data published to UNS in real time for ERP and customer visibility |
| Inconsistent data across sites | Standardized semantic models and KPIs (CESMII i3X aligned) across all sites — same data structure whether it's automotive stamping in Detroit or biologics in Dallas |
| Onboarding acquisitions takes too long | A repeatable digital blueprint: import the package, configure your equipment hierarchy, and you're running — no custom development per site |

### Tactical (Plant Floor)

| Problem | How ProveIT Solves It |
|---------|----------------------|
| Paper-based workflows | Digitized production tracking, batch release, and operator HMI panels replace clipboards and spreadsheets |
| No real-time downtime visibility | ISO 22400-compliant workcenter state tracking with 8 modes and 14 states, automatic OEE calculation every hour |
| Alarm fatigue / no alarm lifecycle | Full alarm management with 8 lifecycle states (Active → Acknowledged → Cleared), triggered automatically from telemetry limit violations |
| Reactive maintenance | Machine learning detects anomalies, forecasts values with confidence bands, and calculates cross-asset correlations — shifting from "fix it when it breaks" to "fix it before it breaks" |
| Compliance gaps (batch release) | Digital batch release workflow for process/bio manufacturing with full traceability |
| No operator-facing dashboards | Purpose-built HMI control panels for bioreactors, filtration skids, buffer vessels, and chromatography systems |

## What's in the Package

ProveIT is a single FUUZ package (`ProveIT Enterprise C - Full App@0.0.1.fuuz`) containing everything needed to run the application:

### 28 Data Models

| Category | Models | What They Track |
|----------|--------|-----------------|
| **Physical Hierarchy** | Site, Area, Line, Cell, Asset | The equipment structure: sites → areas → lines → cells → assets → data points |
| **Telemetry** | DataPoint, TelemetryRaw, TelemetryRawBool, TelemetryRawString, TelemetryHourly, TelemetryDaily | High-frequency sensor data (numeric, boolean, string) with hourly and daily statistical aggregations (avg, min, max, p05–p95, stdDev, cv) |
| **OEE & Production** | Workcenter, WorkcenterHistory, Mode, State, OeeHourly, OeeDaily, ProductionLog | ISO 22400 OEE: Availability × Performance × Quality calculated hourly and daily with full state/mode tracking |
| **Downtime Events** | EventCategory, Event | 12 downtime categories and 75 specific event reasons (mechanical failure, changeover, material issue, etc.) |
| **Production Master Data** | Product, WorkOrder | Products with cycle time standards, work orders with scheduling and completion tracking |
| **Alarm Management** | Alarm, AlarmState | Alarm lifecycle from trigger through acknowledgment to clearance, with 8 states |
| **Machine Learning** | TelemetryBaseline, TelemetryForecast, PatternInsight, CorrelationPair | EWMA baselines, predictive forecasts with confidence bands, anomaly detection, and cross-asset Pearson correlations |

### 26 Screens

- **6 HMI Control Panels** — Operator-facing panels for bioreactors, filtration, buffer prep, chromatography, robotics, and production control
- **4 OEE Dashboards** — Real-time OEE visualization, reliability analysis, hourly and daily drill-down
- **6 Data Management Screens** — Assets, products, workcenters, workcenter history, production logs, alarms
- **4 Telemetry Viewers** — Raw numeric, raw string, hourly aggregation, daily aggregation
- **5 ML/Analytics Screens** — Baselines, forecasts, pattern insights, correlation pairs, and a dedicated ML dashboard
- **1 Batch Release Dialog** — Compliance workflow for process manufacturing

### 39 Data Flows

- **Telemetry Ingestion** — Real-time data collection, cross-tenant ingest, hourly and daily aggregation
- **OEE Engine** — Hourly OEE calculation, daily rollup, planned availability, OEE stub generation, production event detection
- **Production Automation** — Weekly work order generation, daily production simulation, production log submission
- **Workcenter State Machine** — ISO 22400 state change tracking with mode/state transitions
- **Alarm Processing** — Automatic alarm creation from telemetry anomalies
- **Machine Learning** — Anomaly/pattern detection, EWMA forecasting with confidence bands, cross-asset correlation
- **UNS Publishing** — 5 integration flows pushing telemetry, alarms, ML insights, workcenter history, and production data to the enterprise Unified Namespace
- **HMI Backends** — 6 web flows powering the operator control panels

### Also Included

- **3 Auto-Sequence Generators** — Automatic code generation for alarms, assets, and data points
- **3 Security Roles** — Enterprise C Bio, Manufacturing Execution, Telemetry Manager
- **9 Saved Transforms** — OEE calculations, timezone utilities, Gantt chart data, trend visualizations
- **7 Visualizations** — Telemetry trends, OEE component breakdowns, workcenter timeline Gantt, win/loss charts

## Demo Data: 4 Sites, 4 Industries

ProveIT ships with a fully populated multi-site environment:

| Site | Location | Industry | What's Modeled |
|------|----------|----------|----------------|
| **DET** | Detroit | Automotive | Stamping, CNC machining, welding, and assembly lines producing brake components, control arms, sensor housings, and transmission gear blanks |
| **HOU** | Houston | Chemical / Process | Batch and continuous reactors, distillation, filtration, and heat exchange producing resin compounds, polymer bases, and additive blends |
| **MKE** | Milwaukee | Food & Beverage | Batch mixing, continuous blending, filling, and cartoning lines producing sauces, dressings, juice, and tomato paste |
| **Bio DFW** | Dallas | Biologics / Biopharma | SUB-250 bioreactor, TFF-300 filtration skid, SUM-500 buffer vessel, CHR-01 chromatography skid with ISA-style instrumentation |

**By the numbers:** 4 sites, 10 areas, 19 lines, 40 cells, 504 assets, 1,000+ data points, 43 workcenters, 21 products, 534 work orders, 47 units of measure.

## Architecture

```
┌─────────────────────────────────────────────────────┐
│                   FUUZ Enterprise                    │
│                                                     │
│  ┌──────────┐  ┌──────────┐  ┌──────────────────┐  │
│  │ Telemetry│  │   OEE    │  │  Machine Learning │  │
│  │ Ingest & │  │  Engine  │  │  Anomaly Detect   │  │
│  │ Aggregate│  │ ISO 22400│  │  Forecast + Corr  │  │
│  └────┬─────┘  └────┬─────┘  └────────┬─────────┘  │
│       │              │                 │             │
│       ▼              ▼                 ▼             │
│  ┌──────────────────────────────────────────────┐   │
│  │              Unified Data Layer               │   │
│  │  28 Models · 504 Assets · 1000+ Data Points  │   │
│  └──────────────────────┬───────────────────────┘   │
│                         │                            │
│       ┌─────────────────┼─────────────────┐         │
│       ▼                 ▼                 ▼         │
│  ┌─────────┐     ┌───────────┐     ┌──────────┐   │
│  │   HMI   │     │    OEE    │     │    UNS   │   │
│  │ Panels  │     │Dashboards │     │ Publish  │   │
│  │ (6)     │     │   (4)     │     │  (5)     │   │
│  └─────────┘     └───────────┘     └──────────┘   │
│                                          │          │
└──────────────────────────────────────────┼──────────┘
                                           │
                              ┌────────────▼──────────┐
                              │   Enterprise UNS      │
                              │  MQTT · WSS · REST    │
                              │  ERP · MES · WMS      │
                              └───────────────────────┘
```

## FUUZ Platform Capabilities Used

ProveIT exercises nearly every capability of the FUUZ platform:

- **Data Modeling** — 28 interconnected models with referential integrity, auto-sequencing, and seed data
- **Screen Builder** — 26 screens including list/detail views, HMI panels, dashboards, and dialog widgets
- **Data Flow Engine** — 39 flows covering scheduled jobs, event-driven triggers, web flows, and integration flows
- **Visualizations** — Trend charts, Gantt timelines, OEE component breakdowns, win/loss analysis
- **Saved Transforms** — Reusable JSONata calculations for OEE, timezone conversion, and chart data
- **Role-Based Security** — 3 roles with scoped access across modules
- **UNS Integration** — 5 outbound publishing flows to enterprise namespace via MQTT/WSS
- **Cross-Tenant Ingest** — Real-time data flow between FUUZ tenants
- **Auto-Sequences** — Automatic code generation for operational records
- **Scheduled Operations** — 11 scheduled jobs from 15-minute telemetry generation to weekly work orders

## Getting Started

### Import into FUUZ

1. Request a [free trial of FUUZ](https://fuuz.app)
2. Navigate to **Application Lifecycle Management**
3. Upload `ProveIT Enterprise C - Full App@0.0.1.fuuz`
4. Review the import preview and confirm
5. The full application — models, screens, flows, seed data — is ready to use

### Explore the Package

The `.fuuz` file is a gzipped tarball containing three JSON files:

```bash
# Extract the package
mkdir extracted && cd extracted
tar -xzf "../ProveIT Enterprise C - Full App@0.0.1.fuuz"

# What's inside
ls -lh
# manifest.json      - Package metadata (name, version, dependencies)
# definition.json    - Module groups, modules, and enum seed data
# package-data.json  - All 28 data models, 26 screens, 39 flows, and seed data
```

## Resources

| Resource | Link | Description |
|----------|------|-------------|
| **Free Trial** | [fuuz.app](https://fuuz.app) | Request your free trial of FUUZ |
| **Get Started** | [getstarted.fuuz.com](https://getstarted.fuuz.com) | Introductory videos and walkthroughs |
| **FUUZ Academy** | [academy.fuuz.com](https://academy.fuuz.com) | Online LMS with structured courses and certifications |
| **Support & Community** | [support.fuuz.com](https://support.fuuz.com) | Knowledge base, documentation, and customer community |
| **FUUZ Skills for Claude** | [github.com/Fuuz-Industrial-Intelligence/fuuz-skills](https://github.com/Fuuz-Industrial-Intelligence/fuuz-skills) | Claude Code skills for building FUUZ applications |
