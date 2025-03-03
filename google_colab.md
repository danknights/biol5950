# Tutorial: Setting Up Google Colab for Bioinformatics Analysis

In this tutorial, you'll learn how to set up a Google Colab notebook for your bioinformatics class. We'll guide you through downloading the raw gene expression data and its corresponding annotation file, uploading them to Google Drive, and starting a new Colab notebook. After these initial steps, you'll use ChatGPT to assist you with data processing, quality control, and visualization.

## Step 1: Download Gene Expression Data

1. **Access the Gene Expression Data:**
   - Visit the [GEO Accession Viewer for GSE229968](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE229968).

2. **Download the Processed Data File:**
   - Locate the supplementary files section.
   - Click on the link to download the processed data file named `GSE229968_processed_data.txt.gz` (6.0 MB).

## Step 2: Download the Annotation File

1. **Access the Annotation Data:**
   - Visit the [GEO Platform Viewer for GPL14550](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GPL14550).

2. **Download the Annotation File:**
   - Scroll to the bottom of the page to find the platform data table.
   - Click on the "[Download full table]" link to obtain the annotation file for the Agilent-028004 SurePrint G3 Human GE 8x60K Microarray.

## Step 3: Upload Files to Google Drive

1. **Sign in to Google Drive:**
   - Go to [Google Drive](https://drive.google.com/) and log in with your Google account.

2. **Create a New Folder:**
   - Click on "New" > "Folder" to create a new folder named `biol5950_demo_data` (or any name you prefer).

3. **Upload Files to the Folder:**
   - Open the `biol5950_demo_data` folder.
   - Either drag-and-drop the files into the new folder, or click on "New" > "File upload" and select the downloaded files (`GSE229968_processed_data.txt.gz` and the annotation file) to upload them.

## Step 4: Start a New Google Colab Notebook

1. **Access Google Colab:**
   - Visit [Google Colab](https://colab.research.google.com/) and ensure you're logged in with your Google account.

2. **Create a New Notebook:**
   - Click on "File" > "New Notebook" to create a new notebook.

3. **Rename the Notebook:**
   - Click on the default title (e.g., "Untitled") at the top and rename it to `biol5950_demo_analysis`.

## Step 5: Use ChatGPT for Further Analysis

Now that you have your data files uploaded and your Colab notebook set up, you can use ChatGPT to guide you through the subsequent steps, including mounting Google Drive, listing contents, loading files, performing quality control, and visualization.

**Suggested Prompt for ChatGPT:**

```text
For the rest of this conversation, I need you to really hold my hand and walk me through the basics. This means:

1. Only give me one step to do at a time.

2. Before each step, help me check the input files to make sure they are in the right places and have the right filenames. Tell me how to check and I will paste the info here so that you can see it too. Please do not assume that the files are exactly where you think they are or that they are named exactly like you think.

3. If we need to move or rename the files, walk me through the basic steps because I am a beginner on the command line.

4. Then give me the command to run, based on the locations and names of the input files that we found together.

5. Then after I run the command, remind me to paste the output here so that you can make sure it ran as expected and so that you can spot any errors.

6. After we have confirmed that a step worked correctly, you can move on to the next step.
```

## Additional Prompts to Guide Your Analysis

To further assist you in your analysis, consider using the following general prompts with ChatGPT:

1. **Performing Quality Control on Gene Expression Data:**

```text
I have a gene expression dataset on my Google Drive.
I have two files: GPL14550-9757.txt and GSE229968_processed_data.txt.gz.
They are in a folder called biol5950_demo_data on my Google Drive.
I also have a new Google colab open to do the analysis.
I want to perform quality control to ensure the data's reliability.
First, help me access the data in Google colab.
Then please guide me through the necessary steps and methods to assess and improve data quality.
```

2. **Visualizing Gene Expression Data:**

```text
I want to visualize my gene expression data to identify patterns and insights.
Could you suggest effective visualization techniques and guide me on how to implement them?
```

With these or similar prompts, ChatGPT should provide you with detailed, step-by-step guidance for analysis in Google Colab.
