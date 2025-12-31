# Programming for Data Science

## Assessment Reflection

## Overview

# Part 1: PDS_CW_part1.ipynb

## Question 1.1: Reading in rows of a CSV file. 


### Q1.1 – Reading Data from a CSV File

The initial stage of the assignment focused on reading in data rows from a CSV file. This required careful handling of optional parameters such as row ranges while preserving the integrity of the dataset. Opening the file with newline='' ensured line breaks were interpreted correctly across platforms, and encoding='utf-8' guaranteed consistent decoding (Python Software Foundation, 2025).

One challenge I encountered was the presence of a Byte Order Mark (BOM) in the first column header which appeared as '\ufeffcancer' due to a hidden Byte Order Mark (BOM).This affected the processing of other fuctions in the subsequent questions. 

This was resolved by cleaning the header before returning the data ensuring consistency across subsequent questions. 
A strength of this approach was addressing data quality issues at the source, although more defensive checks could have been added to further improve robustness.

----------------------------------------------------------------------------------------------------------------------------------------

### Q1.2: Extracting Columns from the Dataset

This task built directly on the previous function by selecting specific columns and returning them in a dictionary structure. 

The dataset itself used lowercase column names, but the function included error handling to catch cases where the user might input an invalid column name, whether due to case sensitivity, typographical errors, or missing headers. This prevented the program from breaking. 

Reusing the CSV reading logic from Q1.1 reduced duplication and improved clarity.
A strength of this approach was robustness: it could safely handle unexpected user input while remaining functional for subsequent tasks like distance calculations or table generation.

A potential improvement for the csv_cols function would be to automatically convert numeric columns from strings to appropriate numeric types (int or float). This would improve the robustness of subsequent calculations, such as Euclidean distance, and reduce the need for repetitive type conversion elsewhere in the code

----------------------------------------------------------------------------------------------------------------------------------------

### Q1.3 – Computing Euclidean Distance

Calculating the Euclidean distance between two lists required careful validation of inputs. Ensuring that both lists were of equal length prevented logical errors during computation. Implementing the Euclidean distance function raised a decision about using math.sqrt() versus the built-in exponent operator (**0.5) the latter was chosen which allowed the function to remain simple and rely only on Python’s built-in features, aligning with the assignment brief of using only built-in Python functions and operators, avoiding unnecessary imports from the math library.

---------------------------------------------------------------------------------------------------------------------------------------

### Q1.4 – Calculating a Table of Pair-Wise Distances

This question involved combining earlier functions to compute pair-wise distance between columns. Iterating over column pairs while reusing the Euclidean distance function helped maintain modularity.

A key challenge was ensuring that all values were numeric before distance calculations, particularly when working with the full dataset. Once resolved, the function produced a symmetric distance table as expected. This was because of the dictionary returned by csv_cols stores all values as strings, and arithmetic operations like subtraction and exponentiation cannot be performed on strings. To resolve this, values were converted to floats before calling the Euclidean distance function:

```python

col1 = [float(x) for x in data[p]]
col2 = [float(x) for x in data[q]]

```

After this conversion, the function produced a symmetric distance table as expected, meaning the distance from column A to B is the same as from B to A  (Wikipedia, 2025). 

I made use of python nested loop to compute the distance table, but Python’s loops can become slow with large datasets. A potential improvement would be to use vectorized operations using libraries like NumPy to optimize speed, which perform mathematical computations on whole arrays at once rather than one element at a time (Harris et al., 2020; Van Der Walt et al., 2011).

----------------------------------------------------------------------------------------------------------------------------------------

### Q1.5 – Printing a Custom Distance Table

The final task focused on presenting the pair-wise distance results in a readable and structured format. Aligning columns and controlling spacing required experimentation with string formatting and column widths, as some column names initially appeared merged due to insufficient spacing. Introducing an optional column width parameter improved readability while keeping the function interface simple.

Rounding values and enforcing consistent spacing resulted in a clean, well structured table output. Separating the presentation logic from the distance calculations also improved flexibility, as changes to formatting could be made without affecting the underlying computations.



