# More Planning

**Date:** 2026-06-23
**Start:** 2026-06-23T09:00:00.000Z
**End:** 2026-06-23T11:30:00.000Z

---

**[0:03] Jan:** I know.

**[0:03] Rob:** That, that might be how long it takes, but also like...

**[0:08] Jan:** Yeah, I just wanted to have a meeting there. We can we can all have lunch and.

**[0:11] Rob:** All right. Yeah, because I wanted to sort of step away for like an hour and change for lunch at some point.

**[0:14] Michal:** Together, right? They're sharing the screen, and...

**[0:19] Jan:** Yeah, yeah, no problem. Sorry.

**[0:21] Rob:** All right.

**[0:22] Jan:** ..

**[0:23] Michal:** We can get lunch together, looking at our faces, right, and dating.

**[0:28] Jan:** Yeah.

**[0:29] Rob:** I don't know, I wanted to spend it with my spouse, but...

**[0:31] Michal:** The.

**[0:32] Jan:** Yeah.

**[0:35] Rob:** Okay.

**[0:35] Jan:** That's nice. Okay, now, quickly recap of what Michael and I have looked at.

**[0:43] Rob:** Mhm.

**[0:46] Jan:** There, there are around the front end; there was the thing that we with. We had a look at how it is on the portal on my Berlitz currently, and there you actually have stuff like the multiple choice.

**[0:58] Rob:** Mhm.

**[1:06] Jan:** I can show you this. Real quick.

**[1:09] Michal:** But we are sure that is multiple choice or we should select one of these answers that is correct for them. I don't hear you. Okay, I am.

**[1:25] Jan:** Are you? What is this?

**[1:28] Michal:** No, yes, because maybe you play the button of the...

**[1:36] Jan:** I, I think I...

**[1:37] Michal:** You are shutting the port.

**[1:43] Jan:** What is that? Didn't see that before. And. And now I can hardly hear you, but that's a, I think that's a Teams bug.

**[1:57] Michal:** Okay.

**[1:58] Jan:** Oh, no, no, no, it's fine. Rob, , quick, like this is, this is how it looks, and I was, and there is no...

**[2:04] Rob:** Yes. Mhm.

**[2:10] Michal:** No, no, no, but we don't see your screen if you're sharing the lesson.

**[2:13] Jan:** Sorry. Sorry. There we are.

**[2:18] Michal:** No.

**[2:19] Rob:** OK, alright.

**[2:20] Jan:** It's not what I wanted to share; this is what I wanted to share.

**[2:21] Rob:** This.

**[2:23] Michal:** Okay, now.

**[2:23] Rob:** Okay, yeah. Yeah, so this is, yes.

**[2:25] Jan:** Okay, so... Record the correct answer, okay, whatever. So, and that was... Bigger, this is not exactly where we were, right?

**[2:40] Michal:** No, we.

**[2:43] Jan:** The main thing here is there is no audio. Coming, like it's not reading anything to me. This is something that we thought we should have.

**[2:50] Michal:** Yeah.

**[2:57] Jan:** And... And then this was multiple choice before. Maybe if I reload a few times, that changes. I don't know. Ahh. Right, so the way it works, ... Rob is, you have, you can. You push, you have.

**[3:30] Rob:** Yeah, yeah, I, I went, I went through, I went through, I went through a bunch of these lessons, so, so that's why, like, that's why I knew that it had to be important, because this was such an odd interface that was like, okay, this is deliberate.

**[3:31] Jan:** As. Right, OK, and the one thing to...

**[3:39] Michal:** Yeah.

**[3:44] Jan:** Yeah, yeah, it is that.

**[3:45] Michal:** And this is the one correct answer, right? Because it's record the correct answer, not like the...

**[3:45] Rob:** So, and I...

**[3:55] Jan:** Yeah, so the Rob, the interesting thing was I was giving it. This one, so...

**[4:03] Rob:** Mhm.

**[4:14] Jan:** It ignores that I said doesn't. And kind of... Fits this into what it thinks is the right answer.

**[4:26] Rob:** That's.

**[4:26] Jan:** Which is just super weird.

**[4:29] Rob:** That, that's unfortunate.

**[4:32] Jan:** Yeah, so it doesn't it doesn't take the transcript and put the transcript in here and then rank it so. ... I guess. showing this because we need to understand how this works and it probably doesn't work so well.

**[4:52] Rob:** Right.

**[4:54] Jan:** And now.

**[4:54] Rob:** At least if we're going to be leaning on, if we're going to be leaning on MS, the Azure APIs, which is what this currently does. we might have some problems. I only mentioned the Azure APIs because for two reasons. One, it's what that solution uses, but it's also what's in the PRD.

**[5:18] Jan:** Mhm.

**[5:19] Rob:** So.

**[5:21] Jan:** For cost reasons.

**[5:21] Rob:** Say what?

**[5:24] Jan:** For cost reasons.

**[5:26] Rob:** Right.

**[5:27] Jan:** Right.

**[5:28] Rob:** I suspect for cost reasons, but I also feel like... At least for this thing, like ASR and speech to text are fairly small models. If cost is an issue, we should just self-host. It's very straightforward to do that for these things. Yeah.

**[5:45] Jan:** Yeah. We, we, that is actually something that we, I think we absolutely should do, because, because of costs, because if the free T, if we do not have... The Berlitz experience in the free tier. That would really suck.

**[6:05] Rob:** Yeah, these, yeah.

**[6:06] Jan:** But you want, you want them, you want the teacher, the system to read to you the question. and you answer the question. So, I mean, it's, we're not calling it a conversation because it's something different, but this question and answer thing that I believe we should have that rely heavily on audio. And not clicking. Or I mean, here you're not clicking, but... Right, and I think that helps in the whole immersion.

**[6:45] Rob:** Yeah, I also think it is an opportunity to sort of be more mobile friendly because it's just... you press down record, keeps it very clean. Now again. When I've looked at the Figma mockups, I think that commitment isn't quite there yet, but... Yeah, I can see it as being very nice if we sort of just have you tap record, you speak at the app. And it goes.

**[7:15] Jan:** Right. And do you think? Do you do you think we even need the tapping? I mean, if it's currently if it's reading, then it makes sense to tap, but...

**[7:32] Rob:** .. That's, I will say the UI UX issues are not for us to decide.

**[7:43] Jan:** Good point, good point, yeah.

**[7:43] Michal:** Yeah, and one question because of the speak to text, speak to text, I think so that on the mobile apps and the mobile and on the web. Actually, you have some native tools that are supported, I think, so yeah, if I'm not wrong, then now. That I don't know, of course, maybe for the free version or something like that, to not use the some payments or whatever the features that we can use some native support of the browser or mobile tools, and after that for the... course, normal course when you pay something that you can use the better integration, right, or something like that. I don't know if, what do you think about this? And after that, of course, you can call API to get evaluation or whatever from the free one or the normal one. API that do the STT. Because I think so that on the mobile app and on the browser, you can use like the default one that you have with your phone, right? That when you're speaking for your keyboard, et cetera, that is like default one. That if I'm not wrong, you can use it on the app too. That is only like the text timing that. I would to mention.

**[9:18] Jan:** .. Rob, we need your like undivided attention here.

**[9:23] Rob:** Okay.

**[9:24] Jan:** You, you. I think you're making diagrams right now.

**[9:28] Michal:** Yeah.

**[9:30] Rob:** Oh, sorry, it's okay.

**[9:30] Jan:** That.

**[9:36] Rob:** How did ? Did I forget? Did I forget I was sharing my screen like last time?

**[9:38] Jan:** Yeah. No.

**[9:43] Rob:** Okay.

**[9:45] Jan:** I could see it in your eyes.

**[9:47] Rob:** Okay. Oh no. Okay, alright, okay. Alright, let's go. All right. Okay.

**[10:05] Jan:** Because we need to have something that is reasonably cheap. I'm going as far as saying we might need to have certain fallback mechanisms where we maybe have an expensive model, a cheap model, and a...

**[10:17] Rob:** Mhm. Mhm.

**[10:25] Jan:** Maybe on device, maybe slower. Whatever, but something.

**[10:31] Rob:** I think for where we are now, it's... So I think for speech stuff, like I think it should be out of scope that we're going to put anything on the device. But almost every phone these days has an on-device speech recognition that's just built into the phones.

**[10:45] Jan:** Cat. Right.

**[10:55] Rob:** That we can, so I like, if we're gonna do that, it's kind of like good model, worst model, built-in thing.

**[11:02] Jan:** Mhm. Right, okay, right. And you agree that we make a spike? For this.

**[11:10] Rob:** Sure. I'm not sure. The title of that doesn't seem to be quite agreeable, because that's a speech caching for static content. Because that seems to imply, that seems to imply that, oh, we're going to just download the audio ahead of time instead of rendering it.

**[11:21] Jan:** But that's that. Yeah, feel free to change. This is where we came from before, Michael and I, when we discussed that, because it seemed kind of stupid to pay for LLMs to over and over generate stuff.

**[11:35] Rob:** Okay. Okay. Mhm.

**[11:48] Jan:** Maybe it's not so bad when you have caching for the LLMs enabled and it's something that they remember that they used before. But in...

**[11:54] Rob:** Mhm. So what particularly would you like cashed?

**[12:05] Michal:** But.

**[12:05] Jan:** Well, what I would like is to be the free tier to be as cheap as possible.

**[12:12] Rob:** Right, right, right, right. I understand that's the goal, right?

**[12:14] Jan:** And. Yeah.

**[12:17] Michal:** That exists 2 two ways right that we can create when you on the LMS we can generate the using one times LMS and create the audios and after that use the same audio until the new version or we can use some cache like Ian mentioned right? That we can recreate this audio or whatever is called it on the on the user side, right?

**[12:48] Rob:** Mhm.

**[12:49] Michal:** Using the Casares.

**[12:53] Rob:** Right, so... I can see sort of cash in the sense of... We have lesson content, we want it to be spoken, so we render it once into the audio, and then that's just that's something we can save on S3 and pull, and we don't have to keep doing that, so that's one. That's one way of like speech caching I can understand the spike to be about.

**[13:20] Michal:** Yeah, that we generate the audio, we save it, and we use this audio until the new version, right?

**[13:20] Jan:** Mhm.

**[13:26] Rob:** Right.

**[13:27] Jan:** I mean, if yeah, if that's what we want to do, if this could like, you could do that explicitly, you could just say, okay, we render the audio and it's part of a...

**[13:31] Rob:** Yeah.

**[13:39] Jan:** Of the of the. Grilletto.

**[13:43] Rob:** Right.

**[13:43] Jan:** But it's like the audio that is associated with that particular drill.

**[13:47] Rob:** That's right.

**[13:48] Jan:** Or we say... You make the decision to... Or, we present the text and the... the front end has an API endpoint that gets the audio or makes audio out of it. And then if we self-host, it could be, the caching could be built into that. Right, because they're like, okay, have I rendered this before? Yes, I have. So great, it's on, it's somewhere and it gets pulled from there. or streamed or it generates it on the fly.

**[14:27] Rob:** Right. So like I understand that from the perspective of like, we're going to place from like text to speech. So.

**[14:38] Jan:** Mhm.

**[14:38] Rob:** Fr. For something for the other direction where the user speaks and we have to turn it into text, I don't see any notion of...

**[14:41] Jan:** Right.

**[14:51] Rob:** Caching, but I do see a notion of say having fallback ASR models. Yeah, exactly. I think it's kind of its own thing. And that can go from like there's a nice expensive ASR model to there's a cheaper one to we just use the built-in phones ASR model.

**[15:04] Michal:** Yeah.

**[15:13] Jan:** Is that?

**[15:14] Rob:** And these are both valid, these seem like both valid spikes to me.

**[15:34] Jan:** What is going on? This is why I can be a little better.

