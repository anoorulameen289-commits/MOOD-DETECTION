data = [
    ("I got full marks in the test today", "Happy"),
    ("We won the college cricket match", "Happy"),
    ("I lost my phone on the bus", "Sad"),
    ("I failed in the mathematics exam", "Sad"),
    ("I got a new bicycle", "Happy"),
    ("My best friend visited me", "Happy"),
    ("I missed my college bus", "Sad"),
    ("I enjoyed the birthday party", "Happy"),
    ("I broke my favourite watch", "Sad"),
    ("I received a gift from my parents", "Happy"),
    ("I lost my wallet", "Sad"),
    ("I scored good marks in the exam", "Happy"),
    ("My team lost the final match", "Sad"),
    ("I had a great day with friends", "Happy"),
    ("I forgot my assignment at home", "Sad")
]


def count_moods(data):
    happy = 0
    sad = 0

    for sentence, mood in data:
        if mood == "Happy":
            happy += 1
        else:
            sad += 1

    return happy, sad


happy_count, sad_count = count_moods(data)

print("Happy:", happy_count)
print("Sad:", sad_count)


happy_words = [
    "happy", "won", "gift", "great", "good",
    "enjoyed", "love", "marks", "visited", "scored"
]

sad_words = [
    "lost", "failed", "missed", "broke",
    "forgot", "sad", "cry", "lonely"
]


def guess_mood(sentence):
    happy = 0
    sad = 0

    sentence = sentence.lower()

    for word in happy_words:
        if word in sentence:
            happy += 1

    for word in sad_words:
        if word in sentence:
            sad += 1

    if happy > sad:
        return "Happy"
    elif sad > happy:
        return "Sad"
    else:
        return "unknown mood"


correct = 0

for sentence, practice_mood in data:
    predicted_mood = guess_mood(sentence)

    print(sentence, ":", predicted_mood)

    if predicted_mood == practice_mood:
        correct += 1


accuracy = (correct / len(data)) * 100

print("Correct Predictions:", correct)
print("Total Data:", len(data))
print("Accuracy:", accuracy, "%")


def learn_scores():
    scores = {}

    for sentence, mood in data:
        sentence = sentence.lower()

        for word in happy_words:
            if word in sentence:
                if word not in scores:
                    scores[word] = {"Happy": 0, "Sad": 0}
                scores[word][mood] += 1

        for word in sad_words:
            if word in sentence:
                if word not in scores:
                    scores[word] = {"Happy": 0, "Sad": 0}
                scores[word][mood] += 1

    return scores


def guess_mood_learned(sentence):
    scores = learn_scores()
    happy = 0
    sad = 0

    sentence = sentence.lower()

    for word in scores:
        if word in sentence:
            happy += scores[word]["Happy"]
            sad += scores[word]["Sad"]

    if happy > sad:
        return "Happy"
    elif sad > happy:
        return "Sad"
    else:
        return "Not sure"


print("\nLearned Mood Prediction:")
print(guess_mood_learned("I won the college match"))
