# Iterating towards roadmap

**Date:** 2026-06-17
**Start:** 2026-06-17T09:00:00.000Z
**End:** 2026-06-17T10:00:00.000Z

---

WEBVTT

00:00:03.160 --> 00:00:03.440
<v Rob Zinkov>Okay.</v>

00:00:10.080 --> 00:00:12.560
<v Rob Zinkov>So, so Jan, what are we discussing in this meeting?</v>

00:00:14.320 --> 00:00:24.920
<v Jan Hoffmann>Okay, two things. One is maybe, Michal, you can run that is getting some data from the...</v>

00:00:27.440 --> 00:00:31.880
<v Jan Hoffmann>from the recordings that we do and the transcripts of the...</v>

00:00:33.360 --> 00:00:46.720
<v Jan Hoffmann>face-to-face sessions, how we can access that, and how we can also get our hands on the QA rating of some of the...</v>

00:00:48.000 --> 00:00:50.960
<v Jan Hoffmann>some of the session recordings.</v>

00:00:53.120 --> 00:01:05.920
<v Jan Hoffmann>I think that's the first bit that we should talk to with Dainis. And then I would like to get an update on what you guys discussed yesterday in the mobile app.</v>

00:01:08.480 --> 00:01:17.840
<v Jan Hoffmann>Meeting, because apparently some something what Srikant calls a roadmap was discussed, and...</v>

00:01:19.040 --> 00:01:21.280
<v Jan Hoffmann>It's I'm.</v>

00:01:22.520 --> 00:01:29.520
<v Jan Hoffmann>Get me on board, please. Bring me up to speed on that. And then we should have a look at what we have in the current.</v>

00:01:32.080 --> 00:01:51.040
<v Jan Hoffmann>in the plan or in the milestone thingy project, whatever you call that in GitHub. And maybe we also can have, that's probably something that I'll share afterwards. I've made a PRD with the new PRD skill and.</v>

00:01:51.120 --> 00:02:11.080
<v Jan Hoffmann>a bunch of data that I put into the repository for it to chew on. And I have an output which is many, many pages long. I'm still reviewing it. So I don't know if it's any good or not. Like it's okay.</v>

00:02:11.280 --> 00:02:19.880
<v Jan Hoffmann>Ish, and it it yeah pulled a lot of data, but it also pulled some not so right things, and...</v>

00:02:21.520 --> 00:02:22.880
<v Jan Hoffmann>Yeah, we'll have to see.</v>

00:02:26.200 --> 00:02:28.400
<v Jan Hoffmann>Okay, but with that, Michal, do you want to start?</v>

00:02:29.240 --> 00:02:50.200
<v Michal Sobocinski>Yeah, of course. Peace of all, Dainis. Thank you for joining this meeting to put here in the context that we are working, or we want to have all of the knowledge about the content inside the Berlitz company, and what we get the meetings with LMS, Pat, and with...</v>

00:02:50.280 --> 00:03:09.160
<v Michal Sobocinski>The hyperwave, if I'm in front, and now when we spoke with the Martin, I think so was he tell us that he has like the access to recording session with the students and with the transcriptions of these sessions and that.</v>

00:03:09.680 --> 00:03:28.960
<v Michal Sobocinski>you and him working on something to analyze like the feedback from these transcriptions or maybe from video 2 and we want to do something similar that we want to have the access to these transcriptions and videos and check what what the progress of the.</v>

00:03:29.760 --> 00:03:48.480
<v Michal Sobocinski>student is, what he or she can improve or whatever and maybe with the videos to check the pronunstations or other matters that we can improve, right? And I don't know if you can give us the access to this information and other part.</v>

00:03:46.080 --> 00:03:46.560
<v Dainis Tkacovs>Mhm.</v>

00:03:48.880 --> 00:04:07.600
<v Michal Sobocinski>what you are doing in your part of the AI chat box or chat or bot or something like that. Then Martin explained it to me and maybe we can, I don't know, work together or get the information or not to work with the times or enjoy our experience or something like that.</v>

00:04:09.920 --> 00:04:18.960
<v Dainis Tkacovs>Okay, you just a quick first question. You're looking on this all from the learners or students experience perspective mostly, right?</v>

00:04:20.800 --> 00:04:24.360
<v Michal Sobocinski>About right, Jan, that user.</v>

00:04:23.920 --> 00:04:35.120
<v Jan Hoffmann>Yeah, I would say there's probably a little bit of a focus on the learner at the moment, but ultimately it's the whole thing, including teachers.</v>

00:04:34.560 --> 00:04:35.040
<v Dainis Tkacovs>Mhm.</v>

00:04:37.120 --> 00:05:00.640
<v Dainis Tkacovs>Yeah, because we usually try to distinguish really these two parts and analysis of either transcripts or recordings to get some specific information. It will be really, really different depending on what's the use case. It's either to improve instructor daily work or their personal skills or give them feedback or it's for learners or students experience improvements.</v>

00:05:01.040 --> 00:05:19.440
<v Dainis Tkacovs>These are kind of bit different things. And what I'm working on with this agent, with Martin and QA team, is specifically for evaluating instructor performance and how was the lesson delivered? Was it delivered by plan? How was instructor performing in terms of...</v>

00:05:20.800 --> 00:05:40.480
<v Dainis Tkacovs>skills used by instructor to deliver a lesson and so on, and also to evaluate by specific scoring through specific standards. And essentially this agent can do that. There are multiple aspects I will mention in a moment, but in general, yeah, this is a</v>

00:05:40.640 --> 00:05:59.520
<v Dainis Tkacovs>instructor focused and QA teams agent that helps them with their daily work, which they are doing right now manually. As you understand, there are thousands of thousands of lessons and they need to keep an eye and have a quality control over these lessons and instructor performance.</v>

00:05:59.680 --> 00:06:18.800
<v Dainis Tkacovs>to understand where might be some improvements. And now they're doing all of that manually. Until now, they were doing that all manually by just reading transcripts, checking the recordings with their own eyes, yeah, and evaluating. And of course, they were using a specific evaluation system or scoring system.</v>

00:06:19.120 --> 00:06:38.160
<v Dainis Tkacovs>right? But all of that happens without any AI agents, automations, or anything. And now they have this agent that is built on the Microsoft Copilot Studio. I built it a few months ago and we were testing it a lot. And the idea of this agent is that instructor</v>

00:06:39.040 --> 00:06:57.160
<v Dainis Tkacovs>sorry, QA team or Martin and his colleagues are downloading manually right now transcripts from Zoom backend, which is quite simple, just a few clicks away. And they need to upload this transcript to this AI agent, which is available through Microsoft Teams as a channel.</v>

00:06:57.280 --> 00:07:15.960
<v Dainis Tkacovs>Agent can be available in various different channels, but for relevance and convenience for colleagues, it's specifically on Microsoft Teams available. They upload this transcript and just ask, evaluate. An agent does the job. Agent is already trained on specific knowledge base that was created by Martin's team that is exact.</v>

00:07:16.160 --> 00:07:37.440
<v Dainis Tkacovs>description of all these relation and scoring system points that they're using manually, right? And additionally, agent is trained to use this system specifically to go through all the transcript and evaluate and score it. We had multiple iterations to improve this agent's performance, and now it's close to.</v>

00:07:37.480 --> 00:07:57.120
<v Dainis Tkacovs>perfect, I would say. There are just some minor things here and there from time to time that we adjust, but overall it's quite perfect. And the testing went side to side with manual testing. So we were giving agent to analyze some transcripts from actual lessons.</v>

00:07:54.240 --> 00:07:54.480
<v Jan Hoffmann>Bye.</v>

00:07:57.600 --> 00:08:14.800
<v Dainis Tkacovs>And then someone from Martin's team in parallel were evaluating these lessons manually. And then they were comparing this analysis and results by latest iterations were 90, I don't know, 7 or 8% close, something like that, which is quite good. And</v>

00:08:14.480 --> 00:08:28.800
<v Rob Zinkov>Is the date, where is the data, where does this data live that was done by hand versus the agent done in the comparison? Like where, where is all the, where is all that stuff?</v>

00:08:23.760 --> 00:08:23.840
<v Dainis Tkacovs>In.</v>

00:08:26.880 --> 00:08:27.280
<v Dainis Tkacovs>Yeah.</v>

00:08:29.600 --> 00:08:51.200
<v Dainis Tkacovs>Yeah, I think it's an important question to cover. First of all, we have to understand that in Berlitz, we are using two platforms to deliver lessons, which is Zoom primary, and secondary platform is Microsoft Teams. Most of the lessons are delivered through Zoom. And first of all, for first 15 days,</v>

