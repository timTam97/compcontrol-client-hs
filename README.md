
# compcontrol-client

This app allows you to remotely control your computer by making web requests.

It's a re-implementation of [Pushbullet Automation](https://github.com/timTam97/pushbullet-automation), written in Haskell and re-engineered for a [custom API](https://github.com/timTam97/compcontrol-api) deployed on AWS. 

## Setup

If you don't have an API key already, visit https://command.timsam.live/getkey to get an API key. Then, create a system environment variable called `WSS_TOKEN` and set its value as your API key.

Then, either download a pre-built [release](https://github.com/timTam97/compcontrol-client-hs/releases) executable or download the source and build with `stack build`.

## Running the client
Simply double click the executable to run the program. The program runs silently, so no console window will pop up. In the folder where you started the program, there should be a text file called `run.log`. Open this file to verify that the program is successfully connected to the deployed API.

## Sending commands

### The easy way
[Here's](https://www.icloud.com/shortcuts/6eb6e0c280ce460381ad95b67aea1aac) a shortcut for your iPhone that will enable you to control your computer from your phone.

### The slightly-less-easy way
The URL to send commands to is `https://command.timsam.live/send/<command>`.
- Replace `<command>` with the command you want to send to the client.
  - ❗ The client will only respond to `sleep`, `shutdown`, `lock` and `hibernate` commands.
- Place your API key in the `auth` part of the header.
- Send a `POST` request.

For example, if you wanted to send a sleep command and your token was `fwolXHYtGMbmAg`:
```
curl -H "auth: fwolXHYtGMbmAg" \
     -X POST https://command.timsam.live/send/sleep
```
The API will return a status code and JSON indicating success or failure.

## Other bits

The program will automatically attempt to reconnect to the API if the connection is disrupted (eg. waking from sleep), so you won't need to start it again every time.

If you want to make the program run when your computer starts up, place a shortcut to the executable in `C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp`.
