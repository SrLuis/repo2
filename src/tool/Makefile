
COMMON_OBJ = ../common/obj_all/minicore.o ../common/obj_all/malloc.o \
	../common/obj_all/showmsg.o ../common/obj_all/strlib.o \
	../common/obj_all/utils.o ../common/obj_all/des.o ../common/obj_all/grfio.o
COMMON_H = ../common/core.h ../common/mmo.h \
	../common/malloc.h ../common/showmsg.h ../common/strlib.h \
	../common/utils.h ../common/cbasetypes.h ../common/des.h ../common/grfio.h ../config/renewal.h

LIBCONFIG_OBJ = ../../3rdparty/libconfig/libconfig.o ../../3rdparty/libconfig/grammar.o \
	../../3rdparty/libconfig/scanctx.o ../../3rdparty/libconfig/scanner.o ../../3rdparty/libconfig/strbuf.o
LIBCONFIG_H = ../../3rdparty/libconfig/libconfig.h ../../3rdparty/libconfig/grammar.h \
	../../3rdparty/libconfig/parsectx.h ../../3rdparty/libconfig/scanctx.h ../../3rdparty/libconfig/scanner.h \
	../../3rdparty/libconfig/strbuf.h ../../3rdparty/libconfig/wincompat.h
LIBCONFIG_INCLUDE = -I../../3rdparty/libconfig

OTHER_H = ../config/renewal.h

MAPCACHE_OBJ = obj_all/mapcache.o



#####################################################################
.PHONY : all mapcache clean help

all: mapcache

mapcache: obj_all $(MAPCACHE_OBJ) $(COMMON_OBJ) $(LIBCONFIG_OBJ)
	@echo "	LD	$@"
	@gcc  -march=i686 -L/usr/lib -lpthread $(LIBCONFIG_INCLUDE) -o ../../mapcache $(MAPCACHE_OBJ) $(COMMON_OBJ) $(LIBCONFIG_OBJ) -lpcre -lpthread -lpthread -lpthread -lpthread -lpthread -lpthread -lpthread -lrt -lm -lz  -ldl

clean:
	@echo "	CLEAN	tool"
	@rm -rf obj_all/*.o ../../mapcache

help:
	@echo "possible targets are 'mapcache' 'all' 'clean' 'help'"
	@echo "'mapcache'  - mapcache generator"
	@echo "'all'       - builds all above targets"
	@echo "'clean'     - cleans builds and objects"
	@echo "'help'      - outputs this message"

#####################################################################

obj_all:
	-mkdir obj_all

obj_all/%.o: %.c $(COMMON_H) $(OTHER_H) $(LIBCONFIG_H)
	@echo "	CC	$<"
	@gcc -g -O2 -DMAXCONN=16384 -pipe -ffast-math -Wall -march=i686 -DHAS_TLS -Wno-switch -fno-strict-aliasing -DHAVE_SETRLIMIT -DHAVE_STRNLEN  -Wno-pointer-sign -DHAVE_MONOTONIC_CLOCK $(LIBCONFIG_INCLUDE)  -I../common -I/usr/include -c $(OUTPUT_OPTION) $<

# missing common object files
../common/obj_all/%.o:
	@$(MAKE) -C ../common txt

../common/obj_all/mini%.o:
	@$(MAKE) -C ../common txt

LIBCONFIG_OBJ:
	@$(MAKE) -C ../../3rdparty/libconfig
