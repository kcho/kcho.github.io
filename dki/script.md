#Script


##Preprocessing
```
for i in $@
do
    echo ${i}
    ##=============================================
    ## Eddy current correction
    ##=============================================
    #eddy_correct ${i}/*.nii.gz ${i}/dki_eddy.nii.gz 0 

    ##=============================================
    ## Extract B0 image from DKI
    ##=============================================
    #fslroi ${i}/DKI/dki_eddy.nii.gz ${i}/DKI/nodif.nii.gz 0 1


    ##=============================================
    ## registration DKI nodif <-- freesurfer
    ##=============================================
    #mkdir ${i}/registration
    #echo -ne '\tFlirt\n'
    #mri_convert ${i}/freesurfer/mri/brain.mgz ${i}/freesurfer/mri/brain.nii.gz
    #flirt -in ${i}/freesurfer/mri/brain.nii.gz \
        #-ref ${i}/dki/nodif.nii.gz \
        #-dof 6 \
        #-omat ${i}/registration/FreesurferToDKI \
        #-out ${i}/registration/prac_freesurferToDKI.nii.gz

```


##Registration
```
    ##=============================================
    ## registration DTI nodif <-- freesurfer
    ##=============================================
    if [ ! -e ${i}/freesurfer/mri/brain.nii.gz ]
    then
        mri_convert ${i}/freesurfer/mri/brain.mgz ${i}/freesurfer/mri/brain.nii.gz
    fi

    if [ ! -e ${i}/registration/freesurferT1toFA.mat ]
    then
        /usr/local/fsl/bin/flirt \
            -in ${i}/freesurfer/mri/brain.nii.gz \
            -ref ${i}/DTI/dti_FA.nii.gz \
            -out ${i}/registration/freesurferT1toFA \
            -omat ${i}/registration/freesurferT1toFA.mat \
            -bins 256 \
            -cost mutualinfo \
            -searchrx -180 180 \
            -searchry -180 180 \
            -searchrz -180 180 \
            -dof 6  -interp trilinear
    fi

    if [ ! -e ${i}/registration/freesurferT1toNodif.mat ]
    then
        /usr/local/fsl/bin/flirt \
            -in ${i}/freesurfer/mri/brain.nii.gz \
            -ref ${i}/DTI/nodif_brain.nii.gz \
            -out ${i}/registration/freesurferT1toNodif \
            -omat ${i}/registration/freesurferT1toNodif.mat \
            -bins 256 \
            -cost mutualinfo \
            -searchrx -180 180 \
            -searchry -180 180 \
            -searchrz -180 180 \
            -dof 6  -interp trilinear
    fi
```

##Extract ROI from freesurfer
```

    ##=============================================
    ## Extract ROIs from the freesurfer output
    ##     1. Registration of ROIs to diffusion space
    ##=============================================
    #mkdir ${i}/ROI
    #./roiExtractionOrig.py -S ${i}

    #echo -ne '\tROI\n'
    #for imgs in ${i}/ROI/[rl]h*
    #do
        #filename=$(basename "$imgs")

        #flirt -in ${imgs} \
            #-ref ${i}/DKI/nodif.nii.gz \
            #-applyxfm -init ${i}/registration/FreesurferToDKI \
            #-cost mutualinfo \
            #-out ${i}/ROI/dki_${filename}
    #done




    ##=============================================
    ## Extra ROI extraction
    ##=============================================
    #./roiExtraction.py -s ${i}

```

##Apply registration
```
    ##=============================================
    ## Registration of the extra ROIs
    ##=============================================
    #echo -ne '\tROI\n'
    #for imgs in ${i}/extraROIs/*
    #do
        #filename=$(basename "$imgs")

        #flirt -in ${imgs} \
            #-ref ${i}/DKI/nodif.nii.gz \
            #-applyxfm -init ${i}/registration/FreesurferToDKI \
            #-cost mutualinfo \
            #-interp nearestneighbour\
            #-out ${i}/ROI/dki_${filename}
    #done

```


