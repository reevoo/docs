# Pull Requests

We use Pull Requests to ensure new code is good enough *before* it is added to the existing code.

Our code is good enough if it is:
- **Tested** - Working code is the best.
- **Designed for change** - Change is inevitable. Systems should be able to cope with change.
- **Easy to understand** - Code is read many more times than it is written, so it should be read-optimised.
- **Able to cope when things go wrong** - It's better to have thought about something *before* it happens in production!

Good pull requests are:
- **Descriptive** - You're the expert, the reviewer is not; any help you can give makes your review more detailed and leads to less questions being asked.
- **Small** - Small Pull Requests are easier to review.
- **Short-lived** - The longer a Pull Request lasts, the farther away it gets from the main code base, making it harder to merge/rebase.

##### Before Opening a Pull Request
- Make sure the code you have written is able to cope with change. Well-designed code should respect common design principles like [SOLID](https://en.wikipedia.org/wiki/SOLID_(object-oriented_design)) and [The Law of Demeter](https://en.wikipedia.org/wiki/Law_of_Demeter). Ask for a design review if you're not sure.
- Try to close someone else's Pull Request before opening your own.
- Where are your tests? If you don't have any, how did you test it?
- Can you split up the Pull Request into smaller Pull Requests? If not, why not?

##### Your Pull Request
- Your description should answer the question, "what have you done?"
- Why are you doing the work? Reference any stories or GitHub Issues.
- Explain whether the Pull Request is ready to merge or whether you just want to discuss it.

##### Reviewing a Pull Request
- Code quality is extremely important for the future. Remember that you are the last chance to spot mistakes and correct poor design. Pull Requests should take more than 10 minutes for all but the most trivial changes.
- If you read a Pull Request, leave a comment! Don't worry about not being the expert.
- If it's on CI, has it gone green? If it's not on CI, pull the branch, run the tests and leave a comment with the results.
- Did the code need explaining (usually through comments)? If so, the code needs making clearer.
- How is the code tested? What are the edge cases - are they tested? How does the code behave when something goes wrong?
- How is the new feature documented?
- Can we write less code and do the same thing?
- If you think the code is fine, but you are unsure of the context, use "LGTMBWTFDIK" (Looks Good to Me, but What Do I Know).

##### Merging a Pull Request
- The owner should merge the Pull Request; they know whether the Pull Request is ready to merge or not.
- You should have documented evidence that someone has reviewed your code. This can be as simple as "LGTM" (Looks Good to Me) on the Pull Request.