00:08:43.640 --> 00:08:44.120
<v Rob Zinkov>Mhm.</v>

00:08:52.640 --> 00:09:10.400
<v Dainis Tkacovs>from the recording, from the lesson date, recordings and transcripts live on Zoom Cloud or Zoom backend before these recordings and transcripts are being copied to our own AWS servers. And later these recordings are available through either</v>

00:09:10.640 --> 00:09:29.520
<v Dainis Tkacovs>portal, student or instructor portal, no, student portal, or Salesforce directly. And usually technical support team or customer support team are accessing these recordings there. After 90 days of total period, everything is deleted by GDPR requirements. And</v>

00:09:14.160 --> 00:09:14.720
<v Rob Zinkov>Mhm.</v>

00:09:17.200 --> 00:09:17.600
<v Rob Zinkov>Yeah.</v>

00:09:20.000 --> 00:09:20.480
<v Rob Zinkov>Right, right.</v>

00:09:29.920 --> 00:09:48.720
<v Dainis Tkacovs>So first 15 days, the recordings and transcripts live on Zoom and are available through Zoom backend. Just before this meeting, I sent an invitation to all of you guys to create your own profiles on Zoom. As soon as you will do that, please let me know.</v>

00:09:49.760 --> 00:09:59.760
<v Dainis Tkacovs>And I will assign you a specific role so you can actually access these recordings and transcripts and see yourself how is that available there.</v>

00:09:55.360 --> 00:09:55.680
<v Rob Zinkov>Right.</v>

00:09:59.120 --> 00:10:07.200
<v Rob Zinkov>So are the are the transcripts also deleted after 90 days or just the videos?</v>

00:10:08.000 --> 00:10:13.280
<v Dainis Tkacovs>No, it's supposed to be everything because transcripts are attached to videos.</v>

00:10:13.840 --> 00:10:14.320
<v Rob Zinkov>Okay.</v>

00:10:14.960 --> 00:10:17.040
<v Dainis Tkacovs>Yeah, so, so that's a policy.</v>

00:10:15.920 --> 00:10:32.800
<v Rob Zinkov>So the transcripts are also, so okay. You talked about doing an analysis, kind of comparing what the LLM sort of thought of the lesson versus what a human sort of thought of the lesson, right?</v>

00:10:33.600 --> 00:10:34.680
<v Dainis Tkacovs>I correct.</v>

00:10:35.120 --> 00:10:42.480
<v Rob Zinkov>Are those human evaluations stored anywhere that we can see?</v>

00:10:43.360 --> 00:11:00.400
<v Dainis Tkacovs>Oh yeah, probably that's something we can ask from Martin. I'm not sure how they managed this process of manual evaluation. Probably I assume they would share these evaluations somewhere on SharePoint on their Teams folders.</v>

00:11:00.960 --> 00:11:01.600
<v Rob Zinkov>Okay.</v>

00:11:01.360 --> 00:11:04.080
<v Dainis Tkacovs>Nothing fancy, I believe. Yeah.</v>

00:11:04.960 --> 00:11:10.560
<v Rob Zinkov>So how was the agreement done? Was that done manually? So when you say there was sort of high agreement.</v>

00:11:11.640 --> 00:11:13.040
<v Rob Zinkov>How was that done?</v>

00:11:14.320 --> 00:11:17.120
<v Dainis Tkacovs>Oh, you mean the manual process before the AI agent?</v>

00:11:17.480 --> 00:11:26.320
<v Rob Zinkov>No, no, no, no. You're saying that you compared how the AI did it, and you compared how the people did, and you said they agreed. How was that comparison done?</v>

00:11:22.080 --> 00:11:22.480
<v Dainis Tkacovs>Yeah.</v>

00:11:27.120 --> 00:11:46.560
<v Dainis Tkacovs>That was, that comparison was done exactly by the team, by the same Martin team who evaluated these lessons. So there were a couple of colleagues who on a regular basis performed manual analysis and scoring, and then other colleagues tried to do same with same transcripts.</v>

00:11:27.680 --> 00:11:27.800
<v Jan Hoffmann>Yeah.</v>

00:11:34.560 --> 00:11:35.200
<v Rob Zinkov>Okay.</v>

00:11:46.640 --> 00:11:52.640
<v Dainis Tkacovs>about through AI. And then they compare it to documents side by side. And that's about it.</v>

00:11:50.880 --> 00:11:55.840
<v Rob Zinkov>Right, right, who are some of these people, like, just to like have some names?</v>

00:11:56.880 --> 00:11:57.840
<v Dainis Tkacovs>Ohh, mm.</v>

00:12:00.320 --> 00:12:18.880
<v Dainis Tkacovs>Martin, probably, maybe Jose from his team. I don't know, but probably the best idea would be ask Martin because I was working with him directly and from that point he was working with his team. I'm not sure or I don't have information how he delegated the.</v>

00:12:01.920 --> 00:12:02.480
<v Rob Zinkov>Okay.</v>

00:12:05.680 --> 00:12:06.240
<v Rob Zinkov>Okay.</v>

00:12:19.520 --> 00:12:20.880
<v Dainis Tkacovs>This further, yeah.</v>

00:12:19.600 --> 00:12:20.160
<v Rob Zinkov>Okay.</v>

00:12:22.800 --> 00:12:23.520
<v Rob Zinkov>All right.</v>

00:12:24.320 --> 00:12:44.560
<v Dainis Tkacovs>Yeah, so that's about the manual process. About the process, how it works right now through the agent, well, essentially the initial idea was a little bit more sophisticated or complicated to make this process even easier, but due to...</v>

00:12:25.760 --> 00:12:26.440
<v Jan Hoffmann>No.</v>

00:12:45.200 --> 00:13:05.680
<v Dainis Tkacovs>some technical limitations on processes as follows. So first of all, instructors do the usual job. They open Zoom backend, as we call, and they find the necessary lesson by using instructors' email in a search bar of finding some specific recordings and transcripts.</v>

00:13:06.080 --> 00:13:24.560
<v Dainis Tkacovs>Then they find all the all of the lessons, past lessons under the specific instructor. They scroll down, find the real data they need, they open, and they click on download transcript. And it downloads transcript in a BTT format, which is kind of text format, but with the</v>

00:13:25.120 --> 00:13:43.920
<v Dainis Tkacovs>with specific timelines for every phrase or who spoke and something like that, but it's not essentially clean TXT file. And the problem is that on Microsoft Copilot Studio, there's certain file tabs that are accepted by these agents to upload and</v>

00:13:44.320 --> 00:14:03.120
<v Dainis Tkacovs>these agents can actually view. And TXT, PDF, Word, Excel are core type of the files that this agent can read. So essentially we need some workaround. And right now, Team is manually converting these files from VDD to TXT to.</v>

00:14:03.600 --> 00:14:25.840
<v Dainis Tkacovs>some like ChatGPT or Gemini, just chat interface, that's quite easy to do now. But essentially the idea was to build another process for this agent on the background that would use some Power Automate tools to still accept this VTT file and convert it on the background into TXT and then start analysis.</v>

00:14:26.240 --> 00:14:47.400
<v Dainis Tkacovs>But that's kind of complicated to establish for current setup. And right now they're doing this first part manually. So once the files are converted manually, they upload these TXT files and agent is evaluating the lesson based on the knowledge base where it stored all information about the scoring system.</v>

00:14:47.920 --> 00:15:07.840
<v Dainis Tkacovs>and how evaluation must be done exactly. And then there is our custom instructions for the agent to describe how exactly this knowledge base material must be used, what are expected the results, if there are any follow-up questions from the user or anything else. And it takes like maybe up to</v>

00:15:08.240 --> 00:15:27.760
<v Dainis Tkacovs>30 seconds, 45 seconds, and the agent gives the answer, really long answer, like a long document, with everything described, with the recommendations what to improve, and the end score. And then they're able to save this as a sort of copy in.</v>

00:15:27.880 --> 00:15:45.680
<v Dainis Tkacovs>in just copy and paste in some document or download as a PDF, for example, and that's about it. Right now, this agent is available, as I mentioned before, on Microsoft Teams as a separate agent, and it's available specifically for Martin's team because on...</v>

