# QuickBite Food Delivery App

A modern, scalable food delivery web application built with React, Tailwind CSS, and Netlify Functions.

## Features

- **User Module**: Browse restaurants, search, filter, add to cart, checkout (Stripe), and track orders.
- **Admin Module**: Dashboard with analytics, manage restaurants, and view orders.
- **Delivery Module**: Accept/reject orders, update delivery status.
- **Backend**: Serverless API using Netlify Functions and MongoDB Atlas.

## Tech Stack

- **Frontend**: React.js, Tailwind CSS, React Router, Framer Motion
- **Backend**: Netlify Functions (Node.js)
- **Database**: MongoDB Atlas
- **Authentication**: JWT
- **Payments**: Stripe

## Local Development

1. Clone the repository
2. Install dependencies:
   ```bash
   npm install
   ```
3. Create a `.env` file based on `.env.example` and add your keys:
   ```env
   MONGODB_URI="your_mongodb_connection_string"
   JWT_SECRET="your_jwt_secret"
   STRIPE_SECRET_KEY="your_stripe_secret_key"
   VITE_STRIPE_PUBLIC_KEY="your_stripe_public_key"
   ```
4. Start the development server:
   ```bash
   npm run dev
   ```
   *Note: To run Netlify functions locally, you can use the Netlify CLI: `netlify dev`*

## Deployment to Netlify

Follow these steps to deploy the application live on Netlify:

### 1. Push to GitHub
Push your local repository to a new GitHub repository.

### 2. Connect to Netlify
1. Log in to [Netlify](https://app.netlify.com/).
2. Click **"Add new site"** > **"Import an existing project"**.
3. Select **GitHub** and authorize Netlify.
4. Choose your repository.

### 3. Configure Build Settings
Netlify should automatically detect the settings from `netlify.toml`, but verify:
- **Base directory**: (leave empty)
- **Build command**: `npm run build`
- **Publish directory**: `dist`
- **Functions directory**: `netlify/functions`

### 4. Set Environment Variables
Before clicking "Deploy", click **"Show advanced"** > **"New variable"** and add all the variables from your `.env` file:
- `MONGODB_URI`
- `JWT_SECRET`
- `STRIPE_SECRET_KEY`
- `VITE_STRIPE_PUBLIC_KEY`

### 5. Deploy
Click **"Deploy site"**. Netlify will build your React app and deploy your serverless functions.

### 6. MongoDB Atlas Setup
Ensure your MongoDB Atlas cluster allows connections from anywhere (IP `0.0.0.0/0`) since Netlify Functions run on dynamic IPs.
1. Go to MongoDB Atlas > Network Access.
2. Click "Add IP Address".
3. Select "Allow Access From Anywhere".

## Architecture Notes

- The frontend is a Single Page Application (SPA) built with Vite.
- API requests are routed to `/.netlify/functions/*` via the proxy configuration in `netlify.toml`.
- Authentication uses JWT tokens. In a production environment, consider storing these in HTTP-only cookies for better security.
