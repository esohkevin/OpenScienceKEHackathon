#Retrieving Papers from NCBI's PubMed Using EDirect
EDirect is NCBI's commandline Entrez retrieval tool. It is used to retrieve data from a variety of NCBI database, including literature mining from PubMed.
[Insiders Guide to Accessing NLM Data: EDirect Overview](https://dataguide.nlm.nih.gov/edirect/overview.html)

##Installing EDirect
Run the code
```
$ cd ~
  /bin/bash
  perl -MNet::FTP -e \
    '$ftp = new Net::FTP("ftp.ncbi.nlm.nih.gov", Passive => 1);
     $ftp->login; $ftp->binary;
     $ftp->get("/entrez/entrezdirect/edirect.tar.gz");'
  gunzip -c edirect.tar.gz | tar xf -
  rm edirect.tar.gz
  builtin exit
  export PATH=${PATH}:$HOME/edirect >& /dev/null || setenv PATH "${PATH}:$HOME/edirect"
  ./edirect/setup.sh
```

Hit ```Enter``` when you find your cursor blinking on the command ```$ ./edirect/setup.sh```

##Completing Installation
Run the command
```
$ echo "export PATH=\$PATH:\$HOME/edirect" >> $HOME/.bash_profile
```

##Check and Confirm Installation

```
$ esearch -version
```
This should display the most recent version of the tool.

##Example PubMed Search
```
$ esearch -db pubmed -query "Open AND Science[Title]" -datetype PDAT -mindate 2010 - maxdate 2018 | \
  efetch -format xml | \
  xtract -pattern PubmedArticle -element MedlineCitation/PMID > pmids.txt
```
This retrieves the PubMed ID of articles titled "Open Science" from PubMed published between 2010 and 2018

###More on EDirect commands can be found on
###[Entrez Direct: E-utilities on the UNIX Command Line](https://www.ncbi.nlm.nih.gov/books/NBK179288/)
###[NCBI-Hackathons/EDirectCookbook](https://github.com/NCBI-Hackathons/EDirectCookbook)

