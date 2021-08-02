# Phage CRISPRi

The primary intent of these scripts is to aid in the generation of primers for use in Cas-designed silencing approaches. The scripts will generate, for each gene in a specified genome, up to two pairs of primers (fwd/rev) that contain spacer regions immediately downstream of a PAM site on the gene to target. To this end, one can specify the following parameters:
 1. PAM site(s) of the sequences to be targeted
 2. Ideal downstream% of the primers in the gene
 3. Length of the sequence to be extracted

The script takes as input the NCBI accession number of the genome to generate primers for, as well as filepaths to the FASTA and gff files corresponding to this genome. FASTA and gff files are assumed to be named according to the accession number (so, if the accession number is "NC_005856.1", the FASTA file would be named "NC_005856.1.fasta" and the gff file would be named "NC_005856.1.gff3").

When run, the script will access the gff file to extract the locations of all of the genes in the genome, and use the FASTA file to access the corresponding sequences. The script will then do the following for each gene in the genome:
 1. Search through the gene to identify all locations of the PAM sites specified by the user that are at least a distance of _length-to-be-extracted_ apart (so, if the specified PAM sites were "TTTC" and "TTTG" and the length of seq. to be extracted was 8, then this step would only identify two locations from the following sequence: "TTTCATTTGACCGTTTC"; it would not identify the "TTTG" sequence, as it is fewer than 8 nucleotides away from an earlier PAM site).
 2. If more than two locations are identified, identify which two are closest to the user-specified ideal downstream%. Discard all others.
 3. Extract a sequence of length _length-to-be-extracted_ immediately following the PAM site of each identified location.
 4. Perform some minor post-processing, and format a forward and reverse primer around these sequences.
