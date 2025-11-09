# Gensyn-codeassist-

##  TUTORIAL: RUNNING CODEASSIST ON A VPS

This tutorial demonstrates how to run CodeAssist on a VPS. This setup uses port `3001` to avoid potential conflicts with Swarm ports.

> **VPS specifications used:** 4 CPU, 8 GB RAM, 32 GB Swap(as cgpt how to swap your ram to 32.

---

### 1. Create a New Screen Session

This ensures the process continues to run even if your SSH connection drops.

```bash
screen -S codeassist
```

2. Install UV (Python Packager)

```bash
curl -LsSf https://astral.sh/uv/install.sh
```

3. Reload Bash Configuration
This allows uv to be used immediately.
```bash
source ~/.bashrc
```

4. Clone the CodeAssist Repository
```bash
git clone https://github.com/gensyn-ai/codeassist.git
cd codeassist
```

5. Edit the compose.yml File
Open the file with the nano editor:
```bash
nano compose.yml
```

find the 
3000:3000
And change it to 3001:3000 (changing the host port) 
Press Ctrl + X, then Y, then Enter to save and exit.


6. Edit the run.py File
Open the file with the nano editor:
```bash
nano run.py
```
search this section 
#expose web ui port
"3000/tcp": 3000,
then change to
"3000/tcp": 3001,

Press Ctrl + X, then Y, then Enter to save and exit.


7.run the program 
```bash
uv run run.py
```

When prompted, paste your Hugging Face token, then press Enter. (The token input will not be visible in the terminal; this is normal).

8. Create an SSH Tunnel (IMPORTANT Step)

   # IMPORTANT: You cannot log in through a regular tunnel or proxy. You must create an SSH tunnel from your local PC to the VPS.


Open a new terminal on your local PC (CMD/PowerShell/Terminal) and run the following command.

```bash
ssh -L 3001:localhost:3001 -L 8000:localhost:8000 -L 8008:localhost:8008 root@[YOUR_VPS_IP]
```

•Replace [YOUR_VPS_IP] with your VPS's IP address.
•If prompted, type yes, then enter your VPS password.
•Leave this terminal open.

9. Open the Web Interface
Now, open a browser on your local PC and access:
```bash
http://localhost:3001
```
You will now be connected to the CodeAssist web interface running on your VPS.


10. Finish & Training
After you complete 1 or more code tasks in the web interface.
Return to your VPS terminal (inside the screen -S codeassist session).
Press Ctrl + C to stop the uv run run.py process.
The training process will start automatically. Wait for a while.

# Check your Hugging Face account to see if the new model has been uploaded. If yes, the process is complete.

<!-- end list -->
