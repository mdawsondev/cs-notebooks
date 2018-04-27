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

In short, if you're working on a team, a program manager is the one technically responsible for writing a specification. Although (obviously) not mandatory, it's a very specific job with specific needs. Ideally, the skills of a good program manager include being well-spoken, diplomacy, market awareness, user empathy, and good at UI design.

Marketers and coders are not ideal program managers because the skills involved are typically so specific to their talents that they fall short in areas that could be taken care of by a specialist. Additionally, you shouldn't have your coders reporting to a program manager. It's time consuming and it's irrelevant beyond the lead developer's reach. Once the specification has been made and agreed upon, the best way to get things done are to give your team the room they need to get it done.

In short, program management is a separate career path. They need to be technical, but they don't need to be good codes. They study UI, meet customers, and write specifications.

## Part 4: Tips

_[Link to Part 4](https://www.joelonsoftware.com/2000/10/15/painless-functional-specifications-part-4-tips/)_

### Keep Things Interesting

Specs are good, but only if they're being read. Typically from large companies, specs are large and mind-numbing papers that may be glanced at then shelved and never seen again. The idea is to keep your specs **interesting** and readable. Being funny is a good way to keep everyone interested because it generates emotion from otherwise boring documents.

### Keep Things Readable

This is as equally important in code as it is in a spec. Although you could get into a mind-numbing paragraph about how a function works, it's easier (and more to the point, clearer) to just write an example and add a technical note.

> Assume a function AddressOf(x) which is defined as the mapping from a user x, to the RFC-822 compliant email address of that user, an ANSI string. Let us assume user A and user B, where A wants to send an email to user B. So user A initiates a new message using any (but not all) of the techniques defined elsewhere, and types AddressOf(B) in the To: editbox.

This could also have been speced as:

> Miss Piggy wants to go to lunch, so she starts a new email and types Kermit’s address in the “To:” box. 
>
> **Technical note:** _the address must be a standard Internet address (RFC-822 compliant.)_

They both "mean" the same thing but one is far easier to understand. Having to decrypt the meaning of something is unenjoyable and creates frustation. Your spec needs to be understood by everyone involved on a high-level, and the details are filled in once the picture is clear. When writing a spec, try to imagine the person you're addressing it to and imagine what you're asking them to understand at every step.

### Keep Things Simple

Using simple language helps create clarity. Words like "use" instead of "utilize," although less fancy 🤵, keeps things _understandable_ and easy to digest.

* Short sentences.
* Avoid walls of text.
* Use easy words.
* Screenshots!

The last point, screenshots, is important - pictures make text easier to digest and also create a visual representation of what you're trying to portray. If your spec isn't easy to read, then rewrite it.

### Don't Use Templates

Templating your specs may seem like a good idea initially, but the problem is that each project has its own unique needs. One spec may be entirely different than another. Additionally, using templates creates waste - where _bibliography_ might have been the right choice for one spec, adding it to others would simply be a headache and complete waste of time.

## Summary

Overall, a spec is a document that you want people to read. It gets everyone on the same page, it's easy to understand, and it isn't like reading a technical scientific publication. It paints an extremely clear picture of every detail in easy-to-read language that can be referenced as the project moves forward.