# WARNING: do not run this directly, it should be run by the master Makefile

include ../../Makefile.defs
auto_gen =
NAME = aaa_diameter.so

# ===== 追加: 外部 freeDiameter を pkg-config で検出 =====
FDCORE_CFLAGS  := $(shell pkg-config --cflags libfdcore 2>/dev/null)
FDCORE_LIBS    := $(shell pkg-config --libs libfdcore 2>/dev/null)
FDPROTO_CFLAGS := $(shell pkg-config --cflags libfdproto 2>/dev/null)
FDPROTO_LIBS   := $(shell pkg-config --libs libfdproto 2>/dev/null)

# pkg-config が使えた場合は外部版を利用
ifneq ($(strip $(FDCORE_LIBS)),)
    DEFS += $(FDCORE_CFLAGS) $(FDPROTO_CFLAGS)
    LIBS += $(FDCORE_LIBS) $(FDPROTO_LIBS)
else
    # pkg-config が見つからない場合は従来のリンク方法（内部版）
    LIBS += -lfdproto -lfdcore
endif

extra_sources = app_opensips/avps.c

include ../../Makefile.modules
