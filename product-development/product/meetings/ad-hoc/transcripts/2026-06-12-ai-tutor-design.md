# Meet about AI Tutor Design

**Date:** 2026-06-12
**Start:** 2026-06-12T13:00:00.000Z
**End:** 2026-06-12T13:45:00.000Z

---

WEBVTT

00:00:03.251 --> 00:00:04.411
<v Rob Zinkov>No one watches them.</v>

00:00:05.211 --> 00:00:07.531
<v Chayan  Roy>That's good. Okay, cool.</v>

00:00:05.611 --> 00:00:22.171
<v Rob Zinkov>later. So it's just almost 99% of the time, everyone just reads the summary of the transcript, but it's good to have the transcript just in case the summary made something up.</v>

00:00:22.651 --> 00:00:23.131
<v Chayan  Roy>Sure.</v>

00:00:23.771 --> 00:00:25.771
<v Rob Zinkov>Yeah. All right. Okay.</v>

00:00:26.811 --> 00:00:28.571
<v Rob Zinkov>So, finally, how you doing?</v>

00:00:29.611 --> 00:00:49.291
<v Chayan  Roy>How's it going? Yeah, I'm very, it's been very intense, right? Just have to deliver the sign-up flows very soon to Daniel, and I just had a chat with Carmen from the branding team. We had some back and forth for the logo design system stuff. Yeah, very, very intense shipping flows in mobile.</v>

00:00:33.211 --> 00:00:33.611
<v Rob Zinkov>Yeah.</v>

00:00:38.611 --> 00:00:39.131
<v Rob Zinkov>Mhm.</v>

00:00:49.371 --> 00:00:52.251
<v Chayan  Roy>I think you got access now to the Figma. You saw some of those.</v>

00:00:52.491 --> 00:01:04.811
<v Rob Zinkov>I saw you share it. I don't know if I have access. If I don't have access, I'll message you. Yeah. But no, yeah, I saw that was pretty intense. Kind of, yeah, I guess your first week or two and you have to do a full like Figma for a mobile app.</v>

00:00:57.131 --> 00:00:57.691
<v Chayan  Roy>All good.</v>

00:01:07.091 --> 00:01:27.411
<v Chayan  Roy>Yeah, but it was it was fun. I'm happy to happy to do it. I mean, some of the stuff I did it before, like coming, like as an assignment, and some of the stuff I'm just checking how much we can use because the Berlitz existing design system is really old school and I want to make it make it make it still kind of look very 2026 app.</v>

00:01:15.651 --> 00:01:16.131
<v Rob Zinkov>Mhm.</v>

00:01:23.051 --> 00:01:23.691
<v Rob Zinkov>Yeah.</v>

00:01:28.171 --> 00:01:43.851
<v Chayan  Roy>So there is some, there needs to be some, I still want to respect the blue or some stuff like this, but still it needs to be sci-fi, cutting edge, and it needs to at least have some standards, right?</v>

00:01:28.491 --> 00:01:29.131
<v Rob Zinkov>Right.</v>

00:01:44.651 --> 00:01:50.171
<v Rob Zinkov>Yeah, yeah, I, I know what you, yeah, it's the, yeah, the corporate blue just kind of puts can put people to sleep.</v>

00:01:50.571 --> 00:02:08.091
<v Chayan  Roy>I mean, the corporate blue and this like the white thing and it looks like very bureaucratic and this is and also dark mode and white mode. If you need two modes, some of the sci-fi, the cutting edge appeal a little bit goes. So yeah, just navigating.</v>

00:02:08.851 --> 00:02:29.371
<v Chayan  Roy>UX, I think we have a baseline version of the apps. Most of the major screens are kind of mapped. What happens under learn tab, what happens happens under practice tab, tutor progress. So I think as a starting point, the baseline is there. It now it just needs to be like flow wise, okay, we finished the sign up flow, then we finish the.</v>

00:02:15.491 --> 00:02:15.971
<v Rob Zinkov>Mhm.</v>

00:02:18.811 --> 00:02:19.211
<v Rob Zinkov>Right.</v>

00:02:29.691 --> 00:02:49.931
<v Chayan  Roy>what happens in the learn tab and there has been some back and forth discussions with the LX team. Like I've been just trying to understand how much of the existing content ports into mobile. It doesn't port one is to one, but it needs to be broken down to some smaller parts. I think what's relevant for this discussion would be the...</v>

00:02:50.091 --> 00:02:53.291
<v Chayan  Roy>Yeah, I guess, and yeah.</v>

00:02:52.811 --> 00:03:09.051
<v Rob Zinkov>Yeah, AI author, AI tutor, and yeah, yeah, so basically what I kind of want to figure out is like, what do you need? Like, what should like, what flows do you, what endpoints do you need to hit and how and sort of how you want that information kind of coming to you?</v>

00:03:09.211 --> 00:03:09.931
<v Chayan  Roy>Understood.</v>

00:03:11.371 --> 00:03:29.771
<v Chayan  Roy>I mean, from I am designing the screens on Figma right now, so I don't need an endpoint right now, but once we are prototyping it in Claude, it some like a for Tavos, I would just it needs a need an API endpoint, that's how I would prototype that, but from you, whatever.</v>

00:03:28.571 --> 00:03:28.931
<v Rob Zinkov>Right.</v>

00:03:29.931 --> 00:03:34.811
<v Chayan  Roy>I guess also Daniel will be involved in that discussion. So yeah.</v>

00:03:33.851 --> 00:03:34.331
<v Rob Zinkov>Yeah.</v>

00:03:36.171 --> 00:03:54.491
<v Rob Zinkov>Yeah, so I mean, I think basically what we're going to give you is like for the text, I think you're just going to get these different web sockets that you can then kind of push through. My intention is not to, again, some of this I think will be kind of coordinating with Daniel a little bit.</v>

00:03:43.691 --> 00:03:44.011
<v Chayan  Roy>Yeah.</v>

00:03:55.131 --> 00:04:05.211
<v Rob Zinkov>My understanding is like, I'm not going to be giving you web views. Like, it just like, whatever you need, like you will get that content to sort of immediately render.</v>

00:04:05.691 --> 00:04:07.051
<v Chayan  Roy>Yeah, yeah.</v>

00:04:06.651 --> 00:04:13.451
<v Rob Zinkov>So everything kind of looks clear and natural. It just, you show me earlier, you have these things where like, oh, I would like these overlays or oh, I would like this.</v>

00:04:13.771 --> 00:04:20.451
<v Chayan  Roy>Oh yeah, yeah, yeah, those are interesting. I mean, I can show you in Figma. If you just jump onto Figma, I can have...</v>

00:04:20.011 --> 00:04:23.051
<v Rob Zinkov>Sure, can you just give me a URL and I'll go.</v>

00:04:22.491 --> 00:04:31.611
<v Chayan  Roy>Yeah, sure. I'm happy to, I'm happy to give you the link, so that's the that's the link, and if you just...</v>

00:04:33.371 --> 00:04:33.851
<v Rob Zinkov>Okay.</v>

00:04:35.131 --> 00:04:36.011
<v Rob Zinkov>Um...</v>

00:04:37.251 --> 00:04:38.971
<v Chayan  Roy>Where are you from, by the way, Rob?</v>

00:04:39.171 --> 00:04:41.771
<v Rob Zinkov>So I'm originally from the US, but I live in Berlin.</v>

00:04:42.251 --> 00:04:42.891
<v Chayan  Roy>Nice.</v>

00:04:43.291 --> 00:04:47.051
<v Rob Zinkov>So, okay, what email should I be using?</v>

00:04:44.891 --> 00:04:48.731
<v Chayan  Roy>Are you in Berlin? I was, oh yeah, right, because we were supposed to meet, right? Yeah.</v>

00:04:49.291 --> 00:04:56.091
<v Rob Zinkov>Well, we could meet, that was the thing. What links should I be using? Should I be trying to log in with my Berlitz or?</v>

00:04:51.091 --> 00:04:51.611
<v Chayan  Roy>Yeah.</v>

