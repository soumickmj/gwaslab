#  Brisbane plot

##  1. Brisbane plot : GWAS signal density plot

GWASLab can create the [Brisbane plot](https://www.nature.com/articles/s41586-022-05275-y/figures/2) (GWAS signal density plot). Brisbane plot is a scatter plot that shows the signal density (number of variants within the 500 Kb flanking region of the reference variant) for each variant, which is very useful for presenting the independent signals obtained from large-scale GWAS of complex traits. The signals are usually determined by other statistical methods such as conditional analysis. 


### 1.1 Usage

```
mysumstats.plot_mqq(mode="b")
```

!!! note
    To create Brisbane plot using this function, you just need to load the sumstats of indenpedent signals. If you load the entire datasets, the plot will simply reflect the marker density for your sumstats. To investigate indenpedent signals, please use other tools such as GCTA-COJO. GWASLab only calculates the density of all variants in the gl.Sumstats Object.

### 1.2 Options

|Option|DataType|Description|Default|
|-|-|-|-|
|`mode`|`b`|specify Brisbane plot mode|-|
|`bwindowsizekb`|`int`|windowsize in kb (flanking region length on one side)|`100`|


### 1.3 Example
!!! example "Brisbane plot"
    
    Data was obtained from : Yengo, L., Vedantam, S., Marouli, E., Sidorenko, J., Bartell, E., Sakaue, S., ... & Lee, J. Y. (2022). A saturated map of common genetic variants associated with human height. Nature, 1-16.

    ```python
    mysumstats = gl.Sumstats("height_lead.tsv",
                 snpid="SNP",
                 chrom="Chr",
                 pos="BP_HG19",
                 p="P-value")
                 
    mysumstats.plot_mqq(mode="b",anno="GENENAME",
                      build="19",anno_fixed_arm_length=2,
                      anno_args={"rotation":90},
                      marker_size=(30,30),sig_line_color="red")
    ```
    
    <img width=600 src="https://user-images.githubusercontent.com/40289485/197393168-e3e7076f-2801-4d66-9526-80778d44f3da.png">


## 2. Calculate the density for sumstats

```
mysumstats.get_density(windowsizekb=100)
```

Or you can use `.get_density()` to just calculate the density.

|Option|DataType|Description|Default|
|-|-|-|-|
|`windowsizekb`|`int`|window size for calculation of signal density. `DENSITY` |`100`|


!!! example "Calculate signal density"

    ```
    mysumstats.get_density(windowsizekb=100)
    
    mysumstats.data
    	SNPID	CHR	POS	P	STATUS	DENSITY
    0	rs2710888	1	959842	2.190000e-57	9999999	1
    1	rs3934834	1	1005806	2.440000e-29	9999999	1
    2	rs182532	1	1287040	1.250000e-18	9999999	1
    3	rs17160669	1	1305561	1.480000e-28	9999999	1
    4	rs9660106	1	1797947	1.860000e-12	9999999	0
    ...	...	...	...	...	...	...
    12106	rs9628283	22	50540766	5.130000e-15	9999999	1
    12107	rs28642259	22	50785718	1.140000e-13	9999999	1
    12108	rs11555194	22	50876662	2.000000e-15	9999999	2
    12109	rs762669	22	50943423	3.000000e-30	9999999	1
    12110	rs9628185	22	51109992	5.430000e-12	9999999	0
    ```

## Reference
!!! quote "Citation for Brisbane plot"
    Yengo, L., Vedantam, S., Marouli, E., Sidorenko, J., Bartell, E., Sakaue, S., ... & Lee, J. Y. (2022). A saturated map of common genetic variants associated with human height. Nature, 1-16.