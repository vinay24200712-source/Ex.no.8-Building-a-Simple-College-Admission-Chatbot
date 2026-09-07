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
import re

# ---------------------------------------
# College Admission Chatbot
# ---------------------------------------

knowledge_base = {
    "greeting": {
        "patterns": ["hi", "hello", "hey", "good morning", "good afternoon"],
        "responses": [
            "Hello! Welcome to the College Admission Help Desk. How can I assist you today?"
        ]
    },

    "courses": {
        "patterns": [
            "course", "courses", "program", "programs",
            "branch", "department", "specialization"
        ],
        "responses": [
            "We offer B.Tech programs in Information Technology, "
            "Computer Science, ECE, EEE and Mechanical Engineering, "
            "along with M.Tech and MBA programs."
        ]
    },

    "eligibility": {
        "patterns": ["eligibility", "qualification", "marks", "criteria"],
        "responses": [
            "For B.Tech admission, students should have completed "
            "12th standard with the required subjects and marks. "
            "Eligibility may vary depending on the program."
        ]
    },

    "fees": {
        "patterns": ["fee", "fees", "tuition", "cost", "scholarship"],
        "responses": [
            "Tuition fees depend on the selected course and admission category. "
            "Scholarships may be available for eligible students."
        ]
    },

    "dates": {
        "patterns": [
            "date", "dates", "deadline", "last date",
            "admission date", "important date"
        ],
        "responses": [
            "Admission dates and deadlines are announced by the college. "
            "Please check the official admission notification for the latest dates."
        ]
    },

    "application_process": {
        "patterns": [
            "application", "apply", "application process",
            "how to apply", "admission process"
        ],
        "responses": [
            "You can apply by filling out the online application form, "
            "uploading the required documents and paying the application fee."
        ]
    },

    "documents": {
        "patterns": [
            "document", "documents", "certificate",
            "required documents", "proof"
        ],
        "responses": [
            "Commonly required documents include 10th and 12th mark sheets, "
            "transfer certificate, ID proof, passport-size photographs "
            "and other required certificates."
        ]
    },

    "hostel": {
        "patterns": [
            "hostel", "accommodation", "room",
            "hostel facility", "stay"
        ],
        "responses": [
            "Hostel and accommodation facilities are available for students. "
            "Please contact the admission office for room availability and fees."
        ]
    },

    "contact": {
        "patterns": [
            "contact", "phone", "email", "address",
            "admission office", "office"
        ],
        "responses": [
            "For admission-related queries, please contact the college "
            "admission office through the official college website or phone number."
        ]
    },

    "thanks": {
        "patterns": ["thanks", "thank you", "thank", "thx"],
        "responses": [
            "You're welcome! I'm happy to help."
        ]
    },

    "goodbye": {
        "patterns": ["bye", "goodbye", "see you", "exit", "quit"],
        "responses": [
            "Thank you for contacting the College Admission Help Desk. Goodbye!"
        ]
    }
}


# ---------------------------------------
# Find chatbot response
# ---------------------------------------

def get_response(user_input):
    user_input = user_input.lower().strip()

    for intent, data in knowledge_base.items():

        for pattern in data["patterns"]:

            # Match complete words
            if re.search(r"\b" + re.escape(pattern) + r"\b", user_input):
                return data["responses"][0]

    return (
        "I'm sorry, I did not quite understand that. "
        "Could you please rephrase your question?\n\n"
        "I can help with courses, eligibility, fees, application process, "
        "documents, dates, hostel and contact details."
    )


# ---------------------------------------
# Start Chatbot
# ---------------------------------------

def chatbot():
    print("=" * 60)
    print("       COLLEGE ADMISSION CHATBOT")
    print("=" * 60)
    print("Type 'bye' or 'exit' to close the chatbot.\n")

    while True:

        user_input = input("You: ")

        response = get_response(user_input)

        print("Bot:", response)
        print()

        if user_input.lower().strip() in ["bye", "goodbye", "exit", "quit"]:
            break


# ---------------------------------------
# Main Program
# ---------------------------------------

if __name__ == "__main__":
    chatbot()
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