**[15:43] Rob:** This is why, this is why we love Miro, right? Or why you like Miro?

**[15:46] Jan:** Yeah. Just want to edit the text, for crying out loud. Hosting, now it works. , , , , . What did we say? Backup models or backup or fallback?

**[16:12] Rob:** Well, fallback. I said fallback models.

**[16:21] Jan:** Unless we would like to.

**[16:22] Rob:** Yeah, and I would say, , cloud comma on device.

**[16:30] Jan:** What's that? Can you put it in?

**[16:31] Rob:** Ohh, OK. Here, let me let me let me try here. I, I, I know, hold on.

**[16:38] Jan:** Ohh.

**[16:41] Rob:** Wait, why can't I edit this?

**[16:41] Jan:** Yeah. I know.

**[16:44] Rob:** Wait, hold on, wait, wait, hold on. Yes, I, no, no, oh my god.

**[16:45] Jan:** Like, I'm moving away my.

**[16:51] Rob:** Oh wait, I can't. Okay, I did it. Okay, hold on. Okay. .

**[17:05] Michal:** But on device. On ours on cloud or device or local, right? Our server, local server tool, right? Or...

**[17:10] Rob:** Okay.

**[17:21] Jan:** I think that's what is it alright.

**[17:21] Rob:** Right. That's what, okay.

**[17:24] Michal:** Thank you.

**[17:26] Rob:** Did it work? Did I do it?

**[17:27] Michal:** Yeah, but it's only that the cloud, like open router for example, and on device, or we want to investigate local one, like get the server, install the LLM, and serve it for our usage. what I mean?

**[17:45] Rob:** I mean. That would be nice too. I feel like... Almost any model that we have the capability of self-hosting is available for effectively free on open router already. So I'd prefer to start with open router.

**[18:08] Michal:** Yeah.

**[18:09] Rob:** For LM stuff and then only kind of move to hosting the LM stuff when... it feels like we can do it like cheaper because the main motivation here is cost and

**[18:20] Michal:** Yeah, okay. One, one, one thing to mention is that the open routed the free models is failed a lot, like that I don't know, or then 10 runs, I don't know, maybe 6 is failed on and in four or like 50% that is working or not, like...

**[18:30] Rob:** Okay, alright. Okay. Okay, that's okay, that might be a problem.

**[18:40] Michal:** Is. That is my feeling for my testing now, right? what I mean? And maybe it's like there's some limit of the calls per minutes or per seconds or whatever that I know.

**[18:43] Rob:** .. Yeah, yeah. Yeah, this might be some free tier thing where like once you're a paying customer, they're like.

**[18:55] Michal:** Yeah, exactly. I use the free term.

**[18:59] Rob:** Yeah, well, I hope we can get you off the free tier very shortly.

**[19:03] Michal:** Yeah. For this reason, I asked people for the health self-hosted self-hosted.

**[19:09] Jan:** Okay.

**[19:16] Rob:** Right.

**[19:23] Jan:** Okay, are we good with the spikes?

**[19:26] Rob:** .. Yes. I think they're clear to me.

**[19:33] Michal:** Yeah.

**[19:34] Jan:** Yeah, that one has to do with the drill evaluator because the drill is, ah, the drill is weirdly evaluated. And That's actually something that I wanted to bring up with you is with you guys is if there are three, I mean this was essentially what I showed you was a multiple choice, right? And you kind of have to pick the right one and then you say it. But when you say it, ... You could, you can give other correct answers, and currently those are not, they're not counted as correct. They're being...

**[20:13] Rob:** Right.

**[20:24] Jan:** Yeah, I think they're being discarded or not allowed as not seen as a correct answer. We could with, I mean, that's the power of AI, right? We could have, we could feed the result into an LLM and it could say, oh, like we have what you were showing me earlier, this is the correct answer.

**[20:32] Rob:** Right.

**[20:46] Jan:** This is correct. It's not what we expected, but it serves. The purpose or the lesson, the drill goal is met.

**[20:54] Rob:** Yeah.

**[21:02] Michal:** Mhm.

**[21:04] Jan:** So that is, but it means that we're introducing an AI layer into the drill evaluation.

**[21:13] Rob:** Is that bad?

**[21:16] Jan:** .. I think it could be awesome for the user. Because it gives more freedom, it's a bit more flexible.

**[21:27] Rob:** Mhm.

**[21:29] Jan:** .. Since it happens mostly on text, I don't believe it's awfully expensive. And that's kind of the thing with. How? How, how? This is a bunch of tokens really, right? So that costs us nearly nothing, but nearly nothing but times 1,000,000 users can be substantial money.

**[21:54] Rob:** Right. Sure. This is true.

**[22:05] Jan:** That's. Let's do it like that. The dog food. Version of this.

**[22:13] Rob:** But this is like, yeah, yeah, go for it.

**[22:18] Jan:** Dog food is. ... Rigid. Evaluation. Right, and then MVP, or maybe later. .

**[22:39] Rob:** It's. Just to kind of push, just to kind of push it back a little bit here, this is the kind of task that LMs were basically invented to do and do well. So like we could use something from four or five years ago and it probably still nail it great.

**[22:52] Jan:** Mhm. Okay.

**[23:00] Rob:** There's probably stuff we can do, like if we use an old enough model, we could legit run this on CPU using an old, like one of the older LMs.

**[23:13] Jan:** Mhm.

**[23:14] Rob:** Like this task is, , of like, is this, ... Is this grammatically correct? Does this answer this question? could be probably done even on like a fairly small LOM from like four or five years ago.

**[23:24] Jan:** Yeah.

**[23:38] Michal:** Yeah, you, you mean the self-hosted right with?

**[23:42] Rob:** We could self-host, we could just use, we can just use like the oldest, we can use the cheapest LLM we could find.

**[23:50] Michal:** Yeah, one on the, yeah, yeah, yeah.

**[23:54] Jan:** You mean, so yeah, like not even Haiku, but something that is actually if you...

**[23:58] Rob:** Yeah, exactly.

**[24:00] Jan:** And Haiku is already dirt cheap.

**[24:03] Rob:** Right, right. Yeah. Even something like cheaper than Haiku, where you pay like a penny for 5 million tokens.

**[24:12] Jan:** Right. Okay, but do I need to, so then we do that for the MVP or not?

**[24:22] Rob:** ..

**[24:22] Jan:** You make you make it sound really easy.

**[24:26] Rob:** I'm okay with what you have written.

**[24:29] Jan:** Okay.

**[24:30] Rob:** .. But I also feel it's very easy. I also feel for MVP, like... cost should like causes like I think less of a concern, but I'm sort of happy to have that there just to sort of say, okay, at any moment we can pull the switch and cut that cost without even thinking.

**[24:41] Jan:** Okay. Okay. Right. ... This has no. No copy of the there. Okay, just because. ... It's going to be important for the grammar evaluator. I think we need something that... Tells us if something lies within. The... If something is level appropriate.

**[25:34] Rob:** Mhm.

**[25:35] Jan:** So I think we need like a level of probe. We had nurse. Check.

**[25:43] Rob:** Yeah.

**[25:44] Jan:** Checker.

**[25:46] Rob:** Right.

**[25:48] Jan:** Evaluator.

**[25:51] Rob:** I think that would be nice.

**[25:53] Jan:** And the way that I see it is it should... It should have. The grammar or the the vocab.

**[26:03] Rob:** Mhm.

**[26:04] Jan:** Like, Inc, like, grow with lessons. Right, so you can tell it, okay, I'm now in lesson 5 of English 3. And this is exactly the vocab that I that the student should know. And this is exactly the grammar, so if you insert a... If you insert a sentence, it can tell you whether it's level appropriate or not. Make sense?

**[26:40] Rob:** Yes, that makes a lot of sense.

**[26:41] Jan:** And yeah, it was like it was explaining to me what he posted yesterday that this already works pretty well without specifying that, but with.

**[26:46] Michal:** Yeah.

**[26:55] Jan:** I mean.

**[26:57] Rob:** Michal, what do you mean by it works already well without specified? Just so I know what you exactly what you mean.

**[26:57] Jan:** No problem.

**[27:03] Michal:** No, we checked it because that we take Gemma for model that free one on that I use it that which out a lot of stuff that I put the prompt that this is answer text answer by the user, this is the context or target what we want to achieve for the user and the self level is.

**[27:08] Rob:** Okay, yeah. Yeah.

**[27:26] Michal:** And after that, this is going to evaluate if the serve level is correct that you use the phrase on your level or below. For example, when you have the C2 or C1, that is different responded, not you telling only, hi, my name is Michal, that you need to put some.

**[27:36] Rob:** Yes. Yeah, yeah, I am. Yes, and this also agrees with my personal experience of using Gemma 4 and the other local models for generating level appropriate German content. It does actually seem to like... do well enough in that regard.

**[28:06] Jan:** Really? Wow, okay. I mean, that's... Like, my brute force approach would be to give it like the full vocab, which for the first three lessons is not so much, but then later on you have hundreds of words.

**[28:26] Rob:** So, what I specifically did was, please get, please, please give me a text that stays within the Goethe Institute's BEINS word limits, along with questions about it, and I was able to read the text.

**[28:27] Jan:** And. Yes.

**[28:45] Rob:** Which is some indication that it's probably at about the level it needs to be.

**[28:50] Jan:** Wow. Okay.

**[28:53] Rob:** Now, I'm not saying that's what we should do, that's how we should write our prompts. But I felt I found that worked. Fairly well.

**[29:06] Jan:** I mean, we need it per lesson. That's the level of detail that we want. We want to be able to say, okay, this is the new lesson and this is the new words that you're going to learn in that lesson. And this is the your.

**[29:13] Rob:** Right. Right.

**[29:25] Jan:** Your pool of words that you should have already learned.

**[29:29] Rob:** Right.

**[29:30] Jan:** Plus maybe at some point we're able to... to track this on an individual level. I would like to be able to know exactly the words that a student knows. Even with, like...

**[29:49] Rob:** Right.

**[29:51] Jan:** Student X has used the words. I don't know, kitchen five times. And the pronunciation was bad, so I don't know, something like that, ultimately, right? Future stuff. Yeah, but we need the level of appropriateness evaluator.

**[30:10] Rob:** Right, yeah, yeah.

**[30:18] Jan:** And we were sort of... Do you see where I'm going with my mouse?

**[30:27] Rob:** Your mouse is off the screen, so hold on. Are you up? Are you down? Where are you? Hold on. Oh, I see. Yeah, yeah, you're pointing at the front end. Okay.

**[30:30] Jan:** I'm back up, up, up in the mobile app, right? OK, so... Yeah, when you left, Michal and I were discussing like front end is just this audio that may or may not be cached. And now the user input.

**[30:53] Michal:** Mhm.

**[30:54] Jan:** Is. Oh, well, actually... The touch interaction I think we don't have to do. The text is something that, well, we also don't need to do anything. The audio. Is.

**[31:18] Michal:** Audio capture is like the app, right?

**[31:24] Jan:** Well, I'm kind of hiding that here. There's no processing going on. Right. I mean, you could argue. Like dealing with a microphone is front-end business. Then feed this into...

**[31:41] Michal:** But.

**[31:44] Jan:** .. Where do you want to put that?

**[31:48] Rob:** Ohh.

**[31:51] Jan:** Is the evaluator getting the waveform? Or is the evaluator getting text?

**[32:00] Michal:** Depends, right? Because for the grammar, you can use, for example, text or audio, but for the pronunciation score, to get it, I understand that you will need to have the audio to evaluate whole stuff, right? Your pronunciation.

**[32:06] Jan:** Mm. Yeah, so we need a bit of ASR going on anyways here.

**[32:23] Michal:** Yeah, there is the path to get for text that.

**[32:24] Rob:** Right.

