#
# Copyright 2018 Ettus Research, a National Instruments Company
#

.PHONY: all clean

SRCS=rhodium_top.qpf rhodium_top.qsf rhodium_top.sdc rhodium_top.v rhodium_gain_ctrl.v rhodium_gain_table.v rhodium_lo_gain.v
SIM_SRCS=rh_tb.v rhodium_top.v rhodium_gain_ctrl.v rhodium_gain_table.v rhodium_lo_gain.v
SHORT_HASH=$(addprefix GIT_HASH=,$(shell ../../../../../tools/scripts/git-hash.sh))

output_files/rhodium_top_pof.svf: $(SRCS)
	quartus_map rhodium_top --verilog_macro="$(SHORT_HASH)"
	quartus_fit rhodium_top
	quartus_asm rhodium_top
	quartus_sta rhodium_top

all: output_files/rhodium_top_pof.svf

clean:
	rm -rf db incremental_db output_files simulation

a.out: $(SIM_SRCS)
	iverilog -tvvp -D$(SHORT_HASH) -s rh_tb $(SIM_SRCS)