00:04:56.251 --> 00:04:57.211
<v Chayan  Roy>Berlitz.com.</v>

00:04:58.491 --> 00:05:00.091
<v Rob Zinkov>Okay, so let me just, okay.</v>

00:05:02.771 --> 00:05:04.171
<v Rob Zinkov>Hopefully, this like...</v>

00:05:06.651 --> 00:05:07.371
<v Rob Zinkov>Um...</v>

00:05:10.411 --> 00:05:16.251
<v Chayan  Roy>Yeah, you should be able to log in and if you need access, I'm happy to give you access.</v>

00:05:17.291 --> 00:05:20.891
<v Rob Zinkov>I don't know if I have access.</v>

00:05:20.811 --> 00:05:29.371
<v Chayan  Roy>I can, I can give you, as soon as you log in, it will it will ask me that it is Rob Zinkov is asking to view, and I can give you access.</v>

00:05:29.771 --> 00:05:30.971
<v Rob Zinkov>Yeah, okay, let me...</v>

00:05:34.331 --> 00:05:40.091
<v Rob Zinkov>Because I don't know if I have a like Rob doesn't cover Berlitz.com Figma account already.</v>

00:05:42.491 --> 00:05:45.531
<v Rob Zinkov>Did you have to create a Figma account for yourself with the Berlitz email?</v>

00:05:42.811 --> 00:05:43.371
<v Chayan  Roy>Anyone?</v>

00:05:45.931 --> 00:05:53.371
<v Chayan  Roy>Yeah, just, just, just, just punch in your email ID and I think it should be. Or just send.</v>

00:05:46.691 --> 00:05:48.331
<v Rob Zinkov>Okay, okay, then let me, okay.</v>

00:05:52.771 --> 00:05:56.811
<v Rob Zinkov>All right, then I'm just gonna do, okay, I'm gonna just do that now. Okay.</v>

00:05:55.771 --> 00:06:00.251
<v Chayan  Roy>Or just send me your email ID, maybe I can send you an email or something.</v>

00:06:01.371 --> 00:06:02.491
<v Rob Zinkov>Okay, I have...</v>

00:06:04.771 --> 00:06:05.371
<v Rob Zinkov>There we go.</v>

00:06:04.971 --> 00:06:08.491
<v Chayan  Roy>When you when you go to the link, what what does it say?</v>

00:06:12.011 --> 00:06:12.811
<v Rob Zinkov>Hold on.</v>

00:06:20.531 --> 00:06:21.291
<v Rob Zinkov>It's...</v>

00:06:24.011 --> 00:06:28.171
<v Rob Zinkov>I'm still just trying to get myself verified, so just give me a second.</v>

00:06:29.611 --> 00:06:30.251
<v Rob Zinkov>And.</v>

00:07:23.291 --> 00:07:26.251
<v Rob Zinkov>I need to request access. I've requested access.</v>

00:07:27.771 --> 00:07:28.571
<v Chayan  Roy>I have given you.</v>

00:07:29.451 --> 00:07:31.531
<v Rob Zinkov>Okay, cool. So...</v>

00:07:37.451 --> 00:07:39.771
<v Chayan  Roy>Do, do, are you in the flight?</v>

00:07:40.411 --> 00:07:43.531
<v Rob Zinkov>I am loading it now. Okay.</v>

00:07:48.011 --> 00:07:56.731
<v Chayan  Roy>Okay, I see. So just I think the best way would be to just follow me and you can just click on follow and I can give you a quick walkthrough.</v>

00:07:52.891 --> 00:07:53.371
<v Rob Zinkov>Yeah.</v>

00:07:58.011 --> 00:07:58.571
<v Rob Zinkov>Sure.</v>

00:08:01.771 --> 00:08:04.571
<v Chayan  Roy>Okay, cool. So you use follow me, right?</v>

00:08:01.851 --> 00:08:03.291
<v Rob Zinkov>I okay, I.</v>

00:08:05.131 --> 00:08:06.811
<v Rob Zinkov>Yes, okay, I followed you now.</v>

00:08:07.051 --> 00:08:26.851
<v Chayan  Roy>Okay, okay, perfect. Boom. I, I just I just cut the crap and moved straight to the the the main screens, right? So, yeah, it's not it's not some rocket science, just so just like when the learner is talking, let's say, to the avatar.</v>

00:08:15.291 --> 00:08:15.691
<v Rob Zinkov>Yeah.</v>

00:08:16.811 --> 00:08:17.291
<v Rob Zinkov>Mhm.</v>

00:08:26.411 --> 00:08:26.891
<v Rob Zinkov>Mhm.</v>

00:08:26.971 --> 00:08:35.931
<v Chayan  Roy>The AI tutor, like, okay, it asks for, they're talking and there is some real-time, basically some transcription with correction, right?</v>

00:08:36.171 --> 00:08:36.731
<v Rob Zinkov>Right.</v>

00:08:37.611 --> 00:08:55.931
<v Chayan  Roy>It is just like they have said something wrong and it kind of corrects. And then when they say it did auto corrects kind of like, okay, you said this, it's correct. You said, this is kind of where the initial designs, but we can discuss along the way.</v>

00:08:54.331 --> 00:08:54.811
<v Rob Zinkov>Mhm.</v>

00:08:56.251 --> 00:09:15.371
<v Chayan  Roy>how we want to do this for the MVP or the MLP, we can keep it out or it's nice to kind of have, because for someone who is learning a language, maybe sometimes we can have some options that they can switch on and off some of these heads up displays, right? Yeah.</v>

00:08:58.491 --> 00:08:59.131
<v Rob Zinkov>Yeah.</v>

00:09:12.651 --> 00:09:13.051
<v Rob Zinkov>Yeah.</v>

00:09:15.131 --> 00:09:15.651
<v Rob Zinkov>Mhm.</v>

00:09:16.411 --> 00:09:16.811
<v Rob Zinkov>Yeah.</v>

00:09:16.651 --> 00:09:19.611
<v Chayan  Roy>That's pretty much it, man. I mean, it's not, it's nothing.</v>

00:09:19.931 --> 00:09:21.371
<v Rob Zinkov>There's not a lot, yeah.</v>

00:09:22.491 --> 00:09:27.451
<v Rob Zinkov>Yeah, because we're thinking about things in terms of like, yeah, there are lessons.</v>

00:09:22.651 --> 00:09:22.971
<v Chayan  Roy>Yeah.</v>

00:09:26.011 --> 00:09:28.731
<v Chayan  Roy>Just give me a second, so just give me a second, Rob.</v>

00:09:28.971 --> 00:09:29.491
<v Rob Zinkov>No problem.</v>

00:09:58.011 --> 00:10:00.731
<v Chayan  Roy>Back, sorry someone was knocking the door.</v>

00:10:08.291 --> 00:10:10.171
<v Chayan  Roy>Which one? Which what?</v>

00:10:10.211 --> 00:10:14.011
<v Rob Zinkov>above where it says learn chapter practice, it looks very Duolingo.</v>

00:10:10.251 --> 00:10:10.331
<v Chayan  Roy>So</v>

00:10:15.211 --> 00:10:15.691
<v Chayan  Roy>Mhm.</v>

00:10:16.091 --> 00:10:18.171
<v Rob Zinkov>Um, so that that's pretty...</v>

00:10:16.891 --> 00:10:20.011
<v Chayan  Roy>Which, which, which, which specific screen are you looking at?</v>

00:10:20.731 --> 00:10:30.251
<v Rob Zinkov>Okay, let me pull my, so this screen, this screen, this screen, this screen, this screen, all look very Duolingo to me.</v>

00:10:30.571 --> 00:10:35.851
<v Chayan  Roy>Yeah, yeah, and uh, if you just come, if you just follow me on LMS mapping.</v>

00:10:36.731 --> 00:10:37.931
<v Rob Zinkov>Yeah, I'm still following you.</v>

00:10:38.491 --> 00:10:44.091
<v Chayan  Roy>So these they have this you see.</v>

