# GeoIntellis Website Development Log

## 2026-02-19

### Features Added
1.  **Top Navigation Bar**:
    -   Implemented a responsive navigation bar at the top of `index.html`.
    -   Added links: "our aims", "our work", "our interest", "our support", "our IPs", "about us", "Like us".
    -   Styled with a translucent background, hover animations, and mobile responsiveness.

2.  **Detail Pages**:
    -   Created individual HTML pages for each section to support the navigation links:
        -   `aims.html`
        -   `work.html`
        -   `interest.html`
        -   `support.html`
        -   `ips.html`
        -   `about.html`
        -   `like.html`
    -   Each page includes a consistent layout with a title, placeholder content, and a "Back to Home" button.

3.  **Visual Effects**:
    -   **Mouse Trail**: Added a "Magic Dust" particle effect that follows the cursor.
        -   Implemented using a secondary HTML5 Canvas (`#canvas-cursor`) to ensure it doesn't interfere with the background network animation.
        -   Particles are generated on mouse movement and fade out over time.

4.  **Hide BG**
    background-image: url('threeFusionBG.png');
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;