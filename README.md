# **Document Similarity Using Hadoop MapReduce**

## **Objective**

The goal of this assignment is to compute the **Jaccard Similarity** between pairs of documents using **Hadoop MapReduce**. You will implement a MapReduce job that:

1. Extracts words from multiple text documents.
2. Identifies which words appear in multiple documents.
3. Computes the **Jaccard Similarity** between document pairs.
4. Outputs document pairs with their similarity scores.

---

## **Jaccard Similarity Overview**

The Jaccard Similarity between two sets A and B is calculated as:

```
Jaccard Similarity (A, B) = |A ∩ B| / |A ∪ B|
```

Where:

- `|A ∩ B|` is the number of words common to both documents.
- `|A ∪ B|` is the total number of unique words in both documents.

Example Calculation:

```
Document1: {hadoop, is, a, distributed, system}
Document2: {hadoop, is, used, for, big, data, processing}

Common words: {hadoop, is} → |A ∩ B| = 2
Total unique words: {hadoop, is, a, distributed, system, used, for, big, data, processing} → |A ∪ B| = 10

Jaccard Similarity = 2/10 = 0.2 (20%)
```

---

## **Example Input and Output**

### **Input Format**

Each line represents a document and its contents:

```
Document1 hadoop is a distributed system
Document2 hadoop is used for big data processing
Document3 big data is important for analysis
```

### **Expected Output**

```
Document1, Document2 Similarity: 0.20
Document1, Document3 Similarity: 0.10
Document2, Document3 Similarity: 0.44
```

---

## **Approach & Implementation**

### **Mapper**

1. Reads input lines containing document names and their contents.
2. Tokenizes words and builds a set of words for each document.
3. Emits key-value pairs where the key is the document ID, and the value is the set of words.

### **Reducer**

1. Receives document-word set mappings from the Mapper.
2. Computes Jaccard Similarity between every pair of documents.
3. Outputs document pairs along with their computed similarity.

---

## **Environment Setup & Execution**

### **Step 1: Setup Hadoop**

Install Hadoop and set up HDFS:

```sh
hdfs namenode -format
start-dfs.sh
start-yarn.sh
```

### **Step 2: Compile the Java Program**

Use Maven to package the program:

```sh
mvn clean package
```

### **Step 3: Upload Data to HDFS**

```sh
hdfs dfs -mkdir /input
hdfs dfs -put local_input_files/* /input/
```

### **Step 4: Run MapReduce Job**

```sh
hadoop jar target/similarity.jar DocumentSimilarityDriver /input /output
```

### **Step 5: Retrieve Results**

```sh
hdfs dfs -cat /output/part-r-00000
```

---

## **Challenges Faced & Solutions**

1. **Handling Large Datasets**

   - Used Hadoop's distributed processing to manage large input sizes efficiently.

2. **Handling Stopwords and Punctuation**

   - Implemented a preprocessing step to remove common stopwords and special characters.

3. **Pairwise Comparison Efficiency**

   - Optimized by avoiding redundant calculations and using combinatorial logic to generate pairs efficiently.

---

## **Conclusion**

This project successfully implemented **Jaccard Similarity** using **Hadoop MapReduce**. The workflow efficiently computes document similarity, demonstrating how MapReduce can be used for text analysis at scale. The final output provides similarity scores between document pairs, which can be applied in various real-world applications like plagiarism detection and document clustering.

---

## **Submission Details**

- The complete implementation, dataset, and results are committed to the GitHub repository.
- The repository includes a README with detailed instructions on execution and setup.



