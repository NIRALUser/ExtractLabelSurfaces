
# ExtractLabelSurface

This tool creates the surfaces for each brain regions (colored in a vtk file) and updates a text file of seeds list (for tractography)

## USAGE: 

----
	ExtractLabelSurfaces  [--returnparameterfile <std::string>]
                         [--processinformationaddress <std::string>]
                         [--xml] [--echo] [--extractPointData]
                         [--vtkLabelFile <std::string>] [-a <std::string>]
                         [--labelNameInfo <std::string>]
                         [--translateToLabelNumber] [--useTranslationTable]
                         [--labelTranslationTable <std::string>]
                         [--labelNumberInfo <std::string>]
                         [--createSurfaceLabelFiles] [--vtkFile
                         <std::string>] [--overlapping] [-p <std::string>]
                         [-i <std::string>] [--] [--version] [-h]


	Where: 

	   --returnparameterfile <std::string>
	     Filename in which to write simple return parameters (int, float,
	     int-vector, etc.) as opposed to bulk return parameters (image,
	     geometry, transform, measurement, table).

	   --processinformationaddress <std::string>
	     Address of a structure to store process information (progress, abort,
	     etc.). (default: 0)

	   --xml
	     Produce xml description of command line arguments (default: 0)

	   --echo
	     Echo the command line arguments (default: 0)

	   --extractPointData
	     Extract Point Data from the vtk file containing labels : required
	     flags --vtklabelFile --arrayName/-a and --labelNameInfo (default: 0)

	   --vtkLabelFile <std::string>
	     Surface with labels information ( myfile_withLabel.vtk )

	   -a <std::string>,  --arrayName <std::string>
	     Array name containing label information

	   --labelNameInfo <std::string>
	     List containing label information by name.

	   --translateToLabelNumber
	     Translate labelNameInformation file to labelNumberInformation file :
	     required flags --labelNameInfo  and --labelNumberInfo. If you add a
	     Translation table then you need to specified flags --useTable and
	     --labelTranslationTable (default: 0)

	   --useTranslationTable
	     Find label filename with a translation table (default: 0)

	   --labelTranslationTable <std::string>
	     Table containing label number for each label name

	   --labelNumberInfo <std::string>
	     List containing label information by number in accordance with a
	     Translation table (--useTranslationTable) or not.

	   --createSurfaceLabelFiles
	     Create surfaces corresponding to each label : required flags
	     --labelNumberInfo and --vtkFile. You can specified a prefix for
	     identify surfaces files (for exemple : lh or rh). (default: 0)

	   --vtkFile <std::string>
	     Surface without label information from which we extract the different
	     labeled surfaces ( myfile.vtk )

	   --overlapping
	     Reconstruct label surfaces with overlapping (default: 0)

	   -p <std::string>,  --prefix <std::string>
	     Prefix added in names of each output files

	   -i <std::string>,  --ignoreLabel <std::string>
	     Ignore the label Name specify - this label won't be created (ex : -i
	     '0 0 0'). MUST BE USE WITH OPTION --useTranslationTable AND
	     --labelTranslationTable

	   --,  --ignore_rest
	     Ignores the rest of the labeled arguments following this flag.

	   --version
	     Displays version information and exits.

	   -h,  --help
	     Displays usage information and exits.


	   Description: ExtractLabelSurfaces is a tool which extracted labels
	   surfaces from a surface containing labels

	   Author(s): Danaele Puechmaille, Francois Budin, Juan Carlos Prieto, Martin
	   Styner

	   Acknowledgements: This work is part of the National Alliance for Medical
	   Image Computing (NAMIC), funded by the National Institutes of Health
	   through the NIH Roadmap for Medical Research, Grants U01 MH070890 - U54
	   HD079124 - R01 MH091351.
----

## Example run

### Input files

#### 1. parcellationTable.json 
(example 5 ROIs, atlas AAL90 )
[ <br/>
  { <br/>
    "VisuOrder": 78, <br/>
    "MatrixRow": 1, <br/>
    "name": "Precentral_L", <br/>
    "VisuHierarchy": "seed.left.frontal.", <br/>
    "coord": [<br/>
      -38.649999999999999, <br/>
      -5.6799999999999997, <br/>
      50.939999999999998<br/>
    ], <br/>
    "labelValue": "131 44 78", <br/>
    "AAL_ID": 1<br/>
  }, <br/>
  {<br/>
    "VisuOrder": 1, <br/>
    "MatrixRow": 2, <br/>
    "name": "Precentral_R", <br/>
    "VisuHierarchy": "seed.right.frontal.", <br/>
    "coord": [<br/>
      41.369999999999997, <br/>
      -8.2100000000000009, <br/>
      52.090000000000003<br/>
    ], <br/>
    "labelValue": "241 43 17", <br/>
    "AAL_ID": 2<br/>
  }, <br/>
  {<br/>
    "VisuOrder": 77, <br/>
    "MatrixRow": 3, <br/>
    "name": "Frontal_Sup_L", <br/>
    "VisuHierarchy": "seed.left.frontal.", <br/>
    "coord": [<br/>
      -18.449999999999999, <br/>
      34.810000000000002, <br/>
      42.200000000000003<br/>
    ], <br/>
    "labelValue": "126 31 21", <br/>
    "AAL_ID": 3<br/>
  }, <br/>
  {<br/>
    "VisuOrder": 2, <br/>
    "MatrixRow": 4, <br/>
    "name": "Frontal_Sup_R", <br/>
    "VisuHierarchy": "seed.right.frontal.", <br/>
    "coord": [<br/>
      21.899999999999999, <br/>
      31.120000000000001, <br/>
      43.82<br/>
    ], <br/>
    "labelValue": "70 93 250", <br/>
    "AAL_ID": 4<br/>
  }, <br/>
  {<br/>
    "VisuOrder": 76, <br/>
    "MatrixRow": 5, <br/>
    "name": "Frontal_Sup_Orb_L", <br/>
    "VisuHierarchy": "seed.left.frontal.", <br/>
    "coord": [<br/>
      -16.559999999999999, <br/>
      47.32, <br/>
      -13.31<br/>
    ], <br/>
    "labelValue": "19 164 195", <br/>
    "AAL_ID": 5<br/>
  }<br/>
 ]<br/>