00:15:47.120 --> 00:16:07.960
<v Dainis Tkacovs>When we are launching agent, we can specifically allow this agent to be available for specific groups or people or specific people based on how we set up that on Office 365 settings. Yeah, that's about it shortly. Do you guys maybe have any additional questions or comments?</v>

00:16:10.800 --> 00:16:30.360
<v Jan Hoffmann>I have some comments here because there is similar stuff is going on all over the place right now, or related stuff. There is, Nicole has invited for next Wednesday for a workshop.</v>

00:16:30.480 --> 00:16:43.760
<v Jan Hoffmann>With Henning, actually, on what kind of data we would like to get out of the sessions in the future in the future for analysis, so I'm not 100% sure why.</v>

00:16:40.280 --> 00:16:40.480
<v Dainis Tkacovs>Mm.</v>

00:16:42.800 --> 00:16:43.200
<v Dainis Tkacovs>Okay.</v>

00:16:45.120 --> 00:17:03.760
<v Jan Hoffmann>Why the group of product ops is looking into this? That I have to find out. And it's interesting to, in that context, to see what we currently can get out of the live sessions.</v>

00:17:04.240 --> 00:17:15.440
<v Jan Hoffmann>And then we'll have to build it so that similar information also comes from the mobile app in the end.</v>

00:17:04.560 --> 00:17:05.040
<v Dainis Tkacovs>Mhm.</v>

00:17:16.160 --> 00:17:16.640
<v Dainis Tkacovs>Mhm.</v>

00:17:17.280 --> 00:17:19.280
<v Jan Hoffmann>Um, and it's...</v>

00:17:20.400 --> 00:17:28.160
<v Jan Hoffmann>Great to know that you have worked on this stuff already, and I would really like to.</v>

00:17:27.360 --> 00:17:28.480
<v Rob Zinkov>Less stuff for us to do.</v>

00:17:29.520 --> 00:17:50.160
<v Jan Hoffmann>Yeah, what's exactly, what's left to do? And well, yeah, and what's left to do short term is to have a look at it, right? I mean, this is, I think Martin is pointing your way and you're pointing back to Martin. We have to find out where the data is being stored.</v>

00:17:30.480 --> 00:17:31.360
<v Rob Zinkov>Well, hopefully.</v>

00:17:50.800 --> 00:18:12.920
<v Jan Hoffmann>get our own idea of where that is and how accurate it is. Beyond 90% to me sounds almost too good to be true. I mean, get 2 humans to agree on the rating for one session. I don't think you have agreement of 95%.</v>

00:17:55.760 --> 00:17:56.240
<v Dainis Tkacovs>Mhm.</v>

00:17:59.920 --> 00:18:00.400
<v Dainis Tkacovs>Mhm.</v>

00:18:10.800 --> 00:18:11.040
<v Rob Zinkov>Oh.</v>

00:18:14.800 --> 00:18:16.560
<v Jan Hoffmann>But maybe, yeah, maybe it is.</v>

00:18:15.520 --> 00:18:17.840
<v Rob Zinkov>I mean, if the rubric is clear enough.</v>

00:18:16.400 --> 00:18:36.800
<v Dainis Tkacovs>Well, well, yeah, well, the scoring system is super clear. It's like, if it's super clear for a human and probably for LM, it will be also pretty clear and really, really standardized. There's no like that humans when they analyze like, oh, I feel like I should evaluate this in a different way. There's no such thing. So</v>

00:18:21.520 --> 00:18:21.720
<v Jan Hoffmann>Yeah.</v>

00:18:28.680 --> 00:18:29.040
<v Jan Hoffmann>Right.</v>

00:18:35.640 --> 00:18:35.760
<v Jan Hoffmann>Yeah.</v>

00:18:37.120 --> 00:18:42.480
<v Dainis Tkacovs>So it's possible that AI can evaluate really, really close to reality in this case.</v>

00:18:43.200 --> 00:19:01.000
<v Rob Zinkov>Yeah. I don't know if you're the best person to ask this, but it's like, apparently it's one of our responsibilities to sort of track. Jan, I don't know. Please confirm if I'm wrong here. I think part of our responsibility is also tracking AI spend. What?</v>

00:19:01.440 --> 00:19:08.320
<v Rob Zinkov>How, how was the LLM access mediated? Like, who's who's paying to call the LLM?</v>

00:19:10.400 --> 00:19:27.680
<v Dainis Tkacovs>This particular license that I'm using for MS Copilot Studio costs like around $5,000 a year. And it's sponsored by Global Live Global Operations or Henning team specifically. And</v>

00:19:19.040 --> 00:19:19.440
<v Rob Zinkov>Okay.</v>

00:19:25.760 --> 00:19:26.400
<v Rob Zinkov>Okay.</v>

00:19:29.440 --> 00:19:48.000
<v Dainis Tkacovs>We have 10,000 messages or tokens included every month across all the agents, and now the usage is not even closed, but that was the minimum license we could have. If we want to upgrade, if we will have a bigger usage, then of course we can we can buy more tokens on on on the on the monthly basis, right?</v>

00:19:34.240 --> 00:19:34.800
<v Rob Zinkov>Okay.</v>

00:19:48.280 --> 00:19:55.040
<v Dainis Tkacovs>But right now, I think it's a relatively cheap solution that we are using right now.</v>

00:19:53.840 --> 00:19:54.240
<v Rob Zinkov>Yeah.</v>

00:19:55.680 --> 00:20:03.520
<v Rob Zinkov>Yeah, I this is just like ident sort of just identify like where these things are happening because like it's</v>

00:20:03.120 --> 00:20:04.800
<v Dainis Tkacovs>Absolutely understandable, yeah.</v>

00:20:05.720 --> 00:20:17.120
<v Rob Zinkov>You know, Microsoft regularly is like, yeah, we're going to change our pricing now. So it's good to just kind of know where, whose budget it's coming from and things like that is also very useful to know. Okay.</v>

00:20:05.840 --> 00:20:06.320
<v Dainis Tkacovs>Yeah, yeah.</v>

00:20:17.160 --> 00:20:37.360
<v Dainis Tkacovs>Yeah, yeah, yeah. So as mostly internal agents for internal purposes are being created from Microsoft Copilot Studio, then my estimates are not that high from the usage perspective. I don't think in the nearest time we will reach internally 10,000 messages a month.</v>

00:20:38.320 --> 00:20:38.480
<v Rob Zinkov>Mm.</v>

00:20:38.320 --> 00:20:57.400
<v Dainis Tkacovs>But when it comes to start delivering and creating agents for students or instructors, we have more than 700 instructors and God knows how many students, then that probably this environment wouldn't be sufficient. We would need to think about something else.</v>

00:20:58.000 --> 00:20:59.680
<v Dainis Tkacovs>Yeah, but so far so good.</v>

00:20:58.320 --> 00:20:58.600
<v Jan Hoffmann>Yeah.</v>

00:21:00.880 --> 00:21:06.480
<v Jan Hoffmann>But, Dainis, can you, can you show, can you show how it works?</v>

00:21:07.680 --> 00:21:08.240
<v Dainis Tkacovs>Ohh.</v>

00:21:09.000 --> 00:21:09.840
<v Jan Hoffmann>Back to you.</v>

00:21:09.360 --> 00:21:23.280
<v Dainis Tkacovs>Probably I need to have a transcript first from some lessons. I don't know, maybe we could invite Martin because he was usually doing these evaluations. I was building and testing.</v>

00:21:24.400 --> 00:21:26.240
<v Dainis Tkacovs>Um, I'm not sure if Martin is online.</v>

00:21:31.520 --> 00:21:34.960
<v Jan Hoffmann>Well, he lives even further east than you, doesn't he?</v>

00:21:34.400 --> 00:21:36.680
<v Dainis Tkacovs>Is in Japan, yeah, in Tokyo, I think.</v>

00:21:36.240 --> 00:21:36.400
<v Jan Hoffmann>We.</v>

00:21:38.400 --> 00:21:48.160
<v Jan Hoffmann>I actually, like, I shared with you guys yesterday with Michal and Rob. I shared a transcript, so...</v>

00:21:49.600 --> 00:21:50.480
<v Jan Hoffmann>Can Alfonso.</v>

00:21:52.000 --> 00:21:53.040
<v Jan Hoffmann>I can pick that up.</v>

00:21:55.560 --> 00:21:55.680
<v Jan Hoffmann>Yeah.</v>

00:21:59.440 --> 00:22:00.960
<v Dainis Tkacovs>Um, Michael, you are muted.</v>

00:21:59.920 --> 00:22:00.040
<v Jan Hoffmann>Dev.</v>

