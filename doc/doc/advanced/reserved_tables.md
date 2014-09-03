---
layout: default
---

# Internal database schema

The following tables are used internally by DeepDive. There can *not* be tables
with the same name in the database:


                                List of relations
     Schema |                     Name                     |   Type   
    --------+----------------------------------------------+----------
     public | dd_graph_variables_holdout                   | table    
     public | dd_graph_weights                             | table    
     public | dd_graph_weights_id_seq                      | sequence 
     public | dd_inference_result_variables                | table    
     public | dd_inference_result_weights                  | table    
     public | dd_inference_result_variables_mapped_weights | view     
     public | f_[RULE_NAME]_query_user                     | view     
     public | [TABLE]_[VARIABLE]_inference                 | view
     public | [TABLE]_[VARIABLE]_inference_bucketed        | view
     public | [TABLE]_[VARIABLE]_calibration               | view
     public | [TABLE]_[VARIABLE]_cardinality               | table
	
where `[RULE_NAME]` is the name of an inference rule, `[TABLE]` is the
name of a table that contain variables, and `[VARIABLE]` is the name
of variable in the corresponding table.

Description of each schema:

- `dd_graph_variables_holdout`: table that contains all variable ids that are used for holdout. Can be used for custom holdout by a [holdout query](../basics/calibration.html#custom_holdout).




- `dd_graph_weights`: table that contains all the materialized weights.

<!-- TODO (Feiran): how to describe dd_graph_weights? -->

- `dd_graph_weights_id_seq`: a sequence used in creating weights.

- `dd_inference_result_variables`: table that contains inference result (expectation) for all query variables.

- `dd_inference_result_weights`: a table that shows factor weight ids and learned weight values.

- `dd_inference_result_variables_mapped_weights`: a view that maps all distinct factor weights to their description and  their learned values. It is a commonly used view that shows the learned weight value of a factor as well as the number of occurences of a factor. (The schema name is probably misleading)

- `f_[RULE_NAME]_query_user`: a view that is defined by the input query of an [inference rule](../basics/inference_rules.html).

- `[TABLE]_[VARIABLE]_inference`: a view that maps variables with their inference results. It is commonly used for error analysis.

- `[TABLE]_[VARIABLE]_inference_bucketed`: a table that maps variables with their inference results, with expectations separated into 10 buckets. It is used for generating calibration plots.

- `[TABLE]_[VARIABLE]_calibration`: a view that has calibration statistics of a variable. Used in generating calibration plots.

- `[TABLE]_[VARIABLE]_cardinality`: a table that records the cardinality of given variable. Used by grounding.



<!-- TODO (Feiran) check if the tables are correct; check the above one line description for all tables written by Zifei. -->
