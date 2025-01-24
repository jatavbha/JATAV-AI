# JATAV-AI<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI Video Generator</title>
</head>
<body>
    <h1>AI Video Generator</h1>
    
    <form id="videoForm">
        <label for="textInput">Enter Text for Video (e.g., "Animals playing in the park"):</label>
        <input type="text" id="textInput" name="textInput" required>
        
        <label for="musicOption">Do you want music? </label>
        <select id="musicOption" name="musicOption">
            <option value="yes">Yes</option>
            <option value="no">No</option>
        </select>

        <button type="submit">Generate Video</button>
    </form>

    <div id="videoContainer"></div>

    <script>
        document.getElementById('videoForm').addEventListener('submit', function(event) {
            event.preventDefault();
            let text = document.getElementById('textInput').value;
            let musicOption = document.getElementById('musicOption').value;

            fetch('/generate_video', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify({ text: text, music: musicOption })
            })
            .then(response => response.json())
            .then(data => {
                if(data.video_url) {
                    let videoElement = document.createElement('video');
                    videoElement.src = data.video_url;
                    videoElement.controls = true;
                    document.getElementById('videoContainer').appendChild(videoElement);
                }
            });
        });
    </script>
</body>
</html>