00:10:43.211 --> 00:10:47.451
<v Rob Zinkov>Yeah, very, very old-fashioned quizzes.</v>

00:10:47.331 --> 00:11:12.211
<v Chayan  Roy>Yeah, these are very old-fashioned quizzes. These are, they're coming from the, like, they have some pick 61 multiple choice questions. So some of these LMS templates, and I think these LMS templates would have kind of select the correct image. Basically, it's one is to one, right? Some of these templates map one is to one, and some of them don't.</v>

00:10:58.771 --> 00:10:59.251
<v Rob Zinkov>Mhm.</v>

00:11:09.291 --> 00:11:09.451
<v Rob Zinkov>Mm.</v>

00:11:12.331 --> 00:11:18.411
<v Chayan  Roy>And I think some of the stuff under Learn tab is very kind of like microlearning.</v>

00:11:19.211 --> 00:11:38.411
<v Rob Zinkov>Yeah. So some design questions for you. I mean, maybe these are product questions, but I'm just going to give them to you directly. So with their agents, you know, we can introduce a notion of memory so we know what was discussed before.</v>

00:11:19.531 --> 00:11:19.771
<v Chayan  Roy>Yeah.</v>

00:11:38.811 --> 00:11:39.291
<v Chayan  Roy>Mhm.</v>

00:11:38.811 --> 00:11:46.891
<v Rob Zinkov>And that could be incorporated in future lessons. The question is like, how much is that on the roadmap? How much is that something you're trying to design for?</v>

00:11:49.611 --> 00:11:51.851
<v Chayan  Roy>You mean when the learner has...</v>

00:11:53.011 --> 00:12:07.531
<v Chayan  Roy>While the learner is learning, we can extract what has what the learner is at which level, and we can basically show up those cards which the learner needs based on their learning journey. That's what you mean.</v>

00:12:10.171 --> 00:12:28.251
<v Rob Zinkov>So yes, there is this thing of just, we know how well they've been doing for different tasks and where they're weak and where they're strong. We can sort of use that to sort of guide exercise creation. Or sorry, we can use that to guide the exercise they practice. So things that are weaker, they</v>

00:12:14.491 --> 00:12:15.011
<v Chayan  Roy>Mhm.</v>

00:12:23.011 --> 00:12:23.531
<v Chayan  Roy>Mhm.</v>

00:12:28.491 --> 00:12:32.331
<v Rob Zinkov>they do more, they spend more time on things they're good at, they spend less time on.</v>

00:12:32.571 --> 00:12:32.891
<v Chayan  Roy>Yeah.</v>

00:12:34.171 --> 00:12:49.691
<v Chayan  Roy>Yeah, if they're if they if they can't speak like a particular spelling or if they're making more mistakes, we show up pretty much pretty standard practice, right? To to make them practice the stuff more which they're not able to, yeah, right.</v>

00:12:45.051 --> 00:12:45.371
<v Rob Zinkov>Yeah.</v>

00:12:47.131 --> 00:13:03.771
<v Rob Zinkov>Yeah. Right. But also there's, for the avatar, the sort of same thing happens. We remember the conversation they had. We remember anything they sort of said within that conversation and the kind of mistakes they made.</v>

00:12:58.331 --> 00:12:58.891
<v Chayan  Roy>Mhm.</v>

00:13:03.931 --> 00:13:04.411
<v Chayan  Roy>Mhm.</v>

00:13:06.571 --> 00:13:15.211
<v Rob Zinkov>Do you see it in the design that there's some way of sort of also incorporating that here where the agent knows you have trouble pronouncing something so?</v>

00:13:16.491 --> 00:13:18.651
<v Rob Zinkov>There's that sort of also guided in there.</v>

00:13:19.531 --> 00:13:20.971
<v Rob Zinkov>Sorry, the avatar, yeah.</v>

00:13:19.611 --> 00:13:29.291
<v Chayan  Roy>Yeah, yeah, I mean the agent will just simply start talking about that, no, without a UI element. I mean, do you need a UI element for that?</v>

00:13:25.691 --> 00:13:26.251
<v Rob Zinkov>Right.</v>

00:13:31.531 --> 00:13:42.651
<v Rob Zinkov>I'm asking, do you think it makes sense to have a reference to a previous conversation, or do you think just more naturally just have the avatar say, previously you had trouble pronouncing strict?</v>

00:13:45.371 --> 00:13:49.131
<v Rob Zinkov>Do you want to, you know, you know, well hush prosperous do?</v>

00:13:45.611 --> 00:13:46.011
<v Chayan  Roy>Thank you.</v>

00:13:50.571 --> 00:14:06.491
<v Chayan  Roy>Well, just Prakesh, Prix 2, yeah, we, we, we can, we can, we can reference, we can reference old histories, like we can reference some of the stuff, and those references can still show up in a heads-up display like this.</v>

00:13:52.891 --> 00:13:54.411
<v Rob Zinkov>Well, I suppose, please do.</v>

00:14:07.771 --> 00:14:26.251
<v Rob Zinkov>Right. Okay, the other thing is there's a lesson from the current AI avatar they have. So they have this like vocab lesson where you're supposed to use certain words and then the words kind of they appear somewhere and then as you say them.</v>

00:14:08.811 --> 00:14:09.211
<v Chayan  Roy>Yeah.</v>

00:14:21.731 --> 00:14:22.211
<v Chayan  Roy>Mhm.</v>

00:14:26.531 --> 00:14:28.171
<v Rob Zinkov>They essentially get checked off a list.</v>

00:14:29.611 --> 00:14:30.091
<v Chayan  Roy>Mhm.</v>

00:14:31.411 --> 00:14:31.851
<v Rob Zinkov>Um...</v>

00:14:31.771 --> 00:14:37.371
<v Chayan  Roy>Do you, I mean, do you have a, like, where do you mean, like in the current Berlitz platform?</v>

00:14:38.011 --> 00:14:42.731
<v Rob Zinkov>Yeah, on the current Berlitz platform, there is an offering that has that, so...</v>

00:14:41.371 --> 00:14:41.931
<v Chayan  Roy>Mhm.</v>

00:14:45.291 --> 00:14:46.171
<v Rob Zinkov>I, I can.</v>

00:14:47.691 --> 00:14:56.411
<v Rob Zinkov>I can try, I can share a screen to show it or I can just send you a screen. I think the easiest thing might be if I just share, show, share you, send you screenshots so you can see.</v>

00:14:55.611 --> 00:14:59.051
<v Chayan  Roy>Also fine, or if you share your screen, also fine, yeah.</v>

00:14:59.771 --> 00:15:01.211
<v Rob Zinkov>Yeah, yeah, okay, so let's...</v>

00:15:02.971 --> 00:15:04.891
<v Rob Zinkov>Let me go to.</v>

00:15:08.571 --> 00:15:08.971
<v Rob Zinkov>You.</v>

00:15:18.971 --> 00:15:30.891
<v Chayan  Roy>I took the, I saw the, I saw that lady in the black coat and something wearing white. I think I took those AI tutor, probably that.</v>

00:15:20.091 --> 00:15:21.211
<v Rob Zinkov>So, yeah.</v>

00:15:28.651 --> 00:15:29.371
<v Rob Zinkov>Yeah.</v>

00:15:32.971 --> 00:15:37.131
<v Rob Zinkov>So, okay, let me share my screen.</v>

00:15:38.011 --> 00:15:38.411
<v Chayan  Roy>Okay.</v>

00:15:38.651 --> 00:15:39.451
<v Rob Zinkov>Um.</v>

00:15:45.251 --> 00:15:48.971
<v Rob Zinkov>Where is the where is the screen share button?</v>

00:15:50.091 --> 00:15:50.491
<v Chayan  Roy>On.</v>

00:15:51.251 --> 00:15:51.931
<v Rob Zinkov>Yeah, here it is.</v>

00:15:55.371 --> 00:15:56.251
<v Chayan  Roy>Okay, yeah.</v>

00:15:56.291 --> 00:15:56.491
<v Rob Zinkov>Yeah.</v>

