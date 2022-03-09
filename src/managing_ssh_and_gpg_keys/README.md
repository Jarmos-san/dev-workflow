# Managing SSH & GPG Keys

If you've been writing code for a while there's no way you wouldn't know what
[Secure Shell (SSH)][ssh] & [GNU Private Guard (GPG)][gpg] are! They're integral
tools used from securely authenticating into a remote machine to
cryptographically signing electronic emails (and [git-commits][git commits] or
[git-tags][git tags]). And if you weren't aware of any of that, don't fret, I've
got you back!

As a software developer of the 21st Century (_or possibly in the near future_),
all source code you write will probably be stored & version-controlled at
third-party service providers like [GitHub][github] or [GitLab][gitlab]. In a
previous chapter we also mentioned about using (_and recommending_) using `git`
to version control our projects. And on top of it we need to allow `git` & the
third-party service providers to communicate with each other for validating the
authenticity of the source code's author. Such validation tasks are taken care
of by using both SSH & GPG.

Explaining the intricate details of how the validation & authentication is
performed is out-of-scope for this book. You can refer to the references linked
in the Appendices for further info on that context. But regardless, here's an
explanation of how I use SSH & GPG for my specific needs.

- SSH for authenticating myself when pushing `git-commits`. If I were to use
  HTTPS instead, I would've to type in the password & username each time! Using
  SSH is a major improvement of quality of life. And you can read more about it
  on "[_Connecting to GitHub with SSH_][github ssh]".
- I can also obviously use SSH to connect to a remote machine (say a Raspberry
  Pi or a cloud-service provided one) with ease & utmost security.
- And GPG is used to "sign" all of my work! So, all commits & tags I push to.
  GitHub are signed using GPG.

While SSH & GPG can be used elsewhere as well & is not limited to the use cases
I mentioned above, my needs are limited & your mileage may vary. However you
decide to use these tools, they require some secret keys which should managed
across your machines. They can also be configured to suit certain specific needs
& invite some drastic quality of life improvements to your workflow.

How I manage my secret keys & the configurations for SSH & GPG are detailed in
this chapter. The chapter (and its sub-sections) attempts to shed on;

1. How I configure SSH & GPG
2. The reasoning behind a specific configuration to exist.
3. How a specific configuration value improves my quality of life.
4. Generating new keys, backing them up for future requirements & storing them
   securely.

So, withou further adieu let's dive deeper into more specific details of this
chapter!

Useful resources:

- https://risanb.com/code/backup-restore-gpg-key/
- https://msol.io/blog/tech/back-up-your-pgp-keys-with-gpg/
- https://www.jwillikers.com/backup-and-restore-a-gpg-key
- https://www.jabberwocky.com/software/paperkey/
- https://softwareengineering.stackexchange.com/questions/212192/what-are-the-advantages-and-disadvantages-of-cryptographically-signing-commits-a
- https://mikegerwitz.com/2012/05/a-git-horror-story-repository-integrity-with-signed-commits
- https://withblue.ink/2020/05/17/how-and-why-to-sign-git-commits.html
- https://www.freecodecamp.org/news/what-is-commit-signing-in-git/
- https://dlorenc.medium.com/should-you-sign-git-commits-

<!-- Reference links -->

[git commits]: https://git-scm.com/docs/git-commit
[git tags]: https://git-scm.com/docs/git-tag
[github]: https://github.com
[gitlab]: https://about.gitlab.com
[github ssh]:
  https://docs.github.com/en/authentication/connecting-to-github-with-ssh
