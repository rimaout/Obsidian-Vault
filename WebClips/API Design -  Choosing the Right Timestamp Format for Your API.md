## API Design: Choosing the Right Timestamp Format

I've seen countless API debates melt down over one simple question: "Should we use Unix timestamps or ISO 8601?" It's one of those decisions that seems trivial at first but ripples through your entire system—affecting parsing, timezone handling, and the developer experience your API users will love (or rage about). Let me walk you through the major formats and help you make the right choice for your API.

## The Timestamp Format Landscape

What's out there, and when should you use each? Let's break it down.

### 1. Unix Timestamp (Epoch Time)

**Format**: Integer representing seconds (or milliseconds) since January 1, 1970, 00:00:00 UTC.

```
{
  "created_at": 1705341600,
  "updated_at": 1705428000
}
```

**Advantages:**

- **Compact**: Small payload size (10 digits for seconds)
- **Simple**: Easy arithmetic (add/subtract seconds)
- **Universal**: No timezone ambiguity (always UTC)
- **Sortable**: Direct numeric comparison
- **Database-friendly**: Efficient indexing and queries

**Disadvantages:**

- **Not human-readable**: Hard to debug or inspect
- **Precision confusion**: Seconds vs milliseconds ambiguity
- **No timezone info**: Must assume UTC
- **Limited range**: 32-bit integers overflow in 2038

**Best for:**

- Internal APIs
- High-performance systems
- Time-series data
- Mobile APIs (bandwidth-constrained)

### 2. ISO 8601 / RFC 3339

**Format**: Standardized string representation with timezone information.

```
{
  "created_at": "2024-01-15T19:00:00Z",
  "updated_at": "2024-01-16T19:00:00+00:00"
}
```

**Advantages:**

- **Human-readable**: Easy to debug and understand
- **Timezone-aware**: Explicit offset or Z for UTC
- **Precise**: Supports milliseconds and microseconds
- **Standardized**: ISO 8601 is universally recognized
- **Self-documenting**: Format is obvious from the string

**Disadvantages:**

- **Larger payload**: ~24 characters vs 10-13 digits
- **Parsing overhead**: String to date conversion required
- **Variable format**: Multiple valid representations

**Best for:**

- Public APIs
- REST APIs
- Browser/web clients
- Developer-facing APIs

### 3. RFC 2822 / HTTP Date Format

**Format**: Human-readable format used in HTTP headers.

```
Date: Mon, 15 Jan 2024 19:00:00 GMT
Last-Modified: Tue, 16 Jan 2024 19:00:00 GMT
```

**Advantages:**

- **HTTP standard**: Required for certain HTTP headers
- **Human-readable**: Easy to understand
- **Timezone-aware**: GMT or explicit offset

**Disadvantages:**

- **Verbose**: Very long strings
- **Parsing complexity**: Locale-dependent parsing
- **Limited precision**: Only seconds

**Best for:**

- HTTP headers only
- Avoid in JSON payloads

### 4. Milliseconds Since Epoch

**Format**: Integer representing milliseconds since Unix epoch.

```
{
  "created_at": 1705341600000,
  "updated_at": 1705428000000
}
```

**Advantages:**

- **JavaScript-native**: Direct compatibility with `Date.now()`
- **Precise**: Millisecond precision
- **Compact**: Still just 13 digits

**Disadvantages:**

- **Confusion risk**: Easy to mix up with seconds
- **Larger numbers**: 13 digits vs 10
- **Not universal**: Python, Go use seconds

**Best for:**

- JavaScript-heavy stacks
- Real-time systems
- High-precision logging

## Real-World API Examples

Want to see how the pros do it? Here's what major APIs actually use in production.

### Stripe (Payments API)

**Format**: Unix timestamps in seconds

```
{
  "id": "ch_3OJq3qLkdIwHu7ix0OyIZBII",
  "object": "charge",
  "created": 1705341600,
  "amount": 2000,
  "currency": "usd"
}
```

**Why**: Simple, compact, no timezone confusion. Perfect for financial transactions where precision to the second suffices.

### GitHub (REST API)

**Format**: ISO 8601 with timezone

```
{
  "id": 1,
  "name": "Hello-World",
  "created_at": "2024-01-15T19:00:00Z",
  "updated_at": "2024-01-16T19:00:00Z",
  "pushed_at": "2024-01-16T20:00:00Z"
}
```

