# Project: Cryptocurrency Market Data & TWAP Paper Trading API
## Overview
Your task is to create a complete system consisting of both a server API and a client implementation that together enable paper trading using TWAP (Time-Weighted Average Price) orders executed against real market data. The system will collect and standardize order book data from cryptocurrency exchanges in real-time, then use this data to simulate order execution.

## Server Component
The server needs to handle three main tasks:

1. Market Data Collection The server connects to at least two cryptocurrency exchanges (like Binance, Kraken, or others of your choice) via their WebSocket feeds to collect order book data. This data must be standardized into a common format regardless of the source exchange.

2. Public Data Access Anyone can access historical market data through these endpoints:

- Get candlestick (kline) data from any supported exchange
- Get the list of supported exchanges
- Get available trading pairs for each exchange
  
3. Paper Trading System Authenticated users can submit TWAP orders that will be executed against the real-time order book data. The server simulates order execution by:
   
- Dividing the total order quantity into time slices based on the specified duration
- At each time slice, checking the current order book
- If the order book prices meet the limit price constraint, simulating an execution (considering aggressive order for simplicity, which means using the ask price for buy order and bid price for sell order)
- Tracking and reporting the execution progress

## Client Component
You must provide a client implementation that demonstrates how to:

1. Connect and Authenticate Show the complete flow from connecting to the API to maintaining an authenticated session.

2. Submit and Monitor Orders Demonstrate submitting a TWAP order and tracking its execution through both:

- REST API calls to check order status
- WebSocket connection to receive real-time order book data
  
The client should be provided as a Python package that others can use as a reference implementation.

## API Specification
### REST Endpoints
Public Routes:

```plaintext
GET /klines/{exchange}/{symbol}
- Get historical candlestick data
- Parameters: interval (1m, 5m, etc.), limit (number of candles)
```

Authenticated Routes:

```plaintext
POST /orders/twap
- Submit a new TWAP order
- Requires a unique token_id from client
- Server returns immediate accept/reject
```

```plaintext
GET /orders
- List all orders (open, closed, or both)
- Can filter by token_id
```

```plaintext
GET /orders/{token_id}
- Get detailed status of a specific order
```

### WebSocket Feed
The server maintains WebSocket connections to exchanges and provides a WebSocket endpoint for clients. After authentication, clients receive aggregated order book data (top 10 levels) every second for their subscribed symbols.

## Getting Started
Your implementation should follow this sequence:

1. First implement the market data collection system
2. Add the TWAP execution engine
3. Implement the REST API endpoints
4. Add the WebSocket feed
5. Create the client implementation
6. Add authentication
   
## Project Deliverables
1. A server implementation using FastAPI
2. A client Python package with usage examples
3. Swagger documentation for the API
4. A simple README explaining:
  - How to start the server
  - How to use the client
  - Basic troubleshooting
    
## Optional Enhancements
If you complete the core requirements, you can enhance your project with: - A simple GUI client - Support for more exchanges - Additional order execution strategies - Better execution analytics

## Project Organization
- Work in groups of 4-6 people
- Use GitHub for your repository
- Submit via email:
  - Team member names
  - GitHub repository link
  - Any special instructions
