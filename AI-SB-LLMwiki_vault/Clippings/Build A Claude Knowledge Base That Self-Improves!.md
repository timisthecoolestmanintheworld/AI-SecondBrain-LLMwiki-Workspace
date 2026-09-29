---
title: "Build A Claude Knowledge Base That Self-Improves!"
source: "https://www.youtube.com/watch?v=ib74sLgjIBM"
author:
  - "[[Systems Made Better]]"
published: 2026-05-23
created: 2026-09-28
description: "👉 Get my Claude CoWork OS (including this system) at https://bettercreating.com/coworkos and find the Knowledge Base Kit below. In this video I build Karpathy's AI knowledge base from scratch in Clau"
tags:
  - "clippings"
---
## Summary Note
In this BetterCreating video, Simon Pitmann describes how to set up a personal knowledgebase using the [[llm-wiki-Github Gist]] model described by Karpathy, and provides a link to a base skill for building and maintaining it. Those material are at https://tinyurl.com/claudeknowledgekit 

He eludes to his Specialist Agent skill in AgentOS and CoworkOS that self-improve with user interaction - e.g. query and correction. 

## Video Contents


![](https://www.youtube.com/watch?v=ib74sLgjIBM)

👉 Get my Claude CoWork OS (including this system) at https://bettercreating.com/coworkos and find the Knowledge Base Kit below. In this video I build Karpathy's AI knowledge base from scratch in Claude CoWork — in 45 minutes, no Obsidian, no code. You'll get the full architecture (three folders, one CLAUDE.md), the five-step framework, and the Claude Skill that runs the monthly health check for you!  
  
Join the Agentic Business Acceleator 2026: https://agenticbusinessmethod.com/accelerator (includes CoWork OS & Business OS templated systems)  
  
🎉 FREE DOWNLOADS:  
\+ Get the Claude Knowledge Base Starter Kit at https://tinyurl.com/claudeknowledgekit (Includes the CLAUDE.md template, build prompt + Health Check Skill from this vide)  
\+ Get my free PDF guide on “Your First Steps to Building an Agentic Business” 👉 https://tinyurl.com/agentictransformationguide  
  
🔗 MENTIONED LINKS:  
\+ Karparthy’s X Post that started it: https://x.com/karpathy/status/2039805659525644595?s=46&t=so-d50SiR5Zy2uoiwnsjnw  
\+ My Notion Agent OS System: https://bettercreating.com/agentos  
\+ All my Notion templates & agentic business resources: https://bettercreating.com/downloads  
\+ WisprFlow: https://ref.wisprflow.ai/bettercreating  
\+ Get Notion for free: https://link.bettercreating.com/notion  
\+ Claude: https://claude.ai  
  
🧡 FOLLOW ME & STAY IN TOUCH:  
📸 Instagram - https://instagram.com/bettercreating  
🐦 Twitter - https://twitter.com/bettercreating  
🎵 TikTok - https://tiktok.com/@bettercreatingofficial  
📨 🌍 Get Resources & Sign Up to my newsletter here: https://www.bettercreating.com  
🖥️ Get My Notion Templates: https://bettercreating.com/downloads  
☑️ Get my iOS, iPad & Notion Icon Packs: https://bettercreating.com/iosdesignpack  
  
🎬 WATCH NEXT:  
\+ Set Up Claude Cowork better than 99% of people: https://youtu.be/pl90LATQlHI  
\+ Stop Adding AI Tools. Build an Agentic Business: https://youtube.com/watch?v=eABf3JdqoLk  
  
🎥 VIDEO CHAPTERS:  
00:00 Build Karpathy's AI Knowledge Base in Claude  
01:56 My Claude CoWork Knowledge Base: System Overview  
03:56 The Claude Build - System Setup  
11:20 The Claude Build - Information Dump  
16:08 The Claude Build - Create the Wiki  
20:37 Creating A Compounding Loop: Self-Improvement in Claude  
24:22 System Health Check: Claude CoWork Scheduled Task  
33:39 Final Results  
34:53 The 1 Day vs 100 Day Transformation To Aim For  
  
✅ Subscribe to my intentional tech channel: @BetterCreating  
  
👋 SYSTEMS MADE BETTER  
I’m Simon & I help business owners simplify and scale with accessible agentic systems & Notion.  
  
As a Tech YouTuber and Notion Ambassador I went from $0 to $200K+ profit in a year using Notion and agentic AI. Now I teach the system behind it, so you can work less, stay calm, and scale without needing to code. This is systems made better for small & medium businesses and entrepreneurs.  
  
On this channel you’ll learn how to:  
1\. Consolidate scattered context into one Notion knowledge system  
2\. Architect AI-ready workflows and information architecture (no code)  
3\. Activate AI fluency and deploy your own AI agent team  
4\. Automate and scale through intelligent systems, strategic focus and your wider tech stack.  
  
#claude #secondbrain #systemsmadebetter  
  
\--  
  
As either a direct affiliate or Amazon Associate I get a small commission on the product links above at no cost to you, so thanks in advance!

## Transcript

### Build Karpathy's AI Knowledge Base in Claude

**0:00** · For years, I've used a second brain.

**0:02** · This might be the simplest, most powerful self-learning personal knowledge base I've ever discovered built with Claude, and I'm going to show you how to do it. Hi, at the start of 2026, one of the most respected voices in AI quietly posted how he runs his own personal knowledge base, a second brain where you hold all your information and make connections and use it to inform what you do. 105,000 people bookmarked it, and probably almost none of them have built one. And that's the problem.

**0:29** · This is genuinely the most useful AI setup I've seen in months and implemented in Claude, and it takes probably 45 minutes to build over a weekend. No Obsidian, no vector databases, no code, just a brilliant self-improving knowledge base. Here's exactly what you're getting in this video. I'm going to show you the architecture, the whole system in 60 seconds. I'm going to show you the framework of how to build it and build it with you right now on this video.

**0:56** · And then, I'm going to show you the Claude skill that helps you audit it and help it improve and maintain itself over time. The five-step framework is this: you set it up, you dump your information into it, you then get AI to build a wiki, you ask it questions and create a compounding link to save answers back into it, and with a health check and that loop, it just keeps improving over time.

**1:23** · So, by the end of this video, you'll know exactly what the system is, why it beats every Obsidian plus plugins setup you can find for simplicity, and how to build your own right now with Claude. Now, I found that day one of running it, your knowledge base is pretty basic, but day 100, it's a company asset that nobody else has. Your perspective, your sources, your judgment in one place. So, double-check you're actually subscribed to Systems Made Better right now, cuz YouTube might just be feeding you this anyway, and let's get on with all becoming significantly more intelligent very quickly.

### My Claude CoWork Knowledge Base: System Overview

**1:59** · So, here's the top-level design in just 60 seconds before we go ahead and build it. Essentially, you're looking at three folders and one file on your computer that Claude looks at. I'm putting this right inside my Coda OS and I'm going to be adding it to the template system soon. You've got a Claude MD at the top of the knowledge base, which is the schema. It directs Claude on how to read it and use it. You've then got three folders. Raw, think of raw as your junk drawer.

**2:27** · Articles, notes, screenshots, meetings, you just everything goes in here and you save it and you don't organize it. Then you've got the wiki where AI writes the organized version.

**2:36** · You never edit this by hand. It's all done by the AI. And then you've got outputs, answers, briefings, and reports that the AI generates when you ask it questions. And the best bit is those then get fed back in and help to refine it. Plus one file at the root, yeah? The Claude MD. And you could have multiple versions of this within essentially a top-level where it all sits. That means you can have multiple knowledge bases all connected together. That's it. No database, no Obsidian, no vault setup, just folders and text files on your computer.

**3:06** · And before you ask, no, you don't need a rag embedding or any vector store, if you know what all that stuff is. Kaparthy's own knowledge base is around 100 articles and 400,000 words and the LLM handles it fine maintaining an index and reading what it needs. If it works for one of the most respected AI researchers alive, it'll probably work for your business. The best thing, like what I've done in my Notion Agent OS, is you can then point a custom agent at that knowledge base and it becomes a specialist agent expert that you can speak with.

**3:38** · It can use the knowledge to work on problems with you. But that is for another video on the channel. I'll be sharing a video soon about how I'm turning bodies of work from expert thinkers into personal assistants that help me on my business. It's totally wild. \[music\] And we're doing that in both Notion and Claude.

### The Claude Build - System Setup

**3:59** · Okay, I am doing this in Claude co-work.

**4:02** · We've got a new window open and I'm pointing it at my main co-work OS folder. So, basically, I have everything in one folder on my home, the local, there's a Claude co-work folder, everything happens in here. You just direct it at it and I've got instructions like about me files and all of that. But, watch my how to get set up on co-work first if you want to do that.

**4:20** · But, we're going to add a new folder in here called knowledge. There it is.

**4:24** · Going to drop it in at the top level.

**4:26** · We're going to go back to Claude and we're going to set this up. So, I use WhisperFlow to instruct Claude on what I want to build, link in the description.

**4:33** · This is what we're going to say. I want to build a self-improving knowledge base that you manage as a librarian. Let's start and make a folder structure inside the new folder I've added in your Claude co-work folder called knowledge. Inside that, I want three subfolders. We want raw, wiki, and outputs. Plus, drop a Claude MD file in the root and I'll show you what is going to go in that in a moment. And what you could do is give it context of what you're doing.

**5:02** · So, we could say, "For context, here is Andre Karpathy's explanation of what we're about to build." But, we're going to be doing this locally rather than with Obsidian. I'm going to use Opus 4.7 cuz it's intelligent and it'll do the work, but probably don't need it. And there it is. It's turned up. It's dropped those in.

**5:22** · I'm going to just rename this so it's clearer. We'll call it knowledge base.

**5:27** · It's interesting that it couldn't read the Twitter thread, but I'll just put it in here.

**5:31** · Here's the information for you from that thread. However, I'm going to take you through step by step what I want.

**5:39** · Now, if we go back and take a look at the folder, we've got our knowledge base. Now, what we might want to do at our top level is create another one, second brain knowledge, and we could drop the whole thing inside that. And we could give it a subject. So, what do we want this to be on? Why don't we make this one on productivity? All right, I've dropped what we just built into another top level folder, which is called second brain knowledge, and that's going to be the top level where we can create multiple versions of knowledge bases.

**6:08** · So, based on this information and what we've created, please create me another Claude MD file for that folder, which will explain the basic layout when a new knowledge base is created in its folder. Second, I've renamed the knowledge folder to be a productivity knowledge base, which is what we're going to do. And here is a basic template of what I think the Claude MD file for each knowledge base should look like, but please make suggestions and a plan for how we could make this really strong and improve on it.

**6:40** · And then what I've got is a little example of what I think it might look like. So, something like this. How it's organized, what it does. So, we're going to drop that in.

**6:48** · Okay, great. And you can work with Claude to improve this. So, giving it that Karpathy example, it said these are things that we're going to need in your Claude MD. So, I'm going to add these in. We want to make it standardized. We want to know how health checks work and when and how to ingest stuff. It's got a plan. Okay, great. I think ultimately we will set this to be active as a librarian or between active and aggressive. I think I will do this using scheduled tasks, and we'll set those up in a bit.

**7:19** · But first of all, I think the main job is to write the basic Claude MD file for how this is going to work with your best suggestions to keep it clean and simple, but powerful and effective. In terms of ingesting material, this will just be me doing this manually, but it wouldn't be unhelpful for us to add the option for you to work with me and guide me through it in a process, so you could work that in to the top level Claude MD.

**7:44** · But I would like to on the first pass of this knowledge base input a load of stuff, and then you would build the wiki from there. So let's just create the first instructions. And as for monthly health checks, we'll come to that later in detail, but this is a basic suggestion of how this might work. And I'm going to paste what I've written in, review the entire wiki directory, flag contradictions between articles, find topics mentioned, list claims not backed by source, etc.

**8:09** · Please write your proposed top level second brain MD and then knowledge base MD for the productivity knowledge base example we're building. So what I'm essentially asking you to do is based on this feedback is build me its best version, and it's informed by that Kapathy article that we showed it earlier, which was here. So it's kind of going to follow this process, and it's now building what we need. So in the second brain knowledge base, we have a top level one.

**8:40** · It's a container for multiple knowledge bases, and when it creates a new one, we ask it to do that, and this is how the system works, and how they are independent. Nice. And then the detailed behavior is for each system. That's great. Then it should be working on one in here, and now it's building this for us. So it's suggested that the top level file would have a guided ingestion mode to call on. You can see what it's up to here. Okay, it's done it, and here we go. Now what I do want to make sure I've done in my actual Claude MD, we open this up, the focused areas.

**9:12** · So list three specific themes this knowledge base will deepen. I'm going to change that. This knowledge base is focused on the ethos of doing less but better, finding a balanced approach to a greater contribution to the world, deeper thinking, and stronger output whilst managing health, happiness, and balance in your life.

**9:34** · So the themes are attention and energy management, systems design, deep work, essentialism, and effective contributions through productivity principles. Now, one question I have is whether we need a memory file that simply lists when the last action was taken so that the process that's automated knows what is new in the raw files and what is already processed.

**10:09** · Good. So, it agrees that we need a memory to make sure that it knows when it last processed something and we can add that in. This is great. We're all set. Now, of course, you can do all of this manually, but I really like the idea of this being quite automated.

**10:22** · Great. It will make that on the first pass. Excellent. Now, of course, I'm building this as I go. I'm learning it as I go, and I will share my final templated version for this linked below if you want to try it, but it will be part of Co-worker OS. So, check that out after this. So, step one is essentially that. Build that system out. And so, what we should now have is a knowledge base with the MD ready to go, which will explain how everything works. It It talks us through the process, the folder structure, and what the change log MD will be, doubling as a system's memory.

**10:56** · It talks it through how to do things.

**10:58** · You don't need to worry too much about that right now. Uh that is the plan, and you can ask Claude to do it for you.

**11:03** · We've then got our outputs, which will be things that it creates for me, raw and wiki. So, next up, \[music\] we need to do step two, which is the dump. And I think this probably, for most people, might take like 10 minutes just to find everything they currently have and put it into the raw folder. Pretty simple.

**11:18** · I'm just going to do that quite quickly.

### The Claude Build - Information Dump

**11:20** · \[music\] The issue many people miss about using a second brain \[music\] first. Now, if you've spent any time on Twitter X, you've watched the same cycle play out a hundred times. People post a screenshot of their Obsidian Vault or Notion setup, linked notes everywhere, graph views, plugins. People bookmark it, and then you kind of forget about it. And to be honest, I've tried this myself. I've built these in Notion on my computer and everywhere. This is the simplest way.

**11:50** · But this is the point about a second brain as well. We find something brilliant, we save it, and then we lose it. The fix is a second brain that actually works intelligently for you.

**11:59** · Okay, great. So next I want to uh ingest and dump all of my current knowledge on productivity into our first trial knowledge base, the productivity knowledge base. To do this, why don't you find 10 to 20 strong entries in my knowledge base in Notion, that can be found here. So what I'm going to do is jump over to Notion, go into my knowledge and research, and we've got a bunch of stuff in here. So I'm just going to give it the link to this database. So why don't we actually like view the entire database and get the link to it?

**12:29** · We'll go back in, paste that there. I may also attach a couple of files here for you. So you can of course also click this and just add files or entire folders, whatever you want to do, but we're just going to try this as a little example. And while that happens, I'll show you how that's working in customize in Claude CoWork. We can go to connectors, and I've connected up Notion, so it means that it can now go and action find and draw stuff from it.

**12:54** · So this is just an example, but it's also worth saying that in my system, I have an about me section and a context map. And that context map shows all of the key databases in Notion which it can read from. So in many ways, it should have already known that. I didn't actually have to show it, but I really like that approach to have a context map. I think try to find good examples of longer-form entries and clippings, articles, or quotes from books that have been added, rather than the AI research sets. Now while it does that, I want to say something to you.

**13:26** · You don't need to be tidy when you do this. Just copy and paste articles, notes, screenshots, meetings, transcripts into raw. You can even just paste them into the chat and get the AI to add them for you. Don't make this pretty. The point is it's a folder for capture. The organization is the AI's job, and that is why this is so nice to do. For example, here's a blog from Cal Newport on deep working. What I might do is just literally take all of that, copy it, and paste it in here.

**13:56** · Please add this from Cal Newport's deep work post. PS, when we add stuff to the raw file, you just add this as an MD file. Images can also be attached into it from me. For example, I've got a my PDF here of how to build a a gigantic business. I'm just going to take that and drop it into raw.

**14:15** · PDFs are probably harder to read. I think the AI has more trouble with that, but I'm going to put it in as a test.

**14:20** · Great, so it's fetching a bunch of stuff from Notion as an example here. Now, one little tip though, if you're doing this manually, you can use Xcode. It's a free Mac desktop app. In there, you can create markdown files. So, I've just pasted an article into one from Gretchen Rubin here and added it into the folder. So, really quickly, you've added something in. So, if you want to do that, you just are going to open Xcode.

**14:45** · You're going to do file new from template, and you just want to find markdown file. You just select that, create a new file, and you can name it, drop it in, and you're you're good to go, basically. That's how it would work.

**14:59** · So, that'd be a really quick way to manually add markdown files in. But, for a lot of people, um you'll probably be able to just share the information with Claude and get it put in. That does cost credits though. So, it's up to you how you want to do it. If you do choose to use Obsidian, they have a great web kit clipper browser extension that converts any page into a clean markdown file in one click, and that's free. So, that's worth checking out. So, here we go.

**15:23** · We've got a bunch of things in here. We've added them all as markdown files. We've got the PDF that I added. We've also got the one I added using Xcode, similar situation. And you can, of course, also just go in to your downloads folder and just drop images in. So, there's a JPEG there, which is a nice example of the process that we're working through by Corey Gamin. Cool.

**15:48** · So, we've got our raw input. Uh my Claude system also created an ingested \[music\] registry. So, it talks about when everything went in, which is useful. Okay, step three is build the wiki. This probably would take you around 30 minutes. You're going to point Claude at the folder and give it one prompt.

### The Claude Build - Create the Wiki

**16:11** · Read everything in raw and compile a wiki in the wiki folder following the rules in your Claude MD. Create the index MD first, then one MD file per major topic, and link related topics.

**16:25** · And then you basically walk away and let it do the job. What you come back to is information organized. Topic pages with summaries, connections between ideas you didn't know existed, an index that makes everything searchable in second. Now, the problem with something like Notion or Obsidian to manage a second brain for knowledge like this is that they kind of ask you to be the librarian. You organize things yourself, you make the links, you manage the tags and folders, you configure plugins, all the rest of it, and then it kind of goes by the wayside.

**16:55** · What I think Kaparthy has figured out with this approach using LLMs is that the AI becomes the librarian. You dump information in, Claude organizes and links it, summarizes it, and indexes it, and by the end it's learning and improving on its own, helping you actually apply the knowledge to output. Think what this could do for your team, your business, or just your personal output as someone exploring ideas and work. Okay, so it's working through. You'll see it's created a index.

**17:24** · It's written foundational articles, and then it's going to do method articles, thematic articles, and then write a questions MD and a change log. Now, one little tip when you get your AI to do this is to make sure that it's read your anti-AI writing style guide. Now, what that actually looks like in my world is a very similar process to what I've done in my Co-worker OS template. I have this templated in there, and it's really a writing rules MD. And this is built on the Wikipedia anti-AI writing style.

**17:56** · So, if you look up AI writing style on Wikipedia, paste that into Claude and say, "Create yourself instructions to never do any of this." It just avoids bad writing, essentially. I'm not going to go into it much further than that.

**18:09** · But, I've made sure that Claude, as it's writing its wiki, which you can see it's starting to happen here, look. We're getting all these different things. It's doing that using the writing style guide. It's also great to see here, if we just take a little look, there's loads of information going in, but it takes up so little storage. 4 KB, it's nothing.

**18:31** · Uh and this is the joy of MD files. So, let's see what it's got to. Now, I suspect you may be aware that this process is quite demanding. In order to pull this off, you are going to probably either need to do it in sessions, or you're going to want to be in Claude on a Max plan like I am. So, if we go and look in settings, let's take a little look. I've been doing other things on here, but under usage, we're 39% into my current session. And actually, great news, Claude recently announced that they are doubling usage limits across sessions and during peak hours.

**19:01** · That's not weekly limits, but it is session limits. And you can, of course, turn on extra usage, but I don't recommend it. I just got a free spend, which is nice.

**19:14** · Okay, so we have now built our first knowledge base. We've got our top-level knowledge base here. We've got a Claude MD that instructs us how to build knowledge bases and their structure and what they look like, which means that this can be a global knowledge base with lots of individual ones and we've got that. I've actually got a little memory file here, which shows us that I have a place where I keep my projects that I'm working on and this is really just a memory and a project brief brief for building a project knowledge base, so you don't need to worry about that.

**19:44** · And then this is what you've built. You've built a project knowledge base. It has a change log with the most recent entries when things have happened and it has the main Claude MD that instructs the system how to work. So when you do this, make sure you download the templates to get you started on the process from the link below. Then we have our raw, so I've got a a bunch of example raw entries.

**20:08** · They're all things that have just gone in like this and then we have our wiki, which is all of the things it's created. So it created an index, which shows the key concepts within the system so far. And then within that, we then have all of the individual entries for like specific subjects. So effortless state, energy management, habit formation. So you you see these become themes, frameworks, templated \[music\] ideas that are directed by the system.

### Creating A Compounding Loop: Self-Improvement in Claude

**20:40** · So now we need to ask it questions and get things out of it \[music\] and it's this process that actually changes everything cuz every time you ask the agent a question you like the answer to, you can then save that back into raw or into the wiki and the system gets smarter the more you use it. So each question makes the next answer better.

**21:01** · And that is because it's gone into outputs. So what we're going to do is just test this first of all. So I'm going to start a new window. I'd like to test out my new productivity knowledge base, and I have a question to ask you based on the knowledge base. What's the best way for me to balance achieving a huge amount in a short amount of time whilst managing my energy, happiness, and health? So, it's found the productivity knowledge base. It's reading the index. That's promising.

**21:29** · Reading the most relevant wiki entries.

**21:32** · This is a test. It should end up in here. It's comparing Newport, McEwen, and Burkhardt and Forte all covering this answer. You can't win both simultaneously. Trying to is what produces burnout. So, you can't do loads of work and rest. So, seven things the knowledge base says about that I can actually do. This is really cool. I really like this, and it's referencing where stuff is coming from. The test went well. The wiki had the article in every angle of your question. This is all great. Okay. So, we now need to check if it actually did an output.

**22:02** · Let's have a look. Well, it didn't. So, okay, this is great, but we should have a rule within this system, which is when I ask question, the report is generated into outputs so that we are gaining deeper insights. So, please A, update the Claude MD to ensure that this is always the case. B, turn this into a report that goes into outputs. And C, then rerun the process with this query.

**22:32** · Based on everything in the wiki, what are the three biggest gaps in my understanding of this topic? So, we go back in here. Please make sure you first reread the Claude MD for the knowledge base as I've now updated the topic focus. And I'm also going to add one more thing in here, which is write me a 500-word briefing on doing less but better using only what's in the knowledge base. Great. So, I'm going to ask that. So, we're doing a couple of things here. First of all, we're refining the system to make sure that it um always generates reports into outputs.

**23:04** · Secondly, we want to turn the report it's just created into outputs. And thirdly, I'm going to give it two further tests, uh, answering these two questions. And I'm asking it to make sure it rereads the Claude MD for the knowledge base and now I've updated the topic focus. So, if we go and take a little look at the outputs and look at what it's written for us, we can see some great results here. It's saying it's looked at all the articles and it said it has almost nothing on the journey from where most people start, overcommitted, fragmented attention, default on connectivity.

**23:35** · Cool. It's missing the mechanics of stopping and then it's got real decision method for what counts as essential. That's missing. It's missing working with other people, interestingly. It generally presumes that you're working on your own. This is really cool. So, what we could now do is go and use this to feed into the updates and improvements. And we can actually get the AI to build and improve on itself.

**24:01** · Make sure that your instructions say read the outputs and work from there. So, now I'm going to show you step five, which is the health check. And this one really matters. The AI will sometimes write something slightly wrong, you'll save it back, and the next answer quietly builds on a mistake. So, once a month you want to audit this. And the prompt is going to be something like this.

### System Health Check: Claude CoWork Scheduled Task

**24:26** · Now, \[music\] I'm going to show you in a moment how to build a scheduled task and the skill to do that. But, first let's just do this really simply. And to do it, I'm actually just going to point this directly at the folder to demo this. We're going to co-work, we're going to knowledge base and this folder.

**24:46** · So, if you just do this manually, you want to say something like this. Please review the entire productivity knowledge base wiki, flag contradictions and inconsistent data between articles, find missing data, and fill the gaps with web search. List claims not backed by a source in raw, and suggest connections between articles I haven't drawn yet, and three new article candidates. So, this is quality control. The one thing I am going to write here though is, "Please do not invoke my health check skill.

**25:18** · This is a demo of just doing it clean with this instruction." Cuz I've created a health check skill. Let's try it. And now, as this is a demo, actually please just share your results and changes in the chat. Don't edit anything currently in the wikis. I'm just going to say that as well cuz I want to you just see the kind of thing it's going to do. So, what you can see it's now doing is reading through the wiki and the system and making a complete audit of the knowledge base. Now, you would just set this going, leave it, and come back.

**25:46** · But even better, we can schedule it. And while it does that, I'll show you what that scheduled task looks like. If we go into scheduled, we now have this knowledge base monthly health check. All I did here was ask the system to create me a automated health check comprising of a knowledge base health check skill that it would create with its skill creator plugin. And it basically says, "Go through and do the things that we've just asked for based on the skill."

**26:15** · You can set this up so that it runs on different times. But interestingly, you can have a custom schedule. So, if you ask it when you speak in the chat to build you a skill that is monthly, it can do that. Uh not just follow the options that are in the selectors. And that's it basically. It's ready to go.

**26:35** · And you can get it to act without pausing for approval if you want. That's an option. So, I'm going to save that for now. And then if we go into customize, I've also created in skills this knowledge base health check skill. And this will work its way through the process. And it does it in two phases.

**26:55** · It has a first order in file process where it reads my writing rules guide for anything that it's going to write.

**27:00** · It reads the change log, the wiki, and what's been ingested, as well as the outputs that have been created since the last last health check. And then it runs a seven-stage audit. And the seven stages are these: contradictions, broken backlinks and orphaned references, source provenance, coverage that the raw files have, stale articles, anything that's out of date, older than 90 days and not relevant, and suggested new articles. And then this is a report template of how it gives a report.

**27:30** · And then it has a second phase, which is if you're doing this interactively, if you're actually directly asking for it, it will also ask which findings to action and ask user question. So, it means you can kind of go through it fully and then fully uh commit it. In the phase one, it will just give us a report that we can then ask to be actioned later on. Now, I'm creating a templated version of this for you guys so you can just download it via the link in the description and use it.

**27:54** · But for now, let's go and see what our example is up to. And here is our audit. Let's see what it says. Effort versus effortlessness, our contradictions, inconsistent numbers and framing, nice.

**28:07** · It's cleaning up attribution drift, unsourced and under-sourced claims, building a second brain, mood first productivity, it's not captured the link, habit formation, so on and so forth, gaps the wiki has, there's no underlying research for the cathedral effect, we don't have the book, an unprocessed file that we haven't ingested, great. That's something I added recently, an unaccounted JPEG, and then it's found some really interesting connections that we might not have seen.

**28:36** · So, quick verdicts. It's unusually clean for an early-stage knowledge base. All looks pretty solid. Main weaknesses: attribution, unprocessed raw files, not uh naming the underlying study, philosophical contradictions. Okay, great. We'll leave this here as I'm now going to start a new session and compare this with my skill and triggered scheduled task to see how the results compare. So, now we're going to start again and let's run my scheduled task.

**29:03** · So, we can actually go to scheduled, click into the scheduled task and click run now. As simple as that. Now, if we go into the knowledge base, so you can see it's now um implement the the knowledge base health check skill. It's following that now and reading my writing rules. These are anti-AI writing rules. We can see that it's going to have checked the latest uh item in the change log.

**29:28** · So, these are the latest updates. It's working chronologically. It's then going to read through all of the other files and we should see it now work. So, let's let that run and see what we get back. Oh, and if you're interested in this item here, push summary to BriefBuddy, I've actually created myself a little reporting app that is automatically updated and turns up on my phone. You don't need to do this.

**29:50** · Uh the system will just essentially uh you'll see when the scheduled task has run, you'll see a little um blue dot for something and you can go and look at that and find the report and the brief. So, this for example is another scheduled task that I'm running and essentially draft stuff so I can go and look at them and work on it. So, when this goes blue, we'll be ready to see what's happened. Okay, great. So, that took it about 12 minutes. Now, it is worth remembering that this probably is going to cost a few credits to do it.

**30:17** · That's why I'm only scheduling this to be monthly and you might want to do it for each knowledge base you build on a different day so you don't just use all your credits up, but it's a really useful thing to be doing to make it powerful.

**30:28** · So, we can see it turned up. You don't really need anything more than that. If you come into Claude, you'll see that this has happened and we can click on it in either position. We can go in and take a look and we can see it's completed it. It's run that. It's filed a report, the brief buddy thing I'll need to problem solve, but to be honest with you, I don't really need it to do that. And it will show them to us here, but we can just go over to our folders to see what's happened. The change log, first of all, will have been updated today. There you go, health check first run. And it's reported on what's happened. So, the system will know where it's at. That's great.

**31:00** · And then in outputs, we can see here is our health check. There you go, we've got the wiki is unusually well aligned, it's done a similar thing. New candidates, so it's gone through and looked at the issues and discoveries, no stale articles.

**31:15** · It's cleaned up some banned words, American spelling, and then we've got suggested new articles. This is probably where the real value is. So, it's suggesting we look at collaborative productivity, good habit rest recipes, looking at B BJ Fogg, interesting. And we've got effort versus effortlessness, making the frame easy accepting strain inside, interesting. And then it's got an action menu. So, for phase two, things that it could run. And we could now ask it to run those things, and we will get that automatic update.

**31:45** · So, this is a reasonably like in-depth process. You could always simplify it. It really comes down to what you want to do. But, check out the templated options in the description, and you can take it from there. Or, if you're downloading my Co-worker OS, it will be baked in. So, as a final example here, I'm going to get it to actually update.

**32:05** · Please see the latest health check in your productivity knowledge base, and run the action list from it on that knowledge base. Now, what you can see is it's it's written itself a great list, it's applying the writing rule fixes, it's adding the new stuff to ingest, drafting the new articles, and then it's going to update everything, which is great. It's worth saying, I think for most people, once you've tested it in these two stages, it's quite easy for you just to have it automatically do it. So, you could just say, just do the work. Report and action. I think that's better.

**32:35** · And potentially, you kind of refine your instructions to make it rigorous but not cost you loads and loads of credits. As an example, for the example that we've run, so the first one I did without the skills, then the one with the skill, and this, the usage of my Max plan for this current session is at 45%. That's on a 5x Max plan, so that's a significant use of credits. But once a month, for a really powerful knowledge base, not too bad. Let me know in the comments how you feel about that.

**33:05** · And here we go, we've got the results. It's created new articles on habit receipts, working with others, and effort versus effortlessness into the gaps that were missing. It's updated the index questions and change logs, and they're all ingested, which is really cool. It's given me a bit of feedback about some web search stuff, and then it's created the documents. And if we go and check out the files, we'll see the new items have been ingested.

**33:34** · And the new entries in the wiki have been added, which is great.

### Final Results

**33:42** · So it should be that we now get a very different result. So if we ask, in a new task, "Take a look at the productivity knowledge base and give me a report on how I can balance making serious and useful effort versus making my week and days feel effortless in how I contribute to my life." These are just examples, right? But let's just drop it in and see what it gives us. And it's created it.

**34:06** · Now annoyingly, it's not presented it to me. "Please can you update your Claude MD files and the templated one for knowledge bases so that any report that's created in response to a question is presented as a clickable page to open in the chat."

**34:23** · Great, there we go. And it's now shown it to me, so I can actually click on it and read it. And this is what it's given us, a little report. Now here's a nice little tip, if you ever want to make your learning easier when you're doing this, I use Speechify to read things back to me so I can just do control option A and it reads it.

**34:40** · The question: How can I balance making serious and useful effort versus making my week and days feel effortless and how I contribute to my life?

**34:47** · Those are the five steps to \[music\] building, refining, and using a knowledge base that learns as it goes.

### The 1 Day vs 100 Day Transformation To Aim For

**34:56** · So, here's the bit you need to remember to \[music\] take away with you. Day one of running this, your knowledge base isn't going to do loads. It's got whatever you dumped in over the weekend, useful but not revolutionary. But day 100, then you've actually built something valuable. Every meeting transcript that mattered, every answer you've saved back into the system becomes a carefully curated, cross-referenced, linked, and summarized set of information that you can query with the librarian themselves.

**35:22** · And it's that kind of asset that's nearly impossible to replicate because nobody else has read what you've read or saved what you've saved. So, if you only do one thing from any video I make this year, do this. It's 45 minutes on a Saturday morning and you'll thank yourself in 3 months. One last thing, everything we built today, the folders, the Claude MD, the prompt, the health check, they all ship inside the final version of my Claude Co-worker OS when it comes out. It's in beta as I film this and you can download it right now.

**35:54** · It's been brilliantly received so far. The whole point of it is to help you skip past the fiddly setup bits and land on a working Claude environment faster than most people manage on their own. It's been a game-changer for me and a lot of others using it. And of course, you can watch the video that shows you exactly how to do all of that right here. I'll see you on the next one. Bye.