00:22:00.160 --> 00:22:04.640
<v Rob Zinkov>Michal, you're muted, as I said, while also being muted.</v>

00:22:01.040 --> 00:22:02.800
<v Michal Sobocinski>Yeah, yeah, yeah, yeah.</v>

00:22:01.120 --> 00:22:01.280
<v Jan Hoffmann>Yeah.</v>

00:22:05.680 --> 00:22:05.840
<v Michal Sobocinski>Yeah.</v>

00:22:05.880 --> 00:22:06.160
<v Jan Hoffmann>But.</v>

00:22:08.320 --> 00:22:23.600
<v Michal Sobocinski>Maybe we can try with this transcript, right? Yeah, I don't know if you can share this transcript with that, and yeah, and I understand that for now we only evaluate the instructor part, right? Not learner part.</v>

00:22:08.480 --> 00:22:09.080
<v Rob Zinkov>Good, good friend.</v>

00:22:14.600 --> 00:22:17.920
<v Jan Hoffmann>From yesterday, as I showed it, yeah, that.</v>

00:22:19.920 --> 00:22:20.040
<v Jan Hoffmann>And.</v>

00:22:22.240 --> 00:22:22.560
<v Jan Hoffmann>Yeah.</v>

00:22:23.280 --> 00:22:42.640
<v Dainis Tkacovs>Yes. Like lesson quality part, yeah, yeah. Of course, there are certain aspects where it's important how students react or something like that, but that's not the core purpose to improve, I don't know, a learner experience. One note here, I think it's important to mention</v>

00:22:27.040 --> 00:22:27.600
<v Michal Sobocinski>Yeah, yeah.</v>

00:22:43.520 --> 00:23:01.560
<v Dainis Tkacovs>that previously you guys mentioned the analysis of the video possibly or some other data, which was essentially our idea too, because that would help us to evaluate even better because for such thing like delivering a lesson.</v>

00:23:01.680 --> 00:23:18.880
<v Dainis Tkacovs>face to face with the video cameras on, it's important to understand facial expressions, emotions, feelings, gestures, everything. But unfortunately, by understanding how large volume of these lessons we have and how</v>

00:23:20.080 --> 00:23:41.200
<v Dainis Tkacovs>how are tools designed right now to evaluate actual video files, that would be highly expensive and complicated to set up at this moment, at least at this moment, because video analysis is something else and this is not possible with tools that we currently have or even if we...</v>

00:23:41.280 --> 00:23:51.600
<v Dainis Tkacovs>would be, it would probably cost us a bunch of money even to just evaluate a couple of videos. So this is something still in the books, I believe.</v>

00:23:52.840 --> 00:23:55.920
<v Dainis Tkacovs>to understand how we possibly do that or no.</v>

00:23:58.800 --> 00:24:07.680
<v Jan Hoffmann>Yeah, I mean, that's a nice add-on, I think, and in general, for the whole experience, having...</v>

00:24:09.080 --> 00:24:11.520
<v Jan Hoffmann>Gestures in there somehow.</v>

00:24:12.680 --> 00:24:27.200
<v Jan Hoffmann>Like, not only in the analysis, but also in the for the avatar, for example, let me like this is it doesn't let me upload it right now, Team doesn't, so wait.</v>

00:24:25.280 --> 00:24:25.680
<v Michal Sobocinski>No.</v>

00:24:26.760 --> 00:24:30.800
<v Michal Sobocinski>Maybe you send this to Dainis directly, because...</v>

00:24:31.440 --> 00:24:33.520
<v Dainis Tkacovs>Teams doesn't allow you? Weird.</v>

00:24:34.720 --> 00:24:36.640
<v Dainis Tkacovs>Should, because Martin.</v>

00:24:34.800 --> 00:24:36.160
<v Jan Hoffmann>Yeah, let me, let me.</v>

00:24:38.560 --> 00:24:43.280
<v Jan Hoffmann>So, there is more, there is the thing, and...</v>

00:24:44.480 --> 00:24:49.360
<v Jan Hoffmann>I did forward it to you, the two of you, didn't I, yesterday?</v>

00:24:52.400 --> 00:24:53.680
<v Jan Hoffmann>Maria Munoz.</v>

00:24:58.080 --> 00:24:59.360
<v Michal Sobocinski>To check it.</v>

00:25:03.280 --> 00:25:08.640
<v Jan Hoffmann>At least I meant to. Maybe I didn't in the end.</v>

00:25:03.440 --> 00:25:03.840
<v Michal Sobocinski>And.</v>

00:25:08.000 --> 00:25:10.000
<v Michal Sobocinski>Yeah, yeah, Maria, on your, yeah, I see that.</v>

00:25:10.960 --> 00:25:12.160
<v Jan Hoffmann>Yeah, okay.</v>

00:25:12.160 --> 00:25:13.440
<v Rob Zinkov>Where am I looking?</v>

00:25:15.600 --> 00:25:15.840
<v Jan Hoffmann>Hmm?</v>

00:25:16.480 --> 00:25:17.440
<v Rob Zinkov>What am I looking for?</v>

00:25:19.360 --> 00:25:22.040
<v Jan Hoffmann>Should be an hour, or maybe I said.</v>

00:25:20.000 --> 00:25:20.400
<v Michal Sobocinski>Like.</v>

00:25:22.000 --> 00:25:24.480
<v Michal Sobocinski>I see, I see. Wait, if I can...</v>

00:25:26.560 --> 00:25:27.040
<v Michal Sobocinski>But...</v>

00:25:28.000 --> 00:25:28.760
<v Michal Sobocinski>I don't.</v>

00:25:30.640 --> 00:25:35.520
<v Michal Sobocinski>Charlotte and Maria Munoz Douglas.</v>

00:25:39.280 --> 00:25:41.920
<v Michal Sobocinski>I don't have the permission to download it, Jan.</v>

00:25:42.640 --> 00:25:42.880
<v Jan Hoffmann>No.</v>

00:25:43.920 --> 00:25:45.280
<v Michal Sobocinski>We need to go party.</v>

00:25:44.320 --> 00:25:49.680
<v Jan Hoffmann>That's why, OK, that's yeah, that's why I downloaded it locally, but yeah, OK, so...</v>

00:25:46.480 --> 00:25:47.120
<v Michal Sobocinski>But you come.</v>

00:25:48.360 --> 00:25:48.560
<v Michal Sobocinski>Yeah.</v>

00:25:50.560 --> 00:25:51.120
<v Michal Sobocinski>And...</v>

00:25:53.360 --> 00:26:01.920
<v Michal Sobocinski>You can go to the share it folder and you can find the Maria and maybe you can download and paste and send it to Dainis.</v>

00:26:01.560 --> 00:26:04.520
<v Jan Hoffmann>I'm just gonna, yeah, I'm just gonna share the.</v>

00:26:04.320 --> 00:26:09.840
<v Dainis Tkacovs>I'm trying to find some transcripts too. I had somewhere when I was testing.</v>

00:26:12.000 --> 00:26:22.600
<v Jan Hoffmann>And just, yeah, just sending the transcript only. The zip file has videos and audio extracted and everything, so it's kind of a big blip.</v>

00:26:14.560 --> 00:26:14.880
<v Michal Sobocinski>Yeah.</v>

00:26:23.520 --> 00:26:24.080
<v Michal Sobocinski>And...</v>

00:26:24.160 --> 00:26:26.800
<v Jan Hoffmann>200 megs, so maybe that's why it's not so.</v>

00:26:27.720 --> 00:26:52.280
<v Michal Sobocinski>Another question that I have that I understand that this agent is 1 transcript per per session or per whatever is called it, or we can get like the 10 transcripts, like the group 10 transcript, or I don't know, 1000 transcripts and sent to the agent and and he going to put your by this name of the processor or group the process the processor that is.</v>

00:26:34.640 --> 00:26:34.720
<v Jan Hoffmann>The.</v>

00:26:43.040 --> 00:26:43.520
<v Dainis Tkacovs>Oh.</v>

00:26:45.640 --> 00:26:45.800
<v Dainis Tkacovs>Mm.</v>

00:26:52.320 --> 00:27:10.880
<v Michal Sobocinski>instructor that like that I don't know. You have all of the from last month of last 15 days, you have all of the class scripts from one instructor and you're going to give this and you have like the recap of all of them or one by one what was the performance of this instructor or.</v>

00:27:03.200 --> 00:27:03.360
<v Dainis Tkacovs>Mm.</v>

