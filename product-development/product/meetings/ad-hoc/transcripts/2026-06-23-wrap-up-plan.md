# Wrap up Plan

**Date:** 2026-06-23
**Start:** 2026-06-23T13:00:00.000Z
**End:** 2026-06-23T14:00:00.000Z

---

**[0:04] Jan:** Thank you.

**[0:04] Michal:** No.

**[0:05] Rob:** Alright, did you get my email?

**[0:05] Jan:** Awesome, yeah, Greg. Did I get your email? I did not check my email, so I probably got an email from you. Yes.

**[0:13] Rob:** Ahh.

**[0:14] Michal:** And. I don't have any, I think so.

**[0:21] Jan:** I got your email now.

**[0:21] Rob:** S. Okay, alright.

**[0:25] Jan:** Rob was going to be late.

**[0:30] Rob:** Alright.

**[0:31] Jan:** Yeah, I, I don't read email for, like, don't expect me to email every quite so often.

**[0:36] Rob:** All right. Oh, okay, alright. We need to figure out some sort of out-of-band communication thing.

**[0:41] Jan:** I think you may love that. What's that?

**[0:46] Rob:** Because we need to figure out some out of band communication thing because I don't keep Teams on my personal phone.

**[0:54] Jan:** Okay. Why not?

**[0:58] Rob:** .. Okay. Resist the temptation of working out of hours.

**[1:08] Jan:** But that's in your head. You should be stronger than having to resort to this.

**[1:12] Rob:** Yeah.

**[1:16] Jan:** No, but I know what you mean, and I need to find a way to have the notifications off in the right times, because usually I get a lot of notifications to at weird times.

**[1:30] Rob:** Well, global workforce, so like...

**[1:32] Jan:** Exactly, exactly. Okay, now what I was going to say is the current portal was experiencing problems with the Azure Speech Recognition and some people looked into it and it turns out that we have a maximum concurrent user thing in the contract.

**[1:36] Rob:** Okay. Oh.

**[1:53] Jan:** And that was exceeded.

**[1:53] Rob:** Oh.

**[1:56] Jan:** And instead of costing us additional money, it just doesn't work. And...

**[2:02] Rob:** Oh.

**[2:03] Jan:** And I think there was apparently a watchdog in place, but... I don't know, maybe it checked whether the service was available and the service was available, just returning nothing.

**[2:17] Rob:** Okay.

**[2:18] Jan:** .. And Javier explained to me the background. There seems to be like some large number of students enrolled in our system in Southern America. And as students, as they are

**[2:33] Rob:** Mhm. Mhm.

**[2:40] Jan:** Students, they're lazy a long time, and then deadline approaches, and then all of a sudden, all of them are on the platform, and...

**[2:49] Rob:** That's fun.

**[2:51] Jan:** Okay.

**[2:51] Rob:** But also that's maybe that could be good for like provisioning, right?

**[2:56] Jan:** Yeah. Yeah, OK, so just saying that stuff that we have to keep in the back of our minds when we when we make that, that we...

**[3:07] Rob:** Mhm.

**[3:10] Jan:** Have tests in place for that, watchdogs and that sort of stuff.

**[3:11] Michal:** But...

**[3:16] Jan:** The other thing that happened to them was that Microsoft changed the Azure speech recognition somehow, like new model or whatnot, but didn't say it. They didn't communicate the changes to customers.

**[3:35] Rob:** Mhm.

**[3:36] Jan:** So they ended up having problems in certain regions. Out of the blue. And I think that's something that we should also consider that we have. ... Oh, benchmarking of the services.

**[3:57] Rob:** Right.

**[3:58] Jan:** Ongoing.

**[3:59] Rob:** I mean, this is part of country, right? Like... But we. We track not just, well, I mean, how much this is on us, I don't know, but... ... It's hold on. Like... Some of this is on us, some of this is probably on infrastructure team to be like, hey, like, can we like have monitoring? These are all the external services we depend on. Can we have like monitoring for when they're down as well?

**[4:30] Jan:** Mhm. Exactly, so there's like this watchdog aspect, and then there is, I think, we should have something that runs, I don't know, once a week that checks the quality and latency and...

**[4:47] Rob:** Yeah.

**[4:49] Jan:** On a on a fixed data set. You have your data set, that doesn't change, and you give it to the different services. This is a couple that you get, and you track that over time.

**[4:55] Rob:** Yeah. Right.

**[5:00] Jan:** Hopefully not too much changes. But that could also help in the case, for example, if we do detect that a service is out, we could switch to another service at runtime.

**[5:12] Rob:** Exactly.

**[5:16] Jan:** I think.

**[5:16] Rob:** Right.

**[5:18] Jan:** Actually... I think we, I think so. I think they did something similar where they, where they had problems accessing. Ohh. the OpenAI stuff in the US, because that was sometimes terribly slow. So they had some live selection ongoing where they would find the server that was the most responsive at the time.

