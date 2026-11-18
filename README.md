# Social Connection Finder

A Java command-line application for managing a social network and finding the shortest
connection between users. The application stores users, login details, companies,
industries, and relationships in SQLite. It also contains an implementation of
Dijkstra's algorithm for graph-based pathfinding.

## Features

- **Accounts:** Register and log in with an email and password.
- **Account management:** Update a user's name, email, password, and company.
- **Companies and industries:** Select an existing company or register a new company
  under an existing industry.
- **Connections:** Add, delete, and view undirected user connections.
- **Connection strength:** Assign each relationship a strength from 1 (strongest) to
  5 (weakest). These values are used as graph edge weights.
- **Connection search:** Find a user by industry or company, then calculate the
  shortest path from the logged-in user to that person.
- **Graph pathfinding:** Uses Dijkstra's algorithm with a custom priority queue to
  calculate the path and total edge weight.

## Requirements

- Java 11 or newer
- Maven
- SQLite JDBC support (managed automatically by Maven)

## Build

From the project root, compile the application:

```bash
mvn compile
```

Run the test suite:

```bash
mvn test
```

Package the project:

```bash
mvn package
```

## Run

Compile the project, then start the CLI from the project root:

```bash
mvn compile
java -cp "target/classes:lib/sqlite-jdbc-3.30.1.jar" Main.Main
```

The application uses
[`src/main/resources/connections.db`](src/main/resources/connections.db)
as its database. Keep the database and resource directory at their current locations
because the JDBC connection is relative to the project root.

## Database

The SQLite schema is defined in
[`src/main/resources/connections.ddl`](src/main/resources/connections.ddl).
It contains:

- `User` and `LoginInfo` for accounts
- `Industry` and `Company` for employment information
- `Connections` for relationships and their strength

The database resource directory also contains SQL seed/test data. The application
loads connection records into an undirected graph before running Dijkstra's algorithm.

## Usage

At startup, choose to log in, register, or exit. After logging in, the home menu offers:

1. **Find Connections** - search users by industry or company and display the shortest
   path to the selected user.
2. **Manage Connections** - add, delete, or view the current user's connections.
3. **Manage Account** - update account details or register a company.
4. **Logout** - return to the login and registration screen.
5. **Exit** - close the application.

## Tests

JUnit 4 tests cover graph/Dijkstra behavior and priority queue operations.

```bash
mvn test
```

## Project Layout

```text
src/main/java/
  DatabaseConnect/  SQLite access and user/account operations
  Dijkstra/         Dijkstra pathfinding implementation
  Graph/            Graph, node, and edge classes
  Main/             Interactive command-line interface
  PriorityQueue/    Priority queue used by Dijkstra
src/main/resources/ SQLite database and SQL schema/data
src/test/java/      JUnit tests
lib/                Bundled SQLite JDBC library
```
