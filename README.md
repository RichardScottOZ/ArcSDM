# Modified ArcSDM tools on arto-dev
Spatial Data Modeler 5 for ArcGis pro, Version ArcSdm 5.01.08 for ArcGis (Pro and Desktop)<Br>
Updated 23.7.2020<br>
  
## Changed tools and other files <br>

Standard toolbox of ArcSDM 5 works on ArcGis Desktop 10.3-10.7.1, however Experimental toolbox requires components that cannot be installed on ArcGis desktop and doesn't work. ArcGis pro is supported from version 2.5+ forward.<br>
These changes have been made in part in collaboration with the University of Unicamp, Brazil.

### Toolbox<br>

Grand Wofe start method is modified on Toolbox\ArcSDM.pyt at 9.6.2020<br>

### Python files <br>

#### ApplyModel.py 3.9.2019<br>
Unicamp fixes:<br>
1. Added import os<br>
2. Added and try: except: block, for handle errors with xrange().<br>
3. Replacec .maxint by .maxsize function.<br>

#### calculateresponse.py 23.7.2020<br>
1. “import missingdatavar_func” fixed to “import arcsdm.missingdatavar_func” (see Issue 74)<br>
2. The coordinate system of the input raster must be the same as that of the Training points Layer.<br>
3. When using FileSystem (dBase database) as the workspace, the input data of the Calculate Response tool must have the type extension .dbf in the Input Weights Table name. The tool adds that type extension if it is missing.<br>
4. The tool uses the arcpy function sequence implemented by Unicamp University unless you use the file system as the workspace in ArcGIS Pro.<br>

#### calculateweights.py 23.7.2020<br>
1. Obsolete attributes sys.exc_type and sys.exc_value replaced by sys.exc_info ()<br>
2. If the pixel type of the Evidence Raster (Input Raster) is NOT an integer, the raster name is displayed and execution is aborted on error.<br>
3. If Evidence Layer has not attribute table, execution is stopped. You can add it using ‘Build Raster Attribute Table’ tool.<br>
4. If the Data Type of the evidence layer is RasterBand, it is changed to Raster Dataset by changing the raster name.<br>
5. The coordinate system of the Training sites Layer must be the same as that of the Evidence Layer.<br>
6. When using FileSystem as the workspace in ArcGIS Pro (that is, writing the results to a dBase database), the field name of the database table must not be the same as the alias name of the field (case insignificant). ArcGIS Pro will crash if these names are the same. That's why I added an underscore to the end of the alias name.<br>
7. Added a few fixes made by Unicamp.<br>

#### categoricalmembership.py 22.5.2020<br>
The Reclassification parameter requires a database table that defines a classification. The Categorical & Reclass tool can create such a table, but its field names do not match that original command line (VALUE, VALUE, FMx100). ArcGIS Desktop 10.6.1 writes the FROM, TO, and OUT fields to the table. ArcGIS Pro 2.5 writes the FROM_, TO, and OUT fields. These field names have been fixed in the tool.<br>

#### common.py 23.7.2020<br>
Addition of a result raster displayed  to ArcGIS Pro to the Contents panel in addToDisplay feature fixed.<br>

#### Createrandompoints.py 20.7.2018<br>
Unicamp fix: changed the output shape files names, the original names “temp” is causing a BUG.<br>

#### Enrichpoints.py 24.8.2018<br>
Unicamp fixes:<br>
1. Change incorrect printing “Number of non deposits”, change to “Number of deposits”.<br>
2. Added new lines below “for regressor in regressor_names:”<br>

#### fuzzyroc.py 14.5.2020<br>
New tool to execute Calculate Weights, Calculate Response and ROCtool together. This tool gets two or more input rasters and one or more functions and parameters and uses same parameters to each input raster.<br>

#### fuzzyroc2.py 23.6.2020<br>
New tool to execute Calculate Weights, Calculate Response and ROCtool together. This tool gets two or more input rasters and one function and parameter combination to each input raster.<br>

<b><u>Help for both FuzzyROC tools:</u></b><br>
<b>Input raster names</b> – there can be any number of rasters - but at least two so far. Raster is selected either from the drop-down menu (if it found in the Contents list) or by a folder icon from a GDB database or disk (raster file).<br>
<b>Fuzzy Membership Parameters</b> – select the parameters to be used in the Fuzzy Membership tool.<br>
<b>Membership type</b> is selected from the drop-down menu. Numeric values are written in boxes.<br>
<b>Min-max values</b> are the minimum and maximum values between which Midpoint or Spread varies. The FuzzyROC tool starts with minimum values and performs calculation a count of Count times, increasing the minimum value (max - min) / count with each round.<br>
<b>Fuzzy Overlay Parameters</b> - select Overlay type from the drop-down menu. Only the Gaussian type has a parameter<br>
<b>ROC True Positives</b> Feature Class defines a feature class from which known positive cases are read.<br>
<b>ROC Destination Folder</b> - the folder where the ROC tool Output Files is written.<br>
The File Geodatabase database or file folder in the workspace is made up of a set of rasters named FM_n_m from the Fuzzy Membership tool and a set of rasters named FO_n from the Fuzzy Overlay tool.<br>
<b>FuzzyMembership.csv</b> (In the ROC Destination Folder) is an Excel spreadsheet that contains input and output data related to Fuzzy Membership tool performance.<br>
<b>FuzzyOverlay.csv</b> (In the ROC Destination Folder) is an Excel spreadsheet that contains output and output data related to Fuzzy Overlay --- tool execution.<br>
<b>FuzzyROC.csv</b> (In the ROC Destination Folder) is an Excel spreadsheet that contains the results calculated with the ROC tool.<br>

