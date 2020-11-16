# Jitsi PubQuiz 2020

This is a submission for PubQuiz with Jitsi for the Hacking from Home Hackathon.

## Colaborators

Main work was done during [Seven Principles](https://7p-mobility.com/de/) AMR Hackathon (13.11. 10:30 AM - 14.11. 10:30 AM)
Team members are:
* Peter Hennecke
* Karl Kaminski
* Michael Hess
* Saeid Khoshhal
* Felix Hofschulte
* Jaqueline Schweigert

## Brief summary of PubQuiz:

During covid times a lot of social interaction got lost. All summer / winter parties are canceled and nearly everybody worked from home for a long time. 
To enhance social interaction between you and your colleagues, we invented a digital form of the offline PubQuiz.
"A pub quiz is a quiz held in a pub or bar. These events are also called quiz nights, trivia nights, or bar trivia" (see [Wikipedia](https://en.wikipedia.org/wiki/Pub_quiz))

The pub quiz is the perfect possibilty to get to know your team mates and improve team collobaration. 
First a quiz master selects categories and creates questions for each category.
Sample categories might be "Celebrities", "Sports" or "Movies".
Afterwards each player logs in by providing a name and a quiz identifier. 
The quiz id is used to create a Jitsi room. 
When all players arrived, the quiz master finally starts the first round. All team members are split into small teams (up to five members).
While answering the questions together, they can communicate via Jitsi.
If one player enters the solution, all other players of the sub team can see the input as well.
After each round as well as at the end of the quiz, all players come back to a joined room.
The quiz master evaluates the given answers and scores points.

## Our solution

As frontend we utilized [Svelte](https://svelte.dev/).
For saving the required quiz data (metadata, rounds, questions, teams, scores..) we developed a [Spring Boot](https://spring.io/projects/spring-boot) backend in Java.
As a database we used [PostgreSQL](https://www.postgresql.org/).
For communication between Svelte UI and Spring backend we created REST API, the swagger documentation is available via: TODO

Due to the time limitations, we couldn't implement all screen. We designed a few more screens using [Zeplin](https://zeplin.io/).

## Any supporting references
* [Screencast/Demo](https://drive.google.com/file/d/1E_FZeNRbj9Godry6lUFcQRXWX60SW2vP/view?usp=sharing)
* [More sample questions](https://drive.google.com/file/d/1xh-D9TVg_Ylgzcd-mViewL44izbwNP5h/view?usp=sharing)
* [More screens in Zeplin](https://drive.google.com/file/d/1DReA3QtIJDkgayvCZGN7JhX6j8cGXMz9/view?usp=sharing)

## Questions?
You can send questions to jaqueline.schweigert@7p-group.com
