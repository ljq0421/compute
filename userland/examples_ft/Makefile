#
# Makefile for the PF_RING FT examples
#

#
# PF_RING
#
PFRINGDIR  = ../lib
LIBPFRING  = ${PFRINGDIR}/libpfring.a

#
# PF_RING aware libpcap
#
O_FLAG     = -O2 -DHAVE_PF_RING
EXTRA_LIBS =
PCAPDIR    = ../libpcap
LIBPCAP    = ${PCAPDIR}/libpcap.a  ${EXTRA_LIBS}

#
# Search directories
#
PFRING_KERNEL=../../kernel
INCLUDE    = -I${PFRING_KERNEL} -I${PFRINGDIR} -I${PCAPDIR} -Ithird-party `../lib/pfring_config --include`

#
# C compiler and flags
#
#
# CROSS_COMPILE=arm-mv5sft-linux-gnueabi-
#
CC         = ${CROSS_COMPILE}gcc #--platform=native
CFLAGS     = -march=native -mtune=native  ${O_FLAG} -Wall ${INCLUDE} -D HAVE_PF_RING_FT -O2 # -g

#
# User and System libraries
#
LIBS       = ${LIBPCAP} ${LIBPFRING} ${LIBPCAP} ${LIBPFRING} `../lib/pfring_config --libs` `../libpcap/pcap-config --additional-libs --static` -lpthread  -lrt -ldl -lrt

#
# Object files
#
%.o: %.c ftutils.c
	${CC} ${CFLAGS} -c $< -o $@

#
# Main targets
#
ifneq (-D HAVE_PF_RING_FT,)
FTPROGS = ftflow ftflow_pcap fttest
ifneq (,)
LIBS   += /usr/local/lib/libhs.a
CFLAGS += -I/usr/local/include/hs/
endif
endif

TARGETS = ${FTPROGS}

all: ${TARGETS}

ftflow: ftflow.o ${LIBPFRING}
	${CC} ${CFLAGS} ftflow.o ${LIBS} -o $@

ftflow_pcap: ftflow_pcap.o ${LIBPFRING}
	${CC} ${CFLAGS} ftflow_pcap.o ${LIBS} -o $@

fttest: fttest.o ${LIBPFRING}
	${CC} ${CFLAGS} fttest.o ${LIBS} -o $@

install: ${TARGETS}
	mkdir -p $(DESTDIR)/usr/bin
	cp $(TARGETS) $(DESTDIR)/usr/bin/

clean:
	@rm -f ${TARGETS} *.o *~
