<h1><b>CyberEdu</b></h1>

<h2>Challenge</h2>

WEB-INTRO (by Lucian Ioan Nitescu)

DESCRIPTION:

Are you an admin?
Note: Access Denied is part of the challenge.
Flag format: CTF{sha256}

TAGS:
- Web
- DefCamp CTF 21-22

<h2><b>Solution</b></h2>

I first analyzed the web application through Chrome DevTools. My first instinct was check the website's requests through the Network tab but I found nothing useful, so I proceeded by checking the cookies used, found in the Application tab. Trying to find what the cookie contains is always a good thing to do in CTF scenarios. I figured it was partially encoded with a base64 algorithm so I used the base64decode.org/base64encode.org tool to find the hidden message. What I found when decoding was "{"logged_in":"False"}" and some characters impossible to read, which hinted me towards a Flask encoding. I first tried to simply change the base64 'False" field to a base64 'True', but nothing changed when I tried changing the cookie. An important tool for this challenge is flask-unsign, usually used in Linux environments. I figured the secret password used when the author encoded the text with the command found in ADDITIONAL INFO command (1), which was "password". The cookie received after using the command found in ADDITIONAL INFO command (2) was the correct cookie that can grant anyone access to the flag/path.



<h2><b>ADDITIONAL INFO</b></h2>

<b>Download flask-unsign</b>

To use the flask-unsigned command, first download a virtual environment (venv) in your terminal if you haven't already:
  python3 -m venv venv

Activate the virtual environment (venv):
  source venv/bin/activate 

Download flask-unsign:
  pip3 install flask-unsign

<b>Commands used</b>

  (1) flask-unsign -w rockyou.txt --unsign --cookie "TOKEN" --no-literal-eval

  (2) flask-unsign --sign --cookie "{'logged_in': 'True'}" --secret "password"
