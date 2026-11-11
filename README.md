# TriviaBlast

An online trivia web game: practise alone or challenge friends in **private multiplayer rooms** on a classic colour-category board. Questions come live from the [Open Trivia Database (OpenTDB)](https://opentdb.com/), across many categories and difficulty levels.

Team project for the *Web Engineering* course at **Complutense University of Madrid** (Erasmus+, 2026).

![Java](https://img.shields.io/badge/Java-24-orange) ![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.4-brightgreen) ![WebSockets](https://img.shields.io/badge/WebSockets-STOMP-blue) ![Karate](https://img.shields.io/badge/tests-Karate-yellow)

## Features

- **Accounts** – sign up, log in, edit profile (avatar, username, email, password confirmed with the old one) and delete the account.
- **Single-player** – choose the number of questions, category and difficulty; correct answers earn points, wrong answers show the correct one.
- **Anti-cheat by design** – answers are validated only on the server, so the browser never receives the correct answers (try `window.questions` in the console during a game).
- **Multiplayer rooms** – private rooms joined with a code, real-time updates over WebSockets.
- **Leaderboard** – players ranked by total points, visible to registered users.
- **Admin panel** – list of users and full game history, hide or restore players on the leaderboard, open any profile to investigate suspicious results.
- **Design** – UI designed in Figma and implemented with the Figma Dev Mode structure.

## Tech stack

| Layer | Technologies |
|---|---|
| Backend | Java 24, Spring Boot 3.4, Spring MVC, Spring Security, Spring Data JPA (Hibernate) |
| Real time | Spring WebSocket (STOMP) with Spring Security messaging |
| Frontend | Thymeleaf, Bootstrap 5, JavaScript |
| Database | H2 (file database `iwdb`), schema below |
| External API | Open Trivia Database |
| Tests | Karate (account, login, rooms, WebSocket and game flows), JUnit |

## Roles and permissions

| Role | Permissions |
|---|---|
| **Player** | Manage own account, play single-player and multiplayer games, view the leaderboard |
| **Administrator** | Hide, edit, delete or restore user visibility; view every user's game history to detect cheating |

## Game flow

1. Register or log in.
2. Set up your game (questions, category, difficulty) or join a room.
3. Play: questions and answers are shown one by one, with the current question number and score.
4. Points are calculated on the server and the leaderboard is updated.

## Database

![Database schema](DatabaseSchema.png)

- **User** – username, password (hashed), email, avatar, roles, total points, leaderboard visibility.
- **Game** – room code, number of questions, categories, difficulty, number of players, host, state.
- **Player** – links a user to a game with the points earned in it.
- **Message** – messages sent inside a game.

## Run locally

Requirements: JDK 24 and Maven.

```bash
mvn spring-boot:run
```

Then open <http://localhost:8080>. The H2 console is at `/h2`.

Run the tests:

```bash
mvn test
```

### Demo accounts (local database only)

USERNAME : infinite.alex5
PASSWORD : 1234

USERNAME : ana
PASSWORD : 234

USERNAME : juan
PASSWORD : 123

USERNAME : maria1
PASSWORD : 12

(admin) USERNAME : a   
	PASSWORD : aa
(admin) USERNAME : b   
	PASSWORD : bb

## Team

Developed by a student team at Complutense University of Madrid. Repository maintained by **Alexandra Rădulescu** – [GitHub](https://github.com/infinite-alex) · [LinkedIn](https://www.linkedin.com/in/alexandra-r%C4%83dulescu/).
