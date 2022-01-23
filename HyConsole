#!/usr/bin/python3
#Importing on multiple lines per PEP8
import requests
import sys
import time
import psutil
import os
import pytermgui as gui
from pytermgui import WindowManager, Window

# This program will be used to gather data on players from the Hypixel minecraft server via command line
# This program and its creator has 0 affiliation with Hypixel nor the Hypixel server.

#Clearing terminal
os.system('cls;clear')

#Checking if the program was ran via py.exe signifying that it may have been ran from command prompt
#Or pythonw.exe signifying it was ran via Python IDLE which would cause a ton of errors
ppid = os.getppid()
if psutil.Process(ppid).name() == "py.exe":
    print("Program possibly ran via cmd prompt - please note that running from CMD will cause a ton of errors.")
elif psutil.Process(ppid).name() == "pythonw.exe":
    print("Program ran via Python IDLE - this will cause a ton of errors.")
    print("Exitting...")
    exit()

#Obtaining the API + Username from the user
print("Enter your API key:")
apikey = str(input())
print("Enter your username:")
username = str(input())
#bob.
x = "bob"

#Checking if the provided username is valid
validitytest1 = requests.get(url=f"https://api.mojang.com/users/profiles/minecraft/{username}?").json()
try:
    validitytest1 = str(validitytest1["name"])
    if validitytest1 == username:
        print("Valid #1")
except Exception:
    print("Invalid Username!")
    exit()

#Checking if the provided API key is valid
params = { "key": apikey }
validitytest2 = requests.get("https://api.hypixel.net/key", params=params)
if validitytest2.status_code == 403:
    print("Invalid API Key")
    exit()
else:
    print("Valid #2")

#yes.
manager = WindowManager()

#Obtaining player data
playerdata = requests.get(
    url="https://api.hypixel.net/player", params={
        "key": apikey,
        "name": username}).json()
uuid = requests.get(url=f"https://api.mojang.com/users/profiles/minecraft/{username}?").json()
uuid = str(uuid["id"])

#Skyblock Data
skyblockdata = requests.get(
    url="https://api.hypixel.net/skyblock", params={
        "key": apikey,
        "uuid": uuid}).json()

#Leaderboard Data
leaderboarddata = requests.get(
    url="https://api.hypixel.net/leaderboards", params={
        "key": apikey
    }
).json()

#Online Player Count
online = requests.get(
    url="https://api.hypixel.net/status", params={
        "key": apikey,
        "uuid": uuid }
).json()["session"]["online"]

bedwarscoins = playerdata["player"]["stats"]["Bedwars"]["coins"]
bedwarsgames = playerdata["player"]["stats"]["Bedwars"]["games_played_bedwars"]
bedwarskills = playerdata["player"]["stats"]["Bedwars"]["kills_bedwars"]
bedsbroken = playerdata["player"]["stats"]["Bedwars"]["beds_broken_bedwars"]
bedwarswins = playerdata["player"]["stats"]["Bedwars"]["wins_bedwars"]
skywarscoins = playerdata["player"]["stats"]["SkyWars"]["coins"]
skywarswins = playerdata["player"]["stats"]["SkyWars"]["wins"]
skywarskills = playerdata["player"]["stats"]["SkyWars"]["kills"]
skywarsgames = playerdata["player"]["stats"]["SkyWars"]["games"]

# setting up windows that will be opened later
# these here are all of the games for the leaderboards
#online = False ; accidental?
UHC = (
        Window(min_width=50)
        + "UHC Leaderboard Options"
)
SURVIVAL_GAMES = (
        Window(min_width=50)
        + "Survival Games  Leaderboard Options")
QUAKECRAFT = (
        Window(min_width=50)
        + "QuakeCraft Leaderboard Options")
TNTGAMES = (
        Window(min_width=50)
        + "TNT Games Leaderboard Options")
WALLS = (
        Window(min_width=50)
        + "Walls Leaderboard Options")
MURDER_MYSTERY = (
        Window(min_width=50)
        + "Murder Mystery Leaderboard Options")
BUILD_BATTLE = (
        Window(min_width=50)
        + "Build Battle Leaderboard Options")
ARCADE = (
        Window(min_width=50)
        + "Arcade Leaderboard Options")
BEDWARS = (
        Window(min_width=50)
        + "BedWars Leaderboard Options")
DUELS = (
        Window(min_width=50)
        + "Duels Leaderboard Options")
ARENA = (
        Window(min_width=50)
        + "Arena Leaderboard Options")
SPEED_UHC = (
        Window(min_width=50)
        + "Speed UHC Leaderboard Options")
