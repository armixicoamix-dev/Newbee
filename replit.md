# GlobalsBuy E-Commerce Platform

## Overview
A fully functional e-commerce website with admin panel, real-time chat system, product management, editable user profiles, payment system, and order tracking with customizable stages.

## Admin Credentials
- **Login:** admin
- **Password:** Stored in ADMIN_PASSWORD secret (environment variable)

## Technology Stack
- **Frontend:** React, TypeScript, Tailwind CSS, Wouter (routing), TanStack Query
- **Backend:** Express.js, TypeScript
- **Database:** PostgreSQL with Drizzle ORM
- **UI Components:** Radix UI, shadcn/ui
- **Styling:** Tailwind CSS with custom design system

## Project Structure
```
├── client/               # Frontend React application
│   ├── src/
│   │   ├── components/   # Reusable UI components
│   │   ├── hooks/        # Custom React hooks
│   │   ├── lib/          # Utilities and API client
│   │   └── pages/        # Page components
├── server/               # Backend Express application
│   ├── routes.ts         # API routes
│   ├── storage.ts        # Database operations
│   ├── db.ts             # Database connection
│   └── index.ts          # Server entry point
├── shared/               # Shared code between client and server
│   └── schema.ts         # Drizzle database schema
```

## Features

### User Features
- User registration and authentication
- Product catalog with filtering, sorting, and search
- Shopping cart
- Balance top-up with receipt upload and admin approval workflow
- Order placement and tracking
- Real-time chat support
- User profile editing
- View balance request history and status

### Admin Features
- Dashboard with statistics
- Product management (CRUD) with multiple images per product
- Order management with customizable tracking stages
- User management with ban/unban/delete functionality
- Admin hierarchy: Super admin can assign/revoke admin permissions
- Balance request approval workflow (view receipt, approve/reject)
- IP tracking for user logins
- Chat support (respond to customer inquiries)
- Review moderation
- Activity logs
- Settings (payment card, contact info)
- CMS for site content editing

## API Endpoints

### Authentication
- POST /api/auth/register - Register new user
- POST /api/auth/login - User login
- POST /api/auth/logout - User logout
- GET /api/auth/me - Get current user

### Products
- GET /api/products - List products (with filters)
- GET /api/products/:id - Get single product
- GET /api/products/categories - List categories
- GET /api/products/brands - List brands

### Cart
- GET /api/cart - Get user's cart
- POST /api/cart - Add to cart
- PUT /api/cart/:productId - Update quantity
- DELETE /api/cart/:productId - Remove from cart

### Orders
- GET /api/orders - List user's orders
- POST /api/orders - Create order
- GET /api/orders/:id - Get order details

### Chat
- GET /api/chats - List user's chats
- POST /api/chats - Create new chat
- GET /api/chats/:id - Get chat with messages
- POST /api/chats/:id/messages - Send message

### Balance
- POST /api/balance/request - Request balance top-up (with receipt upload)
- GET /api/balance/requests - Get user's balance requests

### Payments
- GET /api/payment-methods - Get available payment methods
- POST /api/payments/create - Create payment for order (redirect to provider)
- GET /api/payments/:orderId/status - Check payment status
- POST /api/webhooks/yookassa - YooKassa webhook
- POST /api/webhooks/cloudpayments/pay - CloudPayments webhook
- POST /api/webhooks/robokassa/result - Robokassa result callback

### Admin API
All admin endpoints require authentication and admin role:
- GET /api/admin/stats - Dashboard statistics
- GET/POST/PUT/DELETE /api/admin/products - Product management
- POST /api/admin/products/:id/images - Add product image
- DELETE /api/admin/products/:id/images/:imageId - Delete product image
- GET/PUT /api/admin/orders - Order management
- GET /api/admin/users - List users with ban status, IP, admin status
- POST /api/admin/users/:id/ban - Ban user
- POST /api/admin/users/:id/unban - Unban user
- DELETE /api/admin/users/:id - Delete user
- POST /api/admin/users/:id/set-admin - Set/revoke admin permissions
- GET /api/admin/balance-requests - List all balance requests
- POST /api/admin/balance-requests/:id/process - Approve/reject balance request
- GET/PUT /api/admin/settings - Settings management
- GET/PUT /api/admin/tracking-stages - Tracking stages configuration
- POST /api/admin/chats/:id/messages - Send admin message

## Database Schema
- users - User accounts (with isBanned, banReason, isSuperAdmin, adminPermissions, lastLoginIp, lastLoginAt)
- products - Product catalog
- productImages - Multiple images per product
- categories - Product categories
- orders - Customer orders
- orderItems - Order line items
- cart - Shopping cart items
- wishlist - User wishlists
- reviews - Product reviews
- chats - Support chat sessions
- chatMessages - Chat messages
- userLogs - Activity logs
- settings - System settings
- balanceRequests - User balance top-up requests with receipt images

## Running the Application
```bash
npm run dev
```
The application will be available on port 5000.

