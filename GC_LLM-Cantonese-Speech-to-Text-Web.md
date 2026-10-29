Please act as an expert frontend developer. I need you to create a single-file HTML web application for a "Cantonese Speech-to-Text" (廣東話語音轉文字) tool. 

Please follow these step-by-step instructions to write the HTML and JavaScript:

\*\*Step 1: Setup Tech Stack & UI Framework\*\*  
\* Use HTML5 and Bootstrap 5 (via CDN) for the layout and styling.  
\* Create a clean, responsive interface centered on the page.  
\* Add two primary buttons: a "Start Recording" (Primary color) and a "Stop Recording" (Danger color) button.  
\* Add a visual status indicator (e.g., a badge or text) that shows whether the microphone is currently "Listening..." or "Stopped".

\*\*Step 2: Initialize Web Speech API for High Accuracy\*\*  
\* Use the browser's native \`SpeechRecognition\` or \`webkitSpeechRecognition\` API.  
\* Set the language code strictly to Hong Kong Cantonese: \`recognition.lang \= 'yue-Hant-HK';\` (or 'zh-HK').  
\* Enable continuous listening: \`recognition.continuous \= true;\` so it doesn't stop after one word.  
\* Enable interim results: \`recognition.interimResults \= true;\` to capture real-time dynamic speech.

\*\*Step 3: Build the Display Areas (Interim vs. Final)\*\*  
\* Create two separate text display areas in the UI:  
  1\. "Live Preview" (Interim Text): A slightly faded or distinct text area (e.g., a \`\<div\>\` with secondary text color) that shows what the user is currently saying in real-time.  
  2\. "Confirmed Text" (Final Text): A large \`\<textarea\>\` where the highly accurate, finalized sentences will be placed.

\*\*Step 4: Implement the Logic and Formatting\*\*  
\* In the \`onresult\` event, loop through \`event.results\`.  
\* If \`result.isFinal\` is false, update the "Live Preview" area so the user sees immediate feedback.  
\* If \`result.isFinal\` is true, append the text to the "Confirmed Text" textarea.  
\* \*\*Crucial Formatting:\*\* Whenever a final sentence is appended to the "Confirmed Text" textarea, add a double line break (\`\\n\\n\`) immediately after it. This ensures every confirmed sentence is separated by a blank line, making the content much easier to read.  
\* Clear the "Live Preview" area once the final text is processed.

\*\*Step 5: Error Handling & Edge Cases\*\*  
\* Include \`onerror\` handling (e.g., microphone permission denied).  
\* Include \`onend\` handling to gracefully update the UI status when the recording stops naturally or is stopped by the user.  
\* Make sure the script checks if the browser supports the Web Speech API before running, and show an alert if it does not.

Please generate the complete, ready-to-run HTML code in a single code block.  
