# Direction to Annotate using PULSAR-rules


## Installation an

0. Download `mae-2.2.4-fatjar.jar`, from https://github.com/keighrim/mae-annotation/releases

1. Open the java interface at the terminal:
`java -jar mae-2.2.4-fatjar.jar`

2. Open the document-type definition file by going to file menu, then select "New Task Definition", and find `PULSARv2.dtd`.

3. Then open the file to annotate, by going to file menu again, selecting "Open Document" and selecting your next document.



## Goals

The goals are to mark up human rights reports so that we can identify what aspects of human rights are being judged over time, as well as who are the perpetrators, victims and sources of information.


### Tagging Chucks of Contiguous Text as Entities

For our purposes text can serve five different relevant purposes. It can signal:

1) what aspects of human rights are being discussed in a given sentence, 
2) what judgements, if any are being offered in a sentence
3) who the perpetrator of any violations is
4) who the victim is of any violations
5) what the source of information is for a judgement

Each of these five purposes is considered an *entity*. 


### Tagging Links Between Entities

In addition, we want to identify connections between these chunks of text. Specifically, we want to be able to identify links:

1) between a judgement and the aspect of human right the judgement is offered on
2) between the perpetrator judged and the judgement of their action
3) between the victim of a judged action and the judgement
4) between the souce of information for a judgement and the judgement

These are each types of relations are *links*.


### Examples


#### Some Specific cases

- Judgements are often verb phrases and aspects noun phrases that include human rights terms, and perpetrators or victims are noun phrases with people as the root of the terms. For example the sentence: 
```
Security forces committed politically motivated killings.
```

has `politically motivated killings` as the aspect, `committed` as the judgement, and `Security forces` as the perpetrator. It then has a __FromPerpetratorToJudgement__ link (`Security forces`,`committed`) and a __FromJudgementToAspect__ link (`committed`,`politically motivated killings`). If a specific person or proper noun is named, that is not an abstract aspect of human rights that is being violated or protected, but instead is usually a victim or a perpetrator. 

- If is important to keep judgement words, like `unlawful`, `arbitrary`, `intense` and `severe` in the judgement expressions. 

- Some expressions are both an aspect and a judgement at once in a sentence. In the phrase: `Abuses included killing`, `killing` is both the aspect (within physcial integrity rights) and the judgement, they did it, although that is implied. There is a special extent tag for this: JointJudgementAspectExpression.

- Sentences with `of' can be confusing because the judgement and aspect are often connected in an ambiguous way. In this example: `Civilian authorities did not maintain effective control of the security forces.` One could think of the `security forces` as the aspect, then the the judgement is `did not maintain effective control of`.  Alternatively, one could think of `control of the security forces` as the aspect and then the judgement would be `did not maintain effective`. In this case, the second coding is slightly preferable, but only because `control of the security forces` is a common phrase and security forces are groups that are more likely to be perpetrators. The `civilian government` is the perpetrator.

- Related to the previous point, keep the phrase `rule of law` together. It is a multiword expression.

- When there are two prepositions, as in `obstruction of the work of nongovernmental organizations (NGOs)`, it is important to focus on the verb, here what is being obstructed is some part of an NGO, so `the work of nongovernmental organizations (NGOs)` is the aspect and the judgement is `obstruction of`.

- Perpetrators in this coding scheme do not alway do negative things. You can perpetrate a protection or a peace accord. Perpetrators are the cause of an effect.

- Conversely, victims are the effected party. 

- Include articles or adjectives in a tag if they would be left dangling ("<The executive>", "the legislature", "severly violated"). This is particularly important when an adjective intensifies or modifies other words within that expression, as in the last example in the previous sentence. 

- Code as much as possible. The sentence:
`In may, rebels crossed from Sudan into the east of the country and attacked` could be mistaken for an EventFact tag, but since it involves physical security, `attacked` is an JointAspectJudgement. In that case, the perpetrator is the rebels, so this is not an EventFact, as the sentence includes a judgement that something happened to influence physical security.

- Judgements can involve more than one actor. The sentence `one of the main rebel factions signed a peace accord with the government` includes the judgement expression `signed` and the aspect expression `peace accord` since this is related to physical security. The perpetrators in this case are the rebel groups, since they signed, and the government. So there should be Perpetrator tags on those two actors and FromPerpetratortoJudgement links for each of rebel groups and government to the judgement expression `signed`.

- Some aspects always imply a set or group of victims, like `child soldiers`, these victims do not need to be tagged separately. So in the phrase, `the use of child soldiers`, `child soldiers` is the aspect expression and `use of` is the judgement.

- The phrasing of `reports` is tricky. A common phrase is `There were reports of` or `There were no reports of`. In these cases, `were reports` or `were no reports of`, if they are the only judgement-like expressions in the sentence, should be coded as the judgements, and then `reports` also tagged as the source of the information. Care needs to be taken when linking the correct parts of these instances.

- When two actors are mentioned with an `and` then include them as seperate entities, and with their links. If two actors are mentioned with an `or` then they should be joined as one extent, since we do not know which one should be used (`or` does not equal both).

- You can use discontinuous extents when necessary. For example, when there is one judgement that is split across the beginning and the end of a sentence.


#### Questions for future

- There are old event in the text. References to past years. Should we have an *old* tag.

- Some sentences have extensive details about an aspect, in particular. Should allo this be included in an aspect, or should be have to different aspect codings. One for the core abstract aspect and another for the details, and then a link between them? Is this just added complexity?