00:15:58.891 --> 00:15:59.211
<v Rob Zinkov>Look.</v>

00:15:59.211 --> 00:16:00.891
<v Chayan  Roy>Yeah, this is the one that I was saying.</v>

00:16:04.931 --> 00:16:06.731
<v Rob Zinkov>But not right now, so...</v>

00:16:06.331 --> 00:16:07.851
<v Chayan  Roy>I can't hear you, but yeah.</v>

00:16:07.891 --> 00:16:09.771
<v Rob Zinkov>Yeah, so you, do you hear me now?</v>

00:16:10.971 --> 00:16:12.171
<v Chayan  Roy>Very faintly.</v>

00:16:12.731 --> 00:16:25.131
<v Rob Zinkov>So, I'm gonna talk loudly, and then so what they'll have is these words here, and then what you can say is, you can say the different, well, ohh, OK.</v>

00:16:16.011 --> 00:16:16.251
<v Chayan  Roy>Just.</v>

00:16:18.411 --> 00:16:18.891
<v Chayan  Roy>Okay.</v>

00:16:27.851 --> 00:16:31.851
<v Rob Zinkov>So, let's, I mean, do I sound normal now?</v>

00:16:32.491 --> 00:16:33.371
<v Chayan  Roy>Yeah, all good.</v>

00:16:33.771 --> 00:16:46.091
<v Rob Zinkov>Okay, so what you have is, here I'll start sharing screen. So what you have is, you have these side panels and then as you speak, they sort of light up.</v>

00:16:46.491 --> 00:16:46.891
<v Chayan  Roy>Yup.</v>

00:16:47.131 --> 00:16:51.371
<v Rob Zinkov>Yeah, but it's sort of made for, I think, more of the desktop where you kind of have.</v>

00:16:52.531 --> 00:16:52.971
<v Rob Zinkov>Dice.</v>

00:16:53.051 --> 00:16:55.611
<v Chayan  Roy>We have some real estate on the desktop on the side, yeah.</v>

00:16:56.011 --> 00:17:01.291
<v Rob Zinkov>Yeah. Do you have any sort of flow in mind for that kind of exercise?</v>

00:17:02.651 --> 00:17:15.211
<v Chayan  Roy>We do, I mean, the, the, I mean, my idea is anything else that needs to happen happens in that HUD display, right? The heads up display, because...</v>

00:17:14.571 --> 00:17:21.531
<v Rob Zinkov>Okay, so you just figure what will happen is as soon as you say a word, it'll sort of like pop up.</v>

00:17:22.571 --> 00:17:43.611
<v Chayan  Roy>Pop up, I mean, if it is true intrusive for the user, the user can also like stop that transcription because if they, if they don't feel like, I mean, in the beginning, the idea is if the learner is talking to some avatar for the first time, it might be a bit disorienting, but ideally, the heads up display kind of acts as the text layer.</v>

00:17:43.851 --> 00:18:02.891
<v Chayan  Roy>Any kind of text kind of goes in there. Any kind of text. It can be like your old discussions, your old references, words, pronunciation, correction. That's the idea. But I also wanted to quickly, quickly address something that you mentioned earlier. The idea was that this whole...</v>

00:17:45.211 --> 00:17:45.851
<v Rob Zinkov>Okay.</v>

00:17:54.011 --> 00:17:56.571
<v Rob Zinkov>Okay, alright, okay, I, I see, okay, now.</v>

00:18:03.531 --> 00:18:20.091
<v Chayan  Roy>Like this whole structure, it's kind of like a broad kind of a baseline structure that we have. It's not, it's at a very much wireframe level, like kind of treated like mockups. And what I'm doing right now, and what I'm doing right now is...</v>

00:18:05.811 --> 00:18:06.291
<v Rob Zinkov>Mmh.</v>

00:18:08.811 --> 00:18:09.451
<v Rob Zinkov>Yeah.</v>

00:18:13.411 --> 00:18:14.331
<v Rob Zinkov>Of course.</v>

00:18:16.731 --> 00:18:18.211
<v Rob Zinkov>Definite 100%.</v>

00:18:22.331 --> 00:18:42.891
<v Chayan  Roy>Finishing the flows one by one. So on the very right, if you see, like, I'm just finishing up the sign of flow, right? And I think when we come to the learn tab or when we come to these kind of finishing the flows, then we can kind of, you know, like do a boxing session and understand like what really makes sense. Duolingo, yes, no.</v>

00:18:26.171 --> 00:18:27.451
<v Rob Zinkov>Yeah, the sign of flow.</v>

00:18:43.291 --> 00:18:47.451
<v Chayan  Roy>You know, we can go into the more nitty-gritties of the each of the flows, right? Yeah.</v>

00:18:43.691 --> 00:18:44.251
<v Rob Zinkov>Okay.</v>

00:18:48.331 --> 00:18:54.411
<v Rob Zinkov>Right. Yeah, I mean, that's fine for me. Okay.</v>

00:18:52.171 --> 00:18:52.491
<v Chayan  Roy>Yeah.</v>

00:18:55.931 --> 00:18:58.571
<v Rob Zinkov>Um, I think...</v>

00:19:00.011 --> 00:19:04.011
<v Rob Zinkov>Yeah, I think that's very, okay, that's fairly clear in that regard for me.</v>

00:19:04.891 --> 00:19:05.291
<v Chayan  Roy>Yeah.</v>

00:19:05.851 --> 00:19:06.411
<v Rob Zinkov>Um...</v>

00:19:07.691 --> 00:19:08.171
<v Rob Zinkov>Okay.</v>

00:19:09.931 --> 00:19:14.171
<v Rob Zinkov>Yeah, I didn't have much more to sort of say that I kind of wanted to sort of...</v>

00:19:13.131 --> 00:19:13.531
<v Chayan  Roy>Eat.</v>

00:19:15.371 --> 00:19:24.331
<v Rob Zinkov>get a sense of like what you were needing and also also kind of a just like, hey, I'm one of the like AI machine learning people. So like.</v>

00:19:25.851 --> 00:19:26.251
<v Chayan  Roy>Sure.</v>

00:19:25.931 --> 00:19:26.331
<v Rob Zinkov>Yeah.</v>

00:19:27.451 --> 00:19:34.971
<v Chayan  Roy>And I think there is some value, like, for example, if you see the screen, do you see, do you still follow me, Rob?</v>

00:19:34.651 --> 00:19:36.091
<v Rob Zinkov>I am still following you, yes.</v>

00:19:36.811 --> 00:19:46.611
<v Chayan  Roy>I think there would be some places where there would be, there might be, the student might have to, you know, like...</v>

00:19:47.691 --> 00:20:06.251
<v Chayan  Roy>The student might have to reference some vocabulary. I don't know if what's the plan in LX team. Like if the student has to refer some vocabulary or grammar or whatever, ideally if the content becomes too much, we can always minimize the call like this and let the student go through some of those.</v>

00:20:05.691 --> 00:20:06.331
<v Rob Zinkov>Right.</v>

00:20:07.451 --> 00:20:07.931
<v Chayan  Roy>Hello?</v>

00:20:10.291 --> 00:20:10.811
<v Chayan  Roy>Mhm.</v>

00:20:13.851 --> 00:20:14.491
<v Chayan  Roy>Mhm.</v>

00:20:14.571 --> 00:20:18.091
<v Rob Zinkov>Those words can probably fit into an overlay just fine.</v>

00:20:18.091 --> 00:20:18.571
<v Chayan  Roy>Sure.</v>

00:20:20.331 --> 00:20:32.331
<v Rob Zinkov>But I could imagine other activities where, you know, you're trying to practice reading or something maybe. But I think from my perspective, it's one of those things where...</v>

00:20:27.611 --> 00:20:28.091
<v Chayan  Roy>Yeah.</v>

00:20:33.931 --> 00:20:34.971
<v Rob Zinkov>We sort of...</v>

00:20:36.411 --> 00:20:45.211
<v Rob Zinkov>We have to decide what lesson content we want to create. And after we sort of decided that, then it'll make sense how it should like fit in.</v>

