% How to git
% Feminist Linux Meetup 2021
% Lusy

---

## Begrüßung

---

## Agenda

* 0) Vorstelungsrunde
* 1) Was ist Versionskontrolle und wofür ist die gut?
* 2) Was ist git? Wie funktioniert es?
* 3) Hands-on Teil
* 4) Zusammenfassung/Ausblick

---

## 0) Vorstellungsrunde

* Wie lange benutzt ihr schon git?
* Wie oft benutzt ihr MRs?
* Wie oft benutzt ihr ...?
* Wie oft benutzt ihr rebase?
* Wollen wir zusammen merge Konflikte lösen?

---

## 1.1) Was ist Versionskontrolle

> "In software engineering, version control (also known as revision control, source control, or source code management) is a class of systems responsible for managing changes to computer programs, documents, large web sites, or other collections of information. Version control is a component of software configuration management."
Aus: [https://en.wikipedia.org/wiki/Version_control](https://en.wikipedia.org/wiki/Version_control)

---

## 1.2) Warum beschäftigen wir uns mit dem Ganzen?

* Vernünftig Versionen tracken/Überblick behalten

![finalfinal](images/finalfinal.png)

---

* Mit anderen am selben Code arbeiten: 
  --> anstatt das per Email rumzuschicken
  --> ermöglicht vernünftiges Zusammenführen von der Arbeit verschiedener Leute (auch wenn man sich damit auch ziemlich ins Bein schießen kann manchmal)
  --> ermöglicht auch einfaches Rückgängig-Machen falls irgendwas kaputt ist
* Änderungen von mir selber und anderen nachvollziehen mittels diffs
  https://github.com/lusy/wikifilters/commit/b31910fa2ebd00ebe33cf9a053ffc4390de6c9fb
* Sicherung der Dateien (ich schreib damit Hausarbeiten)

---

## 2.1) Was ist git?

* What is git? -> Historisch gab es mehrere Systeme (svn, cvs, mercurial + haufen, den ich nie gehört hab hier: https://www.softwaretestinghelp.com/version-control-software/), ich kenne heute aber kaum Projekte/Gruppen, wo was anderes benutzt wird
TODO: vgl auch mit DjangoGirls tutorial
* git geschichte?
  * created by Linus Torvalds in 2005 (für Linux Kernel, löst bitkeeper ab)
  * ". As with most other distributed version control systems, and unlike most client–server systems, every Git directory on every computer is a full-fledged repository with complete history and full version-tracking abilities, independent of network access or a central server."

---

## 2.2) Wie funktioniert es?

* How does it work
  * TODO: Diagram!
  * Schritte/Merkmale
  * Distributed: Man hat ne lokale Kopie auf dem eigenen Rechner -> Vorteil: ich kann auch offline arbeiten/commiten und ein lokales working tree anlegen, das dann bei Gelegenheit online gepush wird

---

## 2.3) Verteilte vs. Zentralisierte Versionskontrollsysteme
  "
Advantages of DVCS (compared with centralized systems) include:

    Allows users to work productively when not connected to a network.
    Common operations (such as commits, viewing history, and reverting changes) are faster for DVCS, because there is no need to communicate with a central server.[6] With DVCS, communication is only necessary when sharing changes among other peers.
    Allows private work, so users can use their changes even for early drafts they do not want to publish.[citation needed]
    Working copies effectively function as remote backups, which avoids relying on one physical machine as a single point of failure.[6]
    Allows various development models to be used, such as using development branches or a Commander/Lieutenant model.[citation needed]
    Permits centralized control of the "release version" of the project[citation needed]
    On FOSS software projects it is much easier to create a project fork from a project that is stalled because of leadership conflicts or design disagreements.

Disadvantages of DVCS (compared with centralized systems) include:

    Initial checkout of a repository is slower as compared to checkout in a centralized version control system, because all branches and revision history are copied to the local machine by default.
    The lack of locking mechanisms that is part of most centralized VCS and still plays an important role when it comes to non-mergeable binary files such as graphic assets or too complex single file binary or XML packages (e.g. office documents, PowerBI files, SQL Server Data Tools BI packages, etc.).[citation needed]
    Additional storage required for every user to have a complete copy of the complete codebase history.[7]
    Increased exposure of the code base since every participant has a locally vulnerable copy.[citation needed]
  "
---

## 3) Hands-on Teil

Wir arbeiten zusammen in einem geteilten Repository: link

--> Leute als Collaborators hinzufügen

--- 

git init
git push
...

---

Hinweis für (graphische) Anwendungen/Clients
ich nutze Command line + tig

Sonst:
gitk?

---

Hands on
3a)Minimalprogramm (das unbedingt passiert)

* Projekt forken/als Collaborator hinzufügen + clonen
  `git clone ...`

* Branch erstellen --> good practice: auf einem eigenen Feature Branch arbeiten und dann einen MR stellen, damit es in `main` zurückgeführt wird
  ```
  $ git branch <branch-name>
  $ git checkout <branch-name>
  ```
  oder
  ```
  $ git checkout -b <branch-name>
  ```

(* `git status` -> immer gut wenn ich nicht weiß was grad sache ist)

* Zeug hinzufügen + pushen
  ```
  $ git add <file-name> [<file-name>]
  $ git commit
  $ git push origin <branch-name>
  ```

* MR (+Review)
  -> Jede Person erstellt den Anfang einer Geschichte und gib den PR weiter an wen anders.
  -> Person 2 reviewt, gibt evtl Verbesserungsvorschläge, bzw. 2. Satz wie es weiter geht.
  -> Person 1 arbeitet die Vorschläge ein
  -> Person 2 approves PR
  -> Person 1 merges

* "Wie werde ich Zeug los, das kaputt ist und ich eigentlich gar nicht commiten wollte?"
  -> Alle erstellen sich einen neuen Branch. Jede Person arbeitet jetzt an eine neue Geschichte, die sie bisher nicht kannte (ich verteile das im Kreis weiter.
  -> 3 Mal was schreiben, was man eigentlich gar nicht schreiben wollte (vlt an der falschen Geschichte. Oder einfach iwas schreiben, dass ich nicht wollte)


** aus dem Staging-Bereich raus
Unstage changes (undo "git add" before commit)
----------------------------------------------
> git reset HEAD <file name>


** lokales Commit verwerfen

> git reset --hard <branch-name>


** remote Commit revert?
    Revert the changes specified by the fourth last commit in HEAD and create a new commit with the reverted changes.

> git revert HEAD~3


* "Ich hab vergessen, was zum letzten Commit hinzuzufügen"

# Edit hello.py and main.py
>git add hello.py
>git commit

# Realize you forgot to add the changes from main.py
>git add main.py
>git commit --amend --no-edit

--no-edit flag will allow you to make the amendment to your commit without changing its commit message.

You can also use 'git commit --amend' to change the last commit messsage

* "Wie kann ich meine Änderungen auf einen anderen Branch/Commit umziehen?"
** letzte Commits/Änderungen auf nen anderen Branch
Move recent commits to another branch
-------------------------------------
# Note: Any changes not committed will be lost.
$ git branch newbranch      # Create a new branch, saving the desired commits
$ git reset --hard HEAD~3   # Move master back by 3 commits (GONE from master) (--hard is important, otherwise the files just get unstaged!)
$ git checkout newbranch    # Go to the new branch that still has the desired commit

** git cherrypick

```
$ git checkout <branch-name>
$ git cherry-pick <commit-hash>
```

Zusatzzeug für wenn Zeit/Lust ist
3b1) Merge Conflict

use `git status` um sich zu orientieren wo es Probleme gibt
entsprechende Dateien editieren
neu commiten

* Exkurs: `git blame` um herauszufinden wer eine Zeile hinzugefügt hat
```
$ git blame -L 1,5 README.md  // -L specifies line range
```

3b2) Rebase
Wenn ich meinen branch immer auf den neuesten `main`-Stand halten möchte

