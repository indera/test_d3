
Learning d3
==

http://bost.ocks.org/mike/bubble-map/


Install Node.js
==

sudo apt-get install build-essential openssl libssl-dev
git clone https://github.com/joyent/node.git
cd node
git fetch --tags
git checkout v0.8.28
./configure --openssl-libpath=/usr/lib/ssl
make
make test
sudo make install
node -v 

sudo npm install -g http-server
sudo npm install -g nodemon
sudo npm install -g mysql
sudo npm install -g gistup

---
assert.js:102
  throw new assert.AssertionError(

AssertionError: agent3 rejected, but should NOT have been
    at ChildProcess.<anonymous> (/home/vagrant/git/test_d3/node/test/simple/test-tls-server-verify.js:217:14)
    at ChildProcess.EventEmitter.emit (events.js:99:17)
    at Process._handle.onexit (child_process.js:686:10)
Command: out/Release/node /home/vagrant/git/test_d3/node/test/simple/test-tls-server-verify.js
---


Create simple page
==
mdir hello
vim index.html

------
<!DOCTYPE html>
<meta charset="utf-8">
Hello, world!
-----

http-server &
[1] 28876
vagrant@debian-70rc1-x64-vbox4210:~/git/test_d3/hello$ Starting up http-server, serving ./ on port: 8080
Hit CTRL-C to stop the server




Getting Data
==

 List of APIs
	http://www.nlm.nih.gov/api/
	http://www.programmableweb.com/apis/directory
	http://library.stmarytx.edu/acadlib/doc/electronic/dbhealth.htm

 Economic data:
	http://www.bea.gov/API/signup/index.cfm
	http://www.bea.gov/api/_pdf/bea_web_service_api_user_guide.pdf

 HIV Drugs database:
	http://aidsinfo.nih.gov/api/drugs/
	http://aidsinfo.nih.gov/api/drugs/306
