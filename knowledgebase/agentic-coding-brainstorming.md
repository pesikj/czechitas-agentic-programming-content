# Agentic Coding Brainstorming

Source: https://chatgpt.com/share/6ac63eba-fa6c-83ed-a88a-3921231acd3f

Exported: 2026-10-07

Transcript of the shared conversation, including voice-message transcriptions. Source links supplied with responses are retained.

---

## 1. User

I am preparing a course of agentic coding and I would like to brainstorm some topics together However, I'll give you some- some background, speak in English, please

---

## 2. ChatGPT

Jasně. Jasně, přepínám do angličtiny. Povídej, jsem jedno velké ucho.

---

## 3. User

Okay, so will you speak English

---

## 4. ChatGPT

Sure, English it is. Go ahead.

---

## 5. User

Okay, so the course is for people who has no required prior knowledge, so it's people who- probably don't have experience with coding and who don't have experience with... ...agentic coding tools, maybe... I would- I believe- or we require to have some... knowledge of AI, of general concept, so... They should be advanced user of tools like ChatGPT, but not necessarily of tools like Codex and Cloud Code and similar and stuff like... ...like Cursor and so on. Also, they don't have prior knowledge of Git... or prior knowledge of Visual Studio Code... and there will be eight lectures. So do you understand the... ...background or do you want to ask something

---

## 6. ChatGPT

That all makes sense. Just a couple quick things to calibrate. How long is each lecture and is the goal more to help them build something small by the end, or to give a broad survey of agentic ideas?

---

## 7. User

Well, each lecture has two point five or three hours. I'm not sure about this, there will be eight lectures as I said... and regarding the final... Yeah, maybe it would be better to build something... but not every lecture has to be focused on- on the project like... there may be multiple lecture that are... ...focused on something else, and... some lectures focused on building... a... ...project

---

## 8. ChatGPT

Perfect, thanks, that helps. Given that length, you can blend concept and hands-on without it feeling rushed. I'd start gentle with what agents are and how they differ from plain prompting. Then maybe a low-friction lab where they tweak a simple agent behavior in a safe, browser-based environment before touching local setup or Git. Does that feel right for your audience, or is that too tool-heavy too soon?

---

## 9. User

No, I think this is... okay... and... uh... I have some other ideas, so I will... tell them... So... there should be some... at least general explanation... of logic, Python will be used. And I would like to show... tools like... conditions... for ...loops- Exceptions... and functions... and it... doesn't have to be- Lecture about the coding... but um... they should... When the code is generated they should understand the basic things like... uh... they should see that it... generated functions. They- uh- or function. They should see... that... there is a condition there, so there- there will be a decision process in... the... ...application itself... and so on

---

## 10. ChatGPT

Right, got it. So you want them to read and reason about generated code without necessarily writing it from scratch, more like code literacy.

---

## 11. ChatGPT

In that case

---

## 12. User

Yeah, exactly. I think... Yeah, go on

---

## 13. ChatGPT

In that case, you can teach just enough Python structure as "reading comprehension", not composition. For conditions and loops, show tiny generated snippets and have them predict behavior in plain English. Then run it to confirm. Same with functions and exceptions: treat them as "named behaviors" and "error stories" so it feels conceptual but grounded. Want me to sketch a sample flow for one three-hour lecture?

---

## 14. User

No, no, I don't want to go... to such detail. I think... uh... we... should... just provide high level topic. So... uh... this... this should be... this should be... the... for- I think the program was- first lecture should be the Python introduction... and also it should include some... basic introduction about how to start Cloud Code... or how to switch... um... or maybe not how to switch a model, but how to start Cloud Code, how to start Visual Studio Code... and perhaps it might be nice... to... see the debugger running because uh... when the debugger is... running

---

## 15. ChatGPT

Mm-hmm.

---

## 16. User

when the- debugger is running... ...we can uh... put there a breakpoint... and the breakpoint will show how... the breakpoint... it show... how... the- uh... how the python runs from... one... one point to... another... uh... and we can put a breakpoint... inside a function... so uh... they see that the core... that Python goes to the function and so on... Maybe this- and also the exception. Like to see that uh... when there is an exception it goes to the... uh... rescue block, let's say... and maybe... or... all this stuff shouldn't be on the... for- one lecture, but for two lectures. What do you think

