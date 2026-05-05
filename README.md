# SAVANNAH-BACKEND
# 🏢 Savannah Property Management System - Backend

[![FastAPI](https://img.shields.io/badge/FastAPI-0.136.0-009688?logo=fastapi)](https://fastapi.tiangolo.com/)
[![Python](https://img.shields.io/badge/Python-3.12+-3776AB?logo=python)](https://www.python.org/)
[![M-Pesa](https://img.shields.io/badge/M--Pesa-Daraja_API-4CAF50)](https://developer.safaricom.co.ke/)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

## 📌 Overview

The **Savannah Property Management System Backend** is a RESTful API built with **FastAPI** that powers a complete property management solution. It handles tenant management, rent collection, payment reconciliation, and integrates with **Safaricom's M-Pesa Daraja API** for automated mobile money payments.

> **Note:** This is the backend repository. The frontend React application can be found [here](https://github.com/Gittechie-111/SAVANNAH-FRONTEND).

---

## ✨ Features

- **🔐 Authentication** – JWT-based user authentication with role-based access (Admin, Accountant, Tenant)
- **🏘️ Property Management** – CRUD operations for properties and rental units
- **💰 Rent Collection** – Record manual payments and track tenant balances
- **📱 M-Pesa Integration** – Automated STK Push payments via Safaricom Daraja API
- **📊 Dashboard Analytics** – Real-time statistics on occupancy, collections, and arrears
- **🔄 Webhook Support** – Automatic payment reconciliation via M-Pesa callbacks
- **📝 Transaction History** – Complete audit trail of all payments

---

## 🛠️ Tech Stack

| Category | Technology |
|----------|------------|
| **Framework** | FastAPI 0.136.0 |
| **Language** | Python 3.12+ |
| **Database** | MongoDB with Mongoose ODM|
| **Authentication** | JWT (PyJWT) |
| **Payment Gateway** | Safaricom Daraja API (M-Pesa) |
| **HTTP Client** | Requests |
| **Server** | Uvicorn |
| **Deployment** | Render.com |

---

## 🚀 Getting Started

### Prerequisites

- Python 3.12 or higher
- MongoDB instance (local or cloud)
- Safaricom Developer Account (for M-Pesa)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/Gittechie-111/SAVANNAH-BACKEND.git
   cd SAVANNAH-BACKEND


    Create virtual environment
    bash

    python -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate

    Install dependencies
    bash

    pip install -r requirements.txt

    Set up environment variables
    Create a .env file in the root directory:
    env

    # MongoDB
    MONGODB_URI=MONGO_URI=mongodb+srv://trizahmuseve69_db_user:BtRDNmFlNTZidKh6@cluster0.cakq9l5.mongodb.net/?appName=Cluster0
    DATABASE_NAME=savannah_pms

    # JWT
    SECRET_KEY="savannah_property_management_secret_key_2024_32_bytes_minimum"

   # M-Pesa Daraja API Sandbox Credentials
    MPESA_CONSUMER_KEY=5YqIDEptj6kVXfM6GWDPN2cN5NgtG0vGw8p6UHWU3EgJVtee
    MPESA_CONSUMER_SECRET=Jazo8BlibqokGn3AEPNPSBXRlFzPIAnXrFY1x6PG7viXFrw1aHeClJ8UIYQhVGAA
    MPESA_PASSKEY=bfb279f9aa9bdbcf158e97dd71a467cd2e0c893059b10f78e6b72ada1ed2c919
    MPESA_SHORTCODE=174379
    
    # Test Credentials (for sandbox only)
    MPESA_TEST_PHONE=254708374149      # Main test phone [citation:3]
    MPESA_TEST_PHONE_ALT=254703459309  # Alternate test phone
    MPESA_TEST_PIN=174379               # Default test PIN [citation:3]
    
    # Callback URL (use ngrok for local testing)
    MPESA_CALLBACK_URL=https://savannah-backend-kcxm.onrender.com/api/mpesa/callback
    MPESA_ENV=sandbox
   
    # CONNECTION TO MONGODB
    MONGO_URI=mongodb+srv://trizahmuseve69_db_user:BtRDNmFlNTZidKh6@cluster0.cakq9l5.mongodb.net/?appName=Cluster0
    PORT=3000

    Run the server
    bash

    uvicorn main:app --reload --port 8000

    Access the API documentation

        Swagger UI: http://localhost:8000/docs

        ReDoc: http://localhost:8000/redoc

📡 API Endpoints
Authentication
Method	Endpoint	Description
POST	/api/auth/login	Login with email & password
POST	/api/auth/register	Register new tenant account
Dashboard
Method	Endpoint	Description
GET	/api/dashboard/stats	Get KPI statistics
GET	/api/dashboard/monthly-collections	Get 6-month collection trends
Properties & Units
Method	Endpoint	Description
GET	/api/properties	List all properties
GET	/api/units	List all rental units
GET	/api/arrears	List tenants with outstanding balances
Transactions
Method	Endpoint	Description
GET	/api/transactions	Get all payment transactions
POST	/api/payments/initiate	Record a manual payment
M-Pesa Integration
Method	Endpoint	Description
POST	/api/mpesa/stkpush	Initiate STK Push to tenant's phone
GET	/api/mpesa/status/{checkout_id}	Check payment status
POST	/api/mpesa/callback	Webhook for M-Pesa confirmation
GET	/api/mpesa/pending	View pending transactions (Admin only)
🧪 Testing M-Pesa Integration (Sandbox)

    Start ngrok to expose your local server:
    bash

    ngrok http 8000

    Update MPESA_CALLBACK_URL in your .env file with your ngrok URL:
    text

    MPESA_CALLBACK_URL=https://your-ngrok-id.ngrok.io/api/mpesa/callback

    Restart your FastAPI server

    Use test credentials in the frontend:

        Test Phone: 254708374149

        Test PIN: 174379

    Simulate payment at Safaricom Developer Portal

📁 Project Structure
text

SAVANNAH-BACKEND/
├── main.py                    # FastAPI application entry point
├── mpesa_service.py           # M-Pesa Daraja API integration
├── models/                    # MongoDB/Mongoose models
│   ├── User.js
│   ├── Property.js
│   ├── Unit.js
│   └── Transaction.js
├── requirements.txt           # Python dependencies
├── .env                       # Environment variables (gitignored)
├── .env.example               # Example environment variables
└── README.md                  # This file

🔐 Environment Variables Reference
Variable	Description	Required
MONGODB_URI	MongoDB connection string	✅ Yes
DATABASE_NAME	Name of the database	✅ Yes
SECRET_KEY	JWT signing secret	✅ Yes
MPESA_CONSUMER_KEY	Safaricom API consumer key	For M-Pesa
MPESA_CONSUMER_SECRET	Safaricom API consumer secret	For M-Pesa
MPESA_PASSKEY	M-Pesa online passkey	For M-Pesa
MPESA_SHORTCODE	Paybill/Till number	For M-Pesa
MPESA_ENV	sandbox or production	For M-Pesa
MPESA_CALLBACK_URL	Webhook callback URL	For M-Pesa
MPESA_TEST_PHONE	Test phone for sandbox	Optional
🚢 Deployment

This backend is deployed on Render.com. To deploy your own instance:

    Push your code to GitHub

    Create a new Web Service on Render

    Connect your repository

    Set the following:

        Build Command: pip install -r requirements.txt

        Start Command: uvicorn main:app --host 0.0.0.0 --port 10000

    Add all environment variables in Render dashboard

    Click Deploy

🧑‍💻 Default Test Accounts
Role	Email	Password
Admin	admin@savannah.co.ke	admin123
Accountant	accountant@savannah.co.ke	account123
Tenant	tenant001@savannah.co.ke	tenant123

    ⚠️ Important: Change these credentials in production!

🤝 Contributing

    Fork the repository

    Create a feature branch (git checkout -b feature/amazing-feature)

    Commit your changes (git commit -m 'Add some amazing feature')

    Push to the branch (git push origin feature/amazing-feature)

    Open a Pull Request

📄 License

This project is licensed under the MIT License - see the LICENSE file for details.
🙏 Acknowledgements

    Safaricom Daraja API – M-Pesa integration

    FastAPI – Modern web framework

    Render – Hosting platform

📞 Contact

Developer: Gittechie-111
Project Link: https://github.com/Gittechie-111/SAVANNAH-BACKEND

⭐ If you found this project helpful, please give it a star on GitHub!   
