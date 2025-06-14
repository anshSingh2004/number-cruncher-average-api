
# Average Calculator HTTP Microservice

A REST API microservice that fetches qualified numbers from third-party APIs and maintains a sliding window average calculation.

## Features

- **Qualified Number IDs**: Supports 'p' (prime), 'f' (fibonacci), 'e' (even), 'r' (random)
- **Sliding Window**: Configurable window size (default: 10)
- **Third-party Integration**: Fetches from evaluation-service APIs
- **Response Time Optimization**: < 500ms response guarantee
- **Duplicate Handling**: Filters duplicate numbers automatically
- **Error Resilience**: Handles timeouts and API failures gracefully

## Quick Start

1. **Start the Backend Server**:
   ```bash
   node src/server/index.js
   ```
   Server runs on `http://localhost:9876`

2. **View the Frontend**:
   ```bash
   npm run dev
   ```
   Frontend runs on `http://localhost:8080`

## API Endpoints

### Fetch Numbers
```
GET /numbers/{numberid}
```

**Supported Number IDs**:
- `p` - Prime numbers
- `f` - Fibonacci numbers  
- `e` - Even numbers
- `r` - Random numbers

**Example Request**:
```bash
curl http://localhost:9876/numbers/e
```

**Example Response**:
```json
{
  "windowPrevState": [],
  "windowCurrState": [2, 4, 6, 8],
  "numbers": [2, 4, 6, 8],
  "avg": 5.00
}
```

### Health Check
```
GET /health
```

### Reset Window
```
POST /reset
```

## Test Cases

The microservice includes comprehensive test scenarios:

1. **First Request** - Empty window state
2. **Subsequent Requests** - Window management and overflow handling
3. **Duplicate Filtering** - Ensures unique numbers only
4. **Timeout Handling** - Graceful handling of slow APIs
5. **Error Recovery** - Maintains service availability

## Architecture

- **Backend**: Express.js with CORS support
- **Frontend**: React with TypeScript
- **Storage**: In-memory sliding window
- **APIs**: Integration with evaluation-service endpoints
- **Error Handling**: Timeout protection and fallback responses

## Configuration

- **Window Size**: 10 (configurable in server code)
- **Timeout**: 500ms for third-party API calls
- **Port**: 9876 (microservice standard)

## Third-party APIs

The service integrates with these evaluation-service endpoints:
- Prime: `http://20.244.56.144/evaluation-service/primes`
- Fibonacci: `http://20.244.56.144/evaluation-service/fibo`
- Even: `http://20.244.56.144/evaluation-service/even`
- Random: `http://20.244.56.144/evaluation-service/rand`

## Technologies Used

- **Backend**: Node.js, Express.js, node-fetch
- **Frontend**: React, TypeScript, Tailwind CSS, shadcn/ui
- **Build Tool**: Vite
- **State Management**: React hooks
- **HTTP Client**: Fetch API with timeout handling
