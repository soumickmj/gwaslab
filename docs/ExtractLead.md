# Extract lead variants

GWASLab can extract the lead variants based on P values or MLOG10P values from identified significant loci using a sliding window, and return the result as a pandas.DataFrame or gl.Sumstats Object.

## 1. get_lead()

```python
mysumstats.get_lead(
           scaled=False,
           windowsizekb=500,
           sig_level=5e-8,
           anno=False,
           build="19",
           source="ensembl",
           verbose=True,
           gls=False)
```

## 2. Options

|`.get_lead()` options|DataType|Description|Default|
|-|-|-|-|
|`scaled`|`boolean`|If True, use MLOG10P for extraction instead of P values|`False`|
|`windowsizekb`|`int`|Specify the sliding window size in **kb**|`500`|
|`sig_level`|`float`|Specify the P value threshold|`5e-8`|
|`anno`|`boolean`|If True, annotate the lead variants with nearest gene names.|`False`|
|`source`|`ensembl` or `refseq`| When `anno=True`, annotate variants using gtf files from `ensembl` or `refseq`|`ensembl`|
|`build`|`"19"` or `"38"`|genome build version "19" or "38".|`"19"`|
|`verbose`|`boolean`|If True, print logs|`True`|
|`gls`|`boolean`|If True, return a new gl.Sumstats Object instead of pandas DataFrame|`False`|

!!! note 
    `.get_lead()` simply extract the lead variants of each significant loci. It is different from clumping.

!!! note 
    Please trying running `.basic_check()` to standardize the sumstats if there are any errors.

!!! quote
    GWASLab basically adopted the definition for novel loci from Global Biobank Meta-analysis Initiative flagship paper. 
    
    **"We defined genome-wide significant loci by iteratively spanning the ±500 kb region around the most significant variant and merging overlapping regions until no genome-wide significant variants were detected within ±1 Mb."** 
    
    (Details are described in Zhou, W., Kanai, M., Wu, K. H. H., Rasheed, H., Tsuo, K., Hirbo, J. B., ... & Study, C. O. H. (2022). Global Biobank Meta-analysis Initiative: Powering genetic discovery across human disease. Cell Genomics, 2(10), 100192. )

    GWASlab currently iteratively extends ± `windowsizekb` kb region around the most significant variant and merges overlapping regions until no genome-wide significant variants were detected within ± `windowsizekb`. (slightly different from the GBMI paper. When `windowsizekb=1000`, it is equvalent to GBMI's definition.)


## 3. Example

!!! example
    Sample sumstats: IS from pheweb.jp [https://pheweb.jp/pheno/IS](https://pheweb.jp/pheno/IS)
    ![image](https://user-images.githubusercontent.com/40289485/196447159-f9b41510-feb6-4ec8-adeb-a8f4c3683061.png)
    ```
    mysumstats = gl.Sumstats("./hum0197.v3.BBJ.IS.v1/GWASsummary_IS_Japanese_SakaueKanai2020.auto.txt.gz",  fmt="saige")
    mysumstats.get_lead()
    ```
    ![image](https://user-images.githubusercontent.com/40289485/196446293-c8f9c2d3-82c3-4122-bddd-184b43f2950f.png)

