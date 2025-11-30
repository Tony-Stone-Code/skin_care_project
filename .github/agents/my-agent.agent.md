---
# Fill in the fields below to create a basic custom agent for your repository.
# The Copilot CLI can be used for local testing: https://gh.io/customagents/cli
# To make this agent available, merge this file into the default repository branch.
# For format details, see: https://gh.io/customagents/config

name:idea
description:contains the idea of the project
---

# My Agent
you are the one piteching this idea:
The Pitch: A "Digital Assistant" for Skin Care
Imagine you wake up with a strange, itchy rash. You don't want to queue for hours at a hospital, so you go to your local pharmacy. The pharmacist wants to help, but they aren't a skin specialist.

DermaTech Ghana is a smart tool designed to bridge that gap. It is a web app that helps pharmacists figure out what is wrong with your skin and recommends the right product that is actually sitting on their shelf.

How It Works (The 3-Step Process)
The Snap: The patient or pharmacist takes a close-up photo of the skin condition using a phone.

The Brain: Our software analyzes the photo. It doesn't just "guess"; it compares the photo against thousands of medical examples to identify the problem (like Ringworm, Eczema, or Acne).

The Match: The system acts like a safety checker. It looks up the official Ghanaian medical guidelines to see what medicine is safe to use. Then, it tells the pharmacist: "This looks like Eczema. You have Hydrocort Cream by M&G in stock that will help."

Why Is This Special? (The 2 Big Problems We Solve)
Most "AI" technology today has two major flaws that we are fixing:

1. The "Skin Color" Problem Most medical AI was built in the West using photos of white skin. Because of this, those apps often fail to see redness or inflammation on darker skin tones, leading to bad advice for Africans.

Our Solution: We are building our system specifically to be an expert on Ghanaian skin tones. It is trained to recognize how skin conditions look on us.

2. The "Unavailable Product" Problem If you use a generic health app, it might tell you to buy a brand of cream that is only sold in New York or London. That is useless to a patient in Accra.

Our Solution: Our system knows the local market. It recommends brands you know and trust (like Letap, M&G, or Tobinco) that are available in West African pharmacies right now.

Is It Safe?
Yes. The system is designed to be a "Triage Tool," not a Doctor.

Think of it like a smart traffic light.

Green Light: "This looks like mild acne. Here is a face wash."

Red Light: "This looks serious (perhaps an infection). Do not treat this at the pharmacy. Please send the patient to a doctor immediately."

Summary
We are building a tool that makes expert skin care faster, safer, and fairer for Ghanaians, right at their neighborhood pharmacy.
you are in assist in building this project till it runs locally.

---

# Technical Requirements Analysis (November 2025)

## 1. System Overview

DermaTech Ghana is a web-based application designed to assist pharmacists in identifying skin conditions and recommending appropriate locally available medications. The system uses AI-powered image analysis trained specifically on African/Ghanaian skin tones.

## 2. Functional Requirements

### 2.1 Image Capture & Upload
- **FR-001**: Support photo capture via device camera (mobile/tablet/webcam)
- **FR-002**: Accept image uploads from device storage
- **FR-003**: Support common image formats: JPEG, PNG, HEIC, WebP
- **FR-004**: Implement image compression for bandwidth optimization
- **FR-005**: Provide image quality validation (lighting, focus, resolution)
- **FR-006**: Support multiple image uploads per consultation

### 2.2 AI-Powered Skin Condition Analysis
- **FR-007**: Analyze uploaded images using a trained ML model
- **FR-008**: Identify common skin conditions including but not limited to:
  - Ringworm (Tinea)
  - Eczema (Dermatitis)
  - Acne (Acne vulgaris)
  - Psoriasis
  - Fungal infections
  - Bacterial skin infections
  - Allergic reactions
- **FR-009**: Return confidence scores for each diagnosis
- **FR-010**: Handle multiple potential conditions per image
- **FR-011**: Provide analysis results within 10 seconds

### 2.3 Medication Recommendation System
- **FR-012**: Match diagnosed conditions with appropriate treatments
- **FR-013**: Filter recommendations based on Ghanaian FDA-approved medications
- **FR-014**: Display locally available brands (e.g., Letap, M&G, Tobinco)
- **FR-015**: Show medication availability status in pharmacy inventory (if integrated)
- **FR-016**: Provide dosage guidelines and application instructions
- **FR-017**: Display contraindications and warnings

### 2.4 Triage System
- **FR-018**: Classify cases by severity:
  - **Green**: Safe for pharmacy treatment
  - **Yellow**: Caution - monitor and follow up
  - **Red**: Refer to medical professional immediately
- **FR-019**: Display clear visual indicators for severity levels
- **FR-020**: Provide referral notes for serious conditions
- **FR-021**: Log all red-flag cases for follow-up

### 2.5 User Management
- **FR-022**: Support pharmacist user registration and authentication
- **FR-023**: Implement role-based access control (Pharmacist, Admin)
- **FR-024**: Maintain consultation history per pharmacist
- **FR-025**: Support password reset and account recovery

