# Notebook Interface

A modern, full-stack React.js application that allows users to upload PDF documents and have intelligent conversations about their content using the Groq API. The app features a split-screen interface with a chat panel on the left and a PDF viewer on the right.

## 🎯 Features

- **PDF Upload & Processing**: Drag-and-drop or click to upload PDF files with progress tracking
- **Intelligent Document Analysis**: Ask questions about your PDF content using Groq's LLaMA 3.3 model
- **Real-time Chat Interface**: Conversational UI with message history and suggested questions
- **PDF Viewer**: Side-by-side PDF viewer to reference content while chatting
- **Error Handling**: Comprehensive error messages and validation
- **Responsive Design**: Beautiful, modern UI built with Tailwind CSS and shadcn/ui components
- **API Integration**: Secure API key handling with server actions

## 🛠️ Tech Stack

- **Frontend**: React 19, Vite, Typescript
- **Styling**: Tailwind CSS v4, shadcn/ui components
- **PDF Processing**: pdf.js (v4.10.38)
- **AI/LLM**: Groq API with LLaMA 3.3 model
- **API Communication**: Fetch API with server actions
- **Icons**: Lucide React
- **TypeScript**: Full type safety

## 📋 Prerequisites

- Node.js 18+ and npm/yarn
- Groq API Key (get it from [console.groq.com](https://console.groq.com))
- A modern web browser

## 🚀 Getting Started

### 1. Clone this Project

```
git clone https://github.com/Ashutosh-Maurya-87/notebookLLM_clone.git
```

### 2. Install Dependencies

```
npm install
# or
yarn install
```

### 3. Set Up Environment Variables

Create a `.env` file in the root directory:

```
VITE_GROQ_API_KEY=your_groq_api_key_here
```

**How to get your Groq API Key:**

1. Visit [console.groq.com](https://console.groq.com)
2. Sign up or log in to your account
3. Navigate to the API Keys section
4. Create a new API key
5. Copy and paste it into your `.env` file

### 4. Run the Development Server

```
npm run dev
# or
yarn dev
```

Open [http://localhost:5173] in your browser to see the application.

## 📁 Project Structure

```
src/
├── App.tsx
├── index.css
├── main.tsx
├── actions/
│   └── actions.ts
├── components/
│   ├── Button/
│   │   ├── Button.tsx
│   │   ├── types/
│   │   │   └── ButtonProps.tsx
│   │   └── _components/
│   │       └── ButtonVariants/
│   │           └── ButtonVariants.tsx
│   ├── ChatInterface/
│   │   ├── ChatInterface.tsx
│   │   ├── types/
│   │   │   └── ChartInterfaceTypes.ts
│   │   ├── _components/
│   │   │   ├── ChatHeader/
│   │   │   │   ├── ChatHeader.tsx
│   │   │   │   └── types/
│   │   │   │       └── ChatHeaderTypes.tsx
│   │   │   ├── ChatInput/
│   │   │   │   ├── ChatInput.tsx
│   │   │   │   └── types/
│   │   │   │       └── ChatInputTypes.tsx
│   │   │   └── ChatMessages/
│   │   │       ├── ChatMessages.tsx
│   │   │       └── types/
│   │   │           └── ChatMessagesTypes.tsx
│   │   └── _hooks/
│   │       └── useChat.ts
│   ├── Layout/
│   │   ├── Layout.tsx
│   │   └── types/
│   │       └── LayoutTypes.ts
│   ├── PDFUploadArea/
│   │   ├── PDFUploadArea.tsx
│   │   ├── types/
│   │   │   └── PDFUploadAreaTypes.tsx
│   │   ├── _components/
│   │   │   ├── UploadCard/
│   │   │   │   ├── UploadCard.tsx
│   │   │   │   └── types/
│   │   │   │       └── UploadCardTypes.tsx
│   │   │   └── UploadingOverlay/
│   │   │       ├── UploadingOverlay.tsx
│   │   │       └── types/
│   │   │           └── UploadingOverlayTypes.tsx
│   │   └── _hooks/
│   │       └── usePDFUpload.ts
│   └── PDFViewer/
│       ├── PDFViewer.tsx
│       ├── types/
│       │   └── PDFViewerTypes.ts
│       ├── _components/
│       │   ├── PDFPageList/
│       │   │   ├── PDFPageList.tsx
│       │   │   └── types/
│       │   │       └── PDFPageListTypes.tsx
│       │   ├── PDFStatus/
│       │   │   ├── PDFStatus.tsx
│       │   │   └── types/
│       │   │       └── PDFStatusTypes.tsx
│       │   └── PDFToolbar/
│       │       ├── PDFToolbar.tsx
│       │       └── types/
│       │           └── PDFToolbarTypes.tsx
│       └── _hooks/
│           └── usePDFViewer.ts
├── lib/
│   └── utils.ts
└── _hooks/
    └── usePDFUpload.tsx
```

## Implementation Reference

1. <img width="1915" height="908" alt="image" src="https://github.com/user-attachments/assets/753f895a-781c-46d1-b1e8-7e9eff0df617" />

2. <img width="1919" height="910" alt="image" src="https://github.com/user-attachments/assets/641dd287-f141-433b-b6c3-cd9e787b2753" />

3. <img width="1919" height="912" alt="image" src="https://github.com/user-attachments/assets/d9029516-bac3-4c62-a4cb-3fdf01d39be7" />

## 🔧 How It Works

### 1. PDF Upload Flow

- User uploads a PDF file via drag-and-drop or file picker
- The app extracts text from all pages using pdf.js
- Progress indicator shows extraction status
- Once complete, the chat interface becomes available

### 2. Chat Flow

- User enters a question about the PDF
- The question and PDF text are sent to the server action
- Server action calls the Groq API with the document context
- Response is streamed back and displayed in the chat
- Conversation history is maintained for context-aware responses

### 3. API Integration

The app uses a **fetch-based approach** with the Groq API:

```
// API call in actions/actions.ts
const response = await fetch("https://api.groq.com/openai/v1/chat/completions", {
  method: "POST",
  headers: {
    "Authorization": `Bearer ${apiKey}`,
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    model: "llama-3.3-70b-versatile",
    messages: [
      { role: "system", content: systemPrompt },
      { role: "user", content: userPrompt }
    ],
    temperature: 0.7,
    max_tokens: 1024,
  }),
})
```

## 🎨 UI Components

### Main Components

- **PDFUploadArea**: Initial upload interface with drag-and-drop support
- **ChatInterface**: Main chat UI with message display and input
- **PDFViewer**: Renders PDF pages using pdf.js
- **Button, Input**: shadcn/ui components for consistent styling

### Color Scheme

- **Primary**: Purple (#7c3aed)
- **Background**: White (#ffffff)
- **Text**: Dark gray (#1f2937)
- **Borders**: Light gray (#e5e7eb)

## 🔐 Security

- **API Key Protection**: The Groq API key is stored in `.env` and only used on the server side
- **Input Validation**: User inputs are validated before sending to the API
- **Error Handling**: Sensitive error information is not exposed to the client

## 🐛 Troubleshooting

### "API key is missing" Error

- Ensure `VITE_GROQ_API_KEY` is set in your `.env` file
- Restart the development server after adding the environment variable
- Verify the API key is valid at [console.groq.com](https://console.groq.com)

### PDF Upload Fails

- Ensure the file is a valid PDF
- Check browser console for specific error messages
- Try with a smaller PDF file first
- Verify your browser supports the File API

### Chat Responses Are Slow

- This is normal for the first request (model warm-up)
- Subsequent requests should be faster
- Check your internet connection
- Verify Groq API status at [status.groq.com](https://status.groq.com)

### "Canvas" Error in PDF Viewer

- This has been fixed in the latest version
- Ensure you're using the latest code from the repository
- Clear browser cache and restart the dev server

## 📚 API Reference

### Server Action: `chatWithGroq`

#### Typescript

```

interface ChatRequest {
  pdfText: string           // Extracted PDF content
  conversationHistory: string // Previous messages
  userInput: string         // Current user question
}

interface ChatResponse {
  success: boolean
  text?: string            // AI response
  error?: string           // Error message if failed
}
```

## 🙋 Support

If you encounter any issues:

1. Check the Troubleshooting section above
2. Review the browser console for error messages
3. Verify your environment variables are set correctly
4. Check the Groq API documentation at [console.groq.com/docs](https://console.groq.com/docs)

## 🔗 Useful Links

- [Groq API Documentation](https://console.groq.com/docs)
- [React.js Documentation](https://react.dev/learn)
- [pdf.js Documentation](https://mozilla.github.io/pdf.js/)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)
- [shadcn/ui Components](https://ui.shadcn.com)

---

**Built with ❤️ using React.js + Vite and Groq API**