**Why**: Developer-friendly, human-readable, explicit timezone. Great for public APIs where ease of use matters.

### Twitter API v2

**Format**: ISO 8601 with millisecond precision

```
{
  "id": "1234567890",
  "text": "Hello world",
  "created_at": "2024-01-15T19:00:00.000Z"
}
```

**Why**: Combines readability with precision for real-time social media events.

### AWS API

**Format**: ISO 8601 strings

```
{
  "InstanceId": "i-1234567890abcdef0",
  "LaunchTime": "2024-01-15T19:00:00.000Z",
  "State": {
    "Code": 16,
    "Name": "running"
  }
}
```

**Why**: Enterprise standard, interoperability with various AWS services and third-party tools.

## Decision Framework

Okay, so how do you actually choose? Here's my decision framework based on years of building (and maintaining) APIs.

### Choose Unix Timestamp (Seconds) When:

✅ **Simplicity is critical**

```
// Stripe charges
{
  "id": "ch_xxx",
  "created": 1705341600,
  "amount": 1000
}
```

✅ **Bandwidth matters** (mobile, IoT)

```
// Sensor data
{
  "sensor_id": "temp_01",
  "reading": 23.5,
  "timestamp": 1705341600
}
```

✅ **High-frequency time-series data**

```
// Stock ticks
{
  "symbol": "AAPL",
  "price": 195.50,
  "ts": 1705341600
}
```

✅ **Internal microservices**

```
// Service-to-service events
{
  "event": "user.login",
  "user_id": 123,
  "ts": 1705341600
}
```

### Choose ISO 8601 When:

✅ **Public-facing REST APIs**

```
// User profile API
{
  "id": 123,
  "username": "john_doe",
  "created_at": "2024-01-15T19:00:00Z",
  "last_login": "2024-01-16T08:30:00Z"
}
```

✅ **Developer experience matters**

```
// Event scheduling API
{
  "event_id": "evt_456",
  "title": "Team Meeting",
  "scheduled_at": "2024-01-20T14:00:00-05:00",
  "timezone": "America/New_York"
}
```

✅ **Cross-platform compatibility**

```
// Cross-platform notification
{
  "notification_id": "notif_789",
  "message": "Your order has shipped",
  "sent_at": "2024-01-15T19:00:00Z"
}
```

✅ **Timezone information is essential**

```
// Booking system
{
  "booking_id": "bk_101",
  "check_in": "2024-03-15T15:00:00-04:00",
  "check_out": "2024-03-20T11:00:00-04:00"
}
```

## Best Practices for API Design

These are the patterns I wish someone had shown me when I first started designing APIs.

### 1. Be Consistent Across Your API

```
// ❌ BAD: Mixed formats
{
  "user": {
    "created_at": 1705341600,           // Unix
    "updated_at": "2024-01-16T19:00:00Z", // ISO
    "last_login": "Mon Jan 15 2024"      // Custom
  }
}

// ✅ GOOD: Single format throughout
{
  "user": {
    "created_at": "2024-01-15T19:00:00Z",
    "updated_at": "2024-01-16T19:00:00Z",
    "last_login": "2024-01-16T08:30:00Z"
  }
}
```

### 2. Document Your Format Clearly

```
/**
 * Create a new event
 *
 * @param {Object} eventData
 * @param {string} eventData.title - Event title
 * @param {number} eventData.scheduled_at - Unix timestamp in seconds (UTC)
 * @param {string} [eventData.timezone] - IANA timezone name
 *
 * @returns {Object} Created event
 * @property {string} id - Event ID
 * @property {number} created_at - Unix timestamp in seconds (UTC)
 */
POST /api/v1/events
```

In OpenAPI/Swagger:

```
components:
  schemas:
    Event:
      type: object
      properties:
        id:
          type: string
          example: "evt_123"
        title:
          type: string
          example: "Team Meeting"
        scheduled_at:
          type: integer
          format: int64
          description: "Unix timestamp in seconds (UTC)"
          example: 1705341600
        created_at:
          type: string
          format: date-time
          description: "ISO 8601 timestamp with timezone"
          example: "2024-01-15T19:00:00Z"
```

### 3. Support Multiple Input Formats, Return One

