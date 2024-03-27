# Technical Writing

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

- Define new or unfamiliar terms
  - If the term already exists, link to a good existing explanation. (Don't reinvent the wheel.)
  - If your document is introducing the term, define the term. If your document is introducing many terms, collect the definitions into a glossary.
- Use terms consistently
  - Apply the same unambiguous word or term consistently throughout your document.
- Use acronyms properly
  - On the initial use of an unfamiliar acronym within a document or a section, spell out the full term, and then put the acronym in parentheses.
  - Put both the spelled-out version and the acronym in boldface.
  - You may then use the acronym going forward.
  - Do not cycle back-and-forth between the acronym and the expanded version in the same document.
    - Don't define acronyms that would only be used a few times.
    - Do define acronyms that meet both of the following criteria:
      - The acronym is significantly shorter than the full term.
      - The acronym appears many times in the document.
- Recognize ambiguous pronouns
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

- Choose strong verbs
  - Choose precise, strong, specific verbs:
    - Raise
    - Generate
    - Ensure
  - Reduce imprecise, weak, or generic verbs:
    - Forms of be: is, are, am, was, were, etc.
    - Occur
    - Happen
- Reduce there is / there are
- Minimize certain adjectives and adverbs
  - Feed your technical readers factual data instead of marketing speak.
  - Refactor amorphous adverbs and adjectives into objective numerical information.

## Short sentences

- Focus each sentence on a single idea
- Convert some long sentences to lists
- Eliminate or reduce extraneous words
- Reduce subordinate clauses
- Distinguish that from which
  - which for nonessential subordinate clauses
  - that for essential subordinate clauses
  - Place a comma before which; do not place a comma before that.

## Lists and tables

- Choose the correct type of list
  - Bulleted lists: Unordered items
  - Numbered lists: Ordered items
- Keep list items parallel
  - All items in a parallel list look like they "belong" together.
    - Grammar
    - Logical category
    - Capitalization
    - Punctuation
- Start numbered list items with imperative verbs
- Punctuate items appropriately
  - Start each list item with a capital letter.
  - If a list is a sentence, use sentence-ending punctuation.
- Create useful tables
  - Label each column with a meaningful header.
  - Avoid putting too much text into a table cell.
  - Although different columns can hold different types of data, strive for parallelism within individual columns.
- Introduce each list and table
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

## Architecture Documentation

C4 model <https://c4model.com/>