---

## 17. ChatGPT

Hmm. Let me think through that pacing real quick.

---

## 18. ChatGPT

Hmm. Let me think through that pacing real quick. I'd split it across two. The first keeps it gentle: Python literacy basics plus environment. So, what Python looks like, variables, conditions, loops, very light functions, and starting Python from VS Code and what the terminal is. Also starting Claude code and having it generate simple code that they read. Second lecture, focus on understanding execution: functions in a bit more depth, parameters and returns, then exceptions and a debugger. Your debugger idea is strong. Use it not as a debugging tool but as a visualization of program flow—step into a function, step out, see variables change, trigger an exception and follow it. And I would not teach Python like a mini programming course. No "write a for loop from scratch" tests. Instead, "Claude generated this loop—let's recognize what it's doing." That's a key distinction, more central to your whole course actually. If they can read and reason about generated code, they'll be safer and more effective later. I'd also introduce the Claude code in lecture 1, otherwise it might feel like a traditional coding course.

---

## 19. User

Mm Mm-hmm

---

## 20. ChatGPT

Does that high-level split work?

---

## 21. User

Yeah, it works for me

---

## 22. ChatGPT

Great. Then use lecture one for literacy plus environment, with immediate "read generated code" tasks, and lecture two for execution flow via debugger and exceptions. That builds the mental model they'll need before the agentic parts.

---

## 23. User

Okay, then... I think... the other... lecture should be focus on Git... because... I believe the Git is... uh... important... when- do you... do the Agentic coding... to... manage the changes. So I would like to show them... how GitHub works... how to... uh... create a repository... how to upload... or push the code to... GitHub... how to see... uh... the changes there... and how to use... uh... basically how to use git as a quality... quality tool... uh... and... this also... give... a possibility... to... roll back some unwanted changes... or it... can be connected with some... other tools like Vercel... when the software is... deployed... to production

---

## 24. ChatGPT

Let me map that sequence carefully.

---

## 25. ChatGPT

Yeah, I'd make that your third lecture. Git is important and it deserves its own slot, but I'd pitch it primarily as change control and safety for agentic coding: "the agent can change a lot, so here's how you stay in control." High-level pieces: what Git and GitHub are, repo and commit, branching basics, diff reading, and a simple revert. The habit you're building is "commit before big agent change, inspect the diff, then accept or roll back." That workflow will carry through the remaining five lectures.

---

## 26. User

Mm

---

## 27. ChatGPT

Then after Git, you can move into the actual agentic development flow. I might avoid deep Git minutiae for now and stick to "I can always get back to a working version."

---

## 28. User

Okay, uh... I made a mistake there will be ten lecture... uh... ten lectures not eight, sorry for this

---

## 29. ChatGPT

Ah, got it. Ten lectures gives you more room. That's a nice correction. With ten, you can keep Git focused and gentle and still have plenty of runway for agent workflows and deployment later. Do you want me to suggest how to spread the remaining seven at a high level, or leave that for later?

---

## 30. User

No

---

## 31. ChatGPT

Got it.

---

## 32. User

I still have some ideas

---

## 33. ChatGPT

Go on.

---

## 34. User

So... the next, I believe, should be the first... real agentic coding lecture... So, I would like to explain how to start... the agentic... coding tool... how to run a prompt, how to wait for the result... how to... manage the user right of the agentic tool... ...how to... switch model... how to see... how much uh... tokens are remaining... how to see what is... model actually... what the- model actually does... but I would like to start this... uh... with... some... basic... introduction... to uh... command prompt... or to shell... because... Agentic coding... uh... means... running... that... mean- that uh... Agentic uh... code... or Agentic tool... runs a lot of... shell commands. So for example, it run... grep tool... uh... to see the file... and I would like to... uh... give some... introduction... There will be a... small complication... that some of the... I guess majority... of the people... will use PowerShell and... the minority will probably use MacOS... or... Linux... but... uh... I believe... it should... be just handled by... uh... running the similar... commands uh... in PowerShell. By the way... how... does the Codex work... in Windows? Does it run... uh... Power Shell commands... or... does it run... Does it run... somehow... in some emulation uh... the- uh... normal shell commands

