# Multnomah Athletic Club: Membership Analytics Dashboard



## Project Overview

This project is a React-based data visualization dashboard designed to modernize membership reporting. It transitions reporting from static sheets to dynamic, interactive visualizations. 



It provides insights into the membership lifecycle, from candidate pipeline flow to financial throughput and demographic census data.



## Business Objectives

* **Pipeline Visibility:** Tracking candidates through the 5-stage governance process (Applicant → Invited).

* **Financial Integrity:** Monitoring monthly dues flux, capital fund contributions, and initiation fee audits.

* **Census Analysis:** Visualizing demographic shifts to inform retention strategies.



## Technical Highlights

* **Framework:** React.js

* **Visualization:** Recharts (Composed Charts, Funnels, and Bar Charts)

* **Styling:** Tailwind CSS for responsive layout

* **Icons:** Lucide-React



## Key Features

1.  **Pipeline Funnel:** Tracks volume and conversion rates across membership intake stages.

2.  **Flux Analysis:** Comparative analysis of member inflow vs. resignation outflow.

3.  **Cash Economics:** Monthly breakdown of Application Fees vs. Capital Contributions.



## Getting Started

### Quick Setup

This is a standalone HTML file that runs entirely in the browser - no build process required!

1. **Clone or download** this repository
2. **Open** `index.html` in a modern web browser
3. That's it! The dashboard will load automatically.

### Browser Requirements

For the best experience, use a modern browser with JavaScript enabled:

* **Recommended:** Chrome 90+, Firefox 88+, Safari 14+, Edge 90+
* **Minimum:** Any browser supporting ES6 and React 18

### How It Works

The dashboard uses CDN-hosted libraries loaded directly in the browser:
* React 18 (production build)
* Recharts for data visualization
* Tailwind CSS for styling
* Lucide React for icons

**No npm, no build step, no server required** - just open the HTML file!

## Deployment

### Local Viewing
Simply open `index.html` in your browser or use a local server:
```bash
# Using Python 3
python -m http.server 8000

# Using Python 2
python -m SimpleHTTPServer 8000

# Using Node.js http-server
npx http-server
```

### Web Hosting
Upload `index.html` to any static hosting service:
* GitHub Pages
* Netlify
* Vercel
* AWS S3
* Azure Static Web Apps

## Troubleshooting

### Dashboard Not Loading?
- Check browser console for errors (F12)
- Ensure you have an active internet connection (CDN resources need to load)
- Try disabling browser extensions that might block CDN resources
- Clear browser cache and reload

### Charts Not Displaying?
- Verify Recharts CDN is accessible
- Check that JavaScript is enabled in your browser
- Ensure browser supports ES6+ features

### Styling Issues?
- Confirm Tailwind CSS CDN loaded successfully
- Try hard refresh (Ctrl+F5 or Cmd+Shift+R)

## Data Updates

The dashboard currently uses static data embedded in the HTML file. To update metrics:

1. Open `index.html` in a text editor
2. Locate the data constants (e.g., `fluxData`, `pipelineData`, `financials`)
3. Update the values
4. Save and refresh your browser

## Contributing

When making changes:
1. Test in multiple browsers
2. Maintain the existing CDN-based architecture
3. Keep the file self-contained (no external dependencies beyond CDNs)
4. Follow the existing code style and structure

## Security Notes

- All external resources are loaded via HTTPS
- CDN integrity checks are recommended for production deployments
- No sensitive data should be hardcoded in the HTML file