**[32:26] Jan:** That's it. That was kind of missing, sorry. I'll add that. By the way, that was my wife.

**[32:41] Rob:** Hold on me, I'll grab my.

**[32:45] Jan:** ****. She wants to have lunch at 1:30. How about you guys? Is that too late for you? You want to have it earlier?

**[32:57] Rob:** Let me just quickly double check. Lonnie, are you home? I don't know.

**[33:07] Jan:** Okay. So.

**[33:15] Michal:** Yeah, in my case, it's all good, one and 30.

**[33:18] Rob:** It's probably fine for me.

**[33:24] Jan:** Ohh my god! That was beautiful. I just changed the length of the meeting. And it had the title weirdly formatted. And then I shrank it and it had more width and the text was like... Animated.

**[33:48] Michal:** CH. Boo.

**[33:50] Jan:** In A Microsoft product. Amazing. Wait. No, I'm not going to show it to you. Anyways, let's continue with the with the fun.

**[34:02] Rob:** This is my spouse. Hello.

**[34:05] Jan:** Hi there.

**[34:06] Rob:** Hi. Are you okay to have lunch at 1:30? Quite good. Yeah, quite good. Okay, yeah, we're...

**[34:06] Michal:** No.

**[34:07] Jan:** Nice to meet you.

**[34:14] Rob:** We can decide later. OK, yeah, yeah. But 1:30 is OK. Yeah, good. OK, OK. Done.

**[34:22] Jan:** Yeah.

**[34:23] Michal:** This is my.

**[34:27] Rob:** Hey.

**[34:28] Jan:** Yeah.

**[34:30] Michal:** Hello, how are you? Hey there. So, what are you as well? The lunch, no? Yeah, OK.

**[34:30] Jan:** Hey there, good.

**[34:32] Rob:** Yeah.

**[34:34] Jan:** Nice to meet you.

**[34:40] Rob:** Okay. All right, good.

**[34:46] Jan:** Okay, so I'll make a little ASR thing here somewhere.

**[34:52] Rob:** Yeah.

**[34:53] Jan:** And talking about drills, so there is the normal drill. How do you, yeah, just called drill?

**[35:05] Rob:** Right.

**[35:05] Jan:** There is the conversational drills.

**[35:09] Rob:** Mm-hmm.

**[35:10] Jan:** And pronunciation. And each of these needs an evaluator. Right, so... So there's grammar evaluator. and vocab.

**[35:32] Michal:** Yeah. But the conversation there is or live avatar evaluator that is going to be like that part, right? That is other type of the evaluation, right, that we will do or... CH.

**[35:50] Jan:** So, come again.

**[35:51] Michal:** Yeah, because this is for the drill, like the pronunciation, one grammar, vocabulary, the pronunciation, but for the conversation, like the free one that you can speak like with AI avatar.

**[36:04] Jan:** Mmh.

**[36:04] Michal:** That I understand that is other type of the evaluator that we're going to use, right? none of this, right? Or we're going to get the transcription and evaluate it or...

**[36:18] Jan:** Well, I mean, one thing is this. I think it needs more of a closed loop that is more like, which is why I made this little thing here.

**[36:29] Rob:** Right, very evocative of a...

**[36:32] Michal:** Yeah. Like the special case, right?

**[36:34] Jan:** It. Yeah, I think this week like this requires real time. The others are sort of like. You speak and then it's okay if you have like a little bit of processing going on and then get the feedback.

**[36:46] Michal:** Yeah, yeah, yeah.

**[36:52] Jan:** But I mean, even if it's half a, like something that you wouldn't want in a conversation, you don't want it to ask a question and then it takes a while for, well, or you give the answer and then it takes 2 seconds to process, right? This is where the latency will. will break the immersion. Right. Okay, but that's maybe so we have a vocab evaluator and we need a pronunciation.

**[37:19] Michal:** And.

**[37:36] Jan:** And this would work for anything that is not a conversation. And we need to have Audi, so... Are we saying audio is... Audio is what the mobile team gets us the stream. And we have to have the little ASR thing happening here for the... Evaluator, right? And we probably want it. Close to the user input. so that we not only get an audio stream, but also a text stream at the same time. That makes sense.

**[38:31] Rob:** Yeah. I, I assume that, , well...

**[38:35] Jan:** But.

**[38:38] Michal:** But...

**[38:38] Rob:** I assume that... We're going to be giving, for many of these, mostly an audio stream, and then that audio will be later converted into text and sent further.

**[38:52] Jan:** Mm-hmm. Well, that's yeah, that's why I think conversation needs the live ASR.

**[39:03] Rob:** Yes.

**[39:03] Jan:** Whereas the others can have... Async, basically.

**[39:09] Rob:** Yeah, I would agree with this.

**[39:12] Jan:** So that's why we have this little... I don't know where to put it. We could also have like...

**[39:23] Rob:** I mean, what I would do, assuming anyone can and we can remember, is I would color code the arrows. So block is async.

**[39:37] Jan:** Okay.

**[39:38] Rob:** And like some, I don't know, blue or... purple or whatever is like, it's a real time.

**[39:48] Jan:** Mhm.

**[39:52] Rob:** .. Because part and part of why I also say that is that like Daniel make it very clear that everything that touches conversation is going to be doing real-time feeds.

**[39:56] Jan:** And so. Mhm. Okay, so we have ASR living here somewhere. And.

**[40:16] Rob:** Yeah.

**[40:22] Jan:** Oops. Well, maybe I want it like that. I don't know. Well, ASR is needed for. The first three. Right.

**[40:37] Rob:** Mhm.

**[40:38] Jan:** So that one would not use it.

**[40:44] Rob:** Yeah.

**[40:44] Jan:** Mhm. Yeah. Ohh, crap. OK, so we have a little bit of things are going on here, and you're saying we should...

**[41:01] Rob:** Sure.

**[41:07] Jan:** What's your preferred color?

**[41:11] Rob:** ..

**[41:12] Jan:** Yeah.

**[41:16] Rob:** I was, I was gonna say, like, sure.

**[41:23] Jan:** Okay, and do we still have something that comes from here? Or are we saying all the real time is happening over here?

**[41:33] Rob:** ..

**[41:35] Jan:** Grammar evaluation.

**[41:39] Michal:** Yeah, my question is that I understand that real time evaluation is that in the moment we want to correct the user to tell him or tell her that you can pronounce better or how to pronounce some word or is like the feedback be after the. The real-time conversation, like we detected that you can improve this phrase or you can pronounce this better or whatever, or they that you can improve your grammar here or here, what I mean, or it's like the moment of the when we conversation that. After we finish our part, that AI tell us, hey, I detected that maybe this sentence is not grammatically correct. You can say this in other way, like this one or this one or something like that.

**[42:33] Jan:** What's your take on that, Rob?

**[42:36] Rob:** .. Do we need the classification? Maybe I misunderstood my house point.

**[42:46] Michal:** No, yeah, like, because we speak about the evaluators, that is like the normal class, but after that we have the real-time conversation, right? That you speak meaningful AI or without AI avatar, but we want to evaluate the user in the real-time too. It means that I...

**[42:54] Rob:** Right.

**[43:05] Michal:** I'm speaking in conversation. I have conversation with like you and you detected that the sentence that I just mentioned that is incorrect because of some error, grammatical error. And when I finish my sentence, do you tell me, hey, I detected that maybe you can. tell this in the better way because it's incorrect because you use some time that is incorrect that you use the past simple and should be whatever and or something like that is on demand in this the same time like the real-time moment that the AI tried to correct you. Or is like the you finish the conversation we have like the dashboard summary something summary and they that we tell the user that hey after this conversation we detected that you can improve these parts or your pronunciation is good or this word should be improved by your. the of this what should be improved at the pronunciation or the grammatical we need you need to watch out with the how time you use or the grammatical correction or something like that after the class or after the conversation or when you're doing the conversation.

**[44:24] Rob:** I feel like during, I feel like it has to be during. Like, from a pedagogical point of view, I it like... It feels so much more effective if it's during, at least for conversation stuff.

**[44:37] Michal:** Yeah, yeah, yeah.

**[44:40] Rob:** Like I think every, like I think the feedback has to be kind of immediate. I think that's something, again, I know that's a product decision, but I have a hard time believing that anything other than give feedback as soon as it makes sense to.

**[44:56] Jan:** Yeah. I...

**[45:00] Michal:** That in this case is not related with our the evaluators API that we spoke before, right? That the level evaluators API is for the normal class and on the real time conversation or whatever we're going to have other type of the.

**[45:01] Jan:** Ile.

**[45:15] Rob:** I mean.

**[45:15] Jan:** Yeah.

**[45:22] Rob:** I mean, so in terms of things like real time, like, yeah, I don't know how... Like every. What? What's going on?

**[45:50] Jan:** Sorry, I think, yeah, I don't know. I dropped off or something.

**[45:54] Rob:** Okay. All right. So I'll try to repeat what I said. I think for real-time stuff, particularly things like the conversation, we do have to be very careful about latency. We could. Oh, I think we're missing Michal, so. Okay.

**[46:21] Michal:** I think.

**[46:21] Rob:** Milla, do you hear me?

**[46:23] Michal:** Yeah, sorry about that.

**[46:24] Rob:** Yeah. So I was saying for latency, I think we have to be careful about what we put there. So in terms of like, yeah, we want the conversation to be level appropriate. But I'm not sure, like I worry about latency if we have a thing where.

**[46:38] Michal:** Yeah.

**[46:43] Rob:** Every time, like, where right before the text is sent for speech, for turning it into speech, we're like, hey, is this text level appropriate, yes or no? If we have to do that evaluation every time, I worry that might introduce a lot of latency.

**[46:57] Jan:** App.

**[47:03] Rob:** Versus like... For Drew, it's probably fine, right?

**[47:10] Michal:** Yeah.

**[47:12] Jan:** So...

**[47:12] Rob:** Mostly because I think we can almost run it, we can cache it, right? We generate the lesson content, we check that it's level appropriate, and if it clears that, it's in the can, it's good. The lesson content is fine.

**[47:29] Jan:** Right.

**[47:32] Rob:** During a conversation, I think it's like it's going to be rough.

**[47:32] Jan:** No. One thing that I wanted to bring up with regards to conversation is we could make it so that The convert like it's a 15 minute Real conversation going back and forth.

**[47:59] Michal:** And.

**[48:00] Jan:** But I think filling 15 minutes is quite a task. and also like meaning of having a meaningful and guided conversation, right? We want to, there's probably multiple goals that you want to achieve and want to go through and all that. So what I was thinking is you could.

**[48:17] Rob:** Right.

**[48:27] Michal:** Hey.

**[48:28] Rob:** I think his Mac ran out of power.

**[48:29] Michal:** I think so, did, yeah, yeah. But it was like that, right? Buttery.

**[48:36] Rob:** Yeah. All right, let's...

**[48:37] Michal:** Right. Yeah, in this case, like I understand it for the real time conversation with you, we're going to use something like Live Avatar or something like this part of API that is streaming, right, that you speak and he or she or whatever is interact with you in the real time and analyze all of the stuff.

**[48:50] Rob:** Mhm.

**[48:59] Michal:** Inside this LLM, right? And for the trees, we're going to use like the asynchronous API that, for example, what I done for the grammar evaluator, right?

**[49:01] Rob:** Yeah. Yes.

**[49:19] Michal:** Okay.

**[49:20] Rob:** ..

**[49:22] Michal:** Makes sense, but I only want to confirm that this like that two parts, right? That one is the real time that maybe is not related with the trace API that we have, like the grammar level later or pronunciations case that.

**[49:33] Rob:** Yeah, well, I mean, like, I think you do need to still do, I think you still need to do grammar evaluations. You still need to do pronunciation evaluation.

**[49:44] Michal:** No, no, yeah, yeah, yeah, but...

