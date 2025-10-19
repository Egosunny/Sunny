# async era starts here 
import asyncio
import logging
import random
import os
from pyfiglet import figlet_format
from cfonts import render
from urllib.parse import unquote
from playwright.async_api import async_playwright
#from fake_useragent import UserAgent


#ua = UserAgent()
#user_agent = ua.random
#print("User-Agent being used:", user_agent)

# 🎨 Terminal colors
# config.py
COLORS = {
    'red': '\033[1;31m',
    'green': '\033[1;32m',
    'yellow': '\033[1;33m',
     'cyan': '\033[36m',
    'blue': '\033[1;34m',
    'reset': '\033[0m',
    'gold': '\x1b[38;5;220m',
    'bold': '\033[1m',
}

background_colors = {
    'black'     : '\033[40m',
    'red'       : '\033[41m',
    'green'     : '\033[42m',
    'yellow'    : '\033[43m',
    'blue'      : '\033[44m',
    'magenta'   : '\033[45m',
    'cyan'      : '\033[46m',
    'white'     : '\033[47m'
}

background_256 = {
    'bright_magenta' : '\033[48;5;201m',
    'bright_blue'    : '\033[48;5;117m',
    'bright_green'   : '\033[48;5;82m',
    'bright_yellow'  : '\033[48;5;226m',
    'bright_cyan'    : '\033[48;5;87m',
    'bright_red'     : '\033[08;5;196m',
    'gray'           : '\033[48;5;244m',
    'orange'         : '\033[48;5;208m',
    'purple'         : '\033[48;5;93m'
}

def lago():
    print(render("• CSNV •", colors=["red", "white"]))
def logo():
    print(render("• GAME OVER •", colors=["red", "white"]))

def banner():
    os.system("cls" if os.name == "nt" else "clear")
    print(render("• CSNV •", colors=["red", "blue"]))
    print(COLORS['blue'] + "Instagram automation NC " + COLORS['reset'])
    print(COLORS['yellow'] + "Created by BANE." + COLORS['reset'])
    print(COLORS['red'] + "Version: v13-testing" + COLORS['reset'])
    print(COLORS['green']+COLORS['bold']+ "also known as\033[0m  "+background_256["bright_red"]+"the RDP killer" + COLORS['reset'])  
    print(background_256['bright_cyan'] + "ASYNC version" + COLORS['reset'])
   # print(render("• CSNV •", colors=["red", "blue"]))

# Logging
logging.basicConfig(level=logging.INFO, format='%(asctime)s - %(message)s')


# Emoji bases
try:
    with open("ufo_bases.txt", "r", encoding="utf-8") as f:
        ufo_bases = [line.strip() for line in f if line.strip()]
