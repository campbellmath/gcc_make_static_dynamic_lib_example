###############################################################################
# compiler setting
###############################################################################
CC       = gcc
CFLAGS   = -g -Wall
AR       = ar
LIBS     = -lm
INCPATH  = -I. -I./inc
DIR      = $(shell pwd)
BASENAME = $(shell basename $(DIR))

###############################################################################
# source files setting
###############################################################################
C_SOURCES   	 = $(shell find . -name "*.c")
C_STATIC_OBJS    = $(patsubst %.c,%_static.o,$(wildcard $(C_SOURCES)))
C_DYNAMIC_OBJS   = $(patsubst %.c,%_dynamic.o,$(wildcard $(C_SOURCES)))
STATIC_OBJS      = $(C_STATIC_OBJS)
DYNAMIC_OBJS     = $(C_DYNAMIC_OBJS)
LIB_A            = $(BASENAME).a
LIB_SO           = $(BASENAME).so

###############################################################################
.PHONY : clean
###############################################################################
all: $(LIB_A) $(LIB_SO)
	@echo ' '

%_static.o:%.c
	$(CC) -c $(CFLAGS) $(INCPATH) $< -o $@

%_dynamic.o:%.c
	$(CC) -c $(CFLAGS) $(INCPATH) $< -o $@ -fPIC

$(LIB_A): $(STATIC_OBJS)
	$(AR) rcs $@ $(STATIC_OBJS)
	@echo 'Finished building: $@'

$(LIB_SO): $(DYNAMIC_OBJS)
	$(CC) $(DYNAMIC_OBJS) -shared -o $@
	@echo 'Finished building: $@'
###############################################################################
clean:
	@rm -vfr $(STATIC_OBJS) $(LIB_A) $(DYNAMIC_OBJS) $(LIB_SO)
###############################################################################
