# Ex.no.8-Building-a-Simple-College-Admission-Chatbot
## Aim :
 To design, implement and test a simple rule-based chatbot in Python that answers frequently asked questions related to college admissions, such as courses offered, eligibility criteria, fees, application process, required documents, important dates, hostel facilities and contact details.
### Introduction
A chatbot is a software application that simulates a conversation with a human user, typically through text. A rule-based (or pattern-matching) chatbot works by comparing the user's message against a predefined set of keywords or patterns and returning a suitable pre-written response. It does not require large training datasets or heavy computation, which makes it an easy and beginner-friendly starting point for understanding how conversational AI systems are built. In this experiment, a College Admission Chatbot is developed to act as a virtual help-desk assistant that instantly answers common queries asked by prospective students.
### Procedure
### Step 1: Import Required Libraries
●	re – Python's regular expression module, used to search for keyword patterns inside the user's message.
●	random – used to randomly pick one response when more than one reply is available for the same intent, so the chatbot does not sound repetitive.
<img width="605" height="37" alt="image" src="https://github.com/user-attachments/assets/5d19fe62-e644-4676-805b-2fe23826e1da" />
### Step 2: Design the Knowledge Base (Intents and Responses)
●	The knowledge base is stored as a Python dictionary, where every key is an intent (topic) such as courses, eligibility, fees or hostel.
●	Each intent stores a list of patterns (keywords/phrases likely to appear in a user's question) and a list of possible responses.
●	Organising the data this way makes the chatbot easy to extend — a new admission topic can be added simply by adding one more entry to the dictionary.
<img width="642" height="222" alt="image" src="https://github.com/user-attachments/assets/146afc71-fa16-4c84-a959-c91bbc2842eb" />
<img width="618" height="359" alt="image" src="https://github.com/user-attachments/assets/6b976de7-7dce-4418-a526-d25b31c66e79" />
Knowledge Base Summary
The table below summarises the complete knowledge base used by the chatbot:
<img width="669" height="403" alt="image" src="https://github.com/user-attachments/assets/991481a9-e6a3-4ce8-a3d0-2f07c4c7adf2" />
### Step 3: Function to Match User Input to an Intent
●	Converts the user's sentence to lower case so that matching is not case-sensitive.
●	re.search() scans the message for each pattern of every intent; the first intent whose pattern is found is returned.
●	If no pattern matches any intent, the function returns None so the fallback response can be used.
<img width="632" height="115" alt="image" src="https://github.com/user-attachments/assets/b4e8db5f-7e9c-4e48-9aeb-82d4c9e43097" />
### Step 4: Define the Chatbot Response Function
●	Calls match_intent() to identify what the user is asking about.
●	random.choice() picks one response from the matched intent's response list.
●	Returns a fallback message when the intent could not be identified, instead of leaving the user without a reply.
<img width="623" height="95" alt="image" src="https://github.com/user-attachments/assets/ab6895ac-bba4-4e66-9c51-cacf8d828286" />
### Step 5: Build the Interactive Conversation Loop
●	input() continuously reads the user's message from the console.
●	get_response() generates the reply for every message typed by the user.
●	The loop ends automatically once the matched intent is “goodbye” (e.g. the user types bye / exit / quit).
<img width="632" height="126" alt="image" src="https://github.com/user-attachments/assets/ae562d77-2461-4bed-b4c1-461b1cea5728" />
### Step 6: Test the Chatbot with Sample Queries
●	A list of realistic sample questions is used to automatically test every intent in the knowledge base.
●	Each query and the chatbot's corresponding reply are printed, which makes it easy to verify that every category of question is answered correctly.
<img width="622" height="113" alt="image" src="https://github.com/user-attachments/assets/4fdb6b4b-c684-4033-94e1-0d51fa19e99b" />
<img width="583" height="251" alt="image" src="https://github.com/user-attachments/assets/2ba37096-9575-4164-b4c3-ebca74ca9aab" />
### Step 7: Run the Chatbot
The complete script is executed in Python. Since input() cannot be used for automated testing, the sample_queries list from Step 6 is run first to validate every intent; the same get_response() function also powers the live chat() loop for real-time conversation with a user. The output produced on running the program is shown below.
Output
### Sample Conversation Output (Part 1)
●	The chatbot correctly greets the user and identifies the courses, eligibility, fees, application process and documents intents from the keywords present in each question.
<img width="646" height="470" alt="image" src="https://github.com/user-attachments/assets/016e1f31-dd01-4348-8815-70b3577b1391" />
### Sample Conversation Output (Part 2)
●	The remaining queries about dates, hostel facility and contact details are correctly matched to their respective intents.
●	The conversation ends gracefully with a goodbye message once the user types “Bye”, terminating the chat loop.
<img width="660" height="380" alt="image" src="https://github.com/user-attachments/assets/698ac90d-7962-406c-b381-03d16bedfb3b" />
## Conclusion
Thus, a simple rule-based College Admission Chatbot was successfully designed, implemented and tested using Python. The chatbot uses a keyword/pattern-based knowledge base to identify the intent behind a user's question and responds with an appropriate, pre-defined answer covering courses, eligibility, fees, application process, documents, dates, hostel and contact information. The experiment demonstrates the fundamental building blocks — knowledge base design, intent matching and response generation — on which more advanced NLP-based and AI-based chatbots are built.


import re
import random

# Knowledge Base
intents = {
    "greeting": {
        "patterns": [r"\bhi\b", r"\bhello\b", r"\bhey\b"],
        "responses": [
            "Hello! Welcome to the College Admission Help Desk.",
            "Hi! How can I help you with college admissions?"
        ]
    },

    "courses": {
        "patterns": [r"courses?", r"programmes?", r"degrees?", r"branches?"],
        "responses": [
            "We offer UG and PG courses in Engineering, Science, Commerce and Arts."
        ]
    },

    "eligibility": {
        "patterns": [r"eligibility", r"eligible", r"qualification", r"criteria"],
        "responses": [
            "Eligibility depends on the course. Students must satisfy the required academic qualifications."
        ]
    },

    "fees": {
        "patterns": [r"fees?", r"fee structure", r"cost", r"tuition"],
        "responses": [
            "The fee structure varies according to the course. Please contact the admission office for details."
        ]
    },

    "application": {
        "patterns": [r"apply", r"application", r"admission process", r"how to join"],
        "responses": [
            "You can apply online through the college admission portal by filling out the application form."
        ]
    },

    "documents": {
        "patterns": [r"documents?", r"certificates?", r"required documents"],
        "responses": [
            "Required documents generally include mark sheets, transfer certificate, ID proof and passport-size photographs."
        ]
    },

    "dates": {
        "patterns": [r"dates?", r"deadline", r"last date", r"important dates"],
        "responses": [
            "Please check the official college admission notice for the latest application and counselling dates."
        ]
    },

    "hostel": {
        "patterns": [r"hostel", r"accommodation", r"rooms?"],
        "responses": [
            "Yes, hostel facilities are available for students with separate accommodation arrangements."
        ]
    },

    "contact": {
        "patterns": [r"contact", r"phone", r"email", r"address"],
        "responses": [
            "For admission enquiries, please contact the college admission office."
        ]
    },

    "goodbye": {
        "patterns": [r"\bbye\b", r"exit", r"quit"],
        "responses": [
            "Thank you for contacting the College Admission Help Desk. Goodbye!"
        ]
    }
}


# Function to match user input with an intent
def match_intent(user_input):
    user_input = user_input.lower()

    for intent, data in intents.items():
        for pattern in data["patterns"]:
            if re.search(pattern, user_input):
                return intent

    return None


# Function to generate chatbot response
def get_response(user_input):
    intent = match_intent(user_input)

    if intent:
        return random.choice(intents[intent]["responses"])

    return "Sorry, I could not understand your question. Please ask about courses, eligibility, fees, application, documents, dates, hostel or contact details."


# Sample queries for testing
sample_queries = [
    "Hello",
    "What courses are offered?",
    "What is the eligibility criteria?",
    "How much are the fees?",
    "How can I apply?",
    "What documents are required?",
    "What is the last date for admission?",
    "Is hostel facility available?",
    "How can I contact the college?",
    "Bye"
]


# Automated testing
print("----- Sample Conversation -----")

for query in sample_queries:
    print("User:", query)
    print("Bot :", get_response(query))
    print()


# Live chatbot
def chat():
    print("----- College Admission Chatbot -----")
    print("Type 'bye' to exit.")

    while True:
        user_input = input("You: ")
        response = get_response(user_input)
        print("Bot:", response)

        if match_intent(user_input) == "goodbye":
            break


# Start chatbot
chat()