except Exception:
    ufo_bases = [
"xns   𝗞𝗔𝗖𝗛𝗥𝗘 𝗪𝗔𝗟𝗘 ", "xns   𝗚𝗨𝗟𝗔𝗠", "xns   𝗞𝗨𝗧𝗧𝗘", "xns  𝗕𝗛𝗔𝗚 𝗠𝗔𝗔𝗧 ", "xns  𝗧𝗠𝗞𝗖", "xns  𝗖𝗛𝗔𝗞𝗞𝗘",
    "xns  𝗟𝗔𝗡𝗗 𝗞𝗛𝗔 𝗚𝗔𝗬𝗔", "xns  𝗦𝗨𝗣𝗣𝗢𝗥𝗧 𝗟𝗔 ", "xns  𝗕𝗛𝗔𝗚𝗢𝗗𝗘", "xns  𝗛𝗔𝗚 𝗗𝗜𝗬𝗔", "xns  𝗧𝗠𝗞𝗕", "xns  𝗕𝗜𝗛𝗔𝗥𝗜", "xns  𝗣𝗬 𝗟𝗔𝗚𝗔𝗡𝗔 𝗦𝗜𝗞𝗛𝗔𝗨  ", "xns  𝗝𝗛𝗔𝗧𝗨"
"xns  𝗥𝗔𝗡𝗗𝗜 𝗞𝗘 ", "xns   𝗖𝗛𝗧𝗠𝗥𝗘", "xns   𝗧𝗠𝗥", "xns  𝗔𝗧𝗠𝗞𝗕𝗙𝗝 🥀 ", "xns  𝗧𝗠𝗞𝗰 𝗺𝗲 𝗽𝗼𝗸𝗲𝗺𝗼𝗻", "xns  𝗵𝗶𝘇𝗱𝗲",
    "xns  𝗿𝗻𝗱𝗶 𝗸𝗲 𝗽𝗶𝗹𝗹𝗲", "xns  𝗡𝗖 𝗟𝗔𝗚𝗔𝗬𝗘𝗚𝗔? ", "xns  𝗖𝗛𝗨𝗗", "xns 𝗸𝗲 𝗯𝗵𝗼𝘀𝗱𝗶 𝗰𝗵𝗶𝗹 𝗷𝗮𝘆𝗲", "xns  𝗧𝗠𝗞𝗕", "xns  𝗕𝗡𝗘𝗣𝗔𝗟𝗜", "xns  𝗦𝗔𝗣𝗥𝗜  ", "xns  𝗕𝗛𝗘𝗡 𝗞𝗔 𝗦𝗢𝗧"
"xns  𝗖𝗢𝗩𝗘𝗥 𝗕𝗨𝗟𝗔", "xns   𝗚𝗨𝗟𝗔𝗠", "xns   𝗕𝗜𝗧𝗖𝗛", "xns  𝗜𝗗𝗛𝗔𝗥 𝗖𝗛𝗨𝗗 ", "xns 𝗕𝗔𝗔𝗣 𝗞𝗢 𝗕𝗛𝗨𝗟 𝗠𝗔𝗧", "xns  𝗚𝗕 𝗥𝗢𝗔𝗗 𝗪𝗔𝗟𝗘",
    "xns  𝗟𝗔𝗡𝗗 𝗟𝗘𝗟𝗘", "xns  𝗦𝗨𝗣𝗣𝗢𝗥𝗧 𝗖𝗛𝗨𝗗𝗔 ", "xns  𝗰𝗵𝘂𝗱 𝗸𝗲 𝗱𝗮𝗳𝗮𝗻", "𝗮𝗯𝗲 𝗻𝗰 𝗸𝘆𝗮 𝗱𝗲𝗸𝗵 𝗿𝗵𝗮 𝗵𝗮𝗶", "xns  𝗧𝗠𝗞𝗟", "xns  𝗞𝗜 𝗕𝗘𝗛𝗘𝗡 𝗖𝗛𝗨𝗗","xns  𝗦𝗨𝗣𝗣𝗢𝗥𝗧 𝗗𝗨  ", "xns  𝗿𝗻𝗱𝗶"
"xns  𝗞𝗔𝗖𝗛𝗥𝗘 𝗪𝗔𝗟𝗘 ", "xns   𝗚𝗨𝗟𝗔𝗠", "xns   𝗞𝗨𝗧𝘁𝗶", "xns  𝗕𝗛𝗔𝗚 𝗠𝗔𝗔𝗧 ", "xns  𝗧𝗠𝗞𝗖", "xns  𝗖𝗛𝗔𝗞𝗞𝗘",
    "xns  𝗟𝗔𝗡𝗗 𝗞𝗛𝗔 𝗚𝗔𝗬𝗔", "xns  𝗦𝗨𝗣𝗣𝗢𝗥𝗧 𝗟𝗔 ", "xns  𝗕𝗛𝗔𝗚𝗢𝗗𝗘", "xns  𝗛𝗔𝗚 𝗗𝗜�𝗔", "xns  𝗧𝗠𝗞𝗕", "xns  𝗕𝗜𝗛𝗔𝗥𝗜", "xns  𝗣𝗬 𝗟𝗔𝗚𝗔𝗡𝗔 𝗦𝗜𝗞𝗛𝗔𝗨  ", "xns  𝗝𝗛𝗔𝗧𝗨"]
