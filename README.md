# PITWALL

## What is this?
=======
PitWall is an **F1 data analysis** and telemetry visualization tool.  
It allows race engineers, sim racers, and data fans to analyze lap times, throttle usage, speed traces, and driver comparisons using real Formula 1 telemetry.



A professional Formula 1 telemetry analysis workstation providing comprehensive race data analysis capabilities.

![PITWALL](/images/page01.png)

---

## 1. Historical Analysis

This group contains deep post-race analysis tools, covering strategy, tires, incidents, and track/environmental context.

![PITWALL](/images/page02.png)

### 1.1 Temperature Analysis
This module visualizes environmental data throughout the race weekend. In addition to track temperature (Track Temp) and air temperature (Air Temp), it integrates live data streams for humidity, pressure, and rainfall. By aligning everything on a shared timeline, you can precisely analyze how environment variables affect lap-time performance on specific laps or tire degradation trends.

It supports switching year and event dynamically, and provides an auto-scaling time-axis chart.

### 1.2 Track Analysis
This module renders a high-precision circuit map and labels all official corner numbers and DRS detection/activation zones. It uses vector data from the API to draw track geometry, and supports overlays such as driver trajectories or telemetry layers (e.g., a speed heatmap).
It includes coordinate conversion logic to map GPS coordinates into on-screen XY plotting coordinates, making it a foundational tool for analyzing racing lines and track characteristics.

### 1.3 Pitstop Analysis
This module provides detailed pitstop analytics with two views: a team summary and a detailed log.
It calculates each driver’s pitstop count, average stationary time, and total pit loss (in/out + stationary). The module includes smart filters to distinguish normal pitstops from drive-throughs, and shows compound changes before/after each stop.


### 1.4 Accident & Flags Analysis
This tool focuses on interruptions and race-control events, including Yellow Flag, Red Flag, Virtual Safety Car (VSC), and Safety Car (SC). It presents these events on a Gantt-chart-style timeline, showing duration and the lap on which they occur.
This is critical for understanding race rhythm changes, strategy decision points, and effective racing laps, and it can be correlated with specific DNF causes.

### 1.5 Tire Strategy Analysis
This is the core module for analyzing tire usage strategy. It uses intuitive horizontal stint bars for each driver: each bar segment represents one set of tires, with colors mapped to compounds (red/yellow/white/green/blue) and segment length mapped to stint length.
Internally, it calculates average lap time and degradation trends per stint, and labels whether a stint started on new or used tires. This lets you quickly compare one-stop vs multi-stop strategies across teams.

### 1.6 Driver Run Position
This module plots a position chart for the entire race (position vs lap). It includes special handling for DNFs to keep position calculations correct for cars still running.
An interactive legend allows quickly filtering drivers for comparison—e.g., focusing on the top 3 battle or a tight midfield fight. Data is sourced directly from official timing position-by-lap records.

### 1.7 Traffic Analysis
This advanced module quantifies traffic conditions encountered during the race. By computing gaps to cars ahead/behind, it determines whether a driver is in clean air or impacted by dirty air/wake.
Results are typically shown as heatmaps or interval charts, highlighting what percentage of race distance a driver was blocked. This is essential for evaluating true pace and pit-window choices.

---

## 2. Telemetry Analysis
This group provides sample-rate (Hz) vehicle physics data analysis for precise comparisons of driving style and car performance.
![PITWALL](/images/page03.png)

### 2.1 Main Telemetry Analysis
The most powerful telemetry tool in the system. It supports synchronized display of multiple channels including Speed, RPM, Gear, Throttle, Brake, and DRS status.
It uses a high-performance plotting engine, supports multi-driver overlay comparison, and includes cursor synchronization: moving the cursor in one chart updates all related charts to the same time point.


### 2.2 Channel-Specific Analysis
These modules are optimized, deeper views for specific signals:

* **Speed Analysis**
    * Focuses on speed-curve detail with finer Y-axis scaling and smoothing to observe minimum corner speed and end-of-straight top speed.

* **Brake Analysis**
    * Analyzes brake input pressure and duration to identify braking points and trail-braking technique.

* **Throttle Analysis**
    * Examines throttle opening changes, especially useful for studying traction control and throttle modulation on corner exit.

* **Gear & RPM**
    * Often used together to analyze shift points, gearing strategy, and engine output characteristics across RPM ranges.

