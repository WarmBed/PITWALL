# PITWALL


## What is this?

PitWall is an  **F1 data analysis** and telemetry visualization tool.  
It allows  data fans to analyze lap times, throttle usage, speed traces, and driver comparisons using real Formula 1 telemetry.


A professional Formula 1 telemetry analysis workstation providing comprehensive race data analysis capabilities.

![F1 data analysis telemetry visualization tool](/images/Live_timing.png)

## 🌟 Features Overview

### Latest Features: Live Timing

Full race replay functionality with real-time race status display, including:
- **Track Map**: Visual circuit representation with driver positions
- **Circle Map**: Circular track visualization for position tracking
- **Lap Time Distribution**: Statistical lap time analysis across all drivers
- **Pit Windows**: Evaluate potential position after pit stop (who will be ahead/behind)
- **Driver Strategy**: Predict lap time performance with fuel weight and tire degradation calculations
- **Speed Trace**: Compare driver speeds at every track position
- **Battle Insight**: Real-time overtake probability analysis with consecutive catching detection
![F1 data analysis telemetry visualization tool](/images/Live_timing_Detial.png)



- **Relay**:
![F1 data analysis telemetry visualization tool](/images/replay.png)

- **P1% & OT%** :
![F1 data analysis telemetry visualization tool](/images/Live_ranking.png)

> ⚠️ **Note**: Real-time mode is currently in testing and stability cannot be guaranteed. Please use with caution.

### Core Analysis Modules
Dynamic dashboard providing real-time season overview
- **Season Progress**: Track completed and upcoming races throughout the season
- **Weather Timeline**: Race weather forecast for the next upcoming event
- **Constructor Standings**: Live team championship rankings and points
- **Driver Standings**: Current driver championship positions and statistics
- **Smart Layout**: Three-column arrangement (left split: progress/weather, middle: constructor, right: driver)
- **Auto-Update**: Automatically selects current season data and next race information
![F1 data analysis telemetry visualization tool](/images/welcome.png)

#### 🌧️ Rain Analysis Module
Analyzes meteorological conditions throughout the race
- **Temperature variation** per lap
- **Rainfall tracking** and trends
- **Weather impact** on race strategy

#### 🏁 Lap Analysis Module
In-depth single-lap performance analysis
- Driver lap time comparison
- Fastest lap analysis
- Comprehensive telemetry data
- Cross-Session Telemetry Comparison Enhanced telemetry analysis modules now support Q vs R session comparison, enabling qualifying-to-race performance analysis across all 9 telemetry modules (Speed, Brake, Throttle, Gear, RPM, Acceleration, Speed Diff, Time Diff, Distance Diff)
![F1 data analysis telemetry visualization tool](/images/Lap.track.png)

**Sub-modules:**
- ⚡ **Speed Analysis** - Velocity tracking and comparison
- 🛑 **Brake Analysis** - Braking pressure and points
- ⚡ **Throttle Analysis** - Accelerator pedal position
- ⚙️ **Gear Analysis** - Gear shifting patterns
- 🔄 **RPM Analysis** - Engine speed monitoring
- 📈 **Acceleration** - G-force analysis
- 📊 **Speed Differential** - Speed difference tracking
- 📏 **Distance Differential** - Cumulative distance gap

#### 🚀 Throttle Analysis Module 
Comprehensive throttle usage analysis and comparison

**Throttle Line Chart:**
- **Dual-driver comparison**: Compare throttle usage patterns between two drivers
- **Per-lap percentage**: Visualize full throttle usage percentage for each lap
- **Interactive tooltips**: Draggable tooltips with detailed lap information
- **System settings integration**: Customize display preferences
- **Driver 2 optimization**: Optional second driver selection (defaults to None)

**Throttle Box Plot:**
- **Statistical distribution**: Box plot visualization of throttle usage across all drivers
- **Percentage modes**: Toggle between actual percentage or lap percentage display
- **Min/Max tooltips**: Hover to see extreme values and outliers
- **Multi-driver comparison**: Analyze throttle patterns for entire grid


![F1 data analysis telemetry visualization tool](/images/throttle.png)

