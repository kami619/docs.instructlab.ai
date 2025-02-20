---
title: Getting Started with Skill Contributions
description: Adding skills to 🐶 InstructLab
logo: images/ilab_dog.png
---
## Getting Started with Skill Contributions

Skills require a much smaller volume of content than knowledge contributions. An entire skill contribution to the taxonomy tree can be just a few lines of YAML in the `qna.yaml` file ("qna" is short for "questions and answers") and an `attribution.txt` file for citing sources.

Your skills contribution pull requests include the following:

- A `qna.yaml` that contains a set of key/value entries
- An `attribution.txt` that includes the sources for the information used in the `qna.yaml`. Even if you are authoring the skill with no additional sources, you must have this file for legal purposes.

!!! tip
    The skill taxonomy structure is used in several ways:

    1. To select the right subset of the taxonomy to use for data generation.
    2. To determine the interpretability by human contributors and maintainers.
    3. As part of the prompt to the LLM used to generate synthetic samples.


!!! important
    There is a limit to how much content can exist in the question/answer pairs for the model to process. Due to this, only add a maximum
    of around 2300 words to your question and answer seed example pairs in the `qna.yaml` file.

Compositional skills can either be grounded (includes a context) or ungrounded (does not include a context).  Grounded or ungrounded is declared in the taxonomy tree, for example: `linguistics/writing/poetry/haiku/` (ungrounded) or `grounded/linguistics/grammar` (grounded). The `qna.yaml` is in the final node.

### The structure of the `qna.yaml` file

