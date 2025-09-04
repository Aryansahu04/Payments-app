# Monexa Payments-apps Monorepo

![Next.js](https://img.shields.io/badge/next.js-000000?style=for-the-badge&logo=next.js&logoColor=white)
![TypeScript](https://img.shields.io/badge/typescript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/tailwindcss-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)
![Prisma](https://img.shields.io/badge/Prisma-2D3748?style=for-the-badge&logo=prisma&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)
![NextAuth.js](https://img.shields.io/badge/NextAuth.js-F39C12?style=for-the-badge&logo=next.js&logoColor=white)
![Turborepo](https://img.shields.io/badge/Turborepo-EF4444?style=for-the-badge&logo=turborepo&logoColor=white)

This monorepo contains a collection of applications and packages designed for a payment system. It includes a bank webhook service, a user application for managing payments and transfers, and shared packages for database interactions, UI components, and configurations.

## Technologies Used

This project leverages the following key technologies:

- **Next.js**: A React framework for building server-side rendered and static web applications.
- **TypeScript**: A strongly typed superset of JavaScript that enhances code quality and maintainability.
- **Tailwind CSS**: A utility-first CSS framework for rapidly building custom designs.
- **Prisma**: A next-generation ORM for Node.js and TypeScript, used for database access.
- **PostgreSQL**: A powerful, open-source object-relational database system.
- **NextAuth.js**: An authentication library for Next.js applications.
- **Turborepo**: A high-performance build system for JavaScript and TypeScript monorepos.

## Applications and Packages

This monorepo is structured into several applications and shared packages:

### Applications

- **`apps/bank-webhook`**: A webhook service that handles incoming notifications from banks, processing transaction confirmations and updates.
- **`apps/user-app`**: The main user-facing application built with Next.js, allowing users to manage their balances, transfer money (P2P), and view transaction history.

### Packages

- **`packages/db`**: Contains the Prisma schema, database migrations, and utilities for interacting with the PostgreSQL database.
- **`packages/eslint-config`**: Shared ESLint configurations for consistent code style across the monorepo.
- **`packages/store`**: Manages application-wide state using Recoil (or similar state management). Includes hooks for balance and other shared states.
- **`packages/typescript-config`**: Reusable TypeScript configurations to ensure consistent TypeScript settings.
- **`packages/ui`**: A collection of reusable UI components (e.g., buttons, cards, text inputs) built with React and Tailwind CSS.

## Setup and Running Instructions

Follow these steps to set up and run the project locally:

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/your-username/Payments-apps.git
    cd Payments-apps
    ```

2.  **Install dependencies:**
    ```bash
    npm install
    ```

3.  **Set up PostgreSQL:**

    You can run PostgreSQL locally using Docker:
    ```bash
    docker run -e POSTGRES_PASSWORD=mysecretpassword -d -p 5432:5432 postgres
    ```

4.  **Environment Variables:**

    Copy the example environment files and update them with your configurations:
    ```bash
    cp .env.example .env # Do this in the root, and also inside apps/bank-webhook and apps/user-app
    ```
    Update the `.env` files with your database URL, NextAuth secret, and other necessary credentials.

5.  **Database Migrations and Seeding:**

    Navigate to the `packages/db` directory and run the migrations and seed the database:
    ```bash
    cd packages/db
    npx prisma migrate dev --name init
    npx prisma db seed
    cd ../../
    ```

6.  **Run the User Application:**

    Start the Next.js user application:
    ```bash
    cd apps/user-app
    npm run dev
    ```

7.  **Run the Bank Webhook (optional, for full functionality):

    If you need to test the bank webhook functionality, start the webhook service:
    ```bash
    cd apps/bank-webhook
    npm run dev
    ```

After these steps, the user application should be accessible at `http://localhost:3000` (or your configured port). You can log in using the credentials provided in `packages/db/prisma/seed.ts` (e.g., phone: `1111111111`, password: `aryan`).

## 🏦 Payment Flow (On-Ramp Simulation)

1. User clicks **Add Money** → creates an `OnRampTransaction` in DB with status **Processing**  
2. User is redirected to a simulated **Bank Page**  
3. Bank (mocked via Express service) calls **webhook** to update transaction status  
4. User’s **balance updates** & transaction marked **Success/Failure**  

---

## 📊 UI Preview  

- **Appbar** with login/logout  
- **Sidebar** navigation: Dashboard, Transactions, Transfer  
- **Balance Card** showing unlocked & locked balance  
- **Add Money Card** to simulate on-ramp transactions  
- **Recent Transactions** panel  

---

## 📌 Future Enhancements  

- 🔄 Real payment gateway integration (Stripe, Razorpay, PayPal)  
- 📱 Mobile-first UI polish  
- 🔔 Notifications for transactions (WebSockets/Push)  
- 💳 P2P Transfers between users  