**[49:45] Rob:** Yeah.

**[49:47] Michal:** But you have one part of the practice that is the tricks like normal one and the other one is like the real time conversation that you and could be the real time conversation. I understand that could be short class too, right? That for example, the role play, like you get like the, you want to have some coffee to grab some coffee that you go to like the coffee shop and.

**[49:54] Rob:** Yeah. Yeah.

**[50:12] Jan:** That's right.

**[50:14] Michal:** The size, et cetera, et cetera, right? That could be not like always 10 or 15 minutes of the real time conversation. That could be like maybe 2 minutes, 5 minutes, depend of the topic, like the real role play.

**[50:25] Rob:** Yeah. Yeah, right, and I'm saying precisely for those, I think it's like we probably can throw in a grammar check, a pronunciation check into those conversations. But, like, I'm, it's... If we throw, if we throw in something like a level check, then it's like, oh no, like the feed. Like that might introduce a lot of latency. That was more of the point that I was making.

**[50:59] Michal:** Mhm. Yeah.

**[51:04] Rob:** Did you?

**[51:04] Jan:** No, so yeah, my battery is down and I'm looking for the power supply that someone stole.

**[51:13] Rob:** Oh no!

**[51:16] Jan:** And I only have a...

**[51:17] Rob:** It's okay, I'll give you mine.

**[51:19] Michal:** Yeah.

**[51:19] Jan:** Thank you. Ah, there it is. I have one, the one for travel that only has like 50 watts or something in it.

**[51:22] Rob:** Okay, good.

**[51:31] Jan:** MacBook is really, really drained.

**[51:31] Rob:** No, that's like, yeah, that's. Yeah.

**[51:37] Jan:** Yeah, okay, so I think... I agree on the on wanting the. bigger checks to be done kind of in the background and then be able to decide whether that's something that we want to show. to users and maybe break the flow of a conversation or but have that. be able to decide whether we want to do that or not. I think that's from a pedagogical point of view might not be the best idea to. , break things up all the time, but... Maybe it is. I don't know. Maybe there's... The other thing that I wanted to mention is... With the with the breaking up of a conversation into segments, because you have this, I think we're... Making it a bit more complex than it has to be. Because you could have like a little section of something that you start out with. And once the goal for that is reached, then you can move on to something else.

**[52:55] Michal:** Yeah.

**[52:56] Jan:** Right, and that could even be a hard cut. At the beginning could be 1 little thingy. This is like the... how you order the coffee and then...

**[53:01] Rob:** Right.

**[53:10] Jan:** I don't know, sitting down and talking about how to get to... The theater in the evening is kind of flows into it, but it is a separate segment.

**[53:22] Michal:** Mhm. Hmm.

**[53:26] Jan:** And doing those segments when we when we switch, then you could, for example, you could show the. You, you should, you could show the grammar problems right, so that it's still you don't break up the conversation, but you...

**[53:43] Michal:** Yeah.

**[53:44] Jan:** Kind of like... Quick, free commercial break, like you're not saying this right.

**[53:49] Michal:** Yeah.

**[53:52] Rob:** Sure. And I mean, like, we have these sort of almost all these like sort of structured conversations. And they are all structured conversations. Like, let's be clear, like, if you have, like, if we're trying to have a conversation to sort of someone sort of introduce them, even like from the beginning lessons of introducing someoneselves is like, I'm going to ask you your name. I'm going to ask you how old you are. I'm going to ask you what country you're from. I might ask some follow-up questions if you say something, if you say something interesting, like, oh, I'm from Fiji. It's like, oh, interesting. But it is structured and

**[54:18] Jan:** Mmh.

**[54:18] Michal:** Yeah.

**[54:31] Rob:** You can, I think it's reasonable to sort of expect like, okay, we can do, we can have these sort of natural transition points and there are some things we can do async because it's structured as well.

**[54:46] Jan:** Mhm.

**[54:51] Rob:** All right, you back.

**[54:53] Jan:** I'm back. ... It's sad how little battery you get out of this machine when you have teams running. Okay, so where's the whiteboard? Yeah.

**[55:15] Rob:** Okay.

**[55:16] Jan:** Right. Up. Okay, but thinking in terms of... Tickets and planning, what we need is the... The ASR in two levels, right? The ASR.

**[55:39] Rob:** Yeah.

**[55:46] Jan:** The real-time. ASR and the not so real-time ASR. They think. Yeah. And the difference is... If we're differentiating that, we're doing that. Because why are we doing it? Is there, is there like, do we think cost and performance is going to? Async, we can do other stuff that is cheaper and... gets okay results and time is more challenging.

**[56:30] Rob:** Some of it is cost, some of it is, I think, to reduce latency.

**[56:37] Jan:** Mm.

**[56:37] Rob:** Like if there are things you can do, if there are multiple things you can have running while things are happening so that as the conversation moves, it's like, think of it this way. Like if in the second part of the conversation, you're going to ask someone how old they are. that script can be generated in advance, or like that text can be sort of generated in anticipation.

**[57:04] Jan:** Right.

**[57:04] Rob:** And then the perceived latency of the conversation is better.

**[57:11] Jan:** Mhm.

**[57:13] Rob:** Like if you already know what you're going to say for the second part. That can be like, oh yeah, that was interesting. Anyway, how old are you?

**[57:25] Jan:** Yeah, yeah. Yeah.

**[57:28] Rob:** I know these structured conversations always feel very wooden. I'm sorry.

**[57:29] Jan:** Cat. So, Rob, by the way, what's your favorite color?

**[57:40] Rob:** Yeah. Yeah. The.

**[57:48] Jan:** Okay, cool. So we need to build these two.

**[57:48] Rob:** I see.

**[57:54] Jan:** What else do we have? We have the these guys here and we have the conference conversation.

**[58:00] Rob:** Alright, *******.

**[58:06] Jan:** Thingy. So in order to have a conversation, conversation. ... That needs. I need some input, right? Like... So, if we call these conversational drills.

**[58:43] Rob:** I, I'm a little unsure what a conversational drill is supposed to be.

**[58:55] Jan:** Mm.

**[58:58] Rob:** Do we have a, is there, is there an issue already written for? Let me see what the issue says.

**[59:26] Jan:** I think for me, it becomes a conversational drill. when it's not free, unbounded conversation.

**[59:40] Rob:** Right, so I have here a guided conversation epic.

**[59:46] Jan:** Mhm.

**[59:50] Rob:** And... So, in the acceptance criteria for, I'm just... I'm just going to quickly read it out because it's... Relatively short. It's a scenario selected from the scenario library.

**[1:00:05] Jan:** No.

**[1:00:06] Rob:** Then, then you're guided through the scenarios of defined objectives. There is a start end tied to the scenario's completion, and then... , you're sort of scored based on like, did you kind of successfully make it through?

**[1:00:24] Jan:** Mhm.

**[1:00:25] Rob:** The scenario. That's the closest thing I have recorded that looks like a conversational drill.

**[1:00:33] Jan:** Right, I think, yeah, exactly, and I think the... The reason is it should not feel as much on rails as the other.

**[1:00:47] Rob:** As things like vocab and grammar drills.

**[1:00:50] Jan:** Exactly, yeah. In those you will have your multiple choice, right? This is like, this is you practicing. I guess that's, now that I say it.

**[1:00:59] Rob:** Right, right.

**[1:01:05] Jan:** The conversational drills could be part of the... what's called perform and what usually is done by the tutor.

**[1:01:23] Rob:** So...

**[1:01:23] Jan:** ..

**[1:01:26] Rob:** So I mean like the way I sort of see the scenario is there's you have some test, your scenario, like, you're trying to order the pizza, a pizza over the phone. So it's like, you introduce yourself, you're going to ask for the pizza, you're probably going to be asked for the dress, you're going to ask, you might, you'll have to ask how you expect to pay for it. And then like, I don't know, maybe you should politely say goodbye to the person you're talking to. And throughout that scenario, you're still being great on pronunciation, grammar, like you're still.

**[1:01:59] Michal:** Mhm.

**[1:02:10] Rob:** There's still going to be some notion of that. whether you be corrected in the scenario or not.

**[1:02:20] Michal:** I think so, that depends of the case, right? That maybe when you want to order the pizza, that is not a good idea to that the guy that is doing the role of the get the phone and asking you what you want to order, that he correct you. Maybe not, but when you have like the class with the AI tutor, that in this case might be yes.

**[1:02:24] Rob:** Yeah. I... I will tell you in Germany they definitely correct you.

**[1:02:42] Michal:** Yeah. Yeah. Could you repeat that?

**[1:02:46] Rob:** It's like, , is kind to Martin.

**[1:02:51] Michal:** Ah.

**[1:02:55] Rob:** So they definitely, I can't speak for a formal learning environment, but in the world, when you, if you will be corrected, so like.

**[1:03:07] Michal:** Yeah.

**[1:03:08] Rob:** But yeah, yeah, there is this notion of like, you're proceeding through steps and there's sort of a little bit of evaluation going on through the steps, like, some, someone says, yeah, we don't have, . we're out of cheese. I don't know, something like that. So there is a sort of like you kind of have to navigate that a bit. And then at the end, there's an assessment. So, as in terms of the API there, I can sort of see that like... There are sort of, it almost looks like a lesson because there are sort of steps you have to go through.

**[1:03:52] Jan:** Yeah.

**[1:03:55] Michal:** Yes, sir.

**[1:03:56] Rob:** In the in the like, it does almost feel like a lesson, because there are these steps you're kind of going through. There's possibility of feedback for each of them, and then there's an assessment at the end.

**[1:03:56] Jan:** Yeah. Mhm.

**[1:04:18] Rob:** So...

**[1:04:18] Michal:** Okay.

**[1:04:20] Jan:** Okay, I'm making this on this side here because for like I have to look it up if there's more to conversate like for me conversation we could. frame it as something that is... ... Yeah. I like the example that you were giving. You could have something that is like you practice how to do stuff on the phone and all that. And it kind of is, it's not so old school, multiple choice E anymore, but it feels more like. conversation because you have the text output and then you respond with your voice. But then once you've done your practice, then it's on to a real conversation.

**[1:05:18] Rob:** Right.

**[1:05:18] Jan:** And that could be a 5-minute thing where you... Order your pizza. On the phone.

**[1:05:28] Rob:** Right.

**[1:05:30] Jan:** And, and that would be sort of in... In the way that, , Srikant is saying this is like... This is the learn bit, this is the practice, and the conversation would live in the tutor area.

**[1:05:50] Rob:** Right.

**[1:05:51] Jan:** Right, I'm. I have to say, I'm not. I'm not agreeing with him so much that we should split this up so rigidly. For me, it should be you learn a little bit of practice, you learn some more, a little bit of practice.

**[1:06:08] Rob:** Yeah, so for this is where I kind of feel I also kind of am a little confused about what's going on with you. But then like for me, like when I look at the mockups of what's tutor, it's literally booking a tutor. So I'm a little confused there. Because from my perspective, I see something much closer to like what Duolingo has where like,

**[1:06:22] Jan:** Right.

**[1:06:30] Rob:** You could have some of these fairly on rails lessons, and then you have something that opens up a little bit in like a guided conversation.

**[1:06:39] Jan:** Mhm.

**[1:06:39] Rob:** And it lives much more in the lesson path.

**[1:06:43] Jan:** Right. Okay, does it matter for us now if a conversation is something? Small versus something that is bigger, longer.

**[1:06:58] Rob:** I think from an API point of view, it does not matter. But open conversations, I think. are implemented differently enough from guided conversations that we have to like. Accounting for that. But lengthwise, I don't think it matters too much.

**[1:07:29] Jan:** Mhm. I mean... I think, yeah, I mean, that's how, like, I don't like that pronouns here. I even sits here. It just feels weird.

**[1:07:46] Michal:** On top.

