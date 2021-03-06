#
#  Makefile
#  ARToolKit5
#
#  This file is part of ARToolKit.
#
#  ARToolKit is free software: you can redistribute it and/or modify
#  it under the terms of the GNU Lesser General Public License as published by
#  the Free Software Foundation, either version 3 of the License, or
#  (at your option) any later version.
#
#  ARToolKit is distributed in the hope that it will be useful,
#  but WITHOUT ANY WARRANTY; without even the implied warranty of
#  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#  GNU Lesser General Public License for more details.
#
#  You should have received a copy of the GNU Lesser General Public License
#  along with ARToolKit.  If not, see <http://www.gnu.org/licenses/>.
#
#  As a special exception, the copyright holders of this library give you
#  permission to link this library with independent modules to produce an
#  executable, regardless of the license terms of these independent modules, and to
#  copy and distribute the resulting executable under terms of your choice,
#  provided that you also meet, for each linked independent module, the terms and
#  conditions of the license of that module. An independent module is a module
#  which is neither derived from nor based on this library. If you modify this
#  library, you may extend this exception to your version of the library, but you
#  are not obligated to do so. If you do not wish to do so, delete this exception
#  statement from your version.
#
#  Copyright 2015 Daqri, LLC.
#  Copyright 2002-2015 ARToolworks, Inc.
#
#  Author(s): Hirokazu Kato, Philip Lamb
#

UNAME = $(shell uname)

AR_HOME = ../../..
AR_CPPFLAGS = -I$(AR_HOME)/include/linux-x86_64 -I$(AR_HOME)/include

CC=gcc
CXX=g++ -std=c++11
CPPFLAGS = $(AR_CPPFLAGS)
CFLAGS = -O3 -fPIC -march=core2 -DHAVE_NFT=1 -I/usr/include/x86_64-linux-gnu
CXXFLAGS = -O3 -fPIC -march=core2 -DHAVE_NFT=1 -I/usr/include/x86_64-linux-gnu
AR=ar
ARFLAGS=rs
RANLIB = true

TARGET1 = $(AR_HOME)/lib/libARgsub.a
TARGET3 = $(AR_HOME)/lib/libARgsub_lite.a

HEADERS1 = \
	$(AR_HOME)/include/AR/gsub.h     \
    $(AR_HOME)/include/AR/config.h   \
    $(AR_HOME)/include/AR/arConfig.h \
    $(AR_HOME)/include/AR/ar.h       \
    $(AR_HOME)/include/AR/matrix.h   \
    $(AR_HOME)/include/AR/param.h    \
	argPrivate.h

HEADERS3= \
	$(AR_HOME)/include/AR/gsub_lite.h \
    $(AR_HOME)/include/AR/gsub_mtx.h \
    $(AR_HOME)/include/AR/config.h \
    $(AR_HOME)/include/AR/ar.h \
    $(AR_HOME)/include/AR/param.h \


OBJS1 = \
	argBase.o      \
	argWindow.o  \
	argFunction.o    \
	argDrawMode.o      \
	argDraw.o        \
	argDrawImage.o       \


OBJS3 = \
	gsub_lite.o      \
	gsub_mtx.o  \


# Implicit rule, to compile C++ files with the .cpp suffix (rule already exists for .cc).
%.o : %.cpp
	$(CXX) -c $(CPPFLAGS) $(CXXFLAGS) $< -o $@

default build all: $(TARGET1) $(TARGET3)

$(OBJS1): $(HEADERS1)

$(OBJS3): $(HEADERS3)

$(TARGET1): $(OBJS1)
	$(AR) $(ARFLAGS) $@ $^
	$(RANLIB) $@ 

./gsubTest:	gsubTest.o $(TARGET1)
	$(CC) -o ./gsubTest gsubTest.o $(LDFLAG) $(LIBS)

gsubTest.o:	gsubTest.c $(HEADERS1)
	$(CC) -c $(CFLAG) gsubTest.c

$(TARGET3): $(OBJS3)
	$(AR) $(ARFLAGS) $@ $^
	$(RANLIB) $@

clean:
	-rm -f *.o *~ *.bak
	-rm $(TARGET1)
	-rm ./gsubTest
	-rm $(TARGET3)

allclean:
	-rm -f *.o *~ *.bak
	-rm $(TARGET1)
	-rm ./gsubTest
	-rm $(TARGET3)
	-rm -f Makefile

distclean:
	rm -f *.o
	rm -f Makefile

