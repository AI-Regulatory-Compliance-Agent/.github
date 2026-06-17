# Project Structure

```text
ai-regulatory-compliance-agent/
│
├── data/                                  # Local only (not version controlled)
│   ├── raw/                               # Source regulatory PDFs
│   ├── extracted/                         # Extracted text files
│   └── chunks/                            # Generated chunk JSON files
│
├── infra/                                 # Repository: org/infra
│   ├── .gitignore
│   ├── .env                               # Local secrets (never committed)
│   ├── .env.example
│   └── docker-compose.yml                 # Infrastructure orchestration
│
├── ingestion/                             # Repository: org/ingestion
│   ├── .gitignore
│   ├── Dockerfile
│   ├── requirements.txt
│   ├── downloader.py                      # Download regulatory documents
│   ├── extractor.py                       # Extract text from PDFs
│   ├── chunker.py                         # Split text into chunks
│   ├── embedder.py                        # Generate embeddings
│   └── ingestor.py                        # Load embeddings into Qdrant
│
├── backend/                               # Repository: org/backend
│   ├── .gitignore
│   ├── Dockerfile
│   ├── requirements.txt
│   │
│   └── app/
│       ├── main.py                        # FastAPI application entry point
│       ├── config.py                      # Environment configuration
│       ├── database.py                    # PostgreSQL connection/session
│       ├── redis_client.py                # Redis connection
│       ├── qdrant_client.py               # Qdrant connection
│       │
│       ├── models/                        # SQLAlchemy models
│       │   ├── __init__.py
│       │   ├── user.py                    # Users table
│       │   ├── company.py                 # Companies table
│       │   ├── analysis.py                # Analysis runs table
│       │   └── report.py                  # Generated reports table
│       │
│       ├── schemas/                       # Pydantic schemas
│       │   ├── __init__.py
│       │   ├── auth.py                    # Authentication schemas
│       │   ├── company.py                 # Company profile schemas
│       │   └── analysis.py                # Analysis response schemas
│       │
│       ├── agents/                        # LangGraph multi-agent workflow
│       │   ├── __init__.py
│       │   ├── state.py                   # Shared ComplianceState
│       │   ├── graph.py                   # Agent workflow definition
│       │   ├── regulation_identifier.py   # Agent 1: Regulation Identification
│       │   ├── gap_analysis.py            # Agent 2: Gap Analysis
│       │   ├── risk_scoring.py            # Agent 3: Risk Assessment
│       │   ├── remediation.py             # Agent 4: Remediation Planning
│       │   └── report_generator.py        # Agent 5: Report Generation
│       │
│       ├── tools/                         # Agent tools
│       │   ├── __init__.py
│       │   ├── qdrant_search.py           # RAG retrieval tool
│       │   └── pdf_generator.py           # PDF generation utility
│       │
│       ├── utils/                         # Shared utilities
│       │   ├── __init__.py
│       │   ├── jwt.py                     # JWT creation/validation
│       │   └── hashing.py                 # Password hashing
│       │
│       └── routers/                       # API routes
│           ├── __init__.py
│           ├── auth.py                    # /auth endpoints
│           ├── analysis.py                # /analyze endpoints
│           ├── history.py                 # Analysis history endpoints
│           └── reports.py                 # Report download endpoints
│           └── websocket.py                 # Report download endpoints
│
└── frontend/                              # Repository: org/frontend
    ├── .gitignore
    ├── Dockerfile
    ├── package.json
    ├── vite.config.js
    ├── index.html
    │
    └── src/
        ├── main.jsx                       # React entry point
        ├── App.jsx                        # Application routing
        │
        ├── api/
        │   └── client.js                  # Axios client & API calls
        │
        ├── context/
        │   └── AuthContext.jsx            # Authentication state management
        │
        ├── hooks/
        │   ├── useAuth.js                 # Login/Register hooks
        │   └── useAnalysis.js             # Analysis workflow hooks
        │   └── useWebSocket.js
        │
        ├── pages/
        │   ├── LoginPage.jsx              # User login
        │   ├── RegisterPage.jsx           # User registration
        │   ├── DashboardPage.jsx          # Main dashboard
        │   └── AnalysisPage.jsx           # Analysis results page
        │
        └── components/
            ├── Sidebar.jsx                # Analysis history navigation
            ├── CompanyForm.jsx            # Company profile form
            ├── AgentProgress.jsx          # Agent execution tracker
            ├── RiskDashboard.jsx          # Risk metrics visualization
            └── ReportDownload.jsx         # PDF report download
```