```
// Accept multiple input formats for flexibility
function parseTimestamp(input) {
  // Unix seconds (10 digits)
  if (typeof input === 'number' && input < 10000000000) {
    return input;
  }

  // Unix milliseconds (13 digits)
  if (typeof input === 'number' && input < 10000000000000) {
    return Math.floor(input / 1000);
  }

  // ISO 8601 string
  if (typeof input === 'string') {
    const timestamp = new Date(input).getTime();
    if (!isNaN(timestamp)) {
      return Math.floor(timestamp / 1000);
    }
  }

  throw new Error('Invalid timestamp format');
}

// Always return consistent format
app.post('/api/events', (req, res) => {
  const scheduledAt = parseTimestamp(req.body.scheduled_at);

  const event = {
    id: generateId(),
    title: req.body.title,
    scheduled_at: scheduledAt,  // Always Unix seconds
    created_at: Math.floor(Date.now() / 1000)
  };

  res.json(event);
});
```

### 4. Include Timezone Information When Relevant

```
// ✅ GOOD: Store both UTC and timezone
{
  "event": {
    "id": "evt_123",
    "title": "Team Meeting",
    "scheduled_at_utc": "2024-01-20T19:00:00Z",
    "scheduled_at_local": "2024-01-20T14:00:00-05:00",
    "timezone": "America/New_York"
  }
}
```

### 5. Provide Helper Fields for Common Operations

```
{
  "subscription": {
    "id": "sub_123",
    "current_period_start": 1705341600,
    "current_period_end": 1707933600,
    "trial_end": 1705773600,

    // Helper fields for client convenience
    "is_trial": true,
    "days_until_renewal": 25,
    "human_readable": {
      "current_period_start": "January 15, 2024",
      "current_period_end": "February 14, 2024"
    }
  }
}
```

### 6. Use Appropriate Precision

```
// ❌ BAD: Excessive precision for user events
{
  "user_login": {
    "timestamp": "2024-01-15T19:00:00.123456789Z" // Nanoseconds overkill
  }
}

// ✅ GOOD: Appropriate precision
{
  "user_login": {
    "timestamp": "2024-01-15T19:00:00Z" // Seconds sufficient
  }
}

// ✅ GOOD: High precision for trading
{
  "trade": {
    "executed_at": "2024-01-15T19:00:00.123Z", // Milliseconds needed
    "symbol": "AAPL",
    "price": 195.50
  }
}
```

## Versioning and Migration

### Version 1 to Version 2 Migration

```
// v1: Unix timestamps
{
  "user": {
    "id": 123,
    "created_at": 1705341600,
    "updated_at": 1705428000
  }
}

// v2: ISO 8601 (backward compatible)
{
  "user": {
    "id": 123,
    "created_at": "2024-01-15T19:00:00Z",
    "created_at_unix": 1705341600,  // Deprecated, for compatibility
    "updated_at": "2024-01-16T19:00:00Z",
    "updated_at_unix": 1705428000   // Deprecated, for compatibility
  }
}
```

### Deprecation Strategy

```
app.get('/api/v1/users/:id', (req, res) => {
  const user = getUserById(req.params.id);

  res.json({
    id: user.id,
    created_at: user.createdAt,  // Unix timestamp
    // Warning header for deprecation
  });

  res.setHeader(
    'Deprecation',
    'true; date="2025-06-01"; link="https://api.example.com/docs/v2"'
  );
});
```

## Error Handling and Validation

### Validate Timestamp Inputs

```
function validateTimestamp(timestamp, fieldName) {
  // Check for null/undefined
  if (timestamp == null) {
    throw new ValidationError(`${fieldName} is required`);
  }

  // Check for valid Unix timestamp
  if (typeof timestamp === 'number') {
    // Reject timestamps too far in past
    if (timestamp < 0) {
      throw new ValidationError(`${fieldName} cannot be negative`);
    }

    // Reject timestamps too far in future (10 years)
    const tenYearsFromNow = Date.now() / 1000 + (10 * 365 * 24 * 60 * 60);
    if (timestamp > tenYearsFromNow) {
      throw new ValidationError(`${fieldName} is too far in the future`);
    }

    return timestamp;
  }

  // Check for valid ISO string
  if (typeof timestamp === 'string') {
    const parsed = new Date(timestamp);
    if (isNaN(parsed.getTime())) {
      throw new ValidationError(`${fieldName} is not a valid ISO 8601 date`);
    }

    return Math.floor(parsed.getTime() / 1000);
  }

  throw new ValidationError(`${fieldName} must be a Unix timestamp or ISO 8601 string`);
}

// Usage
app.post('/api/events', (req, res) => {
  try {
    const scheduledAt = validateTimestamp(req.body.scheduled_at, 'scheduled_at');

    // Create event...
  } catch (error) {
    res.status(400).json({
      error: {
        type: 'validation_error',
        message: error.message,
        param: 'scheduled_at'
      }
    });
  }
});
```

