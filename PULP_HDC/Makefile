ifdef FABRIC
PULP_APP = main
PULP_APP_FC_SRCS  = src/main.c src/associative_memory.c src/aux_functions.c
PULP_ARCH_LDFLAGS = -march=rv32imcxpulpslim -DRV_ISA_RV32=1 -D__riscv__
else
PULP_OMP_APP = main
PULP_APP_OMP_SRCS = src/main.c src/associative_memory.c src/aux_functions.c
#stackSize ?= 5120
endif

CORES ?= 1

ifeq (${OPT}, 0)
PULP_CL_ARCH_CFLAGS = -march=rv32imfc -D__riscv__
PULP_ARCH_LDFLAGS = -march=rv32imfc -D__riscv__
CORES = 1
endif

ifeq (${OPT}, 1)
CORES = 1
endif

ifeq (${OPT}, 2)
CORES = 1
PULP_CFLAGS += -DUSE_INTRINSICS
endif

ifndef FABRIC
ifndef  OPT
PULP_CFLAGS += -DUSE_INTRINSICS
endif
endif

PULP_CFLAGS += -DCORE=$(CORES) -O3 -g3 -Iinc  -DHWPERF
PULP_LDFLAGS = -lm


ifdef FABRIC
#error
include $(PULP_SDK_HOME)/install/rules/pulp_rt.mk
else
include $(PULP_SDK_HOME)/install/rules/pulp.mk
endif
