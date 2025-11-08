# Gensyn-codeassist-
TUTORIAL: RUNNING CODEASSIST VPS (use fresh one althought Will collide with swarm port) i do it on vps 4 cpu 8 GB RAM swap to 32 and its work so well

1. Create a new screen session

screen -S codeassist

2. Install UV

curl -LsSf https://astral.sh/uv/install.sh | sh

3. Reload the bash configuration

source ~/.bashrc

4. Clone the CodeAssist repository

git clone https://github.com/gensyn-ai/codeassist.git
cd codeassist

5. Edit the compose.yml file

nano compose.yml

Find this part:

3000:3000

and change it to:

3001:3000

Then press Ctrl + X, then Y, then Enter to save.

6. Edit the run.py file

nano run.py

Look for the section with:

# red #expose web ui port
"3000/tcp": 3000,

and change it to:

"3000/tcp": 3001,

7. Run the program

uv run run.py

When prompted, paste your Hugging Face token, then press Enter (the input won’t be visible  that’s normal).

IMPORTANT

You can’t log in through a tunnel; you must connect from your local PC.

8. From your local terminal (CMD/PowerShell/Linux terminal), run:

ssh -L 3001:localhost:3001 -L 8000:localhost:8000 -L 8008:localhost:8008 root@<your-vps-ip>

When asked, type yes, then enter your VPS password.

9. Open the web interface In your browser, go to:

http://localhost:3001

And done you Will be on codeassist web

After done solved like 1 or more code
Back to the terminal and Ctrl+c then they Will running the training,
wait for a while then check your hugging face account did the models uploaded or not if yes then Its done.
