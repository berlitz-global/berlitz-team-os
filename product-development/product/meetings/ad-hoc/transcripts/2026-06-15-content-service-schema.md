# Content Service /lesson/{id} endpoint

**Date:** 2026-06-15
**Start:** 2026-06-15T10:30:00.000Z
**End:** 2026-06-15T11:30:00.000Z

---

WEBVTT

00:00:03.112 --> 00:00:04.352
<v Rob Zinkov>Figure out what's...</v>

00:00:06.592 --> 00:00:14.352
<v Rob Zinkov>how to be storing lessons. Because there are these very like interact, there are these very...</v>

00:00:15.872 --> 00:00:24.592
<v Rob Zinkov>interactive things where people can have quizzes and videos and audio and they could be arranged a certain way and um...</v>

00:00:27.032 --> 00:00:38.752
<v Rob Zinkov>And you know, at some point, I expect the combination of people and AI to be authoring them and generating them, so I was sort of trying to figure out, like, what's a sensible schema?</v>

00:00:28.032 --> 00:00:28.192
<v Daniel Peter>Ms.</v>

00:00:40.672 --> 00:00:42.352
<v Rob Zinkov>For storing them.</v>

00:00:46.712 --> 00:00:50.192
<v Daniel Peter>OK, did you look at the designs that Cheyenne made?</v>

00:00:51.392 --> 00:00:52.112
<v Rob Zinkov>Yes.</v>

00:00:52.592 --> 00:00:53.792
<v Daniel Peter>OK, so.</v>

00:00:55.072 --> 00:00:55.392
<v Daniel Peter>Um...</v>

00:00:57.072 --> 00:01:21.472
<v Daniel Peter>There are some assumptions that we need to take as part of this design process, or I even have open questions in this design process. So we have a kind of static set of lessons right now. So someone sits down and defines a lesson, and then this lesson is served to the customer</v>

00:01:02.632 --> 00:01:03.112
<v Rob Zinkov>Mhm.</v>

00:01:21.632 --> 00:01:22.512
<v Daniel Peter>The Berlitz Potel.</v>

00:01:23.952 --> 00:01:42.992
<v Daniel Peter>And then this is a fixed set of possible exercises that can be shown to the user that follows certain patterns, like matching pairs for filling the blank and so on. So we have a fixed set of types</v>

00:01:41.152 --> 00:01:41.472
<v Rob Zinkov>Right.</v>

00:01:43.112 --> 00:01:46.432
<v Daniel Peter>of exercises that we serve as part of a lesson.</v>

00:01:48.592 --> 00:01:49.152
<v Rob Zinkov>Right.</v>

00:01:49.792 --> 00:01:56.512
<v Daniel Peter>So are we talking about these kind of exercises or are you thinking about like tutoring lessons?</v>

00:01:57.552 --> 00:02:11.312
<v Rob Zinkov>I'm thinking of both, but truthfully, it's the first kind that's harder for me. Because for the tutoring one, we're mostly just collecting prompts. So it's like, it's actually, schema-wise, it's actually not so bad.</v>

00:02:02.432 --> 00:02:02.912
<v Daniel Peter>Okay.</v>

00:02:11.952 --> 00:02:12.432
<v Daniel Peter>Okay.</v>

00:02:14.632 --> 00:02:18.592
<v Daniel Peter>That's funny, I would have expected the opposite, that for the tutoring it's harder.</v>

00:02:20.752 --> 00:02:24.512
<v Rob Zinkov>Well, because a lot of what you're going to do is you're going to make a prompt.</v>

00:02:25.632 --> 00:02:46.672
<v Rob Zinkov>And there may be some actions you kind of want to happen during it that are sort of triggered based on certain words or expressions said, but they're kind of both text. So they're like, it's pretty easy to like, you know, a lesson with a certain lesson will have certain problems associated with it.</v>

00:02:47.152 --> 00:02:53.872
<v Rob Zinkov>that might be in a certain order. And so because it's all kind of text, it's actually not so bad.</v>

