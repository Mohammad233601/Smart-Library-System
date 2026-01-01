# Library Management System

A full-stack web application for managing library books with React frontend and Node.js/Express backend using MongoDB database.

## Features

- ✅ Add New Book (Title, Author, ISBN, Year Published)
- ✅ View All Books
- ✅ Delete Books
- ✅ Responsive Design
- ✅ Modern UI with React
- ✅ RESTful API

## Project Structure

```
233601_Mohammad/
├── client/                 # React Frontend
│   ├── src/
│   │   ├── components/    # React Components
│   │   ├── api.js         # API Configuration
│   │   ├── App.jsx        # Main App Component
│   │   ├── main.jsx       # Entry Point
│   │   └── styles.css     # Styles
│   ├── index.html
│   └── package.json
├── server/                 # Node.js Backend
│   ├── models/            # Mongoose Models
│   ├── routes/            # API Routes
│   ├── server.js          # Server Entry Point
│   └── package.json
└── README.md
```

## Technology Stack

### Frontend
- **React 18** - Modern UI library
- **Vite** - Fast build tool
- **Axios** - HTTP client for API calls
- **CSS3** - Responsive styling

### Backend 
- **Node.js** - Runtime environment
- **Express.js** - Web framework
- **MongoDB** - NoSQL database
- **Mongoose** - MongoDB ODM

### Deployment 
- **MongoDB Atlas** - Cloud database
- **Render/Netlify** - Hosting platforms

---

## Setup Instructions

### Prerequisites
- Node.js (v16 or higher)
- MongoDB (local or MongoDB Atlas account)
- npm or yarn

### Step 1: Backend Setup

1. Navigate to server directory:
```bash
cd server
```

2. Install dependencies:
```bash
npm install
```

3. Create `.env` file:
```bash
PORT=5000
MONGODB_URI=mongodb://localhost:5000/library_db
```

For MongoDB Atlas, use:
```
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/library_db
```

4. Start the server:
```bash
npm start
```

Server will run on `http://localhost:5000`

### Step 2: Frontend Setup

1. Navigate to client directory (in a new terminal):
```bash
cd client
```

2. Install dependencies:
```bash
npm install
```

3. Create `.env` file (optional, defaults to localhost:5000):
```bash
VITE_API_URL=http://localhost:5000/api
```

4. Start development server:
```bash
npm run dev
```

Frontend will run on `http://localhost:5173` (or similar port)

### Step 3: Verify Connection

- Backend API: `http://localhost:5000/api/health` should return `{"status":"OK"}`
- Frontend: Open browser to see the application

---

## API Endpoints

### GET /api/books
Get all books
```json
Response: [
  {
    "_id": "...",
    "title": "Book Title",
    "author": "Author Name",
    "isbn": "1234567890",
    "yearPublished": 2024,
    "createdAt": "...",
    "updatedAt": "..."
  }
]
```

### POST /api/books
Create a new book
```json
Request Body:
{
  "title": "Book Title",
  "author": "Author Name",
  "isbn": "1234567890",
  "yearPublished": 2024  // optional
}

Response: Created book object
```

### DELETE /api/books/:id
Delete a book by ID
```json
Response: { "message": "Book deleted successfully", "book": {...} }
```

---

## How Frontend Connects to Backend

1. **API Configuration** (`client/src/api.js`):
   - Uses Axios to create an HTTP client
   - Base URL points to backend server (default: `http://localhost:5000/api`)
   - Environment variable `VITE_API_URL` can override default

2. **Component Integration**:
   - `BookForm.jsx` - Sends POST request to `/api/books` when form is submitted
   - `BookList.jsx` - Sends DELETE request to `/api/books/:id` when delete button clicked
   - `App.jsx` - Fetches all books using GET `/api/books` on component mount

3. **Data Flow**:
   ```
   User Action → React Component → Axios API Call → Express Backend → MongoDB → Response → Update UI
   ```

---

## Deployment Guide

### MongoDB Atlas Setup

