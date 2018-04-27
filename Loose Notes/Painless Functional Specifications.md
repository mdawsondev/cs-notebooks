# Painless Functional Specifications

Notes taken from Joel Spolsky's [Painless Functional Specifications articles](https://www.joelonsoftware.com/2000/10/02/painless-functional-specifications-part-1-why-bother/).

## Part 1: Why Bother

_[Link to Part 1](https://www.joelonsoftware.com/2000/10/02/painless-functional-specifications-part-1-why-bother/)_

Writing specifications saves time in the long run. Ultimately, if you aren't writing specs (writing how the program works in minute details), you can cripple your development process.

An example is given where two developers are creating the same project: one with a spec, and one without. The person without a specification paper sees skipping this process as a way to save time. They may, before the end, find themselves ahead of the process of the developer using the spec, but it's a bittersweet victory. Non-spec developers consistantly end projects with lower quality code that is more difficult to maintain and may not even adhere to what the client ultimately wanted in the first place.

Having to delete code and make changes because a vision isn't clear can cause more time in corrections than it would have initially cost to set clear goals. If a client is expecting more than what they're given, or even something entirely different, this creates a catch where: sure, you've saved time not writing a spec, but you may very well more than quadruple the cost down the road. The idea behind writing a specification is that it gives you a very clean, very precise vision of the project ahead. It may take a couple of hours to flesh out a meaningful spec, but in the end, it ensures you know the exact path to be walked and it also ensures everyone else on the team is on the same page.

Specifications:

* Give a clear path for developers.
* Give a clear picture to everyone working on the project.
* Give a detailed, but still high-level overview of a project's expectations.
* Give the client a chance to ensure the vision is correct.

Making sure the picture is clear to everyone on a team is important beyond a developer's scope. Technical writers need to know what they're writing about, marketers need to know what they're selling, etc.; all of these can easily factor into costing development time for having to explain the project over and over, and may even put a nail in the road causing a complete blowout if the project can't be visualized through the end.

## Part 2: What's a Spec

_[Link to Part 2](https://www.joelonsoftware.com/2000/10/03/painless-functional-specifications-part-2-whats-a-spec/)_

Specifications fall into two major categories, and are ordered by importance:

1. A **functional specification** describes how a product will work entirely from the user's perspective. It doesn't care about how the thing is implemented - it talks about features, it specifies screens, menues, dialogs, nad so on.

2. A **technical specification** describes the internal implementation of the program. It talks about data structures, relational database models, choice of programming languages and tools, algorithms, etc.

_[Link to sample functional specification](https://www.joelonsoftware.com/whattimeisit/)_

**Highlights**:

* Disclaimer
* Written by a Single Author
  * Parts Potentially Done by Individuals
* Overview
* User Scenarios
* Non-Goals
* UX Flowchart
* Screen by Screen Specification
  * Page Specifications
* Allowing Open Issues
* Allowing Side Notes to Specific Teams

**Quick rundown**:

A **disclaimer** will say, "Hey, these are specifications. They can change, and if you feel a change is necessary, let me know." Having these specifications written by a single author, or segmented between multiple authors, allows you to own the mistakes and content made. It allows one person to ensure the quality of the specification is up to par and not murky.

Including an **overview** is like a table of contents; it might be a simple flowchart or an extensive architectural discussion. The idea is that everyone who reads this needs to get the big picture from it.

**Scenarios** give insight to the workflow of the content in question. By providing scenereos, it allows people reading the specification to get into the mindset of potential users and how the site works and who it's for.

**Non-goals** give an opportunity to say very bluntly, "These are the things we are not going to do." They help keep the project in line and don't allow sidetracking.

**Open issues** and **side notes** allow for aside commentary that may be relevant to one specific group of people. If not relevant, it could easily be glossed over and is quickly mentioned. Open issues specifically allow for awareness in potential conflict and encourage input.

Beyond this, everything is about explaining details. Give details about _everything_. The descriptions in alert windows, the login message, etc. design itself shouldn't be a factor here, but it should be very specific about what the user experience will be.

Above all, **User Experience** is key.

## Part 3: But... How

_[Link to Part 3](https://www.joelonsoftware.com/2000/10/04/painless-functional-specifications-part-3-but-how/)_

