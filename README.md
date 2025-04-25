# Medusa Backend Test Instructions

This project is a technical assessment designed to evaluate your familiarity with [Medusa.js](https://medusajs.com/), an open-source headless commerce engine built for modern e-commerce applications.

## Table of Contents

- [Getting Started](#getting-started)
- [Admin Setup](#-admin-setup)
- [Environment Setup](#-environment-setup)
- [Store API Endpoint](#store-api-endpoint)
- [Admin API Endpoints](#admin-api-endpoints)
- [Sample Response](#sample-response)
- [Submission Guidelines](#submission-guidelines)

---

## Getting Started

Install the project dependencies and run the server using your preferred package manager:

Using **npm**:

```bash
npm install
npm run dev
```

Or using **yarn**:

```bash
yarn install
yarn dev
```

Medusa server will typically run at:

- Admin API: `http://localhost:9000/admin`

---

## Admin Setup

Please create an admin user manually using the Medusa CLI:

```bash
medusa user -e cartsmiths-backend@test.com -p Admin123!
```

---

## Environment Setup

Before running the project, create a `.env` file in the root directory with the following content:

```env
MEDUSA_ADMIN_ONBOARDING_TYPE=default
STORE_CORS=http://localhost:8000,https://docs.medusajs.com
ADMIN_CORS=http://localhost:5173,http://localhost:9000,https://docs.medusajs.com
AUTH_CORS=http://localhost:5173,http://localhost:9000,http://localhost:8000,https://docs.medusajs.com
REDIS_URL=redis://localhost:6379
JWT_SECRET=supersecret
COOKIE_SECRET=supersecret
DATABASE_URL=postgres://<your_pg_username>:<your_pg_password>@localhost/<your_pg_database>
```

> **Replace** `<your_pg_username>`, `<your_pg_password>`, and `<your_pg_database>` with your actual Postgres credentials.

---

## Store API Endpoint

### Endpoint

```
POST /store/create-product
```

### Description

Create a new product with associated variants using Medusa's core services.

### Request Body

```json
{
  "title": "string",
  "description": "string",
  "variants": [
    {
      "title": "string",
      "sku": "string",
      "prices": [
        { "amount": number, "currency_code": "string" }
      ]
    }
  ]
}
```

### Functionality

- Create a product and add variants using Medusa's product workflows
- https://docs.medusajs.com/resources/medusa-workflows-reference

---

## Admin API Endpoints (Protected)

> All admin endpoints require a valid admin token (login via Medusa admin or use bearer token).

### 1. Update Product Description

**Endpoint:**

```
POST /admin/update-product-description
```

**Request Body:**

```json
{
  "product_id": "string",
  "description": "string"
}
```

**Functionality:**

- Updates the `description` of the given product.

---

### 2. Get Products with Expensive Variants

**Endpoint:**

```
GET /admin/product-variants
```

**Functionality:**

- Fetches products where any variant price is greater than **$500**.

---

## Sample Response

```json
{
  "title": "Product Title",
  "description": "This would be the store product description",
  "variants": [
    {
      "title": "Small",
      "sku": "sm-01",
      "prices": [{ "amount": 1500, "currency_code": "usd" }]
    },
    {
      "title": "Large",
      "sku": "lg-01",
      "prices": [{ "amount": 2500, "currency_code": "usd" }]
    }
  ]
}
```

---

## Submission Guidelines

- Push all code to a **public GitHub repository**.
- Ensure all custom API files are under `src/api/` with proper structure.
- Share your GitHub repository link once complete.

---

Happy coding!
