PROGRAMS = dtmerge dtoverlay

all: $(PROGRAMS)

# CFLAGS+=-Wall -Wextra -Wmaybe-uninitialized -pedantic-errors -g
CFLAGS+=
LIBPATH = -L./lib -I .

LIBFTD_OBJS = dtoverlay.o lib/fdt.o lib/fdt_ro.o lib/fdt_wip.o lib/fdt_sw.o lib/fdt_rw.o lib/fdt_strerror.o lib/fdt_empty_tree.o

libftd: $(LIBFTD_OBJS)

dtmerge: libftd dtmerge.o
	$(CC) $(LIBPATH) $(CFLAGS) -o dtmerge dtmerge.o $(LIBFTD_OBJS)

dtoverlay: libftd dtoverlay_main.o utils.o
	$(CC) $(LIBPATH) $(CFLAGS) -o dtoverlay dtoverlay_main.o utils.o  $(LIBFTD_OBJS)

clean:
	rm -rf *.o dtmerge dtoverlay lib/*.o

