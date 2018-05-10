## Application Binary Interface (ABI)
Interface between software component at the binary level either at static linkage (not sure if this is where it happens), runtime (shared library and executable).
 - Data representation
 - Data alignment
 - Stack alignment
 - Register usage
 - Function calling convention
 - Name mangling
 - Exception handling
 - Initialization and termination functions (not enough information in how it affect ABI)
 - Virtual tables and runtime type identification
 - Communal data
 - Memory models
 - Relocation of executable code
 - Object file formats
 - Debug information (shouldn't affect ABI but only debuggability)
 - Data endian-ness (shouldn't affect the binary interface but API of the processed data)

 http://infocenter.arm.com/help/index.jsp?topic=/com.arm.doc.subset.swdev.abi/index.html
http://www.nxp.com/docs/en/application-note/PPCEABI.pdf
https://en.wikipedia.org/wiki/X86_calling_conventions
https://wiki.debian.org/ArmEabiPort

# Useful Resources
[1] https://community.kde.org/Policies/Binary_Compatibility_Issues_With_C%2B%2B
[2] http://www.agner.org/optimize/calling_conventions.pdf
[3] 
