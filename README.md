# Thorlabs OSA300/Redstone and OSA200 LabVIEW Drivers 1.0.1
## Support
* LabVIEW 2010 and newer, 64 bit.
* See the system requirement field for the [ThorSpectra application](https://www.thorlabs.com/software_pages/viewsoftwarepage.cfm?code=OSA) (supported OS).
* Requires a prior ThorSpectra application installation, (FTSLib.dll and FTSLV.dll), version 3.20 or newer.  
* The executable for the example vi has not been fully tested.

## Legacy OSA200 only driver
* We do NOT recommend a Labview driver upgrade from the OSA20X Labview Drivers (Libraries tab), if having already employed any program using these drivers. 

## Installation package or ZIP-file
The drivers are available as a vi package or a zipped project. The vi package, (vip-file), created with VI Package Manager, will install the OSA FTS drivers in the Labview environment for driver access through an Instrument I/O and Instrument Driver diagram palette. The vi package installation will also enable access to the driver project file, help files and example vis from the Labview Help menu.
* thorlabs_lib_ofts-1.0.1.X.vip - vi package manager installation, [VIPM guide](./_doc/VIPM%20Driver%20Installation.pdf)
* thorlabs_lib_ofts-1.0.1.X.zip - zipped project

_Please make sure the [ThorSpectra application](https://www.thorlabs.com/software_pages/viewsoftwarepage.cfm?code=OSA) has been installed!_

_Make sure all older OSA200 specific LabVIEW driver files are removed - root folder names contain the 'OSA20X' characters._

To have access to the OSA diagram palette with the zip-file (when not installing with a vip-file) proceed as follows:
* move the driver hierarchi to the labview instr.lib folder, (example LabVIEW 2010 - C:\Program Files\National Instruments\LabVIEW 2010\instr.lib\Thorlabs). Create the   Thorlabs sub-folder if not already present.
* rename the driver root folder to _Thorlabs OSA FTS_, (path: ..\instr.lib\Thorlabs\Thorlabs OSA FTS\Thorlabs FTS.lvproj).
* move all files under Thorlabs OSA FTS\\_examples to ..\National Instruments\Labview 20??\Examples\Thorlabs\Thorlabs OSA FTS
* do a mass compile of the driver hierarchi if using a newer version than LabVIEW 2010.
* do a mass compile of example vis under ..\National Instruments\Labview 20??\examples\Thorlabs\Thorlabs OSA FTS.

## High Level Driver Files
Use only vis directly accessible through the Thorlabs OSA FTS diagram palette, the Tree.vi or if picking vis directly from within Thorlabs FTS.lvproj:
* OSA.lvclass\public

## FTSLib.dll
The driver vis are based on functions in FTSLib.dll version 3.20 or newer, located in the ThorSpectra installation folder, (Program Files\..). The ThorSpectra application installation updates the Path system environment variable with the FTSLib.dll path. 
For detailed information of FTSLib.dll functions; see Manual FTSLib.chm and h-files, available from the Labview Help menu after vip package installation, and located in the ThorSpectra\lib and \include folders.

# Driver vis
See the TREE vis for a categorized overview of the driver vis and the example vis for guidelines of how to use them. For most applications the FTSLib.dll functions supported by the Labview drivers will be appropriate; however some functions have not yet been implemented. When adding new vis that call functions in FTSLib.dll we recommend the Labview import shared library tool.  
# Example vis
A simple example shows the basic spectrum retrival and buffering procedure, and a more complex how to retrieve both interferogram and spectrum with some post dataprocessing. There are also examples for setting data-acquisition options, instrument properties and interferogram/spectrum analysis. A traces example shows how to make use of data buffers allocated by FTSLib.dll.
# Support Files
FTSLV.dll was created for Labview calls to FTSLib functions requiring function pointer parameters. Addresses to functions within FTSLV.dll are fetched via kernel32.dll and serve as input parameter values to data acquisition functions in FTSLib.dll. 

FTSLib.lvlib contains some Labview autogenerated FTSLib.dll wrappers used in some of the driver vis, (most of the vis calling FTSLib.dll functions don’t have wrappers).

_goop4.llb contains vis supporting the main OSA class.
# Building Executables
See the Thorlabs FTS project build specification for the OSA_Example.vi, (regarding support files). 
The path to FTSLib.dll and FTSLV.dll must be set in the PATH system environment variable, (updated during OSA GUI application installation). 
# OSA Class
The fact that the driver vis are part of LabVIEW classes does not necessarily require any attention. When adding new driver vis we recommend starting out with existing driver vis as templates to comply with and conveniently access GOOP class/objects properties. 
# Known Issues
Large Data Sets
When acquiring the largest interferogram datasets in conjunction with zero fill and other data analysis functions; see chapter 7, ‘Recommended Hardware and Software Requirements’ in the Thorlabs OSA manuals for the OSA200 or 300/Redstone series. Data-acquisition to traces, instead of the OSA dedicated Labview buffer, will in most cases improve performance/execution time – see the traces example and trace vis in the tree.vi.
 
# Changes Log
### 1.0.1.16
GetLastStatus_ext() in FTSLV.dll has changed - parameter 'typeOfStatus' added. Bugg in dataAcq_get_spectrum.vi - x-data not properly saved.

### 1.0.0.14
New installation path for OSA FTSLib.dll and FTSLV.dll.

### 1.0.0.13
OSA_example_analyse.vi updated with wavelength meter and extended documentation.

### 1.0.0.12
First release of driver supporting FTSLib.dll version 3.20 and newer.
