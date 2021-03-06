---
layout: post
title: "Lessons Learned from The Great Database Disaster of '11"
date: 2012-01-09 18:24
comments: true
categories: [whoops]
Author: Jack Lawson
---

We were working on the "Shattered Tranquility" update, an
update that would give us much-needed flexibility on the items system, add new
zones and monsters to the game, and really enrich the game's lore by providing
random monster lines and quest backstories. We set up a test server, and put a
test database installation on the production database server; one database was
called something like "Neflaria\_Test", the other "Neflaria".

<!-- more -->

We were near the end of our update; we were about a week past our internal
deadline due to a few extra bugs we found. We wanted to make sure that
everything was perfectly ready; overhauling the entire items system was no
small feat. The entire team was on the project; Mattias even came back for a
few weeks to help out.

One day, about a week away from beta testing, I receive an ominous IM: "Oh no."

While preparing the test environment for the next round of testing, we had
accidentally deleted the entire player table. This had an interesting effect;
inventories and stats were stored seperately from the player table, which was
more account-related and contained login information. So, as we scrambled to
look for backups (more on this later), players began re-creating accounts, to
find themselves having a completely different level and inventory than they had
mere minutes ago.

And then the next disaster was uncovered: the closest database backup we had
was from a month ago.

We had to make a quick decision; players were logging in, and things were
going crazy in Neflaria. We could restore the backup from a month ago, or reset
the game. We also knew that the update would be ready in about two weeks. We
didn't want to reset, because we wanted to do a reset with the next update, and
we wanted to give everyone warning first. We didn't want to restore the backup,
because at a month old, it would put a *lot* of players way behind. So, we took
another option and had a "crazy week" while we worked on the update.

Ok, so now that the background is all together, here's what we learned.

* Keep better database backups. This is web-application-running 101. We *had*
  a backup system, but we completely failed to check that it was running
  properly, and we let a lot of players down. Now we have constant backups
  that run at several intervals during the day.
* Work on communication. A lot of players were upset, and thought we were
  doing a suprise reset. *We won't do that.* It was a mistake, but we didn't do
  a good job at communicating status. We focused all of our efforts on getting
  the update done so that we could release that, when we should have diverted
  some time to talk to the payers.
* Set up contingency plans. We've worked on a framework that allows us to focus
  on the technology behind the game, while allowing the mods and archmods to
  focus on the players in the game. We still have a high activity within the
  game, but we can now delegate communication to the mods.

Disasters can happen; we have to do our best to plan for them and make sure
that during recovery, players know *exactly* what's going on. Our number
one responsibility is to them.
