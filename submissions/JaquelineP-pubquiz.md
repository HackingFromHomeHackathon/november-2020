# Jitsi PubQuiz 2020

This is a submission for PubQuiz with Jitsi for the Hacking from Home Hackathon.

## Preface

Lately a lot of social interaction got lost due to covid restrictions. 
Most of the developers are working from home for a long time. Furthermore, all social company events are canceled.
_70 % of employees say friends at work is the most crucial element to a happy working live_ quotes [theuse](https://www.themuse.com/advice/why-having-friends-at-work-is-actually-crucial-to-your-success). 
Having a good working atmosphere increases personal development, speed of the software development as well as the commitment to high quality.

## Our solution: PubQuiz

To enhance social interaction between you and your colleagues, we invented a digital form of the offline PubQuiz.
_A pub quiz is a quiz held in a pub or bar. These events are also called quiz nights, trivia nights, or bar trivia_ (see [Wikipedia](https://en.wikipedia.org/wiki/Pub_quiz))

The pub quiz is the perfect possibility to get to know your teammates and improve team collaboration. 
First a quiz master selects categories and creates questions for each category.
Sample categories might be _Celebrities_, _Sports_ or _Movies_.
Afterwards each player logs in by providing a name and a quiz identifier. 
The quiz id is used to create a Jitsi room. 
When all players arrived, the quiz master finally starts the first round. All team members are split into small teams (up to five members).
While answering the questions together, they can communicate via Jitsi.
If one player enters the solution, all other players of the subteam can see the input as well.
After each round as well as at the end of the quiz, all players come back to a joined room.
The quiz master evaluates the given answers and scores points.

## Our tech stack

As a frontend, we utilized [Svelte](https://svelte.dev/).
For saving the required quiz data (metadata, rounds, questions, teams, scores etc) we developed a [Spring Boot](https://spring.io/projects/spring-boot) backend in Java.
As a database, we used [PostgreSQL](https://www.postgresql.org/).
For communication between Svelte UI and Spring backend we created REST API, the swagger documentation is available upon request. ![Preview](https://drive.google.com/file/d/1YWKzt-truh231JYsroLjq0SwP_niyCbj/view?usp=sharing) 

Due to the time limitations, we could not implement all screens. We designed a few more screens using [Zeplin](https://zeplin.io/).

## Features
* Audio and video communication using JitsiMeetJS API
* Collobartive answering of questions
* Different question types: free text, multiple choise, video / photo questions, google autocomplete or map questions

## Supporting references

* [Screencast/Demo](https://drive.google.com/file/d/1E_FZeNRbj9Godry6lUFcQRXWX60SW2vP/view?usp=sharing)
* [More sample questions](https://drive.google.com/file/d/1xh-D9TVg_Ylgzcd-mViewL44izbwNP5h/view?usp=sharing)
* [More screens in Zeplin](https://drive.google.com/file/d/1DReA3QtIJDkgayvCZGN7JhX6j8cGXMz9/view?usp=sharing)

## Colaborators

The main work was done during [Seven Principles](https://7p-mobility.com/de/) AMR Hackathon (13.11. 10:30 AM - 14.11. 10:30 AM).

The team consists of:
* Felix Hofschulte
* Jaqueline Schweigert
* Karl Kaminski
* Michael Hess
* Peter Hennecke
* Saeid Khoshhal

## Questions?
You can send questions to [jaqueline.schweigert@7p-group.com](mailto:jaqueline.schweigert@7p-group.com)
