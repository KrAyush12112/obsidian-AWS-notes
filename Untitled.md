# Nestibly: The Modern Home Sharing Platform

Nestibly is a full-stack, role-based application designed to connect property hosts with guests looking for short-term stays. Built on the MERN stack principles with robust security features, Nestibly ensures a seamless and reliable booking experience.

## 🌟 Key Features

### 1. Secure Authentication & Authorization

- **Role-Based Access Control (RBAC):** Users are classified as either a `Host` or a `Guest`. Access to property management or booking features is restricted based on their assigned role.
    
- **Email OTP Verification:** A secure two-step signup process using **Resend/SendGrid** ensures all registered emails are valid, mitigating spam and enhancing security.
    
- **Password Security:** All user passwords are encrypted using **BcryptJS** before being stored in the database.
    

### 2. Robust Booking Workflow (Request-to-Book)

- **Detailed Availability Check:** Guests can search and filter homes based on location, capacity, bedrooms, and real-time booking date availability.
    
- **Pending Requests:** The system operates on a Request-to-Book model. Guest requests are initially saved with a `pending` status.
    
- **Host Management:** Hosts have a dedicated dashboard to view, accept, or reject booking requests made against their properties, ensuring quality control.
    

### 3. Listing Management & Cloud Storage

- **User-Specific Listings:** Hosts can only view and manage their own properties.
    
- **Multi-Image Upload:** Hosts can upload multiple images for a single listing, which are securely stored on **AWS S3 (Simple Storage Service)**.
    
- **Storage Cleanup:** Old images are automatically deleted from the S3 bucket when a listing is updated or removed, ensuring storage efficiency.
    

### 4. Technical Resilience

- **Mongoose Data Modeling:** Utilizes Mongoose Schemas for data validation and relationship management (including embedding favorites directly within the User Model for fast retrieval).
    
- **Express Validator:** Frontend form inputs are checked early in the request lifecycle, ensuring clean and safe data reaches the controller.
    

## 🛠️ Technology Stack

| **Category** | **Technology** | **Purpose** | | **Backend** | Node.js, Express.js | Server-side logic and routing. | | **Database** | MongoDB, Mongoose | Flexible NoSQL data storage and object modeling. | | **Authentication** | BcryptJS, Express Session | Password hashing and user state management. | | **Storage** | **AWS S3** | Scalable, reliable, and centralized image storage. | | **Frontend** | EJS Templating, Tailwind CSS | Dynamic views and fully responsive UI design. |

## 🚀 Getting Started (Deployment)

To run this project locally, follow these steps:

### Prerequisites

1. Node.js (LTS version)
    
2. MongoDB Server (Local or MongoDB Atlas)
    
3. AWS S3 Bucket & Credentials (for image uploads)
    
4. SendGrid/Resend API Key (for OTP email service)
    

### Setup

1. **Clone the Repository:**
    
    ```
    git clone [YOUR-REPO-URL]
    cd nestibly
    
    
    ```
    
2. **Install Dependencies:**
    
    ```
    npm install
    
    
    ```
    
3. **Configure Environment Variables:** Create a `.env` file in the root directory and add your secrets:
    
    ```
    # Database
    MONGO_URI=mongodb://localhost:27017/nestibly_db
    
    # Express Session Secret
    SESSION_SECRET='your_super_long_random_secret'
    
    # Email Service (Resend/SendGrid)
    RESEND_API_KEY='your_resend_api_key'
    # Optional: AWS S3 Configuration if using local disk storage
    
    
    ```
    
4. **Run the Application:**
    
    ```
    node app.js
    # OR
    npm start # if defined in package.json
    
    
    ```
    

The application will be accessible at `http://localhost:3000`.