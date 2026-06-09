# Detailed-data-of-computing-performance-of-three-systems-under-FST-based-method
This repository contains the detailed computational results for three test systems under an FST-based method. Each Excel file records the solving performance for 100 load scenarios and the corresponding thread-level results.

## Files

| File | System | Load IDs | Threads per load | Data rows |
|---|---|---:|---:|---:|
| `Case_study_results_detail_Practical System.xlsx` | Practical system | 0-99 | 2 | 300 |
| `Case_study_results_detail_Polish.xlsx` | Polish system | 0-99 | 10 | 1100 |
| `Case_study_results_detail_RTS.xlsx` | RTS system | 0-99 | 2 | 300 |

Each workbook contains one worksheet named `results`.

## Row Definition

Each row represents the result of one thread under one load scenario.

The `Load_ID` column identifies the load scenario. The valid range is `0-99`.

The `Thread_ID` column identifies the thread or FST setting used for the corresponding load:

| Thread label | Meaning |
|---|---|
| `Cluster_0`, `Cluster_1`, ... | Cluster-based FST threads for the same load scenario |
| `CommonFST` | The common FST setting for the same load scenario |

For each `Load_ID`, the rows with different `Thread_ID` values belong to the same load scenario and should be compared within that group.

## Column Definition

| Excel column | Header | Meaning |
|---|---|---|
| A | `Load_ID` | Load scenario index. The range is `0-99`. |
| B | `Thread_ID` | Thread label, such as `Cluster_0` or `CommonFST`. |
| C | `Obj_Base` | Objective function value from the original full optimization model. |
| D | `Obj_Thread` | Objective function value obtained by the corresponding fixing schemes after fixing variables. |
| E | `Is_Optimal` | Whether the result of this thread is regarded as optimal. `TRUE` means the thread result is optimal for the corresponding load scenario. |
| F | `Fixed_Vars` | Number of fixed variables in the corresponding thread. |
| G | `Root_Relax_Time` | Root relaxation time, in seconds. |
| H | `Fixed_Solve_Time` | Solving time after fixing variables, in seconds. |
| I | `Method_Total_Time` | Total time of the FST-based method, in seconds. It is calculated as `Root_Relax_Time + Fixed_Solve_Time`. |
| J | `Original_Solve_Time` | Solving time of the original full optimization model, in seconds. |
| K | `Speedup` | Speedup of the corresponding thread. It is calculated as `Original_Solve_Time / Method_Total_Time`. |
| L | `Max_Opt_Speedup_By_Load` | For the same `Load_ID`, the maximum `Speedup` among non-`CommonFST` threads whose `Is_Optimal` value is `TRUE`. |
| M | `FST_Speedup_By_Load` | For the same `Load_ID`, the `Speedup` of the `CommonFST` row. |

## Formula Summary

For each row:

```text
Method_Total_Time = Root_Relax_Time + Fixed_Solve_Time
Speedup = Original_Solve_Time / Method_Total_Time
```

For each load scenario:

```text
Max_Opt_Speedup_By_Load = max(Speedup of Cluster_* rows with Is_Optimal = TRUE)
FST_Speedup_By_Load = Speedup of the CommonFST row
```
## Precautions
Due to the numerical problem of the solver, when the difference between the objective function obtained by the fixing schemes and the optimal objective function is within 10, it is considered to have reached the optimal value
