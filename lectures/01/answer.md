# Lecture 01 Answers

## Exercises

- Model's answer to the course-specific question (the 3 homework levels; a summary is fine):
- What you noticed when comparing it with the correct meaning in the glossary:
- Token counts you displayed (input / output):

## Homework

- Level attempted: Basic / Implementation / Advanced
- What you did:
- Results:
- Observations and questions:

- Level attempted: Basic 
1. What you did: ask the question:Explain how recursion works to a 10-year-old using an analogy that most people wouldn’t think of, in exactly 3 sentences.
- Ran the same prompt using Gemini 3.5 Flash Lite (baseline).
- Increased temperature to 1.8 using the same model.
- Changed to the newer Gemini 3.8 Flash model.
2. Results:
- Baseline: Used a Russian nesting dolls analogy to explain recursion.
- Temperature 1.8: Kept the same analogy but made the explanation more creative with a detective story.
- Higher model: Used a jawbreaker candy analogy and explained the stopping condition (Base Case) more clearly.
3. Observations and questions:
- Higher temperature changed the writing style but not significantly the main analogy.
- The newer model provided a different analogy and explained recursion more clearly.
- All three responses followed the three-sentence requirement.
- Question: Does increasing the model version improve answer quality more than increasing temperature?


- Level attempted:Implementation
- What you did: i modify the file ask.py by adding history feature where it store the question and answer in a while true loop that stop when i respond with exit and each time the history and the question are sen to the model.so i ask a definition of processor and then asked him for an exemple of model
- Results:the respond was first a short definition then the history worked by giving me an exemple of processor i7
- Observations and questions:
i noticed that the model has well handeled the history of question so the response stay in the correct context 
but if the history became very long how the model handel it by preserving the quality of response 


- Level attempted: Advanced
- What you did:i have add the token and time couter and ask same question for 3.5 falsh lite and 3.8 flash what is processor and then i add explain in details for all exemples of devices
- Results:3.5 flash lite respond in 3 s and total of 484 token but 3.8 flash respond in 138 s and 1361 token for what is processor and the other question 3.5 flash lite respond in 11.71 s and 1308 token
- Observations and questions:
respond time and token usage vary by the model and the question type .and for gemini free quota there is rpm and tpm rpd so even you have access but there is alimit.if so when we have a history if conversation get long the usage and respond increase so how should we manage this efficiently. 