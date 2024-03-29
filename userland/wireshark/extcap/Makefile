#
# Makefile for the WIreshark Extcap Modules
#
# Try to make both programs written on top of the
# PF_RING library and programs originally written
# on top of PCAP library and linked now to use
# the version with PF_RING aware functionalities.
#



#
# PF_RING
#
PFRINGDIR  = ../../lib
LIBPFRING  = ${PFRINGDIR}/libpfring.a

#
# PF_RING aware libpcap
#
O_FLAG     = -O2 -DHAVE_PF_RING
EXTRA_LIBS =
PCAPDIR    = ../../libpcap
LIBPCAP    = ${PCAPDIR}/libpcap.a  ${EXTRA_LIBS}

#
# Search directories
#
PFRING_KERNEL=../../../kernel
INCLUDE    = -I${PFRING_KERNEL} -I${PFRINGDIR} -I${PCAPDIR} -Ithird-party `../../lib/pfring_config --include`

#
# C compiler and flags
#
#
# CROSS_COMPILE=arm-mv5sft-linux-gnueabi-
#
CC         = ${CROSS_COMPILE}gcc #--platform=native
CFLAGS     = -march=native -mtune=native  ${O_FLAG} -Wall ${INCLUDE} -D ENABLE_BPF -D HAVE_PF_RING_ZC -O2 # -g
# LDFLAGS  =

#
# User and System libraries
#
LIBS       = ${LIBPCAP} ${LIBPFRING} ${LIBPCAP} ${LIBPFRING} `../../lib/pfring_config --libs` -lpthread  -lrt -ldl  -lrt

# How to make an object file
%.o: %.c
#	@echo "=*= making object $@ =*="
	${CC} ${CFLAGS} -c $< -o $@

#
# Main targets
#

TARGETS   = ntopdump

RCOBJS    = ntopdump.o

all: ${TARGETS}

ntopdump: ${RCOBJS} ${LIBPFRING}
	${CC} ${CFLAGS} ${RCOBJS} ${LIBS} -o $@

clean:
	@rm -f ${TARGETS} *.o *~
