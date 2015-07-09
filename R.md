#R

## Ubuntu

* Install
  ```
  sudo apt-get update
  sudo apt-get install r-base
  ```

* Run interactively
  ```
  R
  ```
  and `quit()` to quit.

* Run script
  ```
  Rscript <script>.R
  ```

* Installing packages
  ```
  > install.packages("randomForest")
  Installing package into "/usr/local/lib/R/site-library"
  (as "lib" is unspecified)
  Warning in install.packages("randomForest") :
    'lib = "/usr/local/lib/R/site-library"' is not writable
  Would you like to use a personal library instead?  (y/n) y
  Would you like to create a personal library
  ~/R/x86_64-pc-linux-gnu-library/3.0
  to install packages into?  (y/n) y
  --- Please select a CRAN mirror for use in this session ---
  CRAN mirror
  
   1: 0-Cloud                       2: Algeria
   3: Argentina (La Plata)          4: Australia (Canberra)
   5: Australia (Melbourne)         6: Austria
   7: Belgium                       8: Brazil (BA)
   9: Brazil (PR)                  10: Brazil (RJ)
  11: Brazil (SP 1)                12: Brazil (SP 2)
  13: Canada (BC)                  14: Canada (NS)
  15: Canada (ON)                  16: Canada (QC 1)
  17: Canada (QC 2)                18: Chile
  19: China (Beijing 2)            20: China (Beijing 3)
  21: China (Beijing 4)            22: China (Hefei)
  23: China (Xiamen)               24: Colombia (Cali)
  25: Czech Republic               26: Denmark
  27: Ecuador                      28: El Salvador
  29: Estonia                      30: France (Lyon 1)
  31: France (Lyon 2)              32: France (Montpellier)
  33: France (Paris 2)             34: Germany (Berlin)
  35: Germany (Goettingen)         36: Germany (Frankfurt)
  37: Germany (MÃ¼nster)            38: Greece
  39: Hungary                      40: Iceland
  41: India                        42: Indonesia (Jakarta)
  43: Iran                         44: Ireland
  45: Italy (Milano)               46: Italy (Padua)
  47: Italy (Palermo)              48: Japan (Tokyo)
  49: Japan (Yamagata)             50: Korea (Seoul 1)
  51: Korea (Seoul 2)              52: Korea (Ulsan)
  53: Lebanon                      54: Mexico (Mexico City)
  55: Mexico (Texcoco)             56: Netherlands (Amsterdam)
  57: Netherlands (Utrecht)        58: New Zealand
  59: Norway                       60: Philippines
  61: Poland                       62: Portugal
  63: Russia (Moscow 1)            64: Russia (Moscow 2)
  65: Slovakia                     66: South Africa (Johannesburg)
  67: Spain (A CoruÃ±a)             68: Spain (Madrid)
  69: Sweden                       70: Switzerland
  71: Taiwan (Chungli)             72: Taiwan (Taipei)
  73: Thailand                     74: Turkey
  75: UK (Bristol)                 76: UK (Cambridge)
  77: UK (Hampshire)               78: UK (London)
  79: UK (London)                  80: UK (St Andrews)
  81: USA (CA 1)                   82: USA (CA 2)
  83: USA (IA)                     84: USA (IN)
  85: USA (KS)                     86: USA (MD)
  87: USA (MI 1)                   88: USA (MI 2)
  89: USA (MO)                     90: USA (OH 1)
  91: USA (OH 2)                   92: USA (OR)
  93: USA (PA 1)                   94: USA (PA 2)
  95: USA (TN)                     96: USA (TX 1)
  97: USA (WA 1)                   98: Venezuela
  99: Vietnam
  
  Selection: 81
  trying URL 'http://cran.cnr.Berkeley.edu/src/contrib/randomForest_4.6-10.tar.gz'
  Content type 'application/x-gzip' length 79096 bytes (77 Kb)
  opened URL
  ==================================================
  downloaded 77 Kb
  
  * installing *source* package "randomForest" ...
  ** package "randomForest" successfully unpacked and MD5 sums checked
  ** libs
  gcc -std=gnu99 -I/usr/share/R/include -DNDEBUG      -fpic  -O3 -pipe  -g  -c classTree.c -o classTree.o
  gcc -std=gnu99 -I/usr/share/R/include -DNDEBUG      -fpic  -O3 -pipe  -g  -c regTree.c -o regTree.o
  gcc -std=gnu99 -I/usr/share/R/include -DNDEBUG      -fpic  -O3 -pipe  -g  -c regrf.c -o regrf.o
  gcc -std=gnu99 -I/usr/share/R/include -DNDEBUG      -fpic  -O3 -pipe  -g  -c rf.c -o rf.o
  gfortran   -fpic  -O3 -pipe  -g  -c rfsub.f -o rfsub.o
  gcc -std=gnu99 -I/usr/share/R/include -DNDEBUG      -fpic  -O3 -pipe  -g  -c rfutils.c -o rfutils.o
  gcc -std=gnu99 -shared -o randomForest.so classTree.o regTree.o regrf.o rf.o rfsub.o rfutils.o -lgfortran -lm -lquadmath -L/usr/lib/R/lib -lR
  installing to /home/ubuntu/R/x86_64-pc-linux-gnu-library/3.0/randomForest/libs
  ** R
  ** data
  ** inst
  ** preparing package for lazy loading
  ** help
  *** installing help indices
  ** building package indices
  ** testing if installed package can be loaded
  * DONE (randomForest)
  
  The downloaded source packages are in
          "/tmp/RtmpKQO48c/downloaded_packages"
  >
  ```
