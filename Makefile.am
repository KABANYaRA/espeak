PREFIX=/usr
BINDIR=$(PREFIX)/bin
INCDIR=$(PREFIX)/include/espeak
LIBDIR=$(PREFIX)/lib
DATADIR=$(PREFIX)/share/espeak-data

.PHONY: all clean distclean

EXTRA_DIST=

##### ChangeLog:

ChangeLog:
	git log > ChangeLog

dist-hook: ChangeLog

.PHONY: ChangeLog

EXTRA_DIST += ChangeLog

##### standard build actions:

all: src/libespeak.so src/libespeak.a docs/speak_lib.h

install: all
	cd src && make DESTDIR=$(DESTDIR) PREFIX=$(PREFIX) BINDIR=$(BINDIR) INCDIR=$(INCDIR) LIBDIR=$(LIBDIR) install && cd ..
	install -m 755 src/espeakedit $(DESTDIR)$(BINDIR)

clean:
	cd src && rm -f *.o *~ && cd ..

distclean: clean
	cd src && rm -f libespeak.a libespeak.so.* && cd ..

##### build targets:

common_SOURCE = \
	src/compiledict.cpp \
	src/dictionary.cpp \
	src/intonation.cpp \
	src/klatt.cpp \
	src/mbrowrap.cpp \
	src/numbers.cpp \
	src/readclause.cpp \
	src/phonemelist.cpp \
	src/setlengths.cpp \
	src/sonic.cpp \
	src/synthdata.cpp \
	src/synthesize.cpp \
	src/synth_mbrola.cpp \
	src/translate.cpp \
	src/tr_languages.cpp \
	src/voices.cpp \
	src/wavegen.cpp 

libespeak_SOURCE = \
	src/speak_lib.cpp

docs/speak_lib.h: src/speak_lib.h
	cp $< $@

src/libespeak.a: $(common_SOURCE) $(libespeak_SOURCE)
	cd src && make libespeak.a PREFIX=$(PREFIX) && cd ..

src/libespeak.so: $(common_SOURCE) $(libespeak_SOURCE)
	cd src && make libespeak.so PREFIX=$(PREFIX) && cd ..