00:27:11.600 --> 00:27:13.600
<v Dainis Tkacovs>Yeah, so, so...</v>

00:27:14.880 --> 00:27:35.200
<v Dainis Tkacovs>There are a couple of things about that, of course. It depends really from the use case, like how many transcripts, from how many instructors that team wants to evaluate for their business reasons, right? The second thing is the actual technical limitations, and here we hit some blocks. Since it's happening through...</v>

00:27:36.240 --> 00:27:50.560
<v Dainis Tkacovs>Microsoft Teams and there are certain limitations of in amount of files that can be uploaded per message and also size and length of files. So right now,</v>

00:27:52.080 --> 00:28:11.280
<v Dainis Tkacovs>So, for example, couple some lessons are really long and and there's a lot of discussed in the lesson, so so the the file that they were downloading is quite large and that's why we agreed with Martin and his team that first of all they they convert these files into take TXT documents and they.</v>

00:28:09.600 --> 00:28:09.840
<v Jan Hoffmann>Okay.</v>

00:28:11.840 --> 00:28:30.920
<v Dainis Tkacovs>split them for one file to be up to 10 kilobytes heavy. So for example, if the lesson shows that the transcript is to 40 kilobytes, that they should split into four pieces, right, and then upload. And at one time should be more than three.</v>

00:28:31.040 --> 00:28:52.640
<v Dainis Tkacovs>10 files, I believe, per message. And then evaluation could be done. If we want to automate further, as you just asked, like for example, if we want for instructor A, B, C, D, evaluate latest 15 lessons, right? It sounds like a lot of files there, right? Then we would need to build some other process on the background, for example, that.</v>

00:28:53.200 --> 00:29:11.800
<v Dainis Tkacovs>these transcripts are being saved through a specific process, through API, from Zoom to, let's say, Dataverse. And then there is another process that agent takes these transcripts from Dataverse directly, feeds into Copilot Studio, analyzes, and gives the feedback.</v>

00:29:12.080 --> 00:29:22.000
<v Dainis Tkacovs>So, but this is something that is not working right now, and we haven't thought about that yet. Yeah, that's in short. I share the transcripts.</v>

00:29:23.080 --> 00:29:26.960
<v Dainis Tkacovs>that we have used previously. I think one is VDT file.</v>

00:29:33.040 --> 00:29:34.080
<v Dainis Tkacovs>Check if it works.</v>

00:29:35.640 --> 00:29:35.760
<v Dainis Tkacovs>It.</v>

00:29:48.880 --> 00:29:56.320
<v Jan Hoffmann>OK, well, well, Dainis is preparing that. I think for us, the main...</v>

00:29:57.600 --> 00:30:08.640
<v Jan Hoffmann>The question is, where is the transcript data stored, right? And how is that linked to a lesson?</v>

00:30:10.240 --> 00:30:27.840
<v Jan Hoffmann>ID or, you know, how do we know that this is the instructor guide and the content of the actual lesson and how does that, and then have the record the transcripts linked to that?</v>

00:30:29.440 --> 00:30:51.440
<v Dainis Tkacovs>Only way how we can see the link is that after I will provide you a role once you activate your Zoom accounts, you can go and check on recording and transcript page and find specific instructor. You will see the lessons. You can click on some specific lesson where you will see small tag line.</v>

00:30:43.680 --> 00:30:44.000
<v Jan Hoffmann>No.</v>

00:30:51.760 --> 00:31:05.040
<v Dainis Tkacovs>called transcripts, and then you can download these transcripts. And in that UI, you will see that, hey, this is an email of that instructor, lesson is named like that, name convention, for example, the German level one.</v>

00:31:05.680 --> 00:31:06.080
<v Jan Hoffmann>Huh.</v>

00:31:06.240 --> 00:31:23.680
<v Dainis Tkacovs>unit 3 or something like that, and the transcript. This is the only mapping we can possibly have. How that happens after first 15 days when all the data is copied to our cloud, I don't have information about that. I was specifically working on this part.</v>

00:31:24.680 --> 00:31:25.160
<v Jan Hoffmann>Mhm.</v>

00:31:25.840 --> 00:31:44.400
<v Dainis Tkacovs>And what else? Oh, so there is no mapping exactly unless the lesson is named by instructor in that particular name, which is the program under where they teach it. But we don't have a clear mapping with what was the lesson.</v>

00:31:44.640 --> 00:32:03.520
<v Dainis Tkacovs>about and what was the expected content for that lesson. That is only known by Martin Steam when they manually evaluate actually. So they really know that, hey, this instructor at the 20th of June had this lesson with the student. And from Salesforce, they know that they should.</v>

00:32:03.600 --> 00:32:24.400
<v Dainis Tkacovs>teach Spanish level one, unit 3, business two, something like that, for example. And then they use the material from that lesson, they have from instructor materials database, and they can evaluate if everything from that lesson that must have been delivered.</v>

00:32:24.560 --> 00:32:39.120
<v Dainis Tkacovs>was actually delivered during the lesson. But that's something we cannot map right now on the level of agent. Probably we have to think about some other ideas how we could involve that.</v>

00:32:44.000 --> 00:32:46.800
<v Jan Hoffmann>Well, I mean, without the mapping, the data is pretty much useless.</v>

00:32:48.240 --> 00:32:48.880
<v Jan Hoffmann>Or is it?</v>

00:32:50.480 --> 00:33:11.760
<v Dainis Tkacovs>Not really. No. So now, yeah, latest change was that before Martin's team, anyone, gives these transcripts for evaluation, they give a brief context to agent what was needed to be delivered. Or they can even upload that lesson specific learning material.</v>

00:33:12.800 --> 00:33:29.120
<v Dainis Tkacovs>that was created by Berlitz team for agent to evaluate in the parallel. But how they do that, that's up to them. I'm not sure about these particular details. But I think this part can be solved. It's just not that simple as agent is set up right now.</v>

00:33:35.280 --> 00:33:35.920
<v Dainis Tkacovs>So...</v>

00:33:37.080 --> 00:33:38.000
<v Dainis Tkacovs>On the screen.</v>

00:33:51.600 --> 00:33:54.080
<v Dainis Tkacovs>Sorry, Team is lagging, like always.</v>

00:33:52.160 --> 00:33:52.280
<v Jan Hoffmann>Yeah.</v>

00:33:53.280 --> 00:33:53.360
<v Jan Hoffmann>The.</v>

00:33:59.120 --> 00:33:59.920
<v Rob Zinkov>Okay, there we go.</v>

00:33:59.600 --> 00:34:01.160
<v Dainis Tkacovs>Ohh, yeah.</v>

00:34:02.400 --> 00:34:09.760
<v Dainis Tkacovs>So, yeah, as you can see, Max Agent is available like any other human chat here or group chat.</v>

00:34:12.320 --> 00:34:29.520
<v Dainis Tkacovs>And I can chat with it in a regular way. So what I did here, I asked to, here is transcript of an English lesson. It is broken into five files. Please value the instructor's lesson quality and give a score recommendations in English. It's a full lesson, one-to-one English level one.</v>

00:34:30.640 --> 00:34:50.000
<v Dainis Tkacovs>There are five files, well, 6, I accidentally uploaded the VTT files off for it to evaluate the whole lesson, because the lesson was quite long, so we need to split the five files. And I'm not sure how much, 32, well, basically under a minute. And here's the...</v>

00:34:40.000 --> 00:34:40.120
<v Jan Hoffmann>Yeah.</v>

00:34:50.560 --> 00:34:59.040
<v Dainis Tkacovs>the response we have. So first is a quick summary with strengths and risks. Then there's overall score.</v>

00:35:00.120 --> 00:35:19.200
<v Dainis Tkacovs>Here we go. I'm not an expert of these scores. I don't have a clue what these scores mean. So, but yeah, here they are. This is the main part where everybody's looking in compared to their manual evaluation. Then it's a breakdown into subsections.</v>

00:35:21.120 --> 00:35:30.240
<v Dainis Tkacovs>opening goal, presentation, practice, score for each part, evidence described, and so on.</v>

00:35:31.440 --> 00:35:32.000
<v Dainis Tkacovs>Ohh.</v>

00:35:32.960 --> 00:35:33.760
<v Dainis Tkacovs>Bordner.</v>

00:35:34.960 --> 00:35:55.120
<v Dainis Tkacovs>Okay. Student performance notes, even described here. There are some described strong points and recommendations for improvements. This is something that is done only by AI. So this is not done by humans in general basis. We just want to</v>

