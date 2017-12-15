# Single Subject Analysis

From your preprocessed data, you can redirect to the `./sub_*.results/` subdirectory and open `afni`

To take a look at the data, simply find the `M-R_GLT#_Tstat` contrast under both `Olay` and `Thr`. Then, set your p-value to .001, or some other small number0 of choice. You can move around the brain to get a sense of activation patterns in this subject. 

# Group Analysis

Once you've finished preprocessing on all subjects, there are a few steps before we're ready for group analysis.

## Masking

1) Create a group mask that will mask out all non-brain regions and coverage differences across subjects. For example,

`3dmask_tool -input subject_results/group.ACLr/sub-*.results/mask_group+tlrc.HEAD -frac 1.0 -prefix mask`

## Indexing

2) Choose the correct sub-brick for your analysis - this is easy because there is only one contrast that we're interested in here.

`3dinfo -label stats.sub-01_REML+tlrc.BRIK`

You will find a string that looks like this: 

`stats.sub_01+tlrc[M-R_GLT#0_Coef]`

Keep that string handy. You will need it for performing the group-wise t-test.

## The t-test!

3) Now it's time to run our t-test with the 

`3dttest++ -mask mask+tlrc -prefix finger-lips -setA 'stats*+tlrc.HEAD[M-R_GLT#0_Coef]'`

4) To view, you will want to copy an anatomical file to your current workflow using

`3dcopy ~/abin/MNI_avg152T1+tlrc`
