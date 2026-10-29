Date : 20261029
Generate code


You are an expert full-stack web developer and UI/UX designer. Your task is to build a fully functional, single-file HTML5 web application that acts as a Traditional Chinese (Big5) Text-to-Speech (TTS) converter and client-side audio recorder/downloader.

Please build the application adhering strictly to the following technical requirements and design specifications:

\#\#\# 1\. User Interface & Layout (HTML / CSS)

\*\*Design:\*\* Clean, modern, accessible responsive interface (using Tailwind CSS via CDN or clean vanilla CSS styling with flexbox/grid).  
\*\*Text Input:\*\* A large resizable \<textarea\> pre-filled with a sample Traditional Chinese Big5 text snippet (e.g., mixing Cantonese and Mandarin idioms).  
\*\*Voice / Language Selection Dropdown (\<select\>):\*\*  
  \- Cantonese (Hong Kong: zh-HK)

  \- Cantonese (Macau: zh-MO)

  \- Mandarin (Taiwan / Traditional Big5: zh-TW)

  \- Mandarin (Mainland China: zh-CN)

  \- US English (en-US)

  \- UK / London English (en-GB)

\*\*Controls & Buttons:\*\*  
  \- "Speak (Native)" button: Plays audio instantly using the browser's window.speechSynthesis API.

  \- "Stop" button: Instantly halts speech synthesis and recording.

  \- "Record & Save Audio (.webm / .mp3)" button: Captures the speech stream using navigator.mediaDevices.getDisplayMedia or MediaRecorder loopback so the user can download the generated voice output locally.

  \- Audio speed slider (rate: 0.5x to 2.0x) and pitch slider (0.5 to 2.0).

\#\#\# 2\. Core Functionality & JavaScript Implementation

\*\*Dynamic Voice Mapping:\*\* On window load and speech synthesis voicechanged events, query window.speechSynthesis.getVoices() and automatically map the selected language/accent dropdown value to the most appropriate native OS voice available (prioritizing high-quality or local neural voices when present).  
\*\*Client-Side Audio Recording:\*\*   
  \- When the user clicks "Record & Save", prompt the user to capture the browser tab/system audio.

  \- Initialize a MediaRecorder instance using browser-supported audio mime types (audio/webm or audio/mp4).

  \- Automatically trigger speech synthesis using the configured utterance parameters while recording is active.

  \- When speech ends or the user clicks stop, compile the recorded audio chunks into a Blob, generate a temporary object URL, and automatically trigger a client-side file download (.webm or .mp4/audio file).

\*\*Error Handling & Fallbacks:\*\* Gracefully handle permissions denial (e.g., if user cancels tab audio sharing) with a clear notification message explaining how to retry or use native playback mode.

\#\#\# 3\. Deliverable Format

Provide the complete, self-contained, production-ready code inside a single \`\`\`html code block so it can be saved directly as \`index.html\` and opened locally in any modern browser without external build tools or backend servers.