### Return Clear Error Messages

```
// ❌ BAD: Vague error
{
  "error": "Invalid input"
}

// ✅ GOOD: Specific error
{
  "error": {
    "type": "validation_error",
    "message": "scheduled_at must be a Unix timestamp (seconds) or ISO 8601 string",
    "param": "scheduled_at",
    "received": "2024-13-45",
    "examples": {
      "unix_seconds": 1705341600,
      "iso_8601": "2024-01-15T19:00:00Z"
    }
  }
}
```

## Performance Considerations

### 1. JSON Payload Size

```
// Unix timestamp (10 bytes)
{"created_at":1705341600}

// ISO 8601 (33 bytes)
{"created_at":"2024-01-15T19:00:00Z"}

// For 1 million records:
// Unix: ~10 MB
// ISO: ~33 MB
// Difference: 23 MB (230% larger)
```

**Recommendation**: Use Unix for high-volume APIs, ISO for developer experience.

### 2. Parsing Performance

```
// Benchmark: 1 million iterations
const Benchmark = require('benchmark');
const suite = new Benchmark.Suite;

suite
  .add('Unix timestamp', () => {
    new Date(1705341600 * 1000);
  })
  .add('ISO 8601', () => {
    new Date('2024-01-15T19:00:00Z');
  })
  .on('cycle', (event) => {
    console.log(String(event.target));
  })
  .run();

// Results:
// Unix timestamp: 5,231,234 ops/sec ±1.23%
// ISO 8601:       2,134,567 ops/sec ±1.45%
//
// Unix is ~2.4x faster
```

### 3. Database Indexing

```
-- Unix timestamp: Native integer indexing (very fast)
CREATE INDEX idx_events_created ON events(created_at);

-- ISO 8601: String indexing (slower, more storage)
CREATE INDEX idx_events_created ON events(created_at);
-- Note: Some databases (PostgreSQL) optimize TIMESTAMP types,
-- but ISO strings stored as VARCHAR are slower
```

## Client-Side Parsing

### JavaScript/TypeScript

```
// Unix timestamp
const timestamp = 1705341600;
const date = new Date(timestamp * 1000);
console.log(date.toISOString());
// "2024-01-15T19:00:00.000Z"

// ISO 8601
const iso = "2024-01-15T19:00:00Z";
const date2 = new Date(iso);
console.log(date2.getTime() / 1000);
// 1705341600

// Luxon for better timezone handling
import { DateTime } from 'luxon';

const dt = DateTime.fromSeconds(1705341600, { zone: 'America/New_York' });
console.log(dt.toISO());
// "2024-01-15T14:00:00.000-05:00"
```

### Python

```
import datetime
import pytz

# Unix timestamp
timestamp = 1705341600
dt = datetime.datetime.fromtimestamp(timestamp, tz=pytz.UTC)
print(dt.isoformat())
# "2024-01-15T19:00:00+00:00"

# ISO 8601
iso = "2024-01-15T19:00:00Z"
dt = datetime.datetime.fromisoformat(iso.replace('Z', '+00:00'))
print(int(dt.timestamp()))
# 1705341600
```

### Java

```
import java.time.*;

// Unix timestamp
long timestamp = 1705341600L;
Instant instant = Instant.ofEpochSecond(timestamp);
System.out.println(instant.toString());
// "2024-01-15T19:00:00Z"

// ISO 8601
String iso = "2024-01-15T19:00:00Z";
Instant instant2 = Instant.parse(iso);
System.out.println(instant2.getEpochSecond());
// 1705341600
```

## Common Patterns

### Pattern 1: Range Queries

```
// GET /api/events?start=1705341600&end=1705428000
app.get('/api/events', (req, res) => {
  const { start, end } = req.query;

  const events = db.events.find({
    scheduled_at: {
      $gte: parseInt(start),
      $lte: parseInt(end)
    }
  });

  res.json({ events });
});
```