#### grand_wofe_lr.py 21.7.2020<br>
1. Logistic Regression does not work in ArcGIS Pro when using the File System as a workspace because gp.JoinField_management does not produce the correct values for Temp_Raster and therefore gp.Combine crashes. For some input rasters, execution does not crash, but the result is incorrect.<br>
2. Grand Wofe Name cannot be longer than 7 characters because it is used as part of the result raster name which cannot be longer than 13 characters.<br> 
3. The coordinate system of the input raster must be the same as that of the Training points Layer.<br>
4. Weights table name prefix was formed incorrectly<br>
5. Obsolete attributes sys.exc_type and sys.exc_value replaced by sys.exc_info ()<br>

#### logisticregression.py 21.7.2020<br>
Logistic Regression does not work in ArcGIS Pro when using the File System as a workspace because gp.JoinField_management does not produce the correct values for Temp_Raster and therefore gp.Combine crashes. For some input rasters, execution does not crash, but the result is incorrect. <br>

#### missingdatavar_func.py 15.6.2020<br>
Fixed four typos:<br>
1. “from floatingrasterarray import…” fixed to “from arcsdm.floatingrasterarray import…”<br>
2. “except Exception,Msg:” is invalid syntax, “,Msg” removed<br>
3. “print pymsg” fixed to “print (pymsg)”<br>
4. “print msgs” fixed to “print (msgs)”<br>

#### Modeltrain.py 29.11.2018<br>
Unicamp fixes:<br>
1. Replaced .maxint function by .maxsize function. .maxint is deprecated.<br>
2. Added train_response_name variable to _save_model() function<br>
3. Print train_response_name variable<br>
4. Write Response name to Train text file.<br>

#### nninputfiles.py 20.7.2018<br>
Unicamp fix: Change line 212, incorrect parameters number (“7”), changed to “5” <br>

#### Nnoutputfiles.py 6.12.2018<br>
Unicamp fixes:<br>
1. Modified to handle None parameters (rbndx, rbngx and fc)<br>
2. Replaced getParametersAsText by .valuesAsText (output_name)<br>
3. Replaced <> by != on 3 if rows<br>
4. Replaced addjoin_management() by JoinField_management()<br>
5. Removed Msg from exception.<br>
6. Added () to print function for Python 3 compatibility.<br>

#### rescale_raster.py 29.11.2018<br>
Unicamp fix: Removed the file extension from output raster name.<br>

#### roctool.py 12.5.2020<br>
Added closing of pylab windows because without closing only 20 patterns could be formed.<br>

#### tocfuzzification.py 29.4.2020<br>
Tested, not modified.<br>

#### sdmvalues.py 28.5.2020<br>
1. The default value for Environment.Cell Size is Maximum of Inputs, which can be used as a Cell Size if the mask is FeatureLayer or FeatureClass. If the mask is a raster, the text value cannot be used in the calculation, but the Cell Size must be an integer<br>
2. RasterLayer, RasterBand, FeatureLayer and FeatureClass can be used as the mask. These types are grouped in the code into if-elif-else blocks. In the Else block, all data types other than those defined above are discarded.<br>
3. If the mask is not defined at all, you will be prompted to check the Environment settings.<br>
4. If the “Cells in area” value is 0, execution is aborted.<br>

#### workarounds_93.py 23.7.2020<br>
Obsolete attributes sys.exc_type and sys.exc_value replaced by sys.exc_info ()<br>

### Other files<br>

ArcSDM.pyt - ArcSDM Toolbox menu (Added new Fuzzy ROC tools)<br>
ArcSDM.CalculateResponse.pyt.xml	- HELP for Calculate Response<br>
ArcSDM.CalculateWeightsTool.pyt.xml	 -HELP for Calculate Weights<br>
ArcSDM.FuzzyROC2.pyt.xml - HELP for Fuzzy ROC 2<br>
ArcSDM.LogisticRegressionTool.pyt.xml - Help for Logistic Regression<br>
ArcSDM.GrandWofe.pyt.xml - Help for Grand Wofe<br>
