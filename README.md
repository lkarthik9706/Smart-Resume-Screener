# Smart Resume Screener

An AI-powered resume screening system that extracts structured information from PDF/DOCX resumes and intelligently matches candidates against job descriptions using semantic analysis.

**Technology Stack:**
- **Backend:** Node.js + Express
- **AI Engine:** Google Gemini API
- **Database:** MongoDB
- **Frontend:** React + Vite
- **Document Processing:** pdf-parse, mammoth

---

## 🎯 Problem Statement

Recruiters spend significant time manually reviewing resumes for each job opening. Traditional keyword-based screening can miss qualified candidates whose skills are described differently. **Smart Resume Screener** automates this process with AI-powered semantic matching.

### Key Benefits:
- ✅ Automated resume parsing and structuring
- ✅ Semantic job matching (not just keyword matching)
- ✅ Explainable scoring system (1-10)
- ✅ Skill gap analysis
- ✅ Candidate strengths & weaknesses identification
- ✅ Automated shortlisting decisions

---

## 🎯 Objectives

- ✓ Accept resumes in **PDF** and **DOCX** formats (max 5 MB)
- ✓ Extract structured candidate information:
  - Name, email, phone
  - Education (degree, institution, year)
  - Experience (company, role, duration, description)
  - Technical skills
  - Projects & certifications
- ✓ Store parsed resumes in MongoDB
- ✓ Compare candidates with job descriptions using Gemini AI
- ✓ Generate match scores (1-10) with:
  - Matched & missing skills
  - Strengths & weaknesses
  - Explainable justification
  - Shortlist recommendation (score ≥ 8.0)

---

## 📋 Project Structure

```
Smart-Resume-Screener/
├── client/                    # React + Vite frontend
│   ├── src/
│   │   ├── App.jsx           # Main component
│   │   ├── App.css           # Styling
│   │   └── main.jsx          # Entry point
│   ├── index.html
│   ├── package.json
│   └── vite.config.js
│
├── server/                    # Express backend
│   ├── config/
│   │   └── db.js             # MongoDB connection
│   ├── models/
│   │   └── resume.js         # Resume schema
│   ├── server.js             # Main server logic
│   └── package.json
│
└── README.md
```

---

## 🚀 Quick Start