**[5:50] Rob:** Mhm.

**[5:50] Jan:** By any given time, basically, so that would run that, I don't know, maybe once an hour or four, or even more fine-grained, so, and then select what server to send the request to.

**[5:56] Rob:** Okay.

**[5:56] Michal:** Okay.

**[6:04] Jan:** It's kind of neat. Yeah. Okay. Whiteboard. Ohh. The default action is to not collaborate on this. Thank you, Microsoft.

**[6:27] Rob:** Bing. Well, I think they're thinking about a situation where you're presenting to like 50 people.

**[6:41] Jan:** Yeah, but is that the default? Like, whiteboard is something where people stand in front and work with it.

**[6:45] Rob:** Okay. Yeah, everyone has a marker, yeah.

**[6:53] Jan:** Right, I mean, that's.

**[6:59] Rob:** Okay.

**[7:02] Jan:** All right. ... I need a minute. I'll be right back. You guys can get started.

**[7:09] Rob:** Okay. What are we getting started with?

**[7:14] Michal:** Yeah.

**[7:14] Jan:** Very good. OK.

**[7:19] Rob:** All right. OK, let's see here.

**[7:36] Michal:** All the data, and you have the learning data user learner learning data is like the. Seems like very similar, right?

**[7:48] Rob:** Yeah. Yeah, I think this part probably still needs to be cleaned up a little bit.

**[7:56] Michal:** Yeah.

**[7:57] Rob:** In the sense of like, there's a loop here, I actually think there's probably a virtuous loop here, which is that we're collecting previous instruction, we're collecting previous instruction resources and teaching things, and then... In some sense. Things that happen here kind of feedback into it. So there probably is also another loop here happening.

**[8:22] Michal:** Yeah. Like the you said progression right that is related with the conversation stuff that we prepare like some personalization class or lesson for the user right?

**[8:36] Rob:** Right. I mean, sometimes you can see the loop, like this is the loop, right? Like this is the, we put, we evaluate, we sort of evaluate the users and loosely the teachers. That data is kind of goes, finds its way ultimately into the content factory, which is used to sort of adjust the lessons.

**[8:40] Michal:** Yeah, yeah, yeah. Huh?

**[8:58] Rob:** And so on and so forth. I think if anything, there probably needs to be sort of like... I think there needs to be a square somewhere here about like the information we know about the learner in terms of like what they're good at, what they're bad at, what their interests are. Because it's not quite content factory stuff, but it is sort of information that's used to create the lesson.

**[9:36] Michal:** Yeah. But in this case now, if I'm not wrong, that is the same place, let LMS have this information or...

**[9:44] Rob:** Yeah, yeah, yeah, it all is gonna like it all goes to the LMS.

**[9:49] Michal:** And we want to have all of this information still in LMS in new version. What I mean that the static content and like the progression, the user progression or the learner progression, we want to have inside the LMS or we want to have like the... learner services with this data and after that on demand. With the curriculum factory, create the lessons, they they are tailored to the user. what I mean?

**[10:27] Rob:** So there's actually an ADR on this. ADR 0007, which suggests that there should be for auxiliary information that doesn't fit into the LMS, there should just be a service that. that less information can query in addition to the LMS.

**[10:55] Michal:** Okay.

**[11:02] Rob:** Ohh.

**[11:02] Michal:** Is one that you do, do you wait for the approvals, right?

**[11:08] Rob:** Well, Dude did approve it. Well, Daniel approved it, so. And Daniel, being like one of the lead devs on the mobile app team, suggested sort of like, okay with that.

**[11:12] Michal:** No, OK. Okay.

**[11:21] Rob:** But. All right. What do you think about what has just been said, Jan?

**[11:34] Jan:** Didn't catch all of it, but I... I think... The way that I see, think about content factory right now is that let's first. Try to get some content. some handcrafted content and play around a little bit with Claudio what we can do to automate this process. Once we have that and...

**[11:57] Rob:** Mhm. Yeah.

**[12:06] Jan:** Then I think, yeah, just like putting out, in my eyes, it's not worth putting it on the critical path.

**[12:14] Rob:** Okay.

**[12:14] Jan:** For the mobile app.

**[12:16] Rob:** Okay, so for now, in terms of data learner data, we're just going to store it. We're not going to think about ways to use it, at least for MVP.

**[12:31] Jan:** Yes. I, I would assume we have other stuff.

**[12:36] Michal:** OK.

**[12:37] Jan:** More important, more pressing, more urgent, and more important to get the mobile app running. When we're done with all of them and mobile team doesn't have the app running yet, that's fine. Right then, of course, we can start working on the content factory.

**[12:44] Michal:** Okay.

**[12:44] Rob:** Mhm.

**[12:56] Jan:** When Ali starts, maybe he's... Eager to work on it, right? And we have a new work stream starting.

**[13:04] Rob:** Okay. Yeah, I will join July 1st, to my knowledge, or is it later?

**[13:16] Jan:** No, that's what I know.