00:20:45.531 --> 00:21:04.371
<v Chayan  Roy>Exactly. Ideally the user stays, I think, would you agree that ideally the user kind of stays on one screen without switching much back and forth? Like if they're learning from the AI avatar, they just stay on the AI avatar and we kind of try to do most of the stuff there as a principle.</v>

00:21:04.731 --> 00:21:08.171
<v Rob Zinkov>Um, my feeling is that it...</v>

00:21:09.291 --> 00:21:09.771
<v Rob Zinkov>Uh...</v>

00:21:11.371 --> 00:21:29.611
<v Rob Zinkov>Again, this is just my observations looking at the data, is that I think you kind of need to have, you need to be able to break up the flow. So there's like, you talk to the person in a little bit, you look away from a person, do a quiz, come back and look at them. Like, I think there's a little bit of a like,</v>

00:21:12.811 --> 00:21:14.171
<v Chayan  Roy>Sure, sure, go for it.</v>

00:21:30.011 --> 00:21:30.731
<v Chayan  Roy>Hybrid.</v>

00:21:31.211 --> 00:21:42.811
<v Rob Zinkov>Yeah, I think in terms of each like micro lesson, of course, but I suspect the reality is that no one wants to stare an AI avatar for like an hour straight.</v>

00:21:36.531 --> 00:21:37.011
<v Chayan  Roy>Mhm.</v>

00:21:42.971 --> 00:21:46.571
<v Chayan  Roy>No, not an hour for sure. That would be annoying.</v>

00:21:45.851 --> 00:21:47.931
<v Rob Zinkov>Well, like, in the sense of like...</v>

00:21:49.131 --> 00:21:49.851
<v Rob Zinkov>Oh.</v>

00:21:51.291 --> 00:22:05.051
<v Rob Zinkov>Like we can see this in the data, like people used, people are comfortable sort of using the video avatar for like some amount of time. They're more comfortable using the audio for some amount of time. So I think.</v>

00:22:03.371 --> 00:22:03.851
<v Chayan  Roy>Sure.</v>

00:22:06.091 --> 00:22:09.531
<v Rob Zinkov>I think a lot of engagement will come in like variety.</v>

00:22:10.011 --> 00:22:15.291
<v Chayan  Roy>Yeah, yeah, and which data are you referring to? Uh, do we have, are you do you have access to Berlitz data?</v>

00:22:10.651 --> 00:22:10.691
<v Rob Zinkov>I.</v>

00:22:13.451 --> 00:22:14.171
<v Rob Zinkov>So...</v>

00:22:15.691 --> 00:22:34.331
<v Rob Zinkov>Yeah, so I have access to the API data so I can see how long an average user session is. Currently, they average between 2:00 to 3:00 minutes median. They're fairly short. And people seem to prefer audio.</v>

00:22:23.131 --> 00:22:23.531
<v Chayan  Roy>Poll.</v>

00:22:27.491 --> 00:22:27.971
<v Chayan  Roy>Mhm.</v>

00:22:34.491 --> 00:22:38.971
<v Rob Zinkov>and text over video by a 10 to 1 margin.</v>

00:22:39.211 --> 00:22:40.091
<v Chayan  Roy>Interesting.</v>

00:22:40.811 --> 00:22:52.891
<v Rob Zinkov>Like, there's something about the video where people just don't like using it. So we're consistently seeing 10x to hours tracked for using the audio option versus the video option.</v>

00:22:53.611 --> 00:22:57.051
<v Chayan  Roy>That's on, yeah, that's pretty, that's pretty massive.</v>

00:22:57.531 --> 00:23:16.811
<v Rob Zinkov>And this isn't one, and that's on a per, that's like month to month. So we, I think we only had audio for a while, and then I think we introduced video two, three months ago. But even within the most recent month, again, people are preferring the audio or the text over the video in terms of hours used.</v>

00:23:15.691 --> 00:23:20.571
<v Chayan  Roy>Do we have some recordings or we probably don't have some recordings, right? Like how?</v>

00:23:20.731 --> 00:23:32.491
<v Rob Zinkov>We have the trans, we have transcripts of the interactions, and if you want, I can pull up a few of those for you to sort of just browse and look at and kind of see what they look like.</v>

00:23:22.971 --> 00:23:23.531
<v Chayan  Roy>Okay.</v>

00:23:24.731 --> 00:23:25.531
<v Chayan  Roy>Interesting.</v>

00:23:29.531 --> 00:23:30.091
<v Chayan  Roy>Sure.</v>

00:23:32.731 --> 00:23:53.851
<v Chayan  Roy>Absolutely. I think when I just took again from a very anecdotal experience, it was kind of annoying because that avatar would just like whatever you say, it would just make a very canned facial expression for everything that you say, you know, and it's just off-putting and annoying and that's why.</v>

00:23:38.091 --> 00:23:38.491
<v Rob Zinkov>Yeah.</v>

00:23:50.011 --> 00:23:50.891
<v Rob Zinkov>Yes.</v>

00:23:54.411 --> 00:24:14.411
<v Chayan  Roy>I've been building, before joining Berlitz, I worked on a AI girlfriend kind of a prototype with Tavis. And Tavis, actually, you have to open your camera. So Tavis have perception analysis, which Berlitz doesn't have. And Tavis kind of calibrates.</v>

00:23:58.531 --> 00:23:58.891
<v Rob Zinkov>Yeah.</v>

00:24:02.331 --> 00:24:03.051
<v Rob Zinkov>Sure, sure.</v>

00:24:07.411 --> 00:24:07.891
<v Rob Zinkov>Mhm.</v>

00:24:10.011 --> 00:24:10.571
<v Rob Zinkov>Right.</v>

00:24:14.731 --> 00:24:34.331
<v Chayan  Roy>The way the avatar speaks, it calibrates if the user is annoyed or if the user is bored, it kind of calibrates its personality based on the perception. And all this perception analysis actually can be fed back into, I mean, the instructor or whoever, like whoever is looking at it, we can get a perception data. I'm not sure.</v>

00:24:21.211 --> 00:24:21.931
<v Rob Zinkov>Right.</v>

00:24:23.771 --> 00:24:24.171
<v Rob Zinkov>Yeah.</v>

00:24:31.771 --> 00:24:32.411
<v Rob Zinkov>Yeah.</v>

00:24:34.491 --> 00:24:40.891
<v Chayan  Roy>What's the plan? I just got 2000 or some credits from Tavis. I go ahead.</v>

00:24:38.411 --> 00:24:39.611
<v Rob Zinkov>Yeah, so...</v>

00:24:40.491 --> 00:24:41.651
<v Rob Zinkov>Yeah, sorry, go on.</v>

00:24:42.131 --> 00:25:02.971
<v Chayan  Roy>No, all good. I just wanna, you know, because I'm under a little bit pressure because I have to release the, like, deliver the sign up, sign in, whatever flows. But after that, I'm gonna be, I'm super happy to also show you the prototype or maybe work with the Tavas team somehow, if you see a value in that.</v>

00:24:51.931 --> 00:24:52.411
<v Rob Zinkov>Yeah, yeah.</v>

00:24:59.131 --> 00:24:59.691
<v Rob Zinkov>Yeah.</v>

00:25:03.291 --> 00:25:04.811
<v Rob Zinkov>Yeah, so, yeah.</v>

00:25:06.571 --> 00:25:25.771
<v Rob Zinkov>I know what this week's about. That can be for next week. The challenge is when I looked at the costing, Tavis is 3x the price. And like, that's very hard to like, it's very hard to make the unity economics work with that, even though I think we both agree that Tavis is the better solution.</v>

00:25:14.411 --> 00:25:14.811
<v Chayan  Roy>Okay.</v>

00:25:18.491 --> 00:25:19.131
<v Chayan  Roy>Sure.</v>

00:25:21.291 --> 00:25:21.931
<v Chayan  Roy>Absolutely.</v>

00:25:26.331 --> 00:25:26.731
<v Chayan  Roy>Okay.</v>

