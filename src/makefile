############################################################################
# MOLASSES (MOdular LAva Simulation Software for the Earth Sciences) 
# The MOLASSES model relies on a cellular automata algorithm to 
# estimate the area inundated by lava flows.
#
#    Copyright (C) 2015-2021  
#    Laura Connor (lconnor@usf.edu)
#    Jacob Richardson 
#    Charles Connor
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU General Public License for more details.
#
#    You should have received a copy of the GNU General Public License
#    along with this program.  If not, see <http://www.gnu.org/licenses/>.
###########################################################################

# CFLAGS = -Wall -pedantic -g Wno-long-long
CFLAGS = -Wall -O2 -pthread
INCLUDES = -I$(GDAL_INCLUDE_PATH) -I../include -I./include
# If you compile the gc libraries rather than installing a precompiled version
# into the system, you may need to modify the LIBS variable to indicate
# where you put the -lgc library and include files. Notice the include and lib
# directories in the top level folder.
# If you set a specific path for your GDAL libraries, this will look for it!
ifndef GDAL_LIB_PATH
	LIBS = -lgdal -lgc -L../lib -lpthread -lran -lm
else
	LIBS = -L$(GDAL_LIB_PATH) -lpthread -lgc -lgdal -L../lib -lran -lm
endif

SRCS = driver_LJC2.c \
initialize_LJC2.c \
demloader_LJC.c \
arrayinit_LJC.c \
initflow_2LJC2.c \
pulse_2LJC2.c \
distribute_proportional2slope4_LJC2.c \
neighbor_8.c \
output_2LJC2.c \
set_flow _params2.c \
choose_vent_LJC2.c \
check_vent2.c \

# activate_$(activate).c

OBJ = $(SRCS:.c=.o)

MAIN = molasses.ljc

all:	$(MAIN)
		@echo "*** $(MAIN) has been compiled. ***"

$(MAIN): $(OBJ)
	$(CC) $(CFLAGS) $(INCLUDES) -o $@ $+ $(LIBS)

%.o : %.c
	$(CC) $(CFLAGS) $(INCLUDES) -c $<  -o $@

$(OBJ): include/structs_LJC2.h include/prototypes_LJC2.h

.PHONY:	clean install

clean:
	$(RM) *.o *~ $(MAIN)

install:
	install -d ../bin
	install -m 0755 $(MAIN) ../bin

uninstall:
	-rm $(BINDIR)/$(MAIN) &>/dev/null

