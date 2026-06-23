# AI-Powered Candidate Ranking Engine for Technical Talent Acquisition

A high-performance, memory-optimized talent intelligence engine built to discover and rank the top 100 Senior AI Engineer profiles from an unstructured pool of 100,000 candidates.

## 🚀 Project Overview & Objective
Traditional talent sourcing systems rely heavily on lexical keyword matching, making them highly vulnerable to keyword-stuffing and mismatched profiles. This project implements a sophisticated dual-stage pipeline that combines strict deterministic constraints with advanced semantic vector mappings to accurately identify optimal matches while running seamlessly on localized hardware constraints.

The pipeline is tailored to search for a **Senior AI Engineer (Founding Team)** with:
* **Target Experience:** 5 to 9 years of deep technical engineering depth.
* **Core Tech Stack:** Embeddings, vector search, LLMs, fine-tuning, retrieval, and RAG architectures.
* **Target Locations:** Noida or Pune, India (including candidates open to immediate relocation).

---

## 🏗️ System Architecture & Strategy

To efficiently process 100,000 records on an Intel Core i5 processor with 8GB RAM without experiencing application crashes or execution timeouts, this engine abandons global dataset ingestion in favor of a **Filter-First Architecture**.

### 1. High-Velocity Stream Filtering (Stage 1)
* **Memory Optimization:** The pipeline utilizes a line-by-line file streaming abstraction layer to ingest raw records progressively without overloading the system's RAM allocation.
* **Honeypot Evaded:** It applies rigid exclusion patterns to strip away non-technical profiles and keyword-stuffers (e.g., Marketing, HR, and Sales designations using AI buzzwords).
* **Data Compression:** It screens structural boundaries (Experience range 5–10 years and Target Locations) on-the-fly, instantly dropping unusable profiles. This compresses the active computational dataset from **100,000 down to 252 elite candidates in just 5 seconds**.

### 2. Deep Semantic Vector Embedding (Stage 2)
* Instead of wastefully calculating spatial dimensions for the entire 100K universe, the system executes neural mappings *exclusively* on the 252 pre-filtered candidate profiles.
* The text is vectorized using the advanced open-source embedding model `BAAI/bge-large-en-v1.5` to capture structural semantic alignment against the unstructured Job Description text.
* Vector spatial dimensions are compared using Cosine Similarity metrics to establish a baseline semantic fit.

### 3. Multi-Layered Scoring & Tie-Breaking Optimization
* **Behavioral Signals Integration:** The final score combines semantic similarity scores with operational metric multipliers parsed directly from candidate platform interaction footprints (`redrob_signals.recruiter_response_rate` and `redrob_signals.interview_completion_rate`).
* **Automated Portal Compliance:** To satisfy strict hackathon validation layers, the final result is sorted using a composite metric: **Final Score descending**, with an alphanumeric **Candidate ID ascending tie-breaker** to handle matching scores cleanly.

---

## 📊 Pipeline Performance & Benchmarks

* **Dataset Stream Filtering Time:** ~5 seconds (Processing throughput of ~17,700 records/sec)
* **AI Vector Embedding Generation Time:** ~3 minutes and 8 seconds across the optimized pool.
* **Memory Footprint:** Well under the system's 8GB RAM threshold, with zero paging file lag or CPU thermal throttling.
* **Top 5 Shortlist Preview:**
    * Rank 1: `CAND_0046525` (Score: 0.733095 | 6.1 Years Experience)
    * Rank 2: `CAND_0053605` (Score: 0.717965 | 6.9 Years Experience)
    * Rank 3: `CAND_0093763` (Score: 0.713833 | 5.0 Years Experience)

---

## 📁 Repository Structure

* `candidate_ranker.ipynb`: The end-to-end executable Jupyter Notebook detailing environment setup, mathematical scoring formulations, and data staging arrays.
* `team_ravi_submission.csv`: The finalized output dataset conforming precisely to the structural rules schema required by the verification portal (`candidate_id`, `rank`, `score`, `reasoning`).

---

## 🛠️ Core Technologies Used

* **Deep Learning & NLP:** `SentenceTransformers` (`BAAI/bge-large-en-v1.5`), `Scikit-Learn` (Cosine Similarity metrics)
* **Data Analytics Foundations:** `Pandas`, `NumPy`
* **Performance Diagnostics:** `Tqdm` (High-resolution data stream tracking tracking)