00:35:46.320 --> 00:35:46.440
<v Jan Hoffmann>Yeah.</v>

00:35:55.680 --> 00:36:08.960
<v Dainis Tkacovs>make use of LLM logics and maybe LLM can come up with some new ideas on how to improve the quality of the lesson, which is quite a great addition. Everybody likes this part. Yeah, and that's about it.</v>

00:36:11.760 --> 00:36:14.800
<v Dainis Tkacovs>Quite simple and straightforward, I would say. Nothing fancy.</v>

00:36:19.240 --> 00:36:39.120
<v Dainis Tkacovs>Yeah, in an ideal world, it would be that we wouldn't need to download transcripts from Zoom, upload, convert, and upload here, and something like that. In an ideal world, in an ideal solution, that would happen on the background. We would just, for example, in each other, say, please evaluate Rob's lesson.</v>

00:36:39.360 --> 00:36:53.120
<v Dainis Tkacovs>from 24th of August with this student. Bam, that's it. An agent already knows in which database where to look for a transcript, analyzes it, and provides information. That would be, in my view, a perfect solution.</v>

00:36:57.280 --> 00:36:59.200
<v Dainis Tkacovs>Yeah, that's in short it.</v>

00:37:01.840 --> 00:37:04.800
<v Rob Zinkov>Where do the prompts for this thing live? I'm just curious.</v>

00:37:06.640 --> 00:37:11.680
<v Dainis Tkacovs>Prompt on Microsoft Studio setup of the agent.</v>

00:37:12.960 --> 00:37:18.320
<v Rob Zinkov>Okay, so there's they're not they're not in any repository that we can browse them in right now.</v>

00:37:19.520 --> 00:37:30.160
<v Dainis Tkacovs>Well, technically, if you would open Microsoft Power Platform, I think you can try to find their native repository and check it, but</v>

00:37:31.120 --> 00:37:50.640
<v Dainis Tkacovs>So the essence and the point of Copilot Studio is that low-code or no-code tool that is designed exactly for this purpose for users to not use any repository at all. Yeah, so everything is pretty straightforward and not developer.</v>

00:37:37.080 --> 00:37:37.560
<v Rob Zinkov>Mhm.</v>

00:37:39.600 --> 00:37:40.160
<v Rob Zinkov>Okay.</v>

00:37:45.520 --> 00:37:45.920
<v Rob Zinkov>Right.</v>

00:37:50.760 --> 00:37:58.400
<v Dainis Tkacovs>focused too much. But if you build some more complicated or sophisticated processes on the background, then probably you will need that.</v>

00:37:52.000 --> 00:37:52.400
<v Rob Zinkov>Sorry.</v>

00:37:59.360 --> 00:37:59.520
<v Rob Zinkov>Mm.</v>

00:38:00.800 --> 00:38:12.480
<v Jan Hoffmann>Dainis, you gave it in your prompt, in your, in your, yeah, in the prompt that you made, you gave it the lesson ID.</v>

00:38:14.000 --> 00:38:18.800
<v Jan Hoffmann>Does it does it have any way of accessing the instructor guide for that?</v>

00:38:20.720 --> 00:38:31.360
<v Jan Hoffmann>Or is that would would that would the evaluation would the evaluation look any different if you didn't say English level one?</v>

00:38:22.640 --> 00:38:25.360
<v Dainis Tkacovs>So, my, yeah, my...</v>

00:38:34.560 --> 00:38:42.320
<v Dainis Tkacovs>I need to check the knowledge base file that is created if there are any references for that.</v>

00:38:43.440 --> 00:38:56.800
<v Dainis Tkacovs>I, I'm not sure I need to recheck, but you know about Don AI, right? The agent that has access to our materials to decide that is managed currently by software contract team, and...</v>

00:38:58.240 --> 00:39:17.200
<v Dainis Tkacovs>The point would be that agent has information about what exactly should be under English, English level one, unit one, right? I can in theory connect these agents. And before this agent starts evaluating, it asks interconnected agent about, hey, what's</v>

00:39:17.240 --> 00:39:37.920
<v Dainis Tkacovs>in that lesson, what was instructor supposed to teach from that lesson? It gathers that information and uses to evaluate current lesson against the actual content that must be used, right? And probably that would help to improve the scoring even more and to be even more precise.</v>

00:39:20.440 --> 00:39:21.040
<v Jan Hoffmann>Mm-hmm.</v>

00:39:43.320 --> 00:39:49.280
<v Jan Hoffmann>Okay, cool. Can you maybe until we have everything?</v>

00:39:51.520 --> 00:39:56.080
<v Jan Hoffmann>Until we all have the right access to the right stuff on Zoom, can you?</v>

00:39:54.720 --> 00:39:55.200
<v Dainis Tkacovs>Mhm.</v>

00:39:58.280 --> 00:40:03.600
<v Jan Hoffmann>Can you dig up like 1 transcript that is?</v>

00:40:04.560 --> 00:40:04.880
<v Jan Hoffmann>Good.</v>

00:40:06.560 --> 00:40:25.120
<v Jan Hoffmann>And the and and find us the associated instructor guide, so that we know like exactly this is lesson whatever, English one lesson 5, and so that we have the content of the of the IG.</v>

00:40:16.560 --> 00:40:17.040
<v Dainis Tkacovs>Mhm.</v>

00:40:19.680 --> 00:40:20.160
<v Dainis Tkacovs>Mhm.</v>

00:40:25.680 --> 00:40:29.120
<v Jan Hoffmann>and the transcript of what was actually being done.</v>

00:40:30.160 --> 00:40:30.320
<v Dainis Tkacovs>Mm.</v>

00:40:30.480 --> 00:40:36.720
<v Jan Hoffmann>I would find that very interesting. I would like to see that if and massage that a little bit with Claudio.</v>

00:40:36.760 --> 00:40:55.680
<v Dainis Tkacovs>I think for that purpose, we can use some of already analyzed lessons, both manually, both by Max AI, and I have feedback from Martin's team, how good is that analysis particularly, and I can find material that must be used for that lesson.</v>

00:40:50.920 --> 00:40:51.160
<v Jan Hoffmann>Yeah.</v>

00:40:56.120 --> 00:41:13.680
<v Jan Hoffmann>Yeah, and then is like, I forgot to say that in the beginning, where there's two aspects to this: one is the agent itself and what it does, and if we may want to go forward with it or put it on Claudio or whatever, I don't know, maybe not.</v>

00:40:56.160 --> 00:40:57.280
<v Dainis Tkacovs>Uh, and and right.</v>

00:41:05.480 --> 00:41:06.000
<v Dainis Tkacovs>Of course.</v>

00:41:13.600 --> 00:41:13.920
<v Dainis Tkacovs>Yeah.</v>

00:41:14.320 --> 00:41:32.480
<v Jan Hoffmann>Depends. The other thing is, which is more our concern right now, is where is the data being stored and what do we have to do in order to build something like the curriculum factory or...</v>

00:41:14.880 --> 00:41:15.280
<v Dainis Tkacovs>Yeah.</v>

00:41:24.040 --> 00:41:24.480
<v Dainis Tkacovs>Mhm.</v>

00:41:32.600 --> 00:41:51.440
<v Jan Hoffmann>or some sort of automated thing that helps us generate like these snippets of learning material, micro learning experience, this sort of stuff. This is our, the other lens through which we're looking at this.</v>

00:41:50.000 --> 00:41:50.120
<v Dainis Tkacovs>Yeah.</v>

00:41:52.320 --> 00:42:06.000
<v Dainis Tkacovs>I think it would be super helpful if we could have some other outside, not Zoom Cloud, but our own database. I don't know, what would that be? AWS, Dataverse, whatever, where the process would be.</v>

00:41:52.480 --> 00:41:52.880
<v Jan Hoffmann>I did.</v>

00:42:07.120 --> 00:42:25.040
<v Dainis Tkacovs>would be extracting transcripts from Zoom Cloud and pulling out and storing on our cloud. And then we could use however we want that, right? So that would be ultimately a great idea.</v>

00:42:21.840 --> 00:42:22.320
<v Jan Hoffmann>Mhm.</v>

00:42:25.760 --> 00:42:33.680
<v Jan Hoffmann>Okay, cool. I think we should stop here and Dainis, I'll...</v>

00:42:35.280 --> 00:42:35.600
<v Jan Hoffmann>Um...</v>