**[1:07:46] Jan:** Or is there, how do we do that on my Berlitz right now with the with the Tokyo stuff? Is there a pronunciation?

**[1:07:46] Rob:** Right.

**[1:07:55] Jan:** Drill.

**[1:07:55] Rob:** No, there's no pronunciation lessons. Pronunciation is just something that happens. Well, actually, pronunciation, there's no pronunciation lessons. Pronunciation is just a thing that could appear in your lesson evaluation, and we don't even have it enabled.

**[1:08:15] Jan:** Okay. Okay, I'm going to remove it up here.

**[1:08:18] Rob:** No one on Berlitz is getting pronunciation assessment currently.

**[1:08:22] Jan:** OK, cool. OK, so I would. We'll call this conversation drills, and then there is... The... Free conversation.

**[1:08:42] Rob:** Mhm.

**[1:08:47] Jan:** And...

**[1:08:51] Michal:** I don't know why I don't see your mouse, Jon.

**[1:08:54] Jan:** Sorry. Yeah, because, yeah, yeah, sorry. No, you don't.

**[1:09:05] Michal:** Okay.

**[1:09:07] Jan:** Sorry, I thought you guys saw that, but you couldn't. Okay, so we have... And this would also be in practice. And I want to... Want to have the tabs, Srikant 3 tabs in here. So. We have learned. We have practice. And free conversation is more the tutor kind of thing, I believe.

**[1:09:59] Rob:** Yeah. In all the screens I've seen for Learn, I also like...

**[1:10:01] Jan:** And then...

**[1:10:06] Rob:** It's not, it just looks like the home screen to me.

**[1:10:11] Jan:** Yeah.

**[1:10:12] Rob:** But...

**[1:10:21] Jan:** Kadistan. Office. All right, so this is Tutor. These 2 are practice. Support.

**[1:10:37] Rob:** All that fun.

**[1:10:40] Jan:** And there's learn. Yeah.

**[1:10:45] Rob:** Mhm.

**[1:10:46] Michal:** Mhm.

**[1:11:04] Jan:** Okay, I'm not going to make this any prettier at the moment. Okay, so we have going back to... Going back to the whiteboard.

**[1:11:30] Michal:** Okay.

**[1:11:33] Jan:** Where were we? We have the conversation. Nicole conversation. Runner. Thingy.

**[1:11:52] Rob:** Mhm.

**[1:11:53] Jan:** Module. Potel.

**[1:11:57] Michal:** Controlling sounds good, right?

**[1:12:01] Jan:** The module is also a... A piece of content. Maybe.

**[1:12:08] Michal:** Mm.

**[1:12:10] Jan:** For lack of better words. So. MVP.

**[1:12:20] Michal:** Component.

**[1:12:23] Jan:** MVP, you have conversation component, whatever. Dog food is, we have a scenario, right? Scenario. Be able to run a. conversation scenario.

**[1:12:49] Michal:** Mhm.

**[1:12:49] Jan:** Rob, when you when you looked at Tokyo. So. What kind of... Can we have a look together real quick? , what kind of... drills or sessions or whatever they had in there or what the conversation scenarios were.

**[1:13:11] Rob:** There was open conversations. I've been having trouble logging into Berlitz Hub recently, so like, otherwise I share my screen.

**[1:13:20] Jan:** I can try.

**[1:13:22] Rob:** Okay, if you want to try to log into Berlitz Tub. Using the whatever ID credentials you have.

**[1:13:40] Jan:** Well, look at that.

**[1:13:43] Rob:** Okay, what?

**[1:13:43] Jan:** Is that it? It has pronounced it. What is speak? With call. Yeah, sorry, I did that wrong.

**[1:14:14] Rob:** Oh yeah, yeah, they have this, they have this, this sort of thing, but I don't have an agent thing. This is just their...

**[1:14:42] Michal:** Yeah, it's like the our pronunciation right that we want to implement on the app.

**[1:14:49] Jan:** All right, so we have Wordbook. Ah, Wordbook is probably something that we are missing also. Or is it? I think it's one of the drills.

**[1:15:01] Rob:** But...

**[1:15:02] Jan:** I have to check. So. This needs. This is a pronunciation. Fill, right? And... There is the word.

**[1:15:34] Michal:** But practice drill, 12 drills, that is not the same that we have inside the practice drills, the pronunciation drill, or is like the... In lesson loop you have the practice 12 drills that is not pronunciation drill included.

**[1:15:57] Jan:** .. I don't know. I'll have to check. And same with workbook. I'm want to say it's in the drills. But maybe not.

**[1:16:13] Michal:** But what book is your progress? What you learn it or what you have the problem with some words and... Is what I understood from the Tokyo, right?

**[1:16:24] Jan:** Right, I think this, yeah, this is something that you add to it.

**[1:16:28] Michal:** Yeah, I don't know if you only can add or maybe it's automatically added from your before lessons, but... That you take, but...

**[1:16:39] Jan:** No, I don't think this is automatically done, no. This is right now, it's like just you, you find that interesting and...

**[1:16:49] Michal:** Yeah, and you add the the words to.

**[1:16:54] Jan:** Right, okay, and then I have my daily search. So, but... I think we're losing Rob.

**[1:17:03] Rob:** I'm trying, I'm trying to log into the.

**[1:17:04] Jan:** It. The.

**[1:17:09] Rob:** Because this isn't the view I was talking about.

**[1:17:14] Jan:** Anymore because I started this. Hello, Tim. Is there a topic you want to talk about today? If not, I have a fun question we can try.

**[1:17:14] Rob:** So. Ah, here, here, I found it, I found it. Okay.

**[1:17:36] Michal:** Do we shut the stream, Rob, or?

**[1:17:36] Rob:** I wrote this. Yes, I will share my screen.

**[1:17:43] Michal:** Okay.

**[1:17:44] Rob:** Hold, please. So... Let me. Do that. Yeah, so there's this thing here, so let's go to... And I'm just going to like. I'm just going to paste the URL because maybe... Some of us also, maybe there's a way to access it that I don't know.

**[1:18:13] Jan:** Okay.

**[1:18:16] Rob:** ..

**[1:18:24] Michal:** Could you invite me, or?

**[1:18:27] Rob:** Well. I don't remember how I like got here, but I'm just going to, yeah, okay, let me just share the screen again.

**[1:18:37] Jan:** It.

**[1:18:38] Rob:** So... Like this is, there's a whole content library here. Which has the prompts and the template categories and everything, so... And I'm just going to show because it's, so they're sort of just, you can just talk, they're just open-ended conversations you can just have. And there's a sort of a prompt of how the person's view is supposed to behave. There's...

**[1:19:06] Jan:** Oh, that one I didn't realize. We have that. Okay, so this is for the all of this is for the avatar or for the audio chat.

**[1:19:10] Rob:** Yeah. For both audio and video, both are here. So you have a role play thing where it's like, describe the work you do to a new employee and it's like, act like a worker.

**[1:19:20] Jan:** How do you?

**[1:19:29] Rob:** And then give some example questions to ask, and then there's some target vocabulary that they're supposed to hit.

**[1:19:41] Jan:** Oh, OK. And...

**[1:19:44] Michal:** No. We can download this content or something like that.

**[1:19:46] Jan:** And.

**[1:19:49] Rob:** I have already shared with you, Michal, the, I've already shared all the Excel documents that have this content. We don't have to download or scrape it because we already have it downloaded.

**[1:19:52] Michal:** It.

**[1:20:04] Rob:** At least for English.

**[1:20:07] Michal:** Okay, perfect.

**[1:20:09] Rob:** So, all the we all have all the information here we already have in the document, so...

**[1:20:16] Michal:** Okay, perfect.

**[1:20:19] Rob:** I'm only sharing this because... This I think gives probably the best high level view of like, what is the content look like and what are the lessons look like? Obviously I can go in and like start the lesson for you to see, but I think... I think this is a much better place to kind of at least see how it looks like that.

**[1:20:51] Jan:** Okay.

**[1:20:54] Rob:** And also for the different vocabulary, like... I believe I've showed this to you. , Jan, when we met at the coworking space, but they, there, there is sort of a way to sort of show it for. different phrasing. So for pass on, you get all the like pass on, passes on, passing on, pass John on, passes John, like even all the different formattings.

**[1:21:30] Jan:** Yeah. OK, and this. Where do these appear? Like now you have something that is called take down and pass on information.

**[1:21:46] Rob:** Right, so if we kind of open it in the chat. Peres here. Hello, I am interested in placing an order for some custom made items. I am a repeat customer. My store is upscale. So I don't know how much audio you heard or audio that I was talking, but I was just showing that in the screen you have the audio on the left.

**[1:22:19] Michal:** Yeah.

**[1:22:21] Rob:** The vocabs on the right, as you use the vocab, it'll kind of flash and go away. This is, I think, one of the more guided, this is what the role play exercises look like that Tokyo is implemented.

**[1:22:35] Jan:** When would I be taking this? Is this at the end of?

**[1:22:43] Rob:** So this is unit 19, so I suspect this is a...

**[1:22:43] Jan:** Yeah.

**[1:22:50] Rob:** This is maybe not the initial modules, but even like for Berlitz flex. There is some role-playing exercises that are like... But I am, to answer your question, I'm not sure which level these are in. , so okay, this, yeah, English 6, okay. Sorry, yeah, this is English level 5 is when these are in.

**[1:23:21] Jan:** Can you? Mm. So I have Berlitz English, Felix English 2.

**[1:23:33] Rob:** Support. So, here's for English one. And for English one. It's a very, it looks like it's just a structured conversation.

**[1:23:46] Michal:** Yeah.

**[1:23:47] Rob:** So, you're so basically the prompt is you're told to ask about nationality, country, city. and make sure to ask at least, make sure the student asks at least five questions.

**[1:23:59] Michal:** Mhm. And what is the feedback tab that I saw on the on the top?

**[1:24:13] Rob:** This is feedback from users that have taken this lesson.

**[1:24:14] Michal:** Ohh, OK then, OK.

**[1:24:18] Rob:** And it's a pretty basic one; they didn't they didn't leave anything there, yeah.

**[1:24:20] Michal:** Yeah, you like it or not?

**[1:24:25] Rob:** And they liked it, which, okay, fine.

**[1:24:32] Jan:** Hmm.

**[1:24:35] Rob:** Yeah, I found this view with the content library and the user manager progress much more helpful for understanding what Talki has built and how people interact with it.

**[1:24:50] Jan:** Okay, this looks to me... Nick. If I looked at unit 6 lesson, what is this, English 2 or 1?

**[1:25:04] Rob:** Here.

**[1:25:05] Jan:** Mhm.

**[1:25:07] Rob:** This is some BPO module, but we can look over, if we look here under flex or... Shara, they have more, , which level it is.

**[1:25:22] Jan:** I don't, I would like to know where that where those are shown in the in the learner path.

**[1:25:30] Rob:** Yes, that would be good to know. I do not know. We can ask, I think we can ask Nicolas and John just to double check.

**[1:25:38] Jan:** Mhm. Practice pub.

**[1:25:46] Rob:** You also might have some luck in asking the knowledge base, what is the what are BPO modules?

**[1:25:46] Jan:** Right. Yeah. Well, OK.

**[1:26:04] Rob:** Okay, is there anything else I should show here or should I stop sharing screen?

**[1:26:06] Jan:** Something. So the assumption is what you're, what we're looking at here is the different, this is not something that a student sees, right?

**[1:26:19] Rob:** No, no, no, no, this is...

**[1:26:21] Jan:** This is some definition of some admin definition for. All these are supposed to go. And apparently... Can, can you, can you again open one, please?

**[1:26:39] Rob:** Sure, maybe give your address and phone number.

**[1:26:45] Jan:** My tutor, because it looks, ah, wait, so I'm, I think I'm on the user side of things. You have the admin side.

