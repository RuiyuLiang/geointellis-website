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

4.  **Background Enhancement**:
    -   **Dynamic Slideshow**: Replaced the static background with an automatic image slideshow.
        -   Utilizes a dedicated `#bg-slideshow` container.
        -   Configured to cycle through images from the `BG` folder (`threeFusionBG.png`, `threeFusionBG_quarry.png`, `threeFusionBG_quarry_GEVF.png`) every 5 seconds.
        -   Implemented smooth cross-fade transitions.


5.  **data-driven visualisation solution** and **Auto-Digital Twin for Mining**
    - STAGE 1: CAD and Parameter-based mining method digital twin construction
      - GEVF Engine-driven virtual modelling for real-time visualisation and surrogate model training/Visualisation/knowledge-exchange
    - STAGE 2: Photogrammetry data pop-in and mutlimodal fusion capability
    - STAGE 3: Point cloud data pop-in and Three-Fusion Framework
    - STAGE 4: Knowledge Exchange via GEVF Engine