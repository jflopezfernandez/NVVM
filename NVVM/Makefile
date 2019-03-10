
vpath %.c src
vpath %.h include

#
# Defs
#

CFLAGS :=
CPPFLAGS := -I include

DOXYGEN := doxygen
DOXYGEN_CONFIG := doxygen.config

PROGRAM := nvvm

#
# Start
#

all: documentation $(PROGRAM)

#
# Compilation
#

$(PROGRAM): NVVM.o
	$(CC) $(CPPFLAGS) $(CFLAGS) -o $@ $^

NVVM.o: NVVM.c
	$(CC) $(CPPFLAGS) $(CFLAGS) -c -o $@ $^

#
# Doc
#

documentation: $(DOXYGEN_CONFIG)
	$(DOXYGEN) $(DOXYGEN_CONFIG)

$(DOXYGEN_CONFIG):
	$(DOXYGEN) -g $(DOXYGEN_CONFIG)

.PHONY: clean
clean:
	rm -rf *.o $(PROGRAM)
	rm -rf ./doxygen.config