SKYWARS = (
        Window(min_width=50)
        + "SkyWars Leaderboard Options")

# sorry for the length but I couldn't think of a better way to do this part
LeaderboardMenu = (
        Window(min_width=50)
        + "Use this menu to navigate Leaderboards"
        + ["UHC", lambda *_: manager.add(UHC.copy().center())]
        + ["Survival Games", lambda *_: manager.add(UHC.copy().center())]
        + ["QuakeCraft", lambda *_: manager.add(SURVIVAL_GAMES.copy().center())]
        + ["TNT Games", lambda *_: manager.add(TNTGAMES.copy().center())]
        + ["Walls", lambda *_: manager.add(WALLS.copy().center())]
        + ["Murder Mystery", lambda *_: manager.add(MURDER_MYSTERY.copy().center())]
        + ["Build Battle", lambda *_: manager.add(BUILD_BATTLE.copy().center())]
        + ["Arcade", lambda *_: manager.add(ARCADE.copy().center())]
        + ["BedWars", lambda *_: manager.add(BEDWARS.copy().center())]
        + ["Duels", lambda *_: manager.add(DUELS.copy().center())]
        + ["Arena", lambda *_: manager.add(ARENA.copy().center())]
        + ["Speed UHC", lambda *_: manager.add(SPEED_UHC.copy().center())]
        + ["SkyWars", lambda *_: manager.add(SKYWARS.copy().center())]
        + ["Exit", lambda *_: sys.exit(0)]
)

BedWars = (
        Window(min_width=50)
        + "Coins:"
        + f"{str(bedwarscoins)}"
        + "Kills:"
        + f"{str(bedwarskills)}"
        + "Wins:"
        + f"{str(bedwarswins)}"
        + "Games Played:"
        + f"{str(bedwarsgames)}"
        + "Beds Broken:"
        + f"{str(bedsbroken)}")
SkyWars = (Window(min_width=50)
           + "Coins:"
           + f"{str(skywarscoins)}"
           + "Kills:"
           + f"{str(skywarskills)}"
           + "Wins:"
           + f"{str(skywarswins)}"
           + "Games Played:"
           + f"{str(skywarsgames)}")

ProfileMenu = (
        Window(min_width=50)
        + "Gamemodes Menu"
        + ""
        + ["BedWars", lambda *_: manager.add(BedWars.copy().center())]
        + ["SkyWars", lambda *_: manager.add(SkyWars.copy().center())]
        + ["Exit", lambda *_: sys.exit(0)]
)

pets = (Window(min_width=50))
coins = (Window(min_width=50))
FarmingS = (Window(min_width=50))
MiningS = (Window(min_width=50))
CombatS = (Window(min_width=50))
ForagingS = (Window(min_width=50))
FishingS = (Window(min_width=50))
EnchantingS = (Window(min_width=50))
AlchemyS = (Window(min_width=50))
TamingS = (Window(min_width=50))
DungeonS = (Window(min_width=50))

skills = (
        Window(min_width=50)
        + ["Farming", lambda *_: manager.add(FarmingS.copy().center())]
        + ["Mining", lambda *_: manager.add(MiningS.copy().center())]
        + ["Combat", lambda *_: manager.add(CombatS.copy().center())]
        + ["Fishing", lambda *_: manager.add(FishingS.copy().center())]
        + ["Alchemy", lambda *_: manager.add(AlchemyS.copy().center())]
)

FarmingC = (Window(min_width=50))
MiningC = (Window(min_width=50))
CombatC = (Window(min_width=50))
ForagingC = (Window(min_width=50))
FishingC = (Window(min_width=50))
BossC = (Window(min_width=50))

collections = (Window(min_width=50))

SkyblockMenu = (
        Window(min_width=50)
        + "Skyblocks Profile Menu"
        + ""
        + gui.InputField(prompt="What profile do you wish to view?")
        + ["Exit", lambda *_: sys.exit(0)]
)
Mainmenu = (
        Window(min_width=50)
        + "Welcome to HyConsole"
        + ""
        + f"You are currently viewing the profile of: {username}"
        + ""
        + f"Online: {online}"
        + ""
        + ["Profile", lambda *_: manager.add(ProfileMenu.copy().center())]
        + ["Leaderboard", lambda *_: manager.add(LeaderboardMenu.copy().center())]
        + ["Skyblock", lambda *_: manager.add(SkyblockMenu.copy().center()), lambda *_: mainM.close()]
        + ["Exit", lambda *_: sys.exit(0)]
)
# starting the window
mainM = manager.add(Mainmenu)
manager.run()
