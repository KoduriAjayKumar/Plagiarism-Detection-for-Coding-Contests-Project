# 📚 Plagiarism Detection for Coding Contests

Detect and flag plagiarized code submissions during programming contests to ensure fairness and integrity.

---

## 🚩 Problem Statement
In programming contests, identifying plagiarism manually is a significant challenge. Participants often copy code, compromising the competition's integrity. This project automates plagiarism detection using web scraping, machine learning, and database management to streamline the process.

---

## 🔧 Technologies Used

- ![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python) **Python**
- ![Selenium](https://img.shields.io/badge/Selenium-Web%20Scraping-brightgreen?logo=selenium) **Selenium for Web Scraping**
- ![Machine Learning](https://img.shields.io/badge/ML-SentenceTransformer-yellow?logo=ai) **Machine Learning (Sentence Transformer)**
- ![MySQL](https://img.shields.io/badge/MySQL-Database-orange?logo=mysql) **MySQL**
- ![Flask](https://img.shields.io/badge/Flask-Backend-red?logo=flask) **Flask**

---

## 📖 Project Description
This project is designed to automatically detect the copied code in coding contests by:
- Scraping user submissions from HackerRank with **Selenium**.
- Storing submission data in a **MySQL database**.
- Using **Sentence Transformer** to compute similarities between codes.
- Displaying flagged submissions through a **Flask web application** for easy review.

---

## 🛠️ Inputs Required
To run this project, the following inputs are needed:

1. **HackerRank Login Credentials**: For scraping user submissions with `Selenium.py`.
2. **MySQL Database Details**: Host, user, password, and database name.
3. **Submission Data**: Gathered by running `Selenium.py` to populate the `CodeSubmissions` table.
4. **Model Threshold Value**: Set in `MLPlaglarismCheck.py` for similarity comparison (e.g., 0.98).

---

## 🗂️ Code Explanation

### 1. `Selenium.py` - Web Scraping and Data Storage
**Purpose**: Automates the process of logging into HackerRank, navigating to the submissions page, and scraping relevant data to store in a MySQL database.

**Functionality**:
- **Login and Navigation**: Uses Selenium to log in and navigate to the contest submissions dashboard.
- **Data Extraction**: Extracts `username`, `problem title`, `language`, `time`, `score`, and `source code`.
- **Database Storage**: Inserts scraped data into the `CodeSubmissions` table in the MySQL database.


### 2. MLPlaglarismCheck.py - Detecting Plagiarism
**Purpose:** Retrieves user submissions from the database, compares their source codes using Sentence Transformer, and flags copied submissions based on a set threshold.

**Functionality:**
Data Retrieval: Queries(extracts) the CodeSubmissions table for the latest submission per user.
- **Embedding Generation:** Transforms source codes into embeddings for similarity comparison.
- **Similarity Check:** Compares code pairs and flags those exceeding the similarity threshold (e.g., 0.98).
- **Result Storage:** Inserts details of flagged submissions into the CopiedSubmissions table.


### 3. app.py - Flask Web Application for Display
**Purpose:** Provides a web interface to display flagged plagiarism cases from the CopiedSubmissions table and shows the detailed code of each user when clicked.

**Functionality:**
- **Home Page (/):** Lists all flagged cases with username1, username2, and similarity_score.
- **Details Page**(/details/<username>): Shows the source code for the specified user.
