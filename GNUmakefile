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


#
# "Manual" targets.
#

jrwm	: jrwm.c $(PROTOC) $(PROTOH)
	$(CC) $(CFLAGS) $(LDFLAGS) -o jrwm jrwm.c $(PROTOC)

clean	:
	rm -f jrwm jrwm.o $(PROTOC) $(PROTOH)

install	: jrwm
	$(MKDIR_P) $(INSTALL_DIR)
	$(INSTALL) -s jrwm $(INSTALL_DIR)


#
# Generated file recipes.  Should be made more portable.
#

$(GEN)/%.c	: $(PROTO)/%.xml
	wayland-scanner private-code $< $@

$(GEN)/%.h	: $(PROTO)/%.xml
	wayland-scanner client-header $< $@