**[1:26:54] Rob:** Right, and I don't remember how I got here.

**[1:26:59] Jan:** Ah, oh, okay. And then... I can, I can begin my daily session, or I click on... Scenario, topics, quiz.

**[1:27:14] Michal:** Correct.

**[1:27:14] Jan:** For discussion. Discuss a case and answer questions about it. Interesting. Okay, so... We have to find out if this is integrated into the... Overall learner path.

**[1:27:34] Rob:** Mhm.

**[1:27:35] Jan:** I can't, I don't see that at the moment.

**[1:27:38] Michal:** Because you have the link right, like the direct link to the to the lesson.

**[1:27:42] Rob:** Yeah, I don't know how these are then turned put into the learner path.

**[1:27:50] Jan:** How do we see? Which is? ... If this is audio or avatar.

**[1:28:02] Rob:** Remember, , I think these are all, , these all are both.

**[1:28:08] Michal:** I think so that you have the category on the...

**[1:28:10] Rob:** Because at any moment you can open it and you can get the avatar or the audio. Like, you can have both.

**[1:28:15] Jan:** Ah, okay, let me, let me.

**[1:28:16] Michal:** Yeah, but if you go to the class, I think so that you have, if you go to the administration part. But I think so that you have marked that if is the like the video or text or both, if I'm not wrong. If you go to practice tutor, custom video tutor, in this case you don't have the tutor. And user input, yeah, you have this peak and right, you can.

**[1:28:47] Rob:** Right, you can enable whether for at least on the audio side, you can enable whether this user, so yeah, just we're not gonna.

**[1:28:55] Jan:** Yeah.

**[1:28:55] Michal:** And if is video or not like that with the...

**[1:29:00] Rob:** So...

**[1:29:02] Michal:** Yeah, user input, yeah.

**[1:29:05] Jan:** Okay, yeah, no, yeah, it's here. When you, when you, as a user, go through the thing, you select your scenario, and then it asks you a similar.

**[1:29:13] Rob:** Mm-hmm.

**[1:29:18] Jan:** .. Similar to what you've shown, that you can start a conversation or you can start a video conversation. So audio or video, because we have that number floating about that audio is outperforming video by a factor of 10.

**[1:29:28] Michal:** Yeah.

**[1:29:35] Rob:** Okay.

**[1:29:35] Michal:** Oh.

**[1:29:38] Rob:** Yes.

**[1:29:39] Jan:** Ohh. which is interesting. [unclear].

**[1:29:51] Michal:** And.

**[1:29:53] Jan:** Okay. And...

**[1:29:57] Michal:** And. I have other question that I don't know what is the progress tracking.

**[1:30:03] Jan:** Hello, welcome to the clinic. Would you like to book a doctor's appointment today? Sorry.

**[1:30:05] Michal:** And. Mm. And the progress, yeah, that and the progress tracking that they get something more than if you like it or not the lesson or I don't know if they detect something that some grammar or some pronunciation or whatever gaps you have to.

**[1:30:10] Rob:** Well, at least your audio works. Progress, so...

**[1:30:29] Michal:** Or to do this exercise or practice with you in the future or it's only that you like it, not like it, the lesson. Or that you took or not. Oh.

**[1:30:45] Rob:** It's mostly did you take or not? ...

**[1:30:50] Michal:** Pronunciation chat, video chat, total chat test.

**[1:30:58] Rob:** So.

**[1:30:59] Michal:** Speaking time, listing time, words. Sentence broken. But it's like the, how many? Ohh yeah, yeah.

**[1:31:18] Rob:** Yes, but it's fairly, it's at the granularity of a lesson. So they do a lesson, there's sort of an evaluation of them at the end of that lesson, how much time they spent, how well they did, how much they used it.

**[1:31:38] Michal:** Mm.

**[1:31:39] Rob:** But it's. things that are more detailed like the transcripts and like, like you can go and look at the past conversation you had and see what you said in it. But in terms of like dashboard stuff, we have to go at the level of postman to like go in there and like, really analyze the lesson and things like that. You find something more detailed.

**[1:32:07] Michal:** Thank you.

**[1:32:14] Rob:** ..

**[1:32:28] Michal:** Hey, Cat. Bye.

**[1:32:38] Rob:** Okay, I guess I am out of here. Yeah, Jan, you should be able to log in here, like...

**[1:32:44] Michal:** Yeah.

**[1:32:51] Rob:** So.

**[1:32:55] Michal:** I don't hear you, Ian. You are on mute, or I think so, not mute, but maybe.

**[1:32:56] Rob:** Okay. Maybe the page took over Jan's...

**[1:33:02] Michal:** Yeah.

**[1:33:05] Rob:** Mike, which? Happens. , shall I stop sharing screen? I, I mean, like...

**[1:33:14] Jan:** No. Can you hear me now? Hello. Good. Perfect.

**[1:33:19] Rob:** Yes, yes.

**[1:33:19] Michal:** Yeah.

**[1:33:22] Jan:** I had to close the window.

**[1:33:24] Rob:** Alright, maybe, maybe courses can, maybe this will be a no, there's nothing here. Never mind. No.

**[1:33:34] Jan:** Okay. Yeah, I mean the way that it is. is shown here is you have to know what you want to do.

**[1:33:48] Rob:** Yeah.

**[1:33:49] Jan:** Just kind of... I think that there should be. I don't know. We need to suggest something to the user that makes sense. ... Okay, I'm going to share again.

**[1:34:12] Rob:** Okay, yeah, I'm gonna stop sharing, so...

**[1:34:20] Michal:** Okay.

**[1:34:21] Jan:** Whiteboard, and well, actually, I'm going to share PowerPoint.

**[1:34:31] Michal:** Yes.

**[1:34:36] Jan:** Okay, so we have pronunciation drills, workbook drills, and we have conversation drills. This is what we just...

**[1:34:41] Michal:** Oh.

**[1:34:44] Jan:** For conversation, should I call it scenarios?

**[1:34:55] Michal:** Mm.

**[1:34:58] Rob:** Yeah, maybe scenarios.

**[1:35:02] Michal:** But I think so that we have the scenario libraries right in our issues.

**[1:35:06] Jan:** Exactly, yeah. Then I want to, we have to, I have to figure out if that is something that Claudio made up or if that's actually a thing. Well, it sounds nice. Right, so we want to generate a library of scenarios.

**[1:35:23] Rob:** Yes.

**[1:35:28] Jan:** .. which in my view is just a different output here.

**[1:35:35] Rob:** Mhm.

**[1:35:38] Jan:** And... I. I'm. Okay, that's I think something for later to discuss is for me, practice drills. And conversation drills.

**[1:36:01] Michal:** Mm.

**[1:36:01] Jan:** Should be kind of interchangeable at some point. I think we should be able to do both. Right, so you have like your scenario definition or your goal definition and it can generate some practice drills.

**[1:36:12] Rob:** Mhm.

**[1:36:23] Jan:** From it.

**[1:36:24] Rob:** Right.

**[1:36:25] Jan:** But it could also... Have a... I'll put a conversation scenario that essentially does the same in terms of learning goal.

**[1:36:40] Rob:** Right.

**[1:36:41] Jan:** And then we can, like, I think we at some point we should then go into heavily into like AB testing what works better.

**[1:36:51] Rob:** That's right, yes. I think that's...

**[1:36:55] Jan:** Because we have some assumptions here, but... We need to let that we need to optimize, I think. A lot.

**[1:37:05] Rob:** Yeah, which is why I'm also sort of pretty keen to like have something minimal and then we kind of go from there.

**[1:37:05] Jan:** .. Mhm. Okay, so pronunciation drill and workbook might go in here. . Conversational drill scenarios, state conversation. ... Okay.

**[1:37:40] Rob:** So, okay, yeah. I have a, okay, I logged into the Berlitz Flex learning path if we want to look at that. If we don't, that's fine.

**[1:37:49] Jan:** Ohh, please, if you can, if you can highlight if the, if you can figure out if there are...

**[1:37:53] Rob:** Sure.

**[1:37:58] Jan:** Avatar sessions in there.

**[1:37:58] Rob:** ..

**[1:37:59] Michal:** Yes.

**[1:38:00] Rob:** So the thing, so the way it's sort of set up is there, this is at least in Berlitz Flex. There's a practice lesson, you have the different lessons. And then kind of in there, there can be a live coaching session, a review lesson, and then it kind of, it's. And then as part of them, as you sort of complete them, you could also have this sort of tutor lesson in there that's kind of mixed in.

**[1:38:25] Jan:** Mhm.

**[1:38:30] Rob:** And so that's at least how it's sort of set up. There's this like... You're just doing them in order with different things kind of slotted in.

**[1:38:41] Jan:** Right. Why don't I see that? what?

**[1:38:48] Rob:** But.

**[1:38:48] Jan:** Sorry, it the modules fit so nicely on my screen. And it wasn't showing any like left or right navigation thingies that I thought I was just looking at 5 and that's it.

**[1:39:02] Rob:** Mhm. No, no, there's this like, there's, it's a, it's this, yeah.

**[1:39:10] Jan:** There's this long carousel sort of thing without the UI for a carousel, which is...

**[1:39:12] Rob:** Yeah, exactly, yeah. Well, ish, it's a little like... It's not great.

**[1:39:22] Jan:** Sorry, I'm so stupid.

**[1:39:24] Rob:** No, no, no, no, no, this the UI is a little funny.

**[1:39:24] Jan:** Up. OK, so I move to the to the right, keep moving, and why do I? I'm in English too, so there should be...

**[1:39:37] Rob:** Right. I think we're logged into the same account because I think we were basically given the access to the same account.

**[1:39:42] Jan:** Exactly, so.

**[1:39:44] Michal:** Would you share this account with me, too?

**[1:39:47] Rob:** Yes.

**[1:39:47] Jan:** Yes. We should actually, can we put that in our knowledge base? I think I tried and then GitHub realized that it was credentials and didn't want to put that on GitHub.

**[1:40:00] Michal:** But we have some password manager or...

**[1:40:04] Rob:** We should start doing, we should start doing, we should get into like a habit of not just dumping credentials onto repos anyway, but I'll set what I think we should do is we should either commit to... AWS secret sharing or one pass something and basically. The idea is that we'll dump the we.

**[1:40:34] Michal:** Yeah.

**[1:40:38] Rob:** We essentially have some way of like accessing this information that Claude can like interact with. It's not awful.

**[1:40:47] Jan:** Mhm. , Rob, I think you are... logged in as someone else because you have module completion which I don't have.

**[1:41:02] Rob:** Oh, okay.

**[1:41:02] Jan:** My module is at 0 and I can't really do anything; it's everything in the future.

**[1:41:05] Rob:** Okay. Because this is the credentials I logged in as.

**[1:41:10] Jan:** I thought I also logged in with those.

**[1:41:15] Rob:** So.

**[1:41:15] Jan:** Let me sign out and sign back in.

**[1:41:18] Rob:** Okay, I'm going to stop sharing my screen.

**[1:41:28] Jan:** Okay, Berlitz, Felix, English 2.0. Continue.

**[1:41:43] Michal:** If you want to share.

**[1:41:45] Jan:** Mm. Yeah. That's horrible. Okay, I fool. Oh no, I have a learner path. And I have described travel plans. Ask about schedules.

**[1:42:14] Michal:** I don't see your screen, but...

**[1:42:14] Jan:** And. Or, it's a quiet place, OK.

**[1:42:24] Michal:** Yeah. Okay.

**[1:42:32] Jan:** Oh. So... All I was doing is, with the credentials, are you sharing them, Rob?

**[1:42:41] Rob:** The credentials.

**[1:42:42] Jan:** Yeah.

**[1:42:44] Rob:** I mean, I can share them.

