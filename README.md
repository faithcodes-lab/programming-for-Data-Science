## Assessment Reflection

# Part 1: PDS_CW_part1.ipynb

### Q1.1:  Reading Data from a CSV File  

Reading the csv rows with optional row parameters was straightfowrd, but handling the BOM character and row indexing was challening. I transitioned from using the csv module to parsing manually with enumerate(), which made indexing clearer and solved the BOM (Byte Order Mark) issues with utf-8-sig encoding which ensure consistent csv reading across systems.  Adding try except blocks improved error handling, and improving my code from basic test code to using: 

```python 
if __name__ == "__main__":
```
enabled testing code without pytest and this was used in subsequent questions.


### Q1.2: Extracting Columns from the Dataset 

In the initial approach, I looped through each column using list comprehension but was inefficient due to multiple rows iteration. 
I improved the version to use zip(*) to efficiently structure the data.

I added validation checks to ensure all requested columns exist before processing, which handled extreme cases of empty data by returning a dictionary with empty lists.

The use of f-strings in error messages improved clarity by showing which specific column was missing.
Key takeaways include learning how zip() can efficiently structure data, validating inputs early should happen before processing to avoid wasted computation, and reusing existing functions promote modularity and reduce code duplication. 


### Q1.3: Computing Euclidean Distance  
In this task incorrectly added the import math module in the function, which violated the coursework instruction, but was replaced and i made use of (** 0.5) the equivalent.

I made improvements by transiitioning from list comprehensiom and sum() to an iterative approach which manually accumulate (sum_sq_diff).

This allowed better control over converting data types because CSV files are read as strings and this would throw an error in the calculation phase. The input validation for equal length was consistent in both versions as it's essential during the mathemtical operation. 

### Q1.4 – Calculating a Table of Pair-Wise Distances  

Computing pairwise distances was done using nested loops and re using the euclidean_distance() function. The main challenge was handling data type, the initial version was converting strings to floats inside the loops, which was redundant. 

The updated version relies on using euclidean_distance() for converting and creating the distance matrix to improve readability. 

### Q1.5 – Printing a Custom Distance Table 

I refactored my code from allowing optional column width to a fixed width, add space for alignment, including row labels, and reducing decimals from 4 to 2 for cleaner output. The main improvement was making the table more readable by adding both column and row headers, which makes it easier to identify which columns are being compared.

I had issues with overlapping names in the table but resolved it by editing the column width, formatting good tables requires balancing width precision with readability which significantly improve table interpretation.  


# Part 2: PDS_CW_part2.ipynb

### Q2.1: Explore the dataset
Making use of pandas and seaborn for data exploration made the work flow seamless. Just one challenge I encountered was trying to plot a grouped bar plot of multiple disorders by country. I was able to resolved it by using the melt() funcion.    

### Q2.2: Detect and Remove outliers 

Detecting outliers wasnt an issues for me, but making the decision of keeping or dropping these points was conflicting for me. I had a thousand rows of outliers to drop but theses points are valid data points that reflects extreme mental health conditions in that region/entity. 
From a data scientist point of view, dropping that amount seems to violate data handling principles. To maintain data integrity while following the course work instructions, I narrowed  down the outlier removal to my interesting patterns (anxiety and depression), removing a total of 222 rows instaed of a thousnad rows.


### Q2.3 Hypothesis Testing
Making use of the filtered dataset which was suitable for correlation analysis test, this task was straightforward and easy to provide interpreataion to the results of the test. Implementation was simplied and results showed a significant correlation validating findings from q2.1.    

### Conclusion
This tasks was highly interractive as it took me through each phase of data science data handling process, from using only python inbulit function to using external libraries for exploratory data analysis, to data cleaning, data validation and hypothesis testing to support insights.


### AI Usage statement

- Chatgpt (Open AI, 2026) was consulted specifically in Q1.1 to debug BOM character issue when reading csv files and q2.1 in un derstanding how to use the melt() function in grouping data using a grouped barplot.

- The AI suggested using utf-8-sig encoding, which I then reasearched in pythons documentation to understand how it works.

- For Q2.1 I was directed  to pandas documentation (V2.33) where i studied how to use the function for data visualisation.

- The AI solutions was tested with the provided dataset to ensure that it was correctly handled, validated and adapted to meet the coursewrok requiremnet. 

- All other codes and analysis were developed independently based on course materials, python and pandas documentation.

### Refereneces

Pandas Development Team (2026) pandas.melt — pandas documentation. Available from: https://pandas.pydata.org/docs/reference/api/pandas.melt.html [Accessed 9 January 2026]

Python Software Foundation (2026) Unicode HOWTO. Available from: https://docs.python.org/3/howto/unicode.html [Accessed 19 December 2025]

Python Software Foundation (2026) codecs — Codec registry and base classes. Available from: https://docs.python.org/3/library/codecs.html [Accessed 19 December 2026]
