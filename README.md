# ProveIT

A suite of fully-functional Industrial Intelligence applications built on the [FUUZ](https://fuuz.app) platform — demonstrating how a single platform can unify IIoT telemetry, MES, WMS, OEE, predictive analytics, and enterprise data brokering across 7 global manufacturing sites.

ProveIT was built in **2–3 weeks part-time** to showcase the speed and breadth of what's possible on FUUZ.

## The Scenario

An enterprise oversees **7 global manufacturing sites** — 3 existing FUUZ-enabled plants plus 4 newly acquired facilities. The mandate: scale from plant-level to a **governed enterprise deployment** with a Unified Namespace (UNS) across all sites, no disruptions to live operations, and compliance with data standards for future acquisitions.

ProveIT proves it can be done — with three FUUZ applications working together.

## Three Applications, One Platform

| Application | What It Does | Models | Screens | Flows |
|-------------|-------------|--------|---------|-------|
| [**Enterprise C — Full App**](#enterprise-c--full-app) | IIoT telemetry, OEE, production tracking, alarms, and predictive ML across 4 sites and 500+ assets | 28 | 26 | 39 |
| [**Enterprise B — WMS**](#enterprise-b--wms) | Finished goods warehouse management with receiving, inventory, cycle counting, AGV putaway, and order fulfillment | 38 | 33 | 33 |
| [**Data Broker**](#data-broker) | Multi-system integration hub connecting production, robots, SCADA, WMS, and ERP via MQTT, OPC UA, and REST | 34 | 14 | 22 |
| **Totals** | | **100 models** | **73 screens** | **94 flows** |

## What Problems Does ProveIT Solve?

### Strategic (C-Suite)

| Problem | How ProveIT Solves It |
|---------|----------------------|
| No unified view of operational costs | Real-time production, OEE, inventory, and downtime data published to a single enterprise namespace — giving finance and operations a shared source of truth |
| Limited supply chain visibility | Work orders, production logs, putaway moves, and shipments published to UNS in real time for ERP and customer visibility |
| Inconsistent data across sites | Standardized semantic models and KPIs (CESMII i3X aligned) across all sites — same data structure whether it's automotive stamping in Detroit or biologics in Dallas |
| Onboarding acquisitions takes too long | A repeatable digital blueprint: import the package, configure your equipment hierarchy, and you're running — no custom development per site |
| Real-time financial impact to G/L | Detailed inventory and batch data published in real time for ERP integration |

### Tactical (Plant Floor)

| Problem | How ProveIT Solves It |
|---------|----------------------|
| Paper-based workflows | Digitized production tracking, batch release, receiving, cycle counting, and operator HMI panels replace clipboards and spreadsheets |
| No real-time downtime visibility | ISO 22400-compliant workcenter state tracking with 8 modes and 14 states, automatic OEE calculation every hour |
| Alarm fatigue / no alarm lifecycle | Full alarm management with 8 lifecycle states (Active → Acknowledged → Cleared), triggered automatically from telemetry limit violations |
| Reactive maintenance | Machine learning detects anomalies, forecasts values with confidence bands, and calculates cross-asset correlations — shifting from "fix it when it breaks" to "fix it before it breaks" |
| Compliance gaps (batch release) | Digital batch release workflow for process/bio manufacturing with full traceability |
| Inventory accuracy gaps | GS1/SSCC-compliant handling unit tracking, barcode-driven inventory operations (move/merge/split), and parameterized cycle counting with blind count support |
| Logistics orchestration | Directed putaway with product-preferred locations, AGV-assisted material flow, and truck loading/shipping management |
| Disconnected production systems | Data Broker normalizes data from multiple enterprises, robots, and protocols (MQTT, OPC UA, REST) into a unified ISA-95 hierarchy |

---

## Enterprise C — Full App

**Package:** `ProveIT Enterprise C - Full App@0.0.1.fuuz`

The core IIoT + MES + OEE + Predictive Analytics application managing real-time telemetry ingestion, production execution, alarm management, and machine learning across 4 manufacturing sites.

### 28 Data Models

| Category | Models | What They Track |
|----------|--------|-----------------|
| **Physical Hierarchy** | Site, Area, Line, Cell, Asset | Equipment structure: sites → areas → lines → cells → assets → data points |
| **Telemetry** | DataPoint, TelemetryRaw, TelemetryRawBool, TelemetryRawString, TelemetryHourly, TelemetryDaily | High-frequency sensor data (numeric, boolean, string) with hourly and daily statistical aggregations (avg, min, max, p05–p95, stdDev, cv) |
| **OEE & Production** | Workcenter, WorkcenterHistory, Mode, State, OeeHourly, OeeDaily, ProductionLog | ISO 22400 OEE: Availability × Performance × Quality calculated hourly and daily with full state/mode tracking |
| **Downtime Events** | EventCategory, Event | 12 downtime categories and 75 specific event reasons |
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
- **OEE Engine** — Hourly OEE calculation, daily rollup, planned availability, OEE stub generation
- **Production Automation** — Weekly work order generation, daily production simulation
- **Workcenter State Machine** — ISO 22400 state change tracking with mode/state transitions
- **Alarm Processing** — Automatic alarm creation from telemetry anomalies
- **Machine Learning** — Anomaly/pattern detection, EWMA forecasting, cross-asset correlation
- **UNS Publishing** — 5 integration flows pushing telemetry, alarms, ML insights, workcenter history, and production data to the enterprise UNS
- **HMI Backends** — 6 web flows powering the operator control panels

### Demo Data: 4 Sites, 4 Industries

| Site | Location | Industry | What's Modeled |
|------|----------|----------|----------------|
| **DET** | Detroit | Automotive | Stamping, CNC machining, welding, and assembly lines producing brake components, control arms, sensor housings, and transmission gear blanks |
| **HOU** | Houston | Chemical / Process | Batch and continuous reactors, distillation, filtration, and heat exchange producing resin compounds, polymer bases, and additive blends |
| **MKE** | Milwaukee | Food & Beverage | Batch mixing, continuous blending, filling, and cartoning lines producing sauces, dressings, juice, and tomato paste |
| **Bio DFW** | Dallas | Biologics / Biopharma | SUB-250 bioreactor, TFF-300 filtration skid, SUM-500 buffer vessel, CHR-01 chromatography skid with ISA-style instrumentation |

**By the numbers:** 4 sites, 10 areas, 19 lines, 40 cells, 504 assets, 1,000+ data points, 43 workcenters, 21 products, 534 work orders, 47 units of measure.

---

## Enterprise B — WMS

**Package:** `ProveIT Enterprise B WMS@0.0.1.fuuz`

A finished goods warehouse management system for a beverage manufacturing/distribution operation — handling the full lifecycle from inbound receiving through inventory management, cycle counting, AGV-directed putaway, and outbound order fulfillment.

### 38 Data Models

| Category | Models | What They Track |
|----------|--------|-----------------|
| **Inventory Management** | Inventory, InventoryStatus, InventoryTrace, Lot, HandlingUnit, Product, ProductCategory, Adjustment, TransactionType, Process | Core inventory with barcode/serial tracking, GS1/SSCC-compliant handling units, lot traceability, and inventory operations (move/merge/split) with full audit trail |
| **Cycle Counting** | Count, CountLine, CountLineInventory, CountParameters, CountStatus | Parameterized cycle counting by area, product, zone, or date range with blind count support, barcode scanning, recount capability, and automatic inventory adjustment |
| **Order Fulfillment** | Order, OrderLine, OrderLineRelease, OrderStatus, OrderType, OrderLineReleaseStatus, OrderLineReleaseType | Purchase order processing with multi-release scheduling (firm/forecasted/planned), partial fulfillment support, and full lifecycle tracking |
| **Business Partners** | BusinessPartner, BusinessPartnerAddress | Customer/supplier master data with multi-address support, credit limits, and payment terms |
| **Receiving** | Receipt, ReceiptLine, ReceiptLineOrderLineRelease, ReceiptException, ReceiptExceptionReason, ReceiptStatus | Inbound receiving with ASN/BOL tracking, lot assignment, receipt confirmation, and exception handling (damaged, quantity discrepancy, wrong product, expired) |
| **Site Management** | StorageUnit, StorageZone, StorageUnitStatus, Area | Warehouse layout with ISA-95 aligned hierarchy — areas, zones (with flags for hazardous, refrigerated, high-value, overflow), and storage units (bins, shelves, docks, trucks) |
| **Logistics** | PutawayRequest, AutomatedGuidedVehicle, ProductPreferredStorageUnit, LabelDesign | Directed putaway with product-location affinity, AGV task management with battery/speed/progress tracking, and ZPL/IPL label generation |

### 33 Screens

- **14 Inventory Screens** — Inventory list/table, move/merge/split widgets, create inventory, product management, category/process/adjustment setup
- **5 Cycle Counting Screens** — Count list, count details, location selector, count execution with barcode scanning
- **5 Order/Partner Screens** — Order management, business partner list/detail, address management, order line creation
- **5 Receiving Screens** — New receipt, receipt line creation, confirmation, details modal, exception reporting
- **2 Putaway Screens** — Putaway execution, putaway request queue
- **1 Shipping Screen** — Outbound shipping operations
- **1 WES Dashboard** — Warehouse Execution System monitoring

### 33 Data Flows

- **Cycle Counting** — Count creation, line generation, inventory measurement, exclusion, recount, cancellation, completion with auto-adjustment
- **Inventory Operations** — Move, merge, and split with full traceability
- **Receiving/Orders** — Receipt line creation/confirmation, order status updates, release status updates
- **Putaway/AGV** — Directed putaway execution, AGV brain logic (vehicle routing and task management)
- **UNS Integration** — Storage unit summaries, truck data, and inventory counts published to enterprise namespace via Data Broker

### Demo Data

A fully populated beverage distribution warehouse: 1,000 inventory records, 120 lots, 64 storage units (shelf bays, palletizer stations, trucks), 30 handling units, 16 beverage products (Orange Soda/Cola in 0.5L to 24-packs), 2 AGVs (Robbie and K9), and 52 product-to-location priority mappings.

---

## Data Broker

**Package:** `ProveIT Data Broker App@0.0.1.fuuz`

The integration hub that connects everything together. Sits between production systems, robots, SCADA, WMS, and ERP — normalizing data from multiple enterprises and protocols into a unified ISA-95 hierarchy and brokering it to downstream consumers.

### 34 Data Models

| Category | Models | What They Track |
|----------|--------|-----------------|
| **ISA-95 Hierarchy** | Enterprise, Site, Area, Line, Workcenter, EntityAsset | Normalized equipment hierarchy from multiple source systems into a common structure |
| **Production/Orders** | Workorder, WorkorderCompletion, Item, Lot, Asset | Production work orders, items (with bottle size/pack count for beverage), lot tracking, and equipment assets |
| **Real-Time Process Data** | ProcessData, ProcessCount, ProcessInput, ProcessRate, ProcessState, Process, EnterpriseCValues | Live production counts (infeed/outfeed/defect), rates, analog values (flow, temp, weight), and state tracking |
| **OEE Metrics** | Metric, MetricInput | Real-time OEE (Availability × Performance × Quality) at every hierarchy level with raw input data |
| **IoT Tag System** | IotTag, IotTagHistoricalValue, IotTagType, IotTagUseCase, IotTagDataType | Universal IoT tag management with current values, historical time-series, and device subscription auto-creation |
| **Robot Management** | RobotState, RobotStateHistory, RobotHistory, Mode, State | Fanuc CRX-10 robot state (gripper, sensors, counts, cycle time), with OPC UA telemetry and historical snapshots |
| **Dashboard History** | MetricHistory, ProcessDataHistory, WorkorderHistory, LotHistory | Denormalized historical snapshots for efficient dashboard queries and trending |

### 14 Screens

- **5 IoT Tag Screens** — Tag list, type management, use case configuration, data type setup, tag historian
- **4 Robot Screens** — Robot state list, 2 edge-deployed HMI panels, robot history table
- **3 Dashboard/Test Screens** — Site dashboard, tree-view metrics, state/mode setup
- **2 Edge Screens** — Robot HMI panels deployed to edge gateways at the production line

### 22 Data Flows

#### Inbound (data coming IN)

| Source | Protocol | What It Brings |
|--------|----------|----------------|
| Enterprise B | MQTT | Production data → normalized into ISA-95 hierarchy, OEE metrics, process data, workorders, lots + history |
| Enterprise C | MQTT | Process values → key-value store for downstream SCADA |
| Fanuc CRX-10 | OPC UA | Robot coils, holding registers, discrete inputs, program name → robot state |
| Prosys Simulator | OPC UA | Simulated robot data for testing |

#### Outbound (data going OUT)

| Target | What It Sends |
|--------|---------------|
| SCADA System | Enterprise C process values via dedicated FUUZ tenant |
| WMS | Palletizer/packaging outfeed → triggers inventory creation in WMS |
| Robot Controller | Packing work orders → creates robot work orders via GraphQL |
| UNS | Publishes to local Unified Namespace via edge gateway |

### Integration Architecture

```
    INBOUND                                      OUTBOUND

Enterprise B ──MQTT──┐                    ┌──► SCADA System
                     │                    │    (process values)
Enterprise C ──MQTT──┤                    │
                     │   ┌────────────┐   ├──► WMS
Fanuc CRX-10 ─OPCUA─┤───│  ProveIT   │───┤    (outfeed → inventory)
                     │   │   Data     │   │
Prosys OPC UA ─OPCUA─┤   │  Broker    │   ├──► Robot Controller
                     │   └────────────┘   │    (work orders)
Robot MQTT   ──MQTT──┘                    │
                                          └──► Enterprise UNS
                                               (MQTT via edge gateway)
```

---

## How the Three Apps Work Together

```
┌─────────────────────────────────────────────────────────────────┐
│                        FUUZ Enterprise                           │
│                                                                 │
│  ┌─────────────────┐   ┌──────────────┐   ┌─────────────────┐  │
│  │  Enterprise C    │   │  Data Broker  │   │  Enterprise B   │  │
│  │  Full App        │   │               │   │  WMS            │  │
│  │                  │   │  MQTT · OPCUA │   │                 │  │
│  │  · IIoT Telemetry│◄─►│  · REST · WSS │◄─►│  · Receiving    │  │
│  │  · OEE Engine    │   │               │   │  · Inventory    │  │
│  │  · ML Analytics  │   │  Normalizes & │   │  · Cycle Count  │  │
│  │  · Alarm Mgmt    │   │  routes data  │   │  · Order Fulfill│  │
│  │  · HMI Panels    │   │  between all  │   │  · AGV Putaway  │  │
│  │  · Batch Release │   │  systems      │   │  · Shipping     │  │
│  │                  │   │               │   │                 │  │
│  │  28 models       │   │  34 models    │   │  38 models      │  │
│  │  26 screens      │   │  14 screens   │   │  33 screens     │  │
│  │  39 flows        │   │  22 flows     │   │  33 flows       │  │
│  └─────────────────┘   └──────┬───────┘   └─────────────────┘  │
│                               │                                 │
└───────────────────────────────┼─────────────────────────────────┘
                                │
                   ┌────────────▼────────────┐
                   │   Enterprise UNS         │
                   │   MQTT · WSS · REST      │
                   │   ERP · SCADA · Robots   │
                   └─────────────────────────┘
```

**Data flows between apps:**
- **Enterprise C → Data Broker** — Telemetry and process data published via MQTT
- **Data Broker → WMS** — Palletizer outfeed triggers inventory creation
- **Data Broker → Robot** — Packing work orders sent to robot controller
- **Data Broker → SCADA** — Enterprise C values forwarded to SCADA system
- **WMS → Data Broker → UNS** — Inventory, storage unit, and truck data published to enterprise namespace
- **Enterprise C → UNS** — Telemetry, alarms, ML insights, workcenter history, and production data published directly

## Getting Started

### Import into FUUZ

1. Request a [free trial of FUUZ](https://fuuz.app)
2. Navigate to **Application Lifecycle Management**
3. Upload each `.fuuz` package:
   - `ProveIT Enterprise C - Full App@0.0.1.fuuz`
   - `ProveIT Enterprise B WMS@0.0.1.fuuz`
   - `ProveIT Data Broker App@0.0.1.fuuz`
4. Review the import preview and confirm each
5. The full applications — models, screens, flows, seed data — are ready to use

### Explore the Packages

Each `.fuuz` file is a gzipped tarball containing three JSON files:

```bash
# Extract any package
mkdir extracted && cd extracted
tar -xzf "../ProveIT Enterprise C - Full App@0.0.1.fuuz"

# What's inside
ls -lh
# manifest.json      - Package metadata (name, version, dependencies)
# definition.json    - Module groups, modules, and enum seed data
# package-data.json  - Data models, screens, flows, and seed data
```

## Resources

| Resource | Link | Description |
|----------|------|-------------|
| **Free Trial** | [fuuz.app](https://fuuz.app) | Request your free trial of FUUZ |
| **Get Started** | [getstarted.fuuz.com](https://getstarted.fuuz.com) | Introductory videos and walkthroughs |
| **FUUZ Academy** | [academy.fuuz.com](https://academy.fuuz.com) | Online LMS with structured courses and certifications |
| **Support & Community** | [support.fuuz.com](https://support.fuuz.com) | Knowledge base, documentation, and customer community |
| **FUUZ Skills for Claude** | [github.com/Fuuz-Industrial-Intelligence/fuuz-skills](https://github.com/Fuuz-Industrial-Intelligence/fuuz-skills) | Claude Code skills for building FUUZ applications |