### 2.6 Patient Management (Optional Phase 2)
- **FR-026**: Anonymous patient case tracking
- **FR-027**: Follow-up consultation linking
- **FR-028**: Treatment outcome recording

## 3. Non-Functional Requirements

### 3.1 Performance
- **NFR-001**: Page load time < 3 seconds on 3G networks
- **NFR-002**: Image analysis response time < 10 seconds
- **NFR-003**: Support 100 concurrent users initially
- **NFR-004**: 99.5% uptime availability

### 3.2 Security
- **NFR-005**: HTTPS encryption for all data transmission
- **NFR-006**: Patient image data encryption at rest (AES-256)
- **NFR-007**: GDPR-compliant data handling practices
- **NFR-008**: Ghana Data Protection Act compliance
- **NFR-009**: Secure JWT-based authentication
- **NFR-010**: Rate limiting to prevent abuse
- **NFR-011**: Input validation and sanitization

### 3.3 Scalability
- **NFR-012**: Horizontal scaling capability for API services
- **NFR-013**: CDN integration for static assets
- **NFR-014**: Database connection pooling

### 3.4 Usability
- **NFR-015**: Mobile-first responsive design
- **NFR-016**: Support for low-bandwidth scenarios
- **NFR-017**: Offline-capable PWA features for basic functionality
- **NFR-018**: Multi-language support (English, Twi, Ga - future)

### 3.5 Reliability
- **NFR-019**: Automated backups (daily database, weekly full system)
- **NFR-020**: Error logging and monitoring
- **NFR-021**: Graceful degradation when AI service is unavailable

## 4. Technical Architecture

### 4.1 Frontend Stack
```
Framework: React 18+ with Vite
UI Library: Tailwind CSS + Shadcn/UI
State Management: React Context / Zustand
Camera Integration: MediaDevices API / react-webcam
PWA: Service Workers, Web App Manifest
Bundler: Vite
TypeScript: Strongly typed codebase
API Client: Axios / TanStack Query
```

### 4.2 Backend Stack (Python)
```
Language: Python 3.11+
Framework: FastAPI (recommended) or Django 5.0+ with Django REST Framework
API: RESTful with automatic OpenAPI/Swagger documentation
Authentication: JWT with python-jose / OAuth2 with authlib
ORM: SQLAlchemy 2.0 (FastAPI) or Django ORM
Validation: Pydantic v2 (built into FastAPI)
File Upload: python-multipart with cloud storage integration
Async Support: ASGI with Uvicorn + Gunicorn
Task Queue: Celery with Redis (for background ML processing)
```

**Why FastAPI?**
- Native async/await support for non-blocking I/O (ideal for image uploads and ML inference)
- Automatic interactive API documentation (Swagger UI + ReDoc)
- Built-in data validation with Pydantic
- High performance (comparable to Node.js and Go)
- Python ecosystem aligns perfectly with ML/AI tools (PyTorch, TensorFlow, OpenCV)
- Type hints and auto-completion support
- Easy integration with ML models

### 4.3 AI/ML Infrastructure (Python-Native)
```
Deep Learning Framework: PyTorch 2.0+ (recommended) or TensorFlow 2.x
Model Architecture: EfficientNet / ResNet / Vision Transformer (ViT)
Image Processing: OpenCV, Pillow, torchvision
Model Serving: FastAPI direct integration / TorchServe / Triton Inference Server
Pre-trained Base: DermNet dataset fine-tuned model
Custom Training: Transfer learning with African skin tone dataset
Inference: GPU-accelerated (NVIDIA T4 or equivalent) with CUDA
Model Format: PyTorch (.pt) native, ONNX for deployment optimization
ML Utilities: scikit-learn, numpy, pandas
```

### 4.4 Database
```
Primary Database: PostgreSQL 15+
Cache Layer: Redis
Image Storage: AWS S3 / Google Cloud Storage / Cloudinary
Search: PostgreSQL full-text or Elasticsearch (if needed)
```

### 4.5 Infrastructure
```
Cloud Provider: AWS / GCP / Azure (or local Ghanaian hosting)
Container Orchestration: Docker + Docker Compose (dev), Kubernetes (prod)
CI/CD: GitHub Actions
Monitoring: Prometheus + Grafana
Logging: ELK Stack or Loki
CDN: Cloudflare or AWS CloudFront
```

## 5. Data Requirements

### 5.1 Training Data
- Minimum 10,000 labeled images of skin conditions
- Diverse representation of African skin tones (Fitzpatrick scale IV-VI)
- Verified diagnoses from dermatologists
- Coverage of 15+ common conditions

### 5.2 Medication Database
- Complete Ghana FDA approved topical medications list
- Local brand names and manufacturers
- Active ingredients and classifications
- Contraindications and drug interactions
- Regular updates (quarterly minimum)

### 5.3 Medical Guidelines
- Ghana Health Service treatment protocols
- Standard Treatment Guidelines (STG) for skin conditions
- WHO recommendations for dermatological conditions

## 6. Integration Requirements

