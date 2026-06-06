#
# Basic make settings
#

CC	= gcc
INSTALL	= /usr/bin/install -c
MKDIR_P	= /usr/bin/mkdir -p

INSTALL_DIR	= /usr/local/bin

CFLAGS	= -std=c99 -g -O2 -Wall -I$(GEN)
LDFLAGS	= -lwayland-client -lxkbcommon


#
# Generated file settings. Could be cleaner.
#

GEN	= ./gen
PROTO	= ./protocol

PROTOS	= $(PROTO)/river-layer-shell-v1.xml $(PROTO)/river-window-management-v1.xml $(PROTO)/river-xkb-bindings-v1.xml
PROTOC	= $(GEN)/river-layer-shell-v1.c $(GEN)/river-window-management-v1.c $(GEN)/river-xkb-bindings-v1.c
PROTOH	= $(GEN)/river-layer-shell-v1.h $(GEN)/river-window-management-v1.h $(GEN)/river-xkb-bindings-v1.h
PROTOO	= $(GEN)/river-layer-shell-v1.o $(GEN)/river-window-management-v1.o $(GEN)/river-xkb-bindings-v1.o


#
# "Manual" targets.
#

HFILES	= jrwm.h
CFILES	= jrwm.c manage.c bindings.c
OFILES	= jrwm.o manage.o bindings.o

jrwm	: $(OFILES) $(PROTOO)
	$(CC) -o jrwm $(LDFLAGS) -o jrwm $(OFILES) $(PROTOO)

clean	:
	rm -f jrwm $(OFILES) $(PROTOO) $(PROTOC) $(PROTOH)

install	: jrwm
	$(MKDIR_P) $(INSTALL_DIR)
	$(INSTALL) -s jrwm $(INSTALL_DIR)

# dependencies

jrwm.o		: jrwm.c jrwm.h $(PROTOH)
bindings.o	: bindings.c jrwm.h $(PROTOH)
manage.o	: manage.c jrwm.h $(PROTOH)


#
# Generated file recipes.  Should be made more portable.
#

$(GEN)/%.o	: $(GEN)/%.c $(GEN)/%.h

$(GEN)/%.c	: $(PROTO)/%.xml
	wayland-scanner private-code $< $@

$(GEN)/%.h	: $(PROTO)/%.xml
	wayland-scanner client-header $< $@
