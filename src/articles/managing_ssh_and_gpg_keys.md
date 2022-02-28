# Managing SSH & GPG Keys

Secure Shell (SSH) & GNU Private Guard (GPG) are two tools which are "_an optional necessity_" in a developer's toolkit. I consider them "_optional_" because while not a hard requirement, using them is quite helpful.

I use them in the following ways & your mileage may vary:

- SSH for authenticating to GitHub when using `git` in a CLI environment.
- Using SSH authentication also means there's no repeated prompts for entering username & password! And besides, [GitHub themselves recommends using SSH authentication](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/about-authentication-to-github#authenticating-with-the-command-line).
- `git` enables the user to sign commits & tags for verifying the authenticity of the user's work (see [reference](https://git-scm.com/book/en/v2/Git-Tools-Signing-Your-Work)). And the web UI of GitHub shows a "_green verified_" button for all commits & tags which are GPG-signed.
- I've also configured `git` to sign all my commits & tags for all of my projects because certain FOSS projects I contribute require it.

That said, let's look into how do I set up those tools on my machine(s).

## Generating the Keys

Both SSH & GPG comes with their own pre-packaged tools to generate, manage, encrypt & de-encrypt their respective keys. Most Unix-based distros come with SSH tools installed & on Windows 10/11, OpenSSH is pre-packaged ([as of 2018](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_overview)).

Do note, **I prefer using SSH from Windows Subsystem for Linux  (WSL)** instead of directly from core Windows 10/11.

GPG on the other hand doesn't necessarily come pre-installed on all Unix-based distros. But from personal experienced I noticed all Ubuntu-based distros definitely packages GPG (and it's related tools) with it. You can check if GPG is installed or not, run the following command to check for it's existence:

```bash
$ gpg --version

# gpg (GnuPG) 2.2.19
# ... (output truncated)
```

And in case you find out GPG is missing from your system, please perform [a customary Google Search](https://bfy.tw/SdWg) on "_How to install GPG on X?_" (replace "_X_" with the OS you're using).

Also the UI/UX of using the tools to generate the keys are pretty much the same across all platforms, so you can copy the snippets I share below without any concerns. That said let's generate the keys:

### Generating SSH Keys

Before you proceed ahead with generating the SSH keys, please note, at any point in time if you ever face issues or have doubts, then the `man ssh` command will be your best friend.

That said, running the following command will generate the SSH key pair (a private/public) for the system:

```shell
ssh-keygen -t ed25519 -C "your_example_email.com"
```

This will prompt you to enter a filename for the keys. I prefer keeping the default filenames because it's one step easier to add them to `ssh-agent` (more about it later). I also skip adding a passphrase (**but you shouldn't do so!**).

Once you provide the necessary information, the key pairs are generated at:

- `$HOME/.ssh/id_ed25519` for the private key (**KEEP IT SECRET!**).
- `$HOME/.ssh/id_ed25519.pub` for the public key which can be shared around the Internet without any worries.

After generating the keys, you can then add them to `ssh-agent` like so:

```shell
eval "$(ssh-agent -s)"
```

And for those of you who created a key with a different name other than the default filenames OpenSSH provides, then run this command instead:

```shell
ssh-add $HOME/.ssh/your_custom_key
```

With the SSH keys generated, it's time to add them to GitHub for easier authentication. But before we read more about it, let's check out how can we generate GPG keys as well.

### Generating GPG Keys

Before generating the GPG keys, ensure your system is equipped with the latest tools to do so. Refer to a previous section of this write-up to identify if the tools exists on your system or not. And while generating the keys, if you ever find yourself upon a hurdle, feel free to refer to the man page by invoking the `man gpg` command.

Assuming you're on a fairly new Unix-based distro, it should've `gpg v2.1.17+`. And on Windows, make sure you download the latest version of [Gpg4win](https://www.gpg4win.org/).

That said, let's dive into generating our GPG key for our needs.

Running the following command will prompt the user for some info which will be used to create the keys:

```shell
gpg --full-generate-key
```

When prompted for further info like "_the type of key_", "_key size_" & "_validity of the key_", enter "`RSA`', "`4096`" "_empty_". That should generate a key with a length of 4096 bits using the RSA algorithm. Additionally, you'll want your key to never expire hence leaving the last prompt empty is preferable.

Do note, GitHub expects the keys to be of 4096 bits long & created using the RSA algorithm. Anything else might not working (although I've not checked it out myself yet).

Like the SSH keys, generating GPG keys also require you to share an email address. And when prompted for one, make sure to enter the email address which you use to login to GitHub. You'll also be required to add a passphrase but as usual I don't add one to mine.

With that, the keys are generated & you can view them by running the following command:

```shell
gpg --list-secret-keys --keyid-format=long
```

The said command outputs texts which looks something like this:

```shell
/Users/hubot/.gnupg/secring.gpg
------------------------------------
sec   4096R/3AA5C34371567BD2 2016-03-10
uid                          Hubot
ssb   4096R/42B317FD4BA89E7A 2016-03-10
```

**NOTE**: The GPG ID you'll need further looks like this - `3AA5C34371567BD2`.

We'll need to encrypt the GPG ID before we can share it on GitHub. And to do so, copy the ID & paste it into the following command:

```shell
gpg --armor --export <INSERT GPG ID HERE>
```

The command should produce an encrypted set of text in ASCII format which you should add to the GitHub. And in the next section we'll take a look at exactly that.

## Adding the Keys to GitHub

## Maintaining an Encrypted Backup of the Keys