00:02:57.152 --> 00:02:57.632
<v Daniel Peter>Okay.</v>

00:02:58.432 --> 00:03:06.512
<v Rob Zinkov>versus there's all these different lesson types and you can imagine more lesson types being made. But even if we sort of assume the ones we have for now are fixed.</v>

00:02:58.592 --> 00:03:02.032
<v Daniel Peter>But that's nice to know. I would have expected it to be hard.</v>

00:03:09.152 --> 00:03:09.472
<v Daniel Peter>Yeah.</v>

00:03:10.352 --> 00:03:15.872
<v Daniel Peter>I'm going to turn off my video because my connection seems to be a bit unstable. Don't worry about it.</v>

00:03:15.352 --> 00:03:19.472
<v Rob Zinkov>That's fine. Do you want me to turn off mine? It's up to you.</v>

00:03:20.752 --> 00:03:27.952
<v Daniel Peter>No, it's OK. I think it's mainly the upstream, not the downstream. OK, so...</v>

00:03:21.792 --> 00:03:22.272
<v Rob Zinkov>Okay.</v>

00:03:29.232 --> 00:03:40.272
<v Daniel Peter>Then, so let's write down some questions. So first of all, the first question is what are the types of exercises that we serve as a lesson, right?</v>

00:03:40.992 --> 00:03:41.392
<v Rob Zinkov>Right.</v>

00:03:43.152 --> 00:03:58.352
<v Daniel Peter>And this is going to, this is going to influence the shape of the data object that we send as part of the API request. The second question is, are lessons static, statically defined?</v>

00:03:50.992 --> 00:03:51.392
<v Rob Zinkov>Right.</v>

00:03:59.952 --> 00:04:18.472
<v Daniel Peter>Or dynamic. So do we like when for each user, do we have a set of, do we have a set of exercises that we match to a lesson? Like if they are on level 5.2, do we give them a</v>

00:04:20.112 --> 00:04:35.392
<v Daniel Peter>Do we give them a lesson that is composed of exercises of proficiency level 5.2? Or do we give them like a fixed set, which is like lesson one in unit one is going to be this?</v>

00:04:37.632 --> 00:04:53.472
<v Rob Zinkov>My understanding is that for now, the lessons are fairly static, but we'd like to move to a system where we're automatically generating lessons within a particular set of parameters. But once the lesson is generated,</v>

00:04:37.872 --> 00:04:38.672
<v Daniel Peter>Does that make sense?</v>

00:04:52.232 --> 00:04:52.512
<v Daniel Peter>Okay.</v>

00:04:56.912 --> 00:05:04.112
<v Rob Zinkov>It's just generated. So like if they stop and come back to it, it would still be, it would persist.</v>

00:05:05.792 --> 00:05:14.432
<v Daniel Peter>Okay, and then what is the shape, quote unquote, shape of a lesson, right?</v>

00:05:15.472 --> 00:05:15.792
<v Rob Zinkov>Right.</v>

00:05:15.792 --> 00:05:21.872
<v Daniel Peter>That's uh, that's the that's another question for me, like, what does the data object look like? Um...</v>

00:05:21.432 --> 00:05:21.912
<v Rob Zinkov>Mhm.</v>

00:05:23.632 --> 00:05:33.792
<v Daniel Peter>And then endpoint route, like how do we query? Are lessons defined?</v>

00:05:34.992 --> 00:05:37.712
<v Daniel Peter>per user or per course.</v>

00:05:40.432 --> 00:05:41.152
<v Rob Zinkov>Right.</v>

00:05:41.952 --> 00:05:47.272
<v Daniel Peter>And because a user needs to be, so like a user has a kind of learning path.</v>

00:05:47.752 --> 00:05:48.352
<v Rob Zinkov>Mm-hmm.</v>

00:05:49.752 --> 00:05:56.912
<v Daniel Peter>learning path and it needs to be able to complete certain lessons and how do we dynamically track the learning path.</v>