**[13:21] Rob:** He that he's joining later.

**[13:21] Jan:** Like. No, no, no, that he's like, what do you think is true?

**[13:26] Rob:** Okay.

**[13:27] Jan:** What I heard.

**[13:28] Rob:** Alright, so... OK, you kind of alright, OK, cool.

**[13:38] Jan:** .. It seems like we have everything that we need.

**[13:59] Michal:** I hope.

**[13:59] Jan:** You agree?

**[14:01] Rob:** I am kind of inclined to agree. For where we don't have it, we have a spike that I think will reveal, that will immediately feed into a thing we need to do.

**[14:18] Jan:** Oops. And there's. Two tiny things that I would like to change though. Mhm. Okay, here we have the audio. That is something that... for me is part of the front end. And what I mean by audio is an audio design is. that we currently, I don't believe we have anything like background noise for the questions.

**[15:06] Rob:** Yeah, for things like the avatars.

**[15:10] Jan:** Well, for anything, really.

**[15:11] Rob:** Oh, so...

**[15:12] Jan:** Also, for the avatars, but I would like...

**[15:14] Rob:** Even for pure audio, like if someone says they're in a coffee shop, it would be nice if it felt like it was actually in the coffee shop or...

**[15:22] Jan:** Exactly, you have a little bit of the clatter of of.

**[15:24] Rob:** Yeah.

**[15:29] Jan:** Of what of the classes and stuff, right, and like chatting and all that.

**[15:29] Michal:** And then...

**[15:33] Rob:** Sure, yeah, yeah. Yeah, you can hear there are people in the background, people walking around. Yeah.

**[15:39] Jan:** Right. And then, I mean, I think that's also where Duolingo is really good at. They have the whole, like they have recognizable sound effects.

**[15:50] Rob:** Right. Yeah, I think some of that is on us. So like in terms of like... Making the audio sound good and mixing it, something I think might be on us. Sound effects in the app I think are very much not on us.

**[16:06] Jan:** Yes. Right, yeah, yeah, and I assume that currently we do not have anything like that.

**[16:16] Rob:** I think that is a good, I think that is a correct assumption.

**[16:18] Jan:** Yeah. Okay, but I put it here. This needs, this is a bit ugly over here, needs some.

**[16:23] Michal:** No.

**[16:32] Jan:** Moving around the level assessment, I think we have that as a as something that we want to work on. ... Probably would have to live somewhere near the evaluators.

**[16:45] Rob:** Yeah.

**[16:49] Jan:** Okay. No space.

**[16:54] Rob:** If you wanted to, you could treat it as... part of the evaluators. Like... If you move, if you sort of move lesson loop up, because you now have, like, you have room now here. ... You could probably make your values a little longer and stick level assessment in there.

**[17:22] Jan:** .. I don't want to do that because to me it's... A little bit like a conversation or one of these.

**[17:36] Rob:** Okay, well, okay. The mobile app box is big, so we can move things around in the box. Okay.

**[17:37] Jan:** And if, if I could put it. Yeah. Okay, so first of all... Moving this up is probably a good idea. What's that? ... Now, my beautiful... Circular thing doesn't work anymore.

**[18:04] Rob:** Yeah, yeah, you got it. Yeah.

**[18:06] Jan:** Oh. And that assessment is... Oh, it's probably something that... But it, it is a little bit like... conversation doesn't necessarily need, I don't know if it needs real-time assessment.

**[18:26] Rob:** I explicitly in the previous meeting said that I don't think it makes sense to be having in real time.

**[18:33] Jan:** Ohh. OK, so.

**[18:35] Rob:** But then my impression was that... Level assessment makes sense as the lessons being created. Not. when you're in the lesson already. Like for me level assessment almost is like between content factory and LMS. Or lesson loop, yeah, or lesson loop. Either or.

**[19:06] Jan:** I think that's a, this is one type of. One use case. SS.

**[19:17] Rob:** I know you're sensitive to it, like... being low assessment because like the in the Tokio demo, it's very clear that they're not using level appropriate language, but I think that's a prompting issue. More that's more so a prompting issue than anything else.

**[19:41] Jan:** Yes, okay, but just to be 100% sure that we're on the same page. For me, level assessment is you, first time user, signs up.

**[19:47] Rob:** Okay.

**[19:55] Jan:** And we want to do something with that person. And we want to show some content. And we need to show, we need to be, for the best experience, we need to be really spot on.

**[19:59] Rob:** Mhm.

**[20:09] Jan:** Right, as soon as we use language that is...

**[20:16] Rob:** Okay.

**[20:17] Jan:** Will hate it and be feel overwhelmed. If we bore them to death, I think we can get away with a little bit of boredom more than the other end of the spectrum.

**[20:26] Rob:** Right. Sure.

**[20:31] Jan:** So, for me, this level assessment is... is, I mean, it gives you the starting point in the path.

**[20:41] Rob:** Okay, I understood level assessment differently.

