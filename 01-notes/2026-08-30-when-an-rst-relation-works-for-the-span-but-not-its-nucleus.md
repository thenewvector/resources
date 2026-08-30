# When an RST Relation Works for the Span but Not Its Nucleus

When I began [qualitatively inspecting](https://github.com/thenewvector/identifying-depression-with-rst/blob/main/reports/preliminary-report-solutionhood-topic-depr-rst.md) RST trees produced by two model variants of the same parser, I knew "strong nuclearity" is a thing, or rather that it _should_ be a thing.

Stede et al. (2017, Section 4.6.2) define the principle as follows:

> A segment that is considered as central for the text should be nuclear not only when linking it to its immediate neighbours, but the resulting larger segment should likewise be nuclear in its own context, and so forth. Seen the other way round, this means that a relation that holds between two large segments should in particular apply to the nuclei of these segments.

The way I understand this principle in a more limited sense (from a standpoint of just two or maybe three levels of hierarchically organized nodes) is as follows:

**When a complex span participates in a higher-level relation, its propagated nucleus should be the proposition that makes that relation coherent. Put differently, the higher-level relation should "obtain" between the propagated nuclei of its two spans rather than their satellites.**

The best way for me to really wrap my head around this principle was, however, discovering instances when it was "violated" in automatically produced RST trees that I analyzed closely for [my project](https://github.com/thenewvector/identifying-depression-with-rst).

In several inspected trees, a higher-level relation appeared plausible[^1] when I read the complete spans, but whenever I tested whether that same relation would still make perfect sense if I were to only isolate the nucleus of the node that makes up the span in question, it became more problematic. In other words, what I witnessed was that the proposition that would best license the higher-level interpretation was sometimes actually the satellite of the inner node making up one of the spans of this higher-level relation, while a different proposition was designated as the nucleus and therefore propagated upward.

One example from a document I inspected recently when pursuing the investigation of causal relations in the two competing sets of RST trees that I am using for my project was how a nested causal relation was represented in a tree produced by a `gumrrg`-based version of the parser (RRG). In a nutshell, the outer RRG `causal` relation was plausible because its right span contained the idea that the writer’s difficult personality caused difficulties in communicating with other people -- the state of affairs captured by the left span of this outer node. However, within that right span, the causal proposition about the writer’s personality was itself marked as a satellite. The inner nucleus was the resulting statement that communication was difficult (which in effect is a restatement of the state of affairs realized by the left span of the outer node). Consequently, the material that would make the outer span more interpretable as a cause did not propagate upward as the propagated nucleus largely restated the effect described in the outer nucleus (the left span). A synthetic representation is shown below.[^2]

```
[communication is difficult]N
    <--causal--
[[my personality is difficult]S
    --causal-->
[therefore communication is difficult]N]S
```

Similar examples were discovered in the analysis of `Solutionhood`. For example, a locally plausible question–answer node in a tree derived from the `rstreebank`-based version of the parser (RRT) was subsequently used as the question-side satellite of a larger `Solutionhood` relation, even though the local node’s propagated nucleus was the answer rather than the question (which is required by the constraints of `Solutionhood`). There were a number of other examples similar to this one in the samples analyzed qualitatively in this iteration of the project.

It's hard to say why an automatic parser makes a certain decision on nuclearity. Some may be explained by how a relation is normally assigned and the constraints that exist for this relation in the guidelines for a specific version of RST annotation. An example here is what has been mentioned above: `Solutionhood` in `rstreebank` (as well as in Stede et al. (2017)) only allows for one type of nuclearity where the satellite is the question or problem and the nucleus is the answer or solution. There are similar constraints on the `Cause-effect` relation in `rstreebank` (at least in the annotation guidelines): the satellite is always the cause and the nucleus is always the effect. Because `Solutionhood` and `Cause-effect` constrain which semantic role becomes nuclear, the parser cannot resolve such a conflict merely by reversing nuclearity while retaining the same analysis.

The case with the assignment of the `causal` relation in the RRG-derived tree above is less obvious because the `causal` relation in the inventory that the parser is using lumps two more finer-grained relations:

```
- causal-cause (→←): S is the cause of N
- causal-result (→←): S is the result of N
```

so technically, nuclearity could have been reversed to respect the strong nuclearity principle.

I do not yet know how these cases would be resolved in expert human annotation. An annotator might reverse the nuclearity assignment, change the higher-level relation, attach the span elsewhere, or segment the passage differently. I also do not yet know whether strong nuclearity is enforced equally strictly in the annotation frameworks underlying the two model variants, or whether the observed cases (at least the ones where theoretically there are no constraints on reversal of nuclearity as in the case of RRG's `causal`) are parser errors of some sort.

I take two things from these cases.

The first is methodological insight that full-span semantic plausibility in a relation and structural support from the nuclear path "underlying" the spans of the relation are not necessarily the same thing. I therefore distinguish two judgments in tree inspection: whether the relation is plausible between the complete spans and whether it remains plausible between their propagated nuclei.

The second is that the best way to understand a concept (like strong nuclearity) is to work with real data and actually witness how it's being sustained or overruled. (Shocking, I know /s)

 ## References

Mann, W. C., Matthiessen, C. M. I. M., & Thompson, S. A. (1992). Rhetorical Structure Theory and Text Analysis. _Discourse Description: Diverse Linguistic Analyses of a Fund-Raising Text_, 39–78.

Stede, M., Taboada, M., & Das, D. (2017). Annotation guidelines for rhetorical structure. _Manuscript. University of Potsdam and Simon Fraser University_. [https://www.sfu.ca/~mtaboada/docs/research/RST_Annotation_Guidelines.pdf](https://www.sfu.ca/~mtaboada/docs/research/RST_Annotation_Guidelines.pdf)

[^1]: The term "plausible" is used to emphasize the idea that an RST tree is not altogether arbitrary but not "definitive", either. Cf. "Since the analyst has access to the text, has knowledge of the context in which it was written, and shares the cultural conventions of the writer and the expected readers, but has no direct access to either the writer or other readers, judgments about the writer or readers must be plausibility judgments rather than judgments of certainty. That is, every judgment of the completed analysis is of the form, "_It is plausible to the analyst that..._". (Mann et al., 1992, pp. 50-51)

[^2]: These are "synthetic" generalized example statements that are somewhat similar to the ones that are found in the analyzed documents and just capture their gist but do not reproduce them exactly.