00:25:27.051 --> 00:25:44.731
<v Rob Zinkov>I think there are ways to improve the Berlitz solution. So one of the things I've noticed is we can hook it up to Live Kit. And Live Kit would let us sort of better detect when to pause, when the mood is, and sort of feed some of the information.</v>

00:25:45.091 --> 00:25:45.611
<v Chayan  Roy>Mhm.</v>

00:25:46.491 --> 00:25:52.251
<v Rob Zinkov>So, and of course we can also make custom avatars that are maybe less stiff.</v>

00:25:51.851 --> 00:26:11.011
<v Chayan  Roy>Less candy, less stiff. That's a good word. Yeah, absolutely. Tavos is super expensive, but yeah, I just wanted to bring that up because the conversation was supernatural, right? It's just unbelievable what they're doing with Raven and Sparrow. Again, I'm not an AI or ML engineer.</v>

00:25:54.731 --> 00:25:55.211
<v Rob Zinkov>Yeah.</v>

00:25:56.411 --> 00:25:57.131
<v Rob Zinkov>Um...</v>

00:26:04.851 --> 00:26:05.211
<v Rob Zinkov>Yeah.</v>

00:26:11.131 --> 00:26:28.211
<v Chayan  Roy>I have worked with some TT. I have a local model running on my phone, Quin 3.6, with some TTS and STT on this Run Anywhere app. I'm like prototyping some stuff, but we'll have to see how far we can go with.</v>

00:26:17.531 --> 00:26:18.091
<v Rob Zinkov>Yeah.</v>

00:26:19.211 --> 00:26:20.091
<v Rob Zinkov>Yeah, likewise.</v>

00:26:25.571 --> 00:26:26.011
<v Rob Zinkov>Yeah.</v>

00:26:27.611 --> 00:26:31.611
<v Rob Zinkov>Yeah, I think for TTS and SST.</v>

00:26:31.851 --> 00:26:32.331
<v Chayan  Roy>Mhm.</v>

00:26:32.451 --> 00:26:52.171
<v Rob Zinkov>Sorry, STT. I think things can work on device very well. You know, some things like Parakeet and Quen both work beautifully on devices. There's a question of like older devices, how well they work, but I feel like even phones that are four or five years old have an onboard GPU. So I think we have.</v>

00:26:33.811 --> 00:26:34.811
<v Chayan  Roy>Yesterday, yeah.</v>

00:26:38.531 --> 00:26:38.971
<v Chayan  Roy>Uh-huh.</v>

00:26:52.971 --> 00:26:56.251
<v Rob Zinkov>Something there, but this the video, sorry, go on.</v>

00:26:54.091 --> 00:26:57.531
<v Chayan  Roy>What are you? Go ahead. No, no, go ahead, go ahead.</v>

00:26:57.611 --> 00:27:11.451
<v Rob Zinkov>Yeah, but I think for video, it's a little tricky. My impression is that this is not a static space. Like people are things are constantly moving here. So.</v>

00:27:01.531 --> 00:27:01.891
<v Chayan  Roy>No.</v>

00:27:09.931 --> 00:27:10.491
<v Chayan  Roy>Mhm.</v>

00:27:12.811 --> 00:27:31.691
<v Rob Zinkov>It might be one of those things where we wait a little bit and now Live Avatar has the feature we want. I don't think we want, we're architecting anything in a way where like we're going to be stuck with these things. It's more that we have, I think, like 270,000 credits with Live Avatar.</v>

00:27:14.971 --> 00:27:15.531
<v Chayan  Roy>Sure.</v>

00:27:16.811 --> 00:27:17.291
<v Chayan  Roy>Sure.</v>

00:27:23.451 --> 00:27:24.051
<v Chayan  Roy>Mm-hmm.</v>

00:27:25.131 --> 00:27:27.451
<v Chayan  Roy>Yeah, yeah, yeah, we can change.</v>

00:27:32.091 --> 00:27:32.971
<v Chayan  Roy>So, so, so.</v>

00:27:35.451 --> 00:27:48.651
<v Rob Zinkov>And like we might as well use them and just see how far we've taken. If it turns out that like people still hate the product even after we sort of massage it, you know, we might figure, we'll have to figure out the unit economics there.</v>

00:27:48.331 --> 00:27:58.731
<v Chayan  Roy>Absolutely. I mean, some of those discussions going on in the channel, right, about the costs and stuff. I was shocked to see 173 million or annual AI usage that was like really, yeah.</v>

00:27:59.531 --> 00:28:16.331
<v Rob Zinkov>Well, like, you're talking, remember, we're talking about a million users using the AI. And I don't know, is it that hard to imagine like a million users racking up per month per year, that much cost?</v>

00:28:19.211 --> 00:28:26.091
<v Chayan  Roy>Interesting. I had a chat with someone from Duolingo because I know a designer from Duolingo.</v>

00:28:25.611 --> 00:28:26.171
<v Rob Zinkov>Yeah, yeah.</v>

00:28:27.291 --> 00:28:38.731
<v Chayan  Roy>Yesterday, I'm going to be bringing him just to do like a, what Srikant mentioned, like a brownback session. I don't know where the name is coming from, but just.</v>

00:28:29.211 --> 00:28:29.691
<v Rob Zinkov>Mhm.</v>

00:28:37.451 --> 00:28:40.251
<v Rob Zinkov>Oh, oh, that's awesome. When's that happening?</v>

00:28:40.971 --> 00:28:56.971
<v Chayan  Roy>Yeah, I'm just gonna, because you know what he told me, Duolingo has 60 million daily active users. He works in the subscription and the conversion team. He's right now in US and 10% conversion, 1.2 billion revenue.</v>

00:28:47.491 --> 00:28:47.971
<v Rob Zinkov>Mhm.</v>

00:28:50.651 --> 00:28:51.131
<v Rob Zinkov>Yeah.</v>

00:28:58.331 --> 00:29:17.491
<v Chayan  Roy>Almost 0 human instructor spend, expense. I don't know if there's spending on AI. It's just insane how much money they are making. So yeah, I'm just talking to him for his availability and as soon as he's like, there's a slot.</v>

00:29:17.611 --> 00:29:26.411
<v Chayan  Roy>I'm going to bring him in and we can ask some questions. Of course, he's working in Duolingo, so it's a bit sensitive on how much you can share. But yeah, we'll see.</v>

00:29:26.371 --> 00:29:46.091
<v Rob Zinkov>Yeah, I mean, I'm not sure, like, I don't know how much we need like, like trade secret stuff, but like this question of like, how do you control, how do we control AI spend, I think is relevant. And again, the answer might just be, this is so expensive, we have to in-house. And if that's what we do, that's what we do.</v>

00:29:46.411 --> 00:29:48.091
<v Rob Zinkov>And there are open source, yeah.</v>

00:29:47.051 --> 00:30:07.051
<v Chayan  Roy>Yeah, exactly. I've been just talking to him and trying to understand their learnings, right? And each lesson that they have is 2 to 5 minutes. And they're, from what I understood, they're going even for a lower time, like a lower...</v>

00:29:57.691 --> 00:29:58.171
<v Rob Zinkov>Right.</v>

00:30:07.291 --> 00:30:08.651
<v Rob Zinkov>Yeah, yeah, dude.</v>

00:30:07.371 --> 00:30:20.811
<v Chayan  Roy>Because people's attention span is just, you know, like people are just scrolling, doom scrolling, TikTok, and they want to introduce something like reels even, like quick, like you just scroll 5 reels, maybe you pick up a couple of words or something.</v>

00:30:10.571 --> 00:30:11.051
<v Rob Zinkov>Right.</v>

00:30:21.451 --> 00:30:24.811
<v Rob Zinkov>Right, right, just, yeah, sec spending seconds in the app.</v>

00:30:26.331 --> 00:30:43.211
<v Chayan  Roy>That's the way it is. And some of my challenges, as soon as I joined my interactions with the Alex team, was like, hey, look, it's great what we have there in the web LMS, but all of that content and the learning flow doesn't really port one is to one to the app. And some of the.</v>

