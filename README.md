# Data and results of the MCCBPP experiments

This repository hosts the files backing up the data and experimental results described in our paper Lower Bounds and Heuristics for the Multi-Class Constrained Bin Packing Problem.
The paper is now under revision. A link to it will be provided as soon as possible.

If you have any questions, please feel free to reach out to **baptiste.coutton@gmail.com**


## Data

The CSV files that describe the instances are found in the `instances` folder. There is then one folder for each of the three sets described in the paper: `set1`, `set2`, and `set3`.
In `set2` and `set3`, you will find some sub-folders that further partition the instances. In `set2` there is one subfolder per number of classes, and in `set3` there is one subfolder per combination of volume distribution and correlation between the class capacities and the number of class colors. So, for example, `set3_t1_corr` contains the instances of type T1 where the class capacities are correlated to the number of class colors. 


### The instance folder structure

Then, each individual instance has its own folder. It contains three files: `items.csv`, `bin_types.csv`, and `classes.csv`. Let's describe each of them.

- `items.csv`: This file contains the information about all the items in the instance.  One row corresponds to one item and holds its descriptive attributes. The first column (`volume`) is the item's volume. There is then one column per class (`class_c`, with *c* the class id), and in each column is the item's color for the corresponding class.
The ID of an item is the number of its row in this file.  

- `bin_types.csv`: This file contains the information about the bin types, and is sufficient to then generate the bins individually. One row corresponds to one bin type. The first column (`bin_capacity`) gives the bin type's volume capacity. The second column (`count`) tells how many bins of that type are in the instance. The third column (`cost`) is the bin type's cost.
When creating the bins, we give an ID to each of them. Bins are generated by increasing order of bin type. So if there are for example two bin types (named type 1 and type 2), with 30 bins of type 1 and 10 bins of type 2, the bins of type 1 will have IDs going from 0 to 29 and bins of type 2 will have IDs going from 30 to 39.

- `classes.csv`: This file contains information about classes. One row corresponds to one class. The first column (`class`) indicates which class we are considering. The second column (`colors`) indicates how many colors exist for the class. The third column (`capacity`) is the class's capacity.


### How to read an instance ID

The three instance sets were generated independently by different authors and use distinct naming conventions for their instance directories. We decided to preserve these conventions, and now provide a guide on how to read them.

**Set 1** 

This set was generated by Anand and Guericke (2020). An instance will be named for example `ID2_I100_C120_ALPHA1.41_BETA6.6_U0.1_UB5_R1`
- `ID2` means that this is the second instance randomly generated with the parameters that follow
- `I100` means that there are 100 items in the instance
- `C120` means that there are 120 bins in the instance
- `ALPHA1.41_BETA6.6` means that the *alpha* and *beta* parameters of the beta-distribution used to generate the volume of items are 1.41 and 6.6, respectively
- `UB5` means that the class capacity is 5 for each class
- `R1` means that there is 1 class in the instance

**Set 2**

This set was generated by Borges et al. (2020). An instance will be named for example `Q2C1N3B2W2_1_BPP`. 
- `Q2` gives the number of colors of the first class (as this set was originally designed with one class, only this class has its information in the instance ID). There are three possible values: `Q1` corresponds to 10 colors, `Q2` corresponds to 25 colors, and `Q3` corresponds to 50 colors.
- `C1` gives the capacity of the first class. There are again three possible values: `C1` corresponds to 2, `C2` corresponds to 3, and `C3` corresponds to a number that is either 2 or the average number of items per bin in the classical BPP solution (see the paper for more details)
- `B2` gives the bin volume capacity. Once again there are again 3 possible values: `B1` corresponds to 100, `B2` corresponds to 150, and `B3` corresponds to 200.
- `W2` gives the distribution of the items' volumes were sampled from. In our paper, we have used those distributions to define four instance types. Based on this correspondence, replacing W with T gives the instance's type. So in this case, `W2` means that the instance is of type T2.
- `_1`  means that this is the second instance randomly generated with those parameters (indexation starts at 0 for this set).

The other elements of the instance ID do not bear useful information.

**Set 3**

This set was generated for this paper. Information about the instance type and the correlation between the number of colors and the class capacity is found in the sub-folder names. An instance will then be named for example `I500_C4_6`.
- `I500` means there are 500 items in the instance
- `C4` means there are 4 classes in the instance
- `_6` means this is the sixth instance randomly generated with those parameters  


## Results

The results CSV files are found inside the `results` folder. They are divided between `lower_bounds` and `heuristics`. 

### Lower bounds 

In `lower_bounds`, you will find for each set:
- a file with the results of Column Generation results (files `colgen_*`)
- one file with the results of the compact formulation's relaxation solved using Gurobi (files `gurobi_lp`).

A file contains the results of all the instances in the set. For each instance, we report the number of items and classes, as well as the instance's type (column `type`) for Sets 2 and 3 (this value is always 1 for Set 1, as there is no instance type). 

### Greedy heuristics 

In `heuristics/greedy`, you will find for each set the results of all the greedy heuristics for each instance of the set. 

### ALNS 

In `heuristics/alns`, you will find for each set:
- a file with the results of the 10 ALNS runs for each instance of the set (files `alns_*`)
- a file with only the best solution for each instance (files `best_alns_*`). 

In both cases, you will find the results of the 5-minute and 1-hour runs. 

We also provide the detail of the best solution found by the 1-hour ALNS for each instance. The files are found in `heuristics/alns/detail`. There is one folder per instance (sub)set. A file indicates to which bin an item is assigned, using the item and bin ID systems described above.