Rebase (do only on own branches!!)
------

$ git rebase -i <commit-hash>~1

-> interactive window opens, asking what should happen with each commit
-> write "edit" in front of the commit
-> edit file

$ git add <file_name>
$ git commit --amend --no-edit
$ git rebase --continue
$ git push --force origin master


Rebase Branch2 ontop of Branch1
-------------------------------

Backup Branch2
# from Branch2
$ git checkout -b Branch2_backup

# from Branch2
$ git fetch origin           # update all tracking branches, including Branch1
$ git rebase origin/Branch1  # rebase on latest Branch1

Keep in mind that you have now rewritten the history of Branch2 and if the branch is already published you will have to force push it to the remote via

$ git push --force origin Branch2

### Zusammenfassung


---

> "The European Council (EC) describes their key goals with the Directive as protecting press publications; reducing the "value gap" between the profits made by Internet platforms and by content creators; encouraging collaboration between these two groups, and creating copyright exceptions for text- and data-mining." Source: EN WP

---

## Timeline

    2012 planned revision of 2001 Copyright Directive announced
    Jul 2014 first report on the state of EU copyright published
    14 Sep 2016 first draft of the new directive
    20 Jun 2018 EU Parliament Committee on Legal Affairs
    12 Sep 2018 EU Parliament approves a revised proposal
    13 Feb 2019 final version after trilogue meetings
    26 Mar 2019 EU Parlament votes in favour
    15 Apr 2019 directive approved by the EU Council
    2 year period for Member states to pass appropriate legislation

