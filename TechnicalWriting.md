# Technical Writing

- <https://developers.google.com/tech-writing/overview>
- <https://www.writethedocs.org/>
- <https://levelup.gitconnected.com/document-well-build-better-the-impact-of-software-documentation-on-architecture-2fd46283bc78>

## Markdown

- <https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax>
- <https://www.markdowntutorial.com/>

## Diagrams

Diagram as Code:

- <https://github.com/mingrammer/diagrams>

Tools:

- <https://drawings.google.com/>
- <https://diagrams.net/>
- <https://www.lucidchart.com/pages/>

## Grammar

- Noun: A person, place, concept, or thing
- Pronoun: A noun that replaces another noun (or larger structure)
- Adjective: A word or phrase that modifies a noun
- Verb: An action word or phrase
- Adverb: A word or phrase that modifies a verb, an adjective, or another adverb
- Preposition: A word or phrase specifying the positional relationship of two nouns
- Conjunction: A word that connects two nouns or phrases
- Transition: A word or phrase that connects two sentences

## Words

### Define new or unfamiliar terms

- If the term already exists, link to a good existing explanation. (Don't reinvent the wheel.)
- If your document is introducing the term, define the term. If your document is introducing many terms, collect the definitions into a glossary.

### Use terms consistently

- Apply the same unambiguous word or term consistently throughout your document.

### Use acronyms properly

- On the initial use of an unfamiliar acronym within a document or a section, spell out the full term, and then put the acronym in parentheses.
- Put both the spelled-out version and the acronym in boldface.
- You may then use the acronym going forward.
- Do not cycle back-and-forth between the acronym and the expanded version in the same document.
  - Don't define acronyms that would only be used a few times.
  - Do define acronyms that meet both of the following criteria:
    - The acronym is significantly shorter than the full term.
    - The acronym appears many times in the document.

### Recognize ambiguous pronouns

- Only use a pronoun after you've introduced the noun.
- Place the pronoun as close as possible to the referring noun. In general, if more than five words separate your noun from your pronoun, consider repeating the noun instead of using the pronoun.
- If you introduce a second noun between your noun and your pronoun, reuse your noun instead of using a pronoun.
- The following pronouns cause the most confusion in technical documentation:
  - It
  - They, them and their
  - This
  - That

## Active Voice vs Passive Voice

The vast majority of sentences in technical writing should be in active voice.

- `Active Voice Sentence = actor + verb + target`
- `Passive Voice Sentence = target + verb + actor`
- `passive verb = form of be + past participle verb`

It is easy to mistakenly classify sentences starting with an imperative verb as passive.

## Clear sentences

### Choose strong verbs

- Choose precise, strong, specific verbs:
  - Raise
  - Generate
  - Ensure
- Reduce imprecise, weak, or generic verbs:
  - Forms of be: is, are, am, was, were, etc.
  - Occur
  - Happen

### Reduce there is / there are

### Minimize certain adjectives and adverbs

- Feed your technical readers factual data instead of marketing speak.
- Refactor amorphous adverbs and adjectives into objective numerical information.

## Short sentences

### Focus each sentence on a single idea

### Convert some long sentences to lists

### Eliminate or reduce extraneous words

### Reduce subordinate clauses

### Distinguish that from which

- which for nonessential subordinate clauses
- that for essential subordinate clauses
- Place a comma before which; do not place a comma before that.

## Lists and tables

### Choose the correct type of list

- Bulleted lists: Unordered items
- Numbered lists: Ordered items

### Keep list items parallel

- All items in a parallel list look like they "belong" together.
  - Grammar
  - Logical category
  - Capitalization
  - Punctuation

### Start numbered list items with imperative verbs

### Punctuate items appropriately

- Start each list item with a capital letter.
- If a list is a sentence, use sentence-ending punctuation.

### Create useful tables

- Label each column with a meaningful header.
- Avoid putting too much text into a table cell.
- Although different columns can hold different types of data, strive for parallelism within individual columns.

### Introduce each list and table

- Terminate the introductory sentence with a colon rather than a period.
- Although not a requirement, we recommend putting the word following into the introductory sentence.

## Paragraphs

### Write a great opening sentence

Good opening sentences establish the paragraph's central point.

```text
A loop runs the same block of code multiple times. For example, suppose you wrote a block of code that detected whether an input line ended with a period. To evaluate a million input lines, create a loop that runs a million times.
```

### Focus each paragraph on a single topic

A paragraph should represent an independent unit of logic.

### Don't make paragraphs too long or too short

Readers generally welcome paragraphs containing three to five sentences, but will avoid paragraphs containing more than about seven sentences.

### Answer what, why and how

- What are you trying to tell your reader?
- Why is it important for the reader to know this?
- How should the reader use this knowledge? Alternatively, how should the reader know your point to be true?

## Audience

`good documentation = knowledge and skills your audience needs to do a task − your audience's current knowledge and skills`

### Define your audience

Begin by identifying your audience's role(s). Sample roles include:

- Software engineers
- Technical, non-engineer roles (such as technical program managers)
- Scientists
- Professionals in scientific fields (for example, physicians)
- Undergraduate engineering students
- Graduate engineering students
- Non-technical positions

### Determine what your audience needs to learn

Write down a list of everything your target audience needs to learn to accomplish goals.

### Fit documentation to your audience

- Vocabulary and concepts
- Curse of knowledge (as experts, it is easy to forget that novices don’t know what you already know)
- Simple words
- Cultural neutrality and idioms

## Documents

### State your document's scope

- A good document begins by defining its scope.
- A better document additionally defines its non-scope.

```text
This document describes the design of Project Frambus.
This document does not describe the design for the related technology, Project Froobus.
```

### State your audience

- A good document explicitly specifies its audience.
- A good audience declaration might also specify any prerequisite knowledge or experience.
- In some cases, the audience declaration should also specify prerequisite reading or coursework.

```text
This document is aimed at the following audiences:
- software engineers
- program managers
This document assumes that you understand matrix multiplication and the fundamentals of backpropagation.
You must read "Project Froobus: A New Hope" prior to reading this document.
```

### Summarize key points at the start

- Compare and contrast your ideas with concepts that your audience already understands.

```text
The Froobus API handles the same use cases as the Frambus API, except that the Froobus API is much easier to use.
```

### Write for your audience

- Define your audience's needs:
  - Who is your target audience?
  - What is your target audience's goal? Why are they reading this document?
  - What do your readers already know before they read your document?
  - What should your readers know or be able to do after they read your document?
- Organize the document to meet your audience's needs

## Punctuation

### Commas

- As a guideline, insert a comma wherever a reader would naturally pause somewhere within a sentence.
- Use commas to separate items in an embedded list.
- In sentences that express a condition, place a comma between the condition and the consequence.
- You can also wedge a quick definition or digression between a pair of commas.
- Avoid using a comma to paste together two independent thoughts, use a period instead.

### Semicolons

- A period separates distinct thoughts; a semicolon unites highly related thoughts.
- Ask yourself whether the sentence would still make sense if you flipped the thoughts to opposite sides of the semicolon.
- The thoughts preceding and following the semicolon must each be grammatically complete sentences.

### Em dashes

- An em dash represents a longer pause—a bigger break—than a comma.
- Writers sometimes use a pair of em dashes to block off a digression.

### Parentheses

- Use parentheses to hold minor points and digressions.
- Parentheses inform readers that the enclosed text isn't critical.
- Keep parentheses to a minimum in technical writing.
- The rules regarding periods and parentheses aren't always clear. Here are the standard rules:
  - If a pair of parentheses holds an entire sentence, the period goes inside the closing parenthesis.
  - If a pair of parentheses ends a sentence but does not hold the entire sentence, the period goes just outside the closing parenthesis.

## Self-editing

### Adopt a style guide

- <https://developers.google.com/style>
- <https://developers.google.com/style/highlights>

### Think like your audience

### Read it out loud

Listen for awkward phrasing, too-long sentences, or anything else that doesn't feel natural.

### Come back to it later

### Change the context

Some writers like to print their documentation and review a paper copy, red pencil in hand. A change of context when reviewing your own work can help you find things to improve. For a modern take on this classic tip, copy your draft into a different document and change the font, size, and color.

### Find a peer editor

Ask someone to review your document and give you specific, constructive comments.

## Organizing large documents

### When to write large documents

You can organize a collection of information into longer standalone documents or a set of shorter interconnected documents. A set of shorter interconnected documents is often published as a website, wiki, or similar structured format.

- How-to guides, introductory overviews, and conceptual guides often work better as shorter documents when aimed at readers who are new to the subject matter.
- In-depth tutorials, best practice guides, and command-line reference pages can work well as lengthier documents, especially when aimed at readers who already have some experience with the tools and subject matter.
- A great tutorial can rely on a narrative to lead the reader through a series of related tasks in a longer document. However, even large tutorials can sometimes benefit from being broken up into smaller parts.
- Many longer documents aren't designed to be read in one sitting. For example, users typically scan through a reference page to search for an explanation of a command or flag.

### Organize a document

- Outline a document
  - Before you ask your reader to perform a task, explain to them why they are doing it.
  - Limit each step of your outline to describing a concept or completing a specific task.
  - Structure your outline so that your document introduces information when it's most relevant to your reader.
  - Consider explaining a concept and then demonstrating how the reader can apply it either in a sample project or in their own work.
  - Before you start drafting, share the outline with your contributors.
- Outline exercise
  - Rearrange the existing topics.
  - Add any missing topics you feel should be in an introduction.
  - Remove any topics you feel are irrelevant for an introduction.
- Introduce a document
  - What the document covers.
  - What prior knowledge you expect readers to have.
  - What the document doesn't cover.

### Add navigation

Clear navigation includes:

- introduction and summary sections
- a clear, logical development of the subject
- headings and subheadings that help users understand the subject
- a table of contents menu that shows users where they are in the document
- links to related resources or more in-depth information
- links to what to learn next

### Disclose information progressively

- Where possible, try introducing new terminology and concepts near the instructions that rely on them.
- Break up large walls of text. To avoid multiple large paragraphs on a single page, aim to introduce tables, diagrams, lists, and headings where appropriate.
- Break up large series of steps. If you have a particularly long list of complicated steps, try to re-arrange them into shorter lists that explain how to complete sub-tasks.
- Start with simple examples and instructions, and add progressively more interesting and complicated techniques.

## Illustrating

### Write the caption first

Good captions have the following characteristics:

- They are brief. Typically, a caption is just a few words.
- They explain the takeaway. After viewing this graphic, what should the reader remember?
- They focus the reader's attention.

### Constrain the amount of information in a single drawing

- As a rule of thumb, don't put more than one paragraph's worth of information in a single diagram.
- An alternative rule of thumb is to avoid illustrations that require more than five bulleted items to explain.
- Organize complex systems into subsystems.
- After showing the "big picture," provide separate illustrations of each subsystem.

### Focus the reader's attention

- Visual cues
- Callouts

### Illustrating is re-illustrating

As with writing, the first draft of an illustration is seldom good enough. Revise your illustrations to clarify the content. As you revise, ask yourself the following questions:

- How can I simplify the illustration?
- Should I split this illustration into two or more simpler illustrations?
- Is the text in the illustration easy to read? Does the text contrast sufficiently with its background?
- What's the takeaway?

## Creating sample code

Good sample code is often the best documentation.

### Correct

- Build without errors.
- Perform the task it claims to perform.
- Be as production-ready as possible. For example, the code shouldn't contain any security vulnerabilities.
- Follow language-specific conventions.
- Good documents explain how to run sample code.

### Concise

- Sample code should be short, including only essential components.
- Never use bad practices to shorten your code; always prefer correctness over conciseness.

### Understandable

- Pick descriptive class, method, and variable names.
- Avoid confusing your readers with hard-to-decipher programming tricks.
- Avoid deeply nested code.
- Optional: Use bold or colored font to draw the reader's attention to a specific section of your sample code. However, use highlighting judiciously—too much highlighting means the reader won't focus on anything in particular.

### Commented

- Keep comments short, but always prefer clarity over brevity.
- Avoid writing comments about obvious code, but remember that what is obvious to you (the expert) might not be obvious to newcomers.
- Focus your commenting energy on anything non-intuitive in the code.
- When your readers are very experienced with a technology, don't explain what the code is doing, explain why the code is doing it.

### Reusable

- All information necessary to run the sample code, including any dependencies and setup.
- Code that can be extended or customized in useful ways.

### Sequenced

A good sample code set demonstrates a range of complexity.

## Architecture Documentation

C4 model <https://c4model.com/>