00:05:59.472 --> 00:06:15.632
<v Daniel Peter>Okay, so these are like, I just put them down in writing. So that we have, so that we have them as a kind of guideline. I think the first one is kind of simple, easy to answer. We can, it's for me, that's a big.</v>

00:06:03.312 --> 00:06:03.872
<v Rob Zinkov>Right.</v>

00:06:17.032 --> 00:06:37.352
<v Daniel Peter>data type, and there's like an enum with different cases of different shapes of lessons, like matching pairs is going to be one type of lesson, and then fill the blank is going to be one type of lesson, and each of them defines a kind of</v>

00:06:23.832 --> 00:06:24.312
<v Rob Zinkov>Mhm.</v>

00:06:37.472 --> 00:06:44.912
<v Daniel Peter>right or wrong answer that can be evaluated. So it has like an evaluation expression.</v>

00:06:47.032 --> 00:06:52.912
<v Daniel Peter>And that can, I think that that should inform.</v>

00:06:54.472 --> 00:07:08.672
<v Daniel Peter>Where B is so flexible, let's put it like that, so that we can define static lessons in this format, and we can also dynamically construct them in some way, or dynamically route them in some way, if that makes sense.</v>

00:07:09.552 --> 00:07:10.352
<v Rob Zinkov>Right.</v>

00:07:09.872 --> 00:07:12.832
<v Daniel Peter>The data type should not limit us. We shouldn't be like a...</v>

00:07:14.272 --> 00:07:33.392
<v Daniel Peter>Worst case, the worst thing that we could do is like have invent some kind of custom lesson data format that is serialized and deserialized and editable. I think it just should be should be very simple serializable JSON stuff that we read and write from a database. And then</v>

00:07:29.112 --> 00:07:29.592
<v Rob Zinkov>Mhm.</v>

00:07:32.992 --> 00:07:33.552
<v Rob Zinkov>Okay.</v>

00:07:34.432 --> 00:07:52.512
<v Daniel Peter>I think it would be really nice to have a sort of pool of exercises. It's just a big table that has like all the exercises in it with an assigned type and just assigned evaluation.</v>

00:07:40.432 --> 00:07:40.912
<v Rob Zinkov>Mhm.</v>

00:07:53.712 --> 00:07:57.312
<v Daniel Peter>Like, what is right, what is wrong for this type? Does that make sense?</v>

00:07:58.352 --> 00:07:59.232
<v Rob Zinkov>Yes.</v>

00:08:01.232 --> 00:08:07.312
<v Rob Zinkov>So, like, if we have a lesson that's order the this list of up or order this list.</v>

00:08:09.152 --> 00:08:16.592
<v Rob Zinkov>There is, it sort of includes the elements that should be in the list and what is the correct order of them.</v>

00:08:45.872 --> 00:08:58.432
<v Rob Zinkov>Oh, sure. Yeah, so for example, you might have a type of lesson which is order, you know, put this list in the correct order, and the elements of the list are stored along with the correct order.</v>

00:09:10.432 --> 00:09:12.672
<v Daniel Peter>Yes, so this is, yeah, this is how I see it as well.</v>

00:09:14.432 --> 00:09:21.632
<v Daniel Peter>So then, like a lesson, a lesson has a list of exercises and keeps track of the order of which exercise needs to be done.</v>

00:09:25.072 --> 00:09:29.712
<v Daniel Peter>And then a user, a user has like a learning path that references lessons, right?</v>

00:09:30.192 --> 00:09:30.832
<v Rob Zinkov>Right.</v>

00:09:48.152 --> 00:09:50.752
<v Daniel Peter>which has a list of lessons.</v>

00:09:56.672 --> 00:10:00.512
<v Daniel Peter>User lessons. Let's call them user lessons because they also have like state.</v>

00:10:04.432 --> 00:10:04.832
<v Rob Zinkov>Yes.</v>

00:10:05.792 --> 00:10:09.632
<v Rob Zinkov>Right. And the impression I'm getting from you is that...</v>

00:10:19.432 --> 00:10:27.952
<v Rob Zinkov>Where in terms of schema-wise, like, we'll track lesson types, but in terms of...</v>

