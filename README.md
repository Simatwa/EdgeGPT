# Bing GPT
ChatGPT with internet access

## Requirements
- A Microsoft Account with early access to http://bing.com/chat
- Microsoft Edge

## Setup
### Checking access
- Install the latest version of Microsoft Edge
- Open http://bing.com/chat
- If you see a chat feature, you are good to go

### Getting authentication
- Open the developer tools (F12)
- Go to the Application tab → Storage → Cookies
- Find the cookie named "_U"
- Copy the value of the cookie
- Method 1
  - `export BING_U="<COOKIE_VALUE>"`
- Method 2
  - Use it as command line argument later

## Installation
- `python3 -m pip install revBingGPT`

## Demo usage
- If `BING_U` in environment variables: `python3 -m BingGPT`
- Else: `python3 -m BingGPT "<COOKIE_VALUE>"`

## Developer
Use Async for the best experience

```python
import asyncio
from BingGPT import Chatbot

async def main():
    """
    Main function
    """
    print("Initializing...")
    bot = Chatbot()
    await bot.start()
    while True:
        prompt = input("\nYou:\n")
        if prompt == "!exit":
            break
        elif prompt == "!help":
            print("""
            !help - Show this help message
            !exit - Exit the program
            !reset - Reset the conversation
            """)
            continue
        elif prompt == "!reset":
            await bot.reset()
            continue
        print("Bot:")
        print((await bot.ask(prompt=prompt))["item"]["messages"][1]["text"])
    await bot.close()


if __name__ == "__main__":
    print(
        """
        BingGPT - A demo of reverse engineering the Bing GPT chatbot
        Repo: github.com/acheong08/BingGPT
        By: Antonio Cheong

        !help for help

        Type !exit to exit
        Enter twice to send message
    """
    )
    asyncio.run(main())


```

## Work in progress
- Response streaming (Easily achievable)
- Error handling