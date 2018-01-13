# Wit speech
Makes network request to [Wit.ai](https://wit.ai)'s speech API. For more information about the API see the [official documentation](https://wit.ai/docs/http/20170307#post--speech-link).

## Installation
```
npm install --save witspeech
```

## Usage

### Constructor
```javascript
// Import module.
const WitSpeech = require('witspeech');
// Create an instance.
const witSpeech = new WitSpeech('KEY_CLIENT', '20171207');
```

> Replace 'KEY_CLIENT' with your Client Access Token retrieved from the [wit.ai](https://wit.ai) website.

### Methods
```javascript
// The type of content that you will stream.
let contentType = 'audio/wav';
// Additional and optional web request parameters.
let queryParameters = {};
// Callback function with the response.
let callback = function(error, response) {
  if (error) {
    console.error('ERROR', error);
    return;
  }
  console.log(JSON.parse(response));
};

// Retrieves the web request to pipe information to.
witSpeech.request(
  contentType,
  queryParameters,
  callback
);
```

> To see what content types you can send over see [the official documentation](https://wit.ai/docs/http/20170307#post--speech-link).

### Example

#### From file

```javascript
// Import node module.
const fs = require('fs');

// Initialize module, see constructor section for more information.
const WitSpeech = require('witspeech');
const witSpeech = new WitSpeech('KEY_CLIENT', '20171207');

// Create request, see methods section for more information.
let request = witSpeech.request('audio/wav', {}, function(error, response) {
  if (error) {
    console.error('ERROR', error);
    return;
  }
  console.log(JSON.parse(response));
});

// Create read file stream.
let stream = fs.createReadStream('audio.wav');
// Pipe the stream to the request.
stream.pipe(request);
```

#### From microphone

```javascript
// Initialize module, see constructor section for more information.
const WitSpeech = require('witspeech');
const witSpeech = new WitSpeech('KEY_CLIENT', '20171207');

// Import audio recorder
const AudioRecorder = require('node-audiorecorder');
const audioRecorder = new AudioRecorder();

// Create request, see methods section for more information.
let request = witSpeech.request('audio/wav', {}, function(error, response) {
  if (error) {
    console.error('ERROR', error);
    return;
  }
  console.log(JSON.parse(response));
});

// Start audio recorder.
audioRecorder.start();
// Get microphone stream.
let stream = audioRecorder.stream();
// Pipe the stream to the request.
stream.pipe(request);
```

> For the audio recorder see the [package](https://npmjs.org/package/node-audiorecorder) or [repository](https://github.com/RedKenrok/Node-AudioRecorder) for it.

> For another example see the [Electron-VoiceInterfaceBoilerplate](https://github.com/RedKenrok/Electron-VoiceInterfaceBoilerplate)'s input.js.
