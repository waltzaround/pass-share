# Pass share

This tool is for setting up a way for others (family or those you mostly trust) to recover a master passphrase in the event you aren't able to due to death or illness. It's designed with 1password's master passphrase in mind

This is obviously a fairly tricky thing to do, and involves a few compromises.

Check out the [Generator](https://lox.github.io/pass-share/generate.html) to get a sense of how it works.

## Approach

* Passphrase is encrypted with a randomly generated key and IV.
* The intermediate ciphertext and IV are printed out and stored somewhere physical that your loved ones could access. The fact that this portion is offline provides a "something you have" vs the keys later which are "something you know". This prevents brute force attacks with out physical access. It also means you can update your encrypted passphrase without re-distributing shares.
* The intermediate key is split into shares using [Shamir's threshold secret sharing scheme](http://en.wikipedia.org/wiki/Shamir's_Secret_Sharing) using a customizable threshold and number of shares.
* The shares are distibuted as makes sense to people you trust. You might choose a consensus of 2 and distribute it to 3 people, such that no one person could act alone. In my case I'm going with 4 shares and a consensus of 2. My wife gets 2 shares, and I give a backup share to two family members. This means that even if both my wife and I go, the backups can still combine their shares to meet the threshold.

## Updating

Provided you keep track of intermediate key that is distributed in shares, you can update the passphrase so that you can actually update your Master Passphrase over time.

See https://lox.github.io/pass-share/update.html.

## Recovery

When the shares are distributed, they come with instructions along the lines of:

> This is a piece of a secret code, that when combined with X others can be used to recover Lachlan's 1password Master Password in the event something has happened to him.
>
> Your code is: `801203c28043c4576a7fd43530cd66f4898a7b4e704833a32dadf13a83bbda343705d3fb5b1970d1160e33cc1ca01c3fd75`
>
> You need to get in touch with at least X other people on this list:
>
> * Person 1 <blah@blah.com>
> * Person 2 <blah@blah.com>
> * Person 3 <blah@blah.com>
>
> You will also need the recovery kit that is located  in his desk at his primary residence.
>
> When you have enough secret code pieces and the recovery kit, visit this page:
>
> https://lox.github.io/pass-share/
>
> Enter your code pieces, and the encrypted passphrase from the paper you got from the desk. Press "recover".
>
> At this stage you have the passphrase and you can access Lachlan's 1password vault.
>
> Good luck!


## Risks

* Sarah is like "What?"
* Nobody cares about my passwords
* WebCrypto API breaks in future
* Web page is inaccessible (Github pages)
* Can't access encrypted passphrase at residence
* Family conspires against me 🤷🏼‍♂️

## Todo

* [ ] Less horrible design, with better words
* [ ] Decide whether passphrase should be padded before intermediate encryption.
* [ ] PDF Generator?
