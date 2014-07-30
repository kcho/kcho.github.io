#Cortical thickness

##fsgd file

```
GroupDescriptorFile 1
Title OSGM
Class PAIN
Class CON
Variables Age
Input PAIN01_KJD PAIN 36
Input PAIN02_HIM PAIN 51
Input PAIN03_LYN PAIN 22
Input PAIN04_SSY PAIN 22
Input PAIN05_LHY PAIN 25
Input PAIN06_KCJ PAIN 28
Input PAIN07_HMH PAIN 44
Input PAIN08_PDK PAIN 33
Input PAIN09_BHJ PAIN 30
Input PAIN10_LHJ PAIN 40
Input PAIN11_JSM PAIN 20
Input PAIN12_LJM PAIN 33
Input PAIN13_YEJ PAIN 37
Input PAIN14_KHJ PAIN 31
Input PAIN16_LSO PAIN 59
Input PAIN17_YJH PAIN 23
Input PAIN18_LEY PAIN 52
Input PAIN19_HJS PAIN 20
Input PAIN21_PJA PAIN 53
Input PAIN22_SGO PAIN 49
Input PAIN23_CEJ PAIN 41
Input PAIN24_OAH PAIN 49
Input PAIN25_PSG PAIN 38
Input PAIN26_LHC PAIN 31
Input PAIN27_HSK PAIN 36
Input NOR01_LSJ CON 26
Input NOR04_JJW CON 29
Input NOR06_HYH CON 27
Input NOR08_LYY CON 25
Input NOR09_JJK CON 25
Input NOR11_KYT CON 25
Input NOR14_WSW CON 25
Input NOR16_KYJ CON 28
Input NOR18_JJM CON 34
Input NOR19_KDS CON 37
Input NOR20_JJR CON 24
Input NOR21_JHK CON 35
Input NOR22_KJH CON 35
Input NOR23_CMH CON 40
Input NOR25_KMW CON 26
Input NOR27_YKS CON 24
Input NOR31_HKO CON 31
Input NOR32_LJW CON 32
Input NOR35_SNH CON 34
Input NOR37_LCJ CON 40
Input NOR38_LSJ CON 31
Input NOR39_KSY CON 35
Input NOR40_LJH CON 31
Input NOR41_SMH CON 46
Input NOR42_PSK CON 48
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
    --fsgd g2v2.fsgd \
    --target average \
    --hemi lh \
    --meas thickness \
    --out lh.group_age_iq.thickness.00.mgh

mri_surf2surf \
    --hemi lh \
    --s average \
    --sval lh.group_age_iq.thickness.00.mgh \
    --fwhm 20 \
    --cortex \
    --tval lh.group_age_iq.thickness.20B.mgh

mri_glmfit \
    --y lh.group_age_iq.thickness.20B.mgh \
    --fsgd g2v2.fsgd dods \
    --C group.diff.2cov.mtx \
    --surf average lh \
    --cortex \
    --glmdir lh.group_age_iq.20.glmdir

mri_glmfit-sim \
    --glmdir rh.group_age_iq.20.glmdir \
    --sim perm 5000 3 perm.negative \
    --sim-sign neg \
    --cwpvalthresh 0.05 \
    --overwrite \
    --perm-force&

#right
mris_preproc \
    --fsgd g2v2.fsgd \
    --target average \
    --hemi rh \
    --meas thickness \
    --out rh.group_age_iq.thickness.00.mgh

mri_surf2surf \
    --hemi rh \
    --s average \
    --sval rh.group_age_iq.thickness.00.mgh \
    --fwhm 20 \
    --cortex \
    --tval rh.group_age_iq.thickness.20B.mgh

mri_glmfit \
    --y rh.group_age_iq.thickness.20B.mgh \
    --fsgd g2v2.fsgd dods \
    --C group.diff.2cov.mtx \
    --surf average rh \
    --cortex \
    --glmdir rh.group_age_iq.20.glmdir

mri_glmfit-sim \
    --glmdir lh.group_age_iq.20.glmdir \
    --sim perm 5000 3 perm.negative \
    --sim-sign neg \
    --cwpvalthresh 0.05 \
    --overwrite \
    --perm-force

```

##Extraction script

```

export SUBJECTS_DIR=/Volumes/CCNC_3T/2013_12_painAnalysis/2013_08_23_pain_freesurfer/freesurfer_2014_04_03


echo "# ColHeaders StructName NumVert SurfArea GrayVol ThickAvg ThickStd MeanCurv GausCurv FoldInd CurvInd" > labelCollection/summary.txt

for i in PAIN01_KJD PAIN02_HIM PAIN03_LYN PAIN04_SSY PAIN05_LHY PAIN06_KCJ PAIN07_HMH PAIN08_PDK PAIN09_BHJ PAIN10_LHJ PAIN11_JSM PAIN12_LJM PAIN13_YEJ PAIN14_KHJ PAIN16_LSO PAIN17_YJH PAIN18_LEY PAIN19_HJS PAIN21_PJA PAIN22_SGO PAIN23_CEJ PAIN24_OAH PAIN25_PSG PAIN26_LHC PAIN27_HSK NOR01_LSJ NOR04_JJW NOR06_HYH NOR08_LYY NOR09_JJK NOR11_KYT NOR14_WSW NOR16_KYJ NOR18_JJM NOR19_KDS NOR20_JJR NOR21_JHK NOR22_KJH NOR23_CMH NOR25_KMW NOR27_YKS NOR31_HKO NOR32_LJW NOR35_SNH NOR37_LCJ NOR38_LSJ NOR39_KSY NOR40_LJH NOR41_SMH NOR42_PSK
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

