# Skill — Write MongoDB Migration

Safely change Chef's Console MongoDB schema without Beanie migration framework (introducing one).

## When to use

Adding indexes, backfilling fields, renaming collections.

## Steps

### 1. Create migration file

`backend/migrations/00N_description.py`

```python
"""Add compound index on bookings."""
import asyncio
from motor.motor_asyncio import AsyncIOMotorClient
from config import MONGODB_URL, DATABASE_NAME

async def up():
    client = AsyncIOMotorClient(MONGODB_URL)
    db = client[DATABASE_NAME]
    await db.bookings.create_index(
        [("restaurant_id", 1), ("booking_date", -1)],
        name="idx_restaurant_booking_date",
    )
    client.close()

async def down():
    client = AsyncIOMotorClient(MONGODB_URL)
    db = client[DATABASE_NAME]
    await db.bookings.drop_index("idx_restaurant_booking_date")
    client.close()

if __name__ == "__main__":
    asyncio.run(up())
```

### 2. Update Beanie model Settings indexes (keep in sync)

### 3. Document in teardown `02_BUILD_SPEC/database_schema.md` if structural

### 4. Run

```bash
cd backend
source venv/bin/activate
python migrations/00N_description.py
```

## Rules

- **Idempotent:** check index existence before create
- **Backfill:** use cursor batch updates, not load-all
- **Production:** run off-peak; test on staging copy first
- Never drop collections without explicit human approval

## Backfill pattern

```python
async for doc in db.enquiries.find({"tags": {"$exists": False}}):
    await db.enquiries.update_one(
        {"_id": doc["_id"]},
        {"$set": {"tags": []}},
    )
```

## Checklist

- [ ] `up()` and `down()` defined
- [ ] Tested on local MongoDB
- [ ] Beanie model matches post-migration shape
- [ ] No PII logged during migration
