# Lab 6: Association Rule Mining with Apriori and FP-Growth

### Name: Nischal Joshi 																													
### Course: Advanced Data Mining and Big Data																				
### Date: July 19, 2025	

# Objective

The objective of the lab is to explore the association rule mining using the Apriori and FP-Growth Algorithm on the trancational book rating data. The idea is to identiy the frequent itemset and generate a meaning ful association rules and visualize the patterns to identify any hidden relationships.

## Dataset Used

The dataset being used is Book-Crossing Dataset from Kaggle. It includes 3 csv files for user demographics, book metadata and ratings for the books. The datasets were merged and preprocessed and further the user bok and rating interactions were transformed into a transcational format for the mining purpose

## **Data Cleaning**

* For data cleaning firstly the duplicated datas were removed.
* The implicit rating i.e. rating < 0 is also removed.
* The Age column is converted to numeric values, coercing any invalid or non-numeric entries to NaN
* Rows with missing or invalid age values are dropped.
* Only rows where the age is between 5 and 100 (inclusive) are kept to ensure reasonable age data for analysis.

## **Data Visualization**

The project includes two key visualizations being used bar chart and the heat map

* The horizontal bar chart highlights the 10 books with the highest number of ratings.
  * **Key Observations:**
    * *Wild Animus* stands out as the most rated book, with over 400 ratings.
    * Other popular titles include The Lovely Bones: A Novel and The Da Vinci Code, which also receive a large number of user ratings.Item Co-occurrence Heatmap (Top 10 Items)

- A heatmap illustrates how often the top 10 most rated books are co-rated by users (item co-occurrence).
  - **Key Observations:**
    - The diagonal elements of the heatmap are all 0, which indicates that a book’s co-occurrence with itself is explicitly excluded from this metric.
    - Despite the diagonal zeros, many off-diagonal cells have a value of 1 which shows that certain book pairs are **frequently rated together** by users
    - *The Lovely Bones: A Novel* shows strong co-occurrence with several other top books, including *The Da Vinci Code* and *The Secret Life of Bees*.
    - The two *Harry Potter* books also display a strong mutual co-occurrence, reflecting common reading patterns among fans of the series.


<img width="586" height="266" alt="Screenshot 2025-07-19 at 3 01 39 PM" src="https://github.com/user-attachments/assets/dcbbfdb6-94b7-46fd-8a1f-1e80747475b6" />

<img width="654" height="572" alt="Screenshot 2025-07-19 at 3 02 35 PM" src="https://github.com/user-attachments/assets/1f3f42ae-2f02-49af-b858-1dd95056e358" />

## Methods & Tools

- **Frequent Itemset Mining**:
  - Apriori (via `mlxtend.frequent_patterns.apriori`)
  - FP-Growth (via `mlxtend.frequent_patterns.fpgrowth`)
  - Used a **minimum support threshold of 0.01** (itemsets must appear in at least 1% of all transactions)

- **Association Rule Mining**:
  - Generated rules based on confidence threshold
  - The association were generated using a minimum confidence threshold of **0.5** to ensure meaningful and reliable patterns.
  - Calculated support, confidence, and lift

## Comparative Analysis & Key Insights

- **FP-Growth** performed slightly better and was faster. Generally, it is more scalable for large dataset, because it avoids generating candidate itemsets explicitly and instead builds a compact data structure (the FP-tree) to mine frequent patterns directly.
- **Apriori**, while conceptually simpler and easier to understand, is slightly less efficient for the larger datasets. This is mainly because:
  - It uses a **candidate generation approach**, where it generates and tests all possible item combinations in a bottom-up manner.
  - This leads to **multiple passes over the dataset**, significantly increasing computation time.
  - The number of candidate itemsets can grow **exponentially** as the size of itemsets increases, causing high memory and processing overhead.

<img width="403" height="243" alt="Screenshot 2025-07-19 at 3 06 03 PM" src="https://github.com/user-attachments/assets/ae6330c7-aa5e-4f5d-baf0-fa65e3c0aaff" />
<img width="403" height="243" alt="Screenshot 2025-07-19 at 3 05 50 PM" src="https://github.com/user-attachments/assets/830825c5-1a02-41e7-8ba2-4e445065047e" />


- **Association Rule Insights (Top 5 Books)**
    -  Rule 1:
        If someone reads: 'Harry Potter and the Prisoner of Azkaban (Book 3)'
        They are 50.00% likely to also read: 'Harry Potter and the Chamber of Secrets (Book 2), Harry Potter and the Goblet of Fire (Book 4)'
        This association is 29.11x stronger than random chance
        Support: 0.015 (82 users)
        Business Impact: Very Strong
    -  Rule 2:
       If someone reads: 'Harry Potter and the Chamber of Secrets (Book 2), Harry Potter and the Goblet of Fire (Book 4)'
       They are 84.54% likely to also read: 'Harry Potter and the Prisoner of Azkaban (Book 3)'
       This association is 29.11x stronger than random chance
       Support: 0.015 (82 users)
       Business Impact: Very Strong
    -  Rule 3:
       If someone reads: 'Harry Potter and the Goblet of Fire (Book 4)'
       They are 54.67% likely to also read: 'Harry Potter and the Chamber of Secrets (Book 2), Harry Potter and the Prisoner of Azkaban (Book 3)'
       This association is 28.58x stronger than random chance
       Support: 0.015 (82 users)
       Business Impact: Very Strong
    -  Rule 4:
       If someone reads: 'Harry Potter and the Chamber of Secrets (Book 2), Harry Potter and the Prisoner of Azkaban (Book 3)'
       They are 75.93% likely to also read: 'Harry Potter and the Goblet of Fire (Book 4)'
       This association is 28.58x stronger than random chance
       Support: 0.015 (82 users)
       Business Impact: Very Strong
    - Rule 5:
       If someone reads: 'Harry Potter and the Goblet of Fire (Book 4), Harry Potter and the Prisoner of Azkaban (Book 3)'
       They are 81.19% likely to also read: 'Harry Potter and the Chamber of Secrets (Book 2)'
       This association is 24.00x stronger than random chance
       Support: 0.015 (82 users)
       Business Impact: Very Strong

## Challenges Faced

The major challenges associated with lab as follows:

- Initially there was issue for parsing the csv data set and it was esolved using `encoding='latin-1'` and `on_bad_lines='skip'`
- The data was very noisy and unclean it was cleaned by removing the missing ages, filtering out low-activity users and rarely rated books and also removing duplicate values.