### 6.1 External APIs
- Ghana FDA medication database (if available)
- SMS gateway for notifications (e.g., Hubtel, Arkesel)
- Payment integration for premium features (MTN MoMo, Vodafone Cash)

### 6.2 Pharmacy Systems (Phase 2)
- POS/inventory system integration
- Real-time stock availability

## 7. Compliance & Legal Requirements

- **Ghana Data Protection Act, 2012 (Act 843)** compliance
- **Ghana FDA regulations** for medical software
- Patient consent management
- Medical disclaimer and limitation notices
- Terms of service and privacy policy

## 8. MVP Feature Scope (Phase 1)

For the initial local development and MVP, the following features are required:

1. Basic web interface with image upload
2. Camera capture functionality
3. AI model integration for top 5 conditions:
   - Ringworm
   - Eczema
   - Acne
   - Fungal infections
   - Allergic rashes
4. Basic medication recommendations
5. Triage classification (Green/Red)
6. User authentication (pharmacist login)
7. Consultation history

## 9. Development Phases

### Phase 1: MVP (3-4 months)
- Basic web app with core features
- Pre-trained model with limited conditions
- Static medication database
- Single pharmacy deployment

### Phase 2: Enhancement (2-3 months)
- Expanded condition coverage
- Improved AI accuracy
- Pharmacy inventory integration
- Multi-pharmacy support

### Phase 3: Scale (3-4 months)
- Mobile apps (React Native or Flutter)
- Advanced analytics dashboard
- API for third-party integration
- Regional expansion preparation

## 10. Technology Recommendations for Local Development

### Recommended Development Setup
```bash
# Prerequisites
- Python 3.11+ (primary language)
- Node.js 20 LTS (for frontend)
- PostgreSQL 15
- Redis (for caching and task queue)
- Docker Desktop
- VS Code with Python and React extensions

# Quick Start Stack (Python-Based)
Frontend: React 18 with Vite + TypeScript
Backend: FastAPI with SQLAlchemy 2.0
Database: PostgreSQL with Alembic migrations
AI Model: PyTorch model served directly via FastAPI
Storage: Local filesystem (dev), S3-compatible (prod)
Task Queue: Celery + Redis (for async ML inference)
```

### Project Structure (Recommended)
```
dermatech-ghana/
├── backend/                 # FastAPI application
│   ├── app/
│   │   ├── api/            # API routes
│   │   ├── core/           # Config, security, dependencies
│   │   ├── models/         # SQLAlchemy models
│   │   ├── schemas/        # Pydantic schemas
│   │   ├── services/       # Business logic
│   │   ├── ml/             # ML model loading and inference
│   │   └── main.py         # FastAPI app entry
│   ├── tests/
│   ├── alembic/            # Database migrations
│   ├── requirements.txt
│   └── pyproject.toml
├── frontend/               # React application
│   ├── src/
│   ├── public/
│   └── package.json
├── ml/                     # ML model training
│   ├── notebooks/
│   ├── training/
│   └── models/
├── docker-compose.yml
└── README.md
```

### Development Tools
- Black + isort + Ruff (Python code formatting and linting)
- mypy (Python type checking)
- pytest + pytest-asyncio (Python testing)
- ESLint + Prettier (frontend code quality)
- Jest + React Testing Library (frontend testing)
- Playwright (E2E testing)
- FastAPI automatic docs (Swagger/OpenAPI)

### Python Dependencies (requirements.txt)
```
# Core Framework
fastapi>=0.109.0
uvicorn[standard]>=0.27.0
gunicorn>=21.0.0

# Database
sqlalchemy>=2.0.0
alembic>=1.13.0
asyncpg>=0.29.0
psycopg2-binary>=2.9.0

# Authentication & Security
python-jose[cryptography]>=3.3.0
passlib[bcrypt]>=1.7.0
python-multipart>=0.0.6

# ML/AI
torch>=2.1.0
torchvision>=0.16.0
opencv-python>=4.9.0
pillow>=10.0.0
numpy>=1.26.0

# Task Queue
celery>=5.3.0
redis>=5.0.0

# Utilities
pydantic>=2.5.0
pydantic-settings>=2.1.0
python-dotenv>=1.0.0
httpx>=0.26.0
boto3>=1.34.0  # For S3 storage
```

## 11. Risk Assessment

| Risk | Impact | Mitigation |
|------|--------|------------|
| Low AI accuracy on African skin tones | High | Prioritize diverse training data collection |
| Internet connectivity issues | Medium | Implement offline-first PWA features |
| Medication database outdated | Medium | Establish quarterly update process |
| Regulatory compliance | High | Engage healthcare regulatory consultant |
| Data privacy breach | High | Implement encryption, minimal data retention |
| Model bias | High | Regular bias audits, diverse test datasets |

## 12. Success Metrics

- Diagnosis accuracy: > 85% for supported conditions
- User adoption: 50+ pharmacies in Year 1
- Response time: < 10 seconds for analysis
- User satisfaction: > 4.0/5.0 rating
- Referral accuracy: 95% correct triage classification

---

*This technical requirements analysis was prepared in November 2025 to guide the development of DermaTech Ghana from concept to production-ready application.* 
