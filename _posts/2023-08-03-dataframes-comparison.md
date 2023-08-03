# Analyzing CSV Concatenation and DataFrame Comparison Performance

## Introduction

Handling large datasets is a common challenge in data analysis and processing tasks. In this blog post, we will discuss our findings on comparing the performance of five different frameworks for concatenating CSV files into dataframes and analyzing their CPU consumption. The frameworks we evaluated are `go-dataframe` (Go), `gota` (Go), `pandas` (Python), `petl` (Python), and `pyspark` (Python).

## Task Overview

The task at hand involves three primary steps:

1. Reading multiple CSV files and converting them into dataframes.
2. Concatenating these dataframes into a single dataframe.
3. Writing the consolidated data back to an output file.

To compare the performance of these frameworks, we used benchmarking tools like Hyperfine and CMDBench. Hyperfine allowed us to measure the execution time for each framework, while CMDBench provided insights into the CPU and memory consumption during the task execution.

## CSV File Description

Before diving into the comparison, let's take a brief look at the structure of the CSV files we used for our analysis. These files contain records with columns such as `first_name`, `last_name`, `email`, `ssn`, `job`, `country`, `phone_number`, `user_name`, `zipcode`, `invalid_ssn`, `credit_card_number`, `credit_card_provider`, `credit_card_security_code`, and `bban`.

## CPU Consumption Analysis

We evaluated the CPU consumption of each framework for different scenarios involving varying numbers of CSV files with 100,000 records each. Below are the summarized results:

#### 2 Small Files
*(10 runs | 10 records each)*
| Framework | Mean [s] | Min [s] | Max [s] | Relative |
|:---|---:|---:|---:|---:|
| `go-dataframe` | 1.148 ± 0.081 | 1.070 | 1.288 | 7.74 ± 0.62 |
| `gota` | 0.752 ± 0.096 | 0.690 | 1.021 | 5.07 ± 0.68 |
| `pandas` | 0.485 ± 0.024 | 0.456 | 0.515 | 3.27 ± 0.20 |
| `petl` | 0.148 ± 0.006 | 0.137 | 0.156 | 1.00 |
| `pyspark` | 13.741 ± 2.424 | 11.671 | 20.077 | 92.61 ± 16.70 |

#### 2 Files
*(10 runs | 100,000 records each)*
| Framework | Mean [s] | Min [s] | Max [s] | Relative |
|:---|---:|---:|---:|---:|
| `go-dataframe` | 1.689 ± 0.089 | 1.579 | 1.874 | 1.00 |
| `gota` | 2.282 ± 0.130 | 2.124 | 2.507 | 1.35 ± 0.10 |
| `pandas` | 2.816 ± 0.100 | 2.693 | 2.997 | 1.67 ± 0.11 |
| `petl` | 2.294 ± 0.049 | 2.257 | 2.404 | 1.36 ± 0.08 |
| `pyspark` | 14.142 ± 0.643 | 13.850 | 15.927 | 8.37 ± 0.58 |


#### 5 Files
*(10 runs | 100,000 records each)*
| Framework | Mean [s] | Min [s] | Max [s] | Relative |
|:---|---:|---:|---:|---:|
| `go-dataframe` | 2.583 ± 0.204 | 2.349 | 3.086 | 1.00 |
| `gota` | 4.884 ± 0.316 | 4.462 | 5.374 | 1.89 ± 0.19 |
| `pandas` | 6.527 ± 0.349 | 6.209 | 7.235 | 2.53 ± 0.24 |
| `petl` | 8.117 ± 0.616 | 7.290 | 9.225 | 3.14 ± 0.34 |
| `pyspark` | 21.108 ± 2.345 | 18.462 | 26.281 | 8.17 ± 1.11 |


#### 10 Files
*(10 runs | 100,000 records each)*
| Framework | Mean [s] | Min [s] | Max [s] | Relative |
|:---|---:|---:|---:|---:|
| `go-dataframe` | 3.847 ± 0.253 | 3.585 | 4.280 | 1.00 |
| `gota` | 9.127 ± 0.231 | 8.828 | 9.450 | 2.37 ± 0.17 |
| `pandas` | 14.185 ± 1.546 | 12.161 | 15.737 | 3.69 ± 0.47 |
| `petl` | 24.496 ± 3.328 | 21.238 | 30.702 | 6.37 ± 0.96 |
| `pyspark` | 23.638 ± 0.915 | 22.122 | 24.999 | 6.14 ± 0.47 |

#### 25 Files
*(10 runs | 100,000 records each)*
| Framework | Mean [s] | Min [s] | Max [s] | Relative |
|:---|---:|---:|---:|---:|
| `go-dataframe` | 8.212 ± 0.559 | 7.521 | 9.105 | 1.00 |
| `gota` | 32.663 ± 1.640 | 30.131 | 35.154 | 3.98 ± 0.34 |
| `pandas` | 30.790 ± 0.572 | 30.060 | 31.684 | 3.75 ± 0.26 |
| `petl` | 107.274 ± 3.292 | 100.848 | 111.170 | 13.06 ± 0.98 |
| `pyspark` | 35.659 ± 0.719 | 34.524 | 37.100 | 4.34 ± 0.31 |