## CMS (Content Management System)

### Features
- Content groups for organizing entries (e.g., "hero", "features")
- Content entries with multiple types: text, rich_text, image, link, json
- Media library for uploading and managing images
- Draft/publish workflow for content entries
- Frontend content consumption via useContent hook with fallback values

### Tables
- content_groups - Organize content by sections
- content_entries - Individual content items (text, images, etc.)
- media_assets - Uploaded media files with metadata

### Admin Content Tab
Navigate to Admin Panel > Контент to:
- Create and manage content groups
- Add/edit content entries (text, images, links)
- Upload media to the library
- Publish or save drafts

## Recent Changes
- 2025-12-10: Initial implementation with full e-commerce functionality
- 2025-12-10: Fixed nested `<a>` tag issues in Header and Footer components
- 2025-12-10: Added public settings endpoint for payment information
- 2025-12-10: Added admin-specific chat messaging endpoint
- 2025-12-10: Added tracking stages management endpoints
- 2025-12-10: Added CMS system for managing site content, images, and text
- 2025-12-10: Added multiple product images support (productImages table)
- 2025-12-10: Added balance request system with receipt upload and admin approval workflow
- 2025-12-10: Added user ban/unban/delete functionality with admin UI
- 2025-12-10: Added admin hierarchy with super admin and customizable permissions
- 2025-12-10: Added IP tracking for user logins (lastLoginIp, lastLoginAt fields)
- 2025-12-11: Fixed SQL error in getLogs using drizzle's inArray for proper array handling
- 2025-12-11: Fixed nested `<a>` tag hydration errors in login/register pages
- 2025-12-11: Fixed avatar button border causing layout shift on hover
- 2025-12-11: Added drag-and-drop ImageDropzone component for product image uploads
- 2025-12-11: Added file upload endpoint for product images with multer
- 2025-12-11: Product page now displays image gallery from productImages table
- 2025-12-11: Created dedicated New Arrivals page with featured new products
- 2025-12-11: Created Brands page showcasing partner brands by category (clothing, shoes, accessories, electronics)
- 2025-12-11: Redesigned New Arrivals page with modern card grid layout matching site design
- 2025-12-11: Enhanced CMS admin panel with page-based filtering (all pages selectable)
- 2025-12-11: Added multi-provider payment system (YooKassa, CloudPayments, Robokassa)
- 2025-12-11: Added payment method selection in checkout with support for MIR cards
- 2025-12-11: Added payment success/failed pages with status checking
- 2025-12-11: Added webhook handlers for all payment providers
- 2025-12-11: Security fixes: admin password via env var, session secret required, balance topup admin-only
- 2025-12-11: Updated delivery messaging - cost now included in product price, removed 10K threshold
- 2025-12-11: Enhanced return policy - 30 day full refund for defects or non-original items
- 2025-12-11: Added comprehensive iOS Safari compatibility (viewport-fit, -webkit fixes, 16px inputs)
- 2025-12-11: Made admin panel fully responsive for mobile/tablet/desktop devices
- 2025-12-11: Admin tabs now horizontally scroll with icon-only display on mobile
- 2025-12-11: All admin sections (products, orders, users, balance, chats, reviews, logs) optimized for mobile

## Delivery & Return Policy
- **Delivery:** Cost is included in product price, no additional fees
- **Return Policy:** 30-day return for defective items or non-original products with full refund

## Payment System

### Supported Payment Providers
1. **Balance** - Pay from account balance
2. **YooKassa** - Russian payment system supporting МИР, Visa, MasterCard, СБП, ЮMoney
3. **CloudPayments** - МИР, Visa, MasterCard, Apple Pay, Google Pay
4. **Robokassa** - Payment aggregator with multiple methods

### Required Environment Variables for Payments
```
YOOKASSA_SHOP_ID - YooKassa shop ID
YOOKASSA_SECRET_KEY - YooKassa secret key
CLOUDPAYMENTS_PUBLIC_ID - CloudPayments public ID
CLOUDPAYMENTS_API_SECRET - CloudPayments API secret
ROBOKASSA_MERCHANT_LOGIN - Robokassa merchant login
ROBOKASSA_PASSWORD1 - Robokassa password 1
ROBOKASSA_PASSWORD2 - Robokassa password 2
ROBOKASSA_TEST_MODE - Set to 'true' for test mode
```

### Webhook URLs to Configure
- YooKassa: `https://your-domain/api/webhooks/yookassa`
- CloudPayments: `https://your-domain/api/webhooks/cloudpayments/pay`
- Robokassa Result URL: `https://your-domain/api/webhooks/robokassa/result`
- Robokassa Success URL: `https://your-domain/api/webhooks/robokassa/success`
- Robokassa Fail URL: `https://your-domain/api/webhooks/robokassa/fail`

## User Preferences
- Russian language interface
- Dark theme design
- Modern, futuristic UI with glass-morphism effects
