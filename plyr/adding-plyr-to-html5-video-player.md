## Adding Plyr to Custom HTML5 Video with Additional Features

#### Introduction
Plyr is a lightweight, accessible, and customizable media player for the web that supports HTML5 video, audio, and YouTube. This article will guide you through the process of integrating Plyr into your custom HTML5 video setup, including additional features like customizing the skin and adding a download button.

#### Prerequisites
Before starting, ensure you have basic knowledge of HTML, CSS, and JavaScript. You'll also need a code editor and a web browser for testing.

#### Step-by-Step Guide

##### Step 1: Set Up Your Project
Create a project directory and set up your HTML file. 

```plaintext
project-directory/
    ├── index.html
    └── css/
        └── styles.css
    └── js/
        └── scripts.js
```

##### Step 2: Include Plyr CSS and JavaScript
Plyr can be included via a CDN for ease of use. Add the following lines to the `<head>` section of your `index.html` file.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Custom HTML5 Video with Plyr</title>
    <!-- Plyr CSS -->
    <link rel="stylesheet" href="https://cdn.plyr.io/3.7.2/plyr.css" />
    <!-- Your custom CSS -->
    <link rel="stylesheet" href="css/styles.css">
</head>
<body>
```

Add the Plyr JavaScript at the end of the `<body>` section, along with your custom JavaScript file.

```html
    <!-- Your custom JavaScript -->
    <script src="js/scripts.js"></script>
    <!-- Plyr JavaScript -->
    <script src="https://cdn.plyr.io/3.7.2/plyr.js"></script>
</body>
</html>
```

##### Step 3: Add HTML5 Video Element
In the body of your HTML file, add a video element with custom attributes.

```html
<body>
    <video id="player" playsinline controls>
        <source src="path/to/your/video.mp4" type="video/mp4" />
        <!-- Add more sources if needed -->
    </video>
</body>
```

##### Step 4: Initialize Plyr
Now, initialize Plyr in your `scripts.js` file. This will replace the standard video player with Plyr's player.

```javascript
document.addEventListener('DOMContentLoaded', () => {
    const player = new Plyr('#player');
});
```

##### Step 5: Customize Plyr Controls
Plyr offers extensive customization options. For instance, you can customize the controls by passing an options object when initializing Plyr.

```javascript
document.addEventListener('DOMContentLoaded', () => {
    const player = new Plyr('#player', {
        controls: [
            'play-large', // The large play button in the center
            'restart', // Restart playback
            'rewind', // Rewind by the seek time (default 10 seconds)
            'play', // Play/pause playback
            'fast-forward', // Fast forward by the seek time (default 10 seconds)
            'progress', // The progress bar and scrubber for playback and buffering
            'current-time', // The current time of playback
            'duration', // The full duration of the media
            'mute', // Toggle mute
            'volume', // Volume control
            'captions', // Toggle captions
            'settings', // Settings menu
            'pip', // Picture-in-picture (currently Safari only)
            'airplay', // Airplay (currently Safari only)
            'fullscreen' // Toggle fullscreen
        ],
        settings: ['captions', 'quality', 'speed', 'loop'],
    });
});
```

##### Step 6: Add Custom CSS (Optional)
To style the Plyr player or adjust your page layout, you can add custom CSS in `styles.css`.

```css
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: #f0f0f0;
}

#player {
    width: 80%;
    max-width: 800px;
}
```

##### Step 7: Adding a Download Button
To add a custom download button, we need to extend the Plyr controls and add some custom JavaScript. Modify your Plyr initialization code in `scripts.js`:

```javascript
document.addEventListener('DOMContentLoaded', () => {
    const player = new Plyr('#player', {
        controls: [
            'play-large', // The large play button in the center
            'restart', // Restart playback
            'rewind', // Rewind by the seek time (default 10 seconds)
            'play', // Play/pause playback
            'fast-forward', // Fast forward by the seek time (default 10 seconds)
            'progress', // The progress bar and scrubber for playback and buffering
            'current-time', // The current time of playback
            'duration', // The full duration of the media
            'mute', // Toggle mute
            'volume', // Volume control
            'captions', // Toggle captions
            'settings', // Settings menu
            'pip', // Picture-in-picture (currently Safari only)
            'airplay', // Airplay (currently Safari only)
            'download', // Custom download button
            'fullscreen' // Toggle fullscreen
        ],
        settings: ['captions', 'quality', 'speed', 'loop'],
    });

    // Adding event listener to the custom download button
    const downloadButton = document.createElement('button');
    downloadButton.classList.add('plyr__control');
    downloadButton.innerHTML = '<svg role="presentation" focusable="false"><use xlink:href="#plyr-download"></use></svg>';
    downloadButton.addEventListener('click', () => {
        const videoSrc = document.querySelector('#player source').src;
        const a = document.createElement('a');
        a.href = videoSrc;
        a.download = 'video.mp4';
        document.body.appendChild(a);
        a.click();
        document.body.removeChild(a);
    });

    // Insert the download button before the fullscreen button
    const controls = player.elements.controls;
    const fullscreenButton = controls.querySelector('.plyr__control--fullscreen');
    controls.insertBefore(downloadButton, fullscreenButton);
});
```

##### Step 8: Customize the Skin
To customize the skin of Plyr, you can override the default CSS rules in `styles.css`.

```css
/* Change the color of the play button */
.plyr--full-ui .plyr__control--overlaid {
    background: #1e90ff;
}

/* Customize the progress bar */
.plyr--full-ui .plyr__progress__container {
    background: #d3d3d3;
}

.plyr--full-ui .plyr__progress__buffer {
    background: #a9a9a9;
}

.plyr--full-ui .plyr__progress__played {
    background: #1e90ff;
}
```

#### Conclusion
You have successfully integrated Plyr into your custom HTML5 video setup, customized the controls, added a download button, and customized the skin. Plyr provides a sleek, consistent, and feature-rich media player that enhances the user experience. For more advanced configurations and updates, refer to the official [Plyr documentation](https://github.com/sampotts/plyr).

By following this guide, you can provide a highly customizable and user-friendly video playback experience on your website.

---

### Useful Links

- https://codexdindia.blogspot.com/2021/05/plyrio-video-player-integration-skin-Customizing-and-Adding-Download-Button-to-plyr.html
- https://dev.to/sh20raj/sample-videos-for-testing-4a30
