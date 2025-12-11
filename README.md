# Multnomah Athletic Club: Membership Analytics Dashboard



## Project Overview

This project is a React-based data visualization dashboard designed to modernize membership reporting. It transitions reporting from static sheets to dynamic, interactive visualizations. 



It provides insights into the membership lifecycle, from candidate pipeline flow to financial throughput and demographic census data.



## Business Objectives

* **Pipeline Visibility:** Tracking candidates through the 5-stage governance process (Applicant → Invited).

* **Financial Integrity:** Monitoring monthly dues flux, capital fund contributions, and initiation fee audits.

* **Census Analysis:** Visualizing demographic shifts to inform retention strategies.



## Technical Highlights

* **Framework:** React.js (loaded via CDN for prototyping)

* **Visualization:** Recharts (Composed Charts, Funnels, and Bar Charts)

* **Styling:** Tailwind CSS for responsive layout

* **Icons:** Lucide-React

* **Build:** In-browser Babel transpilation (prototyping only - pinned to v7.23.5 for stability)



## Getting Started

To view the dashboard:

1. Open `index.html` directly in a modern web browser (Chrome, Firefox, Safari, or Edge)
2. Or serve it using a local web server:
   ```bash
   python -m http.server 8080
   # Then navigate to http://localhost:8080/index.html
   ```

**Note:** This is a prototyping setup using CDN-loaded libraries and in-browser Babel transpilation. For production deployment, migrate to a proper build system (Vite, webpack, or Create React App).



## Key Features

1.  **Pipeline Funnel:** Tracks volume and conversion rates across membership intake stages.

2.  **Flux Analysis:** Comparative analysis of member inflow vs. resignation outflow.

3.  **Cash Economics:** Monthly breakdown of Application Fees vs. Capital Contributions.
