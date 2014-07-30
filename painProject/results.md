#Results

##Summary

Side | multiple-comparison correction | results | p-value
---|---|---|
Left|mc-z and perm|
Right|mc-z and perm|

## Left hemisphere

- mc-z.negative.sig.cluster.summary

```
# Cluster Growing Summary (mri_surfcluster)
# $Id: mri_surfcluster.c,v 1.51.2.3 2012/05/31 22:10:05 greve Exp $
# $Id: mrisurf.c,v 1.693.2.7 2013/05/12 22:28:01 nicks Exp $
# CreationTime 2014/04/06-15:15:16-GMT
# cmdline mri_surfcluster --in lh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/sig.mgh --csd lh_group_age_thickness_smoothed_20_glmdir/csd/mc-z.negative.j001-group.diff.1cov.csd --mask lh_group_age_thickness_smoothed_20_glmdir/mask.mgh --cwsig lh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/mc-z.negative.sig.cluster.mgh --vwsig lh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/mc-z.negative.sig.voxel.mgh --sum lh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/mc-z.negative.sig.cluster.summary --ocn lh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/mc-z.negative.sig.ocn.mgh --oannot lh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/mc-z.negative.sig.ocn.annot --annot aparc --csdpdf lh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/mc-z.negative.pdf.dat --cwpvalthresh 0.05 --o lh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/mc-z.negative.sig.masked.mgh --no-fixmni --surf white 
# cwd /Volumes/CCNC_3T/2013_12_painAnalysis/2013_08_23_pain_freesurfer/freesurfer_2014_04_03
# sysname  Darwin
# hostname brainimage.snu.ac.kr
# machine  x86_64
# FixVertexAreaFlag 1
# FixSurfClusterArea 1
# 
# Input      lh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/sig.mgh
# Frame Number      0
# srcsubj average
# hemi lh
# surface white
# annot aparc
# SUBJECTS_DIR /Volumes/CCNC_3T/2013_12_painAnalysis/2013_08_23_pain_freesurfer/freesurfer_2014_04_03/
# SearchSpace_mm2 88825.1
# SearchSpace_vtx 149953
# Bonferroni 0
# Minimum Threshold 3
# Maximum Threshold infinity
# Threshold Sign    neg
# AdjustThreshWhenOneTail 1
# CW PValue Threshold: 0.05 
# Area Threshold    0 mm^2
# CSD thresh  3.000000
# CSD nreps    5000
# CSD simtype  mc-z
# CSD contrast group.diff.1cov
# CSD confint  90.000000
# Overall max 2.10791 at vertex 120141
# Overall min -3.34374 at vertex 124901
# NClusters          1
# Total Cortical Surface Area 88825.1 (mm^2)
# FixMNI = 0
# 
# ClusterNo  Max   VtxMax   Size(mm^2)  MNIX   MNIY   MNIZ    CWP    CWPLow    CWPHi   NVtxs   Annot
   1       -3.344  124901    505.32     -6.2   54.9  -33.9  0.01740  0.01500  0.01980   774  medialorbitofrontal
```

- perm.negative.sig.cluster.summary

```
# Cluster Growing Summary (mri_surfcluster)
# $Id: mri_surfcluster.c,v 1.51.2.3 2012/05/31 22:10:05 greve Exp $
# $Id: mrisurf.c,v 1.693.2.7 2013/05/12 22:28:01 nicks Exp $
# CreationTime 2014/04/06-18:51:07-GMT
# cmdline mri_surfcluster --in lh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/sig.mgh --csd lh_group_age_thickness_smoothed_20_glmdir/csd/perm.negative.j001-group.diff.1cov.csd --mask lh_group_age_thickness_smoothed_20_glmdir/mask.mgh --cwsig lh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/perm.negative.sig.cluster.mgh --vwsig lh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/perm.negative.sig.voxel.mgh --sum lh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/perm.negative.sig.cluster.summary --ocn lh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/perm.negative.sig.ocn.mgh --oannot lh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/perm.negative.sig.ocn.annot --annot aparc --csdpdf lh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/perm.negative.pdf.dat --cwpvalthresh 0.05 --o lh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/perm.negative.sig.masked.mgh --no-fixmni --surf white 
# cwd /Volumes/CCNC_3T/2013_12_painAnalysis/2013_08_23_pain_freesurfer/freesurfer_2014_04_03
# sysname  Darwin
# hostname brainimage.snu.ac.kr
# machine  x86_64
# FixVertexAreaFlag 1
# FixSurfClusterArea 1
# 
# Input      lh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/sig.mgh
# Frame Number      0
# srcsubj average
# hemi lh
# surface white
# annot aparc
# SUBJECTS_DIR /Volumes/CCNC_3T/2013_12_painAnalysis/2013_08_23_pain_freesurfer/freesurfer_2014_04_03/
# SearchSpace_mm2 88825.1
# SearchSpace_vtx 149953
# Bonferroni 0
# Minimum Threshold 3
# Maximum Threshold infinity
# Threshold Sign    neg
# AdjustThreshWhenOneTail 1
# CW PValue Threshold: 0.05 
# Area Threshold    0 mm^2
# CSD thresh  3.000000
# CSD nreps    5000
# CSD simtype  perm
# CSD contrast group.diff.1cov
# CSD confint  90.000000
# Overall max 2.10791 at vertex 120141
# Overall min -3.34374 at vertex 124901
# NClusters          1
# Total Cortical Surface Area 88825.1 (mm^2)
# FixMNI = 0
# 
# ClusterNo  Max   VtxMax   Size(mm^2)  MNIX   MNIY   MNIZ    CWP    CWPLow    CWPHi   NVtxs   Annot
   1       -3.344  124901    505.32     -6.2   54.9  -33.9  0.02120  0.01860  0.02380   774  medialorbitofrontal
```


