Here are the basic instructions on Karrick's directory.  

Log normal work is done in lnNDatacardWork

Shapetesting is the many folder where everything regarding shapes is done.  The most recent work and versions of code will be found in Total_Run
Systematic work is the notebook that creates shapefiles.










================================================================================
Setup Tools
===========

To setup the cms environment, run these in CMSSW/src
source /cvmfs/cms.cern.ch/cmsset_default.sh
cmsenv

To setup the Higgs combine tool, run these in CombinedLimit
. env_standalone.sh
make -j 4

================================================================================
Create Shape files
==================

The Most recent code for generating shape files is
cms-top/kmcgint/HiggsAnalysis/Shapetesting/Total_Run/Systematic work

In order to create a shape file, run the second cell (the one after the imports).  This will copy over all histogram files from Mason's directory over to Total_Run.  In order to specify a different era, change the directory of SourceLoc to be where you want to take the histograms from and then change the variable fileEnding to be the ending of the root files in that directory.  Here are the current ones.

2016 preVFP -> 2016ULpreVFP
2016 postVFP -> 2016ULPostVFP
2017 -> 2017UL
2018 -> 2018UL

Don't include the .root.
Once the cell block finishes, all histograms will be copied over and it will print out the hadd command needed to combine them into a root file with the name (fileEnding).root.  Run this in the directory.  However, the histograms that have to be combined afterwards with methods such as enveloping still need to be combined.  To do this, run the next cell and it will do this work from the combined root file.  Now the only thing that is left is the electron reconstruction histograms which must be done afterwards due to the way the code is written.  Just run the next code block and it should add electron reconstruction histograms and provide an updated hadd command to run.  


--------------------------------------------------------------------------------
Common errors

If you run Combine and it says that it can't find ttbar_MESCUp or ttbar_MESCDown, that means you need to run the enveloping and quadrature code. If it says it can't find ttbar_ERDOUp or ttbar_ERDODown, that means you need to run the symmetric systematic code.

================================================================================
Making datacards
================

Due to the nature of shape files, I typically manually create datacards since the changes are all done inside of the shape files themselves.  However, there is code that can be used to generate datacards.  It is located in 
cms-top/kmcgint/HiggsAnalysis/Shapetesting/Total_Run/Datacard Maker.ipynb
The code is fairly simple and has comments that describe how to use it.  

================================================================================
Shapefile debugging
===================

Many code blocks have been written that do various things to histograms for debugging purposes.  These range from setting minimum and maximum values to deleting bins entirely.  They are not well organized and can be found in the ShapeFileDebugging and shapeFileTesting notebooks in the total_run directory.   