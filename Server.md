<div align="center">
    <a href="https://www.eecs.umich.edu/courses/eecs201/wn2023/"><img src="images/logo.png" alt="Logo" width="80" height="80"></a>
    <h3 align="center">The EECS 201 Master Guide</h3>
</div>
<br/>
<br/>
<br/>

## Course Server
The course server is a CLI computer available for use by all EECS 201 students. The server will be the environment the course autograder will run in, and will act as as a tool for students whose personal machines don't support certain programs (such as [Valgrind](https://valgrind.org/)).

<br/>
<br/>
<br/>

### Registering
In order to access the course server, you must first register your information with us. This will involve submitting your public ssh key and uniqname to us.

<br/>
<br/>

#### Starting Over

**If you do not need to start over, continue to the next section.**
<br/>
<br/>
If you have in some shape or form lost access to your ssh key and are completely unable to retrieve it, you can start this tutorial over with the following command:

    rm ~/.ssh/id_ed25519 ~/.ssh/id_ed25519.pub

<br/>
<br/>

#### Creating your SSH Key
First, you'll need to actually create your ssh key. The program to do this is called ssh-keygen, and it takes a couple of important arguments:

- `-t` refers to the type of the key. There's a few different types of keys, but the two we'll care for are ed25519 and RSA keys. Aim to generate the former type (they're more secure and shorter), but if your system doesn't support it feel free to use RSA
- `-C` allows you to name your keys so you can differentiate between them. Generally, you might see this as something to the effect of `username@computer`.

Overall, your command should look something like this:

    ssh-keygen -t ed25519 -C name@desktopname

You'll get a bunch of prompts asking you questions. Don't change the default location, and (I'd recommend) don't add a passcode.

<br/>

Anyways, what did we just make? [SSH Keys](https://www.ssh.com/academy/ssh-keys) use a concept known as asymmetric encryption to prove a user is who they say they are. SSH involves two keys: a private and public key. Anybody has access to the public key, but only you have access to the private key. The special thing about these keys is that if you encrypt something with either key, you must use the other one in order to decrypt it. In other words, a public key cannot decrypt a message encrypted with a public key, but a private key can.

<br/>

By giving us your public key, we (the server) can (on a very basic level) encrypt some string and return it to you. You are then expected to decrypt the string with your private key. If you return back to us (the server) the same string we originally had, then we know for a fact you are who you say you are, and can let you into the server. Pretty cool! Now, let's actually submit the key.

<br/>
<br/>

#### Submitting Your Key

There are two places you'll need to submit your public key. Before anything else, let's copy your public key into your clipboard. In your terminal, run the command:

    cat ~/.ssh/id_ed25519.pub

and copy the entire output.

Then, log into the [EECS Gitlab server](https://gitlab.eecs.umich.edu/") and click your profile in the top right, then go to SSH keys. Paste in your key and submit it. Next, go to the [course server user account form](https://peritia.eecs.umich.edu/account/) and submit your uniqname. You should recieve an email that will take you to the form and ask you to submit your ssh key.


<br/>
<br/>

### Logging In

Once you have submitted your keys, you're ready to log onto the server. The command is as follows (replacing `<UNIQNAME>` with your actual uniqname):

    ssh <UNIQNAME>@peritia.eecs.umich.edu

This is, however, very verbose and would get annoying to have to type out every single time. Instead, add the following lines to your `~/.ssh/config` file (create it if it doesn't exist):

    Host eecs201
        User <UNIQNAME>
        HostName peritia.eecs.umich.edu

Now, you can very easily log onto the server with:

    ssh eecs201


<p align="right"><a href="/README.md">Back</a></p>