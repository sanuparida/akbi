# BillBook MVP - Development Agent Instructions

## 1. Role

You are the primary software development agent for the BillBook MVP.

Your responsibility is to design, implement, test, review, debug, and maintain the application according to the project documentation inside the `.agent/` directory.

You are not only a code generator.

You must understand:

- Product requirements
- Business rules
- Application architecture
- Backend architecture
- Database design
- UI requirements
- API contracts
- Transaction consistency
- Security requirements
- Testing requirements
- Deployment requirements

Before making implementation decisions, use the documentation in `.agent/` as the source of truth.

---

# 2. Product

The product is a lightweight business management and billing application for small and medium-sized businesses, especially businesses that need a simple alternative to complicated ERP/accounting systems.

The MVP focuses on:

- Business/shop management
- User authentication
- Basic user roles
- Customer management
- Supplier management
- Product management
- Inventory management
- Sales and invoicing
- Purchase management
- Payments
- Expenses
- Basic GST support
- Basic reports
- Invoice generation
- Basic notifications

The product should be:

- Simple
- Fast
- Reliable
- Easy to understand
- Mobile-friendly
- Suitable for small businesses
- Easy to operate for non-technical users

---

# 3. Primary MVP Goal

The MVP must support the complete basic business transaction lifecycle:

    Business
        ↓
    Products
        ↓
    Suppliers
        ↓
    Purchase
        ↓
    Inventory
        ↓
    Customers
        ↓
    Sales / Invoice
        ↓
    Payment
        ↓
    Customer Ledger
        ↓
    Reports

The system must maintain consistency between:

- Sales
- Purchases
- Inventory
- Payments
- Customer balances
- Supplier balances
- Expenses
- Reports

---

# 4. Source of Truth

The `.agent/` directory contains project-specific instructions and documentation.

Use the following priority order when making decisions:

1. Explicit user requirement in the current task
2. `business-rules.md`
3. `architecture.md`
4. Relevant feature documentation
5. `backend/transactions.md`
6. `backend/database.md`
7. `backend/api.md`
8. `backend/services.md`
9. `tech-stack.md`
10. `coding-style.md`
11. `testing.md`
12. `roadmap.md`

If two documents conflict:

1. Follow the higher-priority document.
2. Do not silently change the documentation.
3. Mention the conflict.
4. Ask for clarification if the conflict affects implementation correctness.

---

# 5. Required Documentation Reading

Before implementing a feature, determine which documentation files are relevant.

Always read:

- `vision.md`
- `architecture.md`
- `tech-stack.md`
- `folder-structure.md`
- `business-rules.md`

Then read the relevant feature documentation.

For example:

For invoice development:

- `features/invoices.md`
- `features/customers.md`
- `features/inventory.md`
- `features/payments.md`
- `backend/api.md`
- `backend/database.md`
- `backend/services.md`
- `backend/transactions.md`
- `testing.md`

Do not read every documentation file unnecessarily.

Read the minimum relevant documentation required to make a correct implementation.

---

# 6. Existing Code First

Before creating new code:

1. Inspect the repository.
2. Understand the existing folder structure.
3. Search for related functionality.
4. Search for existing models.
5. Search for existing services.
6. Search for existing APIs.
7. Search for existing utilities.
8. Search for existing tests.

Do not create duplicate:

- Models
- Services
- APIs
- Utilities
- Components
- Database tables
- Validation logic

Reuse existing functionality whenever appropriate.

---

# 7. Do Not Assume

Never assume that functionality exists just because documentation mentions it.

Verify the actual repository.

Never assume:

- A database table exists
- An API exists
- A service exists
- A library is installed
- An environment variable exists
- A payment provider is configured
- A frontend component exists
- A test exists

Check the repository before using it.

---

# 8. MVP Scope

The MVP includes:

## Authentication

- Registration
- Login
- Logout
- Password hashing
- Access token
- Refresh token if required
- Basic authentication validation

## Business

- Create business
- View business
- Update business
- Business settings

## Users

- Owner
- Cashier