##Right hemisphere

- mc-z.negative.sig.cluster.summary

```
# Cluster Growing Summary (mri_surfcluster)
# $Id: mri_surfcluster.c,v 1.51.2.3 2012/05/31 22:10:05 greve Exp $
# $Id: mrisurf.c,v 1.693.2.7 2013/05/12 22:28:01 nicks Exp $
# CreationTime 2014/04/07-01:33:20-GMT
# cmdline mri_surfcluster --in rh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/sig.mgh --csd rh_group_age_thickness_smoothed_20_glmdir/csd/mc-z.negative.j001-group.diff.1cov.csd --mask rh_group_age_thickness_smoothed_20_glmdir/mask.mgh --cwsig rh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/mc-z.negative.sig.cluster.mgh --vwsig rh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/mc-z.negative.sig.voxel.mgh --sum rh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/mc-z.negative.sig.cluster.summary --ocn rh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/mc-z.negative.sig.ocn.mgh --oannot rh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/mc-z.negative.sig.ocn.annot --annot aparc --csdpdf rh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/mc-z.negative.pdf.dat --cwpvalthresh 0.05 --o rh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/mc-z.negative.sig.masked.mgh --no-fixmni --surf white 
# cwd /Volumes/CCNC_3T/2013_12_painAnalysis/2013_08_23_pain_freesurfer/freesurfer_2014_04_03
# sysname  Darwin
# hostname brainimage.snu.ac.kr
# machine  x86_64
# FixVertexAreaFlag 1
# FixSurfClusterArea 1
# 
# Input      rh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/sig.mgh
# Frame Number      0
# srcsubj average
# hemi rh
# surface white
# annot aparc
# SUBJECTS_DIR /Volumes/CCNC_3T/2013_12_painAnalysis/2013_08_23_pain_freesurfer/freesurfer_2014_04_03/
# SearchSpace_mm2 89450
# SearchSpace_vtx 149926
# Bonferroni 0
# Minimum Threshold 3
# Maximum Threshold infinity
# Threshold Sign    neg
# AdjustThreshWhenOneTail 1
# CW PValue Threshold: 0.05 
# Area Threshold    0 mm^2
# CSD thresh  3.000000
# CSD nreps    5000
# CSD simtype  mc-z
# CSD contrast group.diff.1cov
# CSD confint  90.000000
# Overall max 2.45857 at vertex 114811
# Overall min -4.17016 at vertex 25866
# NClusters          1
# Total Cortical Surface Area 89450 (mm^2)
# FixMNI = 0
# 
# ClusterNo  Max   VtxMax   Size(mm^2)  MNIX   MNIY   MNIZ    CWP    CWPLow    CWPHi   NVtxs   Annot
   1       -4.170   25866    476.69     26.2   72.7   -3.9  0.02080  0.01820  0.02340   545  rostralmiddlefrontal
```

- perm.negative.sig.cluster.summary

```
# Cluster Growing Summary (mri_surfcluster)
# $Id: mri_surfcluster.c,v 1.51.2.3 2012/05/31 22:10:05 greve Exp $
# $Id: mrisurf.c,v 1.693.2.7 2013/05/12 22:28:01 nicks Exp $
# CreationTime 2014/04/07-05:08:24-GMT
# cmdline mri_surfcluster --in rh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/sig.mgh --csd rh_group_age_thickness_smoothed_20_glmdir/csd/perm.negative.j001-group.diff.1cov.csd --mask rh_group_age_thickness_smoothed_20_glmdir/mask.mgh --cwsig rh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/perm.negative.sig.cluster.mgh --vwsig rh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/perm.negative.sig.voxel.mgh --sum rh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/perm.negative.sig.cluster.summary --ocn rh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/perm.negative.sig.ocn.mgh --oannot rh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/perm.negative.sig.ocn.annot --annot aparc --csdpdf rh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/perm.negative.pdf.dat --cwpvalthresh 0.05 --o rh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/perm.negative.sig.masked.mgh --no-fixmni --surf white 
# cwd /Volumes/CCNC_3T/2013_12_painAnalysis/2013_08_23_pain_freesurfer/freesurfer_2014_04_03
# sysname  Darwin
# hostname brainimage.snu.ac.kr
# machine  x86_64
# FixVertexAreaFlag 1
# FixSurfClusterArea 1
# 
# Input      rh_group_age_thickness_smoothed_20_glmdir/group.diff.1cov/sig.mgh
# Frame Number      0
# srcsubj average
# hemi rh
# surface white
# annot aparc
# SUBJECTS_DIR /Volumes/CCNC_3T/2013_12_painAnalysis/2013_08_23_pain_freesurfer/freesurfer_2014_04_03/
# SearchSpace_mm2 89450
# SearchSpace_vtx 149926
# Bonferroni 0
# Minimum Threshold 3
# Maximum Threshold infinity
# Threshold Sign    neg
# AdjustThreshWhenOneTail 1
# CW PValue Threshold: 0.05 
# Area Threshold    0 mm^2
# CSD thresh  3.000000
# CSD nreps    5000
# CSD simtype  perm
# CSD contrast group.diff.1cov
# CSD confint  90.000000
# Overall max 2.45857 at vertex 114811
# Overall min -4.17016 at vertex 25866
# NClusters          1
# Total Cortical Surface Area 89450 (mm^2)
# FixMNI = 0
# 
# ClusterNo  Max   VtxMax   Size(mm^2)  MNIX   MNIY   MNIZ    CWP    CWPLow    CWPHi   NVtxs   Annot
   1       -4.170   25866    476.69     26.2   72.7   -3.9  0.02600  0.02320  0.02900   545  rostralmiddlefrontal
```