**[20:41] Michal:** But.

**[20:45] Jan:** That's what I thought.

**[20:46] Rob:** I understood level assessment as... We know roughly what level the user is at because they took a placement test or they've already taken a few lessons. We're about to show them some content and we're going to do a quick check. Is this content level appropriate to show them?

**[20:57] Jan:** Yeah. Yeah. ... Right. That's why I think we need the... The appropriate the level appropriateness test. That would probably come up in more than one application here.

**[21:27] Rob:** Right.

**[21:28] Jan:** So it's definitely something that somewhere in the content creation at some point that check has to be made.

**[21:36] Rob:** Right.

**[21:38] Jan:** Because we don't trust it. And we know that system is better than at critiquing itself than necessarily following the rules. But I was under the impression that we might also need it elsewhere.

**[21:48] Rob:** Right.

**[21:55] Jan:** I mean, for the conversation, for example, definitely. We want to make sure that we, or maybe for the live session with teachers. where you want to make sure that you have that level of appropriateness checked.

**[22:16] Rob:** Right. End. I agree, it's useful there. I worry about latency there.

**[22:33] Jan:** Mhm.

**[22:34] Rob:** But like it's okay, like it's okay to put it there and then like we can always like iterate and remove later if we realize this is a problem.

**[22:47] Jan:** Okay, you're talking level assessment.

**[22:49] Rob:** Yeah, because you were talking about in the within the conversation doing level assessment as the conversation and that I feel like that might be a little overkill.

**[23:01] Jan:** Ohh, okay, yeah.

**[23:04] Rob:** Or, or, okay.

**[23:06] Jan:** Yeah.

**[23:07] Rob:** Or, calls has latency issues.

**[23:22] Michal:** That, if I must have understood all that. Will be exist new OPT part to get the user self level or Berlitz level that would think that he or she has. And after that, we're going to have like this level assessments, like you mentioned, Rob, that... to prepare the class or lessons or whatever we're going to do with level assessment, right? Or check if...

**[23:57] Rob:** Right. So... Yeah. I think this level assessment thing can go and it's useful for it's useful in multiple places. ...

**[24:12] Jan:** Mhm.

**[24:14] Rob:** And so. But certainly... So like at minimum, definitely useful as part of. content factory just to criticize the lessons created, but also...

**[24:30] Michal:** Mm.

**[24:32] Rob:** Yeah, I could see it as like... Hey, I'm about to like give a lesson like... Is this ...

**[24:39] Michal:** Because. Because I understand that we're going to have something when for the user for onboarding for the app, right, that to help him or her. to choose the right level of the language, right? That what level you have if of course is not like the first time that you going to get the class of the case language that I understand that we're going to have some onboarding on the app to help to the user to choose the right level, right?

**[25:08] Rob:** Yeah.

**[25:10] Jan:** Yeah.

**[25:16] Rob:** I, I mean...

**[25:16] Jan:** We didn't choose the level; we choose the level.

**[25:19] Michal:** Yeah.

**[25:20] Rob:** Right, we choose the level and making the user's first thing a placement test, which is a very normal thing to happen in language learning, I think is sort of the way we kind of go about this. We conduct a placement test and then we use, and then that information can be fed to level assessment.

**[25:21] Jan:** Obviously.

**[25:42] Rob:** To evaluate. Now again, that's slightly different, like there's evaluating the learner and evaluating the content and they kind of, they're slightly different and maybe those are both should be called level assessment and maybe they should be called different things. I'm not. I'm kind of okay one way or another. I'm not too... Picky, , but yeah, my impression was that Jan was mostly concerned about that we ... Assess that we have a good assessment of the user.

**[26:21] Jan:** Exactly, that was my main, my main idea here. Is. Yeah, this is. to the path in the progress that is going to be where you... Yeah, where you want to make it enjoyable. and challenging and not too easy, not too difficult.

**[26:48] Rob:** Yeah.

**[26:54] Jan:** Okay. No. Okay.

**[27:03] Michal:** And do you always mention the Duolingo app, right? Like, I think so that is like our reference, what we want to have, right? Or something like that.

**[27:14] Jan:** Maybe.

**[27:14] Michal:** More or less, more or less, right?

**[27:16] Rob:** I think it's more of a reference point for other people than me, but yes.

**[27:21] Michal:** But I don't know if you see it, the Busu app that I put on there, because Duolingo for me was always like the very boring and not like never enjoying the stuff, but for example, with Busu is like the more interactive, more video, more different accents that you hear from video and more...

**[27:25] Rob:** Yeah. Yeah. Yeah.

**[27:44] Michal:** Like this, like you mentioned, like do you have something with that with the coffee shop and use you hear some sound of the coffee shop right on the background that I think so that they have something similar like the AI tutorials or roles that maybe it's...

**[27:53] Jan:** Mhm.

**[28:03] Michal:** Good to check how they work and how is they implemented some stuff, right? Maybe we can investigate something or... Get some ideas or maybe whatever that we can. Get from them.