* **Acceleration (Generic)**
    * Computes longitudinal and lateral acceleration to generate a G-G diagram, useful for evaluating tire grip limits and overall cornering performance.

### 2.3 Delta Analysis
* Directly computes speed differences between two cars at the same track position to show who is faster in corners/straights.
* Integrates speed deltas to estimate spatial distance changes, useful for analyzing how gaps open/close during a chase.
* Provides the classic time-delta curve over a lap relative to a reference lap, helping identify where time is gained or lost.

---

## 3. Lap Performance
This group focuses on statistical lap-time characteristics, consistency, and long-run performance.
![PITWALL](/images/page04.png)

### 3.1 Detailed Lap Data
Provides a feature-rich table listing detailed information for every lap of selected drivers. Columns include lap number, lap time, sector times (S1/S2/S3), speed trap, tire compound and age.
It also marks abnormal laps (e.g., yellow-flag affected, out-laps after a pit stop) and color-codes personal best (green) and overall best (purple), making it the preferred tool for data integrity checks.

### 3.2 Lap Time Box Plot
Uses a box-and-whisker plot to visualize lap-time distribution, showing median, IQR, and outliers.
This helps filter pit laps or traffic-impacted laps to reflect true race pace and consistency. A narrower box indicates a more consistent driver.

### 3.3 Throttle Corner Analysis
Combines throttle data with track corners. It computes metrics such as average throttle opening or full-throttle ratio through specific corners, visualized via box plots or line charts.
This helps evaluate driver confidence, grip conditions, and corner-exit throttle application—key indicators of a driver’s cornering limit.

### 3.4 Pedal Behavior Analysis
![PITWALL](/images/page16.png)

This module presents the pedal usage status distribution for each driver using a stacked bar chart. The system classifies pedal behavior into four states:
* **Throttle Only**: Only the throttle pedal is pressed, typically during straight-line acceleration or full-throttle exit.
* **Brake Only**: Only the brake pedal is pressed, corresponding to heavy braking zones before corner entry.
* **Trail Braking**: Both throttle and brake are operated simultaneously. This is an advanced technique used to maintain balance during corner entry and maximize cornering speed.
* **Coasting**: Neither pedal is pressed, indicating the driver is coasting due to inertia or performing Lift and Coast for fuel saving.

### 3.5 Long Run Analysis
Designed for FP2 long-run simulation analysis. It includes a **stint detection algorithm** to automatically identify continuous, representative timed laps.
Core capability includes **fuel correction**: it estimates corrected lap time by removing fuel weight effects lap-by-lap, allowing you to isolate pure tire degradation rate. This is a key input for race pitstop strategy planning.

---

## 4. Ideal Lap & Sectors
This group reconstructs best sector times to explore theoretical performance limits.
![PITWALL](/images/page05.png)

### 4.1 Ideal Lap Ranking
Computes each driver’s theoretical best lap time by summing their best S1, S2, and S3 from the session.
It compares the theoretical time with actual pole time and calculates the “potential gap,” revealing whether a driver left time on the table due to mistakes or whether the car has hidden performance strengths in specific sectors.

---

## 5. Speed & Corner Analysis

### 5.1 Straight Line Speed
![PITWALL](/images/page06.png)
Collects and compares top speed/trap speed at key straight endpoints. This reflects drag level and engine power.
The module typically filters out abnormal data affected by DRS or strong tow to evaluate intrinsic straight-line performance in clean air, helping assess whether downforce settings are too aggressive.

### 5.2 Brake & Acceleration Performance
Uses scatter plots to analyze deceleration performance in heavy braking zones, and compares accumulated longitudinal G during corner-exit acceleration.
These metrics correlate with mechanical grip and braking system effectiveness, separating cars that excel on stop-and-go tracks from those that are stronger in flowing corners.

![PITWALL](/images/page08.png)

### 5.3 Corner Performance Classification
Classifies corners by speed into low-speed, medium-speed, and high-speed categories, and computes average minimum apex speed per category.
This reveals balance under different aero-load regimes—for example, a team may be extremely fast in aero-dependent high-speed corners but struggle in mechanical-grip low-speed corners.

![PITWALL](/images/page07.png)

---

## 6. AI Prediction Models

![PITWALL](/images/page09.png)
* **FP3/FP2 → Qualifying Prediction**
    Collects practice lap times, tire compounds, and fuel-load assumptions, then uses regression models to predict each driver’s potential fastest qualifying lap.

