# GitHub Location Filter

A Tampermonkey userscript that makes GitHub job listing tables user-friendly by adding location-based filtering. Perfect for browsing careers pages where you need to quickly find positions in specific cities or remote opportunities. The script automatically detects job tables and provides an intuitive filtering interface.

## Features

- **Smart Detection**: Only activates when it detects tables with location columns (location, city, office)
- **Customizable Cities**: Add/remove cities through an intuitive dropdown interface
- **Persistent Storage**: Remembers your city preferences and filter state across sessions
- **Toggle Filter**: Easy on/off toggle with visual status indicators
- **Dark Mode Support**: Automatically adapts to your system's dark mode preference
- **Dynamic Content**: Works with dynamically loaded tables (AJAX content)
- **Flexible Matching**: Supports various location text formats and separators

## Installation

### Option 1: Easy Installation via Greasy Fork (Recommended)
Click this button:

[![Install](https://img.shields.io/badge/Install-Greasy%20Fork-brightgreen)](https://greasyfork.org/en/scripts/547666-github-location-filter)

### Option 2: Manual Installation

**Steps:**
1. Install a userscript manager [Tampermonkey](https://www.tampermonkey.net/), [Greasemonkey](https://www.greasespot.net/), or [Violentmonkey](https://violentmonkey.github.io/)
2. Create a new script
3. Copy and paste the contents of `github-location-filter.user.js`
4. Save the script


## Usage

### Basic Usage

1. Navigate to any GitHub page with tables containing location data
2. The location filter interface will automatically appear in the top-right corner
3. Click on the interface header to expand the dropdown
4. Add cities you want to filter by using the "Add City" input field
5. Toggle the filter ON/OFF using the toggle button

### Interface Controls

- **Header Click**: Expand/collapse the filter interface
- **Toggle Button**: Turn filtering ON/OFF
- **Add City Input**: Type city names and press Enter or click "Add"
- **City Tags**: Click the "×" button to remove cities from the filter
- **Visual Status**: The interface changes color when filtering is active (blue → green)

### City Matching

The script uses exact (case insensitive) matching to find locations:
- **Exact matches**: "Remote", "San Francisco"
- **Case insensitive**: "remote" matches "Remote", "REMOTE"

## Configuration

### Default Cities

The script starts with `['remote']` as the default city. You can modify this by editing the `targetCities` array in the script:

```javascript
let targetCities = ['remote', 'san francisco', 'new york'];
```

### Supported Websites

Currently configured for GitHub (`@match https://github.com/*`), but can be extended to other sites by modifying the `@match` directive:

```javascript
// @match        https://github.com/*
// @match        https://example.com/*
```

## Technical Details

### Storage

The script uses Tampermonkey's `GM_setValue` and `GM_getValue` functions to persist:
- **Cities list**: Your custom city preferences
- **Filter state**: Whether filtering was enabled when you last used it

### Column Detection

Automatically detects location columns by searching for headers containing:
- "location"
- "city" 
- "office"

### Performance

- Minimal performance impact - only processes tables with location columns
- Uses efficient DOM queries and caching
- Observes DOM changes to handle dynamic content
