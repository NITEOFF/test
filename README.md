prefix = "." # Префикс бота
bot_token = "MTAyMzkxNDE2MDcxNjc5MTg3OA.GJy_Y1._hbNkeyi2onLPIxGPmS88Bbrq_6hprY5569El" # Токен
channel_id = "1023915747182923786"
roles = ["Hafnarfjörður:1023930150603202580:hafnafj:1023920359017304115","Hátegsvegur:1023930150603202580:hategs:1023928327662227456","Skólavörðuholt:1023930150603202580:skolavordu:1023929424166522940"]
 
import discord
from discord.ext import commands
 
prefix = prefix
token = bot_token
 
bot = commands.Bot(command_prefix=prefix, intents=discord.Intents.all())
 
bot.setup = False
 
@bot.event
async def on_ready():
    Channel = bot.get_channel(channel_id)
    text= "Pick reaction"
    Moji = await Channel.send(text)
    for role in roles:
        await Moji.add_reaction(role.split(":")[2])
@bot.event
async def on_reaction_add(reaction, user):
    for role in roles:
        splittedReactions = role.split(":")
 
        rolename = splittedReactions[0]
        msgid = splittedReactions[1]
        emoji = splittedReactions[2]
 
        Channel = bot.get_channel(channel_id)
 
        if reaction.message.channel.id != Channel.id:
            return
        if reaction.emoji == emoji or reaction.message.id == msgid:
            Role = discord.utils.get(user.guild.roles, name=rolename)
            await user.add_roles(Role)
 
 
@bot.event
async def on_reaction_remove(reaction, user):
    for role in roles:
        splittedReactions = role.split(":")
 
        rolename = splittedReactions[0]
        msgid = splittedReactions[1]
        emoji = splittedReactions[2]
 
        Channel = bot.get_channel(channel_id)
 
        if reaction.message.channel.id != Channel.id:
            return
        if reaction.emoji == emoji or reaction.message.id == msgid:
            Role = discord.utils.get(user.guild.roles, name=rolename)
            await user.remove_roles(Role)
bot.run(token)
