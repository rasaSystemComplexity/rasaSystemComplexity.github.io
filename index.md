Machine learning (ML) enabled systems are emerging with recent breakthroughs in ML. A model-centric view
is widely taken by the literature to focus only on the analysis of ML models. However, only a small body of work takes
a system view that looks at how ML components work with
the system and how they affect software engineering for ML enabled systems. In this paper, we adopt this system view, and
conduct a case study on Rasa 3.0, an industrial dialogue system
that has been widely adopted by various companies around the
world. Our goal is to characterize the complexity of such a largescale ML-enabled system and to understand the impact of the
complexity on testing. Our study reveals practical implications
for software engineering for ML-enabled systems.
## RQ1: System Complexity Analysis
RQ1 is **how ML componentsare adopted across the modules in Rasa?**
It aims to identify ML components in Rasa and broadly view them from the perspective of dependent libraries and ML models.

## RQ2: Interaction Complexity Analysis
RQ2 is **how ML components interact with other components in Rasa?**
It aims to summarize a comprehensive taxonomy of component interaction patterns. 

<!-- readme of each RQ to describe the column meaning -->
All 43 interaction patterns and 230 instances are available [here](https://rasasystemcomplexity.github.io/blob/main/data/component_interaction.xls)

## RQ3: Component Complexity Analysis
RQ3 is **how the code of ML components is composed by what kinds of code?**
It aims to inspect the source code inside every component to characterize the statistics and composition patterns of different code categories, including data processing code, model usage code, etc. 
All the labeled code snippets are available [here](https://rasasystemcomplexity.github.io/blob/main/data/rq3/code_category.xls)

<!-- func_call meaning, detail data processing type codebook, interaction pattern analysis -->
<!-- todo: composition pattern details -->
## RQ4: Testing Practice Analysis
RQ4 is **how is the characteristic of test cases, and how well they cope with the complexity?**
It aims to quantitatively assess Rasa's test cases from code coverage, test case statistics (i.e., granularity levels, oracletypes, and ML stages), and component interaction coverage perspectives. Further, for the survived mutants, we train Rasa with 3 default configuration files on MutiWoz, a widely used multi-domain TDS dataset. 
We calculate the statistical significance between the performance metrics from mutated Rasa code with metrics from pipelines trained with clean code.

The labeled test cases are [here](https://rasasystemcomplexity.github.io/blob/main/data/rq4/test_case_label.csv), code coverage data is available [here](https://rasasystemcomplexity.github.io/blob/main/data/rq4/test_case_coverage.csv), and interaction patterns coverage data is available [here](https://rasasystemcomplexity.github.io/blob/main/data/component_interaction.xls).

<!-- check test case label number(oracle, stage, granularity and corresponding in rq5) -->


## RQ5: Mutation Testing Analysis
RQ5 is **how is the bug-finding capability of test cases and test data (i.e., the data for testing models), and how well they cope with the complexity?**
It aims to generate mutants (i.e., artificial bugs) and check whether these mutants can be killed (i.e., detected) by test cases. 

Mutmut mutants and Deepcrime mutants and corresponding running results are available [here](https://rasasystemcomplexity.github.io/blob/main/data/rq5/mutmut_mutants.json), and [here](https://rasasystemcomplexity.github.io/blob/main/data/rq5/deepcrime_mutants.json), respectively. 

<!-- add deepcrime exact modified line -->

<!-- steps to reproduce mutants (fix rasa test case first, todo: run mutmut mutants and deepcrime mutants) -->
<!-- mutation status, killed, survived
mutation test data killed, metrics, degradation -->
