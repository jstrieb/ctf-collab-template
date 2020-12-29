# Introduction

Create a collaborative environment inside GitHub Actions; conveniently save
data with git. Particularly useful for solving Capture The Flag
([CTF](https://en.wikipedia.org/wiki/Capture_the_flag#Computer_security))
problems.

For the less technical in the audience, this serves as a sort of "Google Doc"
for working on hacking competitions collaboratively.

# Quick start

[Create a repo from the
template](https://github.com/jstrieb/ctf-collab-template/generate). Do the rest
of the steps from within your copy of the repository.

In all cases, the username is `runner` and the password is `ctf`.

## Connect With Tor

Connecting over Tor is the most secure way to use the server, and doesn't
require signing up for any service. It does, however, require downloading the
Tor Browser Bundle. It also runs with noticeably higher latency than using the
alternative, non-Tor connection method.

1. Download and run the [Tor Browser
   Bundle](https://www.torproject.org/download/).
2. Navigate to the ["Run Collaborative CTF Environment"
   workflow](../../actions?query=workflow%3A"Run+Collaborative+CTF+Environment").
3. Start the server using the button in the top right ("Run workflow").
4. View the output; wait for it to print the connection information.
5. SSH in or connect from the Web using the connection information printed
   during the Action run. Note: whether connection to the `.onion` address
   using the browser or SSH, Tor Browser must be running.
6. Tor browser has a default setting that causes text to be illegible in `ttyd`
   and/or its dependency `xterm.js`. To fix this, go to `about:config` in the
   address bar, and set `privacy.resistFingerprinting` to `false`.

## Connect With ngrok (Without Tor)

Connecting over ngrok instead of Tor is a less secure, but lower-latency way to
connect to the server running on GitHub Actions. This method of connecting
doesn't require downloading Tor, but it does require signing up for ngrok.

1. [Sign up for ngrok](https://dashboard.ngrok.com/get-started/setup).
2. [Copy your ngrok
   Authtoken](https://dashboard.ngrok.com/auth/your-authtoken).
3. Navigate to the ["Run Collaborative CTF Environment"
   workflow](../../actions?query=workflow%3A"Run+Collaborative+CTF+Environment").
4. Paste in your ngrok Authtoken when you start the server using the button in
   the top right ("Run workflow").
   - To avoid pasting the Authtoken every time, paste it into a secret called
     `NGROK_TOKEN` under the [Secrets](../../settings/secrets/actions) settings
     area. It will be saved here and used automatically.
5. View the output; wait for it to print the connection information.
6. SSH in or connect from the Web using the connection information printed
   during the Action run.

## Once Connected

- By default, the collaborative environment uses `tmux` with <kbd>Ctrl +
  A</kbd> as the "prefix," and a few other custom keys that can be viewed in
  [.tmux.conf](dotfiles/.tmux.conf)
  - Read a [good introduction to
    `tmux`](https://www.hamvocke.com/blog/a-quick-and-easy-guide-to-tmux/)
  - Press <kbd>Ctrl + A</kbd> and then <kbd>c</kbd> to open a new window
  - Press <kbd>Ctrl + A</kbd> and then <kbd>n</kbd> to go to the next window
  - Press <kbd>Ctrl + A</kbd> and then <kbd>|</kbd> to split the current pane
    vertically (this is a vertical bar "|", not the letter "L" or "i")
  - Press <kbd>Ctrl + A</kbd> and then <kbd>S</kbd> to split the current pane
    horizontally (this is a *capitalized* "S" – `tmux` cares about
    capitalization)
  - Press <kbd>Ctrl + A</kbd> and then one of the arrow keys to move to the
    pane in that direction
- Use the `quit` command to terminate the server for all connected users
  - Alternatively, the workflow can be canceled from within the GitHub web
    interface
- Create folders in the repo (`~/ctf`) for each CTF to stay organized
  - Save any changes by committing using `git` within the `~/ctf` folder
  - The default identity associated with commits is anonymous
- Theoretically, unlimited users can connect at once via Tor, and up to 40 can
  connect using ngrok for free
  - Practically, the real upper-limit is probably far lower
  - Every new user connects using the same link/connection information
  - Additional users do not need GitHub accounts to connect or commit to the
    repository from within the environment
  - Each user can create their own windows independently, or switch to windows
    created by other users
  - All connected users have passwordless `sudo` capabilities

<details>

<summary><b>Graphical Server</b></summary>

**Don't use the graphical workflow unless absolutely necessary!**

- Sign up for ngrok and get an authentication token
- Run the workflow and pass in the ngrok authentication token
- Wait for ngrok to run, and look in your ngrok dashboard for the server and
  port to connect to
- Connect using an [RDP](https://en.wikipedia.org/wiki/Remote_Desktop_Protocol)
  client if using the graphical workflow
  - Username `runner`
  - Password `ctf`
  - There is a default RDP client installed on Windows
  - For Linux [Remmina](https://remmina.org/how-to-install-remmina/)

</details>

# Be a Good Citizen

This project uses generously-offered, free resources in a way that was likely
not intended by GitHub. Please do not abuse them.

I claim no responsibility for how you use this project. Based on my reading of
GitHub's:

- [Terms of
  Service](https://docs.github.com/en/free-pro-team@latest/github/site-policy/github-terms-of-service#the-github-terms-of-service)
- [Acceptable Use
  Policy](https://docs.github.com/en/free-pro-team@latest/github/site-policy/github-acceptable-use-policies)
- and [Actions Usage
  Policy](https://docs.github.com/en/free-pro-team@latest/github/site-policy/github-additional-product-terms)

I have concluded that using this Actions workflow to do productive work,
particularly if you don't have the ability to run a Linux computer of your own,
is probably permissible if done in good faith, and with an effort made to
reduce excessive resource consumption. For example, don't use the graphical
workflows unless absolutely necessary, because they are considerably more
resource intensive to set up and run.

That being said, I may be reading the policies wrong, and GitHub has the right
to change them at any time. In particular, if this use of GitHub Actions is
abused, it is likely that future ability to do things like this will be limited
by GitHub. **If you like it, don't ruin it for others.**

Note: typical users get [3,000 minutes of private Actions
time](https://docs.github.com/en/free-pro-team@latest/actions/reference/usage-limits-billing-and-administration#usage-limits)
per month per user. This project can quickly run up that time if you are not
careful. Check your own usage [here](https://github.com/settings/billing) to
see how close to the limit you are. Also note that actions stop automatically
after 6 hours.

# Acknowledgments

Thanks to my good friend Logan Snow ([@lsnow99](https://github.com/lsnow99))
for testing, fixing bugs, and other contributions!

This project makes use of several great software packages that have made their
services available for free:

- [Tor](https://www.torproject.org/)
- [ngrok](https://ngrok.com)
- [tmux](https://en.wikipedia.org/wiki/Tmux)
