# **MAOS**

# **MAOS: Meta-Analysis with Overlapping Subjects**

Data from genome-wide association studies are often analyzed jointly for the purposes of combining information from multiple studies of the same disease or comparing results across different disorders. In many instances, the same subjects appear in multiple studies. Failure to account for overlapping subjects can greatly inflate type I error when combining results from multiple studies of the same disease and can drastically reduce power when comparing results across different disorders. MAOS implements valid and efficient statistical methods for meta-analysis of genomewide association studies with overlapping subjects, as described in Lin and Sullivan (submitted for publication, 2009). The [current release ](http://dlin.web.unc.edu/software/maos/)performs logistic regression analysis of individual level data under the additive mode of inheritance. (Meta-analysis of summary results is much simpler to implement.) We are working intensely to improve the capabilities of MAOS, so please check back frequently for updates.

## **General information**

The program is written in C++ language. Executable files are available for Windows and i386-based Linux in the download section below.

## **Usage**

On Windows systems:

> `maos.exe --pheno phenotype_file --geno genotype_file --out output_file`

On Linux systems:

> `maos --pheno phenotype_file --geno genotype_file --out output_file`

## **Input**

This software requires two input files: a phenotype file and a genotype file. The phenotype file contains information about the case-control status, subject identification number (ID), and covariates. The genotype file contains the SNP genotype information. Both files are plain text files in a matrix-like layout. The name of the phenotype file is specified with the `--pheno` command-line option; the name of the genotype file is specified with the `--geno` command-line option.

### **Phenotype file**

The phenotype file is a plain text file with *n* rows and *m* columns. The rows represent subjects. Each subject contributes as many rows as the number of times he/she appeared in the studies. The columns are separated by one or more white spaces (the space character or the TAB character). The columns have fixed meanings, as described below:

> **Column 1**: Subject ID. This column is required and is alpha-numerical. No missing values are allowed. Each study subject is attached with a unique ID. Any subject who appears in multiple studies must have the same ID for the multiple records.

> **Column 2**: Case-control status. This column is required and indicates by the values 1 versus 0 whether the subject is a case or a control. All values other than 0 and 1 are treated as missing.

> **Column 3 – column *m***: Covariates. These columns are optional and contain covariate values. Covariates include study indicators and environmental variables. All covariate values are numerical. Missing values are indicated by -999. All covariates are entered into the model as they are. Any categorical covariate with more than two levels needed to be transformed to appropriate dummy variables by the user.

### **Genotype file**

The genotype file is a plain text file with *s* rows and *n*+1 columns, where *n* is the number of rows of the corresponding phenotype file. The *s* rows represent *s* SNPs with one SNP in each row. The columns are separated by one or more white spaces (the space character or the TAB character). The columns must have the following format:

> **Column 1**: SNP ID. This column is required and is alpha-numerical. No missing values are allowed.

> **Column 2 – column (*n*+1)**: Genotype values. The *j*-th column of the *i*-th row pertains to the value of the *i*-th SNP for the (*j*-1)-th subject in the phenotype file. Accepted genotype values are 0, 1, and 2. Missing values are indicated by 9.

## **Output**

This software writes computational results to the output file named by the user with the `--out` command-line option. This software reports the results for all SNPs in the same order as they appear in the genotype file. For each SNP, the output file shows the parameter estimates, standard errors, standard-normal test statistics, and p-values for the SNP effect (labeled by `SNP effect`), as well as the covariate effects (labeled by `Covariate1`, `Covariate2`, …) if there are covariates in the phenotype file.

## **Example**

A set of example files are provided within each downloadable package below. File [`maos_demo.phe`](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2011/08/maos_demo.zip)is the example phenotype file, and file [`maos_demo.gen`](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2019/05/maos_demo.zip)is the example genotype file. These two files contain data extracted from the [Wellcome Trust Case Control Consortium](http://www.wtccc.org.uk/) (WTCCC). In this example, we treat RA and T1D as cases of two different studies (called Study 1 and Study 2 below), and 58C and NBS as common controls for the two studies. There are 1860 and 1963 cases for Study 1 and Study 2, respectively, with 2938 common controls. All 2938 controls are assigned to both Study 1 and Study 2. As a result, there are (1860+1963)+2\*2938 = 9699 rows in the phenotype file [`maos_demo.phe` ](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2011/08/maos_demo.zip). There is a unique ID for each subject. Each control contributes two rows, with the same ID.

In file [`maos_demo.phe` ](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2011/08/maos_demo.zip), the columns are as follows:

> Column 1: subject ID\
> \
> Column 2: Case-control status\
> \
> Column 3: Covariate 1 = study indicator (Study1=1; Study 2=0)\
> \
> Column 4: Covariate 2 = sex

There are 9699 rows and 4 columns, or 9699 subjects and two covariates.

The example genotype file [`maos_demo.gen` ](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2011/08/maos_demo.zip)contains genotype information on the 8 SNPs that were found to be significantly associated with RA and/or T1D by WTCCC. It has 8 rows and 9700 columns. Column 1 pertains to the SNP rs number. Columns 2 – column 9700 contain the genotype values for the 9699 subjects, in the same order as they appear in the rows of the phenotype file.

The example output file [`maos_demo.out`](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2011/08/maos_demo.zip)was generated by command

> `maos.exe --pheno maos_demo.phe --geno maos_demo.gen --out maos_demo.out`

The output file contains numerical results for the 8 SNPs in the genotype file. For each SNP, the results include the point estimate, standard error, z-statistic, and p-value for three parameters:

> SNP effect\
> Covariate 1\
> Covariate 2

## **Reference**

Lin DY, Sullivan PF. 2009. [Meta-Analysis of Genome-wide Association Studies with Overlapping Subjects](https://www.ncbi.nlm.nih.gov/pubmed/20004761). [The American Journal of Human Genetics](http://www.cell.com/AJHG/home), 85:862-872.

## **Download**

#### **MAOS package for Windows \[updated: 7 October 2009\]**

Executable file and example files **»** [maos-1.2-win.zip](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2011/08/maos-1.2-win.zip)

#### **MAOS package for i386-based Linux \[updated: 7 October 2009\]**

Executable file and example files **»** [maos-1.2-linux.tar.gz](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2011/08/maos-1.2-linux.tar_.gz)

Static executable file and example files **»** [maos-1.2-linux-static.tar.gz](http://dlin.web.unc.edu/wp-content/uploads/sites/1568/2011/08/maos-1.2-linux-static.tar_.gz)
