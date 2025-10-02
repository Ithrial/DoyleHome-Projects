This N8N agent was a succesful attempt to recreate what I was using Open-AIs Tasks or 
Perplexity's Tasks to do for me. Basically I wanted to have a quick news report
give me what was going on in the news every few days. However, to avoid repetitve news stories
I limited the agent to only fild stories SINCE the last time the agent ran, which was every 3 days.

<img width="1617" height="1213" alt="image" src="https://github.com/user-attachments/assets/3c3cb8d2-e565-428d-8b95-1e57b1fa4574" />


So every 3 days at 6am, I'd get an email some of the latest AI stories. BUT more importantly was the formatting.
The email was formatted in the following way:

1) Story Title 
2) Clickable Link - So I could reat the whole story
3) Summary of the Link - So I could decide if I wanted to read the whole story or not
4) Why it was important in the world of AI 
5) WHy it was important to me in my local AI endevors

#5 was important because thats how I discovered Qwen for the first time and when GPT-OSS was launched. 

However, now that my local AI is good enough (for me) where I dont pay for any AI services, I started missing my emails. 

So this Latest AI News Agent, but really could be any information gathering agent uses

1) Cron Schedule - currently runs every 72 hours
2) AI Agent that leverages:
    A) Ollama (GPT-OSS:20B but can be any model)
    B) Simple Memory (didnt feel the need to use my postgres for this)
    C) Local instance of SearXNG - ensure you have JSON as described in the Node docs
    D) Jina AI - Free APi for scraping single URLs
    E) SMTP Email - Using Googles Application Password

AI agent gets the following prompt:

Find the top 10 latest AI news stories since $today. 

Use Searxng to get those URLS then use Jina AI to get the data. 

When you have the best stories,  use the send the email tool to send an email to ithrial@gmail.com with the 
subject "Latest AI News since $today" . Organize the contents in memory in the following structure:

“Story Title”
Provide the Clickable Link to the story
Summary of the Article/Story
“Provide insight as to Why its important to the world of AI”
“Provide insight as to Why its important to me in my local AI endeavors”

Then it goes - gets top 10 URLs, stores in memory, uses Jina AI to scrap the URLs, stores the title, whole store and the summary in memory and then create the email. 
I leveraged the option for letting the model (in the SMTP node) to decide what the Title of the email is and the body, both defined in the original prompt. 

Temp is .6
Context Window is 132K (just incase some of the articles or white papers are long)
Max Token is 8k to ensure enough summary run way.
Model size during execution takes up about 16GB of vRAM 

This is the first time sharing anything like this so I hope people find value in it. I would have shared in the n8n cloud but I dont pay for the account - just host locally.
JSON file has the spots where you should drop in your own email, credentials for SEARXNG, OLLAMA and Jina AI