* **Qualifying → Race Prediction**
    Based on qualifying results and historical overtaking difficulty coefficients for each circuit, it simulates race finishing-position distributions to provide expected-value references for strategy.

---

## 7. Multi-Season Analysis

### 7.1 Historical Track Map
![PITWALL](/images/page10.png)

This module combines a track map, elevation chart, and year-by-year flag statistics table. It fetches historical incident locations (X/Y coordinates) and types via API and marks them on the circuit map.
It also analyzes elevation change to help identify whether incident hotspots are located at blind corners or crested sections. The right panel summarizes Yellow/Red/SC/VSC counts over the last four seasons (2022–2025) for a macro view of track safety characteristics.

### 7.2 Season Start Reaction
![PITWALL](/images/page11.png)

Focuses on drivers’ start performance across the season, using 0–50 km/h acceleration time distribution.
It uses box plots to show median reaction/performance and stability range (IQR). This filters out extreme cases from rain starts or start incidents, reflecting true average start performance. Team-color styling is supported for easy teammate comparisons.

---

## 8. Live Timing

![PITWALL](/images/page12.png)

### 8.1 Core Monitoring

* **Ranking Tower**
    Highly optimized live leaderboard showing position, driver code, tire info, sector times (S1/S2/S3), and current state (Pitting/Out), with animated sorting and team colors.

* **Track Map**
    Live car positions on the circuit. Compared to static analysis maps, this focuses on relative positions and chasing dynamics, with lead group highlighting.

* **Circle Map**
    Abstracts the circuit into a ring to visualize gaps in seconds. This is ideal for judging whether a Safety Car window or pit window is safe.

* **Track & Weather**
    Top info bar showing event name, session time, lap progress, and track status (green/yellow/red/SC/VSC). A second row provides detailed weather: air temp, track temp, humidity, pressure, wind speed, and wind direction.

### 8.2 Strategy & Prescription

![PITWALL](/images/page15.png)

* **Driver Strategy**
    Compares predicted vs actual lap-time curves, including prediction ranges, SC regions, and pit markers to evaluate whether performance matches the model.

* **Battle Insight**
    Deep-dive analysis for a selected battle pair, computing speed delta, DRS availability, and predicted overtake lap in real time.

* **Chase Strategy**
    A chase calculator that predicts whether the chasing car can enter DRS range before the race ends, based on lap-time delta and remaining laps.

* **Pit Window**
    Estimates rejoin position after a pit stop and marks it on the map, factoring pit lane time loss and traffic conditions.

* **Tyre Strategy**
    Monitors tire age and predicted remaining life for all drivers. Combined with Pirelli degradation curves, it warns about potential performance cliffs.

### 8.3 Telemetry & Performance

![PITWALL](/images/page13.png)

* **Real-time Telemetry Traces**
    Live waveforms with multi-driver comparison:
    * `speed_trace`: Speed
    * `throttle_trace`: Throttle
    * `brake_trace`: Brake
    * `rpm_trace`: RPM
    * `gear_trace`: Gear
    * `drs_trace`: DRS state

* **Sector Comparison**
    Compares two drivers’ deltas for a selected sector (S1/S2/S3) with a dual-line design that clearly shows where gaps are created.

* **SF% History**
    Stint Fuel Saving Percentage history. Positive values indicate pushing; negative values indicate lift-and-coast fuel saving. Color intensity (bright/dark green) indicates magnitude.

* **Top Speed History**
    A per-lap top-speed table. Purple text marks personal top speed, useful for monitoring engine modes and tow effects.

### 8.4 History & Stats

![PITWALL](/images/page14.png)

* **Lap History Tables**
    Four independent tables: `Lap Time`, `S1`, `S2`, `S3`. Heatmap tables for every lap, auto-marking overall best (purple) and personal best (green).

* **Lap Time Distribution**
    Visualizes lap-time distribution across the field. Using fastest lap as a baseline, it plots gaps to the leader on the vertical axis and shows tire compound on the right to reveal group structure and dropped-back drivers.

* **Live Traffic Timeline**
    Heatmap timeline showing whether each driver is in “Clean Air” (green) or “Traffic” (orange) per lap, based on distance to the car ahead.

* **Traffic Distance**
    A statistics table quantifying traffic ratio and laps affected. Data is available only in API-only mode from JSON.

### 8.5 Others

* **Race Control**
    Live stream of race-control messages including flag changes, investigations, and penalties, with keyword filtering.

