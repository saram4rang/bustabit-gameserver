The social gambling game

https://www.bustabit.com

Host: GitHub

Language: JavaScript

This installation guide is only suitable to set up bustabit for development and testing.
Additional steps are necessary for a production-ready bustabit.

1. Install Dependencies
If bustabit-depositor is used, bitcoind must be installed and running.

sudo apt-get install git postgresql postgresql-9.4-plv8 nodejs-legacy npm

2. Clone Source
git clone https://github.com/moneypot/bustabit-webserver.git
git clone https://github.com/moneypot/bustabit-gameserver.git
git clone https://github.com/moneypot/bustabit-depositor.git
bustabit-depositor is only needed if payments are to be accepted and may be omitted otherwise.

Run npm install once from within each project directory to install all required npm modules.

3. Initialise Database
sudo -u postgres createuser -P bustabit
sudo -u postgres createdb -O bustabit bustabitdb
sudo -u postgres createlang plv8 bustabitdb
psql -W -U bustabit -d bustabitdb -h localhost -f bustabit-webserver/server/sql/schema.sql


4. Configure and Start Components
All instructions should be followed from within the respective project directories.

bustabit-webserver
Set the database URI, replacing <PASSWORD> with the one you chose in step 3.

export DATABASE_URL=postgres://bustabit:<PASSWORD>@localhost/bustabitdb
Set an extended public key as defined by BIP 32 (starts with xpub).
All deposit addresses will be derived from this key:

export BIP32_DERIVED_KEY=xpub…
By default, bustabit listens for HTTP requests on port 3841.

Optionally, a different port may be specified, for example:
export PORT=8000

Finally, start the server:
npm start

bustabit-gameserver Generate a hashchain (see this forum post for more information on bustabit's probably fair scheme):
node populate_hashes.js

Set the same database URI as in the previous step and start the server:
export DATABASE_URL=postgres://bustabit:<PASSWORD>@localhost/bustabitdb
npm start

bustabit-depositor
Edit the variables in the env file to suit your needs:

BIP32_DERIVED_KEY An extended public key. This should be the same key used in the bustabit-webserver section above.
GENERATE_ADDRESSES Number of addresses to generate and watch. This number should be greater than the number of your users.
BITCOIND_HOST The address at which your bitcoind instance is listening at
BITCOIND_USER and BITCOIND_PASS The RPC credentials of your bitcoind instance.
These should be identical to the credentials defined in bitcoind's configuration file.
Finally, start the depositor in the background with npm start or in the foreground using npm run start-dev.

Dependencies
 package.json	Kind	Requirements	Latest Stable	Latest Release	Licenses	
CBuffer	runtime	^1.1.0	2.0.0	2.0.0	MIT	
almond	development	^0.3.1	0.3.3	0.3.3	MIT	
async	runtime	^1.4.0	2.6.0	2.6.0	MIT	
async-cache	runtime	^1.0.0	1.1.0	1.1.0	ISC	
autolinker	development	^0.18.1	1.6.2	1.6.2	MIT	
better-assert	runtime	^1.0.0	1.0.2	1.0.2	MIT	
bitcoin	runtime	^2.4.0	3.0.1	3.0.1	Unlicense	
bitcoinjs-lib	runtime	^2.0.0	3.3.2	3.3.2	MIT	
body-parser	runtime	~1.3.1	1.18.2	1.18.2	MIT	
chance	development	^0.7.7	1.0.16	1.0.16	MIT	
classnames	development	^2.1.2	2.2.5	2.2.5	MIT	
compression	runtime	^1.0.8	1.7.2	1.7.2	MIT	
cookie-parser	runtime	^1.3.2	1.4.3	1.4.3	MIT	
crypto-js	runtime	~3.1.2-5	3.1.9	3.1.9	MIT	
crypto-rand	runtime	0.0.2	0.0.2	0.0.2	MIT	
curlrequest	development	^0.5.2	1.0.1	1.0.1	MIT	
debug	runtime	^2.2.0	3.1.0	3.1.0	MIT	
del	development	^1.2.0	3.0.0	3.0.0	MIT	
dot-emc	runtime	~0.1.2	0.1.2	0.1.2	MIT	
event-stream	development	^3.3.1	3.3.4	3.3.4	MIT	
express	runtime	^4.13.3	4.16.3	5.0.0-alpha.6	MIT	
gulp	development	^3.9.0	4.0.0	4.0.0	MIT	
gulp-extend	development	^0.2.0	0.2.0	0.2.0	MIT	
gulp-hash	development	^2.0.4	4.2.2	4.2.2	MIT	
gulp-minify-css	development	^1.1.5	1.2.4	1.2.4	MIT	
gulp-rename	development	^1.2.2	1.2.2	1.2.2	MIT	
gulp-replace	development	^0.5.3	0.6.1	0.6.1	MIT	
lodash	runtime	^3.10.0	4.17.10	4.17.10	MIT	
merge-stream	development	^0.1.7	1.0.1	1.0.1	MIT	
mousetrap	development	^1.5.2	1.6.1	1.6.1	Apache-2.0	
multiline	runtime	^1.0.2	1.0.2	1.0.2	MIT	
nodemailer	runtime	^1.3.0	4.6.4	4.6.4	MIT	
nodemailer-ses-transport	runtime	^1.2.0	1.5.1	1.5.1	MIT	
password-hash	runtime	^1.2.2	1.2.2	1.2.2	MIT	
pg	runtime	~4.3.0	7.4.1	7.4.1	MIT	
qr-image	runtime	2.0.x	3.2.0	3.2.0	MIT	
react	development	^0.13.3	16.3.2	16.4.0-alpha.0911da3	MIT	
recaptcha-validator	runtime	^1.0.0	2.0.0	2.0.0	MIT	
request	runtime	^2.36.0	2.85.0	2.85.0	Apache-2.0	
requirejs	runtime	~2.1.15	2.3.5	2.3.5	MIT	
run-sequence	development	^1.1.0	2.2.1	2.2.1	MIT	
screenfull	development	^2.0.0	3.3.2	3.3.2	MIT	
seedrandom	development	^2.4.0	2.4.3	2.4.3	MIT	
socket.io	runtime	^1.3.6	2.1.0	2.1.0	MIT	
socket.io-client	development	^1.3.5	2.1.0	2.1.0	MIT	
socket.io-cookie	runtime	0.0.1	0.0.1	0.0.1	MIT	
speakeasy	runtime	1.0.x	2.0.0	2.0.0	MIT	
timeago	runtime	^0.1.0	1.6.3	1.6.3	MIT	
uuid	runtime	~1.4.1	3.2.1	3.2.1	MIT	
vinyl-paths	development	^1.0.0	2.1.0	2.1.0	MIT	
Project Statistics
Sourcerank	0
Repository Size	6.79 MB
Stars	22
Forks	46
Watchers	14
Open issues	35
Dependencies	50
Contributors	10
Tags	0
Created	Sep 1, 2014
Last updated	Jun 5, 2017
Last pushed	Dec 18, 2015
Top Contributors See all
Rake Sharm Ryan Havar Eric kungfuant Calvin McAnarney Dobry Den Chris Moore jasidlauskas Dan Foad jlfvr

Interesting Forks See all
bryceweiner/moneypot 
The social gambling game
JavaScript - Other - Last pushed Oct 8, 2014 - 1 stars - 2 forks

 Something wrong with this page? Make a suggestion