### Prerequisites
- Node.js v16+ and npm
- MongoDB Atlas account (or local MongoDB)
- Google Gemini API key ([Get here](https://ai.google.dev/))

### Installation

#### 1. Clone the repository
```bash
git clone https://github.com/lkarthik9706/Smart-Resume-Screener.git
cd Smart-Resume-Screener
```

#### 2. Setup Backend

```bash
cd server
npm install

# Create .env file
cat > .env << EOF
PORT=5000
MONGODB_URI=mongodb+srv://<username>:<password>@cluster.mongodb.net/smart-resume-screener
GEMINI_API_KEY=your_gemini_api_key_here
EOF

npm start
```

#### 3. Setup Frontend

```bash
cd ../client
npm install
npm run dev
```

The frontend will run at `http://localhost:5173`

---

## 📡 API Endpoints

### 1. **Parse Resume**
Extract and structure resume information

**Endpoint:** `POST /api/screen-resume`

**Request:**
```bash
curl -X POST http://localhost:5000/api/screen-resume \
  -F "resume=@path/to/resume.pdf"
```

**Response:**
```json
{
  "success": true,
  "message": "Resume successfully processed.",
  "resumeId": "507f1f77bcf86cd799439011",
  "resume": {
    "candidate": {
      "name": "John Doe",
      "email": "john@example.com",
      "phone": "+1-555-0100"
    },
    "education": [
      {
        "degree": "Bachelor of Science",
        "institution": "University of Example",
        "year": "2020"
      }
    ],
    "experience": [
      {
        "company": "Tech Corp",
        "role": "Software Engineer",
        "duration": "2020-2023",
        "description": "Developed web applications..."
      }
    ],
    "skills": ["JavaScript", "React", "Node.js", "MongoDB"],
    "projects": [
      {
        "name": "E-commerce Platform",
        "description": "Full-stack marketplace application",
        "technologies": ["React", "Node.js", "MongoDB"]
      }
    ],
    "certifications": ["AWS Solutions Architect"]
  }
}
```

### 2. **Match Resume to Job**
Compare candidate profile with job requirements

**Endpoint:** `POST /api/match-resume`

**Request:**
```json
{
  "resumeId": "507f1f77bcf86cd799439011",
  "jobDescription": "We are looking for a Senior Frontend Developer with 5+ years of React experience..."
}
```

**Response:**
```json
{
  "success": true,
  "resumeId": "507f1f77bcf86cd799439011",
  "matchResult": {
    "matchScore": 8.5,
    "matchedSkills": ["React", "JavaScript", "Node.js"],
    "missingSkills": ["TypeScript", "GraphQL"],
    "relevantExperience": [
      "2+ years as Frontend Engineer at Tech Corp"
    ],
    "relevantProjects": [
      "E-commerce Platform - demonstrates full-stack capabilities"
    ],
    "strengths": [
      "Strong React and JavaScript expertise",
      "Real-world project experience",
      "Solid backend knowledge"
    ],
    "weaknesses": [
      "Limited TypeScript experience",
      "No GraphQL mentioned in resume"
    ],
    "justification": "Candidate is well-qualified with strong React fundamentals and proven project delivery. Missing TypeScript and GraphQL are learnable skills. Recommend shortlisting.",
    "shortlisted": true
  }
}
```

### 3. **Health Check**
Verify server status

**Endpoint:** `GET /`

**Response:**
```json
{
  "message": "Smart Resume Screener Backend is Running!",
  "ai": "Gemini",
  "database": "MongoDB"
}
```

---

## 🎨 Features

### Resume Upload & Parsing
- Supports **PDF** and **DOCX** formats
- Maximum file size: **5 MB**
- Automatic text extraction
- Structured JSON output

### AI-Powered Extraction
Powered by Google Gemini API:
- Candidate information (name, email, phone)
- Education details
- Professional experience
- Technical skills
- Projects with technologies
- Certifications

### Semantic Job Matching
- **Not just keyword matching** - understands skill context
- Scores candidates 1-10 based on:
  - Technical skills alignment
  - Experience relevance
  - Project portfolio
  - Education fit
- Identifies gaps and strengths
- Provides actionable recruitment insights

### Shortlisting Logic
```
Score 8.0-10.0  → ✅ Shortlisted
Score 6.0-7.9   → ⏳ Review
Score < 6.0     → ❌ Not Shortlisted
```

---

## 💾 Database Schema

### Resume Model (MongoDB)

```javascript
{
  candidate: {
    name: String,
    email: String,
    phone: String
  },
  education: [
    {
      degree: String,
      institution: String,
      year: String
    }
  ],
  experience: [
    {
      company: String,
      role: String,
      duration: String,
      description: String
    }
  ],
  skills: [String],
  projects: [
    {
      name: String,
      description: String,
      technologies: [String]
    }
  ],
  certifications: [String],
  originalFileName: String,
  resumeText: String,
  jobDescription: String,
  matchResult: {
    matchScore: Number,
    matchedSkills: [String],
    missingSkills: [String],
    relevantExperience: [String],
    relevantProjects: [String],
    strengths: [String],
    weaknesses: [String],
    justification: String,
    shortlisted: Boolean
  },
  createdAt: Date,
  updatedAt: Date
}
```

---

## 🔑 Environment Variables

Create a `.env` file in the `server/` directory:

```env
# Server
PORT=5000

# MongoDB
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/smart-resume-screener

# Google Gemini API
GEMINI_API_KEY=your_gemini_api_key_here
```

---

## 🛠️ Development Workflow

### Backend Development
```bash
cd server
npm install
npm start
```
Server runs on `http://localhost:5000`

### Frontend Development
```bash
cd client
npm install
npm run dev
```
Frontend runs on `http://localhost:5173` with Hot Module Replacement (HMR)

### Build for Production
```bash
# Frontend
cd client
npm run build
# Creates optimized build in client/dist/

# Backend
# Deploy server.js with Node.js runtime
```

---

## 📝 Example Workflow

### Step 1: Upload Resume
```bash
curl -X POST http://localhost:5000/api/screen-resume \
  -F "resume=@john-doe-resume.pdf"
```

### Step 2: Get Resume ID
Returns `resumeId: "507f1f77bcf86cd799439011"`

### Step 3: Match with Job Description
```bash
curl -X POST http://localhost:5000/api/match-resume \
  -H "Content-Type: application/json" \
  -d '{
    "resumeId": "507f1f77bcf86cd799439011",
    "jobDescription": "Senior Frontend Developer needed. Required: React, TypeScript, 5+ years experience. Nice to have: GraphQL, Next.js"
  }'
```

### Step 4: Review Results
Get match score, skill gaps, and shortlist recommendation instantly!

---

## 🔒 Security Considerations

- **File Upload:** Limited to 5 MB, only PDF/DOCX accepted
- **API Validation:** Resume ID and job description required
- **CORS:** Enabled for development (configure for production)
- **Database:** Use MongoDB Atlas with IP whitelisting
- **API Keys:** Never commit `.env` files, use environment variables

---

## 🚀 Deployment

### Deploy Backend (Vercel, Railway, Heroku)
```bash
# Set environment variables in deployment platform
# Push to git repository
git push origin main
```

### Deploy Frontend (Vercel, Netlify)
```bash
# Build frontend
cd client
npm run build

# Deploy dist/ folder to hosting service
```

---

## 📚 Tech Stack Details

| Component | Technology | Version |
|-----------|-----------|---------|
| **Runtime** | Node.js | v16+ |
| **Backend** | Express | v5.2.1 |
| **Frontend** | React | v19.2.8 |
| **Build Tool** | Vite | v8.2.0 |
| **Database** | MongoDB | 9.9.3 |
| **AI Model** | Google Gemini | 3.6-flash |
| **PDF Parser** | pdf-parse | v2.4.5 |
| **DOCX Parser** | mammoth | v1.12.1 |
| **File Upload** | multer | v2.2.0 |
| **CORS** | cors | v2.8.6 |

---

## 🐛 Troubleshooting

### Issue: "Unsupported file type"
- Ensure resume is PDF or DOCX format
- Maximum file size is 5 MB

### Issue: "Resume not found"
- Verify resumeId is correct
- Check MongoDB connection is active

### Issue: "Gemini API error"
- Verify GEMINI_API_KEY is set correctly in `.env`
- Check API key has been activated at [Google AI Studio](https://ai.google.dev/)
- Ensure you have available API quota

### Issue: CORS errors
- In development, CORS is enabled
- For production, update CORS policy in `server.js`

---

## 📞 Support & Contribution

Found a bug or have a feature request? 
- Open an issue on GitHub
- Submit a pull request with improvements

---

## 📄 License

This project is open source and available under the ISC License.

---

**Happy Resume Screening! 🎉**

Built with ❤️ using Gemini AI