**[28:19] Rob:** Yeah, this, I am going to, I think I'm gonna try out this app and try to like it. Yep, yep.

**[28:28] Michal:** Yeah, if you... If you new user, you have, you can they give you to try to, I don't know how many one plus or two, whatever, right? At least.

**[28:41] Rob:** Yeah, okay. I'm going to download now. I'm obviously not going to try it now, but yes.

**[28:48] Michal:** I. And they have some similar application that I think so that we want to create.

**[29:03] Rob:** Yeah.

**[29:06] Jan:** You mean that it's a good blueprint for us?

**[29:10] Rob:** Better, maybe better than Duolingo, which ...

**[29:12] Jan:** Yeah. Rob, I remember seeing a lot of different avatar characters.

**[29:22] Rob:** Mhm.

**[29:23] Jan:** And... Distinctly, this Indian woman.

**[29:29] Rob:** Mhm.

**[29:30] Jan:** You remember that?

**[29:32] Rob:** I remember there was an Indian woman, yes.

**[29:37] Jan:** Is that is that something that we as Berlitz currently offer? Or is that was that something that you showed me on Tokyo?

**[29:49] Rob:** .. I believe I showed you based on what the live avatar offers. There's a set of ones that we offer, but it's only a subset. Like I think there's like, there's like 50 avatars. I think we offer like 10. The main unique Berlitz offering is that.

**[30:23] Jan:** Mmh.

**[30:24] Rob:** And we had to transfer all of them manually and mechanically to Live Avatar. And those, I think, are much more unique to Berlitz than anything. Whether you call that Tokyo or not, I don't know, because Tokyo also managed the 11 Lab stuff. But if we're talking about separate from the avatars.

**[30:41] Jan:** Right.

**[30:46] Rob:** There are also voices, and I think there is, there may even be more than one Indian voice. I don't know if there's more than one Indian woman voice.

**[31:01] Jan:** Okay. But can we? Can we change that around or how do we?

**[31:12] Rob:** Change, what do you mean change it around? Like add more voices, change the voices, what do you mean?

**[31:15] Jan:** .. The currently, do we have a selection for the avatar or is this always? The. I think I saw one guy and, well, actually, I think something like 3 different avatars so far.

**[31:37] Rob:** So if you go to Learning Path...

**[31:41] Jan:** Yeah.

**[31:41] Rob:** And go to like, and go to open conversation, like if you, I think it's in practice. You like practice tutor or something. you'll see a selection of people you can practice talking to. And it kind of describes where they're from and all these other things. I felt the accents leave a lot to be desired. But, they are what they are.

**[32:17] Jan:** Where did you see that in the practice hub or?

**[32:20] Rob:** Not in Practice Hub. Like if you're in learning, if you are in the learning path.

**[32:22] Jan:** So, I'm... Mhm.

**[32:27] Rob:** So, let me... So if you are in learning path and you, okay, let me click to see if I can find it. Okay, if you click, yeah, sorry, I apologize. Yeah, if you're in learning path, you click practice hub and then there's my Berlitz conversation partner. You'll see a list of people.

**[32:56] Jan:** Ah, okay, this is, yeah, this is exactly what I... Remembered looking at, and where is... Divya. Is.

**[33:08] Rob:** Upper right.

**[33:09] Jan:** Oh. Yeah, no, I didn't remember her name. I read the name and I found it. And Jeff is the freaky old guy.

**[33:15] Rob:** Yeah. Yes.

**[33:27] Jan:** Okay. Hey.

**[33:35] Rob:** I don't believe we have any custom.

**[33:36] Jan:** Yeah.

**[33:40] Rob:** Avatars, though we have custom voices. If we want a custom avatar, I think we have to pay a certain fixed amount per month, which is for them to host it.

**[33:52] Jan:** Mhm.

**[33:54] Rob:** But it is the thing they offer. You basically send them a two-minute video of the person you want cloned, and then...

**[33:56] Jan:** I think.

**[34:03] Rob:** As long as that person doesn't do anything. Two terms of Service violation, it will be approved.

**[34:10] Jan:** Yeah. Okay. ... Now, we have... We haven't spoken about the avatar at all. I mean, down here in terms of...

**[34:26] Rob:** Right.

**[34:31] Jan:** So, MVP. Yes.

**[34:38] Rob:** I would like, I would like in the MVP to be a way to talk to Avatar, either basically an open-ended conversation and the... scenario-based one.

**[34:57] Jan:** What else is there? The drills.

**[35:00] Rob:** Right. I mean, we could do, yeah, there is the drill, right?

**[35:05] Jan:** Yeah. I mean. If we have conversational drills. Working. Isn't it, does it automatically work for like, if we get the avatar working, then the whole thing works? Yeah, if you have conversation with them.

