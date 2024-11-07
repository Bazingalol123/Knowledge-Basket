# Sal Yeda - Interactive Learning Game

Sal Yeda is a gamified learning platform designed to enhance educational engagement through interactive gameplay. This project, developed using C# and Blazor, provides a rich, animated experience where users can answer questions, receive real-time feedback, and learn in a fun, interactive environment. Aimed at students and educators, Sal Yeda offers a versatile platform that can be easily customized with new content, making it adaptable to various learning objectives.

## Table of Contents

1. [Project Overview](#project-overview)
2. [Key Features](#key-features)
3. [Screenshots](#screenshots)
4. [APIs](#apis)
5. [Setup and Installation](#setup-and-installation)
6. [How to Play](#how-to-play)
7. [Development Notes](#development-notes)

## Project Overview

### Main Objectives

- **Educational Engagement**: Promotes learning through engaging gameplay and visual feedback.
- **Customizable Content**: Allows educators to manage questions, answers, and media content easily.
- **Real-Time Feedback**: Immediate feedback for correct/incorrect answers to enhance the learning experience.

### Technologies Used

- **Primary Language**: C#
- **Framework**: Blazor (Frontend), Unity (Backend/Server Management)
- **Database & APIs**: SQL and custom REST APIs for managing game data.

## Key Features

- **Dynamic Question and Answer Interface**: An animated interface that encourages interaction and engagement.
- **Game Management and Customization**: Includes an admin interface for managing questions, answers, and related media.
- **Responsive Design**: Optimized for various devices and screen sizes, ensuring accessibility.
- **Media Management**: Secure handling and storage of images and multimedia assets for dynamic game elements.

<table>
  <tr> <th>
      example
   </th></tr>

</table>

## Screenshots

| Game Screen                     | Question Editor                     |
| ------------------------------- | ----------------------------------- |
| ![Game Screen](screenshot1.png) | ![Question Editor](screenshot2.png) |

| Feedback Screen                     | Celebration Screen                     |
| ----------------------------------- | -------------------------------------- |
| ![Feedback Screen](screenshot3.png) | ![Celebration Screen](screenshot4.png) |

## APIs

Below is a summary of the API endpoints organized by controller, providing detailed functionality for each endpoint in the Sal Yeda application.

### GamesController

| Endpoint                                                           | Method | Description                                                                   |
| ------------------------------------------------------------------ | ------ | ----------------------------------------------------------------------------- |
| `GetUserGames(int authUserId)`                                     | GET    | Retrieves a list of games for a specific user based on their user ID.         |
| `AddGames(int authUserId, NewGameDTO gameToAdd)`                   | POST   | Adds a new game for a specific user and returns the game details.             |
| `DeleteGame(int authUserId, int gameId)`                           | DELETE | Deletes a game by game ID and user ID.                                        |
| `publishGame(int authUserId, PublishGame game)`                    | PUT    | Updates the publication status of a game by game ID and user ID.              |
| `CheckIfPublished(int authUserId, int id, GamesTable game)`        | GET    | Checks if the game is already published; updates publication status if not.   |
| `EditGameSettings(int authUserId, int id, EditGameDTO gameToEdit)` | PUT    | Updates game settings such as time limits and game name.                      |
| `CanPublishFunc(int gameId)`                                       | GET    | Internal method to verify if the game can be published based on set criteria. |
| `GetGame(int authUserId, int id)`                                  | GET    | Retrieves specific game details for a user based on the game code.            |

### MediaController

| Endpoint                                        | Method | Description                                                                                     |
| ----------------------------------------------- | ------ | ----------------------------------------------------------------------------------------------- |
| `UploadFile([FromBody] string imageBase64)`     | POST   | Accepts a Base64 image, saves it as a PNG in uploadedFiles directory, and returns the filename. |
| `UploadFileTemp([FromBody] string imageBase64)` | POST   | Temporarily saves an image as PNG in uploadTemp directory and returns the filename.             |
| `DeleteImages([FromBody] List<string> images)`  | POST   | Deletes a list of specified images from storage.                                                |
| `MoveFiles([FromBody] List<string> fileNames)`  | POST   | Moves files from uploadTemp to uploadedFiles directory.                                         |

### QuestionsController

| Endpoint                                                                                  | Method | Description                                                                                    |
| ----------------------------------------------------------------------------------------- | ------ | ---------------------------------------------------------------------------------------------- |
| `GetQuestions(int authUserId, int gameId)`                                                | GET    | Retrieves all questions for a specific game if the user is authenticated.                      |
| `GetAnswers(int questionId)`                                                              | GET    | Retrieves all answers for a specific question if it exists.                                    |
| `GetQuestion(int authUserId, int questionId)`                                             | GET    | Returns question details and its answers if the user is authenticated and the question exists. |
| `CreateQuestion(int authUserId, [FromBody] QuestionToEdit newQuestion)`                   | POST   | Creates a new question with answers for an existing game if authenticated.                     |
| `CreateAnswer(int questionId, [FromBody] AnswerToShow newAnswer)`                         | POST   | Adds a new answer to an existing question.                                                     |
| `EditQuestion(int authUserId, int questionId, [FromBody] QuestionToShow updatedQuestion)` | PUT    | Edits an existing question and its answers.                                                    |
| `DeleteQuestion(int questionId)`                                                          | DELETE | Deletes an existing question and all its associated answers.                                   |
| `DeleteAnswer(int authUserId, int answerId)`                                              | DELETE | Deletes an answer if authenticated and more than two answers exist for the question.           |
| `UpdateImages(int id, [FromBody] string ImgName)`                                         | POST   | Updates the image name for a specific question in the database.                                |
| `UpdateImagesAnswer(int id, [FromBody] string ImgName)`                                   | POST   | Updates the image name for a specific answer in the database.                                  |
| `DeleteImageReference(int authUserId, int answerId, [FromBody] dynamic data)`             | DELETE | Deletes the image reference for a specific answer if authenticated.                            |

### UnityController

| Endpoint                     | Method | Description                                                                                       |
| ---------------------------- | ------ | ------------------------------------------------------------------------------------------------- |
| `GameCode(int authGameCode)` | GET    | Checks if the game code exists and is published; returns game details with questions and answers. |

### UsersController

| Endpoint                       | Method | Description                                                       |
| ------------------------------ | ------ | ----------------------------------------------------------------- |
| `GetLoginUser(int authUserId)` | GET    | Verifies user authentication and returns the logged-in user's ID. |

## Setup and Installation

1. Clone the repository:

   ```
   git clone <repository_url>
   cd <repository_name>
   ```

2. **Backend Setup:**

   - Ensure APIs are hosted correctly. Use IIS or Visual Studio for local testing.
   - Update URLs in Unity's `ServerManagerScript` to the correct server base path.

3. **Running the Application:**

   - Use Visual Studio to build and run the Blazor application.
   - Configure the database and apply migrations if needed.

4. **Unity Integration:**
   - Set up Unity to connect to the Blazor backend via the `ServerManagerScript`.
   - Update `projectURL` in Unity to match your backend server's URL.

## How to Play

1. **Start the Game:**

   - Enter the game code to start.

2. **Answer Questions:**

   - Select the correct answer from the options.
   - Receive immediate feedback and progress through questions.

3. **Complete the Game:**
   - After finishing all questions, view your score, and restart if desired.

## Development Notes

- **Primary Technologies**: C#, Blazor, Unity, SQL
- **Database and APIs**: SQL database and custom REST APIs for game and media management.
- **Error Handling**: Extensive error handling and feedback mechanisms for a seamless user experience.
