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

obj-${CONFIG_EMF} := emf.o
ifeq ($(CONFIG_MIPS),y)
EMFOSRC := ../../../brcm/mipsel/emf/bin
EMFCSRC := ../../../brcm/mipsel/emf
else
EMFOSRC := ../../../brcm/arm/emf/bin
EMFCSRC := ../../../brcm/arm/emf
endif
EMFOBJ := $(EMFOSRC)/emfc.o $(EMFCSRC)/emf_linux.o
SYMOBJ := $(EMFOSRC)/emfc.o

# Search for sources under src/router/proxyarp
#ifneq ($(wildcard $(srctree)/$(EMFCSRC)/*.c),)
#  emf-objs := $(EMFOBJ) emf_ksyms.o
#  EXTRA_CFLAGS += -Werror
#else
emf-objs := $(EMFOSRC)/emf.o
#endif

PHONY += $(src)/emf_ksyms.c

quiet_cmd_ksyms = CALL    $<
      cmd_ksyms = $(CONFIG_SHELL) -e $< $(src)/$(SYMOBJ) > $@

$(src)/emf_ksyms.c: $(src)/emf_ksyms.sh $(src)/$(SYMOBJ) FORCE
	$(call cmd,ksyms)

clean-files += $(EMFCSRC)/*.o $(EMFCSRC)/.*.o.cmd 
#$(EMFOSRC)/*.o $(EMFOSRC)/.*.o.cmd