**[35:30] Rob:** I, I, I'm going to, I'm going to say, I'm okay, I'll phrase it this way: I think getting that working is probably 80% of the work, and then there's the other 80% which is getting the avatar hooked up, but I think, relatively speaking, the core of it is that.

**[35:46] Jan:** Yeah. Mhm. Okay, so if we put... If you put here... That the in the MVP we can have the avatar for everything that is. ...

**[36:37] Rob:** Conversation.

**[36:37] Jan:** A conversation. Yeah.

**[36:41] Rob:** I don't think it makes sense for a drill.

**[36:48] Jan:** Well, I'm kind of hoping... I would like to be able to blur the lines between drill and conversation. And if you blur them. hard enough, at some point the whole thing becomes one big conversation.

**[37:15] Rob:** I think, okay, in fairness, I think that is kind of a fun idea. , especially because I think conversations is much more in the like... Berlitz, I mean, is it? I don't know. I asked Martin a few days. I asked Martin yesterday, like, what does he think the Berlitz method is?

**[37:36] Jan:** Mhm.

**[37:38] Rob:** And yeah, what he what he had said to me was... At the lower levels, it's presentation practice performance, and then at the higher levels, it's task-supported learning.

**[37:53] Jan:** Task-supported learning.

**[37:55] Rob:** Things like the scenarios. There's a task, there's a concrete task that you need to do and you use language to you sort of communicate to do it.

**[37:58] Jan:** Mm. Okay. Okay. Oh. Cool. Okay. Now. We have all these.

**[38:17] Rob:** Okay.

**[38:18] Jan:** .. We could... We could ask Claudio to group them. Make epics out of them, and... Ohh. Create tickets for that.

**[38:42] Rob:** Okay.

**[38:47] Jan:** Or we do all of that manually and merge it in with what we already have.

**[38:57] Rob:** I slightly prefer. We do the manual process because I'm afraid Claudio is going to like take all of them and add them. And we're going to have like all this like duplicate stuff.

**[39:11] Jan:** Mhm.

**[39:11] Rob:** But maybe that's okay.

**[39:14] Michal:** And I understand that if exists some issue that we can update with new details or something like that, this issue.

**[39:20] Rob:** Right, right.

**[39:23] Jan:** But I mean, yeah, the okay, and just moving forward, the way that I see it is we have this. We have the PRDs. We haven't reviewed them in detail. Maybe we find the time in the next weeks, maybe we don't.

**[39:45] Rob:** Well, this I feel at least unblocks me and Michal and possibly Ali.

**[39:52] Jan:** Yeah. I hope so. And then, I mean, what we should do, we should have like a definition of ready or something like that going between us. We should, at the very least, we should say, okay, pronunciation, evaluate, no.

**[40:07] Rob:** Yeah.

**[40:15] Jan:** Evaluated with the evaluator should, but what does that mean? Right, what's the ACs for that?

**[40:24] Rob:** Yeah.

**[40:27] Jan:** And I'm being told that the right issue skill or. Command is quite nice and powerful.

**[40:38] Rob:** Yes.

**[40:40] Jan:** ..

**[40:41] Rob:** It's quite good, so you could.

**[40:43] Jan:** Yeah.

**[40:46] Rob:** So okay, before we get to that, I want to actually bring up a more concrete question. We already have a bunch of things called epics already in the issue tracker. What do you want to happen to them? Do you want them archived? Do you want them removed? Do you want them cleared?

**[40:53] Jan:** Mhm. Yes. I don't know, actually. Because I don't remember what they... I mean, if they, if, if this...

**[41:14] Rob:** They loosely correspond to the PRD areas.

**[41:19] Jan:** Right, I mean.

**[41:19] Rob:** There are that granularity.

**[41:22] Jan:** We could group stuff a little bit like that.

**[41:24] Rob:** Right.

**[41:27] Jan:** Or we could. ... The way that I see this is... All the evaluators should be part of the evaluator. ...

**[41:45] Rob:** Epic.

**[41:46] Jan:** Epic and the drill, right? That doesn't mean that this is, we're going to do all of them at the same time or in sequence, but without anything else. We could probably select like the drill evaluator as the easiest one.

**[41:48] Rob:** Right. Right. Okay.

**[42:05] Jan:** And... Start with that.

**[42:08] Rob:** Right. What if we made a, yeah, yeah, what if we made a like a label just for the evaluators and then?

**[42:10] Jan:** Like. It.

**[42:22] Rob:** ..

**[42:24] Jan:** You want to get rid of my pics?

**[42:24] Rob:** We then make it. Mmh.

**[42:28] Jan:** Do you want to get rid of the epics?

**[42:31] Rob:** I'm trying to understand, ... I'm trying to understand what we want to live at the epic level, because with some of the issues now, like there's a lot of stuff living on the epic level. So I kind of want to like, because my understanding with the epics, and I had an argument with Bogdan about this, is that, epics is for.

**[42:51] Jan:** Yeah.

**[42:55] Rob:** Grouping features.

**[42:59] Jan:** Mhm.

