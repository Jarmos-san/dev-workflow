# About SSH & GPG

If you've been writing code for a while you would already be aware of [Secure
Shell (SSH)][ssh] & [GNU Private Guard (GPG)][gpg]! They're integral tools used
from securely authenticating into a remote machine to cryptographic signing of
electronic emails. But more commonly & especially as a professional software
dev, there's a good chance you sign your [git-commits][git commits] and/or
[git-tags][git tags]).

At the time of writing this book, most if not all software developers host their
project's source code on a third-party service like
[GitHub][github]/[GitLab][gitlab]. Both the services make use of SSH & GPG in
some form or the other. For example, SSH is used to authenticate an user when
pushing `git-commits` or `git-tags` to the remote repository. While GPG is used
to verify the authenticity of a pushed commit or a tag.

So, as you can probably figure out, SSH & GPG both serves an integral role in
programmer's toolkit. As such it's **VERY** important to take proper care while
managing things related to those tools. To the uninitiated, the gravity of how
important managing SSH & GPG is mightn't be clear right away. The tools are akin
to the complex set of mechanisms installed at your home to keep intruders out &
let only a specific set of people inside. Those set of specific people (like
your family) probably has an access key code or a physical key without which
they can't get into their own homes either!

SSH & GPG serves similar purposes, as such, being irreponsible with them could
possibly lead to some disastrous consequences. For example, an user with
malicious intent could access your local machine remotely. Or perhaps, an
impostor could share source code of an open-source project claiming to be you!

Hence, similar to how a real-life lock-and-key combination works to protect your
house from intruders, SSH/GPG has to be used & managed in a similar fashion.
Letting your SSH access code land on a malicious user's hands means they can now
access your computer without much effort at all! And with the GPG keys, the user
could share source code of your project claiming to be you!

In a later chapter we'll take a more in-depth look at what happens if your
SSH/GPG keys were to be compromised. We'll also discuss measures you should take
to protect yourself from such compromising situation. And what you should do if
you were in such an unforeseen situation by accident.

So, without further adieu let's dive deeper into more specific details on this
topic! But don't forget to read the [recommended resources for further
reading][appendix] in the Appendix. The resources there will help you further expand
your knowledge about SSH & GPG to manage them as per your specific requirements.

<!-- prettier-ignore-start -->
<!-- Reference links -->

[git commits]: https://git-scm.com/docs/git-commit
[git tags]: https://git-scm.com/docs/git-tag
[github]: https://github.com
[gitlab]: https://about.gitlab.com
[github ssh]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh
[appendix]: ../appendix.html#appendix-recommended-further-reading

<!-- prettier-ignore-end-->