Basic permission control is required.

## Customers

- Create customer
- Update customer
- Delete customer
- View customer
- Customer transaction history
- Customer outstanding balance

## Suppliers

- Create supplier
- Update supplier
- Delete supplier
- View supplier
- Supplier transaction history
- Supplier outstanding balance

## Products

- Create product
- Update product
- Delete/deactivate product
- Product search
- SKU
- Barcode
- Category
- Unit
- Purchase price
- Selling price
- MRP
- GST rate
- Minimum stock

## Inventory

- Opening stock
- Stock increase
- Stock decrease
- Stock adjustment
- Stock movement history
- Current stock
- Low-stock detection

## Sales

- Create invoice
- Add invoice items
- Calculate subtotal
- Apply discount
- Calculate tax
- Calculate total
- Record payment
- Partial payment
- Full payment
- Cancel invoice
- Invoice history

## Purchase

- Create purchase
- Add purchase items
- Increase stock
- Supplier balance
- Record payment
- Purchase history

## Payments

- Cash
- UPI/manual UPI entry if gateway is not yet integrated
- Bank transfer
- Partial payments
- Payment history
- Payment reference

## Expenses

- Create expense
- Update expense
- Delete expense
- Expense categories
- Expense history

## GST

MVP GST support should include:

- GSTIN
- HSN
- GST rate
- CGST
- SGST
- IGST
- GST-inclusive pricing
- GST-exclusive pricing

Advanced GST functionality should not be implemented unless explicitly requested.

## Reports

MVP reports:

- Sales
- Purchases
- Inventory
- Expenses
- Receivables
- Payables
- Basic profit
- Dashboard summary

---

# 9. Features Outside MVP

Do not implement these unless explicitly requested:

- Advanced accounting
- Full ERP
- Payroll
- Manufacturing
- Advanced warehouse management
- Multi-region deployment
- Complex offline synchronization
- AI forecasting
- AI business assistant
- Advanced GST filing automation
- E-invoice automation
- E-way bill automation
- Advanced UPI integration
- WhatsApp automation
- SMS automation
- Multi-country tax systems

These may be added in later roadmap phases.

---

# 10. Architecture Principles

Use a modular architecture.

The application should separate:

- API layer
- Business/service layer
- Data access layer
- Models
- Schemas
- Utilities
- External integrations

Recommended conceptual structure:

    API
     ↓
    Service
     ↓
    Repository / Data Access
     ↓
    Database

Example:

    POST /invoices
          ↓
    Invoice API
          ↓
    Invoice Service
          ↓
    Inventory Service
          ↓
    Payment Service
          ↓
    Database

Do not put complex business logic directly inside API route handlers.

---

# 11. Backend Architecture

The backend should be organized around business domains.

Recommended domains:

- auth
- businesses
- users
- customers
- suppliers
- products
- inventory
- sales
- purchases
- payments
- expenses
- gst
- reports
- notifications

Each domain should contain only the code related to that domain.

Avoid creating a huge single service containing all business logic.

---

# 12. Database Principles

Use relational database design for core business data.

The primary database should maintain relationships between:

- Businesses
- Users
- Customers
- Suppliers
- Products
- Invoices
- Invoice items
- Purchases
- Purchase items
- Payments
- Expenses
- Stock movements

All business-critical relationships must have appropriate foreign keys.

Use database constraints wherever appropriate.

Examples:

- Unique invoice number per business
- Unique SKU per business
- Valid foreign keys
- Non-negative quantities where applicable
- Required fields
- Valid status values

Do not depend entirely on application-level validation.

---

# 13. Multi-Tenant Data Isolation

Every business's data must remain isolated.

Most business-related tables should contain:

    business_id

Example:

    invoices
    --------
    id
    business_id
    customer_id
    invoice_number
    total

Every query must enforce business ownership.

Never allow:

    GET /invoices/123

to return invoice 123 unless invoice 123 belongs to the authenticated user's business.

Never trust a `business_id` supplied directly by the client.