**[43:01] Rob:** And so they're kind of there to like for all the features to be in place and then, feature something that's too big for a task and a task is something that's big enough that you can call the right issue command on it.

**[43:16] Jan:** Mhm.

**[43:18] Rob:** Where task being, we can reasonably expect Claudio to. Write a good issue for it with input outputs and. perhaps even write code to like address the issue, to fix the issue.

**[43:39] Michal:** Like, for example, could be epic like the evaluators and task could be like the grammar evaluator, the evaluator, or whatever. And after that, we have the issue and sub issue for each of them task, right?

**[43:47] Rob:** Right. Yeah.

**[43:56] Jan:** I mean... Theis.

**[44:05] Rob:** ..

**[44:12] Jan:** This could be one epic.

**[44:14] Rob:** Okay.

**[44:14] Michal:** Hritz.

**[44:18] Jan:** And...

**[44:19] Michal:** **** **.

**[44:21] Jan:** Okay, do we have, like, why is that selected? We could have the... Input processing. ...

**[44:48] Rob:** Okay.

**[44:51] Michal:** And we have the spike point, as well.

**[44:51] Jan:** How long? OK.

**[44:56] Michal:** I think that you move the spike ASR to the...

**[45:03] Jan:** Well, yeah, it's.

**[45:05] Rob:** I think all the spikes and anything with the word dogfooded or spike in it is probably closer to a feature or a task that we could use for right issue. And the others, I think, are a little higher level.

**[45:24] Jan:** You mean also for these?

**[45:26] Rob:** I think each one of those is probably a feature or task, each post-it note.

**[45:35] Jan:** Right. So does that mean it's good for? Write issue or is it too big?

**[45:46] Rob:** No, no, no, it's okay for write issue, because I think write issue can write issue has instructions in it to be like, please like tag this with like feature or epic or something if it's getting too large.

**[45:48] Jan:** All right. Mm-hmm.

**[46:06] Rob:** It's more that like... It would be silly for you to go issue by issue for some of these when you can just say, here are 7 issues, they all belong in one epic. Please write the description for that epic. Please consult the PRDs to do so.

**[46:40] Jan:** So you're wanting to make my life easier?

**[46:45] Rob:** .. My main thing is, I don't want to clutter the issue tracker, but I, but I also do want to, but yes. I hope by the issue tracker not being cluttered and disorganized, it makes it easier for you to have a sense of where things are at.

**[47:17] Jan:** Right. I mean, just looking at what we have, like the way that I... Luster it now.

**[47:29] Rob:** Mhm.

**[47:29] Jan:** For me, makes. And. The. For me, that kind of makes sense. ... Maybe even like that. So that would only be like a four. Warish epics. And so I'm late.

**[47:55] Rob:** Right.

**[47:57] Jan:** With the stuff in here.

**[47:59] Rob:** Yeah.

**[47:59] Jan:** And perk.

**[48:02] Rob:** And learner data debatably could even be grouped with. Dog food, old data, limited basic debt lessons.

**[48:13] Jan:** Well, that's Contentstack Factory here, right? I did, I mean, yeah, you could you could see that as part of the loop if you...

**[48:15] Rob:** Yeah, yeah. Oh. Sure, right.

**[48:21] Jan:** But I see that more as a learner thing that has to do with the progress more.

**[48:27] Rob:** Okay, that's fine with me. That's fine with me.

**[48:28] Jan:** And why did the avatar is? Where do we put avatar?

**[48:38] Rob:** Oh.

**[48:39] Jan:** Yeah, yeah, this is all the LLMs, the ASR, TTS.

**[48:45] Rob:** Yeah. Yeah, sort of LLMs, evaluator. Curriculum Factory Learner Progress.

**[48:58] Jan:** -huh.

**[48:59] Michal:** Yeah.

**[49:00] Rob:** Okay, if... I guess for like my perspective, like if you Jon want to sort of make. these into epics and like clean up whatever epics are there because they're no longer useful like to us. That's great. And then I think like... Me and Michal can like start. Like once things are kind of grouped into epics and maybe there's some like... ... Initial. issues for the roughly for these individual post-it notes, we can go in and like use write issue to sort of expand them out. Or you can, I mean like either or.

**[49:50] Jan:** .. How about yeah? Yeah, good idea. I would like actually to do the first few. Maybe to go through the right issue together.

**[50:12] Rob:** Oh, sure.

**[50:13] Jan:** To get like a feeling for what's... that we're on the same page and that we're like aligned on the answers that we would give if it is on. And then we can see if that's something where you want me to do it or something that you do. In either case, I think it needs this definition of.

**[50:21] Rob:** Mhm.

**[50:37] Jan:** Ready. step where we say, OK. I've seen it. You've seen it. We agree on what's in there.

**[50:46] Rob:** Okay. Yeah, that sounds great. Do you want to do that? Do you want to do that tomorrow? I'm being explicitly asked to join the other meeting now. I'm sorry.

