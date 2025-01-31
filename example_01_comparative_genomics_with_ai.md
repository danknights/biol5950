# Example: Comparative Genomics with AI
This could be a list of commands to run in order to do comparative genomics; instead, it is a list of _prompts_ to ask AI! These are just suggestions, but they worked on chatgpt 4o on Jan 24, 2025. I used chatgpt o1 for debugging the python file at the last step.

> Prompt:
> 
> I want to do pangenome analysis on e coli. How do I download some e coli genomes manually from the NCBI website?

Results: chatgpt gave me a link. I followed the link and searched for Escherichia coli. 

> Prompt:
>
> OK I selected 5 genomes, clicked Download > Download package, and it gave me these options:
> 
> Genome sequences (FASTA)
> Annotation features (GTF)
> Annotation features (GFF)
> Sequence and annotation (GBFF)
> Transcripts (FASTA)
> Genomic coding sequences (FASTA)
> Protein (FASTA)
> Sequence report (JSONL)
> What should I select?

Note: use shift-return to enter newlines without submitting the request.

Results: After some discussion, I selected FASTA, GFF. 

This part I did on my own: I downloaded the NCBI files to my local computer and transfered the file, `ncbi_dataset.zip` to my `biol5950` folder on MSI using [ood.msi.umn.edu](ood.msi.umn.edu).

Now -- and this is made all the difference -- I told chatgpt to hold my hand.

> Prompt:
>
> For the rest of this conversation, I need you to really hold my hand and walk
> me through the basics. This means:
> 
> &nbsp;1. Only give me one step to do at a time.
> 
> &nbsp;2. Before each step, help me check the input files to make sure they are in
>    the right places and have the right filenames. Tell me how to check and
>    I will paste the info here so that you can see it too. Please do not
>    assume that the files are exactly where you think think they are
>    or that they are named exactly like you think.
>
> &nbsp;3. If we need to move or rename the files, walk me through the basic steps
>    because I am a beginner on the command line.
>
> &nbsp;4. Then give me the command to run, based on the locations and names of the
>    input files that we found together.
>
> &nbsp;5. Then after I run the command, remind me to paste the output here so that
>    you can make sure it ran as expected and so that you can spot any errors.
>
> &nbsp;6. After we have confirmed that a step worked correctly, you can move on to
>    the next step.

Then I continued with the exercise:

> Prompt:
> 
> OK I have the file ncbi_dataset.zip on MSI, the supercomputer at UMN. What's next?

Results: At this point, the entire analysis proceeded according to chatgpt's instructions!
Every time I ran something, it prompted me to paste the output into the chat.

You might need to spur it along with a prompt like this:

> Prompt:
>
> let's do pangenome analysis. What is a common and easy tool?

Throughout the procees, there were a few errors, and it helped me resolve them. 

For example, it required the software `roary` for pan-genome analysis, which was missing from MSI.
Chatgpt told me how to install it with _conda_, but I used _mamba_ for the install
process as described in the tutorial on [installing packages](installing_packages_with_conda.md).

Then when `roary` had an error, it told me to install and run `prokka`, which I did the same way.

When `prokka` and `roary` were finished (about 10 minutes total), chatgpt
suggested that I make a phylogeny with _iqtree_.
I found the _iqtree2_ module already on MSI and made the tree.

> Prompt:
> 
> What's something cool I can do with the tree and the pangenome analysis?

