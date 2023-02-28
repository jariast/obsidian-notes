## Introduction

You will create a screen recording video of yourself completing the challenge, then send me a link to the file via Google Drive. A few things to consider:

-   We ask that you complete this challenge within the timeframe agreed on in our conversation.
-   **You MUST NOT edit your video, stop it and continue later, use a second screen, copy contents from hidden screens, or anything similar that can be considered cheating. The recording must be without stopping and with no editing.**
-   **You MUST show your operating system clock during the entire recording. Please, do not maximize your screen in a way your operating system clock is hidden. Always keep it visible.**
-   You can use screen recording software like Loom, QuickTime, or something similar, to create the video.
-   The recording should be of the entire coding challenge, from the beginning to end, which is about 70 minutes.
    -   **You will use 45 minutes for the coding challenge and 25 minutes for the problem-solving challenge.**
    -   Remember to record the coding challenge and the problem-solving challenge **together in just one video**; please **do not stop/play and join the video**; if you do it, you will be disqualified.
    -   You can spend more than 45 minutes on the coding challenge, but we will discount points on your challenge. But please, be careful with the 25 minutes limit on the problem-solving challenge; you should avoid spending more than the time limit.
-   You should record your entire screen so we can validate your implementation correctly. **Also, your computer clock should be visible in the entire video.**
-   Please upload the video file to Google Drive and share an open link with us (we support .mp4, files smaller/with less than 4gb).
-   As you complete the challenge, please explain what you are doing. Walk us through your thinking, explain your decisions, etc. Show us your UI work, if applicable.
-   Here is a short clip from a recent coding challenge, as an example of what your recording should look like: [Example video](http://www.loom.com/share/85434243d487456b8ef4ae45c3fbc788). It is from a React challenge, but it is the same for any challenge.

## The Coding Challenge

### Getting Started

Hi! Welcome to the React coding challenge! We want to check your React knowledge by giving you an application to finish. We already have an application, but it is incomplete; your goal is to finish this application and make the application usable.

> _We have a project structured with a pattern, so the time suggested above can be done following the pattern and splitting your time into categories; a good organization will lead you to finish the challenge successfully!_

> _Remember that we are not requesting you to create a responsive application; you can focus only on the web version._

<aside> ⏳ **Recommended duration for each category in the challenge (this is a suggestion) -** **Styling**: 15 minutes **- Components creation**: 10 minutes **- Services and logic**: 10 minutes **- Unit testing**: 10 minutes

_Of course, you can split the time as you want, but we recommend you follow this._

</aside>

### Instructions

The current application displays a list of monsters. Right now, we only have the feature of selecting the player's monsters; your job is to implement the missing functionalities.

You will have to create the monster's card component so we can visualize the monster's strengths and weaknesses correctly.

After selecting the player's monster, you will have to implement the logic to get the computer's monster, which should be randomly selected, not allowing be the same selected as the player; remember that you will select the player's monster by clicking on it.

Once both monsters are selected, the user can “start the battle," and you must implement the service request. We already have an endpoint ready for it. You don't need to worry about the endpoint implementation or even the logic to calculate the monster's battle; your job will be to make the request and display the battle result correctly.

### API

We have our local API configured inside the project. To start it, you should run the command `npm run serve:data`, which will start the server.

_We do not recommend you change any data inside the `data` folder; your goal is to implement the challenge with the data already provided and running._

We have two endpoints, which are the following:

-   `GET /monsters`: This endpoint will return all the needed info for the monster's list.
-   `POST /battle`: This endpoint will receive a body and return the battle's result.

The `GET /monsters` return the following contract when requested:

```bash
[
	{
		"id": "id",
		"name": "Monster 1",
		"attack": 20,
		"defense": 30,
		"hp": 100,
		"speed": 50,
		"type": "Type",
		"imageUrl": "url"
	}
]
```

The `POST /battle` expects to receive a body with the monsters' information; the expected body is the following:

```bash
{
	"monster1Id": "monster-1",
	"monster2Id": "monster-2"
}
```

### Technologies

This project is built using the React ecosystem libraries; it is good you know the following items to have a good performance:

-   [Typescript](https://www.typescriptlang.org/docs/)
-   [React](https://reactjs.org/docs/getting-started.html)
-   [Redux](https://redux-toolkit.js.org/introduction/getting-started)
-   [Material UI](https://mui.com/material-ui/getting-started/usage/)
-   [Jest](https://jestjs.io/docs/getting-started)
-   [Jest Fetch Mock](https://www.npmjs.com/package/jest-fetch-mock)
-   [React testing Library](https://testing-library.com/docs/react-testing-library/intro/)

### Acceptance Criteria

1.  Implementation matches the design
2.  Tests pass, and coverage has been added to cover the changes and new implementations
3.  The computer monster is randomly selected after selecting the player monster
4.  The winner's message should be presented after the battle

### Design

You will need to login or create an account in [Figma](https://www.figma.com/)

After that, you will need the following link for the challenge:

-   [Figma Design](https://www.figma.com/file/wXA5toXu2tZJyhXNY5b5zB/Battle-of-Monsters---Front-End) _(You can use the "Inspect" tab to see the CSS values)_

**Note**: the _“Inspect”_ tab option will just show up if you are logged in; that’s why you need to login or create an account in Figma.

![You will have these options after login](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/89d4320b-15b1-4f1b-96df-7c69cc1db04a/Untitled.png)

You will have these options after login

## The Problem-Solving Challenge

Hi! Welcome to the TypeScript problem-solving code challenge; we want to test your problem-solving skills here.

You will be provided a repository with some challenges and have to solve them by implementing and making all the created tests pass.

> Please, remember to **NOT USE GOOGLE** to solve the reasoning challenges; try to solve them by yourself.

### Challenges

We will provide three challenges on the repository; you will have a time limit mentioned above minutes to solve them and make them pass the tests.

_If you cannot finish all challenges, send the record with what you solved, and we will evaluate it._

Remember to solve them using pure TypeScript, and avoid using libraries or anything that is not your code; we want to see you thinking and solving the challenge.

You can do them in any order, but remember that some challenges are more complex than others.

**At the end of the challenge, run the tests for us before stopping recording. This step is critical; if you forget to do it, it will cause your disqualification.**

### Acceptance Criteria

1.  The code should be readable.
2.  The code should be easy to maintain.
3.  The code should not be complex.
4.  All tests should pass.
5.  **Tests pass**