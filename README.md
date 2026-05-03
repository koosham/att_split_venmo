Vibe coded (Claude Sonnet 4.6) web-based phone app that reads an AT&T bill in PDF format, parses it, and creates Venmo requests for each person.

## Requirements
- Venmo app to be installed on the device
- [Optional] [Dropbox app key](https://www.dropbox.com/developers/apps)

## Usage
From your phone, go to https://koosham.github.io/att_split_venmo and use the app.

## ATT Integration
AT&T does not have a free API for personal use. I just gave up integrating my tool with their app/web-app. So there is no integration. You download the bill as a PDF and feed it to this app.

## Venmo Integration
The tool creates `venmo://` URLs to take you to the Venmo app where you need to tap a couple of buttons. This is very manual. The alternative is to use Venmo's undocumented API, but it comes
with issues like Venmo's strict SOP enforcement and API instability.

## Configuration
All data is stored in [localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage) of client's browser. It's pretty safe and secure. The data includes phone numbers,
Venmo user IDs, and optionally a Dropbox app key. None of these are secrets, but you still don't want them to be published anywhere. Hence the choice for using browser's cache.

The app supports reading a JSON config file for phone number to Venmo user ID mappings in the following format:

```json
{
  "myPhone": "5555555555",
  "myVenmo": "uncle-sam-venmo",
  "lines": [
    { "phone": "5555556666", "nickname": "Oh Dae-su", "venmo": "you-say-i-pay" },
    ...
  ]
}
```

## Dropbox
I want to keep my bills on my Dropbox, so I decided that I would download the PDF and save it on my Dropbox, then load it into the app directly from Dropbox. You can avoid Dropbox and instead
store the PDF on the phone directly and then open it from your files. If you choose to use Dropbox, you need to [create an app](https://www.dropbox.com/developers/apps) in your Dropbox accout
and give it `files.content.read` access. Then copy and paste the app key into this app.

You also need to specify that the hosting domain of the app can reach to your Dropbox's app. This field is called "Chooser / Saver / Embedder domains". If you decided to use my Github-hosted
page (seriously?), then you need to put `koosham.github.io` in there.