Taxonomy skill files must be a valid [YAML](https://yaml.org/) file named `qna.yaml`. Each `qna.yaml` file contains a set of key/value entries with the following keys:

Field | Required? | Content
--|--|--
`version` | yes | The value must be the number 3.
`task_description` | yes | A description of the skill.
`created_by` | yes | The GitHub username of the contributor.
`seed_examples` | yes | A collection of key/value entries. New submissions should have at least five entries, although older files may have fewer.<br/><br/>Note collections are nested lists, like subentries in a bulleted list.
`context` | only for grounded skills | Part of the `seed_examples` collection.<br/><br/>Grounded skills require the user to provide context containing information that the model is expected to take into account during processing. This is different from knowledge, where the model is expected to gain facts and background knowledge from the tuning process.<br/><br/>**Note:** The context key should not be used for ungrounded skills.
 `question` | yes | Part of the `seed_examples` collection.<br/><br/>A question for the model.
`answer` | yes | Part of the `seed_examples` collection.<br/><br/>The desired response from the model.

Other keys at any level are currently ignored.

!!! important
    Each `qna.yaml` file requires a minimum of five question and answer pairs.

### Submissions

To make the `qna.yaml` files easier and faster for humans to read, it is recommended to specify `version` first, followed by `task_description`, then `created_by`, and finally `seed_examples`.
In `seed_examples`, it is recommended to specify `context` first (if applicable), followed by `question` and `answer`.

*Example `qna.yaml`*

```yaml
version: 2
task_description: <string>
created_by: <string>
seed_examples:
  - question: <string>
    answer: |
      <multi-line string>
  - context: |
      <multi-line string>
    question: <string>
    answer: |
      <multi-line string>
  ...
```

Then, you create an `attribution.txt` file that includes the sources of your information, if any. These sources can also be self-authored sources for skills.

*Fields in `attribution.txt`*

```text
[Link to source]
[Link to work]
[License of the work]
[Creator name]
```

*Example of a self-authored source `attribution.txt`*

```text
Title of work: Customizing an order for tea
Link to work: -
License of the work: CC BY-SA-4.0
Creator names: Jean-Luc Picard
```

You may copy this example and replace the title of the work (your skill) and the creator name to submit a skill. The license is [Creative Commons Attribution-ShareAlike 4.0 International](https://creativecommons.org/licenses/by-sa/4.0/), which is shortened to `CC BY-SA-4.0`.

For more information on what to include in your `attribution.txt` file, see [For your attribution.txt file](https://github.com/instructlab/taxonomy/blob/main/CONTRIBUTING.md#for-your-attributiontxt-file) in CONTRIBUTING.md.

### Writing YAML

If you have not written YAML before, YAML is a text file where indentation matters.

!!! tip

    - Spaces and indentation matter in YAML. Use two spaces to indent.
        - Don't use tabs!
    - Do not have trailing spaces at the end of a line.
    - Each example in `seed_examples` begins with a dash (`-`). Place this dash in
    front of the first field (`question` or `context`). The remaining keys in the
    example should not have this dash.
    - Some special characters such as a double quotation mark (`"`) and an apostrophe or single quotation mark (`'`) need to be escaped with backslash. This is why some of the lines for keys in the example YAML start the value with the pipe character (`|`) followed a new line and then an indented multi-line string. This character disables all of the special characters in the value for the key.<br/><br/>You might also want to use the pipe character (`|`) for multi-line strings.
    - Consider quoting all values with double quotation marks (`"`) to avoid surprising YAML parser behavior
    (e.g. Yes answer can be interpreted by the parser as a boolean of `True`
    value, unless "Yes" is quoted.)
    - See [yaml-multiline.info](https://yaml-multiline.info/) for more info.

It is recommended that you **lint**, or verify, your YAML using a tool. One linter option is [yamllint.com](https://yamllint.com). You can copy/paste your YAML into the box and click **Go** to have it analyze your YAML and make recommendations. Online tools like [prettified](https://onlineyamltools.com/prettify-yaml) and [yaml-validator](https://jsonformatter.org/yaml-validator) can automatically reformat your YAML to adhere to our `yamllint` PR checks, such as breaking lines longer than 120 characters.

### Examples

#### Ungrounded compositional skill: YAML example

```yaml
version: 2
task_description: 'Teach the model how to rhyme.'
created_by: juliadenham
seed_examples:
  - question: What are 5 words that rhyme with horn?
    answer: warn, torn, born, thorn, and corn.
  - question: What are 5 words that rhyme with cat?
    answer: bat, gnat, rat, vat, and mat.
  - question: What are 5 words that rhyme with poor?
    answer: door, shore, core, bore, and tore.
  - question: What are 5 words that rhyme with bank?
    answer: tank, rank, prank, sank, and drank.
  - question: What are 5 words that rhyme with bake?
    answer: wake, lake, steak, make, and quake.
```

Here is the location of this YAML in the taxonomy tree. Note that the YAML file
itself, plus any added directories that contain the file, is the entirety of the skill
in terms of a taxonomy contribution:

#### Ungrounded compositional skill: Directory tree example

```ascii
[...]

└── writing
    └── poetry
    |   └── haiku <=== here it is :)
    |   |   └── qna.yaml
    |   |       attribution.txt
        [...]
    └── prose
    |   └── debate
    |   |   └── qna.yaml
    |   |       attribution.txt
    [...]

[...]
```

#### Grounded compositional skill: YAML example

Remember that [grounded compositional skills](skills_guide.md#grounded-compositional-skills) require additional context and include a `context` field.

This example snippet assumes the GitHub username `mairin` and shows some of the question/answer pairs present in the actual file:

```yaml
version: 2
task_description: |
    This skill provides the ability to read a markdown-formatted table.
created_by: mairin # Use your GitHub username; only one creator supported
seed_examples:
  - context: |
      | **Breed**      | **Size**     | **Barking** | **Energy** |
      |----------------|--------------|-------------|------------|
      | Afghan Hound   | 25-27 in     | 3/5         | 4/5        |
      | Labrador       | 22.5-24.5 in | 3/5         | 5/5        |
      | Cocker Spaniel | 14.5-15.5 in | 3/5         | 4/5        |
      | Poodle (Toy)   | <= 10 in     | 4/5         | 4/5        |
    question: |
      Which breed has the most energy?
    answer: |
      The breed with the most energy is the Labrador.
  - context: |
      | **Name** | **Date** | **Color** | **Letter** | **Number** |
      |----------|----------|-----------|------------|------------|
      | George   | Mar 5    | Green     | A          | 1          |
      | Gráinne  | Dec 31   | Red       | B          | 2          |
      | Abigail  | Jan 17   | Yellow    | C          | 3          |
      | Bhavna   | Apr 29   | Purple    | D          | 4          |
      | Rémy     | Sep 9    | Blue      | E          | 5          |
    question: |
      What is Gráinne's letter and what is her color?
    answer: |
      Gráinne's letter is B and her color is red.
  - context: |
      | Banana | Apple      | Blueberry | Strawberry |
      |--------|------------|-----------|------------|
      | Yellow | Red, Green | Blue      | Red        |
      | Large  | Medium     | Small     | Small      |
      | Peel   | Peel       | No peel   | No peel    |
    question: |
      Which fruit is blue, small, and has no peel?
    answer: |
      The blueberry is blue, small, and has no peel.
```

#### Grounded compositional skill: Directory tree example

```ascii
[...]

grounded
└── technology
    └── machine_learning
        └── natural_language_processing
    |   |     └── information_extraction
    |            └── inference
    |   |            └── qualitative
    |   |               ├── sentiment
    |   |               |     └── qna.yaml
    |   |               |         attribution.txt
    │                   ├── quantitative
    │   │                   ├── table_analysis <=== here it is :)
    │   |   |               |     └── qna.yaml
    │   │   │               |         attribution.txt

[...]
```

