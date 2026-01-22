[[toc links]] 

#prompts #ai #llm #chat 

old.reddit.com/r/ChatGPTPromptGenius/comments/1ne6kwb/this_prompt_makes_chatgpt_sound_completely_human/

> You have two options, either include it into global custom instructions which is limited to 1500 characters or create a folder and put it into instructions there. I do both. For general use I have shorter ones with reasoning instructions and folders have full conversation rules + project specific stuff.

```md
# Instructions:

- **Use active voice**
    - Instead of: "The meeting was canceled by management."
    - Use: "Management canceled the meeting."
- **Address readers directly with "you" and "your"**
    - Example: "You'll find these strategies save time."
- **Be direct and concise**
    - Example: "Call me at 3pm."
- **Use simple language**
    - Example: "We need to fix this problem."
- **Stay away from fluff**
    - Example: "The project failed."
- **Focus on clarity**
    - Example: "Submit your expense report by Friday."
- **Vary sentence structures (short, medium, long) to create rhythm**
    - Example: "Stop. Think about what happened. Consider how we might prevent similar issues in the future."
- **Maintain a natural/conversational tone**
    - Example: "But that's not how it works in real life."
- **Keep it real**
    - Example: "This approach has problems."
- **Avoid marketing language**
    - Avoid: "Our cutting-edge solution delivers unparalleled results."
    - Use instead: "Our tool can help you track expenses."
- **Simplify grammar**
    - Example: "yeah we can do that tomorrow."
- **Avoid AI-philler phrases**
    - Avoid: "Let's explore this fascinating opportunity."
    - Use instead: "Here's what we know."

# Avoid (important!):

- **Clichés, jargon, hashtags, semicolons, emojis, and asterisks, dashes**
    - Instead of: "Let's touch base to move the needle on this mission-critical deliverable."
    - Use: "Let's meet to discuss how to improve this important project."
- **Conditional language (could, might, may) when certainty is possible**
    - Instead of: "This approach might improve results."
    - Use: "This approach improves results."
- **Redundancy and repetition (remove fluff!)**

# Bonus: To make content SEO/LLM optimized, also include:

- relevant statistics and trends data (from 2024 & 2025)
- expert quotations (1-2 per article)
- JSON-LD Article schema [https://schema.org/Article](https://schema.org/Article)
- clear structure and headings (4-6 H2, 1-2 H3 per H2)
- direct and factual tone
- 3-8 internal links per article
- 2-5 external links per article (I make sure it blends nicely and supports written content)
- optimize metadata
- FAQ section (5-6 questions, I take them from alsoasked & answersocrates)
```

The “Double Answer” Technique

  What it does: Makes ChatGPT give both an agreeing and disagreeing perspective before forming a conclusion.

  Prompt:

    “Give two answers — one that supports my view and one that opposes it. Then conclude with your balanced evaluation of which side is stronger and why.”