emoji_suffixes = ["🥀", "🤙🏿", "🖖🏿", "🤟🏿", "🔥", "💥", "🚀", "👾" ,"🤘", "🤙", "👎", "👌", "✋", "🖐️", "✊", "👊", "🤛", "🤜", "🤚", "👋", "🫶", "🙌", "👐", "✍️", "🤟", "🤲", "🙏", "💅", "💅", "🩷", "🧡", "💛", "💚", "💔", "❤️", "🔥", "❤️", "🩹", "❣️", "💕", "💞", "💟", "💝", "💘", "💖", "💓", "💗", "💌", "💢", "💥", "💤", "💦", "💨", "🕉️", "☪️", "✝️", "☮️", "🕳️", "💫", "☸️", "✡️", "🔯", "🪯", "🕎", "☯️", "☦️", "🛐", "⛎", "♈", "♉", "♊", "♐", "♏", "♎", "♍", "♌", "♋", "♑", "♒", "🆔", "⚕️", "♾️", "🈸", "🈚", "🈶", "🈹", "🈳", "⚛️", "🈺", "🈷️", "✴️", "🉑", "💮", "🪷", "🉐", "🈴", "🈵", "🆑", "🆎", "🅱️", "🅰️", "🚼", "🈲", "🅾️", "⛔", "🆘", "🛑", "📛", "❌", "⭕", "🚫", "🔇", "🔕", "🚭", "🚷", "❗", "📵", "🔞", "🚱", "🚳", "🚯", "❕", "❓", "❔", "‼️", "⁉️", "💯", "☢️", "〽️", "⚜️", "🔱", "🔆", "🔅", "☣️", "⚠️", "🚸", "🔰", "♻️", "🈯", "💠", "✅", "✳️", "❇️", " 💹", "🌐", "➿", "🛂", "🛃", "🛅", "♿", "🚾", "🅿️", "🚰", "🛜", "📶", "🚮", "🚻", "🚺", "🚺", "🚹", "🕧", "🕦", "🕥", "🕤", "🕣", "🕢", "🕡", "🕠", "🕟", "🕞", "🕝", "🕜", "🕛", "🕚", "🕙", "🕘", "🕗", "🕖", "🕕", "🕔", "🕓", "🕒"] 
used_names = set()
success_count = 0
fail_count = 0
lock = asyncio.Lock()

# Inputs
banner()
session_id = input("Session ID: ").strip() or unquote('3107219309%3A0uz8l9n6AMy2DH%3A2%3AAYfuagxBg_elL3mXJhaoF2P3E89xk2Cq3E0PVwSJKw')
dm_url = input("Group chat URL: ").strip() or 'https://www.instagram.com/direct/t/23884311841232254/'
try:
    task_count = int(input("Number of async tasks: ").strip())
except:
    task_count = 5

def generate_name():  
        base = random.choice(ufo_bases)
        emoji = random.choice(emoji_suffixes)
        name = f"{base}_{emoji}"
        return name

async def rename_loop(context):
    global success_count, fail_count
    page = await context.new_page()
    try:
        await page.goto(dm_url, wait_until='domcontentloaded', timeout=600000)
        gear = page.locator('svg[aria-label="Conversation information"]')
        await gear.wait_for(timeout=160000)
        await gear.click()
        await asyncio.sleep(1)
    except Exception as e:
        logging.error(f"Page init failed: {e}")
        return

    change_btn = page.locator('div[aria-label="Change group name"][role="button"]')
    group_input = page.locator('input[aria-label="Group name"][name="change-group-name"]')
    save_btn = page.locator('div[role="button"]:has-text("Save")')

    while True:
        try:
            name = generate_name()
            await change_btn.click()
            await group_input.click(click_count=3)
            await group_input.fill(name)

            disabled = await save_btn.get_attribute("aria-disabled")
            if disabled == "true":
                async with lock:
                    fail_count += 1
                continue

            await save_btn.click()
            async with lock:
                success_count += 1

            await asyncio.sleep(0.05)

        except Exception:
            async with lock:
                fail_count += 1
            await asyncio.sleep(0.1)

async def live_stats():
    while True:
        async with lock:
            
            #print(f"\033[1;33mSession ID: {session_id}\033[0m")
            print(f"\033[1;34mDM URL: {dm_url}\033[0m")
            print(f"\033[1;35mTasks: {task_count}\033[0m")
            print(f"\033[1;36mUsed Names: {len(used_names)}\033[0m")
            print(f"\033[1;37mTotal Attempts: {success_count + fail_count}\033[0m")
            print(f"\033[42m✅ Success: {success_count}\033[0m  \033[41m❌ Failed: {fail_count}\033[0m", end="\r")
        await asyncio.sleep(0.5)
        os.system("cls" if os.name == "nt" else "clear")

async def main():
    async with async_playwright() as p:
        browser = await p.chromium.launch(headless=True, args=['--no-sandbox', '--disable-gpu', '--disable-dev-shm-usage'])

        context = await browser.new_context(
           # user_agent=user_agent,
            locale="en-US",
            extra_http_headers={"Referer": "https://www.instagram.com/"},
            viewport=None
        )
        await context.add_cookies([{
            "name": "sessionid",
            "value": session_id,
            "domain": ".instagram.com",
            "path": "/",
            "httpOnly": True,
            "secure": True,
            "sameSite": "None"
        }])

        tasks = [asyncio.create_task(rename_loop(context)) for _ in range(task_count)]
        tasks.append(asyncio.create_task(live_stats()))

        try:
            await asyncio.gather(*tasks)
        except KeyboardInterrupt:
            print("\n👋 Done.")
            logo()
        finally:
            await browser.close()

if __name__ == "__main__":
    
    asyncio.run(main())
