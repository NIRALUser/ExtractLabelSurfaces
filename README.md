
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
[
  {
    "VisuOrder": 78, 
    "MatrixRow": 1, 
    "name": "Precentral_L", 
    "VisuHierarchy": "seed.left.frontal.", 
    "coord": [
      -38.649999999999999, 
      -5.6799999999999997, 
      50.939999999999998
    ], 
    "labelValue": "131 44 78", 
    "AAL_ID": 1
  }, 
  {
    "VisuOrder": 1, 
    "MatrixRow": 2, 
    "name": "Precentral_R", 
    "VisuHierarchy": "seed.right.frontal.", 
    "coord": [
      41.369999999999997, 
      -8.2100000000000009, 
      52.090000000000003
    ], 
    "labelValue": "241 43 17", 
    "AAL_ID": 2
  }, 
  {
    "VisuOrder": 77, 
    "MatrixRow": 3, 
    "name": "Frontal_Sup_L", 
    "VisuHierarchy": "seed.left.frontal.", 
    "coord": [
      -18.449999999999999, 
      34.810000000000002, 
      42.200000000000003
    ], 
    "labelValue": "126 31 21", 
    "AAL_ID": 3
  }, 
  {
    "VisuOrder": 2, 
    "MatrixRow": 4, 
    "name": "Frontal_Sup_R", 
    "VisuHierarchy": "seed.right.frontal.", 
    "coord": [
      21.899999999999999, 
      31.120000000000001, 
      43.82
    ], 
    "labelValue": "70 93 250", 
    "AAL_ID": 4
  }, 
  {
    "VisuOrder": 76, 
    "MatrixRow": 5, 
    "name": "Frontal_Sup_Orb_L", 
    "VisuHierarchy": "seed.left.frontal.", 
    "coord": [
      -16.559999999999999, 
      47.32, 
      -13.31
    ], 
    "labelValue": "19 164 195", 
    "AAL_ID": 5
  }]

####2. VTK surface containning a colorTable and labels id known.

####3. If first surfaces doesn't contain label, add other vtk surface with same mesh and a colorTable


### Execution
----
	ExtractLabelSurfaces --extractPointData --translateToLabelNumber --labelNameInfo labelListName.txt --labelNumberInfo  labelListNumber.txt --useTranslationTable --labelTranslationTable parcelaciontTable.json -a colorTableLabel --vtkLabelFile $var/${EXTRA_SURFACE_COLOR} --createSurfaceLabelFiles --vtkFile $var/${SURFACE} ${overlapFlag} ${ignoreFlag} "${labelID}" 
----

### Sample output

####1. labelListName.txt
#####Text file containing label name information for each point - output of ExtractPointData tool 
204 150 68
204 150 68
204 150 68
204 150 68
147 2 98
147 2 98
147 2 98
147 2 98
204 150 68
204 150 68
147 2 98
147 2 98
147 2 98
204 150 68
204 150 68
204 150 68
204 150 68
147 2 98
147 2 98
204 150 68
204 150 68
204 150 68
204 150 68
204 150 68
204 150 68
204 150 68
204 150 68
204 150 68
204 150 68
147 2 98
177 232 171
204 150 68
204 150 68
204 150 68
204 150 68
204 150 68
204 150 68
204 150 68
204 150 68
204 150 68
177 232 171

####2. labelListNumber.txt
#####Text file containing label number information for each point - output of TranslateToLabelNumber tool 
56
56
56
56
88
88
88
88
56
56
88
88
88
56
56
56
56
88
88
56
56
56
56
56
56
56
56
56
56
88
90
56
56
56
56
56
56
56
56
56
90
90
90
90
56
56
56
90

####3.Surfaces for each label

Example of first label in the parcellation table : 
1.asc

#####!ascii - generated by CreateLabelFiles project 
5403 10303
-46.4779 2.81183 15.3132 0
-46.4996 3.3489 15.6246 0
-45.9079 2.95193 15.6016 0
-61.697 -4.39855 14.6822 0
-50.2368 5.08928 16.5498 0
-49.6108 4.87946 16.3573 0
-48.8322 4.80679 16.578 0
-48.1322 3.90311 15.687 0
-48.1015 4.43293 16.2416 0
-48.1208 4.70348 16.8641 0
-46.9305 3.90651 16.2011 0
-47.456 4.42403 16.8322 0
-46.841 4.177 16.9945 0
-44.6103 0.396933 15.834 0
-44.7909 1.55506 15.8372 0
-45.1646 2.49265 15.9203 0
-45.7475 3.25321 16.1263 0
-45.843 3.59799 16.8431 0
-46.3667 3.93505 17.0066 0
-43.36 -0.635979 16.5584 0
-43.9287 0.753653 16.255 0
-44.1906 1.78189 16.3608 0
-44.76 2.65467 16.4939 0
-44.0239 2.17436 16.8038 0
-45.1455 3.15231 16.8226 0
-43.2376 -0.043141 16.6145 0
-43.3201 0.891297 16.6834 0
-43.524 1.60629 16.8149 0
-61.6382 -5.94314 14.9863 0
-61.7547 -5.10005 15.1768 0
-60.5279 -7.52865 15.1722 0
-59.7877 -8.02226 15.5954 0
-61.0178 -6.7231 15.523 0
-61.419 -5.88521 15.7147 0
-61.6152 -5.18673 15.8947 0
-61.2887 -3.83287 15.1867 0
-61.633 -4.34794 15.6757 0
-61.2294 -3.39346 16.0166 0
-58.8814 -8.62694 15.6406 0


####4.parcellationTable.json same file updated by the tool