Machine learning (ML) enabled systems are emerging with recent breakthroughs in ML. A model-centric view
is widely taken by the literature to focus only on the analysis of ML models. However, only a small body of work takes
a system view that looks at how ML components work with
the system and how they affect software engineering for ML enabled systems. In this paper, we adopt this system view, and
conduct a case study on Rasa 3.0, an industrial dialogue system
that has been widely adopted by various companies around the
world. Our goal is to characterize the complexity of such a largescale ML-enabled system and to understand the impact of the
complexity on testing. Our study reveals practical implications
for software engineering for ML-enabled systems.Our data are available at [here](https://zenodo.org/record/7844906#.ZD-w985ByUk).
## RQ1: System Complexity Analysis
RQ1 is **how ML componentsare adopted across the modules in Rasa?**
It aims to identify ML components in Rasa and broadly view them from the perspective of dependent libraries and ML models.

## RQ2: Interaction Complexity Analysis
RQ2 is **how ML components interact with other components in Rasa?**
It aims to summarize a comprehensive taxonomy of component interaction patterns. 

<!-- readme of each RQ to describe the column meaning -->
All 43 interaction patterns and 230 instances are available [here](https://github.com/rasaSystemComplexity/rasaSystemComplexity.github.io/blob/main/data/component_interaction.xls).
The `Compo0` and `Comps` column describe the components involved in the interaction instance.
The `test_coverage` column means: (1) `0`, the instance is not covered in Rasa test cases; (2) `1`, the instance is covered in Rasa test cases; (3) `-1`, the instance should not be considered in test coverage analysis, e.g. components in the interaction instance should not be used together.

## RQ3: Component Complexity Analysis
RQ3 is **how the code of ML components is composed by what kinds of code?**
It aims to inspect the source code inside every component to characterize the statistics and composition patterns of different code categories, including data processing code, model usage code, etc. 

All the labeled code snippets are available [here](https://github.com/rasaSystemComplexity/rasaSystemComplexity.github.io/blob/main/data/rq3/code_category.xls).
The `code category` column describes the code category of the code snippet.
The `detail data processing type` column describes the detail type of data pre-processing and data post-processing code snippets.
The `call_type` column means: (1) `method definition`, the code snippet is a method definition snippet; (2) `anonymous method call`, the code snippet does not explicitly call a method, i.e. it is only a part of a method; (3) `external method call`, the code snippet calls a external method;
(4) `self class method call`, the code snippet calls a method defined in its own class; (5) `parent class method call`, the code snippet calls a method defined in its parent class; (6) `child class method call`, calls a method implemented in its child class.

The codebook of all 4 higher-level and 34 inner-level data processing types is available [here](https://github.com/rasaSystemComplexity/rasaSystemComplexity.github.io/blob/main/data/rq3/data_processing_codebook.xlsx).

<!-- func_call meaning, detail data processing type codebook, interaction pattern analysis -->
<!-- todo: composition pattern details -->
## RQ4: Testing Practice Analysis
RQ4 is **how is the characteristic of test cases, and how well they cope with the complexity?**
It aims to quantitatively assess Rasa's test cases from code coverage, test case statistics (i.e., granularity levels, oracletypes, and ML stages), and component interaction coverage perspectives. Further, for the survived mutants, we train Rasa with 3 default configuration files on MutiWoz, a widely used multi-domain TDS dataset. 
We calculate the statistical significance between the performance metrics from mutated Rasa code with metrics from pipelines trained with clean code.

The labeled test cases are [here](https://github.com/rasaSystemComplexity/rasaSystemComplexity.github.io/blob/main/data/rq4/test_case_label.csv), code coverage data is available [here](https://github.com/rasaSystemComplexity/rasaSystemComplexity.github.io/blob/main/data/rq4/test_case_coverage.csv), and interaction patterns coverage data is available [here](https://github.com/rasaSystemComplexity/rasaSystemComplexity.github.io/blob/main/data/component_interaction.xls).

<!-- TODO: check test case label number(oracle, stage, granularity and corresponding in rq5) -->


## RQ5: Mutation Testing Analysis
RQ5 is **how is the bug-finding capability of test cases and test data (i.e., the data for testing models), and how well they cope with the complexity?**
It aims to generate mutants (i.e., artificial bugs) and check whether these mutants can be killed (i.e., detected) by test cases. 

Mutmut mutants and Deepcrime mutants and their running results on test cases are available [here](https://github.com/rasaSystemComplexity/rasaSystemComplexity.github.io/blob/main/data/rq5/mutmut_mutants_test_case.json), and [here](https://github.com/rasaSystemComplexity/rasaSystemComplexity.github.io/blob/main/data/rq5/deepcrime_mutants_test_case.json), respectively. 
The `status` field means: (1) `ok_killed` and `bad_timeout`, the mutant is killed (i.e. detected) by test cases; (2) `bad_survived`, the mutant is not killed by test cases.
The `test_case_cmd` field describes the pytest command used to check the mutant, which consists of the test cases executed.
The `test_case_res` field describes the execution results of each test case in test case command, including the status and name of all test cases, and error type, error message of killed test cases.

The running results of mutants on test data are available [here](https://github.com/rasaSystemComplexity/rasaSystemComplexity.github.io/blob/main/data/rq5/mutmut_mutants_test_data.csv) and [here](https://github.com/rasaSystemComplexity/rasaSystemComplexity.github.io/blob/main/data/rq5/deepcrime_mutants_test_data.csv).
The `impactedConfig` column describes the impacted configuration files of the mutant, and all three default configuration files are available [here](https://github.com/rasaSystemComplexity/rasaSystemComplexity.github.io/tree/main/data/rq5/config).
The `impactedInNlu` and `impactedInCore` columns describe whether the mutant impact NLU/Policy or not.
The `isKilled` column describes whether the mutant is killed by test data.
The `entity_extractor_f1_deg`, `intent_classifier_f1_deg` and `policy_f1_deg` columns describe the performance degration caused by the mutant on EntityExtractor, IntentClassifier and Policy, respectively.
<!-- The `instance_value` describes the parameter specified by pytest to enable  -->

<!-- add deepcrime exact modified line -->

<!-- todo: steps to reproduce mutants (fix rasa test case first, todo: run mutmut mutants and deepcrime mutants) -->
<!-- mutation test data killed, metrics, degradation -->