---

## 35. ChatGPT

Let me check.

---

## 36. ChatGPT

On Windows, Codex can run natively, directly using PowerShell or other Windows shells. It isn't emulating a Unix shell behind the scenes. If you choose to run it inside WSL, then it's just normal Linux. For an introductory course, I'd avoid requiring WSL; it's another layer. I actually like the shell idea for your fourth lecture—just keep it tight and purpose-driven. Not "learn shell", but "understand enough to read what the agent is doing": pwd/ Get-Location, ls/ Get-ChildItem, cd/ Set-Location, cat/ Get-Content, grep / Select-String, run a program. Then show the mapping side by side. Don't force memorization. The key concept is "the agent is operating my computer by running commands." That's a big conceptual win for agentic coding. Then the second part of that lecture can cover what you listed: starting Codex or Claude Code, sending a task, seeing its actions, permissions, model choice, and tokens. I'd lean on permissions as a safety concept. By the end, they've seen almost every element of the workflow.

Sources:

- [Building a safe, effective sandbox to enable Codex on Windows | OpenAI](https://openai.com/index/building-codex-windows-sandbox/?utm_source=chatgpt.com)
- [Using Codex with your ChatGPT plan | OpenAI Help Center](https://help.openai.com/en/articles/11369540?utm_source=chatgpt.com)
- [Introducing the Codex app | OpenAI](https://openai.com/index/introducing-the-codex-app/?utm_source=chatgpt.com)

---

## 37. User

Okay, it sounds good... so... this could be... lecture four... and... then... the next... lecture, lecture five... uh... it should explain the agentic coding flow... and in this case I'm not... really sure whether this is a content... for... entire... lecture... The agentic... coding flow... as it is... described, I believe, in Cloud... documentation... is explore... plan... code... uh... test... commit. So I would... start with the plan mode, which... I believe... is available... in... Codex... or... Cloud Code... and to... ask... uh... Agentic coding tool... to... write a plan for the implementation. Then... uh... to review the plan... discuss the plan... and... after... After accepting the plan to... continue with... uh... the... build... and I would like to... I would like to show it on... both... uh... writing a new code... and... updating the existing application. So I would like to... prepare some... uh... simple project... or maybe take some existing project... I'm not sure about this... and ask... uh... the participants of the course... to develop... uh... new... feature for existing tool... or... to do... something uh... with existing tool... So... uh... I think the first thing uh... the... that has to be included in this lecture as well... Also... is how to run... how to run the code locally... So... I'm not sure... whether... it would be better... to use... uh... whether it will be better to use... Django... or... some... JavaScript uh... JavaScript... framework... but maybe... Django... might be... better... because... uh... as a full stack... Django... is... uh... advantages... Django is in Python... so... it can be... uh...e- e- easy to link it with... the previous... stuff. It also shows how... the... how... the... front-end works and how the back-end works... so... it can include... showing both of... both of uh... let's say... the sides... of the project... and... another thing... is... that it can also... show how to... database... is created... it will use... SQLite database... and... it will show... how... the database... is run... The... small... disadvantages that probably... the uh... Django is more challenging... to deploy to production... and... uh... it... doesn't uh... or it isn't able... to... generate... very... uh... dynamic... web-page... like... like JavaScript... uh... but... I don't think... this should be... such a big disadvantage... So... what do you think

---

## 38. ChatGPT

Let me think this through.

---

## 39. ChatGPT

I think that is a solid lecture five and enough for a full session, if it's hands-on and not just talk. Treat the flow as the star: explore, plan, implement, test, review, commit. I would avoid making "plan mode" the concept— it's a moving UI detail. Frame it as "ask the agent to investigate and propose a plan, discuss it, then let it implement". That survives tool changes. For the project, I'd use an existing small app, not greenfield. That makes the explore phase real. Django is a good fit here precisely because it's all Python, which lowers cognitive load. You can show request to response, models to templates, and a real database with SQLite without extra infrastructure. Don't worry much about a fancy front end. The goal is workflow literacy, not UI polish. Running locally definitely belongs here, build that "code in a folder" versus "app running on a server" distinction. And deployment can wait for later. So, Django is my pick, shallow Django depth, heavy on agent flow and diff review. That also ties Git and Shell together naturally. Does that fit what you want students to take away?

---

## 40. User

Yeah, yeah, I believe this fits

---

## 41. ChatGPT

Great, sounds good. So, for lecture five, go with the agentic flow on a small existing Django app, emphasize plan before implement, run locally, inspect diff, and commit.

---

## 42. User

I think... uh... there is- there should be... one... another topic to be- to be covered... but probably... this topic will be... too complex... and... maybe this should be... this entire stuff should be... split into two lectures... But... uh... I think... are the tests... because the tests... are... uh... usually generated... automatically... when... uh... there is a change... in the software... like Django... and... uh... the people should understand... what the tests are... and why are they generated... and what is the difference... uh... between the- Unit test... and... integration test... ...and that... if there is a test in the code... it doesn't automatically mean... that the code is... right... but the test... are... specific... and if... AI... doesn't understand... doesn't... understand... the... task... it... uh... also... uh... write a test... that doesn't... fit the tasks... and uh... the... solution... even though the test pass... the solution... is... uh... incorrect... uh... Do you... what do you think

---

## 43. ChatGPT

Let me check.

---

## 44. ChatGPT

Yes, I'd split it. Keep lecture five focused on the flow with minimal testing. Then make lecture six "testing and validation in agentic coding". Anchor it on one sharp lesson: passing tests is not the same as correct behavior. Show a quick demo where the agent misinterprets the requirement, writes code and tests that agree with that misinterpretation, and everything is green but wrong. That plants the key idea that tests verify assumptions, not the original intent. Then give them a small practice: have them review both the code and the tests against the requirement. A quick primer on unit versus integration tests is helpful, but keep it pragmatic, focused on reading and questioning them. That way, it becomes "tests as feedback and skepticism", not "tests as stamp of truth". That kind of healthy questioning of what the agent produces. Just a bit of disillusionment. It fits nicely after the flow. And Then you can still have deployment later without rushing. Do you want that testing lecture to be more conceptual or have them actually run tests and see failures?

---

## 45. User

I would like to make them run the test and to see the failure as well. And maybe... also... to ask AI uh... why do test fail... and uh... to see AI how... it fix the test fixes the test, sorry

---

## 46. ChatGPT

Ah. No, yeah, that works really well, and it's a very "agentic moment". Let them run tests, hit a failure, ask the agent what happened, then watch it propose a fix. It's almost the full loop: observe, hypothesize, change, verify. But keep that healthy doubt. Even when the agent explains and fixes, ask students to sanity-check it. "Does this actually match our intent?" That tiny habit will save them later. And honestly, seeing failures is oddly empowering. It normalizes that tests failing is not a disaster, it's just information.

---

## 47. User

Okay, do you believe that these stuff... this stuff which we- just described... is enough for two lectures... or... should there be more

---

## 48. ChatGPT

Let me look at that.

---

## 49. ChatGPT

Yeah, I think that's enough for two full lectures. Lecture five is the workflow: explore, plan, implement, run locally, inspect diff, commit, maybe a light test run without much theory. Lecture six is testing and verification: unit versus integration, running tests, reading failures, having the agent explain and fix, and the big caveat: tests can pass and still be wrong. I wouldn't add more theory on top. If you want to enrich lecture6, just one extra concept helps a lot: was the test wrong or the code wrong? That's where people start thinking critically instead of deferring to the agent. And a quick exercise around a deliberately bad agent fix works really well. Like when it "fixes" the test instead of the bug. That drives the point home nicely. So I'd stop adding to those two. They're already plenty meaty. Ten lectures gives you room elsewhere rather than packing these.

---

## 50. User

Uh... so... how much lectures... uh... is remaining

---

## 51. ChatGPT

Let me just check that.

---

## 52. ChatGPT

So, four are left. You've sketched the first six, so seven to ten are still open. Those could cover, for example, deployment, monitoring and logging, Prompt and agent safety practices or a capstone project, but we can leave that for later.

---

## 53. User

Uh... maybe I would like... to show them... also a different technology. So... uh... they can see... uh... there are... technological... independence... So... Since we covered Django... We may... uh... try... to run... uh... some... uh... more complex... application setup... so

---

## 54. ChatGPT

Mm-hmm.

---

## 55. User

... maybe, uh... we can run... the code, uh... that... uh... uses Fast API as API... and some... JavaScript... uh... Frontend... uh... written in React, for example

---

## 56. ChatGPT

Hmm. Let me think about that mix.

---

## 57. ChatGPT

Hmm. Let me think about that mix. I think that's a strong idea for lecture seven. It's a clear way to show that agentic coding is not tied to one framework. React plus FastAPI is a nice contrast to monolithic Django, but I'd keep the focus on the agent navigating multiple stacks. Not on teaching React or FastAPI from scratch. Give them a working repo and have the agent implement a small cross-stack change, something like adding a new field that touches the API and the React UI. That becomes a very compelling demo of agentic coding: the agent tracing through unfamiliar tech while students evaluate at a high level. That fits nicely after the workflow and testing lectures, and subtly teaches the principle: you don't have to know all the tech to assess what the agent is doing, but you need the right mental model and checkpoints in place.

---

## 58. User

Uh... Okay, this sounds good... but maybe... if we want to be... really... agentic... The... initial goal... would be... just... here... is the... repository... and try to run it locally. So we can go... uh... With AI... ...to find out the best way... how to install the tools, how to install... Node.js... or... how to install... ...the other stuff because... Uh... like... using AI isn't about... ...development... But it... also... uh... by solving the- uh... supportive tasks. So... it can help... them... ...with... install... uh... Fast API... Or... and... Install... Node.js... and so on

---

## 59. ChatGPT

Let me think that through.

---

## 60. ChatGPT

Yeah, I think that actually makes it better. Making "get this unknown repo running locally" the task is super authentic agent usage. Not about writing code first, but about environment setup, dependency wrangling, reading the repo structure, and asking the agent to plan and explain. That's exactly how people use agents in the wild. The one thing is, you'll want to build in a safety habit. Don't just approve install commands blindly. Make the agent explain what it's about to install and why. That fits your earlier emphasis on control and understanding. I'd also let it vary by OS. Don't hide that difference. A Windows user sees PowerShell commands, Mac users see terminal commands. That highlights adaptability, which reinforces the agentic part better than a polished demo. So lecture seven could be about getting an unfamiliar project running with an agent, and only then doing the FastAPI React change once it's up. That feels very coherent.

---

## 61. User

Okay... uh... So... And the task... would be... Uh... Also like... adding a new... feature... or... Something... like... or... fixing a bug... or something... like this... and maybe... to see... ...that... in case... of... uh... the frontend and backend... uh... ...not... the unit test... are... maybe... not... enough... and another... ...approach for the tests... maybe... is- uh... ...better in this case

---

## 62. ChatGPT

Let me check that.

---

## 63. ChatGPT

Yeah, that's a great escalation. It's the perfect place to show that unit tests aren't the whole story. In a React plus FastAPI world, you can introduce end-to-end tests lightly to show a full user flow across front and back end. You don't have to teach Playwright or Cypress in depth. Just show that unit tests can all pass, while a simple end-to-end test catches a broken API contract. That lines up nicely with your earlier "tests aren't truth" message. And yes, a bug-fix task is perfect for that. Give them a deliberately broken integration and let the agent investigate, with students watching the investigation strategy and verification steps. That is a strong Lecture 7. Unfamiliar repo to running system to cross-stack change to end-to-end verification. It feels very, very agentic.

---

## 64. User

Okay Uh... So... There should be also one lecture about... deployment, that is... uh... because they should... be... able to deploy the code... I'm not sure whether it is better... to deploy... uh... Django application... or whether it is... better to deploy... Uh... the JavaScript... uh... or- ja- the... JavaScript... uh... -tion... but... uh... yeah, what do you think

---

## 65. ChatGPT

Hmm. I wasn't able to check that, but if you'd like, I can try again.

---

## 66. User

Hmm

---

## 67. ChatGPT

Checking.

---

## 68. User

Check

---

## 69. ChatGPT

For the deployment lecture, I'd use the Django app. It shows more of what deployment really means: server, environment variables, database, static files, logs. That's a lot

---

## 70. User

Uh Continue, sorry for interruptions

---

## 71. ChatGPT

No worries. So, deployment- I'd use Django because it shows what deployment really involves—server, environment variables, database migrations, static files, logs. Yeah. That's a little more complex... but that's the point. It teaches what "it works on my machine" misses. Then if time allows, you can do a lighter JavaScript deploy as a contrast, just to show how different stacks feel in production. Does that balance feel right?

---

## 72. User

Yeah, and what service uh... would be, would be the best? I want something uh... that, they can use for free. So there is no extra charge Or at least there should be uh... Free trial version

---

## 73. ChatGPT

Let me check the current free tier and trial options.

---

## 74. ChatGPT

For this course, I'd pick Render. It still has a free web service tier, hooks up to GitHub, auto deploys on push, gives you logs, env vars and rollbacks, which is exactly the learning loop you want students to see. Just don't rely on SQLite in production on Render's free tier, since that file system is ephemeral. Render's free Postgres option expires after 30 days. So if you want to avoid surprises, plan around that. Railway is a decent alternative with a 30-day 5 dollar trial and small free plan but that adds a bit more uncertainty for a class. I'd make lecture eight deploying the Django app on Render. And have the agent figure out the deployment with students instead of giving them steps- so deployment itself becomes an agentic exercise.

Sources:

- [Deploy for Free – Render Docs](https://render.com/docs/free?utm_source=chatgpt.com)
- [Pricing | Railway](https://railway.com/pricing?utm_source=chatgpt.com)
- [Plans and pricing : PythonAnywhere](https://www.pythonanywhere.com/pricing/)
- [Vercel Pricing: Hobby, Pro, and Enterprise plans](https://vercel.com/pricing?utm_source=chatgpt.com)

---

## 75. User

Okay, how many lectures are missing

---

## 76. ChatGPT

So we've sketched out eight. That leaves two. I'd use one as a capstone project where students propose and build something small end-to-end with an agent. And the last one a wrap-up on safety, limits, and next steps- or a showcase where they present what they built.

---

## 77. User

Okay, uh... I agree with your proposal... But now... review... Everything we talked about, and I want to ask... What topics... are missing... And... Regarding- regarding uh... my ideas uh... I think we should also focus on uh... more advanced uh... usage of... uh... coding uh... agentic coding tools uh... like skills... memory... complex and so on

---

## 78. ChatGPT

Checking that.

---

## 79. ChatGPT

Alright. Looking across the whole course, the big missing piece is exactly what you just named- advanced control of the agent itself. Up to now you've got a solid spine: literacy, flow, testing, multi-stack, deployment. Lecture nine is where I'd go meta: context and memory, instruction files versus just prompting, skills, MCP, sub-ag ents.

Sources:

- [管理 Claude 的内存 - Anthropic](https://docs.anthropic.com/zh-CN/docs/claude-code/memory?utm_source=chatgpt.com)
- [Create Skill Version | OpenAI API Reference](https://developers.openai.com/api/reference/cli/resources/skills/subresources/versions/methods/create?utm_source=chatgpt.com)
- [Model Context Protocol (MCP) - Anthropic](https://docs.anthropic.com/en/docs/mcp?utm_source=chatgpt.com)
- [Create an agent | OpenAI API Reference](https://developers.openai.com/api/reference/typescript/resources/beta/subresources/agents/methods/create?utm_source=chatgpt.com)

---

## 80. User

Mm

---

## 81. ChatGPT

A nice teaching progression is to make them feel the pain first. "Run the tests." "Okay, now again, but remember our conventions and test command."

---

## 82. User

Mm Mm

---

## 83. ChatGPT

And eventually, "we keep repeating ourselves." Then show Claude.md or Agents.md and start a new chat. Now it just knows. That's the "aha" moment. Skills next, then MCP as "we're giving the agent more tools and information." Then sub-agents as "parallel, specialized work." Lecture ten, I'd keep our capstone idea, but make it goal-based, not recipe-based: "given an existing app, add a feature, test it, and deploy." That forces them to choose how to use the agent. Smaller things I'd weave in throughout (not as new lectures): context window management, secrets and API keys, malicious instructions in repos, dependency safety, code review habits CI basics, model and cost trade-offs, and when to stop the agent. But with the advanced agent lecture plus capstone, your ten-lecture arc feels complete. Not too many techs, but a clear climb in agency and control.