00:30:42.811 --> 00:30:43.371
<v Rob Zinkov>Right.</v>

00:30:43.451 --> 00:31:01.211
<v Chayan  Roy>some of the LMS templates that I showed you, it's still nice to have some microlearning. And I think my biggest concern would be how do we put all that content? Jan had some good ideas that he said he might have an AI pipeline for the LX content. So we'll have to see. But yeah.</v>

00:30:59.451 --> 00:30:59.931
<v Rob Zinkov>Right.</v>

00:31:03.051 --> 00:31:04.011
<v Chayan  Roy>That's that, man.</v>

00:31:03.171 --> 00:31:09.451
<v Rob Zinkov>Yeah, I, yeah, that, yeah, getting some insights from your friend at Duolingo, I think, would be amazing.</v>

00:31:11.931 --> 00:31:28.491
<v Rob Zinkov>And yeah, I am also exploring like what it would take to sort of like in-house some of this stuff, but I also feel like we're in an environment where we need to have like deliverables in like one month, two month. So like I also understand that like in that environment, like.</v>

00:31:25.451 --> 00:31:26.171
<v Chayan  Roy>Exactly.</v>

00:31:29.691 --> 00:31:37.611
<v Rob Zinkov>Maybe it's okay that we're spending a little bit on APIs if we have a product that looks good. Because if people are sort of convinced that it looks good, then...</v>

00:31:38.571 --> 00:31:45.851
<v Rob Zinkov>That buys time to spend on engineering versus like being hired and having kind of nothing really to show for a few months.</v>

00:31:46.091 --> 00:31:50.251
<v Chayan  Roy>Exactly, yeah, I mean, Duolingo is just, I mean, they have, it's a big company, I mean, they...</v>

00:31:53.851 --> 00:31:54.251
<v Rob Zinkov>Yeah.</v>

00:32:01.291 --> 00:32:05.211
<v Rob Zinkov>Oh no, I think you froze from me. ****.</v>

00:32:12.891 --> 00:32:13.611
<v Chayan  Roy>Hey there.</v>

00:32:14.051 --> 00:32:22.091
<v Rob Zinkov>I'm so sorry, you froze for a second for me. Yeah, yeah, you're the last I heard is, yeah, Duolingo is a big company and they have a lot of people they can...</v>

00:32:15.291 --> 00:32:15.851
<v Chayan  Roy>All good.</v>

00:32:22.811 --> 00:32:26.091
<v Chayan  Roy>Do you know the revenue of Berlitz is how much per year?</v>

00:32:26.091 --> 00:32:32.331
<v Rob Zinkov>I have no clue. That's something that probably Sergey or Srikant might have better access to.</v>

00:32:28.091 --> 00:32:28.571
<v Chayan  Roy>Okay.</v>

00:32:32.811 --> 00:32:33.851
<v Chayan  Roy>Okay, okay, cool.</v>

00:32:34.931 --> 00:32:51.131
<v Chayan  Roy>Okay, yeah, this is where we stand, I guess, and I guess we will be having some of these discussions for the AI avatar and totally makes sense to kind of maybe in-house this and, you know, like you mentioned, swap models in and out, depending on what models keep coming.</v>

00:32:35.771 --> 00:32:36.091
<v Rob Zinkov>Yeah.</v>

00:32:50.811 --> 00:33:12.051
<v Rob Zinkov>Right, right. Well, not just stop models in and out, but also like API providers. Like, you know, if tomorrow like Tavis shows up and they're like, oh yeah, we're like 1.5x the price, or you know, some other person shows up and like, oh, we're like live avatar, but like we actually like use a video feed to like know.</v>

00:32:57.611 --> 00:32:58.011
<v Chayan  Roy>Yeah.</v>

00:33:12.931 --> 00:33:14.411
<v Rob Zinkov>like what your mood is.</v>

00:33:15.771 --> 00:33:18.571
<v Rob Zinkov>You know, 0 hesitation to switch.</v>

00:33:17.131 --> 00:33:17.531
<v Chayan  Roy>Jared.</v>

00:33:18.971 --> 00:33:33.371
<v Chayan  Roy>Sure. One thing I was curious, Rob, I saw some chats in the mobile app group where people mentioned that we would be having this running locally on users' phone. You think that's realistic?</v>

00:33:34.811 --> 00:33:41.051
<v Rob Zinkov>I don't think having it all running locally is realistic, but it might be a way.</v>

00:33:39.531 --> 00:33:40.011
<v Chayan  Roy>Red.</v>

00:33:43.531 --> 00:34:02.811
<v Rob Zinkov>I think having the text to speech and speech, if speech to text and text to speech can be together run locally, and this pattern we have where most of our traffic is coming from people not using the video avatar, we might be able to radically reduce our spend by having even just.</v>

00:33:51.451 --> 00:33:51.771
<v Chayan  Roy>Yeah.</v>

00:34:02.971 --> 00:34:04.491
<v Rob Zinkov>Those run on device.</v>

00:34:05.691 --> 00:34:14.011
<v Chayan  Roy>Because most of the phones, for example, do you see, do you see this? Uh, it's blurred. Do you see that, right?</v>

00:34:14.731 --> 00:34:15.611
<v Rob Zinkov>Yes.</v>

00:34:16.011 --> 00:34:19.051
<v Chayan  Roy>So, I, um, so I can...</v>

00:34:18.811 --> 00:34:20.891
<v Rob Zinkov>That's the Run Anywhere app, right?</v>

00:34:20.731 --> 00:34:44.171
<v Chayan  Roy>Does it run anywhere app? On in run anywhere app, it actually gives me an option to select the platform TTS, which means I'm basically using the phones, my phone's built-in TTS and STT, right? So I'm assuming that most of the Android, like newer Android and iOS phones would already have this platform TTS and STT, so my...</v>

00:34:28.891 --> 00:34:29.371
<v Rob Zinkov>Yeah.</v>

00:34:34.091 --> 00:34:34.811
<v Rob Zinkov>Right.</v>

00:34:41.291 --> 00:34:41.771
<v Rob Zinkov>Yeah.</v>

00:34:44.571 --> 00:34:48.011
<v Chayan  Roy>We might not even need a model for this, or what do you think?</v>

00:34:48.971 --> 00:35:08.971
<v Rob Zinkov>I think it's worth it. My experience has been that like the multilingual performance of some of these built-in things can be so-so. So I think we want to be able to have the option to like put in something better. Because at a previous company I was at, they had their own model and then they switched to the built-in one of the phone.</v>

00:34:56.891 --> 00:34:57.411
<v Chayan  Roy>Okay.</v>

00:35:02.611 --> 00:35:03.091
<v Chayan  Roy>Mhm.</v>

00:35:09.291 --> 00:35:09.891
<v Chayan  Roy>Mhm.</v>

00:35:09.331 --> 00:35:22.091
<v Rob Zinkov>And it turns out many phones, especially older phones, have awful built-in TTS models. And suddenly, the quality people experience of the app is now heavily tied to.</v>

00:35:15.131 --> 00:35:15.531
<v Chayan  Roy>Okay.</v>

00:35:22.491 --> 00:35:24.011
<v Chayan  Roy>Tied to the device hardware.</v>

00:35:24.251 --> 00:35:24.891
<v Rob Zinkov>Right.</v>

00:35:26.011 --> 00:35:45.291
<v Chayan  Roy>That's a fair point, yeah, but I think the main model, like the stuff that stays in between TTS, right, the LLM, I mean, that cannot be in the phone because it's like, what's the size of it? And also the hardware and the performance, it's just a no-brainer to have it outside the phone, right? Streaming cloud.</v>

00:35:46.091 --> 00:35:58.091
<v Rob Zinkov>Right, right. Well, I don't know. Some of the Gemma models I think can fit on newer phones. You know, like the Gemma 4 billion model, particularly with the multi-token predictions, run amazingly on phones.</v>

00:35:51.051 --> 00:35:51.531
<v Chayan  Roy>Okay.</v>

