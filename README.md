# cpanel-emails

This script retrieves & prints a list of all the email addresses created in a cPanel server. The list consists of lines formatted as: owner,user,email.

## Requirements

* [Node.js](http://nodejs.org/)
* [cPanel API2](http://docs.cpanel.net/twiki/bin/view/SoftwareDevelopmentKit/ApiIntroduction#API2)
* [A Remote Acces Key](http://docs.cpanel.net/twiki/bin/view/AllDocumentation/WHMDocs/RemoteAccess)

## Installation & configuration

Clone this project and install the package:

```
git clone git@github.com:luissquall/whm-emails.git
cd whm-emails
npm install
```
Copy config. template and set program settings:
```
cp config.json.default config.json
vim config.json
```


## Execution

Let it be:

```
chmod u+x cli.js
./cli.js
# Save the list in a file
./cli.js > emails.csv
```

### Settings

* `api`: URL of the WHM address of your server. **Requires trailing slash!**. E.g. https://server.monkey.com:2087/
* `credentials.hash`: Server's remote access key

## How does it work?

The program requests [a list of all the accounts](https://documentation.cpanel.net/display/SDK/WHM+API+1+Functions+-+listaccts) in the server, extracts the users from the list and issues a new request per user to [Email::Alistpopswithdisk](https://documentation.cpanel.net/display/DD/cPanel+API+2+Functions+-+Email%3A%3Alistpopswithdisk) to obtain all email accounts from the user's account including their each email account's disk usage in human readable format.

