from pyrogram import Client
import asyncio

api_id = 12345678  # عدد واقعی از my.telegram.org
api_hash = "128449750"
bot_token = "AAGDL7zObqTmHma6syht6AGWLpWR-JkV-Q8"
source_channel = "osarebook"  # بدون @
target_channel = "botheadar"  # بدون @
old_tag = "#تگقدیمی"
new_tag = "#تگجدید"

app = Client("my_bot", api_id=api_id, api_hash=api_hash, bot_token=bot_token)

async def forward_and_edit():
    async for message in app.get_chat_history(source_channel, limit=991):
        try:
            if message.text and old_tag in message.text:
                new_text = message.text.replace(old_tag, new_tag)
                await app.send_message(target_channel, new_text)
                await asyncio.sleep(1)  # جلوگیری از FloodWait
            elif message.caption and old_tag in message.caption:
                new_caption = message.caption.replace(old_tag, new_tag)
                await app.copy_message(
                    chat_id=target_channel,
                    from_chat_id=source_channel,
                    message_id=message.message_id,
                    caption=new_caption
                )
                await asyncio.sleep(1)
        except Exception as e:
            print(f"خطا در پیام {message.message_id}: {e}")

async def scheduler():
    await app.start()
    try:
        while True:
            await forward_and_edit()
            await asyncio.sleep(2 * 60 * 60)  # هر ۲ ساعت یک بار
    finally:
        await app.stop()

if __name__ == "__main__":
    asyncio.run(scheduler())
