# WarDragon ATAK Plugin

ATAK plugin for integrating with WarDragon/DragonSync drone detection systems.

## Features

### Multi-Source Detection
- Connects to one or more WarDragon/DragonSync API endpoints
- Shows per-kit status (up/down + last seen)
- Displays drone and aircraft detections with RID information
- Learns kits via CoT (discovered kits) and can run CoT-only without API
- Uses CoT when live to reduce API polling

### Alert Zones
Geographic areas of interest that trigger multi-modal alerts when drones, aircraft, or signals enter:

- **Create zones** by tapping the map after clicking "+ Add Zone"
- **Configure per-zone**: name, radius, alert triggers (drones/aircraft/signals)
- **Color picker** with 5 tactical presets:
  - Yellow-Amber (default) - monitoring state
  - Blue - friendly/informational
  - Green - safe/permissive zones
  - Purple - special/custom
  - Cyan - airspace/altitude
- **Directional threat highlighting** - red wedge/sector shows bearing to threats
  - Single threat: 30° wedge pointing toward threat
  - Multiple threats: wedge expands to cover all
  - Threats spread >180°: full circle flash
- **Multi-modal alerts**: vibration, sound, toast notification
- **Global settings**: enable/disable, re-alert cooldown, vibrate/sound toggles
- Maximum 20 zones, persisted across ATAK restarts

### Track Management
- Filter by: All / Drones / Aircraft / Signals
- Track detail view with Replay to step through history
- Status tags: Authorized / Unknown / Unauthorized (persisted per-track)
- Configurable TTL to auto-expire stale tracks
- Sort by Latest or Stable (first-seen order)

### Map Integration
- Automatic markers for detected drones, pilots, and home locations
- Zone circles rendered on map with configurable colors
- Focus buttons to pan map to track/zone locations

## Requirements

- ATAK-CIV 5.6.x (built against SDK 5.6.0)
- Android 8+
- DragonSync running on the kit (WarDragon Pro ships with it)

## Install

1. Download the APK from GitHub Releases:
   - Release page: https://github.com/alphafox02/WarDragon-ATAK-Plugin/releases
   - Current version: **0.3** (ATAK-Plugin-WarDragon-0.3-5.6.0-civ-release.apk)
   - SHA256: `74dc27810a1f6aea23235c6f39a84bbed4b79f641b7bfc6f7a16ee14b6a27a75`
2. Sideload onto your ATAK device and enable the plugin.
3. The plugin icon is a monochrome dragon head.

## Quick Start

1. Ensure DragonSync is running on the WarDragon box
2. Ensure the phone and WarDragon are on the same network
3. Open ATAK → WarDragon plugin
4. Go to **Assets** → **Manage**
5. Enter **Name**, **Host**, **Port** (default 8088) → **Add/Update**
6. Select the kit in the list to view **Status**, **Tracks**, and **Config**
7. If CoT is already arriving, use **Manage → Discovered** to add a kit without IP/port (CoT-only)

## Tab Reference

### Assets Tab
- Lists known WarDragon kits and their connection status
- Tap a kit row to select it (used by Tracks/Config tabs)
- Tap expand chevron to see details and **Focus WD**
- Counts `D/A/S` show detections for that specific kit
- **Manage** button to add/edit endpoints

### Tracks Tab
- Filter selector: **All / Drones / Aircraft / Signals**
- Tap a row to expand track details
- Expanded view includes **Track / Pilot / Home** buttons for map focus
- **Replay** steps through recent history points
- Sort toggle: **Latest** (default) vs **Stable** (first-seen order)
- Status tags (Authorized/Unknown/Unauthorized) via overflow menu
- RID make/model/source shown when provided by DragonSync

### Zones Tab
- **Enable zone alerts** - master toggle for all zone alerts
- **+ Add Zone** - tap then tap map to set zone center
- Zone list with enable/disable toggle per zone
- Zone menu (⋮): Edit, Focus, Delete
- **Alert Settings**:
  - Re-alert after: cooldown in seconds (default 60)
  - Vibrate on alert: toggle
  - Sound on alert: toggle

### Config Tab
- Displays config from the selected kit (API required)
- **Track refresh interval** (seconds)
- **Stale tracks TTL** (minutes) - 0 = keep forever
- **Apply TTL to CoT tracks** toggle
- **Diagnostics** toggle for CoT debug info
- **Check Updates** calls the WarDragon API for git update status

## Zone Alert Behavior

When a track enters an enabled zone:

1. **Visual** - Red sector/wedge highlights the threat direction on the map
2. **Toast** - "Zone Alert: [name] - [type] detected ([distance]m)"
3. **Vibration** - 3-pulse pattern (if enabled)
4. **Sound** - 3 beeps (if enabled)

Alerts respect the re-alert cooldown to avoid spam from the same track.

## Screenshots

![Plugin on phone](plugin.jpeg)
![Plugin on tablet](tablet.jpeg)

## Notes / Limitations

- Designed for WarDragon Pro. Requires DragonSync on the kit.
  DragonSync project: https://github.com/alphafox02/DragonSync
- If the API is unreachable, status shows **Down**
- CoT-only kits show status/detections but no config until API is configured
- CoT comes from DragonSync; the plugin does not inject CoT
- Zone alerts require tracks to have valid lat/lon coordinates
- Signals support is a placeholder (coming when API exposes it)

## Troubleshooting

If the plugin shows "Failed to fetch," check:
- IP/Port in **Manage**
- Phone and WarDragon on same network
- DragonSync API running

If zones disappear after restart:
- This was fixed in recent versions using application context for storage
- Update to the latest plugin version

## Future Enhancements

- Sector/arc-shaped zones (half-circles, quarter-circles)
- Polygon zones (non-circular)
- Altitude filtering for zones
- Import/export zones
- Zone-specific sound selection
- Signals support when API exposes it
- Optional long-term history persistence

## Releases & Source

- Binary-only distribution. Source code is not published at this time; licensing may change in the future.
- Copyright © 2025 CEMAXECUTER LLC. All rights reserved.
- If you installed any early pre-release builds, uninstall them before installing this release (signing keys changed).

## Support

- Issues/feedback: open a GitHub issue.