Determine the active business from the authenticated user's authorized context.

---

# 14. Authentication

Authentication must be handled centrally.

Passwords must never be stored as plain text.

Use secure password hashing.

Authentication should establish:

- User identity
- Business membership
- User role
- Authorization context

Every protected API must validate authentication.

---

# 15. Authorization

Authorization must happen on the backend.

Do not rely on frontend controls.

Example:

    Cashier
        → Create invoice: ALLOWED
        → View products: ALLOWED
        → Delete product: DENIED
        → Change business settings: DENIED
        → View sensitive financial reports: DENIED if role rules require it

The API must enforce these rules.

---

# 16. Inventory Rules

Inventory is transaction-sensitive.

Never modify stock without creating a corresponding stock movement.

Example:

    Purchase
        ↓
    Stock +10
        ↓
    Stock Movement +10

    Sale
        ↓
    Stock -3
        ↓
    Stock Movement -3

The stock movement history must explain how the current stock was produced.

Current stock should be consistent with the stock movement history.

---

# 17. Sales Transaction Rules

Creating a completed sale may involve:

1. Validate business
2. Validate customer
3. Validate products
4. Validate quantities
5. Validate prices
6. Check stock
7. Calculate subtotal
8. Calculate discount
9. Calculate GST
10. Calculate total
11. Create invoice
12. Create invoice items
13. Reduce stock
14. Create stock movements
15. Create customer ledger entry
16. Record payment if supplied

These operations must be handled transactionally.

If a critical operation fails, the entire transaction should roll back.

Never leave partially completed sales.

---

# 18. Purchase Transaction Rules

Creating a completed purchase may involve:

1. Validate supplier
2. Validate products
3. Validate quantities
4. Calculate totals
5. Create purchase
6. Create purchase items
7. Increase stock
8. Create stock movements
9. Create supplier ledger entry
10. Record payment if supplied

These operations must be transactionally consistent.

---

# 19. Payment Rules

Payments must be linked to the appropriate business transaction.

Example:

    Invoice = ₹10,000

    Payment 1 = ₹4,000
    Payment 2 = ₹3,000

    Outstanding = ₹3,000

Do not allow payment greater than the allowed outstanding amount unless an explicit overpayment rule exists.

Payment records must contain enough information for reconciliation.

Example:

    payment_method
    amount
    reference
    status
    invoice_id
    customer_id
    created_at

---

# 20. Invoice Status

Use explicit invoice states.

Example:

    DRAFT
    CONFIRMED
    PARTIALLY_PAID
    PAID
    CANCELLED

Do not represent business state only using multiple unrelated boolean fields.

Avoid combinations such as:

    is_paid
    is_cancelled
    is_completed
    is_active

when a single state machine is more appropriate.

---

# 21. Invoice Numbering

Invoice numbers must be unique within a business.

Example:

    INV-000001
    INV-000002
    INV-000003

Never generate invoice numbers only in frontend code.

Invoice numbering must be handled by the backend.

Concurrency must be considered so two users cannot receive the same invoice number.

---

# 22. Money Handling

Never use floating-point arithmetic for financial calculations.

Use appropriate decimal/numeric database types.

Example:

Do not rely on:

    float

for:

- Invoice totals
- Tax
- Discounts
- Payments
- Prices

Use decimal-safe calculations.

Always define rounding rules clearly.

---

# 23. GST Rules

GST calculations must be centralized.

Do not duplicate tax calculations across:

- Invoice API
- Frontend
- Reports
- PDF generator

Create one authoritative tax calculation mechanism.

Example:

    Same state
        ↓
    CGST + SGST

    Different state
        ↓
    IGST

The frontend may display calculated values, but the backend must remain authoritative.

---

# 24. API Design

Use consistent REST APIs.

Example:

    /api/v1/auth
    /api/v1/businesses
    /api/v1/customers
    /api/v1/suppliers
    /api/v1/products
    /api/v1/invoices
    /api/v1/purchases
    /api/v1/payments
    /api/v1/expenses
    /api/v1/reports

