# Config file
include ../../../Makefile.conf

NAME=c

OBJECT_NAME=lib$(NAME).a

OUTPUT_DIR=../../out/system/lib/

CC = ../../../$(COMPILER_PATH)/$(COMPILER_ARCH)gcc
AR = ../../../$(COMPILER_PATH)/$(COMPILER_ARCH)ar
NASM = /usr/bin/nasm

C_SOURCES = $(shell find ./ -type f -name '*.c')
S_SOURCES = $(shell find ./ -type f -name '*.s')
ASM_SOURCES = $(shell find ./ -type f -name '*.asm')
OBJ = ${C_SOURCES:.c=.o} ${ASM_SOURCES:.asm=.o} ${S_SOURCES:.s=.o}

INCLUDE_DIR = ../include

ifeq ($(OSARCH), amd64)
ASM_ARCH := elf64
else ifeq ($(OSARCH), i686)
ASM_ARCH := elf32
endif

CFLAGS := -fPIC -I$(INCLUDE_DIR)

build: $(OBJECT_NAME)

$(OBJECT_NAME): $(OBJ)
	$(AR) rcs  $(OUTPUT_DIR)$@ $(OBJ)

%.o: %.c $(HEADERS) $(HEADERS2)
	$(CC) $(CFLAGS) -std=c17 -c $< -o $@

%.o: %.cpp $(HEADERS) $(HEADERS2)
	$(CC) $(CFLAGS) -std=c++20 -c $< -o $@

%.o: %.asm
	$(NASM) $< -f $(ASM_ARCH) -o $@

clean:
	rm -f $(OBJ)