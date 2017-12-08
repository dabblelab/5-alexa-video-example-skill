# Video Skill Demo

## Overview
The VideoApp interface allows native video files to be streamed in Echo Show. This video provides an introduction to the VideoApp interface using the Alexa Skills Kit SDK for Node.JS.

### Topics Covered
- Things to note
  - Fire TV devices don't support the VideoApp interface
  - Supported video formats are: HLS and H.264
- Configure your skill to implement the VideoApp interface
  - from the developer portal
  - in the `skill.json` schema (for the ASK-CLI)
  ```json
  "apis": {
    "custom": {
      "endpoint": {
        "sourceDir": "lambda/custom"
      },
      "interfaces": [
        {
          "type": "RENDER_TEMPLATE"
        },
        {
          "type": "VIDEO_APP"
        }
      ]
    }
  }
  ```
- Hosting your video files

- Checking for video support
 ```javascript
 if (this.event.context.System.device.supportedInterfaces.VideoApp) {
   //video supported

 } else {
   //video not supported

 }
 ```

- Complete intent example

```javascript
'PlayVideoIntent': function() {

  if (this.event.context.System.device.supportedInterfaces.VideoApp) {
    this.response.speak("Okay. Here is an example video.");
    let meta = {
      title: "Video from pixabay.com",
      subtitle: "Used under creative commons."
    }
    this.response.playVideo('https://s3.amazonaws.com/media.dabblelab.com/video/brooks-river-crystal-clear-10427.mp4', meta);
  } else {
    this.response.speak("The video cannot be played on your device. To watch this video, try launching this skill from an echo show device.");
  }

  this.emit(':responseReady');
}
```
### Resources
[VideoApp Interface Reference](https://developer.amazon.com/docs/custom-skills/videoapp-interface-reference.html)
