DESTDIR ?=
PREFIX ?= /usr/local
BINDIR ?= $(PREFIX)/bin
MANDIR ?= $(PREFIX)/man

CROSS_COMPILE ?=
CC = $(CROSS_COMPILE)gcc

CFLAGS += -Wall -Wextra -Werror -Wfatal-errors
CFLAGS += -I ../include
CFLAGS += -fPIC
CFLAGS += -O2

LDFLAGS += -L ../src
LDFLAGS += -pie

VPATH = ../src:../include/tinyalsa

.PHONY: all
all: -ltinyalsa tinyplay tinycap tinymix tinypcminfo

tinyplay: tinyplay.o libtinyalsa.a -ldl

tinyplay.o: tinyplay.c pcm.h mixer.h asoundlib.h

tinycap: tinycap.o libtinyalsa.a -ldl

tinycap.o: tinycap.c pcm.h mixer.h asoundlib.h

tinymix: tinymix.o libtinyalsa.a -ldl

tinymix.o: tinymix.c pcm.h mixer.h asoundlib.h

tinypcminfo: tinypcminfo.o libtinyalsa.a -ldl

tinypcminfo.o: tinypcminfo.c pcm.h mixer.h asoundlib.h

.PHONY: clean
clean:
	$(RM) tinyplay tinyplay.o
	$(RM) tinycap tinycap.o
	$(RM) tinymix tinymix.o
	$(RM) tinypcminfo tinypcminfo.o

.PHONY: install
install: tinyplay tinycap tinymix tinypcminfo
	install -d $(DESTDIR)$(BINDIR)
	install tinyplay $(DESTDIR)$(BINDIR)/
	install tinycap $(DESTDIR)$(BINDIR)/
	install tinymix $(DESTDIR)$(BINDIR)/
	install tinypcminfo $(DESTDIR)$(BINDIR)/
	install -d $(DESTDIR)$(MANDIR)/man1
	install tinyplay.1 $(DESTDIR)$(MANDIR)/man1/
	install tinycap.1 $(DESTDIR)$(MANDIR)/man1/
	install tinymix.1 $(DESTDIR)$(MANDIR)/man1/
	install tinypcminfo.1 $(DESTDIR)$(MANDIR)/man1/

