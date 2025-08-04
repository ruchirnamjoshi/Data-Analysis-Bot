# 📊 Data Analysis Chatbot

### A **multimodal** data‐analysis assistant built with Gradio and OpenAI’s function‐calling API.  
Upload any CSV, then chat naturally to explore, visualize, and preprocess your data—all driven by GPT-4, with real charts rendered in your browser.
---

### Demo : https://drive.google.com/file/d/1a1qZWS8NpE-S9aGeUDl4qbxpdHzkA_ek/view?usp=drive_link
---

## 🚀 Features

- **Zero-boilerplate CSV ingestion**  
  Upload a CSV and the bot immediately learns its schema.
- **Descriptive statistics**  
  “Give me summary stats” produces a clean Markdown table of mean, std, min/max, quartiles.
- **Interactive plotting**  
  - **Histogram** (custom bins, ranges, colors)  
  - **Scatter** (any two numeric columns, set ranges, point size, color)  
  - **Boxplot** (optionally grouped by a categorical column)  
  - **Line plot** (handles dates & numeric x-axes)  
  - **Correlation heatmap** (all numeric features, annotated)  
- **Data cleaning & preprocessing**  
  - Drop missing rows (`drop_nulls`)  
  - Impute missing values (`impute_missing`)  
  - Remove outliers by Z-score or IQR (`remove_outliers`)  
- **Two-step conversational flow**  
  1. LLM decides which “tool” to call  
  2. Executes locally, then LLM crafts a friendly human reply  
- **Headless chart capture**  
  All Matplotlib/Seaborn plots generated in memory and streamed back—no GUI popups.

---

## ▶️ Installation 

- Just Download and run the .ipynb Notbook
- you will need an OpenAI API key in a .env file

This launches a Gradio UI:

- **Upload CSV** widget  
- **Chat window** to the right  
- **Plots & stats** appear inline

---

## 💬 Usage Examples

1. **Load data**  
   ```
   [Upload your CSV] → “Hello!”
   → “CSV loaded: 1 234 rows × 12 columns.”
   ```

2. **Summarize**  
   ```
   “Show me summary statistics.”
   → Renders a Markdown table of descriptive stats.
   ```

3. **Plot**  
   ```
   “Plot a histogram of ‘price’ between 100k and 1M with 30 bins.”
   → Histogram appears inline.
   ```

4. **Clean & Replot**  
   ```
   “Remove outliers from ‘sqft_living’ using IQR.”
   → “Removed 42 outliers from ‘sqft_living’.”
   “Now plot scatter of ‘price’ vs ‘sqft_living’.”
   → Cleaned scatter plot appears.
   ```

---

## 🔧 Architecture

1. **User** interacts via Gradio chat & file-upload widgets.  
2. **Chat handler** builds a messages list with our dynamic system prompt.  
3. **OpenAI LLM** selects a function to call (e.g. `plot_scatter`).  
4. **Local Python tool** executes request, returns image bytes or stats.  
5. **LLM follow-up** generates a natural response confirming success.  
6. **Gradio** displays text + inline images.

---

## ❓ FAQ

- **Can I upload very large CSVs?**  
  Depends on your machine and memory—Pandas holds the data locally.

- **Is my data sent to OpenAI?**  
  Only column names and function-call arguments (no raw data) are sent. The CSV stays local.

---