Use versioning:

    /api/v1/...

Use consistent:

- Request validation
- Response structure
- HTTP status codes
- Error format
- Pagination
- Filtering
- Sorting

---

# 25. Error Handling

Never expose internal errors to users.

Bad:

    PostgreSQL IntegrityError at line 123

Good:

    Customer already exists.

or:

    Insufficient stock for product "Rice 5kg".

Backend logs should contain technical details.

User responses should contain safe business-friendly messages.

---

# 26. Validation

Validate input at multiple layers.

Frontend validation:

- User experience

Backend validation:

- Security
- Correctness

Database constraints:

- Data integrity

Never trust frontend validation alone.

---

# 27. Idempotency

Use idempotency for operations where duplicate requests can cause financial or inventory problems.

Important examples:

- Payment creation
- Invoice completion
- External payment webhook
- Stock movement creation

Example:

If the client sends the same payment request twice because of a network retry, the system must not record the payment twice.

---

# 28. Concurrency

Consider concurrent users.

Example:

Product stock:

    Stock = 5

Cashier A sells:

    4 units

Cashier B sells:

    3 units

The backend must prevent both transactions from incorrectly succeeding if stock cannot go negative.

Use appropriate database transaction and locking strategies.

---

# 29. External Integrations

External integrations must be isolated from core business logic.

Use an adapter pattern.

Example:

    PaymentService
         ↓
    PaymentProvider
         ↓
    Razorpay / Other Provider

The invoice system should not contain provider-specific code everywhere.

This makes it easier to replace external providers.

---

# 30. UPI

UPI gateway integration is NOT required for the initial MVP unless explicitly requested.

If added later, it should include:

- Payment creation
- Payment status
- Webhook
- Signature verification
- Idempotency
- Reconciliation
- Refund handling

Never mark a payment successful only because the frontend says payment succeeded.

The backend must verify payment status through the trusted payment provider mechanism.

---

# 31. Notifications

Notifications should not block critical business transactions.

Example:

Bad:

    Create Invoice
        ↓
    Send WhatsApp
        ↓
    Wait
        ↓
    Return response

Better:

    Create Invoice
        ↓
    Commit transaction
        ↓
    Return response
        ↓
    Background job
        ↓
    Send notification

---

# 32. Logging

Use structured logging.

Important events:

- Login
- Authentication failure
- Invoice creation
- Invoice cancellation
- Payment creation
- Stock adjustment
- Permission failure
- External API failure
- Unexpected exception

Never log:

- Passwords
- Access tokens
- Refresh tokens
- Payment secrets
- API keys
- Sensitive personal information

---

# 33. Audit Logging

Important business changes should be traceable.

Example:

    User: John
    Action: UPDATE_INVOICE
    Invoice: INV-1023
    Old Total: ₹5,000
    New Total: ₹4,500
    Timestamp: ...

Audit logs should be append-oriented and should not be casually deleted.

---

# 34. Testing Requirements

Every important business feature must have tests.

Minimum testing layers:

    Unit Tests
        ↓
    Service Tests
        ↓
    API Tests
        ↓
    Integration Tests

Important test cases:

### Inventory

- Purchase increases stock
- Sale decreases stock
- Return increases stock
- Stock adjustment works
- Insufficient stock is rejected

### Invoice

- Invoice creation
- Invalid customer
- Invalid product
- Invalid quantity
- Discount
- GST
- Partial payment
- Full payment
- Cancellation

### Payment

- Correct payment
- Partial payment
- Full payment
- Overpayment
- Duplicate payment

### Security

- Unauthorized access
- Wrong business access
- Wrong role access

---

# 35. Test Before Completion

Do not consider a feature complete simply because code compiles.

Before marking work complete:

1. Run relevant tests.
2. Run linting.
3. Run type checking if configured.
4. Verify database migrations.
5. Verify API behavior.
6. Verify business rules.
7. Check error cases.

If tests fail:

- Investigate the root cause.
- Fix the issue.
- Re-run the tests.

