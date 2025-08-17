# steamnoodles-feedback-agent-himashaSandeepani
1.	Feedback Response Agent – Auto-replies to customer reviews based on sentiment.
2.	Sentiment Visualization Agent – Plots positive/negative/neutral sentiment trends over time.

Name - Yaddehige Himasha Sandeepani

University - NSBM

Year - 2 Year

Summary – Agent 1: Customer Feedback Response Agent

This agent is designed to automatically analyse customer reviews, detect sentiment, and generate personalised restaurant responses. The workflow is as follows:

1. Sentiment Detection — Hugging Face's DistilBERT sentiment analysis model (distilbert-base-uncased-finetuned-sst-2-english) classifies the review as positive or negative.
2. LLM-Powered Response Generation – Employs the Groq LLM (llama-3.3-70b-versatile) through LlamaIndex to create short, polite, and personalised replies based on the detected sentiment.
3. Chunking & Embedding Setup – Configures HuggingFace embeddings (BAAI/bge-small-en-v1.5) with SentenceSplitter to handle knowledge base text processing (future scalability for larger datasets).
4. Tool Integration – Demonstrates LlamaIndex FunctionTool usage with simple addition and multiplication tools (extendable to more restaurant-related utilities).
5. Execution Flow,

Input: Raw customer review.

Step 1: Sentiment classification.

Step 2: Prompt generation using sentiment context.

Step 3: LLM produces the final customer-facing reply.

Output: Polite, sentiment-aware restaurant response.

Example,

Review: "The food was great, but the service was a bit slow."

Sentiment: neutral/negative

Response: 

"Dear valued customer,
Thank you for taking the time to share your feedback about your recent visit to our restaurant. We're thrilled to hear that you enjoyed the food, and we appreciate your kind words. However, we apologize that the service was slower than expected. We take pride in providing exceptional service, and it's clear we fell short in your case. We'll use your feedback to improve our timing and ensure that all our guests receive the level of service they deserve. We hope to have the opportunity to serve you again and show you a more seamless dining experience.

Best regards,
[Your Restaurant Name]"


Summary – Agent 2: Sentiment Plotting Agent

This agent analyses restaurant review data over time, infers sentiment from ratings, and visualises sentiment trends within a given date range.

1. Data Loading & Cleaning,
- Reads review data from "Restaurant reviews.csv".
- Parses the Time column into a valid datetime format and removes rows with invalid timestamps.
2. Sentiment Inference – Uses a simple rule-based function infer_sentiment() to classify reviews as:
- Positive: Rating ≥ 4.0
- Neutral: 3.0 ≤ Rating < 4.0
- Negative: Rating < 3.0
- Unknown: Invalid or missing ratings.
3. Date Range Filtering – Filters reviews between start_date and end_date for focused trend analysis.
4. Trend Aggregation – Groups filtered reviews by date and sentiment category, counting the number of occurrences per sentiment.
5. Visualisation – Creates a stacked bar chart showing the daily distribution of positive, neutral, and negative reviews.
6. Saves the visualisation as "sentiment_trend.png".

Example,

For the date range 2019-05-20 to 2019-05-26, the agent outputs a bar chart showing how customer sentiment varied day by day.


Setup & Run Instructions – Agent 1: Customer Feedback Response Agent

1. Open Google Colab - Go to [Google Colab](https://colab.research.google.com/) and open a new Python notebook.
2. Install Required Dependencies - Run this in the first cell to install all required packages:

!pip install llama-index llama-index-core llama-index-embeddings-huggingface llama-index-llms-groq transformers

3. Add Your Groq API Key - Replace the 'API_KEY' variable in your script with your Groq API key.
4. Upload Script to Colab -

   Option 1: Copy and paste your 'agent_feedback_response.py' content into a Colab cell and run it.
   
   Option 2: Upload your `.py` file directly:

   from google.colab import file
   files.upload()  # Select your agent_feedback_response.py file

   Then run:
   
   !python agent_feedback_response.py

5. Run Example Review Response Generation- Once the script is loaded and API key is set, you can test it:

review = "The food was great but the service was a bit slow."

sentiment = get_sentiment(review)

response = generate_response(review, sentiment)

print(f"Sentiment: {sentiment}")

print(f"Response: {response}")

6. Expected Output
   
Example,

Sentiment: negative

Response: 

"Dear valued customer,
Thank you for taking the time to share your feedback about your recent visit to our restaurant. We're thrilled to hear that you enjoyed the food, and we appreciate your kind words. However, we apologize that the service was slower than expected. We take pride in providing exceptional service, and it's clear we fell short in your case. We'll use your feedback to improve our timing and ensure that all our guests receive the level of service they deserve. We hope to have the opportunity to serve you again and show you a more seamless dining experience.

Best regards,
[Your Restaurant Name]"



Setup & Run Instructions – Agent 2: Sentiment Plotting Agent

1. Open Google Colab - Go to Google Colab and open a new Python notebook.
2. Install Required Libraries - Run this in the first cell:

   !pip install pandas matplotlib

3. Upload the Python Script & CSV File - In Colab, run this to upload your files:

from google.colab import files

Upload agent_sentiment_plot.py,

print("Upload agent_sentiment_plot.py")

files.upload()

Upload Restaurant reviews.csv,

print("Upload Restaurant reviews.csv")

files.upload()

Make sure your CSV file is named exactly: Restaurant reviews.csv

4. Run the Script - After uploading, execute:

   !python agent_sentiment_plot.py

5. Check the Output - The script will save the sentiment trend plot to:
   sentiment_trend.png

   To view it directly in Colab:
   
from IPython.display import Image
Image(filename="sentiment_trend.png")

6. Example Run in Colab - If your dataset contains ratings and timestamps, you might run:

from agent_sentiment_plot import plot_sentiment_trends
plot_sentiment_trends("2019-05-20", "2019-05-26")
