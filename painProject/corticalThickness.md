#Cortical thickness

##fsgd file

```
GroupDescriptorFile 1
Title OSGM
Class PAIN
Class CON
Variables Age
Input PAIN01 PAIN 36
Input PAIN02 PAIN 51
Input PAIN03 PAIN 22
Input PAIN04 PAIN 22
Input PAIN05 PAIN 25
Input PAIN06 PAIN 28
Input PAIN07 PAIN 44
Input PAIN08 PAIN 33
Input PAIN09 PAIN 30
Input PAIN10 PAIN 40
Input PAIN11 PAIN 20
Input PAIN12 PAIN 33
Input PAIN13 PAIN 37
Input PAIN14 PAIN 31
Input PAIN16 PAIN 59
Input PAIN17 PAIN 23
Input PAIN18 PAIN 52
Input PAIN19 PAIN 20
Input PAIN21 PAIN 53
Input PAIN22 PAIN 49
Input PAIN23 PAIN 41
Input PAIN24 PAIN 49
Input PAIN25 PAIN 38
Input PAIN26 PAIN 31
Input PAIN27 PAIN 36
Input NOR01 CON 26
Input NOR04 CON 29
Input NOR06 CON 27
Input NOR08 CON 25
Input NOR09 CON 25
Input NOR11 CON 25
Input NOR14 CON 25
Input NOR16 CON 28
Input NOR18 CON 34
Input NOR19 CON 37
Input NOR20 CON 24
Input NOR21 CON 35
Input NOR22 CON 35
Input NOR23 CON 40
Input NOR25 CON 26
Input NOR27 CON 24
Input NOR31 CON 31
Input NOR32 CON 32
Input NOR35 CON 34
Input NOR37 CON 40
Input NOR38 CON 31
Input NOR39 CON 35
Input NOR40 CON 31
Input NOR41 CON 46
Input NOR42 CON 48
```


##mtx : group.diff.1cov.mtx

```
1 -1 0 0
```

##Smoothing

```
FWHM 20
```


##Script

```
mris_preproc \
    --fsgd g2v1.fsgd \
    --target average \
    --hemi lh \
    --meas thickness \
    --out lh.group_age.thickness.00.mgh

mri_surf2surf \
    --hemi lh \
    --s average \
    --sval lh.group_age.thickness.00.mgh \
    --fwhm 20 \
    --cortex \
    --tval lh.group_age.thickness.20B.mgh

mri_glmfit \
    --y lh.group_age.thickness.20B.mgh \
    --fsgd g2v1.fsgd dods \
    --C group.diff.2cov.mtx \
    --surf average lh \
    --cortex \
    --glmdir lh.group_age.20.glmdir

mri_glmfit-sim \
    --glmdir rh.group_age.20.glmdir \
    --sim perm 5000 3 perm.negative \
    --sim-sign neg \
    --cwpvalthresh 0.05 \
    --overwrite \
    --perm-force&

#right
mris_preproc \
    --fsgd g2v1.fsgd \
    --target average \
    --hemi rh \
    --meas thickness \
    --out rh.group_age.thickness.00.mgh

mri_surf2surf \
    --hemi rh \
    --s average \
    --sval rh.group_age.thickness.00.mgh \
    --fwhm 20 \
    --cortex \
    --tval rh.group_age.thickness.20B.mgh

mri_glmfit \
    --y rh.group_age.thickness.20B.mgh \
    --fsgd g2v1.fsgd dods \
    --C group.diff.2cov.mtx \
    --surf average rh \
    --cortex \
    --glmdir rh.group_age.20.glmdir

mri_glmfit-sim \
    --glmdir lh.group_age.20.glmdir \
    --sim perm 5000 3 perm.negative \
    --sim-sign neg \
    --cwpvalthresh 0.05 \
    --overwrite \
    --perm-force

```


##Extra

- AGE & IQ covariate

The group difference was not significant when both AGE and IQ were used as the covariate

<br>
- Extraction script

To extract the thickness values of the cluster that showed significnat group difference ...

```

export SUBJECTS_DIR=/Volumes/CCNC_3T/2013_12_painAnalysis/2013_08_23_pain_freesurfer/freesurfer_2014_04_03


echo "# ColHeaders StructName NumVert SurfArea GrayVol ThickAvg ThickStd MeanCurv GausCurv FoldInd CurvInd" > labelCollection/summary.txt

for i in PAIN01 PAIN02 PAIN03 PAIN04 PAIN05 PAIN06 PAIN07 PAIN08 PAIN09 PAIN10 PAIN11 PAIN12 PAIN13 PAIN14 PAIN16 PAIN17 PAIN18 PAIN19 PAIN21 PAIN22 PAIN23 PAIN24 PAIN25 PAIN26 PAIN27 NOR01 NOR04 NOR06 NOR08 NOR09 NOR11 NOR14 NOR16 NOR18 NOR19 NOR20 NOR21 NOR22 NOR23 NOR25 NOR27 NOR31 NOR32 NOR35 NOR37 NOR38 NOR39 NOR40 NOR41 NOR42
do

    mri_label2label \
        --srcsubject average \
        --srclabel average/label/lh_age_cov_20_FWHM.label \
        --trgsubject ${i} \
        --hemi lh \
        --trglabel labelCollection/lh_${i} \
        --regmethod surface

    mris_anatomical_stats \
        -a ${SUBJECTS_DIR}/${i}/label/lh.aparc.annot \
        -l labelCollection/lh_${i}.label \
        -f labelCollection/lh_${i}.txt \
        -b ${i} lh

    cat labelCollection/lh_${i}.txt|tail -n 1 >> labelCollection/summary.txt

    mri_label2label \
        --srcsubject average \
        --srclabel average/label/rh_age_cov_20_FWHM.label \
        --trgsubject ${i} \
        --hemi rh \
        --trglabel labelCollection/rh_${i} \
        --regmethod surface

    mris_anatomical_stats \
        -a ${SUBJECTS_DIR}/${i}/label/rh.aparc.annot \
        -l labelCollection/rh_${i}.label \
        -f labelCollection/rh_${i}.txt \
        -b ${i} rh

    cat labelCollection/rh_${i}.txt|tail -n 1 >> labelCollection/summary.txt
done
```

