CC=gcc
CFLAGS=-g -Wall -O2 -pthread -march=native -fcommon

BWADIR=bwa
HTSDIR=htslib
INCLUDES=-I$(HTSDIR) -I$(BWADIR)
LFLAGS=-L$(HTSDIR) -L$(BWADIR)
LIBS=$(HTSDIR)/libhts.a $(BWADIR)/libbwa.a
#LDLIBS=-lm -lz -lpthread # older version of htslib, 1.3
#LDLIBS=-lm -lz -llzma -lbz2 -lpthread # older version of htslib, 1.6
LDLIBS=-lm -lz -llzma -lbz2 -lpthread -lcurl

PREFIX = /usr/local
MAIN = eagle
AUX = vector.o util.o calc.o heap.o

all: UTIL HTSLIB BWA
	$(CC) $(CFLAGS) $(LFLAGS) $(INCLUDES) $(MAIN).c -o $(MAIN) $(AUX) $(LIBS) $(LDLIBS)
	$(CC) $(CFLAGS) $(LFLAGS) $(INCLUDES) eagle-rc.c -o eagle-rc $(AUX) $(LIBS) $(LDLIBS)
	$(CC) $(CFLAGS) $(LFLAGS) $(INCLUDES) eagle-nm.c -o eagle-nm $(AUX) $(LIBS) $(LDLIBS)

eagle: UTIL HTSLIB BWA
	$(CC) $(CFLAGS) $(LFLAGS) $(INCLUDES) $(MAIN).c -o $(MAIN) $(AUX) $(LIBS) $(LDLIBS)
eagle-rc: UTIL HTSLIB
	$(CC) $(CFLAGS) $(LFLAGS) $(INCLUDES) eagle-rc.c -o eagle-rc $(AUX) $(LIBS) $(LDLIBS)
eagle-nm: UTIL HTSLIB
	$(CC) $(CFLAGS) $(LFLAGS) $(INCLUDES) eagle-nm.c -o eagle-nm $(AUX) $(LIBS) $(LDLIBS)

HTSLIB:
	$(MAKE) -C $(HTSDIR)/
BWA:
	$(MAKE) -C $(BWADIR)/
UTIL:
	$(CC) $(CFLAGS) $(LFLAGS) $(INCLUDES) -c vector.c util.c calc.c heap.c $(LDLIBS)

install: eagle eagle-rc
	install -p $^ $(PREFIX)/bin

clean:
	rm -f eagle eagle-rc eagle-nm *.o

# DO NOT DELETE THIS LINE -- make depend needs it