**[1:42:46] Jan:** Yeah, I mean, it's just a demo account.

**[1:42:48] Rob:** Yeah, yeah, hold on. Can I just, I'm just gonna paste them in the chat.

**[1:42:49] Jan:** Work for everything. There seems to be like 2 sections to it.

**[1:43:03] Rob:** ..

**[1:43:09] Michal:** Hey.

**[1:43:11] Jan:** Why? Why? Why do I have to do this again?

**[1:43:19] Rob:** I don't know.

**[1:43:21] Jan:** I just want the.

**[1:43:24] Michal:** You can remove the... The things, if you want the message. With password and... Use that. Okay.

**[1:43:47] Jan:** The. Okay. Hey, I heard you're planning a trip soon. Where are you going? You still hear me?

**[1:44:13] Michal:** Yeah.

**[1:44:14] Rob:** Yeah, yeah, I hear you.

**[1:44:15] Jan:** Awesome. Okay.

**[1:44:16] Rob:** We also heard the lesson. It's all good. All right.

**[1:44:18] Michal:** You go to directly to this class, right? And this open it.

**[1:44:18] Jan:** CH.

**[1:44:22] Rob:** Okay.

**[1:44:24] Jan:** Okay, so...

**[1:44:24] Rob:** Okay.

**[1:44:26] Jan:** So, we...

**[1:44:26] Rob:** So I was slightly wrong. There is a place to do pronunciation. Off to the side that Tokyo did provide.

**[1:44:41] Jan:** Right, and the... conversation drills, have you ever, do how they end?

**[1:44:53] Rob:** ..

**[1:44:54] Jan:** Do they have something like, now we covered everything, so we're fine?

**[1:44:55] Michal:** And.

**[1:44:59] Rob:** When the conversation ends, you get the lesson assessment, like this screen kind of pops up.

**[1:45:06] Jan:** But do you do that like as a user? Do you stop it?

**[1:45:11] Rob:** I mean... When I've gone through the conversations. I kind of just like. I just kind of just click stop the conversation and just see what it says.

**[1:45:25] Jan:** No.

**[1:45:26] Rob:** And I mean, I think you could do that. Like you could now just say like, hi, hello. And then at the end, like, be like, that was enough.

**[1:45:37] Jan:** Let me do that real quick.

**[1:45:39] Michal:** OK.

**[1:45:42] Rob:** Cause. Because at the right... like you can just click conversation assessment. Like I bet you can use all four words in a single sentence and it'll be fine.

**[1:46:10] Michal:** Yeah.

**[1:46:26] Rob:** Oh, the other thing that's worth mentioning with the UI is you have to hold space to record for it to hear you. So, it's it's very it's push to talk.

**[1:46:38] Michal:** Yeah, yeah, yeah. And sorry if you're hearing some explosions here because the people are preparing for the holiday.

**[1:46:45] Rob:** And then like.

**[1:47:13] Michal:** But yeah.

**[1:47:19] Rob:** Alright, well, yeah, let's see what happens if you say getting, I guess.

**[1:47:22] Michal:** Yeah. You have animation and other stuff with confetti.

**[1:47:33] Rob:** Okay, but then like...

**[1:47:42] Michal:** Are you over?

**[1:47:45] Rob:** Wait, hold on.

**[1:47:47] Jan:** Can you hear me?

**[1:47:48] Michal:** Yeah, no, yeah.

**[1:47:49] Rob:** Yes.

**[1:47:50] Jan:** Thank you. Okay. Thank you.

**[1:47:51] Rob:** But if you click conversation assessment, like this little pop-out screen appears.

**[1:47:57] Jan:** Yeah, I, I, sorry, yeah, I closed the window, , but, well, actually...

**[1:48:07] Rob:** Yeah, so like, if you...

**[1:48:07] Jan:** Yeah. Yeah, I saw that before. No, to me it just feels stupid because if the target vocabulary, she's not asking me questions that allow me to use my target vocabulary. She's like...

**[1:48:22] Rob:** Right.

**[1:48:27] Jan:** Not helping, and... Yeah, I don't know, that is a **** experience.

**[1:48:34] Rob:** And if you look at the assessment, the pronunciation is nowhere on it. Oh wait, okay, I guess it is now. All right, fine.

**[1:48:41] Michal:** What's that?

**[1:48:42] Jan:** Yeah. Talk. Father.

**[1:48:54] Rob:** Talk. Talk.

**[1:48:56] Jan:** Okay, whatever.

**[1:49:00] Rob:** I don't know. I feel like you say... I don't know. I feel like your pronunciation is fine. I'm a native English speaker. I don't know.

**[1:49:05] Michal:** This.

**[1:49:09] Jan:** Okay. So... We need more. So, I mean, the my idea is that we... On the whiteboard.

**[1:49:28] Rob:** Okay, let's go.

**[1:49:30] Jan:** We need to add a bunch of... Bunch of... Post it for what we do here, drill, drill, learner path, level assessment, front end, like that. No, no progress path. And then... Do we have one? Do we have a post it for the for the drills?

**[1:50:10] Rob:** I just see evaluators. I don't see drills.

**[1:50:10] Jan:** Rob. Right, and that was because we were saying like presentation and drills is like front-end stuff that we don't care about.

**[1:50:21] Rob:** Well... We said, we were saying that. We were saying that the... I don't, there's what you said. What does presentation mean in the Berlitz method is different than front end. And I'm not completely clear. What presentation means in the Berlitz method? I've downloaded a few like instructor guides that I'm just going to physically read, but I haven't done it yet. What?

**[1:50:53] Jan:** That's a good idea. Please do share them.

**[1:50:57] Rob:** It's all the stuff that Martin has already shared. It's just... He shared them, I just didn't read them.

**[1:51:03] Jan:** Okay, one time. ... Okay, presentation is... Teacher standing, teacher lecturing.

**[1:51:17] Rob:** Okay.

**[1:51:18] Jan:** Or video being played that... Shows something that is a learning, so presentation is really...

**[1:51:23] Rob:** Okay. Okay, so it's...

**[1:51:29] Jan:** Presenting something. Right, so it's like...

**[1:51:32] Rob:** So that does feel like static content.

**[1:51:34] Jan:** Right, that is static content, 100% front end, like no, very little interaction.

**[1:51:41] Rob:** Okay.

**[1:51:41] Jan:** Like, play, pause. That, that's about it, and...

**[1:51:45] Rob:** Okay, play, pause, adjust speaking rate. Sorry, adjust speaking speed.

**[1:51:53] Jan:** Yeah, yeah, that's an important feature, I think. Overall, yeah.

**[1:52:00] Rob:** But none of this sounds like it's our responsibility.

**[1:52:03] Jan:** Exactly, and the drills. is building a front end that is capable of handling them.

**[1:52:15] Rob:** Mhm.

**[1:52:16] Jan:** Mostly, and then of course, we on us is the drill evaluation.

**[1:52:22] Rob:** Right. So the main thing I think maybe is on us, maybe not, is that like an endpoint has to be hit to be like, oh, we're going to show the like the video, the educational content here. And then. It is shown.

**[1:52:43] Jan:** Yes, that, okay, yeah. I think that is the path and progress. Thing. That we said that looks at the... what the LM like this is talking to the LMS and says like, okay, now I need something new and then the LMS gives it to this. to the brain.

**[1:53:11] Rob:** Right.

**[1:53:12] Jan:** Wait, how do we do we have that here, learner pro with that one? Right, so that is.

**[1:53:18] Rob:** Yeah, and part of, yeah, and also part of static learner content is the presentation content.

**[1:53:27] Jan:** Yes.

**[1:53:29] Rob:** Okay.

**[1:53:30] Jan:** Okay, and when we build that, that should be able to. ... Select. what should happen next, presentation, drill, blah blah, or like through some user interaction and initiate like.

**[1:53:47] Rob:** Mmh.

**[1:53:54] Jan:** One of those. Cycles.

**[1:53:59] Rob:** Right.

**[1:54:01] Jan:** Then it's back and then progress has been updated and then it starts a new cycle. Okay, and now I think it's important that we... Add, add some of the stuff here.

**[1:54:18] Rob:** Mhm.

**[1:54:18] Jan:** Because it's missing, and... Herault. Okay, so we have... The conversational drill can get started. Do we need to is that anything? There's a free conversation. These 2 sound to me like... We somehow initialize that and then it goes into the conversation. Mode.

**[1:55:11] Rob:** Right.

**[1:55:13] Jan:** That is so the we own the triggering of this. of doing any of these and we added pronunciation wordbook to probably the drills. and something happens in the front end, or if it's a conversation, we go here.

**[1:55:34] Rob:** Right.

**[1:55:35] Jan:** I'm trying to think if we need to do anything on this side, really. Or what, what this is. And it feels to me in the end, it's the path and progress. Controlling.

**[1:55:53] Rob:** Yeah.

**[1:55:54] Jan:** And it just takes one of these. There's not much else going on.

**[1:56:00] Rob:** I think that's true.

**[1:56:00] Jan:** Yeah.

**[1:56:02] Michal:** Yeah.

**[1:56:04] Jan:** I mean, it looks like there's, the way that we have it shown now, looks like there's a lot of crap going on, but there really isn't.

**[1:56:04] Rob:** Again. I think that's true. ... And yeah.

**[1:56:25] Jan:** This is basically.

**[1:56:25] Rob:** And maybe in the app there's a learner place where all the playing the videos happens. And yeah, maybe they're separated out a little bit in the mobile app as they see it now, but I think I broadly agree.

**[1:56:43] Jan:** So, this would... Mm. The way they are, but I would probably... Make this something like... PowerPoint doesn't like it when you go off the slide.

**[1:57:56] Rob:** Oh no.

**[1:57:57] Jan:** Ah, man. OK, so... This picks one of these and then feeds it into the front end. Right, and this is really like this little thing here. Not a whole lot happening.

**[1:58:14] Rob:** Mhm.

**[1:58:19] Jan:** .. And... These are kind of...

**[1:58:40] Rob:** Mm.

**[1:58:41] Jan:** The options that we want to show in the front end. So, one, I mean, another way of looking at it, this is not in terms of what are the front-end.

**[1:58:47] Rob:** Right.

**[1:58:55] Jan:** Modalities, but what are we showing in the front end?

**[1:59:00] Rob:** Right.

**[1:59:01] Michal:** But one question, because here we have like the exercise, whatever, right? Our presentation, no, no, nothing, nothing. It's all good. Sorry for that.

**[1:59:16] Jan:** Could be like this. Right.

**[1:59:20] Rob:** Yeah.

**[1:59:22] Jan:** And this is really just to make sure that. We kind of know. What are the what are the modalities of the formats or? The data streams, whatever.

**[1:59:40] Rob:** Right.

**[1:59:55] Jan:** And this one needs a bit of reordering.

**[1:59:58] Michal:** Yeah.

**[2:00:04] Rob:** I think this, I think this is already much more clear.

**[2:00:23] Jan:** Okay. . Potel. I'm going to leave it on the side here, just might use it afterwards later for something. Okay, and this is what...

**[2:00:43] Rob:** Right, right. Well, yeah, because we need some way to talk about the avatars.

**[2:00:50] Jan:** Yeah. Yeah. Yeah. And practice would be like all of this.

**[2:01:25] Rob:** Oh. ... Done. I figured out what the issue was, why you couldn't see Learning Hub.

**[2:01:35] Jan:** CH.

**[2:01:37] Rob:** You, when you go to the my tutor, you have to log in with your Berlitz.

**[2:01:46] Jan:** Yeah.

**[2:01:47] Rob:** User, and then it, then you see everything.

**[2:01:51] Jan:** Okay. Oh, thank you.

**[2:01:56] Rob:** It needs its own username and password. They're not your like Microsoft 365 thing. It's like a distinct Othio thing, but. When you do that, it works.

