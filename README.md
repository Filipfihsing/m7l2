# m7l2
main.py

import discord
from discord.ext import commands
import os, random
from model import ger_class
intents = discord.Intents.default()
intents.message_content = True

bot = commands.Bot(command_prefix='$', intents=intents)

@bot.event
async def on_ready():
    print(f'Zalogowaliśmy się jako {bot.user}')

@bot.command()
async def hello(ctx):
    await ctx.send(f'Cześć! Jestem botem, {bot.user}!')

@bot.command()
async def heh(ctx, count_heh = 5):
    await ctx.send("he" * count_heh)



@bot.command()
async def check(ctx):
    if ctx.message.attachments:
        for attachment in ctx.message.attachments:
            file_name = attachment.filename
            await attachment.save(f'./{file_name}')
            image = Image.open(f'./{file_name}')
            await ctx.sent(ger_class{image, "labels.txt", "keras_model.h5"})
    else:
        await ctx.send("Nie załączyłeś żadnego pliku!")

bot.run("token")

model.py
import tf_keras as keras  # Importowanie tf-keras – wersja Keras kompatybilna z modelami .h5 
from tf_keras.models import load_model  # Importowanie funkcji load_model z tf_keras, która pomaga nam z otwarciem modelu
from PIL import Image, ImageOps  # Instalowanie pillow zamiast PIL
import numpy as np

import PIL.Image

def ger_class(model, labels):
  np.set_printoptions(suppress=True)

  model = load_model(model, compile=False)
  class_names = open(labels, "r").readlines()
  image = image.convert("RGB")

  data = np.ndarray(shape=(1, 224, 224, 3), dtype=np.float32)
  size = (224, 224)
  image = ImageOps.fit(image, size, Image.Resampling.LANCZOS)
  image_array = np.asarray(image)
  normalized_image_array = (image_array.astype(np.float32) / 127.5) - 1
  data[0] = normalized_image_array


  prediction = model.predict(data)
  index = np.argmax(prediction)
  class_name = class_names[index]
  confidence_score = prediction[0][index]

  return class_name[2:].strip()

image = 
print(ger_class{image, "labels.txt", "keras_model.h5"})





biblioteki
