# FitMind AI Backend

This is the backend for the FitMind AI chatbot application. It provides APIs for file upload, chat functionality, URL processing, podcast processing, and WhatsApp integration.

## Getting Started

### Prerequisites

- Node.js (v14 or later)
- npm (v6 or later)

### Installation

1. Clone the repository:
   ```
   git clone https://github.com/RaheesAhmed/FitMindAIChatbot
   cd backend
   ```

2. Install dependencies:
   ```
   npm install
   ```

3. Create a `.env` file in the root directory and add the following environment variables:
   ```
   PORT=3000
   OPENAI_API_KEY=your_openai_api_key
   VECTOR_STORE_PATH=vectorStore.index
   UPLOADS_DIR=uploads
   WHATSAPP_API_KEY=your_whatsapp_api_key
   WHATSAPP_BUSINESS_ACCOUNT_ID=your_whatsapp_business_account_id
   WHATSAPP_ACCESS_TOKEN=your_whatsapp_access_token
   ```

4. Start the server:
   ```
   npm start
   ```

## API Endpoints

### File Upload and Processing

1. **POST** `/api/file/upload`
   - Upload files for processing
   - Use multipart/form-data with a field named "files"
   - Returns: `{ message: "Files uploaded and processed successfully" }`

2. **POST** `/api/file/set-prompt`
   - Update the AI prompt
   - Body: `{ "prompt": "Your new prompt here" }`
   - Returns: `{ message: "Prompt updated successfully" }`

3. **POST** `/api/file/process-url`
   - Process a URL and extract its content
   - Body: `{ "url": "https://example.com" }`
   - Returns: `{ message: "URL processed successfully" }`

### Chat Functionality

4. **POST** `/api/chat/chat`
   - Send a message to the AI
   - Body: `{ "query": "Your message here" }`
   - Returns: `{ response: "AI's response here" }`

5. **POST** `/api/chat/clear-history`
   - Clear the conversation history
   - No body required
   - Returns: `{ message: "Conversation history cleared" }`

6. **POST** `/api/chat/set-instruction`
   - Set custom instructions for the AI
   - Body: `{ "instruction": "Your custom instruction here" }`
   - Returns: `{ message: "Custom instruction set successfully" }`

### URL Processing

7. **POST** `/api/process-url`
   - Process a URL and extract its content
   - Body: `{ "url": "https://example.com" }`
   - Returns: `{ response: "Extracted content here" }`

### Podcast Processing

8. **POST** `/api/podcast/process`
   - Process an audio file (podcast)
   - Body: `{ "filePath": "/path/to/audio/file.mp3" }`
   - Returns: `{ response: "Transcribed text here" }`

### WhatsApp Integration

9. **POST** `/api/whatsapp/webhook`
   - Handle incoming WhatsApp messages
   - Body: `{ "from": "phone_number", "message": "Incoming message" }`
   - Returns: 200 OK status

10. **POST** `/api/whatsapp/toggle`
    - Toggle the WhatsApp bot on/off
    - Body: `{ "enable": true }` or `{ "enable": false }`
    - Returns: `{ message: "WhatsApp bot enabled/disabled" }`

## Frontend Development

To develop the frontend for this backend:

1. Use the provided `public/index.html` as a starting point for your UI.

2. Implement the following features in your UI:

   a. File Upload:
   - Create a form that allows users to select and upload files.
   - Use the `/api/file/upload` endpoint to send files to the server.

   b. Chat Interface:
   - Create a chat window where users can send messages and view AI responses.
   - Use the `/api/chat/chat` endpoint to send messages and receive responses.
   - Implement a button to clear chat history using `/api/chat/clear-history`.

   c. URL Processing:
   - Add a form where users can input a URL for processing.
   - Use the `/api/process-url` endpoint to send the URL and display the extracted content.

   d. Custom AI Instructions:
   - Create a form where users can input custom instructions for the AI.
   - Use the `/api/chat/set-instruction` endpoint to send these instructions.

   e. Podcast Processing:
   - Implement a feature to upload audio files (podcasts) for transcription.
   - Use the `/api/podcast/process` endpoint to send the file path and display the transcribed text.

   f. WhatsApp Integration (if applicable):
   - Add a toggle switch to enable/disable the WhatsApp bot.
   - Use the `/api/whatsapp/toggle` endpoint to control the bot's status.

3. Implement error handling and loading states for a better user experience.

4. Consider adding a WebSocket connection for real-time chat updates if needed.

Example API calls:

```javascript
// File upload
async function uploadFiles() {
  const formData = new FormData();
  formData.append('files', fileInput.files[0]);
  const response = await fetch('/api/file/upload', {
    method: 'POST',
    body: formData
  });
  const result = await response.json();
  console.log(result);
}

// Set prompt
async function setPrompt(prompt) {
  const response = await fetch('/api/file/set-prompt', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ prompt })
  });
  const result = await response.json();
  console.log(result);
}

// Process URL (File Service)
async function processUrlFileService(url) {
  const response = await fetch('/api/file/process-url', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ url })
  });
  const result = await response.json();
  console.log(result);
}

// Send chat message
async function sendMessage(query) {
  const response = await fetch('/api/chat/chat', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ query })
  });
  const result = await response.json();
  console.log(result);
}

// Clear chat history
async function clearChatHistory() {
  const response = await fetch('/api/chat/clear-history', {
    method: 'POST'
  });
  const result = await response.json();
  console.log(result);
}

// Set AI instructions
async function setInstructions(instruction) {
  const response = await fetch('/api/chat/set-instruction', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ instruction })
  });
  const result = await response.json();
  console.log(result);
}

// Process URL (URL Service)
async function processUrl(url) {
  const response = await fetch('/api/process-url', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ url })
  });
  const result = await response.json();
  console.log(result);
}

// Process podcast
async function processPodcast(filePath) {
  const response = await fetch('/api/podcast/process', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ filePath })
  });
  const result = await response.json();
  console.log(result);
}

// Toggle WhatsApp bot
async function toggleWhatsAppBot(enable) {
  const response = await fetch('/api/whatsapp/toggle', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ enable })
  });
  const result = await response.json();
  console.log(result);
}
```

## Additional Notes

- The backend uses a vector store to process and store document embeddings. Make sure the `uploads` directory exists and is writable.
- The AI service uses OpenAI's API, so ensure you have a valid API key in the `.env` file.
- The WhatsApp integration requires additional setup with the WhatsApp Business API. Make sure to configure the necessary credentials in the `.env` file.

For any questions or issues, please contact the backend development team.