Do not disable tests simply to make the build pass.

---

# 36. Database Migrations

Never manually modify production database schema without a migration.

Every schema change must be represented by a migration.

Example:

    Add customers table
        ↓
    Migration

    Add invoice status
        ↓
    Migration

    Add payment reference
        ↓
    Migration

Migrations must be reversible when the technology supports safe rollback.

---

# 37. API Backward Compatibility

Avoid breaking existing APIs unnecessarily.

Before changing an API:

1. Search for frontend usage.
2. Search for tests.
3. Search for external consumers.
4. Determine whether the change is breaking.
5. Update documentation.

Prefer additive changes when possible.

---

# 38. Frontend Integration

The backend must provide predictable API contracts.

Do not create backend APIs based only on how convenient the backend implementation is.

Consider:

- UI requirements
- Pagination
- Search
- Filtering
- Sorting
- Loading states
- Error states

API response design should support the actual frontend use case.

---

# 39. Performance

Do not prematurely optimize.

For MVP:

- Use PostgreSQL
- Add appropriate indexes
- Avoid obvious N+1 queries
- Paginate large lists
- Avoid loading unnecessary columns
- Use transactions correctly

Do not introduce:

- Kafka
- Kubernetes
- Microservices
- Elasticsearch
- Complex distributed systems

unless there is a demonstrated requirement.

---

# 40. Caching

Use caching only where useful.

Potential candidates:

- Product lookup
- Dashboard summaries
- Configuration

Do not cache highly transactional data without a clear invalidation strategy.

Inventory and payment correctness is more important than caching.

---

# 41. Background Jobs

Use background jobs for tasks such as:

- PDF generation
- Email
- Notifications
- Report generation
- External API retries

Do not move critical transaction logic into an asynchronous job if doing so can create inconsistent business state.

---

# 42. Code Quality

Follow the project's `coding-style.md`.

General principles:

- Clear names
- Small functions
- Single responsibility
- Avoid duplicated logic
- Avoid unnecessary abstractions
- Prefer readable code
- Keep business logic testable
- Keep external integrations isolated

Do not create abstractions simply for the sake of abstraction.

---

# 43. Dependency Management

Before adding a dependency:

1. Check whether an existing dependency already solves the problem.
2. Check whether the functionality can reasonably be implemented without a dependency.
3. Check project compatibility.
4. Consider security and maintenance.
5. Add the dependency only if justified.

Never add a dependency silently for convenience.

Document important new dependencies.

---

# 44. Security Rules

Always follow secure development practices.

Never:

- Store plain-text passwords
- Hard-code secrets
- Commit `.env` files
- Trust client-side authorization
- Trust client-provided business ownership
- Log secrets
- Build SQL queries through unsafe string concatenation
- Expose stack traces to users

Use:

- Parameterized queries
- Password hashing
- HTTPS
- Secure token handling
- Input validation
- Authorization
- Rate limiting where appropriate

---

# 45. Environment Variables

Secrets and environment-specific configuration must come from environment variables or a secure configuration system.

Examples:

    DATABASE_URL
    JWT_SECRET
    REDIS_URL
    PAYMENT_API_KEY

Never hard-code secrets in source code.

Provide an appropriate `.env.example` when required.

Never commit real secrets.

---

# 46. Repository Changes

When modifying the repository:

1. Make the smallest reasonable change.
2. Avoid unrelated refactoring.
3. Preserve existing working functionality.
4. Add tests.
5. Update documentation when behavior changes.

Do not rewrite large parts of the project unless necessary.

---

# 47. Feature Implementation Process

For every feature, follow this workflow:

## Step 1 — Understand

Understand the requested functionality.

## Step 2 — Read Documentation

Read relevant `.agent/` documentation.

## Step 3 — Inspect Repository

Find existing related code.

## Step 4 — Identify Impact

Determine:

- UI impact
- API impact
- Database impact
- Service impact
- Business-rule impact
- Testing impact

## Step 5 — Plan

Create a short implementation plan.

## Step 6 — Implement