**Key Features:**
- 📊 Lap-by-lap throttle usage tracking
- 🎯 Dual-driver comparison with independent selection
- 🖱️ Draggable legend and pinnable data points
- 📈 Real-time data point tooltips with drag support
- ⚙️ Configurable through System Settings dialog
- 🎨 Team-based color schemes

#### 🏎️ Pitstop Analysis Module
Strategic pitstop efficiency evaluation
- Pitstop duration statistics
- Stop frequency comparison
- Team efficiency metrics

![F1 data analysis telemetry visualization tool](/images/pitstop.accidient.png)

#### 🗺️ Track Analysis Module
Interactive track visualization
- Circuit trajectory display
- Driver position markers
- Zoom and pan support

#### 🚗 Detailed Lap Analysis
Advanced lap time data analysis
- Detailed lap time tables
- Box plot visualizations
- Statistical distribution analysis

![F1 data analysis telemetry visualization tool](/images/tire.lap.detailed.rain.png)

#### 🔥 Accident Analysis Module
Race incident investigation
- Incident timestamps
- Involved drivers
- Impact assessment

#### 🏁 Tire Strategy Analysis
Tire usage and strategy evaluation
- Compound selection analysis
- Degradation curves
- Pit stop timing optimization

#### 📊 Ideal Lap Analysis Module 
Comprehensive theoretical best lap analysis and sector comparison

**Ideal Lap Ranking Table:**
- **Complete Grid Analysis**: Theoretical best lap times for all drivers
- **Statistical Metrics**: Median, range, and gap calculations
- **Team Color Coding**: Visual driver identification with standardized colors
- **Session Summary**: Fastest laps and perfect lap achievement rates
- **Sector Breakdown**: Individual sector performance with visual indicators (✓ = optimal, ✗ = improvable)
- **API Integration**: Real-time data from F1T API

**Ideal Lap Sector Comparison:**
- **Sector-by-Sector Analysis**: Detailed S1, S2, S3 delta comparison
- **Cumulative Delta Visualization**: Bar chart showing total improvement potential
- **Sortable Columns**: Click to sort by any sector or cumulative delta
- **Color-Coded Performance**: Unified color standards for gap displays
![F1 data analysis telemetry visualization tool](/images/Ideal_Lap.png)


**UI Refinements** 
- ✅ Sector marks with color separation (green ✓, black ✗)
- ✅ Unified color standards for all gap displays (0.2s, 0.5s thresholds)
- ✅ Sortable cumulative delta in sector comparison table

###  Version: V0.8.0 (2025-11-15)

**Major Features:**
- ✅ **Historical Circuit Analysis**: Comprehensive historical flag statistics (Yellow/Red/SC/VSC) for all circuits from 2022-2025, providing strategic insights into track characteristics and incident patterns

![F1 data analysis telemetry visualization tool](/images/trackmap.png)


**Technical Improvements:**
- Unified translation system using `tr()` function across all telemetry modules
- Translation key standardization (`driver_1_info`, `driver_2_info`, `race_info`, `driver_info`, `versus`)
- Enhanced data loader architecture supporting cross-session parameter management



###  Version: V0.7.0 (2025-11-08)

**Major Features:**
- ✅ **Driver Race Position Analysis**: Track position changes during race with start/finish/best/worst rankings and visual indicators (▲▼━)
- ✅ **Qualifying Prediction Module**: ML-based FP3→Q prediction using XGBoost v3.10 track-specific models with R²/MAE metrics
![Qualifying Prediction Module](/images/QualifyingPrediction.png)

- ✅ **Vehicle Parts Changes Analysis**: FIA technical document parsing with 15 main categories, 61 sub-categories, and multi-filter system
![Vehicle Parts Changes Analysis](/images/Vehicle Parts Changes.png)

###  Version: V0.6.0 (2025-10-27)

**Major Features:**
- ✅ **Track Map Enhancement - Corner Numbering**: Added corner number annotations to track map visualization for improved position identification and reference during analysis
- ✅ **Corner Analysis Module - Dynamic Speed Distribution**: Implements dynamic corner classification system (low/medium/high-speed corners) with speed distribution analysis for three critical phases (entry/apex/exit speed)