1. Create account at [mongodb.com/cloud/atlas](https://www.mongodb.com/cloud/atlas)
2. Create a new cluster (Free tier available)
3. Create database user
4. Whitelist IP address (0.0.0.0/0 for all)
5. Get connection string: `mongodb+srv://username:password@cluster.mongodb.net/library_db`
6. Update `.env` file with Atlas connection string

### Backend Deployment (Render/Heroku)

**Option 1: Render**

1. Push code to GitHub
2. Go to [render.com](https://render.com)
3. Create new Web Service
4. Connect GitHub repository
5. Settings:
   - Build Command: `cd server && npm install`
   - Start Command: `cd server && npm start`
   - Environment Variables:
     - `PORT`: 5000 (auto-assigned by Render)
     - `MONGODB_URI`: Your MongoDB Atlas connection string

**Option 2: Heroku**

```bash
cd server
heroku create your-app-name
heroku config:set MONGODB_URI=your_atlas_connection_string
git push heroku main
```

### Frontend Deployment (Netlify/Vercel)

**Option 1: Netlify**

1. Build frontend: `cd client && npm run build`
2. Go to [netlify.com](https://netlify.com)
3. Drag and drop `client/dist` folder, OR
4. Connect GitHub repo and set:
   - Build command: `cd client && npm install && npm run build`
   - Publish directory: `client/dist`
   - Environment Variable: `VITE_API_URL` = your backend URL

**Option 2: Vercel**

```bash
cd client
npm install -g vercel
vercel
```

Update `VITE_API_URL` in Vercel dashboard with backend URL.

---

## Viva/Explanation Points (10 marks)

### 1. Why React?
- **Component-based architecture**: Reusable components (BookForm, BookList)
- **Virtual DOM**: Efficient UI updates
- **Unidirectional data flow**: Predictable state management
- **Large ecosystem**: Rich library support

### 2. Why Express.js?
- **Minimal and flexible**: Lightweight framework
- **Middleware support**: CORS, JSON parsing, routing
- **RESTful API**: Easy to create REST endpoints
- **Fast**: Built on Node.js, non-blocking I/O

### 3. Why MongoDB?
- **NoSQL**: Flexible schema, good for evolving data
- **Document-based**: Stores data as JSON-like documents
- **Scalable**: Easy horizontal scaling
- **Mongoose**: Provides schema validation and middleware

### 4. RESTful API Design
- **GET /api/books**: Retrieve all resources
- **POST /api/books**: Create new resource
- **DELETE /api/books/:id**: Delete specific resource
- Follows REST conventions for HTTP methods and status codes

### 5. Single Page Application (SPA)
- **Client-side routing**: No page reloads
- **Dynamic updates**: React updates DOM efficiently
- **Better UX**: Faster navigation, smoother interactions
- **Vite**: Fast development and optimized builds

### 6. CORS (Cross-Origin Resource Sharing)
- **Problem**: Browser blocks requests from different origins
- **Solution**: Express CORS middleware enables frontend-backend communication
- **Configuration**: Allows requests from frontend origin (e.g., localhost:5173)

### 7. Environment Variables
- **Security**: Keep sensitive data (database URI) out of code
- **Flexibility**: Different configs for dev/production
- **Best Practice**: Use `.env` files (not committed to Git)

### 8. Responsive Design
- **Media Queries**: CSS adapts to screen size
- **Flexible Layouts**: Grid and Flexbox for responsive components
- **Mobile-first**: Works on phones, tablets, desktops

### 9. Error Handling
- **Frontend**: Try-catch blocks, user-friendly error messages
- **Backend**: Status codes (400, 404, 500), error middleware
- **Validation**: Input validation before database operations

### 10. State Management
- **React Hooks**: `useState` for local state, `useEffect` for side effects
- **Lifting State Up**: Books state in App.jsx, passed to children
- **Optimistic Updates**: UI updates immediately, syncs with server

---

## Testing the Application

1. **Add a book**: Fill form with Title, Author, ISBN, and optional Year
2. **View books**: All books appear in the list below
3. **Delete book**: Click delete button, confirm deletion
4. **Validation**: Try submitting empty form, duplicate ISBN

---

## Common Issues & Solutions

### Backend won't start
- Check MongoDB is running (if using local MongoDB)
- Verify `.env` file has correct MONGODB_URI
- Check port 5000 is not in use

### Frontend can't connect to backend
- Verify backend is running on port 5000
- Check CORS is enabled in backend
- Verify `VITE_API_URL` points to correct backend URL

### Books not saving
- Check MongoDB connection
- Verify all required fields (title, author, ISBN) are provided
- Check browser console for error messages

---

## Author

**Mohammad** (233601)
 
---

## License

This project is for educational purposes.

