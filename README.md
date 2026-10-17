# HANA AI — Intelligent Fashion Stylist & Personal Shopping Assistant

An AI-powered fashion styling chatbot that combines large language models, live fashion research, and shopping product discovery to deliver personalized outfit recommendations and relevant product suggestions.

HANA helps users explore outfit combinations, color palettes, footwear, accessories, styling tips, and fashion trends through a conversational interface. It integrates an AI language model with external search services to provide context-aware recommendations alongside real shopping listings.

Built with **Node.js, Express.js, MongoDB, JavaScript, Together AI, Tavily Search API, and SerpApi**, HANA demonstrates the integration of generative AI, external APIs, persistent chat history, and a responsive browser-based interface in a real-world lifestyle application.

---

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Tech Stack](#tech-stack)
- [System Architecture](#system-architecture)
- [How HANA Works](#how-hana-works)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Installation and Setup](#installation-and-setup)
- [Environment Variables](#environment-variables)
- [Running the Application](#running-the-application)
- [API Documentation](#api-documentation)
- [Database Design](#database-design)
- [Frontend Implementation](#frontend-implementation)
- [AI Integration](#ai-integration)
- [Error Handling](#error-handling)
- [Security Considerations](#security-considerations)
- [Testing](#testing)
- [Limitations](#limitations)
- [Future Enhancements](#future-enhancements)
- [Contributing](#contributing)
- [License](#license)
- [Author](#author)

---

## Overview

HANA is an AI-powered fashion stylist designed to make everyday fashion decisions easier, more personalized, and more accessible.

Instead of providing only static outfit suggestions, HANA combines user prompts with external fashion research and shopping search results before generating its response.

Users can ask questions such as:

- What should I wear for a college event?
- Suggest a minimalist outfit for a dinner date.
- Which colors work well with black trousers?
- Create a casual winter outfit on a budget.
- Recommend accessories for a formal dress.
- Suggest shoes and bags that match my outfit.
- Find currently listed clothing products related to my style.

The application retrieves fashion-related information and shopping listings, passes the collected context to a large language model, and displays the generated styling advice in a structured chat interface.

HANA also saves conversations in MongoDB, allowing users to revisit previously stored chat sessions.

### Project Goals

- Build a practical AI-powered fashion assistant.
- Integrate a large language model with external information retrieval services.
- Retrieve shopping products from a live search API.
- Generate structured and readable fashion recommendations.
- Implement persistent, session-based chat history.
- Develop an interactive frontend using standard web technologies.
- Demonstrate backend API development, database integration, and asynchronous programming.

---

## Key Features

### 1. AI-Powered Fashion Recommendations

HANA uses the Llama 3.3 70B Instruct Turbo model through Together AI to generate conversational fashion advice.

Recommendations can cover:

- Complete outfit combinations.
- Clothing selection and layering.
- Color palettes and complementary colors.
- Footwear recommendations.
- Accessories and styling details.
- Fashion inspiration and trend-related suggestions.
- Practical styling tips and clothing combinations.
- Common styling mistakes to avoid.

The model receives the user's request along with retrieved fashion research and available shopping results.

### 2. Live Fashion Research

HANA integrates the Tavily Search API to retrieve relevant fashion information.

For each valid chat request, the backend constructs a search query related to the user's message and fashion trends, styling advice, and outfit ideas.

The search configuration requests advanced search results, an answer summary, and up to five results.

The retrieved information can include:

- Search-generated summaries.
- Source titles.
- Source URLs.
- Relevant content snippets.

This information is included in the context sent to the AI model. The returned source links are also provided to the frontend.

### 3. Shopping Product Discovery

HANA integrates SerpApi with Google Shopping search to retrieve product listings related to the user's fashion request.

The backend requests shopping results using parameters that target India and English-language results.

Available product information can include:

- Product title.
- Listed price.
- Seller or source.
- Rating.
- Review count.
- Product or search result link.
- Product thumbnail.

The application selects up to eight shopping results from the returned response.

Product data is supplied to the AI model and returned separately to the frontend so that product cards can be rendered.

Product availability, prices, and ratings depend on the external search response and may change over time.

### 4. Conversational Chat Interface

The browser-based interface supports interactive conversations with HANA.

Features include:

- User and assistant message bubbles.
- Message input with automatic resizing.
- Send-button interaction.
- Enter-key message submission.
- Suggested prompts and fashion-related shortcuts.
- Animated typing indicators.
- Markdown-formatted AI responses.
- Product cards displayed alongside relevant recommendations.
- Automatic scrolling to recent messages.

### 5. Session-Based Chat History

HANA assigns a session identifier to a browser chat session and stores it in the browser's local storage.

The backend stores messages in MongoDB, including the session ID, user message, assistant response, associated shopping results, title, and timestamp.

Users can retrieve the list of stored sessions and load their previous conversation history.

### 6. Responsive User Interface

The interface uses HTML, CSS, and vanilla JavaScript.

The design includes:

- Responsive layout adjustments.
- Desktop sidebar and mobile sidebar behavior.
- Dark and light theme controls.
- Animated visual elements.
- Fashion-inspired styling.
- Interactive product cards.
- Typing animations and message transitions.

### 7. Asynchronous API Processing

HANA uses JavaScript's asynchronous programming capabilities to fetch fashion research and shopping results concurrently.

The two external information-retrieval operations run through `Promise.all()`, reducing the need to wait for them sequentially.

Once the results are available, the backend calls the language model and returns the generated response to the browser.

### 8. Persistent Storage with MongoDB

MongoDB provides persistent storage for conversation records.

Mongoose defines the chat schema and provides database operations for saving messages, querying session history, and aggregating session summaries.

The database connection and API credentials are configured through environment variables.

---

## Tech Stack

### Backend

| Technology | Purpose |
|---|---|
| JavaScript (ES Modules) | Backend application logic |
| Node.js | Server-side JavaScript runtime |
| Express.js 5 | HTTP server, routing, middleware, and static file serving |
| REST APIs | Communication between frontend and backend |
| Mongoose | MongoDB schema definition and database operations |
| dotenv | Loading configuration from environment variables |
| cors | Cross-Origin Resource Sharing middleware |
| Axios | HTTP requests to the SerpApi endpoint |
| Native Fetch API | Browser-to-backend HTTP communication |

### Frontend

| Technology | Purpose |
|---|---|
| HTML5 | Page structure and interface components |
| CSS3 | Layout, styling, themes, animations, and responsiveness |
| Vanilla JavaScript | UI behavior, chat interaction, and DOM manipulation |
| Marked.js | Rendering Markdown-formatted AI responses |
| Canvas API | Animated visual background |
| Web Storage API | Persisting the active session identifier |
| Google Fonts | Cormorant Garamond and DM Sans typography |

### Artificial Intelligence and External APIs

| Technology | Purpose |
|---|---|
| Together AI | Hosted AI inference and chat completion requests |
| Llama 3.3 70B Instruct Turbo | Language model used to generate fashion recommendations |
| Tavily Search API | Fashion research and web search results |
| SerpApi | Google Shopping search results |
| Google Shopping engine | Source of shopping listings retrieved through SerpApi |

### Database

| Technology | Purpose |
|---|---|
| MongoDB | Persistent storage of chat records |
| MongoDB Atlas | Cloud database deployment option |
| Mongoose | Schema definition, queries, and aggregation |

### Development and Deployment

| Technology | Purpose |
|---|---|
| npm | Package and dependency management |
| Git | Version control |
| GitHub | Source code hosting |
| Render | Deployment platform, if configured for the deployed instance |
| Environment variables | Runtime configuration and secret management |

**Implementation note:** The repository uses plain HTML, CSS, and JavaScript rather than React or Tailwind CSS. Packages declared in `package.json` are not necessarily used in the application. The `openai`, `react-markdown`, and `body-parser` packages are declared but are not used by the supplied application code.

---

## System Architecture

HANA follows a client-server architecture with an Express backend, a MongoDB database, and external AI and search services.

```text
                 USER
                   |
                   v
       HTML + CSS + JavaScript UI
                   |
                   | POST /chat
                   v
          Node.js + Express
                   |
                   v
          Request Processing
                   |
          +--------+--------+
          |                 |
          v                 v
   Tavily Search       SerpApi
   Fashion Research    Google Shopping
          |                 |
          +--------+--------+
                   |
                   v
          Retrieved Context
                   |
                   v
             Together AI
       Llama 3.3 70B Instruct
                   |
                   v
         Generated Style Advice
                   |
                   v
             MongoDB
          Save Chat Record
                   |
                   v
        JSON Response to UI
                   |
                   v
        Render Reply and Products
```

The diagram represents the intended request flow. If an external research or shopping service fails, the application has fallback behavior described in the implementation sections below.

### Main Components

**1. Frontend**

Collects user messages, sends requests to the backend, displays assistant responses and product listings, and manages the active session ID.

**2. Express backend**

Validates incoming messages, coordinates external API requests, calls the language model, saves chat records, and exposes session-history endpoints.

**3. Fashion research service**

Uses Tavily to retrieve relevant search summaries and source information.

**4. Shopping service**

Uses SerpApi to retrieve Google Shopping listings.

**5. AI generation service**

Uses Together AI to generate a structured fashion recommendation based on the user's message and retrieved context.

**6. MongoDB database**

Stores conversation records and supports session listing and history retrieval.

---

## How HANA Works

### Step 1: User Submits a Message

The user enters a fashion-related prompt through the chat interface.

The frontend sends a JSON request to the backend's `/chat` endpoint. The request contains the message and the active session identifier.

### Step 2: Backend Validates the Request

Express reads the incoming JSON payload.

If the message is missing or contains only whitespace, the server responds with HTTP `400 Bad Request`.

Otherwise, the request proceeds to the research and shopping services.

### Step 3: Fashion Research Runs

The backend constructs a query based on the user's prompt and calls Tavily Search.

The search configuration requests advanced search, an answer summary, and up to five results.

If the search succeeds, HANA collects the summary and relevant source information.

If the search fails, the application logs the error and continues with an empty research result.

### Step 4: Shopping Results Are Retrieved

The backend constructs a shopping query based on the user's message and sends a request to SerpApi.

The request uses Google Shopping as the search engine, with India and English configured as the geographic and language preferences.

The backend maps the returned listings into a consistent product structure and selects up to eight products.

If shopping retrieval fails, the application logs the error and continues with an empty product list.

### Step 5: Research and Shopping Run Concurrently

Both external retrieval operations are started using `Promise.all()`.

This allows them to execute concurrently rather than requiring the fashion research request to finish before the shopping request begins.

### Step 6: The AI Generates Styling Advice

The backend sends a chat completion request to Together AI using the Llama 3.3 70B Instruct Turbo model.

The system instructions establish HANA's role as a fashion stylist and specify a structured response format.

The prompt asks the model to use retrieved research and shopping data when relevant and avoid inventing product prices, links, stores, or ratings.

The response is expected to include sections for outfit recommendations, colors, footwear, accessories, product suggestions, styling tips, and things to avoid.

### Step 7: The Conversation Is Saved

After the AI response is generated, the backend attempts to save the conversation in MongoDB.

The stored record includes the session ID, title derived from the user's message, original user message, generated assistant response, shopping products, and creation timestamp.

A database-save failure is logged separately and does not prevent the already-generated response from being returned.

### Step 8: The Frontend Displays the Result

The server returns JSON containing:

- The generated assistant reply.
- The retrieved product list.
- The fashion research source list.

The frontend renders the assistant's Markdown response, displays any available product cards, and updates the conversation interface.

---

## Project Structure

```text
HanaAI_FashionStylist/
│
├── index.html
│   └── Main frontend interface, CSS styling, and layout
│
├── script.js
│   └── Chat interaction, API calls, session management,
│       message rendering, themes, and canvas animation
│
├── server.js
│   └── Express server, AI integration, external API calls,
│       MongoDB models, and REST endpoints
│
├── package.json
│   └── Project metadata, npm scripts, and dependencies
│
├── package-lock.json
│   └── Locked npm dependency tree
│
├── .gitignore
│   └── Git ignore rules
│
└── README.md
    └── Project documentation
```

The `.env` file must be created locally and should not be committed to GitHub.

The `node_modules/` directory is generated by npm and should not be committed.

---

## Prerequisites

Before running the project, ensure that the following are available:

- **Node.js:** A compatible Node.js version for the dependencies in `package.json`.
- **npm:** Installed with Node.js.
- **MongoDB:** A MongoDB Atlas connection string or an accessible MongoDB deployment.
- **Together AI API key:** Required for generating AI responses.
- **Tavily API key:** Required for fashion research.
- **SerpApi API key:** Required for Google Shopping retrieval.
- **Git:** Optional, for cloning and version control.
- **Web browser:** A modern browser for using the interface.

You will need valid credentials for the external services to use their corresponding functionality.

---

## Installation and Setup

### 1. Clone the Repository

```bash
git clone https://github.com/uroozfatima/HanaAI_FashionStylist.git
```

Navigate into the project directory:

```bash
cd HanaAI_FashionStylist
```

### 2. Install Dependencies

Run:

```bash
npm install
```

This installs the dependencies declared in `package.json` and creates the local `node_modules/` directory.

### 3. Configure Environment Variables

Create a `.env` file in the project root directory.

Add the required configuration variables described in the next section.

Do not share your API keys publicly or commit the `.env` file to version control.

### 4. Configure MongoDB

Create or select a MongoDB database.

If you use MongoDB Atlas:

1. Create a cluster.
2. Configure an appropriate database user.
3. Allow access from your development environment in the network settings.
4. Obtain the connection string.
5. Add the connection string to `MONGODB_URI` in your `.env` file.

Use appropriate access controls and avoid opening database access to all IP addresses unless you understand the risks.

### 5. Configure API Credentials

Obtain credentials from the relevant services:

- Together AI for model inference.
- Tavily for search and fashion research.
- SerpApi for Google Shopping results.

Add these values to the environment configuration.

### 6. Start the Server

Run:

```bash
npm start
```

Alternatively:

```bash
node server.js
```

By default, the server listens on port `3000`, unless a different port is supplied through the `PORT` environment variable.

When startup succeeds, the console logs the server address and database connection status.

### 7. Open HANA in Your Browser

Visit:

```text
http://localhost:3000
```

The Express server serves `index.html` and the other static frontend files.

**Important:** Use the local server URL rather than opening `index.html` directly with a `file://` URL. The frontend uses relative API paths, which should be served from the same origin as the backend.

---

## Environment Variables

Create a `.env` file in the root directory:

```dotenv
PORT=3000

MONGODB_URI=your_mongodb_connection_string

TOGETHER_API_KEY=your_together_ai_api_key

TAVILY_API_KEY=your_tavily_api_key

SERPAPI_API_KEY=your_serpapi_api_key
```

Replace each placeholder with your own configuration value.

| Variable | Required | Purpose |
|---|---|---|
| `PORT` | Optional | Port used by the Express server; defaults to `3000` |
| `MONGODB_URI` | Yes | MongoDB connection string |
| `TOGETHER_API_KEY` | Yes | Authentication for Together AI |
| `TAVILY_API_KEY` | Yes | Authentication for Tavily Search |
| `SERPAPI_API_KEY` | Yes | Authentication for SerpApi |

### Environment Configuration Notes

- The backend loads variables using `dotenv`.
- API keys are used server-side and should never be embedded in frontend JavaScript.
- Keep production credentials in your hosting provider's environment settings.
- Never commit real secrets to GitHub.
- Use separate credentials for development and production when appropriate.
- Rotate credentials immediately if they are exposed.

---

## Running the Application

### Start the Backend

```bash
npm start
```

### Open the Application

```text
http://localhost:3000
```

### Test the Chat Endpoint

You can test the backend using Postman, curl, or another HTTP client.

Example request:

```bash
curl -X POST http://localhost:3000/chat \
  -H "Content-Type: application/json" \
  -d "{\"message\":\"Suggest a casual winter outfit\",\"sessionId\":\"demo-session\"}"
```

A successful response contains the assistant reply, product results, and source information.

Example response structure:

```json
{
  "reply": "Generated fashion advice in Markdown",
  "products": [
    {
      "title": "Example product title",
      "price": "Example listed price",
      "source": "Example seller",
      "rating": 4.2,
      "reviews": 100,
      "link": "https://example.com/product",
      "thumbnail": "https://example.com/image.jpg"
    }
  ],
  "sources": [
    {
      "title": "Example fashion article",
      "url": "https://example.com/article",
      "content": "Relevant source content"
    }
  ]
}
```

The values above illustrate the response format only. Actual products, source links, prices, ratings, and AI responses depend on the live service results.

---

## API Documentation

The Express backend exposes the following application endpoints.

### 1. Home Route

**Endpoint:** `GET /`

**Purpose:** Serves the main HTML interface.

**Response:** HTML page.

Example:

```bash
curl http://localhost:3000/
```

### 2. Chat Endpoint

**Endpoint:** `POST /chat`

**Purpose:** Processes a fashion prompt, retrieves fashion research and shopping results, generates an AI response, attempts to save the conversation, and returns the results.

**Request body:**

```json
{
  "message": "Suggest a minimalist college outfit",
  "sessionId": "session_123456"
}
```

**Request fields:**

| Field | Type | Description |
|---|---|---|
| `message` | String | User's fashion-related request; required |
| `sessionId` | String | Identifier used to associate the conversation with a session |

**Successful response:** HTTP `200 OK`.

```json
{
  "reply": "AI-generated styling recommendation",
  "products": [],
  "sources": []
}
```

**Validation error:** HTTP `400 Bad Request`.

```json
{
  "error": "Message is required"
}
```

**Processing error:** HTTP `500 Internal Server Error`.

```json
{
  "error": "Failed to process request"
}
```

A missing or invalid API credential, an AI service failure, or another unhandled processing error can prevent the request from completing.

### 3. Sessions Endpoint

**Endpoint:** `GET /sessions`

**Purpose:** Retrieves session summaries derived from stored chat records.

The backend sorts records by creation time, groups them by session ID, selects the most recent record's title and timestamp, and sorts the session summaries by recency.

Example:

```bash
curl http://localhost:3000/sessions
```

Example response:

```json
[
  {
    "_id": "session_123456",
    "title": "Suggest a minimalist college outfit",
    "createdAt": "2026-01-01T10:00:00.000Z"
  }
]
```

The response illustrates the general structure; actual dates and values come from the database.

### 4. Chat History Endpoint

**Endpoint:** `GET /history/:sessionId`

**Purpose:** Retrieves stored chat records for a particular session, ordered from oldest to newest.

Example:

```bash
curl http://localhost:3000/history/session_123456
```

The response is an array of stored chat documents, including their available message, product, session, and timestamp fields.

**Important:** These endpoints do not implement user authentication or authorization in the current code. Do not expose private conversation history to untrusted users in a public production deployment without adding appropriate access controls.

---

## Database Design

HANA uses MongoDB with Mongoose to store chat records.

### Chat Model

The application defines a `Chat` model using the following schema:

| Field | Type | Purpose |
|---|---|---|
| `sessionId` | String | Associates the record with a browser chat session |
| `title` | String | Stores the first 40 characters of the user's message as the record title |
| `userMessage` | String | Stores the user's original message |
| `botReply` | String | Stores the generated AI response |
| `products` | Array | Stores shopping results associated with the request |
| `createdAt` | Date | Records when the chat document was created |

The `createdAt` field defaults to the current date and time.

### Example Chat Document

```json
{
  "sessionId": "session_123456",
  "title": "Suggest a minimalist college outfit",
  "userMessage": "Suggest a minimalist college outfit",
  "botReply": "Generated fashion advice in Markdown",
  "products": [],
  "createdAt": "2026-01-01T10:00:00.000Z"
}
```

This is an illustrative example, not a record taken from a live database.

### Session Retrieval

The `/sessions` endpoint uses MongoDB aggregation to group records by `sessionId` and return a summary based on the newest stored record.

The `/history/:sessionId` endpoint uses a database query filtered by session ID and sorts matching records in ascending creation-time order.

### Database Connection

The backend connects using `MONGODB_URI` and sets a server selection timeout of 30 seconds.

The application logs a successful connection or a connection error to the server console.

The current implementation does not define database indexes, user ownership, retention policies, or automatic deletion of old chat records.

---

## Frontend Implementation

The frontend consists of `index.html` and `script.js`.

### HTML5

Defines the page structure, message container, chat input, sidebar, theme controls, welcome screen, and product display areas.

### CSS3

Provides the visual design, including:

- Layout and spacing.
- Responsive behavior.
- Dark and light themes.
- Message bubbles.
- Product cards.
- Typing indicators.
- Animated visual elements.
- Typography and transitions.

### Vanilla JavaScript

The frontend script implements:

- Message submission.
- API communication.
- Message rendering.
- Loading and typing states.
- Session switching.
- Conversation history loading.
- Suggested prompt handling.
- Theme switching.
- Mobile sidebar interactions.
- Animated canvas elements.

### Markdown Rendering

Marked.js converts the assistant's Markdown response into HTML for display in the chat.

Since AI-generated Markdown is converted into HTML, production deployments should sanitize generated HTML before inserting it into the page. Markdown parsing alone is not a security sanitizer.

### Browser Storage

The browser's `localStorage` stores the active session ID so the same browser can continue using that session after a page reload.

This is a client-side session identifier, not a secure authentication token.

---

## AI Integration

### Model

HANA uses the following model identifier in the Together AI chat completion request:

`meta-llama/Llama-3.3-70B-Instruct-Turbo`

The model is configured with a temperature of `0.7` and a maximum output token setting of `1200`.

### Prompt Engineering

The backend supplies a system prompt that defines HANA as a fashion stylist and personal shopping assistant.

It requests a structured response with sections such as:

1. Best outfit.
2. Color palette.
3. Footwear.
4. Accessories.
5. Product suggestions.
6. Styling tips.
7. What to avoid.

The prompt also instructs the model to use the supplied research and product information when relevant and not invent prices, links, stores, or ratings.

### Context Enrichment

The model receives the original user request, the Tavily research result, and the SerpApi shopping results.

This approach provides additional context beyond the user prompt alone.

It is a retrieval-enriched generative AI workflow. The repository does not currently implement a vector database, embedding generation, or a dedicated semantic vector retrieval pipeline.

### External Services and Their Roles

**Together AI:** Generates the natural-language fashion recommendation.

**Tavily:** Retrieves relevant fashion research and source information.

**SerpApi:** Retrieves shopping listings through Google Shopping search.

Each service has a separate role in the application's request pipeline.

---

## Error Handling

The backend includes basic error handling for external services, database persistence, and HTTP requests.

### Fashion Research Failure

If Tavily fails, the research function logs the error and returns an empty summary and source list, allowing processing to continue.

### Shopping Search Failure

If SerpApi fails, the shopping function logs the error and returns an empty product list.

### Database Save Failure

If saving a generated conversation fails, the error is logged. The backend still attempts to return the generated reply and retrieved information.

### Invalid Chat Message

The `/chat` endpoint returns HTTP `400` when the message is missing or consists only of whitespace.

### General Request Failure

Unhandled errors in the main chat processing flow result in HTTP `500` with a generic error message.

### Current Limitations in Error Handling

The application does not currently implement a comprehensive retry strategy, rate-limit handling, request cancellation, circuit breakers, or structured observability.

Errors are primarily logged to the server console.

---

## Security Considerations

The current repository is a functional project implementation and should receive additional security hardening before being used as a public production service.

### API Key Protection

- Store API keys in environment variables.
- Never include private API keys in frontend JavaScript.
- Do not commit `.env` files.
- Configure production secrets through the hosting environment.
- Rotate credentials if exposed.

### Input Validation

The chat endpoint checks whether a message is present and non-empty. More comprehensive validation should be added for message length, request structure, and session identifiers.

### Chat History Access

The session and history endpoints currently do not authenticate users or verify ownership of a session.

A production implementation should introduce authentication and enforce authorization checks before returning stored conversation data.

### Cross-Origin Resource Sharing

The current Express server enables CORS through `app.use(cors())` without a restrictive origin configuration.

For a public deployment, restrict allowed origins to the intended frontend domains when cross-origin access is required.

### HTML Rendering

The frontend uses Markdown parsing to render AI responses. Generated HTML should be sanitized, and rendering should follow a safe content policy to reduce cross-site scripting risks.

### Database Protection

Use a least-privilege database user, appropriate network access controls, and secure connection settings.

### Rate Limiting

Add rate limiting and usage controls to reduce abuse and protect paid AI and search API quotas.

### Logging

Avoid logging API keys, sensitive user data, or complete private conversations in production logs.

---

## Testing

The repository currently does not contain a complete automated test suite.

The `npm test` script is a placeholder that exits with an error indicating that no test is specified.

Before treating the application as production-ready, add automated tests for the main workflows.

### Recommended Test Coverage

**Backend API tests**
- Successful chat request.
- Missing or empty message.
- Invalid request payload.
- AI provider failure.
- Search provider failure.
- Database persistence failure.
- Session retrieval.
- Chat history retrieval.

**Database tests**
- Saving chat records.
- Retrieving session summaries.
- Loading messages in chronological order.
- Handling database connection failures.

**Frontend tests**
- Message submission.
- Loading indicators.
- Markdown rendering.
- Product-card rendering.
- Session switching.
- Responsive sidebar behavior.

**Integration tests**
- End-to-end chat request.
- External API integration.
- Database persistence.
- Error handling across the complete request flow.

Useful future testing tools include Node.js's built-in test runner, Supertest, and a browser automation framework such as Playwright. These are recommendations, not currently implemented project dependencies.

---

## Limitations

The current implementation has the following limitations:

- AI response quality depends on the model and available context.
- External search services may return incomplete, outdated, or irrelevant results.
- Shopping prices, ratings, and product availability can change.
- Shopping retrieval is based on Google Shopping search results, not a guaranteed inventory or checkout integration.
- The current application does not provide a complete purchase or payment workflow.
- Session identifiers are stored in browser local storage and are not tied to authenticated user accounts.
- Session and history endpoints lack user authorization.
- The application does not include a complete automated test suite.
- The current chat schema has no defined indexes or data retention policy.
- External service retries, rate limiting, and advanced monitoring are not implemented.
- AI-generated HTML requires additional sanitization for production safety.
- The model's output is generated text and should not be treated as a guarantee of product accuracy or suitability.
- No image-based outfit recognition, virtual try-on, or body measurement analysis is implemented in the supplied code.

---

## Future Enhancements

Potential improvements include:

### 1. User Authentication

Add secure authentication, user profiles, and session ownership so that conversations can be associated with individual users.

### 2. Personalized Style Profiles

Allow users to configure style preferences, preferred colors, clothing sizes, budgets, occasions, and preferred brands.

### 3. Advanced Recommendation Engine

Improve recommendation relevance using structured user preferences, product metadata, and feedback on previous suggestions.

### 4. Automated Testing

Introduce unit, integration, and end-to-end tests to improve reliability and prevent regressions.

### 5. Security Hardening

Add request validation, HTML sanitization, rate limiting, restrictive CORS settings, and proper authorization.

### 6. Better Database Performance

Add appropriate indexes, pagination, retention policies, and improved data models for chat history and product information.

### 7. Streaming AI Responses

Stream generated tokens to the browser to make the assistant feel more responsive during longer responses.

### 8. Caching

Cache suitable fashion search results and repeated shopping queries to reduce unnecessary external API calls and latency.

### 9. Observability

Introduce structured logging, health checks, metrics, and error monitoring.

### 10. Richer Shopping Experience

Add filters for budget, brand, category, ratings, and occasion, along with more reliable product-link handling.

### 11. Image-Based Styling

Explore image uploads, clothing recognition, outfit analysis, and visual recommendations.

### 12. Production Deployment

Add a repeatable deployment process, environment validation, CI/CD, and a production-ready configuration.

---

## Contributing

Contributions that improve the reliability, usability, maintainability, or functionality of HANA are welcome.

A suggested workflow:

1. Fork the repository.
2. Create a feature branch.
3. Make focused changes.
4. Test the affected functionality.
5. Commit your changes with a descriptive message.
6. Open a pull request explaining the change.

Please do not include API keys, database credentials, or other secrets in commits or pull requests.

---

## License

The repository currently specifies the `ISC` license in `package.json`. Confirm that the appropriate license text is included in the repository before distributing the project.

---

## Author
**Urooz Fatima**
B.Tech Student — Lovely Professional University

## Acknowledgements

HANA integrates several technologies and services that make its functionality possible:

- Node.js and Express.js for backend development.
- MongoDB and Mongoose for persistent storage.
- Together AI and the Llama model for AI-generated recommendations.
- Tavily for fashion-related research.
- SerpApi and Google Shopping for shopping discovery.
- HTML, CSS, JavaScript, and Marked.js for the interactive interface.

---

**HANA AI — Making everyday fashion decisions smarter, simpler, and more personalized.**
Lovely Professional University