##Prac tractography
```
    ##=============================================
    ## tractography 
    ##=============================================
    
    if [ ! -e ${i}/segmentation/left/fdt_paths.nii.gz ]
    then
        rm -rf ${i}/segmentation/left 
        mkdir -p ${i}/segmentation/left
        echo ${i}/extraROIs/lh_LPFC.nii.gz > ${i}/segmentation/left/targets.txt
        echo ${i}/extraROIs/lh_LTC.nii.gz >> ${i}/segmentation/left/targets.txt
        echo ${i}/extraROIs/lh_MPFC.nii.gz >> ${i}/segmentation/left/targets.txt
        echo ${i}/extraROIs/lh_MTC.nii.gz >> ${i}/segmentation/left/targets.txt
        echo ${i}/extraROIs/lh_OCC.nii.gz >> ${i}/segmentation/left/targets.txt
        echo ${i}/extraROIs/lh_OFC.nii.gz >> ${i}/segmentation/left/targets.txt
        echo ${i}/extraROIs/lh_PC.nii.gz >> ${i}/segmentation/left/targets.txt
        echo ${i}/extraROIs/lh_SMC.nii.gz >> ${i}/segmentation/left/targets.txt
        probtrackx --mode=seedmask -x ${i}/extraROIs/lh_thalamus.nii.gz -l -c 0.2 -s 2000 --steplength=0.5 -P 5000 --xfm=${i}/registration/freesurferT1toNodif.mat --forcedir --opd -s ${i}/dti.bedpostx/merged -m ${i}/dti.bedpostx/nodif_brain_mask --dir=${i}/segmentation/left --targetmasks=${i}/segmentation/left/targets.txt --os2t
        echo ${i} segmentation on the left done
    else
        echo ${i} segmentation on the left done
    fi 

    if [ ! -e ${i}/segmentation/right/fdt_paths.nii.gz ]
    then
        rm -rf ${i}/segmentation/right
        mkdir -p ${i}/segmentation/right
        echo ${i}/extraROIs/rh_LPFC.nii.gz > ${i}/segmentation/right/targets.txt
        echo ${i}/extraROIs/rh_LTC.nii.gz >> ${i}/segmentation/right/targets.txt
        echo ${i}/extraROIs/rh_MPFC.nii.gz >> ${i}/segmentation/right/targets.txt
        echo ${i}/extraROIs/rh_MTC.nii.gz >> ${i}/segmentation/right/targets.txt
        echo ${i}/extraROIs/rh_OCC.nii.gz >> ${i}/segmentation/right/targets.txt
        echo ${i}/extraROIs/rh_OFC.nii.gz >> ${i}/segmentation/right/targets.txt
        echo ${i}/extraROIs/rh_PC.nii.gz >> ${i}/segmentation/right/targets.txt
        echo ${i}/extraROIs/rh_SMC.nii.gz >> ${i}/segmentation/right/targets.txt
        probtrackx --mode=seedmask -x ${i}/extraROIs/rh_thalamus.nii.gz -l -c 0.2 -s 2000 --steplength=0.5 -P 5000 --xfm=${i}/registration/freesurferT1toNodif.mat --forcedir --opd -s ${i}/dti.bedpostx/merged -m ${i}/dti.bedpostx/nodif_brain_mask --dir=${i}/segmentation/right --targetmasks=${i}/segmentation/right/targets.txt --os2t &\
    else
        echo ${i} segmentation on the right done
    fi
```

##Extract k values
```
    ##=============================================
    ## Extract values of kax, krad and kmean 
    ## within the mask
    ##=============================================

    #rm ${i}/DKI/mean.txt
    #rm ${i}/DKI/std.txt
    #for dkiImage in ${i}/DKI/k*nii
    #do
        
        #dkiImagename=$(basename "$dkiImage")
        

        #for mask in ${i}/ROI/dki*nii.gz
        #do
            #maskname=$(basename "$mask")
            #origname=${maskname:4} 
            
            #echo $dkiImagename $maskname `fslstats ${dkiImage} -k ${mask} -M` `fslstats ${i}/extraROIs/${origname} -V` >> ${i}/DKI/mean.txt
            #echo $dkiImagename $maskname `fslstats ${dkiImage} -k ${mask} -S` >> ${i}/DKI/std.txt
        #done

    #done

done
```

