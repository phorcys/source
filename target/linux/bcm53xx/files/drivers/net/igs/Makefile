#
# Makefile for the Broadcom PROXYARP
#
# Copyright (C) 2012, Broadcom Corporation. All Rights Reserved.
# 
# Permission to use, copy, modify, and/or distribute this software for any
# purpose with or without fee is hereby granted, provided that the above
# copyright notice and this permission notice appear in all copies.
# 
# THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES
# WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF
# MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY
# SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES
# WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN ACTION
# OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF OR IN
# CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.
#
# $Id: Makefile,v 1.1 2009-10-27 01:27:44 $
#
EXTRA_CFLAGS+=-I$(srctree)/brcm/include -I$(srctree)/brcm/shared/bcmwifi/include -DBCMDRIVER -Dlinux
EXTRA_AFLAGS+=-I$(srctree)/brcm/include -I$(srctree)/brcm/shared/bcmwifi/include -DBCMDRIVER -Dlinux

obj-${CONFIG_IGS} := igs.o

ifeq ($(CONFIG_MIPS),y)
EMFOSRC := ../../../brcm/mipsel/igs/bin
EMFCSRC := ../../../brcm/mipsel/igs
else
EMFOSRC := ../../../brcm/arm/igs/bin
EMFCSRC := ../../../brcm/arm/igs
endif
IGSOBJ := $(IGSOSRC)/igsc.o $(IGSOSRC)/igsc_sdb.o $(IGSOSRC)/osl_linux.o $(IGSCSRC)/igs_linux.o
SYMOBJ := $(IGSOSRC)/igsc.o $(IGSOSRC)/igsc_sdb.o $(IGSOSRC)/osl_linux.o

# Search for sources under src/router/proxyarp
#ifneq ($(wildcard $(srctree)/$(IGSCSRC)/*.c),)
#  igs-objs := $(IGSOBJ) igs_ksyms.o
#  EXTRA_CFLAGS += -Werror
#else
igs-objs := $(IGSOSRC)/igs.o
#endif

PHONY += $(src)/igs_ksyms.c

quiet_cmd_ksyms = CALL    $<
      cmd_ksyms = $(CONFIG_SHELL) -e $< $(src)/$(SYMOBJ) > $@

$(src)/igs_ksyms.c: $(src)/igs_ksyms.sh $(src)/$(SYMOBJ) FORCE
	$(call cmd,ksyms)

clean-files += $(IGSCSRC)/*.o $(IGSCSRC)/.*.o.cmd 
#$(IGSOSRC)/*.o $(IGSOSRC)/.*.o.cmd