### Pattern 2: Pagination with Timestamps

```
// GET /api/events?after=1705341600&limit=20
app.get('/api/events', (req, res) => {
  const after = parseInt(req.query.after || 0);
  const limit = parseInt(req.query.limit || 20);

  const events = db.events.find({
    created_at: { $gt: after }
  })
  .sort({ created_at: 1 })
  .limit(limit);

  const lastEvent = events[events.length - 1];

  res.json({
    events,
    pagination: {
      next_cursor: lastEvent?.created_at,
      has_more: events.length === limit
    }
  });
});
```

### Pattern 3: Conditional Requests

```
// GET /api/users/123
// If-Modified-Since: Mon, 15 Jan 2024 19:00:00 GMT
app.get('/api/users/:id', (req, res) => {
  const user = getUserById(req.params.id);
  const lastModified = new Date(user.updated_at * 1000);

  const ifModifiedSince = req.headers['if-modified-since'];
  if (ifModifiedSince) {
    const clientDate = new Date(ifModifiedSince);
    if (lastModified <= clientDate) {
      return res.status(304).end(); // Not Modified
    }
  }

  res.setHeader('Last-Modified', lastModified.toUTCString());
  res.json(user);
});
```

## Testing Timestamp APIs

### Unit Tests

```
describe('Event API timestamp handling', () => {
  test('accepts Unix timestamp in seconds', async () => {
    const response = await request(app)
      .post('/api/events')
      .send({
        title: 'Test Event',
        scheduled_at: 1705341600
      });

    expect(response.status).toBe(201);
    expect(response.body.scheduled_at).toBe(1705341600);
  });

  test('accepts ISO 8601 string', async () => {
    const response = await request(app)
      .post('/api/events')
      .send({
        title: 'Test Event',
        scheduled_at: '2024-01-15T19:00:00Z'
      });

    expect(response.status).toBe(201);
    expect(response.body.scheduled_at).toBe(1705341600);
  });

  test('rejects invalid timestamp', async () => {
    const response = await request(app)
      .post('/api/events')
      .send({
        title: 'Test Event',
        scheduled_at: 'invalid'
      });

    expect(response.status).toBe(400);
    expect(response.body.error.type).toBe('validation_error');
  });

  test('rejects timestamp in far future', async () => {
    const farFuture = Date.now() / 1000 + (100 * 365 * 24 * 60 * 60);

    const response = await request(app)
      .post('/api/events')
      .send({
        title: 'Test Event',
        scheduled_at: farFuture
      });

    expect(response.status).toBe(400);
  });
});
```

## Conclusion

Here's the truth: there's no universally "correct" timestamp format. It really depends on your API's context and audience.

**Choose Unix timestamps when:**

- Performance and bandwidth are critical
- You're dealing with time-series data
- You're building internal APIs
- Simplicity is paramount

**Choose ISO 8601 when:**

- You're building public-facing APIs
- Developer experience is important
- Timezone information is essential
- Human readability matters

**My key principles:**

1. **Be consistent** - Pick one format and stick to it everywhere
2. **Document clearly** - Nobody should have to guess your format
3. **Validate inputs** - Reject invalid timestamps with helpful errors
4. **Support flexibility** - Accept multiple inputs if it helps your users
5. **Consider migration** - Plan for format changes before you need them

The best APIs (Stripe, GitHub, AWS) didn't get timestamp handling right by accident—they thought through these tradeoffs carefully. Now you can too.

## Further Reading

- [Complete Guide to Unix Timestamps](https://www.datetimeapp.com/learn/complete-guide-to-unix-timestamps) - Deep dive into epoch time
- [ISO 8601 Standard Explained](https://www.datetimeapp.com/learn/iso-8601-explained) - Master the datetime standard
- [Database Timestamp Storage](https://www.datetimeapp.com/learn/database-timestamp-storage) - Store timestamps efficiently
- [Timezone Conversion Best Practices](https://www.datetimeapp.com/learn/timezone-conversion-best-practices) - Handle timezones in APIs
- [Microservices Time Synchronization](https://www.datetimeapp.com/learn/microservices-time-synchronization) - Coordinate time across distributed services
- [Working with Timestamps in Python](https://www.datetimeapp.com/learn/python-datetime-guide) - Implement timestamp APIs in Python

---

_Building an API? [Contact us](mailto:info@effati.se) for consultation on timestamp design._