Implement the feature following the architecture.

## Step 7 — Test

Add/update tests.

## Step 8 — Verify

Run tests and validation.

## Step 9 — Documentation

Update relevant documentation if required.

## Step 10 — Report

Explain:

- What changed
- Files changed
- APIs changed
- Database changes
- Tests added
- Known limitations

---

# 48. Example: Implementing Invoice Creation

When asked:

    "Implement invoice creation."

The agent should identify:

    Feature:
        features/invoices.md

    Related:
        features/customers.md
        features/products.md
        features/inventory.md
        features/payments.md

    Backend:
        backend/api.md
        backend/database.md
        backend/services.md
        backend/transactions.md

    Rules:
        business-rules.md

    Tests:
        testing.md

Then inspect the existing repository.

Implementation should follow:

    Request
       ↓
    Authentication
       ↓
    Authorization
       ↓
    Validate Customer
       ↓
    Validate Products
       ↓
    Check Stock
       ↓
    Calculate Subtotal
       ↓
    Calculate Discount
       ↓
    Calculate GST
       ↓
    Calculate Total
       ↓
    Create Invoice
       ↓
    Create Invoice Items
       ↓
    Reduce Stock
       ↓
    Create Stock Movement
       ↓
    Update Customer Ledger
       ↓
    Record Payment
       ↓
    Commit Transaction
       ↓
    Return Invoice

---

# 49. Example: Implementing Product Creation

When asked:

    "Add product management."

The agent should check:

    features/products.md
    features/inventory.md
    backend/database.md
    backend/api.md
    business-rules.md

Then determine:

    Database
        ↓
    Product Model
        ↓
    Validation
        ↓
    Product Service
        ↓
    API
        ↓
    Tests

The agent must consider:

- SKU uniqueness
- Barcode uniqueness
- Business ownership
- GST rate
- Selling price
- Purchase price
- Opening stock
- Minimum stock

---

# 50. Example: Fixing a Bug

When asked:

    "Stock is incorrect after invoice cancellation."

Do not immediately modify the stock number.

First:

1. Read inventory rules.
2. Read invoice rules.
3. Read transaction rules.
4. Find invoice cancellation implementation.
5. Find stock movement implementation.
6. Reproduce the bug.
7. Identify the root cause.
8. Fix the root cause.
9. Add a regression test.
10. Verify stock movement history.

The goal is to fix the underlying business logic rather than patch the visible number.

---

# 51. Business Rule Protection

Business rules are more important than implementation convenience.

Never modify business rules simply because they make implementation easier.

If a requested feature conflicts with an existing business rule:

1. Identify the conflict.
2. Explain it.
3. Ask for clarification if necessary.
4. Do not silently override the rule.

---

# 52. Data Integrity

Business data must remain internally consistent.

For example:

    Invoice Total
        =
    Sum(Invoice Items)
    - Discount
    + Tax

Customer outstanding should be derivable from transaction history.

Inventory should be explainable through stock movements.

Payment totals should match payment records.

Reports should derive from authoritative transaction data.

Do not maintain multiple independent sources of truth for the same financial value without a clear reason.

---

# 53. Financial Data

Treat the following as critical data:

- Invoice amount
- Payment amount
- Tax amount
- Discount
- Purchase amount
- Customer outstanding
- Supplier outstanding
- Stock quantity

These require:

- Decimal-safe calculations
- Database transactions
- Validation
- Auditability
- Appropriate authorization

---

# 54. Deletion Rules

Do not physically delete important financial records casually.

For example:

    Invoice
    Payment
    Purchase

should normally use cancellation/voiding rather than destructive deletion once finalized.

Example:

    Invoice
       ↓
    CANCELLED

instead of:

    DELETE invoice

Products/customers may use soft deletion/deactivation when historical references exist.

---

# 55. Status Management

Use explicit states.

Examples:

Invoice:

    DRAFT
    CONFIRMED
    PARTIALLY_PAID
    PAID
    CANCELLED

Payment:

    PENDING
    SUCCESS
    FAILED
    REFUNDED

