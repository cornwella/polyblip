# polyblip
polyblip is a Bottle server for use with Polycom VoIP phones that shows a notification containing the name of the caller. It intercepts XML messages from the phone and extracts call information. Some assembly required.

Thanks to [nicqrocks](https://github.com/nicqrocks) for adding Linux support! Yay Linux.


## What you need
- A Polycom phone configured to send XML packets to your server (tested with Polycom VVX 300 phones)
- Windows or Linux as host OS
- [Bottle](http://bottlepy.org/docs/dev/) for the listening web server
- [Untangle](https://github.com/stchris/untangle) for the XML conversion
- [Wontoncc's `balloontip.py`](https://gist.github.com/wontoncc/1808234) for the notifier (which is included, with a hotfix for repeated message displays)

For most people, this will suffice:

```
python -m pip install untangle bottle
```

## Setup
- You will first need to configure your phone to send messages to your server by enabling the "Incoming Call" telephony event notification on the phone's web portal. We're using Polycom VVX 300 devices; other models may or may not work (though I imagine the web portals and XML response messages are fairly standard).

![phone setup](https://i.imgur.com/c7Nid2r.png)

- Define your receiving computer's IP address and port in the included `ip.conf` file. The syntax for this file is a single line featuring `ip:port` (e.g. `127.0.0.1:1337`). You can use nearly any port you want; Bottle isn't very picky.

- Start your server using `polyblip.py`. If everything worked, you now have a listening Bottle server. Have someone call you, and you'll get their name in a popup bubble. It also logs all received raw XML messages to `call.log`.
