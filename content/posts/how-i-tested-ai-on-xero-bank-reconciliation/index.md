---
title: "How I Tested AI on Xero Bank Reconciliation"
date: 2026-10-27T09:00:00+10:00
draft: false
slug: "how-i-tested-ai-on-xero-bank-reconciliation"
description: "Xero truncates the bank feed reference Accounts needs. How I trained an AI agent to propose reconciliation matches, plus the nine steps I used."
summary: "Xero cuts off the exact reference Accounts needs to match a payment. At a Gold Coast manufacturer I got an AI agent to do the detective work instead."
tags: ["xero", "bank-reconciliation", "ai-automation", "ai-agents", "case-study"]
categories: ["Solutions"]
featureimagealt: "A bank feed card for Sample Supplies Pty Ltd whose reference INV 4471 Offic is torn off mid word, next to an empty dashed box with a question mark and a label reading Reference cut off."
---

**TL;DR:** Xero cuts off the exact reference Accounts needs to match a payment. At a Gold Coast manufacturer I got an AI agent to do the detective work instead: find patterns in past reconciliations, follow the same rules Accounts follow, and propose matches for a human to approve. Testing looked very promising and I was in my flow until the boss pulled the plug on the experiment. Only the Bank Rules went live. Now I’m seeking opportunities to finish what I started.

## The problem: Xero cuts off the bit you need

When Xero pulls in the bank feed, it truncates the Payee/Description and Reference fields. And the part that got chopped off may have been the quote, invoice or job number Accounts needed to match the payment.

So every day, all three Accounts team members (one per branch) played detective. It took many hours. I don't have an exact weekly number, so I won't make one up.

## Step one: let AI find the patterns

I exported the entire Past Reconciliations log from Xero to CSV and gave it to Claude Cowork. I asked it to find patterns and the number of times each occurred.

Accounts then went through Claude's spreadsheet and highlighted 23 transactions that could become Bank Rules. Those 23 are the part that made it into production.

## A safe sandbox (and a confession)

The IT Manager was against letting an AI agent loose inside Xero. Fair enough. But we couldn't pull the bank feed through the Xero API, so an agent clicking around the screen like a human turned out to be the only option.

So rather than let AI write straight into Xero's Discuss field, I had it set up three external tables:

- past successful reconciliations
- match attempts
- match failures

That gave AI a safe place to report its result AND its reasoning while I built and tested. I could read how it reached each conclusion and spot gaps in its knowledge and rules.

The first check: could it marry the payer name in the bank feed to an existing Xero contact, based on past transactions?

Confession: in hindsight a simple Google Sheet would have done the job.

## Sitting with Accounts

Next I sat with Accounts and mapped every operational fact and rule they work with. Same as training a new human, really. A sample of what was covered:

- Each branch has its own yearly schedule spreadsheet, with its own filename, branch abbreviation and file path.
- What each column is called and what it holds.
- Invoices are generated after job numbers.
- What invoice, quote and job numbers look like in each application.
- Until a job number exists in the yearly schedule, an invoice can't be generated. So if there's no job number, report "No Job Number".
- When a bank feed entry says "No Job Number", check the yearly schedule every 24 hours until the job number shows up, then add it to the notes.
- Which applications to check, in what order, and what to look for in each.

By the end I understood how the business ran far better than when I started.

With that context, the agent could spot card paid expenses and write notes in the same structure Accounts already use. It could also investigate across Xero contacts, the CRM, the quoting and job system, the past matches table and the yearly schedules to work out whether an invoice and job number existed, who the salesperson was, and report back.

## The test: re-check the human

My main test was simple. Take a transaction a human had already reconciled and tell the agent to investigate it from scratch. Did it land on the same answer?

On the very first test it reached the same conclusion as the human (no job number existed yet). It also flagged that the human had written the wrong branch abbreviation in the Discuss note.

The agent was also taught to review the human-approved matches each day and add them to its past matches table, so it kept learning.

## The nine steps, if you want to try it

1. **Pick an agent with its own computer.** Choose an AI agent that runs on its own virtual computer, with READ access to Xero and every application it needs. I used OpenClaw at the time. Today I'd pick Grok Bot first, then Claude Cowork now it has its own virtual computer.
2. **Set up a Google Sheet** with 3 tabs: Past Successful Reconciliations, Match Attempts, Match Failures.
3. **Mine your history.** Export the full Past Successful Reconciliations history from Xero and have AI find patterns and how often each one occurs, in a tidy spreadsheet.
4. **Let Accounts choose the Bank Rules.** They highlight the transactions that can become new rules.
5. **Brain dump with Accounts.** How spends, quoting, invoicing and payments work, and every application involved.
6. **Write the rule set** and the deduction process the agent should follow.
7. **Test by replicating human results.**
8. **Run it overnight.** Schedule the agent to work through new bank feed items in the early hours before Accounts starts, writing results to the sheet. Review its reasoning and adjust the rules.
9. **Hand over the pen.** Once confidence is high, let the agent write its result straight into Xero's Discuss fields with a short summary of its reasoning.

On human approval: the owner wanted full automation. I aimed for a more sensible first goal where the agent proposes and a human approves.

## Where it stopped

It was a slow start until I landed on the right tool. After that, the written rules came together in 2 to 3 days and testing quickly showed promising results.

Then priorities shifted, and I was (regretfully) told to drop it. Only the Bank Rules went into production. So I have no time-saved or match-rate stats to show you. I'm confident it could have saved hours a day of manual note writing and detective work.

There's also one problem I saw and never got to work through: EFTPOS part payments. The terminal doesn't send one bank feed line per sale. It lumps the whole day's takings into ONE line, so one deposit covers many invoices, and Accounts were matching it against printed paper receipts. That's the challenge I'm most looking forward to sinking my teeth into.

## What I enjoyed

Honestly, I loved this project. It leans right into my natural talents: pulling out the details that matter, writing processes, building a logical system, and coming up with strategies for automating a process, which takes some outside the box thinking.

Once the agent was set up, I was impressed by how well it clicked around each application and followed my rules to the right answer. Watching an AI agent do what a human normally does puts the biggest smile on my face. Not because we can get rid of the human. Because the human gets to focus on more challenging, meaningful and (hopefully) exhilarating work.

## Want to trial it?

If your team doesn't love bank reconciliation and you want to see how much of it an AI agent can handle, I'm looking for one business where I can come in (or remote in) for a few days and see how much we can automate.

In exchange, I'd like a publishable case study with real stats: time saved and line items matched. I'm also taste testing whether this is a niche I want to specialise in, and your business could be the one that benefits. I'm available from mid November 2026.