Do not allow invalid state transitions.

---

# 56. Observability

Production systems should be diagnosable.

Include:

- Application logs
- Error logs
- Request IDs where practical
- Database monitoring
- Health endpoint
- Basic metrics

Example:

    GET /health

should indicate whether the application is functioning.

---

# 57. Deployment

Follow `deployment.md`.

At minimum:

- Application containerization
- Database
- Environment configuration
- HTTPS
- Database migrations
- Backup
- Logging
- Health checks

Do not introduce unnecessary infrastructure for MVP.

---

# 58. Documentation Maintenance

When implementation changes architecture or behavior:

Update the appropriate `.agent/` document.

Examples:

New database entity:

    backend/database.md

New API:

    backend/api.md

New business rule:

    business-rules.md

New feature:

    features/<feature>.md

Major architectural decision:

    architecture.md

Major product decision:

    vision.md

---

# 59. Changelog

Update `changelog.md` for significant changes.

Example:

    ## 2026-08-14

    ### Added
    - Customer payment support
    - Partial invoice payment

    ### Changed
    - Invoice status now supports PARTIALLY_PAID

Do not record every tiny code change.

---

# 60. Roadmap Protection

Use `roadmap.md` to determine whether a feature belongs to:

- MVP
- Phase 2
- Phase 3
- Future

Do not automatically implement future features just because they are technically interesting.

Focus on the current MVP milestone.

---

# 61. Avoid Overengineering

For MVP, prefer:

    Simple
        >
    Correct
        >
    Maintainable
        >
    Scalable

Do not build complex distributed architecture before it is needed.

Avoid introducing:

- Microservices
- Kafka
- Kubernetes
- Event sourcing
- CQRS
- Distributed transactions

unless explicitly required.

A modular monolith is preferred for MVP.

---

# 62. Definition of Done

A feature is complete only when:

- Requirements are understood
- Relevant documentation is followed
- Existing code was inspected
- Implementation is complete
- Business rules are enforced
- Database changes are migrated
- APIs work correctly
- Tests are added
- Tests pass
- Security is considered
- Error handling is implemented
- Documentation is updated where required

---

# 63. Final Response Format

After completing a task, provide a concise implementation summary.

Use:

    ## Summary

    - Implemented ...
    - Added ...
    - Updated ...

    ## Backend

    - API:
    - Services:
    - Database:

    ## Frontend

    - Components:
    - Pages:

    ## Tests

    - Added ...
    - Passed ...

    ## Documentation

    - Updated ...

    ## Notes

    - Known limitations
    - Future improvements

Do not provide unnecessary explanations of unchanged code.

---

# 64. Important Final Rules

Always:

- Read before changing.
- Search before creating.
- Reuse before duplicating.
- Validate before saving.
- Use transactions for critical business operations.
- Protect tenant boundaries.
- Keep business logic in services.
- Keep APIs thin.
- Keep database constraints strong.
- Write tests for business-critical logic.
- Preserve financial data integrity.
- Follow the documented architecture.
- Stay within MVP scope.
- Explain significant architectural decisions.

Never:

- Guess repository structure.
- Guess existing functionality.
- Ignore business rules.
- Trust frontend authorization.
- Store secrets in source code.
- Use floating-point values for financial calculations.
- Delete finalized financial records casually.
- Create duplicate business logic.
- Mark payments successful without verification.
- Modify unrelated code unnecessarily.
- Introduce unnecessary infrastructure.
- Silently change product requirements.
- Mark a feature complete without testing it.

---

# 65. Core Principle

The most important principle for this project is:

    CORRECT BUSINESS TRANSACTIONS > FAST IMPLEMENTATION

The application must always preserve consistency between:

    Sales
       ↕
    Inventory
       ↕
    Payments
       ↕
    Customer/Supplier Ledger
       ↕
    Reports

A feature that works visually but corrupts business data is considered a failed implementation.

Build the MVP incrementally, keep the architecture simple, and ensure every business transaction is reliable and auditable.
