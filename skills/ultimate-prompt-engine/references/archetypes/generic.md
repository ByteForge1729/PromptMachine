# Archetype: generic

Load when no specific archetype fits: a desktop app, a chat bot (Discord, Telegram,
WhatsApp), an automation script, a data pipeline, an internal tool, a smart-home or
hardware-plus-software project, a plugin for another app, or anything new.

A specific archetype is valuable because it knows what the **medium** forces on the
project, the way `mobile-app.md` knows a phone loses signal and kills background work.
This file teaches you to work that out yourself, fast, for any medium.

---

## Step 1: name the medium

State in one line where this runs and what the user touches:
*"A Discord bot that runs on a server and is used through slash commands in a chat."*
If you cannot write that line, the brief is ambiguous: make it the first read-back
question.

## Step 2: research the medium (3 searches)

Search for: the platform's official limits and policies for this kind of thing; how
similar projects break (forum threads, issue trackers); and whether any API or service the
project would rely on has been deprecated or restricted recently. Label findings as
documented, widely reported or your judgment.

## Step 3: ask the medium questions

Pick the ones that apply. Rewrite each as a plain scenario for this project.

### G1: where it runs `[required]`
**Ask:** Where does it actually run: on the user's computer, on a server you pay for, on
someone else's platform, on a device? That decides who pays, who updates it, and what
happens when that machine is off.
**Opens:** hosting, cost (O5), uptime

### G2: who installs and updates it `[required]`
**Ask:** How does a new user get it, and how does a fix reach people who already have it?
A script someone downloaded once never gets your bug fixes.
**Opens:** distribution, auto-update, versioning (S11)

### G3: what starts it `[required]`
**Ask:** What makes it do something: a person typing a command, a schedule, a message
arriving, a sensor, a file appearing? Each trigger has its own way of silently not
firing.
**Opens:** scheduling (S6), monitoring (O6), F2

### G4: what it is allowed to touch `[required]`
**Ask:** What does it need permission to read or change: files, a chat server, an email
account, someone's calendar? Ask for the least; platforms review and users judge broad
permissions harshly.
**Opens:** permission scopes, O3 privacy, security

### G5: the gatekeeper `[required, when a platform hosts or distributes it]`
**Ask:** Who can take it down or block it: an app store, a bot platform's rules, an API's
rate limits or terms? What are their rules for this kind of project?
**Research always:** read the current policy page; say what you found and when.
**Opens:** policy compliance, rate limits, 08-risks.md

### G6: when it fails, who notices `[required]`
**Ask:** If it stops working at 3 a.m., who finds out, and how? Background things fail
silently by default.
**Opens:** O6 alerts, logs, retries

### G7: the physical world `[required, when hardware is involved]`
**Ask:** What happens when power drops, the network is gone, or the device is moved?
Hardware adds parts to buy, wear out and ship.
**Opens:** offline behaviour, bill of materials, safety

## Step 4: write the medium's defaults

After the interview, write 3 to 6 "assume these unless told otherwise" lines for this
medium into `07-decisions.md` as ASSUMED, the same way `mobile-app.md` has its defaults.
If a medium comes up twice, propose turning the notes into a new archetype file.

## Not software at all?

This skill is built for software. If the project is a business plan, research study,
event or physical product with no software, say so plainly in the read-back. Offer to run
only the Product and Feature lenses, adapted, and do not pretend the technical lenses
apply.