00:35:56.291 --> 00:35:56.771
<v Chayan  Roy>Mhm.</v>

00:35:58.331 --> 00:35:58.811
<v Chayan  Roy>Mhm.</v>

00:36:00.411 --> 00:36:01.011
<v Chayan  Roy>Poll.</v>

00:36:01.291 --> 00:36:05.931
<v Rob Zinkov>Particularly like if it's a phone that's come out like the last, you know, two, three years.</v>

00:36:04.891 --> 00:36:07.771
<v Chayan  Roy>How big is that in terms of GBs or MBs?</v>

00:36:08.971 --> 00:36:09.691
<v Rob Zinkov>Um...</v>

00:36:10.651 --> 00:36:21.051
<v Rob Zinkov>I want to say it's, so let me, let me just kind of, I'm just going to pull it up because I already kind of have the tab right here, so let's.</v>

00:36:17.851 --> 00:36:18.331
<v Chayan  Roy>Sure.</v>

00:36:22.731 --> 00:36:23.371
<v Rob Zinkov>Um...</v>

00:36:25.291 --> 00:36:27.691
<v Rob Zinkov>We're looking at a size of like...</v>

00:36:30.971 --> 00:36:36.411
<v Rob Zinkov>I want to say like 2 between 2 and 4 gigabytes.</v>

00:36:38.411 --> 00:36:41.291
<v Chayan  Roy>So someone using that would mean they have to...</v>

00:36:42.491 --> 00:36:46.811
<v Chayan  Roy>Download this stuff on your phone, right? 224 GB, yeah.</v>

00:36:46.411 --> 00:36:47.131
<v Rob Zinkov>Right.</v>

00:36:48.411 --> 00:36:59.531
<v Chayan  Roy>Yeah, and all the and the phones that, that, that, like, yeah, some of the phones that were mentioned there, yeah, we'll have to see how much space and everything, but cool.</v>

00:36:58.811 --> 00:36:59.451
<v Rob Zinkov>Yeah.</v>

00:37:01.931 --> 00:37:03.691
<v Rob Zinkov>And, mind you, like...</v>

00:37:05.131 --> 00:37:21.451
<v Rob Zinkov>You know, maybe this is a thing we can be clever about where we can say like, hey, we're running this from cloud, but you know, you know, we'll give you like, I don't know, a 50, we'll give you a discount if you run it on your device, please.</v>

00:37:21.691 --> 00:37:38.811
<v Chayan  Roy>I mean, running on your device also will have the same problem that you just mentioned, right? Depending on the device, the performance, the delay. And I was running when, I don't know how much, on an iPhone 17, iPhone 16 Pro Max.</v>

00:37:29.771 --> 00:37:30.331
<v Rob Zinkov>Yeah.</v>

00:37:37.611 --> 00:37:44.091
<v Rob Zinkov>So this is like almost, this is like almost the latest iPhone pot. So one of the best phones, okay.</v>

00:37:41.611 --> 00:37:42.011
<v Chayan  Roy>Yeah.</v>

00:37:44.811 --> 00:37:49.131
<v Chayan  Roy>And my iPhone was heating up and the battery was just draining, you know.</v>

00:37:49.611 --> 00:37:50.091
<v Rob Zinkov>Right.</v>

00:37:50.491 --> 00:37:55.371
<v Chayan  Roy>So, it's just like, what, 15 minutes? The battery just went...</v>

00:37:54.651 --> 00:38:10.251
<v Rob Zinkov>Yeah. Now, again, I think we could also maybe do cloud if we use an older model. If we were sort of less powerful model, we might even be able to get away with like some of the cheaper GPU cloud hosting offerings.</v>

00:38:10.891 --> 00:38:11.371
<v Chayan  Roy>Mhm.</v>

00:38:11.531 --> 00:38:18.011
<v Rob Zinkov>Um, you know, I've seen stuff as like cheap as, you know, 60 a day or something like that.</v>

00:38:18.731 --> 00:38:20.971
<v Chayan  Roy>I was using this one.</v>

00:38:22.131 --> 00:38:24.491
<v Chayan  Roy>When 3.6.</v>

00:38:26.491 --> 00:38:45.051
<v Chayan  Roy>Yeah, and then I also use the quen 3, 4 billion parameters. Yeah, it's just, I don't know, running on phone, there was such a delay issue. Yeah, not really sure about that. But anyways, I guess that's not my expertise and you are more qualified and have more experience in that department.</v>

00:38:38.811 --> 00:38:39.371
<v Rob Zinkov>Okay.</v>

00:38:43.851 --> 00:38:45.451
<v Rob Zinkov>Yeah, I mean like...</v>

00:38:46.331 --> 00:38:47.091
<v Rob Zinkov>It's...</v>

00:38:48.491 --> 00:38:52.651
<v Rob Zinkov>I think those latency trade-offs are very real and</v>

00:38:54.971 --> 00:39:15.931
<v Rob Zinkov>It is, I think it's going to be one of those things where like we kind of have to play by ear. I still think that what we choose to do here should be a function of like what user hardware the person has. Like if we know that they have good hardware and they there and we know that the built-in TTS is and SCT are to our standards.</v>

00:39:16.091 --> 00:39:16.571
<v Chayan  Roy>Mhm.</v>

00:39:16.211 --> 00:39:24.491
<v Rob Zinkov>We can say, yeah, if you're on an iPhone 17 Max, if you're on a Pixel 10, if you're on a Samsung S24.</v>

00:39:24.731 --> 00:39:25.131
<v Chayan  Roy>No.</v>

00:39:25.651 --> 00:39:28.491
<v Rob Zinkov>We're gonna let you do that, otherwise you're gonna hit our...</v>

00:39:29.771 --> 00:39:30.971
<v Rob Zinkov>or cloud service.</v>

00:39:29.851 --> 00:39:36.011
<v Chayan  Roy>Or streaming, yeah, yeah, streaming, and yeah, makes sense. Cool.</v>

00:39:36.651 --> 00:39:55.291
<v Rob Zinkov>Yeah. All right, yeah, no, this has been lovely. And yeah, I'm sure we'll be chatting over the coming weeks. And again, like Daniel, well, maybe more so than Daniel, because I actually regularly spend time. I mostly stay in Berlin, but I am physically in Berlin fairly often.</v>

00:39:55.691 --> 00:40:13.451
<v Chayan  Roy>Okay, cool. Yeah, just, I would be, it would be super nice to meet you because Jan mentioned that he was meeting you on one of these Fridays and wedding and he was like, would you want to come? And I'm just like swamped with some deliverables here and there. So let's meet whenever we find some time.</v>

00:40:14.571 --> 00:40:30.651
<v Rob Zinkov>Well, meet when it makes sense. There's like, let's not pre-commit to anything. It's all makes sense. Yeah, there's a co-working space I work in at a wedding. My understanding though is that like you're closer to where Daniel is, like by like Noycon.</v>

00:40:20.171 --> 00:40:20.771
<v Chayan  Roy>Exactly.</v>

00:40:31.131 --> 00:40:34.011
<v Chayan  Roy>No, near Fredericksen and Lichtenberg, yeah.</v>

00:40:34.291 --> 00:40:35.691
<v Rob Zinkov>Coalition, yeah, yeah, so.</v>

00:40:36.811 --> 00:40:38.491
<v Chayan  Roy>Yeah, we'll figure it out.</v>

00:40:36.891 --> 00:40:50.411
<v Rob Zinkov>But let's, we don't, let's not commit to anything now, like, as we start, as like AI features have to be exposed in the mobile app, that's when we'll chat more about stuff.</v>

00:40:41.931 --> 00:40:42.491
<v Chayan  Roy>Sure.</v>

00:40:50.251 --> 00:40:50.891
<v Chayan  Roy>Exactly.</v>

00:40:51.371 --> 00:40:52.491
<v Rob Zinkov>Alright, take care.</v>

00:40:52.851 --> 00:40:53.691
<v Chayan  Roy>You too, bye.</v>

00:40:54.051 --> 00:40:54.411
<v Rob Zinkov>But.</v>

