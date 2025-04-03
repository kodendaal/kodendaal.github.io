---
title:  "How I Built a Fun Team Voting App (Without Losing My Mind!)"
mathjax: true
layout: post
categories: 
  = github
  - website
---

<div style="text-align: center;">
  <img src="http://kodendaal.github.io/assets/team_name.png" alt="team name" style="width: 800px; height: auto;">
</div>


## Introduction

Ever struggled to pick a great team name? Turns out, you're not alone! To solve this everyday dilemma—and add a bit of fun to team building—I decided to create a small but interactive voting application. Here's how I went from "I have no idea what I'm doing" to "Wow, this actually works!" without losing my sanity.

---

## The Idea

We needed a creative team name, but every brainstorming session ended in playful chaos. I figured, why not harness this energy into something productive (and fun)? Thus, our little app was born: a place to anonymously submit hilarious or clever team names, and later vote for the very best.

---

## The Tech Stack

I kept things simple yet modern:

- **Python**: The trusty companion for getting stuff done.
- **Gradio**: An amazing tool for quickly building interactive web interfaces without any frontend coding (because who has time for JavaScript?).
- **Google Sheets API**: Because I wanted persistent storage without paying a dime or worrying about servers (yay, free stuff!).
- **Hugging Face Spaces**: A free and straightforward platform for hosting my app without hassle.

---

## The Journey

Initially, things were smooth sailing. Gradio made creating the frontend incredibly easy. With just a few lines of Python, I had interactive tabs for submitting team names, voting, and checking a real-time leaderboard. But then, reality kicked in.

Turns out, Hugging Face Spaces don't keep data forever. My carefully collected votes vanished every time the container restarted—ouch! Enter Google Sheets to the rescue. With a bit of Googling and a lot of friendly ChatGPT help, I securely connected my app to Google Sheets using a service account. Now every submission and vote was safely stored away in the magical cloud, ready to be accessed anytime.


<div style="text-align: center;">
  <img src="http://kodendaal.github.io/assets/naming_workflow.png" style="width: 400px; height: auto;">
</div>

---

## The Security Adventure

Oh, about that "securely connected" part... Initially, I mistakenly uploaded my sensitive service account JSON file to GitHub. Big mistake! Luckily, I quickly pivoted, learned about environment variables (thanks again, ChatGPT!), and securely stored the credentials using Hugging Face’s built-in secrets feature. Crisis averted!

---

## The Result

In the end, the app was a hit. The submissions poured in—ranging from witty acronyms to cheeky puns. And watching the leaderboard update live with colorful charts? Priceless.

Not only did this small project solve our team naming conundrum, but it also reminded us of the joys (and occasional chaos) of building something from scratch.

---

## Lessons Learned

- **Simple beats fancy**: Gradio’s straightforward approach saved countless hours.
- **Free stuff is amazing (but tricky)**: Hugging Face Spaces and Google Sheets API offer incredible value, but you have to manage their quirks.
- **Security first**: Always, always, always store secrets securely.

---


### See It in Action!

- Check out the live app hosted on [Hugging Face Spaces.](https://huggingface.co/spaces/kode24/name_votinG)
- Explore or contribute to the [Github Repository](https://github.com/kodendaal/rag_pdf_visualizer.git) with all the code. 

Now, back to checking the leaderboard again—I think my favorite name just took the lead!

Happy coding!

