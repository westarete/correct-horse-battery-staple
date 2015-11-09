## A script for generating reasonably strong, memorable passwords 

This script generates random passwords. Each one is made of up four 
dictionary words, separated by spaces. Passwords of this format are easy to 
type and remember, and are surprisingly strong.

To use the script, clone this repo, then run this command from within
the source directory:

```
ruby generate.rb
```

Here's an example of the output (don't use these passwords, of course):

```
wont daughter cells georgetown
resource antibodies prince flute
tunisia hide pins terror
album feature enemy isaac
ginger graphs critic minnesota
sailing chef fires superb
stuart parents conditions historic
department enterprises title netscape
avalon collapse copyright climb
fare historic struck streaming
```

It prints out several possibilities so that you can choose the one that seems
most memorable to you. If you don't like any of them, run it again.

The script draws from a vocabulary of around 10,000 common words. The words 
have been mostly screened for offensive entries, so it should be safe to 
demonstrate its use at work or in public.

## General recommendations for password security

Companies' password databases routinely get compromised and published, exposing 
your username and password for those accounts. Strong, unique passwords will 
protect your accounts from most of these attacks.

A good personal password security policy can be summarized as follows: 

- Use a password manager such as [1Password](https://agilebits.com/onepassword) 
  to generate and store strong, unique passwords for everything. 
- Never reuse any password. Generate a new one for each site, account, or purpose.
- Use this script to generate the one or two unique passwords that you *must* 
  remember, e.g. your laptop's login password, and the master password for 
  your password manager.
- Change your most important passwords periodically (say once per year). Using
  the techniques above, this should not be too onerous.
- Don't use any computer that you suspect could be compromised. If you suspect 
  that your own computer has been compromised, shut it down and consult a
  security expert to safely recover your data and start over.

## Background

![XKCD comic on password strength](http://imgs.xkcd.com/comics/password_strength.png)

[The XKCD cartoon above](https://xkcd.com/936/) illustrates the problem with
traditional made-up passwords:

> Through 20 years of effort, we've successfully trained everyone to use passwords
> that are hard for humans to remember, but easy for computers to guess. 

This script implements the four-random-word technique that he described.  

## Strength comparison

The XKCD technique, as implemented here, is about as strong as an 8-character 
random password: 

```
irb> Math.log(95 ** 8).round(2)  # 8 random characters, including punctuation
=> 36.43

irb> Math.log(10_000 ** 4).round(2)  # 4 random common words
=> 36.84
```

While the XKCD technique may not be strong enough to fully protect passwords 
at sites that use weak hashing algorithms, both 1Password and the Mac login 
keychain use very strong algorithms, so this should be plenty strong for those 
two purposes. Use your password manager to generate long, random passwords for
all other scenarios, as described in the recommendations above.

## The dictionary

I arrived at the ~10,000 words contained in the script through the following process:

1. Download the 1/3 million most common words from 
   [Peter Norvig's Natural Language Corpus Data](http://norvig.com/ngrams/).
2. Trim that list down to the top 12,000.
3. Remove the number counts from each row using sed/search/replace.
4. Sort the list alphabetically for easier reading.
5. Manually scan through the list and delete entries that may be offensive
   or awkward in a work setting or public speaking environment.
   
Obviously the last step is a bit error prone. I may have missed a few 
offensive/awkward words.

## Resources

The original XKCD comic that describes the problem with made-up passwords:

https://xkcd.com/936/

An article that describes how passwords are typically harvested from compromised
websites:

http://arstechnica.com/security/2012/08/passwords-under-assault/

Advances in commodity hardware are making it even easier for attackers to
break weak passwords:

http://arstechnica.com/security/2012/12/25-gpu-cluster-cracks-every-standard-windows-password-in-6-hours/

Recent attacks at common websites that put all their users' passwords at risk:

- [LinkedIn](https://en.wikipedia.org/wiki/2012_LinkedIn_hack)
- [eBay](http://money.cnn.com/2014/05/21/technology/security/ebay-passwords/)
- [Evernote](http://www.digitaltrends.com/mobile/evernote-hack-50-million-users-forced-to-reset-passwords/)
- [DropBox](http://www.businessinsider.com/dropbox-hacked-2014-10)
