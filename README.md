MicrobeDB
=
###ABOUT###
MicrobeDB provides centralized local storage and access to completed Archaea and Bacteria genomes.

MicrobeDB contains three main features. 
1)All "flat" files associated with the each genome are downloaded from NCBI (http://www.ncbi.nlm.nih.gov/genomes/lproks.cgi) and stored locally in a directory of your choosing.

2)For each genome, information about the organism, chromosomes within the organism, and genes within each chromosome are parsed and stored in a MySQL database including sequences and annotations.

3)A Perl API is provided to interface with the MYSQL database and allow easy use of the data.

A presentation providing more information about MicrobeDB is online at: http://tinyurl.com/microbedb

###INSTALL###
For installation information see:
information/INSTALL/INSTALL

###REQUIREMENTS###
MySQL
Perl
Perl Modules
-BioPerl
-Parallel::ForkManager
-Log::Log4perl
-Sys::CPU

###QUICK START GUIDE###

1)Connecting directly to MySQL database
database name:microbedb

"mysql -u perlapi -p"

2)Using MicrobeDB Perl API
At the start of your perl script you need:
use lib '/your/path/to/MicrobeDB';
use MicrobeDB::Search;

See example in "information/example_scripts";

#########################

###Overview of MicrobeDB###
*Note: Information below is available as a Powerpoint presentation in "information/Basic_Overview_MicrobeDB.ppt"

MicrobeDB
Centralized storage and access to completed Archaea and Bacteria genomes
Same as those available at: http://www.ncbi.nlm.nih.gov/genomes/lproks.cgi

Genome/Flat files are stored in one central location

Information at the genome project, chromosome, and gene level are parsed and stored in a MySQL database 
including sequences and annotations 

The files and the database are updated monthly

File Structure

Bacteria (sym-linked to the most recent download folder)
Bacteria_2009-09-01(Version)
Acaryochloris_marina_MBIC11017
Acholeplasma_laidlawii_PG_8A
Acidimicrobium_ferrooxidans_DSM_10331
Acidiphilium_cryptum_JF-5
NC_009467.asn
NC_009467.faa
NC_009467.ffn
NC_009467.fna
NC_009467.gbk
NC_009467.GeneMark-2.5m
NC_009467.GeneMarkHMM-2.6r
NC_009467.gff
NC_009467.Glimmer3
NC_009467.Prodigal-1.10
NC_009467.ptt
NC_009467.rps
NC_009467.rpt
… for each replicon (i.e. chromosome and plasmid)
Acidithiobacillus_ferrooxidans_ATCC_23270
Acidithiobacillus_ferrooxidans_ATCC_53993
…~950 genome projects

MySQL

Version
Each monthly download from NCBI is given a new version number
Advantages
Data will not change if you always use the same version number of microbedb
Version date can be cited for any method publications
Disadvantages
Data is redundant in the database (e.g. multiple versions of the same gene)
A version number (version_id) must always be used when retrieving information otherwise multiple copies will be returned 

Genomeproject
Contains information about the genome project and the organism that was sequenced
E.g. taxon_id, org_name, lineage, gram_stain, genome_gc, patho_status, disease, genome_size, pathogenic_in, temp_range, habitat, shape, arrangement, endospore, motility, salinity, etc.
Each genomeproject contains one or more replicons

Replicon
Chromosome or plasmids
E.g. rep_accnum, definition, rep_type, rep_ginum, cds_num, gene_num, protein_num, genome_id, rep_size, rna_num, rep_seq (complete nucleotide sequence)
Each replicon contains one or more genes

Gene
Contains gene annotations and also the DNA and protein sequences (if protein coding gene)
E.g. gid, pid, protein_accnum, gene_type, gene_start, gene_end, gene_length, gene_strand, gene_name, locus_tag, gene_product, gene_seq, protein_seq
