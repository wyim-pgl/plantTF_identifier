Usage:

1. Prerequisites
   a. install hmmsearch
   b. run pfam_scan to identify pfam domain
2. Install plantTF_identifier
   git clone https://github.com/tangerzhang/plantTF_identifier.git
   mv plantTF_identifier /to/your/working/path/
3. run program
   perl TFinPlant.pl -i pfam.out -p protein.fasta
4. read results
   TFfamily/ directory contain members of each TF family
   member_num.txt is general statistics for each TF family
   gene.domain.txt contains domain signatures for each gene


```bash
i=opuntia_coche.fasta.pep.interpro_kegg

egrep -w "Pfam" ${i} | cut -f 1,4,5 > ${i}_pfam

aa=$(basename ${i} .interpro_kegg)
 perl TFinPlant.pl   -i  ${i}_pfam -p  $aa
mv TFfamily ${aa}_tf
cd  ${aa}_tf
for j in `ls -1 `; do name=$(basename ${j} .txt); no_tf=$(wc -l ${j} | cut -f 1 -d " "); sed -i "s/^/${name}\t/g; s/$/\t${no_tf}/g" $j; done
cat *.txt >> ${i}_all_tf.tab
cd ../
```
