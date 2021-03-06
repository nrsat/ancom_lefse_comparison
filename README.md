# ancom_lefse_comparison
Comparing ANCOM and LEfSe for differential abundance testing.

## Input data
Sample input file provided in wikipedia of LEfSe. I removed class Mid_O2, thus comparing Low_O2 and High_O2 
(hmp_small_aerobiosis.txt, https://bitbucket.org/biobakery/biobakery/wiki/lefse).

## LEfSe
- All level
- Without subclass
- With subclass (body_site)

```
format_input.py hmp_lefse_sub.txt lefse.lefse -f r -u 2 -c 1 -o 1000000
run_lefse.py -s 0 --verbose 0 -l 2 --wilc 0 -b 100 -r lda lefse.lefse lefse.sub.res

Number of significantly discriminative features: 120 ( 0 ) before internal wilcoxon
Number of discriminative features with abs LDA score > 2.0 : 120

format_input.py hmp_lefse_all.txt lefse.lefse -f r -u 3 -c 1 -s 2 -o 1000000
run_lefse.py -s 0 --verbose 0 -l 2 --wilc 1 -b 100 -r lda lefse.lefse lefse.all.res

Number of significantly discriminative features: 63 ( 120 ) before internal wilcoxon
Number of discriminative features with abs LDA score > 2.0 : 63
```

## ANCOM
Used R scripts for ANCOM (https://github.com/FrederickHuangLin/ANCOM).
Modifed to reject null hypothesis by setting W threshold automatically, although the author of original paper stated that they typically recommend the threshold of 0.7 according to https://forum.qiime2.org/t/ancom-low-w-taxa-identified-as-significant-issues-workaround-ancom2-code-instructions/6040. In this comparison, genus with W above W[0.9] is considered significant.   

- Genus only
- Without covariate
- With covariate (body_site)

## Visualization
Genus that were significantly different between High_O2 and Low_O2 were compared by an upset plot.  

ComplexHeatmap (https://github.com/jokergoo)  
firatheme (https://github.com/vankesteren/firatheme/)

- Volcano plot
![volcano_plot](https://raw.githubusercontent.com/nrsat/ancom_lefse_comparison/master/volcano_plot.png)
- Upset plot
![upset_plot](https://raw.githubusercontent.com/nrsat/ancom_lefse_comparison/master/upset_plot.png)