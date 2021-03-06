#
# Makefile:
#	The gpio command:
#	  A swiss-army knige of GPIO shenanigans.
#	https://projects.drogon.net/wiring-pi
#
#	Copyright (c) 2012-2013 Gordon Henderson
#################################################################################
# This file is part of wiringPi:
#	Wiring Compatable library for the Raspberry Pi
#
#    wiringPi is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Lesser General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    wiringPi is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Lesser General Public License for more details.
#
#    You should have received a copy of the GNU Lesser General Public License
#    along with wiringPi.  If not, see <http://www.gnu.org/licenses/>.
#################################################################################

DESTDIR=/usr
PREFIX=/local

#DEBUG	= -g -O0
DEBUG	= -O2
CC	= gcc
INCLUDE	= -I$(DESTDIR)$(PREFIX)/include
CFLAGS	= $(DEBUG) -Wall $(INCLUDE) -Winline -pipe

LDFLAGS	= -L$(DESTDIR)$(PREFIX)/lib
LIBS    = -lwiringPi -lwiringPiDev -lpthread -lm

# May not need to  alter anything below this line
###############################################################################

SRC	=	gpio.c extensions.c readall.c pins.c

OBJ	=	$(SRC:.c=.o)

all:		gpio

gpio:	$(OBJ)
	@echo [Link]
	@$(CC) -o $@ $(OBJ) $(LDFLAGS) $(LIBS)
	
.c.o:
	@echo [Compile] $<
	@$(CC) -c $(CFLAGS) $< -o $@

.PHONY:	clean
clean:
	@echo "[Clean]"
	@rm -f $(OBJ) gpio *~ core tags *.bak gpio.1.gz

.PHONY:	tags
tags:	$(SRC)
	@echo [ctags]
	@ctags $(SRC)

.PHONY:	install
install:
	@echo "[Install]"
	install -d -m 755       $(DESTDIR)$(PREFIX)/bin
	install -d -m 755       $(DESTDIR)$(PREFIX)/lib
	install -d -m 755       $(DESTDIR)$(PREFIX)/include
	install -d -m 755       $(DESTDIR)$(PREFIX)/share/man/man1
	install -m 4755 gpio    $(DESTDIR)$(PREFIX)/bin
	cat gpio.1 |gzip >gpio.1.gz
	install gpio.1.gz       $(DESTDIR)$(PREFIX)/share/man/man1

# TODO do we need this for the final install?
#	@chown root.root	$(DESTDIR)$(PREFIX)/bin/gpio

.PHONY:	uninstall
uninstall:
	@echo "[UnInstall]"
	@rm -f $(DESTDIR)$(PREFIX)/bin/gpio
	@rm -f $(DESTDIR)$(PREFIX)/share/man/man1/gpio.1
	@rm -f $(DESTDIR)$(PREFIX)/share/man/man1/gpio.1.gz

.PHONY:	depend
depend:
	makedepend -Y $(SRC)

# DO NOT DELETE

gpio.o: extensions.h
extensions.o: extensions.h