**[2:02:08] Jan:** Mhm.

**[2:02:10] Rob:** Okay.

**[2:02:21] Jan:** Okay. Emma. Maybe this is better. That's hope.

**[2:02:35] Rob:** It's it feels it feels less redundant, if anything.

**[2:02:41] Jan:** Yeah. Okay. Come on, share the whiteboard.

**[2:02:53] Michal:** Mm.

**[2:02:55] Rob:** All right.

**[2:02:55] Jan:** Yeah. There.

**[2:03:00] Rob:** Okay.

**[2:03:06] Jan:** Okay, so here. We have this guy, then we have some front-end going on. And then we have the elevators and the user input. And if we build this and we build the conversation module. Do we have the level assessment in here? Yes, we do. Level assessment is also there. There's some data collection going on. This is, I don't know, this is... What do we do with this path here?

**[2:03:52] Michal:** I have one question related with that. Who going to have the ownership about the learner progress, right? Because we're going to evaluate some stuff, right? Like the evaluators, that for example, that your pronunciation is good or not or correct.

**[2:03:54] Jan:** Mhm.

**[2:04:12] Michal:** But after that, we're going to call or save this data in some learners, learner services, and after that, or is going to be our part or other team part that they're going to have the ownership. what I mean?

**[2:04:26] Rob:** .. This is, this was the thing that's annoying, right? Usually we say... People who own the service own the data underlying the service. But if we want to own the data for this feedback, because we want to do a lot of things with it. We were on the hook to own the service, or we have to sort of let the app team own the service, and then we only own this, we only own things that ingest the service. We only own the thing, we only own things that... Ingest the data from the service.

**[2:05:16] Michal:** Okay.

**[2:05:23] Rob:** So...

**[2:05:24] Michal:** That in this case, we don't going to develop the service, we're only going to own the data.

**[2:05:30] Rob:** Well... We have two things we can do. One thing we can do is we can just say, I don't know what this LMS is, but we kind of need it to already exist. So we're going to mock it up. And then hopefully eventually it gets built for us with the interfaces we like. And... At the end, we sort of... kind of go from there. The other option is we say mobile app kind of owns everything. And then we're just going to write services that ingest it, just like we ingest instructor guides, just like we ingest transcripts, just like we ingest forms, we're just going to ingest later.

**[2:06:09] Michal:** Sorry, someone touched my head.

**[2:06:21] Rob:** The feedback stuff and use that to make what we want to make.

**[2:06:28] Jan:** Mhm.

**[2:06:28] Rob:** Those are both valid ways of going. It's. I'm kind of happy with going with whichever. ... We should just pick whichever one we think will let us work faster.

**[2:06:43] Jan:** Mhm. Okay, so that means what we have here is another. Another one of these.

**[2:06:59] Rob:** Mhm.

**[2:07:02] Jan:** Which is... Data collection.

**[2:07:09] Rob:** Mhm.

**[2:07:10] Jan:** Lerner. Data collection.

**[2:07:14] Rob:** Yeah.

**[2:07:16] Jan:** Support data. Handling.

**[2:07:22] Rob:** Yeah.

**[2:07:27] Jan:** No, I think it's actually, it's like two things. One is specifically learner data. It's like this is the vocab, this is the grammar that the person is using these things.

**[2:07:42] Rob:** Mhm.

**[2:07:43] Jan:** The other is... More like... Actually, there's three. I think there's the learner data, there's the telemetry. Generic telemetry, like how is the app being used?

**[2:07:59] Michal:** Mhm.

**[2:08:01] Jan:** And then there is... The data that we want to learn to use for curriculum optimization.

**[2:08:11] Rob:** Right. Yeah, they are different data.

**[2:08:12] Jan:** Wicks. Yeah, they're not entirely MEC.

**[2:08:20] Rob:** Right.

**[2:08:21] Jan:** There's some overlap going on.

**[2:08:23] Michal:** Mhm.

**[2:08:24] Rob:** Yeah.

**[2:08:26] Jan:** But I think there's for sure there's the learner. Learner data.

**[2:08:30] Michal:** Because.

**[2:08:33] Jan:** Which is progress vocab on that.

**[2:08:39] Rob:** Mhm.

**[2:08:41] Jan:** Emma. Mission. And then there is the... Should I call it telemetry?

**[2:08:58] Rob:** Right, so telemetry, some notion of telemetry, like already people are doing. So I think like Sean and Rafael are already doing something called telemetry.

**[2:09:11] Jan:** Yes. I was also, yeah, thinking that. Also, Knud has some ideas on what the learner data should be.

**[2:09:22] Rob:** Yes. And I was asked to, this morning, make a document in the knowledge base of what I think it could be shaped like so people can start looking at it and making decisions around that.

**[2:09:38] Jan:** Right, and that's we do that for the dog food or for the MVP already, right?

**[2:09:44] Rob:** Right.

**[2:09:51] Jan:** And by high fidelity, I mean... Yeah, high fidelity, right? No, not. We're not aggregating or processing the processing the data. We want the rawest and the most that we can get.

**[2:09:58] Rob:** Yeah. Right.

**[2:10:13] Jan:** And the telemetry, should I add? Content factory to do that or is that?

**[2:10:26] Rob:** I don't know what is what we mean by telemetry.

**[2:10:32] Michal:** Telemetry is like the what lessons he take, how many time or how many time on the week like the two times per week that he doing the lessons or what is?

**[2:10:47] Jan:** That I would all see in, but I mean, you, yeah, you're saying some things here, like frequency of news. What was the other one?

**[2:10:50] Michal:** Yeah.

**[2:11:00] Jan:** On.

**[2:11:00] Michal:** The classes that he takes or she takes, or no, that is the progress, right? That, that progress.

**[2:11:08] Jan:** Yeah, but no. It's yeah, it's implicit in the progress.

**[2:11:13] Michal:** But telemetry is like that if app is working correctly or is crashed or...

**[2:11:19] Jan:** Yeah.

**[2:11:23] Michal:** If user is happy with the lessons, or...

**[2:11:34] Jan:** I would, yeah, I would say this is... Okay. How often, where do users click?

**[2:11:45] Michal:** If our services is working correctly or something like that, I don't know.

**[2:11:45] Rob:** Ohh.

**[2:11:52] Jan:** Well, to a certain extent, that too. User feedback.

**[2:12:08] Rob:** Yeah, I mean. The telemetry is typically yes stuff. It's. It's 2 things. It's how the users are interacting with it, how long are they spending on the lesson, how long are they spending on the app, what, what, how are they moving around the app? Like, do they go from learn to practice or go practice to tutor? Like, how are they transitioning between them?

**[2:12:35] Jan:** Right.

**[2:12:37] Rob:** But it also includes like more like aggregate. Well, okay, it also includes just. performance of like how well the app is working, how well all our end services are working. So some of this I think kind of is on us. Like we do need telemetry for like all of our evaluators, for example. That's for sure. like what's the latency on our grammar, drill, pronunciation evaluators? What's our uptime on them and things like that? Like we kind of need some of that. That's also part of telemetry. That stuff I think probably is on us. Maybe some of that we can like pawn off on the infrastructure team, but some of it probably is on us.

**[2:13:27] Jan:** Yeah.

**[2:13:28] Michal:** Yeah.

**[2:13:30] Rob:** ..

**[2:13:30] Michal:** But the same from the learner data, right? That some maybe depend of us, but...

**[2:13:37] Rob:** Yeah.

**[2:13:38] Michal:** A lot of data like the data or maybe some progress or whatever that we can send only the our recap and some other team going to create the services and save the data and give us some main point to get this data back if we need to.

**[2:13:48] Rob:** Yeah, yeah.

**[2:13:58] Michal:** To use it on the curriculum site or whatever.

**[2:14:02] Rob:** Mhm.

**[2:14:10] Jan:** Okay, so this week, I think the data... governance or whatever needs to be discussed. With them.

**[2:14:20] Rob:** Yeah.

**[2:14:23] Jan:** .. I'm kind of ignoring everything down here.

**[2:14:34] Rob:** I, I think I, I, I, I'm in favor of this action. , there is... There is like one bit that kind of. Well, I don't know. I think you can get away with ignoring these actions.

**[2:14:58] Jan:** Well, I mean, this is like the picture in the end will need to have it in there, right? But this is like, a little bit about it. I know next to nothing. I know what, like, all in all, that what should be there, but...

**[2:15:04] Rob:** Yes. Well, so like for example, for like scheduling, like part of Tutor is that the humans will be scheduled, like teachers will be scheduled from the app. I think that is one of the features they want to have.

**[2:15:17] Jan:** Then.

**[2:15:27] Rob:** And like you may want to be able to book an in-person class from the app. So, and as part of that, well, let me explain how it connects to our stuff.

**[2:15:32] Jan:** Right, right.

**[2:15:32] Michal:** Yeah.

**[2:15:36] Jan:** Yeah.

**[2:15:41] Rob:** As part of doing that scheduling, maybe you want to send the teacher information about the learner. That we've collected.

**[2:15:57] Jan:** Yes.

**[2:16:00] Rob:** .. My hope is that feedback from the in-person classes back to us can be handled by Curriculum Factory.

**[2:16:14] Jan:** Yes.

**[2:16:18] Rob:** But I don't know if that's true. Because if a teacher, if a student has a live class and the teacher has feedback about the student. ... I don't know where that needs to go. My hope is somewhere here that happens, but I don't know if that's the case.

**[2:16:41] Jan:** But that's also because you have the user data, where is that being stored? This is big constant.

**[2:16:55] Rob:** Well, my hope is that... We have recordings from the teacher or we have the teacher wrote something down and that's here and then it makes its way that way. That's my hope.

**[2:17:06] Jan:** Mhm. Okay. Guys, I have to run.

**[2:17:12] Rob:** Alright.

**[2:17:13] Michal:** Alright.

**[2:17:14] Jan:** Should we reconvene in an hour?

**[2:17:18] Rob:** ..

**[2:17:20] Jan:** Or...

**[2:17:21] Rob:** I, I, I don't, I don't know just yet.

**[2:17:26] Jan:** I think we're almost there, so that's I think it's the cool thing will be to make sure that we have all the.

**[2:17:27] Rob:** I would like. Yeah.

**[2:17:35] Jan:** All the post-its that we need.

**[2:17:37] Rob:** Yeah, I do agree we are almost there.

**[2:17:38] Jan:** And then... Yeah, and then we need to find an order. that we want to attack these.

**[2:17:46] Rob:** Yes.

**[2:17:48] Michal:** Okay, that may be 3 P.m. or something like that or 2 and 5.

**[2:17:54] Jan:** Just let me check my calendar. I have, I can. I'm back at... Two 30.

**[2:18:03] Rob:** Okay.

**[2:18:03] Jan:** We can do three if that's better for you.

**[2:18:07] Rob:** I'd slightly prefer 3, because like if we meet at 2.30, it goes till like 3.30. I have a meeting at 4, like nothing happened. That half hour between is like, I'd much rather like...

**[2:18:19] Jan:** Okay. Sure, that's all three.

**[2:18:23] Rob:** But yeah.

**[2:18:24] Michal:** At 3pm? Okay.

**[2:18:25] Rob:** Okay, cool.

**[2:18:26] Jan:** Mhm. Cruz.

**[2:18:28] Rob:** Sounds good.

**[2:18:30] Michal:** Perfect, then.

**[2:18:31] Rob:** Earth.

**[2:18:32] Jan:** Great, cool.

**[2:18:33] Michal:** See you later, and enjoy your meal.

**[2:18:34] Rob:** Right.

**[2:18:34] Jan:** Call.

**[2:18:37] Rob:** Thank you. Bye.

**[2:18:39] Jan:** So...

**[2:18:40] Rob:** CH.

**[2:18:49] Jan:** I have some, so I have help now.

---