**UI Refinements:**
- 🎨 Corner number overlays on track map with optimal positioning
- 🎨 Speed distribution plots with color-coded corner classifications
- 🎨 Entry-Apex-Exit phase comparison visualization

**Technical Improvements:**
- Dynamic corner detection algorithm based on speed thresholds
- Multi-phase telemetry data extraction and processing
- Statistical distribution analysis for corner performance metrics

![F1 data analysis telemetry visualization tool](/images/corner.png)
### Previous Version: V0.5.0 (2025-10-25)

**Major Features:**
- ✅ **Startup Interface Enhancement**: Improved initialization screen with progress indicators and loading status to provide better user feedback during application launch
![F1 data analysis telemetry visualization tool](/images/initialize.png)
- ✅ **Workspace Management System**: Complete workspace functionality allowing users to save current window layouts, analysis configurations, and restore them on next startup
![F1 data analysis telemetry visualization tool](/images/workspace.png)
- ✅ **Tab Pop-out Feature**: Enhanced tab system with support for detaching tabs into independent floating windows for multi-monitor workflows
![F1 data analysis telemetry visualization tool](/images/popout.png)
**UI Refinements:**W
- 🎨 Startup progress bar with detailed loading stages
- 🎨 Workspace save/load dialog with preview functionality
- 🎨 Tab drag-and-drop support for window detachment
- 🎨 Independent window management for detached analysis modules

#### 🚗 All Drivers Straight Line Speed Analysis (Experimental)
Comprehensive straight-line acceleration and maximum speed analysis for all drivers
- **Maximum Speed Tracking**: Peak velocity achieved on track straights
- **Segment-based Analysis**: Track-specific speed zones and acceleration corridors
- **Performance Visualization**: Bar charts showing relative acceleration times
- **Team Color Coding**: Visual driver identification with standardized team colors
- **Sortable Data Tables**: Click-to-sort functionality for all performance metrics
![F1 data analysis telemetry visualization tool](/images/all_driver_speed .png)

#### 🛑 All Drivers Brake Performance Analysis (Experimental)
Detailed braking efficiency and deceleration analysis across the entire grid
- **Maximum Deceleration**: Peak G-force values during braking zones
- **Brake Distance Analysis**: Distance required for speed reduction
- **Brake Time Measurement**: Duration of braking events
- **Speed Reduction Tracking**: Start/end speeds for braking zones
- **Visual Performance Bars**: Brake time visualization with relative scaling
- **Reference Zone Display**: Track-specific brake zone distance markers
![F1 data analysis telemetry visualization tool](/images/all_driver_brake.png)


**Technical Improvements:**
- Workspace serialization system for MDI layout persistence
- Tab window state management with geometry preservation
- Multi-window coordination for synchronized parameter updates
- Enhanced splash screen with real-time initialization feedback

### Previous Version: V0.4.0 (2025-10-13)
**Major Features:**
- ✅ **Ideal Lap S1/S2/S3 Display**: Complete sector time display for ideal lap analysis modules (sector heatmap, comparison chart, ranking table)
- ✅ **Time-Axis Mode for Lap Analysis**: Time-based X-axis option for all telemetry charts (speed, brake, throttle, RPM, gear, acceleration)
- ✅ **Time Diff Analysis Module**: New dedicated module for lap time difference analysis with cumulative delta visualization
- ✅ **Welcome Page Dashboard**: Integrated dashboard displaying driver standings, constructor standings, season progress, and weather timeline

**UI Refinements:**
- 🎨 S1/S2/S3 sector time display in ideal lap sector heatmap
- 🎨 Time-axis toggle available in lap analysis chart widgets
- 🎨 Welcome page with real-time championship standings and weather forecast

**Technical Improvements:**
- Time data extraction in telemetry data loader base (`_extract_time_data()`)
- `set_time_axis_mode()` method implemented across all lap analysis modules
- Time diff analysis MDI, data loader, and chart widget architecture
- Welcome tab creation with multiple MDI integration (`create_welcome_tab()`)

