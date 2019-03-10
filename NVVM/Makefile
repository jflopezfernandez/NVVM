
vpath %.c src
vpath %.h include

#
# Defs
#

CC := icc
CFLAGS := -Wall -W3 -Wremarks -Wcheck -masm=intel -mavx -m64 -fast -falias -std=c11 -fbuiltin -fdefer-pop -foptimize-sibling-calls -fprotect-parens -O3 -Ofast -mtune=skylake -march=skylake -fno-asynchronous-unwind-tables -fno-exceptions -funroll-all-loops -ansi-alias -ipp -mkl -use-intel-optimized-headers -unroll-aggressive
CPPFLAGS := -I include -I /opt/intel/compilers_and_libraries_2019.2.187/linux/mkl/include -I /opt/intel/compilers_and_libraries_2019.2.187/linux/tbb/include/tbb -I /opt/intel/compilers_and_libraries_2019.2.187/linux/ipp/include

LD := xild
LIBFLAGS := -mkl -static-intel
LFLAGS := -Wl,--strip-debug $(LIBFLAGS)

DOXYGEN := doxygen
DOXYGEN_CONFIG := doxygen.config

PROGRAM := nvvm

#
# Start
#

all: clean documentation $(PROGRAM)

#
# Compilation
#

$(PROGRAM): NVVM.o
	$(CC) $(CPPFLAGS) $(CFLAGS) -o $@ $^ $(LFLAGS)

NVVM.o: NVVM.c
	$(CC) $(CPPFLAGS) $(CFLAGS) -c -o $@ $^

#
# Doc
#

documentation: $(DOXYGEN_CONFIG)
	$(DOXYGEN) $(DOXYGEN_CONFIG)

$(DOXYGEN_CONFIG):
	$(DOXYGEN) -g - | \
	sed -n -E -e 's/^(OUTPUT_DIRECTORY\s*=\s*)/\1 doc/;/.*/p' > $(DOXYGEN_CONFIG)

.PHONY: clean
clean:
	rm -rf *.o $(PROGRAM)
	rm -rf ./doxygen.config
