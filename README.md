# HackerRank: Code Review Feedback

|Link|Desc|
|--|--|
| [solution1](./solution1.md)| flat state|
| [solution2](./solution2.md)| nested objects |
| [see live version on vercel](https://hackerrank-react-code-review.vercel.app/)|deployed solution 1|
| [see HackerRank Website](https://hackerrank-react-code-review.vercel.app/)| for details|

Your task is to create a React application called "Code Review Feedback" that tracks and manages feedback on various aspects of code quality. The component should have upvote and downvote functionality for each aspect, and it must meet all specified requirements.



![image](public\gif-converter.gif)


# Detailed Requirements

> The CodeReviewFeedback component displays five aspects: Readability, Performance, Security, Documentation, and Testing.

> Each aspect has two buttons labeled "Upvote" and "Downvote" to allow users to vote.

> The initial count for upvotes and downvotes for each aspect is set to zero.

> Clicking the "Upvote" button should increment the upvote count for that aspect by 1.

> Clicking the "Downvote" button should increment the downvote count for that aspect by 1.

> Ensure the counts update in the UI immediately upon clicking.

> The component should have a subtle animation when the voting count is updated to enhance the user experience.


# Sample Interaction

## Initial State

    Display all five aspects with their respective upvote and downvote buttons.
    Each aspect shows an initial count of 0 for upvotes and downvotes.

## User Action 1

    User clicks "Upvote" for Readability.
    The upvote count for Readability displays 1.

##  User Action 2

    User clicks "Downvote" for Performance.
    The downvote count for Performance displays 1.

User Action 3 3. User clicks "Upvote" for Security and Documentation multiple times. 4. The upvote count for Security displays 2 and Documentation displays 3.