00:42:36.880 --> 00:42:54.320
<v Jan Hoffmann>I might invite you to the meeting next week with Nicole because I have the feeling you might have something to contribute to that. Henning, I mean Henning is there, so maybe it's not needed, but like I'll invite you anyways. The more the merrier.</v>

00:42:46.040 --> 00:42:46.720
<v Dainis Tkacovs>Absolutely.</v>

00:42:47.560 --> 00:42:47.680
<v Michal Sobocinski>Yeah.</v>

00:42:55.120 --> 00:42:55.920
<v Dainis Tkacovs>Sounds good.</v>

00:42:55.760 --> 00:42:56.000
<v Jan Hoffmann>Kate.</v>

00:42:57.360 --> 00:43:18.240
<v Dainis Tkacovs>Yeah, sounds interesting. Absolutely. And yeah, of course, like a side note, again, I think if we can collectively a little bit think more about how we possibly could make use of analyzing and evaluating actual lesson videos or recordings, that would be like something</v>

00:42:59.600 --> 00:43:00.000
<v Jan Hoffmann>Yeah.</v>

00:43:15.680 --> 00:43:16.160
<v Michal Sobocinski>Mmh.</v>

00:43:18.400 --> 00:43:36.400
<v Dainis Tkacovs>ultimately would help massively in improving quality of the lesson for student and instructor. And this is something that Martin's QA team is expecting like a lot if we can make that happen anytime soon in the future. So yeah, let's not forget about that.</v>

00:43:20.160 --> 00:43:20.480
<v Michal Sobocinski>Okay.</v>

00:43:36.360 --> 00:43:36.960
<v Jan Hoffmann>Mm-hmm.</v>

00:43:38.920 --> 00:43:54.960
<v Michal Sobocinski>What I understand that we need to speak with Martin to have the access to the guidelines or standards that they use in the whole process, right? Or to get access to Power Apps or something like that that you mentioned before or...</v>

00:43:55.520 --> 00:44:15.120
<v Dainis Tkacovs>I think, I think, yeah, I can already provide the knowledge base material document with the scoring system that is being used manually. I can share that with you. But I think it still would be very, very important for you maybe to have a brief call with Martin and he explains exactly how they work on a daily basis. So</v>

00:44:03.040 --> 00:44:03.520
<v Michal Sobocinski>Yeah.</v>

00:44:14.560 --> 00:44:14.800
<v Michal Sobocinski>Hi.</v>

00:44:15.240 --> 00:44:33.840
<v Dainis Tkacovs>for you guys to understand the use case exactly. And also important part is to understand how later on they can use the scoring, what they actually do to improve the lesson quality. Are they having a call with instructor one-to-one to talk about improvements or what exactly they're doing?</v>

00:44:34.160 --> 00:44:52.480
<v Dainis Tkacovs>So we are technical part, right? But in order to understand the technical solution and make it perfect, it would be great to understand fully the process until very end, right? When they improve the instructor performance directly. So I think Martin would be perfect to explain all of that.</v>

00:44:48.200 --> 00:44:48.680
<v Michal Sobocinski>Mhm.</v>

00:44:54.000 --> 00:45:14.800
<v Dainis Tkacovs>Let me know if you need anything else. I will share this guide, this knowledge base that is used for this agent. And also please let me know on Teams, ping me up when you set up your Zoom accounts, when you actually log in and can access it. I will then be able to assign roles for you and I will send you a link where to check the recordings.</v>

00:45:14.920 --> 00:45:26.560
<v Dainis Tkacovs>transcript. So you can see actually in practice where exactly now the data is stored. And the note, as long as we use Zoom to deliver lessons,</v>

00:45:28.640 --> 00:45:44.080
<v Dainis Tkacovs>we will have this data there, right? So for first 15 days, that's non-negotiable. And if we can do something to store that data somewhere else for other use cases, other AI agents, that's great.</v>

00:45:46.320 --> 00:45:46.640
<v Michal Sobocinski>But.</v>

00:45:47.680 --> 00:45:48.160
<v Jan Hoffmann>Mhm.</v>

00:45:48.960 --> 00:46:07.840
<v Jan Hoffmann>Yeah, I think Michal, we need to download the data and either make sure that we delete it after whatever is required or anonymize it in a way that we get the most out of it and are allowed.</v>

00:46:01.760 --> 00:46:02.000
<v Michal Sobocinski>Yeah.</v>

00:46:06.080 --> 00:46:06.360
<v Michal Sobocinski>Yes.</v>

00:46:08.320 --> 00:46:09.040
<v Jan Hoffmann>To keep it.</v>

00:46:08.400 --> 00:46:08.880
<v Michal Sobocinski>Okay.</v>

00:46:10.120 --> 00:46:30.960
<v Michal Sobocinski>Okay, that should be complicated because if we can use the API and after that storage is on S3 bucket, for example, you have like the retention automatically that the Amazon is to remove all of the stuff or X every, I don't know if something has like that 90 days should be.</v>

00:46:22.480 --> 00:46:22.960
<v Dainis Tkacovs>Mhm.</v>

00:46:31.680 --> 00:46:40.160
<v Michal Sobocinski>remove it from the S3 bucket and do it. Amazon is caring about this automatically or other solution that we can implement.</v>

00:46:40.880 --> 00:46:41.440
<v Jan Hoffmann>Mhm.</v>

00:46:41.520 --> 00:46:51.800
<v Dainis Tkacovs>This is how it works right now, practically, on AWS, where our teams are accessing recordings through Salesforce, for example.</v>

00:46:52.480 --> 00:46:52.960
<v Michal Sobocinski>Mhm.</v>

00:46:56.240 --> 00:46:57.600
<v Michal Sobocinski>Yeah, perfect.</v>

00:46:57.760 --> 00:47:05.680
<v Rob Zinkov>Oh, this thing you just uploaded, this is this looks like a lot of like the prompt max gets before it evaluates less.</v>

00:47:05.040 --> 00:47:11.360
<v Dainis Tkacovs>No, this is not the prompt. This is actually a knowledge base document that is feed as a knowledge base. That's not the prompt.</v>

00:47:11.480 --> 00:47:12.640
<v Rob Zinkov>Okay, alright.</v>

00:47:16.400 --> 00:47:20.880
<v Rob Zinkov>Okay, alright, this, okay, this is a document that's alright.</v>

00:47:19.840 --> 00:47:39.760
<v Dainis Tkacovs>Yeah, this is document that is, so during the development process of this agent, we faced some hurdles based on LLM amount of tokens that can be processed within one message. And there are some ways where we were uploading some transcripts and asking to do certain things in analysis.</v>

00:47:30.640 --> 00:47:31.120
<v Rob Zinkov>Mhm.</v>

00:47:31.680 --> 00:47:32.040
<v Jan Hoffmann>Okay.</v>

00:47:39.840 --> 00:47:40.400
<v Rob Zinkov>Okay.</v>

00:47:40.320 --> 00:47:58.880
<v Dainis Tkacovs>and it didn't deliver anything. So we needed to reduce the complexity and length of the document, right, on the knowledge base, because on every request, it opens the document, goes through, and if the token window is not sufficient, then it will just break and don't answer anything. So we needed to</v>

00:47:44.160 --> 00:47:44.720
<v Rob Zinkov>Okay.</v>

00:47:55.840 --> 00:47:56.400
<v Rob Zinkov>Okay.</v>

00:47:56.720 --> 00:47:57.120
<v Jan Hoffmann>OK.</v>

00:47:59.120 --> 00:48:01.280
<v Dainis Tkacovs>Little bit, make it shorter.</v>

00:48:00.080 --> 00:48:03.760
<v Rob Zinkov>So is this is this the compressed document or the full document?</v>

00:48:03.120 --> 00:48:18.960
<v Dainis Tkacovs>Yeah, this is compressed document, but it's not super compressed. Full document, I think Martin should have it. Yeah, yeah, and I can send over a custom prompt as well. I will copy that.</v>

00:48:06.120 --> 00:48:07.240
<v Rob Zinkov>What's the... Yeah.</v>

00:48:11.520 --> 00:48:12.480
<v Rob Zinkov>Okay, alright.</v>

00:48:21.680 --> 00:48:30.080
<v Rob Zinkov>Yes, that would be good just to kind of get a sense for like, it would give me a sense of kind of how the tool was built and things like that.</v>

00:48:29.040 --> 00:48:34.480
<v Dainis Tkacovs>Absolutely. I will make a quick TXT file to not just copy here in the chat.</v>

