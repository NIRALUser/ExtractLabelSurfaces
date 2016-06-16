
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

1. labelListName

2. labelListNumber.txt


### Execution
----
	ExtractLabelSurfaces --extractPointData --translateToLabelNumber --labelNameInfo labelListName.txt --labelNumberInfo  labelListNumber.txt --useTranslationTable --labelTranslationTable parcelaciontTable.json -a colorTableLabel --vtkLabelFile $var/${EXTRA_SURFACE_COLOR} --createSurfaceLabelFiles --vtkFile $var/${SURFACE} ${overlapFlag} ${ignoreFlag} "${labelID}" 
----

### Sample output