**Bug Fixes:**
- ✅ **EXE Language Switching Fixed**: Language configuration now persists correctly in EXE mode using user directory (`~/.f1telemetrystation/`)
- ✅ **PyInstaller Module Coverage**: Updated `F1T_GUI.spec` hiddenimports from 48 to 125 modules for complete Japanese menu support

### Previous Version: V0.3.0 (2025-10-10)
**Major Features:**
- ✅ **Ideal Lap Ranking Analysis**: Comprehensive theoretical best lap comparison for all drivers
- ✅ **Ideal Lap Sector Comparison**: Detailed sector-by-sector performance analysis with cumulative delta visualization
- ✅ **Interactive Lap Analysis Tree**: Hierarchical lap data view with smart filtering and click-to-analyze functionality
- ✅ **Box Plot Typography Standardization**: Unified 8pt font across all chart elements for consistency

**UI Refinements:**
- 🎨 Sector marks with mixed color display (green ✓ for optimal, black ✗ for improvable)
- 🎨 Unified color standards for gap displays (0.2s, 0.5s thresholds)
- 🎨 Sortable cumulative delta column in sector comparison table
- 🎨 Team color coding with black text for better readability

**Technical Improvements:**
- Custom `SectorMarksDelegate` for per-character color rendering
- Shared color configuration module for visual consistency
- Enhanced sorting functionality with dual DisplayRole/UserRole data
- API-first data loading architecture

### Previous Version: V0.2.1 (2025-10-09)
- Colour palette system gains API-only mode toggle
- Refreshed 2025 team/driver colours with API fallback hardening
- Lap/Throttle box plots now render median & outliers in black
- Main window and packaging metadata bumped to V0.2.1

### Previous Version: V0.2.0 (2025-10-08)
- Added Throttle Analysis Module (Line Chart + Box Plot)
- Enhanced tooltip system with drag support
- Improved dual-driver comparison
- Multiple bug fixes and UI improvements

### Legacy Version: V0.1.0
- Initial release with core analysis modules
- Basic telemetry analysis
- MDI workspace system


## 🔗 Special Features

### Linkage System
- **X-axis Synchronization**: Multiple telemetry charts display the same position
- **Click Linkage**: Click on one chart, others follow automatically
- **Master Toggle**: Global enable/disable for linkage functionality

### Workspace Management
- **Save Workspace**: Preserve current analysis configuration
- **Load Workspace**: Quickly restore previous analysis environment
- **Multi-tab Support**: Open multiple analysis perspectives simultaneously

### MDI Window System
- **Free Arrangement**: Drag and resize windows freely
- **Cascade/Tile**: Quick window layout organization
- **Pop-out Feature**: Display analysis windows independently

### Enhanced Chart Interactions (NEW in V0.2.0)
- **Draggable Tooltips**: Pin and drag tooltip boxes to any position
- **Data Point Pinning**: Click to pin data points with persistent tooltips
- **Connection Lines**: Dashed lines connecting tooltips to original data points
- **Dual-driver Tooltip Separation**: Independent tooltips for each driver's data
- **Draggable Legend**: Reposition chart legends for better visibility

## 🌐 System Highlights

- **Multi-language Support**: 中文 🇹🇼 / English 🇺🇸 / 日本語 🇯🇵
- **API-ONLY Mode**: Data retrieval exclusively through REST API 
- **Parameter Synchronization**: Sync year/race/session settings between main and sub-windows
- **Modular Design**: Independent and extensible analysis modules
- **Dynamic Import Architecture**: Optimized memory usage with on-demand module loading


## 👥 Contributing

Contributions are welcome! Please feel free to submit pull requests or open issues for bugs and feature requests.


## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgments

- [FastF1](https://github.com/theOehrly/Fast-F1) API Contributors
- [OpenF1](https://openf1.org/) API Contributors
- PyQt5 Framework
- All contributors and testers

## 📧 Contact

- **GitHub**: [WarmBed/F1-TelemetryStation-Pro](https://github.com/WarmBed/F1-TelemetryStation-Pro)
- **Issues**: [Report a Bug](https://github.com/WarmBed/F1-TelemetryStation-Pro/issues)


---

**Made with ❤️ for F1 enthusiasts and data analysts**

**Star ⭐ this repository if you find it useful!**