**[51:00] Jan:** Okay.

**[51:00] Rob:** I must go. Yes.

**[51:02] Jan:** Bye. Thank you.

**[51:02] Michal:** Hi, and Jan, only to comment that tomorrow is holiday in Spain.

**[51:11] Jan:** Yes, yes, yes, yes, good for you. Thank you for the reminder, yeah, you we wrote that, but I had of course forgotten about it again.

**[51:14] Michal:** Yeah, that's. Don't worry, and I wait to write to you with my vacation that I mentioned, like, I don't remember if you remember a few days ago that I have three days of vacation in this month, the next month, that like the half of the...

**[51:34] Jan:** You don't have to tell me, like, I think technically you should tell Sergey.

**[51:38] Michal:** True. Okay.

**[51:41] Jan:** But... Let me know.

**[51:44] Michal:** Yeah, that's I will, I will. OK, I will put on the chart the dates, but I will. But yeah, I will tell this to Sergey too, because was approved like the a lot of time ago. I hope that I can do this, but yeah, I will take it with the Sergey.

**[52:04] Jan:** Yeah, I don't even like, yeah, I don't even know how to do that, have it, but...

**[52:08] Michal:** Okay, but yeah, because now, yeah, I have approved by the before team that now I need to check it with, okay. Don't worry about that.

**[52:20] Jan:** Okay, so, but in terms of what stuff is, this is the learner progress.

**[52:28] Michal:** Yeah, wait, yeah.

**[52:30] Jan:** And this is, what is this? The... ...

**[52:39] Michal:** A.I. stuff or something related, yeah, and I wait. Because we mix here the speech to text and text to speech, right? And the avatar. And they are part of the...

**[52:58] Jan:** But.

**[53:04] Michal:** And... Yeah, something like that, or... Investigation, or because a lot of things, I think, so they're here are like... Spikes, right?

**[53:19] Jan:** Yeah.

**[53:20] Michal:** Because is the front end provide like the what if we're going to create or not the TTS endpoint if we use ASR or if we going to foot avatar or whatever right that benching benchmarking for audio models that. ... As possible. That.

**[53:51] Jan:** Yes.

**[53:52] Michal:** Yeah, that is the benchmarking for, like, it seems like all investigations, right? So something like that. This section, this group of the tasks.

**[54:05] Jan:** Yeah, what's...

**[54:08] Michal:** The.

**[54:09] Jan:** I mean, that's a third person.

**[54:11] Michal:** Now I don't have any name, maybe we can ask the cloud what could be a cool epic name for this part of the group.

**[54:20] Jan:** Well, right now it's this. That's not a cool name, but...

**[54:25] Michal:** Yeah, yeah, yeah, yeah, I know.

**[54:26] Jan:** The best that I could come up with.

**[54:28] Michal:** Yeah, yeah, but I think so.

**[54:32] Jan:** Okay, so I go and have a look at the epics.

**[54:37] Michal:** Okay.

**[54:39] Jan:** And I will try to... Put issues in.

**[54:48] Michal:** Okay.

**[54:49] Jan:** Do can you do how to assign an epic to a milestone?

**[54:55] Michal:** Yeah, , yeah, I think I think so. Let's let me check. I think so. Let's go here. Yeah, I can share my screen if you want.

**[55:07] Jan:** Theis.

**[55:08] Michal:** Where this here is like the... Yeah. There is some issue that you have right open it right now we have that is assigned it to me and here you have the milestones that you can assign the milestones and what is needed is create a new milestone right that I don't know what was name Evalu. I evaluate those or whatever, and you create new milestone and you can use it here, right?

**[55:42] Jan:** A dog fooding would be one, but maybe if we find a better name that doesn't sound so much like dog food, like internal.

**[55:45] Michal:** Ohh. Yeah. Yeah, and in this case, I think so that you can, or you, because I see that we have the epic level, like for the epics and milestones that you can create here right inside the insights, there's some issue when you go to the issue.

**[56:04] Jan:** Mhm.

**[56:08] Michal:** You can get the issue, and you can... Create the milestones here, right? Or assign one of them.

**[56:20] Jan:** Okay, yeah, I'll see. Where this takes me? Thank you.

**[56:28] Michal:** Well, thank you so much, and if you have... Any problem or whatever, you can call me or ping me. I'm still working.

**[56:37] Jan:** Oh, thank you. Bye-bye.

**[56:38] Michal:** And tomorrow it is something important and I will be watching the teams or something if you need my help or Rob, but I understand that not should be.

**[56:45] Jan:** Yeah. Are you are you back Friday?

**[56:51] Michal:** Yeah, no, no, it's only tomorrow.

**[56:54] Jan:** Okay, okay, good. Okay.

**[56:55] Michal:** I'm back on the on the Tuesday and Friday, right?

**[56:59] Jan:** Okay. Awesome. Thank you. Bye-bye.

**[57:02] Michal:** Okay. Bye.

---