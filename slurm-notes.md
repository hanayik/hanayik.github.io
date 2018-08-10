# SLURM GUIDE
This guide is mainly for my own mind dump, but others may find it useful.

First, my use case is processing thousands of MRI scans (both real, and somewhat simulated). So the choices I make are within that context. Also, there may be other ways to accomplish the tasks I present, but the methods I have used seem simple to me, and they work.

## Data
It's extremely important that your data is organized (files, folder structure, etc.) to facilitate parallel processing on the high performance cluster. 

For example, I have created thousands of artifically lesioned brain images (from real lesions of stroke participants). These images will be processed in a few different ways, with the ultimate goal of comparing processing methods. My data is organized as:

```
method-A (folder):
	-> subj-1 (folder):
		T1_subj1.nii (file)
		Lesion_subj1.nii (file)
	-> subj-2 (folder):
		T1_subj2.nii (file)
		Lesion_subj2.nii (file)
	.
	.
	.
	-> subj-10000 (folder):
		T1_subj10000.nii (file)
		Lesion_subj10000.nii (file)
		
method-B (folder):
	-> subj-1 (folder):
		T1_subj1.nii (file)
		Lesion_subj1.nii (file)
	-> subj-2 (folder):
		T1_subj2.nii (file)
		Lesion_subj2.nii (file)
	.
	.
	.
	-> subj-10000 (folder):
		T1_subj10000.nii (file)
		Lesion_subj10000.nii (file)
```

This structure is highly parallelizable. Nothing in Method B requires information from processing in Method A and vice versa. Also, no subject folder requires information from any other subject folder. 

Each pyhton batch script operates on one method folder and submits jobs to the SLURM scheduler for that method only. This way, batch processing scripts stay modular, and correspond with only one dataset. For example, batch_scriptA.py would only be able to access and process data in the MethodA folder. Keep in mind this are just generalized examples. In reality things are named a bit more appropriately.

{work in progress}

{todo: give code examples for sbatch, and pyhton submission scripts}