####2. VTK surface containning a colorTable and labels id known.

####3. If first surfaces doesn't contain label, add other vtk surface with same mesh and a colorTable


### Execution
----
	ExtractLabelSurfaces --extractPointData --translateToLabelNumber --labelNameInfo labelListName.txt --labelNumberInfo  labelListNumber.txt --useTranslationTable --labelTranslationTable parcelaciontTable.json -a colorTableLabel --vtkLabelFile $var/${EXTRA_SURFACE_COLOR} --createSurfaceLabelFiles --vtkFile $var/${SURFACE} ${overlapFlag} ${ignoreFlag} "${labelID}" 
----

### Sample output

####1. labelListName.txt
#####Text file containing label name information for each point - output of ExtractPointData tool 
204 150 68 <br/>
204 150 68<br/>
204 150 68<br/>
204 150 68<br/>
147 2 98<br/>
147 2 98<br/>
147 2 98<br/>
147 2 98<br/>
204 150 68<br/>
204 150 68<br/>
147 2 98<br/>
147 2 98<br/>
147 2 98<br/>
204 150 68<br/>
204 150 68<br/>
204 150 68<br/>
204 150 68<br/>
147 2 98<br/>
147 2 98<br/>
204 150 68<br/>
204 150 68<br/>
204 150 68<br/>
204 150 68<br/>
204 150 68<br/>
204 150 68<br/>
204 150 68<br/>
204 150 68<br/>
204 150 68<br/>
204 150 68<br/>
147 2 98<br/>
177 232 171<br/>
204 150 68<br/>
204 150 68<br/>
204 150 68<br/>
204 150 68<br/>
204 150 68<br/>
204 150 68<br/>
204 150 68<br/>
204 150 68<br/>
204 150 68<br/>
177 232 171<br/>

####2. labelListNumber.txt
#####Text file containing label number information for each point - output of TranslateToLabelNumber tool 
56<br/>
56<br/>
56<br/>
56<br/>
88<br/>
88<br/>
88<br/>
88<br/>
56<br/>
56<br/>
88<br/>
88<br/>
88<br/>
56<br/>
56<br/>
56<br/>
56<br/>
88<br/>
88<br/>
56<br/>
56<br/>
56<br/>
56<br/>
56<br/>
56<br/>
56<br/>
56<br/>
56<br/>
56<br/>
88<br/>
90<br/>
56<br/>
56<br/>
56<br/>
56<br/>
56<br/>
56<br/>
56<br/>
56<br/>
56<br/>
90<br/>
90<br/>
90<br/>
90<br/>
56<br/>
56<br/>
56<br/>
90<br/>

####3.Surfaces for each label

Example of first label in the parcellation table : 
1.asc

#####!ascii - generated by CreateLabelFiles project 
5403 10303<br/>
-46.4779 2.81183 15.3132 0<br/>
-46.4996 3.3489 15.6246 0<br/>
-45.9079 2.95193 15.6016 0<br/>
-61.697 -4.39855 14.6822 0<br/>
-50.2368 5.08928 16.5498 0<br/>
-49.6108 4.87946 16.3573 0<br/>
-48.8322 4.80679 16.578 0<br/>
-48.1322 3.90311 15.687 0<br/>
-48.1015 4.43293 16.2416 0<br/>
-48.1208 4.70348 16.8641 0<br/>
-46.9305 3.90651 16.2011 0<br/>
-47.456 4.42403 16.8322 0<br/>
-46.841 4.177 16.9945 0<br/>
-44.6103 0.396933 15.834 0<br/>
-44.7909 1.55506 15.8372 0<br/>
-45.1646 2.49265 15.9203 0<br/>
-45.7475 3.25321 16.1263 0<br/>
-45.843 3.59799 16.8431 0<br/>
-46.3667 3.93505 17.0066 0<br/>
-43.36 -0.635979 16.5584 0<br/>
-43.9287 0.753653 16.255 0<br/>
-44.1906 1.78189 16.3608 0<br/>
-44.76 2.65467 16.4939 0<br/>
-44.0239 2.17436 16.8038 0<br/>
-45.1455 3.15231 16.8226 0<br/>
-43.2376 -0.043141 16.6145 0<br/>
-43.3201 0.891297 16.6834 0<br/>
-43.524 1.60629 16.8149 0<br/>
-61.6382 -5.94314 14.9863 0<br/>
-61.7547 -5.10005 15.1768 0<br/>
-60.5279 -7.52865 15.1722 0<br/>
-59.7877 -8.02226 15.5954 0<br/>
-61.0178 -6.7231 15.523 0<br/>
-61.419 -5.88521 15.7147 0<br/>
-61.6152 -5.18673 15.8947 0<br/>
-61.2887 -3.83287 15.1867 0<br/>
-61.633 -4.34794 15.6757 0<br/>
-61.2294 -3.39346 16.0166 0<br/>
-58.8814 -8.62694 15.6406 0<br/>


####4.parcellationTable.json same file updated by the tool