Results:
ChatGPT told me to visualize core vs accessory genes on the tree.
I transferred the tree file back to my laptop. I uploaded the tree to the Interactive
Tree of Life (https://itol.embl.de/).

I then had ChatGPT write a python script to generate an
annotation file for iTOL to show core vs. accessory vs. unique genes for each strain using a 
barchart on the tree (its idea).

> Prompt:
> 
> Give me a python script to get the core/accessory/unique itol metadata from the gene_presence_absence.csv file

Results: This was actually the hardest step because it made two mistakes in the file format. One it 
fixed easily (based on the error from iTOL). For the other one, I had to bring out the big guns: chatgpt o1.
This is the prompt that I used. Note the use of --------------------------- to separate content.

<div>
<blockquote>
Prompt (for chatgpt o1):
<br>I have pangenome output from roary called gene_presence_absence.csv. The first few lines look like this:

\-----------------------------
<br>"Gene","Non-unique Gene name","Annotation","No. isolates","No. sequences","Avg sequences per isolate","Genome Fragment","Order within Fragment","Accessory Fragment","Accessory Order with 
Fragment","QC","Min group size nuc","Max group size nuc","Avg group size nuc","GCF_000005845.2","GCF_000008865.2","GCF_000013265.1","GCF_002853715.1","GCF_003697165.2"
<br>"hemA","","Glutamyl-tRNA reductase","5","5","1","2","7870","","","","1256","1325","1283","PICPPNBC_01206","LIHDBMIF_01680","PKBHPNHA_01287","DHKDBCCC_02678","BFLNMBHB_02675"
"group_1001","","Invasin","5","5","1","2","7882","","","","1394","1430","1408","PICPPNBC_01219","LIHDBMIF_01692","PKBHPNHA_01298","DHKDBCCC_02667","BFLNMBHB_02664"
<br>\-----------------------------

I'm using this python script to generate an annotation file for iTOL:

\-----------------------------
import pandas as pd

\# Load the gene_presence_absence.csv file
<br>input_file = "gene_presence_absence.csv"
<br>output_file = "itol_core_accessory_unique.txt"

\# Read the CSV file (skip the first line with non-standard header information)
<br>df = pd.read_csv(input_file, skiprows=1)

\# Extract genome names from the column headers (starting from column 14)
<br>genomes = df.columns[14:]  # Extract columns with genome presence/absence data

\# Initialize counts for each genome (use GCF IDs directly)
<br>gene_counts = {genome: {"core": 0, "accessory": 0, "unique": 0} for genome in genomes}

\# Iterate over rows and classify genes
<br>for _, row in df.iterrows():
<br>&nbsp;&nbsp;&nbsp;&nbsp;presence_absence = row[14:]  # Presence/absence data for genomes
<br>&nbsp;&nbsp;&nbsp;&nbsp;present_in = presence_absence.notna().sum()

&nbsp;&nbsp;&nbsp;&nbsp;\# Classify gene
<br>&nbsp;&nbsp;&nbsp;&nbsp;if present_in == len(genomes):
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;for genome in genomes:
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;gene_counts[genome]["core"] += 1
<br>&nbsp;&nbsp;&nbsp;&nbsp;elif present_in == 1:
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;genome = presence_absence.notna().idxmax()  # Find genome where the gene is unique
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;gene_counts[genome]["unique"] += 1
<br>&nbsp;&nbsp;&nbsp;&nbsp;else:
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;for genome in presence_absence[presence_absence.notna()].index:
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;gene_counts[genome]["accessory"] += 1

\# Write iTOL metadata file
<br>with open(output_file, "w") as f:
<br>&nbsp;&nbsp;&nbsp;&nbsp;f.write("DATASET_MULTIBAR\n")
<br>&nbsp;&nbsp;&nbsp;&nbsp;f.write("SEPARATOR TAB\n")
<br>&nbsp;&nbsp;&nbsp;&nbsp;f.write("DATASET_LABEL\tCore/Accessory/Unique\n")
<br>&nbsp;&nbsp;&nbsp;&nbsp;f.write("FIELD_COLORS\t#FF0000\t#00FF00\t#0000FF\n")  # Red: Core, Green: Accessory, Blue: Unique
<br>&nbsp;&nbsp;&nbsp;&nbsp;f.write("FIELD_LABELS\tCore\tAccessory\tUnique\n")
<br>&nbsp;&nbsp;&nbsp;&nbsp;f.write("DATA\n")

&nbsp;&nbsp;&nbsp;&nbsp;for genome, counts in gene_counts.items():
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;f.write(f"{genome}\t{counts['core']}\t{counts['accessory']}\t{counts['unique']}\n")

print(f"iTOL metadata written to {output_file}")
<br>\-----------------------------

But the output looks like this, with the wrong genome IDs:> 
<br>\-----------------------------
<br>DATASET_MULTIBAR
<br>SEPARATOR TAB
<br>DATASET_LABEL	Core/Accessory/Unique
<br>FIELD_COLORS	#FF0000	#00FF00	#0000FF
<br>FIELD_LABELS	Core	Accessory	Unique
<br>DATA
<br>PICPPNBC_01219	3278	622	404
<br>LIHDBMIF_01692	3278	692	1402
<br>PKBHPNHA_01298	3278	1138	413
<br>DHKDBCCC_02667	3278	949	629
<br>BFLNMBHB_02664	3278	1266	163
<br>\-----------------------------

Please help me fix it.
</blockquote>
</div>


Chatgpt o1 took 45 seconds to think and fixed the problem immediately.

I uploaded the annotation file to iTOL, manually changed the barchart colors, and got this:

<img width="855" alt="image" src="https://github.com/user-attachments/assets/6849bf5a-278d-4b7a-8a21-03d94bc51c01" />