#### 50 Files 
*(5 runs | 100,000 records each)*
| Framework | Mean [s] | Min [s] | Max [s] | Relative |
|:---|---:|---:|---:|---:|
| `go-dataframe` | 16.669 ± 1.990 | 14.858 | 19.575 | 1.00 |
| `gota` | 91.149 ± 4.158 | 88.691 | 98.500 | 5.47 ± 0.70 |
| `pandas` | 60.217 ± 2.036 | 58.558 | 62.916 | 3.61 ± 0.45 |
| `pyspark` | 65.071 ± 1.078 | 64.086 | 66.612 | 3.90 ± 0.47 |

#### 100 Files
*(5 runs | 100,000 records each)*
| Framework | Mean [s] | Min [s] | Max [s] | Relative |
|:---|---:|---:|---:|---:|
| `go-dataframe` | 26.075 ± 0.522 | 25.426 | 26.518 | 1.00 |
| `pandas` | 116.856 ± 0.334 | 116.315 | 117.220 | 4.48 ± 0.09 |

## Memory Consumption Analysis

For the memory consumption analysis, we created graphs using CMDBench. Here are the key insights:

#### 2 Files
*(100,000 records each)*
| go-dataframe | gota | pandas | petl | pyspark |
|---|---|---|---|---|
| ![go-dataframe](https://i.ibb.co/CwQHfqt/go-dataframe.png) | ![gota](https://serv1.dragndropz.com/user_images/2023_07_03/8283_URj6u2_gota.png) | ![pandas](https://serv1.dragndropz.com/user_images/2023_07_03/8284_ebMsVN_pandas.png) | ![petl](https://serv1.dragndropz.com/user_images/2023_07_03/8285_72MTkJ_petl.png) | ![pyspark](https://i.ibb.co/P6d9fv8/pyspark.png) |


#### 5 Files
*(100,000 records each)*
| go-dataframe | gota | pandas | petl | pyspark |
|---|---|---|---|---|
| ![go-dataframe](https://i.ibb.co/tsG0WDn/go-dataframe.png) | ![gota](https://i.ibb.co/8gMR1JP/gota.png) | ![pandas](https://i.ibb.co/mSvtQbw/pandas.png) | ![petl](https://i.ibb.co/bBgyM5S/petl.png) | ![pyspark](https://i.ibb.co/hY2T1c7/pyspark.png) |


#### 10 Files
*(100,000 records each)*
| go-dataframe | gota | pandas | petl | pyspark |
|---|---|---|---|---|
| ![go-dataframe](https://i.ibb.co/19v4Wr9/go-dataframe.png) | ![gota](https://i.ibb.co/Rhc2f70/gota.png) | ![pandas](https://i.ibb.co/NCzspqQ/pandas.png) | ![petl](https://i.ibb.co/0c6wFMk/petl.png) | ![pyspark](https://i.ibb.co/6ggkr0D/pyspark.png) |

#### 25 Files
*(100,000 records each)*
| go-dataframe | gota | pandas | petl | pyspark |
|---|---|---|---|---|
| ![go-dataframe](https://i.ibb.co/b3VvJq7/go-dataframe.png) | ![gota](https://i.ibb.co/x3R0v6k/gota.png) | ![pandas](https://i.ibb.co/2ZthrZR/pandas.png) | ![petl](https://i.ibb.co/xqTwRkW/petl.png) | ![pyspark](https://i.ibb.co/Sfbpc9x/pyspark.png) |

#### 50 Files 
*(100,000 records each)*
| go-dataframe | gota | pandas | petl | pyspark |
|---|---|---|---|---|
| ![go-dataframe](https://i.ibb.co/tHtJxhN/go-dataframe.png) | ![gota](https://i.ibb.co/NYzNH1W/gota.png) | ![pandas](https://i.ibb.co/QMdp4JG/pandas.png) | ![petl](https://i.ibb.co/rZ08W2H/petl.png) | ![pyspark](https://i.ibb.co/YymBQ4p/pyspark.png) |

#### 100 Files
*(100,000 records each)*
| go-dataframe | pandas |
|---|---|
| ![go-dataframe](https://i.ibb.co/r0n8jvC/go-dataframe.png) | ![pandas](https://i.ibb.co/kK54wNh/pandas.png) |

## Conclusion

From our analysis, we can draw several conclusions:

1. For small datasets, `petl` outperforms all other frameworks in terms of CPU consumption, closely followed by `pandas`.
2. As the dataset size increases, `pyspark` consistently shows the highest CPU consumption, making it less suitable for large datasets in a single-node setup.
3. Overall, `go-dataframe` outperforms all other frameworks in terms of CPU and memory consumption

Choosing the right framework depends on the specific requirements of your task, including dataset size, available resources, and the desired level of parallelization. We hope this analysis helps you make an informed decision when working with CSV concatenation and dataframe comparison tasks. Happy data processing!