# OrbitAlign - Satellite Dish Alignment Tool

A mobile-first web app to help users align satellite dishes with geostationary satellites. Works entirely client-side with no build process or server required - perfect for GitHub Pages deployment.

## Features

- **GPS Location Support**: Automatically get your location from your mobile device, or enter coordinates manually
- **Comprehensive Satellite Database**: 80+ satellites including popular ones for:
  - Australia (Optus, NBN Sky Muster)
  - Malaysia/SE Asia (MEASAT, Astro, AsiaSat, Thaicom)
  - Europe (Astra, Eutelsat Hot Bird)
  - Americas (Viasat, DirecTV, Dish Network)
- **Smart Filtering**:
  - Filter satellites by region (Oceania, Asia, Europe, Americas)
  - Show only satellites visible from your location
  - Search by satellite name or description
- **Visual Alignment Guides**:
  - Compass view showing azimuth direction
  - Elevation view showing dish tilt angle
  - LNB skew rotation indicator
- **Below Horizon Warning**: Alerts when a satellite cannot be seen from your location

## How to Use

1. **Set Your Location**: 
   - Tap "Use GPS" to get your location automatically, or
   - Enter your latitude and longitude manually

2. **Select a Satellite**:
   - Search for a satellite by name
   - Filter by region using the buttons
   - Enable "Show only visible satellites" to hide satellites below your horizon
   - Or enter the satellite's orbital longitude directly

3. **Align Your Dish**:
   - **Azimuth**: Point your dish in this compass direction (from True North)
   - **Elevation**: Tilt your dish up by this angle from horizontal
   - **Skew**: Rotate your LNB by this angle (positive = clockwise when looking at dish from behind)

## Understanding the Calculations

### Azimuth
The horizontal direction to point your dish, measured in degrees clockwise from True North (0-360°). If using a magnetic compass, you'll need to adjust for your local magnetic declination.

### Elevation  
The vertical angle to tilt your dish above the horizon (0° = horizontal, 90° = straight up). A negative elevation means the satellite is below the horizon and cannot be received.

### Skew (Polarization Tilt)
The rotation angle of the LNB to align with the satellite's polarization. This compensates for your position relative to the satellite and ensures optimal signal reception.

## Technical Notes

### Math Formulas Used

**Elevation:**
```
el = arctan((cos(L)×cos(ΔG) - r) / √(1 - (cos(L)×cos(ΔG))²))
```
Where:
- L = user latitude
- ΔG = longitude difference (user - satellite)
- r = Earth radius / satellite orbital radius ≈ 0.1513

**Azimuth:**
```
az = 180° + arctan2(tan(ΔG), sin(L))  [Northern hemisphere]
az = arctan2(tan(ΔG), sin(L))         [Southern hemisphere, normalized to 0-360°]
```

**Skew:**
```
skew = arctan(sin(ΔG) / tan(L))
```

### Satellite Orbital Parameters
- Geostationary orbit altitude: ~35,786 km above equator
- Orbital radius from Earth center: ~42,164 km
- All geostationary satellites are positioned above the equator (0° latitude)

## Deployment

This app runs entirely in the browser with no dependencies. To deploy:

1. Push to a GitHub repository
2. Enable GitHub Pages in repository settings
3. Access at `https://yourusername.github.io/repository-name/`

## Browser Support

Works on all modern browsers. GPS functionality requires:
- HTTPS connection (or localhost)
- User permission for location access

## License

MIT License - Free to use and modify.
