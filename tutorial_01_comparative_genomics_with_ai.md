# Tutorial 01: Comparative Genomics with AI
This could be a list of commands to run to do comparative genomics; instead, it is a list of _prompts_ to ask AI! These are just suggestions, but they worked on ChatGPT 4o on Jan 24, 2025.

## Obtain data
> I want to do pangenome analysis on e coli. How do I download some e coli genomes from NCBI?

Chat-GPT gave me a link. I followed the link and searched for Escherichia coli. 

> OK I selected 10 genomes, clicked Download > Download package, and it gave me these options:
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

Note: I selected FASTA, GFF. I downloaded the files to my local computer and transfered the file, `ncbi_dataset.zip` to my `biol5950` folder on MSI using [ood.msi.umn.edu](ood.msi.umn.edu).

## Tell the AI to hold your hand
> For the rest of this conversation, I need you to really hold my hand and walk
> me through the basics. This means:
> 
> 1. Only give me one step to do at a time.
> 2. Before each step, help me check the input files to make sure they are in
>    the right places and have the right filenames. Tell me how to check and
>    I will paste the info here so that you can see it too. Please do not
>    assume that the files are exactly where you think think they are
>    or that they are named exactly like you think.
> 3. If we need to move or rename the files, walk me through the basic steps
>    because I am a beginner on the command line.
> 4. Then give me the command to run, based on the locations and names of the
>    input files that we found together.
> 5. Then after I run the command, remind me to paste the output here so that
>    you can make sure it ran as expected and so that you can spot any errors.
> 6. After we have confirmed that a step worked correctly, you can move on to
>    the next step.
 

## Continue to follow AI's instructions.
> OK I have the file ncbi_dataset.zip on MSI. What's next?

At this point, the entire analysis proceeded according to ChatGPT's instructions!

There were a few errors, but it helped me resolve them, as follows. 

It required the software _roary_ for pan-genome analysis, which was missing from MSI.
The AI told me how to install it with _conda_, but I used _mamba_ for the install
process as described in the tutorial on [installing packages](installing_packages_with_conda.md).

Then when _roary_ had an error, it told me to install _prokka_, which I did the same way.

Then _prokka_ had an error (because the _blastp_ version was too old), and I could have installed
_blast_, but I knew that MSI has _blast_, so I searched for it [as described here](loading_modules.md),
and loaded a newer version with `module load ncbi_blast/2.8.1`.

