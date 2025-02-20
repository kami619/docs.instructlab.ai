---
title: Knowledge Guide
description: An overview of 🐶 InstructLab's knowledge
logo: images/ilab_dog.png
---
# What is "Knowledge"?

In the InstructLab world, knowledge consists of data and facts and is backed by documents. When you create knowledge for a model, you're giving it additional data to more accurately answer questions.

Knowledge contributions in this project contain a few things:

- A file in a git repository that holds your information. For example, these repositories can include markdown versions of information on Oscar 2024 winners, Law books, Shakespeare, Sports, Chemistry, etc.
- A `qna.yaml` file that asks and answers questions about the information in the git repository.
- An `attribution.txt` file that includes the sources for the information used in the `qna.yaml`.

You can learn more about the knowledge structure in [Getting Started with Knowledge contributions](https://github.com/instructlab/taxonomy/blob/main/README.md#getting-started-with-knowledge-contributions).

## Accepted Sources of Knowledge

!!! important
    We are currently only accepting knowledge contributions as a limited private beta and sources will be limited to articles from Wikipedia.

These are the main knowledge domains that we are currently accepting knowledge contributions for:  arts, engineering, geography, history, linguistics, mathematics, philosophy, religion, science, and technology.

Due to the open source nature of InstructLab, all content has to meet specific licensing requirements. This list has currently approved sources for knowledge. If you wish to use a different source, we need to approve it, and that means your submission will be on hold until we get legal review and approval. Please be patient!

Domain Name | Status | Notes
--|--|--
[Wikipedia](https://en.wikipedia.org/wiki/Main_Page) | approved | -
[Project Gutenberg](https://www.gutenberg.org) | approved | Pre-1927 works; public domain under US copyright law
[Wikisource](https://en.wikisource.org) (library) | approved | "free library that anyone can improve"
[OpenStax textbooks family of publications](https://openstax.org/subjects) | approved | -
[The Open Organization publications](https://theopenorganization.org) | approved | -
[The Scrum Guide](https://scrumguides.org/index.html) | approved | -
[US Congress site](https://www.congress.gov) | reviewed - manually verify | US government sources may have different licensing; a legal review will need to verify each source
[US White House site](https://www.whitehouse.gov) | reviewed - manually verify | US government sources may have different licensing; a legal review will need to verify each source
[US Senate site](https://www.senate.gov) | reviewed - manually verify | US government sources may have different licensing; a legal review will need to verify each source
[US IRS site](https://www.irs.gov) | reviewed - manually verify | US government sources may have different licensing; a legal review will need to verify each source
[NASA](https://www.nasa.gov) | reviewed - manually verify | [See guidelines](https://www.nasa.gov/nasa-brand-center/images-and-media/)
[Smithsonian Libraries](https://library.si.edu/) | reviewed - manually verify | For any material marked \"No Copyright - United States" or "CC0" as [described here](https://library.si.edu/copyright)
[European Union (EU) site](https://european-union.europa.eu/) | reviewed - manually verify | Specifically documents submitted under "public registrars" as [described here](https://european-union.europa.eu/principles-countries-history/principles-and-values/access-information_en)
[Internet Archive](https://archive.org/) | reviewed - manually verify | Pre-1927 works; public domain under US copyright law
[PLOS family of open access journals](https://plos.org/publish) | reviewed - manually verify | -
[Open Practice Library](https://openpracticelibrary.com/) | reviewed - manually verify | -
[Cynefin.io wiki](https://cynefin.io/wiki/Main_Page) | reviewed - manually verify | -
[The Open Education Project](https://research.redhat.com/blog/research_project/foundations-in-open-source-education/) | reviewed - manually verify | -


## Avoid These Topics

While the tuning process may eventually benefit from being used to help the models work with complex social topics, at this time this is an area of active research we do not want to take lightly. Therefore, please keep your submissions clear of the following topics:

- PII (personally identifiable information) or any content invasive of individual privacy rights
- Violence, including self-harm
- Cyber bullying
- Internal documentation or other information that is confidential to your employer or organization, such as trade secrets
- Discrimination
- Religion
  - Facts such as, "[Christianity is, according to the 2011 census, the fifth most practiced religion in Nepal, with 375,699 adherents, or 1.4% of the population](https://en.wikipedia.org/wiki/Christianity_in_Nepal)", are fine as a knowledge contribution. However, advocating in favor of or against any religious faith is not acceptable.
- Medical or health information
  - Facts such as,  "[In mammals, pulmonary ventilation occurs via inhalation (breathing)](https://opentextbc.ca/biology/chapter/11-3-circulatory-and-respiratory-systems/)," are fine as a knowledge contribution. However, tailored medical/health advice is not acceptable.
- Financial information
  - Facts such as "[laissez-faire economics ... argues that market forces alone should drive the economy and that governments should refrain from direct intervention in or moderation of the economic system](https://openstax.org/books/world-history-volume-2/pages/6-3-capitalism-and-the-first-industrial-revolution)," are fine as a knowledge contribution. However, tailored financial advice is not acceptable.
- Legal settlements or mitigations
- Gender bias
- Hostile language, threats, slurs, and derogatory or insensitive jokes or comments
- Profanity
- Pornography and sexually explicit or suggestive content
- Any contributions that would allow for automated decision making that affect an individual's rights or well-being, such as social scoring
- Any contributions that engage in political campaigning or lobbying

We are also not accepting submissions of the following content:

- Code
  - Anything code-related that can be traced back to code for a computer. Not limited to `sed` or `bash` or `yaml`s for OpenShift or Kubernetes, to `python` snippets to `Java` suggestions. There are specific models focused on this space and this isn't for this model for the time being.
- Jokes
- Poems

We received many joke and poem submissions at the beginning of the project, and with jokes and poems being "in the eye of the beholder" and puns requiring nuance for native English speakers, we realized we were possibly unconsciously biasing our model. We have discovered that working with both topics has its own challenges, and if we want something generalized, finding consensus was unsuccessful. For now, we're not accepting additional submissions of jokes and poems.

## Building Your LLM Intuition

LLMs have inherent limitations that make certain tasks extremely difficult, like doing math problems. They're great at other tasks, like creative writing. And they could be better at things like logical reasoning.

Providing an LLM training pipeline with knowledge helps create a basis of information that the model can learn from. With InstructLab, you can teach it to use this knowledge via the `qna.yaml` files.

For example, you can give an LLM the entire periodic table, then in a `qna.yaml` add something like:

```yaml
question: What is the symbol and atomic number for Chlorine?
answer: |
  The symbol for chlorine is Cl and the atomic number is 17.
```

With a few of these question-and-answer pairs, the model will learn the periodic table because it has the knowledge data.

### LLMs are great at

LLMs are great at these:

- Brainstorming
- Creativity
- Connecting information
- Cross-lingual behavior

For these, however, it's common for LLMs to already have excellent performance. Try 3-5 examples in `lab chat` to confirm a deficit in the model before you build your submission, and then share the examples in your Pull Request (PR).

### LLMs need help with

LLMs need help with these:

- Chains of reasoning
- Analysis
- Story plots
- Reassembling information
- Effective and succinct summaries

LLM behavior in these sorts of topics are very difficult for the model to get right. Try several examples to understand the nuances of the model's ability to do these sorts of tasks, and then consider using corrections to the results you get in your tuning process.

### LLMs are not so great at

LLMs are not so great at these:

- Math
- Computation
- "Turing-complete" type tasks
- Generating only true real-world information (they're prone to hallucinations)

 LLMs may struggle with solving math and computation problems. That said, improving some of these foundational skills may be something this work tackles in the future, but not at this time.
