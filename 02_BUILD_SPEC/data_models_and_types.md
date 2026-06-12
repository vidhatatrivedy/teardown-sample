# Data Models & Types

Canonical definitions shared across backend (Pydantic) and frontend (TypeScript).

## User

```typescript
interface User {
  id: string;
  email: string;
  full_name: string;
  is_active: boolean;
  is_verified: boolean;
  has_password: boolean;
  onboarding_completed: boolean;
  restaurant_created: boolean;
  email_integrated: boolean;
  auth_provider: "email" | "google";
  timezone: string;
  language: string;
  created_at: string;
  updated_at: string;
}
```

## Restaurant

```typescript
interface Restaurant {
  id: string;
  name: string;
  owner_id: string;
  members: RestaurantMember[];
  settings: RestaurantSettings;
  is_active: boolean;
  is_subscription_active: boolean;
  subscription_expiry_date?: string;
}

interface RestaurantMember {
  user_id: string;
  role: "owner" | "manager" | "staff";
  is_active: boolean;
}

interface RestaurantSettings {
  currency: string;
  timezone: string;
  auto_confirm_bookings: boolean;
  require_deposit: boolean;
  deposit_percentage: number;
  bank_details?: BankDetails;
}
```

## Client

```typescript
interface Client {
  id: string;
  company_name: string;
  contact_person: string;
  email: string;
  phone?: string;
  default_price_per_item: number;
  default_price_per_item_child?: number;
  billing_details?: { name?: string; address?: string };
  delivery_details?: { address?: string };
  restaurant_id: string;
  is_active: boolean;
}
```

## Enquiry

```typescript
type EnquiryStatus =
  | "new" | "read" | "replied"
  | "approved" | "rejected" | "closed";

interface Enquiry {
  id: string;
  booking_reference: string;
  customer_name: string;
  customer_email: string;
  customer_phone: string;
  subject: string;
  message: string;
  status: EnquiryStatus;
  client_id: string;
  tourmanager_id?: string;
  delivery_date?: string;
  delivery_time?: string;
  extracted_entities?: Record<string, unknown>;
  tags: string[];
  restaurant_id: string;
  created_at: string;
  updated_at: string;
}
```

## Booking

```typescript
type BookingStatus = "pending" | "confirmed" | "cancelled" | "completed";
type PaymentStatus = "pending" | "paid" | "partial" | "refunded";

interface Booking {
  id: string;
  booking_reference: string;
  company_name: string;
  booking_date: string;
  booking_time: string;
  number_of_people: number;
  number_of_children: number;
  contact_person_name: string;
  contact_email: string;
  contact_phone: string;
  total_amount: number;
  status: BookingStatus;
  payment_status: PaymentStatus;
  order_preparation_status: string;
  enquiry_id: string;
  restaurant_id: string;
  enquiry?: Partial<Enquiry>;
  client?: Partial<Client>;
}
```

## Order

```typescript
interface OrderItem {
  id: string;
  name: string;
  quantity: number;
  price: number;
  notes?: string;
}

interface Order {
  id: string;
  booking_reference: string;
  order_date: string;
  delivery_date: string;
  delivery_time: string;
  delivery_address: string;
  items: OrderItem[];
  total_amount: number;
  enquiry_id: string;
  restaurant_id: string;
}
```

## Email entities

```typescript
interface EmailIntegration {
  id: string;
  provider: "gmail" | "outlook" | "imap";
  email_address: string;
  status: "active" | "paused" | "error";
  restaurant_id: string;
}

interface EmailMessage {
  id: string;
  thread_id: string;
  subject: string;
  sender_email: string;
  body_text?: string;
  processing_status: string;
  confidence_score?: number;
  extracted_data?: Record<string, unknown>;
}
```

## Shared keys

| Field | Links |
|-------|-------|
| `restaurant_id` | All tenant entities → Restaurant |
| `client_id` | Enquiry → Client |
| `enquiry_id` | Booking, Order → Enquiry |
| `booking_reference` | Enquiry, Booking, Order (business key) |

## Target: ExtractedEnquiryEntities (to implement)

```typescript
interface ExtractedEnquiryEntities {
  customer_name?: string;
  customer_email?: string;
  customer_phone?: string;
  booking_reference?: string;
  party_size?: number;
  delivery_date?: string;
  delivery_time?: string;
  company_name?: string;
  confidence: number;
  provider: "openai" | "deepseek";
  prompt_version: string;
}
```

Replace free-form `extracted_entities: dict` with this typed model.

## Source files

| Layer | File |
|-------|------|
| Backend models | `backend/app/models/*.py` |
| Frontend types | `frontend/src/types/index.ts` |
| OpenAPI | `GET /openapi.json` (generated) |