---

## Draft Article 11 (Article 15): "link tax"

"news aggregators or media-monitoring services" which use news articles for commercial purposes should pay the publishers for accessing them

---

> "The protection granted under the first subparagraph shall not apply to acts of
hyperlinking.

> The rights provided for in the first subparagraph shall not apply in respect of the use of
individual words or very short extracts of a press publication."

---

> "4.
The rights provided for in paragraph 1 shall expire two years after the press publication is
published. That term shall be calculated from 1 January of the year following the date on
which that press publication is published."

---

> "5.
Member States shall provide that authors of works incorporated in a press publication
receive an appropriate share of the revenues that press publishers receive for the use of
their press publications by information society service providers."

---

## Draft Article 13 (Article 17): "upload filters"

tasks service providers that host user-generated content to employ "effective and proportionate" measures to prevent users from violating copyright

---

> "Mit der Schrotflinte auf Youtube geschossen, halbes Netz mitgetroffen"

<small>[https://netzpolitik.org/2019/chance-verpasst-dieses-urheberrecht-bleibt-in-der-vergangenheit-stecken/](https://netzpolitik.org/2019/chance-verpasst-dieses-urheberrecht-bleibt-in-der-vergangenheit-stecken/)</small>

---

<img src="images/Spontante_Kundgebung_in_Hamburg_gegen_EU-Urheberrechtsvorhaben_4.jpg" height="500" alt="protests Hamburg">
<small>[Markus Göllnitz](https://commons.wikimedia.org/wiki/User:CamelCaseNick)
[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/deed.en)</small>

---

<img src="images/schulze-tweet.png" height="500" alt="Sven Schulze tweet">
<small>[https://twitter.com/schulzeeuropa/status/1096445520770404352](https://twitter.com/schulzeeuropa/status/1096445520770404352)</small>

---

<img src="images/Blackout_of_wikipediade_by_Wikimedia_Deutschland_-_March_2019.png" height="500" alt="blackout German Wikipedia March 2019">
<small>[https://upload.wikimedia.org/wikipedia/commons/c/c5/Blackout_of_wikipedia.de_by_Wikimedia_Deutschland_-_March_2019.png](https://upload.wikimedia.org/wikipedia/commons/c/c5/Blackout_of_wikipedia.de_by_Wikimedia_Deutschland_-_March_2019.png)</small>

---

## Lawrence Lessig

<img src="images/Lawrence_Lessig_May_2017.jpg" height="400" alt="Lawrence Lessig">
<small>By [Joi Ito](https://www.flickr.com/photos/joi/33668559574/), CC BY 2.0, [https://commons.wikimedia.org/w/index.php?curid=59092992](https://commons.wikimedia.org/w/index.php?curid=59092992)</small>

---

## Code and Other Laws of Cyberspace

<img src="images/code_v1_book.jpg" height="400" alt="Code v1">
<small>By Source, Fair use, [https://en.wikipedia.org/w/index.php?curid=34070395](https://en.wikipedia.org/w/index.php?curid=34070395)</small>

---

## Code Version 2.0

<img src="images/code_v2_book.jpg" height="400" alt="Code v2">
<small>By Source, Fair use, [https://en.wikipedia.org/w/index.php?curid=34069549](https://en.wikipedia.org/w/index.php?curid=34069549)</small>


---

## The pathetic dot theory

<img src="images/Pathetic_dot_theory.png" height="400" alt="pathetic dot theory">
<small>By Lawrence Lessig - [https://www.socialtext.net/data/workspaces/codev2/attachments/what_things_regulate:20061211230426-1-8535/scaled/4constraints.png](https://www.socialtext.net/data/workspaces/codev2/attachments/what_things_regulate:20061211230426-1-8535/scaled/4constraints.png), CC BY-SA 2.5, [https://commons.wikimedia.org/w/index.php?curid=25113167](https://commons.wikimedia.org/w/index.php?curid=25113167)</small>


---

# Chapter 10: Intellectual Property

---

## In a nutshell

> "We are not entering a time when copyright
> is more threatened than it is in real space. We are instead entering a time
> when copyright is more effectively protected than at any time since Gutenberg."

---

# Copyright, historically

---

"the single, defining feature of these norms can perhaps be summarized like
this: that a consumer could do with the copyrighted content that he legally
owned anything he wanted to do, without ever triggering the law of copyright."

---

"Roughly put, copyright gives a copyright holder certain exclusive rights over
the work, including, most famously, the exclusive right to copy the work."

"The right is protected to the extent that laws (and norms) support it,"
"it is threatened to the extent that technology makes it easy to copy."
"In this sense, copyright has always been at war with technology."

---

## Analog vs digital

"Thus there were many ways in which you could use creative work in the
analog world without producing a copy."

"Digital technology, at its core, makes copies."

"There is no way to use any content in a digital
context without that use producing a copy."

---

## Possible regulators

"What means would bring
about the most efficient set of protections for property interests in cyberspace?"

"One is the traditional protection of
law—the law defines a space where others should not enter and punishes
people who enter nonetheless. The other protection is a fence, a technological
device (a bit of code) that (among other things) blocks the unwanted from
entering."

---

"it is hard for the law to distinguish between legitimate and illegitiamate uses of cyberspaces"

---

## White Paper 1995

"The White Paper proceeds as if the problem of protecting intellectual property in cyberspace was just like the problem of
protecting intellectual property in real space.
[...]
But something fundamental has changed: the role that code plays in the
protection of intellectual property. Code can, and increasingly will, displace
law as the primary defense of intellectual property in cyberspace. Private
fences, not public law."

---

## DMCA 1998

"Code that someone implements to control either access to or use of a copyrighted work got
special legal protection under the DMCA: Circumvention of that code, subject
to a few important exceptions, constituted a violation of the law."

---

## Law vs contracts vs code

"As Stefik writes:
[T]he consumer does not have the option of
disregarding a digital contract by, for example, making unauthorized copies of
a work."

---

## For whom is the law

"Private law creates private rights to the extent that these private rights
serve some collective good. If a private right is harmful to a collective good,
then the state has no reason to create it."

---

"If the law did not
protect authorship at all, there would be fewer authors."

---

"Now if all you think about is protecting the distribution of professionally
created culture, this might not concern you much. If you’re trying to stop
“piracy,” then a regime that says every use requires permission is a regime
that gives you a fairly broad range of tools for stamping out piracy."

---

"Standing alongside professional culture is amateur culture—where amateur doesn’t mean inferior or without talent, but instead culture created by
people who produce not for the money, but for the love of what they do."

"Importantly, too, this kind of cultural remix has historically been free of
regulation."

---

## Fair use

"Were these transactions left free because it
was too costly to meter them? Or were these transactions left free because
keeping them free was an important public value tied to copyright?"

---

"But maybe this conflict is just temporary. Couldn’t the code be changed
to protect fair use?
The answer to that hopeful (and again, hopeful because my main point is
about whether incentives to protect fair use exist) question is no, not directly.
Fair use inherently requires a judgment about purpose, or intent. That judgment is beyond the ken of even the best computers."

---

## right to read anonymously

"we must ask whether the latent right
to read anonymously, given to us before by imperfections in technologies,
should be a legally protected right."

---

"These three examples reveal a common pattern—one that will reach far
beyond copyright. At one time we enjoyed a certain kind of liberty. But that
liberty was not directly chosen; it was a liberty resulting from the high costs of
control."

---

## Pending Choices

- whether to allow intellectual property in effect to
become completely propertized
- whether to allow this regime to
erase the anonymity latent in less efficient architectures of control
- whether
to allow the expansion of intellectual property to drive out amateur culture

---

## What values are we protecting?

---

# Thank you!

These slides are licensed under the [CC BY-SA 4.0 License](https://creativecommons.org/licenses/by-sa/4.0/).

![by](images/Cc-by_new_white.svg)
![sa](images/Cc-sa_white.svg)

---

# Questions? Comments? Thoughts?
