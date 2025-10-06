to reproduce our results:

OS required: linux/unix with tcsh shell & python installed, python package scikit-learn (https://scikit-learn.org/) must also be installed 

modify the script 
scan_all_jkn_boostrf_top1_ent_null_knowgene.job
scan_all_jkn_boostrf_top1_ent_null_knowgene_tr.job
to point the variable PYTHON to the python version that you installed scikit-learn



####
genes with known symptoms/side-effects are in 
all_gn_symGAN_symfreqge2.lst    column 1:  gene symbol; column 2: number of symptoms/side-effects it has
symptoms/side-effects are listed in
all_symGAN_side_red_symfreqge2.lst  column 1: UMLS_CUI  column 2: number of known genes causing it, column 3 to N-1: name column N (last): side effect or symptom label
The label file 
omim_sym_label_0.txt has the column's values according to the order in all_symGAN_side_red_symfreqge2.lst 

For all benchmarking gene-symptom/side-effect table see
all_phe_gn_symGAN_side_red_symfreqge2.tsv 


####
to predict gene to symptoms with leave one out:
#### important ####
#### if you do not have computer cluster to do this, it will take around 5000 days to finish all  4828 genes ####
#### because for each gene, one  has to train a model that take ~ 1 day on single node                       ####
#### thus, if you want to try this, use computer cluster by submit the jobs !!!                              ####
./scan_all_jkn_boostrf_top1_ent_null_knowgene.job

####
to predict gene to symptoms for novel genes:
this will take ~24 hours
./scan_all_jkn_boostrf_top1_ent_null_knowgene_tr.job

####
merge gene-symptom predictions:
./scan_all_jkn_boostrf_top1_ent_null_knowgene_kn.job


####
generate symptom/side-effect's gene list scores:
./scan_all_sym2gn_score.job 
results are in subdirectories
predsym2gn
predsym2novelgn

#### compare results at allpredsym2gn_me_(1-5).zip  && allpredsym2novelgn_me_(1-10).zip #### 