00:48:35.200 --> 00:48:35.760
<v Rob Zinkov>Yeah.</v>

00:48:41.680 --> 00:49:00.560
<v Rob Zinkov>But yeah, I do broadly agree that, like, we probably need a we probably need to have a chat with Martin to kind of get a good sense of what the requirements are, but it sounds like you've already, like, just through working on this, have a sense for, like, what what his group really wants and needs.</v>

00:48:42.400 --> 00:48:42.640
<v Dainis Tkacovs>Yeah.</v>

00:49:01.120 --> 00:49:20.400
<v Dainis Tkacovs>Yeah, yeah, that was essentially part of testing. We had multiple testing rounds. I provided one version of agent. They were testing, providing me the feedback. Based on the feedback, I was adjusting the prompt and the knowledge base. And we did that like maybe six or seven times until the moment when they were like, okay, this is nearly perfect and this is great.</v>

00:49:06.240 --> 00:49:06.640
<v Rob Zinkov>Yeah.</v>

00:49:27.840 --> 00:49:29.440
<v Rob Zinkov>Yeah, yeah, that makes sense.</v>

00:49:29.320 --> 00:49:29.600
<v Dainis Tkacovs>Yeah.</v>

00:49:31.120 --> 00:49:41.760
<v Dainis Tkacovs>All right, yeah, that's about it. So yeah, guys, if you will have any further questions or anything, feel free to send me an email or drop a message in Teams and I will be happy to help.</v>

00:49:44.320 --> 00:49:45.120
<v Jan Hoffmann>Great, thank you.</v>

00:49:46.240 --> 00:49:46.560
<v Dainis Tkacovs>Right.</v>

00:49:47.240 --> 00:49:47.440
<v Jan Hoffmann>Um...</v>

00:49:48.320 --> 00:49:57.120
<v Rob Zinkov>Yeah, oh, this is maybe not so. I noticed that you have, I noticed that you're 5 hours ahead of where are you just on.</v>

00:49:58.160 --> 00:49:59.120
<v Dainis Tkacovs>I'm in Bangkok.</v>

00:49:59.680 --> 00:50:02.880
<v Rob Zinkov>Fun. That's nice.</v>

00:50:01.520 --> 00:50:05.040
<v Dainis Tkacovs>Yeah, it's nice. I'm here for the last three years already.</v>

00:50:05.680 --> 00:50:07.280
<v Rob Zinkov>Yeah, it's an amazing place.</v>

00:50:07.920 --> 00:50:10.240
<v Dainis Tkacovs>Oh yeah, one of the best in the world, I would say.</v>

00:50:10.640 --> 00:50:18.640
<v Rob Zinkov>Yeah, but it's good to know 'cause like I'm sort of like, okay, alright, this is alright, we, we gotta catch you, we gotta catch you early in our day.</v>

00:50:19.520 --> 00:50:37.360
<v Dainis Tkacovs>Yeah, yeah, probably for some meetings like this, probably earlier, but I'm quite flexible. I understand that we have colleagues also from the US or late hours in Europe, so I can adjust some time and be even available on the evenings. Usually I work early in the mornings and</v>

00:50:19.600 --> 00:50:19.760
<v Jan Hoffmann>Okay.</v>

00:50:37.440 --> 00:50:46.400
<v Dainis Tkacovs>Also, I like to work with these agents early, late in the evenings as well. So just hit me up. If I will be able to answer, I will do that.</v>

00:50:37.960 --> 00:50:38.080
<v Jan Hoffmann>Yeah.</v>

00:50:42.720 --> 00:50:43.200
<v Rob Zinkov>Okay.</v>

00:50:43.400 --> 00:50:43.520
<v Jan Hoffmann>The.</v>

00:50:45.600 --> 00:50:46.320
<v Rob Zinkov>Alright.</v>

00:50:47.200 --> 00:50:49.040
<v Rob Zinkov>Okay, well, yeah, sounds awesome.</v>

00:50:49.760 --> 00:50:50.160
<v Dainis Tkacovs>Yep.</v>

00:50:50.560 --> 00:50:51.040
<v Jan Hoffmann>Cool.</v>

00:50:51.280 --> 00:50:52.560
<v Dainis Tkacovs>All right, guys. Thank you.</v>

00:50:53.680 --> 00:50:55.440
<v Jan Hoffmann>Bye, Dainis. Talk to you soon.</v>

00:50:55.200 --> 00:50:56.480
<v Dainis Tkacovs>Bye. Bye.</v>

00:50:55.880 --> 00:50:57.200
<v Michal Sobocinski>Thank you so much. Bye-bye.</v>

00:50:59.760 --> 00:51:01.920
<v Jan Hoffmann>The two of you now.</v>

00:51:03.280 --> 00:51:03.320
<v Jan Hoffmann>Uh...</v>

00:51:04.560 --> 00:51:20.160
<v Jan Hoffmann>I didn't want it to go so much in the direction of that agent, really. Sorry. We have some stuff to discuss, but lunchtime is approaching and I need to get some food.</v>

00:51:11.080 --> 00:51:11.280
<v Rob Zinkov>Yeah.</v>

00:51:12.480 --> 00:51:12.880
<v Rob Zinkov>I...</v>

00:51:18.640 --> 00:51:19.040
<v Rob Zinkov>I...</v>

00:51:20.000 --> 00:51:39.240
<v Rob Zinkov>Yeah, I actually have a meeting at noon, but I think my day is clear. Like, let me just quickly like look at my day. I think I'm basically all clear today. So whenever we want to meet, I'll be available. I just, I have a meeting like at noon, otherwise I'm good.</v>

00:51:40.880 --> 00:51:44.080
<v Jan Hoffmann>Right, let me, I think what I need to do is I need to...</v>

00:51:45.360 --> 00:51:48.000
<v Jan Hoffmann>Read, read, and review the PRD.</v>

00:51:49.240 --> 00:52:01.680
<v Rob Zinkov>Okay, sounds good. Also, feel free to skim how I've set up the iterations. I sort of took like, I kind of took what you put as a starting point and kind of adjusted things a little bit, but.</v>

00:52:03.200 --> 00:52:06.480
<v Rob Zinkov>And they put priorities on all the on all the uh issues.</v>

00:52:08.000 --> 00:52:09.760
<v Jan Hoffmann>Yes, I'll have a look. Yeah.</v>

00:52:10.960 --> 00:52:11.360
<v Jan Hoffmann>Cool.</v>

00:52:11.840 --> 00:52:23.920
<v Rob Zinkov>But yeah, other than like immediately like now where I will be meeting and eating food, I'm available all of today. So just ping whenever and I can we can pop into a meeting.</v>

00:52:20.520 --> 00:52:20.880
<v Michal Sobocinski>Yeah.</v>

00:52:24.480 --> 00:52:25.160
<v Jan Hoffmann>Perfect.</v>

00:52:24.560 --> 00:52:28.640
<v Michal Sobocinski>Me too, except at 3 P.m. that I have the meeting with, not.</v>

00:52:29.600 --> 00:52:30.080
<v Rob Zinkov>Okay.</v>

00:52:29.760 --> 00:52:30.240
<v Michal Sobocinski>And...</v>

00:52:32.560 --> 00:52:39.840
<v Jan Hoffmann>Yeah, I have like my my afternoon is not so not so empty, sadly, but that's.</v>

00:52:41.200 --> 00:52:42.880
<v Jan Hoffmann>Let's try to get the roadmap.</v>

00:52:45.200 --> 00:52:51.440
<v Jan Hoffmann>kicked off of our list. If not today, then maybe tomorrow in the morning.</v>

00:52:46.480 --> 00:52:46.640
<v Michal Sobocinski>Yeah.</v>

00:52:47.040 --> 00:52:47.440
<v Rob Zinkov>Yeah.</v>

00:52:52.400 --> 00:52:52.840
<v Rob Zinkov>All right.</v>

00:52:53.040 --> 00:52:53.520
<v Michal Sobocinski>Okay.</v>

00:52:54.080 --> 00:52:54.880
<v Jan Hoffmann>Thank you.</v>

00:52:54.400 --> 00:52:54.640
<v Rob Zinkov>So...</v>

00:52:55.760 --> 00:52:56.880
<v Rob Zinkov>Sounds good. Bye.</v>

00:52:57.120 --> 00:52:57.600
<v Michal Sobocinski>Bye.</v>

00:52:57.600 --> 00:52:58.400
<v Jan Hoffmann>Later. Bye bye.</v>

