# Midas Core

Midas Core is a Spring Boot application that processes financial transactions through Kafka and provides balance query capabilities. It's part of the Midas project, which aims to handle financial transactions with proper validation and incentive processing.

## Features

- **Transaction Processing**: Processes incoming transactions via Kafka
- **Balance Validation**: Ensures sufficient funds before processing transactions
- **Incentive Integration**: Integrates with an external incentive API
- **Balance Querying**: REST API endpoint to query user balances
- **H2 Database**: In-memory database for storing user and transaction records

## Technical Stack

- Java 17
- Spring Boot 3.2.5
- Apache Kafka 3.1.4
- H2 Database 2.2.224
- Spring Data JPA
- Spring Web
- Spring Kafka
- Testcontainers for Kafka testing

## API Endpoints

### Query Balance

```
GET /balance?userId={userId}
```

Returns the current balance for the specified user. If the user doesn't exist, returns a balance of 0.

Response format:

```json
{
  "amount": 1234.56
}
```

## Configuration

The application uses the following configuration (application.yml):

- Server port: 33400
- Kafka bootstrap servers: localhost:9092
- Kafka consumer group: midas-group
- H2 database: In-memory mode
- JPA: Create-drop mode

## Getting Started

1. Ensure you have Java 17 installed
2. Clone the repository
3. Start the Incentive API service (required for transaction processing)
4. Run the application:
   ```bash
   ./mvnw spring-boot:run
   ```

## Testing

Run the test suite:

```bash
./mvnw test
```

The project includes comprehensive tests for:

- Transaction processing
- Balance validation
- Incentive integration
- Balance querying

## Architecture

The application follows a clean architecture with:

- Controllers for REST endpoints
- Services for business logic
- Repositories for data access
- Entity classes for data modeling
- Kafka listeners for event processing

Key components:

- `KafkaTransactionListener`: Processes incoming transactions
- `BalanceController`: Handles balance queries
- `IncentiveService`: Integrates with external incentive API
- `UserRecord` & `TransactionRecord`: JPA entities

## Error Handling

- Returns 0 balance for non-existent users
- Validates transaction amounts against sender balances
- Handles Kafka consumer errors gracefully
- Provides proper error responses for API endpoints

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## License

This project is proprietary and confidential.
