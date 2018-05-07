# The Joel Test

Notes taken from Joel Spolsky's [The Joel Test: 12 Steps to Better Code](https://www.joelonsoftware.com/2000/08/09/the-joel-test-12-steps-to-better-code/).

## About The Test

The Joel Test, written by Joel Spolsky, is a quick 12-step test to verify whether your project is up to snuff. It's supposed to combat the overly complicated SEMA.

1. Do you use source control?
2. Can you make a build in one step?
3. Do you make daily builds?
4. Do you have a bug database?
5. Do you fix bugs before writing new code?
6. Do you have an up-to-date schedule?
7. Do you have a spec?
8. Do programmers have quiet working conditions?
9. Do you use the best tools money can buy?
10. Do you have testers?
11. Do new candidates write code during their interview?
12. Do you do hallway usability testing?

For everything answered "no," subtract one point from the results. 12 is a perfect score, 11 is tollerable, but 10 or lower causes problems. While not a factor in determining success or failure, this short test can help you address loose ends to really tighten a project.

### Source Control

Source control is imprtant for a number of reasons. Logging history makes it easy to see who changed what, and mistakes need an easy way to be rolled back. Source code itself is checked out on every hard drive it's picked up on, so code is a lot harder to lose. Joel mentions CVS, but it's since been replaced with Git (since this article is ancient).

### One-Step Build

A one-step build answers a question of: how many steps does it take to make a shipping build from the latest source snapshot? There should really be only one script that needs to be run to do a full checkout, rebuild the code, make EXEs (in all versions, languages, and combinations), creates the install package, and creates the final media. A one-step build is important because every step you introduce to the process creates the probability of increasing mistakes.

### Daily Builds

Daily builds help prevent errors in much of the same way that source control does. Breaking the build is common, so the idea of creating a daily build helps ensure no breaks will go unnoticed. It also gives you the chance to find and address the issue much earlier without piling up a lot of new code that you'll have to sift through to find the solution. Joel's team used to run a build every day at noon, then everyone would check it and if it worked they would continue going about their business.

_Aside: This is also called a nightly build._

### Bug Database

Remembering bugs in your head is too hard, and is nonsense. Keeping track of bugs formally allows all developers on the project to see the issues publicly, and can be used to track bug history. Typically these databases include (at minimum):

* Complete steps to reproduce the bug.
* Expected behavior.
* Observed (buggy) behavior.
* Who it's assigned to.
* Whether it's been fixed or not.

This is easy to manage with platforms like GitHub these days, but there's no reason it can't be tracked with a simple table.

### Bug Fixes before New Code

In general, the longer you wait to fix a bug, the costlier it is in time and money. Waiting to fix a bug also means that you're potentially creating new data around existing issues which will further dig into those issues. Additionally, waiting to fix a bug means you're likely going to forget the exact details you mentally noted while working on the code at the time. Fixing bugs ensures being able to provide timely schedules - if you wait to fix a number of bugs at once, it's almost impossible to guess how long it would take to track down and fix all of the issues in one sitting. The best way to approach this is with Test Driven Development and thinking in a "ready to ship at all times" mindset.

## Up-to-Date Schedule

Having a schedule for delivery is important whether you like it as a programmer or not. Businesses need to know when products can be ready for shipping, and having a schedule is the only way to allow a business to make plans in advance, including: demos, trade shows, advertising, etc.. Having a schedule also forces you to decide what features are the least important and cut them rather than slipping into "feature creep" which is the ever-ongoing expansion of new features without making progress.

## Specs

Specs are one of the most critical parts of any project. Without a spec clearly outlining the project, the project is likely to become a confusing mess. Both Netscape and Mozilla had massive issues with their early specs that it caused problems internally with their companies. A spec will help the project be crystal clear to everyone working on it, from the developers to the marketers. It keeps everyone on the same page and paints a picture of the details.

## Quiet Working Conditions

This one is fairly obvious, but programmers need a quiet working environment to "get into the zone," or really be productive. Constant distractions like phone calls, messages, conversations, etc., all serve to drag a person away from what they're concentrating on and it can take up to 15 minutes to return to that state of productivity. Minimizing distractions is important.

## Best Tools Money can Buy

This goes beyond the scope of hardware, but does include it. The issue stems from time and complexity: if it's taking you five times as long to compile a program on ann older computer than it would take on a newer one, that's five times longer it takes to return to being productive. Working with a single-monitor setup is nearly impossible if not an incredible headache due to the number of sources and information a programmer needs to use. Even things like being forced to use MS Paint over Photoshop or other better graphics tools can cause frustration, consume a lot more time, and ultimately kill productivity (and even quality). This doesn't mean you need to work on a quantum computer with a 50 4k monitor setup, but it does mean you should allow yourself or your team the space they need in terms of technology to get the job done to the best of their abilities.

## Testing

Testers are important: period. Testing code while building it is a start, but having someone dedicated to trying to break that code is just as important as TDD. It wastes programming time for the programmer to have to try and break their own code, while also limiting them because they know how something is "supposed to work," but can't see it through fresh eyes of a user's mindset.

## Coding Interviews

This one is less about projects and more about a team itself, but working with people who know what they're doing will help a lot. Joel makes the comment, "You wouldn't hire a magician without asking them to show you some magic tricks."

## Hallway Usability Testing

TDD and dedicated testers are great, but in the end, it's the end user that will be using your program: someone who likely has little to no experience with your program or company. The idea behind this type of testing is to "grab the nearest person in the hallway" and ask them to try using your software. If they're confused by what they're working with, or end up breaking something, then it's not their fault: it's yours as the programmer, and it needs to be resolved.