00:10:29.392 --> 00:10:30.672
<v Daniel Peter>Yes, ideally.</v>

00:10:31.312 --> 00:10:32.352
<v Rob Zinkov>I think that's fine.</v>

00:10:31.872 --> 00:10:52.352
<v Daniel Peter>And the kind of, like, as I said, the kind of backend for front end approach, where the backend just says, "You should show UI of that shape," and then the front end shows the UI of that shape, and then I completed this. I successfully completed this with an error.</v>

00:10:52.832 --> 00:10:54.032
<v Daniel Peter>and so on.</v>

00:11:41.792 --> 00:11:45.072
<v Daniel Peter>Yeah, into modules. That's what I would call them.</v>

00:11:45.432 --> 00:11:52.352
<v Rob Zinkov>Because like again, like we're going to have things like cultural navigator where like we're not learning languages. There'll be another grouping.</v>

00:12:05.792 --> 00:12:11.552
<v Rob Zinkov>Yeah, and there will be lessons that, like, don't make sense in a module necessarily, but...</v>

00:12:22.592 --> 00:12:34.032
<v Rob Zinkov>For me, it's kind of, but I am broadly okay with this. There's a path, a path, yeah, there's a path kind of specific to different.</v>

00:12:37.632 --> 00:12:43.872
<v Daniel Peter>You, so you put lessons in order in a module on a path - that's what you said, right?</v>

00:12:49.152 --> 00:12:54.512
<v Daniel Peter>Yes, so a user has a list of learning paths because they can have multiple languages.</v>

00:12:56.912 --> 00:13:15.632
<v Daniel Peter>Each learning path consists of modules, which have some form of, yeah, some form of state. Actually, like their state is derived from their user lessons. And a user lesson consists of a list of exercises. And these exercises are typed.</v>

00:13:51.792 --> 00:13:52.272
<v Daniel Peter>Yes.</v>

00:14:06.832 --> 00:14:21.712
<v Rob Zinkov>Right. Yes. So it should be easy, I think, to add a, it should be relatively straightforward to add a new kind of exercise. Basically, we extend the enum and then we put a sort of a new.</v>

00:14:22.832 --> 00:14:31.552
<v Rob Zinkov>JSON form on the back end and then a new front end is made for it that knows how to handle those kind of lessons.</v>

00:19:52.152 --> 00:20:12.672
<v Rob Zinkov>Yeah. Yeah, so my gut, again, this is like, this is pure, this is much more of a, I think maybe more of a product opinion than that. My gut feel is that I love this good exercise, but I think what I think will end up like feeling better is if we just pull the entire lesson in one shot.</v>

00:20:12.912 --> 00:20:20.032
<v Rob Zinkov>because it's not that much content and also it gives you the advantage that someone could like do the lesson kind of offline a bit.</v>

00:20:21.632 --> 00:20:22.432
<v Daniel Peter>I am, too.</v>

00:20:43.392 --> 00:20:49.872
<v Rob Zinkov>Yeah, in fairness, what you're suggesting I think is the correct way to do this. Be a little more deliberate.</v>

00:22:16.752 --> 00:22:22.032
<v Rob Zinkov>Exactly. Oh, yeah, yeah, yeah, totally. Exactly. Okay.</v>

00:23:29.312 --> 00:23:34.112
<v Rob Zinkov>Is there anything else we need to talk about? Like, I know you booked a chunk of time, but like, you know, like...</v>

00:23:44.272 --> 00:23:50.432
<v Daniel Peter>I think we're aligned on the shape of the API and the data objects that we would have to send.</v>

00:24:02.272 --> 00:24:04.672
<v Rob Zinkov>Yeah, let's hand back that half hour.</v>

00:24:05.432 --> 00:24:07.232
<v Daniel Peter>Yes, okay. I'll have lunch.</v>

00:24:07.792 --> 00:24:10.672
<v Rob Zinkov>Alright, take it easy. Bye.</v>

00:24:08.992 --> 00:24:09.872
<v Daniel Peter>I'll see you later.</v>
